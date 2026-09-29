# Geral

Documentação geral do projeto Mash — decisões, requisitos e artefatos transversais.

## Sobre o projeto

**Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal**

Projeto Integrador — Desenvolvimento de Software Multiplataforma — FATEC Registro (2026).

O Mash propõe uma plataforma para apoiar pequenos produtores de cerveja artesanal no acompanhamento da mosturação, no teste de iodo e na rastreabilidade das análises. A visão computacional com Python/OpenCV é prevista para auxiliar na identificação de amido residual por características de cor.

> **Status (29/09/2026):** MVP entregue no depósito do PI em 03/11 (Encerramento do PI — DSM). Sem desenvolvimento de novas funcionalidades; bancas em 16–27/11, com o pitch apresentado na banca.

## Papéis ágeis (GAPS)

| Papel | Responsável | Atribuições |
|---|---|---|
| **Product Owner (PO)** | IA — Team Lead (agente de IA do projeto) | Gestão e refinamento do backlog, priorização das issues (MoSCoW), validação dos critérios de aceite e atualização do Project |
| **Product Manager (PM)** | Haimon Cugler Vieira | Visão de produto, decisões de escopo, aprovação de prioridades e responsabilidade final das entregas |
| **Scrum Master (SM)** | Haimon Cugler Vieira (rotativo) | Facilitação do processo ágil, cerimônias (planning, review, retrospectiva), remoção de impedimentos e organização do quadro |
| **Desenvolvedores** | Todos os integrantes (incluindo PO e SM) | Implementação, testes, revisão por pares e documentação |

> Papéis de PO e SM são rotativos entre os ciclos do projeto. A IA atua como apoio de gestão e revisão; todas as decisões finais passam pelo PM.

## Equipe

| Integrante | Área |
|---|---|
| João Alexandre Pinto Camargo | Backend e deploy da API |
| Jocieli Pontes Domingues da Silva | Artigo e documentação |
| Kevin da Silva Oliveira | Design |
| Haimon Cugler Vieira | Frontend, Backend e gestão do projeto |

## ODS (Objetivos de Desenvolvimento Sustentável)

- **ODS 9** (Indústria, Inovação e Infraestrutura) — alternativa de automação acessível para pequenos produtores
- **ODS 12** (Consumo e Produção Responsáveis) — potencial redução de desperdício e melhoria de rendimento (a validar)

## Canvas (Modelo de Negócio)

Disponível em `artefatos_projeto.pdf`, seção 3 (Figura 5). Detalha os nove blocos: parceiros, atividades, recursos, proposta de valor, relacionamento, canais, segmentos, custos e receitas.

## SWOT

A definir na issue #52 (sub-issue de #37).

## Roteiro de Execução

> **Issue central (fonte de verdade):** [conloq/mash#66](https://github.com/conloq/mash/issues/66) — 🗺️ Roteiro de Execução

Este é o documento de referência para saber **a ordem de execução das issues, as metas de cada sprint e o que fazer a qualquer momento**. Atualizado pelo PO a cada sprint. **Os resumos abaixo são espelho — em caso de divergência, vale a #66.** Adições de 29/09: #70 (contrato CRUD de usuário, João, S4) e #71 (migrations como fonte de verdade, João, S4).

### Sprints do semestre

> ⚠️ Pontos de S4–S7 são provisórios: recalibrados na Sprint Review de 01/10 com a velocity real (histórica: 13 pts/sprint).

| Sprint | Período | Foco | Pontos |
|---|---|---|---|
| Sprint 1 | 10/08 – 01/09 | Base do projeto + artigo (fundamentação inicial) | 11 |
| Sprint 2 | 01/09 – 16/09 | Artigo (Estado da Arte, lacuna científica) | 15 |
| **Sprint 3** | **16/09 – 01/10** | **CRUD receitas + contrato de iodo + branch protection** | **14** |
| Sprint 4 | 01/10 – 16/10 | Testes HTTP e IDOR (João) + lotes e wizard (Haimon) | 21+ |
| Sprint 5 | 16/10 – 31/10 | Consulta/upload de iodo, telas e deploy #68/#69 | 19+ |
| Sprint 6 | 31/10 – 03/11 | Estabilização + **depósito do PI em 03/11** (Encerramento do PI — DSM) | janela de 3 dias |
| **Pós-depósito** | 04/11 – 27/11 | **Sem desenvolvimento.** 04–16/11: período de correção do PI · 16–27/11: bancas (pitch apresentado na banca) | — |

> **PI encerrado em 03/11.** Issues fora do recorte do depósito não serão implementadas (ver "Fora de escopo" abaixo). A FTX'26 ocorreu em 28–29/05 (1º semestre) e não faz parte do calendário deste projeto.

### Fora de escopo (PI encerrado em 03/11)

Issues registradas no backlog como histórico, **não serão implementadas**: #2 (reprocessamento), #5 e #65 (avaliação da classificação), #34 com #42–#44 (OpenCV), #45–#49 com #8 (temperatura/IoT/alertas), #59 e #64 (relatório consolidado).

### Apresentação na banca (16–27/11)

- **Pitch apresentado na banca** — roteirização e ensaio na #62; atualizações de pitch (#25–#28) limitadas ao que demonstra o PI entregue.
- **Banner (#29):** opcional, decisão do PM.
- Demo ao vivo do fluxo entregue (`login → receita → lote → upload → consulta`) com vídeo gravado como plano B.

### Ordem de execução por épico

Cada épico tem um comentário fixo no topo com a ordem de execução das suas sub-issues, links diretos abaixo:

| Épico | Sprint | Link da ordem |
|---|---|---|
| [#30 — API REST do Mash](https://github.com/conloq/mash/issues/30) | S3–S6 (depósito) | [Ordem](https://github.com/conloq/mash/issues/30#issuecomment-5720845904) |
| [#36 — Contrato de iodo](https://github.com/conloq/mash/issues/36) | S3 | [Ordem](https://github.com/conloq/mash/issues/36#issuecomment-5720852657) |
| [#12 — Frontend ↔ Backend](https://github.com/conloq/mash/issues/12) | S4–S6 | [Ordem](https://github.com/conloq/mash/issues/12#issuecomment-5720858568) |
| [#34 — Análise OpenCV](https://github.com/conloq/mash/issues/34) | fora de escopo | — |
| [#37 — Artefatos do PI](https://github.com/conloq/mash/issues/37) | S4–S6 | [Ordem](https://github.com/conloq/mash/issues/37#issuecomment-5720861684) |
| [#56 — Artigo Científico](https://github.com/conloq/mash/issues/56) | S5 | [Ordem](https://github.com/conloq/mash/issues/56#issuecomment-5720849209) |
| [#57 — Pitch do Mash](https://github.com/conloq/mash/issues/57) | preparação para a banca (16–27/11) | [Ordem](https://github.com/conloq/mash/issues/57#issuecomment-5720868314) |

### Regras de ouro antes de puxar uma issue

1. Ela está na sprint atual? (consulte o [roteiro](https://github.com/conloq/mash/issues/66))
2. Tem assignee atribuído?
3. Não está bloqueada por outra issue?

Se qualquer resposta for **"não"**, consulte o PO antes de iniciar.

## Regras de trabalho

### Status das tarefas (Project Mash)

- **Backlog:** tarefa identificada, mas não priorizada
- **Ready:** tarefa definida, com responsável e informações suficientes
- **In Progress:** tarefa em execução
- **In Review:** tarefa concluída, aguardando revisão
- **Testing / Validation:** revisada, em fase de testes
- **Done:** implementada, revisada, testada, aceita e documentada

### Critérios para mover para Done

1. Foi implementada
2. Foi revisada
3. Foi testada
4. Está funcionando conforme o escopo
5. A documentação foi atualizada

### Prioridades

- 🔴 **Alta/Urgent:** funcionalidade crítica para a próxima entrega
- 🟡 **Medium:** importante, não impede funcionamento principal
- 🟢 **Low:** melhoria posterior às funcionalidades essenciais

### Tipos de tarefa

Feature, Bug, Improvement, Research, Documentation, Design, Test

## Boas práticas para uso de IA

- Não utilizar código sem entender seu funcionamento
- Revisar todo código gerado antes de commit
- Não inserir credenciais em ferramentas de IA
- Validar referências acadêmicas nas fontes originais
- Não utilizar referências, resultados ou funcionalidades inventados pela IA
- IA é ferramenta de apoio, não substituição da análise da equipe

## Ferramentas de IA por área

| Área | Ferramenta | Uso |
|---|---|---|
| Artigo | Prism | Escrita científica, revisão, LaTeX, busca de literatura |
| Design/Frontend | Open Design | Ideias de interface, componentes, responsividade |
| Backend | OpenCode | APIs, CRUDs, banco, debug, testes, Flask/OpenCV |

## Convenção de commits

```text
<tipo>(<escopo>)?: descrição curta da alteração
```

Tipos: `feat`, `fix`, `refactor`, `test`, `docs`, `style`, `chore`, `build`, `ci`, `perf`, `revert`.

### Regras

- Descrição curta e objetiva
- Verbo de ação claro
- Não incluir credenciais
- Relacionar à issue quando aplicável
- Evitar misturar frentes diferentes
- Revisar e testar antes de commit
- **Nunca commitar direto na `main`** — branch própria + PR + peer review

## Decisões técnicas relevantes

| Decisão | Status | Issue |
|---|---|---|
| Migração para API REST | Em andamento | #30 |
| JWT vs session | JWT (implementado no Back-End) | #38 |
| Argon2id vs bcrypt | Argon2id (implementado no Back-End) | #38 |
| Migrations vs sync() | **(a) Migrations como fonte de verdade (decisão 29/09)** — adicionar script + `.sequelizerc`, corrigir 5a–5e e remover o `sync()` do boot (`app.js:22`) | #71, #66 |
| Padrão de resposta | Sucesso `{ "message": "..." }` (+ entidade no singular/plural quando aplicável), erro `{ "error": "..." }` — string direta, **mensagens sempre em pt-BR** (base aula-05 DW3); `204` sem corpo no DELETE. **Sem wrapper `data`** (26/09) | #30, #41, #66 |
| Portas | Frontend **4000** / API **8080** — nunca a mesma (decisão 19/09) | #6, #66 |
| Nomenclatura da API | EN snake_case em rotas, tabelas, colunas e payload; coleção plural (`/recipes`, `/lots`, `/analyses`), recurso único singular (`/user`), `login` à parte; parâmetro `:id`; FK `<entidade>_id` | #30, #66 |
| Resultado da análise (enum) | `PASSED` / `FAILED` / `null` | #34 |
| Espaço de cor (HSV vs CIELab) | Ambos (a definir na bancada) | #42 |
| Tempo real (polling/SSE/WS) | **Resolvido: re-render server-side** — sem `fetch()` no browser nem WebSocket, salvo exceção aprovada | #36, #8 |
| Credencial de dispositivo IoT | Revogável, própria | #36 |
| IA generativa no classificador | NÃO decide o resultado | #34 |
| Database `cervejaria` vs `mash` | ⚠️ Divergente — unificar na migração, trabalho de banco com issue própria | #30 |
| Caixa dos nomes de tabela | Divergente (`Users`/`Temperatures` maiúsculo, `receitas` minúsculo) e FK `users` ≠ `Users` — normalizar na #71 (5a–5e) | #71 |
| Payload vs colunas | Mesma nomenclatura: o payload usa o nome da coluna, sem camada de tradução. Colunas em português viram inglês (`nome`→`name`, `fone`→`phone`); `receitas`→`recipes`. Não usar `underscored: true` global (28/09) | #30, #66 |
| `collectedTemperature` | Dado declarado manualmente pelo operador no upload — leitura automática por dispositivo fica pós-depósito (26/09) | #33, #36 |
| Contrato do CRUD de usuário | Publicado na #70 (6 rotas; `GET /user` sem `password` via `attributes:{exclude}`) — João, S4 | #70 |
| Fonte do schema | **Migrations** (decisão 29/09, escolha (a)); `sync()` sai do boot; nomes de tabela minúsculos, FK casando com o nome real | #71 |
| Escopo do depósito (03/11) | 13 rotas em 5 grupos: receitas, lotes, upload, consulta e histórico básico; temperatura/alertas, OpenCV, reprocessamento, relatório e avaliações ficam pós-depósito | #66 |
| #4 relatório consolidado | #4 fechada como duplicata de #64; #59/#64 estão fora do depósito e na S7 | #64, #66 |
| #2 reprocessamento | Reaberta intencionalmente, mas movida para S7; não bloqueia o histórico básico da #3 | #2, #3, #66 |

## Bugs conhecidos (código real)

| Bug | Local | Issue |
|---|---|---|
| ~~ReferenceError (`id` usado antes de declarar)~~ — corrigido no código | Back-End `recipeController.js` | #32 |
| ~~`createRecipe()` vazio~~ — implementado em 18/09 (commit 159c1ce) | Back-End `recipeService.js` | #32 |
| `GET /recipes/:id` inexistente; apenas 4 rotas em `/receitas` no código | Back-End `recipeRoutes.js` | #32 |
| Rotas ainda em `/receitas` — migrar para `/recipes` (breaking para o frontend #58) | Back-End `recipeRoutes.js` | #32 |
| 409 "Receita já existe" ausente no createRecipe | Back-End `recipeService.js` | #32 |
| `res.status(204)` sem `send()` no delete (resposta não encerra) | Back-End `recipeController.js` e `userController.js` (validação da #70 em 29/09 confirmou no user) | #32, #41, #70 |
| ~~API key Context7 versionada~~ — removida via [frontend#1](https://github.com/conloq/frontend/pull/1); **rotação da chave pendente de confirmação** | frontend `opencode.json` | #54 |
| Credenciais hardcoded | mash `sequelize-config.js`, `session.js` | #39 |
| `.env.example` inexistente em Back-End e mash; boot não valida env obrigatória | Back-End, mash | #39 (fechada em 19/09; evidência dos critérios restantes pendente) |
