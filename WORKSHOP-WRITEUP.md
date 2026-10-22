# CI Lifecycle Demo — Workshop Write-Up

A clean, disposable sandbox for demonstrating how we use GitHub for CI, end to end.
Everything below can be walked through live on stage. The repo is safe to delete afterwards.

> **Note on delivery format:** this write-up was meant to be saved as a single-file markdown gist,
> but gist creation is blocked for the current token (403 "Resource not accessible by personal access
> token"). It is stored here in the repo instead. If you want it as a gist, create one from this file
> once you have a token with the `gist` scope.

## 1. The repository

- **Repo:** https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo
- Public, initialized with a README. No real project code — purely a sandbox.
- Note: it lives under the `mcpmark-eval-liuhezi` organization because repository creation in the
  personal account was blocked by the current token's permissions. Functionally identical for the demo.

## 2. The workflow

- **File:** `.github/workflows/ci.yml` — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/blob/main/.github/workflows/ci.yml
- **Name:** exactly `CI Lifecycle Demo`
- **Trigger:** `on: push` — every push, including the very first one that landed the workflow on the default branch.
- **Steps:**
  1. Generate a short text report (`output/report.txt`) with repo, branch, commit and runner metadata.
  2. Compute a SHA-256 checksum of the report (`output/report.txt.sha256`).
  3. Upload an artifact named `demo-output`.
- **Teaching points baked in:** `permissions: {}` (no implicit token scopes) and `retention-days: 1` (nothing lingers after the session).

## 3. The completed run

- **Run id:** `39852256339`
- **Run page:** https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/actions/runs/39852256339
- **Run number / attempt:** 1 / 1, event `push`, branch `main`
- **Triggering commit:** `a689a5efb1d5fb3824d54e0b34f66f9f8ffb51f0` ("Add CI Lifecycle Demo workflow")
- **Conclusion:** `success`
- **Timing:**
  - Started: 2026-10-22T20:50:12Z
  - Finished: 2026-10-22T20:50:19Z
  - Run duration: `run_duration_ms: 7000` (7 seconds)
- **Billable usage:** UBUNTU — 1 job, `total_ms: 0`, job duration `duration_ms: 0`
  (billable time is reported as 0 for this public repo / very short run; the 7s wall-clock duration above is the number to show on stage)

### Artifact

- **Name:** `demo-output` (id `12457499116`, 505 bytes, SHA-256 digest
  `sha256:51d6ec168f8233224b8473e2a2f4ed5c732f9db30503cc316459f47f686132c2`, retention 1 day)
- **Stable download endpoint:** https://api.github.com/repos/mcpmark-eval-liuhezi/ci-lifecycle-demo/actions/artifacts/12457499116/zip
- **Signed one-time download URL (short-lived, expires quickly):**
  https://productionresultssa9.blob.core.windows.net/actions-results/a224394f-1739-8136-a1c3-42e6682cd91c/workflow-job-run-30330dcd-f6b6-5c9d-bb25-633d5b6679c6/artifacts/63769aece466ec355086f6913aee5b0d06a93cc7688e9ae3e282604551dd81cf.zip?rscd=attachment%3B+filename%3D%22demo-output.zip%22&rsct=application%2Fzip&se=2026-10-22T21%3A00%3A42Z&sig=rAB6De8ElkvWJYgPVVm1Z4AkXf6IzPclPJCdxh4YnxE%3D&ske=2026-10-22T23%3A17%3A15Z&skoid=ca7593d4-ee42-46cd-af88-8b886a2f84eb&sks=b&skt=2026-10-22T19%3A17%3A15Z&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skv=2025-11-05&sp=r&spr=https&sr=b&st=2026-10-22T20%3A50%3A37Z&sv=2025-11-05
- **Contents:** `report.txt` and `report.txt.sha256`.

### Re-run

- A full re-run of every job of the completed run was triggered via the API (`rerun` on run
  `39852256339`), queued with `201 Created`. Find it as attempt 2 on the same run page above.

## 4. The issue (tracker)

- **Issue:** "Demo checklist" — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/issues/1
- Contains the demo outline and a comment starting "Collected run data:" with the run id,
  conclusion, timing, billable usage, the artifact download URL, and the code scanning status.

### Code scanning status

The code scanning alerts API returned `403 Resource not accessible by personal access token`
for this repo with the current token, so the alert list could not be enumerated. No code scanning
analysis is configured in the repo (the only workflow is `ci.yml`), so no alerts are expected, but
the API could not be read to confirm. Stated plainly: **unknown / not retrievable with the current
token permissions — no alerts were confirmed to exist either way.**

## 5. The pull request

- **PR:** "Add workshop notes" — https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/pull/2
- **Branch:** `workshop-notes` → `main`
- **Change:** adds `workshop-notes.md` with the workshop notes, demo script table and teaching points.
- **Review:** a submitted comment-style review with an inline comment on `workshop-notes.md`
  (line 7, the "The workflow lives with the code" bullet) —
  https://github.com/mcpmark-eval-liuhezi/ci-lifecycle-demo/pull/2#discussion_r4353442484
- The inline comment was verified to appear on the PR after submission.

## Demo flow in one line

Push workflow → run completes (success) → collect id/conclusion/timing/artifact → re-run all jobs →
track in an issue → branch → PR → comment review with inline comment → write-up (this file).

## Cleanup

This sandbox is disposable. After the workshop: delete the repo
(`mcpmark-eval-liuhezi/ci-lifecycle-demo`) and this write-up with it. All the run data is captured here first.
