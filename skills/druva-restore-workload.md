---
name: druva-restore-workload
description: Restore a Druva-protected workload from a snapshot to its original or an alternate location, and track the restore job.
api: Druva Enterprise Workloads API
generated: '2026-09-06'
method: generated
source: >-
  Grounded in openapi/druva-enterprise-workloads-openapi.json. Every operationId below is
  present in the published specification.
operations:
  - FSGetBackupsetsRequest
  - FSGetSnapshotsRequest
  - FSOriginalRestoreRequest
  - FSAlternateRestoreRequest
  - FSGetRestoreJobReportRequest
  - FSCancelJobRequest
  - SQLGetBackupsetDetailsRequest
  - SQLListSnapshotRequest
  - SQLRestoreToOriginalInstanceRequest
  - SQLRestoreToAlternateInstanceRequest
  - SQLGetRestoreJobReportRequest
  - GetSnapshotRequest
  - RestoreOriginalRequest
  - VMwareGetAllRestoreJobsInfoRequest
  - OracleDTCGetSnapshotsRequest
  - OracleDTCRestoreOriginalRequest
---

# Restore a workload from a Druva snapshot

Authenticate first (`druva-authenticate`). Base URL `https://apis.druva.com`, or
`https://govapis.druva.com` for GovCloud. Everything is `{orgID}`-scoped.

A restore is the highest-consequence write on this API: it overwrites live data at the
target. Druva publishes no dry-run mode and no idempotency key, so the safety has to come
from choosing the right snapshot and the right target before you POST.

## 1. Find the backup set

`FSGetBackupsetsRequest` — `GET /fileserver/v1/orgs/{OrgID}/reports/backupsets`
(SQL: `SQLGetBackupsetsRequest`; VMware: `VMwareGetBackupsetsRequest`;
NAS: `NASGetBackupsetsRequest`; Hyper-V: `HVGetBackupSetReportRequest`).

## 2. List its snapshots and pick one

| Workload | operationId | Path |
|---|---|---|
| File Server | `FSGetSnapshotsRequest` | `GET /fileserver/v2/orgs/{orgID}/backupsets/{backupsetID}/snapshots` |
| SQL Server | `SQLListSnapshotRequest` | `GET /sqlserver/v2/orgs/{orgID}/backupsets/{backupsetID}/snapshots` |
| VMware | `GetSnapshotRequest` | `GET /vmware/v1/orgs/{orgID}/backupsets/{backupsetID}/snapshots` |
| Oracle | `OracleDTCGetSnapshotsRequest` | `GET /oraclesbt/v1/orgs/{orgID}/backupsets/{backupsetID}/snapshots` |

For SQL, `SQLGetBackupsetDetailsRequest` (`GET /sqlserver/v2/orgs/{orgID}/backupsets/{backupsetID}`)
gives the instance and database detail you need to build a valid restore request.

## 3. Choose original vs alternate — this is the irreversible decision

**Original location** overwrites the source. **Alternate location** writes somewhere else and
leaves the source untouched. If you are acting on a human's behalf and the instruction is
ambiguous, restore to an alternate location and report back.

| Workload | Original | Alternate |
|---|---|---|
| File Server | `FSOriginalRestoreRequest` — `POST /fileserver/v2/orgs/{orgID}/jobs/restores/originalServer` | `FSAlternateRestoreRequest` — `POST /fileserver/v2/orgs/{orgID}/jobs/restores/alternateServer` |
| SQL Server | `SQLRestoreToOriginalInstanceRequest` — `POST /sqlserver/v2/orgs/{orgID}/jobs/restores/original` | `SQLRestoreToAlternateInstanceRequest` — `POST /sqlserver/v2/orgs/{orgID}/jobs/restores/alternate` |
| VMware | `RestoreOriginalRequest` — `POST /vmware/v1/orgs/{orgID}/jobs/restores/original` | not published |
| Oracle | `OracleDTCRestoreOriginalRequest` — `POST /oraclesbt/v1/orgs/{orgID}/jobs/restores/original` | not published |

## 4. Track the restore

`FSGetRestoreJobReportRequest` — `GET /fileserver/v1/orgs/{OrgID}/reports/jobs/restores`
(`SQLGetRestoreJobReportRequest`, `VMwareGetAllRestoreJobsInfoRequest`,
`NASGetRestoreJobReportRequest`, `HVGetRestoreJobReportRequest`,
`AHVGetAllRestoreJobsInfoRequest`, `OracleSBTGetRestoreJobReportRequest`,
`PBSGetRestoreJobReportRequest` for the other workloads).

## 5. If it has to stop

Cancel with the same per-workload cancel operation used for backups — `FSCancelJobRequest`,
`SQLCancelJobRequest`, `CancelJobRequest`, `AllJobCancelJob`. Druva states no window inside
which cancel is guaranteed, and **data already written to the target is not rolled back**.
Cancelling a restore is not an undo.
