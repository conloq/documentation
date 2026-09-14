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
| Preto | — | `#000000` | Textos principais |

### Tipografia

| Fonte | Uso | Características |
|---|---|---|
| **Poppins** | Títulos, chamadas, elementos de destaque | Traços suaves, moderna, dinâmica |
| **Roboto** | Textos longos, corpo | Neutra, legível, adaptável |

## Landing page

### Seções

1. **Hero** — apresentação inicial da Conloq e acesso ao projeto
2. **Sobre Nós** — objetivos e proposta da equipe
3. **Equipe** — integrantes com nome, função e tecnologias
4. **Cerveja artesanal** — contexto da mosturação e teste de iodo
5. **Mash** — apresentação visual do sistema e proposta de visão computacional
6. **Contatos** — redes sociais, GitHub, LinkedIn, e-mail

### Stack

| Camada | Tecnologia |
|---|---|
| Estrutura | HTML5 |
| Estilização | CSS3 |
| Interatividade | JavaScript |
| Hospedagem | GitHub Pages |
| Versionamento | Git e GitHub |

Sem `package.json` ou etapa de build — página estática.

## Figma

As telas do sistema foram prototipadas no Figma. O frontend tem exportações em `docs/figma-export/` com screenshots e tokens de design.

| Tela exportada | Descrição |
|---|---|
| `receita-authenticated.png` | Tela de receitas com usuário autenticado |
| `tokens.md` | Design tokens (cores, espaçamento, tipografia) |

## Issues ativas (Design)

| Issue | Título | Prioridade | Status |
|---|---|---|---|
| #23 | Adicionar ícones à seção de propósitos | High | Test |
| #24 | Revisar o fluxo de criação de lote no Figma | Urgent | In progress |
| #25 | Atualizar o pitch com demonstração do fluxo real | Medium | Ready |
| #26 | Adicionar legendas em português ao pitch | Medium | Ready |
| #27 | Adicionar trilha sonora ao pitch | Medium | Ready |
| #28 | Demonstrar captura e envio da imagem no pitch | Medium | Ready |
| #29 | Atualizar o banner do Mash | High | Ready |
