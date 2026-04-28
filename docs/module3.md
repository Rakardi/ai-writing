# AI Limitations

!!! quote ""

    "The real problem is not whether machines think but whether men do." — B. F. Skinner

AI is powerful, and it is confidently wrong. Those two facts coexist, and learning to hold them together is most of what this module is about. The failures below aren't edge cases you might occasionally meet; they're structural features of how these systems work. Knowing the shape of each one is what lets you keep the speed AI offers without paying for it in quiet mistakes that reach your readers.

By the end of this module, you'll be able to:

- Recognize the six categories of AI limitation — factual, contextual, reasoning, stylistic, ethical, and operational — and name a mitigation for each.
- Distinguish the three failure modes that sit under the umbrella term "hallucination": pattern-matching errors, reasoning-chain errors, and sycophancy.
- Apply the Four Ds (Delegation, Description, Discernment, Diligence) as a competency map for working with AI safely.
- Classify any AI-generated claim as factual, structural, stylistic, or reasoning — and choose the verification technique that fits each kind.

---

## AI Limitations at a Glance

| Category | What it looks like | Why it happens | What to do |
|---|---|---|---|
| **Factual** | Content that sounds authoritative but is wrong, outdated, or fabricated. | Models predict likely text, not verified facts. Training data has a cutoff. | Verify against authoritative sources. Ground with RAG where you can. |
| **Contextual** | Output misses the nuance of your audience, product, or organization. | The model has no memory of your product or policies unless you supply them. | Provide explicit context; use RAG for context too long to paste. |
| **Reasoning** | Plausible conclusions reached through flawed logic or unexamined assumptions. | Fluent output ≠ sound reasoning. A visible chain isn't a trustworthy chain. | Check assumptions, not just conclusions. |
| **Stylistic** | Generic, padded prose; loss of brand voice; the uniform "AI-sounding" cadence. | Models gravitate toward the statistical average of fluent English. | Supply voice samples; edit for voice as a distinct pass. |
| **Ethical** | Bias, exclusion, unattributed content, confidentiality leaks, IP exposure. | Models inherit their training data's biases and have no sense of "appropriate." | Apply human judgment; disclose AI use; follow policy. |
| **Operational** | Cost, latency, rate limits, version drift, outages. | AI tools are infrastructure, not magic. | Treat AI as a service with SLAs and fallback plans. |

The rest of the module takes the three categories where technical writers meet the most trouble — Factual, Reasoning, Ethical — and gives each the depth it deserves. Context, Stylistic, and Operational are covered briefly; they matter, but they are less likely to quietly damage your work.

---

## Hallucinations and Factual Errors

A **hallucination** is content that sounds plausible but is wrong, fabricated, or unsupported by any real source. It isn't a glitch. A language model's job is to produce statistically likely text, not true text; most of the time those coincide, and sometimes — on niche, recent, or specialized topics — they don't.

In technical writing, hallucinations tend to take recognizable shapes: fabricated API endpoints and parameters that look right but don't exist; incorrect version numbers, release dates, or compatibility claims; invented citations and standards references; plausible-looking code that calls libraries that aren't there; and confidently wrong explanations of how something works internally.

### Three failure modes under one name

"Hallucination" is a useful umbrella word, but underneath it sit three distinct failure modes. They differ in mechanism, and learning to spot each one sharpens your judgment about where to look.

**Traditional hallucinations — pattern-matching errors.**
A standard LLM extrapolates beyond its training data, filling gaps with confident-sounding invention. Think of it as the model pattern-matching its way toward something that looks like a correct answer, without any mechanism for noticing when the pattern has drifted from the truth. The giveaway is usually surface-level: a plausible endpoint name, a tidy but fictional version history, a citation that points nowhere.

**Reasoning-model errors — confident wrong answers.**
Newer reasoning models are designed to think step by step, and they often display their reasoning chain so you can follow along. This is genuinely useful, and it introduces a new failure mode. A reasoning model can produce a chain that is internally consistent, fluently argued, and still wrong — because one early assumption was wrong. The chain looks like careful deliberation. The conclusion looks hard-earned. Both can be confidently incorrect at the same time.

!!! tip ""

    Try this when you meet a long reasoning chain on a claim that matters: read the first two or three steps, then ask, *"Are the premises here actually true?"* If yes, read on. If no, the elegance of the downstream reasoning doesn't save you.

**Sycophancy — the agreeable-output failure mode.**
Models can be trained, or fine-tuned, to produce outputs users find agreeable rather than outputs that are accurate. Yours may confirm your assumptions, validate your draft, or soften every disagreement into near-agreement. If you notice the model reliably opens with "Great approach!" before offering feedback, treat that warmth as ambient tone, not as evaluation. Paste a deliberately flawed draft sometime and see whether the model catches the flaws or praises the structure. A little adversarial probing tells you quickly how agreeable your tool is under the hood.

**The fix in all three cases.**
The mechanisms differ; the habit is the same. Verify claims against authoritative sources, especially for anything high-stakes. Validate *assumptions*, not just conclusions. And assume that newer or more expensive models have *different* failure modes, not zero failure modes — the sophistication of the tool changes the shape of its mistakes, not the fact of them.

*Further reading:* Anthropic's research blog ([anthropic.com/research](https://www.anthropic.com/research)) and OpenAI's research pages ([openai.com/research](https://openai.com/research)) are the useful anchor points. For practitioner-level guidance, search for *"LLM hallucination mitigation"* and *"AI sycophancy"* — this field moves quickly, and recent practitioner posts are often more useful than older survey papers.

### Mitigations that actually work

- **Ground the model.** Paste authoritative source material directly into the prompt, or use a RAG-enabled tool that retrieves from your real documentation.
- **Verify every factual claim.** Treat a specific fact in AI output as a lead to check, not an answer to use.
- **Ask for citations.** They can themselves be fabricated, but asking nudges the model toward content that is more traceable.
- **Cross-check with a second model.** Agreement between two independent models is a mild positive signal on a specific fact. Disagreement is a strong signal that more checking is needed.
- **Lower the temperature** for factual work, if your tool exposes the setting. Lower temperatures produce more deterministic, less inventive responses.

---

## Context and Stylistic Drift

Even factually correct output can miss the context of *your* product, *your* audience, or *your* organization. The model doesn't know your product's terminology, your audience's skill level, your legal constraints, or what was decided in last week's roadmap meeting. It also doesn't write in your voice. Left unattended, AI prose drifts toward the statistical middle: grammatically perfect, tonally flat, padded with "It is important to note that…" and "In order to…", and rhythmically identical paragraph after paragraph.

The fix for both is the same in shape: give the model what it can't infer. A short reusable "context block" at the start of relevant prompts — audience, product name, style conventions — handles a lot. Actual voice samples from your documentation ("Rewrite in a style similar to this passage…") steer the model more reliably than any number of adjectives like *concise* or *conversational*. Name anti-patterns explicitly: *"Avoid opening with 'In this guide' or 'It is important to note.'"* And accept that voice is an editorial pass of its own — first-draft AI prose will need one, and the time for it belongs in the plan.

---

## Reasoning Failures

Reasoning failures are the hardest to catch, because the output sounds coherent. The model reaches a plausible conclusion through flawed logic, an unexamined assumption, or a leap that wouldn't survive careful scrutiny. The usual shapes: **unstated assumptions** (a default Linux environment, an English-speaking user, a web context) that don't hold for your documentation; **correlation-for-causation**, dressed up as explanation; **ignored edge cases**, where the happy path works and the edges fail silently; and **overconfident synthesis**, where two unrelated facts are bridged with a plausible-sounding connector that is, on inspection, nonsense.

A complication worth naming: **a visible reasoning chain is not the same as a trustworthy reasoning chain.** When a reasoning model shows its work, it looks like transparency, and that appearance can lull you into skipping verification. The chain is the model's narration of its process — not a guarantee that the narration matches what the model actually did, nor that the narration is correct.

So check assumptions, not just conclusions. Ask *what is this answer taking for granted?* before asking whether the answer feels right. Probe with adversarial prompts: *"Give me three reasons this answer could be wrong,"* or *"What assumptions does this answer make?"* — the responses often surface real gaps. And when the subject is outside your expertise, that is exactly the moment to involve an SME, not the moment to trust the fluent explanation the model gave you.

---

> 💡 **The Four D Framework: Your Competency Map for Working with AI**
>
> The limitations above are a long list. The Four Ds are the synthesis that keeps the list actionable — four competencies that determine how well you navigate every category.
>
> - **Delegation** — Knowing which tasks belong with AI and which must stay with you. Handing the wrong task to AI produces confident-sounding bad outcomes. *(See The Spectrum: Augmentation ← Hybrid → Replacement)*
> - **Description** — Communicating intent clearly. A well-structured prompt largely determines whether AI helps you or misleads you. *(See Prompt Engineering.)*
> - **Discernment** — Reading AI output critically. Knowing what to trust, what to question, and what to verify regardless of how confident the output sounds. This is the competency that protects you from everything in this module.
> - **Diligence** — Validating outputs before they go anywhere. "Verify relentlessly" is not a motto; it is the professional standard for anyone publishing AI-assisted content. The next section is Diligence in practical form.
>
> Tools will change. Model categories will come and go. Failure modes will shift as the technology evolves. These four competencies will not.

## Evaluating AI Outputs

Every AI course tells you to verify outputs. Few tell you how. This section is Diligence in working form: a way to triage what you're reading and a small kit of techniques that fit into real work.

### Four kinds of claim, four kinds of check

Not every claim in AI output is checked the same way. Classify before you check, and you'll spend your effort where it actually matters.

| Kind of claim | What it looks like | How to check |
|---|---|---|
| **Factual** | "The API returns 200 on success." "This feature shipped in v3.2." | Check against the authoritative source — docs, spec, ticket, code. A plausible-looking hyperlink is not evidence a source exists; following the link and reading the source is. |
| **Structural** | "The request body must contain `user_id` and `session_token`." | Check against schema, spec, or a working example. |
| **Stylistic** | "Rewritten in a more formal tone." | Check against your style guide or voice samples. |
| **Reasoning** | "Because X, therefore Y." | Check the assumptions behind X, not just the plausibility of Y. |

Reasoning failures are hardest to spot, so scan for those first when something surprises you. Factual failures are most common, so check for those most routinely.

### A working kit

Match the technique to the stakes — you don't need all of these on every output.

- **Source-grounded checking.** For any factual claim that matters, pull up the authoritative source and read it directly.
- **Cross-model checking.** Ask the same question of a second model. Agreement is a mild signal of correctness; disagreement is a strong signal that more checking is needed. Cheap and disproportionately useful on high-stakes factual claims.
- **Adversarial prompting.** Ask: *"List three ways this answer could be wrong,"* or *"What assumptions does this answer make?"* The model is often surprisingly good at critiquing itself — sycophancy notwithstanding, a direct request for self-critique tends to surface real gaps.
- **Golden-set testing (for repeating workflows).** Keep a small set of representative inputs with known-good outputs. When you change your prompt, tool, or model, run the golden set and compare. This is how you detect silent regressions before your readers do.
- **Round-trip testing (for code or structured output).** If the AI generated code or a schema, actually run it. "Looks correct" is not correct. Compiling is not running. Running is not running against edge cases.

### Measuring whether AI is helping you

AI-readiness includes telling whether AI is actually improving your work — or quietly making it worse in ways that show up weeks later. A few lightweight signals are enough.

- **Time-to-publish.** Has "brief received" to "content published" actually dropped?
- **Error-catch rate at review.** A rise may mean AI drafts are introducing new problems; a fall may mean reviewers are skimming because output "looks fine."
- **Revision count.** Rising revision counts are a warning sign.
- **Post-publication issues.** User-reported errors, support tickets traceable to documentation, broken examples. Lagging but unambiguous.

A notebook, a shared spreadsheet, or a periodic team retrospective is enough — no dashboard required. The point is that without *any* measurement you are flying blind, and the shift from helping to costing can happen slowly enough that you won't notice without the instrument panel.

---
