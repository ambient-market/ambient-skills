# Task workflows

## Offer or allocate something

1. Determine the subject, capacity, participant rules, timing, pricing, and confirmation policy.
2. Choose direct claim, sealed auction, or lottery from the intended clearing rule.
3. Create a private draft.
4. Present the normalized rules for review.
5. Publish with the draft's current version after approval.
6. Read the resulting commitments or creator record as needed.

## Request proposals

1. Define what is requested in the public subject schema.
2. Define what every private proposal must contain in the offer schema.
3. Set selection capacity, offer deadline, later selection deadline, and pricing rule.
4. Create and review the private RFO draft.
5. Publish after approval.
6. After offers close, use the requester-scoped offer read and select up to capacity before the selection deadline.
7. Read the commitment and ordered market record.

## Participate

1. Discover or retrieve the exact published market with public HTTP reads, SDK `listMarkets`/`getMarket`, or MCP `list_markets`/`get_market`. Read [participation.md](participation.md) for public URLs and a self-representing agent example.
2. Verify the subject, mechanism, capacity, deadlines, funding, confirmation, and required submission shape.
3. Verify the represented principal and current authority.
4. Submit the claim, bid, offer, or lottery entry with a stable command ID and the submission fields required by that listing.
5. Retain the receipt returned by Ambient.
6. Use the participant-scoped outcome read to recover the authoritative result.
7. Confirm or decline a pending commitment before its deadline when required.

## Review lottery candidates

1. After entry close and the worker's draw, read `get_lottery_review` with creator confirmation authority.
2. Check selected candidates against the published eligibility terms.
3. Confirm eligible candidates, or decline with a specific reason to promote the next original alternate. Re-read review after a decline.
4. Finish before candidate expiry and the hard resolution deadline. Expiry does not promote.
5. After resolution, retrieve the complete creator record for seed, order, decisions, and reconstruction verification.

## Review a draft

Present a concise summary containing:

- what the market is for;
- mechanism and clearing rule;
- capacity;
- who may participate;
- public subject and private submission schemas;
- pricing or bidding rules;
- relevant deadlines;
- confirmation and expiration behavior;
- discoverability;
- represented principal and authority; and
- funding and fulfillment handoff.

Call out missing, surprising, or irreversible terms. Do not bury them in raw JSON.

## Verify a result

Participants use their scoped outcome view. Creators retrieve the ordered record, verify its content hash, and compare the final commitment with the mechanism result. Direct-claim, lottery, and request-for-offers records also support state reconstruction checks. Sealed-auction records do not yet support independent reconstruction. Lottery creator records are unavailable until resolution; selected-candidate review is available during review. Public activity is not an authoritative substitute for either private view.
