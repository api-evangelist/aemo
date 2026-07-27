---
name: Lodge and manage network and generator outages
description: Create, inspect, update and withdraw outages in AEMO's Outage Management System from a network operator or generator perspective.
api: openapi/aemo-outage-management-external-v1-openapi.yml
operations: [retrieveOutageFromOutageManagement, getParticularOutage, retrieveLatestOutageStatusForNetworkOperator, createANewNetworkOutageInOutageManagementSystem, createANewGeneratorOutageInOutageManagementSystem, updateExistingNetworkOutageInOutageManagementSystem, withdrawExistingNetworkOutageInOutageManagementSystem, withdrawExistingNetworkOutagesInOutageManagementSystem]
---

# Lodge and manage network and generator outages

Use the AEMO Outage Management API (`openapi/aemo-outage-management-external-v1-openapi.yml`) to
lodge and maintain planned outages. These are **safety-critical power-system operations** — an
outage submission or withdrawal affects power-system security. Treat every write as
human-in-the-loop: propose, show the exact payload, and only submit on explicit approval. See
`agentic-access/aemo-agentic-access.yml`.

## Auth

APIM subscription key + AEMO-signed TLS client certificate + `Authorization` (URM Basic or OAuth 2.0
bearer), plus `X-initiatingParticipantID` and `X-market`. See
`authentication/aemo-authentication.yml`.

## Steps

1. **Survey what exists.** `retrieveOutageFromOutageManagement` returns outages for the caller;
   `retrieveLatestOutageStatusForNetworkOperator` returns the latest status for a network operator.
2. **Inspect one.** `getParticularOutage` takes the `outageNumber` path parameter.
3. **Create.** `createANewNetworkOutageInOutageManagementSystem` for network assets;
   `createANewGeneratorOutageInOutageManagementSystem` for generating units. Capture the returned
   outage number.
4. **Amend.** `updateExistingNetworkOutageInOutageManagementSystem` (PUT, keyed on `outageNumber`).
5. **Withdraw.** `withdrawExistingNetworkOutageInOutageManagementSystem` for one, or
   `withdrawExistingNetworkOutagesInOutageManagementSystem` for a bulk withdrawal. Always confirm
   the exact set of outage numbers with the operator before a bulk withdrawal.

## Rules

- Never create, update, withdraw or bulk-withdraw without explicit operator confirmation of the
  outage number(s) and the window.
- Re-read with `getParticularOutage` after every write; there is no idempotency key
  (`conventions/aemo-conventions.yml`).
- `422` is a business validation failure or a URM permission gap. `429` is gateway throttling.
- AEMO's planned IT change windows are published separately at
  `lifecycle/aemo-lifecycle.yml` → `status_page`.
