# Infraestrutura

Documentação de infraestrutura e DevOps do projeto Mash.

## Fonte

A topologia e os endereços abaixo são a proposta dos artefatos do projeto (`artefatos_projeto.pdf`, seção 4), não uma rede comprovada nesta conferência. O ambiente local observado é descrito em [database/evidencias](../database/evidencias/README.md): MariaDB 10.4.32, banco mash. O deploy é conferido separadamente.

## Topologia da rede

**Topologia em estrela**: todos os dispositivos conectados a um switch central na sala técnica. O switch está ligado ao modem/roteador (gateway para internet).

## Endereçamento

| Dispositivo | Endereço IP | Função |
|---|---|---|
| Roteador / Gateway | `192.168.0.1` | Acesso à internet |
| Servidor | `192.168.0.2` | Armazenamento, processamento das análises, execução da aplicação |
| Computador da Sala Técnica | `192.168.0.10` | Monitoramento, gerenciamento operacional |
| Dispositivos móveis | DHCP automático | Captura de imagens, acesso remoto via Wi-Fi |

## Componentes

| Componente | Descrição |
|---|---|
| **Roteador / Gateway** | Acesso à internet, gateway padrão, distribuição da comunicação |
| **Switch Central** | Interligação dos dispositivos, estrutura central da topologia estrela |
| **Servidor** | Processamento das análises, execução da aplicação, armazenamento de dados |
| **Computador da Sala Técnica** | Monitoramento, gerenciamento operacional, controle local |
| **Dispositivos Móveis** | Captura das imagens do teste de iodo, acesso remoto via Wi-Fi |

## Rede

- **Cabeada:** Ethernet Cat6 (estabilidade e velocidade)
- **Sem fio:** Ponto de acesso Wi-Fi na sala técnica
- **Servidor:** IP fixo

## Diagrama de usabilidade

Fluxo planejado do recorte: conta → receitas/rampas → lotes. O código observado contempla conta, receitas e criação/listagem de rampas; lotes ainda são planejados. A validação do deploy é separada (#68 e #69). O recorte do semestre está centralizado em [geral/README.md](../geral/README.md) e na [#66](https://github.com/conloq/mash/issues/66).

## DevOps

| Aspecto | Estado |
|---|---|
| CI/CD | `conloq/.github` tem o workflow `mash-project-notifications.yml` (notificações de sprint); pipeline de testes nos Pull Requests fica para depois do depósito (#94) |
| Verificações | Evidências na #41; o Back-End tem scripts de verificação, sem inferir validação de todo ambiente publicado |
| Migrations | Fonte do schema desde 12/10/2026: `npm run db:migrate` antes de subir a API e a cada deploy (#71) |
| Deploy | Manual, no Render gratuito: API na #68 (com MySQL externo no TiDB Cloud desde 24/10/2026) e frontend na #69 (decisão de 13/10/2026, substitui Railway) |
| Monitoramento | mash_project_notifier (Python, em .github) |

