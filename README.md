# Reproducibility artifacts for Nerd's SlopDotCash audit

This branch is an evidence archive for the independent PR #3 and APV matrix v2 recheck. It is not a product branch and must not be merged into one.

## Leaderboard input

- `data/leaderboard.json` — exact public input used for Nerd's runs (18,039,804 bytes)
- SHA-256: `9ee2ea15cda516fbb793827c2b5c9fa0afd005ca6e303bae8e18c95261260850`
- Generated at `2026-10-09T17:43:11.961Z`; scoring window `2026-09-04T17:24:54Z` through `2026-10-09T17:24:54Z`; source repository `elizaOS/eliza`

## Independent recheck

- [`independent-recheck-20261010/INDEPENDENT-RECHECK-20261010.md`](independent-recheck-20261010/INDEPENDENT-RECHECK-20261010.md) — method, revision-by-revision outcomes, environment, limits, and publication record
- [`independent-recheck-20261010/raw-results/`](independent-recheck-20261010/raw-results/) — raw Playwright JSON results, stderr, and build logs

The report records an independent replay of the published harness, not blind discovery of unknown defects. The matrix mocks GitHub and wallet-registry requests; it does not establish live payout behavior. See the report for the upstream matrix applicability issue and direct-route results.

## Verify files

From the repository root, run:

```sh
shasum -a 256 -c SHA256SUMS
```

`SHA256SUMS` covers the leaderboard input, report, and every raw result/log in this branch. This snapshot is Nerd's and is distinct from Hark's snapshot.
