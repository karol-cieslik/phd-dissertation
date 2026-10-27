# Build and verify the dissertation template

This repository uses **pdfLaTeX and BibTeX**. The root document is `K_Cieslik_phd_thesis.tex`. Run all commands from the repository root.

## Overleaf

1. Create a new Overleaf project from this repository's files.
2. In the project settings, select **pdfLaTeX** and set `K_Cieslik_phd_thesis.tex` as the main document.
3. Recompile. Overleaf normally invokes BibTeX as needed for the bibliography.

The repository's source examples use both English and Polish. For an English main document the last option in `\usepackage[polish,english]{babel}` is `english`; switch the active language deliberately if writing the thesis in Polish.

## Local build

Install a full TeX distribution or at least pdfLaTeX, BibTeX, `latexmk`, Latin Modern fonts, Polish Babel support, and the required LaTeX packages (including `mhchem`, `siunitx`, `microtype`, `caption`, `rotating`, `acronym`, `threeparttable`, `hypcap`, and `titlesec`).

On Debian/Ubuntu systems with appropriate repositories enabled, the relevant TeX Live collections are typically:

```sh
sudo apt-get install latexmk texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texlive-lang-polish texlive-science
```

Build with:

```sh
latexmk -pdf -interaction=nonstopmode -halt-on-error -file-line-error K_Cieslik_phd_thesis.tex
```

`latexmk` handles repeated LaTeX passes and runs BibTeX when required. To remove generated build files, use `latexmk -c` (which normally keeps the PDF).

## Expected output

The build should produce `K_Cieslik_phd_thesis.pdf` using **A4** pages with mirrored inner/outer margins suitable for two-sided printing. The sample should include the title page, bilingual front matter, contents, example chapters, figures, tables, bibliography, and appendix.

CI compiles from scratch, rather than relying on the historical PDF and auxiliary files already tracked by this repository.

## Troubleshooting

- **File `*.sty` not found:** install the relevant TeX Live/MiKTeX package collection; see the list above.
- **Missing figure or chapter:** verify the path and capitalization exactly. Linux is case-sensitive.
- **References or citations show `??`:** use `latexmk` for all necessary LaTeX/BibTeX passes.
- **A package update breaks a command:** report the compiler, TeX distribution/version, exact error, and a minimal reproduction.

The older committed example PDF was generated with MiKTeX in 2023. Do not use it as evidence that the latest source has passed the current build; consult the GitHub Actions build result.
