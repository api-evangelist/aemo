---
name: Pull Gas Bulletin Board reports
description: Retrieve AEMO Gas Bulletin Board public reporting data — nominations, forecasts, production and flow, capacity outlooks and secondary capacity trades.
api: openapi/aemo-report-v1-openapi.yml
operations: [dailyFacilitiesReport, dailyReportForNominationAndForecastData, dailyReportForProductionFlowAndStorage, dailyReportForProductionAndUsageAtEachConnectionPoint, dailyReportForCapacityOutlookForTheMediumTerm, adhocReportOnStates, adhocReportForLinepackCapacityAdequacy, adhocReportForStandingNameplateCapacity, adhocReportOnUncontractedCapacityOutlookOnPipelinesAndStorageFacilities, adhocReportPipelineNodeTransfer, weeklyReportOnSecondaryPipelineCapacityAvailableForSaleOnBBPipelines, weeklyReportOnSecondaryPipelineCapacityTrades, dailyReportWithListOfRegisteredParticipants]
---

# Pull Gas Bulletin Board reports

Two specifications expose the Gas Bulletin Board (GBB) reporting surface:

- `openapi/aemo-report-v1-openapi.yml` — GET-based report endpoints.
- `openapi/aemo-gasbb-reporting-public-data-openapi.yml` — the same report family exposed as POST
  with a request body, plus chart/map exports (`gasGraph`, `mapExport`,
  `pipelineChartsActualFlowAndNominationWithCapacity`,
  `productionChartsActualFlowAndNominationWithCapacity`,
  `dailyStorageActualAndForecast`). This one uses the `X-DC-DEVKEY` header.

Grep the spec for the exact `operationId` before calling — the two specs share operation names but
differ in method and body.

## Steps

1. **Establish the reference data.** `dailyFacilitiesReport` (facilities),
   `dailyReportForAllProductionAndDemandLocationsInTheBB2` (locations),
   `dailyReportWithListOfRegisteredParticipants` (participants),
   `adhocReportForRegisteredContactDetailsForEachParticipant` (contacts).
2. **Bound the window.** Most report operations take `FromGasDate` / `ToGasDate` and often
   `FacilityIds`, `FacilityTypes` or `CapacityTypes`. Always send an explicit date range — an
   unbounded pull is what trips the gateway throttle.
3. **Pull the daily series.** `dailyReportForNominationAndForecastData`,
   `dailyReportForProductionFlowAndStorage`,
   `dailyReportForProductionAndUsageAtEachConnectionPoint`,
   `adhocReportOnTheDailyProductionAndFlow`, `adhocReportOnTheDailyNominationsAndForecasts`.
4. **Pull outlooks.** `dailyReportForCapacityOutlookForTheMediumTerm`,
   `adhocReportOnTheDailyStorageOfGasAtEachStorageFacility` (short-term capacity outlook),
   `adhocReportOnUncontractedCapacityOutlookOnPipelinesAndStorageFacilities`,
   `adhocReportForLinepackCapacityAdequacy`.
5. **Pull secondary capacity.** `weeklyReportOnSecondaryPipelineCapacityAvailableForSaleOnBBPipelines`
   and `weeklyReportOnSecondaryPipelineCapacityTrades`.

## Rules

- Every operation here is a read. None of them change market state — but they are still gated by
  the APIM subscription key and, for the participant-facing variants, TLS and URM/OAuth.
- Chunk long histories into date windows rather than one wide range; `429` throttling is documented
  but no quota is published (`rate-limits/aemo-rate-limits.yml`).
- If you only need bulk public gas and electricity data and are not an onboarded participant, the
  free feeds are `https://nemweb.com.au/Reports/Current/` and
  `https://data.wa.aemo.com.au/public/`, and the WA gas bulletin board is at
  `https://gbbwa.aemo.com.au/`.
