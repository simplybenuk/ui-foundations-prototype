---
layout: default
title: Shadows
parent: Foundations
nav_order: 6
---

# Shadows

Shadows (also called elevation) help communicate depth, layering and focus.  
The current Kahootz UI uses almost no shadows — only a few isolated cases such as editor elements — which makes this foundation lightweight and safe to introduce.

The aim is to:

- provide a consistent shadow scale,
- avoid one-off box-shadow declarations,
- support future components such as modals, popovers and dropdowns.

## Current usage in Kahootz

The legacy CSS contains almost *no* real shadows. The interface is mostly flat, which is fine, but limiting when building modern UI. Adding a shadow scale gives us controlled depth when needed without changing anything today.

## Shadow tokens

These tokens define a simple elevation scale:

    :root {
      --kz-shadow-none: none;

      --kz-shadow-sm: 
        0 1px 2px rgba(0, 0, 0, 0.06);

      --kz-shadow-md: 
        0 2px 4px rgba(0, 0, 0, 0.10);

      --kz-shadow-lg: 
        0 4px 10px rgba(0, 0, 0, 0.15);
    }

- **none** — default; matches the current Kahootz flat style  
- **sm** — subtle separation (dropdowns, small menus)  
- **md** — mid-level elevation (cards, popovers)  
- **lg** — major elevation (dialogs, modals)

## Usage guidelines

### Dropdowns / menus

    .kz-menu {
      box-shadow: var(--kz-shadow-sm);
    }

### Panels / cards

    .kz-card {
      box-shadow: var(--kz-shadow-md);
    }

### Modals / dialogs

    .kz-modal {
      box-shadow: var(--kz-shadow-lg);
    }

### Hover elevation (optional)

Use sparingly for interactive cards:

    .kz-card:hover {
      box-shadow: var(--kz-shadow-lg);
    }

## Token reference

| Token | Value | Use |
|-------|--------|-----|
| --kz-shadow-none | none | default, flat elements |
| --kz-shadow-sm | 0 1px 2px rgba(0,0,0,0.06) | small menus, tooltips |
| --kz-shadow-md | 0 2px 4px rgba(0,0,0,0.10) | cards, floating elements |
| --kz-shadow-lg | 0 4px 10px rgba(0,0,0,0.15) | dialogs, modal surfaces |

## Implementation notes

- Adding these tokens is non-breaking; nothing changes visually until components use them.
- Do not introduce new box-shadow values.
- When designing new components (dropdowns, modals, popovers), choose the closest shadow token.
- For accessibility, avoid overusing shadows as the only way to indicate depth. Combine elevation with clear borders or background contrast.