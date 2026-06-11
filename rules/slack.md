# Slack formatting rules

Slack uses **mrkdwn**, not standard Markdown. Many Markdown constructs render as raw text.

## Supported constructs

| Construct | Syntax | Notes |
|---|---|---|
| Bold | `*text*` | Single asterisk, not double |
| Italic | `_text_` | Underscore |
| Strikethrough | `~text~` | Tilde |
| Inline code | `` `code` `` | Backtick |
| Code block | ` ```code``` ` | Triple backtick, no language tag |
| Link | `<url\|display text>` | Angle brackets, pipe separator |
| Bare URL | `<url>` | Auto-linked |
| Bullet list | `• item` or `- item` | Slack renders hyphens as bullets |
| Numbered list | `1. item` | Renders correctly |
| Blockquote | `> text` | Renders as a gray left border |
| Emoji | `:name:` | Standard Slack emoji codes |

## Not supported

- HTML tags — strip or rewrite as plain text.
- Heading syntax (`#`, `##`) — rewrite as `*HEADING*` bold text.
- Horizontal rules (`---`) — omit or replace with a blank line.
- Nested bullets beyond 1 level — flatten to a single level.
- Tables — rewrite as bullet lists or labeled lines (see below).
- Image embeds — replace with a bare URL or `[image: description]`.
- Definition lists — rewrite as labeled bullets.
- Footnotes — inline the content at the point of reference.

## Links

Always use `<url|display text>` form when display text differs from the URL.

```
<https://example.com|Read the docs>
```

For bare URLs with no display text:

```
<https://example.com>
```

Do not use Markdown `[text](url)` — it renders literally in Slack.

## Headings

Rewrite headings as bold text on its own line:

```
*Section Title*
```

For major sections, add a blank line before and after.

## Tables

Rewrite as bullet lists with bold labels:

Source table:
```
| Name | Status |
|------|--------|
| Auth | Done   |
| API  | WIP    |
```

Slack equivalent:
```
• *Auth* — Done
• *API* — WIP
```

## Code blocks

Use triple backtick, no language hint:

```
```
code here
```
```

## Blockquotes

`> text` renders a gray sidebar in Slack. Preserve blockquotes.

For multi-line quotes, prefix each line:

```
> First line
> Second line
```

## Emphasis rules

- Use `*bold*` for important terms or labels.
- Use `_italic_` sparingly — it can be hard to read in Slack.
- Avoid nesting (`*_bold italic_*`) — results vary by client.

## Length guidance

- Single message: aim for under 500 words / ~3000 characters.
- Long content: split and label `(1/2)`, `(2/2)`.
- Dense technical content: prefer bullets over prose paragraphs.
