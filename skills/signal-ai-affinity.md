---
name: Signal AI knowledge-graph affinity
description: Resolve entities/topics and query the Signal AI Knowledge Graph for concept affinity.
api: openapi/signal-ai-openapi-original.json
operations: [find-entities, find-topics, post-affinity]
---

# Knowledge-graph affinity with Signal AI

Use this skill to measure proximity between concepts (topic ownership, differentiation).

## Authenticate
OAuth2 client-credentials bearer token (see `authentication/signal-ai-authentication.yml`); the `affinity` scope is required for `post-affinity`.

## Steps
1. **`find-entities`** (`GET /entities`) — resolve a name to entity concept ids (filter by `name`, `type`).
2. **`find-topics`** (`GET /topics`) — resolve topic concept ids the same way.
3. **`post-affinity`** (`POST /affinity`) — submit a source concept id and receive a `PostAffinityResponse`: a `source-concept` plus ranked related `Concept` edges from the Signal AI Knowledge Graph (nodes = entities/topics, edges = relationships).

## Notes
- A `Concept` is typed by `ConceptTypeEnum` (entity or topic). Ground ids from step 1/2 before calling affinity.
- See the entity graph in `data-model/signal-ai-data-model.yml`.
