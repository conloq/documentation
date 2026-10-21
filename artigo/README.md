# Artigo

Documentação da área Artigo do projeto Mash.

## Responsável

Jocieli Pontes Domingues da Silva

## Repositório do artigo

O artigo científico é gerido fora dos repositórios de código. O PDF atual está disponível como artefato do projeto.

## Arquivos

| Arquivo | Descrição |
|---|---|
| `artigo_main.pdf` | Artigo científico completo (9 páginas, LaTeX; versão de 09/10, com a Figura 1, o fluxograma da plataforma) |
| `artefatos_projeto.pdf` | Artefatos do Projeto de Software (14 páginas: UML, MER, Canvas, Infraestrutura, UX/UI) |

## Recorte vigente

OpenCV e todo o fluxo real do teste de iodo ficam no backlog para outro semestre. Neste semestre permanece somente a simulação no frontend, com cena obrigatória no pitch, sem etiqueta de simulação na cena ([decisão de 21/10/2026, #66](https://github.com/conloq/mash/issues/66)). As metas, o protocolo e as referências abaixo descrevem a proposta científica existente; não são resultados experimentais comprovados. O PDF e os arquivos acadêmicos não foram reescritos nesta atualização documental.

## Artigo científico

**Título:** Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal

**Autores:** Haimon Cugler Vieira, João Alexandre Pinto Camargo, Jocieli Pontes Domingues da Silva, Kevin da Silva Oliveira

**Instituição:** Faculdade de Tecnologia do Estado de São Paulo (FATEC Registro)

### Objetivos específicos (metas propostas para trabalho futuro)

| Objetivo | Meta |
|---|---|
| Acurácia das classificações conclusivas (teste de iodo) | Meta numérica a definir após o estudo piloto |
| Tempo de resposta (envio → resultado) | Média ≤ 2 s; métrica percentílica a definir após a caracterização do protótipo |
| Registro de leituras válidas | 100% com data/hora, temperatura, classificação, tempo |
| Taxa de resultados inconclusivos | ≤ 10% |
| Concordância entre capturas repetidas | ≥ 90% |

### Estado da Arte: Trabalhos relacionados

| Trabalho | Contribuição | Limitação |
|---|---|---|
| Parizotto [6] | Controle térmico PI (sobressinal máximo de 2,54%) | Sem feedback bioquímico |
| Almeida/Ribeiro [4] | Teste de iodo visual (positivo/negativo) | Subjetivo, sem rastreabilidade |
| Li et al. [11] | R²=0,9941 no canal vermelho RGB, recuperação média de 95,72% | Erro relativo médio de 3,83% entre iluminações; matriz vegetal |
| Nyarko et al. [12] | Segmentação HSV para espuma de cerveja | Reflexos no vidro, autofoco e aderência da espuma |

### Lacuna científica

Ausência de soluções integradas que unifiquem: (i) amostragem padronizada, (ii) análise cromática objetiva via visão computacional, (iii) associação ao histórico térmico da mosturação.

### Metodologia

**Arquitetura (4 módulos):** aquisição de dados → processamento de imagem → registro de parâmetros → interface de acompanhamento.

**Protocolo de aquisição:** iluminação controlada, fundo neutro, câmera fixa, alíquota padronizada, controles positivo/negativo por sessão, padrão branco/cinza para balanço de cor.

**Espaços de cor:** HSV e CIELab (a*, b*).

**Classes de classificação:**
1. **Presença de amido**: violeta, azul-escura, arroxeada
2. **Conversão parcial**: tonalidade intermediária entre os controles positivo e negativo
3. **Ausência de amido**: amarela, ambarina

**Validação:** matriz de confusão, acurácia entre classificações conclusivas, precisão, sensibilidade e F1 por classe, taxa de inconclusivos, repetibilidade e tempo de processamento. Validar em bancada antes de ambiente real.

### Decisões relevantes para as issues

- IA generativa NÃO decide o resultado (#34)
- HSV + CIELab propostos (mapeamento em definição pelo Backend)
- ROI a definir nos testes de bancada (#42)
- Limiares finais só após etapa piloto
- Temperatura é contexto, não input do classificador

## Issues da área

O status de cada issue fica no [Project Mash](https://github.com/orgs/conloq/projects/2) e nos épicos, não aqui: [#56](https://github.com/conloq/mash/issues/56) (artigo) e [#37](https://github.com/conloq/mash/issues/37) (artefatos do PI). A #21 (protocolo de validação) foi para o próximo semestre com o OpenCV; a meta mínima de acurácia pedida pela banca está na [#90](https://github.com/conloq/mash/issues/90).

## Referências do artigo

1. Anuário da Cerveja 2025: Ano de Referência 2024 (MAPA, 2025): 1.949 cervejarias no Brasil
2. EXPOBEER Vale do Ribeira (Prefeitura de Registro, 2025)
3. Hornink, *Princípios da Produção Cervejeira e as Enzimas na Mosturação*, 2ª ed. (2024)
4. Almeida e Ribeiro, *Revista Ifes Ciência*, vol. 10, n. 2 (2024)
5. United Nations, *The 17 Goals: Sustainable Development Goals* (2015)
6. Parizotto, TCC de Engenharia Elétrica, UTFPR (2017)
7. Groover, *Automação Industrial e Sistemas de Manufatura*, 3ª ed. (2011)
8. Ogata, *Engenharia de Controle Moderno*, 5ª ed. (2011)
9. Gonzalez e Woods, *Digital Image Processing*, 4ª ed. (2018)
10. Szeliski, *Computer Vision: Algorithms and Applications*, 2ª ed. (2022)
11. Li et al., *Scientific Reports*, vol. 15 (2025)
12. Nyarko et al., *Fermentation*, vol. 7, n. 2 (2021)
13. Bradski, *The OpenCV Library* (2000)
14. OpenCV Team, documentação de processamento de imagem e conversão de espaços de cor (2026)

