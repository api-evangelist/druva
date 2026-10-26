# Druva (druva)

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

Druva is a cloud data protection and management company running the Druva Resilience Cloud, a fully managed SaaS platform for backup, disaster recovery, cyber resilience and data governance across endpoints, data centres, AWS and Azure workloads, and SaaS applications including Microsoft 365, Google Workspace, Salesforce, Dynamics 365, Entra ID and Okta. Druva publishes 19 first-party OpenAPI and Swagger definitions covering roughly 970 operations from its developer portal, advertised in an RFC 9727 API catalog document, spanning Endpoints and Data Governance, Enterprise Workloads, Cyber Resilience, AWS Native Workloads and CloudRanger, MSP tenant management, Platform administration and job management - each with a separate GovCloud contract where one exists. Authentication is OAuth 2.0 client credentials against a per-cloud token endpoint, and Druva also runs a first-party hosted MCP server at mcp.druva.com for AI agents.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/druva/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/druva/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Producing

## Tags

- Backup
- Cyber Resilience
- Data Protection
- Disaster Recovery
- SaaS Backup
- Ransomware Recovery
- Data Governance
- Enterprise Workloads
- MSP
- Legal Hold
- Endpoints
- GovCloud
- MCP

## Timestamps

- **Created:** 2026-03-27
- **Modified:** 2026-09-06

## APIs

### Druva Authentication API

Token endpoint for the Druva Cloud Platform. Exchanges a base64-encoded Client ID and Secret Key for an OAuth 2.0 client-credentials bearer token used by every other Druva product API on the public cloud.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com`
- **Operations:** 1

#### Tags

- Authentication
- OAuth
- Token

#### Properties

- [OpenAPI](openapi/druva-authentication-openapi.json)
- [Documentation](https://developer.druva.com/reference)
- [Authentication](https://developer.druva.com/docs/authentication)

### Druva MSP Authentication API

Token endpoint for the Druva Managed Service Provider surface. MSP integrations authenticate here rather than at the common Druva token endpoint.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/msp`
- **Operations:** 1

#### Tags

- Authentication
- MSP
- OAuth

#### Properties

- [OpenAPI](openapi/druva-msp-authentication-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva GovCloud Authentication API

Token endpoint for Druva Endpoints and Data Governance GovCloud. Tokens minted here are valid for 15 minutes and cannot be used against any other Druva cloud.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govcloudapis.druva.com`
- **Operations:** 2

#### Tags

- Authentication
- GovCloud
- OAuth

#### Properties

- [OpenAPI](openapi/druva-govcloud-authentication-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Hybrid Workloads GovCloud Authentication API

Token endpoint for Druva Hybrid / Enterprise Workloads GovCloud. Separate from the Endpoints GovCloud token endpoint; tokens are not interchangeable between Druva clouds.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govapis.druva.com`
- **Operations:** 1

#### Tags

- Authentication
- GovCloud
- OAuth

#### Properties

- [OpenAPI](openapi/druva-hybrid-workload-govcloud-authentication-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Endpoints and Data Governance API

The inSync Cloud API for Druva Endpoints and Data Governance. Covers device and user management, backup and restore of endpoint data, profiles, AD/LDAP synchronisation, federated search, legal hold, sensitive data governance, audit trail and the Events API used to export inSync events to a SIEM in JSON, CEF or Syslog form.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/insync`
- **Operations:** 63

#### Tags

- Endpoints
- Data Governance
- Legal Hold
- Event
- Sensitive Data Governance
- Backup

#### Properties

- [OpenAPI](openapi/druva-insync-cloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Endpoints and Data Governance GovCloud API

The inSync GovCloud API - the FedRAMP-boundary equivalent of the Endpoints and Data Governance surface, served from govcloudapis.druva.com with its own token endpoint and a 15-minute access token.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govcloudapis.druva.com/insync`
- **Operations:** 53

#### Tags

- Endpoints
- Data Governance
- GovCloud
- Legal Hold
- Event

#### Properties

- [OpenAPI](openapi/druva-insync-govcloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Enterprise Workloads API

The Phoenix API for Druva Enterprise Workloads. Job management, on-demand backup, restore to original or alternate location, snapshots, backup policies and reporting across File Server, NAS, VMware, Hyper-V, Nutanix AHV, SQL Server, Oracle SBT, Azure, PBS and DRaaS workloads, plus alerts, audit trail and cloud cache.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/phoenix`
- **Operations:** 94

#### Tags

- Enterprise Workloads
- Backup
- Restore
- VMware
- SQL Server
- Jobs

#### Properties

- [OpenAPI](openapi/druva-enterprise-workloads-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Enterprise Workloads GovCloud API

The Enterprise Workloads API inside the Druva GovCloud boundary, served from govapis.druva.com. Same workload coverage as the public-cloud contract with the Azure family omitted.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govapis.druva.com/phoenix`
- **Operations:** 91

#### Tags

- Enterprise Workloads
- GovCloud
- Backup
- Restore
- Jobs

#### Properties

- [OpenAPI](openapi/druva-enterprise-workloads-govcloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Cyber Resilience API

The Realize API for Druva Cyber Resilience. Accelerated Ransomware Recovery quarantine ranges and snapshots, curated snapshot jobs, threat hunting, threat intel IOC sets and lookup, threat watch, unusual data activity anomaly detection, restore scans and the Realize event stream.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/realize`
- **Operations:** 62

#### Tags

- Cyber Resilience
- Ransomware Recovery
- Threat Hunting
- Threat Intel
- Curated Snapshots
- Event

#### Properties

- [OpenAPI](openapi/druva-cyber-resilience-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Cyber Resilience GovCloud API

The Cyber Resilience surface inside the Druva GovCloud boundary. Ransomware recovery, curated snapshots, threat hunting, threat intel, data anomalies and restore scans, served from govapis.druva.com/realize.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govapis.druva.com/realize`
- **Operations:** 50

#### Tags

- Cyber Resilience
- GovCloud
- Ransomware Recovery
- Threat Hunting
- Threat Intel

#### Properties

- [OpenAPI](openapi/druva-cyber-resilience-govcloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva GovCloud Cyber Resilience Authorization API

Authorization endpoints for the Druva GovCloud Cyber Resilience surface, published as a separate contract from the Cyber Resilience API itself.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govapis.druva.com`
- **Operations:** 2

#### Tags

- Authentication
- GovCloud
- Cyber Resilience

#### Properties

- [OpenAPI](openapi/druva-cyber-resilience-govcloud-authorization-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva CloudRanger Native Workloads API

The CloudRanger API for Druva Native Workloads on AWS. Backup, disaster recovery and lifecycle management for EC2, EBS, RDS, Redshift, DynamoDB, S3 buckets and auto-scaling groups, with policies, schedules, DR plans and file-level restore. Served from api.cloudranger.com, the domain Druva acquired with CloudRanger in 2018 and still documents as the Native Workloads base URL.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://api.cloudranger.com/202004`
- **Operations:** 223

#### Tags

- CloudRanger
- AWS
- Native Workloads
- Backup
- Disaster Recovery

#### Properties

- [OpenAPI](openapi/druva-cloudranger-openapi.json)
- [Documentation](https://developer.druva.com/reference)
- [GettingStarted](https://developer.druva.com/docs/getting-started-with-cloudranger-api-trial)

### Druva AWS Native Workloads API

The AWS Native Workloads API served from the common Druva gateway at apis.druva.com/awsnative. The CloudRanger capability set - accounts, backups, restores, policies, schedules, environments and DR plans - reached through Druva Cloud Platform credentials rather than CloudRanger keys.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/awsnative`
- **Operations:** 191

#### Tags

- AWS
- Native Workloads
- Backup
- Disaster Recovery

#### Properties

- [OpenAPI](openapi/druva-aws-native-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva MSP API

The Managed Service Provider API. Customer and tenant provisioning, suspension and patching, per-customer API token generation, asynchronous task tracking, quota configuration and consumption metering, customer events, and the chargeback, telemetry and service-monitoring report family used to bill managed customers.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/msp`
- **Operations:** 103

#### Tags

- MSP
- Managed Service Providers
- Multi-Tenant
- Reports
- Quota

#### Properties

- [OpenAPI](openapi/druva-msp-openapi.json)
- [Documentation](https://developer.druva.com/reference)
- [GettingStarted](https://developer.druva.com/docs/getting-started-with-druva-msp-api-1)

### Druva Platform API

The Druva Cloud Platform administration API. Administrators, administrator roles, platform-level reports and the platform event stream shared across Druva products.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/platform`
- **Operations:** 12

#### Tags

- Platform
- Administration
- Reports
- Event

#### Properties

- [OpenAPI](openapi/druva-platform-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Microsoft 365 API

App management and restore operations for Druva-protected Microsoft 365 data - OneDrive and Exchange Online restores, and SharePoint Online restores.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com`
- **Operations:** 8

#### Tags

- Microsoft 365
- SaaS Backup
- Restore
- SharePoint

#### Properties

- [OpenAPI](openapi/druva-microsoft-365-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Google Workspace API

App management for Druva-protected Google Workspace data.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com`
- **Operations:** 1

#### Tags

- Google Workspace
- SaaS Backup

#### Properties

- [OpenAPI](openapi/druva-google-workspace-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Job Management API for Cloud Workloads

The Unity job-management surface for cloud workloads - create and cancel backup and restore jobs for Azure SQL and NAS from a single contract.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/unity`
- **Operations:** 8

#### Tags

- Jobs
- Azure SQL
- NAS
- Backup

#### Properties

- [OpenAPI](openapi/druva-job-management-cloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Job Management API for GovCloud Workloads

The Unity job-management surface inside the Druva GovCloud boundary, covering NAS backup and restore jobs.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://govapis.druva.com/unity`
- **Operations:** 4

#### Tags

- Jobs
- GovCloud
- NAS
- Backup

#### Properties

- [OpenAPI](openapi/druva-job-management-govcloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva Legal Hold Targeted Download API

Legal hold and targeted download operations for legal and compliance teams preserving and extracting data from devices under hold. Druva publishes these operations inside the Endpoints and Data Governance (inSync) contract under the Legal Hold tag rather than as a standalone specification.

- **Human URL:** [https://developer.druva.com](https://developer.druva.com)
- **Base URL:** `https://apis.druva.com/insync`
- **Operations:** 63

#### Tags

- Legal Hold
- Compliance
- eDiscovery

#### Properties

- [OpenAPI](openapi/druva-insync-cloud-openapi.json)
- [Documentation](https://developer.druva.com/reference)

### Druva MCP Server

Druva's first-party hosted Model Context Protocol server. MCP-compatible AI clients connect to a single global endpoint over streamable HTTP, authenticate with 3-legged OAuth 2.1 and PKCE, and reach the Druva Resilience Cloud through five tools that discover and execute cloud-delivered skills across endpoint health, SaaS apps, cyber resilience and data governance. Destructive deletes are blocked server-side and every call is bounded by the caller's Druva RBAC.

- **Human URL:** [https://help.druva.com/en/articles/15654265-getting-started-with-the-druva-mcp-server](https://help.druva.com/en/articles/15654265-getting-started-with-the-druva-mcp-server)
- **Base URL:** `https://mcp.druva.com/mcp`

#### Tags

- MCP
- Agents
- AI
- Cyber Resilience

#### Properties

- [MCPServer](mcp/druva-mcp.yml)
- [ToolCrosswalk](mcp/druva-tool-crosswalk.yml)
- [Documentation](https://help.druva.com/en/articles/15654265-getting-started-with-the-druva-mcp-server)

## Repository artifacts

- **OAuthScopes** — [scopes/druva-scopes.yml](scopes/druva-scopes.yml)
- **AgenticAccess** — [agentic-access/druva-agentic-access.yml](agentic-access/druva-agentic-access.yml)
- **TrustCenter** — [security/druva-trust-center.yml](security/druva-trust-center.yml)
- **DomainSecurity** — [security/druva-domain-security.yml](security/druva-domain-security.yml)
- **Authentication** — [authentication/druva-authentication.yml](authentication/druva-authentication.yml)
- **WellKnown** — [well-known/druva-well-known.yml](well-known/druva-well-known.yml)
- **APICatalog** — [well-known/druva-api-catalog.json](well-known/druva-api-catalog.json)
- **MCPServer** — [mcp/druva-mcp.yml](mcp/druva-mcp.yml)
- **ToolCrosswalk** — [mcp/druva-tool-crosswalk.yml](mcp/druva-tool-crosswalk.yml)
- **Packages** — [packages/druva-packages.yml](packages/druva-packages.yml)
- **LLMsTxt** — [llms/druva-llms.txt](llms/druva-llms.txt)
- **Conformance** — [conformance/druva-conformance.yml](conformance/druva-conformance.yml)
- **Compliance** — [security/druva-trust-center.yml](security/druva-trust-center.yml)
- **ErrorCatalog** — [errors/druva-problem-types.yml](errors/druva-problem-types.yml)
- **Lifecycle** — [lifecycle/druva-lifecycle.yml](lifecycle/druva-lifecycle.yml)
- **ChangeLog** — [changelog/druva-changelog.yml](changelog/druva-changelog.yml)
- **Conventions** — [conventions/druva-conventions.yml](conventions/druva-conventions.yml)
- **DataModel** — [data-model/druva-data-model.yml](data-model/druva-data-model.yml)
- **Plans** — [plans/druva-plans-pricing.yml](plans/druva-plans-pricing.yml)
- **RateLimits** — [rate-limits/druva-rate-limits.yml](rate-limits/druva-rate-limits.yml)
- **AgentSkill** — [skills/_index.yml](skills/_index.yml)
- **FinOps** — [finops/druva-finops.yml](finops/druva-finops.yml)
- **Overlay** — [overlays/druva-aws-native-overlay.yaml](overlays/druva-aws-native-overlay.yaml)
- **Overlay** — [overlays/druva-cloudranger-overlay.yaml](overlays/druva-cloudranger-overlay.yaml)
- **Overlay** — [overlays/druva-cyber-resilience-govcloud-overlay.yaml](overlays/druva-cyber-resilience-govcloud-overlay.yaml)
- **Overlay** — [overlays/druva-cyber-resilience-overlay.yaml](overlays/druva-cyber-resilience-overlay.yaml)
- **Overlay** — [overlays/druva-insync-cloud-overlay.yaml](overlays/druva-insync-cloud-overlay.yaml)
- **Overlay** — [overlays/druva-insync-govcloud-overlay.yaml](overlays/druva-insync-govcloud-overlay.yaml)
- **Overlay** — [overlays/druva-microsoft-365-overlay.yaml](overlays/druva-microsoft-365-overlay.yaml)
- **SDKs** — [packages/druva-packages.yml](packages/druva-packages.yml)

## Links

- **LinkedIn** — [https://www.linkedin.com/company/druva](https://www.linkedin.com/company/druva)
- **Website** — [https://www.druva.com](https://www.druva.com)
- **Documentation** — [https://docs.druva.com/](https://docs.druva.com/)
- **DeveloperPortal** — [https://developer.druva.com](https://developer.druva.com)
- **APIReference** — [https://developer.druva.com/reference](https://developer.druva.com/reference)
- **Support** — [https://support.druva.com](https://support.druva.com)
- **GitHub** — [https://github.com/druvainc](https://github.com/druvainc)
- **Integrations** — [https://www.druva.com/partners/ecosystem/technology-alliance-program](https://www.druva.com/partners/ecosystem/technology-alliance-program)
- **LlmsText** — [https://developer.druva.com/llms.txt](https://developer.druva.com/llms.txt)
- **Blog** — [https://www.druva.com/blog](https://www.druva.com/blog)
- **StatusPage** — [https://support.druva.com/s/druvacloudstatus](https://support.druva.com/s/druvacloudstatus)
- **Deprecation** — [https://developer.druva.com/docs/migration-process](https://developer.druva.com/docs/migration-process)
- **Pricing** — [https://www.druva.com/pricing](https://www.druva.com/pricing)
- **SignUp** — [https://login.druva.com/](https://login.druva.com/)
- **TermsOfService** — [https://www.druva.com/terms-of-use](https://www.druva.com/terms-of-use)
- **PrivacyPolicy** — [https://www.druva.com/privacy-policy](https://www.druva.com/privacy-policy)
- **GettingStarted** — [https://developer.druva.com/docs/introduction](https://developer.druva.com/docs/introduction)
- **GitHubOrganization** — [https://github.com/druvainc](https://github.com/druvainc)
- **Console** — [https://login.druva.com/](https://login.druva.com/)

## Not published by Druva

Kept here so absence reads as deliberate rather than unchecked:

- **No agent card.** `/.well-known/agent-card.json` and `/.well-known/agent.json` were probed on
  every Druva host and returned 404, or a soft-404 HTML shell. Nothing was authored on Druva's
  behalf — an agent card asserts that the provider serves the document, so deriving one would be
  a false claim.
- **No idempotency.** No `Idempotency-Key` header, parameter, or replay-safety statement exists in
  any of the 19 published specifications or in the developer documentation.
- **No published rate limits** and no rate-limit response headers. `429` is declared on 2 of 970
  operations with no `Retry-After`.
- **No published prices.** Every Druva pricing tier page renders a `$` placeholder and a
  contact-sales path. `plans/druva-plans-pricing.yml` records that as `plan_count: 0`.
- **No AsyncAPI, webhooks or event push.** The Events API is polled, not pushed.
- **No RFC 9457 problem+json**, no gRPC `.proto`, no SOAP WSDL, no GraphQL.
- **No first-party SDK in any package registry.** The official Python SDK installs from a git
  subdirectory; the Go helper library was last released in 2023.

### A correction to this profile, 2026-09-06

An earlier round of this profile stored an API Evangelist–authored *model* of the Druva API in
`openapi/_original/` — the directory reserved for verbatim provider harvests — where it was
credited to Druva. That file said so in its own description ("Best-effort OpenAPI…") and carried
an API Evangelist contact address. It has been moved to `openapi/_scaffold/`, stamped, and
excluded from the record; the eight per-tag splits and the Postman/OpenCollection files derived
from it went with it, to `collections/_scaffold/`.

It is superseded by Druva's own contracts: **19 first-party OpenAPI and Swagger definitions,
roughly 970 operations**, downloaded from `https://developer.druva.com/openapi/<name>.json` and
enumerated by Druva's own RFC 9727 catalog at
`https://developer.druva.com/.well-known/api-catalog`.
