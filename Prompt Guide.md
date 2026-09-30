# Prompts Guide

A collection of effective prompts and prompting strategies for GitHub Copilot, with guidance on model selection and token cost efficiency.

---

## Consumption-Based Billing

GitHub Copilot bills on **AI credits** (1 credit = $0.01 USD) based on tokens consumed: **input** (what you send), **cached input** (reused context), **cache writes** (context stored for reuse), and **output** (what the model generates).

> **Code completions and next-edit suggestions are not billed in AI credits.** Only Copilot Chat and agentic interactions consume credits. Lean on inline suggestions for repetitive edits.

**The two levers that matter most:**
1. **Model choice** — Model prices differ substantially. Match the model to the task complexity and check GitHub's live pricing before cost-sensitive work.
2. **Output length** — The most expensive part of any interaction. Constrain it with explicit format instructions.

### Cost Formula

Prices vary by model and, for some models, context size:

Cost = (Input Tokens × Input Price) + (Cached Input Tokens × Cached Input Price) + (Cache-Write Tokens × Cache-Write Price) + (Output Tokens × Output Price)

- Divide token counts by 1,000,000 before multiplying by the prices below.
- Cached-input discounts are model-specific; do not assume a fixed percentage.
- Cache-write charges apply to Anthropic models and newer OpenAI models.
- Long-context pricing applies after the model-specific input threshold.

---

## Model Selection Reference

Model names, availability, release status, and prices change frequently. Use GitHub's live [AI model comparison](https://docs.github.com/en/copilot/reference/ai-models/model-comparison), [supported models](https://docs.github.com/en/copilot/reference/ai-models/supported-models), and [models and pricing](https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing) pages as the source of truth. Availability also depends on plan, client, organization policy, and feature.

### Quick Choice by Programming Task

| Task | Best model tier or family | Best current workflow | Why |
|---|---|---|---|
| Syntax help, explanations, documentation, small functions | Lightweight/fast: Luna, mini/nano, Haiku, Gemini Flash, MAI-Code Flash, or Kimi Code | Interactive | Lowest latency and cost for bounded work |
| Everyday feature work, tests, reviews, and moderate refactors | Balanced: Terra, Claude Sonnet, Grok, or a general-purpose GPT | Interactive | Good quality, speed, tool use, and instruction following |
| Codebase search and multi-file implementation | Coding/agent: Codex, Sol, Claude Sonnet/Opus, Kimi K3, or Grok agentic models | Interactive with tools, or a specialized custom agent | Better planning, tool use, error recovery, and validation |
| Difficult debugging, architecture, migrations, or security analysis | Deep reasoning: flagship GPT/Sol, Claude Opus, or another powerful reasoning model | Plan, then Interactive implementation | Stronger multi-step reasoning and trade-off analysis |
| Long-running autonomous work across a large repository | Long-horizon agent: Astra, Claude Fable/Opus, Kimi K3, or the current equivalent | Autopilot or an implementation agent | Designed for sustained planning, large context, and repeated verification |
| Unsure or mixed work | Auto | Any | Copilot selects for availability and task complexity; paid plans may receive an Auto discount |

Start with **Auto** or a balanced model. Move to a lightweight model when speed and cost matter more than depth; move to a powerful model only when the task requires complex reasoning, large-context analysis, or long-running agent work.

### Languages and Frameworks

Language usually matters less than **task size, ambiguity, and required tool use**. Current coding models are broadly capable across mainstream stacks. Choose a model for the work being done, then provide the framework version, project conventions, relevant files, and build/test commands.

| Stack | Good default | Step up to a powerful reasoning/agent model for |
|---|---|---|
| **ASP.NET MVC / .NET Core / C#** | Balanced GPT/Terra, Codex, or Claude Sonnet for controllers, services, EF Core, tests, and routine refactors | .NET Framework-to-modern .NET migrations, dependency injection or middleware issues, distributed systems, performance, and multi-project solutions |
| **Angular / TypeScript** | Codex, balanced GPT, or Claude Sonnet for components, services, RxJS, forms, tests, and upgrades with clear requirements | Major-version migrations, complex RxJS flows, state architecture, monorepos, build failures, and broad strict-typing changes |
| **React / Next.js / TypeScript** | Codex, balanced GPT, or Claude Sonnet for components, hooks, routes, tests, and accessibility fixes | Rendering and hydration bugs, state architecture, performance, framework migrations, and large design-system changes |
| **Python / Django / FastAPI** | Balanced GPT, Codex, or Claude Sonnet for application code, APIs, tests, typing, and data scripts | Concurrency, difficult type-system issues, framework migrations, performance, data pipelines, and large package refactors |
| **Java / Spring** | Codex, balanced GPT, or Claude Sonnet for services, controllers, persistence, tests, and routine upgrades | Legacy modernization, complex dependency or transaction problems, JVM performance, and large multi-module builds |
| **SQL / data access** | A balanced model for queries, mappings, migrations, and straightforward schema work | Query-plan analysis, concurrency, indexing strategy, data migrations, and cross-service consistency |
| **HTML / CSS / UI libraries** | A lightweight or balanced model for components, responsive styling, and accessibility corrections | Large design systems, difficult browser behavior, visual regression analysis, and coordinated application-wide changes |
| **Shell / PowerShell / CI/CD configuration** | A lightweight or balanced model for small scripts and pipeline edits | Security-sensitive automation, complex deployment failures, cross-platform behavior, and multi-environment infrastructure changes |

For small, well-scoped work in any language, a lightweight model is usually enough. For migrations, architecture, subtle bugs, or repository-wide changes, use a stronger reasoning model even when the language itself is familiar.

### Model-Family Benefits

These are family-level tendencies, not guarantees. Prefer the newest available member that fits your plan and task.

| Family | Programming benefit | Best uses | Usually unnecessary for |
|---|---|---|---|
| **OpenAI Luna / nano / mini** | Fast and cost-efficient | Syntax questions, boilerplate, small edits, summaries, unit-test stubs | Architecture or ambiguous multi-file debugging |
| **OpenAI Codex** | Specialized for software engineering and agentic coding | Features, tests, debugging, refactors, reviews, repository tasks | Simple Q&A where a lightweight model is faster |
| **OpenAI Terra / general-purpose GPT** | Balanced coding, writing, reasoning, and tool use | Daily development, interactive coding, moderate agent tasks | Tiny repetitive edits |
| **OpenAI Sol / flagship reasoning GPT** | Careful multi-step reasoning and validation | Complex bugs, architecture, migrations, large codebases | Straightforward formatting or boilerplate |
| **OpenAI Astra** | Long-horizon autonomous planning and verification | Large features, broad refactors, sustained agent runs | Short interactive questions |
| **Claude Haiku** | Fast responses with reliable lightweight coding help | Explanations, small functions, quick edits, documentation | Deep architectural work |
| **Claude Sonnet** | Strong balance of coding quality, reasoning, and efficient tool use | General feature work, code review, refactoring, agent mode | Very small tasks when latency is the priority |
| **Claude Opus** | Sophisticated reasoning, debugging, and error recovery | Hard bugs, design trade-offs, complex multi-step implementations | Routine code generation |
| **Claude Fable** | Upfront planning and long-running autonomous work | Deep repository research, major features, complex workflows | Quick edits; review the supported-model page for data-handling notes |
| **Gemini Flash** | Low-latency coding help and rapid iteration | Lightweight questions, repetitive edits, prototyping | Long, difficult reasoning chains |
| **Microsoft MAI-Code Flash** | Fast code completion, explanation, instruction following, and tool use | General coding assistance and quick agent tasks | The hardest architecture or debugging problems |
| **Moonshot Kimi Code / Kimi K3** | Coding-focused answers; K3 emphasizes long context and multi-step agents | Repository exploration, large-context work, multi-file tasks | Small prompts that do not need long context |
| **xAI Grok** | General coding plus sophisticated reasoning; newer agentic variants handle multi-step workflows | Problem solving, agent tasks, alternate implementation approaches | Routine low-cost edits |
| **Qwen** | Code generation, reasoning, repair, and debugging where available | General coding and fixing localized defects | Tasks requiring Copilot features the selected deployment does not support |

### Current Copilot Agent Modes and Reasoning Effort

VS Code replaced the older **Ask / Edit / Agent** chat-mode picker with agent modes and custom agents. Names can differ between the **Copilot** and **Local** session targets.

| Mode, agent, or setting | Best for | Guidance |
|---|---|---|
| **Interactive** | Questions, explanations, focused edits, and normal implementation work | State whether the agent should only answer, propose a change, or edit files |
| **Plan** or `/plan` | Architecture, decomposition, and reviewing an approach before implementation | Use for ambiguous or high-risk work, then approve the plan or switch to Interactive |
| **Autopilot** *(when offered)* | Long-running implementation with fewer interruptions | Use only when the task and verification criteria are clear; review the approval level first |
| **Custom agent** | Repeatable roles such as code review, planning, testing, or framework-specific implementation | Select an agent from the agent picker; workspace agents use `.github/agents/*.agent.md` |
| **Low/fast reasoning** | Repetitive and deterministic work | Prefer for formatting, boilerplate, renames, and simple test generation |
| **Regular reasoning** | Most daily programming | Default choice for features, tests, reviews, and ordinary debugging |
| **High/extended reasoning** | Hard debugging, architecture, security, and migrations | Use only when deeper analysis is worth the added latency and cost |
| **Fast model mode** *(when offered)* | Getting the same model family's answer sooner | Improves latency, not task suitability; check live pricing because it may cost more |

Sources: [Plan work with agents in VS Code](https://code.visualstudio.com/docs/agents/run/planning) and [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents).

---

## Set Up GitHub Copilot

### Visual Studio Code

1. Update to the latest stable version of Visual Studio Code.
2. Hover over the **Copilot** icon in the status bar and select **Use AI Features**.
3. Choose a sign-in method and authenticate with the GitHub account that has your Copilot plan. An eligible account without a paid plan can enroll in Copilot Free.
4. Open Chat and select **Auto** or a specific model from the model picker.
5. Verify that Copilot is active by opening the Copilot status dashboard from the status bar. The dashboard also shows the percentage of your monthly allowance used.
6. Optionally run `/init` in Chat for a repository. Copilot analyzes the project and creates starter custom instructions so future requests need less exploratory context.

If Copilot is associated with a GitHub Enterprise account, select **Continue with GHE.com** during sign-in and enter the enterprise URL.

Source: [Set up GitHub Copilot in VS Code](https://code.visualstudio.com/docs/setup/copilot)

### Visual Studio

GitHub Copilot is supported in Visual Studio 2022 version 17.10 or later and current Visual Studio releases.

1. Launch **Visual Studio Installer**.
2. Find the Visual Studio installation and select **Modify**.
3. Select at least one workload, such as **.NET desktop development**.
4. Under **Optional** components, select **GitHub Copilot**.
5. Select **Modify** to install the component, then open Visual Studio.
6. Select the Copilot status icon in the upper-right corner and choose **Sign in to use Copilot**.
7. Sign in with the GitHub account that has Copilot access and verify that the status icon reports **Active**.

Source: [Manage GitHub Copilot installation and state in Visual Studio](https://learn.microsoft.com/visualstudio/ide/visual-studio-github-copilot-install-and-states)

### Prompt Cache Setup

GitHub Copilot and the selected model provider manage prompt caching automatically. Cache behavior, pricing, and retention depend on the model.

The VS Code team documents that it enabled extended prompt caching for supported OpenAI models by sending the `prompt_cache_retention` request-body parameter. Setting that provider parameter to `"24h"` keeps eligible cached prompt prefixes for up to 24 hours instead of the usual 5-10 minutes of inactivity. This happens automatically inside Copilot.

> "After careful evaluation, we enabled extended prompt caching for supported models through the `prompt_cache_retention` body parameter."
>
> Source: [Improving token efficiency for GitHub Copilot in VS Code — Extended prompt caching](https://code.visualstudio.com/blogs/2026/06/17/improving-token-efficiency-in-github-copilot#_extended-prompt-caching)

That article describes a parameter in Copilot's request to OpenAI, not a user-facing VS Code setting. The following configuration is **not documented by GitHub or VS Code**, and `prompt_cache_retention` is not present in the Copilot extension's published settings schema:

```json
"github.copilot.advanced": {
  "prompt_cache_retention": "24h"
}
```

VS Code may preserve the unknown property in `settings.json`, but that does not prove the extension sends it to the model provider. Treat it as unsupported and potentially ignored. No manual setting is needed because VS Code already enables extended retention for supported OpenAI models.

To preserve the automatic cache:

- Choose the model, reasoning level, context size, enabled tools, and MCP servers before starting a session.
- Keep the same model and settings for related turns. Switching them mid-session invalidates the existing cache.
- Prefer **Auto** model selection. Auto changes models at natural cache boundaries, such as a new session or after compaction, rather than on every turn.
- Keep related work in one active session, but start a new chat when switching to an unrelated problem.
- Do not revive a large, stale session solely to preserve context. OpenAI model caches expire after about 24 hours of inactivity; most other model caches expire after about one hour.
- In Copilot CLI, run `/compact` before continuing a long or stale session. Compaction is currently a CLI feature, not a VS Code or Visual Studio Chat command.

Source: [Optimizing your AI usage to maximize efficiency and reduce cost](https://docs.github.com/en/copilot/tutorials/optimize-ai-usage#4-preserve-the-cache)

---

## Token-Saving Techniques

Reduce credit consumption without sacrificing output quality.

- **Use Auto on paid plans:** Auto model selection receives a 10% model-cost discount in Copilot Chat, Copilot CLI, the GitHub Copilot app, and Copilot cloud agent.
- **Use regular reasoning by default:** Raise reasoning effort only for architecture, difficult debugging, and other tasks that benefit from deeper analysis.
- **Separate planning from execution:** Plan with a strong reasoning model, then start a focused implementation session with a cheaper execution model.
- **Use cheaper models for subagents:** A focused subagent starts with scoped context and often does not need the main session's expensive model.
- **Constrain the format upfront:** "Bullet list only. No intro or summary." Prose is expensive; structured output is short.
- **Cap response length:** "Answer in under 50 words." or "One paragraph max."
- **Name the relevant files:** Point Copilot to known files, errors, logs, and services so it does not spend tokens discovering them.
- **Avoid broad workspace context:** Attach only the files needed for the task instead of including an entire workspace by default.
- **Close unrelated editor tabs:** Open tabs can contribute context, depending on the active feature and client.
- **Right-size the model:** Default to lightweight. Step up only when output quality is insufficient.
- **Batch related questions:** One prompt with three questions costs less than three separate prompts.
- **Start a new chat for a new problem:** Long conversations resend their history on later requests.
- **Keep custom instructions short:** Store stable repository conventions, commands, and known pitfalls in `.github/copilot-instructions.md`; remove generic or one-off guidance.
- **Enable only relevant tools:** Large MCP and tool sets add schemas to the context. Use focused toolsets when possible.
- **Skip confirmation steps for routine tasks:** Remove "restate my question" or "ask clarifying questions" from everyday prompts — reserve them for high-stakes work only.
- **Ground cheaply:** "Answer only based on the information I provide. If unsure, say so." achieves reliable grounding without verbose instructions.
- **Prefer `Auto` model selection:** Copilot's automatic selection balances capability and cost; override only when you have a specific reason.
- **Add deterministic guardrails:** Tests, linters, and security scans cost some tokens up front but prevent expensive chains of incorrect edits and retries.
- **Monitor actual usage:** In VS Code, open the Copilot status dashboard. For account-wide details, review the [GitHub AI usage page](https://github.com/settings/billing).

### Cost-Efficient Prompt Template

```
Task: [specific change]
Scope: [files, services, or components]
Context: [known error, constraints, and relevant facts]
Output: [exact format or implementation requirement]
Done when: [measurable stopping condition]
Do not: [unrelated work to avoid]
```

This structure adds a small amount of input but reduces exploration, retries, scope drift, and unnecessary output.

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

**Model:** Any lightweight/fast family, such as Luna, mini, Haiku, Gemini Flash, or MAI-Code Flash.

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

**Model:** Any lightweight/fast family, such as Luna, mini, Haiku, Gemini Flash, or MAI-Code Flash.

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

**Model:** A balanced or deep-reasoning family, such as Claude Sonnet/Opus or OpenAI Sol/flagship GPT — depth is the point here.

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

**Model:** Use a powerful agentic family, such as Claude Sonnet/Opus/Fable, OpenAI Sol/Astra, Kimi K3, or the current equivalent. These tasks justify the cost; a lightweight model may produce shallower synthesis.

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
