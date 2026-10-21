# Frontend

Documentação da área Frontend do projeto Mash.

> **Atualizado em 21/10/2026.** O detalhe de telas, rotas e chamadas à API fica no README do [`conloq/frontend`](https://github.com/conloq/frontend#readme), que acompanha o código; aqui ficam só as decisões e o mapa da área.

## Repositório

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/frontend`](https://github.com/conloq/frontend) | Telas EJS com Tailwind que consomem a API do Back-End | Login, cadastro, perfil, receitas e rampas ligados à API desde 13/10 (`7a6fc89`); lotes planejados; iodo somente como simulação no frontend |

## Arquitetura (decisão de 12/10/2026, conloq/mash#6)

- O `index.js` só entrega as telas (EJS) e injeta `window.API_URL`; não tem sessão, banco nem regra de negócio.
- **O navegador chama a API direto**, em `public/js/app.js`, com o token no `localStorage` (`mash-token`) enviado como `Authorization: Bearer`. O Back-End libera CORS para `FRONTEND_URL`. Risco de XSS aceito pelo time; substitui a decisão de 09/10 (API só pelo servidor, cookie `HttpOnly`).
- As mensagens de sucesso e erro aparecem como a API devolve, em pt-BR; o frontend não traduz nem cria texto de negócio.
- **Portas:** frontend na 4000, API na 8080, nunca a mesma.
- As telas reais consomem a API; a simulação do teste de iodo é a exceção explícita da decisão de 21/10/2026.
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

## Integração entregue e recorte vigente

As rotas `/recipes` e os campos camelCase já estão na main do Back-End conferida em 21/10; as telas de receitas/rampas acompanham na #86. A conferência de schema não comprova o deploy público. OpenCV e todo o fluxo real do teste de iodo ficam no backlog para outro semestre. Neste semestre permanece somente a simulação no frontend, com cena obrigatória no pitch, sem etiqueta de simulação na cena ([decisão de 21/10/2026, #66](https://github.com/conloq/mash/issues/66)).

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#12](https://github.com/conloq/mash/issues/12) (design e navegação), [#83](https://github.com/conloq/mash/issues/83) (login), [#80](https://github.com/conloq/mash/issues/80) (receitas e rampas), [#81](https://github.com/conloq/mash/issues/81) (lotes), [#82](https://github.com/conloq/mash/issues/82) (simulação do teste de iodo) e [#61](https://github.com/conloq/mash/issues/61) (deploy).

## Diferenças mash vs frontend

| Aspecto | conloq/mash (legado) | conloq/frontend |
|---|---|---|
| Persistência | MySQL + Sequelize no próprio app | Nenhuma: os dados vêm da API do Back-End |
| Autenticação | express-session + bcrypt | JWT da API, guardado no `localStorage` |
| CSS | Custom | Tailwind compilado |
| Regra de negócio | No servidor | No Back-End; o frontend só mostra |

