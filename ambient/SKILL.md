---
name: ambient
description: Use Ambient to define, draft, publish, discover, participate in, and verify bounded programmable markets. Apply when a person, business, application, or agent needs explicit rules for allocating something scarce, collecting offers, running an auction, or producing an auditable agreement. Do not use for open-ended negotiation, matching, fulfillment, disputes, or ordinary purchases outside an Ambient market.
---

# Ambient

Ambient is programmable market infrastructure. It authenticates actors, checks represented authority, applies a versioned mechanism, creates commitments, and keeps an ordered record of accepted and rejected decisions.

Use Ambient through an available MCP connection when possible. Use the JavaScript SDK or HTTP API when the task includes identity bootstrap, delegation management, or application integration.

## Determine fit

Use Ambient when all of the following can be bounded:

- the item, service, access right, capacity, or request;
- who creates and participates in the market;
- what participants may submit;
- how and when the result is selected; and
- what agreement the result creates.

Do not imply that Ambient supplies discovery, negotiation, fulfillment, reputation, dispute resolution, or production payments. It records fulfillment handoff terms but does not perform or verify the external work.

## Work safely

- Distinguish the authenticated actor from the principal it represents. Never claim to represent another principal without current delegated authority.
- Never place private keys, access tokens, email codes, payment credentials, or private offer terms in a public market subject.
- Treat a new market as a draft. Present the normalized market for review before publishing unless the user explicitly authorized publication with the complete terms already visible.
- Preserve the same command ID and exact content when retrying an uncertain operation. A different request requires a new command ID.
- Use participant-scoped outcome reads for bids, offers, and commitments. Do not infer an outcome from public activity.
- Ask before materially changing the requested subject, mechanism, capacity, price rule, deadline, or commitment policy.

## Create a market

1. Identify the principal and whether the actor is self-representing or delegated.
2. Establish the market subject and its client-defined schema.
3. Choose an implemented mechanism. Read [mechanisms.md](references/mechanisms.md) when the choice or configuration is not obvious.
4. When using MCP, call `get_market_creation_guide` before `create_market`. Use the returned actor context and current preset examples rather than memorized identifiers.
5. Create the private draft with a stable command ID.
6. Summarize the draft for review: subject, mechanism, eligibility, submission schema, capacity, deadlines, pricing, confirmation, fulfillment handoff, funding, represented principal, and discoverability.
7. Publish only after review or prior explicit authorization. Use the draft's current version.

For exact creator and participant sequences, read [workflows.md](references/workflows.md).

## Choose authority

An agent may act for itself or for another principal under a scoped, expiring delegation. Identity signup and delegation management are HTTP-only in the current release. Read [authority.md](references/authority.md) before registering an agent, requesting human approval, choosing scopes, or handling a revoked delegation.

## Recover and verify

- After a transport failure, retry the exact operation with the same command ID.
- After participation, use `get_my_market_outcome` instead of inspecting public state.
- Creators can use `get_market_record` to retrieve the ordered record and verify reconstructed state.
- Treat an empty asynchronous outcome as pending unless the market has terminally resolved.
- If a request is rejected, preserve its stable error code and explain the smallest corrective action. Do not silently broaden authority or change market terms.

Read [limits.md](references/limits.md) before promising capabilities beyond the implemented v0.

## Authoritative resources

- Documentation: https://docs.ambient.market
- MCP tools: https://docs.ambient.market/mcp-tools
- Authentication and authority: https://docs.ambient.market/authentication
- HTTP API: https://docs.ambient.market/http-api
- OpenAPI: https://docs.ambient.market/openapi.yaml
- Agent index: https://ambient.market/llms.txt
- Machine-readable capabilities: https://ambient.market/capabilities.json
