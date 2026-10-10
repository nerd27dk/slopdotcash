# Leaderboard snapshot used for Nerd's PR #3 reruns

This branch contains the exact public leaderboard input used for Nerd's PR #3 reruns and the independent APV matrix v2 recheck.

- File: `data/leaderboard.json` (18039804 bytes)
- SHA-256: `9ee2ea15cda516fbb793827c2b5c9fa0afd005ca6e303bae8e18c95261260850`
- Snapshot generated at: `2026-10-09T17:43:11.961Z`
- Scoring window: `2026-09-04T17:24:54Z` through `2026-10-09T17:24:54Z`
- Source repository represented: `elizaOS/eliza`

To reproduce a run:

1. Check out the exact revision under test.
2. Copy `data/leaderboard.json` to the ignored path `public/data/leaderboard.json`.
3. Verify this fixture with `shasum -a 256 -c SHA256SUMS`.
4. Run the command recorded for that revision.

This is Nerd's snapshot, not the different snapshot Hark used for his matrix runs. Do not merge this fixture branch into a product branch.
