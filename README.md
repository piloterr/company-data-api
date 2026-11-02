<p align="center">
  <a href="https://www.piloterr.com"><img src="images/banner.png" alt="Company Database Scraper API by Piloterr – scrape Company Database data as JSON" width="100%"></a>
</p>

# Company Database Scraper API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/Piloterr-Get%20a%20free%20API%20key-111827)](https://app.piloterr.com) [![API docs](https://img.shields.io/badge/Docs-OpenAPI-0EA5E9)](https://app.piloterr.com/openapi) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **Piloterr Company Database Scraper API** lets you extract public data from Company Database as **clean, structured JSON** — no proxies, headless browsers or HTML parsing to maintain. Endpoints available in production:

- **Company Database API** — Retrieve comprehensive company data including financials, technologies, social profiles, and location by domain name.

Use it for lead generation, CRM enrichment, market mapping, investment research or job market analytics.

| Endpoint | Path | Credits | What you get |
|---|---|---|---|
| [Company Database API](#company-database-api) | `/v2/company` | 1 | Retrieve comprehensive company data including financials, technologies, social profiles, and location by domain name. |

## Table of contents

- [How it works](#how-it-works)
- [Company Database API](#company-database-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Practical use cases](#practical-use-cases)
- [Why Piloterr?](#why-piloterr)
- [FAQ](#faq)
- [Related scrapers](#related-scrapers)
- [Support](#support)

## How it works

1. **Create a free Piloterr account** and copy your API key from the [dashboard](https://app.piloterr.com).
2. **Send a `GET` (or `POST`) request** to `https://api.piloterr.com/v2/...` with the header `x-api-key: YOUR_API_KEY`.
3. **Receive structured JSON** — Piloterr handles rendering, proxies, retries and parsing.

```bash
export PILOTERR_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

> Every endpoint accepts both `GET` (query string) and `POST` (JSON body with the same fields).

## Company Database API

Retrieve comprehensive company data including financials, technologies, social profiles, and location by domain name.

`GET | POST https://api.piloterr.com/v2/company` · **1 credit per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | The domain name of the company to look up. Accepts multiple formats: |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/company",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "gucci.com",
    },
    timeout=120,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type CompanyDatabase = {
  name?: string;
  domain?: string;
  founded?: number;
  revenue?: string;
  location?: {
    lat?: string;
    lng?: string;
    city?: string;
    address?: unknown;
    country?: string;
    postcode?: string;
    country_code?: string;
  };
  domain_tld?: string;
  industries?: string[];
  updated_at?: unknown;
  description?: string;
  domain_name?: string;
  staff_range?: string;
  phone_number?: string;
  technologies?: string[];
  business_type?: unknown;
  social_networks?: {
    twitter?: string;
    youtube?: string;
    facebook?: string;
    linkedin?: string;
    instagram?: string;
    pinterest?: string;
    twitter_id?: string;
    youtube_id?: string;
    facebook_id?: string;
    instagram_id?: string;
    pinterest_id?: string;
    linkedin_id_alpha?: string;
    linkedin_id_numeric?: number;
    linkedin_sales_navigator?: string;
  };
  monthly_visitors?: string;
  technology_categories?: string[];
};

const params = new URLSearchParams({
  "query": "gucci.com",
});

const response = await fetch(`https://api.piloterr.com/v2/company?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as CompanyDatabase;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/company
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "gucci.com"}
```
</details>

### Output example

Example response from the API reference, abridged — real values depend on the page you scrape.

```json
{
  "name": "Gucci",
  "domain": "gucci.com",
  "founded": 1921,
  "revenue": "over-1b",
  "location": {
    "lat": "43.7567104",
    "lng": "11.1847619",
    "city": "Scandicci",
    "address": null,
    "country": "Italy",
    "postcode": "50018",
    "country_code": "IT"
  },
  "domain_tld": "com",
  "industries": [
    "fashion",
    "jewelry"
  ],
  "updated_at": null,
  "description": "Influential, innovative and progressive, Gucci is reinventing a wholly modern approach to fashion. Under the new vision of creative direc…",
  "domain_name": "gucci",
  "staff_range": "over-10k",
  "phone_number": "example",
  "technologies": [
    "akamai",
    "amazon-cloudfront"
  ],
  "business_type": null,
  "social_networks": {
    "twitter": "http://twitter.com/gucci",
    "youtube": "https://youtube.com/user/gucciofficial",
    "facebook": "http://www.facebook.com/gucci",
    "linkedin": "https://www.linkedin.com/company/6585",
    "instagram": "https://instagram.com/gucci",
    "pinterest": "https://pinterest.com/gucci",
    "twitter_id": "gucci",
    "youtube_id": "gucciofficial",
    "facebook_id": "gucci",
    "instagram_id": "gucci",
    "pinterest_id": "gucci",
    "linkedin_id_alpha": "gucci",
    "linkedin_id_numeric": 6585,
    "linkedin_sales_navigator": "https://www.linkedin.com/sales/company/6585"
  },
  "monthly_visitors": "100m-500m",
  "technology_categories": [
    "accounting-and-finance",
    "application-development"
  ]
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `name` | string |  |
| `domain` | string |  |
| `founded` | integer |  |
| `revenue` | string |  |
| `location` | object |  |
| `location.lat` | string |  |
| `location.lng` | string |  |
| `location.city` | string |  |
| `location.address` | object |  |
| `location.country` | string |  |
| `location.postcode` | string |  |
| `location.country_code` | string |  |
| `domain_tld` | string |  |
| `industries` | string[] |  |
| `updated_at` | object |  |
| `description` | string |  |
| `domain_name` | string |  |
| `staff_range` | string |  |
| `phone_number` | string |  |
| `technologies` | string[] |  |
| `business_type` | object |  |
| `social_networks` | object |  |
| `social_networks.twitter` | string |  |
| `social_networks.youtube` | string |  |
| `social_networks.facebook` | string |  |

## Code examples in other languages

Ready-to-run examples live in the [`examples/`](examples) folder. Each one reads your key from the `PILOTERR_API_KEY` environment variable.

| Language | API |
|---|---|
| cURL (Bash) | [`default`](examples/curl/default.sh) |
| PHP | [`default`](examples/php/default.php) |
| C# | [`default`](examples/csharp/Default.cs) |
| Go | [`default`](examples/go/default.go) |
| Java | [`default`](examples/java/DefaultExample.java) |
| Ruby | [`default`](examples/ruby/default.rb) |
| Node.js | [`default`](examples/nodejs/default.mjs) |

## Practical use cases

- **Lead generation** — Build target account lists from public company data.
- **CRM enrichment** — Keep firmographics, websites and descriptions up to date.
- **Market mapping** — Map competitors and segments across countries and industries.
- **Investment research** — Screen companies, funding and signals for deal flow.
- **Job market analytics** — Track hiring, roles and salaries where available.

## Why Piloterr?

- **No infrastructure** — no proxies, headless browsers or CAPTCHA solving to run yourself.
- **Structured JSON** — stable, documented fields instead of brittle HTML selectors.
- **Pay per request** — transparent credit cost per endpoint, failed requests are retried for you.
- **One API key, hundreds of sources** — Company Database plus many other e-commerce, search and company data endpoints in the [Piloterr library](https://www.piloterr.com/library).
- **Any language** — plain HTTPS + JSON, with examples for Python, TypeScript, cURL, PHP, C#, Go, Java, Ruby and Node.js.

## FAQ

### Is it legal to scrape Company Database?

Collecting publicly available data is generally allowed in many jurisdictions, but rules depend on your country, the data you collect and how you use it. Avoid personal data unless you have a lawful basis, respect the website's terms where they apply, and get legal advice for your specific use case. This is not legal advice.

### Do I need proxies or a headless browser?

No. Piloterr handles rendering, proxy rotation and retries on its side. You only send an HTTPS request with your `x-api-key` header and receive JSON.

### How much does a request cost?

Credits per call: `/v2/company` **1**. See the [Piloterr website](https://www.piloterr.com) for plans.

### What data does the Company Database API return?

Each endpoint returns structured JSON: **Company Database** — `name`, `domain`, `founded`, `revenue`, `location`, `location.lat`.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Related scrapers

- [Crunchbase Scraper API](https://github.com/piloterr/crunchbase-scraper)
- [Europages Scraper API](https://github.com/piloterr/europages-scraper)
- [Fiverr Scraper API](https://github.com/piloterr/fiverr-scraper)
- [G2 Scraper API](https://github.com/piloterr/g2-scraper)
- [GitHub Scraper API](https://github.com/piloterr/github-scraper)
- [Glassdoor Scraper API](https://github.com/piloterr/glassdoor-scraper)
- [All Piloterr scrapers on GitHub](https://github.com/piloterr)

## Support

- 💬 Join the [Piloterr Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Browse the [API reference (OpenAPI)](https://app.piloterr.com/openapi) and the [Piloterr library](https://www.piloterr.com/library).
- 🔑 [Get your API key](https://app.piloterr.com).

---

<p align="center">
  <a href="https://www.piloterr.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="Piloterr" height="32">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.piloterr.com">Piloterr</a> — web scraping APIs for e-commerce, search, real estate and more, one API key.</sub>
</p>

<sub>Company Database is a trademark of its respective owner. This repository is not affiliated with or endorsed by Company Database. Examples are released under the MIT license.</sub>
