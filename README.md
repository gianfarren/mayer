# mayer

A Claude plugin for university mathematics: tutoring, work checks, a mistake-log practice loop, clean write-ups of your own solutions, LaTeX study guides, and a study priority planner.

## Why "mayer"

Everyone knows Einstein as a genius. Fewer people know he did not do all of his math alone.

From 1929, Einstein worked with Walther Mayer (1887–1948), an Austrian mathematician he called his "calculator". Mayer was the stronger technician. When the equations got heavy, Mayer carried them. When Einstein moved to Princeton in 1933, he brought Mayer with him. Mathematicians still know Mayer's name from the Mayer–Vietoris sequence.

But the questions were never Mayer's. Relativity and the light quantum came from Einstein's mind, years before Mayer arrived. Mayer could solve what was put in front of him. Deciding what was worth solving was Einstein's job.

## Why I built it

I'm a math student. For a whole semester, I opened every new chat with Claude the same way. Give me a worked example before you test me. Don't hand me the answer when I'm wrong; show me where my reasoning broke. Check my work and find the first mistake, not the last one.

Every chat, I started from zero.

So I wrote those rules down once, as skills. Now the assistant knows my courses, my notation, and the mistakes I keep making. It solves, checks, and builds study guides. It doesn't decide what I should understand, or what a result means. That part is still mine.

Anyone can have their own Mayer now. The assistant is the easy part.

> "You still have to be Einstein."

## Skills

You don't call the skills by name. Each one starts when your message matches its trigger phrases. My favorite is `math-socratic-tutor`.

| Skill | Starts on | What it does |
|---|---|---|
| `math-tutor-style` | "solve", "ajari saya", "kenapa jadi X", a photo of a problem | Core style: full solutions with verification and a reusable pattern table, single-step explanations, definitions, and course conventions. The other skills build on it. |
| `math-work-check` | "bener?", "udah bener?" + your work | A bare final answer gets a quick ✓/✗. Shown work gets the first wrong step, the error type, sanity checks, and one guiding question. |
| `math-socratic-tutor` | "dari nol", "cek pemahaman", "pola kesalahan saya apa" | Concept-by-concept sessions with a worked example before every question. Also keeps a persistent Mistake Log and builds practice worksheets when a mistake repeats. |
| `tugas-write-up` | "rapikan jawaban saya", "versi folio" + your own work | Turns *your* worked solution into a compact write-up in standard undergraduate style, after pointing out any errors. If you haven't tried the problem yet, it sends you to the tutor skills instead. |
| `diktat-builder` | "buat diktat UTS", "diktat materi hari ini" | LaTeX PDF study guides. *Ultimate* mode for midterms and finals, *Review* mode for daily lectures with 20+ practice problems. Every answer is checked in code. |
| `study-priority-planner` | A brain dump of courses and tasks, "prioritas" | An ordered list of concrete objectives with reasons, then an optional plan and Google Calendar blocks. |

## What this is, and what it isn't

Each skill is a Markdown file that tells Claude how to tutor, check work, and build study guides. There's no code here, and it only works inside Claude.

It's built to make me do the work. I get a worked example before every question, my errors get pointed out rather than fixed for me, and the write-up skill only formats solutions I wrote myself.

Some courses don't allow AI help on assignments. If yours doesn't, follow that.

Claude also makes mistakes. Answers get checked in code where that's possible, but I still read everything critically.

## Install

1. Download `mayer.plugin` from the [Releases](../../releases) page.
2. Add it to Claude as a plugin.

## Note

These skills are written for my own setup: a Mathematics undergraduate at Universitas Indonesia (FMIPA), working in mixed Indonesian and English, with my courses' textbooks and conventions built in. To use them for your own courses, fork the repo and edit the course conventions table in `skills/math-tutor-style/SKILL.md`.

## License

MIT. See [LICENSE](LICENSE).
