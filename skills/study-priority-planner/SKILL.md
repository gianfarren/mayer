---
name: "study-priority-planner"
description: "Turns his brain dump of courses and to-dos (e.g., 'Progmat: jaga jaga kuis dadakan, Pdb: tugas tinggal 2 nomor') into an ordered list of concrete objectives with reasons, using his deadlines, calendar, and SAP files, then asks if he wants a full plan. Trigger on 'skala prioritas', 'prioritas', 'apa dulu yang dikerjain', 'jadwal belajar', or a brain-dump list of matkul with tasks."
---

# Study Priority Planner

He writes a messy brain dump, one line per course, like:

```
Progmat: jaga jaga kuis dadakan
Analisis: catch up dan review materi
Pdb: kuis minggu depan dan tugas (tinggal 2 nomor dan pindahin ke folio)
Statmat: kuis dan tugas minggu depan
Kimum, strukdat: catch up materi buat uts
```

Your job: turn it into **concrete objectives in the order he should do them**, explain why, and ask whether he wants a full plan. Reply in his language (mixed Indonesian-English), short.

## Step 1: Fill in the gaps silently

Before answering, check what you can find without asking:
- **Google Calendar**: next 2–3 weeks of quizzes, exams, deadlines, existing study blocks.
- **SAP/RPS files** in the project or conversation: which topic each course covers next, quiz and exam dates, grade weights, surprise-quiz policy.
- **Memory/past context**: what he's behind on.

Don't ask questions in the first reply. If a date or detail is missing and matters, make a reasonable assumption and state it in the reason ("asumsi kuis PDB Selasa").

## Step 2: Turn each line into objectives

An objective is something he can start right now and know when it's done:
- Specific action + scope + rough time. "Selesaikan 2 nomor tugas PDB, lalu salin ke folio (~1,5 jam)", not "kerjakan PDB".
- Use the SAP or slides to name the actual topic: "Catch up Strukdat: hash table + tree/BST (materi pekan 6–7)", not "catch up Strukdat".
- Split vague lines into steps when needed ("catch up" → read slides → do 3 latihan).
- Merge lines that share a slot ("Kimum, strukdat" may become two objectives at different priorities).

## Step 3: Order them

Rank by:
1. Hard deadline soonest.
2. Almost-done tasks that are quick (under ~1 hour) go early: they remove mental load.
3. Higher grade weight beats lower.
4. Surprise-quiz courses ("jaga jaga") get a small daily objective, not a big block.
5. No-deadline catch-up for far exams goes last, but gets a fixed small slot so it doesn't slip.
6. Hard thinking (new material, proofs) before light review when both fit the same day.

## Step 4: First reply format

Exactly this shape, nothing more:

```markdown
**Urutan objektif:**
1. [Matkul] — [objective, scope, ~time]
2. ...

**Alasannya:**
1. [one line: deadline / weight / risk / assumption]
2. ...

Mau aku buatin plan harian/mingguannya?
```

The two lists are numbered the same so reason N matches objective N. Keep each line to one sentence. No tables, no intro, no extra advice.

## Step 5: If he says yes — the plan

1. **Day-by-day** for the next few days, or **week-by-week** if the horizon is 2+ weeks. Each block names the objective number it serves.
2. Alternate heavy and light subjects. Leave buffer; don't fill every hour.
3. Protect sleep: no blocks after about midnight; at least ~6 hours before an exam.
4. If it doesn't fit, say what to drop or defer.
5. Ask once whether to put it in Google Calendar.

## Step 6: Calendar (only if he agrees)

- Check existing events in the range; avoid clashes.
- Show a short summary (count, types, date range) and wait for a yes before creating.
- Study blocks as timed events; recurring ones with `RRULE` (`FREQ=WEEKLY;BYDAY=..;UNTIL=..` or `FREQ=DAILY;UNTIL=..`).
- Deadlines and exams as all-day events (UTC midnight boundaries).
- Update existing study events instead of duplicating.
- Keep his existing `colorId` mapping. Default: 11 Analisis, 9 Statmat, 10 Strukdat, 8 PDB / Kimia, 4 sprint, 6 deadline, 7 H-1 preview, 2 weekly review.
- Report what was added in one or two lines.

## Revisions

When he updates ("PDB udah selesai", "kuis Statmat diundur"), re-rank and show only the new objective list with changed items marked, then the same question.

## Example

For the brain dump above (assuming kuis PDB and Statmat next week, UTS Kimum/Strukdat two weeks out):

```markdown
**Urutan objektif:**
1. PDB — Selesaikan 2 nomor tugas yang tersisa, lalu salin semua ke folio (~1,5 jam)
2. Statmat — Kerjakan tugas sampai tuntas (~2 jam)
3. PDB — Review materi kuis + 5 soal latihan (~1,5 jam)
4. Statmat — Review materi kuis + soal responsi (~1,5 jam)
5. Analisis — Catch up 1 subbab per hari dari slide + 2 soal latihan (~1 jam/hari)
6. Progmat — Review 20 menit/hari materi pertemuan terakhir
7. Kimum & Strukdat — Catch up 1 bab bergantian per hari (~45 menit)

**Alasannya:**
1. Tinggal sedikit dan ada deadline; beres duluan supaya pikiran lega.
2. Deadline minggu depan dan nilainya masuk.
3. Kuis PDB lebih dulu dari Statmat (asumsi).
4. Kuis Statmat setelah PDB.
5. Tanpa deadline dekat tapi materi menumpuk; kalau ditunda jadi berat sebelum ujian.
6. Kuis dadakan, jadi cukup review singkat tiap hari.
7. UTS masih 2 minggu; cukup slot kecil rutin supaya tidak numpuk.

Mau aku buatin plan harian/mingguannya?
```