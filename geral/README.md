# Geral

Documentação geral do projeto Mash — decisões, requisitos e artefatos transversais.

## Sobre o projeto

**Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal**

Projeto Integrador — Desenvolvimento de Software Multiplataforma — FATEC Registro (2026).

O Mash propõe uma plataforma para apoiar pequenos produtores de cerveja artesanal no acompanhamento da mosturação, no teste de iodo e na rastreabilidade das análises. A visão computacional com Python/OpenCV é prevista para auxiliar na identificação de amido residual por características de cor.

## Equipe

| Integrante | Área |
|---|---|
| João Alexandre Pinto Camargo | Backend |
| Jocieli Pontes Domingues da Silva | Artigo e documentação |
| Kevin da Silva Oliveira | Design |
| Haimon Cugler Vieira | Frontend |

## ODS (Objetivos de Desenvolvimento Sustentável)

- **ODS 9** (Indústria, Inovação e Infraestrutura) — alternativa de automação acessível para pequenos produtores
- **ODS 12** (Consumo e Produção Responsáveis) — potencial redução de desperdícios e melhoria de rendimento (a validar)

## Canvas (Modelo de Negócio)

Disponível em `artefatos_projeto.pdf`, seção 3 (Figura 5). Detalha os nove blocos: parceiros, atividades, recursos, proposta de valor, relacionamento, canais, segmentos, custos e receitas.

## SWOT

A definir na issue #52 (sub-issue de #37).

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
| Artigo | Prism (OpenAI) | Escrita científica, revisão, LaTeX, busca de literatura |
| Design/Frontend | Open Design | Ideias de interface, componentes, responsividade |
| Backend | OpenCode | APIs, CRUDs, banco, debug, testes, Flask/OpenCV |

## Convenção de commits

```text
<tipo>: descrição curta da alteração
```

Tipos: `feat`, `fix`, `refactor`, `test`, `docs`, `style`, `chore`.

### Regras

- Descrição curta e objetiva
- Verbo de ação claro
- Não incluir credenciais
- Relacionar à issue quando aplicável
- Evitar misturar frentes diferentes
- Revisar e testar antes de commit

## Decisões técnicas relevantes

| Decisão | Status | Issue |
|---|---|---|
| Migração para API REST | Em andamento | #30 |
| JWT vs session | JWT (implementado no Back-End) | #38 |
| Argon2id vs bcrypt | Argon2id (implementado no Back-End) | #38 |
| Migrations vs sync() | Migrations (a implementar) | #40 |
| Padrão HTTP de erros | `{ error: { code, message, fields? } }` | #41 |
| Espaço de cor (HSV vs CIELab) | Ambos (a definir na bancada) | #42 |
| Tempo real (polling/SSE/WS) | A definir pela equipe | #36 |
| Credencial de dispositivo IoT | Revogável, própria | #36 |
| IA generativa no classificador | NÃO decide o resultado | #34 |
| Database `cervejaria` vs `mash` | ⚠️ Divergente — unificar na migração | #30 |
| Tabela `usuarios` vs `users` | ⚠️ Divergente — unificar na migração | #30 |

## Bugs conhecidos (código real)

| Bug | Local | Issue |
|---|---|---|
| ReferenceError (`id` usado antes de declarar) | Back-End `recipeController.js` | #32 |
| `createRecipe()` vazio | Back-End `recipeService.js` | #32 |
| Sem CRUD completo de receita (só GET list) | Back-End `recipeRoutes.js` | #32 |
| API key Context7 versionada | frontend `opencode.json` | #39 |
| Credenciais hardcoded | mash `sequelize-config.js`, `session.js` | #39 |
