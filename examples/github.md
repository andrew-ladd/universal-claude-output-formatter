# Example: GitHub output

Formatted from [source.md](source.md) using [rules/github.md](../rules/github.md).

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

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Migration timeout | Medium | Run during low-traffic window |
| Auth regression | Low | Covered by e2e suite |
| Rate limiter false-positive | Low | Feature-flagged, can disable |

### Rollback

> If anything goes wrong, revert using the tag `v2.2.9` and open an incident ticket.

```bash
git checkout v2.2.9
npm run deploy
```

---

## Transformation notes

This is the closest to the source format — GitHub uses GFM which matches the source document's structure almost exactly.

- Headings, links, bold, italic, code blocks, tables, blockquotes: all preserved as-is.
- `#1042` in the steps list is a GitHub issue reference and will auto-link in a GitHub context.
- No constructs needed to be rewritten.
