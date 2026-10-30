# Skill Benchmark: product-reality-check

**Model**: claude-opus-5
**Date**: 2026-08-04T09:21:53Z
**Evals**: 0, 1 (1 run each per configuration)

> **Timing and token columns are INVALID this iteration** - the runs were interrupted by a
> session limit and resumed. They are recorded as 0 and must not be interpreted.

## Summary

| Metric | With Skill | Without Skill | Delta |
|--------|------------|---------------|-------|
| Pass Rate | 100% ± 0% | 83% ± 0% | +0.17 |
| Time | n/a (invalid) | n/a (invalid) | n/a |
| Tokens | n/a (invalid) | n/a (invalid) | n/a |

## Per-eval

| Eval | With Skill | Without Skill |
|------|-----------|---------------|
| eval-0-echook-viability | 6/6 | 5/6 |
| eval-1-gradient-svg-positioning | 6/6 | 5/6 |

## Notes

- TIMING AND TOKENS ARE INVALID THIS ITERATION and are recorded as 0 everywhere. All four runs were interrupted mid-flight by a session-limit outage and resumed, so wall-clock and token totals measure the outage, not the work. Do not read the time/token rows in this benchmark, and do not compare them to any future iteration.
- Single run per configuration (runs_per_configuration is 1, not 3), so every stddev is 0 by construction and no variance claim can be made. A pass-rate difference of one assertion out of six is within the noise a single run can produce.
- Overall: with_skill 12/12 (100%), without_skill 10/12 (83%), delta +0.17. The skill did not fail anything, but the baseline was unusually strong - this is a weak discrimination signal, not a strong endorsement.
- NON-DISCRIMINATING - 10 of the 12 assertions passed in BOTH configurations. In eval-0: falsification-section-present, external-claims-carry-session-urls, named-buyer-archetypes-with-price-anchors, plain-viability-verdict, adoption-metrics-decomposed-or-caveated. In eval-1: largest-claim-explicitly-audited, defensible-narrower-claim-supplied, hostile-scrutiny-pass-present, monetization-verdict-addresses-freerider-costs, falsification-section-present. These measure competent analyst writing, which the model already does unprompted.
- DISCRIMINATING #1 - eval-0 'no-unaudited-superlative' (with_skill PASS / without_skill FAIL). This is the only assertion that failed on substance rather than form. The baseline recommended a README headline ('One notification layer for Claude Code, Cursor, and Codex') resting on cross-editor uniqueness it never checked: its own competitor table records 25 repos with stars, dates and licences but not editor coverage - the single axis it declared to be the moat. It is also internally contradicted, asserting per-agent audio identity is 'unmet' while its own evidence section lists Voxlert and cmux-skills doing exactly that. The with_skill run, same prompt and date, found DevinoSolutions/anotifier-for-claude-codex-cursor (CC+Codex+Gemini+Cursor), ctoth/claudio, peon-ping and Cursor's native Claude-Code-hook compatibility layer.
- DISCRIMINATING #2 - eval-1 'competitor-table-with-sources' (with_skill PASS / without_skill FAIL). Mechanical: 10 of 10 named competitors carry a resolvable URL with the skill; 3 of 16 without. This one separates on citation hygiene rather than analytical depth - the baseline counted capsule-render's 69 colour presets from its source JSON, which is deeper work than a URL list proves.
- DISCRIMINATING #3 (unmeasured by any assertion, and the largest observed behavioural gap) - self-correction. Both with_skill runs shipped a hostile red-team memo, a patch record, and struck-through retractions inside the customer-facing verdict; neither baseline shipped any self-correction artifact. In eval-1 the red team overturned four claims that were about to ship as public copy: '186 distinct effects' (true value 168, 18 aliases rendering byte-identically), 'capsule-render is static by default' (5 of 6 sampled types loop - refutable by one curl), a false confession that '70 of 355 are static' (all 70 animate), and a fused '489x adoption gap' (like-for-like is ~2,590x). The eval-1 baseline recommends the unverified 186 figure as approved copy in its claims ledger, graded green.
- SURPRISE - the baselines are strong, not weak. Both scored 5/6 and produced work the assertions do not reward: the eval-0 baseline verified Anthropic's native rate_limits/terminalSequence fields first-hand from fetched docs (the finding that reversed its own verdict) and rejected five widely-repeated market figures for lack of primary sourcing; the eval-1 baseline found that Vercel's Fair Use terms classify asking for donations as commercial usage, making a donate button on the current Hobby deployment a terms violation. Any claim that this skill 'adds rigour' has to clear that bar, not a naive baseline.
- PATTERN ACROSS EVALS - the generative difference is measuring the artifact versus reading the manifest. Both eval-1 runs counted 186 effects from the registry; only the skill run rendered all 355 templates, hashed the outputs, found 168 distinct results, and caught 24 non-deterministic templates being served with immutable year-long cache headers. Both eval-0 runs caveated clone counts; only the skill run computed the 78/85 cloner-to-viewer ratio, concluded no human population produces 92%, and banned the metric outright.
- OUTPUT VOLUME differs by roughly 6.5x and is not currently measured or bounded: with_skill produced 424,982 chars across 15 files (eval-0) and 176,810 across 7 files (eval-1); without_skill produced 65,592 across 5 files and 60,516 across 5 files. Whether that depth is worth the read is a judgement no assertion in this set makes.
- EVAL-DESIGN ACTION for iteration 2 - the URL-count floor ('at least 5 distinct URLs') is dead weight: the baseline cleared it with 10 while leaving every competitor star count, HN quote and buyer price anchor unsourced; the skill run produced 113. Similarly 'sourced price anchor' is glossed as 'a real product/tier price, not an invented number', which memory satisfies. Add a URL requirement to both, and add two new assertions covering the unmeasured gaps: (a) the deliverable records at least one claim it retracted, with the evidence that forced it; (b) at least one headline product number is corrected by measuring the artifact rather than its manifest.