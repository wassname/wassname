# Profile update and deployment

Prepared by Codex/Astra, 2026-09-13. Wassname edited the bios and approved deployment; spelling review found no errors. The website, CV and GitHub profile were published and verified before the requested ML bench screenshot addition.

GitHub sidebar bio stays unchanged, as confirmed by wassname. The extra profile-write authorization was cancelled; repository publishing already worked.

> Machine Learning researcher focused on Pragmatic AI alignment. Waiting to be uploaded.

The README adds the fellowship, ML bench and suppressed-activations (WIP). The website and CV add the fellowship and ML bench; suppressed-activations remains a source-only website TODO. Wassname shortened the fellowship introductions and removed the dates; these edits were preserved verbatim.

ML bench screenshot: captured from the public page, with the title, cost/score plot and controls. SHA-256 `35b3b77b2296ae4db2c3cd075d87e357d63353017799bcbc982c5cdb85f2baa4`. Alt readings are from [results.json v97](https://github.com/wassname/ml-bench/blob/a0c07d5aa5a13a0c266f6b23cabb096c7bc95b8b/results.json), checked against the screenshot by Codex/Astra and a fresh-eyes agent. The GitHub thumbnail is 300 pixels wide and comes first in Evals & datasets; the website uses its existing thumbnail style. Both images link to the interactive results.

VJP image: [published PNG](https://raw.githubusercontent.com/wassname/vjp-steering/main/results/plot.png), SHA-256 `215d81497461c5197de47e4a790bb167c7f47cfaa5fd11a031465b2489b037b0`. Downloaded unchanged. Alt coordinates come from the [interactive figure's JSON](https://github.com/wassname/vjp-steering/blob/main/results/index.html), rounded to two decimals, and were checked against the PNG by Codex/Astra and a fresh-eyes Codex/Astra agent. The plot smooths coordinates; its endpoints differ from the unsmoothed results table. This replaces the old 20-question figure with the public 100-question figure, including PCA and the random envelope, as requested this session.

Verification: `just build` passed (homepage, HTML/PDF CV, agenda); introduced links returned HTTP 200; image hashes match the download, profile asset, website output and deployment staging copy. Rendered HTML/PDF contains the fellowship and ML bench, with no Steerability Challenge; the website TODO is stripped. Both source diffs pass `git diff --check`. Build log: `../.local/homepage-update/build.log` from this repository's root.
