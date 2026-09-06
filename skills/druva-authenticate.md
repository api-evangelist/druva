---
name: druva-authenticate
description: Exchange Druva API credentials for a bearer access token on the correct Druva cloud, and refresh before it expires.
api: Druva Authentication API
generated: '2026-09-06'
method: generated
source: >-
  Grounded in openapi/druva-authentication-openapi.json and
  https://developer.druva.com/docs/authentication. Every operationId below is present in the
  published specification.
operations:
  - reference-getting-started
---

# Authenticate against a Druva cloud

Every Druva product API — Endpoints and Data Governance, Enterprise Workloads, Cyber
Resilience, MSP, Platform — is behind the same OAuth 2.0 client-credentials exchange. Get
this wrong and every call returns 403 with `User is not authorized to access this resource
with an explicit deny`.

## 1. Pick the right cloud

A token minted on one cloud **cannot** call another. Choose the base URL first:

| Scope | Base URL |
|---|---|
| Enterprise Workloads, Endpoints and Data Governance, Cyber Resilience, MSP, Platform | `https://apis.druva.com` |
| Endpoints and Data Governance GovCloud | `https://govcloudapis.druva.com` |
| Enterprise Workloads / Cyber Resilience GovCloud | `https://govapis.druva.com` |
| Native Workloads (CloudRanger) | `https://api.cloudranger.com/202004` — different scheme, see step 5 |

## 2. Get credentials

A Cloud Administrator creates a Client ID and Secret Key in the Druva Cloud Platform Console
(<https://login.druva.com/>). A read-only integration should be issued the **Cloud Admin Read
Only** role rather than full Cloud Administrator.

## 3. Exchange them (`reference-getting-started`)

Base64-encode `<Client ID>:<Secret Key>` and send it as HTTP Basic:

```
POST https://apis.druva.com/token
Authorization: Basic <base64(client_id:secret_key)>
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&scope=read
```

`200` returns `{"access_token": "...", "token_type": "bearer", "expires_in": 1800}`.

## 4. Use and refresh it

Send `Authorization: Bearer <access_token>` on every subsequent call.

Token lifetime is fixed and **cannot be extended**:

- 30 minutes — public cloud, and Hybrid Workloads GovCloud
- 15 minutes — Endpoints and Data Governance GovCloud

Refresh on a timer rather than on failure. Druva returns **403**, not 401, for an expired
token, so treat 401 and 403 as the same refresh trigger and only escalate to a permissions
problem after a fresh token also fails.

## 5. Native Workloads is different

CloudRanger uses a two-header scheme: `x-api-key` from the CloudRanger user-settings page,
exchanged at `GET https://api.cloudranger.com/202004/authorize` for a bearer token. Both
headers then go on every call.

## Rules that apply to whatever you call next

- There is **no idempotency mechanism** anywhere in the Druva API estate. Do not blind-retry
  a POST; read `conventions/druva-conventions.yml` before writing anything.
- Errors are a vendor envelope — `{code, message, data, retryable}`. Honour `retryable`.
- No rate limits are published and no rate-limit headers are returned. Pace yourself.
