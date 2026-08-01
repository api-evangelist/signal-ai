---
name: Signal AI events and risk events
description: Identify coverage-driving events and score entities against risk-event definitions.
api: openapi/signal-ai-openapi-original.json
operations: [search-events, get-event-by-hash, risk-events-definitions, risk-events-search, risk-events-scores]
---

# Events & risk intelligence with Signal AI

Use this skill to find significant coverage clusters and monitor enterprise risk.

## Authenticate
OAuth2 client-credentials bearer token. The `events` scope is required for events; the `risk-events` scope for the risk operations.

## Events
1. **`search-events`** (`POST /events`) — submit an `EventSearchQuery` to find clusters of coverage (`Event`s) about entities/topics; results carry `story-ids`, `entities`, `topics`, and coverage counts. Page with `from-cursor`/`size`.
2. **`get-event-by-hash`** (`GET /events/{hash}`) — retrieve a single event by its `hash`.

## Risk events
3. **`risk-events-definitions`** (`GET /risk-events-definitions`) — list the available risk-event definitions to match against.
4. **`risk-events-search`** (`POST /risk-events-search`) — search risk-classified events.
5. **`risk-events-scores`** (`POST /risk-events-scores`) — retrieve `RiskScore`/`RiskEntityScore` values for entities of interest to power continuous risk monitoring.

## Notes
- All list responses are cursor-paginated (see `conventions/signal-ai-conventions.yml`).
