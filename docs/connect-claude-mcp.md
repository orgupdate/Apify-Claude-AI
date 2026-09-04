# Connect the Orgupdate Actors to Claude (MCP)

The Orgupdate job scrapers run on [Apify](https://apify.com). Apify hosts a
**Model Context Protocol (MCP)** server at `https://mcp.apify.com` that exposes
every Actor as a tool. Once you connect that server to Claude as a **connector**,
Claude can run the scrapers for you.

This page covers the setup in full. If you just want the short version, see the
Quick start in the [README](../README.md).

---

## 1. Prerequisites

- **Apify account** — free tier is fine. [Sign up](https://apify.com).
- **Claude plan that supports connectors** — Free (limited to one connector),
  Pro, Max, Team, or Enterprise.
- **Claude Desktop** or **claude.ai** in a browser.

Custom connectors talk to `https://mcp.apify.com` from Anthropic's servers, so
the MCP server must be publicly reachable — Apify's hosted server already is, so
there is nothing to configure on your side.

---

## 2. Choose your tool scope

The MCP server URL takes a `?tools=` parameter that decides which tools Claude
loads.

| URL | Use it when |
|---|---|
| `https://mcp.apify.com/?tools=actors,docs` | **Recommended.** Claude can discover and run **any** Orgupdate Actor on demand. Best for scraping across multiple job boards. |
| `https://mcp.apify.com/?tools=actors,docs,orgupdate/indeed-jobs-scraper` | You mostly use one source and want its input schema loaded up front. |
| `https://mcp.apify.com/?tools=actors,docs,orgupdate/indeed-jobs-scraper,orgupdate/reed-jobs-scraper` | You use a fixed set of two or three sources. |

`actors` gives Claude the generic `search-actors`, `fetch-actor-details`, and
`call-actor` tools. `docs` lets Claude look up Apify documentation when it needs
to. Adding a specific `username/actor-name` pins that Actor's tool so its inputs
are always visible.

See [actors.md](actors.md) for every Orgupdate slug.

---

## 3a. Add the connector on claude.ai (Pro / Max)

1. Open **Customize → Connectors** (or **Settings → Connectors**).
2. Click **"+" → Add custom connector**.
3. Paste your chosen server URL, e.g.
   `https://mcp.apify.com/?tools=actors,docs`
4. (Optional) Open **Advanced settings** if you want to supply your own OAuth
   client — most people skip this.
5. Click **Add**.
6. Click **Connect**. Your browser opens Apify's sign‑in page. Approve the
   requested permissions.

## 3b. Add the connector on claude.ai (Team / Enterprise)

An organisation **Owner** adds it once for everyone:

1. **Organization settings → Connectors → Add → Custom → Web**.
2. Enter `https://mcp.apify.com/?tools=actors,docs`, optionally add OAuth
   details, click **Add**.

Each **member** then:

1. Opens **Customize → Connectors**.
2. Finds the Apify / Orgupdate connector and clicks **Connect** to authenticate.

## 3c. Add the connector in Claude Desktop

**Option 1 — connector directory (easiest):**

1. **Settings → Connectors**.
2. Search for **"Apify"**.
3. Click **Connect** / **Install** and approve access in the browser.

**Option 2 — custom connector:**

1. **Settings → Connectors → Add custom connector**.
2. Use `https://mcp.apify.com` (or add `?tools=actors,docs`).
3. Approve in the browser.

---

## 4. Authentication options

### OAuth (default, recommended)

When you click **Connect**, a browser window opens and you sign in to Apify. You
grant Claude permission to run Actors on your account. Claude never receives your
password or API token. You can revoke access any time from
**Apify Console → Settings → Integrations** or from Claude's connector settings.

### API token (advanced)

If you manage MCP config as JSON (some Claude Desktop setups) you can pass a
token instead of using OAuth:

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com/?tools=actors,docs",
      "headers": {
        "Authorization": "Bearer YOUR_APIFY_TOKEN"
      }
    }
  }
}
```

Get `YOUR_APIFY_TOKEN` from **Apify Console → Settings → API & Integrations**.
Treat it like a password.

---

## 5. Verify the connection

Ask Claude:

> What Apify tools are available to you right now?

Expect to see tools like `search-actors`, `fetch-actor-details`, `call-actor`,
and (if you pinned one) an Orgupdate Actor tool.

Then run a tiny test:

> Search Apify for the Orgupdate Reed jobs scraper and show me its input schema.

If Claude returns the schema (`includeKeyword`, `locationName`, `countryName`,
`pagesToFetch`, …) you are ready. Move on to
[running-actors.md](running-actors.md).

---

## 6. Changing the scope later

To widen or narrow which Actors are available, edit the connector URL:

1. **Settings → Connectors →** the Apify connector **→ Configure / Edit**.
2. Change the `?tools=` value.
3. Reconnect if prompted.

You do **not** need to remove and re‑add the connector.

---

## Common setup problems

See [troubleshooting.md](troubleshooting.md) for:

- the connector not appearing after you add it,
- the browser auth window closing without connecting,
- "no tools available" after a successful sign‑in,
- Free‑plan users hitting the one‑connector limit.
