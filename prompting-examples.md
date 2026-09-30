# Prompting Techniques: Current Copilot Guidance

## Are One-Shot and Few-Shot Prompts Still Useful?

Yes, but use them selectively. Current Copilot models can infer common coding patterns from clear instructions and repository context. Examples remain useful when the required output format, transformation, naming convention, or edge-case behavior is difficult to describe precisely.

Prefer this order:

1. Give a clear task, scope, constraints, and definition of done.
2. Reference an existing file or symbol that already demonstrates the pattern.
3. Provide one example only when the pattern is not available in the repository.
4. Provide multiple examples only when one example leaves important ambiguity.

Do not paste large examples that Copilot can already read from the workspace. Repeated examples increase input tokens and can distract from the task.

---

## Zero-Shot

Zero-shot means **no examples**, not no context. Include requirements and acceptance criteria.

> Create an ASP.NET Core MVC `CalculatorController` with an `Add(decimal a, decimal b)` action. Return the result view with a strongly typed `CalculationResult` model. Follow the repository's controller conventions. Do not modify unrelated files.

**Use when:** The task follows common patterns or the repository already provides enough context.

---

## Repository-Grounded Prompt

For coding tasks, referencing existing code is usually more effective and cheaper than writing a synthetic one-shot example.

> Add `Multiply` and `Divide` actions to `CalculatorController`. Match the structure, validation, result model, and error handling used by the existing `Add` and `Subtract` actions. For division by zero, add a model validation error and return the input view. Change only the controller and its tests.

**Use when:** The desired pattern already exists in the codebase.

---

## One-Shot

Provide one compact example when Copilot cannot access the source pattern or when the exact output shape matters.

> Use this response shape:
>
> ```json
> {"operation":"add","result":5,"error":null}
> ```
>
> Return the equivalent JSON for `divide(10, 2)`. Output JSON only.

**Use when:** One example fully establishes the required schema, style, or transformation.

**Avoid when:** The example merely repeats requirements that are simpler to state directly.

---

## Few-Shot

Provide two or three short examples when the model must infer a mapping or distinguish edge cases.

> Follow these mappings:
>
> ```text
> add(2, 3)       -> {"operation":"add","result":5,"error":null}
> divide(10, 2)   -> {"operation":"divide","result":5,"error":null}
> divide(10, 0)   -> {"operation":"divide","result":null,"error":"Division by zero"}
> ```
>
> Produce the result for `multiply(4, 6)`. Output JSON only.

**Use when:** Multiple examples are necessary to reveal a rule, exception, classification boundary, or exact formatting convention.

**Avoid when:** Examples are long, redundant, inconsistent, or available in repository files.

---

## Decision Guide

| Approach | Best use | Token cost | Current recommendation |
|---|---|---:|---|
| Zero-shot | Common, well-scoped tasks | Lowest | Default starting point |
| Repository-grounded | Matching existing project code | Low | Preferred for coding tasks |
| One-shot | Exact format or pattern unavailable in the repository | Medium | Use only when it removes ambiguity |
| Few-shot | Rules with meaningful variations or edge cases | Highest | Use the minimum examples needed |

## Cost-Efficient Prompt Pattern

```text
Task: [specific change]
Pattern: Follow [file or symbol]
Constraints: [behavior and boundaries]
Output: [required format]
Done when: [measurable result]
```

Keep examples at the end of the prompt so stable instructions and context remain easy to reuse. Remove examples after the pattern has been captured in repository code or custom instructions.
