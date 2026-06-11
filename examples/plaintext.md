# Example: Plain text output

Formatted from [source.md](source.md) using [rules/plaintext.md](../rules/plaintext.md).

---

DEPLOY CHECKLIST FOR V2.3.0
============================

We need to ship the auth refactor and the RATE LIMITER this Friday.
See the release plan (https://example.com/releases/v2.3.0) for full context.

STEPS

1. Merge the auth PR -- #1042
2. Run the migration: npm run migrate:prod
3. Verify the health endpoint returns 200
4. Update the CHANGELOG.md

NOTES

• The rate limiter defaults to 100 REQ/MIN per user.
• If the migration fails, run npm run migrate:rollback and notify #incidents.
• Do NOT deploy on Friday after 16:00 UTC.

RISK MATRIX

Migration timeout  |  Medium  |  Run during low-traffic window
Auth regression    |  Low     |  Covered by e2e suite
Rate limiter FP    |  Low     |  Feature-flagged, can disable

ROLLBACK

> If anything goes wrong, revert using the tag v2.2.9
> and open an incident ticket.

    git checkout v2.2.9
    npm run deploy

---

## Transformation notes

- `**bold**` → ALL CAPS for key terms
- `*italic*` → removed, rewritten for clarity
- `[text](url)` → `text (url)`
- Table → pipe-aligned columns
- Blockquote → `> ` prefix per line
- Code block → 4-space indent, no fencing
- `#` heading → ALL CAPS + `====` underline (top level) or ALL CAPS only (sub)
- `---` horizontal rule → preserved as-is
