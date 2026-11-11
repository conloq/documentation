# Templates da FATEC Registro

Cópias dos templates oficiais usados pela equipe, para que a documentação possa ser recompilada sem depender do GitHub. São mantidos pelo professor responsável; a equipe não altera o conteúdo destas pastas.

| Pasta | Uso | Origem | Commit copiado | Licença |
|---|---|---|---|---|
| `paper/` | Artigo científico (LaTeX) | [fbamuniz/template-paper-f299](https://github.com/fbamuniz/template-paper-f299) | `b1ed5b8` (09/02/2026) | MIT, Fred Barbosa |
| `artefatos/` | Artefatos do projeto de software (LaTeX) | [fbamuniz/template-artefacts-f299](https://github.com/fbamuniz/template-artefacts-f299) | `0d26885` (09/02/2026) | MIT, Fred Barbosa |
| `beamer/` | Apresentação Beamer | [fbamuniz/template-beamer-f299](https://github.com/fbamuniz/template-beamer-f299) | `b3011bd` (09/02/2026) | MIT, Fred Barbosa |

## O que foi excluído da cópia

- Arquivos de compilação (`.aux`, `.bbl`) e os PDFs de exemplo gerados pelo template. Os exemplos já estão em `../artigo/` (`artigo_template_exemplo.pdf`, `artefatos_template_exemplo.pdf` e `apresentacao_pitch.pdf`).
- Diretório `.git`.

## Como compilar

Cada pasta é independente. Exemplo com o template de Beamer:

```bash
cd templates/beamer
pdflatex apresentacao.tex
pdflatex apresentacao.tex
```

O pacote `roboto` é necessário para o tema. A apresentação da equipe usa uma cópia adaptada deste template em [`../apresentacao/`](../apresentacao/README.md).

## Relação com os documentos da equipe

- `../apresentacao/apresentacao.tex`: derivado de `beamer/`, com as alterações listadas em `../apresentacao/CHANGELOG.md`.
- `../artefatos/`: projeto LaTeX da equipe (ver `../artefatos/README.md`).
- `../artigo/`: artigo final em PDF, gerido fora deste repositório (ver `../artigo/README.md`).
