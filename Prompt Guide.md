# Prompts Guide

A collection of effective prompts and prompting strategies to get the best results from LLMs.

---

## Avoiding LLM Confusion — General Best Practices

Use these prompts to keep the model focused and reduce hallucination or drift.

- **Set the role upfront:** "You are a senior software engineer specialising in C#. Answer only within that context."
- **Constrain scope:** "Answer only based on the information I provide. Do not use outside knowledge."
- **Prevent over-answering:** "Give me a concise answer. No preamble, no summary at the end."
- **Clarify first:** "Before providing any code or solution, carefully review my instructions and ask any clarifying questions necessary to fully understand the problem and my requirements. Do not proceed with a solution until you have confirmed your understanding with me. Once you have asked your questions and I have answered, summarize your understanding of the problem and your proposed approach. Only after I confirm that your understanding and approach are correct, proceed to provide the solution. After presenting the solution, ask me to review and confirm before finalizing or implementing any changes."
- **Check comprehension:** "Restate my question in your own words before answering so I can confirm you understood it correctly."
- **Prevent scope creep:** "Only change what I explicitly ask. Do not refactor, rename, or improve anything else."
- **Validate then execute (end-to-end):** "Before you begin, summarise exactly what you are going to do and why. List each step you plan to take. Wait for my confirmation. Once I confirm, carry out every step completely — do not stop partway through, do not ask for permission at each step, and do not leave anything for me to finish. Deliver the full completed result."

---

## One-Shot Prompting

Provide a single example of the format or behaviour you want before your real request. The model mirrors the pattern.

**When to use:** You want a specific output format, tone, or structure and one example is enough to demonstrate it.

**Template:**
```
Here is an example of the output I want:

[Your example here]

Now do the same for: [Your actual request]
```

**Example:**
```
Here is an example of a user story in the format I want:
"As a customer, I want to reset my password so that I can regain access to my account."

Now write a user story for: A user uploading a profile photo.
```

---

## Few-Shot Prompting

Provide two or more examples before your request to establish a stronger pattern. Ask the model to confirm it understands the pattern before it applies it.

**When to use:** The output structure is nuanced or the model needs more than one example to infer the rule.

**Template:**
```
Here are some examples of the pattern I want you to follow:

Example 1: [input] → [output]
Example 2: [input] → [output]
Example 3: [input] → [output]

Before you apply this pattern, explain the pattern back to me in your own words so I can confirm you have understood it correctly.

Once I confirm, apply the pattern to: [Your actual request]
```

**Example:**
```
Here are some examples of the tone and format I want for error messages:

Example 1: File not found → "We couldn't find that file. Check the name and try again."
Example 2: Network timeout → "The connection timed out. Please check your internet and retry."
Example 3: Invalid input → "That value doesn't look right. Please enter a number between 1 and 100."

Before you apply this pattern, explain the pattern back to me in your own words.

Once I confirm, write an error message for: The user's session has expired.
```

---

## Chain-of-Thought Reasoning

Ask the model to think step by step and show its reasoning at each stage. Use this to rank, prioritise, or diagnose complex problems.

**When to use:** Ranking trade-offs, root cause analysis, architecture decisions, prioritisation exercises — anywhere the reasoning matters as much as the answer.

**Template:**
```
List the top [X] [things] for [context].
For each one, tell me:
1. Why you think it belongs in the top [X]
2. How significant the impact is and why
3. A suggested way to address it

Think step by step. Show me your thinking for each item before moving to the next.
```

**Example — code review:**
```
List the top 5 risks in this codebase for a production deployment.
For each one, tell me:
1. Why you think it is a significant risk
2. The likely impact if it materialises
3. A concrete step to mitigate it

Think step by step. Show me your reasoning for each risk before moving to the next.
```

**Example — learning a topic:**
```
List the top 3 things a developer must understand before using async/await in C#.
For each one:
1. Explain why this concept is essential
2. Describe the mistake developers commonly make without this knowledge
3. Give a one-sentence rule of thumb to remember

Think step by step and show me your reasoning for each item.
```

---

## Agentic / Deep Research Prompting

Use this when you want the model to act autonomously across multiple sources or reasoning steps — research, synthesis, and structured output in one prompt.

**When to use:** Competitive analysis, trend research, technology evaluation, strategic summaries.

**Template:**
```
Do deep research on [TOPIC].
Analyse and cross-reference all the major trends, sources, and perspectives you can identify.
Find the [X] most important insights or trends.
For each one, explain why it is significant and how it connects to the others.
Then draft a one-page executive summary covering all [X] insights, written for [AUDIENCE].
```

**Example:**
```
Do deep research on the current state of AI adoption in enterprise software development.
Analyse and cross-reference all the major trends, analyst reports, and community signals you can identify.
Find the three most important trends shaping this space right now.
For each trend, explain why it is significant and how it connects to the others.
Then draft a one-page executive summary covering all three trends, written for a non-technical leadership audience.
```

---

## The DRAG Framework

DRAG is a structured prompting framework that ensures the model has everything it needs to give a high-quality, grounded response.

| Letter | Stands for | What to include |
|--------|------------|-----------------|
| **D** | **Direction** | The role, persona, or expertise the model should adopt |
| **R** | **Request** | The specific task or question you are asking |
| **A** | **Action** | The format, structure, or style of the output |
| **G** | **Goal** | The purpose — why you need this and what success looks like |

**Template:**
```
Direction: You are [role/persona with relevant expertise].
Request: [Specific task or question].
Action: Respond as [format — bullet list / step-by-step guide / table / one-page summary / etc.].
Goal: The output will be used to [purpose]. Success looks like [criteria].
```

**Example:**
```
Direction: You are a senior cloud architect with 10 years of experience designing Azure solutions for regulated industries.
Request: Review the following architecture diagram description and identify the three biggest security risks.
Action: Present your findings as a numbered list. For each risk, include: the risk, the potential impact, and one recommended mitigation.
Goal: The output will be presented to a security review board. Success means each risk is clearly explained so a non-technical stakeholder can understand it.
```

**Why DRAG works:** By separating direction, request, action, and goal you eliminate the most common causes of vague or off-target responses — the model knows *who it is*, *what you want*, *how to present it*, and *why it matters*.


