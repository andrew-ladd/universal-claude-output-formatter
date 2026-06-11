# Expected output: Plain Markdown

Destination: CommonMark / plain Markdown
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

## Table (rewritten — CommonMark does not support tables)

**Column A:** Alpha — **Column B:** 1 — **Column C:** Yes

**Column A:** Beta — **Column B:** 2 — **Column C:** No

**Column A:** Gamma — **Column B:** 3 — **Column C:** Maybe

---

## Mixed paragraph

The service runs on **port 8080** by default. To override, set `PORT=9000` before starting. See [configuration guide](https://example.com/config) for all options.

> Warning: do not expose port 8080 publicly without authentication.

---

## Acceptance notes

- [ ] `**bold**`, `*italic*` preserved
- [ ] `~~strikethrough~~` preserved (note: GFM extension — omit if strict CommonMark)
- [ ] `` `inline code` `` preserved
- [ ] `[text](url)` links preserved
- [ ] Fenced code block preserved
- [ ] `> blockquote` preserved
- [ ] Table → rewritten as bold-labeled lines (CommonMark incompatible)
- [ ] Nested bullets preserved
- [ ] No HTML tags introduced
