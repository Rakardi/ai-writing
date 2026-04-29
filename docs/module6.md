# Prompt Library

!!! tip "How to use this module"
    
    Unlike the modules before it, this one is a **reference, not a read-through**. You don't need to work through every prompt to complete the course — skim the structure, note what's here, and come back when a real task on your desk matches one of the entries. The prompts are organized by stage of the writing process so you can find the right one fast. Treat this module the way you'd treat the glossary: useful when you need it, not homework.

If [Prompt Engineering](module4.md) taught you the anatomy of a prompt and [AI in the Technical Writing Process](module5.md) walked you through the shape of the technical writing process, this module gives you the raw material — a working collection of prompts, one for every place in the process where AI most often earns its keep.

Think of what follows as a phrasebook rather than a script. A phrasebook gives you the sentences that work in recognizable situations; it doesn't tell you exactly what to say in every conversation. Every prompt below is a starting point. Your product, your audience, your voice, and your constraints aren't in the prompt yet — that's the part you bring. Try one, adapt it, notice what changed, and keep the version that worked for you.

## How this library is organized

The twenty prompts below are organized by **stage of the technical writing process**, matching the stages introduced in AI in the Technical Writing Process: Preparation, Research, Organization, Writing, Revision, Publication & Maintenance. That way, when a task lands on your desk, you can find the stage, find the prompt closest to your need, and adapt from there.

Each prompt is also **tagged with the techniques from Prompt Engineering** it leans on — zero-shot, few-shot, chain-of-thought, role-based, self-consistency, prompt chaining, meta-prompting. You won't need to memorize the tags; they're there so that if you want to deepen a specific technique, you can filter by it.

A small legend:

| Tag | What it means |
|---|---|
| **Zero-shot** | No examples provided; the model works from instructions alone. |
| **Few-shot** | One or more worked examples are included to tune tone, format, or edge-case handling. |
| **Chain-of-thought** | The model is asked to reason through the task in explicit steps. |
| **Role-based** | The model is assigned a persona or perspective to shape its output. |
| **Self-consistency** | Multiple independent responses are requested so you can compare or pick the best. |
| **Prompt chaining** | The task is broken into a sequence of smaller prompts, each feeding the next. |
| **Meta-prompting** | The model is asked to critique or improve a prompt before running it. |

## A consistent anatomy for every prompt

Each of the twenty prompts follows the same structure, so you can scan quickly:

- **When to reach for it** — the situation the prompt fits.
- **Techniques used** — the Module 4 tags.
- **The prompt** — the actual text, in a fenced block so you can copy cleanly.
- **What to watch for in the output** — the failure modes this prompt is most susceptible to.
- **How to adapt** — the knobs most worth turning for your own work.

> 💡 **Try this before you read further.** Pick one stage of your current project — Preparation, Research, anything — and hold a real task in mind as you read the corresponding section. A prompt you read with a real task in view lands differently from a prompt you read in the abstract. You'll notice which details are already right for you and which you'll want to change.

> ⚠️ **A reminder from Module 1.** Every prompt below asks you to paste something — a brief, a spec, source material, a draft. Before you paste, run the *Before You Paste* checklist. A sanitized input is cheaper than any conversation you'll have after a data leak.


## Preparation

The preparation stage is where the shape of the project is decided. AI is surprisingly useful here — not to make the decisions, but to make sure you've considered the full space of options before you commit.

### Prompt 1.1 — The "What Am I Missing?" Brief Review

**When to reach for it.** You've received a brief and you can't quite tell whether it's complete. Something feels off — a missing stakeholder, an unstated constraint, an ambiguity you'll regret in week three — but you can't put your finger on it.

**Techniques used.** Role-based, chain-of-thought, meta-prompting (the brief becomes the "prompt" the model critiques).

**The prompt:**

```
You are a senior technical writing lead with 15 years of experience
scoping documentation projects. I'm about to accept the following
documentation brief. Before I commit, review it with a skeptical eye.

Think step by step:
1. List every assumption this brief is making — both stated and unstated.
2. List every stakeholder implied by the brief but not named.
3. List every ambiguity that could lead to rework if not clarified now.
4. List every question I should ask before accepting this brief.

Be specific. Prefer concrete observations about this brief over
generic project-management advice.

Brief:
[paste brief]
```

**What to watch for in the output.**

- Generic project-management platitudes ("make sure to communicate with stakeholders"). If you see them, re-run with the instruction to be more specific.
- Overconfident inference about your organization. The model will sometimes guess at your context; treat those guesses as prompts for your own thinking, not facts.
- A list that's exhaustive but not prioritized. Ask a follow-up: *"Of these, which three would matter most if left unresolved?"*

**How to adapt.**

- Swap the role ("senior documentation manager," "lead UX writer," "compliance-focused technical editor") to change the lens.
- Add a "What I already know" paragraph before the brief to save the model from speculating about your context.


### Prompt 1.2 — Three-Persona Audience Sketch (with Diversity Pressure)

**When to reach for it.** You need audience personas fast, and you want them to be varied enough to surface real differences in reading behavior — not three personas who all turn out to be "a developer, but slightly different."

**Techniques used.** Role-based, few-shot, self-consistency (variety is the point).

**The prompt:**

```
You are a user researcher specializing in documentation audiences.

Product: [describe product in 2–3 sentences]
Primary purpose of the documentation: [describe purpose]

Create three user personas who are genuinely different from each
other — not three variants of the same person. They should differ
along at least three of these dimensions: technical background,
attitude toward reading documentation (supportive / skeptical /
reluctant), preferred format, country or region of origin, time
pressure, prior product exposure.

For each persona, include:
- Name and role
- Technical background (concrete, not "technical" or "non-technical")
- Primary goal when using this documentation
- What would make them abandon the documentation halfway through
- Preferred format (video, step-by-step, reference, search)

Before you write the personas, briefly list the three dimensions
along which you've chosen to vary them.

Example of the kind of specificity I'm looking for (style only —
not content):

  Mei, 34, DevOps engineer at a mid-size fintech in Singapore.
  Comfortable at the command line; impatient with marketing prose;
  skims aggressively and bails if the first code block doesn't run.
  Reads docs while debugging, not before.
```

**What to watch for in the output.**

- Three personas who are secretly the same person. Re-run asking explicitly: *"Make persona 2 someone who would disagree with persona 1 about how this documentation should be written."*
- Names and geographies used as set dressing, with no impact on how the persona reads. Push back: *"Why does persona 3's location actually change how they use this doc?"*
- Personas that match the brief's assumed audience too comfortably. The value here is pressure-testing; at least one persona should make you slightly uncomfortable.

**How to adapt.**

- Replace the example with a real persona from your own past work to steer the style more precisely.
- If your product serves both consumers and professionals, ask for five personas split across both.
- For regulated industries, add a dimension: "relationship to compliance (resents it / tolerates it / champions it)."


### Prompt 1.3 — Oversight Gate Map for a Planned Workflow

**When to reach for it.** You're sketching a documentation workflow that will involve AI, maybe just a recurring AI-assisted draft. You want to decide *where the humans look* before you build the workflow, not after something goes wrong.

**Techniques used.** Role-based, chain-of-thought.

**The prompt:**

```
You are a workflow designer specializing in AI-assisted documentation
pipelines. I'm designing the following workflow:

[describe workflow — trigger, steps, systems touched, outputs]

Identify the decision points where a human reviewer must approve
or intervene before the process continues. For each gate, specify:

1. What the reviewer is checking for (be concrete — "accuracy" is
   not an answer; "the breaking-change classification is correct"
   is an answer).
2. What a passing result looks like.
3. What would trigger escalation to someone more senior.
4. What happens if the reviewer is unavailable.

Think step by step. Before listing the gates, briefly explain how
you decided where they belong. If you see a place I've designed a
gate in but that you think is unnecessary, say so. If you see a
place I haven't designed a gate in but should have, say so.
```

**What to watch for in the output.**

- Gates placed at every step, which defeats the purpose. Push back: *"Which two or three of these gates are truly non-negotiable? Which ones could we drop if the workflow proves reliable?"*
- Vague check criteria ("the output is good"). Ask for concrete, observable criteria.
- Missing failure-mode gates — the ones triggered when something goes *wrong* rather than when something proceeds normally.

**How to adapt.**

- For low-stakes internal workflows, ask for a minimal-gates version and a maximal-gates version; the contrast is informative.
- For high-stakes or regulated content, add: *"Assume that any published error will trigger a post-incident review. Design the gates accordingly."*
- Reuse the output as a checklist during workflow testing — gates are where bugs hide.


## Research

The research stage is where raw material enters the pipeline. AI is excellent at processing volume — long specs, large ticket batches, wall-of-text wikis — and terrible at noticing what's not there. The prompts below lean on the first strength while designing around the second.

### Prompt 2.1 — Source-Grounded Summary with Gaps Flagged

**When to reach for it.** You have a long or messy source document — a spec, a wiki cluster, a transcript, a design doc — and you need to extract what matters for a specific documentation task without reading every word.

**Techniques used.** Role-based, chain-of-thought, zero-shot.

**The prompt:**

```
You are a technical editor preparing research notes for a writer
who will document [product feature]. Your audience for these notes
is the writer — not the end user.

Summarize the following source material for that purpose. Do not
summarize everything; summarize what the writer actually needs.

Structure your response in four sections:

1. What the feature does (one paragraph, plain language).
2. Who it is for (describe the primary and secondary user, with
   evidence from the source).
3. Known edge cases, constraints, or limitations (list).
4. Things a user might misunderstand (list).

Then add a fifth section, titled GAPS AND CONTRADICTIONS. In it,
flag:
- Anything the source material implies but does not state.
- Any points where two parts of the source disagree.
- Any claims that would need verification from an SME before
  publication.

If a section would be empty, say so explicitly rather than
inventing content to fill it.

Source material:
[paste content]
```

**What to watch for in the output.**

- An empty GAPS section filled in to look complete. The whole point of that section is for the model to admit what's missing; if it's suspiciously tidy, re-run with: *"Re-examine the source. I expect at least two genuine gaps. If you can't find them, say so directly."*
- Claims in the summary that don't actually appear in the source. Spot-check two or three before trusting the rest.
- A "summary" that's nearly as long as the source. Ask for a target length: *"Keep section 1 under 100 words."*

**How to adapt.**

- For very long sources, use prompt chaining: ask first for the structure and TOC of the source, then summarize one section at a time.
- For sources with code or API definitions, add: *"Quote any signatures, endpoint paths, or configuration keys exactly; do not paraphrase them."*
- Reuse this prompt's output as the briefing document you bring into an SME interview — it surfaces your questions for you.


### Prompt 2.2 — SME Interview Question Generator

**When to reach for it.** You have 30 minutes on an SME's calendar next week and you want to spend them well. You've done the reading, you have a rough model of the feature, and you now need the right questions to fill the gaps.

**Techniques used.** Role-based, chain-of-thought, few-shot.

**The prompt:**

```
You are an experienced technical writer preparing for a 30-minute
interview with a subject matter expert. I have limited time and I
need the highest-signal questions.

Context I already have:
[paste your current understanding of the feature — the output of
Prompt 2.1 works well here]

Known gaps I still need to close:
[list your gaps]

Generate 8–12 interview questions, grouped into three categories:

1. Understanding questions — to confirm my model is correct.
2. Gap-closing questions — to fill the known gaps above.
3. Risk-surfacing questions — to uncover edge cases, failure modes,
   or disagreements that the SME might not volunteer.

For each question, briefly note (one line) why it's worth asking.

Avoid questions the SME can answer with "yes" or "no" unless a
yes/no answer genuinely closes the gap.

Example of the tone I want:

  "Walk me through what happens when a user submits this form
  with an expired token — what does the system actually do, and
  what do you want the docs to say it does?"

  (Worth asking because the spec is silent on token expiry, and
  the answer determines whether we need a dedicated troubleshooting
  section.)
```

**What to watch for in the output.**

- Questions the SME will find insulting because you should already know the answer. Before the interview, scan the list and cut any question your own reading already answered.
- Questions that are actually two or three questions stacked together. Split them; you'll get better answers.
- No risk-surfacing questions, or risk questions that are vague ("are there any edge cases?"). Push for specific, hypothesis-shaped questions.

**How to adapt.**

- For a recurring SME relationship, add: *"Avoid questions we've covered in previous interviews — here's a summary: [paste]."*
- For a hostile or time-poor SME, ask the model to reorder the questions so that if the interview is cut to 10 minutes, the most valuable questions come first.
- Keep the unasked questions in a parking lot — they often become the outline of the FAQ.


### Prompt 2.3 — User Feedback Clustering with Evidence

**When to reach for it.** You have a pile of user feedback — support tickets, survey responses, forum posts, review comments — and you need to understand the shape of the complaints before you decide what the docs should change.

**Techniques used.** Chain-of-thought, self-consistency (cluster stability is a signal), role-based.

**The prompt:**

```
You are a documentation analyst. I'm going to paste user feedback
about [product / feature]. Cluster it into themes and help me see
what the data is telling me.

Think step by step:

1. Read through the entire set before clustering.
2. Propose 4–7 clusters. Each cluster should be specific enough
   that I can act on it ("users can't find the reset-password
   flow") rather than generic ("usability issues").
3. For each cluster, list:
   - The theme, in one sentence.
   - How many items fall into it (approximate is fine).
   - Two or three representative quotes, verbatim from the source.
   - Whether this looks like a documentation problem, a product
     problem, or both.
4. Flag any items that don't fit cleanly into any cluster —
   outliers are often the most interesting signal.

After the clusters, add a section titled WHAT THIS DATA DOES NOT
TELL US. In it, note the questions that the feedback raises but
cannot answer — things that would need a user interview or a
product-analytics query to resolve.

Feedback:
[paste feedback]
```

**What to watch for in the output.**

- Clusters that are really one big "usability" bucket in disguise. Ask: *"Split the largest cluster into two clusters with sharper boundaries."*
- Quotes that don't appear in the source material (rare, but possible). Spot-check.
- A missing "doc problem vs. product problem" split. This distinction determines whether your work ends with a rewrite or a ticket; don't let it slide.

**How to adapt.**

- Run the prompt twice with the same input and compare cluster structures. If the two runs largely agree, the signal is real. If they disagree, your data is noisier than it looks.
- For multilingual feedback, add: *"Preserve quotes in their original language; translate only the cluster summaries."*
- When feedback is large, chain: cluster one source first, then feed the cluster summaries back in with a new batch and ask the model to merge.


## Organization

Organization is where structure is decided — outlines, hierarchies, sequencing, cross-references. AI is a capable thinking partner here, but structure is also where *your* judgment about the reader is most visible. Use these prompts to generate options, not to outsource the decision.

### Prompt 3.1 — Outline in Three Different Shapes

**When to reach for it.** You're outlining a new piece of documentation and you suspect the first shape that came to mind is just *a* shape, not *the* shape. You want to see the alternatives before you commit.

**Techniques used.** Role-based, self-consistency (diversity of structure is the point), chain-of-thought.

**The prompt:**

```
You are an information architect for technical documentation. I'm
outlining the following piece of content:

Topic: [topic]
Audience: [primary audience — use a persona from Prompt 1.2 if you
have one]
Primary user goal: [what the reader is trying to accomplish]
Length target: [rough word count or section count]

Produce three different outlines for this content. Each outline
should use a genuinely different organizing principle — not three
variants of the same structure.

Suggested organizing principles to choose from:
- Task-ordered (what the reader does, step by step)
- Concept-first (what the reader needs to understand before acting)
- Decision-tree (branches by the reader's situation)
- Reference-shaped (optimized for lookup, not reading)
- Problem-first (starts from the reader's pain and works outward)
- Progressive disclosure (quick start → fuller explanation → deep reference)

For each outline:
1. Name the organizing principle.
2. Give the section hierarchy (three levels deep is enough).
3. In one paragraph, describe the reader this outline serves best.
4. Note one risk or weakness of this shape.

After the three outlines, recommend one — and explain, in 3–4
sentences, why.
```

**What to watch for in the output.**

- Three outlines that are secretly the same shape with different headings. Ask: *"Outline 2 and Outline 3 feel structurally similar. Can you replace Outline 3 with something genuinely different?"*
- A recommendation that always picks the first outline. The model has a mild primacy bias; consider ignoring the recommendation and choosing on your own.
- Outlines that go too deep too fast. For a quick-start or overview, four or five top-level sections is often better than a dense tree.

**How to adapt.**

- If you already have a draft outline, paste it as a fourth option and ask the model to compare yours against the three it generated.
- For a series of related pages, run the prompt once per page and then ask the model to check that the resulting outlines work together — cross-page consistency is its own skill.


### Prompt 3.2 — Sequencing Check for a Task Flow

**When to reach for it.** You have the steps, roughly in the right order, but something about the sequence isn't quite right — maybe the prerequisites come after the action that needs them, or a concept is used before it's introduced.

**Techniques used.** Chain-of-thought, role-based.

**The prompt:**

```
You are reviewing a task-based documentation sequence for a first-
time reader who has never done this task before.

Here is my current sequence:
[paste numbered steps or section headings]

Walk through the sequence from the reader's perspective. Think
step by step:

1. At each step, ask: "Does the reader have everything they need
   to complete this step, from what has come before?" If not, note
   what's missing.
2. At each step, ask: "Is there a concept, term, or tool being used
   here that was not introduced earlier?" If so, note it.
3. At each step, ask: "Could the reader reasonably skip this step
   or do it in a different order?" If so, note it — the answer
   affects whether the step is mandatory or optional.

After the walk-through, propose a revised sequence. For each change
you make, state the reason in one sentence.

If the existing sequence is already sound, say so — do not invent
improvements to look useful.
```

**What to watch for in the output.**

- Suggested changes that are pure re-labeling rather than re-sequencing. Ask: *"Which of your changes actually change the order of operations, not just the wording?"*
- Missing the most common sequencing bug — a prerequisite buried mid-procedure. If the model doesn't catch it, prompt: *"Re-check: are any prerequisites mentioned only after they would already be needed?"*
- An overly aggressive rewrite. Ask for minimal changes if the draft is already close.

**How to adapt.**

- For cross-team procedures (where different roles do different steps), add: *"Flag any step where the actor changes — the reader needs a cue at every handoff."*
- Run this prompt after writing (Stage 4) as well as during outlining. Sequencing bugs often survive drafting and die only in review.


### Prompt 3.3 — Information Architecture Sanity Check

**When to reach for it.** You've sketched an IA for a larger doc set — a landing page, a sidebar, a full navigation tree — and you want a second opinion on whether a new reader could find their way.

**Techniques used.** Role-based, few-shot, chain-of-thought.

**The prompt:**

```
You are a first-time user of the following product, in the role of
[persona — reuse Prompt 1.2 output]. You have never seen this
documentation before and you have a specific task in mind.

Here is the proposed navigation structure:
[paste IA — page titles and hierarchy, two or three levels]

For each of the following user intents, trace the path the reader
would most likely follow through this IA. If the reader would
probably end up in the wrong place, say where they'd end up and why.

Intents to test:
1. [a common intent — e.g., "I installed it and it doesn't start."]
2. [a less common but valuable intent]
3. [an intent that could plausibly fit in more than one place]
4. [an intent a new user has but experienced users forget they had]

For each intent, produce:
- The path you think the reader would take (page → page → page).
- Whether they'd find what they needed, partly find it, or end up
  somewhere wrong.
- One change to the IA that would make this path clearer — or "no
  change needed" if the path is already good.

Example of the kind of trace I'm looking for:

  Intent: "I want to deploy this to production."
  Path: Home → Getting Started → "Your first deploy"
  Outcome: Partly. They find deploy instructions, but the
  production-specific caveats live under Reference → Deployment
  Configuration, which a new user is unlikely to check.
  Suggested change: Add a link from "Your first deploy" to the
  production caveats, or fold the caveats into the getting-started
  path.
```

**What to watch for in the output.**

- Paths that assume the reader will use search. Search is part of IA, but a healthy IA supports browsing too.
- Over-eager restructuring. The question is *where does the reader get lost*, not *how would you rebuild this*. If the model wants to redesign the whole tree, pull it back to specific intents.
- Missing failure modes for the "fits in more than one place" intent — that's the intent most likely to expose genuine IA weakness.

**How to adapt.**

- For large doc sets, run this prompt once per persona and compare traces. Conflicts across personas are often the signal for a landing page or a "choose your path" page.
- Feed in analytics data if you have it: *"The three most-searched terms in this doc set are X, Y, Z. Do those terms appear clearly in the IA?"*


## Writing

Writing is where most AI time goes, and where the temptation to accept a plausible-sounding draft is highest. The four prompts below span the drafting lifecycle — from a blank page, to a section expansion, to tone adjustment, to the specific failure modes of writing *with* AI rather than *against* it.

### Prompt 4.1 — First Draft from a Structured Outline

**When to reach for it.** You have an outline you trust (possibly from Prompt 3.1). You want a first draft to react to — something concrete enough that you can start editing rather than generating.

**Techniques used.** Role-based, zero-shot, few-shot (optional style example).

**The prompt:**

```
You are a technical writer drafting documentation for [product].

Audience: [persona or audience description]
Voice: clear, calm, specific. Prefer short sentences to long ones.
Use the second person ("you") to address the reader. Avoid
marketing language, avoid "simply" and "just," and avoid hedges
like "basically" or "essentially."

Here is the outline to draft from:
[paste outline]

Draft the content section by section, following the outline
exactly. For each section:
- Write no more than [N] words unless the section calls for more.
- Use concrete verbs. Where you would write "users can configure,"
  prefer "configure" or "to configure, do X."
- If the outline names a concept you can't define from the context
  I've given you, write [TK: define <concept>] instead of inventing
  a definition.
- If a code example is called for but you don't have enough
  information to write a real one, write [TK: code example — <what
  it should demonstrate>] instead of inventing one.

Here is a short sample of the voice I want (match the rhythm and
specificity, not the content):

  "Before you run the migration, take a snapshot of the database.
  The migration rewrites every row in the users table, and a rollback
  without a snapshot means restoring from the previous night's backup."
```

**What to watch for in the output.**

- Invented facts dressed as specifics. The [TK: ...] instruction is designed to catch this; if you see a suspiciously confident claim with no [TK] nearby, verify it.
- Drift into marketing voice even with the instruction. Reinforce with a second pass: *"Rewrite this draft removing every word that sounds like marketing. Show me the list of words you removed."*
- Over-length sections. Ask for a version trimmed by 30% — you'll often like it better.

**How to adapt.**

- Replace the voice sample with a real paragraph from your own doc set. This single change has more effect than almost any other knob.
- For product families with a strict style guide, paste the relevant rules (not the whole guide) into the voice section.
- If the outline is very long, use prompt chaining: draft one section per turn, editing as you go, rather than asking for the whole thing at once.


### Prompt 4.2 — Expanding a Stub into a Full Explanation

**When to reach for it.** You have a section that's more placeholder than content — a heading and a sentence, or a bullet list you meant to flesh out. You want a first pass at the full text, grounded in source material you trust.

**Techniques used.** Role-based, chain-of-thought, few-shot.

**The prompt:**

```
You are a technical writer expanding a stub into a full section.

Section heading: [heading]
Current stub: [paste what you have]
Source material I trust: [paste spec excerpts, prior docs, SME notes]
Audience: [persona]
Target length: [word count or paragraph count]

Before you expand, do this silently:
1. Identify everything the stub implies but doesn't state.
2. Check whether the source material actually supports those
   implications.
3. If the source material is silent on something the expanded
   section would need, note it as [TK: confirm with SME — <what>].

Then write the expanded section. Rules:
- Every factual claim must be traceable to the source material.
  If it isn't, mark it [TK].
- Keep the stub's existing sentences where they still work; don't
  rewrite for the sake of rewriting.
- End with a "See also" bullet list of 2–3 related topics, if and
  only if they appear in the source material.

Example of the density I want (style only):

  "The scheduler runs every five minutes. If a job fails, the
  scheduler retries it up to three times with exponential backoff,
  then moves it to the dead-letter queue. Jobs in the dead-letter
  queue are not retried automatically; an operator must requeue them."
```

**What to watch for in the output.**

- Claims that overshoot the source. The [TK] discipline helps; spot-check anyway.
- "See also" lists that invent topics that don't exist in your doc set. Verify every link target is real.
- A rewrite of the stub's existing sentences, even when they worked. If it happens, re-run with: *"Preserve the original stub's sentences verbatim wherever they fit; expand around them."*

**How to adapt.**

- For concept-heavy sections, add: *"Define every term the first time it appears. If a term needs more than one sentence to define, it deserves its own subsection — flag it."*
- For procedure-heavy sections, switch the example to a procedural one and ask the model to use numbered steps for any sequence of three or more actions.


### Prompt 4.3 — Tone Shift Without Losing Meaning

**When to reach for it.** You have a draft that's accurate but the voice is wrong for the audience — too formal, too casual, too jargon-dense, too cautious. You want to shift the tone without touching the facts.

**Techniques used.** Few-shot, role-based, chain-of-thought.

**The prompt:**

```
You are a technical editor. I have a draft whose content is correct
but whose tone is wrong for the audience. Shift the tone without
changing any facts.

Current draft:
[paste draft]

Current tone, in my words: [describe — e.g., "stiff, overly formal,
sounds like a legal notice"]
Target tone, in my words: [describe — e.g., "clear and direct, like
a senior engineer explaining something to a peer over coffee"]

Before you rewrite, do this:
1. List the three most tone-defining patterns in the current draft
   (specific word choices, sentence shapes, rhetorical habits).
2. Propose the replacement patterns that would land the target
   tone.

Then rewrite. Rules:
- Do not add, remove, or alter any factual claim. If you think a
  claim is wrong, do not fix it — flag it as [CHECK: <claim>] and
  leave it for me.
- Preserve every number, name, code block, and cross-reference
  exactly.
- If a sentence cannot be tonally shifted without losing meaning,
  leave it and note why.

Example pairs of the shift I want (tone only, not content):

  Before: "It is recommended that the user ensure the configuration
  file is properly formatted prior to execution."
  After:  "Check that your configuration file is valid before you
  run the command."
```

**What to watch for in the output.**

- Silent factual edits. Do a diff-style read: line by line, does every number and name still match?
- Over-correction in the opposite direction. A "friendly" rewrite that slides into cute or patronizing is worse than the original. Ask for a middle version.
- Loss of precision in the name of clarity. Sometimes the formal sentence was formal for a reason (regulated content, legal exposure). The [CHECK] convention helps surface those.

**How to adapt.**

- For long documents, shift tone section by section rather than all at once — mid-document drift is common.
- Keep your before/after example pairs in a personal style file. Over time they become a more reliable tone-steering tool than any adjective.


### Prompt 4.4 — Catching AI's Characteristic Writing Tells

**When to reach for it.** You've written a draft *with* AI assistance and you want a final pass specifically tuned for the patterns AI-assisted drafts fall into — the telltale rhythms, the filler phrases, the hedges, the transitions that don't transition to anything.

**Techniques used.** Role-based, few-shot, meta-prompting (you're asking the model to critique the kind of output it typically produces).

**The prompt:**

```
You are a skeptical technical editor. This draft was written with
AI assistance and may carry the characteristic patterns of AI-
assisted writing. Do a pass specifically aimed at removing them.

Draft:
[paste draft]

Look for and propose edits to each of the following patterns, and
any you notice that aren't on this list:

1. Throat-clearing openings. ("In today's fast-paced world…",
   "It is important to note that…", "When it comes to X…")
2. Empty intensifiers. ("very," "really," "quite," "simply,"
   "just," "basically," "essentially.")
3. Bidirectional hedging. ("may or may not," "can sometimes,"
   "often tends to.")
4. Tricolon filler. Three-item lists where one or two of the items
   exist only to make the list a triple.
5. Transition words that don't transition. ("Moreover,"
   "Furthermore," "Additionally," when no actual addition follows.)
6. Definitional padding. ("X, which is a kind of Y that…") when the
   audience already knows what X is.
7. Self-referential meta-sentences. ("This section will explain…",
   "As we have seen…", "It is worth mentioning that…")
8. False balance. Cautious "on the one hand / on the other hand"
   framing where the draft actually has a clear position.

For each edit you propose:
- Quote the original phrase.
- Give the replacement.
- In five words or fewer, name the pattern.

At the end, note any patterns the draft does *not* exhibit — this
helps me calibrate.

Examples of the kind of edit I want:

  Original: "It is important to note that the API rate limit is
  100 requests per minute."
  Edit:     "The API rate limit is 100 requests per minute."
  Pattern:  Throat-clearing opener.

  Original: "This feature simply allows users to reset their
  password."
  Edit:     "This feature lets users reset their password."
  Pattern:  Empty intensifier ("simply").
```

**What to watch for in the output.**

- Edits that introduce new throat-clearing while removing the old. Spot-check.
- Over-editing — rewriting sentences that were fine. If half the draft is flagged, the model is pattern-matching rather than seeing your actual prose. Ask for the top-ten highest-impact edits only.
- Missed patterns. If the draft reads as AI-flavored to you but the model reports few edits, prompt with one example of the tell you're seeing and ask for a second pass.

**How to adapt.**

- Add your organization's own banned-words list to the pattern list. Every team has its own AI tells.
- Run this prompt as the *last* edit pass, after content review but before style review. Content errors dressed in fluent prose are more dangerous than awkward prose.
- Over time, keep a personal "tells I fixed" log. You'll start catching them while writing instead of after.


## Revision

Revision is where verification earns its name. The prompts below assume you already have a draft; they exist to pressure-test it against the audience, the source material, the style guide, and the many ways a plausible-sounding sentence can still be wrong.

### Prompt 5.1 — Reading This as My Persona Would

**When to reach for it.** Your draft reads well to you, but you know that's partly because you already understand the product. You want to see the draft through the eyes of someone who doesn't.

**Techniques used.** Role-based, chain-of-thought, few-shot.

**The prompt:**

```
You are going to read the following draft in character as this
persona:

[paste persona from Prompt 1.2 — full, not a one-line summary]

Stay in character throughout. React to the draft the way this
persona actually would — including impatience, confusion, skepticism,
or boredom where they fit.

As you read, produce a running commentary. For each section of the
draft:

1. What you understood.
2. What you didn't understand — and where exactly you got lost.
3. Any moment you would have stopped reading, and why.
4. Any moment the draft assumed knowledge you, as this persona,
   don't have.
5. Any moment the draft felt like it was written for someone else.

At the end, out of character, summarize:
- The three changes that would most improve this draft for this
  persona.
- Anything this persona would *not* need that the draft currently
  gives them.

Draft:
[paste draft]

Example of the kind of reaction I want (style only):

  Section "Configuring the webhook":
  Understood that I need to paste a URL somewhere.
  Didn't understand what "HMAC secret" is or whether I need to
  generate one. Stopped reading here; I would have Googled instead.
```

**What to watch for in the output.**

- Generic "a user might find this confusing" commentary. Push back: *"Be specific. At which sentence did this persona get lost, and what about that sentence caused it?"*
- Commentary that's too gentle. If your persona is skeptical or impatient, the reaction should show it. Re-run with: *"Persona 2 is not polite. Read again as Persona 2."*
- Missing the "already knows" problem — sections where the draft explains something the persona doesn't need explained. That one is easy to miss and costly to leave.

**How to adapt.**

- Run the prompt twice with two different personas. The diff between the two reactions is often the most valuable artifact.
- For long drafts, chunk by section. A running commentary over 40 pages degrades.
- Use this prompt *before* your first SME review, not after. It catches the errors SMEs don't notice because they, like you, already understand the product.


### Prompt 5.2 — Factual Claim Audit

**When to reach for it.** Your draft is nearly done and you want a structured pass specifically aimed at factual claims — numbers, names, versions, commands, behaviors. This is the verification step the Four Ds (see AI Limitations) call *Diligence* in its most concrete form.

**Techniques used.** Chain-of-thought, role-based.

**The prompt:**

```
You are a technical fact-checker. Your job is not to rewrite the
draft; your job is to list every factual claim in it and assess
whether it can be verified from the source material I've provided.

Draft:
[paste draft]

Source material:
[paste specs, prior docs, SME notes]

Produce a table with these columns:

1. Claim — the factual claim, quoted or closely paraphrased.
2. Type — number / name / version / command or code / behavior /
   other.
3. Source support — "supported," "partially supported,"
   "unsupported," or "contradicted" by the provided sources.
4. Evidence — the specific passage or fact in the source that
   supports or contradicts the claim. If unsupported, say so.
5. Action — verify with SME / cross-check in product / accept as
   is / rewrite.

Include every factual claim, even ones that seem obvious. The
claims that "everyone knows" are the ones that most often turn out
to be wrong.

After the table, list the three claims you are least confident
about — the ones you'd prioritize checking first if time were
tight.
```

**What to watch for in the output.**

- Claims the model missed. Scan your draft once yourself, especially for numbers and version strings, and spot-check against the table.
- "Supported" judgments that are really "plausible." Read the evidence column, not just the verdict.
- Over-broad claims marked supported when only a narrow version of the claim is supported. ("The system scales to millions of users" is not supported by a source that says "the system has been tested to 100,000 users.")

**How to adapt.**

- For regulated content, add: *"Flag any claim whose wording could be read as a promise, a guarantee, or a performance commitment."*
- For draft-by-AI content, run this prompt regardless of how confident you feel. Fluent writing masks fabricated facts; the audit is the counterweight.
- Keep the output as a review artifact. If a reader later challenges a claim, the audit trail matters.


### Prompt 5.3 — Style Guide Conformance Pass

**When to reach for it.** You have a house style guide (or a borrowed one) and you want a pass that checks the draft against it — not every rule, but the rules that actually matter for this document.

**Techniques used.** Few-shot, role-based, chain-of-thought.

**The prompt:**

```
You are a style editor. Check the following draft against the style
rules below. Do not critique anything that isn't in the rules.

Style rules that apply to this document:
[paste the 10–20 most relevant rules. Examples:
- Use "sign in," not "login," as a verb.
- Numbers one through nine are spelled out; 10 and above are
  numerals.
- Headings are sentence case, not title case.
- Code identifiers are in `monospace`, not "quotes."
- Use "select," not "click," for UI controls.]

Draft:
[paste draft]

For each violation, produce:
- The rule it violates (quote the rule).
- The offending phrase or construction (quote it).
- The proposed correction.
- The line or section where it occurs.

If the draft follows a rule consistently, don't mention that rule —
I only want violations.

If you notice a pattern the rules don't cover but probably should
(an inconsistent usage that appears repeatedly), add it at the end
under a section titled RULES TO CONSIDER ADDING, with two or three
example occurrences.
```

**What to watch for in the output.**

- Invented rules — violations flagged against rules you didn't provide. The "don't critique anything that isn't in the rules" instruction helps; verify anyway.
- Missed violations in code blocks or headings. The model sometimes focuses on prose and skips over structural elements. Prompt: *"Re-check headings and code blocks specifically."*
- Over-confident corrections for context-sensitive rules ("sign in" vs. "log in" when the product's own UI says "Log in"). Product UI wins; note these as exceptions.

**How to adapt.**

- Keep a short "rules that catch the most real issues" list separate from the full style guide. Thirty rules outperform three hundred when the model has to hold them all at once.
- After an AI-heavy writing session, run this prompt as a matter of course. AI drafts drift toward generic style even when your guide is specific.


### Prompt 5.4 — Pre-Publication Readiness Review

**When to reach for it.** The draft has been through content review and style review. You want a final, cross-cutting read before it ships — the kind of pass a careful lead writer would do on someone else's work.

**Techniques used.** Role-based, chain-of-thought, self-consistency (ask twice, compare).

**The prompt:**

```
You are a senior technical writer doing a final review of a
colleague's draft before it's published. You are not rewriting;
you are signing off — or not.

Draft:
[paste draft]

Audience: [persona]
Purpose: [one sentence on what the doc must achieve]
Constraints: [compliance, length, platform, anything else
non-obvious]

Go through the draft and answer each of the following, briefly
but specifically:

1. Does this doc achieve its stated purpose? If not, where does it
   fall short?
2. Is there anything in the draft that a reasonable reader could
   misinterpret in a way that causes harm (time lost, data lost,
   a bad decision)? If so, name it.
3. Is there anything missing — a step, a warning, a link, a
   prerequisite — whose absence would cause a reader to fail?
4. Is there anything present that could be cut with no loss?
5. Are the first two paragraphs strong enough to keep a skeptical
   reader reading?
6. Are the last two paragraphs strong enough that a reader who
   only skims the end still leaves with the right picture?

End with a verdict: READY TO PUBLISH, PUBLISH WITH MINOR FIXES, or
NOT READY — and the specific reason.

Do this review twice, independently. Label them Review A and Review B.
Then produce a short RECONCILIATION section noting where A and B
agreed, where they disagreed, and which view you trust more and why.
```

**What to watch for in the output.**

- A/B reviews that are identical. Re-run with: *"Review B should approach this from a different angle than Review A — perhaps the reader's point of view rather than the editor's."*
- A soft verdict ("mostly ready, probably fine") that dodges the question. Push for the three-choice verdict.
- Harm analysis (question 2) treated superficially. That question is the highest-stakes one in the list; if the answer is one line, prompt: *"Think harder about question 2. What is the worst outcome if this draft is read carelessly?"*

**How to adapt.**

- For docs that touch regulated content, add a seventh question: *"Is there any claim in this draft that our compliance or legal reviewers should see before publication?"*
- Keep the reconciliation section as a review artifact alongside the factual audit from Prompt 5.2. Together they form a record of due diligence.


## Publication & Maintenance

The last stage is the one most often skipped in AI-assistance conversations, and the one where quiet drift does the most damage. The three prompts below cover the moment of shipping, the moment of translating for a wider audience, and the moment of letting go.

### Prompt 6.1 — Release Notes from a Change Log

**When to reach for it.** You have a raw change log — commit messages, ticket titles, a PR list — and you need release notes that are useful to readers, not a dump of internal vocabulary.

**Techniques used.** Role-based, few-shot, chain-of-thought.

**The prompt:**

```
You are a technical writer producing release notes for [product],
version [X], from a raw change log.

Audience: [who reads these release notes — end users, admins,
developers, or a mix]
Tone: factual, specific, lightly human. No marketing language.

Raw change log:
[paste]

Produce release notes grouped under these headings, in this order,
skipping any heading with no entries:

1. Breaking changes — changes that require action from the reader.
2. New features — user-visible additions.
3. Improvements — user-visible changes that aren't new features.
4. Bug fixes — corrections to previously broken behavior.
5. Deprecations — things still working but planned for removal.
6. Security — entries that describe a security-relevant change.

For each entry:
- One sentence, user-facing, written for a reader who has never
  read the internal ticket.
- If the entry requires action from the reader, start it with
  "Action required:" and describe the action in one sentence.
- If the change log entry is unclear or ambiguous, do NOT invent
  a reader-facing description. Instead, write [UNCLEAR: <the raw
  entry>] and move on.

Example of the style I want:

  New features
  - You can now export dashboards as PDF. The export includes all
    widgets visible on screen; hidden widgets are not exported.

 Breaking changes
  - Action required: the `/v1/users` endpoint now returns paginated
    results by default. If your integration expects a single array,
    update it to follow the `next` cursor. See the migration guide.
```

**What to watch for in the output.**

- Internal vocabulary leaking through ("refactored the FooService," "bumped lodash"). These are signs the model is paraphrasing the ticket rather than re-purposing it for readers. Re-run: *"Rewrite every entry so that a reader who has never seen the code base would understand it."*
- Marketing drift ("we're excited to announce…"). The tone instruction usually holds, but not always. Catch it in review.
- Missing "Action required" labels on entries that actually require action. Cross-reference the Breaking changes section against the rest; anything in Breaking should almost always carry the label.
- Silent filling-in of [UNCLEAR] entries. The whole point of that convention is to preserve ambiguity; if the model resolved every entry confidently, some confidence is probably unearned.

**How to adapt.**

- For products with distinct audiences (end users and administrators, say), ask for two parallel sets of release notes rather than one blended set.
- For monthly or quarterly releases, keep a running "voice sample" of past release notes and paste a short excerpt as the style example. Consistency across releases is a feature.
- For security entries, add: *"For each security entry, note the severity level and whether a CVE is associated. If either is missing from the change log, flag it for the security team."*


### Prompt 6.2 — Localization-Ready Rewrite

**When to reach for it.** A document is scheduled for translation into one or more languages and you want to reduce the things that break in translation before handing it off — long sentences, culture-bound references, idioms, ambiguous pronouns, embedded humor that won't travel.

**Techniques used.** Role-based, chain-of-thought, few-shot.

**The prompt:**

```
You are a technical editor preparing a draft for localization into
multiple languages. The goal is not to translate; the goal is to
rewrite the English so that translation is cheaper, faster, and less
error-prone.

Draft:
[paste draft]

Target languages (for context, not for translation):
[e.g., German, Japanese, Brazilian Portuguese, Simplified Chinese]

Do the following, in order:

1. Scan for patterns that cause translation trouble:
   - Sentences over 25 words.
   - Embedded idioms or culturally specific references ("home run,"
     "ballpark figure," "out of left field").
   - Ambiguous pronouns whose antecedent is more than one noun away.
   - Noun stacks ("user authentication configuration policy settings").
   - Humor, sarcasm, or wordplay.
   - Units, dates, currency, and address formats that assume a US
     reader.
   - UI strings embedded in sentences (these usually need to match
     the localized UI and shouldn't be rewritten inside the prose).

2. For each pattern you find, quote the original and propose a
   localization-friendly rewrite. Do not rewrite passages that are
   already clean.

3. At the end, list:
   - Anything in the draft that should NOT be translated (product
     names, code identifiers, specific legal terms).
   - Anything that may need a locale-specific note (date formats,
     regulatory references, support phone numbers).

Example of the kind of rewrite I want:

  Original: "If you hit a home run on the first try, great — but
  most admins find they need to tweak the policy settings a few times
  before it clicks."
  Rewrite:  "If the configuration works on the first try, you're
  done. Most administrators need to adjust the policy settings
  several times before the configuration is correct."
  Pattern:  Idiom ("hit a home run," "before it clicks") and
  ambiguous pronoun ("it").
```

**What to watch for in the output.**

- Rewrites that strip all voice along with the trouble. Ask for a middle version: *"Rewrite for localization while keeping the draft's characteristic rhythm where possible."*
- Missed noun stacks. They're invisible to native English speakers and expensive to translate. If the draft has any heading longer than five words, check specifically.
- "Do not translate" lists that are too aggressive or too lax. A product name with a trademark should not be translated; a descriptive noun sometimes should. Have a localization specialist review the list if one is available.

**How to adapt.**

- Keep a project glossary of "do not translate" and "translate carefully" terms. Paste it in as context; the list becomes more useful with every project.
- For simultaneous publication across several languages, run this prompt *before* the final style pass. A style pass on the English will otherwise have to be redone after localization surfaces new issues.


### Prompt 6.3 — Retirement and Redirect Plan for Outdated Content

**When to reach for it.** A product area is being deprecated, merged, or renamed. You need to decide what to keep, what to archive, what to redirect where, and what to rewrite — and you want the decision made thoughtfully rather than by whoever gets to the page last.

**Techniques used.** Role-based, chain-of-thought.

**The prompt:**

```
You are a content strategist helping retire a documentation area
responsibly. The goal is not to delete; the goal is to leave
readers who arrive at old URLs in a better place than they were
before.

Here is what's changing:
[describe the change — feature removed, product renamed, area
merged into another, etc.]

Here is the affected content (list of page titles, with a one-line
description of each):
[paste list]

Here is what the change log says end-users should do instead, if
anything:
[paste or describe]

For each page, recommend one of the following, with a reason:

- KEEP AS-IS, with a banner explaining the deprecation timeline.
- KEEP, but rewrite for the new name/structure.
- REDIRECT to a specific new page (name the page).
- ARCHIVE with a tombstone page (a short "this feature was removed
  on [date]; here's what to use instead" page at the old URL).
- DELETE (only when the content is genuinely harmful to keep — for
  example, instructions that now lead to errors).

Think step by step. Before producing the recommendations, briefly
describe:
1. What readers are most likely to be searching for when they
   arrive at these pages after the change.
2. Which of those readers are best served by being forwarded to
   new content, and which would prefer a brief honest explanation
   that the feature is gone.

After the per-page recommendations, propose a single banner
message that could go on every "keep as-is" page during the
transition period.
```

**What to watch for in the output.**

- Over-use of DELETE. Outright deletion breaks inbound links from blog posts, Stack Overflow, and old tickets. If the model recommends DELETE liberally, push back: *"Reconsider. What would a reader arriving from a three-year-old Stack Overflow answer see?"*
- Redirects into pages that don't actually answer the reader's question. A redirect is only a good answer if the destination page is a good answer.
- A banner message that's longer than the content beneath it. Ask for a banner in two sentences or fewer.

**How to adapt.**

- For large-scale retirements, chain this prompt: recommend a strategy across the whole set first, then work page by page under that strategy.
- Keep the tombstone pages, even for small retirements. They're cheap to maintain and they dramatically reduce "this used to work" support tickets.

---

## Building your own prompt library

Twenty prompts is a starter set, not a finish line. Every team's prompt library eventually looks different from every other team's, because every team's product, audience, and voice are different — and because the prompts that actually earn their place in your library are the ones you've refined against real work.

Think of what you've just read as seeds. A few of them will take root in your practice; a few will be replaced within a month; a few will evolve past recognition. That is the whole intent. The goal of a personal library is not to collect every prompt you've ever run — it's to keep the ones that reliably produce work you're willing to sign your name to.

A few practices that help a prompt library grow usefully rather than just grow:

- **Save the prompt with the context that made it work.** A prompt without its voice sample, its persona, or its style rules is half a prompt. Save them together.
- **Date your prompts.** A prompt that worked brilliantly against one model version may disappoint on the next. A date in the header tells you when to re-test.
- **Keep the failures too.** The prompt that produced a confident hallucination is a teacher. Note what it got wrong; you'll recognize the pattern faster next time.
- **Share sparingly, curate heavily.** A shared library of 200 prompts is less useful than a shared library of 30 good ones. Prefer the second.
- **Review the library quarterly.** Retire what you no longer use. Promote the prompts you keep reaching for into a "core set" that new team members can start from.

For the deeper treatment of prompt library practice — how to organize, version, and govern one at team scale — see the **Building a Prompt Library** callout earlier in this course. This module gives you the raw material; The Building a Prompt Library callout gives you the habits for tending it.

And for a reminder of what this library is *for*: every prompt above exists to make a specific stage of Module 5's process faster, sharper, or more honest. The library is not the work. The work is the document that ships, the reader it serves, and the judgment you brought to both.
