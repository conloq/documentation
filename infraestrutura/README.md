# Infraestrutura

Documentação de infraestrutura e DevOps do projeto Mash.

## Fonte

Detalhes extraídos dos artefatos do projeto (`artefatos_projeto.pdf`, seção 4).

## Topologia da rede

**Topologia em estrela** — todos os dispositivos conectados a um switch central na sala técnica. O switch está ligado ao modem/roteador (gateway para internet).

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

A infraestrutura prevê execução de uma **aplicação Flask** (Python) no servidor para o processamento das imagens. Este serviço é interno (`POST /analyze`), chamado apenas pelo Backend Node.js, conforme issue #34 e sub-issues #42–#44.

## DevOps

| Aspecto | Estado |
|---|---|
| CI/CD | `conloq/.github` tem workflow `mash-project-notifications.yml` (notificações de sprint) |
| Testes automatizados | Não implementados (#41) |
| Migrations | Não implementadas (#40) |
| Deploy | Manual (sem pipeline de deploy) |
| Monitoramento | mash_project_notifier (Python, em .github) |
