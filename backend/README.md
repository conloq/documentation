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
- **Credenciais:** Via `.env` (dotenv) — `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET_KEY`, `CLOUD_NAME`, `API_KEY_CLOUDINARY`, `API_SECRET_KEY_CLOUDINARY`, `FRONTEND_URL` (CORS para o frontend)
- **Database:** `mash` (⚠️ diferente de `cervejaria` do mash original)
- **Tabela usuário:** hoje `Users` (name, email, fone, password, url_image); a #71 a normaliza para `users` (`name`, `email`, `phone`, `password`, `urlImage`) — diferente de `usuarios` do mash
- **Foreign key:** `userId` e `recipeId` depois da #71 (hoje `user_id`; diferente de `usuario_id` do mash)
- **Banco (decisão de 12/10/2026):** o schema vem das **migrations do Sequelize**; `npm run db:migrate` roda antes de `npm start` e a cada deploy. A #71 tira o `Connection.sync()` do `app.js`. A #40 continua fechada.
- **Nomes (decisão de 13/10/2026, #30):** JSON e banco no **mesmo camelCase** em inglês (`userId`, `recipeId`, `urlImage`, `collectedAt`, `createdAt`), sem `underscored` e sem código de tradução. Rotas em inglês. Colunas em português mudam para inglês (`nome`→`name`, `fone`→`phone`) e a tabela `receitas` vira `recipes`. Substitui a regra de 08/10 (snake_case com `underscored: true`) e a de 28/09.
- **Deploy (decisão de 13/10/2026, #61):** Render gratuito com MySQL externo (Aiven); `GET /health` pela #68.

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
| POST | `/receitas/temperatura/:recipe_id` | authMiddleware | Rampas de temperatura da receita. Faz parte do depósito desde 09/10 e passa a `POST /recipes/:id/temperatures`, com campos em camelCase (#32). Temperatura por sensor, gráficos e alertas ficam para depois do depósito |
| GET | `/api-docs` | — | Documentação Swagger |
| GET | `/recipes/:id` | — | **Não existe no código** — pendência da #32 |

> Nota de migração: o contrato vigente (#30/#32) define `/recipes` (inglês). O código ainda usa `/receitas` — a correção é da #32 e quebra o frontend, que acompanha na #86.

## Pendências da #32 (conferidas em `7e66b98`, 13/10/2026)

O contrato e a lista completa do que falta estão na [#32](https://github.com/conloq/mash/issues/32); alterar e excluir receita foram para a [#93](https://github.com/conloq/mash/issues/93). Já estão no código: o 409 de duplicidade no cadastro e o `res.sendStatus(204)` na exclusão. Faltam, entre outros: a rota de detalhe, as rotas em `/recipes`, o 404 único para receita alheia ou inexistente e a rampa em `/recipes/:id/temperatures`.

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

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#30](https://github.com/conloq/mash/issues/30) (base da API: padrões, schema e evidências), [#83](https://github.com/conloq/mash/issues/83) (conta e segurança), [#80](https://github.com/conloq/mash/issues/80) (receitas e rampas), [#81](https://github.com/conloq/mash/issues/81) (lotes), [#82](https://github.com/conloq/mash/issues/82) (teste de iodo) e [#61](https://github.com/conloq/mash/issues/61) (deploy). OpenCV ([#34](https://github.com/conloq/mash/issues/34)) e temperatura por dispositivo ([#36](https://github.com/conloq/mash/issues/36)) ficam para o próximo semestre.

## Pontos de atenção

1. **Credenciais hardcoded** em `config/sequelize-config.js` e `config/session.js` (mash) — #39
2. **`.env.example` inexistente** no Back-End; boot não valida env obrigatória — #39
3. **Sem testes automatizados, por decisão:** a validação é manual e fica registrada na #41
4. **`Connection.sync()` ainda no `app.js`** até a #71; o schema vem das migrations (12/10/2026), então rode `npm run db:migrate` antes de subir a API
5. **Middleware inconsistente** — algumas rotas POST do mash não têm `isLogado`
6. **Geolocalização externa** — `loginController.js` chama `ip-api.com` no login
7. **Branch protection do Back-End:** o repositório é público e a `main` está protegida: Pull Request com 1 aprovação; João e Haimon fazem o merge, e o João está dispensado da aprovação (#35)
