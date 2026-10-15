# Infraestrutura

Documentação de infraestrutura e DevOps do projeto Mash.

## Fonte

Detalhes extraídos dos artefatos do projeto (`artefatos_projeto.pdf`, seção 4).

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

Fluxo de interação: usuário → acessa aplicação → envia imagem do teste de iodo → recebe resultado da análise → consulta histórico armazenado.

## Observação sobre o serviço Python/OpenCV

Previsto para o **próximo semestre** (decisão de 14/10/2026): um serviço Python interno (`POST /analyze`) para processar as imagens, chamado apenas pelo Back-End Node.js, conforme a #34 e as sub-issues #42–#44. Não faz parte do ambiente do depósito.

## DevOps

| Aspecto | Estado |
|---|---|
| CI/CD | `conloq/.github` tem o workflow `mash-project-notifications.yml` (notificações de sprint); pipeline de testes nos Pull Requests fica para depois do depósito (#94) |
| Testes automatizados | Fora do escopo; a validação é manual e fica registrada na #41 |
| Migrations | Fonte do schema desde 12/10/2026: `npm run db:migrate` antes de subir a API e a cada deploy (#71) |
| Deploy | Manual, no Render gratuito: API na #68 (com MySQL externo no Aiven) e frontend na #69 (decisão de 13/10/2026, substitui Railway) |
| Monitoramento | mash_project_notifier (Python, em .github) |
