# Documentação do Projeto Mash

**Conloq**: Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal

Projeto Integrador III, Back-End II, DSM3, FATEC Registro

---

## O que este repositório contém

Este repositório centraliza **toda a documentação** do projeto Mash, organizada por área de atuação da equipe. Cada pasta contém os documentos técnicos, acadêmicos e visuais da respectiva frente.

Não é um repositório de código: use os repositórios de código para implementação:

| Repositório | Código |
|---|---|
| [`conloq/mash`](https://github.com/conloq/mash) | Aplicação original (Express + EJS + MySQL) |
| [`conloq/Back-End`](https://github.com/conloq/Back-End) | API REST (JWT + Argon2id, migração em andamento, código mapeado) |
| [`conloq/frontend`](https://github.com/conloq/frontend) | Frontend EJS/Tailwind com integração à API |


## Contexto e arquitetura canônicos

- [`geral/architecture.md`](./geral/architecture.md): fronteiras técnicas e dependências cross-repo comprovadas.
- [`geral/context-lifecycle.md`](./geral/context-lifecycle.md): processo conceitual portátil de descoberta e sincronização de contexto.
- [Índice global Conloq/Mash](https://github.com/conloq/.github/blob/main/PROJECT_CONTEXT.md): registry, hierarquia de fontes e links canônicos.
---

## Navegação por área

### 🖥️ [Backend](./backend/README.md)

Documentação da área Backend: arquitetura da aplicação original (mash) e da migração para API REST (Back-End). Inclui models Sequelize, rotas HTTP, padrão de autenticação (JWT/Argon2id), issues ativas e pontos de atenção técnicos.

### 🎨 [Frontend](./frontend/README.md)

Frontend EJS com Tailwind, integrado à API nas telas entregues. O teste de iodo permanece somente como simulação para a demonstração e o pitch, conforme a #66.

### 🗄️ [Database](./database/README.md)

Schema atual `mash` conferido no banco local (MariaDB 10.4.32): `users`, `recipes`, `temperatures` e `SequelizeMeta`, com MER, DDL de referência e evidências de metadados. O legado `cervejaria` fica preservado e identificado separadamente; lotes ainda são planejados e análises reais ficam para outro semestre.

### 📝 [Artigo](./artigo/README.md)

Artigo científico e templates LaTeX/Beamer, com estado da arte, lacuna científica e metodologia. As metas de classificação e a validação experimental pertencem ao trabalho futuro; não são resultados medidos do depósito.

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
| Artigo Científico (PDF) | ✅ Versão de 23/10 publicada; #56 encerrada com pendências aceitas |
| Artefatos do Projeto (LaTeX) | 🔄 Em atualização (#37, #50–#53) |
| Projeto de Software (GitHub) | 🔄 Em desenvolvimento (#30–#36; Back-End com JWT/Argon2id, bugs em recipeController) |
| Pesquisa de Usuário (IHC) | [TODO] |
| Banco de Dados (BDNR) | Schema local conferido; evidências em [database/evidencias](database/evidencias/README.md) |
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

