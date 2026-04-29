# Augmentation ← Hybrid → Replacement

## Introduction

In this module, explore one of the most practical — and underappreciated — skills in AI-assisted technical writing: knowing how much of a task to hand to AI, and how much to keep for yourself.

It sounds simple. In practice, it is anything but. The amount of AI involvement that is right for drafting internal meeting notes is completely wrong for safety-critical procedures. The right dial setting for a writer who knows a domain deeply is not the same as for a writer who is documenting an unfamiliar system for the first time. And the right setting on a generous deadline is not the same as on a deadline that is already past.

This module gives you a framework for making these decisions deliberately—for any task, at any stage, in any context.

By the end of this module, you'll be able to:
- Describe the augmentation–replacement spectrum and place specific documentation tasks on it.
- Apply a four-question decision framework to any task to determine the appropriate level of AI involvement.
- Recognize the warning signs that tell you AI has too much control.
- Identify which content types call for augmentation, hybrid approaches, or high automation.


## The Spectrum: Augmentation ← Hybrid → Replacement

AI involvement in documentation work is not a binary choice. Think of it as a dial with three zones:

| Zone | What it looks like | Who decides |
|---|---|---|
| **Augmentation** | AI assists; human leads. You research, structure, and draft; AI suggests improvements or catches errors. You review every AI output before it goes anywhere. | Human decides; AI informs. |
| **Hybrid** | AI and human share the work. AI generates the first draft; human reviews, edits, and decides on contested passages. Responsibility is distributed based on the task. | Shared; depends on the task. |
| **Replacement** | AI completes the task; human monitors or spot-checks. Human intervenes only when something appears wrong. | AI decides; human audits. |

None of these zones is inherently right or wrong. The right zone depends entirely on the task.

**A practical illustration: release notes**

| Approach | What it looks like |
|---|---|
| **Augmentation** | You ask AI what shipped this sprint. AI lists features with details. You decide which are noteworthy, write the narrative, and emphasize what users care about. AI helps you think. You decide the message. |
| **Hybrid** | AI queries your ticket system, extracts features and bugs, groups them, and generates a draft. You review the draft, rewrite 20%, ask AI to refine based on your feedback. AI does initial organization. You shape the message. You iterate together. |
| **Replacement** | AI generates final release notes from tickets. You spot-check for obvious errors and publish. AI does the work. You validate at the end. |

Which approach fits? For a routine patch with a tight deadline: hybrid or replacement. For a mission-critical release where users are paying close attention: augmentation or hybrid. For a small internal fix: replacement.


## The Decision Framework: Four Questions

Before committing to an approach for any task, work through these four questions. Your answers guide you to the right zone on the spectrum.

**Question 1: Is there a single right answer?**

Some documentation tasks have clear, verifiable correct outputs: listing the parameters for an API endpoint, extracting error codes from a log, translating a UI string. These are good candidates for AI to take the lead—there is no judgment call, and if the output is correct, the task is done.

Other tasks involve judgment, audience awareness, or contextual decisions where multiple valid approaches exist: choosing what to emphasize in a release note, structuring a conceptual guide, deciding what tone fits a specific audience. For these, AI can inform but should not decide.

| Task | Single right answer? | Approach |
|---|---|---|
| "Extract all error codes from the logs" | Yes | Replacement |
| "Summarize the main benefits of this feature" | No (depends on audience) | Augmentation or Hybrid |
| "Translate this into Spanish" | Mostly yes (with localization nuance) | Hybrid |
| "Decide if this feature is important enough for the changelog" | No (depends on user needs) | Augmentation |
| "Generate API endpoint descriptions from the spec" | Yes | Replacement |

**Question 2: How much do you know about the domain?**

If you are the domain expert, you know when AI is wrong—and you can catch errors before they leave your desk. Augmentation or hybrid approaches work well; AI accelerates your work but your judgment leads.

If the domain is new to you, you may not recognize a subtle error in AI's output. The right response is not to avoid AI—it's to add a subject-matter expert review gate into the workflow alongside AI assistance.

The key test: *If the AI generates something wrong, would I catch it?* If the honest answer is no, your workflow needs an SME gate, regardless of which zone you're in.

**Question 3: What is the cost of an error?**

| Content type | Potential cost of error | Approach |
|---|---|---|
| Medical device instructions | High (user harm, liability) | Augmentation |
| Security documentation | High (vulnerability exposure) | Augmentation |
| API documentation | Medium (user frustration, workarounds) | Hybrid |
| Product release notes | Medium (user confusion, bad decisions) | Hybrid |
| Internal architecture notes | Low (easy to correct) | Replacement |
| Meeting minutes (internal only) | Low (easy to correct) | Replacement |
| Blog post (public, non-critical) | Medium (reputation) | Hybrid |

**Question 4: How much time is available for review?**

More time available allows for careful augmentation and deep iteration. Less time creates pressure to trust AI outputs more than is warranted. Name this pressure explicitly—it is one of the most common routes to publishing content that hasn't been properly reviewed.

| Available time | Approach | Confidence level |
|---|---|---|
| 1+ hours per 1,000 words | Augmentation | High |
| 30–60 min per 1,000 words | Hybrid | Medium-high |
| 15–30 min per 1,000 words | Spot-check replacement | Medium (risky) |
| Less than 15 min per 1,000 words | Don't publish yet | Too risky |


## Red Flags: When Replacement Goes Wrong

Three patterns signal that AI has too much control for the task at hand. Recognize them early—the shift toward over-reliance is gradual and comfortable, until it isn't.

**Red Flag 1: You're skimming, not reading.**

You're approving AI outputs faster than it would take to read them. You think: "it looks fine." The danger is that subtle errors, context mismatches, and compounding small mistakes hide in plain sight when no one is reading carefully.

*How to recover:* slow down and read one full output word for word. If you catch issues, add a structured review checklist and revert to hybrid. If you don't catch issues but feel uncertain, rebuild domain knowledge before trusting the replacement approach again.

**Red Flag 2: You can't explain the content to a subject-matter expert.**

If a colleague asks you why you wrote something a particular way, and the honest answer is "that's what AI wrote," you are publishing content you do not understand. If an expert finds a flaw, you cannot fix it without AI—which puts you in a dependent position neither your employer nor your users should be comfortable with.

*How to recover:* require, as a personal standard, that you can explain any key decision in an AI-generated output before you publish it. If you cannot, that passage is not ready to publish.

**Red Flag 3: You don't know when to trust the output.**

You feel uncertain, but you publish anyway because the deadline is looming. This is the most dangerous pattern. You are responsible for the content; AI is not.

*How to recover:* if you cannot say you are 80% confident in a given output, that output is not ready to publish. Get an SME to validate, or negotiate a delay. If this happens repeatedly, shift to augmentation and rebuild your confidence in the domain.

!!! warning "Word of caution"

    The shift toward over-reliance is gradual and comfortable. Outputs look good. They usually are good. It's the edge cases—the hallucination that looked plausible, the outdated fact that slipped through—that cost you. Build the habit of reading before approving, even when everything seems fine.
