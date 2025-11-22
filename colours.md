---
layout: default
title: Colours
parent: Foundations
nav_order: 1
---

# Colours

This page documents the **current colour behaviour** in the product and expresses it as semantic tokens so we can evolve it safely over time.

Right now, most colours are hard-coded hex values in the CSS (e.g. `#333`, `#313c44`, `#038`, `#ffc13c`). The goal of this foundation is to:

- define a **core palette** that reflects how the UI already looks, and  
- give us a way to **gradually migrate** legacy colours onto named tokens.

---

## Core tokens (current behaviour)

The existing CSS uses:

- `body` text colour: `#333`
- heading text colour: `#313c44`
- page background: `#eaebec`
- main surfaces (header, content panels): `#fff`
- subtle borders: `#e0e0e0`
- strong borders / dividers: `#999`
- links: `#038`
- top bar: `#ffc13c`
- number badges: `#3a87ad`
- notification dots: `#d33`

We wrap those in semantic tokens:

    :root {
      /* Text */
      --kz-color-text-primary:  #333333;  /* body text */
      --kz-color-text-heading:  #313c44;  /* headings, group bars */
      --kz-color-text-muted:    #666666;  /* secondary text */
      --kz-color-text-subtle:   #999999;  /* low priority meta, hints */
      --kz-color-text-inverse:  #ffffff;  /* text on dark/strong backgrounds */

      /* Backgrounds */
      --kz-color-bg-page:       #eaebec;  /* overall page background */
      --kz-color-bg-surface:    #ffffff;  /* cards, header panels */

      /* Borders & dividers */
      --kz-color-border-subtle: #e0e0e0;
      --kz-color-border-strong: #999999;

      /* Accents & brand */
      --kz-color-accent-primary:   #003388;  /* links etc. (current #038 approximated to full hex) */
      --kz-color-accent-header:    #ffc13c;  /* top bar background */
      --kz-color-accent-groupbar:  #313c44;  /* group bar background */

      /* Status / notifications (current usage) */
      --kz-color-badge-default:    #3a87ad;  /* number pills, counters */
      --kz-color-notification-dot: #d33333;  /* red notification dot */
    }

These values are deliberately close to the current implementation. Later changes (e.g. refined palette, extra states) should update the tokens, not reintroduce raw hex values into components.

---

## Token reference (with swatches)

### Text

- `--kz-color-text-primary` – `#333333`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#333333;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-text-heading` – `#313c44`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#313c44;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-text-muted` – `#666666`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#666666;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-text-subtle` – `#999999`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#999999;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-text-inverse` – `#ffffff`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#ffffff;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

### Backgrounds

- `--kz-color-bg-page` – `#eaebec`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#eaebec;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-bg-surface` – `#ffffff`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#ffffff;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

### Borders

- `--kz-color-border-subtle` – `#e0e0e0`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#e0e0e0;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-border-strong` – `#999999`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#999999;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

### Accents & brand

- `--kz-color-accent-primary` – `#003388` (current links `#038` normalised)
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#003388;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-accent-header` – `#ffc13c`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#ffc13c;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-accent-groupbar` – `#313c44`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#313c44;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

### Status / notifications

- `--kz-color-badge-default` – `#3a87ad`
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#3a87ad;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

- `--kz-color-notification-dot` – `#d33333` (normalised from `#d33`)
  <span style="display:inline-block;width:1.2em;height:1.2em;background:#d33333;border:1px solid #ddd;margin-left:0.5em;vertical-align:middle;"></span>

Swatches are for visual reference only — components must still use the semantic token names.

---

## Accessibility and contrast

To meet accessibility expectations (based on WCAG 2.1):

- **Body text and standard UI text** must have at least **4.5 : 1** contrast against their background.
- **Large text** (18px regular or 14px bold and above) must have at least **3 : 1** contrast.
- Icons and status indicators (badges, dots, tags) must have at least **3 : 1** contrast against adjacent colours.
- Text on strong backgrounds (e.g. header bar, badges, dots) must use `--kz-color-text-inverse` or another colour that meets the ratio.

When adding or changing colours:

- Check contrast against `--kz-color-bg-page` and `--kz-color-bg-surface` for text.
- Check contrast against `--kz-color-text-primary` for badges and filled components.
- If a client brand colour fails contrast, use it as a **supporting accent** (border, stripe, icon) rather than body text or primary button background.

---

## Customer branding

Today, customer branding is handled via **site-specific stylesheets** that tweak header and accent colours.

Going forward, the recommendation is that branded styles:

- **Override tokens**, not component CSS.
- Limit themselves to a small set of brand-related tokens such as:

    :root {
      /* Default / Kahootz brand */
      --kz-color-accent-primary: #003388;
      --kz-color-accent-header:  #ffc13c;
    }

    .kahootz-theme-nhs {
      --kz-color-accent-primary: #005eb8; /* example */
      --kz-color-accent-header:  #005eb8;
    }

    .kahootz-theme-la {
      --kz-color-accent-primary: #7a0177;
      --kz-color-accent-header:  #7a0177;
    }

System colours like `--kz-color-text-primary`, `--kz-color-text-muted` and `--kz-color-border-subtle` should remain consistent across brands so that layout and meaning stay predictable.

---

## Using with frameworks (e.g. Bootstrap)

If a CSS framework is introduced later, these tokens remain the **source of truth** and the framework maps onto them:

    :root {
      --kz-color-accent-primary: #003388;
    }

    a,
    .btn-link {
      color: var(--kz-color-accent-primary);
    }

    .btn-primary {
      background-color: var(--kz-color-accent-primary);
      border-color:     var(--kz-color-accent-primary);
      color:            var(--kz-color-text-inverse);
    }

This keeps the visual language stable even if the underlying toolkit changes.

---

## Implementation notes

Right now:

- Many additional hex colours exist in the legacy CSS.
- Only the **most widely used structural and accent colours** have tokens.

As we touch parts of the UI, we should:

1. Identify any direct hex colours being used.
2. Map them to an existing token **or** (if truly new) add a new semantic token here.
3. Remove the raw hex value from component CSS.

Over time this will reduce the number of “mystery colours” and make branding changes and theme work safer.

---

## Usage guidelines

When adding or updating UI:

- Use `--kz-color-text-primary` for main content text.
- Use `--kz-color-text-muted` or `--kz-color-text-subtle` for secondary/meta text.
- Use `--kz-color-accent-primary` for links and key interactive accents.
- Use `--kz-color-bg-surface` for panels, cards and content containers.
- Avoid introducing new hex colours directly in components – add or reuse a token instead.