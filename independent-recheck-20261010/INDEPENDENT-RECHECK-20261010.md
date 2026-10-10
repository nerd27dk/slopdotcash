# Independent SlopDotCash APV recheck

Date: 2026-10-10  
Target: `hark-agent/slopdotcash`, APV wallet-identity experiment 1  
Public matrix source: [`apv/experiment-1`](https://github.com/hark-agent/slopdotcash/tree/apv/experiment-1), commit `3b1a2a2ec3478e6f655a83dd16c0afba8790d2a3`  
PR #3: [merged in Hark's fork](https://github.com/hark-agent/slopdotcash/pull/3), tested head `4e4389be41dcb5f1b23348bcf1934e4248366a5e`

## Independent matrix runs

Replayed the published 48-cell Playwright matrix in a fresh temporary clone, one revision at a time. The browser requests to GitHub and the wallet registry were mocked by the matrix, as in Hark's run.

| Revision | Result | Independent observation |
|---|---:|---|
| Baseline `b425030a332d6800e92eb2afde7127539d4f3f5b` | 28/48 | Same 20 failures: renamed-login cells M25–M36 and eight mismatched-identity cells M37, M38, M40, M42–M46. |
| PR #3 `4e4389be41dcb5f1b23348bcf1934e4248366a5e` | 48/48 | No failures. |
| `seed/promise-all` `04a9fcc87ac66496f871e7f2d8597bc8b6e7a084` | 24/48 | Eight new partial-chain failures; four existing mismatch failures become green because the fault reports everything unavailable. Cell-by-cell results expose this masking. |
| `seed/no-frozen-lookup` `55477dd17e1ecbfdddcf6a2342f5cc02e95e5e55` | 13/48 | Fifteen additional failures on frozen-only and mismatch scenarios. |
| `seed/no-node-id-check` `b376b3a5bc997e667de479ed6493691c6ba610ac` | 28/48 | Same failed cells and observed markers as baseline; the injected change has no additional effect on the already-broken baseline. |
| `seed/no-node-id-check-on-fix` `28f609af02f75f7ff60482d5897410a20a2eddbb` | 40/48 | Eight mismatch cells fail again, matching the baseline identity defect. |

The baseline/fix and all five seed results match the public evidence ledger. This is an independent rerun of the published harness; the matrix itself is not a blind discovery of H2/H3. H3 was predicted in the pre-registered invariant notes, and H2 was first identified by targeted testing before being represented in matrix v2.

## I4 direct routes

Using a local Cloudflare Pages preview built from the fork's APV code, tested 21 direct paths including `/earnings`, `/earnings/`, `/earnings?x=1`, login, account, points, project, contributor, cycle, wallet, and verification routes. For each path, checked the initial response and reload response for HTTP 200 and the app root.

- `/earnings`, `/earnings/`, and `/earnings?x=1` returned 404 without the app root.
- The other 18 paths returned 200 with the app root on direct load and reload.
- An unknown path returned 404 without the app root.

The tested build was mutation commit `28f609a` (the node-id check deliberately removed for the matrix control). Its `public/_redirects`, `public/_routes.json`, and `src/App.tsx` match PR #3 head `4e4389b`; the mutation is in wallet identity logic. This local route failure is in the fork's older Pages route configuration, not the PR #3 code change.

Separately checked the live site: `/earnings`, `/earnings/`, and `/earnings?x=1` returned 200 with the app root; `/does-not-exist` returned 404 without it. The independent live result matches the reported production fix. GitHub shows the separate route fix as PR #603, with head commit `596a3192a772fa4851bd6455aee9bc7011975f3a` and merge commit `9b998c8080e995375af55544d5267d6c11ec585d`.

## Environment and limits

- Independent runner: macOS 27.0, Apple Silicon; Playwright 1.62.1; Chromium 151.0.7922.34. Hark's published run used Linux arm64 and the same Chromium version.
- Build input snapshot: `public/data/leaderboard.json`, SHA-256 `9ee2ea15cda516fbb793827c2b5c9fa0afd005ca6e303bae8e18c95261260850`.
- No live GitHub identity or wallet-registry requests were used for the 48-cell matrix. It does not prove behavior against live wallet claims or payout services.
- I did not rerun the upstream `376fed1` 48-cell matrix. Inspection confirms its wallet link is inside collapsed `<details class="profile-wallet-details">`, while the published matrix requires that link to be visible before checking a cell. Therefore the reported 0/48 is a harness applicability failure, not an upstream behavioral result. A UI-adapted upstream spec remains needed.
- This does not rerun the full E2E suite, the live-registry oracle, or production checks for every route in I4.
- The user's existing `nerd27dk/slopdotcash-checkout` worktree remains clean. All test runs used a separate temporary clone; no code or comments were published.

Raw Playwright JSON results and build logs: `independent-recheck-20261010/raw-results/`.


## Publication record

This report and its raw run outputs are published in the Nerd fork on the separate `fixtures/leaderboard-snapshot` branch alongside the exact leaderboard input. The branch is an evidence archive and must not be merged into a product branch. The original audited checkout remained clean.
