# Web Hygiene MCP

[![AllMCPs Verified](https://allmcps.com/api/badge/web-hygiene-mcp?style=shield)](https://allmcps.com/mcp/web-hygiene-mcp) · Official MCP Registry: `io.github.Luca-003/web-hygiene-mcp`

Remote MCP server (Streamable HTTP) that gives AI agents **seven tools answering from the live web** — never from a cache or the model's memory:

| Tool | What it does |
|---|---|
| `site_overview(site)` | robots.txt (sitemaps declared, AI crawlers addressed, blanket disallow), `llms.txt`, sitemaps with URL count sample, feeds |
| `list_site_urls(site_or_sitemap, max_urls, include_regex, exclude_regex)` | URLs a site publishes in its sitemaps, with `lastmod` (≤ 2,000) |
| `check_url(url)` | HTTP status, full redirect chain, final URL, response time, content type |
| `check_links(urls \| site_or_sitemap, max_urls, problems_only)` | Bulk check: 404s, 5xx, timeouts, SSL errors, redirect chains, slow pages (≤ 300) |
| `discover_feeds(site)` | RSS / Atom / JSON feeds of a website |
| `read_feed(feed_or_site, max_items, include_content)` | Normalised feed items: title, link, date in UTC, author, summary, enclosures (≤ 100) |
| `verify_citations(text \| urls \| citations, check_archive, max_citations)` | Per cited URL: `verified` / `mismatch` / `not-found` / `redirected-home` / `paywalled` / `blocked` …, real title/date/author, quote match evidence, Internet Archive copy for dead links (≤ 50) |

## Connect

```
URL:    https://bruco3--web-hygiene-mcp.apify.actor/mcp
Header: Authorization: Bearer <YOUR_APIFY_API_TOKEN>
```

Claude Desktop / Cursor / any Streamable HTTP client:

```json
{
  "mcpServers": {
    "web-hygiene": {
      "url": "https://bruco3--web-hygiene-mcp.apify.actor/mcp",
      "headers": { "Authorization": "Bearer YOUR_APIFY_API_TOKEN" }
    }
  }
}
```

A free Apify account gives you an API token and $5 of monthly credits. Tool calls are billed pay-per-event to your Apify account: a `check_url` costs a fraction of a cent; verifying the 10 sources of an answer about two cents. No subscription, nothing to run.

## Try it — three prompts

1. *"Check the sources in the answer you just gave me: does each link exist, and is the quote really on the page?"* → `verify_citations`
2. *"Before we cite anything from example.com, what does the site publish and allow?"* → `site_overview`
3. *"Check every link in this README and tell me which are broken or redirected."* → `check_links`

**Claude Code**: ready-made plugin with two skills — `/plugin marketplace add Luca-003/web-hygiene-claude-plugin` then `/plugin install web-hygiene@luca-003` ([repo](https://github.com/Luca-003/web-hygiene-claude-plugin)).

## Why

Language models are confident about links and sources they have never fetched. These tools let an agent **look before it claims**: verify a URL exists and where it leads, check robots.txt and `llms.txt` before quoting a site, read what a site really publishes, confirm a cited page carries the quoted passage.

## Details, pricing, issues

Full documentation, pricing table and issue tracker: **https://apify.com/bruco3/web-hygiene-mcp**

Related Actors for whole-site / whole-document jobs: [Sitemap URL Extractor](https://apify.com/bruco3/sitemap-url-extractor) · [Broken Link Checker](https://apify.com/bruco3/broken-link-checker) · [Feed Monitor](https://apify.com/bruco3/feed-monitor) · [Citation & Link Verifier](https://apify.com/bruco3/citation-verifier)

## Legal

The tools request only public files sites publish for automated readers (sitemaps, feeds, robots.txt, llms.txt) and public pages you name, with a clear `User-Agent`. No personal data is collected or stored.

This repository holds the registry metadata (`server.json`) and documentation; the server runs on Apify.
