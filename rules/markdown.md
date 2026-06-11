# Plain Markdown formatting rules

Plain Markdown targets the CommonMark spec — the lowest common denominator that renders correctly across most tools (VS Code, Obsidian, static site generators, README renderers).

Avoid GFM-only extensions (task lists, tables, autolinks) unless you know the renderer supports them.

## Supported constructs

| Construct | Syntax | Notes |
|---|---|---|
| Bold | `**text**` | Double asterisk |
| Italic | `*text*` | Single asterisk |
| Inline code | `` `code` `` | Backtick |
| Fenced code block | ` ```lang ` | CommonMark 0.30+ |
| Indented code block | 4-space indent | Universally supported |
| Link | `[text](url)` | Standard |
| Reference link | `[text][ref]` + `[ref]: url` | Good for repeated links |
| Image | `![alt](url)` | |
| Heading | `# H1` … `###### H6` | ATX style preferred |
| Bullet list | `- item` | Hyphen preferred |
| Numbered list | `1. item` | |
| Blockquote | `> text` | |
| Horizontal rule | `---` | Three hyphens on its own line |
| Line break | Two trailing spaces or blank line | |

## Not safe in plain Markdown (avoid unless renderer is known)

- Tables — not part of CommonMark; use bullets or labeled lines instead.
- Task lists (`- [ ]`) — GFM extension.
- Strikethrough (`~~`) — GFM extension.
- Autolinks (`<url>`) — behavior varies.
- HTML tags — rendered or escaped depending on parser.
- Footnotes — extension, not universally supported.

## Links

Standard form:

```markdown
[Read the docs](https://example.com)
```

Reference form (useful when the same URL appears multiple times):

```markdown
See the [documentation][docs] or the [changelog][docs].

[docs]: https://example.com/docs
```

## Code blocks

Fenced blocks with a language hint:

````markdown
```bash
git commit -m "fix: resolve null reference"
```
````

Use a 4-space indent when renderer compatibility is uncertain:

```
    function hello() {
      return "world";
    }
```

## Headings

ATX style (`#` prefix) — preferred over Setext (`===` underline):

```markdown
# Document Title

## Section

### Subsection
```

Leave one blank line before and after each heading.

## Lists

Flat bullets:

```markdown
- First item
- Second item
- Third item
```

Nested bullets (use consistent indentation — 2 or 4 spaces):

```markdown
- Parent item
  - Child item
  - Another child
- Back to top
```

Numbered lists:

```markdown
1. Step one
2. Step two
3. Step three
```

Mixed (numbered steps with bullet sub-items):

```markdown
1. Install dependencies
   - Run `npm install`
   - Confirm no audit errors
2. Start the server
```

## Blockquotes

```markdown
> This is a blockquote.
> It can span multiple lines.

> Nested:
> > Inner quote
```

## Emphasis rules

- Use `**bold**` for important terms and labels.
- Use `*italic*` for titles, filenames, and light emphasis.
- Avoid adjacent or nested emphasis where possible.
- Never use HTML `<strong>` or `<em>` tags — portability degrades.

## Tables (when renderer is known to support them)

If you know the renderer supports GFM tables:

```markdown
| Name | Value |
|------|-------|
| foo  | 1     |
| bar  | 2     |
```

Otherwise, rewrite as bullets:

```markdown
- **Name:** foo — **Value:** 1
- **Name:** bar — **Value:** 2
```

## Length guidance

- Plain Markdown has no length limits — it is a file format.
- Structure long documents with headings and a table of contents.
- Use horizontal rules (`---`) sparingly to separate major sections.
