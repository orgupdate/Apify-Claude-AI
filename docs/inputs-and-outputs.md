# Inputs and outputs

Every Orgupdate job Actor takes the same input and returns the same fields. This
page is the reference; you rarely type JSON yourself — you describe what you want
and Claude fills the input in for you.

---

## Input parameters

| Parameter | Type | Required | Description | Example |
|---|---|---|---|---|
| `includeKeyword` | string | yes (in practice) | Search terms, job title, or skills. Comma‑separated values are supported. | `"product manager"`, `"react, node.js"` |
| `locationName` | string | yes | City, state, or region to search in. | `"London"`, `"New York, NY"` |
| `countryName` | string | yes | Country context for the search. | `"usa"`, `"uk"`, `"germany"`, `"all"` |
| `pagesToFetch` | integer | yes | How many result pages to walk. Higher = more results and higher cost. | `1`, `3`, `5` |
| `companyName` | string | no | Restrict results to a single employer. | `"Microsoft"` |
| `jobType` | string | no | Employment type. One of `FULLTIME`, `PARTTIME`, `CONTRACTOR`, `INTERN`. | `"FULLTIME"` |
| `datePosted` | string | no | Recency filter. One of `all`, `today`, `3days`, `week`, `month`. | `"week"` |
| `targetLocations` | array of strings | no *(supported on Google, Indeed‑style, Caterer, SimplyHired, Workday, Workable)* | Extra cities to search in the same run. | `["Austin", "Denver"]` |

### Example input JSON

```json
{
  "includeKeyword": "software engineer, python",
  "locationName": "new york",
  "countryName": "usa",
  "companyName": "",
  "jobType": "FULLTIME",
  "datePosted": "week",
  "pagesToFetch": 3
}
```

---

## Output fields

Results land in an Apify **dataset**. Each item looks like this:

```json
{
  "job_title": "Senior Frontend Developer",
  "company_name": "Tech Corp Inc.",
  "location": "New York, NY (Remote)",
  "posted_via": "LinkedIn",
  "salary": "$120,000 - $150,000 a year",
  "date": "2025-03-25",
  "job_type": "Full-time",
  "URL": "https://www.indeed.com/viewjob?jk=..."
}
```

| Field | Meaning |
|---|---|
| `job_title` | Role title as published by the employer |
| `company_name` | Hiring organisation |
| `location` | City / region, or `Remote` where stated |
| `posted_via` | The board or source the listing was found on |
| `salary` | Pay or pay range, when the employer provides one |
| `date` | Posting date |
| `job_type` | Full‑time / part‑time / contract / internship, when stated |
| `URL` | Direct link to the listing or application page |

Not every listing has every field — `salary`, `job_type`, and an exact `date`
vary by posting. When you ask Claude for a table, tell it how to handle blanks
(e.g. *"leave salary empty if not listed"*).

---

## How plain English maps to the input

| You say to Claude | Input Claude builds |
|---|---|
| "remote React jobs in Germany posted this week" | `includeKeyword: "react"`, `locationName: "Germany"` (or a city), `countryName: "germany"`, `datePosted: "week"` |
| "full-time nurse roles in Manchester, UK, first 5 pages" | `includeKeyword: "nurse"`, `locationName: "Manchester"`, `countryName: "uk"`, `jobType: "FULLTIME"`, `pagesToFetch: 5` |
| "what is Stripe hiring for in the US right now" | `companyName: "Stripe"`, `countryName: "usa"`, `locationName: "United States"`, `datePosted: "month"` |
| "internships for data science students, anywhere" | `includeKeyword: "data science"`, `jobType: "INTERN"`, `countryName: "all"`, `locationName: "United States"` |

### Tips that improve results

- **Use a job‑title style query.** `"registered nurse"` beats
  `"caring hospital role for a qualified nurse"`.
- **Always give a location.** Most sources return little or nothing for an empty
  location; if you only have a country, use the country name as the location too.
- **Start with `pagesToFetch: 1`** to sanity‑check the query, then increase.
- **Widen `datePosted`** if you get too few results; narrow it (`today`, `3days`)
  for scheduled runs so you only see new postings.
