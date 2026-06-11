# Expected output: Plain text

Destination: Plain text (no markup rendered)
Source: [input_mixed.md](input_mixed.md)

---

OVERVIEW
========

This is a BOLD statement with italic emphasis and some removed strikethrough text.

Inline code: const x = 42; -- should survive in all destinations.

A link to the docs (https://example.com/docs) and a bare URL: https://example.com

---

BULLET LIST

• First item
• Second item
  - Nested child
  - Another nested child
• Third item

NUMBERED LIST

1. Step one
2. Step two
3. Step three

---

CODE BLOCK

    function add(a, b) {
      // This comment must be preserved exactly
      return a + b;
    }

---

BLOCKQUOTE

> This is a quoted passage.
> It spans two lines.

---

TABLE

Column A: Alpha  |  Column B: 1  |  Column C: Yes
Column A: Beta   |  Column B: 2  |  Column C: No
Column A: Gamma  |  Column B: 3  |  Column C: Maybe

---

MIXED PARAGRAPH

The service runs on PORT 8080 by default. To override, set PORT=9000 before
starting. See the configuration guide (https://example.com/config) for all options.

> Warning: do not expose port 8080 publicly without authentication.

---

## Acceptance notes

- [ ] `**bold**` → ALL CAPS for key terms
- [ ] `*italic*` → removed or rewritten for clarity
- [ ] `~~strikethrough~~` → removed or noted as "(removed)"
- [ ] `` `inline code` `` → plain text, no markers
- [ ] Fenced code block → 4-space indent, no backticks
- [ ] `[text](url)` → `text (url)`
- [ ] Bare URL → preserved as-is
- [ ] Nested bullets → `•` top level, `-` second level, 2-space indent
- [ ] `> blockquote` → `> ` prefix per line
- [ ] Table → pipe-aligned labeled columns
- [ ] `#` heading → ALL CAPS + underline (top) or ALL CAPS only (sub)
- [ ] No syntax characters that could be misread as markup
