# Expected output: Slack

Destination: Slack mrkdwn
Source: [input_mixed.md](input_mixed.md)

---

*Overview*

This is a *bold* statement with _italic_ emphasis and some strikethrough text.

Inline code: `const x = 42;` — should survive in all destinations.

A <https://example.com/docs|link to the docs> and a bare URL: <https://example.com>

----

*Bullet list*
• First item
• Second item
• Nested child
• Another nested child
• Third item

*Numbered list*
1. Step one
2. Step two
3. Step three

*Code block*
```
function add(a, b) {
  // This comment must be preserved exactly
  return a + b;
}
```

*Blockquote*
> This is a quoted passage.
> It spans two lines.

*Table*
• *Column A:* Alpha — *Column B:* 1 — *Column C:* Yes
• *Column A:* Beta — *Column B:* 2 — *Column C:* No
• *Column A:* Gamma — *Column B:* 3 — *Column C:* Maybe

*Mixed paragraph*
The service runs on *port 8080* by default. To override, set `PORT=9000` before starting. See <https://example.com/config|configuration guide> for all options.

> Warning: do not expose port 8080 publicly without authentication.

---

## Acceptance notes

- [ ] `**bold**` → `*bold*` (single asterisk)
- [ ] `*italic*` → `_italic_` (underscore)
- [ ] `~~strikethrough~~` → plain text (not supported; stripped cleanly)
- [ ] `` `inline code` `` → preserved as-is
- [ ] `[text](url)` → `<url|text>`
- [ ] Bare URL → `<url>`
- [ ] Nested bullets → flattened to 1 level
- [ ] Fenced code block → triple backtick, no language tag
- [ ] `> blockquote` → preserved
- [ ] Table → bullet list with bold column labels
- [ ] `#` heading → `*bold*` text
- [ ] Horizontal rule → blank line (or `----`)
