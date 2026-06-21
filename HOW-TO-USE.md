# How to Use the Manuscript Writing Review Skill

## What This Is

The file `SKILL.md` encodes a systematic writing-quality review process based on
Dr. Kristin Sainani's "Writing in the Sciences" methodology, augmented with the
physics writing traditions of Kip S. Thorne and John A. Wheeler. When placed in
the right location, an AI tool will automatically discover and apply these review
standards whenever you ask it to review your manuscript's writing.

Think of it as teaching the AI the editorial standards of a demanding journal
reviewer who also happens to have strong opinions about equation punctuation.

## Setup

### In Claude.ai

**Account-wide (recommended):** Download the repository as a ZIP file, then go to
Settings → Customize → Skills → + Create skill, and upload the ZIP.

**Project-scoped:** Download `SKILL.md` and upload it to a Project's knowledge base.

### In Claude Code

Place the skill inside your manuscript project:

```
my-manuscript/
├── .claude/
│   └── skills/
│       └── manuscript-review/
│           └── SKILL.md
├── draft.tex
├── figures/
└── references.bib
```

Commands:

```
cd /path/to/my-manuscript
mkdir -p .claude/skills/manuscript-review
cp /path/to/SKILL.md .claude/skills/manuscript-review/SKILL.md
```

### In any other AI tool

Paste the contents of `SKILL.md` into the tool's persistent-instructions mechanism
(Custom GPT, Gemini Gem, system prompt, etc.).

## Example Prompts

### Full manuscript review

```
Review the writing quality of draft.tex
```

```
Do a full writing review of my manuscript. Target journal is Physical Review D.
```

### Single section

```
Review the writing in my Introduction (sections/introduction.tex)
```

```
Check the Discussion section for clutter and passive voice
```

### Targeted pass — specific checks

```
Check my equations are punctuated as prose
```

```
Audit my Results section for keyword consistency — make sure variable names
match what I defined in Methods
```

```
Fix the passive voice in my Introduction
```

```
Strip the clutter from my Discussion. It's too wordy.
```

```
Check that my figure captions are self-contained
```

```
Check the cross-paragraph flow in Section 3 — it feels choppy
```

### Interactive, paragraph-by-paragraph editing

```
Walk me through improving the writing in my Introduction,
paragraph by paragraph
```

This mode is the most instructive: the AI shows you the original, a revised
version, and explains every change before moving on.

### Physics/LaTeX-specific prompts

```
Review my LaTeX manuscript for writing quality. Pay special attention to
equation integration — I want to make sure all displayed equations are
properly punctuated as part of the surrounding sentences.
```

```
Check that no sentences begin with bare mathematical symbols in my paper
```

```
Audit my manuscript for smothered verbs and nominalization — I think the
prose is too noun-heavy
```

## What the Output Looks Like

For full and section reviews, the AI produces a structured report:

* **Summary** — 2–3 sentence overall assessment
* **Pass 1: Clutter** — specific instances with original text, suggested revision, and rationale
* **Pass 2: Voice and Verbs** — same format
* **Pass 3: Sentence Architecture** — same format, including equations-as-prose findings for LaTeX
* **Pass 4: Terminology** — same format
* **Pass 5: Numbers and Citations** — same format
* **Top 5 Priority Revisions** — the highest-impact changes, ranked

Each finding is tagged with a severity level: CRITICAL, MAJOR, or MINOR.

## Tips for Best Results

**Tell the AI your target journal.** Different journals have different conventions.
Physical Review, MNRAS, ApJ, and CQG all share the equations-as-prose convention
but differ on equation numbering, reference formatting, and other details.

**Provide enough text for context.** The skill checks cross-paragraph flow,
keyword consistency, and argument navigation — all of which require seeing
multiple paragraphs at once. A full section is the minimum useful unit for a
comprehensive review.

**Point to specific pain points.** If you know your Discussion is bloated but
your Methods are clean, say so:

```
My Discussion is twice as long as it should be. Help me strip it down
without losing any of the scientific arguments.
```

**Use interactive mode for learning.** The paragraph-by-paragraph mode teaches
you why each change matters — useful for building permanent writing habits.

**For LaTeX source:** Paste or upload the `.tex` file directly. The skill
recognizes LaTeX math environments and commands, parsing through markup to the
underlying prose. It will not flag `\frac{}{}` or `\begin{equation}` as writing
issues — it checks how those equations integrate into the surrounding sentences.

## What This Skill Does NOT Do

* It does **not** evaluate scientific content, methods, or results.
* It does **not** check citation formatting (use a reference manager for that).
* It does **not** restructure your argument or reorder sections — though it will
  tell you if a section's argument lacks navigational scaffolding.
* It does **not** generate new text — it only revises existing prose.
* It does **not** check or re-derive equations — that is content review, not
  writing review.

If you need a full technical peer review (methods, novelty, significance),
that is a different task. This skill is purely about writing clarity and
precision.
