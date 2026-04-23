# PA.gov / Keystone Design System — GitHub Copilot Instructions

**Source:** Keystone Design System Authoring Guide (https://wcmauthorguide.pa.gov/en/keystone-design-system/)
**Source Revalidated:** April 20, 2026

---

## KDS Overview

The Keystone Design System (KDS) is the official design system for Commonwealth of Pennsylvania websites and web applications. It provides a shared library of components, design tokens, and authoring guidelines that ensure consistency, accessibility, and brand alignment across all PA.gov properties.

KDS is currently in beta. Storybook and Figma files are the authoritative references for implementation. Always apply KDS patterns when building or authoring PA.gov content.

---

## Design Principles

1. **Accessibility First** — Every component and content pattern must meet WCAG 2.1 AA standards. Keyboard navigation and screen reader support are non-negotiable.
2. **Consistency** — Use shared tokens, components, and patterns. Do not invent custom variants when a KDS component exists.
3. **Flexibility** — KDS components are configurable. Apply the available variants and options before reaching for custom code.
4. **Plain Language** — Write at a 5th-grade reading level. Use active voice, short sentences, and direct instructions.
5. **Mobile-First** — All layouts and components must be tested at all four breakpoints. The XS breakpoint is the design baseline.
6. **Audience First** — Structure content around what the user needs to do, not what the agency wants to say.

---

## Foundations

### Color

KDS uses a Material Design 3–based color token system with light and dark mode variants.

#### Light Mode Tokens

| Token Role | Hex |
|---|---|
| Primary | `#00629E` |
| On Primary | `#FFFFFF` |
| Primary Container | `#CFE5FF` |
| On Primary Container | `#001D34` |
| Secondary | `#526070` |
| On Secondary | `#FFFFFF` |
| Secondary Container | `#D6E4F7` |
| On Secondary Container | `#0F1D2A` |
| Tertiary | `#835500` |
| On Tertiary | `#FFFFFF` |
| Tertiary Container | `#FFDDB4` |
| On Tertiary Container | `#291800` |
| Error | `#BA1A1A` |
| On Error | `#FFFFFF` |
| Error Container | `#FFDAD6` |
| On Error Container | `#410002` |

#### Dark Mode Tokens

| Token Role | Hex |
|---|---|
| Primary | `#9ACBFF` |
| On Primary | `#003355` |
| Primary Container | `#004A78` |
| On Primary Container | `#CFE5FF` |
| Secondary | `#BAC8DA` |
| On Secondary | `#243240` |
| Secondary Container | `#3A4857` |
| On Secondary Container | `#D6E4F7` |
| Tertiary | `#FFB954` |
| On Tertiary | `#452B00` |
| Tertiary Container | `#633F00` |
| On Tertiary Container | `#FFDDB4` |
| Error | `#FFB4AB` |
| On Error | `#690005` |
| Error Container | `#93000A` |
| On Error Container | `#FFDAD6` |

**Rules:**
- Always use semantic token roles (e.g., `color.light.primary`), not raw hex values.
- Never rely on color alone to convey meaning — always pair with text or icons.
- Ensure all text/background combinations meet WCAG AA contrast minimums (4.5:1 for body text, 3:1 for large text).

---

### Typography

**Typefaces:**
- **Zilla Slab** — Display and Headline styles
- **Plus Jakarta Sans** — Title, Body, and Label styles

#### Type Scale

| Style | Desktop | Mobile | Line Height | Typeface |
|---|---|---|---|---|
| Display Large | 72px | 48px | 105% | Zilla Slab |
| Display Medium | 56px | 40px | 105% | Zilla Slab |
| Display Small | 48px | 32px | 105% | Zilla Slab |
| Headline Large | 40px | 24px | 120% | Zilla Slab |
| Headline Medium | 32px | 20px | 120% | Zilla Slab |
| Headline Small | 24px | 16px | 120% | Zilla Slab |
| Title Large | 20px | — | 120% | Plus Jakarta Sans |
| Title Medium | 16px | — | 120% | Plus Jakarta Sans |
| Title Small | 12px | — | 120% | Plus Jakarta Sans |
| Body Large | 16px | — | 150% | Plus Jakarta Sans |
| Body Medium | 14px | — | 150% | Plus Jakarta Sans |
| Body Small | 12px | — | 150% | Plus Jakarta Sans |
| Label Large | 14px | — | 125% | Plus Jakarta Sans |
| Label Medium | 12px | — | 125% | Plus Jakarta Sans |
| Label Small | 11px | — | 125% | Plus Jakarta Sans |

**Body max-widths:** Body Large = 510px, Body Medium = 486px, Body Small = 384px.

**Rules:**
- Recommended line length: 40–75 characters.
- Use smaller scale values at breakpoints below 992px (Medium).
- Maintain logical heading hierarchy (H1 → H2 → H3) in HTML even when visual styling varies.
- Pre-titles always use Title Small uppercase.
- Pair type styles from the same size tier (e.g., Large with Large).

---

### Design Tokens

**Naming convention:** `[attribute].[theme].[role]`

Examples:
- `color.light.primary`
- `color.dark.on-surface`
- `space.large`
- `elevation.4`

**Token types:** color · spacing · typography · elevation

**Rules:**
- Always reference tokens by name, never by raw values, to enable consistent theming across light/dark modes.
- Tokens abstract design decisions; adding new raw values breaks design consistency.

---

### Elevation

Elevation communicates visual hierarchy and focus through shadow depth.

**Principles:**
- **Consistency** — Use the same elevation level for the same type of element site-wide.
- **Hierarchy** — Higher elevation = higher priority or active focus state.
- **Subtlety** — Elevation should be functional, not purely decorative.
- **Accessibility** — Sufficient color contrast must be maintained at all elevation levels.

**Rules:**
- Do not add decorative shadows outside the elevation token scale.
- Use elevation to signal focus, modal state, or interactive priority — not aesthetic preference.

---

### Icons

**Library:** [Remix Icons](https://remixicon.com/) (accessible to Commonwealth network users)

**PA.gov icon catalog:** [https://wcmauthorguide.pa.gov/en/style-guide/icons.html](https://wcmauthorguide.pa.gov/en/style-guide/icons.html) — Browse all available `ri-*` class names organized by category (Arrows, Buildings, Business, Communication, Design, Development, Device, Document, Editor, Finance, Food, Health & Medical, Logos, Map, Media, System, User & Faces, Weather, Others). Use this catalog to select icon class names when generating code.

**Rules:**
- One icon = one consistent meaning throughout the entire site. Do not reuse the same icon for different concepts.
- Always pair icons with text unless the meaning is universally understood.
- Decorative icons must include `aria-hidden="true"` so screen readers skip them.
- Interactive icons must have an accessible label (`aria-label` or visible text).

---

### Grid / Layout

| Breakpoint | Range | Columns | Gutter | Margin |
|---|---|---|---|---|
| X-Small | 0–640px | 4 | 16px | 16px |
| Small | 641–991px | 8 | 16px | 24px |
| Medium | 992–1439px | 12 | 24px | 32px |
| Large | 1440px+ | 12 | 24px | Auto |

At 1440px and above, the grid is fixed: content area = 1200px wide, centered.

**Mobile-first CSS breakpoints:**

```css
/* XS — base styles, no media query needed (0–640px) */

/* Small — 641px and up */
@media (min-width: 641px) { }

/* Medium — 992px and up */
@media (min-width: 992px) { }

/* Large — 1440px and up */
@media (min-width: 1440px) {
  .content-area { max-width: 1200px; margin-inline: auto; }
}
```

**Rules:**
- NEVER use tables for page layout. Tables are for data only.
- Design mobile-first (XS breakpoint as baseline), expand for larger breakpoints.
- Use the grid column system for all multi-column layouts.
- Use `min-width` media queries only — never `max-width` queries (they invert the mobile-first cascade).
- Never introduce custom breakpoint values outside the four KDS breakpoints above.

---

## Components

### Accordion

Progressively discloses content under a heading. Users expand sections relevant to them.

**When to use:**
- Content that is only relevant to specific user groups, not everyone.
- Reducing cognitive load on long pages.

**When NOT to use:**
- Critical information that all users must see — do not hide it in an accordion.

**Rules:**
- Every accordion item requires a heading that accurately describes the hidden content.
- Headings must reflect document hierarchy (do not skip levels).
- Effective, specific headings are critical for usability.

---

### Breadcrumb

A horizontal trail showing the user's location in the site hierarchy.

**When to use:** Show on all pages except the homepage.

**Rules:**
- Keyboard: Tab / Shift+Tab to navigate between crumbs; Enter to activate.
- Labels must reflect the actual page destination — no vague or truncated labels.

---

### Button

Triggers an action (submit, save, sign up, delete). Not for navigation (use Link for navigation).

| Variant | Purpose | Constraint |
|---|---|---|
| Primary | Most important CTA on the page or section | **One per page/section** (e.g., Submit, Log In, Save) |
| Secondary | Helpful but non-essential action | Always pair with a Primary button (e.g., Cancel, Instructions) |
| Ghost | Low-priority action | Use when presenting three or more buttons (e.g., View Details) |
| Icon | Space-saving action button | Use sparingly; always provide an accessible text label |

**Rules:**
- Links navigate; buttons act. Do not use a button where a link is semantically correct, or vice versa.
- Label buttons with the outcome, not the mechanism: "Submit application", not "Click here".
- Avoid generic labels: "Click Here", "Download Now", "Get Help".
- One Primary button per visual section.

---

### Card

A visual container grouping a title, description, and link for a single topic or item.

**Required fields:** title + description + link  
**Optional fields:** image, icon, date, tags

**When to use:**
- Differentiating similar destination links that have distinct features or descriptions.
- When items benefit from an image or icon to aid recognition.

**When NOT to use:**
- When no compelling image or icon is available — use List Group instead.
- Never place a single card alone; cards are always shown in groups.

**Rules:**
- Every card must have a meaningful link destination with descriptive link text.
- Images must have alt text that describes the image content in context.

---

### Checkbox

Allows users to select one or more options from a list.

**When to use:** Multi-selection in forms, filters, or agreement acceptance.

**When NOT to use:** Single-choice selection — use Radio Button instead.

**Rules:**
- Keep option lists short. Break long lists into multiple questions.
- Every checkbox must have a clear, concise label.
- Include help text when the label alone is insufficient.

---

### Drop-Down Select

A single-choice input that displays a scrollable list of options in a dropdown menu.

**When to use:** Single-choice selection from a long list; ideal for forms where options are brief.

**When NOT to use:**
- Multi-selection — use Checkbox.
- 1–2 options — use Radio Button.

**Rules:**
- Always provide an accurate, descriptive label for the field.
- Assign a unique `id` to any associated help text.
- Use `aria-describedby` to link the input to its help text.

---

### Footer

The site footer. Required on every PA.gov page.

**Structure:** Agency logo + up to 3 link lists + copyright/policy banner.

**Rules:**
- **NEVER remove the footer.** It is a required component on every page.
- Group related links under clear, descriptive headings (aids screen reader navigation).
- Use clear, descriptive link text — avoid vague labels.

---

### Global Alert

A banner that appears across every page of the site.

**When to use:** Critical information or emergencies only (system outages, declared emergencies, urgent safety notices).

**When NOT to use:** Information relevant to a single page or process — use In-Page Alert instead.

**Rules:**
- Choose the variant (info, warning, error, success) that matches the actual severity.
- Keep the title clear and brief.
- Body: ≤2 sentences in plain language.
- Include an end date/time if the situation is temporary.
- Conclude with a descriptive link to a page with full details.
- **Remove the alert as soon as the event or issue is resolved.**

---

### Header

The site header. Required on every PA.gov page.

**Structure:** Official Commonwealth website banner + navigation bar (agency/program logo, program name, search bar, navigation menu with dropdowns).

**Responsive behavior:** Collapses to a hamburger menu on small screen sizes.

**Rules:**
- **NEVER remove the header.** It is a required component on every page.
- All navigation menu items must have clear, descriptive labels.
- The official PA.gov banner must always be visible — it establishes trust and authenticity.

---

### Icon Object

A standalone icon displayed inside a circular background container, typically used to represent a service or topic.

**When to use:** Representing categories, services, or topics where a visual cue aids recognition.

**Rules:**
- Always accompany the icon with a text label. Users cannot be expected to interpret icons alone.
- One icon = one consistent meaning across the entire site.
- Decorative uses must include `aria-hidden="true"`.
- Do not use Icon Objects to compensate for confusing page structure — fix the structure first.

---

### In-Page Alert

An alert banner scoped to a single page or process.

**When to use:**
- Errors (submission failed, required fields missing).
- Missing required field notifications.
- Important non-critical information relevant only to this page.
- Changes to a process or deadline.

**When NOT to use:** Site-wide emergencies — use Global Alert instead.

**Rules:**
- Variant must match actual severity (info, warning, error, success).
- Clear brief title + ≤2 sentence plain-language summary.
- Include an end date/time if applicable.
- Conclude with a descriptive link to more details.

---

### Link

Navigates to another page or resource. Not for triggering actions (use Button for actions).

**Variants:**
- **Standalone Link** — Can include a leading or trailing icon.
- **Inline Link** — Embedded within body text; no icon.

**Rules:**
- Link text must clearly describe the destination. Specific examples:
  - ✅ "Your account", "View election results", "Register for the event"
  - ❌ "Click here", "Read more", "This link"
- For PDF links, append `[PDF]` to the link text: "2024 Annual Report [PDF]"
- Keyboard: Tab to focus, Enter to activate.

---

### List Group

A vertically stacked list of links, displayed in 1–2 columns. Used for supplementary navigation.

**Item structure:** Required: title + link destination + link icon. Optional: leading icon, pretitle, description.

**When to use:** Category-, subject-, or audience-based navigation sections (e.g., "Services for businesses", "Resources for families").

**When NOT to use:** Bulleted or numbered lists in running body copy — use standard HTML list elements.

**Rules:**
- Every item must have a link destination.
- All link text must be meaningful and descriptive.

---

### Radio Button

Allows a user to select exactly one option from a list of 2 or more. Selecting a new option automatically deselects the previous selection.

**When to use:** Single-choice selection from 2 or more options.

**When NOT to use:** Multi-selection — use Checkbox.

**Rules:**
- Labels: ≤3 words, sentence case, NO ALL CAPS.
- Keep the option list short.
- Keyboard: Arrow keys to move between options; Space to select.

---

### Tag

A small keyword label that categorizes or classifies content. Can be informational (read-only) or dismissable (includes an × close button).

**When to use:** Large content collections with well-defined categories (e.g., filter by publication date, filter by audience type).

**When NOT to use:** Unique identifiers (e.g., user IDs, case numbers).

**Rules:**
- Avoid vertical stacking of tags.
- Labels must be brief and clear.
- Do not rely on tag color alone to convey meaning — always include a text label.

---

### Table

A structured grid of rows and columns for presenting data.

**When to use:**
- Displaying and comparing structured data.
- Scannable content with short cell values.

**When NOT to use:**
- Paragraph-length cell content.
- **NEVER use tables for page layout** — use the grid system.

**Rules:**
- Every table needs a clear descriptive header (caption or heading above the table) for context.
- Column and row labels must be brief and in plain language.
- For large datasets, split into multiple smaller tables with clear headings rather than one overwhelming table.
- Tables with more than one page of records must include **pagination controls**: previous/next buttons and page number indicators.
- Paginated tables must include a **records-per-page selector** (a Drop-Down Select) allowing users to choose how many rows to display (e.g., 10, 25, 50). Place it above or below the table, clearly labeled (e.g., "Rows per page").
- The current page and total page/record count must be visible (e.g., "Showing 1–25 of 143 results").
- Pagination controls must be keyboard-accessible and announced to screen readers (use `aria-label` on navigation buttons; update a live region or page heading when the page changes).

---

### Text Input

A single-line text field for collecting short text responses.

**When to use:** Short text input — names, usernames, passwords, short identifiers.

**When NOT to use:** Responses of one sentence or more — use a textarea instead.

**Field anatomy:**
- **Label** (required) — Clearly describes the expected input. Sentence case.
- **Help text** (optional) — Provides context or formatting instructions. Sentence case. Persistent below the field.
- **Placeholder text** (optional) — Example value inside the field. Sentence case. Disappears when the user types.

**Variants:**
- **Warning** — User should review their response before proceeding. Warning message replaces help text.
- **Error** — Response prevents submission or saving (missing required value, invalid format). Error message replaces help text.

**Rules:**
- **NEVER put critical information in placeholder text.** It disappears when the user starts typing. Always use help text for essential instructions.
- Label and help text must be in sentence case.
- Placeholder text: use sparingly; sentence case; never the only source of important guidance.

---

## Content & Writing Guidelines

### Plain Language

- Write at a 5th-grade reading level.
- Use active voice and short, direct sentences.
- Prefer common, everyday words over jargon and technical terms.
- Break long content into short sections with descriptive headings.
- Use bulleted lists to replace long sentences with multiple items.
- Recommended body line length: 40–75 characters.

### Voice and Tone

- **Trusted and Informed** — Sound like a knowledgeable, calm guide. Not bureaucratic, not promotional.
- Lead with what the user needs to do, not what the agency wants to say.
- Use factual, plain statements. Avoid hype or urgency for routine content.
- Operational UI text (button labels, empty states, validation messages) should be direct and task-focused.

### Inclusive Language

- Use person-first language.
- Avoid ableist, ageist, racist, or sexist language.
- Use gender-neutral terms: "constituents", "residents", "guests" — not gendered greetings.
- Replace gendered role names with neutral equivalents.
- Do not make assumptions about the user's income, education, or background.
- Avoid vision-specific instructions ("see the section below", "as shown in the image"). Use alternatives: "refer to", "check", "learn about".

### Link and Button Text

| Context | Good example | Bad example |
|---|---|---|
| Link | "View election results" | "Click here" |
| Link | "Register for the event" | "Read more" |
| Button | "Submit application" | "Go" |
| Button | "Download 2024 Annual Report [PDF]" | "Download" |

### Scannability

- Break copy into small, focused sections.
- Use headings and subheadings to group related content.
- Use bulleted lists for 3+ related items.
- Use bold text sparingly for emphasis; do not bold for decoration.
- Use statistical callouts (large numbers with brief context labels) for key data points.

---

## Accessibility Standards

### WCAG 2.1 AA Requirements

- **Color contrast:** Body text ≥ 4.5:1 · Large text (18px+, or 14px+ bold) ≥ 3:1 · UI components ≥ 3:1.
- **Keyboard navigation:** All interactive elements reachable and operable via keyboard alone.
- **Focus indicators:** Visible focus states on all interactive elements.
- **Screen reader support:** Semantic HTML, ARIA roles and labels where native semantics are insufficient.
- **No color-only meaning:** Always pair color cues with text or icons.
- **Alt text:** Every meaningful image must have descriptive alt text. Decorative images use `alt=""`.

### Component-Specific Accessibility

| Component | Keyboard pattern | ARIA requirement |
|---|---|---|
| Accordion | Tab to focus header, Enter/Space to expand | `aria-expanded`, `aria-controls` |
| Breadcrumb | Tab/Shift+Tab to navigate, Enter to activate | `aria-label="breadcrumb"` on nav |
| Button | Tab to focus, Enter/Space to activate | Descriptive label; `aria-label` if visual text is insufficient |
| Checkbox | Tab to focus, Space to toggle | `aria-checked`, associated `<label>` |
| Drop-Down Select | Tab to focus, arrow keys to select | Associated `<label>`, `aria-describedby` for help text |
| Icon (decorative) | Not focusable | `aria-hidden="true"` |
| In-Page Alert | — | `role="alert"` or `aria-live` for dynamic insertion |
| Link | Tab to focus, Enter to activate | Descriptive link text; `aria-label` if text is ambiguous |
| Radio Button | Tab to first option, arrow keys to move, Space to select | Fieldset + legend; `aria-checked` |
| Text Input | Tab to focus | Associated `<label>`, `aria-describedby` for help/error text |

---

## Data Application UI Patterns

Use these patterns when building government line-of-business applications: data entry forms, workflow processing screens, and data management grids. All patterns use KDS components and tokens only — no custom components.

---

### Page Layout for Data Applications

Government data apps typically follow a three-zone structure. Use KDS grid columns at each breakpoint.

```
┌──────────────────────────────────────────────────┐
│  Header (required — KDS Header component)        │
├──────────────────────────────────────────────────┤
│  Page title + action bar (H1 + Primary button)   │
├──────────────────────────────────────────────────┤
│  Search / filter bar  │  (optional side panel)   │
├──────────────────────────────────────────────────┤
│  Data table / content area                       │
├──────────────────────────────────────────────────┤
│  Footer (required — KDS Footer component)        │
└──────────────────────────────────────────────────┘
```

**Rules:**
- Place the page H1 and the single Primary action button ("Add record", "Submit application") at the top of the content area — not inside the table.
- Keep the search/filter bar visually separated from the table (use spacing tokens, not a visible divider line).
- Never put the Header or Footer inside a CSS grid content column — they span full width.
- On XS/Small breakpoints, collapse side panels below the main content area; do not use horizontal scroll.

---

### Data Entry Forms

**KDS requirements for forms:**
- Every field must use a KDS form component (Text Input, Drop-Down Select, Checkbox, Radio Button).
- Every field must have an associated `<label>` rendered via the KDS label pattern.
- Error states must use the KDS component error variant (not custom styling).
- Action buttons must use KDS Button variants.

**Usability recommendations (not KDS rules):**
- **Prefer a single-column vertical layout** (one field per row). Multi-column form layouts increase error rates and are harder to scan — this is a well-established usability finding (Nielsen Norman Group, GOV.UK, USWDS), not a KDS mandate. Multi-column is acceptable when fields are short and logically paired (e.g., First name / Last name, City / State / Zip).
- On narrow viewports, always collapse to a single column regardless of the desktop layout.

**Field grouping:**
- Group related fields under a `<fieldset>` with a concise `<legend>` (e.g., "Contact information", "Address details").
- Separate groups with vertical spacing tokens, not ruled lines.
- Long forms (more than ~7 fields) should be broken into logical sections using H2/H3 subheadings or multi-step workflow (one section per step).

**Label and help text:**
- Every field must have a visible `<label>`. Never rely on placeholder text alone.
- Mark required fields with an asterisk (*) and include a note above the form: "Fields marked * are required."
- Place help text below the label, above the input, using the KDS help text pattern with `aria-describedby`.

**Validation:**
- Validate on submit first; then validate inline on blur for individual fields after the first failed submit.
- Show a KDS In-Page Alert (error variant) at the top of the form listing all errors — in addition to inline field-level error messages.
- Never clear a field's value when showing an error. Preserve what the user typed.
- Use `aria-invalid="true"` and link error messages via `aria-describedby` on every field in error.

**Action buttons (form footer):**
- Primary button = the submit/save action ("Submit application", "Save record"). One per form.
- Secondary button = the cancel/back action ("Cancel", "Back"). Always paired with Primary.
- Destructive actions ("Delete", "Discard") use Ghost button variant. Separate from the primary action group with spacing; do not place adjacent to Submit.
- Never disable a Submit button to prevent submission — show validation errors instead. Disabled buttons have no accessible error feedback.

---

### Data Tables with CRUD Actions

#### Table Toolbar (above the table)

Place a toolbar row between the page title and the table containing:
1. **Search input** — Text Input labelled "Search [record type]" (e.g., "Search applications"). Triggers filtering.
2. **Filter controls** — Drop-Down Select components for filterable columns (status, date range, category). Label each clearly.
3. **Add button** — Primary button: "Add [record type]" (e.g., "Add application"). Only one per table view.
4. **Records-per-page selector** — Drop-Down Select labelled "Rows per page" with options 10 / 25 / 50.

On XS/Small breakpoints, stack toolbar controls vertically. The Add button remains at the top.

#### Table Column Structure

- **First column:** The primary identifier for the record (name, ID, reference number). This value becomes the link for the View/detail action.
- **Middle columns:** Key status and date fields relevant to the workflow. Keep to 4–6 columns maximum for readability.
- **Last column:** An "Actions" column containing row-level action controls (see below).

#### Row-Level Actions

Use Ghost buttons for all row-level actions to avoid visual noise from repeated Primary/Secondary buttons:

| Action | Control | Label |
|---|---|---|
| View | Ghost button or linked record identifier | "View" / use record name as link |
| Edit | Ghost button | "Edit" |
| Delete | Ghost button | "Delete" |

**Rules:**
- When all three actions are present, order them: View → Edit → Delete.
- Separate "Delete" visually or with a divider character (\|) when displayed inline with View/Edit — it is destructive and should not be accidentally activated.
- **Always require confirmation before deleting.** Show a modal-style In-Page Alert or a dedicated confirmation page — never delete on a single click.
- For icon-only action buttons (space-constrained views), use the KDS Icon button variant with `aria-label` ("View record", "Edit record", "Delete record"). Pair with a visible tooltip if possible.
- When a row is in a state where an action is not available (e.g., a submitted record cannot be edited), omit the button entirely — do not render it as disabled.

#### Empty State

When the table has no records (new dataset, or search returns no results), replace the table body with a plain-language message:

```html
<p>No [record type] found. <a href="/add">Add the first [record type]</a>.</p>
```

Do not show an empty table shell with zero rows.

#### Table Status Indicators

Use KDS Tags (read-only variant) in status columns to show record state (e.g., Pending, Approved, Rejected, Under Review). Follow these rules:
- Never rely on tag color alone — the label text must communicate the status.
- Use a consistent, documented set of status values. Do not invent ad-hoc statuses per screen.
- Limit status tags to one per row in most cases; two maximum.

---

### Workflow / Status Screens

When a record moves through a multi-step process (submitted → under review → approved/rejected):

- Show the current status prominently near the page H1 using a Tag (read-only) or KDS In-Page Alert (info variant for neutral states).
- If workflow steps are linear, show a step indicator above the content area listing the steps and marking the current one (can be implemented as a styled ordered list using KDS tokens — no custom component needed).
- Workflow action buttons ("Approve", "Return for correction", "Reject") follow the same Button rules: one Primary per section, destructive actions (Reject) as Ghost with confirmation.
- Place workflow actions at the bottom of the record detail view, after all the data fields, so users read the record before acting.

---

### Detail / View Record Screen

When a user selects a record to view:

- Display fields in a definition-list (`<dl>` / `<dt>` / `<dd>`) or a two-column label/value layout using KDS grid columns — not a table.
- Labels (`<dt>`) use Label Medium style (Plus Jakarta Sans, 12px). Values (`<dd>`) use Body Medium.
- Group fields under the same `<fieldset>`/section structure used on the entry form so the layout feels consistent.
- Place Edit and Back buttons at the bottom. "Edit" = Secondary button (it leads to a new action, not the primary reason for this screen). "Back to list" = Ghost button or a Standalone Link.
- Show a read-only status Tag near the H1.

---

### General Data Application Rules

- **Scannable tables over dense forms:** Display data in a table first; only expand to a full form view when the user explicitly chooses View or Edit.
- **Preserve filter and pagination state** when the user returns from a detail view — use URL query parameters or session state so users are not reset to page 1.
- **Confirm destructive actions** — always. Use clear language: "Are you sure you want to delete [record name]? This cannot be undone."
- **Show success feedback** after save/submit/delete using a KDS In-Page Alert (success variant) at the top of the resulting page or list view. Auto-dismiss after 5 seconds if non-critical.
- **Empty required fields** — flag them on submit with the KDS Text Input error variant + In-Page Alert summary. Do not silently fail.
- **Loading states** — if a data fetch takes more than 300ms, show a loading indicator and disable action buttons to prevent duplicate submissions. Use `aria-busy="true"` on the loading region.
- **No inline editing** — do not make table cells directly editable. Link to a dedicated edit form. Inline editing is inaccessible and violates KDS form field patterns.

---

## Code Generation Rules

When generating HTML, templates, or components for PA.gov:

1. **Use semantic HTML** — correct heading hierarchy (H1 → H2 → H3), landmark elements (`<nav>`, `<main>`, `<footer>`, `<header>`), and list elements for lists.
2. **Reference design tokens by name** — never hardcode raw hex values or pixel sizes.
3. **Apply the correct component variant** — match the visual variant to its intended semantic use (error = error, warning = warning).
4. **One Primary button per section** — never place two Primary buttons in the same visual group.
5. **Never use tables for layout** — tables are for tabular data only.
6. **Descriptive link and button text** — every link and button must communicate its destination or outcome without surrounding context.
7. **Append `[PDF]` to PDF links** — always, in the visible link text.
8. **Decorative icons: `aria-hidden="true"`** — interactive icons need an accessible label.
9. **Pair every icon with text** unless the meaning is universally unambiguous.
10. **Help text over placeholder text** — never put essential instructions in placeholder text.
11. **Header and Footer are required** — never omit them. They are required on every page.
12. **Global Alert removes when resolved** — include a removal condition in any code managing Global Alert visibility.
13. **Grid system for all layouts** — use KDS breakpoints and column counts; no custom breakpoints.
14. **Mobile-first CSS** — write base styles for XS (0–640px) and use `min-width` media queries to enhance for larger breakpoints.
15. **WCAG AA contrast** — verify all foreground/background color pairs before shipping.

---

## Code Audit Checklist

When asked to review or update existing source code for KDS compliance, check each item below. Flag violations and apply the fixes described in [Common Violations and Fixes](#common-violations-and-fixes).

### Structure and Layout
- [ ] Every page includes a `<header>` containing the official PA.gov banner
- [ ] Every page includes a `<footer>`
- [ ] Page content is wrapped in a `<main>` landmark
- [ ] No `<table>` element is used for page layout (columns, sidebars, centering)
- [ ] Multi-column layouts use CSS grid/flexbox with KDS breakpoints, not `float` or layout tables
- [ ] All `@media` queries use `min-width` (mobile-first), not `max-width`
- [ ] No custom breakpoint values outside 641px, 992px, 1440px

### Typography and Color
- [ ] No hardcoded hex colors (`#xxxxxx`, `rgb(...)`, `hsl(...)`) in CSS or inline styles
- [ ] No hardcoded font-size pixel values — reference tokens or the type scale
- [ ] No `<font>` tags
- [ ] Heading levels are sequential — no skipped levels (H1 → H2 → H3)
- [ ] No heading level used purely for visual size — use CSS classes for visual styling
- [ ] Display/Headline styles use Zilla Slab; Title/Body/Label styles use Plus Jakarta Sans

### Links and Buttons
- [ ] No `<a>` whose visible text is "Click here", "Read more", "Learn more", "Here", or "This link"
- [ ] No `<a href="#">` or `<a href="javascript:void(0)">` used to trigger actions — use `<button>`
- [ ] No `<div>`, `<span>`, or `<td>` with an `onclick` attribute acting as a button
- [ ] No `<button>` used purely for navigation to a URL — use `<a>`
- [ ] No more than one Primary button variant within any single visual section
- [ ] All PDF links include `[PDF]` in the visible link text
- [ ] Every `<button>` has a discernible accessible name (visible text or `aria-label`)

### Forms
- [ ] Every `<input>`, `<select>`, and `<textarea>` has an associated `<label for="...">` or `aria-label`
- [ ] No form field relies solely on `placeholder` text for its label or essential instructions
- [ ] Help text and error text elements have a unique `id` and are linked to their field via `aria-describedby`
- [ ] Fields in an error state include `aria-invalid="true"`
- [ ] All radio button groups are wrapped in `<fieldset>` with a `<legend>`
- [ ] All checkbox groups are wrapped in `<fieldset>` with a `<legend>`
- [ ] Drop-Down Select fields use `<label>` + `aria-describedby` for any help text

### Images and Icons
- [ ] Every meaningful `<img>` has non-empty, descriptive `alt` text
- [ ] Decorative `<img>` elements have `alt=""`
- [ ] Decorative icons have `aria-hidden="true"`
- [ ] Icon-only interactive elements (buttons, links) have `aria-label` providing a text alternative

### Alerts
- [ ] Site-wide emergencies use Global Alert — not an In-Page Alert
- [ ] Single-page alerts use In-Page Alert — not a Global Alert
- [ ] Dynamic In-Page Alerts use `role="alert"` (errors/urgent) or `aria-live="polite"` (informational)
- [ ] Alert variant matches actual severity (info ≠ warning ≠ error ≠ success)

### General Accessibility
- [ ] No positive `tabindex` values (`tabindex="1"` or higher)
- [ ] Focus styles are not suppressed with `outline: none` or `outline: 0` without a replacement visible style
- [ ] Color is never the only differentiator between states (always pair with text or icon)
- [ ] All interactive elements are reachable and operable by keyboard alone

---

## Common Violations and Fixes

Apply these patterns when updating existing code. Each entry shows the non-compliant pattern and its KDS-compliant replacement.

> **Note on CSS token variable names:** KDS exposes design tokens as CSS custom properties. The exact variable names are defined in the KDS stylesheet. Use the format shown below as a placeholder (`--kds-*`) and verify against the imported KDS CSS file in the project. Never substitute raw hex values.

---

### 1. Hardcoded color → design token

```css
/* ❌ Non-compliant */
color: #00629E;
background-color: #CFE5FF;

/* ✅ KDS-compliant — reference the CSS custom property from the KDS stylesheet */
color: var(--kds-color-primary);
background-color: var(--kds-color-primary-container);
```

---

### 2. `<div onclick>` acting as a button → `<button>`

```html
<!-- ❌ Non-compliant -->
<div onclick="submitForm()" class="btn">Submit</div>

<!-- ✅ KDS-compliant -->
<button type="button" class="btn btn--primary" onclick="submitForm()">Submit application</button>
```

---

### 3. Generic link text → descriptive link text

```html
<!-- ❌ Non-compliant -->
<a href="/results">Click here</a>
<a href="/register">Read more</a>

<!-- ✅ KDS-compliant -->
<a href="/results">View election results</a>
<a href="/register">Register for the event</a>
```

---

### 4. `<a>` triggering an action → `<button>`

```html
<!-- ❌ Non-compliant — link used to submit a form or open a modal -->
<a href="#" onclick="openModal()">Open form</a>

<!-- ✅ KDS-compliant -->
<button type="button" onclick="openModal()">Open application form</button>
```

---

### 5. Form field with label only in placeholder → proper label + help text

```html
<!-- ❌ Non-compliant -->
<input type="text" placeholder="Enter your first name">

<!-- ✅ KDS-compliant -->
<div class="field">
  <label for="first-name">First name</label>
  <span id="first-name-help" class="field__help">Enter your legal first name as it appears on your ID.</span>
  <input type="text" id="first-name" name="first-name"
         aria-describedby="first-name-help"
         placeholder="e.g. Jane"
         autocomplete="given-name">
</div>
```

---

### 6. Form field error state missing ARIA → add `aria-invalid` and linked error message

```html
<!-- ❌ Non-compliant -->
<input type="email" class="error">
<span class="msg">Enter a valid email.</span>

<!-- ✅ KDS-compliant -->
<div class="field field--error">
  <label for="email">Email address</label>
  <span id="email-error" class="field__error">Enter a valid email address, e.g. name@example.com</span>
  <input type="email" id="email" name="email"
         aria-describedby="email-error"
         aria-invalid="true"
         autocomplete="email">
</div>
```

---

### 7. Radio group without fieldset → `<fieldset>` + `<legend>`

```html
<!-- ❌ Non-compliant -->
<div>
  <p>How do you prefer to be contacted?</p>
  <input type="radio" id="r-email" name="contact"> <label for="r-email">Email</label>
  <input type="radio" id="r-phone" name="contact"> <label for="r-phone">Phone</label>
</div>

<!-- ✅ KDS-compliant -->
<fieldset>
  <legend>How do you prefer to be contacted?</legend>
  <div class="radio">
    <input type="radio" id="r-email" name="contact" value="email">
    <label for="r-email">Email</label>
  </div>
  <div class="radio">
    <input type="radio" id="r-phone" name="contact" value="phone">
    <label for="r-phone">Phone</label>
  </div>
</fieldset>
```

---

### 8. Decorative icon missing `aria-hidden` → add `aria-hidden="true"`

```html
<!-- ❌ Non-compliant -->
<i class="ri-arrow-right-line"></i>

<!-- ✅ KDS-compliant -->
<i class="ri-arrow-right-line" aria-hidden="true"></i>
```

---

### 9. Icon-only button missing accessible name → add `aria-label`

```html
<!-- ❌ Non-compliant -->
<button><i class="ri-search-line"></i></button>

<!-- ✅ KDS-compliant -->
<button type="button" aria-label="Search">
  <i class="ri-search-line" aria-hidden="true"></i>
</button>
```

---

### 10. Layout table → semantic grid structure

```html
<!-- ❌ Non-compliant — table used for two-column layout -->
<table>
  <tr>
    <td class="sidebar">Navigation</td>
    <td class="content">Main content</td>
  </tr>
</table>

<!-- ✅ KDS-compliant — use CSS grid/flexbox -->
<div class="layout-grid">
  <nav aria-label="Section navigation">...</nav>
  <main>...</main>
</div>
```

---

### 11. Focus style removed → replace with visible focus indicator

```css
/* ❌ Non-compliant */
:focus { outline: none; }
a:focus { outline: 0; }

/* ✅ KDS-compliant */
:focus-visible {
  outline: 2px solid var(--kds-color-primary);
  outline-offset: 2px;
}
```

---

### 12. Table missing caption or scope → add `<caption>` and `scope` attributes

```html
<!-- ❌ Non-compliant -->
<table>
  <thead>
    <tr><th>Vehicle type</th><th>Annual fee</th></tr>
  </thead>
  <tbody>
    <tr><td>Passenger car</td><td>$38</td></tr>
  </tbody>
</table>

<!-- ✅ KDS-compliant -->
<table>
  <caption>License renewal fees by vehicle type</caption>
  <thead>
    <tr>
      <th scope="col">Vehicle type</th>
      <th scope="col">Annual fee</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Passenger car</th>
      <td>$38</td>
    </tr>
  </tbody>
</table>
```

---

### 13. `max-width` media query → convert to `min-width` mobile-first

```css
/* ❌ Non-compliant — desktop-first with max-width */
.component { display: flex; }
@media (max-width: 640px) { .component { display: block; } }

/* ✅ KDS-compliant — mobile-first with min-width */
.component { display: block; }
@media (min-width: 641px) { .component { display: flex; } }
```

---

### 14. Missing PDF indicator → append `[PDF]` to link text

```html
<!-- ❌ Non-compliant -->
<a href="/reports/annual-2024.pdf">2024 Annual Report</a>

<!-- ✅ KDS-compliant -->
<a href="/reports/annual-2024.pdf">2024 Annual Report [PDF]</a>
```

---

## HTML Structural Patterns

Reference these canonical markup patterns when generating or rewriting KDS components. Class names follow KDS BEM-style conventions — verify exact class names against the KDS Storybook and stylesheet.

---

### Page Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page title — Agency Name | PA.gov</title>
</head>
<body>
  <!-- Required: PA.gov header -->
  <header class="kds-header" role="banner">
    <div class="kds-header__banner">Official website of the Commonwealth of Pennsylvania</div>
    <nav class="kds-header__nav" aria-label="Main navigation">...</nav>
  </header>

  <main id="main-content">
    <!-- Page content -->
  </main>

  <!-- Required: PA.gov footer -->
  <footer class="kds-footer" role="contentinfo">...</footer>
</body>
</html>
```

---

### Accordion

```html
<div class="kds-accordion">
  <h3>
    <button type="button"
            class="kds-accordion__trigger"
            aria-expanded="false"
            aria-controls="accordion-1-content"
            id="accordion-1-heading">
      Accordion item heading
    </button>
  </h3>
  <div id="accordion-1-content"
       class="kds-accordion__panel"
       role="region"
       aria-labelledby="accordion-1-heading"
       hidden>
    <p>Accordion panel content.</p>
  </div>
</div>
```

---

### Breadcrumb

```html
<nav aria-label="Breadcrumb" class="kds-breadcrumb">
  <ol>
    <li class="kds-breadcrumb__item"><a href="/">Home</a></li>
    <li class="kds-breadcrumb__item"><a href="/services">Services</a></li>
    <li class="kds-breadcrumb__item kds-breadcrumb__item--current">
      <span aria-current="page">Renew your license</span>
    </li>
  </ol>
</nav>
```

---

### Button group (Primary + Secondary)

```html
<div class="kds-button-group">
  <!-- One Primary button per section -->
  <button type="submit" class="kds-button kds-button--primary">Submit application</button>
  <!-- Secondary is always paired with Primary -->
  <button type="button" class="kds-button kds-button--secondary">Cancel</button>
</div>
```

---

### In-Page Alert — error (dynamic)

```html
<div role="alert" class="kds-alert kds-alert--error">
  <strong class="kds-alert__title">Submission failed</strong>
  <p class="kds-alert__body">
    Your application could not be submitted. Check the required fields and try again.
    <a href="/help/submission-errors">Troubleshoot submission errors</a>.
  </p>
</div>
```

### In-Page Alert — informational (dynamic)

```html
<div aria-live="polite" aria-atomic="true" class="kds-alert kds-alert--info">
  <strong class="kds-alert__title">Processing times have changed</strong>
  <p class="kds-alert__body">
    Allow 10–15 business days for processing until June 30, 2026.
    <a href="/processing-times">View updated processing times</a>.
  </p>
</div>
```

---

### Text Input with help text

```html
<div class="kds-field">
  <label class="kds-field__label" for="full-name">Full name</label>
  <span id="full-name-help" class="kds-field__help">
    Enter your legal name as it appears on your government-issued ID.
  </span>
  <input class="kds-field__input"
         type="text"
         id="full-name"
         name="full-name"
         aria-describedby="full-name-help"
         autocomplete="name">
</div>
```

---

### Text Input in error state

```html
<div class="kds-field kds-field--error">
  <label class="kds-field__label" for="email">Email address</label>
  <span id="email-error" class="kds-field__error">
    Enter a valid email address, e.g. name@example.gov
  </span>
  <input class="kds-field__input"
         type="email"
         id="email"
         name="email"
         aria-describedby="email-error"
         aria-invalid="true"
         autocomplete="email">
</div>
```

---

### Drop-Down Select

```html
<div class="kds-field">
  <label class="kds-field__label" for="county">County</label>
  <span id="county-help" class="kds-field__help">Select the county where you currently reside.</span>
  <select class="kds-field__select"
          id="county"
          name="county"
          aria-describedby="county-help">
    <option value="">Select a county</option>
    <option value="philadelphia">Philadelphia</option>
    <option value="allegheny">Allegheny</option>
  </select>
</div>
```

---

### Radio Button group

```html
<fieldset class="kds-fieldset">
  <legend class="kds-fieldset__legend">How do you prefer to be contacted?</legend>
  <div class="kds-radio">
    <input class="kds-radio__input" type="radio" id="contact-email" name="contact" value="email">
    <label class="kds-radio__label" for="contact-email">Email</label>
  </div>
  <div class="kds-radio">
    <input class="kds-radio__input" type="radio" id="contact-phone" name="contact" value="phone">
    <label class="kds-radio__label" for="contact-phone">Phone</label>
  </div>
</fieldset>
```

---

### Checkbox group

```html
<fieldset class="kds-fieldset">
  <legend class="kds-fieldset__legend">Which services do you use?</legend>
  <div class="kds-checkbox">
    <input class="kds-checkbox__input" type="checkbox" id="svc-benefits" name="services" value="benefits">
    <label class="kds-checkbox__label" for="svc-benefits">Unemployment benefits</label>
  </div>
  <div class="kds-checkbox">
    <input class="kds-checkbox__input" type="checkbox" id="svc-license" name="services" value="license">
    <label class="kds-checkbox__label" for="svc-license">Driver license renewal</label>
  </div>
</fieldset>
```

---

### Data Table

```html
<table class="kds-table">
  <caption class="kds-table__caption">License renewal fees by vehicle type</caption>
  <thead class="kds-table__head">
    <tr>
      <th scope="col">Vehicle type</th>
      <th scope="col">Annual fee</th>
      <th scope="col">Renewal period</th>
    </tr>
  </thead>
  <tbody class="kds-table__body">
    <tr>
      <th scope="row">Passenger car</th>
      <td>$38</td>
      <td>2 years</td>
    </tr>
  </tbody>
</table>
```

---

*Source: Keystone Design System Authoring Guide — https://wcmauthorguide.pa.gov/en/keystone-design-system/ — Revalidated April 20, 2026. The KDS is in active development; revalidate component-level rules against the live authoring guide and Storybook before major implementations.*
