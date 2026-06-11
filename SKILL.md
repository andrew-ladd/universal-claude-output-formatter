# universal-output-formatter

Rewrite source text or notes into the best paste-ready format for a specified destination.

## When to use this skill

- You have text (notes, a summary, a doc, an error log) and need it formatted for a specific tool.
- You are copying content between tools and want it to render correctly.
- The source text has mixed formatting that will break in the target.

## Supported destinations

| Destination | Rule file |
|---|---|
| Slack | [rules/slack.md](rules/slack.md) |
| Jira | [rules/jira.md](rules/jira.md) |
| GitHub (issues, PRs, comments) | [rules/github.md](rules/github.md) |
| Plain Markdown | [rules/markdown.md](rules/markdown.md) |

To add a new destination, create `rules/<destination>.md` following the same structure, then add it to this table.

## Decision rules (in priority order)

1. Preserve factual meaning over style.
2. Follow destination-specific rules (see rule files).
3. Prefer readability over cosmetic formatting.
4. Rewrite unsupported constructs into the closest readable equivalent — never drop them silently.
5. Do not add facts, examples, or opinions not present in the source.

## When to ask a clarifying question

Ask **one** clarifying question before formatting when:
- No destination is specified.
- The destination is ambiguous (e.g. "a ticket" could be Jira or GitHub).

Question template: `Which destination should I format this for? (Slack / Jira / GitHub / Markdown)`

Do not ask for clarification about style preferences — apply the rules and format.

## When to split into multiple messages

Split output into multiple messages when:
- Slack: formatted output exceeds ~3000 characters (Slack message limit is 40k but readability drops sharply before that).
- Jira: a single description field would exceed ~32k characters.
- GitHub: a comment or issue body would exceed ~65k characters.

When splitting, label each part: `(1/2)`, `(2/2)`.

## Output transformation rules

### Links
- Slack: `<url|display text>` — see [rules/slack.md](rules/slack.md)
- GitHub: `[display text](url)` — standard Markdown
- Jira: `[display text|url]` — see [rules/jira.md](rules/jira.md)
- Markdown: `[display text](url)`

### Emphasis
- Preserve bold and italic only when the destination renders them cleanly.
- Avoid nested emphasis (`***bold italic***`).

### Lists
- Keep bullet structure stable across destinations.
- Use numbered lists only when order matters.
- Max nesting depth: 2 levels for Slack, 3 for all others.

### Code
- Preserve code blocks exactly (content is never rewritten).
- Keep inline code inline unless the destination cannot render backticks.

### Blockquotes
- Preserve for GitHub and Markdown.
- Rewrite as bullet-prefixed text for Slack and Jira when blockquote syntax is not supported.

### Tables
- Preserve for GitHub and Markdown.
- Rewrite as bulleted labeled lines for Slack.
- Rewrite as `||header||header||` wiki markup for Jira.
- If a table cannot be rewritten cleanly, represent each row as a bullet with labeled values.

## Examples

See the [examples/](examples/) folder:
- [examples/source.md](examples/source.md) — shared source text
- [examples/slack.md](examples/slack.md) — formatted for Slack
- [examples/jira.md](examples/jira.md) — formatted for Jira
- [examples/github.md](examples/github.md) — formatted for GitHub
- [examples/markdown.md](examples/markdown.md) — formatted as plain Markdown

## Validation checklist

Run through this after formatting:

- [ ] No factual content was added or removed.
- [ ] All links are in the correct syntax for the destination.
- [ ] Code blocks are intact and unchanged.
- [ ] Bold/italic is only used where the destination renders it.
- [ ] Tables have been converted if the destination does not render them.
- [ ] Bullet depth does not exceed the destination's supported limit.
- [ ] Blockquotes are in supported form or rewritten.
- [ ] Output length is within destination limits (or split if not).
- [ ] No unsupported Markdown constructs remain (e.g. HTML tags in Slack).

## Test plan

See [tests/](tests/) for sample inputs and acceptance notes. The test suite exercises:
- Links (inline, bare URL, reference-style)
- Bullet lists (flat and nested)
- Bold and italic emphasis
- Inline code and fenced code blocks
- Blockquotes
- Tables
- Mixed content (all of the above in one document)
