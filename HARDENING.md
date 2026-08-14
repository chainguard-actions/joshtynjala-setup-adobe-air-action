<!-- markdownlint-disable -->

# Hardening Report: joshtynjala--setup-adobe-air-action/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **joshtynjala--setup-adobe-air-action/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 10 'uses: actions/checkout@v3' references in .github/workflows/main.yml use a mutable tag (@v3) instead of a pinned 40-character SHA commit hash. This exposes the workflow to supply-chain attacks if the tag is moved to point to a different (potentially malicious) commit. Each job's checkout step is affected.

Locations:

- `.github/workflows/main.yml:17`
- `.github/workflows/main.yml:28`
- `.github/workflows/main.yml:39`
- `.github/workflows/main.yml:53`
- `.github/workflows/main.yml:65`
- `.github/workflows/main.yml:77`
- `.github/workflows/main.yml:89`
- `.github/workflows/main.yml:101`
- `.github/workflows/main.yml:114`
- `.github/workflows/main.yml:127`

### missing-permissions (severity: medium)

The workflow file .github/workflows/main.yml has no top-level 'permissions:' key and none of its 10 jobs define a job-level 'permissions:' block. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned all 10 'actions/checkout@v3' references to the full commit SHA 'a37ce9120846195fa4ece8f58b268e6043cb2f26' with '# v3' comments for readability. 2. Added 'permissions: {}' at the top level of the workflow to enforce least privilege on the GITHUB_TOKEN, since none of the jobs require any token permissions.

