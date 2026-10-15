# Frontend

Documentação da área Frontend do projeto Mash.

> **Atualizado em 15/10/2026.** O detalhe de telas, rotas e chamadas à API fica no README do [`conloq/frontend`](https://github.com/conloq/frontend#readme), que acompanha o código; aqui ficam só as decisões e o mapa da área.

## Repositório

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/frontend`](https://github.com/conloq/frontend) | Telas EJS com Tailwind que consomem a API do Back-End | Login, cadastro, perfil, receitas e rampas ligados à API desde 13/10 (`7a6fc89`); lote, upload e resultado na Sprint 5 |

## Arquitetura (decisão de 12/10/2026, conloq/mash#6)

- O `index.js` só entrega as telas (EJS) e injeta `window.API_URL`; não tem sessão, banco nem regra de negócio.
- **O navegador chama a API direto**, em `public/js/app.js`, com o token no `localStorage` (`mash-token`) enviado como `Authorization: Bearer`. O Back-End libera CORS para `FRONTEND_URL`. Risco de XSS aceito pelo time; substitui a decisão de 09/10 (API só pelo servidor, cookie `HttpOnly`).
- As mensagens de sucesso e erro aparecem como a API devolve, em pt-BR; o frontend não traduz nem cria texto de negócio.
- **Portas:** frontend na 4000, API na 8080, nunca a mesma.
- Cada tela é feita primeiro com o design novo e dados simulados e depois ligada à API (decisão de 09/10/2026).
- Campos de temperatura limitados a 0–100 °C com `min`/`max` no HTML, no lugar das barras deslizantes (14/10/2026).

## Stack

| Tecnologia | Uso |
|---|---|
| Node.js (ESM) + Express 5 | Servidor que entrega as telas |
| EJS | View engine |
| Tailwind CSS 4 | Estilos (`npm run build:css`) |
| Phosphor Icons | Ícones |

## Como executar

```bash
git clone https://github.com/conloq/frontend.git
cd frontend
npm install
npm run build:css
npm start            # http://localhost:4000; a API precisa estar em API_URL (padrão http://localhost:8080)
```

## Mudança prevista

Com a conloq/mash#71 e a conloq/mash#32, a API passa a `/recipes` e a campos em camelCase. A troca no `app.js` e nos formulários é a conloq/mash#86, que também atualiza a documentação do `conloq/frontend`.

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#12](https://github.com/conloq/mash/issues/12) (design e navegação), [#83](https://github.com/conloq/mash/issues/83) (login), [#80](https://github.com/conloq/mash/issues/80) (receitas e rampas), [#81](https://github.com/conloq/mash/issues/81) (lotes), [#82](https://github.com/conloq/mash/issues/82) (upload e resultado) e [#61](https://github.com/conloq/mash/issues/61) (deploy).

## Diferenças mash vs frontend

| Aspecto | conloq/mash (legado) | conloq/frontend |
|---|---|---|
| Persistência | MySQL + Sequelize no próprio app | Nenhuma: os dados vêm da API do Back-End |
| Autenticação | express-session + bcrypt | JWT da API, guardado no `localStorage` |
| CSS | Custom | Tailwind compilado |
| Regra de negócio | No servidor | No Back-End; o frontend só mostra |
