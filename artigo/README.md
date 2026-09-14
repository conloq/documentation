# Artigo

Documentação da área Artigo do projeto Mash.

## Responsável

Jocieli Pontes Domingues da Silva

## Repositório do artigo

O artigo científico é gerido fora dos repositórios de código. O PDF atual está disponível como artefato do projeto.

## Arquivos

| Arquivo | Descrição |
|---|---|
| `artigo_main.pdf` | Artigo científico completo (9 páginas, LaTeX) |
| `artefatos_projeto.pdf` | Artefatos do Projeto de Software (14 páginas: UML, MER, Canvas, Infraestrutura, UX/UI) |

## Artigo científico

**Título:** Plataforma de Monitoramento da Etapa de Mosturação na Fabricação de Cerveja Artesanal

**Autores:** Haimon Cugler Vieira, João Alexandre Pinto Camargo, Jocieli Pontes Domingues da Silva, Kevin da Silva Oliveira

**Instituição:** Faculdade de Tecnologia do Estado de São Paulo (FATEC Registro)

### Objetivos específicos (metas)

| Objetivo | Meta |
|---|---|
| Acurácia das classificações conclusivas (teste de iodo) | ≥ 50% |
| Tempo de resposta (envio → resultado) | Média ≤ 2s, P60 ≤ 10s |
| Registro de leituras válidas | 100% com data/hora, temperatura, classificação, tempo |
| Taxa de resultados inconclusivos | ≤ 10% |
| Concordância entre capturas repetidas | ≥ 90% |

### Estado da Arte — Trabalhos relacionados

| Trabalho | Contribuição | Limitação |
|---|---|---|
| Parizotto [5] | Controle térmico PI (sobresignal < 2.54%) | Sem feedback bioquímico |
| Almeida/Ribeiro [4] | Teste de iodo visual (positivo/negativo) | Subjetivo, sem rastreabilidade |
| Li et al. [8] | R²=0.9941 canal vermelho RGB, recuperação 95.72% | Erro ~20%, matriz vegetal |
| Nyarko et al. [9] | Segmentação HSV para espuma de cerveja | Sensível a iluminação |

### Lacuna científica

Ausência de soluções integradas que unifiquem: (i) amostragem padronizada, (ii) análise cromática objetiva via visão computacional, (iii) associação ao histórico térmico da mosturação.

### Metodologia

**Arquitetura (4 módulos):** aquisição de dados → processamento de imagem → registro de parâmetros → interface de acompanhamento.

**Protocolo de aquisição:** iluminação controlada, fundo neutro, câmera fixa, alíquota padronizada, controles positivo/negativo por sessão, padrão branco/cinza para balanço de cor.

**Espaços de cor:** HSV e CIELab (a*, b*).

**Classes de classificação:**
1. **Presença de amido** — violeta, azul-escura, arroxeada
2. **Conversão parcial** — marrom, acinzentada, transição
3. **Ausência de amido** — amarela, ambarina

**Validação:** matriz de confusão, acurácia, sensibilidade, especificidade, taxa de inconclusivos, repetibilidade, tempo de processamento. Validar em bancada antes de ambiente real.

### Decisões relevantes para as issues

- IA generativa NÃO decide o resultado (#34)
- HSV + CIELab propostos (mapeamento em definição pelo Backend)
- ROI a definir nos testes de bancada (#42)
- Limiares finais só após etapa piloto
- Temperatura é contexto, não input do classificador

## Issues ativas (Artigo)

| Issue | Título | Status |
|---|---|---|
| #15 | Fundamentar o processamento digital de imagens | In review |
| #16 | Fundamentar Visão Computacional aplicada ao teste de iodo | In review |
| #17 | Documentar OpenCV, espaço de cor e parâmetros | In review |
| #19 | Ampliar e registrar o Estado da Arte | Backlog |
| #20 | Criar fluxograma rastreável do método | Ready |
| #21 | Planejar protocolo de validação experimental | In review |
| #37 | Consolidar e manter os artefatos do Projeto de Software | Backlog |
| #50 | Atualizar UML e MER | Backlog |
| #51 | Atualizar documentação de infraestrutura | Backlog |
| #52 | Completar Canvas e criar SWOT | Backlog |
| #53 | Criar índice de artefatos e Diário de Bordo | Backlog |

## Referências do artigo

1. Anuário da Cerveja 2025 (MAPA, 2025) — 1949 cervejarias no Brasil
2. EXPOBEER Vale do Ribeira (Prefeitura de Registro, 2025)
3. Hornink, *Princípios da Produção Cervejeira e as Enzimas na Mosturação* (2024)
4. Almeida/Ribeiro, *Revista Resciência* vol. 10 (2024)
5. Parizotto, TCC Engenharia Elétrica UTFPR (2017)
6. Groover, *Automação Industrial* (2014)
7. Ogata, *Engenharia de Controle Moderno* (2010)
8. Li et al., *Scientific Reports* vol. 15 (2025)
9. Nyarko et al., *Fermentation* vol. 7 (2021)
10. Bradski, *The OpenCV Library* (2000)
