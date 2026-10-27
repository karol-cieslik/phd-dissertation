# PhD dissertation template (LaTeX)

An unofficial, editable starting point for a physics dissertation. It demonstrates a two-sided thesis layout, bilingual English/Polish front matter, scientific notation, figures, tables, citations, and an appendix.

This is a personal template, not an official Jagiellonian University template. University and faculty requirements change and may differ by discipline. Check the current instructions from your doctoral school or faculty before submitting a thesis. In particular, confirm the required title-page wording, margins, pagination, spacing, and accessibility rules.

## First-time users

1. Download or clone this repository, or upload the ZIP to an Overleaf project.
2. Compile `K_Cieslik_phd_thesis.tex` using pdfLaTeX.
3. Edit the `\thesistitle`, `\thesisauthor`, and other clearly marked fields in the main file.
4. Replace the **placeholder declaration**, example chapters, figures, and references before using it for real work.

**[Read the student-friendly getting-started guide](GETTING_STARTED.md)** for copyable examples of figures, cross-references, equations, SI units, citations, tables, acronyms, and troubleshooting.

## Build the PDF

Use a current TeX Live or MiKTeX installation with latexmk, BibTeX, and the packages loaded in the main file. From the repository root, run:

```sh
latexmk -pdf -file-line-error -interaction=nonstopmode K_Cieslik_phd_thesis.tex
```

`latexmk` handles the repeated LaTeX/BibTeX passes required for cross-references and citations. To remove generated build files:

```sh
latexmk -C
```

The GitHub Actions workflow also builds the thesis on each push and publishes the resulting PDF as a downloadable workflow artifact.

## Project structure

- K_Cieslik_phd_thesis.tex — document setup, title page, declaration, front matter, table of contents, bibliography, and chapter order.
- chapters/*.tex — editable sample chapters and front matter. Replace the placeholder text and remove sections you do not need.
- figures/ — sample figures referenced by the chapters.
- library.bib — BibTeX references. Add entries here and cite them with \cite{...}.

The preamble is grouped by purpose: page layout; language and typography; maths, chemistry, and units; figures and tables; page styling; and links. Remove optional subject-specific packages only after checking that no example chapter uses them.

## Design choices

The refreshed layout keeps a restrained serif body, clear chapter and section hierarchy, generous binding-side margin for two-sided printing, consistent running heads, and a muted ink-blue accent for headings and links. Figures and tables should remain legible at print size, use descriptive captions, and stay within the text area. The accent color may be changed to black if required for print or institutional submission.

The exact layout is deliberately easy to adapt. The current values are examples, not a claim of compliance with any university's rules.
