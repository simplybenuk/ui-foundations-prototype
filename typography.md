---
layout: default
title: Typography
parent: Foundations
nav_order: 2
---

# Typography

Typography defines the core rules for how text appears across the product: font families, sizes, weights and line heights.

This page starts by reflecting the **current implementation**, then wraps it in tokens so we can evolve in a controlled way later (e.g. adjusting sizes, moving to a system font stack, or integrating with a framework).

---

## Current type tokens

The existing CSS uses a 15px base size on `<body>`, with headings defined as percentages of that size.

To make this easier to reason about, we express the current behaviour as tokens:

    :root {
      /* Font families (current) */
      --kz-font-family-base: Arial, "Lucida Grande", sans-serif;
      --kz-font-family-mono: monospace;

      /* Base body size */
      --kz-font-size-body: 15px;

      /* Heading sizes (approximate pixel values from current percentages) */
      --kz-font-size-h1: 28px; /* ~185% of 15px */
      --kz-font-size-h2: 23px; /* ~155% of 15px */
      --kz-font-size-h3: 20px; /* ~135% of 15px */
      --kz-font-size-h4: 19px; /* ~125% of 15px (used for h4–h6) */

      /* UI / utility sizes */
      --kz-font-size-xs: 12px; /* badges, number pills, very small UI text */
      --kz-font-size-sm: 14px; /* 95% of body – notes, small meta text */
      --kz-font-size-md: 15px; /* main body text (current default) */

      /* Line heights */
      --kz-line-height-body:    1.5;
      --kz-line-height-heading: 1.15;

      /* Weights */
      --kz-font-weight-regular: 400;
      --kz-font-weight-bold:    700;
    }

These token values are intentionally close to the existing CSS rather than “nice” round rem values. Once the system is in use, we can normalise them (e.g. move to a rem-based scale) as a separate change.

---

## Core styles (as implemented today)

### Body text

Current behaviour, expressed using tokens:

    body {
      font-family: var(--kz-font-family-base);
      font-size:   var(--kz-font-size-md);      /* 15px */
      line-height: var(--kz-line-height-body);  /* 1.5 */
      font-weight: var(--kz-font-weight-regular);
      color:       var(--kz-color-text-primary);
    }

Usage:

- Main content and descriptive text.
- Forms, long descriptions, help copy.

### Headings

All headings currently share the same colour, weight and line-height:

    h1,
    h2,
    h3,
    h4,
    h5,
    h6 {
      color:       #313c44;
      font-weight: normal;
      line-height: var(--kz-line-height-heading);
    }

Sizing with tokens:

    h1 {
      font-size: var(--kz-font-size-h1);
      margin: 1em 0 0.5em 0;
    }

    h2 {
      font-size: var(--kz-font-size-h2);
      margin: 1em 0 0.5em 0;
    }

    h3 {
      font-size: var(--kz-font-size-h3);
      margin: 0.5em 0 0.5em 0;
    }

    h4,
    h5,
    h6 {
      font-size: var(--kz-font-size-h4);
      margin: 0.5em 0 0.5em 0;
    }

Suggested semantic usage (even if the CSS is shared):

- **H1** – page titles.
- **H2** – main sections within a page.
- **H3** – subsections.
- **H4–H6** – rare; only when deeply nesting content.

Headings should follow semantic order (H1 → H2 → H3) rather than being picked purely for how they look.

### UI labels, meta text and badges

Some existing patterns introduce smaller sizes:

- `.small-note` and `.in_poweredBy` use ~95% of body size (≈ 14px) for secondary notes.
- `.in_numberBox`, `.in_notificationDot` and similar badges use `12px` for compact status text.

Expressed with tokens:

    .kz-meta,
    .small-note {
      font-size:   var(--kz-font-size-sm);  /* ~14px */
      line-height: var(--kz-line-height-body);
      color:       var(--kz-color-text-muted);
    }

    .kz-badge,
    .in_numberBox,
    .in_notificationDot {
      font-size:   var(--kz-font-size-xs);  /* 12px */
      line-height: 1;
      font-weight: var(--kz-font-weight-regular);
    }

Guidance:

- Use `--kz-font-size-sm` for helper text, footnotes and low-priority meta.
- Use `--kz-font-size-xs` only where space is very constrained (badges, counts, notification dots).

### Code and technical values

Current CSS:

    pre,
    code {
      font-family: monospace;
    }

Token-based equivalent:

    pre,
    code,
    .kz-monospace {
      font-family: var(--kz-font-family-mono);
      font-size:   var(--kz-font-size-sm);
      line-height: var(--kz-line-height-body);
    }

Use the monospace family for:

- Code snippets.
- IDs or reference numbers that benefit from alignment.
- Highly technical values (e.g. IP addresses).

---

## Token reference

### Font families

- `--kz-font-family-base` – **current** base stack: `Arial, "Lucida Grande", sans-serif`.  
  - This reflects the legacy implementation and is safe across browsers.
  - In future we may replace this with a system-font stack while keeping the token name.
- `--kz-font-family-mono` – generic monospace for code and technical text.

### Font sizes

- `--kz-font-size-xs` (12px) – badges, counters, notification dots.
- `--kz-font-size-sm` (~14px) – notes, small meta text, footer text.
- `--kz-font-size-md` (15px) – main body text (current default).
- `--kz-font-size-h4` (~19px) – smaller headings (used for H4–H6).
- `--kz-font-size-h3` (~20px) – sub-section headings.
- `--kz-font-size-h2` (~23px) – section headings.
- `--kz-font-size-h1` (~28px) – page titles.

### Line heights

- `--kz-line-height-body` (1.5) – all body and UI text.
- `--kz-line-height-heading` (1.15) – headings, group titles.

---

## Accessibility guidelines

- Minimum size for **body text**: `--kz-font-size-md` (15px) on desktop; avoid going below this except in dense UI elements such as badges.
- Minimum size for **UI labels and buttons**: `--kz-font-size-sm` (~14px).
- Avoid relying solely on **colour or weight** for emphasis; combine size, weight and spacing.
- Ensure text always uses colours that satisfy the **contrast rules** defined in the Colours foundation.

If new layouts require smaller sizes, they should be treated as design exceptions and explicitly reviewed.

---

## Using with frameworks (e.g. Bootstrap)

If we introduce a CSS framework later, these tokens remain the **source of truth** and the framework maps onto them:

    body {
      font-family: var(--kz-font-family-base);
      font-size:   var(--kz-font-size-md);
    }

    .h1, h1 {
      font-size:   var(--kz-font-size-h1);
      line-height: var(--kz-line-height-heading);
    }

    .badge,
    .kz-badge {
      font-size:   var(--kz-font-size-xs);
    }

This keeps the visual system stable even if the underlying toolkit changes.

---

## Future improvements

These changes are **not** in the product yet, but are likely future directions:

- Move from px to a **rem-based scale** for better browser scaling.
- Replace the legacy `Arial` stack with a **system font stack** while keeping `--kz-font-family-base` as the interface.
- Introduce a clearer, named type scale (e.g. `--kz-font-size-2xl`, `--kz-font-size-xl`, etc.) and map H1–H4 onto it.

Those evolutions can happen incrementally, with this page acting as the contract for what typography should do.