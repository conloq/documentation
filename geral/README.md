# Geral

Documentação geral do projeto Mash — decisões, requisitos e artefatos transversais.

## Sobre o projeto

**Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal**

Projeto Integrador — Desenvolvimento de Software Multiplataforma — FATEC Registro (2026).

O Mash propõe uma plataforma para apoiar pequenos produtores de cerveja artesanal no acompanhamento da mosturação, no teste de iodo e na rastreabilidade das análises. A visão computacional com Python/OpenCV é prevista para auxiliar na identificação de amido residual por características de cor.

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
| João Alexandre Pinto Camargo | Backend |
| Jocieli Pontes Domingues da Silva | Artigo e documentação |
| Kevin da Silva Oliveira | Design |
| Haimon Cugler Vieira | Frontend |

## ODS (Objetivos de Desenvolvimento Sustentável)

- **ODS 9** (Indústria, Inovação e Infraestrutura) — alternativa de automação acessível para pequenos produtores
- **ODS 12** (Consumo e Produção Responsáveis) — potencial redução de desperdício e melhoria de rendimento (a validar)

## Canvas (Modelo de Negócio)

Disponível em `artefatos_projeto.pdf`, seção 3 (Figura 5). Detalha os nove blocos: parceiros, atividades, recursos, proposta de valor, relacionamento, canais, segmentos, custos e receitas.

## SWOT

A definir na issue #52 (sub-issue de #37).

## Roteiro de Execução

> **Issue central (fonte de verdade):** [conloq/mash#66](https://github.com/conloq/mash/issues/66) — 🗺️ Roteiro de Execução

Este é o documento de referência para saber **a ordem de execução das issues, as metas de cada sprint e o que fazer a qualquer momento**. Atualizado pelo PO a cada sprint. **Os resumos abaixo são espelho — em caso de divergência, vale a #66.**

### Sprints do semestre

> ⚠️ Pontos de S4–S7 são provisórios: recalibrados na Sprint Review de 01/10 com a velocity real (histórica: 13 pts/sprint).

| Sprint | Período | Foco | Pontos |
|---|---|---|---|
| Sprint 1 | 10/08 – 01/09 | Base do projeto + artigo (fundamentação inicial) | 11 |
| Sprint 2 | 01/09 – 16/09 | Artigo (Estado da Arte, lacuna científica) | 15 |
| **Sprint 3** | **16/09 – 01/10** | **CRUD receitas + contrato de iodo + segredos + branch protection** | **10** |
| Sprint 4 | 01/10 – 16/10 | CRUD lotes + testes HTTP + infra (CORS) + auth/IDOR + trabalho de banco (nova issue) | ~17 |
| Sprint 5 | 16/10 – 31/10 | Análises de iodo (#1, #2, #3) + upload (#33) + frontend resultado + deploy | ~13 |
| Sprint 6 | 31/10 – 15/11 | Histórico (#3) + pacote de depósito (#63) + **depósito PI 03/11** | ~17+ |
| Sprint 7 | 15/11 – 30/11 | Relatório consolidado (#59/#64) + OpenCV + avaliação (#65) + pitch + **bancas 16–27/11** | 13 |

### Ordem de execução por épico

Cada épico tem um comentário fixo no topo com a ordem de execução das suas sub-issues, links diretos abaixo:

| Épico | Sprint | Link da ordem |
|---|---|---|
| [#30 — API REST do Mash](https://github.com/conloq/mash/issues/30) | S3–S5 | [Ordem](https://github.com/conloq/mash/issues/30#issuecomment-5720845904) |
| [#36 — Contrato de iodo](https://github.com/conloq/mash/issues/36) | S6 | [Ordem](https://github.com/conloq/mash/issues/36#issuecomment-5720852657) |
| [#12 — Frontend ↔ Backend](https://github.com/conloq/mash/issues/12) | S6 (filhas S4–S6) | [Ordem](https://github.com/conloq/mash/issues/12#issuecomment-5720858568) |
| [#34 — Análise OpenCV](https://github.com/conloq/mash/issues/34) | S7 (Could — pós-depósito) | [Ordem](https://github.com/conloq/mash/issues/34) |
| [#37 — Artefatos do PI](https://github.com/conloq/mash/issues/37) | S4–S6 | [Ordem](https://github.com/conloq/mash/issues/37#issuecomment-5720861684) |
| [#56 — Artigo Científico](https://github.com/conloq/mash/issues/56) | S5 (In progress) | [Ordem](https://github.com/conloq/mash/issues/56#issuecomment-5720849209) |
| [#57 — Pitch do Mash](https://github.com/conloq/mash/issues/57) | S6 (filhas S6–S7) | [Ordem](https://github.com/conloq/mash/issues/57#issuecomment-5720868314) |

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
| Migrations vs sync() | Runtime vigente: `Connection.sync()` no startup. Pasta `migrations/` existe (26/09) mas os arquivos não são executáveis; nova migration só com issue própria | #40 (fechada), #66 |
| Padrão de resposta | Sucesso `{ "message": "..." }` (+ entidade no singular/plural quando aplicável), erro `{ "error": "..." }` — string direta, **mensagens sempre em pt-BR** (base aula-05 DW3); `204` sem corpo no DELETE. **Sem wrapper `data`** (26/09) | #30, #41, #66 |
| Portas | Frontend **4000** / API **8080** — nunca a mesma (decisão 19/09) | #6, #66 |
| Nomenclatura da API | EN + camelCase; coleção plural (`/recipes`, `/lots`, `/analyses`), recurso único singular (`/user`), `login` à parte | #30, #66 |
| Resultado da análise (enum) | `PASSED` / `FAILED` / `null` | #34 |
| Espaço de cor (HSV vs CIELab) | Ambos (a definir na bancada) | #42 |
| Tempo real (polling/SSE/WS) | **Resolvido: re-render server-side** — sem `fetch()` no browser nem WebSocket, salvo exceção aprovada | #36, #8 |
| Credencial de dispositivo IoT | Revogável, própria | #36 |
| IA generativa no classificador | NÃO decide o resultado | #34 |
| Database `cervejaria` vs `mash` | ⚠️ Divergente — unificar na migração, trabalho de banco com issue própria | #30 |
| Tabela `usuarios` vs `users` | Resolvido — tabela `Users` (padrão do Back-End) | #30 |
| JSON vs colunas físicas | JSON camelCase na borda; colunas físicas snake_case. Não usar `underscored: true` global (26/09) | #30, #66 |
| `collectedTemperature` | Dado declarado manualmente pelo operador no upload — leitura automática por dispositivo fica pós-depósito (26/09) | #33, #36 |
| Scope do depósito (03/11) | 14 rotas em 6 grupos (receitas, lotes, upload, consulta, reprocessamento condicional, histórico); temperatura/alertas, OpenCV, relatório consolidado e avaliações fora (26/09) | #66 |
| #4 relatório consolidado | Resolvido — #4 fechada como duplicata de #64 (19/09); a #64 está fora do depósito (D7 — pendente PO) | #64 |
| #2 reprocessamento | Reaberta intencionalmente (19/08); reescopo sem OpenCV pendente de confirmação (26/09) — #2 | #2 |

## Bugs conhecidos (código real)

| Bug | Local | Issue |
|---|---|---|
| ~~ReferenceError (`id` usado antes de declarar)~~ — corrigido no código | Back-End `recipeController.js` | #32 |
| ~~`createRecipe()` vazio~~ — implementado em 18/09 (commit 159c1ce) | Back-End `recipeService.js` | #32 |
| `GET /recipes/:id` inexistente; apenas 4 rotas em `/receitas` no código | Back-End `recipeRoutes.js` | #32 |
| Rotas ainda em `/receitas` — migrar para `/recipes` (breaking para o frontend #58) | Back-End `recipeRoutes.js` | #32 |
| 409 "Receita já existe" ausente no createRecipe | Back-End `recipeService.js` | #32 |
| `res.status(204)` sem `send()` no delete (resposta não encerra) | Back-End `recipeController.js` e `userController.js` | #32 |
| ~~API key Context7 versionada~~ — removida via [frontend#1](https://github.com/conloq/frontend/pull/1); **rotação da chave pendente de confirmação** | frontend `opencode.json` | #54 |
| Credenciais hardcoded | mash `sequelize-config.js`, `session.js` | #39 |
| `.env.example` inexistente em Back-End e mash; boot não valida env obrigatória | Back-End, mash | #39 (fechada em 19/09; evidência dos critérios restantes pendente) |
