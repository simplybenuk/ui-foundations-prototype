---
layout: default
title: Colours
parent: Foundations
nav_order: 1
---

# Colours

Our colour system has two layers:

1. **System colours** – used for text, backgrounds, borders and status messages (success, warning, error, info).
2. **Customer branding** – site-specific headers and accent colours, applied via a separate stylesheet per branded site.

The goal is that customer branding **overrides** a small set of semantic colour tokens, rather than introducing new unmanaged colours.

---

## System colour tokens

These are the base colours the product is expected to support, regardless of branding.

    :root {
      /* Text */
      --color-text-primary: #1f2933;
      --color-text-muted:   #6b7280;
      --color-text-inverse: #ffffff;

      /* Backgrounds */
      --color-bg-page:      #ffffff;
      --color-bg-surface:   #f5f5f5;

      /* Borders */
      --color-border-subtle: #d4d4d8;
      --color-border-strong: #6b7280;

      /* Accent + states */
      --color-accent-primary:    #005ea5;
      --color-accent-on-primary: #ffffff;
      --color-success:           #00703c;
      --color-warning:           #ffbf47;
      --color-danger:            #d4351c;
    }

These are **semantic** tokens (what the colour is *for*), not brand colours like “blue” or “purple”.
Developers should reference these tokens instead of hard-coding hex values.

---

## Customer branding

Each branded site can have its own stylesheet which **overrides** a small subset of the tokens above.

Example:

    /* Default brand */
    :root {
      --color-accent-primary: #005ea5;
    }

    /* NHS-branded site */
    .kahootz-theme-nhs {
      --color-accent-primary: #005eb8;
    }

    /* Local authority site */
    .kahootz-theme-la {
      --color-accent-primary: #7a0177;
    }

Key principles:

- Themes **change tokens**, not component CSS.
- System colours like `--color-success` and `--color-danger` stay consistent across brands.
- New UI components must use semantic tokens, not new one-off colours.

This ensures branding flexibility **without fragmenting** the UI.

---

## Usage guidelines

- Use `--color-text-primary` for main content text.
- Use `--color-text-muted` for secondary or supporting text.
- Use `--color-accent-primary` for primary actions and key links.
- Use `--color-bg-surface` for cards, panels and well backgrounds.
- Avoid introducing new colours — if something feels new, it likely needs a new semantic token.

---

## Future improvements

- Document light vs dark variants (if introduced)
- Define contrast requirements for accessibility
- Add swatches to visually preview tokens