# AEMO (aemo)

AEMO, the Australian Energy Market Operator, is the independent system and market operator for Australia's electricity and gas systems — it dispatches and prices the National Electricity Market across Queensland, New South Wales, Victoria, South Australia and Tasmania every five minutes, runs the Wholesale Electricity Market and the Gas Bulletin Board in Western Australia, operates the Victorian gas declared wholesale market and the Gas Supply Hubs, maintains the MSATS metering registry and the national Distributed Energy Resources register, and publishes the Integrated System Plan. It sits at the centre of the value chain: it does not generate, network or retail energy, it clears the market and holds the settlement-grade metering data that every other participant depends on. Under the Consumer Data Right extended to energy, AEMO is the designated SECONDARY data holder and gateway — retailers are the primary data holders, and AEMO serves NMI standing data, distributed energy resource records and up to twenty-four months of interval meter data through mandated Consumer Data Standards endpoints. Its API posture splits cleanly in two, and the split is the whole story: the market-data half is genuinely, radically open — 103 live NEMWeb report directories plus 68 archive directories of dispatch, price, demand, bidding, constraint and settlement data downloadable by anyone with no key, no account and no licence, alongside anonymous JSON endpoints behind the public NEM dashboard; the participant and consumer half is completely closed — a public developer portal at dev.aemo.com.au catalogues 74 APIs and 771 operations that anyone may read, but every one of them requires registration as an AEMO market participant, a Participant ID, MSATS user rights and an AEMO-signed mutual-TLS client certificate, and the OpenAPI documents the portal exports publicly are empty shells that declare zero paths and point at internal hostnames.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/aemo/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/aemo/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- Electricity
- Gas
- Energy Markets
- Grid
- Market Operator
- System Operator
- Open Energy Data
- Consumer Data Right
- CDR
- Smart Metering
- Distributed Energy Resources
- Renewables
- Utilities

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### AEMO NEM Data Dashboard API

The JSON API behind AEMO's public National Electricity Market data dashboard, and the closest thing AEMO operates to an open real-time market API. Confirmed live and fully anonymous on 2026-07-27: GET /aemo/apps/api/report/ELEC_NEM_SUMMARY returned HTTP 200 with five-minute regional records for NSW1, QLD1, SA1, TAS1 and VIC1 — settlement date, spot price and price status, total demand, net interconnector interchange, scheduled and semi-scheduled generation, administered-price and market-suspension flags, per-interconnector flows with export and import limits — plus a full FCAS price set (raise/lower regulation and 1s, 6s, 60s and 5min contingency) and the ten most recent AEMO electricity market notices. POST /aemo/apps/api/report/5MIN with body {"timeScale":["5MIN"]} returned HTTP 200 with a rolling five-minute regional price and demand series. No API key, no account, no licence, no rate-limit challenge. It is also entirely undocumented — AEMO publishes no reference, no schema and no terms for it, so it is recorded here as a verified public endpoint rather than as a supported product.

- **Human URL:** [https://visualisations.aemo.com.au/aemo/apps/visualisations/index.html](https://visualisations.aemo.com.au/aemo/apps/visualisations/index.html)
- **Base URL:** `https://visualisations.aemo.com.au/aemo/apps/api/report`

#### Tags

- National Electricity Market
- Open Data
- Real Time
- Prices
- Demand
- Generation
- Interconnectors
- FCAS
- Energy
- Australia

#### Properties

- [Documentation](https://visualisations.aemo.com.au/aemo/apps/visualisations/index.html)
- [Website](https://visualisations.aemo.com.au/)

### AEMO NEMWeb Public Data Feed

NEMWeb is AEMO's open bulk-data channel for the National Electricity Market and the single largest genuinely open energy dataset in Australia. It is not a REST API — it is an anonymously browsable HTTP directory tree of zipped CSV reports, refreshed on dispatch, daily and settlement cycles, and it is how the entire Australian energy analytics industry gets its data. Confirmed on 2026-07-27: GET https://nemweb.com.au/Reports/Current/ returned HTTP 200 listing 103 report directories — Dispatch_Reports, DispatchIS_Reports, Dispatch_SCADA, Bidmove_Complete, Billing, Marginal_Loss_Factors, Market_Notice, Medium_Term_PASA_Reports, Next_Day_*, Network, ROOFTOP_PV, TradingIS_Reports and more — and GET /Reports/Archive/ returned HTTP 200 with a further 68 archive directories. A sample file, /Reports/CURRENT/DispatchIS_Reports/PUBLIC_DISPATCHIS_202607252230_0000000529244762.zip, downloaded with HTTP 200 and 18,252 bytes of application/x-zip-compressed with no credential of any kind. The MMS Data Model that describes the CSV schemas is published separately at /Reports/Current/MMSDataModelReport.

- **Human URL:** [https://nemweb.com.au/Reports/Current/](https://nemweb.com.au/Reports/Current/)
- **Base URL:** `https://nemweb.com.au/Reports`

#### Tags

- National Electricity Market
- Open Data
- Bulk Data
- Dispatch
- Prices
- Settlements
- Bidding
- Energy
- Australia

#### Properties

- [Documentation](https://nemweb.com.au/Reports/Current/MMSDataModelReport/)
- [Data Feed](https://nemweb.com.au/Reports/Current/)
- [Archive](https://nemweb.com.au/Reports/Archive/)

### AEMO WA Market Data Public Feed

The Western Australian equivalent of NEMWeb, covering the Wholesale Electricity Market that AEMO operates separately from the NEM. Confirmed anonymous and live on 2026-07-27: GET https://data.wa.aemo.com.au/public/ returned HTTP 200 with directory listings for market-data, public-data, outages, advisories, infographic and INF, and GET /public/market-data/ returned HTTP 200 exposing capo, dsp, mt-pasa, outages, st-pasa and wemde subdirectories — the WEM Dispatch Engine outputs, short and medium term PASA, demand side programme and capacity data. Like NEMWeb it is an open HTTP file tree rather than a REST API, and like NEMWeb it needs no key, account or licence.

- **Human URL:** [https://data.wa.aemo.com.au/public/](https://data.wa.aemo.com.au/public/)
- **Base URL:** `https://data.wa.aemo.com.au/public`

#### Tags

- Wholesale Electricity Market
- Western Australia
- Open Data
- Bulk Data
- Dispatch
- Capacity
- Energy
- Australia

#### Properties

- [Data Feed](https://data.wa.aemo.com.au/public/market-data/)
- [Data Feed](https://data.wa.aemo.com.au/public/public-data/)
- [Data Feed](https://data.wa.aemo.com.au/public/outages/)

### AEMO B2BMessagingAsync

The B2BMessagingAsync API is a B2B SMP APIs used to send and recieve B2B messages between the participants in an asynchronous fashion. AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /ws/B2BMessagingAsync. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2bmessaging-async-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2bmessaging-async-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO B2BMessagingPull

The B2BMessagingPull API is a B2B SMP API used to send and receive B2B messages between the participants in a Pull messaging pattern. The messages will be queued in the e-Hub and the receiving participant can poll the e-Hub, ‘pull’ and process the messages that are queued. AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /ws/B2BMessagingPull. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2bmessaging-pull-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2bmessaging-pull-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO B2BMessagingSync

The B2BMessagingSync API is a B2B SMP APIs used to send and receive B2B messages between the participants in a synchronous fashion. AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /ws/B2BMessagingSync. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2bmessaging-sync-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2bmessaging-sync-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO B2MMessagingAsync

The B2MMessagingAsync push-push API supports inbound submitMessages, submitMessageAcknowledgements, and getQueueMetaData endpoints and suits a high volume exchange of messages. Participants push their outgoing message to the e-Hub and the e-Hub pushes the message to the Participants Gateway. AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/B2MMessagingAsync. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2mmessaging-async-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2mmessaging-async-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO B2MMessagingPull

The B2MMessagingPull push-pull API supports inbound submitMessages, submitMessageAcknowledgements, getMessages, and getQueueMetaData endpoints and suits low volume exchange of messages. Participants using B2MMessagingPull are responsible for implementing the polling logic to poll their Participant Hub Queue to retrieve new messages, similar to batch programs used to poll their outbox using FTP. AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/B2MMessagingPull. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2mmessaging-pull-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2mmessaging-pull-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO B2MMessagingSync

The B2MMessagingSync API supports generateC1Report, generateC4Report, getMSATSLimits,NMIDiscovery, getNMIDetail, getParticipantSystemStatus, and getMeterData endpoints.The API participant pushes their outgoing message to the e-Hub and the e-Hub pushes the message to the API recipient.The message delivery occurs synchronously where the participant sends the message to the e-Hub and AEMO immediately AEMO's public API catalogue lists 7 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/B2MMessagingSync. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-b2mmessaging-sync-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/b2mmessaging-sync-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2

AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2.1

AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2-1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2.2

AEMO's public API catalogue lists 6 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2-2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2.3

AEMO's public API catalogue lists 6 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-3-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2-3?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2.4

AEMO's public API catalogue lists 6 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-4-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2-4?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Reports v2.5

AEMO's public API catalogue lists 7 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-reports-v2-5-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-reports-v2-5?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Balancing Submission v2

AEMO's public API catalogue lists 8 operation(s) for this API, gateway-routed under the path prefix /WEM/balancing/submissions. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-balancing-submission-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/balancing-submission-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Bilateral/Stem Submission v1

AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /WEM/trading. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-bilateral-stem-submission-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/bilateral-stem-submission-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO BlindUpdate

The BlindUpdateTool API supports Upload of blind update Data by participants facing API's to backend MSATS systems , Download processed Blind Update file, List of all the Blind Update files uploaded by the Participants. Participants will access the BlindUpdateTool tab from the Browser which invokes the respective process in the API Management. AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/BlindUpdate. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-blindupdate-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/blindupdate-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Capacity

The Capacity API is used by facility operators and trading participants to submit and receive data relating to capacity trades and day ahead auction for AEMO’s Capacity Transfer Platform (CTP) and Day-Ahead Auction (DAA) market systems. AEMO's public API catalogue lists 13 operation(s) for this API, gateway-routed under the path prefix /ws/gsh/capacity. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Gas Supply Hub
- Gas
- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-capacity-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/capacity-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO CapacityAuction

The Capacity Auction API is used by facility operators and trading participants to submit and receive data relating to capacity trades and day ahead auction for AEMO’s Capacity Transfer Platform (CTP) and Day-Ahead Auction (DAA) market systems. AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /ws/gsh/capacityAuction. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Gas Supply Hub
- Gas
- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-capacityAuction-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/capacityAuction-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO CDR

The Consumer Data Right (CDR) APIs allow Registered Financially Responsible Market Participants (FRMPs) to service API requests for AEMO data from Accredited Data Recipients. AEMO's public API catalogue lists 6 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/cds-au/v1/secondary/energy. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)
- **Base URL:** `https://apis.prod.aemo.com.au:9319/NEMRetail/cds-au/v1/secondary/energy`

#### Tags

- Consumer Data Right
- CDR
- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-cdr-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/cdr?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)
- [OpenAPI](openapi/aemo-cds-energy-api-openapi.yml)
- [API Standards](https://consumerdatastandardsaustralia.github.io/standards/#energy-secondary-dh-apis)
- [Documentation](https://dev.aemo.com.au/CDR)

### AEMO CDR Common

AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/cds-au/v1/discovery. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)
- **Base URL:** `https://apis.prod.aemo.com.au:9319/NEMRetail/cds-au/v1/discovery`

#### Tags

- Consumer Data Right
- CDR
- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-cdr-common-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/cdr-common?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)
- [OpenAPI](openapi/aemo-cds-common-api-openapi.yml)
- [API Standards](https://consumerdatastandardsaustralia.github.io/standards/#discovery-apis)
- [Documentation](https://dev.aemo.com.au/CDR-Common)

### AEMO DER Registration For Account Holders

Using the DER Registration APIs, Account Holders can • Submit DER Connection Agreement data. • Provide AC Connections, and Device details in the same submission AEMO's public API catalogue lists 31 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/DER/consumer/registration. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Distributed Energy Resources
- DER
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-der-consumer-registration-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/der-consumer-registration-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO DER Registration for NSPs

Using the DER Registration APIs, NSPs can • Submit DER Connection Agreement data. • Provide AC Connections, and Device details in the same submission AEMO's public API catalogue lists 8 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/DER/registration. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Distributed Energy Resources
- DER
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-der-business-registration-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/der-business-registration-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO EE Simulation Status Update

EE Simulation Status Update APIs are used by EE to submit the simulation status update AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /ee-simulation-status-update. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-ee-simulation-status-update-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/ee-simulation-status-update-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO EnablementInstruction

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /NEM/v1/ISF-External/enablementInstruction. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-enablementinstruction-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/enablementinstruction-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO GasBB Reporting Public Data

This API is intended for AEMO's use only, used by AEMO web pages and is not supported for any other use. It can change at any time. See https://dev.aemo.com.au/ for information on using AEMO APIs. AEMO's public API catalogue lists 29 operation(s) for this API, gateway-routed under the path prefix /gasbb-reporting-data. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Gas Bulletin Board
- Gas
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-gasbb-reporting-public-data-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/gasbb-reporting-public-data?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO GeneratorRecall

The Generator Recall API is used by generators to send information about recall times into the Generator Recall web-based interface in the EMMS Markets Portal. The system will then transfer the information to a central AEMO database for viewing and reporting by AEMO operators. AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /ws/GeneratorRecall. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-generatorRecall-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/generatorRecall-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO HubMessageManagement

The HubMessageManagement API is a B2B SMP APIs used retrieve the current list of stop files for all participants or for a specific participant (using alerts) resource. Participants can use this resource to: 1. Ensure technical requirements required to connect to e-Hub are validated (for example, appropriate network ports are open). AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /ws/HubMessageManagement. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-hubmsgmgt-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/hubmsgmgt-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO HubMessageManagementV2

The HubMessageManagement push API retrieves the current list of B2B and B2M stop files. Business transactions are sent as aseXML documents carried as payloads inside the API message and transmitted over HTTPS. Participants can also use this API to: 1. Ensure technical requirements required to connect to the e-Hub are validated (for example, appropriate network ports are open). 2. AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /HubMessageManagement. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-hubmsgmgt-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/hubmsgmgt-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO IdentityService(v2)

This API is used by a Participant to update their password for MSATs. AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /ws/Common/identityService. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Authentication
- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-identityService-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/identityService-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Intermittent Generation Availability Submissions

This API is used for intermittent generation availability submissions. AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /v1/IntermittentGen. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-opsforecasting-intermittentgen-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/opsforecasting-intermittentgen-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO LFAS Reports v2

AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /WEM/lfas/v2. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-lfas-reports-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/lfas-reports-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO LFAS Submission v2

AEMO's public API catalogue lists 8 operation(s) for this API, gateway-routed under the path prefix /WEM/lfas/submissions/v2. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-lfas-submission-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/lfas-submission-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Market Reports v2

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/market. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-market-reports-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/market-reports-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO MeterExemption

The Meter Exemptions API enables registered Metering Coordinators (MCs) to create and manage metering exemptions within MSATS. AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /NEMRetail/v1/meterExemption. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Retail
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-meterexemption-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/meterexemption-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO MT PASA Offers

The MT PASA Offers API allows Scheduled Generators, Market Customers, Market Network Service Providers, and Integrated Resource Providers to submit their MT PASA Offers for Bi-directional Units (BDU), Scheduled Generation Units (SGU), Scheduled Load Units (SLU), and Scheduled Network Services (SNS). MT PASA Offers are input into the MT PASA process. AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/v1/mtpasaoffers. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-mtpasaoffers-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/mtpasaoffers-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO NEMDispatchBidding

Bidding Service Open API specification AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/bidding. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-bidding-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/bidding-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO oauth-v1

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /oauth/v1. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Authentication
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-oauth-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/oauth-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO OIP

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/outageIntentionPlan. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-oip-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/oip-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Outage Management

AEMO's public API catalogue lists 8 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/outageManagement. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-outage-management-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/outage-management-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO P2PMessagingSync

The P2PMessagingSync API is a B2B SMP APIs used to exchange the following Peer-to-Peer information via the e-Hub: - Free-form information - Documents (also called Attachments). The P2PMessagingSync API supports exchange of the following attachment types (configurable): pdf, csv, jpeg, jpe, jpg, gif, zip & txt. In future, this API will support additional attachment types. AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /ws/P2PMessagingSync. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-p2pmessaging-sync-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/p2pmessaging-sync-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Pre-Balancing Reports v6

AEMO's public API catalogue lists 70 operation(s) for this API, gateway-routed under the path prefix /WEM/reports. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-pre-balancing-reports-v6-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/pre-balancing-reports-v6?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Pre-Balancing Reports v7

AEMO's public API catalogue lists 71 operation(s) for this API, gateway-routed under the path prefix /WEM/reports. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-pre-balancing-reports-v7-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/pre-balancing-reports-v7?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Pre-Balancing Reports v7.1

AEMO's public API catalogue lists 71 operation(s) for this API, gateway-routed under the path prefix /WEM/reports. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-pre-balancing-reports-v7-1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/pre-balancing-reports-v7-1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Pre-Balancing Reports v8

AEMO's public API catalogue lists 73 operation(s) for this API, gateway-routed under the path prefix /WEM/reports. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-pre-balancing-reports-v8-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/pre-balancing-reports-v8?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Prudentials

This API supports the various operations performed on Prudentials dashboard AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/Prudentials. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-prudentials-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/prudentials-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO RCM Operations

AEMO's public API catalogue lists 50 operation(s) for this API, gateway-routed under the path prefix /WEM/RCM. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-rcm-ops-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/rcm-ops-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Reallocations

The Reallocation API allow you to create, authorise, cancel reallocations. You can also search and retrieve reallocations, calendars, participants, profile types, agreement types, and market price cap AEMO's public API catalogue lists 13 operation(s) for this API, gateway-routed under the path prefix /ws/NEMWholesale/reallocations. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-reallocations-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/reallocations-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Report

The report API allows participants to retrieve data from the Gas Bulletin Board (BB). AEMO's public API catalogue lists 22 operation(s) for this API, gateway-routed under the path prefix /ws/gbb/report. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Gas Bulletin Board
- Gas
- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-report-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/report-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO RTMS

The WEM-Reform API for Real-Time Market submissions available to all Market Participants. AEMO's public API catalogue lists 15 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/realTimeMarketSubmission. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-rtms-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/rtms-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO SelfForecast

The Self forecasting API is used by participants who wish to submit their Solar or Wind Forecasts for a DUID to AEMO. AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /ws/NEMWholesale/selfForecast. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-selfForecast-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/selfForecast-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Settlement Direct

This API supports the various operations performed in Settlement Direct API AEMO's public API catalogue lists 13 operation(s) for this API, gateway-routed under the path prefix /NEMWholesale/PublishingDirect. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-settlementDirect-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/settlementDirect-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO Submission

The submission API allows participants to submit data to the Gas Bulletin Board (BB). Data submission from BB reporting entities to the BB are divided into two key areas- - Data transfer formats which includes the form, validation rules, and timing of submissions. - Data submission methods to the BB, and how the success and failure of those submissions is communicated back to the submitter. AEMO's public API catalogue lists 37 operation(s) for this API, gateway-routed under the path prefix /ws/gbb/submission. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Gas Bulletin Board
- Gas
- e-Hub
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-submission-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/submission-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2

AEMO's public API catalogue lists 7 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.1

AEMO's public API catalogue lists 9 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.2

AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.3

AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-3-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-3?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.4

AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-4-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-4?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.5

AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-5-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-5?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO System Management Reports v2.6

AEMO's public API catalogue lists 10 operation(s) for this API, gateway-routed under the path prefix /WEM/sm. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-system-management-reports-v2-6-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/system-management-reports-v2-6?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO TLS Certificate Mgmt v1

The TLS Certificate Management API allows authorised participants to self-manage their AEMO-signed TLS certificates. AEMO's public API catalogue lists 8 operation(s) for this API, gateway-routed under the path prefix /v1/TlsCertificateMgmt. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)
- **Base URL:** `https://partner.api.aemo.com.au/v1/TLSCertificateManagement`

#### Tags

- Authentication
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-tls-certificate-mgmt-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/tls-certificate-mgmt-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO VariableParameter

AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /NEM/v1/ISF-External/variableParameter. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- National Electricity Market
- Wholesale
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-variableparameter-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/variableparameter-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEM Attributes Report

AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/attributes. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-attributes-report-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/attributes-report-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEM DER Installation V2

WEM DER Installation API enables the Network Operator to create, update, and retrieve the DER Register information details for the DER installations they have submitted to the DER Register database and to view and resolve associated exceptions AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /v2/der-register. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Distributed Energy Resources
- DER
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-der-register-installation-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/der-register-installation-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEM DER NMI

Using the WEM DER Registration APIs, consumers can Create, update and retrieve NMI details AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /wem/v1/der-register. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Distributed Energy Resources
- DER
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-der-register-nmi-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/der-register-nmi-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchCase

AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/dispatchCase. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchcase-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchcase-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchCase V2

AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /WEM/v2/dispatchCase. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchcase-external-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchcase-external-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchInstruction

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/dispatchInstruction. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchinstruction-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchinstruction-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchSolution

AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/dispatchSolution. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchsolution-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchsolution-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchSolution V2

AEMO's public API catalogue lists 3 operation(s) for this API, gateway-routed under the path prefix /WEM/v2/dispatchSolution. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchsolution-external-v2-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchsolution-external-v2?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DispatchSummary

AEMO's public API catalogue lists 4 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/dispatchSummary. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dispatchsummary-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dispatchsummary-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE DSPDispatchInstruction

AEMO's public API catalogue lists 5 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/DSPDispatchInstruction. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-dspdispatchinstruction-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-dspdispatchinstruction-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE NCESS

AEMO's public API catalogue lists 2 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/Ncess. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-ncess-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-ncess-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE NotInServiceCapacity

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/notInServiceCapacity. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-notinservicecapacity-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-notinservicecapacity-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE ReferenceTradingPrice

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/referenceTradingPrice. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-referencetradingprice-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-referencetradingprice-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

### AEMO WEMDE TradingDayReport

AEMO's public API catalogue lists 1 operation(s) for this API, gateway-routed under the path prefix /WEM/v1/tradingDayReport. The OpenAPI document AEMO exports for it publicly is a shell: it carries the title, description and API-key security schemes but declares paths: {} — zero operations — and names an internal host rather than a reachable gateway. Harvested verbatim on 2026-07-27 (HTTP 200).

- **Human URL:** [https://dev.aemo.com.au/api-docs](https://dev.aemo.com.au/api-docs)

#### Tags

- Wholesale Electricity Market
- Western Australia
- Energy
- Australia

#### Properties

- [OpenAPI](openapi/aemo-wemde-tradingdayreport-external-v1-openapi.yml)
- [API Reference](https://dev.aemo.com.au/developer/apis/wemde-tradingdayreport-external-v1?api-version=2022-04-01-preview)
- [Documentation](https://dev.aemo.com.au/api-docs)

## Common Properties

- [Website](https://aemo.com.au/)
- [DeveloperPortal](https://dev.aemo.com.au/)
- [Documentation](https://dev.aemo.com.au/api-docs)
- [API Reference](https://dev.aemo.com.au/developer/apis?api-version=2022-04-01-preview)
- [GettingStarted](https://dev.aemo.com.au/working-with-aemo-apis)
- [SignUp](https://dev.aemo.com.au/signup)
- [TermsOfService](https://dev.aemo.com.au/terms)
- [Authentication](https://dev.aemo.com.au/urm-username-password)
- [OAuth](https://dev.aemo.com.au/oauth)
- [PostmanCollection](https://documenter.getpostman.com/view/10032049/2s93CNNDaK)
- [ConsumerDataRight](https://aemo.com.au/initiatives/major-programs/cdr-at-aemo)
- [API Standards](https://consumerdatastandardsaustralia.github.io/standards/)
- [Regulator](https://www.cdr.gov.au/)
- [Data Feed](https://nemweb.com.au/Reports/Current/)
- [Data Feed](https://data.wa.aemo.com.au/public/)
- [Dashboard](https://visualisations.aemo.com.au/aemo/apps/visualisations/index.html)
- [GasBulletinBoard](https://gbbwa.aemo.com.au/)
- [MarketsPortalHelp](https://markets-portal-help.docs.public.aemo.com.au/Content/API_Reference/API_introduction.htm)
- [Registration](https://www.aemo.com.au/energy-systems/registration)
- [LinkedIn](https://au.linkedin.com/company/aemo)

## Maintainers

- Kin Lane — kin@apievangelist.com
