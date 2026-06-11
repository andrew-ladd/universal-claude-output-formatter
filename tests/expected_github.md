# Expected output: GitHub

Destination: GitHub Flavored Markdown
Source: [input_mixed.md](input_mixed.md)

---

## Overview

This is a **bold** statement with *italic* emphasis and some ~~strikethrough~~ text.

Inline code: `const x = 42;` — should survive in all destinations.

A [link to the docs](https://example.com/docs) and a bare URL: https://example.com

---

## Bullet list

- First item
- Second item
  - Nested child
  - Another nested child
- Third item

## Numbered list

1. Step one
2. Step two
3. Step three

---

## Code block

```javascript
function add(a, b) {
  // This comment must be preserved exactly
  return a + b;
}
```

---

## Blockquote

> This is a quoted passage.
> It spans two lines.

---

## Table

| Column A | Column B | Column C |
|----------|----------|----------|
| Alpha    | 1        | Yes      |
| Beta     | 2        | No       |
| Gamma    | 3        | Maybe    |

---

## Mixed paragraph

The service runs on **port 8080** by default. To override, set `PORT=9000` before starting. See [configuration guide](https://example.com/config) for all options.

> Warning: do not expose port 8080 publicly without authentication.

---

## Acceptance notes

- [ ] All GFM constructs preserved as-is (source is already GFM-compatible)
- [ ] `**bold**`, `*italic*`, `~~strikethrough~~` preserved
- [ ] `` `inline code` `` preserved
- [ ] `[text](url)` links preserved
- [ ] Fenced code block with language tag preserved
- [ ] `> blockquote` preserved
- [ ] Table preserved with alignment row
- [ ] `#` headings preserved as `##` / `###` (document-level `#` only if this is a README)
- [ ] Nested bullets preserved at original depth
