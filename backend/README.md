# Backend

Documentação da área Backend do projeto Mash.

> Conferido em 21/10/2026 contra Back-End `7f33203d06bd796c7840f13f1a445d082dbd7457` e os metadados do banco local. [Evidências do schema](../database/evidencias/README.md). O contrato vigente está nas issues e na #66.

## Repositórios

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/mash`](https://github.com/conloq/mash) | Aplicação original full-stack (Express + EJS + MySQL, session auth) | Funcional |
| [`conloq/Back-End`](https://github.com/conloq/Back-End) | API REST (migração em andamento, JWT + Argon2id) | Em migração (#30): código real mapeado |

## Arquitetura atual (mash)

- **Padrão:** Server-rendered MVC (sem API REST)
- **Fluxo:** Rota → Middleware (isLogado) → Controller → Model (Sequelize) → MySQL → Render EJS
- **Autenticação:** express-session (cookie `connect.sid`, 7 dias) + SequelizeStore (MySQL)
- **Identidade:** `req.session.userId`
- **Porta:** 8080
- **Legado:** o monólito tem seu próprio schema e uso de sync. Isso não define a estratégia da API; no Back-End a fonte são migrations.

## Arquitetura da migração (Back-End: código real)

- **Padrão:** Rota → Controller → Service → Model → Sequelize → MySQL
- **Autenticação:** JWT no header Authorization (Bearer), `req.userId`, Argon2id, `JWT_SECRET_KEY`
- **Hash:** Argon2id (memoryCost 2^16, timeCost 3, parallelism 1)
- **Upload:** Multer memoryStorage → Cloudinary
- **Credenciais:** Via `.env` (dotenv): `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET_KEY`, `CLOUD_NAME`, `API_KEY_CLOUDINARY`, `API_SECRET_KEY_CLOUDINARY`, `FRONTEND_URL` (CORS para o frontend)
- **Database:** `mash` (⚠️ diferente de `cervejaria` do mash original)
- **Tabelas da API:** `users`, `recipes`, `temperatures`; atributos camelCase e colunas snake_case. `SequelizeMeta` registra as três migrations aplicadas.
- **Foreign key:** coluna `user_id` e `recipe_id` (atributo `userId` e `recipeId` no model e no JSON); diferente de `usuario_id` do mash
- **Banco (decisão de 12/10/2026):** o schema vem das **migrations do Sequelize**; `npm run db:migrate` roda antes de `npm start` e a cada deploy. O bootstrap atual não chama `Connection.sync()`; `prestart` executa as migrations. A #40 continua fechada.
- **Nomes (08/10/2026, reafirmada em 15/10/2026, #30):** JSON em camelCase em inglês (`userId`, `recipeId`, `urlImage`, `collectedAt`, `createdAt`); banco em **snake_case** nas tabelas e colunas (`user_id`, `recipe_id`, `url_image`, `created_at`). Os models declaram os atributos em camelCase e a conexão usa `define: { underscored: true }`, sem código de tradução. Rotas em inglês. Os nomes atuais já usam `name`, `phone` e a tabela `recipes`; os nomes em português pertencem ao legado. A regra de 13/10 (banco em camelCase) foi revertida; a de 28/09 (snake_case no JSON) continua substituída.
- **Deploy (decisão de 13/10/2026, #61):** Render gratuito com MySQL externo (Aiven); `GET /health` pela #68.

## Padrão de resposta (decisão da equipe: base aula-05 DW3)

- Sucesso sem entidade: `{ "message": "..." }`; com entidade: `{ "message": "...", "<singular>": { ... } }`; listagem: `{ "<plural>": [ ... ] }`; detalhe: `{ "<singular>": { ... } }`
- **Sem wrapper genérico `data` em nenhuma rota.**
- Erro: `{ "error": "mensagem em pt-BR" }`, string direta, **sem código interno**
- DELETE: `204` sem corpo, com `res.sendStatus(204)`
- **Mensagens sempre em pt-BR**: o frontend exibe o texto da API sem traduzir

## Rotas e schema da API

Na main `7f33203`, receitas usam `/recipes` e `/recipes/:id`; o detalhe está conectado. Criar e listar rampas usa `/recipes/:id/temperatures`. Usuário/login continuam em `/user` e `/login`, com foto de perfil em `/user/upload`. Essas rotas têm documentação no Swagger versionado.

Lotes (#31/#92) e edição/exclusão de rampas (#97) são planejamento, não tabelas ou rotas observadas na main auditada. As regras de exclusão de receita com lotes pertencem à #93. A comprovação do banco local está em [database/evidencias](../database/evidencias/README.md).

OpenCV e todo o fluxo real do teste de iodo ficam no backlog para outro semestre. Neste semestre permanece somente a simulação no frontend, com cena obrigatória no pitch, sem etiqueta de simulação na cena ([decisão de 21/10/2026, #66](https://github.com/conloq/mash/issues/66)).

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

## Rotas HTTP (mash: server-rendered)

| Método | Rota | Middleware | Descrição |
|---|---|---|---|
| GET | `/` | isGuest | Login |
| POST | `/login` | - | Autenticar |
| GET | `/cadastro` | isGuest | Cadastro |
| POST | `/cadastrar` | - | Criar usuário |
| GET | `/usuario` | isLogado | Perfil |
| GET | `/usuario/sair` | - | Logout |
| POST | `/usuario/atualizar` | - | Atualizar perfil |
| GET | `/usuario/deletar` | - | Deletar usuário |
| POST | `/usuario/foto` | Multer | Upload foto |
| GET | `/receita` | isLogado, infoGlobal | Listar receitas |
| POST | `/receita/criar` | - | Criar receita |
| POST | `/receita/temperatura/criar` | - | Criar temperatura |
| POST | `/receita/temperatura/editar` | - | Editar temperatura |
| POST | `/receita/temperatura/definir-temperatura` | - | Ativar/desativar temperatura |
| POST | `/receita/deletar` | - | Deletar receita |
| GET/POST | `/receita/iodo/criar/:id` | isLogado, infoGlobal | Criar iodo |
| GET/POST | `/receita/iodo/editar/:id` | isLogado, infoGlobal | Editar iodo |

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#30](https://github.com/conloq/mash/issues/30) (base da API: padrões, schema e evidências), [#83](https://github.com/conloq/mash/issues/83) (conta e segurança), [#80](https://github.com/conloq/mash/issues/80) (receitas e rampas), [#81](https://github.com/conloq/mash/issues/81) (lotes), [#82](https://github.com/conloq/mash/issues/82) (teste de iodo) e [#61](https://github.com/conloq/mash/issues/61) (deploy). OpenCV ([#34](https://github.com/conloq/mash/issues/34)) e temperatura por dispositivo ([#36](https://github.com/conloq/mash/issues/36)) ficam para o próximo semestre.

## Pontos de atenção

- O schema de trabalho foi conferido por metadados, sem alterar dados. O ambiente publicado deve ser conferido separadamente.
- `package.json` executa migrations no `prestart`; `app.js` valida variáveis obrigatórias e não cria o schema por sync.
- O Back-End tem scripts de verificação em `scripts/`; o `npm test` continua sendo placeholder. Não declarar ausência total de verificações nem aprovação automática de todos os cenários.
- Cloudinary real e regras ainda pendentes de perfil ficam nas evidências e na #70; não foram exercitados nesta conferência de banco.
- O legado mantém suas próprias limitações; não usar seus modelos, SQL ou instruções de sync para inicializar a API.
- Fluxo de integração e permissões seguem a decisão vigente da [#66](https://github.com/conloq/mash/issues/66), sem copiar configurações antigas de proteção de branch.
