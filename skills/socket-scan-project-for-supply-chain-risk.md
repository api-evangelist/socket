---
name: Scan a project for supply chain risk
description: Upload a project's manifest files to Socket, create a full scan, and read back
  the resulting supply-chain and vulnerability alerts.
api: openapi/socket-openapi-original.json
operations:
- getSupportedFiles
- CreateOrgFullScan
- getOrgFullScan
- getOrgFullScanMetadata
- alertsList
---

# Scan a project for supply chain risk

Use this to produce a full SBOM scan of a codebase and review its Socket alerts.

## Auth
Send `Authorization: Bearer <ORG_API_TOKEN>`. The token needs the `full-scans:create`,
`full-scans:list`, and `alerts:list` scopes. All calls are under `https://api.socket.dev/v0`
and are metered against your organization quota.

## Steps
1. `getSupportedFiles` — GET `/orgs/{org_slug}/supported-files` to confirm which manifest
   filenames (package.json, package-lock.json, requirements.txt, go.mod, …) can be uploaded.
2. `CreateOrgFullScan` — POST `/orgs/{org_slug}/full-scans` with the manifest files as a
   multipart upload. Up to 10000 files, 268 MB each. Returns the full scan with SBOM artifacts.
3. `getOrgFullScanMetadata` — GET `/orgs/{org_slug}/full-scans/{full_scan_id}/metadata` to
   check status/summary counts.
4. `getOrgFullScan` — GET `/orgs/{org_slug}/full-scans/{full_scan_id}` to stream all SBOM
   artifacts. Results are stale-while-revalidate; re-poll if analysis is still running.
5. `alertsList` — GET `/orgs/{org_slug}/alerts` to list the latest alerts, paginating with
   `endCursor`/`startAfterCursor` until `endCursor` is null (an empty `items` page is NOT the
   end — only a null cursor is).

## Rules
- Errors use `{ "error": { "message": ..., "details": ... } }`; a 403 means a missing token
  scope, a 429 means quota exhausted (check GET `/quota`).
- There is no idempotency-key header; do not blind-retry a create on timeout — re-list first.
