---
name: Read Consumer Data Right energy data from AEMO
description: Use AEMO's Consumer Data Right secondary data holder APIs to read energy plans, service points, usage, DER and account data under the Consumer Data Standards.
api: openapi/aemo-cds-energy-api-openapi.yml
operations: [listEnergyPlans, getEnergyPlanDetail, listElectricityServicePoints, getElectricityServicePointDetail, getElectricityServicePointUsage, listElectricityUsageForServicePoints, getElectricityDERForServicePoint, listElectricityDERForSpecificServicePoints, listEnergyAccounts, getEnergyAccountDetail, getStatus, getOutages]
---

# Read Consumer Data Right energy data from AEMO

AEMO is the Consumer Data Right **secondary data holder** for energy. Two specs back this flow:

- `openapi/aemo-cds-energy-api-openapi.yml` — the CDR Energy API (Consumer Data Standards v1.36.0).
- `openapi/aemo-cds-common-api-openapi.yml` — Common (customer) plus the discovery endpoints.

The e-Hub-fronted variants are `openapi/aemo-cdr-openapi.yml` and
`openapi/aemo-cdr-common-openapi.yml` at
`https://apis.prod.aemo.com.au:9319/NEMRetail/cds-au/v1/…`.

## Required headers

Consumer Data Standards headers, not AEMO-invented ones:

- `x-v` — the endpoint version you are requesting; `x-min-v` — the minimum you will accept.
- `x-fapi-interaction-id`, `x-fapi-auth-date`, `x-fapi-customer-ip-address` — FAPI interaction
  headers.
- `x-cds-client-headers`, and `x-cds-arrangement` where the endpoint requires the arrangement ID.

Consented, customer-present calls carry the consumer's authorisation; unattended calls must
respect the arrangement. See `conformance/aemo-conformance.yml`.

## Steps

1. **Check the surface is up.** `getStatus` (`GET /discovery/status`) and `getOutages`
   (`GET /discovery/outages`) are the machine-readable health and planned-outage endpoints. Call
   `getStatus` before a batch run.
2. **Generic plans** (no consent needed): `listEnergyPlans`, then `getEnergyPlanDetail` for
   `{planId}`.
3. **Service points**: `listElectricityServicePoints`, then `getElectricityServicePointDetail` for
   `{servicePointId}`.
4. **Usage**: `getElectricityServicePointUsage` for one service point, or
   `listElectricityUsageForServicePoints` (POST) for a specific set.
5. **DER**: `getElectricityDERForServicePoint`, or
   `listElectricityDERForSpecificServicePoints` (POST) for a set.
6. **Accounts**: `listEnergyAccounts`, `getEnergyAccountDetail`, and the balance / invoice /
   billing / concession / payment-schedule endpoints on the same spec.

## Rules

- **Paginate properly.** `page` and `page-size` on request; `meta.totalRecords`, `meta.totalPages`
  and `links.next` on response. Follow `links.next` rather than guessing page counts.
- **Errors are the CDS error object**, not RFC 9457: `errors[]` of `{code, title, detail, meta}`.
  `422` carries the mandated CDS business-validation codes. See `errors/aemo-error-codes.yml`.
- `406` means your `x-v` / `x-min-v` combination is unsupported — negotiate down, do not retry
  unchanged.
- `429` is throttling with no published quota; back off exponentially.
- Consumer energy data is personal information under the Privacy Act and the CDR rules. Retrieve
  only what the consent covers, and do not persist it beyond the arrangement.
