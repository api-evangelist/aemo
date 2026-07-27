---
name: Maintain DER Register installation and NMI records
description: Create, read, update and audit distributed energy resource (DER) records against AEMO's DER Register for the NEM and the WEM.
api: openapi/aemo-der-register-installation-v2-openapi.yml
operations: [retrieveDERInstallationRecords, retrieveDERInstallationRecord, retrieveDERInstallationHistory, createDERInstallationRecord, updateDERInstallationRecord, createsANewNMIRecord, returnsTheCurrentNMIDetails, updatesANMIRecord]
---

# Maintain DER Register installation and NMI records

Two specifications back this flow:

- `openapi/aemo-der-register-installation-v2-openapi.yml` — DER installation records keyed by NMI.
- `openapi/aemo-der-register-nmi-v1-openapi.yml` — WEM DER NMI detail records.

DER Register records are a regulated obligation on network service providers and installers. Writes
change a regulated register; propose, then write on explicit approval.

## Auth

APIM subscription key (`x-apikey` / `subscription-key`) + AEMO-signed TLS certificate +
`Authorization`. The consumer/installer-facing registration API uses Azure AD B2C OpenID Connect
instead — see `well-known/aemo-derr-openid-configuration.json`.

## Steps

1. **Look up the NMI.** `retrieveDERInstallationRecord` (path parameter `{nmi}`) for the current
   installation record, or `returnsTheCurrentNMIDetails` for the WEM NMI detail record.
2. **Survey a set.** `retrieveDERInstallationRecords` lists installation records.
3. **Audit changes.** `retrieveDERInstallationHistory` (`/installation/{nmi}/history`) returns the
   change history for a NMI — use it before amending, so you know what you are overwriting.
4. **Create.** `createDERInstallationRecord` for a new installation;
   `createsANewNMIRecord` for a new WEM NMI record.
5. **Update.** `updateDERInstallationRecord` / `updatesANMIRecord` (PUT, keyed on `{nmi}`).
6. **Verify.** Re-read the record and its history after every write.

## Rules

- Always read the record and its history before an update — no idempotency key exists, and a PUT
  replaces state (`conventions/aemo-conventions.yml`).
- `404` on a NMI means no record, not an error to retry.
- `422` is a business validation failure or a URM permission gap.
- Device reference data (manufacturer, series, model, device type) is available from the DER
  consumer registration API — `listInverterManufacture`, `listInverterSeries`,
  `listInverterModels`, `listOfDeviceTypes`, `listDeviceSubType` in
  `openapi/aemo-der-consumer-registration-v1-openapi.yml`. Resolve device identifiers there before
  writing a record.
