---
name: "math-work-check"
description: "Checks his own math work (photo, PDF, typed, or just a final answer) when he asks 'bener?', 'udah bener?', 'am I on track?', 'cek jawaban saya': quick verdict for bare final answers, first-wrong-step diagnosis for shown work. Uses mayer:math-tutor-style for formatting and course conventions."
---

# Math Work Check

Branch of **mayer:math-tutor-style**. Follow that skill for language, formatting (LaTeX, ✓ ✗ ⚠️), and course conventions; load it too if it isn't already.

## Mode 1: Only a final answer

A bare final answer means he already understands the method and doesn't want a tutoring loop. Keep it quick.

- Solve it yourself silently (use code for heavy computation).
- **Correct:** "✓ Benar." plus the answer, nothing else. No follow-up questions, no explanation.
- **Wrong:** "✗" plus the correct answer and a one-line hint of where it likely went wrong (e.g., "cek tanda di batas bawah", "faktor $\tfrac12$ dari substitusi hilang"). Don't ask for his steps. If he wants details, he'll send the work.
- **Multiple choice:** give the letter and, if wrong, one line on why.

## Mode 2: Work shown (steps, photo, PDF)

Goal: he fixes his own work; you point to where and why.

1. **Read everything first.** If a line in a photo is unclear (signs, exponents, bounds), ask about that line before judging. A misread minus creates a mistake he never made.
2. **Solve it yourself silently** so you know the correct path.
3. **Verdict:** ✓ on track / ⚠️ partially right / ✗ off track.
4. **Find the first wrong step.** Later lines that are wrong only because of it are not separate mistakes; say "baris setelahnya ikut salah karena ini" once.
5. **If wrong:** quote that exact line, name the error type (table below), explain *why* that move is invalid, and ask one guiding question or suggest a concrete check. Don't write the corrected line.
6. **If right but incomplete:** confirm and say what comes next.
7. **Sanity checks:** run the relevant ones and mention any that fail.
8. **Don't re-solve from scratch** unless he says "yang bener gimana" / "solve aja" / "lupakan cara saya", or he has missed the same step twice. Then give the full solution in mayer:math-tutor-style Pattern A.

If several independent errors exist, report the earliest first.

## Error Types

Name the type explicitly so he learns to spot it himself.

| Type | Examples |
|---|---|
| Sign | dropped minus from $v = -e^{-y}$; negative lower bound evaluated as positive; wrong sign in integrating-factor formula |
| Bounds / support | integrating outside the support; reversed limits; limits from where $f = 0$ instead of the region |
| Index | $n \le K$ vs $n \ge K$; w-index vs t-index; bounds not shifted after substitution; $x$ left inside a sum after $t = x - 1$ |
| Notation | $p_1 \cap p_2$ instead of $P(A \cap B)$; comma (joint) vs bar (conditional); $F$ vs $f$; $\mu$ vs $\mu^2$ |
| Rule misuse | product rule on $[u(t)]^n$; $\lvert a-b \rvert \le \lvert a \rvert - \lvert b \rvert$; missing chain-rule factor; linearity applied to MGF |
| Logic | assuming the conclusion in an induction step; restating the claim instead of proving it; wrong quantifier; one example used to prove "for all" |
| Convention | row 0 sign in Progmat; "ambil sembarang" in Analisis; redefining lab functions in Praktikum |
| Carry-over | correct value found, then a factor dropped on the next line |
| Arithmetic | plain calculation slip |

## Sanity Checks

| Check | Applies to |
|---|---|
| Probability in $[0,1]$; total mass $= 1$ | Statmat |
| $\sigma^2 > 0$; $M(0) = 1$; $F$ non-decreasing, ends at 1 | Statmat |
| Substitute back into the ODE; initial condition holds | PDB |
| Error shrinks as $h$ shrinks; matches textbook table | Praktikum PDB |
| Plug in $n = 1, 2$; inequality direction after multiplying by a negative | Analisis |
| Optimal point satisfies all constraints; $Z$ matches | Progmat |
| Result matches one of the answer options | Multiple choice |

## Format (Mode 2)

```markdown
⚠️ Sebagian benar. Langkah 1–2 ✓.

Baris ke-3:
$$\int_{-2}^{0} \ldots \Big|_{x=2}$$

**Jenis kesalahan:** tanda (batas bawah).
Batas bawahnya $-2$, tapi yang disubstitusi $x = 2$. Baris 4–5 ikut salah karena ini.

Coba substitusi ulang batas bawahnya. Hasilnya harus positif — kenapa?
```

## Pola Kesalahan

If the same error type shows up again in the conversation, point it out in one line ("pola yang sama dengan soal 3 tadi") and name the sanity check that would have caught it.