# Agentic AI Workflows for Technical Writers

## From Prompts to Pipelines

Through the previous modules, you have worked with AI as a conversational partner: you prompt, it responds, you iterate. Agentic AI shifts this relationship. Instead of responding to a prompt, an agent pursues a goal — planning steps, using tools, handling intermediate results, and iterating until the goal is met or human input is needed.

For technical writers, this matters because a significant portion of documentation work is not single prompts but multi-step pipelines: "every time a new ticket closes, extract the user-visible change, classify it, add it to the release-notes draft, flag breaking changes for engineer review, and notify the team when the draft is ready." A single prompt cannot do this. An agent can.

By the end of this module, you'll be able to:
- Describe what agentic AI is and how it differs from prompt-based AI.
- Identify the kinds of documentation work that benefit from agentic workflows.
- Recognize the risks specific to agents — and how to mitigate them.
- Read a real-world agentic workflow design and identify where human judgment is preserved.


## What Makes an AI System "Agentic"?

An AI agent has four characteristics that a simple prompt-response system does not:

1. **Goal-directedness.** Works toward an outcome, not a single output.
2. **Tool use.** Can call external tools — APIs, search engines, code execution, other models — to get things done.
3. **Memory and state.** Keeps track of what has happened so far and adjusts based on intermediate results.
4. **Loop and recovery.** Can repeat steps, try alternative approaches, and handle exceptions without restarting.

A useful mental model: an LLM is a very knowledgeable colleague who answers one question at a time. An agent is a junior colleague with a task list, the ability to use the team's tools, and the initiative to keep going until the list is done — or until they need to ask you something.

> 💡 The **Model Context Protocol (MCP)** is an emerging open standard for connecting AI models to external tools and data sources in a consistent way. If your organization is building agentic workflows, MCP is worth knowing as the standard that is likely to shape how tools and agents interoperate over the next few years. You do not need to master it to use agents effectively today; you do need to know that the ecosystem is moving toward standardization, which will make agent-based work more portable and less tool-specific over time.


## The Five Risks Specific to Agents

Agentic workflows add five classes of risk that prompt-based work does not have. Address each deliberately.

1. **Silent drift.** The agent quietly produces worse output over time — model versions change, upstream data changes, prompt regressions accumulate. *Mitigation:* golden-set tests and periodic audits (see **Evaluating AI Outputs**).
2. **Compounding errors.** An error in step 1 becomes the input to step 2, and so on, with each step amplifying the original mistake. *Mitigation:* human review gates and sanity checks between steps, not only at the end.
3. **Tool misuse.** The agent calls a tool in a way its designers did not anticipate — writing to a system it should only read, or consuming API quota at unexpected rates. *Mitigation:* scoped permissions; quota alarms; dry-run modes during development.
4. **Runaway loops.** The agent iterates endlessly on an unreachable goal. *Mitigation:* explicit stopping conditions, maximum step counts, time budgets.
5. **Accountability gap.** When agent output is wrong, who is responsible? *Mitigation:* every agent output is attributed to a human owner. "The agent did it" is not an answer.


## When To Use an Agent

An agent earns its place when the work has a specific shape. Before commissioning one, check the task against these five criteria. The more of them it satisfies, the stronger the case.

**The task repeats on a predictable cycle.** Agents are infrastructure. Like any infrastructure, they carry a build-and-maintain cost. That cost only pays off when the task runs often enough — weekly, every sprint, every release. A task you do once a quarter is almost never worth automating.

**The task is triggered by an event you can detect.** Agents need a reliable signal to start. A sprint moving to Active. A pull request merging. A ticket changing status. If the trigger is "someone emails me," the agent has no way in. If the trigger is "a webhook fires," it does.

**The steps are stable and definable.** An agent follows a sequence. If the sequence changes significantly every time — because the inputs are unpredictable, because the stakeholders are different, because the answer depends on judgment calls no one has written down — the agent will need constant rewriting to keep up. The best candidates are the tasks where you could write a procedure document and have it still be accurate six months later.

**The inputs come from systems the agent can reach.** An agent that needs to read your ticket system, fetch a linked specification page, and write to a Git repository can be built. An agent that needs to read an email thread, interpret a conversation, or understand an unwritten team convention cannot — at least not reliably. Check that your data lives in systems with APIs before you design around it.

**The output can be verified.** Because agents run without step-by-step supervision, you need to be able to check their work at defined points. If you can articulate what a correct output looks like — a correctly classified ticket, a well-formed draft, a release note that matches the change log — you can build a review gate. If "correct" is too contextual to define in advance, the task belongs in the Augmentation zone the Augmentation zone (see The Spectrum: Augmentation ← Hybrid → Replacement), not in an agent.

A quick reference:

| Signal | What it tells you |
|---|---|
| "I do this every sprint and it always starts the same way." | Strong candidate. |
| "It depends on the project — no two are alike." | Weak candidate; keep it as a prompt workflow. |
| "I know exactly what wrong looks like." | Strong candidate — you can build a gate. |
| "I'd know a bad output if I saw it, but I can't define it in advance." | Weak candidate; human judgment required throughout. |
| "The data is all in Jira and Confluence." | Strong candidate — the tools have APIs. |
| "Half the context comes from Slack threads and memory." | Weak candidate; inputs are too unstructured. |
| "This takes me two hours every time and never varies." | Strong candidate; the ROI is there. |
| "Something this important should have a human on every step." | Don't automate — redesign the workflow with tighter human gates instead. |


## When Not To Use an Agent

Not every repeating task is an agent candidate. An agent is the wrong tool when:

- The task is rare (once a month or less). The maintenance cost of the agent will exceed the time it saves.
- The task requires information that lives mostly in a conversation or in someone's head.
- The cost of a silent error is catastrophic and the task is hard to validate at volume — safety-critical procedures, legal disclosures, security advisories.
- The underlying system changes frequently and unpredictably. Agents assume their environment is stable enough to reason about.

Prompt engineering remains the right tool for one-off, judgment-heavy, or context-sensitive work. Agents are for the repeating, stable, verifiable work — and even then, with human review gates built into the design.


## A Worked Example: The Intelligent Documentation System

Abstract definitions of agentic AI are easier to hold when anchored to something real. The example below describes a documentation workflow that a technical writer or team lead could plausibly design and commission. It is not a product that exists off the shelf — it is an illustration of how the concepts in this module combine in practice.

### The Problem It Solves

Sprint after sprint, the same work falls to the technical writer manually: scan the backlog, figure out what needs documenting, determine what is new versus updated versus irrelevant, prioritise the list, chase stakeholders, and start drafting. This is not judgment work. It is mechanical triage that repeats on a fixed cycle. That is exactly the profile of work suited to an agent.

### What the System Does

The Intelligent Documentation System (IDS) is a supervised agentic workflow triggered at the start of each sprint, when a Jira sprint is moved to Active status. From that trigger, it works through a sequence of steps without human direction — until it reaches a gate where human judgment is required.

**Step 1 — Ingest.** The agent reads every issue in the sprint backlog via the Jira API: summaries, descriptions, labels, linked specification pages, linked design files, and any issues carried over from the previous sprint.

**Step 2 — Classify.** For each issue, the agent determines what documentation work is implied. Does this need a user guide update? An API reference entry? A security note? Are there UI strings that will affect translation? It does this by reading the issue description semantically — not just by checking labels, because developers frequently forget to add them.

**Step 3 — Prioritise and map.** The agent produces a structured task list, sorted by priority (hotfixes and carry-overs first, new features next, minor changes last), alongside a stakeholder map for each task showing who owns the feature, who designed it, and who the tech writer should contact.

**Step 4 — Notify and wait.** The agent sends the task list to the assigned technical writer. The writer reviews each item: approve as classified, amend the priority or doc type, or relegate to a stash of deferred items. **This is the first human gate. Nothing proceeds until it is cleared.**

**Step 5 — Research and scaffold.** For approved tasks, the agent researches each one — re-reading the Jira issue, fetching linked specification content, querying an internal knowledge base for related existing documentation. It then creates a structured draft file in the documentation repository: not a finished article, but a scaffold with suggested headings, AI-generated paragraph drafts drawn from the source material, inline source citations, and clearly flagged gaps where no information was found.

**Step 6 — Open a pull request.** Each scaffolded draft is committed to a feature branch and surfaced as a pull request. The tech writer edits the draft directly in the pull request, requests SME input on specific lines, and merges when satisfied. The existing pipeline that builds and deploys the documentation site does the rest. Merge equals publish. **This is the second human gate. No content reaches the portal without it.**

**Step 7 — Ingest meeting notes.** At any point during the sprint, the tech writer can feed meeting transcripts or written notes into the system. The agent reads them, extracts relevant decisions and clarifications, reconciles them with existing drafts, fills gaps where possible, and flags contradictions between what was said in a meeting and what was written in the original ticket.

**Step 8 — Close the loop.** At sprint end, the agent generates a documentation retrospective: what was completed, what moved to stash, what carried over. It stores the tech writer's amendments and uses them to improve its classifications in future sprints.

### What Makes This Agentic

The IDS exhibits all four properties introduced earlier in this module:

| Property | Where it appears |
|---|---|
| Goal-directedness | The agent is not responding to a prompt. It is working toward a goal: a complete, reviewed set of documentation tasks for the sprint. |
| Tool use | Jira API, specification repositories, Git, messaging tools, a search index over the existing documentation corpus. |
| Memory and state | It maintains a stash across sprints, tracks amendment history, and stores the status of every draft throughout its lifecycle. |
| Loop and recovery | It re-ingests new information (meeting notes) against existing drafts, reconciles contradictions, and iterates without restarting from scratch. |

### Where Humans Stay in Control

The tech writer is not removed from the workflow — their role shifts. They spend less time on triage and more time on judgment.

There are two hard gates where nothing proceeds without a human decision:

- **After Step 3:** the tech writer must approve, amend, or relegate each task before any drafting begins.
- **After Step 5:** the tech writer must review and merge the pull request before any content is published.

Between those gates, the agent works. At those gates, the human decides.

Trust is built incrementally. A sensible onboarding path: the system starts in observe-only mode for the first few sprints — reporting what it would do, but not acting. As the tech writer develops confidence in its classifications, it is given progressively more autonomy. High-confidence, routine tasks are eventually handled end-to-end; low-confidence and ambiguous tasks always remain gated.

### The Five Risks, Applied

The five risks named earlier in this module each appear in this system. Here is how the design addresses them:

| Risk | How it appears here | Mitigation in this design |
|---|---|---|
| Silent drift | Classification accuracy degrades as the product evolves and issue descriptions change. | The tech writer's amendments are logged and fed back into the classifier; a sample of classifications is audited periodically. |
| Compounding errors | A misclassified issue produces a draft in the wrong section of the portal, reviewed in the wrong context. | The tech writer approval gate at Step 4 catches classification errors before any drafting begins. |
| Tool misuse | The agent writes to a branch it should not, or calls the ticket API in a way that modifies data. | The agent has read-only access to the ticket system; Git write access is scoped to the documentation repository only. |
| Runaway loops | The meeting-notes ingestion step runs indefinitely on a large transcript. | An explicit maximum processing budget per run; a timeout with a logged warning. |
| Accountability gap | A published draft contains an error and no one is sure whether it came from the agent or the tech writer. | Every agent-generated sentence carries an inline source citation in the draft. The pull request history records every human edit. The published file's version history shows who merged it and when. |

### What This Is Not

This system is not designed for safety-critical documentation, legal disclosures, or content where a silent error has severe consequences. It is designed for the high-volume, repeating, classifiable documentation work that makes up the majority of sprint-by-sprint output: user guide updates, admin guide additions, API reference entries, release notes.

For regulated or high-stakes content, the Augmentation zone (see The Spectrum: Augmentation ← Hybrid → Replacement) remains the right choice. Agents earn their place on routine, stable, verifiable work — and this system is honest about that boundary.

!!! note

    The Intelligent Documentation System is not a product you install. It is a design pattern you implement. The building blocks — a ticket system with an API, a Git repository, a documentation platform, an LLM API, a knowledge search index — are all standard tools. The agentic layer is the orchestration that connects them and the gate design that keeps a human in the loop at the right moments. The pattern is what is transferable; the specific tools will vary by organisation.
