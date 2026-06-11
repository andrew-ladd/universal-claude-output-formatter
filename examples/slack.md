# Example: Slack output

Formatted from [source.md](source.md) using [rules/slack.md](../rules/slack.md).

---

*Deploy checklist for v2.3.0*

Shipping *auth refactor* and *rate limiter* this Friday. <https://example.com/releases/v2.3.0|Release plan>

*Steps*
1. Merge the auth PR — `#1042`
2. Run the migration: `npm run migrate:prod`
3. Verify the health endpoint returns `200`
4. Update `CHANGELOG.md`

*Notes*
• Rate limiter defaults to *100 req/min* per user.
• If migration fails, run `npm run migrate:rollback` and notify #incidents.
• Do _not_ deploy on Friday after 16:00 UTC.

*Risk matrix*
• Migration timeout — Medium likelihood. Mitigation: run during low-traffic window.
• Auth regression — Low likelihood. Mitigation: covered by e2e suite.
• Rate limiter false-positive — Low likelihood. Mitigation: feature-flagged, can disable.

*Rollback*
> If anything goes wrong, revert using tag `v2.2.9` and open an incident ticket.

```
git checkout v2.2.9
npm run deploy
```

---

## Transformation notes

- `#` heading → `*bold*` text
- `**bold**` → `*bold*` (mrkdwn)
- `[text](url)` → `<url|text>`
- Table → bullet list with labeled fields
- Blockquote → preserved as `> text`
- Code block → preserved, language tag removed
- `*italic*` → `_italic_`
