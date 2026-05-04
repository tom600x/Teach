# Prompting Techniques: MVC Calculator Examples

## Zero-Shot
No examples or context provided — just the raw request.

> "Create an ASP.NET MVC controller for a calculator that adds two numbers."

Copilot must infer everything: naming, structure, patterns, return types.

---

## One-Shot
You provide **one example** to establish the pattern you want.

> "Here's how my HomeController is structured:
> ```csharp
> public IActionResult Index() => View();
> ```
> Following that pattern, create a `CalculatorController` with an `Add(int a, int b)` action that passes the result to a view."

Now Copilot understands your naming style, return type preference, and view-centric pattern.

---

## Few-Shot (Multi-Shot)
You provide **multiple examples** to establish richer patterns.

> "Here are examples of my existing actions:
> ```csharp
> // GET: /Calculator/Add
> public IActionResult Add(int a, int b) {
>     ViewBag.Result = a + b;
>     ViewBag.Operation = "Addition";
>     return View("Result");
> }
>
> // GET: /Calculator/Subtract
> public IActionResult Subtract(int a, int b) {
>     ViewBag.Result = a - b;
>     ViewBag.Operation = "Subtraction";
>     return View("Result");
> }
> ```
> Following the same pattern with `ViewBag.Result` and `ViewBag.Operation`, add `Multiply` and `Divide` actions. For Divide, handle division by zero."

Now Copilot matches your exact naming convention, `ViewBag` usage, shared view name, and knows to add domain-specific error handling.

---

## Key Teaching Points

| Technique | Context Given | Output Quality | Use When |
|---|---|---|---|
| Zero-shot | None | Generic | Quick scaffolding |
| One-shot | 1 example | Matches one pattern | You have a style to follow |
| Few-shot | 2+ examples | Highly consistent | Establishing a convention across many files |

The more examples you give, the more Copilot can infer **your** conventions vs. generic defaults — especially useful in Lab 02 (Chat Mode) and Lab 03 (Agent Mode) where richer context is available.
