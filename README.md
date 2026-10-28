# AEMO

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AEMO, the Australian Energy Market Operator, is the independent system and market operator for Australia's electricity and gas systems — it dispatches and prices the National Electricity Market across Queensland, New South Wales, Victoria, South Australia and Tasmania every five minutes, runs the Wholesale Electricity Market and the Gas Bulletin Board in Western Australia, operates the Victorian gas declared wholesale market and the Gas Supply Hubs, maintains the MSATS metering registry and the national Distributed Energy Resources register, and publishes the Integrated System Plan. It sits at the centre of the value chain: it does not generate, network or retail energy, it clears the market and holds the settlement-grade metering data that every other participant depends on. Under the Consumer Data Right extended to energy, AEMO is the designated SECONDARY data holder and gateway — retailers are the primary data holders, and AEMO serves NMI standing data, distributed energy resource records and up to twenty-four months of interval meter data through mandated Consumer Data Standards endpoints. Its API posture splits cleanly in two, and the split is the whole story: the market-data half is genuinely, radically open — 103 live NEMWeb report directories plus 68 archive directories of dispatch, price, demand, bidding, constraint and settlement data downloadable by anyone with no key, no account and no licence, alongside anonymous JSON endpoints behind the public NEM dashboard; the participant and consumer half is completely closed — a public developer portal at dev.aemo.com.au catalogues 74 APIs and 771 operations that anyone may read, but every one of them requires registration as an AEMO market participant, a Participant ID, MSATS user rights and an AEMO-signed mutual-TLS client certificate, and the OpenAPI documents the portal exports publicly are empty shells that declare zero paths and point at internal hostnames.

**Areas:** Energy · Australia · Electricity · Gas · Energy Markets · Grid · Market Operator · System Operator · Open Energy Data · Consumer Data Right · CDR · Smart Metering

## AEMO on APIs.io

Everything profiled for AEMO is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aemo/](https://apis.io/providers/aemo/)** — or go straight to one of the APIs or properties below.

### APIs (63)

- [AEMO NEM Data Dashboard API](https://apis.io/apis/aemo/aemo-nem-data-dashboard-api/) — The JSON API behind AEMO's public National Electricity Market data dashboard, and the closest thing AEMO operates to an open real-time market API. Confirmed…
- [AEMO NEMWeb Public Data Feed](https://apis.io/apis/aemo/aemo-nemweb-public-data-feed/) — NEMWeb is AEMO's open bulk-data channel for the National Electricity Market and the single largest genuinely open energy dataset in Australia. It is not a…
- [AEMO WA Market Data Public Feed](https://apis.io/apis/aemo/aemo-wa-market-data-public-feed/) — The Western Australian equivalent of NEMWeb, covering the Wholesale Electricity Market that AEMO operates separately from the NEM. Confirmed anonymous and…
- [AEMO B2 B Messaging Pull API](https://apis.io/apis/aemo/aemo-b2bmessagingpull-api/) — The B2BMessagingPull API is a B2B SMP API used to send and receive B2B messages between the participants in a Pull messaging pattern. The messages will be…
- [AEMO B2 M Messaging Pull API](https://apis.io/apis/aemo/aemo-b2mmessagingpull-api/) — Introduction
- [AEMO B2 M Messaging Sync API](https://apis.io/apis/aemo/aemo-b2mmessagingsync-api/) — Introduction
- [AEMO Balancing Reports v2.5 API](https://apis.io/apis/aemo/aemo-balancing-reports-v2-5-api/) — Balancing Reports v2.5
- [AEMO Balancing Submission v2 API](https://apis.io/apis/aemo/aemo-balancing-submission-v2-api/) — Balancing Submission v2
- [AEMO Bilateral/Stem Submission v1 API](https://apis.io/apis/aemo/aemo-bilateral-stem-submission-v1-api/) — Bilateral/Stem Submission v1
- [AEMO Blind Update API](https://apis.io/apis/aemo/aemo-blindupdate-api/) — Introduction
- [AEMO Capacity API](https://apis.io/apis/aemo/aemo-capacity-api/) — Capacity
- [AEMO Capacity Auction API](https://apis.io/apis/aemo/aemo-capacityauction-api/) — CapacityAuction
- [AEMO CDR API](https://apis.io/apis/aemo/aemo-cdr-api/) — Introduction
- [AEMO CDR Common API](https://apis.io/apis/aemo/aemo-cdr-common-api/) — CDR Common
- [AEMO Data Holder Customers API](https://apis.io/apis/aemo/aemo-data-holder-customers-api/) — Data Holder Customer endpoints
- [AEMO Data Holder Operations API](https://apis.io/apis/aemo/aemo-data-holder-operations-api/) — Data Holder Operations endpoints
- [AEMO DER Registration For Account Holders API](https://apis.io/apis/aemo/aemo-der-registration-for-account-holders-api/) — Introduction
- [AEMO Distributed Energy Resources API](https://apis.io/apis/aemo/aemo-distributed-energy-resources-api/) — Distributed Energy Resource endpoints
- [AEMO EE Simulation Status Update API](https://apis.io/apis/aemo/aemo-ee-simulation-status-update-api/) — Introduction
- [AEMO Electricity Service Points API](https://apis.io/apis/aemo/aemo-electricity-service-points-api/) — Electricity Service Point endpoints
- [AEMO Electricity Usage API](https://apis.io/apis/aemo/aemo-electricity-usage-api/) — Electricity Usage endpoints
- [AEMO Enablement Instruction API](https://apis.io/apis/aemo/aemo-enablementinstruction-api/) — EnablementInstruction
- [AEMO Energy Account Balances API](https://apis.io/apis/aemo/aemo-energy-account-balances-api/) — Energy Account Balance endpoints
- [AEMO Energy Account Billing API](https://apis.io/apis/aemo/aemo-energy-account-billing-api/) — Energy Account Billing endpoints
- [AEMO Energy Accounts API](https://apis.io/apis/aemo/aemo-energy-accounts-api/) — Energy Account endpoints
- [AEMO Energy Plans API](https://apis.io/apis/aemo/aemo-energy-plans-api/) — Energy Plan endpoints
- [AEMO GasBB Reporting Public Data API](https://apis.io/apis/aemo/aemo-gasbb-reporting-public-data-api/) — This API is intended for AEMO's use only, used by AEMO web pages and is not supported for any other use. It can change at any time. See…
- [AEMO Generator Recall API](https://apis.io/apis/aemo/aemo-generatorrecall-api/) — The Generator Recall API is used by generators to send information about recall times into the Generator Recall web-based interface in the EMMS Markets…
- [AEMO Hub Message Management API](https://apis.io/apis/aemo/aemo-hubmessagemanagement-api/) — Introduction
- [AEMO Hub Message Management V2 API](https://apis.io/apis/aemo/aemo-hubmessagemanagementv2-api/) — Introduction
- [AEMO Identity Service(v2) API](https://apis.io/apis/aemo/aemo-identityservice-v2-api/) — Introduction
- [AEMO Intermittent Generation Availability Submissions API](https://apis.io/apis/aemo/aemo-intermittent-generation-availability-submissions-api/) — Introduction
- [AEMO LFAS Reports v2 API](https://apis.io/apis/aemo/aemo-lfas-reports-v2-api/) — LFAS Reports v2
- [AEMO LFAS Submission v2 API](https://apis.io/apis/aemo/aemo-lfas-submission-v2-api/) — LFAS Submission v2
- [AEMO Market Reports v2 API](https://apis.io/apis/aemo/aemo-market-reports-v2-api/) — Market Reports v2
- [AEMO Meter Exemption API](https://apis.io/apis/aemo/aemo-meterexemption-api/) — The Meter Exemptions API enables registered Metering Coordinators (MCs) to create and manage metering exemptions within MSATS.
- [AEMO NEM Dispatch Bidding API](https://apis.io/apis/aemo/aemo-nemdispatchbidding-api/) — Bidding Service Open API specification
- [AEMO OIP API](https://apis.io/apis/aemo/aemo-oip-api/) — OIP
- [AEMO Outage Management API](https://apis.io/apis/aemo/aemo-outage-management-api/) — Outage Management
- [AEMO Pre-Balancing Reports v8 API](https://apis.io/apis/aemo/aemo-pre-balancing-reports-v8-api/) — Pre-Balancing Reports v8
- [AEMO Prudentials API](https://apis.io/apis/aemo/aemo-prudentials-api/) — This API supports the various operations performed on Prudentials dashboard
- [AEMO RCM Operations API](https://apis.io/apis/aemo/aemo-rcm-operations-api/) — RCM Operations
- [AEMO Reallocations API](https://apis.io/apis/aemo/aemo-reallocations-api/) — Introduction
- [AEMO Report API](https://apis.io/apis/aemo/aemo-report-api/) — Report
- [AEMO RTMS API](https://apis.io/apis/aemo/aemo-rtms-api/) — The WEM-Reform API for Real-Time Market submissions available to all Market Participants.
- [AEMO Self Forecast API](https://apis.io/apis/aemo/aemo-selfforecast-api/) — Introduction
- [AEMO Settlement Direct API](https://apis.io/apis/aemo/aemo-settlement-direct-api/) — This API supports the various operations performed in Settlement Direct API
- [AEMO Submission API](https://apis.io/apis/aemo/aemo-submission-api/) — Submission
- [AEMO System Management Reports v2.2 API](https://apis.io/apis/aemo/aemo-system-management-reports-v2-2-api/) — System Management Reports v2.2
- [AEMO TLS Certificate Mgmt v1 API](https://apis.io/apis/aemo/aemo-tls-certificate-mgmt-v1-api/) — The TLS Certificate Management API allows authorised participants to self-manage their AEMO-signed TLS certificates. This API provides the following features:
- [AEMO Variable Parameter API](https://apis.io/apis/aemo/aemo-variableparameter-api/) — VariableParameter
- [AEMO WEM Attributes Report API](https://apis.io/apis/aemo/aemo-wem-attributes-report-api/) — WEM Attributes Report
- [AEMO WEM DER Installation V2 API](https://apis.io/apis/aemo/aemo-wem-der-installation-v2-api/) — Introduction
- [AEMO WEM DER NMI API](https://apis.io/apis/aemo/aemo-wem-der-nmi-api/) — Introduction
- [AEMO WEMDE DispatchCase API](https://apis.io/apis/aemo/aemo-wemde-dispatchcase-api/) — WEMDE DispatchCase
- [AEMO WEMDE DispatchInstruction API](https://apis.io/apis/aemo/aemo-wemde-dispatchinstruction-api/) — WEMDE DispatchInstruction
- [AEMO WEMDE DispatchSolution API](https://apis.io/apis/aemo/aemo-wemde-dispatchsolution-api/) — WEMDE DispatchSolution
- [AEMO WEMDE DispatchSummary API](https://apis.io/apis/aemo/aemo-wemde-dispatchsummary-api/) — WEMDE DispatchSummary
- [AEMO WEMDE DSPDispatchInstruction API](https://apis.io/apis/aemo/aemo-wemde-dspdispatchinstruction-api/) — WEMDE DSPDispatchInstruction
- [AEMO WEMDE NCESS API](https://apis.io/apis/aemo/aemo-wemde-ncess-api/) — WEMDE NCESS
- [AEMO WEMDE NotInServiceCapacity API](https://apis.io/apis/aemo/aemo-wemde-notinservicecapacity-api/) — WEMDE NotInServiceCapacity
- [AEMO WEMDE ReferenceTradingPrice API](https://apis.io/apis/aemo/aemo-wemde-referencetradingprice-api/) — WEMDE ReferenceTradingPrice
- [AEMO WEMDE TradingDayReport API](https://apis.io/apis/aemo/aemo-wemde-tradingdayreport-api/) — WEMDE TradingDayReport

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Aemo Ehub Events](https://apis.io/asyncapis/aemo/aemo-ehub-events/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Aemo Agentic Access](https://apis.io/agentic-access/aemo/aemo-agentic-access/)

#### JSON Schema (19)

The data models the API reads and writes.

- [EnergyAccountDetailResponseV4](https://apis.io/schemas/aemo/aemo-energy-account-detail-response-v4/)
- [EnergyAccountListResponseV2](https://apis.io/schemas/aemo/aemo-energy-account-list-response-v2/)
- [EnergyBalanceListResponse](https://apis.io/schemas/aemo/aemo-energy-balance-list-response/)
- [EnergyBalanceResponse](https://apis.io/schemas/aemo/aemo-energy-balance-response/)
- [EnergyBillingListResponseV3](https://apis.io/schemas/aemo/aemo-energy-billing-list-response-v3/)
- [EnergyConcessionsResponse](https://apis.io/schemas/aemo/aemo-energy-concessions-response/)
- [EnergyDerDetailResponse](https://apis.io/schemas/aemo/aemo-energy-der-detail-response/)
- [EnergyDerListResponse](https://apis.io/schemas/aemo/aemo-energy-der-list-response/)
- [EnergyInvoiceListResponse](https://apis.io/schemas/aemo/aemo-energy-invoice-list-response/)
- [EnergyPaymentScheduleResponse](https://apis.io/schemas/aemo/aemo-energy-payment-schedule-response/)
- [EnergyPlanListResponse](https://apis.io/schemas/aemo/aemo-energy-plan-list-response/)
- [EnergyPlanResponseV3](https://apis.io/schemas/aemo/aemo-energy-plan-response-v3/)
- [EnergyServicePointDetailResponseV2](https://apis.io/schemas/aemo/aemo-energy-service-point-detail-response-v2/)
- [EnergyServicePointListResponseV2](https://apis.io/schemas/aemo/aemo-energy-service-point-list-response-v2/)
- [EnergyUsageListResponse](https://apis.io/schemas/aemo/aemo-energy-usage-list-response/)
- [ResponseCommonCustomer](https://apis.io/schemas/aemo/aemo-response-common-customer/)
- [ResponseCommonCustomerDetailV2](https://apis.io/schemas/aemo/aemo-response-common-customer-detail-v2/)
- [ResponseCommonDiscoveryStatus](https://apis.io/schemas/aemo/aemo-response-common-discovery-status/)
- [ResponseDiscoveryOutagesList](https://apis.io/schemas/aemo/aemo-response-discovery-outages-list/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Aemo Context](https://apis.io/jsonld/aemo/aemo-context/)

#### Collections (76)

Postman and Open Collection request collections.

- [WEM Attributes Report](https://apis.io/collections/aemo/open-aemo-attributes-report-external-v1/)
- [B2BMessagingAsync](https://apis.io/collections/aemo/open-aemo-b2bmessaging-async-v1/)
- [B2BMessagingPull](https://apis.io/collections/aemo/open-aemo-b2bmessaging-pull-v1/)
- [B2BMessagingSync](https://apis.io/collections/aemo/open-aemo-b2bmessaging-sync-v1/)
- [B2MMessagingAsync](https://apis.io/collections/aemo/open-aemo-b2mmessaging-async-v1/)
- [B2MMessagingPull](https://apis.io/collections/aemo/open-aemo-b2mmessaging-pull-v1/)
- [B2MMessagingSync](https://apis.io/collections/aemo/open-aemo-b2mmessaging-sync-v1/)
- [Balancing Reports v2](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2/)
- [Balancing Reports v2.1](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2-1/)
- [Balancing Reports v2.2](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2-2/)
- [Balancing Reports v2.3](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2-3/)
- [Balancing Reports v2.4](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2-4/)
- [Balancing Reports v2.5](https://apis.io/collections/aemo/open-aemo-balancing-reports-v2-5/)
- [Balancing Submission v2](https://apis.io/collections/aemo/open-aemo-balancing-submission-v2/)
- [NEMDispatchBidding](https://apis.io/collections/aemo/open-aemo-bidding-v1/)
- [Bilateral/Stem Submission v1](https://apis.io/collections/aemo/open-aemo-bilateral-stem-submission-v1/)
- [BlindUpdate](https://apis.io/collections/aemo/open-aemo-blindupdate-v1/)
- [Capacity](https://apis.io/collections/aemo/open-aemo-capacity-v1/)
- [CapacityAuction](https://apis.io/collections/aemo/open-aemo-capacityAuction-v1/)
- [CDR](https://apis.io/collections/aemo/open-aemo-cdr/)
- [CDR Common](https://apis.io/collections/aemo/open-aemo-cdr-common/)
- [CDR Common API](https://apis.io/collections/aemo/open-aemo-cds-common-api/)
- [CDR Energy API](https://apis.io/collections/aemo/open-aemo-cds-energy-api/)
- [DER Registration for NSPs](https://apis.io/collections/aemo/open-aemo-der-business-registration-v1/)
- [DER Registration For Account Holders](https://apis.io/collections/aemo/open-aemo-der-consumer-registration-v1/)
- …and 51 more published on APIs.io

#### Overlays (136)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aemo Attributes Report External V1 Overlay](https://apis.io/overlays/aemo/aemo-attributes-report-external-v1-overlay/)
- [Aemo B2Bmessaging Async V1 Overlay](https://apis.io/overlays/aemo/aemo-b2bmessaging-async-v1-overlay/)
- [Aemo B2Bmessaging Pull V1 Overlay](https://apis.io/overlays/aemo/aemo-b2bmessaging-pull-v1-overlay/)
- [Aemo B2Bmessaging Sync V1 Overlay](https://apis.io/overlays/aemo/aemo-b2bmessaging-sync-v1-overlay/)
- [Aemo B2Bmessagingpull Api Overlay](https://apis.io/overlays/aemo/aemo-b2bmessagingpull-api-overlay/)
- [Aemo B2Mmessaging Async V1 Overlay](https://apis.io/overlays/aemo/aemo-b2mmessaging-async-v1-overlay/)
- [Aemo B2Mmessaging Pull V1 Overlay](https://apis.io/overlays/aemo/aemo-b2mmessaging-pull-v1-overlay/)
- [Aemo B2Mmessaging Sync V1 Overlay](https://apis.io/overlays/aemo/aemo-b2mmessaging-sync-v1-overlay/)
- [Aemo B2Mmessagingpull Api Overlay](https://apis.io/overlays/aemo/aemo-b2mmessagingpull-api-overlay/)
- [Aemo B2Mmessagingsync Api Overlay](https://apis.io/overlays/aemo/aemo-b2mmessagingsync-api-overlay/)
- [Aemo Balancing Reports V2 1 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-1-overlay/)
- [Aemo Balancing Reports V2 2 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-2-overlay/)
- [Aemo Balancing Reports V2 3 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-3-overlay/)
- [Aemo Balancing Reports V2 4 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-4-overlay/)
- [Aemo Balancing Reports V2 5 Api Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-5-api-overlay/)
- [Aemo Balancing Reports V2 5 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-5-overlay/)
- [Aemo Balancing Reports V2 Overlay](https://apis.io/overlays/aemo/aemo-balancing-reports-v2-overlay/)
- [Aemo Balancing Submission V2 Api Overlay](https://apis.io/overlays/aemo/aemo-balancing-submission-v2-api-overlay/)
- [Aemo Balancing Submission V2 Overlay](https://apis.io/overlays/aemo/aemo-balancing-submission-v2-overlay/)
- [Aemo Bidding V1 Overlay](https://apis.io/overlays/aemo/aemo-bidding-v1-overlay/)
- [Aemo Bilateral Stem Submission V1 Api Overlay](https://apis.io/overlays/aemo/aemo-bilateral-stem-submission-v1-api-overlay/)
- [Aemo Bilateral Stem Submission V1 Overlay](https://apis.io/overlays/aemo/aemo-bilateral-stem-submission-v1-overlay/)
- [Aemo Blindupdate Api Overlay](https://apis.io/overlays/aemo/aemo-blindupdate-api-overlay/)
- [Aemo Blindupdate V1 Overlay](https://apis.io/overlays/aemo/aemo-blindupdate-v1-overlay/)
- [Aemo Capacity Api Overlay](https://apis.io/overlays/aemo/aemo-capacity-api-overlay/)
- …and 111 more published on APIs.io

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [AEMO API Rules](https://apis.io/rules/aemo/aemo-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Aemo Authentication](https://apis.io/security/aemo/aemo-authentication/)
- [Aemo Domain Security](https://apis.io/security/aemo/aemo-domain-security/)
- [Aemo Vulnerability Disclosure](https://apis.io/security/aemo/aemo-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Aemo Scopes](https://apis.io/scopes/aemo/aemo-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Aemo Plans Pricing](https://apis.io/plans/aemo/aemo-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Aemo Rate Limits](https://apis.io/rate-limits/aemo/aemo-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://aemo.com.au/)
- [Documentation](https://dev.aemo.com.au/api-docs)
- [Getting started](https://dev.aemo.com.au/working-with-aemo-apis)
- [API reference](https://dev.aemo.com.au/developer/apis?api-version=2022-04-01-preview)
- [Sign up](https://dev.aemo.com.au/signup)
- [Support](https://dev.aemo.com.au/contact-us)
- [Changelog](https://aemo.com.au/market-notices?marketNoticeFacets=MARKET+SYSTEMS)
- [Blog](https://www.aemo.com.au/newsroom/news-updates)
- [Security](https://www.aemo.com.au/.well-known/security.txt)
- [Terms of service](https://dev.aemo.com.au/terms)
- [Privacy policy](https://aemo.com.au/en/privacy-and-legal-notices/privacy-policy)
- [Status](https://www.aemo.com.au/energy-systems/market-it-systems/it-change-and-release-management)

## API Evangelist rating

**Kin Score 54.3** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 50.5 |
| Contract governance | 19.7 |
| Operational transparency | 52.6 |
| Developer ergonomics | 70.8 |
| Access clarity | 34.2 |

**Agent readiness 39.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | mostly |

**Regulatory alignment 39.3** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aemo/](https://apis.io/providers/aemo/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AEMO: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aemo/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
