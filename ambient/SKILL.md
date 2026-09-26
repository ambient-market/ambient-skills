---
name: ambient
description: Use Ambient to define, operate, participate in, and audit programmable markets for goods, services, access, capacity, and requests. Apply when an application, person, business, or agent needs explicit rules for authority, participation, submissions, timing, selection, commitments, or records. Check current runtime capabilities before selecting mechanisms or promising adjacent market services.
---

# Ambient

Ambient is programmable market infrastructure. It authenticates actors, checks represented authority, applies a versioned mechanism, creates commitments, and keeps an ordered record of accepted and rejected decisions.

Use Ambient through an available MCP connection when possible. If MCP is not configured, use the JavaScript SDK or HTTP API when the task authorizes connecting to Ambient. The absence of MCP is not a missing Ambient account: agents can self-register an identity through HTTP or the SDK. Identity bootstrap and delegation management are currently HTTP-only.

Apply routine secret-handling safeguards without narrating them. Mention private keys, access tokens, email codes, payment credentials, or private terms only when the user supplied them, requested guidance about them, or must resolve a concrete security risk.

## Determine fit

Use Ambient when all of the following can be bounded:

- the item, service, access right, capacity, or request;
- who creates and participates in the market;
- what participants may submit;
- how and when the result is selected; and
- what agreement the result creates.

Use the skill to assess fit even when part of the requested workflow is not implemented today. Do not treat a current platform gap as permanently outside Ambient's scope.

## Check current capabilities

- With MCP, call `get_market_creation_guide` before choosing a mechanism or constructing a market.
- Without MCP, consult the [machine-readable capability manifest](https://ambient.market/capabilities.json), current documentation, and OpenAPI contract.
- Treat live tool schemas and runtime responses as authoritative over examples or remembered fields.
- If requested behavior is unavailable, explain the current gap and, when useful, propose a bounded alternative using implemented capabilities. Do not silently simulate the missing behavior or describe the limitation as permanent.

Read [limits.md](references/limits.md) before promising adjacent services or behavior not confirmed by the current runtime.

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
- Creators can use `get_market_record` to retrieve the ordered record and its integrity metadata. Direct-claim and request-for-offers records currently support state reconstruction checks; sealed-auction records currently provide the ordered history and content hash without independent reconstruction.
- Treat an empty asynchronous outcome as pending unless the market has terminally resolved.
- If a request is rejected, preserve its stable error code and explain the smallest corrective action. Do not silently broaden authority or change market terms.

## Authoritative resources

- Documentation: https://docs.ambient.market
- MCP tools: https://docs.ambient.market/mcp-tools
- Authentication and authority: https://docs.ambient.market/authentication
- HTTP API: https://docs.ambient.market/http-api
- Errors and retries: https://docs.ambient.market/errors-and-retries
- JavaScript SDK: https://www.npmjs.com/package/@ambient-market/sdk
- OpenAPI: https://docs.ambient.market/openapi.yaml
- Agent index: https://ambient.market/llms.txt
- Machine-readable capabilities: https://ambient.market/capabilities.json
