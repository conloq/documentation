# Geral

Documentação geral do projeto Mash: decisões, requisitos e artefatos transversais.

## Sobre o projeto

**Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal**

Projeto Integrador: Desenvolvimento de Software Multiplataforma, FATEC Registro (2026).

O Mash propõe uma plataforma para apoiar pequenos produtores de cerveja artesanal no acompanhamento da mosturação, no teste de iodo e na rastreabilidade das análises. A visão computacional com Python/OpenCV, para identificar o amido residual pela cor, fica para o próximo semestre (conloq/mash#34); no depósito, o teste de iodo é somente simulação no frontend, com cena obrigatória no pitch; upload, registro, consulta e histórico reais ficam para outro semestre.

> **Status (15/10/2026):** Sprint 5 em andamento (16 a 30/10), com o código congelando em 30/10. Depósito do PI em 03/11 (Encerramento do PI: DSM), com o pitch e o banner. Bancas em 16–27/11. O banner é exposto na HubTec (data no calendário acadêmico, a confirmar); a FTX de 2026 foi em maio.

## Papéis ágeis (GAPS)

| Papel | Responsável | Atribuições |
|---|---|---|
| **Product Owner (PO)** | IA: Team Lead (agente de IA do projeto) | Gestão e refinamento do backlog, priorização das issues (MoSCoW), validação dos critérios de aceite e atualização do Project |
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

- **ODS 9** (Indústria, Inovação e Infraestrutura): alternativa de automação acessível para pequenos produtores
- **ODS 12** (Consumo e Produção Responsáveis): potencial redução de desperdício e melhoria de rendimento (a validar)

## Canvas (Modelo de Negócio)

Disponível em `artefatos_projeto.pdf`, seção 3 (Figura 5). Detalha os nove blocos: parceiros, atividades, recursos, proposta de valor, relacionamento, canais, segmentos, custos e receitas.

## SWOT

Na issue conloq/mash#52 (Canvas completo e SWOT), filha do épico #37, na Sprint 5.

## Roteiro de Execução

> **Issue central (fonte de verdade):** [conloq/mash#66](https://github.com/conloq/mash/issues/66): 🗺️ Roteiro de Execução

Este resumo incorpora o recorte da #66 de 21/10/2026; **em caso de divergência, vale a #66**. Ordem, responsáveis e pontos de cada issue estão lá e no Project Mash.

### Sprints do semestre

| Sprint | Período | Situação |
|---|---|---|
| Sprint 1 a 3 | 10/08 – 01/10 | Encerradas; pontos concluídos: 11, 9 e 2 |
| Sprint 4 | 01/10 – 15/10 | Encerrada; resultados e replanejamento no roteiro #66 |
| **Sprint 5** | **16/10 – 30/10** | Fluxo real de conta, receitas, rampas e lotes; teste de iodo somente como simulação no frontend, em ambiente publicado; código congela em 30/10 |
| Sprint 6 | 31/10 – 03/11 | Estabilização e **depósito do PI em 03/11** (Encerramento do PI: DSM), com pitch, banner e documento de artefatos |
| Depois do depósito | 04/11 – 27/11 | 04–16/11: período de correção · 16–27/11: bancas |

### Épicos do depósito (fatias verticais, desde 14/10/2026)

Cada épico entrega uma funcionalidade inteira, da API à tela (aula 09 de GAPS).

| Épico | O que entrega |
|---|---|
| [#83: Conta e segurança](https://github.com/conloq/mash/issues/83) | Cadastro, login e autorização por dono do recurso |
| [#80: Receitas e rampas](https://github.com/conloq/mash/issues/80) | Receitas e rampas de temperatura, na API e na tela |
| [#81: Lotes](https://github.com/conloq/mash/issues/81) | Lotes vinculados à receita, na API e no wizard |
| [#82: Teste de iodo](https://github.com/conloq/mash/issues/82) | Simulação do teste de iodo no frontend para a demonstração e a cena obrigatória do pitch |
| [#30: Base da API](https://github.com/conloq/mash/issues/30) | Padrões, schema por migrations e evidências (#41) |
| [#12: Interface](https://github.com/conloq/mash/issues/12) | Design das telas e navegação sem botões quebrados |
| [#61: Deploy](https://github.com/conloq/mash/issues/61) | API, MySQL e frontend publicados |
| [#37: Artefatos do PI](https://github.com/conloq/mash/issues/37) | UML, MER, infraestrutura, Canvas, SWOT, Diário de Bordo e documento em LaTeX |
| [#56: Artigo](https://github.com/conloq/mash/issues/56) | Metodologia com o que é entregue e o que é planejado |
| [#57: Pitch e banner](https://github.com/conloq/mash/issues/57) | Pitch de 1 a 2 minutos com legendas e banner da HubTec |
| [#84: Entrega e apresentação](https://github.com/conloq/mash/issues/84) | Depósito pelo Teams, pesquisa de usuário de IHC e ensaios |

### Próximo semestre (Won't nesta entrega)

Também ficam fora do depósito o upload, o armazenamento, a consulta e o histórico reais de iodo (#1, #3, #11 e #33). Permanecem como planejamento: [#34](https://github.com/conloq/mash/issues/34) análise do teste de iodo com OpenCV (com #42–#44 e #65), [#36](https://github.com/conloq/mash/issues/36) temperatura por dispositivo e alertas (#45–#49 e #8) e [#85](https://github.com/conloq/mash/issues/85) rastreabilidade avançada (#2, #59 e #64).

### Pitch, banner e apresentação

- **Pitch** (#25 a #28): artefato do depósito, de 1 a 2 minutos, com legendas em português e inglês. Mostra o fluxo real e, obrigatoriamente, a cena do teste de iodo usando a simulação no frontend, sem etiqueta de simulação na cena, a pedido do orientador.
- **Banner** (#29): pronto para o depósito e exposto na HubTec.
- **Banca** (#62): 10 a 11 minutos, começando com dados já cadastrados; demonstração ao vivo com vídeo gravado como reserva.

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
- **Test:** revisada, em validação
- **Done:** implementada, revisada, testada, aceita e documentada

### Critérios para mover para Done

1. Foi implementada
2. Foi revisada
3. Foi testada
4. Está funcionando conforme o escopo
5. A documentação foi atualizada

### Prioridades (MoSCoW, aulas 03 e 09 de GAPS)

| Campo Priority | Label | Significado |
|---|---|---|
| High | `scope:must-have` | Sem isto a demonstração para a banca falha |
| Medium | `scope:should-have` | Importante, mas o sistema funciona sem; é o primeiro a sair se faltar tempo |
| Low | `scope:could-have` ou `scope:wont-have` | Só depois de Must e Should prontos; Won't fica para o próximo semestre |

O tipo vai em `type:feature` ou `type:bugfix` (aula 09), ao lado de `enhancement`, `bug` e `documentation`.

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
- **Nunca commitar direto na `main`**: branch `<tipo>/<número da issue>-<descrição-curta>` + PR + peer review
- **Modelo de Pull Request:** todo PR novo já abre com o modelo da organização, que fica em [`conloq/.github`](https://github.com/conloq/.github#modelo-de-pull-request). São cinco seções, as da aula 08 de GAPS: tipo de alteração, issue relacionada (`Closes conloq/mash#N`), descrição, checklist de DoD e evidências de teste. Marque só o que foi feito e anexe a evidência (JSON no backend, captura de tela no frontend).
- **Revisão automática (09/10/2026):** no `Back-End` e no `frontend`, o CodeRabbit comenta cada Pull Request em português (configuração em `.coderabbit.yaml`) e o CodeQL do GitHub analisa o código a cada Pull Request e a cada push na `main`; os alertas ficam em Security > Code scanning. No `Back-End`, o `.github/CODEOWNERS` pede a revisão do Tech Lead em todo Pull Request. Nenhum dos três aprova ou bloqueia o merge: a aprovação continua sendo de uma pessoa.

## Decisões técnicas relevantes

Espelho da seção "Decisões vigentes" da [#66](https://github.com/conloq/mash/issues/66) com o recorte de 21/10/2026; em caso de divergência, vale a #66.

| Decisão | Situação | Issue |
|---|---|---|
| Migração para API REST | Em andamento; o legado `conloq/mash` não é publicado | #30 |
| JWT e Argon2id | Implementados no Back-End | #38 |
| Fonte do schema | **Migrations do Sequelize** (12/10): `npm run db:migrate` antes de `npm start` e a cada deploy; o bootstrap atual já não usa `Connection.sync()` | #71, #66 |
| Nomes | JSON em camelCase (`userId`, `recipeId`, `urlImage`, `createdAt`); banco em **snake_case** nas tabelas e colunas (`user_id`, `recipe_id`, `url_image`, `created_at`), ligados por `define: { underscored: true }`, sem código de tradução (08/10/2026, reafirmada em 15/10/2026; a regra de 13/10, banco em camelCase, foi revertida); tabelas atuais `users`, `recipes`, `temperatures`; `lots` planejada e `analyses` no próximo semestre; rotas em inglês, coleção no plural, `/user` singular, `login` à parte, parâmetro `:id` | #30, #71 |
| Padrão de resposta | Sucesso `{ "message": "..." }` (+ entidade nomeada), erro `{ "error": "..." }` em pt-BR, sem wrapper `data`; `DELETE` responde 204 sem corpo | #30, #41 |
| Recurso alheio | O mesmo 404 de recurso inexistente | #38 |
| Portas | Frontend **4000**, API **8080** | #6 |
| Frontend chama a API | Pelo navegador, com o token no `localStorage` (`mash-token`) e `Authorization: Bearer`; a API libera CORS para `FRONTEND_URL`. Risco de XSS aceito (12/10) | #6 |
| Hospedagem | Render gratuito para API e frontend; MySQL gratuito externo (Aiven); imagens no Cloudinary (13/10, substitui Railway) | #61, #68, #69 |
| Escopo do depósito | 14 rotas planejadas em 3 grupos reais: receitas, rampas e lotes; iodo somente simulado no frontend | #66 |
| Imagem do teste de iodo | Upload e armazenamento reais no próximo semestre | #33, #66 |
| Teste de iodo no depósito | Somente simulação no frontend, com cena obrigatória no pitch; sem registro real em processing | #9, #10, #25, #28, #66 |
| Coleta de iodo | Dado do fluxo futuro; não exigir captura ou persistência reais no depósito | #33, #66 |
| Campos de temperatura | Limitados a 0–100 °C, com mínimo nunca maior que máximo, nas rotas e telas reais de rampas; a simulação de iodo não exige API | #32, #86, #97 |
| Visão computacional | Próximo semestre; o pitch mostra a cena como prévia do produto (14/10 e 15/10) | #34, #25, #28 |
| IA generativa no classificador | Não decide o resultado | #34 |
| Testes automatizados | Fora do escopo do depósito: validação manual registrada na #41; pipeline de CI fica para depois (15/10) | #41, #94 |
| Legado `cervejaria` | Banco do app antigo, documentado como registro em `conloq/database`; a API usa o banco `mash` | #30 |

## Evidências atuais de código e banco

A conferência de 21/10 compara o banco local com Back-End `7f33203`: três tabelas de negócio, 25 colunas, duas FKs e três migrations, sem divergências estruturais nos atributos conferidos. [Metadados, comparação e limites](../database/evidencias/README.md).

Detalhe de receita, rotas em inglês e nomes físicos snake_case já existem na main auditada. Estado das pendências de lotes, rampas, perfil e deploy deve ser consultado nas issues; tabelas históricas de bugs não substituem a evidência do código atual.
