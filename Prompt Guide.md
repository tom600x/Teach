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

---

## KDS (Keystone Design System) Prompts

Use these prompts in **GitHub Copilot Chat** or **agent mode** when building or updating PA.gov screens. All prompts assume the `kds-instructions.md` instruction file is active in the workspace.

---

### New Screen Generation

**Generate a new data entry form:**
```
Build a KDS-compliant data entry form for [describe the form's purpose, e.g., "submitting a new permit application"].
Include the following fields: [list fields with types, e.g., "Applicant name (text), County (drop-down), Submission date (date), Notes (textarea)"].
Mark required fields with an asterisk and a note above the form.
Group related fields under fieldset/legend elements.
Add a Submit (Primary button) and Cancel (Secondary button) in the form footer.
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a data table with CRUD actions:**
```
Build a KDS-compliant data table for [describe the record type, e.g., "permit applications"].
Include columns for: [list columns, e.g., "Application ID, Applicant name, County, Status, Date submitted, Actions"].
The Actions column should contain Ghost buttons for View, Edit, and Delete.
Add a toolbar above the table with a search input, a Status filter drop-down, an "Add [record type]" Primary button, and a "Rows per page" drop-down (10/25/50).
Include pagination controls below the table showing current page, total pages, and a record count ("Showing X–Y of Z results").
Show an empty state message when there are no records.
Use KDS Tag (read-only) in the Status column.
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a record detail / view screen:**
```
Build a KDS-compliant record detail screen for [record type].
Display the following fields as a definition list (dl/dt/dd): [list fields].
Show the record status as a KDS Tag (read-only) near the page H1.
Place a Secondary button ("Edit") and a Ghost button ("Back to list") at the bottom of the page.
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a workflow action screen:**
```
Build a KDS-compliant workflow action screen for [describe the workflow step, e.g., "reviewing a submitted permit application"].
Display the record fields read-only using a definition list.
Show the current status as a KDS Tag near the H1.
At the bottom, provide workflow action buttons: [list actions, e.g., "Approve (Primary), Return for Correction (Secondary), Reject (Ghost)"].
Rejecting must trigger a confirmation step using a KDS In-Page Alert (error variant) with Confirm and Cancel buttons.
Follow all KDS component rules and accessibility requirements from the instructions file.
```

---

### Audit and Update Existing Screens

Use these prompts when you have an existing screen open in the editor and want Copilot to review or update it.

**Full KDS compliance audit (chat window — open file first):**
```
Audit the open file against the KDS instructions.
Check every component, color, typography class, button variant, form label, accessibility attribute, and icon usage.
List every violation found, grouped by category (Structure, Typography, Color, Buttons, Forms, Icons, Accessibility, Alerts).
For each violation, state: what is wrong, which KDS rule it breaks, and the exact fix required.
Do not make any changes yet — just report findings.
```

**Apply all KDS violations found in an audit:**
```
Apply every fix from the audit you just completed to the open file.
Change only what the audit identified. Do not refactor, rename variables, or restructure anything beyond the KDS violations.
After completing all fixes, list what was changed.
```

**Update buttons to KDS:**
```
Review all buttons in the open file and update them to use the correct KDS Button variants.
Rules: one Primary button per section (main action), Secondary for cancel/back, Ghost for low-emphasis and destructive actions.
Never use a Primary button for a destructive action.
Pair every icon button with an aria-label.
Report what was changed.
```

**Update form fields to KDS:**
```
Review all form fields in the open file and update them to comply with KDS Text Input, Drop-Down Select, Checkbox, and Radio Button rules.
Ensure: every field has a visible label element, placeholder text is not the only source of guidance, help text uses aria-describedby, error states use the KDS error variant with aria-invalid="true".
Report what was changed.
```

**Update typography to KDS:**
```
Review all text in the open file and update it to use the correct KDS typography CSS classes.
Use Plus Jakarta Sans variable font. Apply the correct scale classes for headings (H1–H6), body text, labels, and captions.
Do not use hardcoded font sizes, weights, or line heights — use KDS tokens only.
Report what was changed.
```

**Update colors to KDS tokens:**
```
Review all color values (hex, rgb, hardcoded Tailwind classes, custom CSS variables) in the open file.
Replace them with the appropriate KDS Material Design 3 color tokens (e.g., --md-sys-color-primary, --md-sys-color-surface, --md-sys-color-on-surface).
Do not introduce any color value that is not a KDS token.
Report what was changed.
```

**Update icons to KDS / Remix Icons:**
```
Review all icons in the open file.
Replace any non-Remix Icon classes with the equivalent ri-* class from the PA.gov icon catalog.
Ensure decorative icons have aria-hidden="true". Ensure interactive icon buttons have aria-label set.
Pair every icon with visible label text unless it is in a space-constrained context, in which case confirm aria-label is present.
Report what was changed.
```

**Add accessibility attributes to the open file:**
```
Review the open file for accessibility gaps against WCAG 2.1 AA and KDS requirements.
Check: all images have alt text, all form fields have labels and aria-describedby where needed, all interactive elements are keyboard-reachable, all icon buttons have aria-label, dynamic regions use aria-live or role="alert", all tables have captions and proper th scope attributes.
Fix every gap found. Report what was changed.
```

---

### Agent Mode Prompts

Use these in **agent mode** (where Copilot can read and write multiple files) for larger tasks.

**Audit all screens in a folder for KDS compliance:**
```
Audit every HTML/template file in [folder path] against the KDS instructions.
For each file, list all violations grouped by category (Structure, Typography, Color, Buttons, Forms, Icons, Accessibility, Alerts).
Output a summary table at the end: file name | violation count | highest-severity issue.
Do not make any changes — reporting only.
```

**Upgrade an entire feature to KDS:**
```
Update all files in [folder path] to be fully KDS-compliant.
Work through each file systematically: fix buttons, form fields, typography, colors, icons, and accessibility attributes.
After each file, confirm what was changed.
Only change what is required for KDS compliance. Do not refactor logic, rename variables, or restructure components.
```

**Generate a complete CRUD screen set for a new entity:**
```
Generate a full KDS-compliant CRUD screen set for [entity name] with the following fields: [list fields with types].
Create four files:
1. list.html — data table with toolbar (search, filters, Add button, rows-per-page), pagination, status tags, and View/Edit/Delete Ghost buttons per row.
2. add.html — data entry form with fieldset grouping, required field marking, Submit and Cancel buttons.
3. edit.html — same form as add.html pre-populated with record data, with Save and Cancel buttons.
4. view.html — read-only definition list layout with status tag, Edit and Back buttons.
All files must follow KDS component rules, accessibility requirements, and data application UI patterns from the instructions file.
```

**Update all tables to use CRUD actions and pagination:**
```
Review every data table in all files in [folder path] and update them to follow the KDS data table pattern.
For each table:
1. Add an Actions column as the last column with Ghost buttons for View, Edit, and Delete.
2. Add a toolbar above the table with a search input, relevant filter drop-downs, an "Add [record type]" Primary button, and a "Rows per page" drop-down (options: 10, 25, 50).
3. Add pagination controls below the table showing Previous and Next buttons, current page number, total page count, and a record count ("Showing X–Y of Z results").
4. Add an empty state message displayed when the table has no rows.
5. Ensure the table has a caption element, all header cells use th with the correct scope attribute, and status values use KDS Tag (read-only).
Only change table markup and surrounding controls. Do not alter non-table content, form fields, or page layout.
After completing all files, list each file updated and summarize what was added.
```

**Consistency check across screens:**
```
Review all files in [folder path] and check for consistency across screens.
Verify: the same status values and Tag colors are used everywhere, button labels for the same action are identical across pages, form field labels for the same data are identical, pagination controls use the same pattern on every list screen.
List every inconsistency found with the file name, line reference, and recommended fix.
```



