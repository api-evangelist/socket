---
name: Export an SBOM and fetch fixes
description: Export a Socket scan as a CycloneDX / SPDX / OpenVEX SBOM and fetch available
  dependency upgrades that resolve its vulnerabilities.
api: openapi/socket-openapi-original.json
operations:
- exportCDX
- exportSPDX
- exportOpenVEX
- fetch-fixes
---

# Export an SBOM and fetch fixes

Use this to hand a scan's SBOM to downstream tooling and to compute remediation upgrades.

## Auth
`Authorization: Bearer <ORG_API_TOKEN>` with `report:read` (exports) and `fixes:list`
(fixes). Base URL `https://api.socket.dev/v0`.

## Steps
1. Export the SBOM in the format you need (each takes the scan/report `id`):
   - `exportCDX` — GET `/orgs/{org_slug}/export/cdx/{id}` (CycloneDX)
   - `exportSPDX` — GET `/orgs/{org_slug}/export/spdx/{id}` (SPDX)
   - `exportOpenVEX` — GET `/orgs/{org_slug}/export/openvex/{id}` (OpenVEX v0.2.0, carries
     reachability-based exploitability: not_affected / affected / under_investigation).
   Supported ecosystems: crates, go, maven, npm, nuget, pypi, rubygems.
2. `fetch-fixes` — GET `/orgs/{org_slug}/fixes` with exactly one of `repo_slug`,
   `full_scan_id`, or `tar_hash`, plus `vulnerability_ids` (comma-separated GHSA/CVE IDs, or
   `*` for all). The response's `fixDetails` maps each vulnerability to a
   `fixFound` / `partialFixFound` / `noFixAvailable` / `fixNotApplicable` variant with the
   `purl` and `fixedVersion` to upgrade to.

## Rules
- When several vulnerabilities share a package, their fix entries carry the same
  `fixedVersion`; apply per package without reconciling.
- Errors use `{ "error": { "message", "details" } }`; 429 = quota exhausted.
