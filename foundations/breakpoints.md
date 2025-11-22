---
layout: default
title: Breakpoints
parent: Foundations
nav_order: 8
---

# Breakpoints

Breakpoints define the screen widths at which layouts can adapt.  
Kahootz is not fully responsive today, but documenting breakpoints now ensures all future UI changes use a consistent sizing model.

The goal is *not* to retrofit responsiveness immediately, but to establish the names and values that new components or features must use.

## Breakpoint tokens

These values follow common device ranges and give us a stable language for layout:

    :root {
      --kz-breakpoint-xs: 360px;   /* very small devices */
      --kz-breakpoint-sm: 480px;   /* small phones */
      --kz-breakpoint-md: 768px;   /* tablets / small desktops */
      --kz-breakpoint-lg: 1024px;  /* normal desktops */
      --kz-breakpoint-xl: 1280px;  /* large desktops / widescreens */
    }

These values do not change any existing layout until used in media queries.

## Usage guidelines

### Simple mobile adjustments

    @media (max-width: var(--kz-breakpoint-sm)) {
      .kz-hide-on-small {
        display: none;
      }
    }

### Stacking layouts on smaller screens

    @media (max-width: var(--kz-breakpoint-md)) {
      .kz-actions {
        flex-direction: column;
        gap: var(--kz-space-2);
      }
    }

### Widening layouts for large screens

    @media (min-width: var(--kz-breakpoint-lg)) {
      .kz-page {
        max-width: 1100px;
        margin: 0 auto;
      }
    }

## Breakpoint meanings

| Token | Value | Typical device range |
|-------|--------|----------------------|
| --kz-breakpoint-xs | 360px | small Android devices |
| --kz-breakpoint-sm | 480px | standard phones |
| --kz-breakpoint-md | 768px | tablets, small laptops |
| --kz-breakpoint-lg | 1024px | desktop (common width) |
| --kz-breakpoint-xl | 1280px | large desktop monitors |

These are not strict guarantees of layout behaviour today;  
they define the contract that **new** UI should follow.

## Implementation notes

- Adding breakpoints is safe — nothing changes until media queries reference them.
- When new components are designed, they should reference tokenised breakpoints rather than hard-coded px values.
- Do not introduce new pixel breakpoints; select the nearest existing token.

## Migration strategy

1. New pages or features: always use breakpoint tokens in media queries.
2. When editing old layouts: replace old @media values (e.g. 600px, 700px) with the closest token.
3. Long term: create responsive containers using the md and lg breakpoints.

This approach upgrades Kahootz towards modern responsive behaviour without a risky rewrite.