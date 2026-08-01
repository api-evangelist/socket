---
name: Diff-scan a pull request
description: Create a diff scan between a repository's current HEAD full scan and new manifest
  changes, then read the dependency/alert diff as GitHub-flavored markdown for a PR comment.
api: openapi/socket-openapi-original.json
operations:
- createOrgRepoDiff
- getDiffScanById
- GetDiffScanGfm
- createOrgDiffScanFromIds
---

# Diff-scan a pull request

Use this to show what a change adds/removes in supply-chain risk terms, for a PR gate.

## Auth
`Authorization: Bearer <ORG_API_TOKEN>` with `repo:list`, `diff-scans:create`, and
`full-scans:create` scopes. Base URL `https://api.socket.dev/v0`.

## Steps
1. `createOrgRepoDiff` — POST `/orgs/{org_slug}/diff-scans/from-repo/{repo_slug}` with the
   changed manifest files. Socket diffs them against the repo's current HEAD full scan and
   returns diff-scan metadata (including an `api_url`).
   - Alternatively, `createOrgDiffScanFromIds` — POST `/orgs/{org_slug}/diff-scans/from-ids`
     to diff two existing full scan IDs in the same repository.
2. `getDiffScanById` — GET `/orgs/{org_slug}/diff-scans/{diff_scan_id}` to fetch the full
   diff contents (added/removed/changed dependencies and new alerts).
3. `GetDiffScanGfm` — GET `/orgs/{org_slug}/diff-scans/{diff_scan_id}/gfm` to get a
   ready-to-post GitHub-flavored-markdown comment summarizing the diff.

## Rules
- Fail the PR when the diff introduces alerts whose action is `error` under your security
  policy (`getOrgSecurityPolicy`).
- Paginate any list calls with `endCursor`/`startAfterCursor` until the cursor is null.
