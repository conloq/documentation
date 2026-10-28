# Índice de artefatos do Projeto de Software

Estado conferido em 24/10/2026. A situação de cada entrega aponta para sua issue, que continua sendo a fonte do status e do escopo. Os arquivos originais ficam em seus repositórios e áreas de origem; este índice não os duplica.

| Artefato | Arquivo | Versão (data) | Responsável | Issue | Situação |
|---|---|---|---|---|---|
| Diário de Bordo, Sprints 1 a 4 | [conloq/logbook-backup/diario-de-bordo](https://github.com/conloq/logbook-backup/tree/main/diario-de-bordo), PRs #1–#4 | 24/10/2026; histórico das Sprints 1–4 mesclado | Equipe, geração pela automação | [#96](https://github.com/conloq/mash/issues/96) | entregue |
| Diário de Bordo, Sprints 5 e 6 | [conloq/logbook-backup/diario-de-bordo](https://github.com/conloq/logbook-backup/tree/main/diario-de-bordo), aguardando geração/revisão | 24/10/2026; Sprint 5 prevista após 30/10 | Equipe, geração pela automação | [#96](https://github.com/conloq/mash/issues/96) | planejado |
| Diagramas UML: casos de uso, classes e objetos | `conloq/documentation`, arquivos editáveis e exportações previstos na issue | 24/10/2026; arquivos não encontrados na main | Jocieli | [#50](https://github.com/conloq/mash/issues/50) | planejado |
| MER do banco | [diagrama_mer_mash.mmd](https://github.com/conloq/database/blob/main/diagrama_mer_mash.mmd) e [diagrama_mer_planejado.mmd](https://github.com/conloq/database/blob/main/diagrama_mer_planejado.mmd); [PR #10 mesclado](https://github.com/conloq/database/pull/10) | 24/10/2026; PR #10 mesclado na `main` | Jocieli, com atualização preparada por Haimon | [#87](https://github.com/conloq/mash/issues/87) | em revisão |
| Canvas e análise SWOT | `conloq/documentation`; artefatos ainda não encontrados na main | 24/10/2026 | Jocieli | [#52](https://github.com/conloq/mash/issues/52) | planejado |
| Infraestrutura de rede e implantação | [infraestrutura/README.md](../infraestrutura/README.md); topologia e endereços descritos como proposta, com o ambiente local e o publicado na seção Ambiente do depósito | 28/10/2026; Pull Request da [#51](https://github.com/conloq/mash/issues/51) | Jocieli | [#51](https://github.com/conloq/mash/issues/51) | em revisão |
| UI de alta fidelidade no Figma | Figma da equipe; referências de cada quadro dispensadas nas issues | 23/10/2026; issues #75 e #78 fechadas | Kevin | [#75](https://github.com/conloq/mash/issues/75), [#78](https://github.com/conloq/mash/issues/78) | entregue |
| Interfaces do website no ambiente publicado | Capturas do frontend publicado; ainda não verificadas | 24/10/2026; publicação pendente | Haimon | [#69](https://github.com/conloq/mash/issues/69) | planejado |
| Pitch de 1 a 2 minutos, com legendas em português e inglês | Vídeo, arquivos SRT e trilha final; ainda não entregues | 24/10/2026 | Kevin | [#25](https://github.com/conloq/mash/issues/25), [#26](https://github.com/conloq/mash/issues/26), [#27](https://github.com/conloq/mash/issues/27) | planejado |
| Artigo científico | [artigo/artigo_main.pdf](../artigo/artigo_main.pdf) | 23/10/2026; publicado. #56 encerrada com exceções aceitas no comentário de fechamento | Haimon e Jocieli | [#56](https://github.com/conloq/mash/issues/56) | entregue |
| Documento consolidado dos artefatos do projeto | [artigo/artefatos_projeto.pdf](../artigo/artefatos_projeto.pdf); cópia antiga, não comprova o DoD atual da #79 | 14/09/2026; oito seções finais ainda pendentes | Jocieli | [#79](https://github.com/conloq/mash/issues/79) | planejado |

## Evidências e limites

- O PR #10 foi mesclado em 24/10/2026 na `main` de `conloq/database`; o MER implementado representa as três tabelas migradas. `lots` aguarda a migration da #31, por isso a entrega completa da #87 continua em revisão.
- O README de infraestrutura separa a proposta de rede física do ambiente publicado: a topologia e o endereçamento continuam como proposta, e o depósito está descrito com as URLs do Render e as evidências das #68 e #69. As capturas de interface dependem da publicação na #69.
- O PDF consolidado existente é anterior à SWOT, ao Diário de Bordo das Sprints 5 e 6 e às capturas do ambiente publicado. Não é a entrega final da #79.
- A #96 registra as Sprints 1–4 mescladas no histórico. A geração da Sprint 5 e a primeira execução agendada continuam pendentes.
