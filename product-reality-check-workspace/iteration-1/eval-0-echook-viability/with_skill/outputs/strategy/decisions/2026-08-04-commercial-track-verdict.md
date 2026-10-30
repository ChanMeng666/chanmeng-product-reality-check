# 2026-08-04 — Stop treating echook as a product business; run one paid test; research the maintainer lane

**Status:** Recommended by the research engagement of 2026-08-04. **Not yet accepted by the owner** —
this record exists so the decision, if taken, has its basis attached. Basis: the five research reports
of 2026-08-04, the kill memo, and the patch record, all in `research/`.

## Trigger

The owner asked: *"I've been building echook for months — MIT, agent-first, v6.x, people seem to like it
but I have zero revenue and no idea whether anyone would pay, who the buyers are, or whether to keep it a
free portfolio piece. Is there a business here?"*

**The proposal as originally framed** — worth recording because it did not survive — was that the answer
would turn on *positioning*: that echook had a real differentiator ("AI-operated, not AI-assisted") which
was being communicated badly, and that the engagement would find the buyer it had been mispitched to.
It did not. The differentiator was table stakes, and the buyer was not found because on this evidence it
does not currently exist.

**A second framing of mine also did not survive**: that orgs locked out of Anthropic's native mobile push
(Bedrock, Vertex, Foundry, gateways, ZDR) were an addressable enterprise lane. It inverted — hooks work on
every provider, so those orgs write their own notifier and are the *least* likely buyers of an unaudited
78-star repo. Sized at $0. See correction C5.

## Decisions

1. **Stop treating echook as a product business.** Do not build features in pursuit of revenue. The
   realistic annual pool is $0–$200 with a median of $0, there is no payment rail in any of the three
   ecosystems, and the donation experiment has already run for nine months with 222 followers and 0
   sponsors.
2. **Run exactly one commercial test before closing the question** — G1 in `viability.md`: a $5 one-time
   licence on Polar/Lemon Squeezy, announced once, counted for 14 days, reporting **2026-08-25**.
   ≥25 payers reopens the commercial track; ≤4 closes it.
3. **Fix the six shipped surfaces** stating a wrong hook count, plus the stale version string and the
   repo description/`homepageUrl`. 23 minutes. This is not cosmetic: the live README currently violates
   six entries on this workspace's own banned-claims list, and a landing page leading with claims the
   owner's own research refuted is the single most damaging class of finding in the method.
4. **Retire permanently** the words banned in `marketing/copy/messaging-library.md` (BC-1 … BC-15),
   including under paraphrase. Enforce by *shape*, not wording.
5. **Do not publish any comparison against Anthropic's mobile push.** Compare against the hook surface or
   not at all — see BC-13 and correction R2.
6. **Research the maintainer/consulting lane properly before acting on it.** It is currently an
   unresearched hypothesis priced off one page of agency data, and this engagement applied a
   40×–100× reachability discount to the lane it killed and none to the lane it recommended.

## The honest status of this decision

**Decision 6 is the weak point and it is the one carrying the recommendation.** The package is better at
killing the product than at establishing the alternative. Nobody was interviewed; every archetype is
reasoned rather than observed; the consulting anchor describes agencies, not solo maintainers.

Decisions 1 and 2 rest on much firmer ground: the absence of a payment rail was the load-bearing fact,
the red team independently verified it byte-for-byte, and it is the best-verified claim in the package.

## Committed follow-up

Check these at the start of the next session. **Unexecuted follow-ups are a finding, not an oversight** —
a decision recorded and never propagated converts a strength into evidence against the owner.

| By | Action | Owner |
|---|---|---|
| 2026-08-11 | The 23-minute README/description fixes shipped | owner |
| 2026-08-11 | One paragraph in `SECURITY.md` explaining GitGuardian #34199726 was synthetic | owner |
| 2026-08-18 | G2: opt-in usage reporting shipped, or formally abandoned with a reason | owner |
| 2026-08-25 | G1 result recorded in `viability.md` — **including if it is zero** | owner |
| 2026-09-04 | G4: tracked link live; one technical write-up published | owner |
| 2026-11-04 | The steelman's expiry: if tests 1–3 have not moved, the "fleets of agents" argument stops being a reason to continue | owner |

## What would reverse this

- **≥25 payers in G1** → decision 1 reverses outright.
- **≥2 of 20 named orgs request a quote** → correction C5 was wrong; the enterprise lane reopens.
- **Telemetry showing ≥100 machines/week firing hooks** → "78 stars" was measuring the wrong thing, and
  every funnel argument reopens. This is the cheapest way to be wrong about all of it, and it is
  currently unmeasurable — which is why decision-adjacent gate G2 matters more than its size suggests.
- **A sound-related Claude Code issue crossing ~40 reactions** → the demand finding, now the
  best-evidenced item in the package, is overturned.
