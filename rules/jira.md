# Jira formatting rules

Jira supports two markup systems depending on configuration:
- **Jira Wiki Markup** — used in Server, Data Center, and some Cloud fields.
- **Atlassian Document Format (ADF)** — used in Jira Cloud description and comment fields rendered via the editor.

When the target is unknown, default to **Jira Wiki Markup** — it is compatible with both and pastes cleanly in plain-text fields.

## Jira Wiki Markup reference

| Construct | Syntax | Notes |
|---|---|---|
| Bold | `*text*` | Asterisk |
| Italic | `_text_` | Underscore |
| Underline | `+text+` | Plus sign |
| Strikethrough | `-text-` | Hyphen |
| Monospace / inline code | `{{code}}` | Double curly braces |
| Code block | `{code}...{code}` or `{code:java}...{code}` | Optional language |
| Link | `[display text\|url]` | Pipe separator |
| Bare URL | `[url]` | |
| Jira issue link | `[PROJECT-123]` | Auto-linked |
| Bullet list | `* item` | Asterisk + space |
| Numbered list | `# item` | Hash + space |
| Heading 1–6 | `h1. text` … `h6. text` | |
| Horizontal rule | `----` | Four hyphens |
| Blockquote | `bq. text` | Single-line only |
| Table | `\|\|header\|\|` / `\|cell\|` | See below |
| Image | `!url!` | Exclamation marks |

## Not supported in Wiki Markup

- Standard Markdown syntax (`##`, `**`, `[text](url)`) — renders literally.
- HTML tags — strip or rewrite.
- Fenced code blocks (` ``` `) — use `{code}` macro instead.
- Nested bold/italic in some renderers — avoid.

## Links

```
[Read the docs|https://example.com]
```

For a bare URL with no label:

```
[https://example.com]
```

## Code blocks

```
{code}
function hello() {
  return "world";
}
{code}
```

With language hint:

```
{code:javascript}
function hello() {
  return "world";
}
{code}
```

## Inline code

Use double curly braces:

```
The {{--force}} flag skips validation.
```

## Tables

```
||Name||Status||Notes||
|Auth|Done|Shipped in v2|
|API|WIP|ETA next sprint|
```

- `||` delimiter for header row.
- `|` delimiter for data rows.
- No trailing pipe required.

## Bullet lists

```
* First item
* Second item
** Nested item
** Another nested
* Back to top level
```

Use `**` for second-level nesting, `***` for third.

## Numbered lists

```
# Step one
# Step two
## Sub-step
# Step three
```

## Headings

```
h2. Section Title
```

Use `h2.` or `h3.` for most content. Reserve `h1.` for document-level titles.

## Blockquotes

Single-line only with `bq.`:

```
bq. This is a quoted line.
```

For multi-line quoted content, use a `{quote}` macro (Cloud only) or rewrite as a bullet with a `>` label:

```
* > "The system was unavailable from 14:00 to 15:30."
```

## Emphasis rules

- Use `*bold*` for labels, field names, and important terms.
- Use `_italic_` for titles or light emphasis.
- Avoid nesting emphasis constructs.

## Length guidance

- Jira description fields support up to ~32k characters.
- Prefer structure (headings, bullets) over prose for long content.
- Split into comments if content exceeds a single description field logically.
