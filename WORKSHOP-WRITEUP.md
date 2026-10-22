# CI Lifecycle Demo — Workshop Write-Up

A clean, disposable sandbox for demonstrating how we use GitHub for CI, end to end.
Everything below can be walked through live on stage. The repo is safe to delete afterwards.

> **Note on delivery format:** this write-up was meant to be saved as a single-file markdown gist,
> but gist creation is blocked for the current token (403 "Resource not accessible by personal access
> token", confirmed twice). It is stored here in the repo instead. If you want it as a gist, create one
> from this file once you have a token with the `gist` scope. Your gist list is currently empty, so
> nothing similar exists there yet.

## 1. The repository

- **Repo:** https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo
- Public, initialized with a README. No real project code — purely a sandbox.
- Note: it lives under the `mcpmark-eval-liuhezi` organization because repository creation in the
  personal account (`HeziLiu`) was blocked by the current token's permissions. Functionally identical
  for the demo.

## 2. The workflow

- **File:** `.github/workflows/ci.yml` — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/blob/main/.github/workflows/ci.yml
- **Name:** exactly `CI Lifecycle Demo`
- **Trigger:** `on: push` — every push, including the very first one that landed the workflow on the
  default branch (that push is what made it run).
- **Steps:**
  1. Generate a short text report (`output/report.txt`) with repo, branch, commit and runner metadata.
  2. Compute a SHA-256 checksum of the report (`output/report.txt.sha256`).
  3. Upload an artifact named `demo-output`.
- **Teaching points baked in:** `permissions: {}` (job gets no implicit token scopes) and
  `retention-days: 1` (nothing lingers after the session).

## 3. The completed run

- **Run id:** `39852256339`
- **Run page:** https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/actions/runs/39852256339
- **Run number:** 1, event `push`, branch `main`
- **Triggering commit:** `a689a5efb1d5fb3824d54e0b34f66f9f8ffb51f0` ("Add CI Lifecycle Demo workflow")
- **Conclusion:** `success`
- **Timing — first attempt:** started 2026-10-22T20:50:12Z, finished 2026-10-22T20:50:19Z
  (`run_duration_ms: 7000`, 7 seconds wall clock)
- **Timing — full re-run (attempt 2):** started 2026-10-22T20:53:21Z, finished 2026-10-22T20:53:30Z,
  conclusion `success`. The re-run covered **every job**, not just the failed ones.
- **Billable usage (usage API):** UBUNTU — 2 jobs (one per attempt), `total_ms: 0`, each job
  `duration_ms: 0`, `run_duration_ms: 9000`. Billable time is reported as 0 for this public repo /
  very short run — show the wall-clock duration on stage instead.

### Artifact

- **Name:** `demo-output` — contains `report.txt` and `report.txt.sha256`.
- **Current artifact (from the re-run attempt):** id `12456969234`, 505 bytes, digest
  `sha256:14d39aa301faa9646a45393b20a308274101e714a25ed34a07e6e49a8ecc0921`,
  expires 2026-10-23T20:53:26Z.
- **Stable download endpoint:** https://api.github.com/repos/mcpmark-eval-liuhezi/ci-lifecycle-demo/actions/artifacts/12456969234/zip
- **Signed one-time download URL (short-lived, expires quickly):**
  https://productionresultssa10.blob.core.windows.net/actions-results/38b9f758-a4f7-8393-8206-088f51767bba/workflow-job-run-86ceefc1-127f-5006-ba0c-8277086789d8/artifacts/63769aece466ec355086f6913aee5b0d06a93cc7688e9ae3e282604551dd81cf.zip?rscd=attachment%3B+filename%3D%22demo-output.zip%22&rsct=application%2Fzip&se=2026-10-22T21%3A23%3A50Z&sig=TLdabnj6nkpzaeS7BPze73St4vPLgg%2BfCyAz33%2B9sWM%3D&ske=2026-10-22T23%3A17%3A23Z&skoid=ca7593d4-ee42-46cd-af88-8b886a2f84eb&sks=b&skt=2026-10-22T19%3A17%3A23Z&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skv=2025-11-05&sp=r&spr=https&sr=b&st=2026-10-22T21%3A13%3A45Z&sv=2025-11-05
- **Note:** re-running a run replaces the artifact of the same name, so the artifact captured
  before the re-run (id `12457499116`) is gone; use the endpoint above.

### Code scanning status

The code scanning alerts API returned `403 Resource not accessible by personal access token`
for this repo with the current token, so the alert list could not be enumerated. No code
scanning analysis is configured in the repo (the only workflow is `ci.yml`), so no alerts are
expected. Stated plainly: **no code scanning alerts were confirmed to exist — the API check
itself was blocked by token permissions.**

## 4. The issue (tracker)

- **Issue:** "Demo checklist" — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/issues/1
- Contains the demo outline plus a comment starting "Collected run data:" with the run id,
  conclusion, timing, billable usage, the artifact download URLs, and the code scanning status.

## 5. The pull request

- **PR:** "Add workshop notes" — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/pull/2
- **Branch:** `workshop-notes` → `main`
- **Change:** adds `workshop-notes.md` with the workshop notes, demo script table and teaching points.
- **Review:** a submitted comment-style review with an inline comment on `workshop-notes.md`
  (line 7, the "The workflow lives with the code" bullet) —
  https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/pull/2#discussion_r4353442484
- The inline comment was verified to appear on the PR after submission.

## Demo flow in one line

Push workflow → run completes (success) → collect id/conclusion/timing/artifact → re-run all
jobs → track in an issue → branch → PR → comment review with inline comment → write-up gist
(stored in this file while gist creation is blocked).

## Cleanup

This sandbox is disposable. After the workshop: delete the repo
(`mcpmark-eval-liuhezi/ci-lifecycle-demo`) and this write-up with it. All the run data is
captured here first.
