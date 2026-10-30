# Viability gates — echook

**LIVING DOCUMENT.** The go/no-go instrument. Thresholds are set **in advance** and move only via a dated
decision record in `decisions/`. A threshold quietly lowered to make a week look better has destroyed the
instrument.

**Zeros are reported as zeros.** The temptation to omit an empty row is the exact failure mode this
document exists to prevent.

**Decide with the whole table, not metric by metric.**

---

## The situation these gates are calibrated against

- 9 months, 152 commits, 53 releases, **78 GitHub stars**, 7 forks, 1 open issue (titled "Good job!").
- **Zero revenue. Zero telemetry. Zero customer conversations.** No release has ever carried a
  downloadable asset, so no download counter has ever existed.
- Stars peaked at **19 in April 2026** and fell to **4 in July 2026** — while June–July was the heaviest
  shipping period in the project's history (v6.0.0 → v6.4.0, ten releases). **Shipped hardest, acquired
  fewest.**
- A GitHub Sponsors listing and a Buy Me a Coffee button are already live, with **222 followers and 0
  sponsors**. The donation experiment has already run for nine months and returned zero.

---

## G1 — The paid experiment  ·  reports 2026-08-25

**The only gate that can produce evidence nothing else in this engagement can.** Everything else measures
interest; this measures money.

**Test:** open a $5 one-time supporter licence on Polar or Lemon Squeezy (this bypasses the missing
payment rail entirely — see below). Announce it once to the 78 stargazers, the plugin directories, and
nowhere else. Count for 14 days. Cost: one afternoon.

| Threshold | Reading |
|---|---|
| **≥ 25 payers** | **GO.** Falsifies the assumption carrying ~100% of the realistic pool. Reopen commercial work. |
| 5–24 payers | Ambiguous. Extend 14 days, do not build. |
| **≤ 4 payers** | **STOP the commercial track.** Proceed to the portfolio/consulting track (G4). |

**Both thresholds are printed above deliberately.** Quoting only the stop criterion is the sin this
posture exists to avoid.

**Current value: not run. 0 payers, 0 attempts.**

**Why $5 and why one-time:** the nearest sourced anchor is Pushover's $4.99 one-time licence `[PAGE]` —
and that is an *upper* bound, since Pushover operates a hosted delivery network while echook is MIT and
entirely local. A subscription against a set-once utility is a pricing model fighting the customer's
behaviour.

---

## G2 — Usage instrumentation  ·  reports 2026-08-18

**Currently unevaluable, and that is the finding.** No gate that depends on a funnel number can be
assessed, because no funnel number exists or has ever existed.

**Test:** ship opt-in anonymous telemetry, or a one-command `audio-hooks report` that a user can
voluntarily send. The local NDJSON event log (`hook_runner.py:70-73`, schema `audio-hooks.v1`) already
records the right events — **it has no return path.**

| Metric | Threshold | Current |
|---|---|---|
| Instrumentation shipped | yes/no | **NO** |
| Distinct machines firing a hook in a 7-day window | ≥ 100 | **UNKNOWN — cannot be measured** |
| Median hooks/machine/week (is it *used* or just installed?) | ≥ 20 | **UNKNOWN** |
| Machines still firing 28 days after first seen (retention) | ≥ 40% | **UNKNOWN** |

**Do not substitute clone counts for any row above.** 78 unique cloners against 85 unique viewers is a
92% ratio no human population produces; the number is contaminated by machines to an unknown degree
(cross-report correction C8).

---

## G3 — Demand direction  ·  reports monthly, next 2026-09-01

Does anyone want this *more* over time?

| Metric | GO threshold | STOP threshold | Current (2026-08-04) |
|---|---|---|---|
| New stars/month | ≥ 25 and rising | ≤ 5 for 3 consecutive months | **4** (Jul); Jun 9, May 12 |
| Non-network issues opened/month | ≥ 3 | 0 for 3 months | **0** since 2026-05-10 |
| External PRs merged/quarter | ≥ 1 | 0 for 2 quarters | **0** in the last 2 quarters |
| Any unsolicited external write-up | ≥ 1/quarter | 0 for 2 quarters | **0 found** |

**Two of four rows are already at their STOP threshold** and a third reaches it on 2026-09-01 if August
lands ≤ 5. This table is the instrument that says the commercial answer is likely already decided.

---

## G4 — The maintainer track  ·  reports 2026-09-04

The lane with a sourced price **50–250× the entire product pool**, and the only one currently unmeasured
rather than measured-at-zero.

**Test:** replace the bare `mailto:` in the README's "Need a custom app like this one?" pitch with a
tracked link; publish one technical write-up of a genuinely hard thing solved here (cross-harness hook
normalization, or the width-aware status-line reflow); measure inbound over 30 days. Cost: ~1 hour + one
piece of writing.

| Metric | Threshold | Current |
|---|---|---|
| Tracked inbound clicks on the hire pitch | ≥ 20/month | **UNKNOWN — untracked, the pitch is already shipped** |
| Qualified inbound conversations | ≥ 1/quarter | **0 recorded** |

**Anchor:** Clutch puts custom project work at **$10,000–$49,000** `[PAGE]`. One engagement exceeds the
entire realistic product pool by two orders of magnitude.

---

## The whole table, read together

| Gate | Reports | Status |
|---|---|---|
| G1 paid experiment | 2026-08-25 | **not run** |
| G2 instrumentation | 2026-08-18 | **not built — everything downstream unevaluable** |
| G3 demand direction | monthly | **2 of 4 rows at STOP** |
| G4 maintainer track | 2026-09-04 | **shipped but unmeasured** |

**Reading as of 2026-08-04:** the commercial track has one unrun cheap test (G1) standing between it and
a stop decision, and the demand instrument (G3) is already pointing at stop. The maintainer track (G4)
is the only lane that is unmeasured rather than measured-at-zero, and it has the highest sourced price
in the engagement.

---

## What would prove this instrument wrong

These gates are decision aids, not autopilots. Ways they are miscalibrated:

1. **G1's threshold may be far too high for a 78-star repo.** 25 payers from 78 stargazers is a 32%
   conversion — wildly above any plausible rate. It is set high **on purpose**: the question is not "can
   this earn pocket money" but "is there a business," and 5 payers × $5 is not a business at any
   conversion rate. If the goal changes from "a business" to "does anyone value this at all", the
   correct threshold is ~5 and the gate must be rewritten in a dated decision record, not adjusted
   quietly.
2. **G3 measures GitHub stars, which measure interest in a post, not demand for a product.** A tool with
   flat stars and 5,000 happy daily users would fail G3 and deserve to pass. **This is exactly why G2
   exists**, and why G2 being unbuildable-so-far is the most consequential zero in the document.
3. **The 14-day window in G1 is short** for an audience that checks GitHub occasionally. A null result
   at 14 days is weaker evidence than a null result at 60.
4. **Every threshold here was set by an outside analyst, not the owner.** The owner's own answer to
   "what would make you stop" was never recorded — the engagement had no live intake. If the owner's
   real threshold differs, these numbers are the wrong instrument and should be replaced, in writing,
   before the next reading.
