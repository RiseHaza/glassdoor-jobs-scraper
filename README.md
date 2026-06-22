[Glassdoor Jobs Scraper](https://apify.com/parseforge/glassdoor-jobs-scraper?fpr=data)

![ParseForge Banner](https://images.apifyusercontent.com/P72M168tNYRUI4-For2DJl7v_jfpX5sdZNMVVrywgJE/w:1800/cb:1/aHR0cHM6Ly9hcGlmeS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vNVU4T0lMOFNwUzlQY2pQODRWZzBRanJINkpGWTFEVUFfaW1hZ2UucG5n.webp)

# 🚀 Glassdoor Jobs Scraper

> 🚀 **Scrape job listings from Glassdoor. Search by keyword, location, or company name. Extracts job title, salary, description, skills, location with coordinates, company rating, logo, apply URL, remote wo**.

> 🕒 **Last updated:** 2026-04-24 · **📊 12+ fields** per record · **🔍 6 filters** · **🚫 No auth** required

Scrape job listings from Glassdoor. Search by keyword, location, or company name. Extracts job title, salary, description, skills, location with coordinates, company rating, logo, apply URL, remote work type, education and experience requirements.

Supports pagination and full job detail enrichment.

---

## 📋 What the Glassdoor Jobs Scraper does

- 🎯 **Targeted filtering.** Use the input schema to narrow results to what you need.
- 📦 **Structured output.** Clean, typed records with every field documented.
- 🔄 **Live data.** Every run fetches fresh data at runtime, no cached responses.
- 🔌 **Easy integration.** Consume via Apify API, webhooks, or direct dataset export.
- 📊 **Scale on demand.** Run once or run on a schedule, the same way.

> 💡 **Why it matters:** teams that rely on this source no longer need to babysit a custom crawler. Set up your filters once, get updated data on demand.

---

## ⚙️ Input

Send a JSON body with any of the documented input fields. All fields are optional unless the schema marks them required.

| Field | Type | Name | Description |
| --- | --- | --- | --- |
| `startUrl` | string | Start URL | Direct Glassdoor job search URL. Use this OR the keyword/company fields below. |
| `maxItems` | integer | Max Items | Free users: Limited to 100. Paid users: Optional, max 1,000,000 |
| `keyword` | string | Job Keyword | Search keyword for job listings. Example: software engineer, data analyst, product manager |
| `location` | string | Location | Location filter for job search. Example: New York, San Francisco, London |
| `companyName` | string | Company Name | Search for jobs at a specific company. Example: Google, Apple, Microsoft |
| `includeJobDetails` | boolean | Include Job Descriptions | Fetch full job descriptions from detail pages. Slower but provides complete job information. |
| `proxyConfiguration` | object | Proxy Configuration | Residential proxies are required for Glassdoor. |

> ⚠️ **Good to Know:** free users are limited to 10 items per run for preview purposes. Upgrade to Apify paid plans for higher limits.

---

## 📊 Output

The dataset returns one structured record per item. Each record includes identifiers, descriptive fields, and a link back to the source. Consume the dataset as JSON, CSV, Excel, XML, or RSS via the Apify console or API.

---

## 💼 Business use cases

| ### 📊 Analysts and researchers     - Build longitudinal datasets for trend analysis - Benchmark across sources and regions - Feed BI tools and custom dashboards - Enrich existing pipelines with fresh data | ### 🛠️ Engineers and operators     - Power internal APIs without building your own crawler - Schedule weekly deltas to a database - Plug into existing ETL stacks via Apify webhooks - Skip the infra work, get clean structured output |
| --- | --- |
| ### 🎯 Growth and sales teams     - Discover new leads and accounts at scale - Monitor competitor coverage and positioning - Build outbound lists keyed to real signals - Prioritize outreach with structured context | ### 🧪 Product and data teams     - Prototype features against live data - A/B test ranking or matching logic - Train or evaluate domain-specific models - Validate hypotheses before committing engineering |

---

## 🌟 Beyond business use cases

Data like this powers more than commercial workflows. The same structured records support research, education, civic projects, and personal initiatives.

| ### 🎓 Research and academia     - Empirical datasets for papers, thesis work, and coursework - Longitudinal studies tracking changes across snapshots - Reproducible research with cited, versioned data pulls - Classroom exercises on data analysis and ethical scraping | ### 🎨 Personal and creative     - Side projects, portfolio demos, and indie app launches - Data visualizations, dashboards, and infographics - Content research for bloggers, YouTubers, and podcasters - Hobbyist collections and personal trackers |
| --- | --- |
| ### 🤝 Non-profit and civic     - Transparency reporting and accountability projects - Advocacy campaigns backed by public-interest data - Community-run databases for local issues - Investigative journalism on public records | ### 🧪 Experimentation     - Prototype AI and machine-learning pipelines with real data - Validate product-market hypotheses before engineering spend - Train small domain-specific models on niche corpora - Test dashboard concepts with live input |

---

## ✨ Why choose this Actor

|  | Capability |
| --- | --- |
| 🎯 | **Built for the job.** Scoped specifically to this data source so you skip the parser engineering entirely. |
| 🔖 | **Structured output.** Clean, typed fields ready for analysis, dashboards, or downstream pipelines. |
| ⚡ | **Fast.** Optimized request patterns return results in seconds, not minutes. |
| 🔁 | **Always fresh.** Every run pulls live data, so the dataset reflects the source as of run time. |
| 🌐 | **No infra to manage.** Apify handles proxies, retries, scaling, scheduling, and storage. |
| 🛡️ | **Reliable.** Battle-tested across many runs and edge cases, with graceful error handling. |
| 🚫 | **No code required.** Configure in the UI, run from CLI, schedule via cron, or call from any language with the Apify SDK. |

> 📊 Production-grade structured data without the engineering overhead of building and maintaining your own scraper.

---

## 📈 How it compares to alternatives

| Approach | Cost | Coverage | Refresh | Filters | Setup |
| --- | --- | --- | --- | --- | --- |
| **⭐ Glassdoor Jobs Scraper** *(this Actor)* | $5 free credit, then pay-per-use | Full source coverage | **Live per run** | Source-native filters supported | ⚡ 2 min |
| Build your own scraper | Engineering hours | Full once built | Whenever you maintain it | Custom code | 🐢 Days to weeks |
| Paid managed APIs | $$$ monthly | Vendor-defined | Live | Vendor-defined | ⏳ Hours |
| Third-party data dumps | Varies | Subset, often stale | Periodic | None | 🕒 Variable |

Pick this Actor when you want broad coverage, server-side filtering, and no pipeline maintenance.

---

## 🚀 How to use

1. 📝 **Create a free account.** Sign up at [console.apify.com](https://console.apify.com/sign-up?fpr=vmoqkp) to get $5 in credits.
2. 🔍 **Open the actor.** Paste your filters into the input schema in the Apify console.
3. ▶️ **Click Start.** Wait a few seconds for the first records to land.
4. 📤 **Export the data.** Download JSON/CSV or pipe to webhooks, Google Sheets, or Zapier.
5. 🔄 **Schedule it.** Apify Schedules let you rerun on a cron cadence for free.

> ⏱️ Total time to first data: about 60 seconds.

---

## 🤖 Ask an AI assistant about this scraper

Open a ready-to-send prompt about this ParseForge actor in the AI of your choice:

- 💬 [**ChatGPT**](https://chat.openai.com/?q=How%20do%20I%20use%20the%20GLASSDOOR%20JOBS%20SCRAPER%20Scraper%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🧠 [**Claude**](https://claude.ai/new?q=How%20do%20I%20use%20the%20GLASSDOOR%20JOBS%20SCRAPER%20Scraper%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🔍 [**Perplexity**](https://perplexity.ai/search?q=How%20do%20I%20use%20the%20GLASSDOOR%20JOBS%20SCRAPER%20Scraper%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🅒 [**Copilot**](https://copilot.microsoft.com/?q=How%20do%20I%20use%20the%20GLASSDOOR%20JOBS%20SCRAPER%20Scraper%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)

---

## ❓ Frequently Asked Questions

### 🔍 What does the Glassdoor Jobs do?

Scrape job listings from Glassdoor. Search by keyword, location, or company name. Extracts job title, salary, description, skills, location with coordinates, company rating, logo, apply URL, remote work type, education and experience requirements. Supports pagination and full job. Pass your filters via the input schema and run the actor.

### 🛠️ How do I get started?

Open the actor in Apify, fill in the input fields, and click Start. The dataset appears on your run page within seconds.

### 💰 How much does it cost?

Free Apify users can run the actor and preview up to 10 records. Paid plans remove the preview cap. See the Apify pricing page for details.

### 📅 How fresh is the data?

Every run scrapes live from the source at runtime. No cached responses, no pre-loaded dumps. You get the snapshot visible to the source when the actor starts.

### 🗂️ What filters are supported?

The input schema exposes startUrl, keyword, location, companyName, includeJobDetails. Combine them to narrow results. If a filter is empty, the default ordering from the source is used.

### 🔐 Do I need an API key, account, or authentication?

No. The actor runs against public endpoints using Apify residential proxies. You just need your Apify account to launch the run.

### 🧾 What fields are returned per record?

Each record includes the primary identifiers, descriptive fields, URLs to the source page, and any structured data the source exposes. Exact fields depend on the source and are documented in the output schema.

### ⚡ How fast is a run?

Most runs return a first batch of records within a minute. Throughput depends on source rate limits and the number of filters stacked, not on Apify.

### 📤 Can I export the dataset?

Yes. Apify exposes the dataset as JSON, CSV, XML, Excel, or RSS via the UI or API. You can also stream new records into webhooks, Google Sheets, Airtable, and more.

### 🧭 Can I schedule recurring runs?

Yes. Apify Schedules let you run this actor on a cron cadence and deliver fresh data to your destination. No extra code is required.

### 🛡️ Is scraping this source legal for commercial use?

This actor only retrieves publicly available information. You are responsible for complying with the source website terms and any applicable privacy and competition rules in your jurisdiction.

### 🤝 What if a run fails or returns fewer items than expected?

Open the run log for the exact error. Most failures come from source rate limits or filter combinations with no matches. Retry with a broader filter or contact support via the Tally form below.

---

## 🔌 Integrate with any app

Connect the Glassdoor Jobs Scraper to cloud services via [Apify integrations](https://apify.com/integrations):

- [**Make**](https://docs.apify.com/platform/integrations/make) - visual automation builder
- [**Zapier**](https://docs.apify.com/platform/integrations/zapier) - 5000+ app connectors
- [**Google Sheets**](https://docs.apify.com/platform/integrations/drive) - pipe rows directly
- [**Airbyte**](https://docs.apify.com/platform/integrations/airbyte) - ingest into data warehouses
- [**Slack**](https://docs.apify.com/platform/integrations/slack) - receive run alerts
- [**HTTP webhooks**](https://docs.apify.com/platform/integrations/webhooks) - custom downstream

---

## 🔗 Recommended Actors

Pair the Glassdoor Jobs Scraper with related actors:

- [**🌐 Website Content Crawler**](https://apify.com/parseforge/website-content-crawler) - crawl any page at scale
- [**🔍 Google Search Scraper**](https://apify.com/parseforge/google-search-scraper) - harvest SERPs
- [**📄 Article Extractor**](https://apify.com/parseforge/article-extractor) - extract clean article text
- [**📊 Google Trends Scraper**](https://apify.com/parseforge/google-trends-scraper) - capture demand signals
- [**📸 Screenshot URL**](https://apify.com/parseforge/screenshot-url) - render any page to image

> 💡 **Pro Tip:** browse the complete [ParseForge collection](https://apify.com/parseforge) for more niche actors.

---

**🆘 Need Help?** [**Open our contact form**](https://tally.so/r/BzdKgA)

---

> ⚠️ **Disclaimer:** This actor retrieves data from publicly available sources. You are responsible for complying with the source website's terms of service and applicable laws in your jurisdiction. ParseForge is not affiliated with the data source.