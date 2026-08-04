# product-reality-check

A Claude agent skill for the developer who built something good and has no users.

It runs the unglamorous half of shipping a product: finding out who would actually pay,
auditing the claims you have been making against prior art, sizing the opportunity from named
buyers rather than a press-release TAM, hunting the contradictions between what your landing
page says and what your code does, and then red-teaming the whole thing in the voice of the
skeptic whose "no" would hurt most.

The posture is validation-first. **The deliverable is truth, not encouragement.** When the
honest answer is "this is a good $1M/year business and not a venture-scale one," or "the
differentiator you have been leading with is already table stakes for the market leader," the
skill says so, then says what is actually left standing. That is not pessimism as a style —
conceding weaknesses openly is what buys credibility for the claims that survive. Readers
punish discovered weakness, not disclosed weakness.

## What it does

- **Scaffolds a research workspace** — `strategy/`, `research/`, `decisions/`, `data/` — with a
  living-vs-append-only convention, dated reports that are never rewritten, and a competitor
  database whose entries go stale after 30 days on purpose.
- **Audits superlatives before you build on them.** Any "first", "only", or "nobody does this"
  gets checked against adjacent categories, historical work, academic papers and dormant twins
  *before* it enters a pitch. Convergent invention turns out to be evidence the gap is real —
  and "the one still maintained and complete" is a better story than a false "first".
- **Sizes bottom-up.** Named buyer archetypes × sourced price anchors × defensible counts, with
  realistic and stretch pools kept apart, plus the base rate of everyone who already tried.
- **Diagnoses the product** — pricing pages that contradict themselves, margins computed on the
  billed event only, download counts that are mostly your own CI.
- **Writes the deliverables** — positioning, a banned-claims list, a narrative sequenced
  weakness-first, an objection pack with honest `unresolved` statuses, and a claim ledger where
  every external number carries a source and a verification date.
- **Red-teams it** — a kill memo with "I pass because…", the ten meeting-ending questions, the
  single load-bearing fact (then checks it), and a patch loop that puts every finding back into
  the documents.
- **Sets numeric gates** with dates, before the evidence arrives, that move only via a dated
  decision record. Zeros are reported as zeros.

Reports come out in whatever language you are writing in; the internal templates are English.

## Install

Copy the `product-reality-check/` directory into your skills folder:

```bash
# Personal — available in every project
cp -r product-reality-check ~/.claude/skills/

# Or per-project — checked into the repo, shared with the team
mkdir -p .claude/skills && cp -r product-reality-check .claude/skills/
```

Then just describe the problem. It triggers on the real questions people ask — "who would pay
for this?", "is my side project viable?", "why is nobody using it?", "check my competitors",
"help me position this", "is this pricing sane?", "review my pitch" — without anyone having to
say the words "market research".

## Where the methodology came from

It is distilled from a real engagement: a solo founder with a shipped open-source compiler, a
commercial product on top of it, and effectively no customers. Over several weeks that work
produced a dozen dated research reports, a positioning doc whose central moat claim was refuted
twice and rewritten twice, a bottom-up sizing that concluded the exciting infrastructure
re-positioning relocated the ceiling rather than escaping it, a prior-art audit that killed the
words "first" and "only" permanently by finding a 1975 research language and three dormant
twins, and a kill memo that verified the headline traction number — accurate to the digit — and
found that two thirds of it sat on the founder's own release days. Every move in this skill is
one of those moves, generalized off that product and rewritten to work for any developer's.

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 Chan Meng.
