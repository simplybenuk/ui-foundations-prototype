---
layout: default
title: Buttons
parent: Components
nav_order: 1
---

# Buttons

Buttons trigger actions: saving changes, submitting forms, starting workflows or navigating to key destinations.

They should:

- use a small set of **clear variants**,
- look and behave consistently across the product,
- and always be identifiable as interactive elements.

This page describes the current approach to buttons and how they map onto the **Colours** and **Typography** foundations.

---

## Variants

We support the following button types:

- **Primary** – main action on a page or in a dialog (e.g. “Save”, “Continue”).
- **Secondary** – less prominent actions (e.g. “Cancel”, “Back”, “Done”).
- **Destructive** – actions that delete or remove data (e.g. “Delete”, “Remove user”).
- **Disabled** – non-interactive state when an action is not currently available.

Each variant uses the same basic anatomy and layout, changing only colour and (sometimes) border style.

---

## Anatomy

A standard button contains:

1. Container – the clickable area (hit target).
2. Label – the action text.
3. Optional icon – placed before or after the label (if used consistently).

Buttons must:

- use the **same font** and **base size**,
- have enough padding for a comfortable hit target,
- and have a visible focus outline for keyboard users.

---

## Base styles (proposed mapping)

These styles are expressed using tokens from **Colours** and **Typography**.  
You can map these onto your existing button classes.

    /* Base button */

    .kz-btn {
      display: inline-block;
      padding: 0.35em 0.9em;
      border-radius: 3px; /* could later become --kz-radius-md */
      border-width: 1px;
      border-style: solid;

      font-family: var(--kz-font-family-base);
      font-size:   var(--kz-font-size-sm);      /* 14px - compact UI text */
      line-height: var(--kz-line-height-body);
      font-weight: var(--kz-font-weight-regular);

      cursor: pointer;
      text-decoration: none;
      text-align: center;
      white-space: nowrap;

      /* default colours; specific variants override these */
      background-color: var(--kz-color-bg-surface);
      border-color:     var(--kz-color-border-subtle);
      color:            var(--kz-color-text-primary);
    }

    .kz-btn + .kz-btn {
      margin-left: 0.5em;
    }

This base style should feel close to your current “default” buttons, but expressed through tokens.

---

## Primary button

Used for the main action in a context. There should usually be only **one primary button per container** (dialog, form, panel).

    .kz-btn-primary {
      background-color: var(--kz-color-accent-primary);
      border-color:     var(--kz-color-accent-primary);
      color:            var(--kz-color-text-inverse);
    }

    .kz-btn-primary:hover {
      background-color: #002864; /* slightly darker than accent */
      border-color:     #002864;
    }

    .kz-btn-primary:active {
      background-color: #001f4d;
      border-color:     #001f4d;
    }

    .kz-btn-primary:disabled,
    .kz-btn-primary[disabled] {
      opacity: 0.6;
      cursor: default;
    }

Usage:

- Use for the **single most important** action on a page or dialog.
- Avoid having more than one primary button next to each other.
- Do not use to represent destructive actions; use a dedicated destructive variant.

---

## Secondary button

Used for actions that are available but not the main focus.

    .kz-btn-secondary {
      background-color: var(--kz-color-bg-surface);
      border-color:     var(--kz-color-border-strong);
      color:            var(--kz-color-text-primary);
    }

    .kz-btn-secondary:hover {
      background-color: #f0f0f0;
    }

    .kz-btn-secondary:active {
      background-color: #e2e2e2;
    }

Usage:

- “Cancel”, “Back”, “Close”, “View details”.
- Supporting actions in toolbars or below tables.

---

## Destructive button

Used for delete/remove actions where data is permanently removed or hard to undo.

    .kz-btn-destructive {
      background-color: var(--kz-color-notification-dot); /* red tone */
      border-color:     var(--kz-color-notification-dot);
      color:            var(--kz-color-text-inverse);
    }

    .kz-btn-destructive:hover {
      background-color: #b22222;
      border-color:     #b22222;
    }

    .kz-btn-destructive:active {
      background-color: #891919;
      border-color:     #891919;
    }

Usage:

- Only for clearly destructive actions (delete record, remove member).
- Prefer to pair with a **confirmation step** (dialog) for high-impact actions.
- Do not use purely for “warning” – use messages/alerts for that.

---

## Disabled state

Buttons may be disabled when:

- preconditions are not met (e.g. required fields empty),
- an action is not available for a particular item.

Disabled buttons must:

- appear visually distinct from enabled buttons,
- not respond to hover or click,
- remain readable but clearly “muted”.

    .kz-btn:disabled,
    .kz-btn[disabled] {
      opacity: 0.6;
      cursor: default;
    }

Avoid using disabled buttons as the only explanation for why an action is unavailable – pair them with:

- inline validation,
- helper text near the control,
- or tooltip-style explanations.

---

## Focus and keyboard access

All buttons must:

- be reachable via `Tab` / `Shift+Tab`,
- show a **visible focus outline** distinct from hover.

Example focus styling:

    .kz-btn:focus-visible {
      outline: 2px solid var(--kz-color-accent-primary);
      outline-offset: 2px;
    }

Guidelines:

- Do not remove focus outlines.
- If custom focus styles are needed, they must be at least as visible as the browser default.
- When buttons are part of a dialog or wizard, ensure focus is moved appropriately when the dialog opens and closes.

---

## Layout and spacing

Buttons should:

- have enough padding to feel clickable without being crowded,
- align consistently in forms and dialogs.

Recommended spacing:

- Horizontal padding: `0.9em`
- Vertical padding: `0.35em`
- Space between buttons in a group: `0.5em` (left margin on subsequent buttons)
- Align primary action to the **right** of secondary actions in dialogs (or follow existing established Kahootz pattern).

---

## Accessibility checklist

For every new button or button layout:

- [ ] The control is a real `<button>` element (or `role="button"` with full keyboard support).
- [ ] The label describes the action (avoid vague labels like “OK” where possible).
- [ ] The button can be reached and activated via keyboard.
- [ ] Focus state is clearly visible.
- [ ] Colour contrast between text and background meets the requirements in **Colours**.
- [ ] Destructive actions use the destructive style and, for high-risk operations, a confirmation step.

---

## Mapping to existing implementation

Where existing CSS already defines button styles (e.g. legacy `.button`, `.submit`, `.saveButton` classes), the recommended approach is:

1. Map each existing class onto one of the variants above (primary, secondary, destructive).
2. Gradually replace direct hex colours with the tokens from **Colours**.
3. Avoid adding new one-off button styles; extend these variants instead.

Examples:

- `.saveButton` → `.kz-btn kz-btn-primary`
- `.cancelButton` → `.kz-btn kz-btn-secondary`
- `.deleteButton` → `.kz-btn kz-btn-destructive`

This allows the visual system to be improved over time without forcing a large, risky rewrite.