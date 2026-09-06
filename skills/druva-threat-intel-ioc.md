---
name: druva-threat-intel-ioc
description: Manage Druva Cyber Resilience Threat Intel IOC sets — list, create, look up, update and delete indicators of compromise.
api: Druva Cyber Resilience API
generated: '2026-09-06'
method: generated
source: >-
  Grounded in openapi/druva-cyber-resilience-openapi.json. Every operationId below is present
  in the published specification.
operations:
  - ListIocSetRequest
  - CreateIOCSetRequest
  - IocSetDetailsRequest
  - GetIOCsRequest
  - IocLookupRequest
  - UpdateIocSetRequest
  - DeleteIocsRequest
  - DeleteIocSetRequest
---

# Work with Threat Intel IOC sets

Base URL `https://apis.druva.com/realize` (GovCloud: `https://govapis.druva.com/realize`).
Authenticate first — see `druva-authenticate`.

## Read first

- `ListIocSetRequest` — `GET /threatintel/v1/ioc-sets`
- `IocSetDetailsRequest` — `GET /threatintel/v1/ioc-sets/{iocsetid}`
- `GetIOCsRequest` — `GET /threatintel/v1/ioc-sets/iocs`
- `IocLookupRequest` — `GET /threatintel/v1/ioc/lookup` — check whether an indicator already
  exists in **any** set before adding it anywhere.

## Write

- `CreateIOCSetRequest` — `POST /threatintel/v1/ioc-sets`
- `UpdateIocSetRequest` — `PATCH /threatintel/v1/ioc-sets/{iocsetid}`

No idempotency key exists on this API. Run `IocLookupRequest` first rather than relying on a
retry being safe.

## Delete — irreversible

- `DeleteIocsRequest` — `DELETE /threatintel/v1/ioc-sets/{iocsetid}/iocs`
- `DeleteIocSetRequest` — `DELETE /threatintel/v1/ioc-sets/{iocsetid}`

Druva publishes **no undelete path** for either. Export the set with `IocSetDetailsRequest`
and `GetIOCsRequest` before deleting anything you might want back.

Note that these operations are not reachable through the Druva MCP server, which blocks
destructive deletes; an agent working through MCP cannot perform this step at all.

## Errors

Cyber Resilience returns the vendor envelope with product-prefixed codes — `ransomware-*`,
`RealizeUda-*`, `TIMaster-*`, `THMaster-*`, `realizecommon-*` — plus a `retryable` boolean.
Full list in `errors/druva-problem-types.yml`.
