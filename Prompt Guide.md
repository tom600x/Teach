# Prompts Guide

A collection of effective prompts and prompting strategies for GitHub Copilot, with guidance on model selection and token cost efficiency.

---

## Consumption-Based Billing

GitHub Copilot bills on **AI credits** (1 credit = $0.01 USD) based on tokens consumed: **input** (what you send), **output** (what the model generates), and **cache writes** (context stored for reuse). Output tokens are 4–20× more expensive than input tokens depending on the model.

> **Code completions and next-edit suggestions are not billed in AI credits.** Only Copilot Chat and agentic interactions consume credits. Lean on inline suggestions for repetitive edits.

**The two levers that matter most:**
1. **Model choice** — A lightweight model can be 10–50× cheaper than a powerful one. Match the model to the task complexity.
2. **Output length** — The most expensive part of any interaction. Constrain it with explicit format instructions.

### Cache Discount

Token pricing follows a simple formula, but there's a hidden discount most developers don't know about:

Cost = (Uncached Input × Input Price) + (Cached Input × Input Price × 0.1) + (Output Tokens × Output Price)

- Cached input tokens receive a 90% discount compared with uncached input tokens.
- This is why reusing context efficiently can materially reduce cost over multiple turns.
- In practice, keeping prompts structured and reusable often matters as much as choosing a cheaper model.
- Check each model’s documentation for its specific caching behavior and cache retention window, since these vary by provider and model.

---

## Model Selection Reference

Prices are **per 1M tokens**. Use **Auto** model selection in Chat if unsure — it picks the best available model automatically.

### Lightweight (cheapest)

| Model | Input | Output | Best for |
|---|---:|---:|---|
| GPT-5.4 nano | $0.20 | $1.25 | Trivial edits, syntax fixes |
| GPT-5 mini | $0.25 | $2.00 | General coding, documentation, visuals |
| Raptor mini *(preview)* | $0.25 | $2.00 | Inline suggestions and explanations |
| Gemini 3 Flash *(preview)* | $0.50 | $3.00 | Fast lightweight coding questions |
| GPT-5.4 mini | $0.75 | $4.50 | Agentic codebase exploration |
| MAI-Code-1-Flash | $0.75 | $4.50 | Everyday coding and multi-turn workflows |
| Claude Haiku 4.5 | $1.00 | $5.00 | Quick questions, repetitive tasks |
| Gemini 3.5 Flash | $1.50 | $9.00 | Fast coding questions |

### Versatile (mid-range)

| Model | Input | Output | Best for |
|---|---:|---:|---|
| Gemini 2.5 Pro | $1.25 | $10.00 | Complex code, debugging, research |
| GPT-5.3-Codex | $1.75 | $14.00 | Agentic software development |
| Gemini 3.1 Pro *(preview)* | $2.00 | $12.00 | Long-context reasoning, edit-test loops, visuals |
| Claude Sonnet 4.x | $3.00 | $15.00 | General-purpose complex tasks, visuals |
| Qwen2.5 | — | — | Code generation, reasoning, debugging |

### Powerful (most expensive)

| Model | Input | Output | Best for |
|---|---:|---:|---|
| GPT-5.4 | $2.50 | $15.00 | Deep reasoning, architecture analysis |
| GPT-5.5 | $5.00 | $30.00 | Multi-step problem solving |
| Claude Opus 4.x | $5.00 | $25.00 | Complex reasoning and debugging |
| Claude Fable 5 | $10.00 | $50.00 | Long-horizon autonomous coding |

*Long-context tiers add additional pricing above model thresholds (272K tokens for OpenAI models, 200K for Gemini). Cache write costs apply to Anthropic models.*

---

## Token-Saving Techniques

Reduce credit consumption without sacrificing output quality.

- **Constrain the format upfront:** "Bullet list only. No intro or summary." Prose is expensive; structured output is short.
- **Cap response length:** "Answer in under 50 words." or "One paragraph max."
- **Reference, don't paste:** Use `#file` or `@workspace` references instead of pasting large code blocks into the prompt.
- **Right-size the model:** Default to lightweight. Step up only when output quality is insufficient.
- **Batch related questions:** One prompt with three questions costs less than three separate prompts.
- **Skip confirmation steps for routine tasks:** Remove "restate my question" or "ask clarifying questions" from everyday prompts — reserve them for high-stakes work only.
- **Ground cheaply:** "Answer only based on the information I provide. If unsure, say so." achieves reliable grounding without verbose instructions.
- **Prefer `Auto` model selection:** Copilot's automatic selection balances capability and cost; override only when you have a specific reason.

---

## Avoiding LLM Confusion — General Best Practices

Use these prompts to keep the model focused and reduce hallucination or drift.

- **Set the role upfront:** "You are a senior software engineer specialising in C#. Answer only within that context."
- **Constrain scope:** "Answer only based on the information I provide. If unsure, say so."
- **Prevent over-answering:** "Concise answer. No preamble, no summary."
- **Clarify first *(high-stakes tasks only)*:** "Before writing any code, ask any clarifying questions needed to fully understand the problem. Once I confirm your understanding, summarise your approach. Then proceed. After presenting the solution, ask me to confirm before finalising."
- **Check comprehension:** "Restate my question in your own words before answering."
- **Prevent scope creep:** "Only change what I explicitly ask. Do not refactor, rename, or improve anything else."
- **Validate then execute:** "Summarise what you will do and list each step. Wait for my confirmation. Then carry out every step completely — do not stop midway, do not ask permission at each step, deliver the full result."

> **Cost tip:** "Clarify first" and "Check comprehension" add a full extra round-trip of tokens. Reserve them for complex or high-risk work.

---

## One-Shot Prompting

Provide a single example of the output format before your real request. The model mirrors the pattern.

**When to use:** You want a specific output format, tone, or structure and one example is enough.

**Model:** Any lightweight model (GPT-5 mini, MAI-Code-1-Flash).

**Template:**
```
Example: [your example]

Now do the same for: [request]
```

**Example:**
```
Example: "As a customer, I want to reset my password so that I can regain access to my account."

Now do the same for: A user uploading a profile photo.
```

> **Cost tip:** Remove "Here is an example of the output I want" and similar framing — it adds tokens without improving the result. Just show the example directly.

---

## Few-Shot Prompting

Provide two or more examples to establish a stronger pattern. Ask the model to confirm it in one sentence before applying it.

**When to use:** The output structure is nuanced or one example is insufficient to infer the rule.

**Model:** Any lightweight model (GPT-5 mini, MAI-Code-1-Flash).

**Template:**
```
Pattern examples:
Example 1: [input] → [output]
Example 2: [input] → [output]
Example 3: [input] → [output]

Explain the pattern in one sentence. Once I confirm, apply it to: [request]
```

**Example:**
```
Pattern examples:
Example 1: File not found → "We couldn't find that file. Check the name and try again."
Example 2: Network timeout → "The connection timed out. Check your internet and retry."
Example 3: Invalid input → "That value doesn't look right. Enter a number between 1 and 100."

Explain the pattern in one sentence. Once I confirm, apply it to: The user's session has expired.
```

> **Cost tip:** Ask the model to explain the pattern in *one sentence*, not a paragraph. This cuts confirmation output tokens significantly.

---

## Chain-of-Thought Reasoning

Ask the model to reason step by step. Use for ranking, diagnosis, and trade-off decisions where the reasoning matters as much as the answer.

**When to use:** Risk ranking, root cause analysis, architecture decisions, prioritisation.

**Model:** Versatile or powerful (Claude Sonnet 4.x, Gemini 3.1 Pro, GPT-5.4) — depth is the point here.

**Template:**
```
List the top [X] [things] for [context].
For each: why it belongs in the top [X], impact severity, one suggested mitigation.
Think step by step.
```

**Example — code review:**
```
List the top 5 production deployment risks in this codebase.
For each: why it's a risk, likely impact, one concrete mitigation.
Think step by step.
```

**Example — learning a topic:**
```
List the 3 concepts a developer must understand before using async/await in C#.
For each: why it's essential, the common mistake without it, one-sentence rule of thumb.
Think step by step.
```

> **Cost tip:** "Think step by step" triggers chain-of-thought reasoning on its own. Remove "Show me your thinking for each item before moving to the next" — it's redundant and generates extra output tokens.

---

## Agentic / Deep Research Prompting

Use when you want the model to act autonomously across multiple sources or reasoning steps — research, synthesis, and structured output in one prompt.

**When to use:** Competitive analysis, trend research, technology evaluation, strategic summaries.

**Model:** Use a powerful or versatile model (Claude Opus 4.x, GPT-5.4, Gemini 3.1 Pro). These tasks justify the cost — a lightweight model will produce shallower synthesis.

**Template:**
```
Research [TOPIC]. Find the [X] most important insights or trends.
For each: why it's significant and how it connects to the others.
Output: one-page executive summary for [AUDIENCE]. No preamble.
```

**Example:**
```
Research the current state of AI adoption in enterprise software development.
Find the three most important trends shaping this space.
For each: why it's significant and how it connects to the others.
One-page executive summary for a non-technical leadership audience. No preamble.
```

> **Cost tip:** "No preamble" saves the opening paragraph of output tokens. "Analyse and cross-reference all the major trends, sources, and perspectives you can identify" is implied by the task — removing it saves ~25 input tokens per prompt.

---

## The DRAG Framework

A structured framework that ensures the model has everything it needs for a high-quality, grounded response.

| Letter | Stands for | What to include |
|--------|------------|-----------------|
| **D** | **Direction** | The role or expertise to adopt |
| **R** | **Request** | The specific task or question |
| **A** | **Action** | The output format |
| **G** | **Goal** | The purpose and success criteria |

**Model:** Match to task complexity. DRAG works at any tier.

**Template:**
```
Direction: You are [role with relevant expertise].
Request: [Specific task or question].
Action: Respond as [format — bullet list / numbered steps / table / one-page summary].
Goal: The output will be used to [purpose]. Success looks like [criteria].
```

**Example:**
```
Direction: You are a senior cloud architect with experience designing Azure solutions for regulated industries.
Request: Review the following architecture and identify the three biggest security risks.
Action: Numbered list. For each: the risk, likely impact, one recommended mitigation.
Goal: Presented to a security review board. Success means a non-technical stakeholder can understand each risk.
```

**Why DRAG works:** Separating direction, request, action, and goal eliminates vague responses — the model knows *who it is*, *what you want*, *how to format it*, and *why it matters*.

> **Cost tip:** Specifying the Action (format) upfront prevents the model from choosing its own structure, which often produces longer prose. A tight Action instruction directly reduces output tokens.

---

## KDS (Keystone Design System) Prompts

The KDS-specific prompt library now lives in its own guide for easier maintenance:

- [KDS Prompt Guide.md](./KDS%20Prompt%20Guide.md)
- [KDS-Agent-Guide.md](./KDS-Agent-Guide.md)

Use the dedicated guide for screen-generation, audit, remediation, and agent-mode prompts related to PA.gov KDS work.


