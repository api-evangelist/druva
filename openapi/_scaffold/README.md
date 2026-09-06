# Quarantined scaffold — NOT published by Druva

Everything in this directory was **written by API Evangelist**, not harvested from Druva.

`druva-openapi.yml` says so in its own `info.description` ("Best-effort OpenAPI for Druva's
cloud data protection REST API") and carries `info.contact.email: kin@apievangelist.com`. It was
previously stored in `openapi/_original/`, which the indexer treats as the verbatim provider
harvest — so an API Evangelist model of ~11 operations was being credited to Druva at full
first-party weight. The eight `druva-*-api-openapi.yml` files are per-tag splits of that same
scaffold.

**Superseded 2026-09-06.** Druva publishes 19 real OpenAPI/Swagger definitions (970 operations)
from its own developer portal, advertised in its own RFC 9727 API catalog:

- `https://developer.druva.com/.well-known/api-catalog` (HTTP 200)
- `https://developer.druva.com/openapi/<filename>.json` (HTTP 200 each)

Those are now in `openapi/_original/` (verbatim) and `openapi/` (working copies), and `apis.yml`
points at them. Nothing in this directory is wired into `apis.yml` any more. It is kept, not
deleted, because the audit trail is the point.

`../../collections/_scaffold/` holds the Postman / OpenCollection files that were derived from
these scaffold specs; they describe the same non-existent operations.
