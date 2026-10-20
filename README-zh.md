# 南开大学 Beamer 模板

<p align="center">
    <a href="README.md"><img src="https://img.shields.io/badge/README-English-blue" alt="README"></a>
    <a href="README-zh.md"><img src="https://img.shields.io/badge/README-%E4%B8%AD%E6%96%87-red" alt="README-zh"></a>
    <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License">
</p>

一个面向**南开大学**师生的 LaTeX Beamer 学术汇报模板。采用*南开紫*配色，支持中文、英文与混合排版，并提供计算机学术汇报常用示例。

## 预览

效果请查看 [main.pdf](main.pdf)，对应源文件为 [main.tex](main.tex)。

## 特性

- **南开紫**配色方案
- **16:9 宽屏**布局，包含校名标志、校徽与校训图片
- 基于 `ctexbeamer` 与 XeLaTeX 的**中文、英文及中英混排**支持
- **自适应章节导航**：当前章节高亮，其他章节淡化
- **自适应页脚**：显示院校、汇报简称、汇报人和当前／总帧数
- 页面底部显示**汇报进度条**
- **七种自定义内容盒子**：通用、定理、定义、引理、证明、注记、高亮
- **小字号帧级脚注引用**，支持在自定义盒子内引用
- **计算机学术示例**：数学、伪代码、源代码、表格、子图、流程图和绘图
- 每节自动目录、参考文献、致谢页，以及**独立编号的附录**

## 项目结构

```text
NKU-Beamer-Template/
├── main.tex                        # 主演示文稿源文件
├── main.pdf                        # 编译后的预览
├── references.bib                  # BibTeX 格式的文献数据库
├── resources/
│   ├── NKU.png                     # 校徽与校名组合标志（封面）
│   ├── NK-Emblem.png               # 圆形校徽（页面标题与致谢页）
│   └── NK-Motto.png                # 校训图片（封面）
├── style/
│   ├── beamerthemeNankai.sty        # 主题加载与资源路径
│   ├── beamercolorthemeNankai.sty   # 颜色定义
│   ├── beamerfontthemeNankai.sty    # 字号与字形
│   ├── beamerinnerthemeNankai.sty   # 封面、标准区块、自定义盒子
│   ├── beamerouterthemeNankai.sty   # 导航、页脚、进度条
│   └── nankaibib.sty                # 帧级引用脚注
├── README.md
├── README-zh.md
└── LICENSE
```

## 快速开始

可从 [Releases](https://github.com/InfinityUniverse0/NKU-Beamer-Template/releases) 下载即用 ZIP。每个压缩包包含模板源码、主题、图片、文献数据库、说明文档、许可证和重新编译的 `main.pdf`。解压后在该目录编译，或将 ZIP 上传到 Overleaf 并选择 **XeLaTeX**。

### 环境要求

使用较新的 **TeX Live**、**MacTeX** 或 **MiKTeX**，并安装 **XeLaTeX** 与 **Biber**。验证环境为 TeX Live 2024、Beamer 3.71。

示例使用以下宏包：

- 主题与字体：`ctex`、`beamer`、`tikz`、`tcolorbox`、`calligra`
- 数学：`amsmath`、`amssymb`、`amsfonts`、`mathtools`、`bm`
- 算法与代码：`algorithm2e`、`listings`
- 表格、图形与数字排版：`booktabs`、`multirow`、`array`、`makecell`、`tabularx`、`subcaption`、`pgfplots`、`siunitx`
- 文献与附录编号：`biblatex`、`appendixnumberbeamer`
- 可选的自动构建工具：`latexmk`

完整 TeX 发行版包含这些宏包；精简安装需要通过发行版的宏包管理器补齐缺失项。Biber 与 biblatex 应来自兼容的发行版版本。示例保留 ctex 默认字体选择，根据当前系统选用中文字体，因此不同操作系统的字体外观可能不同。如需多台机器保持一致，可在各机器安装相同字体并显式指定，见下方字体建议。`listings` 无需 shell escape 或外部代码高亮程序。

### 编译命令

在仓库根目录运行：

```bash
latexmk -xelatex main.tex
```

也可以手动编译：

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

`.bib` 文件使用 **BibTeX 数据库格式**，但 `backend=biber` 指定的处理器是 **Biber**，应运行 `biber main`，而非 `bibtex main`。多遍 XeLaTeX 编译用于更新章节导航、交叉引用与总帧数；`latexmk` 会自动完成必要步骤。

使用 Overleaf 时，上传完整项目，将 `main.tex` 设为主文档，并选择 **XeLaTeX** 编译器。

### 使用步骤

1. 克隆仓库：

   ```bash
   git clone https://github.com/InfinityUniverse0/NKU-Beamer-Template.git
   cd NKU-Beamer-Template
   ```

2. 修改 `main.tex` 中的元信息：

   ```latex
   \title[汇报简称]{你的完整学术汇报标题}
   \subtitle{学术研讨会或汇报场合}
   \author[姓名]{你的姓名}
   \institute[南开大学]{南开大学\quad 计算机学院}
   \date{2026 年 10 月 20 日}
   ```

3. 替换示例页面与参考文献，然后编译。方括号中的可选参数用于页脚中的简短信息。

### 中文与英文文稿

保留项目的 `style/` 与 `resources/` 目录，即可使用以下最小中文示例：

```latex
\documentclass[aspectratio=169,UTF8]{ctexbeamer}
\makeatletter
\providecommand*\input@path{}
\g@addto@macro\input@path{{style/}}
\makeatother
\usetheme{Nankai}
\title[汇报简称]{你的学术汇报标题}
\author[姓名]{你的姓名}
\institute[南开大学]{南开大学}
\date{2026 年 10 月 20 日}
\begin{document}
\begin{frame}[plain,noframenumbering]
  \titlepage
\end{frame}
\section[背景]{研究背景与问题}
\begin{frame}{研究问题}
  支持中文与英文混排：Knowledge Extraction。
\end{frame}
\end{document}
```

英文正文可以直接使用相同配置，无需切换。如果希望自动名称和日期也采用标准 Beamer 约定（通常为英文），可以选择增加 `scheme=plain`：

```latex
\documentclass[aspectratio=169,UTF8,scheme=plain]{ctexbeamer}
% 保留上方示例中的主题加载代码。
\title[Short Title]{An Academic Presentation}
\author[Your Name]{Your Name}
\institute[Nankai University]{Nankai University}
\date{October 20, 2026}
```

中文、英文与中英混排都无需切换语言选项。默认的 `scheme=chinese` 使用中文自动名称与日期约定，例如“图”“表”和 `\today`；可选的 `scheme=plain` 保留标准 Beamer 约定，但仍然支持中文。它是整份文稿的风格选择，不是正文的语言开关，也不会自动翻译手写的页面标题、章节名或 Box 标题。中英混排时，选择一套统一的自动名称风格即可，各页正文可自由使用两种语言。常用宏包配置、代码配色与每节自动目录位于 `main.tex`，并非仅加载 `\usetheme{Nankai}` 就会全部启用。

### 字体建议

示例不强制指定字体集。Beamer 默认采用无衬线正文，学术汇报通常适合清晰的中文黑体：

- **macOS：**可以选用苹方（PingFang SC），替代默认中文字体。
- **Windows、macOS、Linux 统一外观：**推荐思源黑体（Source Han Sans SC）或 Noto Sans CJK SC，在各机器上安装相同字体。

例如，在已安装苹方的 Mac 上，在文档类之后添加：

```latex
\setCJKsansfont{PingFang SC}[BoldFont={PingFang SC Semibold}]
```

也可以指定已安装的思源黑体：

```latex
\setCJKsansfont{Source Han Sans SC}[BoldFont={Source Han Sans SC Bold}]
```

这些命令修改中文无衬线字体；西文与数学字体可以独立配置。缺少中文系统字体时，ctex 可能自动使用 Fandol，也可以显式设置 `fontset=fandol` 作为兼容性备选；中英混排并不要求使用 Fandol。

## 自定义指南

### 配色方案

| 名称 | RGB 值 | 十六进制 | 用途 |
|---|---|---|---|
| `NKPurple` | 122, 24, 84 | `#7A1854` | 主色调、链接、线条 |
| `NKPurpleDark` | 86, 16, 59 | `#56103B` | 强调色、副标题 |
| `NKPurpleLight` | 162, 72, 124 | `#A2487C` | 辅助色、分割线 |
| `NKPurpleVeryLight` | 245, 238, 242 | `#F5EEF2` | 浅色背景 |
| `NKGray` | 160, 160, 160 | `#A0A0A0` | 辅助文字 |
| `NKDarkGray` | 80, 80, 80 | `#505050` | 正文备选色 |
| `NKLightGray` | 230, 230, 230 | `#E6E6E6` | 浅色线条与进度条底色 |

颜色定义位于 `style/beamercolorthemeNankai.sty`。加载主题后可重新定义颜色，例如 `\definecolor{NKPurple}{RGB}{122,24,84}`。

### 章节导航与页脚

页眉按章节文字的自然宽度排布，并将剩余空间分配到章节间隔。整行超宽时，会整体缩小以适应页宽。当前章节高亮，其他章节淡化。较长章节名建议提供简短导航名：

```latex
\section[研究方法]{基于检索增强生成的知识抽取方法}
```

页脚中院校／标题／作者／帧数的默认宽度分别为页宽的 **18% / 36% / 20% / 10%**。内容超过默认宽度时，字段按自然宽度扩展；空间不足时回收其他字段的闲置默认宽度，仍无法容纳时再整体缩小。适当设置简称可以保持文字清晰：

```latex
\title[知识抽取研究]{一个较长且详细的完整学术汇报标题}
\author[张三]{张\;三}
\institute[南开大学]{南开大学\quad 计算机学院}
```

页码使用 **Beamer 的帧计数器**，不一定等于 PDF 的物理页数。分步显示的 overlay 共用一个帧编号；`allowframebreaks` 生成的每张续页都会推进帧计数。`main.tex` 的封面与致谢页使用 `[plain,noframenumbering]`；目录与参考文献计入正文总帧数。单独使用 `[plain]` 只隐藏页眉页脚，不会停止计数。

使用 `appendixnumberbeamer` 时，`\appendix` 之后的附录独立编号，不增加正文总帧数。附录导航取决于附录实际定义的章节；若未定义附录章节，该导航栏为空。

### 自定义环境

七种环境都接受可选的 `tcolorbox` 参数。通过 `title={...}` 设置中文或英文标题，`title={}` 隐藏默认标题，也可用 `colback` 等参数调整外观。这些内容盒子不会自动为定理编号，也不会将内容自动拆分到多个 Beamer 帧。

```latex
\begin{nkbox}[title={研究问题}]
  说明任务范围与基本假设。
\end{nkbox}

\begin{nkdefinition}[title={定义：候选集合}]
  定义研究方法中使用的对象。
\end{nkdefinition}

\begin{nktheorem}[title={定理}]
  给出结论及其成立条件。
\end{nktheorem}

\begin{nklemma}[title={引理}]
  陈述用于后续推导的辅助结论。
\end{nklemma}

\begin{nkproof}[title={证明}]
  给出所述结论的证明过程。
\end{nkproof}

\begin{nkremark}[title={实现说明}]
  补充实际实现中需要考虑的细节。
\end{nkremark}

\begin{nkhighlight}
  强调本页的核心结论。
\end{nkhighlight}
```

请将各示例分别放入有足够空间的 frame 中。标准 Beamer 环境 `block`、`exampleblock` 和 `alertblock` 也已适配主题风格。

### 脚注引用

按前面的示例设置 `style/` 搜索路径，并在 **biblatex 之后**加载引用辅助宏包：

```latex
\usepackage[backend=biber,style=numeric-comp,sorting=none,
            maxbibnames=2,giveninits=true,
            doi=false,isbn=false,url=false]{biblatex}
\addbibresource{references.bib}
\usepackage{nankaibib}
```

在正文或自定义 Box 内使用 `\footfullcite`，即可用小字号脚注显示完整文献信息：

```latex
\begin{frame}{相关工作}
  \begin{nkbox}[title={检索增强生成}]
    检索为生成过程提供外部上下文。\footfullcite{lewis2020rag}
  \end{nkbox}
\end{frame}
```

辅助宏包保留 biblatex 的前注／后注可选参数，以及逗号分隔的多个文献键：

```latex
\footfullcite[pp.~1--2]{lewis2020rag}
\footfullcite[参见][pp.~1--2]{lewis2020rag}
\footfullcite{bordes2013translating,lewis2020rag}
```

支持普通页面、自定义 Box、分栏和 `[plain]` 页面，脚注编号在整份文稿中连续累加。引用应放在页面内容中，避免用于页面标题、章节名等需要写入目录或导航的参数。脚注占用正常页面空间，同一页引用较多文献时应减少正文内容。`\cite{key}` 仍为行内数字引用。文末列出已引用文献：

```latex
\begin{frame}[allowframebreaks]{参考文献}
  \printbibliography[heading=none]
\end{frame}
```

### 代码展示

`main.tex` 配置了南开配色的 `listings` 样式。包含逐字代码的页面必须使用 `[fragile]`：

```latex
\begin{frame}[fragile]{代码示例}
  \begin{lstlisting}[language=Python,caption={问候函数}]
def hello():
    print("Hello, Nankai!")
  \end{lstlisting}
\end{frame}
```

### `main.tex` 中的计算机学术示例

| 示例内容 | 宏包／功能 |
|---|---|
| 公式、向量、定理与证明 | `amsmath`、`mathtools`、`bm`、自定义 Box |
| 伪代码 | `algorithm2e`，在 frame 中使用 `[H]` |
| Python 源代码 | `listings`、`[fragile]` 页面 |
| 分组单元格与表头格式 | `booktabs`、`multirow`、`makecell` |
| 自动换行的表格列 | `tabularx`、`array` |
| 物理量与数字排版 | `siunitx` |
| 方法流程图 | TikZ |
| 并排子图与绘图 | `pgfplots`、`subcaption` |
| 中英文内容与附录 | `ctexbeamer`、`appendixnumberbeamer` |

### 资源路径

图片通过 `\nkresourcepath` 定位，默认目录为 `resources/`。更换目录时，在加载主题**之前**定义该宏，并保留末尾的斜杠：

```latex
\providecommand{\nkresourcepath}{my-assets/}
\usetheme{Nankai}
```

请在该目录保留 `NKU.png`、`NK-Emblem.png` 和 `NK-Motto.png`，或同步修改主题内对应的图片引用。

## 使用技巧

- `main.tex` 中的 `\AtBeginSection` 会在每节开始插入目录页，可删除或自定义该钩子。
- 如需其他页面比例，修改 `aspectratio=169`，随后检查内容布局。
- 保持项目文件完整，并从项目根目录编译，以便正确解析主题与图片的相对路径。
- 修改元信息、章节或附录后重新编译，使导航与总帧数更新。
- 添加密集表格、代码或脚注引用后检查 PDF；Beamer 每帧的内容空间固定。

## 许可证

模板源代码基于 [MIT License](LICENSE) 发布。南开大学校名、校徽、校训等标识与图片的相关权利属于各自权利人；代码许可证不授予大学标识的使用权，也不表示南开大学为本项目背书。使用这些资源时请遵守适用的学校规定。

## 致谢

- 本项目使用了南开大学的视觉标识资源，谨致谢意。
