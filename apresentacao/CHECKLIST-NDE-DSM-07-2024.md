# Checklist: Manual NDE-DSM-07/2024 (alterado em 01/07/2025)

Status: **não declarar conformidade ainda.** Falta confirmar o escopo com o professor e revisar o vídeo.

Verificado em 11/11/2026: compilação sem avisos de transbordo; 10 páginas; nenhum rótulo "a confirmar", "SOBRENOME" ou "Seu Nome" no PDF; revisão visual dos 10 slides em `_versoes/revisao-visual/`.

## Diretrizes dos slides

| Item | Status | Observação |
|---|---|---|
| 1.1 Pouco texto | OK | Listas curtas; tabela do Estado da Arte é o slide mais denso. |
| 1.2 Imagens que complementam a fala | OK | Brassagem, teste do iodo, malte, amido com Lugol, tina de mosturação. |
| 1.3 Numeração, legenda e referência | OK | Figuras 1 a 6, cada uma com legenda e nota. |
| 1.5 Sequência e nomes | **A CONFIRMAR** | Slides 01 a 08 na ordem do manual. Resultados (09) e Conclusão (10) não estão no deck, porque o trabalho do semestre vai até Metodologia. O manual lista essas duas seções: confirmar com o professor. |
| 1.5.3 Pitch de 1 a 2 min | PARCIAL | 1 min 48 s pelos metadados do YouTube. Conteúdo não revisado por mim. |
| 1.6 Sem novas seções | OK | Ferramental está dentro de Metodologia; encerramento dentro de Apresentação prática. |
| 1.7 Sem diagramas, fluxogramas ou telas | OK | Fluxograma e capturas de tela removidos. As telas aparecem só na demonstração ao vivo. |
| 1.9 Template Beamer, mudanças mínimas | OK | Cabeçalho, rodapé, tema e fonte do original preservados. |
| 1.10 Referências em nota de rodapé | OK | Todas as citações e créditos de imagem. |
| 1.11 Sem slide de referências | OK | |

## Procedimentos e postura

| Item | Status |
|---|---|
| 2.1 Cumprimento à banca; 2.2 um membro apresenta a equipe | Haimon (plano de falas) |
| 2.3 Agenda e duração | OK no slide 02 |
| 2.5 Agradecimento final | OK no último slide, fala de Kevin |
| 3.1 Sem material de apoio | Plano de falas é só para ensaio |
| 3.6 Intercalar falas | Haimon → Jocieli → João → Kevin |
| 6.1 Ensaio | **PENDENTE** |

## Precisão científica

| Regra | Status |
|---|---|
| Iodo qualitativo; não mede açúcar | OK (slide 04) |
| Resultado negativo não prova conversão total | OK (o deck não faz essa afirmação) |
| Captura, OpenCV e validação como planejados | OK (slides 06 e 07) |
| Simulação do iodo não apresentada como classificador | OK (slide 08: "leituras simuladas") |
| OpenCV.js como prova de conceito fora do sistema | OK (slide 07, 2) |
| Li et al.: antrona em tabaco, não iodo nem mosto | OK (slide 05) |
| Lacuna restrita aos trabalhos analisados | OK (slide 05) |

## Imagens

| Figura | Arquivo | Fonte e licença | Verificação |
|---|---|---|---|
| 1 | `imgs/produto/logo-mash.png` | Acervo da equipe, `conloq/frontend` (commit 879c7b2) | **A CONFIRMAR**: quem criou o logo e com que ferramenta. Se foi gerado por IA ou derivado de imagem de terceiros, registrar. |
| 2 | `imgs/verificadas/bg-pitch-brassagem.jpg` | Sdgjake, *Coors Mash Tun*, Commons, CC BY-SA 3.0 | SHA-1 do original `b32013df...`; recortada com degradê |
| 3 | `imgs/verificadas/fig1-jodprobe.jpg` | Flo Sorg, *Jodprobe.jpg*, Commons, domínio público | SHA-1 `48a9ee50...` |
| 4 | `imgs/verificadas/bg-objetivo-malte.jpg` | Noralambert, *Carapils Malt for Brewing*, Commons, CC BY-SA 4.0 | SHA-1 do original `2be678e1...`; recortada com degradê |
| 5 | `imgs/verificadas/fig2-lugol-recorte-4x3.jpg` | Aleromjar1403, Commons, CC0 | SHA-1 do original `96488c26...`; recorte 4:3 |
| 6 | `imgs/verificadas/bg-pratica-tina.jpg` | Ekrem Canli, *Brasserie Cantillon's mash tun 2024*, Commons, CC BY-SA 4.0 | SHA-1 do original `440d351c...`; recortada com degradê |

As adaptações das fotos CC BY-SA (recorte e degradê) herdam a mesma licença. As fotos de fundo originais (`imgs/fundo/`) continuam na pasta, fora do PDF, porque não têm autoria registrada.
