# Pennsylvania Government Website Design System - GitHub Copilot Prompt

**Source:** Pennsylvania WCM Author Guide (https://wcmauthorguide.pa.gov/en/style-guide.html)
**Date Extracted:** July 18, 2025
**Source Revalidated:** March 9, 2026

---

## Design System Overview

When building components or pages for Pennsylvania government websites, follow these design principles and patterns extracted from the PA.gov style guide:

### Core Design Principles

1. **Accessibility First**: All designs must be accessible and inclusive
2. **Scannability**: Content must be easily scannable and digestible
3. **5th Grade Reading Level**: Content and UI should be understandable at a 5th grade level
4. **Mobile-First**: All components must work responsively across devices
5. **Audience First**: Structure content around the task the person is trying to complete
6. **Trusted and Informed Tone**: Use calm, direct, factual language that helps people act with confidence

---

## Component Design Patterns

### Hero Component
```
Structure:
- H1 title (mandatory)
- Optional pre-title
- Description text (recommended for search results)
- Optional quick search bar OR call-to-action buttons
- Optional image (4:3 ratio, 1200x900px recommended)

Layout Options:
- Text alignment: Left (default) or Center
- Image alignment: Left, Right, or Top
- Background: Can use container background colors

Mobile Behavior:
- Images always appear on top on mobile/tablet
- Text should be left-aligned when using images
```

### Button/CTA Design Hierarchy
```
Primary Buttons:
- High visual impact
- Use for important, final actions (Save, Confirm)
- Only one primary button per group

Secondary Buttons:
- Medium emphasis
- Important but not primary actions
- Use for secondary actions in button groups

Ghost Buttons:
- Lowest priority actions
- Use when presenting multiple options
- Minimal visual impact until interaction
```

### Container System
```
Background Colors Available:
- Surface
- Background
- Background Alt
- Surface Container Lowest
- Surface Container Low
- Surface Container High

Width Options:
- Full width (stretches to page edges)
- Component Container (centered with margins)

Border Options:
- None (default)
- Container Border Radius (2rem)
- Container Small Border Radius (1rem)

Padding Options:
- Top/Bottom: None, Top, Bottom, or Top and Bottom
- Left/Right: None, Right, Left, or Left and Right
```

---

## Typography Hierarchy

### Heading Structure
```
H1: Page title (required, part of Hero component)
H2: Topic headlines/major sections
H3: Brief intro or sub-copy related to H2
H4: Body copy related to H2
H5: Body copy related to H2
H6: Closing body copy
```

### Text Formatting Guidelines
```
Bold/Italic Usage:
- Use sparingly for emphasis
- Avoid overuse as it impacts readability
- Consider accessibility - screen readers don't announce formatting

Accessibility Considerations:
- Avoid vision-specific words ("see", "view", "watch")
- Use alternatives: "access", "check", "learn about", "explore"
- Use gender-neutral language
- Write at 5th grade reading level
```

---

## Content Design Patterns

### Scannability Techniques
```
Content Structure:
- Break copy into smaller sections
- Group related content together
- Use headings and subheadings
- Implement bulleted lists
- Use short words, sentences, and paragraphs
- Minimize jargon
- Display information multiple ways
- Include content recaps

Visual Hierarchy:
- Use font colors and weights for emphasis
- Implement statistical callouts (large numbers with context)
- Create clear content groupings
```

### Inclusive Language Requirements
```
Writing Guidelines:
- Use person-first language
- Avoid ableist, ageist, sexist language
- Use gender-neutral greetings ("guests", "peers", "constituents")
- Replace gendered roles with neutral terms
- Use "holiday season" instead of "Christmas"
- Be mindful of classism and assumptions about education/income
```

### Voice And Tone
```
Voice Principles:
- Sound trustworthy, helpful, and direct
- Focus on what the user can do next
- Prefer factual, plain statements over promotional language
- Keep operational content calm and task-oriented

Operational UI Guidance:
- Lead with the task, not the system name
- Use action labels that describe the outcome
- Explain delays, empty states, and validation in plain language
```

---

## Accessibility Standards

### Essential Requirements
```
Navigation:
- Must be keyboard navigable
- Support screen readers
- Include ARIA labels where needed

Interactive Elements:
- CTAs reachable by Tab
- Selectable with Space or Enter
- Descriptive button labels (avoid "Click here", "Learn more")

Content:
- Meaningful headings for screen reader navigation
- Alt text for images
- Proper color contrast
- No reliance on color alone for meaning
```

### Button Accessibility
```
Label Requirements:
- Use descriptive, action-oriented labels
- Examples: "Submit this form", "Apply for benefits", "Explore our services"
- Avoid: "Click Here", "Download Now", "Get Help"
- 2-3 words recommended for button copy
- Include ARIA labels if visual text isn't descriptive enough
```

---

## Responsive Design Guidelines

### Mobile Considerations
```
Hero Component:
- Images always stack on top on mobile
- Text remains left-aligned
- CTAs may expand to full width

General:
- Test all components using device emulator
- Ensure touch-friendly interaction areas
- Consider thumb reach on mobile devices
```

---

## Implementation Notes

### Component Organization
```
Root Containers (built into templates):
- Hero section Container
- Main content Container  
- Bottom content Container (full width)

Additional Containers:
- Can be added as needed
- Support background colors and borders
- Enable content grouping and styling
```

### Image Guidelines
```
Hero Images:
- Optimal ratio: 4:3
- Recommended size: 1200x900px
- Disable lazy loading for hero images
- Full bleed option available for homepage hero
```

---

## Code Generation Guidelines

When generating code based on this design system:

1. **Always include accessibility attributes** (ARIA labels, roles, keyboard navigation)
2. **Implement responsive behavior** following mobile-first principles
3. **Use semantic HTML** with proper heading hierarchy
4. **Include descriptive button labels** and avoid generic text
5. **Support multiple background color options** for containers
6. **Implement proper focus states** for keyboard navigation
7. **Ensure color contrast meets WCAG standards**
8. **Use inclusive, plain language** in all UI text
9. **Test with screen readers** and keyboard-only navigation
10. **Follow the component hierarchy** (Hero → H2 sections → H3 subsections → content)

---

## Keystone Design System Specifications

### Typography System

**Primary Typefaces:**
- **Zilla Slab**: Used for display and headline styles
- **Plus Jakarta Sans**: Used for titles, labels, and body text

**Typography Scale:**
```
Display Styles (Zilla Slab):
- Display Large: 72px desktop / 48px mobile, 105% line height
- Display Medium: 56px desktop / 40px mobile, 105% line height  
- Display Small: 48px desktop / 32px mobile, 105% line height

Headline Styles (Zilla Slab):
- Headline Large: 40px desktop / 24px mobile, 120% line height
- Headline Medium: 32px desktop / 20px mobile, 120% line height
- Headline Small: 24px desktop / 16px mobile, 120% line height

Title Styles (Plus Jakarta Sans):
- Title Large: 20px, 120% line height
- Title Medium: 16px, 120% line height
- Title Small: 12px, 120% line height

Body Styles (Plus Jakarta Sans):
- Body Large: 16px, 150% line height, max-width 510px
- Body Medium: 14px, 150% line height, max-width 486px
- Body Small: 12px, 150% line height, max-width 384px

Label Styles (Plus Jakarta Sans):
- Label Large: 14px, 125% line height
- Label Medium: 12px, 125% line height
- Label Small: 11px, 125% line height
```

**Typography Guidelines:**
- Pair styles from the same size group (Large with Large, etc.)
- Pre-titles should always use title.small.uppercase
- Maintain logical HTML hierarchy regardless of visual styling
- Responsive breakpoint: Use smaller variants for screens < 992px

### Color System

**Primary Colors:**
```
Light Mode:
- Primary: #00629E rgb(0, 98, 158)
- On Primary: #FFFFFF rgb(255, 255, 255)
- Primary Container: #CFE5FF rgb(207, 229, 255)
- On Primary Container: #001D34 rgb(0, 29, 52)

Dark Mode:
- Primary: #9ACBFF rgb(154, 203, 255)
- On Primary: #003355 rgb(0, 51, 85)
- Primary Container: #004A78 rgb(0, 74, 120)
- On Primary Container: #CFE5FF rgb(207, 229, 255)
```

**Secondary Colors:**
```
Light Mode:
- Secondary: #526070 rgb(82, 96, 112)
- On Secondary: #FFFFFF rgb(255, 255, 255)
- Secondary Container: #D6E4F7 rgb(214, 228, 247)
- On Secondary Container: #0F1D2A rgb(15, 29, 42)

Dark Mode:
- Secondary: #BAC8DA rgb(186, 200, 218)
- On Secondary: #243240 rgb(36, 50, 64)
- Secondary Container: #3A4857 rgb(58, 72, 87)
- On Secondary Container: #D6E4F7 rgb(214, 228, 247)
```

**Tertiary Colors:**
```
Light Mode:
- Tertiary: #835500 rgb(131, 85, 0)
- On Tertiary: #FFFFFF rgb(255, 255, 255)
- Tertiary Container: #FFDDB4 rgb(255, 221, 180)
- On Tertiary Container: #291800 rgb(41, 24, 0)

Dark Mode:
- Tertiary: #FFB954 rgb(255, 185, 84)
- On Tertiary: #452B00 rgb(69, 43, 0)
- Tertiary Container: #633F00 rgb(99, 63, 0)
- On Tertiary Container: #FFDDB4 rgb(255, 221, 180)
```

**Error Colors:**
```
Light Mode:
- Error: #BA1A1A rgb(186, 26, 26)
- On Error: #FFFFFF rgb(255, 255, 255)
- Error Container: #FFDAD6 rgb(255, 218, 214)
- On Error Container: #410002 rgb(65, 0, 2)

Dark Mode:
- Error: #FFB4AB rgb(255, 180, 171)
- On Error: #690005 rgb(105, 0, 5)
- Error Container: #93000A rgb(147, 0, 10)
- On Error Container: #FFDAD6 rgb(255, 218, 214)
```

### Design Token Structure

**Token Naming Convention:**
`[attribute].[theme].[role]`

Examples:
- `color.light.primary` - Primary color in light mode
- `color.dark.on-surface` - Text color on surface in dark mode
- `space.large` - Large spacing value
- `elevation.4` - Elevation level 4 shadow

**Token Categories:**
- **Color tokens**: Primary, secondary, tertiary, error, neutral shades
- **Spacing tokens**: Harmonious spacing scale for margins, padding, gaps
- **Typography tokens**: Font families, sizes, weights, line heights
- **Elevation tokens**: Shadow styles for depth and focus

### AEM Component System

**Available Beta Components:**
- Breadcrumb
- Button (Primary, Secondary, Ghost styles)
- Card
- Checkbox
- Link
- List group
- Radio button
- Tag

**Template Structure:**
```
Root Containers (built-in):
- Hero section Container
- Main content Container
- Bottom content Container (full width)

Component Library Access:
- Full library: Main body content containers
- Limited library: Bottom full-width containers
```

**Content Management Features:**
- Content Fragments: Page-independent, multi-channel content
- Experience Fragments: Grouped component experiences
- Workflows: Automated content management processes
- Publishing: Multi-stage content approval and publication

### Accessibility Standards

**Color Contrast Requirements:**
- Large text (18px+ or 14px+ bold): Minimum 3:1 contrast ratio
- Standard text (under 18px or under 14px bold): Minimum 4.5:1 contrast ratio
- Default text color: `on-surface` or `on-surface-variant`

**Interactive Elements:**
- All components must be keyboard navigable
- Support Tab navigation and Space/Enter activation
- Include appropriate ARIA labels and roles
- Maintain logical focus order

---

## Additional Implementation Resources

### External Links
- [Keystone Design System Figma Kit](https://www.figma.com/design/ac5bYA99KL6iBeFUSa9Y1V/Keystone-Design-System)
- [Font Package Download](https://wcmauthorguide.pa.gov/content/dam/copapwp-wcmauthorguide/en/global/files/KDS%20Fonts.zip)
- [KDS Feedback Form](https://forms.office.com/Pages/ResponsePage.aspx?id=QSiOQSgB1U2bbEf8Wpob3lTJtNR1BGhJhkpivjJ200JUNzdJWUxZSkQ4MkI2WERaQTRWVFBYUTRBNy4u) (PA.gov email required)
- [PA.gov Accessibility and Inclusion](https://wcmauthorguide.pa.gov/en/style-guide/accessibility-and-inclusion)
- [PA.gov Scannability](https://wcmauthorguide.pa.gov/en/style-guide/scannability)
- [PA.gov UX-friendly Content](https://wcmauthorguide.pa.gov/en/style-guide/best-practices-writing-ux-friendly-web-content)
- [PA.gov Trusted and Informed Agent](https://wcmauthorguide.pa.gov/en/style-guide/the-trusted-and-informed-agent)
- [PA.gov Writing for a 5th Grade Reading Level](https://wcmauthorguide.pa.gov/en/style-guide/writing-for-a-5th-grade-reading-level)
- [PA.gov Icon Library](https://wcmauthorguide.pa.gov/en/style-guide/icons)

### Getting Started with AEM
- User groups and permissions management
- Content authoring workflow
- Publishing and approval processes
- Component selection and customization
- Template framework utilization

---

*Note: The Keystone Design System is currently in beta. The PA.gov style guide remains strongly content-focused, so this prompt combines content guidance from the authoring guide with visual system details used for implementation planning. Revalidate component-level rules against the live authoring guide and Keystone assets before major UI refreshes.*
