# Backend

Documentação da área Backend do projeto Mash.

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
- **Sem migrations:** Models sincronizados via `.sync({force: false})` no startup

## Arquitetura da migração (Back-End — código real)

- **Padrão:** Rota → Controller → Service → Model → Sequelize → MySQL
- **Autenticação:** JWT no header Authorization (Bearer), `req.userId`, Argon2id, `JWT_SECRET_KEY`
- **Hash:** Argon2id (memoryCost 2^16, timeCost 3, parallelism 1)
- **Upload:** Multer memoryStorage → Cloudinary
- **Credenciais:** Via `.env` (dotenv) — `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET_KEY`, `CLOUD_NAME`, `API_KEY_CLOUDINARY`, `API_SECRET_KEY_CLOUDINARY`
- **Database:** `mash` (⚠️ diferente de `cervejaria` do mash original)
- **Tabela usuário:** `users` (name, email, fone, password, url_image) — ⚠️ diferente de `usuarios` do mash
- **Foreign key:** `user_id` (⚠️ diferente de `usuario_id` do mash)

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

## Bugs encontrados (Back-End — código real)

| Bug | Local | Descrição |
|---|---|---|
| ReferenceError | `recipeController.js` → `showRecipe` | `if(!id)` usado ANTES de `const id = req.userId` |
| Service incompleto | `recipeService.js` → `createRecipe` | Método vazio (só chaves) |
| Sem CRUD completo | `recipeRoutes.js` | Só GET /receitas — sem PUT/DELETE/:id |
| Sem validação de senha atual | `userService.js` → `updateUser` | Permite trocar senha sem verificar a atual |

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

| Issue | Título | Prioridade |
|---|---|---|
| #30 | Migrar gradualmente para a API REST | Urgent |
| #31 | Implementar CRUD de lotes | Urgent |
| #32 | Corrigir CRUD de receitas | Urgent |
| #33 | Implementar upload da imagem do teste de iodo | High |
| #34 | Implementar análise do teste de iodo com OpenCV | Low |
| #36 | Definir contrato de configurações de temperatura e teste de iodo | Urgent |
| #38 | Corrigir autenticação e autorização | — |
| #39 | Proteger segredos | — |
| #40 | Definir migrations Sequelize | — |
| #41 | Criar testes e padrão HTTP | — |

## Pontos de atenção

1. **Credenciais hardcoded** em `config/sequelize-config.js` e `config/session.js`
2. **Sem `.env`** — não há dotenv no projeto
3. **Sem testes** — `npm test` retorna erro
4. **Sem migrations** — usa `.sync()` no startup
5. **Middleware inconsistente** — algumas rotas POST não têm `isLogado`
6. **Geolocalização externa** — `loginController.js` chama `ip-api.com` no login
