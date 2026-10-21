> Documento histórico do schema legado. Não descreve o banco atual da API nem o recorte vigente; consulte o [README atual](../README.md).

# Database

Documentação do banco de dados do projeto Mash.

## Repositório

[`conloq/database`](https://github.com/conloq/database): schema MySQL, MER, SQL

## Stack

- **SGBD:** MySQL
- **ORM:** Sequelize 6
- **Database:** `cervejaria` (mash) / `mash` (Back-End: ⚠️ divergente)
- **Timezone:** -03:00
- **Charset:** utf8mb4_unicode_ci

## ⚠️ Divergência de schema: mash vs Back-End

Os dois backends usam **databases e tabelas diferentes**. A migração (#30) unifica o schema conforme as decisões abaixo.

| Aspecto | mash (original) | Back-End (migração) |
|---|---|---|
| Database | `cervejaria` | `mash` |
| Tabela usuário | `usuarios` (nome, email, telefone, senha, url_imagem) | `users` (name, email, phone, password, url_image) depois da #71 |
| Tabela receita | `receitas` (nome, usuario_id) | `recipes` (name, user_id) depois da #71 |
| FK receita | `usuario_id` | `user_id` |
| Temperatura no Back-End | ✅ implementação parcial (`Temperatures` + POST por receita) | ✅ rampas de temperatura por receita (`Temperatures`, POST), dentro do depósito desde 09/10 (#32); leitura por sensor fica para depois |
| Iodo e histórico de login no Back-End | ✅ Existem no app legado | ❌ não existem na API nova |
| Credenciais | Hardcoded no código | Via `.env` (dotenv) |

## Decisões vigentes (15/10/2026)

- **Nomes (08/10/2026, reafirmada em 15/10/2026):** tabelas e colunas em inglês **snake_case** (`user_id`, `recipe_id`, `url_image`, `created_at`, `updated_at`); o JSON da API usa camelCase. Os models declaram os atributos em camelCase e a conexão usa `define: { underscored: true }`, sem código de tradução. A regra de 13/10 (banco em camelCase) foi revertida.
- **Schema por migrations (12/10/2026):** toda tabela ou coluna entra por arquivo em `migrations/` do Back-End, aplicado com `npm run db:migrate` antes de `npm start` e a cada deploy. O `Connection.sync()` sai do `app.js` na #71; a #40 continua fechada.
- **`collectedTemperature` na análise de iodo é dado declarado manualmente** pelo operador; a leitura por dispositivo (#45–#48) fica para o próximo semestre.
- **Hospedagem:** MySQL gratuito externo (Aiven), porque o Render gratuito não oferece MySQL (#61, #68).
- O MER do banco novo é a [#87](https://github.com/conloq/mash/issues/87), feita depois dos nomes finais da #71.

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

- As rampas de temperatura da receita (`temperatures`) fazem parte do depósito; a leitura por sensor fica para o próximo semestre.
- Credenciais não devem ser mantidas no código. Use variáveis de ambiente.
- Configuração atual: `host: localhost, username: root, password: '', database: cervejaria`.
- Model Sequelize `Historico_Login` gera tabela `Historico_Logins` (pluralização automática).
- O SQL documenta o **app legado**. O schema oficial do Back-End vem das migrations: hoje `Users`, `receitas` e `Temperatures`, que a #71 padroniza para `users`, `recipes` e `temperatures`.

## Entidades futuras (propostas, não implementadas)

Conforme issues #31, #1, #2 e #36, o schema será expandido para incluir:

| Entidade | Issue | Rotas esperadas | Descrição |
|---|---|---|---|
| `lots` | #31, #92 | `/lots` | Lotes vinculados a receitas (Sprint 5) |
| `analyses` | #1 | `/analyses/:id` | Entidade de análise do teste de iodo (Sprint 5) |
| `analysis_executions` | #2 | `/analyses/:id/reprocess` | Execuções de reprocessamento (próximo semestre) |
| `evaluations` | #65 | `/evaluations` | Avaliação da classificação (próximo semestre, com o OpenCV) |
| leituras de temperatura | #45 | próximo semestre | Leituras de temperatura por lote (IoT) |
| dispositivos | #46 | próximo semestre | Credenciais de dispositivos IoT |

