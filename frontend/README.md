# Frontend

Documentação da área Frontend do projeto Mash.

> **Sincronizado em 08/10.** Frontend na porta **4000** e API na 8080, nunca a mesma (#6, #66). O `preview-server.js` é temporário: foi feito para ver as telas antes de a API existir e sai quando o frontend passar a consumir o Back-End. Enquanto existir, ele sobe na 8080 se a variável `PORT` não estiver definida; use `PORT=4000`.

## Repositórios

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/frontend`](https://github.com/conloq/frontend) | Preview EJS com Tailwind (validação UX) | Funcional (mock) |

## Sobre o preview

O `frontend` é um **preview estático** do Mash com dados mockados em memória. Não há MySQL, Sequelize, autenticação real, sessões, bcrypt, Multer ou uploads persistentes.

**Propósito:** validar visual/UX antes da integração com a API REST da #30.

## Arquitetura (decisão vigente, 19/09)

- **Server-rendered EJS:** o Express injeta os dados nas views. Hoje a entrada é o `preview-server.js`; a #6 o substitui pelo `index.js` na raiz, como nos projetos de DW2.
- **Integração real (#58):** `fetch()` **server-side** no `index.js` para a API (porta 8080). **Não há `fetch()` no browser** nem WebSocket (salvo exceção aprovada).
- **Mensagens:** o Frontend exibe o texto pt-BR devolvido pela API (`{message}`/`{error}`) — **não traduz nem gera texto de negócio**.
- **Porta:** `4000` (a 8080 é reservada à API). Configurar `API_URL` no `.env` do frontend.

## Stack

| Tecnologia | Versão | Uso |
|---|---|---|
| Node.js (ESM) | — | Runtime |
| Express | ^5.2.1 | Servidor estático |
| EJS | ^5.0.2 | View engine |
| Tailwind CSS | ^4.3.3 | Framework CSS |
| Phosphor Icons | ^2.1.2 | Ícones |

## Estrutura

```
frontend/
├── preview-server.js           # Express estático (8 rotas GET, sem POST logic)
├── views/                      # EJS templates
│   ├── partials/               # header, sidebar, topBar, footer
│   ├── index.ejs, login.ejs, cadastro.ejs, usuario.ejs, receita.ejs
│   ├── adicionarTemperatura.ejs, editarTemperatura.ejs
│   └── adicionarIodo.ejs, editarIodo.ejs
├── public/
│   ├── css/style.css           # Tailwind compilado (30 KB)
│   ├── css/tailwind.css        # Input Tailwind (1.6 KB)
│   └── js/script.js            # JS cliente
├── docs/                       # Documentação (codebase, specs, figma-export)
├── codemap.md                  # Mapa do frontend
└── AGENTS.md                   # Convenções
```

## Rotas (preview — apenas GET)

| Rota | View |
|---|---|
| `/` | login |
| `/cadastro` | cadastro |
| `/usuario` | usuario |
| `/receita` | receita |
| `/receita/temperatura/criar/:id` | adicionarTemperatura |
| `/receita/temperatura/editar/:id` | editarTemperatura |
| `/receita/iodo/criar/:id` | adicionarIodo |
| `/receita/iodo/editar/:id` | editarIodo |

## Como executar

```bash
git clone https://github.com/conloq/frontend.git
cd frontend
npm install
npm run build:css
npm start
# Preview em http://localhost:4000
```

## Issues ativas (Frontend) — estado 07/10

| Issue | Título | Prioridade | Status |
|---|---|---|---|
| #75 | Desenhar as telas de upload e de resultado do teste de iodo (Kevin) | High | Ready (S4); libera #60, #9 e #10 |
| #6 | Implementar login com cookie seguro e token nas chamadas à API | High | Ready (S4) |
| #7 | Simplificar o fluxo de criação de lote (wizard mock) | Low | Fora do depósito; o wizard entra direto pela #58 |
| #58 | Integrar o wizard à API real | High | Backlog (S5); aguarda #6, #31 e #32 |
| #8 | Implementar controles de temperatura acessíveis e integrados | Low | Fora do depósito |
| #9 | Criar upload de imagem do teste de iodo | High | Backlog (S5); aguarda #33 e #75 |
| #10 | Criar tela de resultado da análise do teste de iodo | High | Backlog (S5); aguarda #1, #9 e #75 |
| #11 | Criar histórico de análises por lote | Low | Fora do depósito |
| #73 | Corrigir navegação, ações e estados das telas | Low | Fora do depósito; separada da #6 em 07/10 |
| #69 | Publicar frontend e configurar integração com a API | High | Backlog (S5); Railway, depois da #68 |
| #12 | Integrar os fluxos do frontend aos contratos reais do backend (épico) | High | Ready (S6) |

## Diferenças mash vs frontend

| Aspecto | conloq/mash | conloq/frontend |
|---|---|---|
| Persistência | MySQL + Sequelize | Nenhuma (mock) |
| Autenticação | express-session + bcrypt | Nenhuma |
| CSS | Custom (17 KB) | Tailwind compilado (30 KB) |
| POST | Lógica real + redirect | Apenas redirect para navegação |
| Dados | Reais do banco | Mockados nas views EJS |
