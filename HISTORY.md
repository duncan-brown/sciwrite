# Updating SciWrite for Physics Manuscripts

This file describes the interactions between the user and a Claude Opus 4.6 (high) model to incorporate Thorne and Wheeler's writing tips into Barba's skill.

## Establish the task

### Prompt

Lorena Barba has written a skill to help engineering doctoral students improve the writing in their papers by following best practices. We are going to build on this skill to include two classic documents on best writing practices for physicists. First load the skill-creator skill to make sure you understand the format and structure of skills. The parse all of the information from the GitHub repository containing the existing skill at https://github.com/labarba/sciwrite

Make sure you copy https://github.com/dda4ef83-4d85-4e0f-ba50-4e39d39aec55 locally as that is the SKILL.md file you will be modifying. 

Then read the attached two documents. The first is Kip Thorne’s writing tips from 1987. I was a postdoc with Kip; he gives this document to all of his mentees and I have given this document to all of mine. The second is a shorter writing skills document from John Wheeler, Kip’s PhD advisor. Both Kip and Wheeler are outstanding writers in the field of physics.

After you have done that, summarize Lorena’s skill and tell me what you have learned about the construction of the skill. 

Then compare and contrast Kip and Wheeler’s writing tips to those in Lorena’s skill. Where do the agree and where do they differ?

Do not attempt to modify or write the skill yet, I want to review and discuss the similarities and differences first.

### Response

**Summary of Lorena Barba's Skill and Skill Construction**

The skill is called "manuscript-writing-review" and encodes the methodology of Kristin Sainani's Stanford course "Writing in the Sciences," distilled from 30 video lectures. Barba created it through a clever three-tool pipeline: an agentic browser extracted the YouTube playlist URLs, NotebookLM synthesized the transcripts into a writing standards manual, and Claude converted that manual into a properly formatted SKILL.md.

The skill operates as a sentence-and-paragraph-level editorial reviewer, running five sequential audit passes: (1) clutter extraction — with a lookup table of dead-weight phrases and their concise replacements; (2) active voice and verb vitality — including a protocol for resurrecting "smothered verbs" (nominalizations); (3) sentence architecture — flagging buried predicates, monotonous sentence length, and underused punctuation; (4) keyword consistency — the "Banana Rule" that technical terms must not be varied for stylistic reasons; and (5) numerical consistency and citation integrity — cross-checking values across abstract, text, tables, and figures, and flagging the "telephone game" problem of citing statistics through reviews rather than primary sources. Four review modes are available (full-review, section, targeted, interactive), and findings are tagged with CRITICAL/MAJOR/MINOR severity.

What I learned about skill construction from the skill-creator framework: a skill is a SKILL.md file with YAML frontmatter (name and description, where the description drives triggering) and a Markdown body under ~500 lines. The description field should be somewhat "pushy" to combat under-triggering, including both positive triggers and explicit exclusions. The body should use imperative voice, explain why behind instructions rather than relying on heavy MUST/NEVER directives, include concrete examples, and keep things general enough to work across many inputs rather than overfitting to specific test cases. Bundled resources (scripts, reference files, assets) go in subdirectories and are loaded on demand.

---

**Comparison of Kip Thorne and Wheeler with Barba/Sainani**

The three sources agree on a core set of principles but diverge substantially in scope, specificity, and emphasis.

**Where they agree:**

All three champion active voice, concision, and strong verbs. Barba's Pass 2 (nominalization resurrection, passive-to-active conversion) maps directly onto Wheeler's "Power of the active" and "Suppress the verb 'to be,'" and onto Kip's advice about clear, flowing prose. All three would look at a sentence like "An investigation was carried out by the authors" and want it rebuilt as "We investigated." Similarly, all three want clutter eliminated — Barba provides a lookup table for it, Kip says the body should be "as concise as they would like," and Wheeler's triple imperative "Simplify! Simplify! Simplify!" says it most memorably.

All three also insist on audience awareness, though they frame it differently. Kip provides the most detailed treatment, with his hierarchy of audiences (title → abstract → introduction → figures → body → appendices) and his injunction to write each section for the specific audience that will read it. Barba's skill respects disciplinary conventions and asks about the target journal, but operates at a different level of granularity. Wheeler addresses audience implicitly through his emphasis on motivation and accessibility.

**Where Kip and Wheeler add something Barba's skill lacks:**

The most significant gap is *document-level architecture*. Kip devotes his entire Section II to the organizational structure of a paper — the insight that material is inherently nonlinear and requires figures, footnotes, appendices, and boxes (à la Misner-Thorne-Wheeler) to preserve that nonlinearity in a linear presentation. His audience-stratification framework, where each section of the paper serves a different readership of decreasing size, is a powerful organizing principle that Barba's sentence-level review tool does not address.

Kip's Section I on the *writing process itself* — the sequence of outlines from random brainstorm to organized categories, the organic growth of the body, the practice of writing the abstract last, and the discipline of checking all equations from scratch without looking at the original derivations — is mentoring advice aimed at the writer before and during composition. Barba's skill is a post-hoc review instrument. These serve complementary but quite different functions.

*Equations as prose* is entirely absent from Barba's skill and thoroughly treated by Kip: punctuate equations as part of the sentence, do not use mathematical symbols as verbs, do not begin sentences with symbols, number every equation a reader might want to reference, and give explicit verbal instructions for how equations are obtained. This is essential for physics papers and irrelevant for, say, epidemiology — which explains the gap, but it means the skill needs augmentation for your purposes.

*Figures* get an entire section from Kip (with Wheeler and Penrose held up as exemplars), but only appear in Barba's skill as items to cross-check for numerical consistency and keyword usage.

*Scientific attribution and credit* — Kip's all-caps imperative about giving full credit as the paramount rule of scientific etiquette — appears in Barba's skill only as a check against secondary-source citation drift, not as a principle about intellectual honesty.

*Prose flow across paragraphs* — Kip's "connecting phraseology" advice, where the beginning of each paragraph refers back (often subtly) to the previous one to create smooth flow, and his techniques for navigating long arguments (introductory paragraphs that roadmap the argument, signpost sentences at the beginning and end of each section), are absent from Barba's sentence-architecture pass, which focuses within paragraphs rather than between them.

Wheeler contributes several powerful rules that have no counterpart in Barba's skill: *the power of the present tense* (avoid past tense unless talking about history), the power of the singular and specific ("the black hole" not "a black hole," "when" not "if" or "suppose"), the elimination of *-ing words *in favor of finite verbs, *key word placement* at the beginning or end of the sentence rather than buried in the middle, and the *rhetorical rule of threes* (three descriptors to triangulate an idea). Wheeler's overarching demand for motivation — that text should read like a detective story, every sentence quotable — introduces a dimension of narrative compulsion that neither Barba nor Kip explicitly addresses, though Kip achieves it implicitly by recommending Hawking's post-1973 introductions as models.

**Where Barba's skill adds something Kip and Wheeler lack:**

Barba's *keyword consistency audit* (the "Banana Rule") is operationally valuable and not stated by either Kip or Wheeler. Both assume disciplined terminology but neither makes it an explicit, checkable audit. The same is true for *acronym austerity* — the rule that non-standard acronyms created for author convenience should be eliminated.

The *numerical consistency checklist* — cross-checking sample sizes, percentages, and significant figures across abstract, tables, and figures — is a reviewer's quality-control step that neither Kip nor Wheeler addresses. Similarly, the *citation telephone-game audit* adds a dimension of source integrity that goes beyond Kip's advice to cite specific pages.

Most fundamentally, Barba's skill provides a *structured, repeatable review protocol* with severity tags and concrete revision suggestions. Kip and Wheeler provide principles for the writer; Barba provides a machine-actionable editorial checklist.

**One area of apparent tension:**

Kip warns against "resonating" repeated words in neighboring sentences, recommending varied phrasing to avoid distracting the reader. Barba's Banana Rule says the opposite for defined technical terms: never substitute synonyms, always use the exact same term. These are not actually contradictory — Kip is talking about ordinary English words, Barba about defined variables and group names — but the surface-level advice points in opposite directions and would need to be reconciled explicitly in a combined skill to avoid confusing the reviewer about when repetition is a virtue (technical terms) versus a vice (ordinary prose).

---

That's the landscape. The natural question for discussion: how do you want to layer the Kip and Wheeler material into the skill? I see at least three possible approaches — extending the existing passes with physics-specific content, adding new passes (equations, figures, document architecture, attribution), or restructuring the skill to separate sentence-level review from document-level review. Happy to think through any of these once you've had a look.

## Establish the framework for executing the task

### Prompt

Before we begin, note that we want to enhance Lorena’s structure but ultimately create the same architecture: a post-hoc review instrument that can be used in an algorithmic way to improve writing. Advice from Kip and Wheeler on the process of writing is not relevant to this use model, but you should encode this advice if you think that the manuscript you are given to review needs a more significant overhaul that LLM based editing. You can point the user to the advice on the writing process in these cases. But this should not overload the skill as a post-hoc review and editing tool. 

We will enhance Lorena’s skill in the following sequence. This is built in a hierarchical manner, so pay attention to the sequence as well as the instructions. 

Identify places where Kip’s and Wheeler’s advice complements and reinforces the advice in Lorena’s skill. You can then just use the information from Kip/Wheeler to augment the existing skill. Any changes here would augment, but not change, the existing skill architecture.

Then identify places where Kip/Wheeler contain advice that can be implemented WITHIN Lorena’s existing architecture by adding specific, contained functionality. For example, there could be a directive to check that equations are written as prose, which would fit into Lorena’s existing sentence-based architecture.

Then identify places where Kip/Wheeler contain advice that can be implemented AS A MINOR EXTENSION Lorena’s existing architecture. For example, a check for consistency per Kip’s advice ACROSS paragraphs and in addition to within them.

Then identify advice from Kip/Wheeler where implementation would DEVIATE from Lorena’s current architecture. That is, it could not be simply implemented in the way that Lorena implemented the skill. For example, advice about the process of writing: drafting, discussing, revision, etc.

Do not make any modifications to the skill yet. We are still in the analysis stage, not the implementation stage. 

If my instructions are clear, go ahead. If not ask for clarification.

### Reponse

Your instructions are clear. Here's the four-tier analysis.

**Tier 1: Augmentation of existing passes — same architecture, richer content**

These items reinforce principles already present in Lorena's skill. Implementation means adding examples, sub-checks, or lookup-table entries to passes that already exist.

**Pass 1 (Clutter Extraction) augmentations:**

Kip's *double negatives* — "not dissimilar," "does not lack," "not uncommon" — are a specific clutter pattern absent from Lorena's current lookup table. These add cognitive load without adding information. They fit naturally as additional entries in the dead-weight phrase table or as a flagging rule ("flag any clause containing two negatives").

Wheeler's *subjunctive avoidance* — "We would like to express the metric as..." is a dead-weight construction Lorena's current table doesn't catch. The conditional hedge ("would like to") delays the action. This is functionally identical to Lorena's existing "it is worth noting that" deletions: throat-clearing that can be stripped.

**Pass 2 (Active Voice and Verb Vitality) augmentations:**

Wheeler's *suppression of "to be"* extends Lorena's nominalization resurrection to a broader class of weak verb constructions. Lorena catches "provides a review of" → "reviews" (smothered verbs), but Wheeler's rule catches the simpler case where "is/are/was/were" appears without a nominalization and a stronger verb exists. Lorena's existing structure already has a table of smothered forms and resurrected verbs; Wheeler's examples ("He is happy" → "He beams happiness"; "Schwarzschild geometry is distinguished from..." → "Schwarzschild geometry distinguishes itself from...") would extend this table to non-nominalization cases.

Wheeler's *"-ing" word elimination* identifies another specific category of weak verb form not in Lorena's current pass: progressive/gerund constructions where a simple finite verb would be stronger. "The Earth is rotating" → "The Earth rotates"; "before escaping or plunging" → "before it escapes or plunges." This can be added as a sub-check alongside the nominalization check — same diagnostic logic (spot the weak pattern, identify the stronger replacement), just a different pattern to spot.

Wheeler's *power of the present tense* — using present tense for established results ("The study shows" rather than "The study showed") unless you're specifically narrating historical sequence. This augments Lorena's verb vitality pass with a tense-selection check. It's the same kind of operation as the passive→active conversion: spot a weaker form, flag it, suggest the stronger alternative.

**Pass 3 (Sentence Architecture) augmentations:**

Kip's *modifier placement rules* complement Lorena's existing buried-predicate audit. Lorena counts words between subject and verb. Kip adds three related checks: (a) keep modifiers near what they modify — don't let them dangle off in a distant part of the sentence; (b) don't split modifiers of the same word, with some in front and others behind; (c) avoid dangling participles. These are all specific, mechanically checkable sentence-structure issues that extend the buried-predicate concept without changing the architecture of Pass 3. Kip provides worked examples for each (the "spacetimes that are, in some suitable sense, similar to Schwarzschild" dangling-verb repair, the "these equations, when written in terms of partial derivatives..." split-modifier repair).

**Pass 5 (Numerical Consistency and Citation Integrity) augmentation:**

Kip's emphasis on *full attribution* — his statement that no rule of scientific etiquette is more important than giving clear credit for others' work, and making explicit which contributions in the paper are new versus prior — reinforces and extends Lorena's citation telephone-game audit. Lorena checks whether statistics are traced to primary sources. Kip's principle adds a complementary check: does the manuscript make clear the boundary between the  authors' new contributions and prior work? This fits as an additional item in the citation integrity checklist.

---

**Tier 2: New contained functionality within existing passes**

These are checks not currently present in Lorena's skill, but which fit cleanly within one of the five existing passes as a self-contained module. Each requires adding a new sub-section, not restructuring the pass.

**Pass 2 — Wheeler's power of the singular, specific, and committed:**

Wheeler's trio of rules ("anyone designing an earth satellite" not "those designing earth satellites"; "the black hole" not "a black hole"; "when" not "if" or "suppose") constitutes a coherent check for vague, plural, hedged construction versus committed, specific, definite construction. This operates at the word/phrase level and fits within Pass 2 because it's about replacing weaker forms with stronger ones — the same logic as nominalization resurrection, just applied to nouns, articles, and conditionals rather than verbs. It could be implemented as a sub-section with its own small lookup pattern: flag plurals where a singular would be more forceful, flag indefinite articles where the definite would be more precise, flag conditional "if/suppose" where declarative "when" would be stronger.

**Pass 2 — Wheeler's infinitive construction preference:**

"To derive the invariance of the interval, use the Principle of Relativity" is structurally different from "We use the Principle of Relativity to derive the invariance of the interval." The infinitive-leading form puts the goal first and the method second, which Wheeler argues is more direct. This is a sentence-restructuring pattern that fits as a sub-check in Pass 2: when a sentence has a purpose clause ("in order to," "to derive," "to determine") buried after the method, flag it and suggest leading with the purpose.

**Pass 3 — Equations as prose (Kip):**

This is the most significant Tier 2 addition for physics manuscripts. Kip provides four specific, mechanically checkable rules: (a) equations must be punctuated as part of the prose — commas, semicolons, or periods at the ends of displayed equations; (b) mathematical symbols should not be used as verbs ("When A = B" is wrong; "When A is equal to B" is correct); (c) sentences should not begin with a mathematical symbol ("H is used to denote the horizon" is wrong; "The symbol H denotes the horizon" is correct); (d) built-up (multi-line) equations should not appear inline — they must be set off as display equations. These are all sentence-architecture checks that can be implemented as a contained "Equations in Prose" sub-section within Pass 3, parallel to the existing buried-predicate audit and punctuation-for-efficiency sub-sections. For manuscripts without equations, this sub-section simply returns no findings.

**Pass 3 — Voice and person consistency within paragraphs (Kip):**

Kip warns against changing voice (active to passive or vice versa) or changing the acting person ("one" to "they" to "you") mid-paragraph. This is a consistency check within individual paragraphs — the same granularity Pass 3 already operates at. It can be implemented as a sub-check: for each paragraph, identify the voice (active/passive) and grammatical person of the subject, and flag shifts that occur without clear rhetorical justification.

**Pass 3 — Word resonance detection (Kip):**

Kip identifies a specific readability problem: when the same non-technical word appears multiple times in neighboring sentences, the repetitions "resonate" in the reader's mind and become distracting. This is distinct from Lorena's Banana Rule (Pass 4), which says technical terms should be repeated. The word-resonance check flags non-technical repetition — ordinary English words like "approach," "significant," "based," "framework" that appear two or three times in adjacent sentences. Implementation: for each sentence pair, flag shared non-technical words (excluding defined terms, proper nouns, and common function words). Note the explicit exception Kip gives: deliberate repetition for parallel structure or as connectors is acceptable.

**Pass 3 — Key word placement (Wheeler):**

Wheeler's rule that the key word or concept in a sentence belongs at the beginning or at the end, not buried in the middle. This is a sentence-level structural check that complements Lorena's buried-predicate audit. The predicate audit checks that the verb isn't too far from the subject; the key-word-placement check verifies that the most important concept in the sentence occupies a position of emphasis. This is more subjective than the predicate audit but can be operationalized for flagging: when a sentence's main concept appears only in a subordinate clause or parenthetical in the middle of the sentence, suggest restructuring to front-load or end-load it.

---

**Tier 3: Minor extensions to existing architecture**

These require extending the scope of an existing pass beyond its current boundaries — typically from within-paragraph to across-paragraph, or from sentence-level to section-level. They preserve the five-pass structure but expand what a pass examines.

**Pass 3 extension — Cross-paragraph flow and connecting phraseology (Kip):**

Lorena's Pass 3 currently operates within paragraphs (sentence length variation, buried predicates, punctuation). Kip's most distinctive prose advice operates between paragraphs: the beginning of each paragraph should refer back, often subtly, to the previous paragraph or sentence, creating smooth flow rather than a feeling of discontinuous jumps. Without this "connecting phraseology," the reader loses the sense of where the argument has come from and where it's going. Extending Pass 3 to include a cross-paragraph coherence check would add a second scale of analysis. The check: for each paragraph transition, does the opening sentence of the new paragraph contain any backward reference (topical, logical, or verbal) to the preceding material? Flag transitions where the new paragraph introduces its topic with no connection to what came before.

**Pass 3 extension — Argument navigation and signpost sentences (Kip):**

Kip provides three specific techniques for making complex, multi-paragraph arguments readable: (a) an introductory paragraph at the beginning of a long argument that explains the argument is beginning, gives a rough idea of its length, and previews its pieces; (b) a topic sentence at the beginning of each piece saying what it will address, and a closing sentence saying the piece is finished; (c) parallel structure across the pieces. This extends Pass 3 to section-level flow — checking whether long technical arguments have the navigational infrastructure a reader needs. The check: for any argument spanning more than three paragraphs, does the section have a roadmap paragraph? Do the sub-sections have topic and closing sentences? This is more judgment-intensive than sentence-level checks but can be operationalized as a flagging heuristic.

**Pass 3 extension — Parallel structure audit across sentences (Kip):**

Kip emphasizes parallel structure — using the same grammatical form for items of the same logical type — as a major tool for making complex material readable, including his specific advice to use (i), (ii), (iii) or (a), (b), (c) numbering for items of similar logical sort, but not (1), (2), (3) because that can be confused with equation numbering. Lorena's Pass 3 currently checks sentence length variation but not whether logically parallel items use parallel grammatical forms. This extension would check whether lists, comparisons, and series within and across sentences maintain consistent structure.

**Pass 4 extension — Figure caption self-sufficiency (Kip):**

Kip observes that figures are seen by an audience nearly as large as reads the abstract, and recommends writing figure captions that enable the reader to understand the figure without reading the text. Lorena's Pass 4 currently checks that figure captions use the same terminology as the text. Extending this pass to also check whether captions are self-contained — do they identify what is being plotted, define any symbols or abbreviations, and state the main takeaway? — adds a new dimension to the keyword/terminology pass without changing its fundamental nature. It's a natural extension: from "are the terms consistent?" to "are the terms consistent and sufficient?"

**Pass 4 extension — Acronym definition in figure/table legends (Lorena already partially addresses this):**

Lorena already states that acronyms should be defined in the abstract, main text, and each table/figure legend, since readers don't read linearly. This is more of a confirmation that the existing architecture supports this, but Kip's advice about figure captions as standalone documents reinforces the principle and might warrant a more explicit check: for each figure/table, are all acronyms used in the caption defined within that caption?

**Rhetorical rule of threes (Wheeler):**

When a new concept or term is introduced, Wheeler recommends providing three complementary descriptors to triangulate the idea ("proper time, interval, wristwatch time" or "Schwarzschild radial coordinate, r, reduced circumference"). This operates at the concept-introduction level — higher than sentence, lower than section. It extends Pass 4 (terminology) by checking not just that terms are consistent, but that key terms are adequately introduced with enough descriptive context for the reader to grasp them. This is a softer check than Lorena's current binary "is the same term used?" audit, and would flag cases where a technical term appears without adequate introduction.

---

**Tier 4: Deviates from current architecture**

These items cannot be implemented as review checks within the five-pass structure. They represent process advice, holistic judgments, or content-level assessments that fall outside the scope of a post-hoc sentence/paragraph review tool. The skill should recognize when a manuscript has problems that require this level of intervention and point the user to these resources.

**The writing process — outlining, drafting, organic revision (Kip Section I):**

Kip's advice about sequential outlines (random → categorized → organized → reworked), the organic growth of the body, writing the abstract last, and making at least two complete passes through the finished paper is mentoring advice about *how to write*, not *how to review*. The skill could include a diagnostic that fires when the review reveals pervasive structural problems — sections that don't serve their audience, an abstract that doesn't match the body, no clear logical progression — and recommend that the author step back to the outlining/restructuring stage rather than trying to fix the manuscript sentence by sentence.

**Figure quality and design (Kip Section III):**

Evaluating whether figures use effective perspective, shading, line weight, and visual design is a visual assessment outside the scope of a text-review tool. The skill's role here is limited to checking captions and terminology (covered in Tiers 1–3).

**Narrative motivation and compulsion (Wheeler):**

Wheeler's "Motivate! Motivate! Motivate!" and his "detective story" metaphor describe a holistic quality of writing — the reader's experience of being drawn forward through the text. This cannot be decomposed into a checklist. It's the emergent property of doing everything else well (active voice, strong verbs, clear structure, connecting phraseology, good signposting). The skill could include a holistic assessment note in the summary section that comments on overall narrative drive, but this is a qualitative judgment, not an algorithmic pass.

**Equation verification and derivation checking (Kip):**

Kip's advice to re-derive all equations from scratch is content review, which Lorena's skill explicitly excludes. The skill should continue to exclude this.

**Pre-publication critique and venue selection (Kip):**

Process advice about having others critique the article and choosing the right publication venue. Not reviewable post-hoc. The skill could note in its constraints section that it does not substitute for peer feedback, reinforcing what's already there.

**Audience-appropriate style calibration across sections (Kip):**

Kip's observation that a style appropriate for theoretical physicists is not appropriate for the Astrophysical Journal audience, and his example of Hawking and Ellis regretting the mathematical style of *The Large-Scale Structure of Spacetime*, is a holistic judgment about whether the register of the entire manuscript matches its intended readership. Individual sentences can be checked for clarity (Tiers 1–3), but the overall calibration of technical depth and stylistic register to audience is a document-level assessment that doesn't decompose into a pass. The skill could address this in a lightweight way by asking the user to specify the target journal and audience, then checking whether the introduction and abstract are accessible to non-specialists (per Kip's audience hierarchy), but this is closer to Tier 3 than Tier 4 and the check would be necessarily coarse.

---

That's the full four-tier decomposition. Ready to discuss before moving to implementation.

## Refine the framework

### Prompt

Good, I agree with your approach here. Before we move to implementation, two questions that may need you to do research:

You will be working with TeX/LaTeX source code for manuscripts. Do you have sufficient knowledge of TeX/LaTeX to implement Kip’s equations as prose across TeX/LaTeX math commands? That is, you should recognize that things like \begin{equation} are markup and ignored when parsing the document for prose, but the presence or absence of a period at the end if a displayed equation matters to the grammatical structure of the sentence.

Would it be helpful for you to read some of the authors that Kip cites as exemplars (e.g. Hawking or Thorne and Wheeler themselves) if you do, do this using research so as not to overflow the context window we are using to rebuild the skill.

Answer these questions, and do research if necessary, and then we will move to updating the skill if we both agree.

### Response

Good questions. Let me address them in order.

**Question 1 — LaTeX competence for equations-as-prose checking:**

Yes, I have sufficient working knowledge of LaTeX to implement this. The key distinctions the skill would need to handle:

Displayed equation environments (`\begin{equation}`, `\begin{align}`, `\begin{eqnarray}`, `\[...\]`, `$$...$$`) are block-level elements that interrupt prose flow but remain grammatically part of the surrounding sentences. The skill needs to check that the text preceding a displayed equation sets it up as part of a sentence, and that the equation itself ends with appropriate punctuation (period, comma, semicolon) matching its role in the sentence structure. Inline math (`$...$`, `\(...\)`) is part of the running text and should be treated as noun phrases or expressions within the sentence.

I can also recognize that LaTeX commands within math mode (`\frac{}{}`, `\int`, `\sum`, `\sqrt{}`, `\mathbf{}`, `\mathrm{}`, etc.) are markup — the skill should parse through them to the semantic content. And I can distinguish multi-line environments (`align`, `gather`, `multline`) where line-breaking and alignment decisions matter per Kip's advice about where to break long equations.

The specific checks I'd implement for Kip's rules: does the sentence surrounding a displayed equation read grammatically if you mentally replace the equation with "this expression"? Does the equation end with punctuation? Does the preceding text explain how the equation was obtained (per Kip's directive about giving readers derivation instructions)? Does the text avoid using math symbols as verbs (i.e., does it not say "When A=BA = B
A=B" but rather "When AA
A is equal to BB
B")? Does any sentence begin with a bare math symbol?

I'm confident on the LaTeX parsing. If there's a specific edge case you're worried about — say, `amsthm` theorem environments, or unusual equation markup conventions in CE documents — flag it and I'll check.

**Question 2 — Reading exemplar authors:**

I think this would be valuable but narrowly targeted. I don't need to read Hawking or Penrose or MTW for general stylistic absorption — I already know their writing well enough to recognize what Kip is pointing to. What would actually help is reading one or two short examples where the principles are executed well, specifically to extract *patterns that can be operationalized as checks*. For instance, reading a Hawking post-1973 introduction would help me write a more concrete description of what "accessible to non-specialists" looks like in practice for the section-level audience check, versus just citing the principle abstractly.

But I want to be disciplined about this. The risk is that reading exemplars expands the context window with material that makes me better at writing but doesn't translate into better *review instructions* for the skill. The skill needs to tell Claude what to flag and how to fix it, not how to channel Hawking's voice.

My recommendation: I do a focused research pass on two specific things — (a) a brief look at how the best physics papers handle the equations-as-prose issue in practice, to make sure my LaTeX checks are calibrated to actual conventions rather than just Kip's prescriptions (since some of Kip's 1987 formatting advice may have evolved), and (b) a quick check on whether there are any widely cited updates or extensions to the Sainani/Thorne/Wheeler writing principles that we should be aware of (e.g., Sainani has published some material beyond the video course). This keeps the research targeted at improving the skill rather than broadening my general appreciation of good physics prose.

Shall I run that focused research, or would you rather skip it and proceed directly to implementation? I'm genuinely uncertain whether the marginal value exceeds the context-window cost, so I'll defer to your judgment on this one.

## Perform research to augment knowledge

### Prompt

Do the focused research using deep research mode so that it creates a research artifact that won’t overwhelm the context window.

### Response

The research question is clear and specific enough to launch directly. Let me kick this off.

Your research brief on equations-as-prose conventions and the Sainani/Thorne/Wheeler writing principles is ready. It covers how major physics/astronomy journals (APS, MNRAS, AAS, IOP/CQG) handle equation punctuation, traces the lineage of Thorne's 1987 rules through Knuth and Higham, evaluates the empirical evidence behind "cut clutter" and anti-jargon advice (including counter-evidence from Weinberger et al. and Hyland's hedging work), and reviews existing AI prior art like `labarba/sciwrite`. It closes with a staged build plan separating hard typographic checks from soft stylistic heuristics, plus journal-specific style profiles and calibration caveats.

## Techincal augmentation of skill

### Prompt

One last thing before we update Lorena’s skill. I have cloned Lorena’s GitHub repository to https://github.com/duncan-brown/sciwrite and we are going to check my updates to the skill in there. Load the su-chart-of-accounts skill to understand how I version my skills and maintain them in GitHub. Make sure you understand how you would add version and date information and update Lorena’s skill in my GitHub repository, preserving the history. Since this is just a simple SKILL.md you don’t need to worry about the zip file in the dust directory (unless you need to add asset files, if you do, let’s discuss first). Load this and tell me if you are ready to update the skill, update the README and How to use file, and check it in to my GitHub repository.

### Response

I now have a clear picture of your versioning conventions and the repo structure. Here's what I understand and what I can do:

**Your versioning pattern** (from su-chart-of-accounts): a version block right after the title (Skill Version, Created, Last Updated), a reverse-chronological Version History section with per-version changelogs, and Version Update Instructions. For the sciwrite fork, this means Lorena's original becomes v1.0, and our enhanced version becomes v2.0 (given the scope of changes — new passes, new sub-checks, physics-specific functionality — this warrants a major version bump, which I'd confirm with you before finalizing).

**Your repo** at duncan-brown/sciwrite is a fork of labarba/sciwrite with 5 commits on main. It contains SKILL.md, README.md, HOW-TO-USE.md, and LICENSE (CC-BY 4.0). No dist directory, no bundled scripts or assets — just the three markdown files and the license. The fork relationship preserves Lorena's commit history.

**What I can do:** Create the updated SKILL.md, README.md, and HOW-TO-USE.md locally, present them to you for review, and provide the exact git commands to commit and push to your fork. I don't anticipate needing additional asset files for this skill — the enhancements are all instruction-based (new sub-checks, lookup tables, LaTeX-aware directives) rather than script-based, so the single-SKILL.md architecture holds.

**What I cannot do from here:** Network egress is disabled in this environment, so I can't clone the repo, make commits, or push directly. You'll need to do the git operations yourself (or I can provide a script).

**My plan for the update:**

The SKILL.md gets versioned as v2.0, with Lorena's original documented as v1.0 in the changelog. I'll add the version block, history, and all Tier 1–3 enhancements we agreed on. The README gets updated to credit Thorne and Wheeler as additional sources alongside Sainani, document the physics/LaTeX extensions, and note your fork's relationship to Lorena's original. The HOW-TO-USE gets physics-specific example prompts (e.g., "check my equations are punctuated as prose," "review this LaTeX section for sentence-initial symbols").

Ready to proceed with implementation if you are.

## Execute

### Prompt

Yes, go ahead. Make sure you faithfully implement what we planned and do not get too side tracked by the information in the research artifact.

### Response

Let me start by reading the current SKILL.md I saved locally, then build the updated version systematically following our four-tier plan.

Now let me read the skill-creator's guidance on line limits one more time to calibrate.

Good — 500-line target, currently at 247. I have room for the enhancements. Let me build the updated SKILL.md now.

419 lines — well within the 500-line limit. Now the README.

Now the HOW-TO-USE.

Here are all three files. SKILL.md is 419 lines (under the 500-line target), README.md is 109, HOW-TO-USE.md is 180.

**What I implemented, by tier:**

**Tier 1 (augmentation of existing passes): **Double negatives and subjunctive-avoidance in Pass 1. "To be" suppression, "-ing" elimination, and present-tense preference in Pass 2. Modifier placement and dangling participles in Pass 3. Attribution clarity in Pass 5. Hedging allowlist added to Pass 1 to prevent over-aggressive clutter removal.

**Tier 2 (new contained functionality):** Wheeler's singular/specific/committed construction and infinitive-leading sentences in Pass 2. Equations-as-prose sub-pass in Pass 3 with all four checks (terminal punctuation, sentence-initial symbols, symbols-as-verbs, inline built-up expressions) and LaTeX parsing guidance. Voice/person consistency, word resonance detection, and key-word placement in Pass 3.

**Tier 3 (minor extensions):** Cross-paragraph flow and argument navigation checks in Pass 3. Parallel structure audit in Pass 3. Figure caption self-sufficiency in Pass 4.

**Tier 4 (pointer only):** Structural Assessment section that fires when pervasive problems suggest the manuscript needs restructuring before sentence-level editing, with a reference to Thorne's writing-process advice.

To commit to your fork:

```
cd /path/to/sciwrite
cp /path/to/downloaded/SKILL.md .
cp /path/to/downloaded/README.md .
cp /path/to/downloaded/HOW-TO-USE.md .
git add SKILL.md README.md HOW-TO-USE.md
git commit -m "v2.0: Add Thorne/Wheeler physics writing principles

- Pass 1: double negatives, subjunctive checks, hedging allowlist
- Pass 2: to-be suppression, -ing elimination, present tense,
  singular/specific, infinitive-leading construction
- Pass 3: modifier placement, equations-as-prose (LaTeX), cross-paragraph
  flow, argument navigation, parallel structure, word resonance,
  key-word placement, voice/person consistency
- Pass 4: figure caption self-sufficiency
- Pass 5: attribution clarity
- Structural assessment diagnostic for manuscripts needing overhaul
- Updated description to trigger on LaTeX/physics manuscripts"
git tag v2.0
git push origin main --tags
```
      