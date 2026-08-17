<!-- markdownlint-disable -->

# Hardening Report: joshtynjala--setup-adobe-air-action/v2.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **joshtynjala--setup-adobe-air-action/v2.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v3` (a mutable tag reference) in all 9 jobs instead of a pinned full-length SHA digest. A tag can be moved to point to a different, potentially malicious commit, enabling supply-chain attacks. All occurrences should be replaced with the full 40-character commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/main.yml:14`
- `.github/workflows/main.yml:27`
- `.github/workflows/main.yml:38`
- `.github/workflows/main.yml:51`
- `.github/workflows/main.yml:64`
- `.github/workflows/main.yml:77`
- `.github/workflows/main.yml:90`
- `.github/workflows/main.yml:103`
- `.github/workflows/main.yml:116`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/main.yml` has no top-level `permissions:` key and no job-level `permissions:` block on any of its 9 jobs. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all` for older repositories). A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned all 10 occurrences of `actions/checkout@v3` to the full SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` with a `# v3` comment for readability. 2. Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

