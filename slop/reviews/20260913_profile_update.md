# Profile update for editorial review

Prepared by Codex/Astra, 2026-09-13. Local changes only; no push, deployment or account-bio change.

GitHub account bio draft (existing wording retained, fellowship added):

> Machine Learning researcher focused on Pragmatic AI alignment. Fellow, AI Safety Australia & New Zealand. Waiting to be uploaded.

The README adds the fellowship, ML bench and suppressed-activations (WIP). The website and CV add the fellowship and ML bench; suppressed-activations remains a source-only website TODO.

VJP image: [published PNG](https://raw.githubusercontent.com/wassname/vjp-steering/main/results/plot.png), SHA-256 `215d81497461c5197de47e4a790bb167c7f47cfaa5fd11a031465b2489b037b0`. Downloaded unchanged. Alt coordinates come from the [interactive figure's JSON](https://github.com/wassname/vjp-steering/blob/main/results/index.html), rounded to two decimals, and were checked against the PNG by Codex/Astra and a fresh-eyes Codex/Astra agent. The plot smooths coordinates; its endpoints differ from the unsmoothed results table. This replaces the old 20-question figure with the public 100-question figure, including PCA and the random envelope, as requested this session.

Verification: `just build` passed (homepage, HTML/PDF CV, agenda); introduced links returned HTTP 200; image hashes match the download, profile asset, website output and deployment staging copy. Rendered HTML/PDF contains the fellowship and ML bench, with no Steerability Challenge; the website TODO is stripped. Both source diffs pass `git diff --check`. Build log: `../.local/homepage-update/build.log` from this repository's root.
