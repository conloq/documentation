# Frontend

Documentação da área Frontend do projeto Mash.

## Repositórios

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/frontend`](https://github.com/conloq/frontend) | Preview EJS com Tailwind (validação UX) | Funcional (mock) |

## Sobre o preview

O `frontend` é um **preview estático** do Mash com dados mockados em memória. Não há MySQL, Sequelize, autenticação real, sessões, bcrypt, Multer ou uploads persistentes.

**Propósito:** validar visual/UX antes da integração com a API REST da #30.

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
# Preview em http://localhost:8080
```

## Issues ativas (Frontend)

| Issue | Título | Prioridade | Status |
|---|---|---|---|
| #6 | Corrigir navegação, ações e estados de autorização | Urgent | In progress |
| #7 | Simplificar o fluxo de criação de lote | Urgent | Ready |
| #8 | Implementar controles de temperatura acessíveis e integrados | High | Ready |
| #9 | Criar upload de imagem do teste de iodo | Medium | Ready |
| #10 | Criar tela de resultado da análise do teste de iodo | Medium | Ready |
| #11 | Criar histórico de análises por lote | Medium | Ready |
| #12 | Integrar os fluxos do frontend aos contratos reais do backend | High | Ready |

## Diferenças mash vs frontend

| Aspecto | conloq/mash | conloq/frontend |
|---|---|---|
| Persistência | MySQL + Sequelize | Nenhuma (mock) |
| Autenticação | express-session + bcrypt | Nenhuma |
| CSS | Custom (17 KB) | Tailwind compilado (30 KB) |
| POST | Lógica real + redirect | Apenas redirect para navegação |
| Dados | Reais do banco | Mockados nas views EJS |
