---
layout: default
title: Borders
parent: Foundations
nav_order: 5
---

# Borders

Borders define edges between elements: input outlines, panel edges, list dividers and table lines.

The existing Kahootz CSS already uses a small set of border widths and styles, but they are hard-coded in many places:

- **1px solid** grey for most containers, inputs and dividers  
  - `#e0e0e0` for panels, menubars, content boxes  
  - `#bababa` for inputs and selects  
  - `#ccc` / `#aaa` for rules and tables 
- **5px solid** left border on blockquotes (visual call-outs) 1  
- **1px dotted** underline for acronyms 2  
- **1px dashed** outlines for TinyMCE table editing states 3  

This page defines a small set of **border tokens** that match those patterns and can be used by components instead of new ad-hoc values.

## Border tokens

:root {
      --kz-border-width-none: 0;
      --kz-border-width-thin: 1px;
      --kz-border-width-thick: 2px;
      --kz-border-width-heavy: 5px;

      --kz-border-style-default: solid;
      --kz-border-style-muted: dotted;
      --kz-border-style-helper: dashed;
    }

## Usage guidelines

### Containers and panels

    .kz-panel,
    .in_contentBody,
    .in_menubar {
      border-width: var(--kz-border-width-thin);
      border-style: var(--kz-border-style-default);
      border-color: var(--kz-color-border-subtle);
    }

### Inputs and fake inputs

    .kz-input,
    input[type="text"],
    textarea,
    select,
    .in_fakeInput {
      border-width: var(--kz-border-width-thin);
      border-style: var(--kz-border-style-default);
      border-color: var(--kz-color-border-subtle);
    }

### Dividers and list lines

    .kz-divider,
    .in_lineAndSpace > li,
    .in_notificationItem {
      border-top-width: var(--kz-border-width-thin);
      border-top-style: var(--kz-border-style-default);
      border-top-color: var(--kz-color-border-subtle);
    }

### Tables

    table.kz-grid,
    table.in_importwordtable,
    table.in_tableborder-outeronly,
    table.in_tableborder-columns,
    table.in_tableborder-rows {
      border-width: var(--kz-border-width-thin);
      border-style: var(--kz-border-style-default);
      border-color: var(--kz-color-border-strong);
    }

### Call-outs (blockquotes)

    blockquote {
      border-left-width: var(--kz-border-width-heavy);
      border-left-style: var(--kz-border-style-default);
      border-left-color: var(--kz-color-border-strong);
    }

### Dotted and dashed helpers

    .in_acronym {
      border-bottom-width: var(--kz-border-width-thin);
      border-bottom-style: var(--kz-border-style-muted);
      border-bottom-color: var(--kz-color-border-strong);
    }

    .mce-content-body table[data-mce-selected] {
      border-width: var(--kz-border-width-thin);
      border-style: var(--kz-border-style-helper);
      border-color: var(--kz-color-border-subtle);
    }

---

## 🔹 CHUNK 3 – Reference + mapping + implementation

```markdown
## Token reference

| Token | Value | Typical use |
|-------|-------|-------------|
| `--kz-border-width-none` | `0` | no visible border |
| `--kz-border-width-thin` | `1px` | default for inputs, panels, tables, dividers |
| `--kz-border-width-thick` | `2px` | stronger outlines / focus if needed |
| `--kz-border-width-heavy` | `5px` | blockquote / major call-outs |
| `--kz-border-style-default` | `solid` | normal borders |
| `--kz-border-style-muted` | `dotted` | subtle underlines (acronyms, hints) |
| `--kz-border-style-helper` | `dashed` | editor helpers / selection states |

## Mapping from existing CSS

When you touch existing code:

- `border: 1px solid #e0e0e0` → thin + default + `--kz-color-border-subtle`  
- `border: 1px solid #bababa` → thin + default + input/neutral border token  
- `border-top: 1px solid #e0e0e0` → divider using thin + default + subtle  
- `border: 1px solid #aaa` or `#ccc` → thin + default + strong/subtle depending on context  
- `border-left: 5px solid #999` → heavy + default + strong  
- `border-bottom: 1px dotted #999` → thin + muted + strong  
- `border: 1px dashed #bbb` → thin + helper + subtle  

Avoid adding new one-off border widths or styles. If a genuinely new pattern is needed, add a token here first.

## Implementation notes

- Introducing these tokens is **non-breaking** until components adopt them.  
- New or refactored components should use width + style tokens and border colours from the Colours foundation.  
- Over time this will reduce the variety of one-off border declarations and make it easier to evolve the visual style (for example, lightening borders or adjusting thickness) in one place.

The general rule:

> When you’re already changing a component, replace raw `border` values with tokens instead of adding more ad-hoc CSS.