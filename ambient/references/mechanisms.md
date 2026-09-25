# Mechanism selection

Choose the mechanism from how the result should be reached, not from the business category.

## Direct claim

Use `direct-claim.v1` when valid participation should consume available capacity in server order.

Required decisions:

- positive capacity;
- free or posted pricing;
- confirmation by nobody, the creator, the participant, or both; and
- a positive hold duration when confirmation is required.

Good fits include reservations, limited releases, workshop seats, equipment borrowing, and appointment requests.

## Sealed forward auction

Use `sealed-forward-auction.v1` when eligible participants submit private bids before a fixed close and the scarce item should clear by the implemented second-price rule.

Required decisions:

- currency;
- fixed future close;
- positive winner-confirmation period; and
- optional reserve amount.

Do not expose bid amounts through public activity. Participants recover their own receipts and outcomes through scoped reads.

## Request for offers

Use `request-for-offers.v1` when a requester wants private proposals and will choose up to a defined capacity after submissions close.

Required decisions:

- positive selection capacity;
- creator-defined offer schema;
- offer deadline;
- later selection deadline; and
- pricing forbidden, optional, or required.

Selected offer terms and the requester's selection form the commitment. Providers may replace or withdraw an active offer before the offer deadline.

## Not implemented

Lottery, ranked choice, open-ended negotiation, automatic ranking, and rolling RFO selection are not implemented mechanisms. Do not translate these into a supported mechanism without the user's informed approval.
