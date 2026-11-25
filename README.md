# Strata MCP — Lightweight Apify Actors & MCP Tools for AI Agents

Fast, zero-bloat **Model Context Protocol (MCP)** tools hosted on [Apify](https://apify.com/strata-mcp). Built with pure HTTP and structured parsing (no headless browsers or LLM overhead) for low latency, predictable JSON outputs, and automated agentic workflows.

## Available Tools

| Tool | Apify Actor ID | Key Capabilities | Pricing (PPE) |
| :--- | :--- | :--- | :--- |
| **[EAA & WCAG 2.2 Static HTML Accessibility Auditor](https://apify.com/strata-mcp/eaa-wcag-accessibility-auditor)** | `strata-mcp/eaa-wcag-accessibility-auditor` | Single-URL, batch, and full-site `sitemap.xml` bulk audits (up to 500 URLs, `<sitemapindex>`, `.xml.gz`) across 9 EAA / EN 301 549 / WCAG 2.2 static rule categories | $5.00 / 1,000 audited URLs |
| **[Japan Law & Statute Lookup (e-Gov API v2)](https://apify.com/strata-mcp/japan-law-egov-lookup)** | `strata-mcp/japan-law-egov-lookup` | Official Japan Digital Agency e-Gov Law API v2 search & article extraction with 38+ built-in English legal aliases and PDL 1.0 attribution | $5.00 / 1,000 law records |

> **Free Testing:** Every Apify Free account includes **$5.00/month in free usage credit**, so you can test both tools immediately without a credit card. Failed or errored requests are never charged.

---

## Quick Start: Connect via Apify MCP Server

Both tools run directly inside **Claude Desktop**, **Cursor**, **Windsurf**, or any MCP-compatible client using Apify's official MCP server.

### Option A: Remote Hosted MCP Server (Recommended)

Point your MCP client to Apify's hosted MCP endpoint with both Actors preloaded:

```text
[https://mcp.apify.com/?actors=strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/japan-law-egov-lookup](https://mcp.apify.com/?actors=strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/japan-law-egov-lookup)
```

### Option B: Local MCP Config (`claude_desktop_config.json` / `.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "strata-mcp-apify": {
      "command": "npx",
      "args": [
        "-y",
        "@apify/actors-mcp-server",
        "--actors",
        "strata-mcp/eaa-wcag-accessibility-auditor,strata-mcp/japan-law-egov-lookup"
      ],
      "env": {
        "APIFY_TOKEN": "YOUR_APIFY_API_TOKEN"
      }
    }
  }
}
```

---

## Tool Details

### 1. EAA & WCAG 2.2 Static HTML Accessibility Auditor

- **Apify Store:** https://apify.com/strata-mcp/eaa-wcag-accessibility-auditor
- **Best for:** Web agencies, compliance engineers, SEO/dev pipelines, and coding agents screening sites for European Accessibility Act (EAA), EN 301 549, and WCAG 2.2 static HTML issues.
- **What it checks:** `<html lang>`, `<title>`, `<img>` alt attributes, heading hierarchy (`h1`–`h6`), form control labels, empty links/buttons, landmarks & skip links, viewport zoom restrictions, inline low-contrast styles, and positive `tabindex`.
- **Full-site bulk audit:** Pass any `sitemap.xml` URL (supports nested `<sitemapindex>` and compressed `.xml.gz` files) with `maxUrls` (up to 500), `includeUrlPatterns`, and `excludeUrlPatterns`.

**Sample Input (Sitemap Bulk Audit):**

```json
{
  "sitemapUrl": "[https://example.com/sitemap.xml](https://example.com/sitemap.xml)",
  "maxUrls": 100,
  "excludeUrlPatterns": ["/tag/", "/feed/"]
}
```

**Example Agent Prompt:**
> "Run an accessibility audit on up to 50 pages from `https://example.com/sitemap.xml`, excluding `/blog/`, and summarize all Critical and Serious WCAG 2.2 issues."

---

### 2. Japan Law & Statute Lookup (e-Gov API v2)

- **Apify Store:** https://apify.com/strata-mcp/japan-law-egov-lookup
- **Best for:** Legal AI agents, cross-border compliance teams, and researchers querying official Japanese legislation without managing API keys or raw XML parsing.
- **Key features:**
  - Direct connection to Japan Digital Agency's official **e-Gov Law API v2**.
  - Built-in English alias mapping for 38+ major Japanese laws (e.g., `APPI`, `Companies Act`, `Labor Standards Act`, `Civil Code`, `Constitution of Japan`).
  - Supports keyword/statute search and clean single-article extraction with English metadata labels, enforcement dates, repeal status, and official PDL 1.0 (CC BY 4.0 compatible) attribution.

**Sample Input:**

```json
{
  "mode": "search",
  "keyword": "APPI",
  "limit": 5
}
```

**Example Agent Prompt:**
> "Look up Japan's Personal Information Protection Act (APPI) using the Japan Law Lookup tool and return its official statute number, enforcement status, and key metadata."

---

## Maintainer

Built and maintained by **[Strata MCP](https://apify.com/strata-mcp)**.
For issues, feature requests, or custom Actor inquiries, please open a GitHub Issue in this repository.
