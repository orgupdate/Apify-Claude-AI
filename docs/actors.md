# Orgupdate job Actors — catalogue

Every Orgupdate job scraper on the Apify Store, the source it reads, and the MCP
URL that pins it as a Claude tool.

All Actors share the **same input schema** and the **same output shape** — see
[inputs-and-outputs.md](inputs-and-outputs.md). That means once you know how to
drive one, you know how to drive all of them.

---

## Full list

| Source site | Apify slug | Best for |
|---|---|---|
| Google Jobs | `orgupdate/google-jobs-scraper` | Broad aggregation — Google pulls from LinkedIn, Indeed, Glassdoor, ZipRecruiter and company pages |
| Indeed | `orgupdate/indeed-jobs-scraper` | One of the largest job boards worldwide, all industries |
| LinkedIn | `orgupdate/linkedin-jobs-scraper` | Professional and corporate roles |
| Dice | `orgupdate/dice-jobs-scraper` | US technology, engineering and IT roles |
| Glassdoor | `orgupdate/glassdoor-jobs-scraper` | Roles alongside company ratings and salary data |
| Monster | `orgupdate/monster-jobs-scraper` | General job board, all industries and levels |
| ZipRecruiter | `orgupdate/ziprecruiter-jobs-scraper` | US marketplace distributed across 100+ partner sites |
| SimplyHired | `orgupdate/simplyhired-jobs-scraper` | Aggregator across thousands of boards and company pages |
| Reed | `orgupdate/reed-jobs-scraper` | UK — the largest independent UK job site |
| Totaljobs | `orgupdate/totaljobs-jobs-scraper` | UK — nationwide roles across all sectors |
| Caterer.com | `orgupdate/caterer-jobs-scraper` | UK hospitality, catering and food‑service |
| Welcome to the Jungle | `orgupdate/welcome-to-the-jungle-jobs-scraper` | Europe — rich employer profiles |
| Wellfound | `orgupdate/wellfound-jobs-scraper` | Startups (formerly AngelList Talent) |
| We Work Remotely | `orgupdate/we-work-remotely-jobs-scraper` | Remote‑only roles in tech, support, marketing, design |
| Remote.co | `orgupdate/remote-co-jobs-scraper` | Hand‑curated fully remote jobs |
| FlexJobs | `orgupdate/flexjobs-jobs-scraper` | Remote, hybrid and flexible‑schedule roles |
| Upwork | `orgupdate/upwork-jobs-scraper` | Freelance, contract and project work |
| Handshake | `orgupdate/handshake-jobs-scraper` | Students and recent graduates |
| Workday | `orgupdate/workday-jobs-scraper` | Public Workday career sites (myworkdayjobs.com) used by large enterprises |
| Workable | `orgupdate/workable-jobs-scraper` | Public job pages hosted on Workable (jobs.workable.com) |

> Slugs use the `orgupdate/` namespace. If you fork or self‑publish an Actor,
> replace `orgupdate` with your own Apify username.

---

## Pinning one Actor as a tool

Add the slug to the connector URL after `actors,docs`:

```
https://mcp.apify.com/?tools=actors,docs,orgupdate/dice-jobs-scraper
```

Pinned Actors have their input schema loaded immediately, so Claude does not need
a discovery step before the first run.

## Pinning several Actors

Comma‑separate them:

```
https://mcp.apify.com/?tools=actors,docs,orgupdate/indeed-jobs-scraper,orgupdate/reed-jobs-scraper,orgupdate/we-work-remotely-jobs-scraper
```

Keep the list short (2–4). For anything broader, use just `?tools=actors,docs`
and let Claude discover Actors by name at run time — for example:

> Run the Orgupdate Wellfound jobs scraper for "backend engineer", remote, posted this month.

Claude will call `search-actors`, find `orgupdate/wellfound-jobs-scraper`, and
run it.

---

## Which source should I use?

| If you want… | Start with |
|---|---|
| The widest net in one call | `google-jobs-scraper`, then `indeed-jobs-scraper` |
| US tech roles | `dice-jobs-scraper`, `linkedin-jobs-scraper` |
| UK roles | `reed-jobs-scraper`, `totaljobs-jobs-scraper` |
| Remote‑only roles | `we-work-remotely-jobs-scraper`, `remote-co-jobs-scraper`, `flexjobs-jobs-scraper` |
| Startup roles | `wellfound-jobs-scraper`, `welcome-to-the-jungle-jobs-scraper` |
| Freelance / contract | `upwork-jobs-scraper` |
| Early‑career / graduate | `handshake-jobs-scraper` |
| A specific big employer | `workday-jobs-scraper` or `workable-jobs-scraper` with `companyName` set |

To sweep **all** relevant sources for one search brief, follow the
[how-to-scrap-orgupdate](https://github.com/orgupdate/how-to-scrap-orgupdate)
playbook.
