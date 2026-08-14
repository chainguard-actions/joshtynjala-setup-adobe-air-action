<!-- markdownlint-disable -->

# Hardening Report: joshtynjala--setup-adobe-air-action/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **joshtynjala--setup-adobe-air-action/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 10 jobs in the workflow use `actions/checkout@v3`, which is a mutable tag reference rather than a pinned 40-character commit SHA. If the tag is moved (e.g. by a supply-chain compromise), the workflow will silently execute different code. Each job should pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/main.yml:16`
- `.github/workflows/main.yml:27`
- `.github/workflows/main.yml:38`
- `.github/workflows/main.yml:52`
- `.github/workflows/main.yml:65`
- `.github/workflows/main.yml:78`
- `.github/workflows/main.yml:91`
- `.github/workflows/main.yml:104`
- `.github/workflows/main.yml:117`
- `.github/workflows/main.yml:130`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/main.yml` has no top-level `permissions:` key and none of its 10 jobs define a `permissions:` block. Without explicit permissions, GitHub Actions grants the default token permissions (which can include `contents: write` on some repository configurations), violating the principle of least privilege. A top-level `permissions: {}` or minimal per-job permissions block should be added.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/main.yml: (1) Pinned all 10 occurrences of `actions/checkout@v3` to the full commit SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` with `# v3` comment for readability. (2) Added `permissions: {}` at the top level of the workflow to enforce least privilege, since the workflow only tests the action and requires no GitHub token permissions.

