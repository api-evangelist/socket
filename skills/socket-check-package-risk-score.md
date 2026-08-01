---
name: Check a package's risk score before adding it
description: Look up Socket's supply-chain, quality, maintenance, vulnerability, and license
  scores plus alerts for one or more packages by PURL before installing them.
api: openapi/socket-openapi-original.json
operations:
- batchPackageFetchByOrg
- getScoreByNPMPackage
- getIssuesByNPMPackage
---

# Check a package's risk score before adding it

Use this to vet a dependency (or a batch of them) before it enters a project.

## Auth
`Authorization: Bearer <ORG_API_TOKEN>` with the `packages:list` scope for the org-scoped
batch endpoint. Base URL `https://api.socket.dev/v0`.

## Steps
1. Preferred (batch, org-scoped): `batchPackageFetchByOrg` — POST `/orgs/{org_slug}/purl`
   with a body of PURL components, e.g.
   `{ "components": [ { "purl": "pkg:npm/express@4.19.2" } ] }`.
   Add `?alerts=true` to include alert data. Batch limit is 1024 PURLs; this costs 100 quota
   units. Works across npm, PyPI, Maven, Go, NuGet, RubyGems, Cargo.
2. Quick single npm lookups: `getScoreByNPMPackage` — GET `/npm/{package}/{version}/score`,
   and `getIssuesByNPMPackage` — GET `/npm/{package}/{version}/issues`.

## Rules
- Scores span supply-chain, quality, maintenance, vulnerability, and license dimensions —
  the same data the `depscore` MCP tool returns.
- When `alerts=true`, Socket may synthesize `pendingScan` (analysis not finished) or
  `notFound` alert types; use `poll=true` to wait for pending analysis, `poll=false` to fail
  open fast.
