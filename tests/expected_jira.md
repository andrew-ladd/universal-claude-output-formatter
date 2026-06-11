# Expected output: Jira

Destination: Jira Wiki Markup
Source: [input_mixed.md](input_mixed.md)

---

h2. Overview

This is a *bold* statement with _italic_ emphasis and some -strikethrough- text.

Inline code: {{const x = 42;}} — should survive in all destinations.

A [link to the docs|https://example.com/docs] and a bare URL: [https://example.com]

----

h2. Bullet list

* First item
* Second item
** Nested child
** Another nested child
* Third item

h2. Numbered list

# Step one
# Step two
# Step three

h2. Code block

{code:javascript}
function add(a, b) {
  // This comment must be preserved exactly
  return a + b;
}
{code}

h2. Blockquote

bq. This is a quoted passage. It spans two lines.

h2. Table

||Column A||Column B||Column C||
|Alpha|1|Yes|
|Beta|2|No|
|Gamma|3|Maybe|

h2. Mixed paragraph

The service runs on *port 8080* by default. To override, set {{PORT=9000}} before starting. See [configuration guide|https://example.com/config] for all options.

bq. Warning: do not expose port 8080 publicly without authentication.

---

## Acceptance notes

- [ ] `**bold**` → `*bold*` (Jira Wiki)
- [ ] `*italic*` → `_italic_`
- [ ] `~~strikethrough~~` → `-strikethrough-`
- [ ] `` `inline code` `` → `{{code}}`
- [ ] Fenced code block → `{code:lang}...{code}`
- [ ] `[text](url)` → `[text|url]`
- [ ] Bare URL → `[url]`
- [ ] Nested bullets use `**` for second level
- [ ] `> blockquote` → `bq.` (multi-line collapsed to single `bq.`)
- [ ] Table → `||header||` / `|cell|` format
- [ ] `#` heading → `h2.` / `h3.`
- [ ] `---` → `----` (four hyphens)
