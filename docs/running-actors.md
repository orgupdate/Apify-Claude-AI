# Running an Actor from Claude

Once the connector is added ([connect-claude-mcp.md](connect-claude-mcp.md)),
running a scraper is a conversation.

---

## The basic pattern

> Use the Orgupdate **{source}** jobs scraper to find **{keywords}** jobs in
> **{city}, {country}**, posted **{recency}**. Fetch **{n}** pages and show the
> results as a table with title, company, location, salary and link.

Example:

> Use the Orgupdate Dice jobs scraper to find "DevOps engineer" jobs in Austin,
> USA, posted this month. Fetch 3 pages and show the results as a table with
> title, company, location, salary and link.

### What Claude does

1. Finds the Actor (`orgupdate/dice-jobs-scraper`) — instantly if it is pinned in
   your connector URL, otherwise via a quick `search-actors` call.
2. Builds the input JSON from your sentence.
3. Calls `call-actor`, which starts the run **on your Apify account**.
4. Waits for the run to finish, reads the dataset, and formats the answer.

A typical run takes from a few seconds to a couple of minutes depending on
`pagesToFetch`.

---

## Being specific

You can control any input directly:

> Run the Orgupdate Reed jobs scraper. Keywords: "project manager, prince2".
> Location: Birmingham. Country: uk. Job type: full-time. Posted in the last
> 3 days. Pages: 5.

Or restrict to one employer:

> Use the Orgupdate Workday jobs scraper to list every open role at "Salesforce"
> in the United States posted this month.

---

## Reading and reshaping results

After a run, the data is in the conversation. Ask follow‑ups without re‑running:

- *"Sort by salary, highest first."*
- *"Only show roles that mention Kubernetes."*
- *"Group by company and count."*
- *"Drop anything without an apply link."*
- *"Give me the 10 best matches for a senior backend engineer and say why."*

---

## Exporting

Claude can hand you the data in whatever form you need:

| Ask for | You get |
|---|---|
| *"…as a CSV"* | CSV text you can paste into a spreadsheet |
| *"…as a Markdown table"* | A table you can drop into a doc or issue |
| *"…as JSON"* | Raw array of objects |
| *"…as a shortlist with notes"* | A written summary per role |

The raw dataset also stays on Apify. In **Apify Console → Storage → Datasets**
you can download the same run as JSON, CSV, Excel, XML, or HTML, or pull it from
the dataset API.

---

## Cost

Orgupdate Actors use **pay‑per‑result** pricing:

- You are charged per job result returned, plus a tiny automatic actor‑start fee
  (about `$0.0001`) per run.
- A run that returns **no** results costs only that start fee.
- More `pagesToFetch` → more results → higher cost. Start small.

Check your usage any time in **Apify Console → Billing**.

### Agent payments (x402)

The Actors support the **x402** protocol, so an AI agent or MCP client can pay
for runs in USDC (on Base) without an Apify account or API token. For normal
Claude use with the connector, you are simply billed through your Apify account —
x402 is only relevant if you are building autonomous agents.

---

## Running more than one source

You can ask Claude to run several scrapers in sequence:

> Run the Orgupdate Indeed, LinkedIn and Dice jobs scrapers for "machine learning
> engineer" in Seattle, USA, posted this week (1 page each). Merge the results,
> remove duplicates by URL, and show one combined table.

For a structured way to cover the **whole market** — every relevant board, with
ranking, de‑duplication and a tracker — use the
[how-to-scrap-orgupdate](https://github.com/orgupdate/how-to-scrap-orgupdate)
playbook.
