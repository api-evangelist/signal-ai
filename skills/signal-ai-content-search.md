---
name: Signal AI content search and metrics
description: Search Signal AI's global content corpus and pull coverage & sentiment metrics for a query.
api: openapi/signal-ai-openapi-original.json
operations: [search-documents, get-document, get-metrics]
---

# Content search & metrics with Signal AI

Use this skill to build a hyper-relevant content feed and summarize coverage.

## Authenticate first
Signal AI uses OAuth2 **client credentials**. Exchange your client id/secret for a bearer token, then send it on every call.

```bash
curl -X POST -d 'grant_type=client_credentials' \
  -d 'client_id=YOUR_CLIENT_ID' -d 'client_secret=YOUR_CLIENT_SECRET' \
  https://api.signal-ai.com/auth/token
```
Send `Authorization: Bearer <access_token>` on all requests. Tokens live 24h. The `search` and `metrics` scopes are required for the operations below.

## Steps
1. **`search-documents`** (`POST /search`) — submit a `DocumentSearchQuery` to retrieve matching `Document`s. Responses include `next-cursor`; page forward by sending it back as the `from-cursor` query param, and set `size` for page size.
2. **`get-document`** (`GET /documents/{id}`) — fetch the full record for any document id returned above.
3. **`get-metrics`** (`POST /metrics`) — submit a `MetricsQuery` to get coverage & sentiment aggregations for the same query, for BI/dashboards.

## Conventions
- Pagination is cursor-based (`from-cursor` / `size` -> `next-cursor`). See `conventions/signal-ai-conventions.yml`.
- Errors are JSON (not RFC 9457). No idempotency key contract.
