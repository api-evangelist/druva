---
name: druva-msp-provision-tenant
description: Provision a Druva MSP customer and tenant, poll the async task to completion, and suspend or unsuspend an existing tenant.
api: Druva MSP API
generated: '2026-09-06'
method: generated
source: >-
  Grounded in openapi/druva-msp-openapi.json and
  https://developer.druva.com/docs/getting-started-with-druva-msp-api-1. Every operationId
  below is present in the published specification.
operations:
  - GetCustomersV3
  - CreateCustomerV3
  - GetCustomerV3
  - UpdateCustomerV3ForDoc
  - CreateTenantV3
  - GetTenantsV3
  - GetTenantV3
  - PatchTenant
  - SuspendTenant
  - UnsuspendTenant
  - GetTask
  - GetCustomerEvents
---

# Provision an MSP customer and tenant

The MSP surface has its own token endpoint: `POST https://apis.druva.com/msp/auth/v1/token`.
Authenticate there, not at `/token`, then send `Authorization: Bearer <token>`.

Every write in this section is **asynchronous and non-idempotent**. Each one returns a
`taskID` and no idempotency key exists, so a retried create is a second customer or a second
tenant. Send once, then poll.

## 1. Check whether the customer already exists

`GetCustomersV3` — `GET /msp/v3/customers`. Page with `pageToken`.

This is your only defence against duplicate creation. Do it before every create.

## 2. Create the customer

`CreateCustomerV3` — `POST /msp/v3/customers`

Druva documents the constraints tightly: only `licenseManagedAllowed` and
`dataAccessAllowed` are supported attributes, any other attribute is an error, and
`dataAccessAllowed` accepts only `1` (Managed). With no attributes you get an MSC Provisioned
managed customer by default.

## 3. Poll the task

`GetTask` — `GET /msp/v2/tasks/{taskID}`

Do not proceed to the tenant until the customer task reports success. `GetCustomerV3`
(`GET /msp/v3/customers/{customerID}`) confirms the result.

## 4. Create the tenant

`CreateTenantV3` — `POST /msp/v3/customers/{customerID}/tenants`, then poll `GetTask` again.

Constraints Druva publishes, all of which cause a failed task rather than a validation error
if you get them wrong:

- Sandbox tenants **cannot** be created through this API.
- Enterprise Workloads licences run eight years; SaaS Apps and Endpoints licences three.
- Storage regions can be added but never removed.
- Business edition supports exactly one storage region, and AWS and Azure regions must be in
  the same geography.
- At least one AWS storage region is required for Enterprise Workloads.
- Endpoints, D365 and Okta do not support Business edition.
- Premium Security is Enterprise Workloads only, and requires both Security Posture &
  Observability and Accelerated Ransomware Recovery to be enabled on the same tenant.

Valid products and attribute values:
<https://developer.druva.com/docs/msp-product-and-attribute-values>

## 5. Amend rather than recreate

`PatchTenant` — `PATCH /msp/v3/customers/{customerID}/tenants/{tenantID}`.
`isEnabled` is required whenever tenant features are specified, and a feature toggled in the
service plan cannot be overridden here. `UpdateCustomerV3ForDoc` updates the customer, and
requires every non-updated field to be resent with its existing value.

## 6. Suspend and unsuspend — the reversible pair

- `SuspendTenant` — `POST /msp/v2/customers/{customerID}/tenants/{tenantID}/suspend`
- `UnsuspendTenant` — `POST /msp/v2/customers/{customerID}/tenants/{tenantID}/unsuspend`

Both are asynchronous and return a `taskID`. A suspended tenant's console is inaccessible.
Druva publishes **no window** after which unsuspend stops working, so do not assume one —
confirm state with `GetTenantV3` rather than inferring it.

## 7. Audit what happened

`GetCustomerEvents` — `GET /msp/v3/customers/{customerID}/events`.
