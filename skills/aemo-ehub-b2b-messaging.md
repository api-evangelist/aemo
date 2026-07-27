---
name: Exchange B2B and B2M messages through the AEMO e-Hub
description: Send, receive and acknowledge aseXML business documents through AEMO's e-Hub, using either the asynchronous push model or the polling model.
api: openapi/aemo-b2bmessaging-async-v1-openapi.yml
operations: [submitAB2BMessage, determineWhatMessagesAreInTheEHubQueue, submitMessageAcknowledgement, deleteMessageAcknowledgement, submitMessages, submitMessageAcknowledgements, getQueueMetaData, getAlert, getAlerts, getStatusOfCoreEHubApplications]
---

# Exchange B2B and B2M messages through the AEMO e-Hub

The e-Hub carries aseXML business documents between market participants (B2B), between a
participant and AEMO's market systems (B2M), and participant-to-participant (P2P). Pick the
delivery model first — see `asyncapi/aemo-ehub-events.yml`:

- **push-push (async)** — you push to the e-Hub, the e-Hub pushes to the recipient's gateway.
  `openapi/aemo-b2bmessaging-async-v1-openapi.yml`, `openapi/aemo-b2mmessaging-async-v1-openapi.yml`.
  High volume.
- **push-pull** — you poll your Participant Hub Queue.
  `openapi/aemo-b2bmessaging-pull-v1-openapi.yml`, `openapi/aemo-b2mmessaging-pull-v1-openapi.yml`.
  Low volume.
- **sync** — request and business response on one call.
  `openapi/aemo-b2bmessaging-sync-v1-openapi.yml`, `openapi/aemo-b2mmessaging-sync-v1-openapi.yml`,
  `openapi/aemo-p2pmessaging-sync-v1-openapi.yml`.

## Steps

1. **Check the hub is healthy.** `getStatusOfCoreEHubApplications` (`GET /ping`,
   `openapi/aemo-hubmsgmgt-v1-openapi.yml`).
2. **Check for stop files before sending.** `getAlert` (v1) or `getAlerts`
   (`openapi/aemo-hubmsgmgt-v2-openapi.yml`) returns current B2B/B2M stop-file alerts. A stop file
   means message flow is halted — do not keep pushing into it.
3. **Send.** `submitAB2BMessage` (B2B) or `submitMessages` (B2M). The body is an aseXML document.
4. **Inspect your queue.** `determineWhatMessagesAreInTheEHubQueue` (B2B async) or
   `getQueueMetaData` (B2M) returns queue metadata for the initiating participant. On the pull
   APIs, poll the queue and retrieve messages.
5. **Acknowledge everything you receive.** `submitMessageAcknowledgement` (B2B) or
   `submitMessageAcknowledgements` (B2M). Every message generates an acknowledgement, with
   documented exceptions.
6. **Clean up** where the pull API supports it: `deleteMessageAcknowledgement`.

## Rules

- Carry `X-initiatingParticipantID`, `X-market`, and where the operation defines them,
  `X-transactionId` / `messageContextID`. These correlation identifiers are your only
  reconciliation mechanism — **there is no idempotency key**.
- On a timeout, inspect the queue before resending; a duplicate aseXML document is a real business
  event, not a free retry.
- `400 "The service cannot be found for the endpoint reference (EPR)"` means the routing target is
  wrong, not that the payload is malformed.
- `411` means `Content-Length` is missing; `413` means the payload exceeds the (unpublished)
  gateway ceiling.
- `500` / `503` "e-Hub is operational but downstream systems are not available" is a downstream
  outage — back off and check the alerts endpoint.
