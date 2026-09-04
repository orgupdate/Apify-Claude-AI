# FAQ

**Is this an official integration?**
The connection uses Apify's official hosted MCP server (`https://mcp.apify.com`)
and Anthropic's official connector feature. The Orgupdate Actors are published on
the Apify Store. Nothing here is a workaround or an unofficial hack.

**Do I need Claude Code?**
No. This guide is for **Claude Desktop** and **claude.ai** (web). Claude Code can
also use the same MCP server, but it is not required.

**Which Claude plan do I need?**
Any plan that supports connectors: Free (one connector), Pro, Max, Team, or
Enterprise.

**What does it cost to run a scrape?**
Apify charges **per job result** returned, plus a tiny actor‑start fee (about
`$0.0001`) per run. Empty runs cost only the start fee. Your Apify free‑tier
credit covers a lot of small runs. See
[running-actors.md](running-actors.md#cost).

**Does Claude see my Apify password or API token?**
No. OAuth grants Claude permission to run Actors on your behalf without exposing
credentials. Revoke it any time from Apify Console or Claude's connector
settings.

**Where does the job data come from?**
Each Actor reads **public** job listings from its source site (Indeed, LinkedIn,
Reed, and so on) and returns them as structured data. The Actors are independent
tools and are not affiliated with or endorsed by those sites, and they do not use
private APIs.

**Can an autonomous agent pay for runs itself?**
Yes — the Actors support the **x402** protocol for USDC payments on Base, so an
agent can discover, pay for, and run an Actor with no Apify account. For everyday
Claude use you just connect once and are billed through Apify.

**Can I scrape every job board at once?**
Not in a single Actor call, but you can ask Claude to run several in sequence and
merge the output. The
[how-to-scrap-orgupdate](https://github.com/orgupdate/how-to-scrap-orgupdate)
playbook is built for exactly that.

**Can I use my own forked Actors?**
Yes. Publish them under your Apify username and use `yourname/actor-name` in the
`?tools=` URL and in your requests to Claude.

**How current is the data?**
It is scraped live at run time. Use `datePosted` to control recency.

**A run failed — what now?**
See [troubleshooting.md](troubleshooting.md). Most failures are an empty query, a
missing location, or a budget limit.
