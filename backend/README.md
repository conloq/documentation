# Backend

Documentação da área Backend do projeto Mash.

> **Sincronizado em 07/10** com o código (`conloq/Back-End` @ `32a6dab`; o último commit de código é de 24/09) e com as decisões vigentes (#30, #66). O contrato de cada rota está na issue correspondente.

## Repositórios

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/mash`](https://github.com/conloq/mash) | Aplicação original full-stack (Express + EJS + MySQL, session auth) | Funcional |
| [`conloq/Back-End`](https://github.com/conloq/Back-End) | API REST (migração em andamento, JWT + Argon2id) | Em migração (#30) — código real mapeado |

## Arquitetura atual (mash)

- **Padrão:** Server-rendered MVC (sem API REST)
- **Fluxo:** Rota → Middleware (isLogado) → Controller → Model (Sequelize) → MySQL → Render EJS
- **Autenticação:** express-session (cookie `connect.sid`, 7 dias) + SequelizeStore (MySQL)
- **Identidade:** `req.session.userId`
- **Porta:** 8080
- **Sem migrations no runtime:** #40 está fechada como not_planned; a estratégia vigente é `.sync({ force: false })` no startup.

## Arquitetura da migração (Back-End — código real)

- **Padrão:** Rota → Controller → Service → Model → Sequelize → MySQL
- **Autenticação:** JWT no header Authorization (Bearer), `req.userId`, Argon2id, `JWT_SECRET_KEY`
- **Hash:** Argon2id (memoryCost 2^16, timeCost 3, parallelism 1)
- **Upload:** Multer memoryStorage → Cloudinary
- **Credenciais:** Via `.env` (dotenv) — `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET_KEY`, `CLOUD_NAME`, `API_KEY_CLOUDINARY`, `API_SECRET_KEY_CLOUDINARY`
- **Database:** `mash` (⚠️ diferente de `cervejaria` do mash original)
- **Tabela usuário:** `Users` (name, email, fone, password, url_image) — ⚠️ diferente de `usuarios` do mash
- **Foreign key:** `user_id` (⚠️ diferente de `usuario_id` do mash)
- **Banco:** runtime vigente é `Connection.sync()` em `app.js`. A pasta `migrations/` existe (decisão 26/09), mas os arquivos atuais **não são executáveis** — não usar; trabalho de schema/migration tem issue própria.
- **Naming (08/10/2026, #30):** JSON em inglês camelCase (`userId`, `recipeId`, `collectedAt`), no corpo da requisição, nos campos de formulário e na resposta. Rotas, tabelas e colunas em inglês snake_case. Os models declaram os atributos em camelCase e a conexão do Sequelize usa `define: { underscored: true }`, que gera as colunas em snake_case sem código de tradução. Colunas em português mudam para inglês (`nome`→`name`, `fone`→`phone`) e a tabela `receitas` vira `recipes`. ⚠️ `Connection.sync()` não renomeia coluna nem tabela — a alteração recria as tabelas (#71). Substitui a regra de 28/09, que punha snake_case também no JSON.

## Padrão de resposta (decisão da equipe — base aula-05 DW3)

- Sucesso sem entidade: `{ "message": "..." }`; com entidade: `{ "message": "...", "<singular>": { ... } }`; listagem: `{ "<plural>": [ ... ] }`; detalhe: `{ "<singular>": { ... } }`
- **Sem wrapper genérico `data` em nenhuma rota.**
- Erro: `{ "error": "mensagem em pt-BR" }` — string direta, **sem código interno**
- DELETE: `204` sem corpo, com `res.sendStatus(204)`
- **Mensagens sempre em pt-BR** — o frontend exibe o texto da API sem traduzir

## Rotas HTTP (Back-End — código real)

| Método | Rota | Middleware | Descrição |
|---|---|---|---|
| POST | `/login` | — | Autenticar (retorna JWT token) |
| POST | `/user` | — | Criar usuário (201) |
| GET | `/user` | authMiddleware | Ver perfil (exclui password) |
| DELETE | `/user` | authMiddleware | Deletar usuário |
| PUT | `/user` | authMiddleware | Atualizar perfil |
| PUT | `/user/upload` | authMiddleware, Multer | Upload imagem → Cloudinary |
| GET | `/receitas` | authMiddleware | Listar receitas do usuário |
| POST | `/receitas` | authMiddleware | Criar receita (201) |
| PUT | `/receitas/:id` | authMiddleware | Atualizar receita |
| DELETE | `/receitas/:id` | authMiddleware | Deletar receita (⚠️ 204 sem encerrar no código atual) |
| POST | `/receitas/temperatura/:recipe_id` | authMiddleware | Config de temperatura por receita (⚠️ fora do padrão; a temperatura por lote ficará para o pós-depósito) |
| GET | `/api-docs` | — | Documentação Swagger |
| GET | `/recipes/:id` | — | **Não existe no código** — pendência da #32 |

> Nota de migração: o contrato vigente (#30/#32) define `/recipes` (inglês). O código ainda usa `/receitas` — a correção é breaking para o frontend (#58) e faz parte do hotfix da #32.

## Pendências da #32 (CRUD de receitas — Sprint 4, depois da #71)

1. **Rota `GET /recipes/:id` ausente** — só existem 4 rotas; falta o detalhe da receita.
2. **Rotas em inglês:** código usa `/receitas`; contrato define `/recipes` — breaking para o frontend (#58).
3. **409 ausente:** contrato prevê `409 { "error": "Receita já existe" }`; não há verificação de duplicata.
4. **204 sem encerrar na exclusão:** `res.status(204)` sem `send()` — corrigir para `res.sendStatus(204)`.
5. **404 único:** receita inexistente ou de outro usuário devolve o mesmo 404; hoje o código responde 400 e 403.
6. **Validação:** manual, registrada em comentário na #41. Testes automatizados estão fora do escopo.
7. **Contrato sem `description`:** a #32 não exige mais `description` (decisão 26/09).
8. **Duplicidade:** o mesmo usuário não pode ter duas receitas com o mesmo nome, sem diferenciar maiúsculas (decisão 07/10).

## Models Sequelize (mash)

```
Usuario (usuario)
  ├─ 1:N → Receita (receitas) [usuario_id]
  ├─ 1:N → LogConexao (Historico_Login) [usuario_id]

Receita (receitas)
  ├─ 1:N → Temperatura (temperaturas) [receita_id, CASCADE]
  └─ 1:N → Iodo (iodo) [receita_id, CASCADE]
```

| Model | Tabela | Campos |
|---|---|---|
| Usuario | `usuario` | nome, email, telefone, senha (bcrypt), url_imagem |
| Receita | `receitas` | nome, usuario_id |
| Temperatura | `temperaturas` | rampa_min, rampa_max, temp_max, temp_min, temporizador, inicializacao, tempo_ideal, temperatura_ativa, receita_id |
| Iodo | `iodo` | tempo_primeira_coleta, intervalo_testes, qtd_max_testes, receita_id |
| LogConexao | `Historico_Login` | endereco_ip, data_hora, localidade, status, usuario_id |

## Rotas HTTP (mash — server-rendered)

| Método | Rota | Middleware | Descrição |
|---|---|---|---|
| GET | `/` | isGuest | Login |
| POST | `/login` | — | Autenticar |
| GET | `/cadastro` | isGuest | Cadastro |
| POST | `/cadastrar` | — | Criar usuário |
| GET | `/usuario` | isLogado | Perfil |
| GET | `/usuario/sair` | — | Logout |
| POST | `/usuario/atualizar` | — | Atualizar perfil |
| GET | `/usuario/deletar` | — | Deletar usuário |
| POST | `/usuario/foto` | Multer | Upload foto |
| GET | `/receita` | isLogado, infoGlobal | Listar receitas |
| POST | `/receita/criar` | — | Criar receita |
| POST | `/receita/temperatura/criar` | — | Criar temperatura |
| POST | `/receita/temperatura/editar` | — | Editar temperatura |
| POST | `/receita/temperatura/definir-temperatura` | — | Ativar/desativar temperatura |
| POST | `/receita/deletar` | — | Deletar receita |
| GET/POST | `/receita/iodo/criar/:id` | isLogado, infoGlobal | Criar iodo |
| GET/POST | `/receita/iodo/editar/:id` | isLogado, infoGlobal | Editar iodo |

## Issues ativas (Backend)

| Issue | Título | Prioridade | Estado (07/10) |
|---|---|---|---|
| #30 | Migrar gradualmente para a API REST | Urgent | In progress |
| #71 | Normalizar nomes de tabela e reconciliar o schema | High | Ready (S4, João) |
| #31 | Implementar CRUD de lotes | High | Backlog (S5, João); aguarda #71 e #32 |
| #32 | Corrigir CRUD de receitas | High | Backlog (S4, João); aguarda #71 |
| #1 | Criar entidade e consulta de análise de iodo | High | Backlog (S5, Haimon); aguarda #31 |
| #33 | Implementar upload da imagem do teste de iodo | Medium | Backlog (S5, Haimon); aguarda #1 e #31 |
| #3 | Histórico de análises por lote | Medium | Backlog (S5, João); primeira a sair se o prazo apertar |
| #34 | Implementar análise do teste de iodo com OpenCV | Low | Backlog, fora do depósito |
| #36 | Contrato de iodo e temperatura futura | High | Backlog; temperatura fica pós-depósito |
| #38 | Corrigir autenticação e autorização | High | Ready (S5, João); traz o contrato do login |
| #39 | Proteger segredos | High | Ready (S5, João); entrega o `.env.example` usado no deploy |
| #41 | Validar contrato HTTP e registrar evidências | High | Ready (S5, Haimon); validação manual |
| #60 | Aprovar contrato de análise de iodo pelo frontend | High | Backlog (S5, Haimon); não bloqueia o backend |
| #70 | Publicar contrato do CRUD de usuário | High | Ready (S5, João) |
| #68 | Publicar API e MySQL | Medium | Backlog (S5, João); Railway |

> **#40 (migrations) permanece FECHADA como not_planned.** Em 26/09 o time decidiu manter os arquivos existentes em `migrations/`, mas sem executá-los; o runtime vigente é `Connection.sync()` e qualquer nova migration exige issue própria.

## Pontos de atenção

1. **Credenciais hardcoded** em `config/sequelize-config.js` e `config/session.js` (mash) — #39
2. **`.env.example` inexistente** em Back-End e mash; boot não valida env obrigatória — #39
3. **Sem testes automatizados, por decisão:** a validação é manual e fica registrada na #41
4. **Migrations presentes mas inutilizáveis** (`migrations/` do Back-End); runtime vigente é `Connection.sync()`
5. **Middleware inconsistente** — algumas rotas POST do mash não têm `isLogado`
6. **Geolocalização externa** — `loginController.js` chama `ip-api.com` no login
7. **Branch protection do Back-End:** o repositório é público e a `main` está protegida: Pull Request com 1 aprovação; João e Haimon fazem o merge, e o João está dispensado da aprovação (#35)
