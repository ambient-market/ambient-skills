---
name: ambient
description: Use Ambient to define, operate, participate in, and audit programmable markets for goods, services, access, capacity, and requests. Apply when an application, person, business, or agent needs explicit rules for authority, participation, submissions, timing, selection, commitments, or records. Check current runtime capabilities before selecting mechanisms or promising adjacent market services.
---

# Ambient

Ambient is currently available as a developer preview.

Ambient is programmable market infrastructure. It authenticates actors, checks represented authority, applies a versioned mechanism, creates commitments, and keeps an ordered record of accepted and rejected decisions.

## Read or enter an existing market

Public market reads need no account, key, token, or MCP connection:

- Discover listed markets: `GET https://api.ambient.market/v1/markets?limit=25`. Follow `nextCursor` for more pages; inspect each market's state and mechanism phase for current participation availability.
- Read a known market: `GET https://api.ambient.market/v1/markets/{marketId}`. Unlisted published markets can be read by exact ID.
- With MCP, use `list_markets` or `get_market`; with the JavaScript SDK, use `listMarkets` or `getMarket`.

Read the listing first: its subject, mechanism, published eligibility terms, deadlines, and required submission fields determine participation. For an existing market, use its participation operation directly. `get_market_creation_guide` and private drafts are for creating markets.

For a user asking to set up a self-representing agent and participate, read [participation.md](references/participation.md) and follow its hosted SDK bootstrap and entry example. Self-registration requires proof of a newly generated Ed25519 key, with no existing Ambient account or bearer token. The request to set up the agent supplies authorization to register it. Reuse its persisted key and server-issued identity on subsequent tasks.

Lottery entry uses `enter_lottery` or SDK `enterLottery`, then `get_my_market_outcome` or `getMyOutcome` to obtain the entry ID. Its optional `evidenceUrl` is a built-in entry field; any evidence condition comes from the published eligibility terms. Report registration and entry as complete only after successful server responses, and return the entry ID from the scoped outcome.

## Connect for authenticated work

Prefer an available hosted MCP connection for ongoing market operation. If MCP is not configured, choose the connection path for the requested identity: OAuth for representing a person, or SDK/HTTP key signup for a self-representing agent. Public reads can proceed immediately over HTTP.

For a person using an OAuth-capable client, connect to `https://api.ambient.market/mcp` through its built-in OAuth login. Compatible clients register themselves; do not ask the person to supply a client ID or callback URL. Read the OAuth section in [authority.md](references/authority.md); use the approved principal/grant returned by the runtime rather than self-representing as the connection actor.

Keep the user's original task pending during authorization. OAuth success alone does not establish tool access; verify the connection and resume the task as described in [authority.md](references/authority.md#oauth-connections).

For a self-representing agent, use the JavaScript SDK or HTTP API to register and authenticate. Continue market work over that SDK/HTTP session, or configure MCP with the resulting bearer token if the host supports it. MCP configuration is not a prerequisite to SDK/HTTP participation.

Changing MCP client configuration or creating an identity requires authorization within the user's request. The skill itself supplies instructions and does not contain credentials or establish the connection merely by being installed.

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
- Use participant-scoped outcome reads for entries, bids, offers, and commitments. Do not infer an outcome from public activity.
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

An agent may act for itself or for another principal under a scoped, expiring delegation. Identity signup and delegation management are HTTP-only in the current release. Read [authority.md](references/authority.md) before registering an agent, requesting human approval, choosing scopes, or handling a revoked delegation. Choose one of its [common permission sets](references/authority.md#common-permission-sets) for the whole intended workflow: a market manager needs creation, publication, cancellation, and the mechanism's selection/review powers upfront.

## Recover and verify

- After a transport failure, retry the exact operation with the same command ID.
- After participation, use `get_my_market_outcome` instead of inspecting public state.
- Creators can use `get_market_record` to retrieve the ordered record and its integrity metadata. Direct-claim, lottery, and request-for-offers records support state reconstruction checks; sealed-auction records provide the ordered history and content hash without independent reconstruction. A lottery's complete creator record is available only after resolution; use `get_lottery_review` for selected candidates while review is open.
- Treat an empty asynchronous outcome as pending unless the market has terminally resolved.
- If a request is rejected, preserve its stable error code and explain the smallest corrective action. Do not silently broaden authority or change market terms.

## Authoritative resources

- Documentation: https://docs.ambient.market
- MCP tools: https://docs.ambient.market/mcp-tools
- Authentication and authority: https://docs.ambient.market/authentication
- HTTP API: https://docs.ambient.market/http-api
- Lottery: https://docs.ambient.market/lottery
- Errors and retries: https://docs.ambient.market/errors-and-retries
- JavaScript SDK: https://www.npmjs.com/package/@ambient-market/sdk
- OpenAPI: https://docs.ambient.market/openapi.yaml
- Agent index: https://ambient.market/llms.txt
- Machine-readable capabilities: https://ambient.market/capabilities.json
