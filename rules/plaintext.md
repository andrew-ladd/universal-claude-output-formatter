# Plain text formatting rules

Plain text targets environments that render no markup at all — Slack compose box, email clients, terminal output, SMS, plain notes. No syntax characters will be interpreted; everything must communicate through spacing, capitalization, and ASCII conventions.

## Core principle

Structure through layout, not syntax. Use whitespace and capitalization to create visual hierarchy.

## Headings

Use ALL CAPS on its own line. For top-level headings, follow with a line of dashes equal to the heading length. For sub-headings, skip the underline.

```
DEPLOY CHECKLIST FOR V2.3.0
============================

STEPS

NOTES
```

## Emphasis

- Bold → ALL CAPS for individual words or short phrases. Use sparingly or the effect dilutes.
- Italic → omit, or rewrite the sentence so emphasis is carried by word choice.
- Strikethrough → remove or rewrite as "(removed)" / "(deprecated)".

```
Set the PORT to 8080 by DEFAULT.
```

## Lists

Use `•` for bullets. Indent nested items with 2 spaces and use `-` to distinguish the level.

```
• First item
• Second item
  - Nested child
  - Another nested child
• Third item
```

Numbered lists — use plain numbers:

```
1. Step one
2. Step two
3. Step three
```

## Code and inline code

For inline code, wrap in backticks if the context will show them literally (e.g. Slack compose), or just leave as plain text with no markers — rely on context:

```
Run npm run migrate:prod to start the migration.
```

For code blocks, indent 4 spaces and add a blank line before and after:

```
    function add(a, b) {
      return a + b;
    }
```

If the block needs a label, add a plain-text heading above it:

```
EXAMPLE:

    git checkout v2.2.9
    npm run deploy
```

## Links

Write display text followed by the URL in parentheses:

```
See the release plan (https://example.com/releases/v2.3.0) for full context.
```

If the URL is the display text, just write it bare:

```
https://example.com
```

Do not use any bracket or angle-bracket syntax.

## Blockquotes

Prefix each line with `> ` (greater-than + space):

```
> If anything goes wrong, revert using the tag v2.2.9
> and open an incident ticket.
```

## Tables

Represent as labeled lines — one item per line, label in ALL CAPS followed by a colon:

```
RISK: Migration timeout
LIKELIHOOD: Medium
MITIGATION: Run during low-traffic window

RISK: Auth regression
LIKELIHOOD: Low
MITIGATION: Covered by e2e suite
```

For compact tables with few columns, use a separator:

```
Migration timeout  |  Medium  |  Run during low-traffic window
Auth regression    |  Low     |  Covered by e2e suite
```

Align columns manually when the table is short enough to scan.

## Horizontal dividers

Use a line of dashes for section breaks:

```
---
```

Or a longer run for major breaks:

```
------------------------------------------------------------
```

## Length guidance

Plain text has no hard limits. Structure long content with ALL CAPS headings and clear blank lines between sections so it remains scannable when rendered in a fixed-width font.
