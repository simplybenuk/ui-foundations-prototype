---
layout: default
title: Colours
parent: Foundations
nav_order: 1
---

# Colours

Our colour system has two layers:

1. **System colours** – used for text, backgrounds, borders and status states (success, warning, error, info).
2. **Customer branding** – site-specific header and accent colours, applied via a separate stylesheet per branded site.

The goal is that customer branding **overrides** a small set of semantic colour tokens, rather than introducing new unmanaged colours.

---

## System colour tokens

These are the base colours the product is expected to support, regardless of branding.

    :root {
      /* Text */
      --kz-color-text-primary: #1f2933;
      --kz-color-text-muted:   #6b7280;
      --kz-color-text-inverse: #ffffff;

      /* Backgrounds */
      --kz-color-bg-page:      #ffffff;
      --kz-color-bg-surface:   #f5f5f5;

      /* Borders */
      --kz-color-border-subtle: #d4d4d8;
      --kz-color-border-strong: #6b7280;

      /* Accent + states */
      --kz-color-accent-primary:    #005ea5;
      --kz-color-accent-on-primary: #ffffff;
      --kz-color-success:           #00703c;
      --kz-color-warning:           #ffbf47;
      --kz-color-danger:            #d4351c;
    }

These are **semantic** tokens (what the colour is *for*), not brand colours like “blue” or “purple”.
Developers should reference these tokens instead of hard-coding hex values.

---

## Swatches

### Text & Background

| Token | Sample | Hex |
|---|---:|---|
| `--kz-color-text-primary` | <div style="width:40px;height:20px;background:#1f2933;border:1px solid #ddd;"></div> | `#1f2933` |
| `--kz-color-text-muted` | <div style="width:40px;height:20px;background:#6b7280;border:1px solid #ddd;"></div> | `#6b7280` |
| `--kz-color-bg-surface` | <div style="width:40px;height:20px;background:#f5f5f5;border:1px solid #ddd;"></div> | `#f5f5f5` |

### Accents & States

| Token | Sample | Hex |
|---|---:|---|
| `--kz-color-accent-primary` | <div style="width:40px;height:20px;background:#005ea5;border:1px solid #ddd;"></div> | `#005ea5` |
| `--kz-color-success` | <div style="width:40px;height:20px;background:#00703c;border:1px solid #ddd;"></div> | `#00703c` |
| `--kz-color-warning` | <div style="width:40px;height:20px;background:#ffbf47;border:1px solid #ddd;"></div> | `#ffbf47` |
| `--kz-color-danger` | <div style="width:40px;height:20px;background:#d4351c;border:1px solid #ddd;"></div> | `#d4351c` |

Swatches are for visual reference only — components must still use semantic tokens.

---

## Accessibility and contrast

To meet accessibility expectations (based on WCAG 2.1):

- **Body text and standard UI text** must have at least **4.5 : 1** contrast ratio against its background.
- **Large text** (18px regular or 14px bold and above) must have at least **3 : 1** contrast ratio.
- **Icons and UI indicators** that convey meaning (e.g. status dots, tag backgrounds, borders) must have at least **3 : 1** contrast against adjacent colours.
- Text placed over `--kz-color-accent-primary`, `--kz-color-success`, `--kz-color-warning` or `--kz-color-danger` must use a colour (usually `--kz-color-accent-on-primary` or `--kz-color-text-inverse`) that maintains the appropriate ratio.

Practical rules:

- When introducing a new colour token, **check contrast** against:
  - `--kz-color-bg-page` and `--kz-color-bg-surface` (for text),
  - and against `--kz-color-text-primary` (for badges, tags, buttons).
- If a brand colour does not meet contrast requirements, **adjust only the UI usage** (e.g. use it for borders or accents) rather than forcing it into text or primary button backgrounds.

Any new component design should explicitly confirm that its text and key UI elements meet these minimum contrast ratios.

---

## Customer branding

Each branded site can have its own stylesheet which **overrides** a small subset of the tokens above.

Example:

    /* Default brand */
    :root {
      --kz-color-accent-primary: #005ea5;
    }

    /* NHS-branded site */
    .kahootz-theme-nhs {
      --kz-color-accent-primary: #005eb8;
    }

    /* Local authority site */
    .kahootz-theme-la {
      --kz-color-accent-primary: #7a0177;
    }

Key principles:

- Themes **change tokens**, not component CSS.
- System colours like `--kz-color-success` and `--kz-color-danger` stay consistent across brands.
- New UI components must use semantic tokens, not new one-off colours.

This ensures branding flexibility **without fragmenting** the UI.

---

## Using with frameworks (e.g. Bootstrap)

If a framework is introduced later:

- Tokens remain the **source of truth**.
- Framework variables or utility classes can consume them, for example:

    :root {
      --kz-color-accent-primary: #005ea5;
    }

    .btn-primary {
      background-color: var(--kz-color-accent-primary);
      border-color:     var(--kz-color-accent-primary);
    }

The design system remains framework-agnostic while implementation details can evolve.

---

## Implementation notes: token-driven swatches

Currently, swatches are defined manually in this page.

In future, we can:

- Move token definitions into a data file (for example `_data/colours.yml`).
- Use the data file to **auto-generate swatch tables**, ensuring documentation always reflects the latest tokens.
- Use a single source of truth for:
  - token name,
  - hex value,
  - and usage notes.

Until that automation exists, any change to a colour token should update:

1. The token definition in CSS.
2. The corresponding swatch entry in this page.

---

## Usage guidelines

- Use `--kz-color-text-primary` for main content text.
- Use `--kz-color-text-muted` for secondary or supporting text.
- Use `--kz-color-accent-primary` for primary actions and key links.
- Use `--kz-color-bg-surface` for cards, panels and well backgrounds.
- Avoid introducing new colours — if something feels new, it likely needs a new semantic token.