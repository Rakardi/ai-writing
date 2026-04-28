
# Key Concepts

This module gives you the vocabulary you need to understand the AI field, follow vendor documentation, and choose the right tool for a given task — without getting lost in hype or acronyms.

By the end of this module, you'll be able to:

- Define the core concepts — AI, ML, NLP, LLMs, RAG, SLMs, and agentic AI — in plain terms, and explain where each fits in a technical writer's work.
- Distinguish the main categories of AI models (general-purpose LLMs, reasoning models, SLMs, multimodal, RAG-enabled, agents) and recognize which category a given tool belongs to.
- Apply a three-step decision aid — shape, stakes, sensitivity — to choose the right kind of AI tool for a documentation task.

---

## Key Concepts

### Artificial Intelligence

Artificial Intelligence (AI) mimics human intelligence in complex processes such as learning, reasoning, and self-correction. Tasks that can be automated or enhanced with AI include visual perception, speech recognition, decision-making, and translation. When used in technical communication, AI can help authors generate and review content, automate repetitive tasks, enhance user experience through intelligent bots, and streamline content management and workflow processes. Rather than replacing people, AI can take over mundane tasks, allowing technical writers to have more time for strategic, creative, and decision-making tasks.

!!! tip ""

    *Think of AI as a very sophisticated mimic that has read everything ever written. It can imitate intelligence—sometimes brilliantly—without having experienced the world that produced all those words. That gap between imitation and understanding is where errors, hallucinations, and misjudgments enter the picture.*

### Machine Learning

Machine Learning (ML) is a core subset of AI. Its focus is on developing algorithms that enable computers to learn from data and make informed predictions or decisions autonomously. ML does not simply follow written instructions. Rather, it analyzes "training data", creates mathematical models, and then uses those to perform tasks with minimum to no human intervention. In the field of technical communication, ML can analyze user behaviour and feedback to improve the usability and relevance of technical documents. It can be trained to parse through, organize, structure, categorize, and find patterns in large amounts of technical information.

!!! tip ""

    *Think of ML as a chef who has tasted thousands of dishes and gradually internalized the rules of flavor—not by being told "salt enhances sweetness," but by tasting enough dishes that the pattern revealed itself. The chef can now create new dishes by feel, without being able to articulate every rule they follow. Impressively capable; not infallible.*

### Natural Language Processing

Natural Language Processing (NLP) has emerged as a product of computer science, AI, and linguistics. It provides algorithms that allow computers to emulate the human processes of processing and generating written and spoken communication. NLP is indispensable in language translation, sentiment analysis, and bots. In technical communication, NLP plays a vital role by transforming structured data inputs into intelligible human language. This enables tasks such as automatic content summarization and initial draft generation, enhancing the efficiency and scalability of technical writing processes.

!!! tip ""

    *Think of NLP as a professional interpreter who doesn't just translate words but reads intent and adjusts for tone. Without NLP, AI would see the sentence "Can you open the window?" as a question about capability; NLP enables it to recognize that same sentence as a request.*

### Large Language Models

Large Language Models (LLMs), such as ChatGPT and other generative pre-trained transformers, are advanced AI models dedicated to processing and generating intelligible human-like text. Extensive datasets comprising books, articles, websites, and other textual content are used to train LLMs so that they process context within their input window and generate statistically likely continuations. In the realm of technical communication, LLMs are to make a lasting impact. Creating initial drafts is just one application that easily springs to mind. More impressive, however, is their capability to refine content, add a personal touch to it based on iterative collaboration with the author. By adopting LLMs, technical writers can develop comprehensive documents driven by the target audience needs, and can do so faster than ever, without compromising the delivered quality. This enables technical writers to focus more on strategic tasks, elevating the role of human creativity and decision making in producing superior technical content.

!!! tip ""

    *Think of an LLM as a remarkably well-read generalist who has internalized millions of documents. Ask them anything and they'll give you a fluent, plausible answer—but their knowledge has a cutoff date, they can confabulate with great confidence, and they work by predicting what words are likely to come next, not by "understanding" a topic the way you do.*

> 💡 **Two terms worth a minute.**
>
> **Tokens** are the pieces an LLM reads and writes — roughly, a word, a punctuation mark, or a fragment of a long word. A short paragraph is maybe 100 tokens; a long document is tens of thousands. Every model prices and limits its work in tokens, and most of the tool's surprising behaviour — pricing, cutoffs, truncation — comes back to them.
>
> The **context window** is how many tokens a model can consider at once. Everything in your current conversation (your prompt, the documents you pasted, the model's previous replies) competes for space in that window. Exceed it and the earliest content drops out silently — which is often the cause of "the AI forgot what I told it earlier."

### Retrieval-Augmented Generation

Retrieval-Augmented Generation (RAG) is a technique that enhances an LLM's outputs by first retrieving relevant, up-to-date information from a specified source—such as a product knowledge base, internal documentation repository, or live database—and then feeding that information into the model as context before generating a response. Unlike a standard LLM, which answers entirely from its training data, a RAG-enabled system can access documents it was never trained on, significantly reducing hallucinations on factual or domain-specific content.

For technical writers, RAG is particularly useful for building internal documentation assistants: tools that answer user questions by drawing on your team's actual documentation, not on generic internet data.

!!! tip ""

    *The difference between a standard LLM and a RAG-enabled system is the difference between asking a colleague to answer from memory versus asking them to look it up in the company documentation first, then answer. The lookup step grounds the response in your actual content.*

#### RAG in Practice: What the Technical Writer Owns

You will encounter RAG most often in one of two situations: your organization is building a documentation chatbot or internal knowledge assistant, or an external AI tool you use has been connected to your team's knowledge base. In both cases, the quality of the RAG system depends heavily on work that falls squarely in the technical writer's domain.

A simple RAG pipeline has five stages: **ingest** (load source content), **chunk** (split it into passages), **embed** (convert each passage into a numerical representation), **retrieve** (find the most relevant passages for a query), and **generate** (produce an answer grounded in those passages).

The technical writer influences four of these five stages — more than any other role:

- **Source quality.** RAG can only retrieve what is in the knowledge base. Outdated, duplicated, or contradictory documentation produces outdated, confused, or contradictory answers. A RAG project is an opportunity to clean house.
- **Chunking strategy.** If chunks are too large, the retriever surfaces too much noise. Too small, and the retrieved passage lacks context. Structured, well-headed documentation chunks naturally; wall-of-text documentation does not. Your information architecture decisions become retrieval decisions.
- **Metadata and tagging.** Tags such as product version, audience, content type (task / reference / concept), and last-updated date let the retriever filter by context. Untagged content forces the retriever to guess. Adding structured metadata is often the single highest-leverage contribution a writer can make to a RAG project.
- **Answer evaluation.** When the chatbot returns a wrong or incomplete answer, someone has to diagnose whether the retrieval stage or the generation stage failed — and whether the source content was the real problem. That diagnosis usually lands with the writer.

### Small Language Models

Small Language Models (SLMs) are AI models that are significantly more compact than large general-purpose LLMs. They are typically fine-tuned on a narrow domain—medical terminology, legal language, a company's proprietary style guide, software documentation—making them faster to run, cheaper to operate, and often more accurate on specialized tasks than a general-purpose model that has learned "a little about everything."

For technical writers, SLMs represent a practical option for high-volume, domain-specific tasks: checking adherence to a specific style guide, extracting terminology, or classifying documentation types. The trade-off is limited generality—a model tuned for software documentation will struggle if asked to write marketing copy.

!!! tip ""

    *Think of an SLM as a specialist consultant versus a generalist. Less breadth; more depth. And considerably cheaper per consultation.*

### Agentic AI

Agentic AI refers to AI systems that can pursue a goal across multiple steps—using external tools, adapting based on intermediate results, and completing work without requiring human direction at every stage. Where a standard LLM responds to a prompt, an agent acts on a goal: it fetches data, makes decisions, calls other services, and iterates until the task is complete or it needs human input.

For technical writers, this matters because agents can handle the routine, repeating, multi-step documentation work that prompt engineering alone cannot: weekly release note generation from live ticket systems, automated style guide compliance checks across a document library, or real-time synchronization of API documentation with a spec file.

The concept of agentic AI is explored in detail in **Agentic AI Workflows for Technical Writers**.

!!! tip ""

    *Think of an agent as a project coordinator who takes your goal, breaks it into tasks, assigns each task to the right tool, checks on progress, handles exceptions, and reports back—without needing you to be present at every step. Powerful; but the coordinator still needs your oversight at key decision points.*

---

> 💡 **A map of AI model categories**
>
> Specific AI product names and capabilities change rapidly—often quarterly. Rather than a product list that would date quickly, here is a more stable map of model *categories* that helps you understand what is available and when each type fits your work:
>
> - **General-purpose LLMs** — The most widely used category. Handle text generation, summarization, Q&A, translation, and drafting. Most AI tools a technical writer encounters day-to-day fall here.
> - **Reasoning models** — A newer category that deliberates before responding. Slower and more expensive, but better suited to complex decisions and ambiguous problems where the "why" matters as much as the "what." Useful when accuracy matters more than speed.
> - **Small Language Models (SLMs)** — Compact models, often fine-tuned for a specific domain or style guide. Cheaper, faster, and sometimes more accurate for narrow tasks. Increasingly available for self-hosted or on-device deployment.
> - **Multimodal models** — Handle combinations of text, images, audio, and video in a single model. Not covered in depth in this course; technical writers most often encounter them via visual description, alt-text generation, and diagram-to-code workflows.
> - **RAG-enabled systems** — Any model category can be wrapped in a RAG pipeline to ground responses in your organization's content.
> - **Agents and agentic frameworks** — Systems that combine models with tools, memory, and decision loops. Covered in depth in **Agentic AI Workflows for Technical Writers**.
>
> When in doubt, start with a general-purpose LLM. Escalate to reasoning models for complex judgment, SLMs for repeatable narrow tasks, and agentic frameworks only when a task truly requires multi-step execution.

---

## Choosing the Right Tool: A Decision Aid

One of the most common questions a new AI-assisted writer asks is: *"For this task, which kind of tool should I reach for?"* The decision aid below is intentionally simple. It will not be right 100% of the time, but it will be right often enough to keep you out of trouble.

**Step 1. What is the shape of the task?**

| If the task is… | Then reach for… | Because… |
|---|---|---|
| A one-off text generation, summary, or rewrite | A general-purpose LLM | It's the Swiss Army knife. Fast, flexible, good enough for most one-off work. |
| A complex decision or analysis with ambiguity | A reasoning model | It deliberates before answering, catching issues a fast model would miss. |
| A repeating, narrow task on domain-specific content | An SLM or a fine-tuned LLM | Cheaper to run at volume, often more accurate on the narrow task. |
| A factual lookup over your team's own content | A RAG-enabled system | Grounds the answer in your actual documentation, not the model's training data. |
| A multi-step task with tool use (fetch data, generate, post back) | An agentic workflow | Single prompts cannot loop, call tools, or recover from errors; agents can. |
| A task involving images, diagrams, audio, or video | A multimodal model | Text-only models cannot see or hear. |

**Step 2. What is the stakes level?**

- **Low-stakes** (internal drafts, brainstorming, personal notes) — any approved tool is fine; iterate freely.
- **Medium-stakes** (public-facing draft before review) — general-purpose LLM is fine, but verify factual claims against sources.
- **High-stakes** (regulated content, legal or safety implications, customer-visible published content) — use the most accurate tool available (often a reasoning model), ground it with RAG or authoritative sources, and apply stronger human review.

**Step 3. What is the data sensitivity?**

Return to **Data Handling in Practice: What to Paste, What Not to Paste**. If the input is Confidential or Restricted, tool choice is constrained by what your organization has approved — not by what would be technically ideal. Policy beats preference.

> 💡 **Rule of thumb:** Match the tool to the task's *shape*, *stakes*, and *sensitivity*. If you're choosing a tool for reasons other than those three, you're probably choosing it because it's familiar, not because it's right.

---
