# Documentação do Projeto Mash

**Conloq** — Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal

Projeto Integrador III — Back-End II — DSM3 — FATEC Registro

---

## O que este repositório contém

Este repositório centraliza **toda a documentação** do projeto Mash, organizada por área de atuação da equipe. Cada pasta contém os documentos técnicos, acadêmicos e visuais da respectiva frente.

Não é um repositório de código — use os repositórios de código para implementação:

| Repositório | Código |
|---|---|
| [`conloq/mash`](https://github.com/conloq/mash) | Aplicação original (Express + EJS + MySQL) |
| [`conloq/Back-End`](https://github.com/conloq/Back-End) | API REST (JWT + Argon2id, migração em andamento, código mapeado) |
| [`conloq/frontend`](https://github.com/conloq/frontend) | Preview frontend com Tailwind |

---

## Navegação por área

### 🖥️ [Backend](./backend/README.md)

Documentação da área Backend: arquitetura da aplicação original (mash) e da migração para API REST (Back-End). Inclui models Sequelize, rotas HTTP, padrão de autenticação (JWT/Argon2id), issues ativas e pontos de atenção técnicos.

### 🎨 [Frontend](./frontend/README.md)

Preview EJS com Tailwind para validação de UX antes da integração com a API. Inclui rotas, diferenças entre o preview e a aplicação original, stack e issues ativas da área.

### 🗄️ [Database](./database/README.md)

Schema MySQL completo (`cervejaria`), modelo Entidade-Relacionamento (MER), script SQL, diagrama Mermaid e entidades futuras previstas nas issues (#31 lotes, #1 análises, #45 leituras IoT).

### 📝 [Artigo](./artigo/README.md)

Artigo científico completo, templates LaTeX/Beamer e metas de validação experimental (acurácia ≥ 50%, tempo ≤ 2s, inconclusivos ≤ 10%, concordância ≥ 90%). Inclui estado da arte, lacuna científica e metodologia.

### 🎭 [Design](./design/README.md)

Guia de estilos (paleta 60-30-10, tipografia Poppins/Roboto), landing page institucional, Figma, pitch com IA Generativa e issues da área design.

### 🌐 [Infraestrutura](./infraestrutura/README.md)

Topologia de rede (estrela), endereçamento IP, componentes (servidor, switch, dispositivos móveis), DevOps e automação de notificações (mash_project_notifier em Python).

### 📋 [Geral](./geral/README.md)

Requisitos transversais, decisões técnicas com referência às issues, regras de trabalho (status, prioridades, commits), boas práticas de IA e entregas obrigatórias do PI.

---

## Entregas obrigatórias do PI (Mind Map)

Consulte [`geral/entregas/mind-map-entregas-pi.mm`](./geral/entregas/mind-map-entregas-pi.mm) para o mapa completo das entregas obrigatórias do Projeto Integrador III.

| Entrega | Status |
|---|---|
| Artigo Científico (LaTeX) | ✅ 1ª versão pronta |
| Artefatos do Projeto (DOCX) | 🔄 Em atualização (#37, #50–#53) |
| Projeto de Software (GitHub) | 🔄 Em desenvolvimento (#30–#36; Back-End com JWT/Argon2id, bugs em recipeController) |
| Pesquisa de Usuário (IHC) | [TODO] |
| Banco de Dados (BDNR) | ✅ Documentado |
| Documentação (GAPS/SWOT) | 🔄 Em andamento (#52) |
| Apresentação (10-11 min) | 🔄 Pitch em produção (#25–#27) |
| Escola de Inovadores | [TODO] |

---

## Templates de referência

Os documentos acadêmicos seguem os templates da FATEC:

| Template | Repositório |
|---|---|
| Artigo científico (LaTeX) | [fbamuniz/template-paper-f299](https://github.com/fbamuniz/template-paper-f299) |
| Artefatos do projeto | [fbamuniz/template-artefacts-f299](https://github.com/fbamuniz/template-artefacts-f299) |
| Apresentação Beamer | [fbamuniz/template-beamer-f299](https://github.com/fbamuniz/template-beamer-f299) |

---

## Equipe

| Integrante | Área |
|---|---|
| João Alexandre Pinto Camargo | Backend |
| Jocieli Pontes Domingues da Silva | Artigo e documentação |
| Kevin da Silva Oliveira | Design |
| Haimon Cugler Vieira | Frontend |

## Licença

Este projeto é destinado a fins educacionais e acadêmicos.
