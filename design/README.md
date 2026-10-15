# Design

Documentação da área Design do projeto Mash.

## Responsável

Kevin da Silva Oliveira

## Repositórios

| Repositório | Papel |
|---|---|
| [`conloq/landing-page-conloq`](https://github.com/conloq/landing-page-conloq) | Landing page institucional (HTML5 + CSS3 + JS) |
| `conloq/frontend` | Preview com Tailwind (interface do sistema) |

## Guia de Estilos (UX/UI)

### Paleta de cores (proporção 60-30-10)

| Cor | Proporção | HEX | Aplicação |
|---|---|---|---|
| Branco/off-white | 60% | `#FAFAFA` | Fundos principais, áreas de respiro |
| Marrom escuro | 30% | `#4E342E` | Header, menus, fundos secundários |
| Laranja | 10% | `#F57C00` | Botões, links, chamadas de ação |
| Preto | - | `#000000` | Textos principais |

### Tipografia

| Fonte | Uso | Características |
|---|---|---|
| **Poppins** | Títulos, chamadas, elementos de destaque | Traços suaves, moderna, dinâmica |
| **Roboto** | Textos longos, corpo | Neutra, legível, adaptável |

## Landing page

### Seções

1. **Hero**: apresentação inicial da Conloq e acesso ao projeto
2. **Sobre Nós**: objetivos e proposta da equipe
3. **Equipe**: integrantes com nome, função e tecnologias
4. **Cerveja artesanal**: contexto da mosturação e teste de iodo
5. **Mash**: apresentação visual do sistema e proposta de visão computacional
6. **Contatos**: redes sociais, GitHub, LinkedIn, e-mail

### Stack

| Camada | Tecnologia |
|---|---|
| Estrutura | HTML5 |
| Estilização | CSS3 |
| Interatividade | JavaScript |
| Hospedagem | GitHub Pages |
| Versionamento | Git e GitHub |

Sem `package.json` ou etapa de build: página estática.

## Figma

As telas do sistema foram prototipadas no Figma. O frontend tem exportações em `docs/figma-export/` com screenshots e tokens de design.

| Tela exportada | Descrição |
|---|---|
| `receita-authenticated.png` | Tela de receitas com usuário autenticado |
| `tokens.md` | Design tokens (cores, espaçamento, tipografia) |

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#12](https://github.com/conloq/mash/issues/12) (design e navegação das telas), [#82](https://github.com/conloq/mash/issues/82) (telas de upload e resultado, #75) e [#57](https://github.com/conloq/mash/issues/57) (pitch e banner). O pitch mostra a cena da visão computacional como prévia de como o Mash vai funcionar; o banner é exposto na HubTec.
