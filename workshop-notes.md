# Workshop Notes — GitHub CI Lifecycle

These notes back the live demo of the CI lifecycle in `ci-lifecycle-demo`.

## What we're showing

1. **The workflow lives with the code** — `.github/workflows/ci.yml` is just a file in the repo.
   Landing it on the default branch triggers its very first run; no dashboard clicking required.
2. **Runs are inspectable objects** — each run has an id, a status, a conclusion, timing/billable
   usage numbers, and artifacts you can download.
3. **Re-runs are one click (or one API call)** — you can re-run every job of a completed run,
   not just the failed ones.
4. **Reviews close the loop** — branch, pull request, submitted review with inline comments, merge.
5. **Everything is linkable** — run page, artifact, issue tracker, PR, and a write-up gist.

## Demo script

| Step | Action | Where |
| --- | --- | --- |
| 1 | Show the workflow file | `.github/workflows/ci.yml` |
| 2 | Show the completed run | Actions tab / run page |
| 3 | Download the `demo-output` artifact | Run page, Artifacts section |
| 4 | Re-run all jobs | Run page, "Re-run all jobs" |
| 5 | Track progress in an issue | "Demo checklist" issue |
| 6 | Review the notes PR | Pull request with inline review |

## Things worth pointing out on stage

- Artifacts are ephemeral by default — the demo workflow sets `retention-days: 1` on purpose,
  so nothing lingers after the session.
- `permissions: {}` at the top of the workflow means the job gets no implicit token scopes.
  Good default to teach.
- The checksum step proves the artifact contents are deterministic enough to compare across runs.

## Cleanup

This repo is disposable. After the workshop, delete the repo and the write-up gist if you like —
the run data is all captured in the issue and the gist first.
