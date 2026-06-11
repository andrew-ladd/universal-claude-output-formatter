# GitHub formatting rules

GitHub renders **GitHub Flavored Markdown (GFM)** in issues, pull requests, comments, and wikis. GFM is a superset of CommonMark.

## Supported constructs

| Construct | Syntax | Notes |
|---|---|---|
| Bold | `**text**` | Double asterisk |
| Italic | `*text*` or `_text_` | |
| Strikethrough | `~~text~~` | Double tilde |
| Inline code | `` `code` `` | Backtick |
| Fenced code block | ` ```lang ` | With optional language |
| Link | `[display text](url)` | Standard Markdown |
| Autolink | `<url>` | Angle brackets |
| Heading | `# H1` … `###### H6` | |
| Bullet list | `- item` or `* item` | |
| Numbered list | `1. item` | Auto-increments |
| Task list | `- [ ] item` / `- [x] item` | Renders checkboxes |
| Blockquote | `> text` | |
| Table | `\| col \| col \|` | GFM extension |
| Horizontal rule | `---` | Three hyphens |
| Image | `![alt](url)` | |
| Footnote | `[^1]` / `[^1]: text` | Supported in most GitHub contexts |
| Details/summary | `<details>` HTML | Collapsible sections |
| Emoji | `:name:` | GitHub emoji codes |
| Mention | `@username` | Links to GitHub user |
| Issue/PR reference | `#123` | Auto-links to issue |
| Commit reference | `abc1234` | 7+ character SHA |

## Links

Standard Markdown:

```markdown
[Read the docs](https://example.com)
```

For relative links within the repo:

```markdown
[Contributing guide](CONTRIBUTING.md)
[Line reference](src/main.ts#L42)
```

## Code blocks

Always use fenced blocks with a language identifier for syntax highlighting:

````markdown
```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}
```
````

Common language identifiers: `bash`, `typescript`, `javascript`, `python`, `json`, `yaml`, `sql`, `diff`.

For `diff` output:

````markdown
```diff
- old line
+ new line
```
````

## Tables

GFM tables render cleanly. Always include the separator row:

```markdown
| Name | Status | Notes |
|------|--------|-------|
| Auth | Done   | Shipped in v2 |
| API  | WIP    | ETA next sprint |
```

Alignment:

```markdown
| Left | Center | Right |
|:-----|:------:|------:|
| a    |   b    |     c |
```

## Task lists

Use in PR descriptions and issue bodies for tracking:

```markdown
- [x] Write tests
- [ ] Update docs
- [ ] Get review
```

## Collapsible sections

For long stack traces, verbose logs, or optional detail:

```markdown
<details>
<summary>Full error log</summary>

```
stack trace here
```

</details>
```

## Blockquotes

Standard Markdown blockquotes work fully:

```markdown
> This is a quoted block.
> It can span multiple lines.
```

For callouts (GitHub-specific alert syntax):

```markdown
> [!NOTE]
> Useful information.

> [!WARNING]
> Critical information.
```

## Headings

Use `##` and `###` for section headings within issues and PRs. Reserve `#` for document-level titles in wikis and READMEs.

## Emphasis rules

- Use `**bold**` for important terms, labels, and action items.
- Use `*italic*` for titles, filenames, and light emphasis.
- Use ~~strikethrough~~ for deprecated or removed items.
- Avoid triple emphasis (`***text***`) — not universally rendered.

## Length guidance

- Issue/comment body: up to 65,536 characters.
- PR description: no hard limit but aim for scannable structure.
- Prefer headings and bullets over long paragraphs for PR descriptions.
- Use collapsible `<details>` blocks for verbose supplementary content.
