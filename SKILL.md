---
name: universal-output-formatter
description: >
  Claude Code only (untested in other agents). Format text for a specified destination
  (Slack, Jira, GitHub, plain Markdown, plain text). Rewrites existing source text, or
  applies destination formatting to Claude's own responses — either for one message or
  persistently. Use when the user wants to reformat content, paste Claude's output into
  another tool, or says "/universal-output-formatter".
---

# universal-output-formatter

Format text for a specified destination — either by rewriting existing source text, or by producing all subsequent responses directly in the destination's format.

## When to use this skill

**Reformat mode** — you have existing text to convert:
- You have text (notes, a summary, a doc, an error log) and need it formatted for a specific tool.
- You are copying content between tools and want it to render correctly.
- The source text has mixed formatting that will break in the target.

**Live output mode** — you want all responses formatted for a destination from now on:
- The user says something like "reply in Slack format", "use Jira formatting", or "I'm pasting your answers into GitHub".
- The user wants to copy-paste Claude's responses directly without any post-processing.
- The user wants formatting to persist across multiple turns.

The two modes are independent. Reformat mode is one-shot. Live output mode is persistent until cancelled.

## Supported destinations

| Destination | Rule file |
|---|---|
| Slack | [rules/slack.md](rules/slack.md) |
| Jira | [rules/jira.md](rules/jira.md) |
| GitHub (issues, PRs, comments) | [rules/github.md](rules/github.md) |
| Plain Markdown | [rules/markdown.md](rules/markdown.md) |
| Plain Text | [rules/plaintext.md](rules/plaintext.md) |

To add a new destination, create `rules/<destination>.md` following the same structure, then add it to this table.

## Decision rules (in priority order)

1. Preserve factual meaning over style.
2. Follow destination-specific rules (see rule files).
3. Prefer readability over cosmetic formatting.
4. Rewrite unsupported constructs into the closest readable equivalent — never drop them silently.
5. Do not add facts, examples, or opinions not present in the source.

## Live output mode

### Activation

Live mode has two sub-modes: **single-response** and **persistent**. Choose based on the user's phrasing.

**Single-response mode** — apply the destination format to the next response only, then revert silently. No confirmation needed. Triggered by one-off phrasing like:
- "answer in Slack format"
- "give me that as a Jira comment"
- "format this response for GitHub"
- "send that in mrkdwn"

**Persistent mode** — apply the destination format to all subsequent responses until cancelled. Triggered by phrasing that signals ongoing intent:
- "format your responses for Slack"
- "reply in Jira format from now on"
- "use GitHub Markdown going forward"
- "I'm pasting your answers into [destination]"
- "keep formatting as [destination]"

When in doubt about which sub-mode the user wants, default to **single-response**.

On persistent mode activation, confirm once: `Got it — I'll format all responses for [Destination] until you tell me to stop.`

Single-response mode needs no confirmation — just format and revert.

Then (for persistent mode) immediately apply the destination's rules to **every subsequent response** in the conversation, including:
- Plain answers and explanations
- Code explanations and summaries
- Lists and tables you generate
- Any text the user would paste or share

### What live mode changes

In live mode, every response is authored in the destination format from the start — not post-processed. This means:
- Write bold/italic in the destination's syntax, not Markdown's.
- Use the destination's link format for any URLs.
- Structure responses using the destination's native constructs (mrkdwn, Wiki Markup, GFM, etc.).
- Do not produce hybrid output that mixes formats.

### What live mode does NOT change

- Code blocks: always preserve content exactly.
- Factual accuracy and completeness.
- Response length — format to the destination, but do not pad or truncate meaning.

### Deactivation

Stop live mode when the user says:
- "stop formatting"
- "back to normal"
- "turn off [destination] mode"
- "reset formatting"
- Any equivalent instruction to stop.

On deactivation, confirm once: `Got it — back to standard formatting.`

### Mode stacking

Only one destination is active at a time. If the user requests a new destination while live mode is already on, switch immediately and confirm: `Switched to [NewDestination] format.`

## When to ask a clarifying question

Ask **one** clarifying question before formatting when:
- No destination is specified (reformat mode or live mode activation is ambiguous).
- The destination is ambiguous (e.g. "a ticket" could be Jira or GitHub).

Question template: `Which destination should I format this for? (Slack / Jira / GitHub / Markdown)`

Do not ask for clarification about style preferences — apply the rules and format.

## Clipboard offer

After producing formatted output, offer to copy it to the clipboard unless:
- The user's request already included a clipboard instruction (e.g. "pipe to pbcopy", "copy to clipboard"), or
- The output was split across multiple messages (offer only once, after the final part).

Offer template: `Copy to clipboard?`

If the user accepts (yes / sure / copy it / etc.), run:

```bash
pbcopy << 'EOF'
<formatted output>
EOF
```

Do not offer in live output mode — clipboard copy only makes sense for discrete, finished outputs.

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
- [examples/plaintext.md](examples/plaintext.md) — formatted as plain text

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
