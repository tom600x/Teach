# KDS Prompt Guide

A standalone guide for KDS-specific prompts used in GitHub Copilot Chat and agent mode when building or updating PA.gov screens.

This guide complements the main prompt guide and assumes the KDS instruction file is active in the workspace.

---

## KDS (Keystone Design System) Prompts

Use these prompts in GitHub Copilot Chat or agent mode when building or updating PA.gov screens. All prompts assume the `kds-instructions.md` instruction file is active in the workspace.

**Model recommendation:** Use a versatile model (Claude Sonnet 4.x, Gemini 3.1 Pro) for full screen generation. Use a lightweight model (GPT-5 mini, MAI-Code-1-Flash) for targeted audits and single-component updates.

---

### New Screen Generation

**Generate a new data entry form:**
```
Build a KDS-compliant data entry form for [purpose].
Fields: [list with types, e.g., "Applicant name (text), County (drop-down), Submission date (date), Notes (textarea)"]
Required fields: mark with asterisk and note above form.
Group related fields under fieldset/legend.
Footer: Submit (Primary), Cancel (Secondary).
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a data table with CRUD actions:**
```
Build a KDS-compliant data table for [record type].
Columns: [list, e.g., "Application ID, Applicant name, County, Status, Date submitted, Actions"].
Actions column: Ghost buttons for View, Edit, Delete.
Toolbar: search input, Status filter drop-down, "Add [record type]" Primary button, Rows per page (10/25/50).
Pagination: current page, total pages, record count ("Showing X–Y of Z results").
Empty state message when no records. Status column: KDS Tag (read-only).
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a record detail / view screen:**
```
Build a KDS-compliant record detail screen for [record type].
Fields as definition list (dl/dt/dd): [list fields].
Status as KDS Tag (read-only) near H1.
Buttons: Edit (Secondary), Back to list (Ghost).
Follow all KDS component rules and accessibility requirements from the instructions file.
```

**Generate a workflow action screen:**
```
Build a KDS-compliant workflow action screen for [workflow step].
Read-only fields: definition list. Status: KDS Tag near H1.
Workflow buttons: [list, e.g., "Approve (Primary), Return for Correction (Secondary), Reject (Ghost)"].
Reject: confirmation step using KDS In-Page Alert (error variant) with Confirm and Cancel.
Follow all KDS component rules and accessibility requirements from the instructions file.
```

---

### Audit and Update Existing Screens

Use these prompts when you have an existing screen open in the editor.

**Full KDS compliance audit:**
```
Audit the open file against the KDS instructions.
Check: components, color, typography, button variants, form labels, accessibility, icon usage.
List violations grouped by category (Structure, Typography, Color, Buttons, Forms, Icons, Accessibility, Alerts).
For each: what is wrong, which KDS rule it breaks, exact fix required.
No changes — report only.
```

**Apply all KDS violations found in an audit:**
```
Apply every fix from the audit to the open file.
Change only what the audit identified. Do not refactor, rename variables, or restructure beyond KDS violations.
List what was changed.
```

**Update buttons to KDS:**
```
Update all buttons in the open file to correct KDS variants.
Rules: one Primary per section (main action), Secondary for cancel/back, Ghost for low-emphasis and destructive. No Primary for destructive actions. Icon buttons need aria-label.
Report changes.
```

**Update form fields to KDS:**
```
Update all form fields in the open file to comply with KDS Text Input, Drop-Down Select, Checkbox, and Radio Button rules.
Ensure: visible label per field, placeholder not sole guidance, help text uses aria-describedby, error states use KDS error variant with aria-invalid="true".
Report changes.
```

**Update typography to KDS:**
```
Update all text in the open file to correct KDS typography classes.
Plus Jakarta Sans. Correct scale classes for headings (H1–H6), body, labels, captions.
No hardcoded font sizes, weights, or line heights — KDS tokens only.
Report changes.
```

**Update colors to KDS tokens:**
```
Replace all color values (hex, rgb, hardcoded Tailwind, custom CSS variables) in the open file with KDS Material Design 3 tokens (e.g., --md-sys-color-primary, --md-sys-color-surface).
No color values that are not KDS tokens.
Report changes.
```

**Update icons to KDS / Remix Icons:**
```
Replace all non-Remix Icon classes in the open file with equivalent ri-* classes from the PA.gov icon catalog.
Decorative icons: aria-hidden="true". Interactive icon buttons: aria-label. Pair every icon with visible label text unless space-constrained (confirm aria-label is present).
Report changes.
```

**Add accessibility attributes:**
```
Review the open file for WCAG 2.1 AA and KDS accessibility gaps.
Check: images have alt text, form fields have labels and aria-describedby, interactive elements are keyboard-reachable, icon buttons have aria-label, dynamic regions use aria-live or role="alert", tables have captions and correct th scope.
Fix every gap. Report changes.
```

---

### Agent Mode Prompts

Use these in agent mode for larger tasks. A versatile model (Claude Sonnet 4.x, Gemini 3.1 Pro) balances cost and quality for multi-file work.

**Audit all screens in a folder:**
```
Audit every HTML/template file in [folder path] against the KDS instructions.
For each file: list violations grouped by category (Structure, Typography, Color, Buttons, Forms, Icons, Accessibility, Alerts).
Summary table: file name | violation count | highest-severity issue.
No changes — report only.
```

**Upgrade an entire feature to KDS:**
```
Update all files in [folder path] to be fully KDS-compliant.
Work through each file: fix buttons, forms, typography, colors, icons, accessibility.
After each file, list changes.
Only change what is required for KDS compliance.
```

**Generate a complete CRUD screen set:**
```
Generate KDS-compliant CRUD screens for [entity] with fields: [list with types].
Create four files:
1. list.html — table with toolbar (search, filters, Add button, rows-per-page), pagination, status tags, View/Edit/Delete Ghost buttons per row.
2. add.html — data entry form with fieldset grouping, required field marking, Submit and Cancel.
3. edit.html — same as add.html pre-populated, Save and Cancel.
4. view.html — read-only definition list, status tag, Edit and Back buttons.
All files: KDS component rules, accessibility requirements, data application UI patterns.
```

**Update all tables to CRUD pattern:**
```
Update every data table in all files in [folder path] to the KDS data table pattern.
Per table:
1. Actions column (last): Ghost buttons for View, Edit, Delete.
2. Toolbar: search input, filter drop-downs, "Add [record type]" Primary button, Rows per page (10/25/50).
3. Pagination: Previous/Next, current page, total pages, record count ("Showing X–Y of Z results").
4. Empty state message.
5. Table caption, th with correct scope, status values as KDS Tag (read-only).
Only change table markup and controls. After all files, list changes per file.
```

**Consistency check across screens:**
```
Check all files in [folder path] for cross-screen consistency.
Verify: same status values and Tag colors everywhere, identical button labels for the same action, identical form field labels for the same data, same pagination pattern on all list screens.
List every inconsistency with file name, line reference, and fix.
```

---

## Related Guides

- Main prompt guide: [Prompt Guide.md](./Prompt%20Guide.md)
- KDS agent usage guide: [KDS-Agent-Guide.md](./KDS-Agent-Guide.md)
