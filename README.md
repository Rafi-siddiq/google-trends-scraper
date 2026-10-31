<!-- Landing README for a public GitHub repo. The Actor runs on Apify; this repo is for discovery and issues. -->
[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-0d9488?style=for-the-badge)](https://apify.com/rsiddiq95/google-trends-scraper)

# Google Trends Scraper

Get Google Trends data for any list of keywords: **interest over time**, **interest by region** (countries, states, cities or US metro areas), **top and rising related searches**, and today's **Trending Now** searches with traffic estimates and news links.

You pay only for keywords that return data. Failed lookups, and keywords Google has no data for, are free.

## What can this Google Trends Scraper do?

- 📈 **Interest over time.** The 0–100 search interest timeline for any period, from the past hour to 2004 onward, or exact dates you choose.
- 🗺️ **Interest by region.** See where a keyword is most popular, by country, state/region, city, or US metro area (DMA).
- 🔎 **Related searches.** Top and rising queries, with "Breakout" flags for searches that grew more than 5,000%.
- ⚖️ **Comparisons.** Compare up to 5 keywords on the same scale, just like typing them together on Google Trends.
- 🔥 **Trending Now.** The searches trending right now in any country, with approximate traffic and the news stories behind them.
- 🎯 **Filters.** Location, category, and search type (web, images, news, Google Shopping, YouTube).
- 💸 **Fair billing.** Errors and empty results are never charged.

## What data can I get from Google Trends?

| Field | Example |
|---|---|
| Search term | `air fryer` |
| Average interest | `65` |
| Interest over time | weekly or daily points with date, label and 0–100 value |
| Interest by region | `Wyoming: 100`, `Nebraska: 36`, … |
| Related searches (top) | `air fryer chicken: 100`, `air fryer oven: 70` |
| Related searches (rising) | `best air fryer 2026: Breakout` |
| Trending search | `sndk stock`, `2000+` searches, 3 news links |
| Google Trends URL | link to the same query on trends.google.com |

## How to scrape Google Trends

1. Click **Try for free**.
2. Enter your **search terms**, one per line.
3. Optionally pick a **location** (for example `US` or `US-CA`), a **time range**, and a **category**.
4. Turn on **Compare terms against each other** if you want keywords on the same scale.
5. Click **Start**, then download your data as JSON, CSV, Excel, or HTML, or pull it through the API.

## Input example

```json
{
    "searchTerms": ["air fryer", "standing desk"],
    "geo": "US",
    "timeRange": "today 12-m",
    "regionResolution": "REGION",
    "trendingNowGeos": ["US", "GB"]
}
```

## Output example

```json
{
    "resultType": "keyword",
    "hasData": true,
    "searchTerm": "air fryer",
    "comparedWith": [],
    "geo": "US",
    "timeRange": "today 12-m",
    "category": 0,
    "searchProperty": "web",
    "averageInterest": 65,
    "interestOverTime": [
        { "date": "2025-10-26T00:00:00.000Z", "label": "Oct 26 – Nov 1, 2025", "value": 52, "hasData": true, "isPartial": false }
    ],
    "interestByRegion": [{ "geoCode": "US-WY", "geoName": "Wyoming", "value": 100, "hasData": true }],
    "relatedQueries": {
        "top": [{ "query": "air fryer chicken", "value": 100, "formattedValue": "100", "isBreakout": false }],
        "rising": [{ "query": "best air fryer 2026", "value": 6050, "formattedValue": "Breakout", "isBreakout": true }]
    },
    "trendsUrl": "https://trends.google.com/trends/explore?q=air+fryer&date=today+12-m&hl=en-US&geo=US",
    "scrapedAt": "2026-10-29T20:29:12.206Z"
}
```

Trending Now rows have `resultType: "trending"` with `rank`, `title`, `approxTraffic`, `startedAt`, `pictureUrl` and `newsItems`.

## How much does it cost to scrape Google Trends?

This Actor uses pay-per-result pricing, so you only pay for keywords and trending searches that return data. See the **Pricing** tab for current prices. Apify's free plan includes monthly credit, enough to try the Actor on hundreds of keywords.

## Tips

- **Values are relative.** Google scales every result from 0 to 100 within the query, where 100 is the peak. Compare keywords on the same scale by turning on **Compare terms against each other**.
- **Use exact dates for repeatable reports.** A custom range such as `2025-01-01 2025-12-31` returns the same window every time.
- **Large lists.** The Actor paces itself and retries automatically when Google rate-limits it. For thousands of keywords, schedule several smaller runs.

## Limitations

- Google Trends has no official public API yet, so this Actor reads the public Google Trends website. Google can change it at any time; we monitor the Actor and update it when that happens.
- Related topics are not included, because Google does not provide them to automated tools.
- The Trending Now feed lists the top trending searches Google publishes for each country, usually about 10–20.

## Works well with

- **[Google Sheets Sync](https://apify.com/rsiddiq95/google-sheets-sync):** send each run's keywords to a Google Sheet automatically and keep a growing trends log without duplicates.
- **[Google Ads Transparency Scraper](https://apify.com/rsiddiq95/google-ads-transparency-scraper):** see which competitors are advertising on the keywords that are trending.

## FAQ

**Is it legal to scrape Google Trends?**
This Actor collects aggregated, anonymous search statistics that Google publishes openly, with no personal data. Make sure your use complies with Google's terms and the laws that apply to you.

**Can I use it through the API or with other tools?**
Yes. Run it through the Apify API, on a schedule, or connect it to Make, Zapier, n8n, Google Sheets, and more through Apify integrations.

**Something isn't working.**
Open an issue on the **Issues** tab with your input, and we'll respond quickly.

## Links

- Apify Store page: https://apify.com/rsiddiq95/google-trends-scraper
- Questions and bug reports: open an issue here or on the Actor's Issues tab.
