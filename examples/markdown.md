# Example: Plain Markdown output

Formatted from [source.md](source.md) using [rules/markdown.md](../rules/markdown.md).

---

## Deploy checklist for v2.3.0

We need to ship the **auth refactor** and the **rate limiter** this Friday. See the [release plan](https://example.com/releases/v2.3.0) for full context.

### Steps

1. Merge the auth PR — `#1042`
2. Run the migration: `npm run migrate:prod`
3. Verify the health endpoint returns `200`
4. Update the `CHANGELOG.md`

### Notes

- The rate limiter defaults to **100 req/min** per user.
- If the migration fails, run `npm run migrate:rollback` and notify `#incidents`.
- Do *not* deploy on Friday after 16:00 UTC.

### Risk matrix

**Migration timeout** — Likelihood: Medium. Mitigation: run during low-traffic window.

**Auth regression** — Likelihood: Low. Mitigation: covered by e2e suite.

**Rate limiter false-positive** — Likelihood: Low. Mitigation: feature-flagged, can disable.

### Rollback

> If anything goes wrong, revert using the tag `v2.2.9` and open an incident ticket.

```bash
git checkout v2.2.9
npm run deploy
```

---

## Transformation notes

- Headings, links, bold, italic, code blocks, blockquotes: all preserved.
- Table → rewritten as bold-labeled lines (CommonMark does not include tables).
- `#incidents` left as-is — it is a label, not a Markdown construct.
