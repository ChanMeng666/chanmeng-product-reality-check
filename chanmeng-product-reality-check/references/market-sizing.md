# Market sizing and the who-pays question

The question is never "how big is the market." It is **"who specifically would move money,
how much, and what does that sum to."** Sizing done any other way produces a number nobody
can act on and no skeptic believes.

## The rule: bottom-up only

Top-down sizing — "the industry is $40B, we need 0.1%" — is not evidence. It is arithmetic
performed on someone else's press release, it can be made to produce any answer, and every
experienced reader discounts it to zero on sight. It also teaches the user nothing: no action
follows from a TAM.

Bottom-up sizing is:

> **named buyer archetype × sourced price anchor × defensible buyer count**, summed, with
> realistic and stretch pools kept separate.

Every one of those three inputs is checkable, and each one is a place where the answer can
turn out to be "nobody."

## Building the archetypes

Three to five archetypes is right. More and they overlap; fewer and you have not decomposed.
Each is a *kind of organization or person with a budget*, not a market segment label. "Small
businesses" is not an archetype. "Listing platforms that need programmatic floor plans" is.

For each, write:

**Who** — named example companies. If you cannot name five real ones, the archetype is
imaginary and should be deleted or merged. Naming them also produces the outreach list, which
is the point: an archetype you cannot name is an archetype you cannot go ask.

**Price anchor `[PAGE]`** — what does something comparable actually cost, from a pricing page
fetched this session? Anchors from adjacent categories are fine and often the only ones
available; label the analogy. If no comparable price exists anywhere, that absence is itself
the headline finding: *no third-party licensing deal of this shape was found to exist* is a
far stronger sentence than a made-up ACV.

**Buyer count `[estimate]`** — how many such organizations exist, and how many are *reachable
by this user*. Keep those two numbers separate. An unknown solo maintainer reaches a different
fraction of a market than an incumbent with a sales team, and conflating them is where sizing
usually inflates by 10×.

**Realistic ACV `[estimate]`** — with the reasoning visible. An engine license is worth less
than a hosted service at the same nominal scope because it carries no hosting, no data, no
SLA and no support. Discount for what the user does not provide, and say what you discounted.

**Realistic pool** = reachable buyers × realistic ACV. **Stretch pool** = whole archetype ×
optimistic ACV, explicitly labelled as the whole industry across all vendors, not the user's.

**Adversarial note** — the strongest reason this archetype does not pay. Every archetype gets
one. If you cannot write it, you have not looked hard enough.

## The arithmetic honesty rules

- **Never quote a capture percentage against the wrong pool.** "We capture 2–10%" reads as
  modest against the stretch pool and as absurd against the realistic one. Present one coherent
  formulation, and state which pool the percentage is of, in the same sentence.
- **Sum the realistic pools; report the stretch separately.** Never add the two.
- **State the volume ceiling where one exists.** Some products are structurally unable to reach
  metered scale. If the entire addressable activity happens 200,000 times a year worldwide, a
  per-call pricing model has a hard ceiling in the low hundreds of thousands of dollars no
  matter how the market develops — and that arithmetic, done once, kills a whole pricing
  strategy before anyone builds the billing for it.
- **A free substitute that is the same software caps the price.** If the product is open source
  or trivially reproducible, the buyer can decline to pay and still have it. Say so in the ACV
  reasoning rather than discovering it in a sales call.

## Base rates: what happened to the people who already tried this

The single most persuasive section in a sizing report is usually not the arithmetic — it is the
base rate. Find the two or three companies that already pursued this exact thesis, and report
what they raised and what they are worth now.

If the best-credentialed teams in the category, founded years ago, with the right pedigree,
have raised single-digit millions and are still small, that is the category's base rate, and it
is a stronger signal than any bottom-up sum. Report it plainly. Then look for the variable that
has changed since they started — if there is one, it is the actual thesis; if there is not, the
verdict is written.

Also check the other side: is there any example of the *owner* of this kind of thing capturing
a large outcome? A widely-adopted open format whose maintainer is a small seed-stage company
four years in is evidence that adoption and capture are close to independent events. A pitch
that conflates "this becomes standard" with "this is a big company" is conflating two things
the evidence says are separate.

## The honest verdict section

Every sizing report ends with a verdict stated in one sentence, before the reasoning:

> **"No — not as stated. This is a $X–Y ARR business, which is a good outcome and not the one
> a venture round is priced for."**

Then:

**The conditions under which the answer changes.** A "no" without conditions is not useful.
Name each condition (C1, C2, …) precisely enough that the user can go test it, mark which
require becoming a materially different company, and mark which are unresearched. Then present
them honestly:

- An unresearched condition is a **hypothesis**, and it must be labelled as one everywhere it
  appears. The most common failure is an unsized lane presented in the same visual weight as a
  sized one — an unsized box on a slide reads as the most valuable box on the slide, because
  the reader fills it in with their own optimism. Either size it or remove it from the
  presentation and keep it in the long-form document with its status stated.
- A condition whose named falsifier has already fired is **falsified**, and should be marked
  so rather than left standing.

**What this report does not say.** Include this. "This is not venture-scale" is routinely
misread as "this is a bad project," and the two are unrelated. If the comps show that a
technically excellent product in a rare category can build a $1–2.5M ARR business, that is a
good life and a real company; the harm is only in pricing a raise as if it were something else.
Say that explicitly, because the user will otherwise hear the verdict as a judgment of their
work.

**What would prove this wrong**, ordered by cost to test, each written as a specific observation
with a method:

1. *Prove-wrong signal* — the concrete thing that would have to be observed.
2. *Why it decides things* — which finding it overturns.
3. *How to test* — the actual next action, in days not dollars. "Approach 20 named targets with
   a concrete offer, not a survey" is a test. "Do more research" is not.

Mark which items, landing together, would overturn the verdict rather than merely dent it.

**The steelman you could not refute.** Every sizing of an emerging category has one: *all of
this measures a pre-existing world, and if the workflow becomes default within two years the
buyer counts are backward-looking by construction.* Write it at full strength. Then note why it
is not sufficient on its own — it is unfalsifiable in the present tense, which is exactly why
the dated tests above exist. **The correct posture toward an unfalsifiable steelman is not to
reject it but to date it:** if the cheap tests have not moved within two quarters, the market
is not being created on the timeline the argument assumes.

**Open gaps.** The price anchors you could not reach, the vendors whose sites blocked the
fetcher, the archetypes you could not verify. List them, and mark the highest-value one. Any
number in the report that a gap makes soft must be labelled soft where it is used, not only
where it is confessed.

## When the answer is "nobody, yet"

Sometimes the honest finding is that no one currently pays for this in any form. That is a
result, not a failure of research, and it is far more useful than an invented number. Report it
as: the pools that exist adjacent to it, the reason the direct pool is empty (no payment rail,
no precedent, a free substitute, a volume floor), and which of those reasons is time-sensitive
by construction versus structural. A missing payment rail is a statement about this quarter. A
volume ceiling is a law. Distinguishing them tells the user whether to wait or to change.

## Pricing sanity checks

When the user asks about pricing rather than sizing, the same discipline applies at smaller
scale:

- **What does the buyer pay today** for the thing they would stop doing? That is the ceiling.
- **What is the cheapest adequate alternative**, including free and including "keep doing it
  by hand"? That is the floor, and it is often zero.
- **Does the billing model match the buying rhythm?** A subscription against a once-in-a-decade
  purchase, or a per-call meter against a workload that happens twice a month, is a pricing
  model fighting the customer's actual behaviour. Check the review pages of subscription
  competitors — auto-renewal complaints are a reliable, free signal about a mismatch.
- **Compute the margin fully loaded**, not on the billed event alone. See
  `product-diagnostic.md`; this is where most indie unit economics are wrong.
