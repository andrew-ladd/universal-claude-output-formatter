# Example: Jira output

Formatted from [source.md](source.md) using [rules/jira.md](../rules/jira.md).

---

h2. Deploy checklist for v2.3.0

We need to ship the *auth refactor* and the *rate limiter* this Friday. See the [release plan|https://example.com/releases/v2.3.0] for full context.

h3. Steps

# Merge the auth PR — {{#1042}}
# Run the migration: {{npm run migrate:prod}}
# Verify the health endpoint returns {{200}}
# Update the {{CHANGELOG.md}}

h3. Notes

* The rate limiter defaults to *100 req/min* per user.
* If the migration fails, run {{npm run migrate:rollback}} and notify #incidents.
* Do _not_ deploy on Friday after 16:00 UTC.

h3. Risk matrix

||Risk||Likelihood||Mitigation||
|Migration timeout|Medium|Run during low-traffic window|
|Auth regression|Low|Covered by e2e suite|
|Rate limiter false-positive|Low|Feature-flagged, can disable|

h3. Rollback

bq. If anything goes wrong, revert using the tag {{v2.2.9}} and open an incident ticket.

{code:bash}
git checkout v2.2.9
npm run deploy
{code}

---

## Transformation notes

- `#` heading → `h2.` / `h3.` syntax
- `**bold**` → `*bold*` (Jira Wiki)
- `*italic*` → `_italic_`
- `` `code` `` → `{{code}}`
- ` ```bash ``` ` → `{code:bash}...{code}`
- `[text](url)` → `[text|url]`
- Table → `||header||` / `|cell|` format
- Blockquote → `bq.` (single line; content condensed)
