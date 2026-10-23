---
name: "diktat-builder"
description: "Builds a diktat (LaTeX-compiled PDF study guide) in two modes: Ultimate for UTS/UAS (full theory, solved archives, prediction package) and Review for day-to-day lectures (compact theory, many practice problems). Every answer verified in code. Trigger on 'buat diktat', 'diktat UTS/UAS/kuis', 'diktat materi hari ini', 'diktat pertemuan', 'rangkuman + latihan', or requests to update a diktat or make a soal-only PDF."
---

# Diktat Builder

A diktat is his study guide as a LaTeX-compiled PDF. Follow **mayer:math-tutor-style** for notation and course conventions (Analisis proof format, Progmat row-0 sign, Statmat notation, Praktikum Octave rules).

Correctness matters more than polish. A wrong answer key teaches a wrong method.

## Pick the mode

| Mode | When | Size |
|---|---|---|
| **Ultimate** | UTS, UAS, or a big kuis covering several chapters. "diktat UTS", "diktat UAS", "ultimate" | No limit (typically 50–100 pages) |
| **Review** | Day-to-day: one lecture, one subbab, this week's material. "diktat materi hari ini", "diktat pertemuan X", "review" | Compact theory, ~10–25 pages, mostly practice |

If the request doesn't make the mode clear, ask once which one.

## Shared steps (both modes)

### 1. Scope
Course, topics or subbab, assessment and date if any, anything to exclude (e.g., "tanpa soal prediksi"). Ask once if the topic list is missing. If he attached a previous diktat, match its format; otherwise use the default preamble below.

### 2. Gather material first
Read everything before writing LaTeX: slides, notes, RPS/SAP/Sub-CPMK, responsi, tugas, assistant modules, past exams, and the textbook section when slides are thin. Use `pdftotext -layout` for text PDFs; rasterize scanned pages and read them as images.

### 3. Verify everything in code before writing
Never put an unverified number in the diktat.
- Symbolic (series, ODEs, integrals, MGFs): `sympy`
- LP / simplex / duality: exact `fractions`, cross-checked with `scipy.optimize.linprog`
- Data structures: Python traces
- Numerical methods: Octave or Python, checked against textbook tables
- Probability: exact fractions; distributions sum to 1

Keep the scripts. When a source has an error (typo, wrong interval, two correct PG options), flag it in an `awasbox` titled "Koreksi" with the fix. If problems are recalled from a textbook rather than taken from a file, say so.

### 4. The example rule
Before each new problem type in any practice section, include one fully worked example of that type (`contohbox`). Practice problems never appear without a matching worked example earlier in the same section.

### 5. Build
- Modular source: `main.tex` plus one file per chapter, pulled in with `\input`.
- Write long documents in stages: preamble and outline first, then chapter by chapter.
- `pdflatex` three passes.
- Fix overfull hboxes (`\quad` instead of `\qquad`, `align*` for long displays, `tabularx` for wide tables).
- Direction fields: scale axes explicitly and compute arrow angles with `atan2`.
- Render a few pages to PNG and look at them.

### 6. Deliver
Send the PDF and a zip of the source. Then one short message: mode, page count, number of practice problems, anything flagged. Don't recap contents.

## Mode: Ultimate (UTS / UAS)

Add an archive analysis before writing: a frequency table of topic × year with question format (PG, esai, isian, pseudocode), recurring traps, and which archive is closest to the current exam style.

Structure:
1. **Cover + peta materi**: scope note (in/out), archive frequency table, recommended study order.
2. **Theory chapters, one per topic**: `defbox`/`thmbox`, derivations, `langkahbox`, `contohbox`, `tipbox`, `awasbox`.
3. **Solusi latihan**: every exercise from slides, responsi, and tugas, fully solved.
4. **Arsip**: every archived exam fully solved, by year. Mark ambiguous PG answers with `*` and explain.
5. **Paket prediksi + latihan tambahan**: an exam-shaped package matching the real format and length, plus extra problems weighted by archive frequency. Answer key in a separate section after all problems. Skip if he says no prediction.
6. **Strategi ujian**: time plan for the real exam duration, common-mistakes checklist (include his known error patterns), what to do first.
7. **Lampiran**: formula cheat sheet, 1–2 pages.

## Mode: Review (day-to-day)

Goal: understand today's material fast, then drill it. Theory short, practice heavy.

Structure:
1. **Ringkasan** (1–3 pages per topic): key definitions and theorems in boxes, the standard procedure in a `langkahbox`, one-line "kenapa" for each formula, an `awasbox` with the typical traps.
2. **Latihan bertingkat** per topic, each level opened by a worked example of its problem type:
   - **Dasar**: single-step, direct application (4–6 problems)
   - **Gabungan**: two or more ideas combined, exam-like (4–6 problems)
   - **Variasi sulit**: twists, edge cases, archive-style traps (2–4 problems)
3. **Campuran**: 5–8 mixed problems with no topic labels, so he must choose the method himself.
4. **Kunci jawaban**: separate section at the end. Short final answers first, then full solutions, so he can check quickly without seeing the work.
5. **Kartu rumus**: half a page of the formulas from this material.

Source practice problems from, in order: the lecture's own exercises, responsi, textbook exercises for that section, then new problems you write. Aim for at least 20 problems total.

## Variants (either mode)

- **Soal saja**: a clean practice PDF with only questions (no answers), each question kept on one page. Fix obviously broken questions and list the fixes in the reply.
- **Versi pendek**: a summary he will copy by hand within a page limit he gives. Match slide content, cut non-syllabus material.
- **Update**: when new material arrives, verify it, integrate it into the existing chapters, update the cover and tables, and redeliver. Don't rebuild from scratch.
- **Review → Ultimate**: before an exam, combine the Review diktats for the exam's scope as the theory chapters, then add the Ultimate-only parts (archive analysis, arsip, prediksi, strategi).

## Use

The diktat contains lecturers' and assistants' problems; it is for his personal study. If he wants to share or publish it, suggest replacing archived problems with original ones and crediting sources.

## Default preamble

```latex
\documentclass[11pt,a4paper]{article}
\usepackage[a4paper,margin=2.2cm]{geometry}
\usepackage{amsmath,amssymb,mathtools}
\usepackage[most]{tcolorbox}
\usepackage{tikz,pgfplots}\pgfplotsset{compat=1.18}
\usetikzlibrary{arrows.meta,calc,positioning}
\usepackage{forest}
\usepackage{tabularx,booktabs,xltabular}
\usepackage{enumitem}
\usepackage{listings,xcolor}
\usepackage{fancyhdr}
\usepackage{hyperref}

\tcbset{diktat/.style={enhanced,breakable,fonttitle=\bfseries,arc=2pt,boxrule=0.6pt,left=6pt,right=6pt}}
\newtcolorbox{defbox}[1][]{diktat,colback=blue!4,colframe=blue!60!black,title=Definisi,#1}
\newtcolorbox{thmbox}[1][]{diktat,colback=violet!4,colframe=violet!60!black,title=Teorema,#1}
\newtcolorbox{langkahbox}[1][]{diktat,colback=teal!5,colframe=teal!60!black,title=Langkah baku,#1}
\newtcolorbox{contohbox}[1][]{diktat,colback=green!4,colframe=green!45!black,title=Contoh,#1}
\newtcolorbox{tipbox}[1][]{diktat,colback=orange!6,colframe=orange!70!black,title=Tips,#1}
\newtcolorbox{awasbox}[1][]{diktat,colback=red!5,colframe=red!65!black,title=Awas,#1}
\newtcolorbox{soalbox}[1][]{diktat,colback=gray!5,colframe=gray!60!black,title=Soal,#1}

% Analisis 1 proof labels
\newcommand{\AP}{\noindent\underline{\textbf{Analisis pendahuluan.}}\ }
\newcommand{\BF}{\noindent\underline{\textbf{Bukti formal.}}\ }

\lstset{basicstyle=\ttfamily\small,breaklines=true,frame=single,columns=fullflexible}
\pagestyle{fancy}\fancyhf{}\rhead{\thepage}
```

Box titles take options: `\begin{contohbox}[title=Contoh 2: Big M]`.