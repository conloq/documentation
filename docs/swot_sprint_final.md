# Diagnóstico SWOT e Planejamento da Sprint Final

Diagnóstico situacional do Mash na reta final, com a matriz TOWS e o plano de contingência da apresentação.

Projeto Mash, Projeto Integrador III, DSM3, FATEC Registro. Disciplina GAPS, atividade avaliativa AT2 do módulo 11. Data: 29/10/2026.

## 1. Papéis na reta final

| Papel | Integrante | Responsabilidade nesta etapa |
|---|---|---|
| Product Owner | João | Lidera o corte de escopo, blinda o fluxo principal e publica a declaração de alinhamento ([#108](https://github.com/conloq/mash/issues/108)) |
| Scrum Master e facilitador | Haimon | Conduz o diagnóstico, identifica impedimentos, organiza a Milestone e o quadro do Project |
| Desenvolvimento | Haimon e João | Relatam o débito técnico e a viabilidade de entrega de cada funcionalidade |
| Documentação e artefatos | Jocieli | Documento de artefatos, diagramas e índice ([#79](https://github.com/conloq/mash/issues/79), [#53](https://github.com/conloq/mash/issues/53)) |
| Design e conteúdo | Kevin | Telas no Figma, pitch, legendas e banner ([#25](https://github.com/conloq/mash/issues/25) a [#29](https://github.com/conloq/mash/issues/29)) |

## 2. Análise SWOT

### Ambiente interno, sob controle da equipe

**Forças**

- API com JWT e senha guardada em Argon2id, com isolamento por usuário no mesmo 404 ([#38](https://github.com/conloq/mash/issues/38)).
- Receitas e rampas de temperatura ligadas da tela ao banco, sem tela provisória ([#32](https://github.com/conloq/mash/issues/32), [#86](https://github.com/conloq/mash/issues/86)).
- Schema criado por migrations, sem `sync()` como fonte paralela ([#71](https://github.com/conloq/mash/issues/71)).
- API e frontend publicados em ambiente acessível ([#68](https://github.com/conloq/mash/issues/68), [#69](https://github.com/conloq/mash/issues/69)).
- Decisões e recorte do semestre registrados em um só lugar ([#66](https://github.com/conloq/mash/issues/66)).

**Fraquezas**

- Sem testes automatizados. A validação é manual, por exceção registrada e aceita ([#41](https://github.com/conloq/mash/issues/41), [#66](https://github.com/conloq/mash/issues/66)).
- A classificação automática do teste de iodo não existe: não há serviço em Python com OpenCV nem integração do Node com ele, e ficam para o próximo semestre ([#34](https://github.com/conloq/mash/issues/34), [#43](https://github.com/conloq/mash/issues/43), [#44](https://github.com/conloq/mash/issues/44)).
- Lotes ainda não estão na `main` do Back-End, dependem da [#31](https://github.com/conloq/mash/issues/31).
- Os diagramas UML e o documento de artefatos estão atrasados em relação ao código ([#50](https://github.com/conloq/mash/issues/50), [#79](https://github.com/conloq/mash/issues/79)).
- Equipe de quatro pessoas, duas programando.

### Ambiente externo, fora do controle da equipe

**Oportunidades**

- 1.949 cervejarias no Brasil, com crescimento de 5,5% em 2024 (artigo científico, referência [1]).
- EXPOBEER Vale do Ribeira e a produção regional de cerveja artesanal (artigo, referência [2]).
- A banca avalia o fluxo principal, não a funcionalidade fora do recorte (críticas de 09/10, [#66](https://github.com/conloq/mash/issues/66)).
- A simulação do teste de iodo no frontend dispensa OpenCV e imagem real ([#9](https://github.com/conloq/mash/issues/9), [#10](https://github.com/conloq/mash/issues/10), [#66](https://github.com/conloq/mash/issues/66)).

**Ameaças**

- Prazo do depósito em 03/11/2026, inegociável ([#66](https://github.com/conloq/mash/issues/66)).
- Rede do local da apresentação, ainda não testada.
- O plano gratuito do Render desliga a API após 15 minutos sem uso ([#61](https://github.com/conloq/mash/issues/61)).
- A iluminação altera a leitura da cor do iodo, que é a limitação que o produto ataca (artigo científico, referência [11]).

## 3. Matriz TOWS

| Vetor | Fatores cruzados | Ação para a reta final |
|---|---|---|
| **Ofensivo (S × O)** | API autenticada e fluxo receita, rampas e lote ligados ponta a ponta, com banca focada no fluxo principal | Demonstrar o ciclo completo do login ao lote, começando com usuário, receita e lote já cadastrados, que foi o que a banca pediu em 09/10 |
| **Reforço (W × O)** | Ausência de testes automatizados, com banca tolerante a escopo menor | Congelar o escopo e executar um roteiro de validação manual do fluxo nuclear na véspera, registrado na [#41](https://github.com/conloq/mash/issues/41), para não descobrir falha durante a apresentação |
| **Confronto (S × T)** | Deploy publicado no Render, com rede e cota gratuita como ameaça | Manter banco local com migrations aplicadas e dados de demonstração cadastrados, API em `localhost:8080` e frontend em `localhost:4000`; gravar o vídeo do fluxo como plano B |
| **Sobrevivência (W × T)** | Pipeline de visão computacional inexistente (sem serviço Python com OpenCV, sem integração com o Node) e documento de artefatos atrasado, contra prazo de 03/11 | **Corte inegociável:** sai todo o teste de iodo automatizado, ou seja, o serviço Python com OpenCV, a integração com o Back-End, o upload, a análise e o histórico de análises. Entra a simulação de interface já pronta. O documento de artefatos consome a Sprint 6 inteira, sem esperar código novo |

## 4. Plano de contingência da apresentação

1. Antes da banca, cadastrar no banco local um usuário, uma receita com rampas de temperatura e um lote, com o mesmo roteiro que será demonstrado.
2. Conferir na véspera: `npm run db:migrate`, API respondendo em `localhost:8080` e frontend em `localhost:4000`.
3. Se a rede do local falhar, rodar a demonstração inteira no ambiente local.
4. Se o ambiente local falhar, exibir o vídeo gravado do mesmo fluxo, que é a gravação prevista na [#28](https://github.com/conloq/mash/issues/28).

## 5. Corte de escopo resultante

O corte é aplicado no GitHub pela [#108](https://github.com/conloq/mash/issues/108), com etiqueta `scope:wont-have` e Priority Low, e ratificado na declaração do PO.

- **Fluxo nuclear, o único Must Have:** login, receita com rampas de temperatura, lote e teste de iodo na simulação de interface, de ponta a ponta.
- **Entra também na Sprint Final:** documento de artefatos e pitch.
- **Fica fora, por corte de visão computacional:** o teste de iodo automatizado inteiro, isto é, serviço Python com OpenCV ([#43](https://github.com/conloq/mash/issues/43)), integração do Node com o serviço ([#44](https://github.com/conloq/mash/issues/44)), entidade e endpoint de análise ([#1](https://github.com/conloq/mash/issues/1)), upload da imagem ([#33](https://github.com/conloq/mash/issues/33)) e histórico de análises por lote ([#3](https://github.com/conloq/mash/issues/3)).

Este documento é o insumo da declaração de alinhamento do PO, que registra o fluxo demonstrável, a justificativa dos cortes e o plano de contingência.
