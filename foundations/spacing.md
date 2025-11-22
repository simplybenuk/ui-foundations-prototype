---
layout: default
title: Spacing
parent: Foundations
nav_order: 3
---

# Spacing

Spacing controls the gaps **inside** components (padding) and **between** components (margins).

Our current CSS uses many different pixel values (1, 2, 3, 4, 5, 6, 8, 10, 12, 15, 20, 25, 30, 32, 45, 55, 60, …). This works visually, but it makes the layout hard to reason about and hard to change safely.

This page defines a **simple spacing scale** that is close to our existing values and can be adopted gradually as we touch parts of the UI.

---

## Spacing scale

The spacing scale is defined in tokens:

    :root {
      --kz-space-1: 4px;
      --kz-space-2: 8px;
      --kz-space-3: 12px;
      --kz-space-4: 16px;
      --kz-space-5: 24px;
      --kz-space-6: 32px;
      --kz-space-7: 48px;
      --kz-space-8: 64px;
    }

This scale:

- sits close to the values already used in the legacy CSS, and  
- gives us a **shared language** for layout (e.g. “space sections with `--kz-space-5`”).

---

## What each step is for

### Inside components (padding)

- `--kz-space-1` (4px)  
  - Very tight content: icon + text spacing, chips, tiny counters.  
  - Fine adjustments inside dense components.

- `--kz-space-2` (8px)  
  - Button padding (vertical).  
  - Input padding (top/bottom).  
  - Small gaps between controls in a toolbar.

- `--kz-space-3` (12px)  
  - Button padding (horizontal) for medium buttons.  
  - Padding inside cards, panels and alerts.  
  - Vertical spacing between label and input.

### Between components (margins)

- `--kz-space-4` (16px)  
  - Space between standard form rows.  
  - Gap between stacked buttons and helper text.  
  - Space between elements in a dialog.

- `--kz-space-5` (24px)  
  - Space between groups of fields.  
  - Space between tables/cards and surrounding content.  
  - Vertical rhythm in content-heavy pages.

- `--kz-space-6` (32px)  
  - Separation between large sections on a page.  
  - Space above/below primary page titles or key call-to-action areas.

### Large layout spacing

- `--kz-space-7` (48px)  
  - Major section breaks on long pages.  
  - Large gaps between hero/header areas and main content.

- `--kz-space-8` (64px)  
  - Reserved for very large layout spacing (rarely used).  
  - Use sparingly to avoid excessive whitespace.

---

## Examples

### Buttons

    .kz-btn {
      padding: 0.35em 0.9em; /* existing style */
      /* could be normalised to tokens later as:
         padding: var(--kz-space-1) var(--kz-space-3); */
    }

When refactoring:

- Use `--kz-space-1` for vertical padding.  
- Use `--kz-space-3` for horizontal padding.

### Form fields

    .kz-form-row {
      margin-bottom: var(--kz-space-4); /* space between rows */
    }

    .kz-form-row label {
      display: block;
      margin-bottom: var(--kz-space-1); /* label to control */
    }

### Sections

    .kz-section {
      margin-bottom: var(--kz-space-5); /* between logical sections */
    }

    .kz-page-section--major {
      margin-bottom: var(--kz-space-6); /* big breaks */
    }

---

## Mapping from existing values

Many existing `px` values can be mapped onto this scale when code is touched.

Suggested mapping:

- 1–6px  ➜ `--kz-space-1`  
- 8–10px ➜ `--kz-space-2`  
- 11–13px ➜ `--kz-space-3`  
- 14–20px ➜ `--kz-space-4`  
- 21–28px ➜ `--kz-space-5`  
- 29–36px ➜ `--kz-space-6`  
- 45–55px ➜ `--kz-space-7`  
- 56px+   ➜ `--kz-space-8`

We do **not** need to clean up all existing spacing at once. The rule is:

> When a part of the UI is being changed anyway, prefer spacing tokens instead of new raw `px` values.

---

## Negative spacing

The legacy CSS includes a small number of **negative margins** to work around layout constraints.

Guidance:

- Avoid introducing new negative margins where possible.  
- If a layout appears to need a negative margin, consider:
  - adjusting the spacing of surrounding elements using tokens, or  
  - using flexbox/grid (for new work) instead of offset hacks.

Where negative margins must remain, they should be treated as **layout exceptions** and documented in the component or layout that uses them.

---

## Accessibility and spacing

Spacing affects readability and usability:

- Ensure form fields have enough vertical space (`--kz-space-4` or more) so they don’t blur together.  
- Maintain consistent gaps between related controls so users can visually group them.  
- Avoid crowding touch targets; small controls should still respect padding based on `--kz-space-2` and `--kz-space-3`.

When designing new layouts:

- Fewer, consistent spacing values are easier to scan than many slightly different gaps.  
- Use spacing to signal grouping (closer together) and separation (further apart).

---

## Using with frameworks (e.g. Bootstrap)

If a CSS framework is introduced later, these tokens can map onto its spacing utilities.

Examples:

    .kz-stack > * + * {
      margin-top: var(--kz-space-3);
    }

    .kz-stack-lg > * + * {
      margin-top: var(--kz-space-5);
    }

Framework-specific utilities (e.g. `mb-3`, `py-2`) should be used in a way that stays close to these values, or wrapped in helper classes that use the tokens.

---

## Implementation notes

Currently:

- Existing CSS uses many different `margin` and `padding` values.
- This scale is intentionally **compatible** with those values rather than forcing a radical change.

When editing or adding CSS:

1. Prefer spacing tokens from this page.  
2. Avoid introducing new raw `px` spacing values.  
3. Where you see odd values (e.g. `17px`, `23px`), consider whether they can safely be replaced by the nearest token.

Over time, this will make the layout more predictable and easier to change without regressions.