# Apresentação da banca: Mash (Beamer)

Pasta padrão da apresentação.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `apresentacao.tex` / `apresentacao.pdf` | Versão atual (10 slides): visual do original restaurado, conteúdo científico corrigido, escopo até Metodologia + demonstração. |
| `CHANGELOG.md` | Mudanças por slide em relação ao original. |
| `PLANO-DE-FALAS.md` | Papéis originais da equipe, tempos e âncoras de memória (só para ensaio). |
| `CHECKLIST-NDE-DSM-07-2024.md` | Verificação contra o manual, a ciência do artigo e as imagens. |
| `_original/` | Original antes de qualquer revisão. |
| `imgs/verificadas/` | Imagens com licença conferida (ver checklist). |
| `imgs/produto/logo-mash.png` | Logo do Mash (usado no slide 01). Outros arquivos de `imgs/fundo/` e `imgs/produto/` ficam fora do repositório: sem autoria verificada, ou não usados. |

## Compilar

```bash
TEXMFHOME=~/texmf-roboto pdflatex apresentacao.tex
TEXMFHOME=~/texmf-roboto pdflatex apresentacao.tex
```

Requer Beamer, `babel` (brazilian), `qrcode` e `roboto`.

## Vídeo do pitch

`https://youtu.be/4jTvFUkc8AM`, não listado, 1 min 48 s (metadados do YouTube). Depende de internet; tenha uma cópia local em mp4 por garantia.

## Precisa de confirmação

Ver o fim da checklist e a resposta no chat.


## Nota de versão

A pasta `_removido/` (slides 09 e 10 retirados por decisão da equipe) não está mais na pasta de trabalho. Para reinserir Resultados e Conclusão, é preciso refazer os slides a partir do histórico desta versão.
