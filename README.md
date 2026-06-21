# Funding & Press Signal Scanner MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-funding-press-signal-scanner)](https://smithery.ai/servers/mambabuilt/mcp-funding-press-signal-scanner) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-funding-press-signal-scanner/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-funding-press-signal-scanner) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-funding-press-signal-scanner%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-funding-press-signal-scanner&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-funding-press-signal-scanner)](https://www.npmjs.com/package/@mambalabsdev/mcp-funding-press-signal-scanner) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-funding-press-signal-scanner)](https://www.npmjs.com/package/@mambalabsdev/mcp-funding-press-signal-scanner) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-funding-press-signal-scanner)](https://github.com/mambalabsdev/mcp-funding-press-signal-scanner/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-funding-press-signal-scanner)

Give it a company domain, get back a clean list of that company's recent business events: funding rounds, executive moves, product launches, acquisitions, partnerships, and IPOs. The actor searches public news and press sources, classifies each story into a typed event, deduplicates the same event reported across multiple outlets, and returns one flat row per company. Built for Clay users, RevOps teams, and outbound agencies who want account signals without paying for a Crunchbase seat.

## What it does

This server gives an AI client one tool:

- `get_funding_press_signals`: scan Google News and PR wires for a company's funding rounds, executive moves, product launches, acquisitions, partnerships, and IPOs. Returns deduplicated, dated events in flat, Clay-ready JSON, one row per company, with a per company summary (`has_recent_funding`, `funding_total_estimated`, `latest_event_date`, `most_recent_event_type`) and an `events` array where each event carries its type, date, amount, funding stage, source URL, and a corroborating source count.

All of the work runs on Apify. This package is a thin client that routes the tool call to the actor and hands back the result.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config:

```json
{
  "mcpServers": {
    "funding-press-signal-scanner": {
      "command": "npx",
      "args": ["-y", "@mambalabsdev/mcp-funding-press-signal-scanner"],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Get your token at https://console.apify.com/account/integrations, paste it in, and restart Claude Desktop. The tool will be available.

## Prerequisites

- Node.js 18 or newer
- An Apify account with an API token

## Example prompts

- "What funding, exec moves, and product launches has stripe.com had recently?"
- "Has ramp.com raised any funding in the last year, and how much?"
- "Scan deel.com (company name Deel) for acquisitions and partnerships."
- "Show me the most recent press events for notion.so as flat JSON."

## Tool and inputs

`get_funding_press_signals`:

- `domain` (string, required): company domain to scan, without https or www, e.g. stripe.com.
- `company_name` (string, optional): company name hint, used when the domain does not match the brand name, e.g. Deel for deel.com.

The output is one row per company: `company_domain`, `company_name`, `total_events`, `latest_event_date`, `has_recent_funding`, `funding_total_estimated`, `funding_total_currency`, `most_recent_event_type`, `most_recent_headline`, an `events` array of typed events, a `sources_queried` array, and `run_date`. Each event in the array has `event_type` (funding_round, exec_move, product_launch, acquisition, partnership, ipo), `date`, `headline`, `source_url`, `source_name`, `amount`, `currency`, `funding_stage`, `names`, `description`, and `corroborating_source_count`.

## Full actor documentation

For the complete input and output reference, pricing, and run history, see the Funding & Press Signal Scanner actor on the Apify Store (canonical immutable Actor ID URL):

https://apify.com/mambalabs/FS13X6dhQVgX3XOM6

---

## Mamba Labs GTM Suite

This server is part of the **Mamba Labs GTM Suite**, a fleet of twelve specialized MCP servers for go-to-market signal intelligence, each backed by a dedicated Apify actor.

| Actor | Immutable Actor ID |
|---|---|
| [GTM Hiring Signal Scraper](https://console.apify.com/actors/D7O1SA2EqwHGsGr1P) | `D7O1SA2EqwHGsGr1P` |
| [GTM Tech Stack Signal Enrichment](https://console.apify.com/actors/qyd7nNyqFPelQViBx) | `qyd7nNyqFPelQViBx` |
| [GTM Signals Aggregator](https://console.apify.com/actors/xKdRfnfFNkdMpFuNs) | `xKdRfnfFNkdMpFuNs` |
| [Job Board Keyword Signal Scanner](https://console.apify.com/actors/4DvqpvhMR74NLcDDY) | `4DvqpvhMR74NLcDDY` |
| [Domain to LinkedIn URL Resolver](https://console.apify.com/actors/3HtnSaqPHOg1Qg5gx) | `3HtnSaqPHOg1Qg5gx` |
| [ICP Fit Scorer](https://console.apify.com/actors/W161DT8W4kW55dMFh) | `W161DT8W4kW55dMFh` |
| [Domain Deliverability Checker](https://console.apify.com/actors/0tVgxI7A6o9jMlxmc) | `0tVgxI7A6o9jMlxmc` |
| [Company Firmographic Enricher](https://console.apify.com/actors/YlUtLWjfPpqykmB8g) | `YlUtLWjfPpqykmB8g` |
| [Company Social Presence Mapper](https://console.apify.com/actors/4k6CCemkgBDz18m2h) | `4k6CCemkgBDz18m2h` |
| [Company Identity Resolver](https://console.apify.com/actors/lr8fTRAmZCBZmuwwh) | `lr8fTRAmZCBZmuwwh` |
| [Company Change-Event Feed](https://console.apify.com/actors/oX44rS0fkEJ3rXLWe) | `oX44rS0fkEJ3rXLWe` |
| [Funding & Press Signal Scanner](https://console.apify.com/actors/FS13X6dhQVgX3XOM6) | `FS13X6dhQVgX3XOM6` |

> Built by [Mamba Labs](https://github.com/mambalabsdev) | [npm](https://www.npmjs.com/org/mambalabsdev) | [Apify Store](https://apify.com/mambalabs)

## License

MIT

Built by Mamba Labs. https://apify.com/mambalabs
