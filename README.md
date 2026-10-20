# NKU Beamer Template

<p align="center">
    <a href="README.md"><img src="https://img.shields.io/badge/README-English-blue" alt="README"></a>
    <a href="README-zh.md"><img src="https://img.shields.io/badge/README-%E4%B8%AD%E6%96%87-red" alt="README-zh"></a>
    <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License">
</p>

A LaTeX Beamer template for academic presentations at **Nankai University** (南开大学), with a *Nankai Purple* palette, Chinese and English typesetting, and computer science examples.

## Preview

See [main.pdf](main.pdf) for the compiled example and [main.tex](main.tex) for its source.

## Features

- **Nankai Purple** (南开紫) color palette
- **16:9 widescreen** layout with university logo, emblem, and motto assets
- **Chinese, English, and mixed-language text** via `ctexbeamer` and XeLaTeX
- **Adaptive section navigation**: current section highlighted, other sections dimmed
- **Adaptive footline**: institution, short title, presenter, and current/total frame numbers
- A bottom **presentation progress bar**
- **Seven custom boxes**: general purpose, theorem, definition, lemma, proof, remark, and highlight
- **Small frame-level citation footnotes**, including citations inside custom boxes
- **CS examples**: mathematics, pseudocode, code, tables, subfigures, diagrams, and plots
- Automatic section TOCs, bibliography, thank-you slide, and separately numbered appendix

## Project Structure

```text
NKU-Beamer-Template/
├── main.tex                        # Main presentation source
├── main.pdf                        # Compiled preview
├── references.bib                  # BibTeX-format bibliography database
├── resources/
│   ├── NKU.png                     # University emblem and wordmark (title page)
│   ├── NK-Emblem.png               # Circular emblem (frame titles and closing page)
│   └── NK-Motto.png                # Motto image (title page)
├── style/
│   ├── beamerthemeNankai.sty        # Theme loader and resource path
│   ├── beamercolorthemeNankai.sty   # Color definitions
│   ├── beamerfontthemeNankai.sty    # Font sizes and styles
│   ├── beamerinnerthemeNankai.sty   # Title page, standard blocks, custom boxes
│   ├── beamerouterthemeNankai.sty   # Navigation, footline, progress bar
│   └── nankaibib.sty                # Frame-level citation footnotes
├── README.md
├── README-zh.md
└── LICENSE
```

## Getting Started

Download a ready-to-use ZIP from [Releases](https://github.com/InfinityUniverse0/NKU-Beamer-Template/releases). Each package contains the template source, theme, images, bibliography, documentation, license, and a freshly compiled `main.pdf`. Extract it and compile from the extracted directory, or upload the ZIP to Overleaf and select **XeLaTeX**.

### Prerequisites

Use a recent **TeX Live**, **MacTeX**, or **MiKTeX** installation with **XeLaTeX** and **Biber**. The validation environment is TeX Live 2024 with Beamer 3.71.

The example uses:

- Theme/fonts: `ctex`, `beamer`, `tikz`, `tcolorbox`, `calligra`
- Mathematics: `amsmath`, `amssymb`, `amsfonts`, `mathtools`, `bm`
- Algorithms/code: `algorithm2e`, `listings`
- Tables/figures/numbers: `booktabs`, `multirow`, `array`, `makecell`, `tabularx`, `subcaption`, `pgfplots`, `siunitx`
- Bibliography/appendix: `biblatex`, `appendixnumberbeamer`
- Optional build automation: `latexmk`

A full TeX distribution includes these packages; with a smaller installation, install missing packages through its package manager. Keep Biber and biblatex from compatible distribution releases. The example uses ctex's default font selection, which chooses Chinese fonts for the local system. Font appearance may therefore differ between operating systems. For a consistent appearance across machines, install the same fonts on each machine and select them explicitly (see below). `listings` does not require shell escape or an external syntax highlighter.

### Compilation

Run from the repository root:

```bash
latexmk -xelatex main.tex
```

Or compile manually:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

The `.bib` file uses **BibTeX database syntax**, but the processor is **Biber**, as configured by `backend=biber`. Use `biber main`, not `bibtex main`. Repeated XeLaTeX runs resolve navigation, cross-references, and frame totals; `latexmk` handles the steps automatically.

On Overleaf, upload the complete project, select `main.tex` as the main document, and choose **XeLaTeX**.

### Quick Start

1. Clone the repository:

   ```bash
   git clone https://github.com/InfinityUniverse0/NKU-Beamer-Template.git
   cd NKU-Beamer-Template
   ```

2. Edit the metadata in `main.tex`:

   ```latex
   \title[Short Title]{Your Full Presentation Title}
   \subtitle{Seminar or Conference}
   \author[Your Name]{Your Name}
   \institute[Nankai University]{Nankai University\quad College of Computer Science}
   \date{October 20, 2026}
   ```

3. Replace the example frames and bibliography entries, then compile. The optional arguments in square brackets provide the shorter text used in the footline.

### Chinese and English Documents

A minimal English presentation, keeping the supplied `style/` and `resources/` directories:

```latex
\documentclass[aspectratio=169,UTF8]{ctexbeamer}
\makeatletter
\providecommand*\input@path{}
\g@addto@macro\input@path{{style/}}
\makeatother
\usetheme{Nankai}
\title[Short Title]{An Academic Presentation}
\author[Your Name]{Your Name}
\institute[Nankai University]{Nankai University}
\date{October 20, 2026}
\begin{document}
\begin{frame}[plain,noframenumbering]
  \titlepage
\end{frame}
\section[Introduction]{Introduction and Motivation}
\begin{frame}{Research Question}
  English and Chinese text can coexist: 南开大学。
\end{frame}
\end{document}
```

The same class options support Chinese, English, and mixed-language presentations. For Chinese content, replace the visible text:

```latex
\documentclass[aspectratio=169,UTF8]{ctexbeamer}
% Keep the theme-loading code from the example above.
\title[汇报简称]{你的学术汇报标题}
\author[姓名]{你的姓名}
\institute[南开大学]{南开大学\quad 计算机学院}
\date{2026 年 10 月 20 日}
```

No language switch is needed between Chinese and English text or frames. The default `scheme=chinese` uses Chinese conventions for automatic labels and dates, such as `图`, `表`, and `\today`. Optionally add `scheme=plain` to the class options to retain standard Beamer conventions (typically English). Chinese text remains supported with either scheme. This is a document-wide style choice, not a text-language switch; it does not translate manually written frame titles, section names, or box titles. For mixed-language slides, choose one consistent convention for the presentation and write each frame in the desired language. Package configuration, code styling, and automatic section TOCs are provided in `main.tex`; they are not all enabled by `\usetheme{Nankai}` alone.

### Font Choices

The example does not force a font set. For presentations, a clean sans-serif Chinese font usually works well because Beamer uses sans-serif text by default:

- **macOS:** PingFang SC is a good alternative to the default Chinese fonts.
- **Across Windows, macOS, and Linux:** Source Han Sans SC or Noto Sans CJK SC provides a consistent appearance when installed on every machine.

For example, after the document class, select PingFang on a Mac where it is installed:

```latex
\setCJKsansfont{PingFang SC}[BoldFont={PingFang SC Semibold}]
```

Or select an installed Source Han Sans family:

```latex
\setCJKsansfont{Source Han Sans SC}[BoldFont={Source Han Sans SC Bold}]
```

These commands change Chinese sans-serif text; Latin and math fonts remain separately configurable. On systems without Chinese system fonts, ctex may choose Fandol automatically; `fontset=fandol` can also be used explicitly as a portability fallback. It is not required for bilingual typesetting.

## Customization

### Color Palette

| Name | RGB | Hex | Usage |
|---|---|---|---|
| `NKPurple` | 122, 24, 84 | `#7A1854` | Primary accent, links, rules |
| `NKPurpleDark` | 86, 16, 59 | `#56103B` | Emphasis and subtitles |
| `NKPurpleLight` | 162, 72, 124 | `#A2487C` | Secondary accents and dividers |
| `NKPurpleVeryLight` | 245, 238, 242 | `#F5EEF2` | Tinted backgrounds |
| `NKGray` | 160, 160, 160 | `#A0A0A0` | Secondary text |
| `NKDarkGray` | 80, 80, 80 | `#505050` | Alternative body text |
| `NKLightGray` | 230, 230, 230 | `#E6E6E6` | Light rules and progress track |

Colors are defined in `style/beamercolorthemeNankai.sty`. Override them after loading the theme, for example with `\definecolor{NKPurple}{RGB}{122,24,84}`.

### Navigation and Footline

Sections use their natural text widths, with remaining space distributed between them. An overwide navigation row is scaled to fit. The current section is highlighted; other sections are dimmed. Give long section names concise navigation labels:

```latex
\section[Methods]{Retrieval-Augmented Knowledge Extraction Methods}
```

The footline starts with widths of **18% / 36% / 20% / 10%** of the page for institution / title / author / frame count. A field expands beyond its default to fit its content. When space runs out, unused default space is reclaimed; if the row still does not fit, it is scaled down. Short metadata helps preserve readability:

```latex
\title[Knowledge Extraction]{A Long and Detailed Presentation Title}
\author[A. Researcher]{Alice Researcher}
\institute[Nankai University]{Nankai University\quad College of Computer Science}
```

Numbers follow **Beamer's frame counter**, which need not match the physical PDF page count. Overlays share a frame number; each continuation page created by `allowframebreaks` increments the frame counter. In `main.tex`, title and thank-you frames use `[plain,noframenumbering]`; TOC and bibliography frames count toward the main total. `[plain]` hides the navigation and footline but does not by itself exclude a frame from numbering.

With `appendixnumberbeamer`, frames after `\appendix` have separate appendix counts and do not increase the main total. Appendix navigation follows sections defined in the appendix; without an appendix section, the navigation row is empty.

### Custom Environments

All seven environments accept optional `tcolorbox` keys. Use `title={...}` for a Chinese or English title, `title={}` to omit a default title, and keys such as `colback` to adjust appearance. These boxes do not automatically number theorems or split content across Beamer frames.

```latex
\begin{nkbox}[title={Research Question}]
  State the scope and assumptions of the task.
\end{nkbox}

\begin{nkdefinition}[title={Definition: Candidate Set}]
  Define the objects used in the method.
\end{nkdefinition}

\begin{nktheorem}[title={Theorem}]
  State a result together with its assumptions.
\end{nktheorem}

\begin{nklemma}[title={Lemma}]
  State a supporting result.
\end{nklemma}

\begin{nkproof}[title={Proof}]
  Give the argument for the stated result.
\end{nkproof}

\begin{nkremark}[title={Implementation Note}]
  Explain a practical consideration.
\end{nkremark}

\begin{nkhighlight}
  Emphasize the key takeaway.
\end{nkhighlight}
```

Place each example in a frame with enough space for its content. Standard Beamer `block`, `exampleblock`, and `alertblock` environments are also styled by the theme.

### Footnote Citations

Load the helper **after** biblatex, using the `style/` search path above:

```latex
\usepackage[backend=biber,style=numeric-comp,sorting=none,
            maxbibnames=2,giveninits=true,
            doi=false,isbn=false,url=false]{biblatex}
\addbibresource{references.bib}
\usepackage{nankaibib}
```

Use `\footfullcite` in frame body text or inside a custom box to place a full reference in a small footnote:

```latex
\begin{frame}{Related Work}
  \begin{nkbox}[title={Retrieval-Augmented Generation}]
    Retrieval supplies external context for generation.\footfullcite{lewis2020rag}
  \end{nkbox}
\end{frame}
```

The helper preserves biblatex's optional prenote/postnote arguments and comma-separated keys:

```latex
\footfullcite[pp.~1--2]{lewis2020rag}
\footfullcite[See][pp.~1--2]{lewis2020rag}
\footfullcite{bordes2013translating,lewis2020rag}
```

Citations work in normal frames, custom boxes, columns, and `[plain]` frames. Footnote numbers run continuously through the document. Use citations in frame content rather than titles, section names, or other moving arguments. Footnotes occupy normal frame space, so a frame with several full references needs less body content. `\cite{key}` remains an inline numeric citation. To collect cited works at the end:

```latex
\begin{frame}[allowframebreaks]{References}
  \printbibliography[heading=none]
\end{frame}
```

### Code Listings

`main.tex` configures Nankai-themed `listings` colors. Frames containing verbatim code must use `[fragile]`:

```latex
\begin{frame}[fragile]{Code Example}
  \begin{lstlisting}[language=Python,caption={Greeting}]
def hello():
    print("Hello, Nankai!")
  \end{lstlisting}
\end{frame}
```

### CS Examples in `main.tex`

| Content | Packages / features |
|---|---|
| Equations, vectors, theorem and proof | `amsmath`, `mathtools`, `bm`, custom boxes |
| Pseudocode | `algorithm2e`, using `[H]` inside a frame |
| Python source | `listings`, `[fragile]` frame |
| Tables with grouped cells and formatted headings | `booktabs`, `multirow`, `makecell` |
| Tables with wrapping columns | `tabularx`, `array` |
| Quantities and numeric formatting | `siunitx` |
| Method flowchart | TikZ |
| Plots arranged as subfigures | `pgfplots`, `subcaption` |
| Chinese/English content and appendix | `ctexbeamer`, `appendixnumberbeamer` |

### Resource Path

Images are located through `\nkresourcepath`, defaulting to `resources/`. To use another directory, define it **before** loading the theme and include the trailing slash:

```latex
\providecommand{\nkresourcepath}{my-assets/}
\usetheme{Nankai}
```

Keep `NKU.png`, `NK-Emblem.png`, and `NK-Motto.png` in that directory, or update the corresponding references in the theme.

## Tips

- The `\AtBeginSection` hook in `main.tex` inserts a TOC at each section start; remove or customize it to change that behavior.
- Change `aspectratio=169` for another page ratio, then check your content layout.
- Keep all project files together and compile from the root so relative theme and image paths resolve.
- Recompile after changing metadata, sections, or appendix content to update navigation and totals.
- Inspect the PDF after adding dense tables, code, or citation footnotes; Beamer frames have a fixed content area.

## License

The template source code is distributed under the [MIT License](LICENSE). Nankai University's name, emblems, and motto imagery remain subject to the rights of their respective owners. The code license does not grant rights to university marks or imply university endorsement; follow applicable university rules when using those assets.

## Acknowledgments

- The author gratefully acknowledges the use of Nankai University's visual identity assets in this project.
