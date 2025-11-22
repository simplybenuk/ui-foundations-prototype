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

The goal is that customer branding **overrides** a small set of semantic colour tokens, rather than introducing totally new ad-hoc colours.

---

## System colour tokens

These are the base colours the product expects to exist, regardless of branding.

```css
:root {
  /* Text */
  --color-text-primary: #1f2933;
  --color-text-muted:   #6b7280;
  --color-text-inverse: #ffffff;

  /* Backgrounds */
  --color-bg-page:      #ffffff;
  --color-bg-surface:   #f5f5f5;

  /* Borders */
  --color-border-subtle:   #d4d4d8;
  --color-border-strong:   #6b7280;

  /* Accent + states */
  --color-accent-primary:          #005ea5;
  --color-accent-on-primary:       #ffffff;
  --color-success:                 #00703c;
  --color-warning:                 #ffbf47;
  --color-danger:                  #d4351c;
}