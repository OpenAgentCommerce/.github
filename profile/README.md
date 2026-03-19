# OpenAgentCommerce

**The unbiased product index for AI agents.**

OpenAgentCommerce is a paid MCP server and API that lets your personal AI agent search, compare, and buy products across the open web — with no sponsored placements, no merchant fees, and no platform intermediary deciding what you see.

You pay for the index. The index works for you.

---

## How it works

Add our MCP server to your agent. That's it.

```json
{
  "mcpServers": {
    "commerce": {
      "url": "https://mcp.openagentcommerce.dev",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

Your agent gets access to tools like:

- `search_products` — natural language product search across all indexed merchants
- `compare_prices` — find the same or similar product across multiple stores
- `check_availability` — real-time stock and shipping info
- `get_product_details` — specs, reviews, policies, return windows
- `create_cart` — build a cart at a specific merchant
- `get_checkout_url` — get a one-click checkout link to complete the purchase

Works with Claude Code, any MCP-compatible client, or directly via the REST API.

## Why this exists

Every shopping surface today is paid for by sellers.

Google Shopping ranks by ad spend. Amazon ranks by sponsored placement and who uses FBA. ChatGPT's shopping feature routes through merchants who've opted into OpenAI's protocol. Even Shopify's Catalog only includes Shopify merchants, distributed through platforms with their own monetization layers.

None of these are optimized for the buyer. They can't be — their revenue comes from the other side.

OpenAgentCommerce is funded by buyer subscriptions. We don't charge merchants to be listed. We don't run ads. We don't take a cut of transactions. The ranking function optimizes for one thing: best match for your query.

When the buyer pays, the buyer is the customer.

## What's in the index

We aggregate product data from:

- **Shopify stores** — every store's public MCP endpoint (`/api/mcp`), no auth required
- **UCP merchants** — crawling `/.well-known/ucp` manifests across the web
- **ACP merchants** — merchants exposing Agentic Commerce Protocol endpoints
- **Direct integrations** — merchants we onboard individually, connecting to their existing payment processor (Stripe, Square, Adyen, etc.)

The index grows as we onboard more merchants and crawl more of the open commerce web. Coverage is transparent — you can query what's indexed and what isn't.

## Payments

Today, checkout works via URL. Your agent builds the cart, you get a link, you tap and pay on the merchant's own checkout page. This works with every indexed merchant, no special integration required.

As Stripe's SPT (Shared Payment Token) program opens up, we'll support fully headless checkout — your agent finds the product, you approve, payment completes without leaving your terminal.

## Pricing

**Personal** — $10/month
- Unlimited product searches
- Checkout URL generation
- Standard rate limits

**Developer** — $30/month  
- Higher rate limits
- Batch query support
- Webhook notifications for price drops and restocks

**Self-hosted** — Free  
- Run your own index from our open source crawlers
- Bring your own infrastructure
- Community-maintained merchant integrations

## Architecture

```
Your Agent (Claude Code, local LLM, any MCP client)
        │
        ▼
┌─────────────────────────┐
│  OpenAgentCommerce MCP  │  ← You are here
│                         │
│  search_products        │
│  compare_prices         │
│  check_availability     │
│  create_cart            │
│  get_checkout_url       │
└────────────┬────────────┘
             │
     ┌───────┼───────┐
     ▼       ▼       ▼
  Shopify   UCP    Direct
  MCPs    Manifests Integrations
     │       │       │
     └───────┼───────┘
             ▼
         Merchants
```

We're a read layer over the open commerce web. We don't hold inventory, we don't process payments, we don't fulfill orders. Merchants remain the merchant of record. Your relationship is with them, not us.

## For merchants

Listing is free. We want maximum coverage because that's what makes the index valuable.

If you're on Shopify, you're probably already indexed — we crawl public MCP endpoints automatically.

If you're not on Shopify and want to be discoverable by agents, reach out. We'll integrate with your existing payment processor and give you an agent-accessible storefront at no cost. More customers finding your products through their personal agents is a new sales channel with zero CAC.

`merchants@openagentcommerce.dev`

## Principles

**No sponsored results.** Ever. Merchant fees create bias. We don't charge merchants, so we can't be biased.

**Agent-agnostic.** We don't care what model you use. Claude, GPT, Gemini, Llama, a bash script — if it speaks MCP or HTTP, it works.

**Buyer-aligned.** You pay us. You're the customer. The index is optimized for you.

**Transparent coverage.** We publish what's indexed. If we don't have a merchant, we'll tell you. We'd rather be honest about gaps than pretend they don't exist.

**No lock-in.** Standard MCP protocol. Remove us from your config and you're gone. We stay good because you can leave.

## Status

Early development. Join the waitlist at [openagentcommerce.dev](https://openagentcommerce.dev).

We're looking for:

- **Early subscribers** who want to shape what the index covers
- **Merchants** who want to be discoverable by personal agents
- **Contributors** to the open source crawlers and merchant integrations

## Repos

| Repo | Description |
|------|-------------|
| `oac-server` | The MCP server and REST API |
| `oac-crawlers` | Shopify MCP crawler, UCP manifest ingestion, product normalization |
| `oac-index` | Product index and search infrastructure |
| `oac-checkout` | Cart building and checkout URL generation |
| `oac-sdk` | Client libraries for Python and TypeScript |

## License

Server and crawlers are source-available. Client SDKs are MIT.

---

*Your agent should shop for you. Not for whoever paid the most to be seen.*
