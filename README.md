# SciWrite — Manuscript Writing Review

An [Agent Skill](https://agentskills.io) that reviews scientific and engineering manuscripts for writing quality, applying the methodology from Dr. Kristin Sainani's [*Writing in the Sciences*](https://www.coursera.org/learn/sciwrite) course at Stanford, augmented with the physics writing traditions of Kip S. Thorne and John A. Wheeler.

## About This Fork

This is a fork of [labarba/sciwrite](https://github.com/labarba/sciwrite) by [Duncan Brown](https://github.com/duncan-brown), extending the original skill with writing principles from the physics and astronomy community. The original skill (v1.0) was created by [Lorena A. Barba](https://github.com/labarba) at the George Washington University.

**What this fork adds (v2.0):**

- Physics-specific checks for LaTeX manuscripts, including equations-as-prose verification (terminal punctuation, sentence-initial symbols, symbols-as-verbs, inline built-up expressions)
- Wheeler's rules: suppress weak "to be" verbs, eliminate unnecessary "-ing" constructions, prefer present tense, lead with the singular and specific, place key words at sentence boundaries
- Thorne's prose architecture: modifier placement, cross-paragraph connecting phraseology, argument navigation scaffolding, parallel structure, word-resonance detection
- A hedging allowlist informed by Ken Hyland's metadiscourse research, preventing over-aggressive clutter removal of epistemically necessary hedges
- Figure caption self-sufficiency checks, attribution clarity checks, and a structural assessment diagnostic for manuscripts that need more than sentence-level editing

The v2.0 enhancements draw on Thorne's "Some Specific Tips About Technical Writing" (Caltech, 1987) and Wheeler's "Rules of Writing" (Am. J. Phys. 67, 1999), both canonical documents in the gravitational-wave physics community. The equations-as-prose checks are grounded in the current style guides of the American Physical Society, the American Astronomical Society, and the Royal Astronomical Society (MNRAS), as well as Higham's *Handbook of Writing for the Mathematical Sciences* (SIAM, 3rd ed. 2020).

Subsequent updates: v2.1 relicensed the project under Apache 2.0 and added documentation. v2.2 added two checks informed by research into golden-age physics writing (documented in [RESEARCH2.md](RESEARCH2.md)): a concept-introduction ordering check based on Penrose's practice (name → intuition → formalism → figure) and a payoff-before-machinery check based on Misner's "half-track" method.

## What This Skill Does

Clear writing is not a cosmetic concern in science; it determines whether reviewers and readers can follow your argument. Yet most graduate students receive little formal training in scientific writing, and self-editing for clarity is difficult because you already know what you meant to say.

This skill encodes a systematic editorial review process. When loaded into an AI tool, it performs sequential audit passes on your manuscript text:

1. **Clutter extraction.** Flags dead-weight phrases, unnecessary jargon, filler language, double negatives, and empty subjunctive constructions, with concise replacements. Respects legitimate epistemic hedges.
2. **Voice and verb vitality.** Identifies passive constructions, smothered verbs (nominalizations), weak "to be" verbs, unnecessary progressive ("-ing") forms, and suggests active, present-tense, specific alternatives.
3. **Sentence architecture.** Evaluates sentence structure and flow — buried predicates, modifier placement, dangling participles, voice/person consistency, word resonance, key-word placement, sentence length variation, parallel structure, and concept-introduction ordering. For LaTeX manuscripts, checks that equations are integrated into prose with correct punctuation. Checks cross-paragraph flow, argument navigation, and whether formalism is motivated before it is presented.
4. **Keyword consistency.** Checks that key technical terms are used consistently throughout, with self-sufficient figure captions and austere acronym usage.
5. **Numerical and citation integrity.** Audits numerical values for internal consistency, flags secondary-source citation chains, and checks that the boundary between new and prior work is clear.

The skill supports four review modes: full-manuscript, single-section, targeted (one pass only), and interactive (paragraph-by-paragraph with explanations). The output is a structured report with specific findings, concrete revisions, and severity tags.

Importantly, the skill does not alter scientific content, data, or technical claims. It improves how those claims are delivered.

## How to Use This Skill

### In Claude.ai (recommended starting point)

**Option A: Install account-wide via Customize (recommended)**

1. Download this repository as a ZIP file (click the green **Code** button, then **Download ZIP**).
2. Open [claude.ai](https://claude.ai). In the left sidebar, click **Customize** (the toolbox icon), then go to **Skills**.
3. Click the **+** button, then **+ Create skill**, and upload the ZIP file.
4. The skill will appear in your Skills list. Make sure its toggle is turned on.
5. Start any conversation and ask Claude to review your writing.

**Option B: Add to a specific Project's knowledge base**

1. Download the `SKILL.md` file from this repository.
2. Open or create a **Project** in Claude.ai.
3. In the Project's knowledge base, click **Add content** and upload the `SKILL.md` file.
4. Start a conversation inside that Project and ask Claude to review your writing.

### In Claude Code (terminal agent)

Place `SKILL.md` in `.claude/skills/manuscript-review/` inside your manuscript project directory, then launch Claude Code and ask for a review. See [`HOW-TO-USE.md`](HOW-TO-USE.md) for full setup instructions, example prompts, and tips for each review mode.

### In Claude's Cowork (desktop agent)

If you installed the skill account-wide via Customize (Option A above), it is already available in Cowork — no additional setup needed.

### In ChatGPT, Google Gemini, or any other AI tool

The skill is plain Markdown with no platform dependencies. Paste the contents of `SKILL.md` into your tool's persistent-instructions mechanism (Custom GPT, Gemini Gem, system prompt, etc.) and provide your manuscript text. See [`HOW-TO-USE.md`](HOW-TO-USE.md) for details.

## Tips for Getting Good Results

**Provide enough text for context.** A single isolated sentence is hard to review for keyword consistency or cross-paragraph flow. A full section gives the skill enough material to identify patterns.

**Specify your target journal.** Different journals have different conventions (MNRAS left-aligns and numbers all equations; APS numbers only referenced equations; some journals prefer passive voice in Methods). Telling the skill your target journal helps it calibrate.

**Use the interactive mode for learning.** The paragraph-by-paragraph mode shows before/after revisions with explanations — useful for building long-term writing habits, not just fixing a single draft.

**Review the output critically.** Occasionally the skill will flag a construction that is standard in your field or that serves a deliberate rhetorical purpose. Use your judgment.

**For LaTeX manuscripts:** Paste or upload the `.tex` source directly. The skill parses through LaTeX markup to the underlying prose and checks equation integration, symbol usage, and display-math punctuation.

## Customizing the Skill

The skill encodes general principles of scientific writing clarity with physics-specific extensions. You can further customize it with journal-specific conventions:

```
## Journal-Specific Conventions

Target journal: Physical Review D
- Equations referenced as Eq. (1), not equation (1), unless at the start of a sentence.
- Use Oxford commas.
- Number only equations that are referenced in the text.
```

You can also adjust the severity thresholds, add or remove entries from the clutter-phrase lookup table, extend the hedging allowlist for your subfield, or modify the review modes to match your workflow.

## Contributing

If you use this skill and find an edge case it doesn't handle well — a field-specific writing convention it misjudges, a LaTeX pattern it misparses, a common clutter pattern it misses, or a false positive that comes up repeatedly — contributions are welcome. Open an issue describing the case, or submit a pull request with your proposed change.

## How This Skill Was Built

The development of this skill is documented in companion files:

- **[HISTORY.md](HISTORY.md)** — An edited transcript of the Claude conversation that produced the v2.0 and v2.1 updates. It illustrates the full workflow: analyzing the original skill's architecture, comparing it against the Thorne and Wheeler sources, designing a four-tier enhancement plan, conducting focused research on journal conventions, implementing the skill files, and handling licensing. Provided as a pedagogical guide to remixing open-source AI agent skills; it covers the v2.0/v2.1 development cycle and does not include the v2.2 additions.

- **[RESEARCH.md](RESEARCH.md)** — A research brief on equations-as-prose conventions in physics and astronomy journals (APS, MNRAS, AAS, IOP) and the empirical evidence for and against the Sainani/Thorne/Wheeler writing principles. Produced during the v2.0 development conversation using Claude's deep research capability.

- **[RESEARCH2.md](RESEARCH2.md)** — A research brief on the writing techniques of the black-hole golden age (Penrose, Thorne, Wheeler, Hawking, 1963–1994) and the evolution of Thorne's textbook style from *Gravitation* (MTW, 1973) to *Modern Classical Physics* (Thorne & Blandford, 2017). Incorporates findings from a transcript of the MTW@50 anniversary celebration. This research informed the v2.2 additions.

For the history of how the original v1.0 skill was created (using Comet, NotebookLM, and Claude), see Lorena Barba's [original README](https://github.com/labarba/sciwrite).

## License

This work is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0). You are free to use, adapt, and share it under the terms of that license.

The original v1.0 skill by Lorena A. Barba was released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). CC-BY 4.0 permits derivative works to be distributed under a different license, provided that attribution is maintained. Attribution for the original work is preserved in the [NOTICE](NOTICE) file, as required by the Apache License.

## Acknowledgments

The writing methodology encoded in this skill draws on three traditions:

- **Kristin Sainani**, [*Writing in the Sciences*](https://www.coursera.org/learn/sciwrite) (Stanford University). The original video lectures are available on [YouTube](https://www.youtube.com/playlist?list=PLVc-QdfGfSl2Ntc6CvIP83Nj_uHTSdNSw) under a CC-BY license. The v1.0 skill was developed by Lorena A. Barba as part of the course [MAE 6291: Generative AI for Engineering Research](https://generative-ai-engineerin-u4bkjgp.gamma.site) at the George Washington University, shared through the [GW Engineering AI Academy](https://www.seas.gwu.edu/ai-academy).

- **Kip S. Thorne**, ["Some Specific Tips About Technical Writing"](https://www.its.caltech.edu/~kip/index.html/KipTechWritingTips.pdf) (Caltech, July 28, 1987). Written for Thorne's graduate students and postdocs, this document has been passed down through generations of gravitational-wave physicists. Thorne noted in October 2018 that most of the tips remain as relevant as when he wrote them.

- **John A. Wheeler**, ["Wheeler's Rules of Writing,"](https://doi.org/10.1119/1.19169) assembled by Edwin F. Taylor and published in *American Journal of Physics* 67(11), November 1999. Wheeler's aphoristic rules — "Motivate! Motivate! Motivate!", "Simplify! Simplify! Simplify!", the power of the singular, the specific, and the committed — distill decades of experience writing physics for physicists.

- **Roger Penrose** and **Charles Misner**, via the MTW@50 anniversary celebration (ISGRG, 2023) and scholarly analysis of the golden-age papers. Penrose's concept-introduction technique (name → intuition → formalism → figure) and Misner's "half-track" method (show the physical payoff before the mathematical machinery) informed the v2.2 checks.
