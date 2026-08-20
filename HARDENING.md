<!-- markdownlint-disable -->

# Hardening Report: bufbuild--buf-breaking-action/v1.1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **bufbuild--buf-breaking-action/v1.1.4** was hardened automatically. 7 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### broad-permissions (severity: medium)

The workflow uses `permissions: read-all` at the top level, which grants overly broad read access across all scopes. It should be replaced with specific minimal permissions (e.g., `contents: read`).

Locations:

- `.github/workflows/ci.yaml:10`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. This means the workflow runs with the default (potentially write) token permissions. A `permissions:` block with minimal scopes should be added.

Locations:

- `.github/workflows/add-to-project.yaml:1`

### unpinned-uses (severity: high)

Multiple `uses:` references are pinned to mutable tags or branch names instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if the referenced tag or branch is moved. Failing references: `actions/checkout@v4` (line 15), `actions/setup-go@v5` (line 19), `actions/setup-node@v4` (line 23), `bufbuild/buf-setup-action@v1` (line 29).

Locations:

- `.github/workflows/ci.yaml:15`
- `.github/workflows/ci.yaml:19`
- `.github/workflows/ci.yaml:23`
- `.github/workflows/ci.yaml:29`

### unpinned-uses (severity: high)

The `uses:` reference `bufbuild/base-workflows/.github/workflows/add-to-project.yaml@main` is pinned to the mutable branch `main` instead of a full 40-character commit SHA, making the workflow vulnerable to supply-chain attacks.

Locations:

- `.github/workflows/add-to-project.yaml:19`

### unpinned-uses (severity: high)

The `uses:` reference `bufbuild/base-workflows/.github/workflows/emergency-review-bypass.yaml@main` is pinned to the mutable branch `main` instead of a full 40-character commit SHA, making the workflow vulnerable to supply-chain attacks.

Locations:

- `.github/workflows/emergency-review-bypass.yaml:11`

### unpinned-uses (severity: high)

The `uses:` reference `bufbuild/base-workflows/.github/workflows/notify-approval-bypass.yaml@main` is pinned to the mutable branch `main` instead of a full 40-character commit SHA, making the workflow vulnerable to supply-chain attacks.

Locations:

- `.github/workflows/notify-approval-bypass.yaml:9`

### unpinned-uses (severity: high)

The `uses:` reference `bufbuild/base-workflows/.github/workflows/pr-title.yaml@main` is pinned to the mutable branch `main` instead of a full 40-character commit SHA, making the workflow vulnerable to supply-chain attacks.

Locations:

- `.github/workflows/pr-title.yaml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** broad-permissions, missing-permissions, unpinned-uses

**Notes:**

Fixed all findings across 5 workflow files: (1) ci.yaml: replaced `permissions: read-all` with `permissions: contents: read` (broad-permissions fix), and pinned actions/checkout@v4, actions/setup-go@v5, actions/setup-node@v4, and bufbuild/buf-setup-action@v1 to their full commit SHAs. (2) add-to-project.yaml: added `permissions: {}` top-level block (missing-permissions fix) and pinned bufbuild/base-workflows@main to SHA 7c0b54b718244c78f00037343ff7cb33ef7caca9. (3) emergency-review-bypass.yaml: pinned bufbuild/base-workflows@main to full SHA. (4) notify-approval-bypass.yaml: pinned bufbuild/base-workflows@main to full SHA. (5) pr-title.yaml: pinned bufbuild/base-workflows@main to full SHA. All mutable tag/branch references replaced with full 40-character commit SHAs with inline tag comments for readability.

