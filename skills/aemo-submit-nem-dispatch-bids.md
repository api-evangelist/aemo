---
name: Submit and verify NEM dispatch bids and offers
description: Submit Energy, FCAS or MNSP bids and offers into AEMO's National Electricity Market dispatch process, then read them back to confirm what AEMO holds.
api: openapi/aemo-bidding-v1-openapi.yml
operations: [submitBids, getBid, getBids, getSubmission, getSubmissions]
---

# Submit and verify NEM dispatch bids and offers

Use the AEMO `NEMDispatchBidding` API (`openapi/aemo-bidding-v1-openapi.yml`) to lodge bids and
offers and to confirm what AEMO holds after lodgement. This is a **market submission** flow — it
changes a participant's dispatch position. Never submit without an explicit, current instruction
from the participant.

## Before you start

- You must be an authorised AEMO market participant, formally onboarded to this API.
- Every call carries three things: an APIM subscription key (`x-apikey` header or `subscription-key`
  query parameter), an AEMO-signed TLS client certificate on the connection, and an `Authorization`
  header — base64 URM username:password, or an OAuth 2.0 bearer token from
  `https://api.aemo.com.au/oauth/v1/token?grant_type=client_credentials`.
- Every call also carries `X-initiatingParticipantID` (e.g. `P01`) and `X-market` (e.g. `NEM`).
- See `authentication/aemo-authentication.yml` for the full model.

## Steps

1. **Read the current position first.** Call `getBids` with `fromTradingDate`, `toTradingDate` and
   either `duid` or `interconnectorId`, plus `service` and `includeSuperseded`. Confirm what is
   already lodged before changing anything.
2. **Read a specific bid** when you need interval detail: `getBid` requires `offerTimeStamp`,
   `tradingDate`, `duid` and `service`. Valid `service` values are `ENERGY`, `MNSP`, `RAISE1SEC`,
   `RAISE6SEC`, `RAISE60SEC`, `RAISE5MIN`, `RAISEREG`, `LOWER1SEC`, `LOWER6SEC`, `LOWER60SEC`,
   `LOWER5MIN`, `LOWERREG`. For an MNSP the response returns Link IDs in the DUID objects, not
   interconnector IDs.
3. **Submit.** Call `submitBids` with the bid/offer payload. A rebid must carry a rebid explanation
   (`reason`, `eventTime`, `awareTime`, `decisionTime`, `category`) — the market rules require it,
   and the payload models it.
4. **Confirm the submission landed.** Call `getSubmissions` (or `getSubmission` for one) and check
   `status`, `transactionId` and `referenceId` against what you sent.
5. **Verify the effective bid.** Re-run `getBid` for the trading date and DUID and diff it against
   the submitted payload.

## Rules

- **There is no idempotency key.** AEMO publishes no `Idempotency-Key` contract anywhere
  (`conventions/aemo-conventions.yml`). Do **not** blind-retry `submitBids` on a timeout — re-read
  with `getSubmissions` first and only resubmit if the submission is genuinely absent.
- Correlate instead of retrying: keep the `offerTimeStamp` you sent and the `transactionId` /
  `referenceId` returned, and use them to reconcile.
- **422** means a business validation failure *or* that the URM user lacks the required permission —
  a participant administrator fixes permissions in MSATS.
- **429** means AEMO's gateway throttled you. No quota is published and no `Retry-After` header is
  documented; back off exponentially (`rate-limits/aemo-rate-limits.yml`).
- **500 / 503** on the e-Hub usually means "e-Hub is operational but downstream systems are not
  available" — retry a *read*, never a blind re-submit.
- Full status-code catalogue: `errors/aemo-error-codes.yml`.
