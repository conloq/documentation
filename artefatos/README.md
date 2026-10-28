# Artefatos de Projeto de Software - FATEC Registro

Documento LaTeX para apresentação de artefatos de projetos de software do curso de Desenvolvimento de Software Multiplataforma (DSM) da FATEC Registro.

## Características

- Cabeçalho institucional com logos da FATEC, Governo SP e CPS
- Capa padronizada com informações do curso e projeto
- Sumário automático
- Seções separadas em arquivos `.tex`
- Referências ABNT com BibTeX
- Estrutura modular para facilitar manutenção

## Estrutura de Diretórios

```text
artefatos/
|-- artefatos.tex              # Arquivo principal do documento
|-- referencias.bib            # Base bibliográfica
|-- README.md
|-- config/
|   |-- packages.tex           # Pacotes LaTeX
|   |-- colors.tex             # Cores do documento
|   |-- layout.tex             # Layout, cabeçalho e rodapé
|   `-- macros.tex             # Comandos reutilizáveis
|-- frontmatter/
|   |-- capa.tex               # Capa
|   |-- sumario.tex            # Sumário
|   `-- nota-importante.tex    # Texto introdutório
|-- sections/
|   |-- 01-canvas.tex
|   |-- 02-swot.tex
|   |-- 03-ux-ui.tex
|   |-- 04-website.tex
|   |-- 05-uml.tex
|   |-- 06-devops.tex
|   `-- conclusao.tex
|-- backmatter/
|   `-- referencias.tex        # Inclusão da bibliografia
`-- imgs/
    |-- base/                  # Logos e imagens base
    `-- ...
```

## Onde editar cada parte

- Capa: `frontmatter/capa.tex`
- Introdução e observações iniciais: `frontmatter/nota-importante.tex`
- Conteúdo dos artefatos: arquivos em `sections/`
- Referências: `referencias.bib`
- Pacotes, layout e estilo visual: arquivos em `config/`

## Como compilar

Execute na pasta `artefatos`:

```powershell
pdflatex artefatos.tex
bibtex artefatos
pdflatex artefatos.tex
pdflatex artefatos.tex
```

Versão silenciosa:

```powershell
pdflatex -interaction=nonstopmode artefatos.tex | Out-Null
bibtex artefatos
pdflatex -interaction=nonstopmode artefatos.tex | Out-Null
pdflatex -interaction=nonstopmode artefatos.tex | Out-Null
```

## Organização adotada

A estrutura foi separada para evitar um único arquivo muito grande e facilitar:

- edição por seção
- revisão de conteúdo
- reaproveitamento de configuração
- manutenção de capa, layout e bibliografia sem misturar com o texto principal

## Ferramentas recomendadas

- CANVAS: Canvanizer, Miro, Figma
- SWOT: PowerPoint, Google Slides, Miro
- UX/UI: Figma, Adobe XD, Sketch
- Diagramas UML: PlantUML, Draw.io, Lucidchart, StarUML
- DevOps/Infraestrutura: Draw.io, Miro, Cloudcraft

## Limpeza de arquivos temporários

```powershell
Remove-Item *.blg, *.fdb_latexmk, *.fls, *.out, *.log -ErrorAction SilentlyContinue
```

## Recursos adicionais

- [Documentação ABNTeX2](https://www.abntex.net.br/)
- [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX)
- [Overleaf Documentation](https://www.overleaf.com/learn)
- [CTAN - Pacotes LaTeX](https://ctan.org/)
