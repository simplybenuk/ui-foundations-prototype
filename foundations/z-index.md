---
layout: default
title: Z-index
parent: Foundations
nav_order: 7
---

# Z-index

Z-index defines how elements stack above or below each other.  
The Kahootz CSS includes several one-off values such as 2, 3, 5, 9, 10 and higher editor-related values (e.g. TinyMCE overlays). These work locally but make global layering unpredictable.

This foundation introduces a clear stacking scale so future components (menus, dialogs, drawers, notifications) all sit at consistent layers.

## Current usage in Kahootz

The legacy CSS includes:

- 2 / 3 — layout nudge elements  
- 5 — header and content tools  
- 9 / 10 — dropdowns, toolbars, overlays  
- Large editor z-index values inside TinyMCE (handled separately)

These values suggest roughly four real layers.

## Z-index tokens

A simple stack that matches the real layering in Kahootz:

    :root {
      --kz-z-base:        1;      /* normal content */
      --kz-z-sticky:      100;    /* sticky headers, toolbars */
      --kz-z-dropdown:    500;    /* menus, popovers */
      --kz-z-overlay:     1000;   /* modal backdrops */
      --kz-z-modal:       1100;   /* dialogs, modals */
      --kz-z-toast:       1200;   /* notifications */
    }

Why these values:

- jumps are large enough to avoid accidental overlap  
- no insane numbers (9999), just predictable layers  
- drop-in replacement when touching old code

## Usage guidelines

### Base content

Most elements should not specify z-index at all:

    .kz-page,
    .kz-card,
    .kz-section {
      z-index: var(--kz-z-base);
    }

### Sticky headers / toolbars

Equivalent to existing 5–9 in legacy CSS:

    .kz-toolbar,
    .kz-sticky-header {
      z-index: var(--kz-z-sticky);
    }

### Dropdowns / menus

Used for TBS dropdowns, toolbar menus, popovers:

    .kz-dropdown,
    .kz-menu {
      z-index: var(--kz-z-dropdown);
    }

### Overlays

Dimmed backgrounds behind dialogs:

    .kz-overlay {
      z-index: var(--kz-z-overlay);
    }

### Modals / dialogs

Front-most interactive layer:

    .kz-modal {
      z-index: var(--kz-z-modal);
    }

### Toasts / notifications

Notifications should sit above modals:

    .kz-toast {
      z-index: var(--kz-z-toast);
    }

## Token reference

| Token | Value | Purpose |
|-------|--------|---------|
| --kz-z-base | 1 | normal content |
| --kz-z-sticky | 100 | sticky toolbars / headers |
| --kz-z-dropdown | 500 | menus, popovers, dropdowns |
| --kz-z-overlay | 1000 | modal backdrop layer |
| --kz-z-modal | 1100 | dialogs, modals |
| --kz-z-toast | 1200 | toasts, alerts, notifications |

## Mapping from existing CSS

- z-index: 2 → use base  
- z-index: 3 → base or sticky depending on element  
- z-index: 5 → sticky  
- z-index: 9 → dropdown  
- z-index: 10 → dropdown or overlay depending on context  
- z-index: 99+ → usually modal-related, map to modal or toast  
- TinyMCE editor values → keep isolated; do not tokenise

## Implementation notes

- Adding tokens is safe; nothing changes until applied.
- When touching old code, replace raw values with tokens.
- Avoid introducing new numerical z-index values.
- Keep the stack simple: if something must sit above another element, choose the next token up rather than inventing `z-index: 47`.

Over time this will eliminate stacking bugs and make overlays, modals, and dropdowns predictable.