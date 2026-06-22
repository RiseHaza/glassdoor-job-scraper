[Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=data)

## What does Glassdoor Job Scraper do?

Glassdoor Job Scraper extracts structured job data from [glassdoor.com](https://glassdoor.com) — including salary data, contact details, company metadata, full descriptions, remote-work indicators, location data, and ratings and reviews. It supports keyword search, location filters, and controllable result limits, so you can run the same query consistently over time. The actor also offers detail enrichment (full descriptions, company profiles, and contact information) where the source provides them.

**New to Apify?** [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) and use the included $5 monthly platform credit to test this actor.

## Key features

- **Incremental mode** — recurring runs emit and charge only for listings that are new or whose tracked content changed. First run builds the baseline state; subsequent runs emit only new or changed records.
- **Detail enrichment** — full descriptions, company profiles, and contact information where the source provides them.
- **Compact mode** — AI-agent and MCP-friendly payloads with core fields only.

## What data can you extract from glassdoor.com?

Each result includes Core listing fields (`jobId`, `jobKey`, `title`, `location`, `salaryText`, `salaryMin`, `salaryMax`, and `salaryCurrency`, and more), detail fields when enrichment is enabled (`description`, `descriptionHtml`, `descriptionLength`, `benefits`, and `detailFetched`), contact and apply information (`applyUrl` and `extractedEmails`), and company metadata (`company`, `companyUrl`, `companyRating`, and `companyReviewsCount`). In standard mode, all fields are always present — unavailable data points are returned as `null`, never omitted. In compact mode, only core fields are returned.

Enable detail enrichment in the input to get richer fields such as full descriptions, company profiles, and contact information where the source provides them.

## Input

The main inputs are a search keyword, an optional location filter, and a result limit. Additional filters and options are available in the input schema.

Key parameters:

- **`query`** — Job search keywords. Use JSON array for multi-query.
- **`country`** — Which Glassdoor domain to search (21 markets). (default: `"US"`)
- **`location`** — City, state, or region. Use JSON array for multi-location.
- **`startUrls`** — Direct Glassdoor search or job detail URLs.
- **`maxResults`** — Maximum total job listings to return. Uses 1024 MB memory for ≤25 results, 2048 MB for 26+. (default: `25`)
- **`maxPages`** — Maximum SERP pages to scrape per search source. (default: `5`)
- **`postedDays`** — Only return jobs posted within this many days. Snapped to nearest valid: 1, 3, 7, or 14.
- **`jobType`** — Filter by employment type.
- **`remoteFilter`** — Filter by remote work arrangement.
- **`radius`** — Radius around the location in miles/km (5, 10, 15, 25, 35, 50, or 100). Snapped to nearest valid value.
- **`sort`** — Sort results by relevance or posting date. (default: `"relevance"`)
- **`includeDetails`** — Fetch each job's detail page for full description, salary data, and company info. (default: `true`)
- ...and 8 more parameters

### Input examples

**Basic search** — Keyword-driven search with a result cap.

→ Full payload per result — all standard fields populated where the source provides them.

```
{
  "query": "software engineer",
  "maxResults": 50
}
```

**Incremental tracking** — Only emit jobs that changed since the previous run with this `stateKey`.

→ First run builds the baseline state. Subsequent runs emit only records that are new or whose tracked content changed. Set `emitUnchanged: true` to include unchanged records as well.

```
{
  "query": "software engineer",
  "maxResults": 200,
  "incrementalMode": true,
  "stateKey": "software-engineer-tracker"
}
```

**Compact filtered output** — Combine filters with compact mode for a lightweight AI-agent or MCP data source.

→ Core fields only — ideal for piping into LLMs or downstream tools without token overhead.

```
{
  "query": "software engineer",
  "jobType": "fulltime",
  "maxResults": 50,
  "compact": true
}
```

## Output

Each run produces a dataset of structured job records. Results can be downloaded as JSON, CSV, or Excel from the Dataset tab in Apify Console.

### Example job record

```
{
  "jobId": "a3ab7c825d9e6d2e3bfaa653dfdadb1c71b569453fe20ec70e9271e962a82dc2",
  "jobKey": "1010090472882",
  "title": "AI Manager",
  "company": "Leonard Truck & Trailer",
  "companyUrl": null,
  "location": "North Jackson, OH",
  "description": "Leonard Truck & Trailer is a family-owned and operated dealership specializing in trucks and trailers, established in 1963. We pride ourselves on building trusting relationships with our employees, cu...",
  "descriptionHtml": "<p>Leonard Truck &amp; Trailer is a family-owned and operated dealership specializing in trucks and trailers, established in 1963. We pride ourselves on building trusting relationships with our employ...",
  "descriptionLength": 2930,
  "salaryText": "USD 25.38–30.57 HOURLY",
  "salaryMin": 25.379808,
  "salaryMax": 30.570192,
  "salaryCurrency": "USD",
  "salaryType": "HOURLY",
  "employmentType": "Full-time",
  "postedDate": "2026-04-04",
  "validThrough": null,
  "canonicalUrl": "https://www.glassdoor.com/job-listing/ai-manager-leonard-truck-trailer-JV_IC1146396_KO0,10_KE11,32.htm?jl=1010090472882",
  "applyUrl": "https://www.glassdoor.com/partner/jobListing.htm?pos=101&ao=1110586&tgt=APPLY_START&s=58&guid=0000019d5a700f54853a18cbd35c5258&src=GD_JOB_VIEW&t=NS&vt=w&ea=1&cs=1_9727b676&cb=1775338786751&jobListingI...",
  "requirements": [],
  "benefits": [],
  "portalUrl": "https://www.glassdoor.com",
  "sourceUrl": "https://www.glassdoor.com/job-listing/ai-manager-leonard-truck-trailer-JV_IC1146396_KO0,10_KE11,32.htm?jl=1010090472882",
  "sourceCountry": "US",
  "sourceDomain": "www.glassdoor.com",
  "searchQuery": "software engineer",
  "searchUrl": "https://www.glassdoor.com/Job/jobs.htm?sc.keyword=software+engineer&locT=&locKeyword=New+York",
  "isSponsored": false,
  "locationCity": "North Jackson, OH",
  "locationRegion": "Ohio",
  "locationCountry": "United States",
  "postalCode": null,
  "isRemote": false,
  "locationFormatted": "North Jackson, OH",
  "companyRating": 1.9,
  "companyReviewsCount": null,
  "companyLogoUrl": "https://media.glassdoor.com/sql/1718860/leonard-truck-and-trailer-squarelogo-1633681945375.png",
  "scrapedAt": "2026-04-04T21:38:26.917Z",
  "detailFetched": true,
  "contentQuality": "full",
  "extractedEmails": [],
  "latitude": 41.1,
  "longitude": -80.8575,
  "companyIndustry": "Vehicle Dealers",
  "companyEmployeeRange": "Unknown",
  "companyEmployeeRangeRaw": "Unknown",
  "companySectorNames": [
    "Retail & Wholesale"
  ],
  "companyRevenue": "Unknown / Non-Applicable",
  "companyFoundedYear": null,
  "companyHeadquarters": "North Jackson, OH",
  "companyWebsite": "https://www.leonardtrailers.com",
  "companyOpenJobsCount": null,
  "companyDescription": null,
  "companyCeo": "Clint Leonard",
  "changeType": null,
  "trackedHash": null,
  "firstSeenAt": null,
  "lastSeenAt": null,
  "previousSeenAt": null,
  "expiredAt": null,
  "stateKey": null
}
```

### Incremental fields

When `incremental: true`, each record also carries:

- `changeType` — one of `NEW`, `UPDATED`, `UNCHANGED`, `REAPPEARED`, `EXPIRED`. Default output covers `NEW` / `UPDATED` / `REAPPEARED`; set `emitUnchanged: true` or `emitExpired: true` to opt into the others.
- `firstSeenAt`, `lastSeenAt` — ISO-8601 timestamps tracking the listing across runs.
- `isRepost`, `repostOfId`, `repostDetectedAt` — populated when a new listing matches the tracked content of a previously expired one. Set `skipReposts: true` to drop detected reposts from the output.

## How to scrape glassdoor.com

1. Go to [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) in Apify Console.
2. Enter a search keyword and optional location filter.
3. Set `maxResults` to control how many results you need.
4. Enable `includeDetails` if you need full descriptions, contact info, or company data.
5. Click **Start** and wait for the run to finish.
6. Export the dataset as JSON, CSV, or Excel.

## Use cases

- Extract job data from glassdoor.com for market research and competitive analysis.
- Track salary trends across regions and categories over time.
- Monitor new and changed listings on scheduled runs without processing the full dataset every time.
- Build outreach lists using contact details and apply URLs from listings.
- Research company hiring patterns, employer profiles, and industry distribution.
- Use structured location data for regional analysis, mapping, and geo-targeting.
- Feed structured data into AI agents, MCP tools, and automated pipelines using compact mode.
- Export clean, structured data to dashboards, spreadsheets, or data warehouses.
- Collect ratings and reviews for reputation monitoring and benchmarking.

## How much does it cost to scrape glassdoor.com?

Glassdoor Job Scraper uses [pay-per-event](https://docs.apify.com/platform/actors/paid-actors/pay-per-event) pricing. You pay a small fee when the run starts and then for each result that is actually produced.

- **Run start:** $0.01 per run
- **Per result:** $0.002 per job record

Example costs:

- 10 results: **$0.03**
- 100 results: **$0.21**
- 500 results: **$1.01**

### Example: recurring monitoring savings

These examples compare full re-scrapes with incremental runs at different churn rates. Churn is the share of listings that are new or whose tracked content changed since the previous run. Actual churn depends on your query breadth, source activity, and polling frequency — the scenarios below are examples, not predictions.

Example setup: 100 results per run, daily polling (30 runs/month). Event-pricing examples scale linearly with result count.

| Churn rate | Full re-scrape run cost | Incremental run cost | Savings vs full re-scrape | Monthly cost after baseline |
| --- | --- | --- | --- | --- |
| 5% — stable niche query | $0.21 | $0.02 | $0.19 (90%) | $0.60 |
| 15% — moderate broad query | $0.21 | $0.04 | $0.17 (81%) | $1.20 |
| 30% — high-volume aggregator | $0.21 | $0.07 | $0.14 (67%) | $2.10 |

Full re-scrape monthly cost at daily polling: $6.30. First month with incremental costs $0.79 / $1.37 / $2.24 for the 5% / 15% / 30% scenarios because the first run builds baseline state at full cost before incremental savings apply.

 

## FAQ

### How many results can I get from glassdoor.com?

The number of results depends on the search query and available listings on glassdoor.com. Use the `maxResults` parameter to control how many results are returned per run.

### Does Glassdoor Job Scraper support recurring monitoring?

Yes. Enable incremental mode to only receive new or changed listings on subsequent runs. This is ideal for scheduled monitoring where you want to track changes over time without re-processing the full dataset.

### Can I integrate Glassdoor Job Scraper with other apps?

Yes. Glassdoor Job Scraper works with Apify's [integrations](https://apify.com/integrations?fpr=1h3gvi) to connect with tools like Zapier, Make, Google Sheets, Slack, and more. You can also use webhooks to trigger actions when a run completes.

### Can I use Glassdoor Job Scraper with the Apify API?

Yes. You can start runs, manage inputs, and retrieve results programmatically through the [Apify API](https://docs.apify.com/api/v2). Client libraries are available for JavaScript, Python, and other languages.

### Can I use Glassdoor Job Scraper through an MCP Server?

Yes. Apify provides an [MCP Server](https://apify.com/apify/actors-mcp-server?fpr=1h3gvi) that lets AI assistants and agents call this actor directly. Use compact mode and `descriptionMaxLength` to keep payloads manageable for LLM context windows.

### Is it legal to scrape glassdoor.com?

This actor extracts publicly available data from glassdoor.com. Web scraping of public information is generally considered legal, but you should always review the target site's terms of service and ensure your use case complies with applicable laws and regulations, including GDPR where relevant.

### Your feedback

If you have questions, need a feature, or found a bug, please [open an issue](https://apify.com/blackfalcondata/glassdoor-job-scraper/issues?fpr=1h3gvi) on the actor's page in Apify Console. Your feedback helps us improve.

## You might also like

- [Actiris Brussels Job Scraper](https://apify.com/blackfalcondata/actiris-scraper?fpr=1h3gvi) — Scrape all active job listings from actiris.brussels — official Brussels public employment service..
- [Adzuna Job Scraper](https://apify.com/blackfalcondata/adzuna-scraper?fpr=1h3gvi) — Scrape adzuna.com - the global job board with 20+ country markets. Structured salary.
- [APEC.fr Scraper - French Executive Jobs](https://apify.com/blackfalcondata/apec-scraper?fpr=1h3gvi) — Scrape apec.fr - French executive job listings with salary ranges, company, location, skills,.
- [Arbeitsagentur Scraper - German Jobs](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Scrape arbeitsagentur.de - Germany’s official employment portal with 1M+ listings. Contact data,.
- [Arbetsformedlingen Job Scraper](https://apify.com/blackfalcondata/arbetsformedlingen-scraper?fpr=1h3gvi) — Scrape arbetsformedlingen.se (Platsbanken) — Sweden's official employment portal. Returns 84.
- [AutoScout24 Scraper](https://apify.com/blackfalcondata/autoscout24-scraper?fpr=1h3gvi) — Scrape autoscout24.com - Europe's largest used car marketplace with 770K+ listings. Structured.
- [Bayt.com Scraper - Jobs from the Middle East](https://apify.com/blackfalcondata/bayt-scraper?fpr=1h3gvi) — Scrape bayt.com - the leading Middle East job board. Salary data, experience requirements.
- [Bilbasen Scraper - Denmark’s Car Marketplace](https://apify.com/blackfalcondata/bilbasen-scraper?fpr=1h3gvi) — Scrape bilbasen.dk - Denmark’s largest car marketplace. Full vehicle specifications, seller.

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open this actor and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).