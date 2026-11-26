# Strata MCP — Lightweight Apify Actors & MCP Tools for AI Agents

A collection of ultra-lightweight, zero-browser **Model Context Protocol (MCP)** tools hosted on [Apify](https://apify.com/strata-mcp) for AI agents (Claude Desktop, Cursor, Windsurf, custom agents) and automated workflows.

All tools run on **pure HTTP and structured parsing** (no Playwright/Puppeteer overhead, no LLM bloat), returning clean, predictable JSON in seconds at minimal compute cost.

---

## Available MCP Tools

| Tool | Best For | Bulk / Scale | Apify Store |
| :--- | :--- | :--- | :--- |
| **EAA & WCAG 2.2 Accessibility Auditor** | Static HTML screening for European Accessibility Act (EAA), EN 301 549, and WCAG 2.2 (9 core checks) | Single URL, batch, or `sitemap.xml` (up to 500 URLs, `<sitemapindex>` & `.xml.gz`) | [View on Apify](https://apify.com/strata-mcp/eaa-wcag-accessibility-auditor) |
| **AI Readiness & `llms.txt` Bulk Auditor** | GEO / AI search readiness: `/llms.txt`, `/llms-full.txt`, 9 AI crawlers in `robots.txt`, JSON-LD validation, and SPA empty-shell risk | Single URL, batch, or `sitemap.xml` (up to 500 URLs, `<sitemapindex>` & `.xml.gz`) | [View on Apify](https://apify.com/strata-mcp/ai-readiness-llms-txt-auditor) |
| **Japan Law & Statute Lookup (e-Gov API v2)** | Official Japanese statutes & article extraction via Japan Digital Agency's e-Gov Law API v2 with 38+ English legal aliases and PDL 1.0 attribution | Keyword search & exact article lookup (zero API key required) | [View on Apify](https://apify.com/strata-mcp/japan-law-egov-lookup) |

---

## Quick Connect via Apify Hosted MCP Endpoint

Connect all three tools at once using Apify's hosted MCP server:

```text
[https://mcp.apify.com/?actors=strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/ai-readiness-llms-txt-auditor,strata-mcp/japan-law-egov-lookup](https://mcp.apify.com/?actors=strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/ai-readiness-llms-txt-auditor,strata-mcp/japan-law-egov-lookup)
```

### Example MCP Client Configuration (Claude Desktop / Cursor)

```json
{
  "mcpServers": {
    "strata-mcp-apify": {
      "command": "npx",
      "args": [
        "-y",
        "@apify/actors-mcp-server",
        "--actors",
        "strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/ai-readiness-llms-txt-auditor,strata-mcp/japan-law-egov-lookup"
      ],
      "env": {
        "APIFY_TOKEN": "YOUR_APIFY_API_TOKEN"
      }
    }
  }
}
```

---

## Example Agent Prompts

- **Full-site accessibility audit:** `"Run a WCAG 2.2 / EAA audit on up to 50 pages from https://example.com/sitemap.xml and summarize the top critical issues."`
- **AI search & `llms.txt` check:** `"Audit https://docs.apify.com for AI readiness—check llms.txt, AI crawler rules in robots.txt, JSON-LD errors, and SPA rendering risks."`
- **Japanese law lookup:** `"Look up Article 17 of Japan's APPI (Act on the Protection of Personal Information) using the e-Gov Law API tool."`

---

## Pricing & Free Testing

- All Actors use **Apify Pay-Per-Event (PPE)** at **$5.00 per 1,000 successful records** ($0.005/event).
- Failed or errored requests are **never charged**.
- Apify's Free plan includes **$5.00/month in platform credit**, allowing you to test all tools without a credit card.
