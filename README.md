# How to use Apify Actors from Claude

**Scrape job listings from Claude — no code — by connecting the Orgupdate Actors to Claude through the Apify MCP server.**

This repository is a written guide. It shows you how to add Orgupdate's job scrapers to **Claude Desktop** or **claude.ai** as a connector, then ask Claude in plain English to pull live job data from Indeed, LinkedIn, Google Jobs, Dice, Glassdoor, Reed, Wellfound, Upwork and 12 more sources.

> Looking for the end‑to‑end "search the whole market" playbook instead? See
> **[how-to-scrap-orgupdate](https://github.com/orgupdate/how-to-scrap-orgupdate)**.

---

## What you get

- One connector in Claude that exposes **20+ job‑board scrapers** as tools.
- Natural‑language runs: *"Find remote React jobs in Germany posted this week."*
- Structured results (title, company, location, salary, date, apply link) that Claude can turn into a table, CSV, or summary.
- **Pay‑per‑result** pricing on Apify — a run that returns nothing is effectively free.

## Requirements

| You need | Notes |
|---|---|
| An **Apify account** | Free tier works. Sign up at [apify.com](https://apify.com). |
| A **Claude plan** with connectors | Free (1 connector), Pro, Max, Team, or Enterprise. |
| **Claude Desktop** or **claude.ai** (web) | Both support custom connectors / the Apify directory entry. |

You do **not** need Claude Code, the Apify CLI, Node.js, or Python for this guide.

---

## Quick start (5 minutes)

1. **Add the connector.**
   In Claude, open **Settings → Connectors → Add custom connector** and paste:

   ```
   https://mcp.apify.com/?tools=actors,docs
   ```

   (Claude Desktop users can also just search **"Apify"** in the connector directory.)

2. **Authenticate.**
   Your browser opens an Apify sign‑in page. Approve access. Claude never sees your password or API token.

3. **Confirm it works.**
   Ask Claude:

   > What Apify tools do you have available?

   You should see Actor tools such as `search-actors` and `call-actor`.

4. **Run your first scrape.**

   > Use the Orgupdate Indeed jobs scraper to find "product manager" jobs in New York, USA, posted in the last week. Show the results as a table.

   Claude runs the Actor on your Apify account and returns parsed listings.

That's it. The rest of this repo is reference material.

---

## Documentation

| Guide | What it covers |
|---|---|
| [docs/connect-claude-mcp.md](docs/connect-claude-mcp.md) | Full connector setup for claude.ai (Pro/Max and Team/Enterprise) and Claude Desktop, OAuth, API‑token alternative, scoping to one Actor |
| [docs/actors.md](docs/actors.md) | The full catalogue of Orgupdate job Actors — slug, source site, and MCP URL for each |
| [docs/inputs-and-outputs.md](docs/inputs-and-outputs.md) | Every input parameter, every output field, and how plain‑English requests map to them |
| [docs/running-actors.md](docs/running-actors.md) | How to phrase requests, how Claude calls an Actor, reading and exporting the dataset, cost and x402 |
| [docs/troubleshooting.md](docs/troubleshooting.md) | Connector not showing, auth loops, empty results, budget warnings, duplicates |
| [docs/faq.md](docs/faq.md) | Is it official, what it costs, privacy, plan requirements, agent payments |

---

## About

The Orgupdate Actors are a suite of job‑market data tools published on the Apify Store. They read **public** job listings and return them as structured data. They are independent tools and are not affiliated with or endorsed by the job boards they cover.

This guide is maintained by Orgupdate. Issues and pull requests welcome.
