# GitHub Copilot Models Guide

_For use in slide deck / class instruction_  
Updated from official GitHub Docs: <https://docs.github.com/en/copilot/reference/ai-models/supported-models>

---

## What is a model?

Think of models like different expert consultants you can call on demand.

The GitHub Copilot interface stays the same — the AI brain behind it changes.

- Some models are **unlimited** (`0x` = no premium request cost).
- Others consume premium requests at different rates (`0.25x`, `0.33x`, `1x`, `3x`).
- You switch models in the model picker inside Chat or Agent mode.

## What is "Auto" mode?

- Copilot automatically picks the best available model for your task.
- Gives you a **10% discount** on premium request usage.
- Good default when you are not sure which model to pick.
- You can override Auto and choose a specific model at any time.

---

## Tier 1 — Unlimited models (`0x` multiplier)

These models consume **zero premium requests**. Use them freely.

### GPT-4.1 (OpenAI)

- The speed champion — very fast responses with low latency.
- Great for inline completions, quick code generation, and boilerplate.
- Best for short focused tasks: write a function, fix a typo, generate a snippet.
- Works well across all major languages and frameworks.
- Works great as your everyday starting model before reaching for something heavier.

- **Multiplier:** `0x` (unlimited)
- **Best for:** Speed, everyday coding, quick completions

### GPT-4o (OpenAI)

- Classic fast general-purpose model, also at `0x` — nothing to lose by trying it.
- Good for conversational code questions and quick explanations.
- Works well for writing functions and small code blocks.
- Available across all Copilot clients and plans.
- A safe fallback when other models are unavailable.

- **Multiplier:** `0x` (unlimited)
- **Best for:** Fast explanations, code Q&A, lightweight tasks

### GPT-5 mini (OpenAI) _(labeled "Medium" quality)_

- Reliable default for most coding and writing tasks.
- Fast and accurate — works well across languages and frameworks.
- Good for generating documentation, comments, and summaries.
- Handles errors and quick debugging questions well.
- Available on all Copilot plans including Free.

- **Multiplier:** `0x` (unlimited)
- **Best for:** Everyday general coding, documentation, quick debugging

---

## Tier 2 — Low-cost models (`0.25x–0.33x` multiplier)

These consume a fraction of a premium request and are very cost-efficient.

### Grok Code Fast 1 (xAI)

- Specialized specifically for coding tasks.
- Performs well on code generation and debugging across multiple languages.
- Fast, accurate code completions and explanations.
- Good alternative to GPT models for coding-focused workflows.
- Available across most Copilot clients.

- **Multiplier:** `0.25x` (very low cost)
- **Best for:** Code generation, multi-language debugging, coding-focused chat

### Claude Haiku 4.5 (Anthropic)

- Anthropic's fastest and lightest model — designed for quick repeated tasks.
- Best for fast, reliable answers to lightweight coding questions.
- Great when you need many quick answers without burning through premium requests.
- Good for code explanations, small refactors, and simple Q&A.
- Available across all Copilot clients and plans.

- **Multiplier:** `0.33x` (low cost)
- **Best for:** Fast lightweight help, high-volume Q&A, quick code explanations

### Gemini 3 Flash (Google) _(Preview)_

- Google's fast lightweight model — optimized for speed.
- Best for fast, reliable answers to lightweight coding questions.
- Good at quick code generation and iteration.
- Preview status — behavior may change; great for experimenting.
- Available on most clients (not Copilot CLI).

- **Multiplier:** `0.33x` (low cost)
- **Best for:** Fast lightweight help, quick code generation

### GPT-5.4 mini (OpenAI) _(labeled "Medium" quality)_

- Designed for agentic software development workflows.
- Especially effective at codebase exploration using grep-style tools.
- Good at navigating large codebases and finding relevant code sections.
- Cost-efficient choice when running Agent mode tasks.
- Works well for reading and summarizing code across files.

- **Multiplier:** `0.33x` (low cost)
- **Best for:** Agent mode codebase exploration, file navigation tasks

---

## Tier 3 — Standard premium models (`1x` multiplier)

These cost one premium request per use and are the workhorse tier for most serious work.

### Claude Sonnet 4.5 (Anthropic)

- General-purpose coding and agent-task model — versatile workhorse.
- Strong complex problem-solving and sophisticated reasoning.
- Well-balanced between speed and capability.
- Great for Ask mode and Edit mode workflows.
- Works across all Copilot clients.

- **Multiplier:** `1x`
- **Best for:** General coding, agent tasks, balanced reasoning

### Claude Sonnet 4.6 (Anthropic) _(High quality rating)_

- Latest Claude Sonnet with elevated quality for coding and agent workflows.
- Strong at complex problem-solving and sophisticated reasoning.
- Best for Ask mode conversations where you need explanations and reasoning.
- Good for refactoring, code reviews, and architecture discussions.
- Available on GitHub.com, Copilot CLI, VS Code, and Visual Studio.

- **Multiplier:** `1x` _(subject to change per GitHub Docs)_
- **Best for:** High-quality chat, refactoring, code review, agent workflows

### Gemini 2.5 Pro (Google)

- Google's flagship reasoning model for deep work.
- Best for complex code generation, debugging, and research workflows.
- Handles multi-file context well and understands dependencies.
- Strong at code analysis and test generation for large projects.
- Available on GitHub.com, VS Code, Visual Studio, JetBrains, and Xcode.

- **Multiplier:** `1x`
- **Best for:** Deep debugging, complex code generation, research workflows

### Gemini 3.1 Pro (Google) _(Preview)_

- Optimized specifically for edit-then-test development loops.
- High tool precision — works well with Agent mode tool calls.
- Best for iterative coding workflows (write, run, fix, repeat).
- Good at test generation and validation tasks.
- Preview status — strong candidate for advanced Agent mode work.

- **Multiplier:** `1x`
- **Best for:** Edit-test loops, agentic workflows, high-precision tool use

### GPT-5.2 (OpenAI)

- Deep reasoning model for multi-step problem solving.
- Strong for architecture-level code analysis and system design questions.
- Best for hard debugging problems that require reasoning across a codebase.
- Handles large technical questions with nuance and accuracy.
- Successor to o3 for reasoning tasks.

- **Multiplier:** `1x`
- **Best for:** Deep reasoning, hard bugs, architecture analysis

### GPT-5.2-Codex (OpenAI)

- Built specifically for agentic software development tasks.
- Strong at executing multi-step coding workflows in Agent mode.
- Best for implementing features, writing tests, and refactoring in sequence.
- Good at following complex multi-part instructions.
- Use when you want Copilot to work like a developer, not just answer questions.

- **Multiplier:** `1x`
- **Best for:** Agentic development, multi-step feature implementation

### GPT-5.3-Codex (OpenAI) _(GitHub's top recommendation for general coding)_

- Delivers higher-quality code on complex engineering tasks.
- Handles features, tests, debugging, refactors, and reviews without lengthy prompts.
- Recommended by GitHub as the top general-purpose coding model.
- No need for long detailed prompts — understands intent naturally.
- Successor to GPT-5.1-Codex (which retired April 2026).

- **Multiplier:** `1x`
- **Best for:** Complex engineering, test generation, refactoring, code review

### GPT-5.4 (OpenAI) _(labeled "Medium" quality)_

- Advanced reasoning model with deep problem-solving capability.
- Strong for multi-step problem solving and architecture-level code analysis.
- Great for tackling hard logic problems or debugging complex systems.
- Combines reasoning with strong code generation quality.
- Available on Pro, Pro+, Business, and Enterprise plans.

- **Multiplier:** `1x`
- **Best for:** Hard reasoning, complex debugging, architecture decisions

---

## Tier 4 — High-cost models (`3x` multiplier)

These cost three premium requests per use. Reserve them for the hardest problems.

### Claude Opus 4.5 (Anthropic)

- Anthropic's most capable model for complex problem-solving.
- Exceptional at sophisticated reasoning across long conversations.
- Best for architecture design, security analysis, and system-level thinking.
- Handles ambiguous or highly complex requirements better than Sonnet.
- Slower than Sonnet — the tradeoff is depth and accuracy.

- **Multiplier:** `3x` (high cost — use for genuinely hard problems)
- **Best for:** Hardest bugs, architecture, security review, complex agent plans

### Claude Opus 4.6 (Anthropic) _(High quality rating)_

- Latest and most capable Claude model in Copilot.
- Strong at complex problem-solving with sophisticated multi-step reasoning.
- Best for Agent mode tasks requiring deep understanding of large codebases.
- Ideal for long-context refactoring, design docs, and compliance reviews.
- Available on all clients across all paid Copilot plans.

- **Multiplier:** `3x` (high cost — use for genuinely hard problems)
- **Best for:** Most complex tasks, deep Agent workflows, large codebase reasoning

---

## Quick decision guide (for the slide deck)

| Task | Recommended model | Cost |
|---|---|---|
| Quick code completion / boilerplate | GPT-4.1 or GPT-5 mini | FREE |
| Everyday coding questions | GPT-5.3-Codex | `1x` |
| Fast lightweight help, many small tasks | Claude Haiku 4.5 | `0.33x` |
| Codebase exploration in Agent mode | GPT-5.4 mini | `0.33x` |
| Refactoring and code explanation | Claude Sonnet 4.6 | `1x` |
| Deep debugging / reasoning | GPT-5.4 or Gemini 2.5 Pro | `1x` |
| Agentic multi-step development | GPT-5.2-Codex or GPT-5.3-Codex | `1x` |
| Edit-then-test iterative loops | Gemini 3.1 Pro | `1x` |
| Architecture + hardest problems | Claude Opus 4.6 | `3x` |
| Not sure what to pick | Auto (10% discount) | Varies |

---

## Rule of thumb for beginners

1. Start with **Auto** — it picks a good model and costs 10% less.
2. Use **GPT-4.1** or **GPT-5 mini** for everyday unlimited free tasks.
3. Switch to **GPT-5.3-Codex** for serious coding work (`1x`).
4. Use **Claude Sonnet 4.6** when you need explanation, reasoning, or refactoring.
5. Only reach for **Opus** (`3x`) when the problem is genuinely hard.

---

## Note on retiring models (as of April 2026)

- GPT-5.1 retires April 15, 2026 — switch to GPT-5.3-Codex.
- Claude Sonnet 4 has a deprecation warning — move to Claude Sonnet 4.5 or 4.6.
- Goldeneye and Claude Opus 4.6 (1M context) are internal only, not for general use.
