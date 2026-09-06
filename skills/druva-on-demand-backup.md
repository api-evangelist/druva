---
name: druva-on-demand-backup
description: Trigger an on-demand Druva Enterprise Workloads backup, watch the job to completion, and cancel it if it has to be stopped.
api: Druva Enterprise Workloads API
generated: '2026-09-06'
method: generated
source: >-
  Grounded in openapi/druva-enterprise-workloads-openapi.json. Every operationId below is
  present in the published specification.
operations:
  - FSListFileServerRequest
  - FSGetBackupsetsRequest
  - FSBackupNowRequest
  - FSGetAllJobsReportRequest
  - FSGetBackupJobReportRequest
  - FSCancelJobRequest
  - SQLBackupNowRequest
  - SQLCancelJobRequest
  - BackupNowRequest
  - CancelJobRequest
  - BackupJobBackupNow
  - AllJobCancelJob
---

# Run an on-demand backup and track it

Base URL `https://apis.druva.com` (GovCloud: `https://govapis.druva.com`), product prefix
`/phoenix` is implied by the Enterprise Workloads contract. Authenticate first — see
`druva-authenticate`.

Everything here is scoped by an **organisation id** (`{orgID}`), which appears in every path.

## 1. Find what to back up

- Windows/Linux file servers: `FSListFileServerRequest` —
  `GET /fileserver/v1/orgs/{OrgID}/reports/servers`
- Backup sets for those servers: `FSGetBackupsetsRequest` —
  `GET /fileserver/v1/orgs/{OrgID}/reports/backupsets`

Responses page with `nextPageToken`; replay it as `pageToken`. A single response caps at
4,097 records.

## 2. Trigger the backup

Pick the operation for the workload you actually have — Druva ships one per workload family
and they are **not** interchangeable:

| Workload | operationId | Path |
|---|---|---|
| File Server | `FSBackupNowRequest` | `POST /fileserver/v2/orgs/{orgID}/jobs/backupNow` |
| SQL Server | `SQLBackupNowRequest` | `POST /sqlserver/v2/orgs/{orgID}/jobs/backupNow` |
| VMware | `BackupNowRequest` | `POST /vmware/v1/orgs/{orgID}/jobs/backupNow` |
| Oracle (SBT) | `BackupJobBackupNow` | `POST /oraclesbt/v1/orgs/{orgID}/jobs/backupNow` |

**Before you POST:** there is no `Idempotency-Key` on this API and no dry-run mode. A retried
`backupNow` is a second backup job, not a deduplicated one. Send it once and move to polling.

## 3. Watch the job

- All jobs: `FSGetAllJobsReportRequest` — `GET /fileserver/v1/orgs/{OrgID}/reports/jobs`
- Backup jobs only: `FSGetBackupJobReportRequest` —
  `GET /fileserver/v1/orgs/{OrgID}/reports/jobs/backups`

Equivalents exist per workload (`SQLGetBackupJobReportRequest`,
`VMwareGetAllBackupJobsInfoRequest`, `HVGetBackupJobReportRequest`,
`NASGetBackupJobReportRequest`, `AHVGetAllBackupJobsInfoRequest`,
`OracleSBTGetBackupJobReportRequest`, `PBSGetBackupJobReportRequest`).

Backup failures also surface as alerts: `ListBackupFailureAlertsRequest` —
`GET /alerts/v1/orgs/{OrgID}/alerts/jobs/backupFailures`.

## 4. Cancel if you need to

This is the reversal path, and it is the only one — a completed backup cannot be un-run:

| Workload | operationId | Path |
|---|---|---|
| File Server | `FSCancelJobRequest` | `POST /fileserver/v2/orgs/{orgID}/jobs/cancel` |
| SQL Server | `SQLCancelJobRequest` | `POST /sqlserver/v2/orgs/{orgID}/jobs/cancel` |
| VMware | `CancelJobRequest` | `POST /vmware/v1/orgs/{orgID}/jobs/cancel` |
| Oracle | `AllJobCancelJob` | `POST /oraclesbt/v1/orgs/{orgID}/jobs/cancel` |

Druva does **not** publish a window inside which cancel still works. Treat cancellation as
best-effort and confirm from the job report rather than from the cancel response.

## Error handling

Vendor envelope `{code, message, data, retryable}`. Retry only when `retryable` is true.
403 can mean an expired token, the wrong Druva cloud, or a missing Cloud Administrator role —
re-authenticate once before concluding it is permissions.
