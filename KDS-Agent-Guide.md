# KDS Compliance Agent — Usage Guide

Use the **KDS Evaluator** agent in GitHub Copilot to audit and fix PA.gov screens against the Keystone Design System.

---

## Prerequisites

The following files must be present in the workspace:

| File | Purpose |
|---|---|
| `.github/instructions/kds-instructions.md` | KDS rules — loaded automatically by Copilot as an instruction file |
| `.github/prompts/kds-evaluator.prompt.md` | The agent prompt — invoked manually (see below) |

Both files are already in this repo. No installation required.

---

## How to invoke the agent

1. Open **Copilot Chat** in VS Code (`Ctrl+Alt+I`)
2. Set the mode to **Agent** (dropdown at the bottom of the chat panel)
3. Type:

```
/kds-evaluator
```

Or use the full invoke path:

```
Run the KDS Compliance Evaluator on [describe what to audit, e.g., "all files in src/screens/"].
```

**Model recommendation:** Use **Claude Sonnet 4.x** or **Gemini 3.1 Pro** — the agent reads multiple files and reasons across them, which benefits from a versatile model.

---

## What the agent does

The agent runs in two phases.

### Phase 1 — Orientation

Before scanning, the agent asks you five questions:

1. What is the application? (public-facing, internal tool, form-heavy workflow, etc.)
2. What technology stack? (HTML/CSS, React, Blazor, Razor Pages, etc.)
3. Are KDS CSS tokens and the KDS stylesheet already imported?
4. Who is the target audience?
5. Is a Figma/Storybook file available?

Answer these directly in the chat. The agent confirms its understanding before proceeding.

### Phase 2 — Full Audit

The agent scans all `.html`, `.cshtml`, `.razor`, `.jsx`, `.tsx`, `.vue`, `.css`, `.scss`, `.ts`, `.js` files in scope and checks every item across six categories:

| Category | What it checks |
|---|---|
| **Structure & Layout** | Header/footer present, no layout tables, mobile-first breakpoints |
| **Typography & Color** | No hardcoded hex/px values, correct typefaces, sequential headings |
| **Links & Buttons** | Descriptive text, correct element semantics, one Primary per section |
| **Forms** | Labels, help text, error states, fieldset/legend, `aria-describedby` |
| **Images & Icons** | Alt text, `aria-hidden` on decorative icons, `aria-label` on icon buttons |
| **Alerts** | Correct scope (Global vs In-Page), correct variant, `role="alert"` |

Each finding is reported as:

```
[SEVERITY] CATEGORY > Finding
File: path/to/file.html  Line: XX
Current code: <snippet>
KDS rule violated: <rule summary>
```

**Severity levels:**

| Level | Meaning |
|---|---|
| CRITICAL | Breaks WCAG AA, removes required structure, causes screen reader failure |
| HIGH | Violates a hard KDS rule (hardcoded colors, missing labels, wrong semantics) |
| MEDIUM | Violates a guideline where a valid alternative exists — agent will discuss trade-offs |
| LOW | Style, tone, wording (plain language, heading capitalisation, missing PDF indicator) |

### Phase 3 — Remediation

After the audit, the agent:
1. Groups findings by category and asks for your approval before fixing each group
2. Presents pros and cons for MEDIUM findings where multiple valid approaches exist
3. Applies approved fixes directly to the files
4. Reports what was changed per file

---

## Scope examples

**Single file (open in editor):**
```
Run the KDS evaluator on the open file.
```

**Specific folder:**
```
Run the KDS evaluator on all files in src/screens/permits/.
```

**Audit only, no changes:**
```
Run the KDS evaluator on src/screens/. Report findings only — do not make any changes.
```

**Single category:**
```
Run the KDS evaluator on the open file, checking accessibility only.
```

---

## Tips

- **Audit before building** — Run the evaluator on a new screen before wiring up backend logic. Structural fixes are cheaper early.
- **Use audit-only mode first** — Get the full findings list before approving fixes. You may want to handle some manually.
- **One folder at a time** — For large feature sets, scope the agent to one folder per run rather than the entire project. Keeps the output manageable.
- **CRITICAL and HIGH first** — Address these before MEDIUM and LOW. Accessibility failures block launch.
- **Check the instructions file** — If the agent produces unexpected output, verify `.github/instructions/kds-instructions.md` is present and Copilot instructions are enabled in VS Code settings (`github.copilot.chat.codeGeneration.useInstructionFiles: true`).

---

## Reference

- **KDS Authoring Guide:** https://wcmauthorguide.pa.gov/en/keystone-design-system/
- **Remix Icons catalog:** https://wcmauthorguide.pa.gov/en/style-guide/icons.html
- **Prompt templates for manual use:** see [Prompt Guide.md](./Prompt%20Guide.md) → KDS section
