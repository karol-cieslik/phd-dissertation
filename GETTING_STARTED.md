# Getting started with the dissertation template

This is an **unofficial example**, not an approved dissertation format. Before submitting, check the current requirements of your doctoral school or faculty (title page, required statements, language, layout, accessibility, and deposit format). The supplied university, institute, author, and chapter content are examples.

## 1. Make your first PDF

**Online:** Download this GitHub repository as a ZIP, upload/extract its contents into a new Overleaf project, select `K_Cieslik_phd_thesis.tex` as the main document, and use **pdfLaTeX**. Keep the `chapters/`, `figures/`, `library.bib`, and logo files alongside the main document.

**On your computer:** Install a reasonably complete TeX Live or MiKTeX distribution with pdfLaTeX, BibTeX, and `latexmk`. From the directory containing the main file, run:

```sh
latexmk -pdf -file-line-error -interaction=nonstopmode K_Cieslik_phd_thesis.tex
```

`latexmk` normally reruns LaTeX/BibTeX enough times to resolve references. The resulting PDF is `K_Cieslik_phd_thesis.pdf`. Use `latexmk -C` to remove generated build files.

**GitHub:** The Actions workflow also builds a PDF for pull requests and pushes. Open a successful workflow run and download the `phd-dissertation-pdf` artifact. This is useful if your own installation is not configured yet.

## 2. Personalize the title page

Open `K_Cieslik_phd_thesis.tex`. Immediately above the `hyperref` setup, find and replace these fields:

| Field | Meaning |
| --- | --- |
| `\thesisuniversity`, `\thesisinstitute`, `\thesisdepartment` | Institutional names as approved by your school |
| `\thesistitle` | Dissertation title (also becomes the PDF title) |
| `\thesisauthor` | Your name (also becomes the PDF author) |
| `\thesissupervisor` | Supervisor's name and title |
| `\thesiscityyear` | Place and year |

The current image `uj_logo.jpg` is an example. Replace or remove it according to the institution's instructions, and confirm you may use the selected mark. Test long titles: all title-page content should stay on **one A4 page**.

**Important:** The declaration page deliberately contains a visible placeholder. Insert only the declaration text officially required for your degree. Do not submit placeholder wording or sample signatures.

## 3. Write and reorder chapters

- Edit the files in `chapters/`. For example, `chapters/introduction.tex` begins with `\chapter{Introduction}`. Each chapter file is included by `K_Cieslik_phd_thesis.tex`.
- Rename files if you wish, then update the matching `\include{chapters/your-name}` line in the main file. Filename capitalization must match exactly on Linux/Overleaf.
- Add a new file, for example `chapters/discussion.tex`, with `\chapter{Discussion}` and add `\include{chapters/discussion}` before the conclusion. Do **not** put another `\documentclass`, `\begin{document}`, or `\end{document}` inside a chapter.
- Remove sample chapters you do not need, and revise the front-matter `\include` lines if you do not require two languages, acknowledgements, or acronyms. Be careful to remove or change the corresponding table-of-contents lines.
- The front matter uses roman page numbers; the main chapters start again at Arabic page 1. Leave the `\clearpage` before `\pagenumbering{arabic}` in place.

## 4. Copyable examples

### Section and cross-reference

Add the label after the heading, then refer to it using `\ref`:

```latex
\section{Measurement procedure}\label{sec:measurement}
The calibration procedure is described in Section~\ref{sec:measurement}.
```

### Figure

Place your image at `figures/experimental/my-setup.png` first:

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=0.8\linewidth]{figures/experimental/my-setup.png}
  \caption{Experimental arrangement. Explain any symbols or panels here.}
  \label{fig:setup}
\end{figure}

Figure~\ref{fig:setup} shows the apparatus.
```

Let LaTeX place floating figures; `[htbp]` gives it reasonable options. If a figure exceeds the printable area, reduce its width. Prefer PDF/vector graphics for plots and high-resolution raster images for photographs.

### Citations and bibliography

Put an entry such as `@article{MyKey2026, ...}` in `library.bib`, then cite it:

```latex
This result is consistent with earlier work~\cite{MyKey2026}.
```

The project uses **BibTeX** with the `ieeetr` bibliography style, not `biblatex`/Biber. The existing `Cie2022` entry is an example. Avoid including local file paths exported by reference managers; they are unnecessary for bibliography generation.

### Equations, chemistry, and SI units

```latex
\begin{equation}
  E = h\nu
  \label{eq:photon}
\end{equation}
The photon energy in Equation~\ref{eq:photon} is measured in
\SI{1.5}{\electronvolt}. The sample was heated to
\SI{300}{\degreeCelsius}; the oxide is written \ce{TiO2}.
```

`amsmath` supplies equation environments; `siunitx` formats units and numbers; `mhchem` supplies `\ce` for chemical formulas/reactions.

### Small table with aligned numbers

```latex
\begin{table}[htbp]
  \centering
  \caption{Example measurements.}
  \label{tab:values}
  \begin{tabular}{l S[table-format=2.1]}
    \toprule
    Sample & {Energy (\si{\electronvolt})} \\
    \midrule
    A & 1.2 \\
    B & 12.5 \\
    \bottomrule
  \end{tabular}
\end{table}
```

`booktabs` provides the three horizontal rules; the `S` column from `siunitx` aligns numbers. See `chapters/experimental.tex` for more elaborate tables, including a rotated full-page table.

### Acronyms

Define an acronym in `chapters/acronyms.tex`, for example `\acro{AES}{Auger electron spectroscopy}`, then use `\ac{AES}` in a chapter. The first use expands the term and later uses abbreviate it.

## 5. What are the packages for?

These packages are already loaded in `K_Cieslik_phd_thesis.tex`. Add others only when a real need arises; extra packages increase the chance of conflicts.

| Package | Purpose |
| --- | --- |
| `geometry` | A4 size and mirrored print/binding margins |
| `babel`, `fontenc`, `microtype` | English/Polish language support, font encoding, and text microtypography |
| `indentfirst` | Indent the first paragraph after a heading |
| `amsmath` | Equations and mathematical alignment |
| `mhchem` | Chemical formulas and reactions with `\ce` |
| `siunitx` | Consistent scientific units and numeric table columns |
| `graphicx`, `rotating` | Figures and landscape/sideways floats |
| `caption`, `booktabs`, `threeparttable` | Captions, clean tables, and table notes |
| `enumitem`, `acronym` | Lists and abbreviations |
| `fancyhdr`, `titlesec`, `xcolor` | Page headers, headings, and theme color |
| `hyperref` | PDF links, bookmarks, and document metadata |
| `lipsum` | **Sample filler text only:** remove it when no examples need it |

Advanced writers might choose `cleveref` for smarter cross-references, `glossaries-extra` for a complex glossary, or `tikz` for programmatic graphics. These are **not required** for the template and may involve extra configuration. Switching from BibTeX to `biblatex`/Biber changes the build and bibliography code; do not just load both systems.

## 6. Troubleshooting

| Symptom | First thing to check |
| --- | --- |
| `File ... not found` | Path, filename capitalization, and whether the file is present |
| `Undefined control sequence` | Typo or missing package; find the first occurrence in the `.log` |
| Citation or reference shows `?` | Check the citation key/label; rebuild with `latexmk` |
| `*.sty not found` | Install the named LaTeX package in your TeX distribution; a minimal install may be insufficient |
| `Overfull \hbox` | Inspect the indicated line, long URL, equation, or table; verify the final PDF visually |
| A very long title spills to a new page | Reduce title text or logo size/spacing in the `titlepage` block, then check the result |
| On-screen PDF looks different from printed pages | Confirm A4 output, margins, font embedding, print scaling, and grayscale contrast |

When something fails, read the **first actual error** in the log rather than the last generic “build failed” line. Do not solve page overflow by globally shrinking everything; address the offending content.

## 7. Before circulating or submitting

- Replace **all** placeholder institutional names, title details, filler text, sample figures, demonstration citations, acronyms, dates, and declaration wording.
- Verify the doctoral school's up-to-date submission rules. This repository does not guarantee compliance, nor does successful compilation.
- Review PDF pages individually for overflowing figures/tables, headings left at page bottoms, mixed page numbering, TOC entries, bookmarks, and legibility.
- Confirm which images, institutional marks, third-party text, and fonts you have permission to redistribute.
- Do not treat a successful CI run as a substitute for proofreading and an official formatting check.
