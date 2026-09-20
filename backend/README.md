# Backend

Documentação da área Backend do projeto Mash.

> **Sincronizado em 20/09** com o estado real do código (commits 159c1ce→2981318) e as decisões vigentes (#30, #32, #66).

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
- **Sem migrations:** por decisão (#40 not_planned) — Models sincronizados via `.sync({force: false})` no startup

## Arquitetura da migração (Back-End — código real)

- **Padrão:** Rota → Controller → Service → Model → Sequelize → MySQL
- **Autenticação:** JWT no header Authorization (Bearer), `req.userId`, Argon2id, `JWT_SECRET_KEY`
- **Hash:** Argon2id (memoryCost 2^16, timeCost 3, parallelism 1)
- **Upload:** Multer memoryStorage → Cloudinary
- **Credenciais:** Via `.env` (dotenv) — `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_DATABASE`, `JWT_SECRET_KEY`, `CLOUD_NAME`, `API_KEY_CLOUDINARY`, `API_SECRET_KEY_CLOUDINARY`
- **Database:** `mash` (⚠️ diferente de `cervejaria` do mash original)
- **Tabela usuário:** `users` (name, email, fone, password, url_image) — ⚠️ diferente de `usuarios` do mash
- **Foreign key:** `user_id` (⚠️ diferente de `usuario_id` do mash)

## Padrão de resposta (decisão da equipe — base aula-05 DW3)

- Sucesso: `{ "message": "..." }` (com `"data"` quando houver dados)
- Erro: `{ "error": "mensagem em pt-BR" }` — string direta, **sem código interno**
- DELETE: `204` sem corpo
- **Mensagens sempre em pt-BR** — o frontend exibe o texto da API sem traduzir
- Implementado e verificado nos commits 922e6eb ("Mensagens em pt-br") e 2981318 ("Trocando messages por error")

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
| DELETE | `/receitas/:id` | authMiddleware | Deletar receita (204) |
| GET | `/api-docs` | — | Documentação Swagger |

## Pendências da revisão da #32 (CRUD receitas — In review)

1. **Rotas em inglês:** código usa `/receitas`; contrato da #30 define `/recipes` — ⚠️ breaking change para o frontend (#58)
2. **409 ausente:** contrato prevê `409 { "error": "Receita já existe" }`; não há verificação de duplicata
3. **Testes:** escopo da #41 (`npm test` ainda sem suíte)

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

| Issue | Título | Prioridade | Status (19/09) |
|---|---|---|---|
| #30 | Migrar gradualmente para a API REST | Urgent | In progress |
| #31 | Implementar CRUD de lotes | Urgent | Ready (S4) |
| #32 | Corrigir CRUD de receitas | Urgent | In review (S3) |
| #33 | Implementar upload da imagem do teste de iodo | High | Backlog (S4) |
| #34 | Implementar análise do teste de iodo com OpenCV | Low | Backlog (S4, Could) |
| #36 | Definir contrato de configurações de temperatura e teste de iodo | Urgent | Backlog (S6) |
| #38 | Corrigir autenticação e autorização | Urgent | Ready (S4) |
| #39 | Proteger segredos | High | In review (fechamento contestado — 3 checkboxes abertos) |
| #41 | Criar testes e padrão HTTP | Urgent | Ready (S4) |
| #60 | Documentar contrato de temperatura e teste de iodo (desbloqueador) | Urgent | Ready (S3) |

> **#40 (migrations) foi FECHADA como not_planned** — não haverá migrations; `Model.sync()` é a estratégia definitiva. Não listá-la como ativa.

## Pontos de atenção

1. **Credenciais hardcoded** em `config/sequelize-config.js` e `config/session.js` (mash) — #39
2. **`.env.example` inexistente** em Back-End e mash; boot não valida env obrigatória — #39 (fechamento em revisão)
3. **Sem testes** — `npm test` retorna erro — #41
4. **Sem migrations** — por decisão (#40 not_planned), `.sync()` no startup é vigente
5. **Middleware inconsistente** — algumas rotas POST não têm `isLogado`
6. **Geolocalização externa** — `loginController.js` chama `ip-api.com` no login
