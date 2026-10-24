---
name: "tugas-write-up"
description: "Turns his own worked solution to a math tugas into a compact write-up in standard undergraduate style: mostly mathematics, minimal words, exact forms, checked for errors. Trigger on 'tulis rapi', 'rapikan jawaban saya', 'buat versi folio', 'write up' when he sends his own work. If he has no attempt yet, it sends him to math-tutor-style or math-socratic-tutor first."
---

# Tugas Write-Up

The input is **his own worked solution** (photo, PDF, or typed). The output is a clean, compact version of that same solution: the mathematics carries the argument, and words appear only where the logic needs them. It is not a tutoring explanation, and it is not a substitute for doing the work.

## Academic integrity

- **Start from his attempt.** If he asks for a write-up without sending his own work, don't write one. Ask for his attempt, or offer **mayer:math-tutor-style** (to learn the method) or **mayer:math-socratic-tutor** (to work it out together).
- **Keep his method.** Keep his approach and his steps, fixing only presentation and errors. Don't swap in a different proof or method he didn't use.
- **Errors get flagged, not silently fixed.** When his work has a mathematical error, point it out with **mayer:math-work-check** rules, then write up the corrected version only after he has seen the error.
- **Follow the course's AI policy.** If a course forbids AI help on tugas, say so once and stop. He decides; the skill doesn't decide for him.

Follow **mayer:math-tutor-style** course conventions (Analisis proof format, Statmat notation, Progmat row-0 sign, PDB textbook notation). Ignore its tutoring formatting: no headers per step, no Ringkasan Pola, no Intinya, no analogies, no emoji.

## Before writing

1. Solve every problem independently and **verify in code** (sympy, exact fractions, scipy, Octave), so you can compare against his work. Never write up a result that fails the check.
2. If the problem statement looks wrong (typo, inconsistent data, missing sub-part), write the answer for the most sensible reading and flag it to him in one line **outside** the write-up.

## Style rules

- **Indonesian**, formal and brief.
- **Words allowed only as logical connectives**: "Perhatikan", "Misalkan", "Maka", "Akibatnya", "Karena ..., maka ...", "Jadi", "Terbukti", "Tinjau kasus". No sentences that explain *why a method works*.
- **Justify steps by citation, not prose**: a short tag at the end of the line, e.g. `(Teorema Apit)`, `(integral parsial)`, `(kondisi awal)`, `(Lema sup)`. In Analisis, cite theorems by name or statement, not number.
- **One logical step per line**; chain equalities with aligned `=`.
- **Exact forms**: keep $e$, $\pi$, $\ln$, fractions, radicals. Decimals only for numerical-methods problems or when the question asks.
- **Final answer** on its own line, prefixed with $\therefore$ (or boxed if he prefers).
- **Diketahui / Ditanya** only for word problems (modeling, LP, probability stories). Skip it for pure computations and proofs.
- **Verification lines** are not included unless the problem asks to verify.

## By problem type

| Type | Shape |
|---|---|
| Computation | Setup line → chained steps → $\therefore$ answer |
| ODE | Classify in one line (e.g., "PD linear orde 1") → method → general solution → apply initial condition → $\therefore$ |
| Proof | "Bukti." → argument → "Terbukti." or $\blacksquare$. Analisis: **Analisis pendahuluan** (scratch, backward) then **Bukti formal** (forward, with $\forall, \exists, \ni$), using "misalkan", never "ambil sembarang" |
| Case analysis | "Kasus 1: ..." / "Kasus 2: ..." each with its own chain, then the combined result |
| LP / simplex | Model (variabel, fungsi tujuan, kendala) → tableaus as tables → optimal solution and $Z^*$ |
| Numerical methods | Formula once → one fully shown iteration → table of all iterations (with exact solution and error columns if asked) |
| Sketch / phase line / graph | Write "Sketsa:" followed by what to draw: axes, key points with coordinates, asymptotes, direction. Add a small ASCII preview so he can check the shape |
| Multiple choice with reasoning | Key computation in 1–3 lines → chosen option |

## Output

- Default: in the chat, LaTeX math, problems numbered exactly as in the tugas (1a, 1b, ...).
- If he asks for a file: compile a PDF with the same content.
- Directly after the write-up, outside it: flagged issues (if any) in one line each. Nothing else.

## Folio space

If he asks how much space to reserve for skipped problems, estimate pages per problem from its length in this compact style (count lines of math and sketches), round up, and give a total.

## Example

**3b.** $y' + 2y = e^{-t},\ y(0)=1$

PD linear orde 1, $\mu(t) = e^{\int 2\,dt} = e^{2t}$.

$$\begin{aligned}
(e^{2t}y)' &= e^{t}\\
e^{2t}y &= e^{t} + C\\
y &= e^{-t} + Ce^{-2t}
\end{aligned}$$

$y(0)=1 \Rightarrow 1 = 1 + C \Rightarrow C = 0$.

$$\therefore\ y(t) = e^{-t}$$