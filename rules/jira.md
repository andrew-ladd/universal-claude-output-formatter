# Jira formatting rules

Jira Cloud's comment and description editor renders **standard Markdown** when pasted directly. Use Markdown syntax — not Jira Wiki Markup (`h3.`, `||header||`, `{{code}}`).

## Markdown reference for Jira Cloud

| Construct | Syntax |
|---|---|
| Bold | `**text**` |
| Italic | `*text*` |
| Inline code | `` `code` `` |
| Code block | ` ```lang ``` ` |
| Link | `[display text](url)` |
| Heading 1–3 | `#`, `##`, `###` |
| Bullet list | `- item` |
| Numbered list | `1. item` |
| Horizontal rule | `---` |
| Table | GFM pipe tables (see below) |
| Blockquote | `> text` |

## What NOT to use

- Jira Wiki Markup (`h3. Title`, `*bold*`, `{{inline}}`, `{code}`, `||header||`) — renders as literal text in the Cloud editor.
- HTML tags — strip or rewrite.

## Code blocks

````
```javascript
function hello() {
  return "world";
}
```
````

## Inline code

```
The `--force` flag skips validation.
```

## Tables

```
| Name | Status | Notes |
|---|---|---|
| Auth | Done | Shipped in v2 |
| API | WIP | ETA next sprint |
```

## Headings

Use `###` or `####` for most content sections. Reserve `##` for top-level section headers.

## Bullet lists

```
- First item
- Second item
  - Nested item
- Back to top level
```

## Blockquotes

```
> This is a quoted line.
```

## Emphasis rules

- Use `**bold**` for labels, field names, and important terms.
- Use `*italic*` for titles or light emphasis.
- Avoid nesting emphasis constructs.

## Length guidance

- Jira description fields support up to ~32k characters.
- Prefer structure (headings, bullets) over prose for long content.
- Split into comments if content exceeds a single description field logically.
