# Database

Documentação do banco de dados do projeto Mash.

## Repositório

[`conloq/database`](https://github.com/conloq/database) — schema MySQL, MER, SQL

## Stack

- **SGBD:** MySQL
- **ORM:** Sequelize 6
- **Database:** `cervejaria` (mash) / `mash` (Back-End — ⚠️ divergente)
- **Timezone:** -03:00
- **Charset:** utf8mb4_unicode_ci

## ⚠️ Divergência de schema: mash vs Back-End

Os dois backends usam **databases e tabelas diferentes**. A migração (#30) unifica o schema conforme as decisões abaixo.

| Aspecto | mash (original) | Back-End (migração) |
|---|---|---|
| Database | `cervejaria` | `mash` |
| Tabela usuário | `usuarios` (nome, email, telefone, senha, url_imagem) | `Users` (name, email, fone, password, url_image) |
| Tabela receita | `receitas` (nome, usuario_id) | `receitas` (nome, user_id) |
| FK receita | `usuario_id` | `user_id` |
| Tabelas temperatura/iodo/log | ✅ Existem | ❌ Não existem ainda |
| Credenciais | Hardcoded no código | Via `.env` (dotenv) |

## Decisões vigentes (26/09)

- **Colunas físicas em snake_case**; o contrato JSON da API é camelCase. A tradução é feita na borda via DTO/serialização — **não** existe `underscored: true` global (a opção renomearia também `createdAt`, `updatedAt` e FKs automáticas do schema existente e corromperia o banco).
- **Runtime atual:** `Connection.sync()` no startup do Back-End (`app.js`), decisão #40 mantida como not_planned.
- **A pasta `migrations/` existe, mas os arquivos atuais não são executáveis de forma segura** (migration de receita vazia; `DataTypes` sem import; `down()` da temperatura derruba a tabela errada). Nenhuma migration é executada até uma issue de banco revisá-las em branch + PR com teste de banco vazio.
- **`collectedTemperature` na análise de iodo é dado declarado manualmente** (decisão D5=A em 26/09) até a cadeia de temperatura por dispositivo (#45–#48) voltar ao escopo.

## Arquivos

| Arquivo | Descrição |
|---|---|
| `mash.sql` | Script SQL completo (CREATE DATABASE + todas as tabelas do app legado) |
| `diagrama_mer_mash.mmd` | Diagrama MER em formato Mermaid |
| `README.md` | Documentação detalhada do schema |

## Schema atual (5 tabelas)

### Modelo Entidade-Relacionamento

```
USUARIOS 1:N RECEITAS
USUARIOS 1:N HISTORICO_LOGINS
RECEITAS 1:N IODOS
RECEITAS 1:N TEMPERATURAS
```

### Tabelas

#### `usuarios`
| Campo | Tipo | Constraint |
|---|---|---|
| id | INT AUTO_INCREMENT | PK |
| nome | VARCHAR(255) | NOT NULL |
| email | VARCHAR(255) | NOT NULL |
| telefone | VARCHAR(255) | NULL |
| senha | VARCHAR(255) | NOT NULL (bcrypt hash) |
| url_imagem | VARCHAR(255) | NULL |

#### `receitas`
| Campo | Tipo | Constraint |
|---|---|---|
| id | INT AUTO_INCREMENT | PK |
| nome | VARCHAR(255) | NOT NULL |
| usuario_id | INT | FK → usuarios.id |

#### `temperaturas`
| Campo | Tipo | Constraint |
|---|---|---|
| id | INT AUTO_INCREMENT | PK |
| rampa_temperatura_minima | INT | NOT NULL |
| rampa_temperatura_maxima | INT | NOT NULL |
| temp_maxima_limite | INT | NOT NULL |
| temp_minima_limite | INT | NOT NULL |
| temporizador | TIME | NOT NULL |
| inicializacao | TIME | NOT NULL |
| tempo_ideal | TIME | NOT NULL |
| temperatura_ativa | BOOLEAN | NOT NULL, DEFAULT FALSE |
| receita_id | INT | FK → receitas.id, ON DELETE CASCADE |

#### `iodos`
| Campo | Tipo | Constraint |
|---|---|---|
| id | INT AUTO_INCREMENT | PK |
| tempo_primeira_coleta | TIME | NOT NULL |
| intervalo_testes | TIME | NOT NULL |
| qtd_max_testes | INT | NOT NULL |
| receita_id | INT | FK → receitas.id, ON DELETE CASCADE |

#### `Historico_Logins`
| Campo | Tipo | Constraint |
|---|---|---|
| id | INT AUTO_INCREMENT | PK |
| endereco_ip | VARCHAR(255) | NOT NULL |
| data_hora | DATETIME | DEFAULT CURRENT_TIMESTAMP |
| localidade | VARCHAR(255) | NOT NULL |
| status | BOOLEAN | NULL |
| usuario_id | INT | FK → usuarios.id, ON DELETE CASCADE |

Todas as tabelas possuem `createdAt` e `updatedAt` (timestamps do Sequelize não desativados).

## Observações

- A tabela `temperaturas` não faz parte do foco acadêmico principal desta etapa (foco: teste de iodo).
- Credenciais não devem ser mantidas no código. Use variáveis de ambiente.
- Configuração atual: `host: localhost, username: root, password: '', database: cervejaria`.
- Model Sequelize `Historico_Login` gera tabela `Historico_Logins` (pluralização automática).
- O SQL documenta o **app legado**. O schema oficial do Back-End vigente é o que `Connection.sync()` gera a partir dos models (`Users`, `receitas`, `Temperatures`).

## Entidades futuras (propostas, não implementadas)

Conforme issues #31, #1, #2 e #36, o schema será expandido para incluir:

| Entidade | Issue | Rotas esperadas | Descrição |
|---|---|---|---|
| `lotes` | #31 | `/lots` | CRUD de lotes vinculados a receitas |
| `analises` | #1 | `/analyses/:id` | Entidade de análise do teste de iodo |
| `analysis_execucoes` | #2 | `/analyses/:id/reprocess` | Execuções de reprocessamento |
| `evaluations` | #5 | `/evaluations` (não `/avaliacoes`) | Avaliação reproduzível com conjunto de referência |
| `leituras_temperatura` | #45 | pós-depósito | Leituras de temperatura por lote (IoT) |
| `dispositivos` | #46 | pós-depósito | Credenciais de dispositivos IoT |
