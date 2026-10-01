# Switchboard Finance MCP server

<img src="icon.png" width="64" align="right" alt="">

**Australian business loans for the self-employed.** A remote MCP server that lets AI assistants check which business finance fits a situation — ATO debt, caveat loans, second mortgages, private lending after a bank decline, commercial property, development, equipment, truck and vehicle finance, invoice finance, overdrafts, bad credit, motels and pubs — and, with the owner's consent, request a callback from a licensed broker.

Run by Switchboard Finance Pty Ltd, Credit Representative 576702 of Australian Credit Licence 517192. General information only: no lender is named, nothing is a credit decision, offer or advice, and consumer loans are out of scope.

- **MCP endpoint:** `https://api.switchboardfinance.com.au/mcp` (Streamable HTTP, no sign-in)
- **Protocols:** 2026-07-28, 2025-11-25, 2025-06-18, 2025-03-26
- **Docs:** https://api.switchboardfinance.com.au/docs
- **Official MCP Registry:** `io.github.Nicklim123/switchboard-finance`
- **Also:** OpenAPI at `/openapi.json`, A2A agent card at `/.well-known/agent-card.json`

## Tools

| Tool | What it does | Writes? |
|---|---|---|
| `check_fit` | Which finance types fit a scenario, with loan size, LVR, timing and trading-history checks, documents usually needed, deal-breakers and the expected callback time. Renders an interactive card (MCP Apps) where supported. | No |
| `list_products` | Every finance type with observed sizes, time to fund, LVR and rate ranges. | No |
| `search` / `fetch` | Search published information and fetch full text with a source URL. | No |
| `request_callback` | Sends one consented enquiry to a licensed broker; returns a reference and expected contact time. Idempotent. | One enquiry |

## Connect

**Claude:** Settings → Connectors → Add custom connector → paste the endpoint.
**ChatGPT:** Settings → Apps → Developer mode → Create app → paste the endpoint.
**Claude Code:** `claude mcp add --transport http switchboard-finance https://api.switchboardfinance.com.au/mcp`
**VS Code:** `code --add-mcp '{"name":"switchboard-finance","type":"http","url":"https://api.switchboardfinance.com.au/mcp"}'`
**Cline:** MCP Servers → Remote Servers → name `switchboard-finance`, URL above (see [llms-install.md](llms-install.md)).
**Cursor:** this repo is a Cursor / Agent Plugin (`.cursor-plugin/plugin.json`, `mcp.json`, a skill). Or add it manually:
```json
{ "mcpServers": { "switchboard-finance": { "type": "http", "url": "https://api.switchboardfinance.com.au/mcp" } } }
```

## Example prompts
- "We owe the ATO $180k and need it cleared this week. We own a warehouse worth $1.2M with $400k owing."
- "I need $120k for an excavator for my civil company."
- "What documents do I need for invoice finance?"

![Fit check card](screenshot.png)

Demo walkthrough (all test cases against the live server): [demo.mp4](demo.mp4)

## Privacy and support
Only details a person agrees to send through `request_callback` are received: https://api.switchboardfinance.com.au/privacy · terms: https://api.switchboardfinance.com.au/terms · hello@switchboardfinance.com.au · 0483 980 567

This repository documents a hosted service; the server itself is not open source.
