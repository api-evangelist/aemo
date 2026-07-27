---
name: Manage AEMO-signed TLS client certificates
description: Self-manage the AEMO-signed TLS certificates a participant needs to connect to the e-Hub — list, download, generate, reissue, renew and revoke.
api: openapi/aemo-tls-certificate-mgmt-v1-openapi.yml
operations: [getTheScopeForAUser, getAllCertificateOrders, getDetailsOnACertificateOrder, createANewCertificate, downloadACertificate, reissueACertificate, renewACertificate, revokeACertificate]
---

# Manage AEMO-signed TLS client certificates

Every authenticated AEMO e-Hub API call presents an AEMO-signed TLS client certificate. The TLS
Certificate Management API (`openapi/aemo-tls-certificate-mgmt-v1-openapi.yml`) lets a participant
manage that certificate estate itself instead of raising a ticket. This API uses its own key header,
`x-aemo-api-key`.

## Steps

1. **Check what you may do.** `getTheScopeForAUser` (`GET /scope`) returns the caller's scope.
2. **Inventory.** `getAllCertificateOrders` (`GET /orders`) lists orders;
   `getDetailsOnACertificateOrder` (`GET /orders/{order-id}`) drills into one.
3. **Generate.** `createANewCertificate` (`POST /certificates`).
4. **Download.** `downloadACertificate` (`GET /certificates/{certificate-id}/download`). Treat the
   downloaded material as a secret — never log it, never echo it into a transcript.
5. **Renew before expiry.** `renewACertificate` (`POST /orders/{order-id}/renewal`). Monitor expiry
   proactively; an expired client certificate takes every e-Hub integration offline at once.
6. **Reissue** when a certificate must be replaced without a full re-order:
   `reissueACertificate` (`POST /orders/{order-id}/reissue`).
7. **Revoke** on compromise: `revokeACertificate` (`POST /certificates/{certificate-id}/revoke`).

## Rules

- **Revocation is destructive and immediate** — it will break live integrations. Require explicit
  human confirmation naming the certificate ID.
- Never write certificate material or private keys into logs, tool output or memory.
- If a certificate is suspected compromised, revoke first, then generate and deploy a replacement,
  then notify AEMO's Cyber Security Team at `cybersecurity@aemo.com.au`
  (`security/aemo-vulnerability-disclosure.yml`).
- This API's documentation is explicitly marked as an evolving design; re-read the spec before
  relying on a field.
