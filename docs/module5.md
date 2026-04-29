# AI in the Technical Writing Process

Until now, you have learned *how* AI works, *what* its limits are, and *how to prompt it well*. This module brings those threads together. Think of it as the place where the conceptual parts of the course meet the desk you actually sit at — the briefs that land in your inbox, the SME interviews on your calendar, the drafts you owe by Friday.

The technical writing process has always had a shape: you prepare, you research, you organize, you draft, you revise, you publish. AI does not change that shape. What it changes is *where inside each stage the work lives* — which parts shrink because a machine can do them in seconds, which parts expand because you now have time to do them properly, and which parts stay stubbornly, irreducibly human.

This module walks through the stages one at a time. For each, you'll see what AI does well, where human judgment is essential, and one or two worked prompts you can adapt tomorrow. Treat the prompts as starting points — conversations, not scripts. (The full prompt library appears later in [Prompt Library](module6.md), with around twenty examples covering every stage below.)

By the end of this module, you'll be able to:

- Identify where AI can support each stage of the technical writing process: preparation, research, organization, writing, revision, and publication.
- Select appropriate AI-assisted prompts for common documentation tasks, and recognize which tasks still require human judgment regardless of AI assistance.
- Name the non-negotiable checkpoints in your own workflow — and explain the cost of skipping each.
- Sketch an initial oversight plan for any documentation workflow that incorporates AI.

!!! warning ""
    Before introducing AI into any new workflow, confirm it is permitted under your project's AI policy and obtain the appropriate permissions from stakeholders — so as not to expose any sensitive data to the LLM.


## AI Across the Technical Writing Process

A useful way to read the sections that follow: for each stage, ask yourself two questions. *What is the shape of the work at this stage?* and *Where would I most want another pair of eyes — or another pair of hands?* AI is rarely a replacement for the first; it is often a plausible substitute for the second.

Each stage below has three parts: **What happens** (a short framing of the stage), **How AI can help** (what to ask for and what kind of output to expect), and **Where human judgment is essential** (the parts you won't want to delegate, even when you can). A small table of example prompts follows — treat them as scaffolds to adapt, not recipes to follow.


### Stage 1. Preparation

*What happens.* Understanding the brief, identifying stakeholders, scoping the work, setting acceptance criteria, choosing a medium, agreeing a timeline, selecting a style guide, sketching a revision plan. The unglamorous stage where most project failures are quietly born. A preparation done well is invisible later; a preparation skipped makes itself felt every day of the project.

*How AI can help.*

- **Generate audience personas** to pressure-test your understanding of who you're writing for. AI is good at producing three or four realistic-sounding personas fast; you are the one who decides which of them match the people who will actually use your docs.
- **Brainstorm scope boundaries, risks, and open questions** — the things you might not have thought to ask.
- **Summarize past documentation** to find what already exists, avoid duplication, and identify content you can build on.
- **Draft a stakeholder matrix** covering typical roles, their interests, and their preferred communication formats.
- **Compare tracking approaches** — spreadsheets, project management tools, docs-as-code pipelines — and summarize trade-offs before you commit.
- **Draft a revision plan structure** with review stages, sign-off points, and iteration cycles.
- **Map the oversight gates** in a planned workflow — the decision points where a human reviewer needs to approve before the process continues.

*Where human judgment is essential.*

- **Choosing the actual audience and scope.** AI can explore options; it cannot make organizational or strategic decisions about which audience your team is actually resourced to serve.
- **Interpreting vague briefs.** Often the most important insight is what the brief does *not* say — the assumption someone forgot to write down. AI has no way to know that the brief is incomplete.
- **Reading the room.** Which stakeholders are cautious about AI? Which reviewer hates passive voice? Which SME will be on leave in week three? None of this is in the training data.

*A couple of worked prompts.* Try these as starting points; adjust the bracketed fields for your project.

| Task | Example prompt |
| --- | --- |
| Generate realistic user personas. | "The product is [describe product]. The primary purpose of its documentation is to guide users through the product with minimal frustration. Create three user personas. For each persona include: name, role, technical background, primary goals when using the documentation, attitude toward reading documentation (supportive / skeptical / reluctant), preferred format, and country or region of origin if relevant. Be specific and realistic." |
| Map the oversight gates in a planned workflow. | "I am designing the following documentation workflow: [describe workflow]. Assume the role of a technical workflow designer. Identify the decision points where a human reviewer must approve or intervene before the process continues. For each gate, specify: what the reviewer should check, what a passing result looks like, and what would trigger escalation to a human decision-maker." |

!!! tip "Try this"

    Before you run either prompt, pause and write down what *you* think the answer should look like — two or three bullets will do. Compare your version to AI's. The gap between them is where the real learning sits: sometimes AI surfaces something you'd missed, and sometimes you realize you knew more than you gave yourself credit for.


### Stage 2. Research

*What happens.* Gathering information from the sources that actually exist: SMEs and their calendars, specifications and their gaps, code and its comments, tickets and their half-finished threads, existing documentation and its contradictions. Research is where the raw material of the documentation comes from. It is also where most factual errors enter the pipeline — usually not because the research was wrong but because a small thing was misunderstood early and carried forward.

*How AI can help.*

- **Summarize long source documents, specifications, or ticket threads** — the wall-of-text artefacts that would otherwise consume an afternoon of reading.
- **Draft interview questions for SMEs** before you meet them, so the hour with the engineer is spent on the things only the engineer knows.
- **Extract key claims from dense material and organize them** by theme, by risk, or by deliverable.
- **Analyze batches of user feedback or support tickets** to surface recurring themes before you decide which to act on.
- **Create first-draft glossary entries** from source material, which you then verify against authoritative sources.
- **Answer factual questions grounded in your knowledge base**, when a RAG-enabled tool is available (see **Retrieval-Augmented Generation**).
- **Assess whether a repeating research task is a good candidate for automation** — the sort of question that earns its keep if the task will repeat every sprint or every release.

*Where human judgment is essential.*

- **Interviewing the SME.** AI cannot replace the nuance of a real conversation with someone who knows things that are not written down. A good interview is half the research in most projects. You won't get a transcript that captures the pause before the engineer says "well, technically…" — but that pause is often where the truth lives.
- **Distinguishing what is true, current, and specific to your product** from what is plausible and generic. An AI summary of a spec sounds authoritative; it doesn't know which paragraphs of the spec are aspirational and which are shipped.
- **Following the contradiction.** If two sources disagree, AI will often pick one or smooth over the conflict. A writer's job is to notice the conflict and ask which source to trust — and why.

*A couple of worked prompts.*

| Task | Example prompt |
| --- | --- |
| Summarize secondary source material for a specific documentation task. | "Summarize the following materials for a technical writer documenting [product feature]: [paste content]. Focus on: what the feature does, who it is for, known edge cases or limitations, and anything a user might misunderstand. Flag any gaps or contradictions in the source material." |
| Evaluate whether a research task is automation-worthy. | "I need to complete the following research task repeatedly: [describe task]. It involves these steps: [list steps] and these data sources: [list sources]. Assess whether this task is a good candidate for an automated agent workflow by evaluating: how routine and well-defined the steps are, how frequently the task repeats, and what the setup cost vs. time savings trade-off might be. List any additional information I would need to design the workflow." |

!!! tip "Useful habit"

    When AI summarizes a source for you, ask it a follow-up: *"What claims in this summary should I verify before trusting?"* Models are often surprisingly good at flagging their own weak points when you invite them to. It's a small move that saves hours later.

### Stage 3. Organization

*What happens.* Turning raw research into a structure a reader can navigate. Outlining, sequencing, deciding what belongs in a quick-start and what belongs in a reference, grouping related concepts, choosing an information architecture, picking the right content type (tutorial? how-to? explanation? reference?), and negotiating the shape of the deliverable with the people who will review it. Organization is where the document stops being a pile of facts and starts being a document.

*How AI can help.*

- **Generate outline options** for a given topic and audience — several structures, not just one, so you can pick or combine.
- **Suggest logical groupings** for a list of topics or tasks you've already researched.
- **Compare content-type frameworks** (Diátaxis, DITA, topic-based authoring) and propose which might fit your material.
- **Propose a table of contents** from a brief or a set of source materials.
- **Recommend a sequence** for a procedural document — first-do-this-then-that — based on dependencies you describe.
- **Identify missing sections** by comparing your outline to typical structures for similar documents.
- **Draft heading hierarchies** that follow style-guide conventions you specify (sentence case, parallel structure, action verbs).

*Where human judgment is essential.*

- **Knowing what the reader came for.** AI can produce a tidy, logical outline that nobody actually needs. You have to keep asking *what question does the reader walk in with?* — and organize around the answer.
- **Deciding what to leave out.** A good outline is as much about omission as inclusion. AI tends to include everything plausible; your job is to cut.
- **Sequencing around dependencies the AI can't see.** If step 4 requires a permission that takes two weeks to obtain, that belongs in the prerequisites, not step 4. AI won't know unless you tell it — and sometimes you won't think to tell it.

*A couple of worked prompts.*

| Task | Example prompt |
| --- | --- |
| Generate outline options for a new document. | "I am writing [document type] for [audience] about [topic]. The goal is [goal]. The audience's existing knowledge is [describe]. Propose three different outline structures: one task-oriented, one concept-oriented, and one hybrid. For each, list the top-level headings and a one-line rationale. Note which structure you would recommend and why." |
| Group a messy list of topics. | "Here are 22 topics I've gathered from research: [paste list]. Group them into a logical outline for a [document type]. Use no more than 5 top-level groups. For each group, suggest a heading in sentence case, starting with an action verb where appropriate. Flag any topics that don't fit, and any groups that look thin enough to merge." |

!!! tip "Try this"

    Ask for *three* outlines rather than one. Variation is cheap for the model and expensive for you; letting AI generate alternatives is one of the places the economics tilt most clearly in your favor. The outline you finally ship will often be a stitch of the best bits from two of the three.


### Stage 4. Writing

*What happens.* Turning the outline into sentences. Drafting. The stage most people picture when they picture "writing," though by this point much of the thinking has already been done. Writing is where voice, rhythm, and precision live — and where the difference between documentation that works and documentation that technically exists is made.

*How AI can help.*

- **Generate a first draft** from an outline and source material, which you then edit heavily rather than publish directly.
- **Produce multiple drafts of short passages** (an introduction, a warning callout, a release-note entry) so you can pick the best phrasing or stitch together the parts that work.
- **Rewrite in different tones or registers** — more formal, less jargon, shorter sentences, friendlier voice.
- **Translate between content types** — turn a conceptual explanation into a step-by-step procedure, or a procedure into a reference table.
- **Draft boilerplate sections** — prerequisites, assumptions, "who this guide is for," related-links blocks — that follow predictable patterns.
- **Expand terse notes into full sentences** when you're working from a sparse outline and want momentum.
- **Condense wordy drafts** when you've over-written and need to find the core.
- **Generate examples, analogies, and edge cases** to test whether your explanation holds up.

*Where human judgment is essential.*

- **Voice and style.** AI defaults to a generic middle register — pleasant, grammatical, instantly forgettable. Your readers know your product's voice; AI does not. Impose your voice every time.
- **Technical accuracy.** Every factual claim, every code sample, every parameter name, every version number. AI will produce confidently wrong text faster than you can read it. The fix in all cases is the same — verify.
- **Deciding what is worth saying.** A draft generated from an outline will often contain three paragraphs where one sentence would do. Writing is largely the art of knowing what not to write.
- **Accessibility and inclusion.** AI-generated text can slip into idioms, culturally loaded metaphors, or assumptions about the reader's context. Read with accessibility and internationalization in mind.

*A couple of worked prompts.*

| Task | Example prompt |
|---|---|
| Draft a procedure from source notes. | "Using the notes below, draft a step-by-step procedure for [task]. Audience: [describe]. Style: numbered steps, imperative mood, one action per step, no more than one sentence per step. Include a short prerequisites list and a one-sentence confirmation of success at the end. Notes: [paste notes]. Flag any step where the notes are ambiguous or incomplete rather than guessing." |
| Rewrite in a different register. | "Rewrite the following paragraph for a non-specialist audience. Keep all technical claims intact. Shorten sentences to 20 words or fewer where possible. Replace jargon with plain equivalents, but keep any term that is a product name or an industry-standard term. Preserve the original meaning exactly — flag any sentence where plain language would require losing precision. Paragraph: [paste paragraph]." |

!!! tip "Useful habit"

    When AI produces a draft, read it once for what it says — then read it again asking *what does it sound like it's trying to sound like?* That second read is where you catch the generic-corporate voice creeping in. It's also where your voice gets put back in.


### Stage 5. Revision

*What happens.* Reviewing, editing, and improving a draft. Checking facts, style, structure, tone, accessibility, completeness, consistency, and fit with the brief. Responding to reviewer comments. Deciding what to cut. The stage where a draft becomes a document — or where a document quietly fails to become one, if the time isn't protected.

*How AI can help.*

- **Proofread for grammar, spelling, and punctuation** — a baseline sweep before human review.
- **Flag inconsistencies** in terminology, capitalization, numbered step formats, or heading structure across a document.
- **Check style-guide compliance** when you've given the AI a specific style guide (or the parts of it that matter most for this document).
- **Suggest clearer phrasing** for sentences you know are clunky but can't quite unknot.
- **Identify passive voice, long sentences, nominalizations, weak verbs** — the usual suspects — and offer alternatives.
- **Spot gaps** by comparing the draft against the outline, the brief, or a reference document.
- **Summarize reviewer comments** into themes when you're staring at fifty tracked changes and need to plan a response.
- **Generate a revision checklist** tailored to the document type.
- **Simulate a reviewer's perspective** — "read this as a skeptical SME" or "read this as a first-time user" — to surface problems before a real reviewer does.

*Where human judgment is essential.*

- **Deciding which suggestions to accept.** AI will offer dozens of edits; some will improve the text, some will flatten it, and some will introduce errors. Every accepted change is still your decision.
- **Weighing reviewer feedback.** Two reviewers will disagree. One will be right on one point and wrong on another. AI cannot negotiate the politics of review; you can.
- **Protecting the document's purpose.** Under revision pressure, documents drift — a clear quick-start becomes a hedged reference as each reviewer adds their favorite caveat. Keeping the document on purpose is a human job.
- **Knowing when to stop.** "Done" is a judgment call. AI will happily suggest edits forever.

*A couple of worked prompts.*

| Task | Example prompt |
|---|---|
| Review a draft against a style guide. | "Review the following draft against these style rules: [list 5–10 rules, e.g., sentence-case headings, no Latin abbreviations, second-person voice, Oxford commas, numbered steps in imperative mood]. For each rule, list the specific sentences or headings that violate it, and suggest a fix. Do not rewrite the whole draft. Draft: [paste draft]." |
| Simulate a skeptical reviewer. | "Read the following draft as a skeptical senior engineer reviewing for technical accuracy. List every claim you would want to verify before approving, every place where a step could fail silently, and every assumption the draft makes about the reader's environment. Be concrete. Draft: [paste draft]." |

!!! tip "Try this"

    Run the same draft through two different "reviewer personas" — a first-time user and a skeptical SME. The comments you get back will barely overlap, and that's exactly the point. Each persona surfaces a different class of weakness.


### Stage 6. Publication and Maintenance

*What happens.* Shipping the document and keeping it useful. Formatting for the target platform, checking cross-references and links, generating translations, publishing, monitoring reader feedback, and — often the most neglected step — deciding when and how to update. Publication isn't a single moment; it's the beginning of a document's working life.

*How AI can help.*

- **Format and adapt content** for different platforms or output formats (Markdown to DITA, long-form to release notes, web to PDF-friendly layouts).
- **Generate release-note entries** from a list of changes, tickets, or commit messages.
- **Draft first-pass translations** or localization notes, to be reviewed by a qualified translator — never shipped directly.
- **Produce alt text and image descriptions** as a starting point for accessibility review.
- **Cluster and summarize user feedback** to identify which sections readers struggle with most.
- **Flag stale content** by comparing a document against a newer source (a release notes file, a changelog, an updated spec) and surfacing sections likely to be out of date.
- **Draft a maintenance plan** — review cadence, triggers for updates, ownership assignments.

*Where human judgment is essential.*

- **Final sign-off.** Somebody's name goes on the published document. That somebody is accountable for what it says.
- **Translation and localization quality.** Machine translation has improved enormously and is still not a substitute for a human translator on anything customer-facing. Cultural nuance, legal exposure, and product-specific terminology all require a human.
- **Deciding what to retire.** Old documents that nobody reads cost almost nothing to keep and slowly erode trust in the docs that *are* current. AI can flag staleness; a human decides what to archive.
- **Reading real feedback.** An angry support ticket, a confused forum post, a quiet drop in a page's traffic — these are signals that deserve human attention, not just clustering.

*A couple of worked prompts.*

| Task | Example prompt |
|---|---|
| Draft release-note entries from a changelog. | "Below is a list of changes from the [product] [version] changelog. Draft user-facing release notes grouped into: New features, Improvements, Bug fixes, and Breaking changes. Each entry should be one or two sentences, written in plain language for an end user rather than a developer. Omit internal refactors and purely cosmetic changes. Flag any change that needs SME clarification before it can be described to users. Changelog: [paste changelog]." |
| Identify candidates for content retirement. | "I will paste a list of documentation pages along with their last-updated date and page-view count over the past year. For each page, recommend one of: keep as-is, needs update, candidate for archive, candidate for merge. Briefly justify each recommendation. Flag any page where the title suggests it may still be important even if traffic is low. Data: [paste data]." |


## Checkpoints, Gates, and the Cost of Skipping Them

Across every stage above, a recurring theme emerges: AI accelerates the work, but the value of the document still depends on the human checkpoints in the workflow. Think of these checkpoints as **gates** — decision points where a human looks at what AI has produced and decides whether it should move forward.

Some gates are obvious. You would not publish a security-sensitive page without a security review, AI-assisted or not. Others are quieter, and quieter gates are the ones most often skipped:

- **The "does this claim check out?" gate** after any AI-generated factual content.
- **The "does this sound like us?" gate** after any AI-generated prose.
- **The "would a reader actually do it this way?" gate** after any AI-generated procedure.
- **The "are we still answering the original question?" gate** after any AI-assisted revision cycle.

Gates cost time. Skipping them saves that time — until it doesn't. The cost of a skipped gate is not evenly distributed: most of the time nothing happens, and then occasionally something happens that would have been caught by a two-minute check.

A short, non-exhaustive cost-of-skipping inventory:

| Gate skipped | Typical immediate cost | Occasional long-tail cost |
|---|---|---|
| Fact-check on AI-drafted claims | None visible at publish time | A support escalation, a customer trust incident, a corrections thread |
| Voice and style review | A document that reads as slightly off | Gradual drift in the docs' voice across a quarter; reader disengagement |
| Procedure walk-through | None visible | A step that silently fails for a subset of users; support load |
| Accessibility and inclusion pass | A slightly less accessible page | Exclusion of a real segment of your users; compliance exposure |
| "Are we answering the brief?" pass | A document that meets the spec as written | A document that meets the spec as written but not the problem it was meant to solve |

!!! tip "Useful exercise"

    Pick one workflow you're running this month. List the gates — all the places where a human currently looks at output before it moves to the next step. Then ask: if I added AI to this workflow, which gates would I keep, which would I strengthen, and which would I be tempted to quietly remove? The answers will often tell you more about the workflow than about the AI.


## The Process at a Glance

For quick reference, here is the technical writing process summarized across its six stages, the AI-assistable tasks at each, and the human responsibilities that remain:

| Stage | AI can help with | Human judgment essential for |
| --- | --- | --- |
| **Preparation** | Audience personas, stakeholder matrices, scope brainstorms, oversight-gate mapping, revision-plan structures | Choosing the real audience, interpreting vague briefs, reading organizational context |
| **Research** | Summarizing sources, drafting SME interview questions, extracting claims, clustering feedback, first-pass glossaries | Conducting SME interviews, separating true from plausible, resolving source contradictions |
| **Organization** | Outline options, topic groupings, TOC drafts, content-type recommendations, sequencing suggestions | Knowing what the reader came for, deciding what to cut, sequencing around invisible dependencies |
| **Writing** | First drafts, register shifts, boilerplate, expanding notes, condensing, example generation | Voice, technical accuracy, deciding what to say, accessibility and inclusion |
| **Revision** | Proofreading, consistency checks, style-guide compliance, gap-finding, reviewer-comment summarization, reviewer simulation | Which edits to accept, weighing reviewer feedback, protecting the document's purpose, knowing when to stop |
| **Publication and Maintenance** | Format adaptation, release notes, first-pass translation, alt text, feedback clustering, stale-content detection | Sign-off, translation quality, retirement decisions, reading real feedback |

Read across any row and you'll notice a pattern: the AI column grows as the task becomes more mechanical, the human column grows as the task becomes more contextual. This is the shape of the division of labor across the whole process. When a task feels mechanical, AI is probably a good fit. When a task feels like it requires knowing something not written down, it probably requires you.


## Looking Ahead: From Process to Prompt Library

This module has given you, for each stage, one or two worked prompts — enough to start experimenting. The full prompt library, with around twenty prompts spanning every stage, lives in Prompt Library. Think of that module as a reference you return to rather than read through once: when a new task lands on your desk, find the stage, find the prompt closest to your need, and adapt from there.

Two habits will serve you well when you get there:

1. **Treat the library as a starting point, not a menu.** Every prompt in it is a first draft of a conversation with a model. Your project, your audience, your style guide — none of them are in the prompt yet. Adapt.
2. **Write down what works.** When you adapt a prompt and it produces something useful, save the adapted version. Over a few months, you'll have built a personal prompt library that fits your work far better than any generic one. Prompt Engineering introduced the idea; Prompt Library gives you the raw material.

Before you move on, a short self-check: for each of the six stages above, can you name one task you'd delegate to AI and one task you wouldn't? If the answer comes easily, the stage is clear for you. If it doesn't, that's the stage to re-read — or to experiment with first.
