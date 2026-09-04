# Troubleshooting

---

## Connector / setup

**The connector doesn't appear after I add it.**
Refresh Claude (reload the tab or restart the desktop app). On Team/Enterprise,
the connector must be added by an Owner in **Organization settings → Connectors**
before members can see it under **Customize → Connectors**.

**The browser auth window opens, then closes, and nothing is connected.**
Pop‑up blockers and third‑party‑cookie blockers are the usual cause. Allow
pop‑ups for `claude.ai` and `apify.com`, then click **Connect** again. If you are
signed in to more than one Apify account, sign out of the others first.

**"No tools available" even though sign‑in succeeded.**
Your `?tools=` value may be empty or malformed. Edit the connector and set it to
exactly:
```
https://mcp.apify.com/?tools=actors,docs
```
Reconnect if prompted.

**I'm on the Claude Free plan and can't add it.**
Free plans allow **one** custom connector. Remove an existing one, or upgrade.

**I want my own API token instead of OAuth.**
Only some Claude Desktop configurations accept a JSON block with an
`Authorization: Bearer` header — see
[connect-claude-mcp.md](connect-claude-mcp.md#4-authentication-options). On
claude.ai, use OAuth.

---

## Runs

**Claude says it can't find the Actor.**
Use the full name in your request: *"the Orgupdate Reed jobs scraper"* or the
slug `orgupdate/reed-jobs-scraper`. Check the slug against
[actors.md](actors.md). If you pinned Actors in the URL, make sure the slug is
spelled correctly there.

**The run returns no results.**
- Confirm `includeKeyword` is not empty.
- Use a job‑title style query, not a long descriptive phrase.
- Check the spelling of `locationName` and `countryName`.
- Remove `jobType` / `datePosted` filters and try again.
- Increase `pagesToFetch`.
You are **not** charged the per‑result fee for an empty run.

**Fewer results than I expected.**
Some queries genuinely have thin coverage on a given board. Broaden the keyword
(`"engineer"` instead of `"senior staff backend engineer"`), widen `datePosted`,
raise `pagesToFetch`, or run a second source.

**"Budget exceeded" / the run stops early.**
Raise the run budget limit in Apify (**Console → the run → Budget**), or lower
`pagesToFetch`. Pay‑per‑result runs need enough budget for at least one page.

**Duplicate jobs across runs or sources.**
The same posting often appears on several boards. Ask Claude to *"remove
duplicates by URL, then by company + title"*. For scheduled scraping set
`datePosted` to `today` or `3days` so each run only returns new postings.

**Some listings are missing salary / job type / exact date.**
Normal — not every employer publishes those fields. Tell Claude how to handle
blanks in your output.

---

## Still stuck?

- Check the Actor's own page on the Apify Store for status and notes.
- Open an issue on this repository with the request you sent Claude and what
  came back.
