---
layout: default
title: Border radius
parent: Foundations
nav_order: 4
---

# Border radius

Border radius defines how “soft” or “sharp” component corners appear. The current product already uses a small set of radii, but they are applied directly in CSS rather than through shared tokens. This page standardises those values into a clean radius scale based on the real patterns found in the existing Kahootz UI.

## Current usage in Kahootz

The legacy stylesheet contains the following radii:

- 2px — inputs, selects, fake checkboxes  
- 4px — content panels, menubars, dropdowns  
- 5px — a single toggle element  
- 6px — scrollbar thumb (WebKit only)  
- 9px — notification pill bubbles  
- 10px — special search input & search button  
- 50% — circular avatars

Only 2px, 4px, 10px, and pill/circle shapes are meaningful patterns; the rest are local exceptions.

## Radius tokens

    :root {
      --kz-radius-none: 0;
      --kz-radius-sm:   2px;
      --kz-radius-md:   4px;
      --kz-radius-lg:   10px;
      --kz-radius-round: 9999px;
      --kz-radius-circle: 50%;
    }

## Usage guidelines

### Buttons
    .kz-btn { border-radius: var(--kz-radius-sm); }

### Text inputs, selects, textareas
    .kz-input,
    input[type="text"],
    textarea,
    select { border-radius: var(--kz-radius-sm); }

### Cards, panels, menus, content containers
    .kz-card,
    .kz-panel,
    .in_menubar,
    .in_contentBody { border-radius: var(--kz-radius-md); }

### Special widgets (search / TBS)
    .in_tbsInput[type="text"],
    .in_tbsButton { border-radius: var(--kz-radius-lg); }

### Notification bubbles & counters
    .in_numberBox,
    .in_notificationDot { border-radius: var(--kz-radius-round); }

### Avatars
    .in_avatar { border-radius: var(--kz-radius-circle); }

## Token reference

| Token | Value |
|-------|--------|
| --kz-radius-none | 0 |
| --kz-radius-sm | 2px |
| --kz-radius-md | 4px |
| --kz-radius-lg | 10px |
| --kz-radius-round | 9999px |
| --kz-radius-circle | 50% |

## Mapping from existing CSS

- 2px → --kz-radius-sm  
- 4px → --kz-radius-md  
- 5px → nearest (sm or md)  
- 6px → scrollbar only  
- 9px → --kz-radius-round  
- 10px → --kz-radius-lg  
- 50% → --kz-radius-circle  

## Implementation notes

Adding tokens to the product is safe and non-breaking. When touching a component:

1. Replace raw radii with the nearest token  
2. Do not introduce new pixel radii  
3. Use these tokens for all new UI  

This creates consistency without a large refactor.