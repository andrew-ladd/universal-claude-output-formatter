# universal-output-formatter

A Claude Code skill that formats text for a specific destination — Slack, Jira, GitHub, or plain Markdown.

## Installation

Clone or copy this skill into your Claude skills directory:

```bash
git clone https://github.com/andrew-ladd/universal-claude-output-formatter \
  ~/.claude/skills/universal-output-formatter
```

Claude Code picks up skills automatically from `~/.claude/skills/` — no restart required. The skill is available immediately as `/universal-output-formatter`.

## What it does

**Reformat mode** — paste in existing text and get it back in the correct syntax for a target tool. Handles links, emphasis, code blocks, tables, and blockquotes, rewriting unsupported constructs rather than dropping them.

**Live output mode** — ask Claude to format its own responses for a destination. Two variants:

- *Single-response*: "give me that as a Jira comment" — formats one reply, then reverts silently.
- *Persistent*: "format your responses for Slack from now on" — stays on until you say "back to normal".

## Supported destinations

| Destination | Syntax | Rule file |
|---|---|---|
| Slack | mrkdwn | [`rules/slack.md`](rules/slack.md) |
| Jira | Wiki Markup | [`rules/jira.md`](rules/jira.md) |
| GitHub | GitHub Flavored Markdown | [`rules/github.md`](rules/github.md) |
| Plain Markdown | CommonMark | [`rules/markdown.md`](rules/markdown.md) |

## Usage

### Reformat existing text

```
Format this for Slack:

## Deploy checklist
- Merge PR #1042
- Run `npm run migrate:prod`
- Verify health endpoint
```

### Single-response live mode

```
Summarize this incident report as a Jira comment.
```

### Persistent live mode

```
Format your responses for GitHub from now on.
```

```
Back to normal.
```

## Repo structure

```
SKILL.md               # Entry point: rules, decision logic, validation checklist
rules/
  slack.md             # mrkdwn reference and rewrite rules
  jira.md              # Jira Wiki Markup reference and rewrite rules
  github.md            # GFM reference and rewrite rules
  markdown.md          # CommonMark rules and GFM extension warnings
examples/
  source.md            # Shared source text (deploy checklist)
  slack.md             # Same content formatted for Slack
  jira.md              # Same content formatted for Jira
  github.md            # Same content formatted for GitHub
  markdown.md          # Same content formatted as plain Markdown
tests/
  input_mixed.md       # Canonical test input (links, bullets, emphasis, code, table, blockquote)
  expected_slack.md    # Expected Slack output + acceptance checklist
  expected_jira.md     # Expected Jira output + acceptance checklist
  expected_github.md   # Expected GitHub output + acceptance checklist
  expected_markdown.md # Expected plain Markdown output + acceptance checklist
```

## Extending

To add a new destination (e.g. Notion, Confluence):

1. Create `rules/<destination>.md` following the structure of an existing rule file.
2. Add a row to the destinations table in `SKILL.md` and this README.
3. Add formatted examples in `examples/` and acceptance notes in `tests/`.
