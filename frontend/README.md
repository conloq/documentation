# Frontend

Documentação da área Frontend do projeto Mash.

> **Atualizado em 28/10/2026.** O detalhe de telas, rotas e chamadas à API fica no README do [`conloq/frontend`](https://github.com/conloq/frontend#readme), que acompanha o código; aqui ficam só as decisões e o mapa da área.

## Repositório

| Repositório | Papel | Status |
|---|---|---|
| [`conloq/frontend`](https://github.com/conloq/frontend) | Telas Next.js (React) com Tailwind que chamam a API do Back-End | Login, cadastro, perfil, receitas e rampas ligados à API desde 13/10; JWT no navegador desde 28/10; lotes planejados |

## Arquitetura (JWT no navegador, 28/10/2026, conloq/mash#66)

- As telas são páginas Next.js em `src/pages`; `src/services/api.js` chama a API do Back-End com `axios` e envia `Authorization: Bearer` em toda requisição.
- **O navegador chama a API direto** e guarda o JWT no `localStorage` (`mash_token`), então um XSS alcança o token. Isso substitui a decisão de 24/10, da sessão no servidor; a tabela `sessions` foi removida do Back-End em 28/10/2026.
- As mensagens de sucesso e erro aparecem como a API devolve, em pt-BR; o frontend não traduz nem cria texto de negócio.
- **Portas:** frontend na 4000, API na 8080, nunca a mesma.
- Campos de temperatura limitados a 0–100 °C com `min`/`max` no HTML, no lugar das barras deslizantes (14/10/2026).

## Stack

| Tecnologia | Uso |
|---|---|
| Next.js (React, Pages Router) | Páginas e roteamento |
| axios | Chamadas à API do Back-End, direto do navegador |
| Tailwind CSS 4 | Estilos (`npm run build:css`) |
| Phosphor Icons | Ícones |

## Como executar

```bash
git clone https://github.com/conloq/frontend.git
cd frontend
npm install
npm run build:css
npm run dev          # http://localhost:4000; a API precisa estar em NEXT_PUBLIC_API_URL (padrão http://localhost:8080)
```

## Integração entregue

As rotas `/recipes` e os campos camelCase já estão na `main` do Back-End; as telas de receitas/rampas acompanham na #86. A conferência de schema não comprova o deploy público. O recorte do semestre está centralizado em [geral/README.md](../geral/README.md) e na [#66](https://github.com/conloq/mash/issues/66).

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#12](https://github.com/conloq/mash/issues/12) (design e navegação), [#83](https://github.com/conloq/mash/issues/83) (login), [#80](https://github.com/conloq/mash/issues/80) (receitas e rampas), [#81](https://github.com/conloq/mash/issues/81) (lotes), [#82](https://github.com/conloq/mash/issues/82) (simulação do teste de iodo) e [#61](https://github.com/conloq/mash/issues/61) (deploy).

## Diferenças mash vs frontend

| Aspecto | conloq/mash (legado) | conloq/frontend |
|---|---|---|
| Persistência | MySQL + Sequelize no próprio app | Nenhuma no app; os dados de negócio vêm da API do Back-End |
| Autenticação | express-session + bcrypt | JWT no `localStorage` (`mash_token`), enviado em `Authorization: Bearer` |
| CSS | Custom | Tailwind compilado |
| Regra de negócio | No servidor | No Back-End; o frontend só mostra |

