# Narrative and positioning

Turning research into the documents that get used: a positioning statement, a messaging
library with a banned-claims list, a narrative, an objection pack, a deck outline, and the
claim ledger that holds them all to account.

- [Positioning](#positioning)
- [Messaging library and banned claims](#messaging-library-and-banned-claims)
- [The narrative](#the-narrative)
- [Objection pack](#objection-pack)
- [Deck outline](#deck-outline)
- [Claim ledger](#claim-ledger)

---

## Positioning

`strategy/positioning.md` is a **living** document and the single source of truth: if a claim
is not supported here, it does not ship anywhere. Put that sentence at the top.

Open with the status: **positioning is a hypothesis under test, not a settled truth.** Name the
date and the evidence that would falsify it. This framing is what keeps copy falsifiable rather
than assuming the win, and it is what makes the document survive contact with a market that
disagrees.

**The statement**, in outcome language:

> **For** \<the person, described by their situation, not a demographic\>
> **\<Product\>** is \<the category they already understand\> that \<the outcome they get\>
> **Unlike** \<the specific alternative they would otherwise use\>, \<the difference, stated as
> something they would notice\>
> **You pay** \<when, and why that matches how they buy\>

Write the mechanism *last* and in outcome language, or leave it out. Buyers do not buy
architectures. If the differentiator can only be stated as a mechanism, it is not yet a
differentiator — it is an implementation detail waiting for a benefit.

**Then, in the same file:**

**The corrected moat** — what the research actually left standing, written as a heading, with
the refuted version named and struck. The most common shape: the claimed moat is table stakes
for the market leader, and what survives is a narrower quality-or-trust claim that is harder to
sell and genuinely defensible. Mark it **provisional** if buyers have not yet been observed
valuing it — and say plainly that copy must treat it as "here is the difference; you tell us if
it matters," not as established fact.

**The clock on the moat.** Any advantage a funded competitor could bolt on in two quarters is a
lead, not a moat. Say which it is. A document that calls a lead a moat is wrong in a way that
will be discovered.

**The messaging do-NOTs**, each with its evidence. Three that recur:

1. **Do not sell the mechanism to the audience that buys the outcome.** Whole companies have
   spent years and millions evangelizing "X as code" and then told their own users nobody needs
   to touch it. The mechanism can be front-and-centre for a *different* audience in a different
   room — a developer funnel alongside a consumer one — but the two pitches never mix.
2. **Do not lead with the technology label in communities that resent it.** Check the actual
   rules of the venues in `channels.json`; many ban promotion, market research, or AI-tool posts
   outright, and professionals in adjacent trades often read the pitch as a livelihood threat.
   Lead with the help, not the machinery.
3. **Do not overclaim on the consequential outcome** — permits, compliance, safety, legality,
   guaranteed results. Write the honest verbatim answer once and reuse it exactly.

**Elevator pitches, one per audience, kept separate.** Different audiences want different
things and the wrong pitch in the wrong room backfires. Note explicitly if two products or
audiences must not be launched in the same post.

**Objection-handling table** — the objection *as the buyer actually says it*, the honest
response, and the evidence path. Where an objection concedes a real disadvantage, concede it in
the answer: "true today, and we won't pretend otherwise" followed by the deliberate bet, is
more persuasive than a deflection, and it is the only version that survives the buyer checking.

**What would change this positioning** — the closing section. Three to five specific
observations, each with what it would force.

---

## Messaging library and banned claims

`marketing/copy/messaging-library.md` is the reusable copy bank: approved taglines, one-liners
per audience, boilerplate, and the **verbatim-locked answers** for the questions where
improvisation is dangerous (the honest limitation answer, the pricing-model answer, the
competitor-comparison lines). Verbatim-locked means: use exactly this wording, do not
paraphrase — because each was written to be defensible to the word.

**Approved competitive-comparison sentences** get their own section, and the rule beside them:
each is exactly what the research supports and no more, framed as "here is the difference, you
decide," never as a proven verdict.

**The banned-claims list** is the most valuable part of the file. Every claim the research
refuted, numbered, with its refutation in one clause. Typical entries:

1. The differentiator the market leader also has. *False for the market leader; it is table
   stakes.*
2. A specific competitor figure that turned out to be wrong. *Refuted — don't cite it even to
   contrast.*
3. Any overclaim on the regulated or consequential outcome.
4. Mechanism jargon aimed at the outcome-buying audience.
5. "Replaces \<the professional\>" — the honest job is usually to shrink that spend, not
   eliminate it.
6. An unproven assumption stated as established fact.
7. Hype vocabulary — "revolutionary", "game-changing", "the future of", "10x". Unfalsifiable
   everywhere and actively downvote-bait in technical communities.

Enforce the list by **shape, not wording**. A banned "only" claim returns as "the one property
nothing else in this field has," which is the same claim under paraphrase and slips past a grep
for the literal word. When you review copy, look for the *move*: an exclusivity assertion, a
superlative, a capability promise beyond what was demonstrated.

---

## The narrative

The long-form document (`investor/narrative.md` or its equivalent — a founder story, a Show HN
post, a pitch). Sequencing is the whole technique.

**Weakness-first sequencing.** Order the sections: what it is → what it buys → **what we do not
know** → then the market and the ask. The instinct is to put the unknowns at the end where they
do least damage. That instinct is wrong: a reader who meets the concessions early reads
everything after them as credible, and a reader who meets them late feels they were being
managed. The reading order *is* the argument.

**Status gate at the top.** If the document is not ready to be sent — because the evidence it
would be judged on does not exist yet — say so in the first paragraph, with the date and the
condition. "Not for sending before \<gate\>; until then this is for design-partner
conversations where the ask is a pilot, not a check" is a legitimate and common state for a
narrative to be in, and writing it down prevents the document leaking into the wrong room.

**Sections that earn their place:**

- **The thesis**, in one sentence a reader can repeat.
- **What it is and what it is not** — scope stated before any claim, so no reader has to guess
  what is being claimed.
- **What the thing buys** that is not attributable to something else. Isolate the contribution:
  if part of the value comes from a component anyone can buy, measure the rest separately and
  say how.
- **What we do not know yet** — the honest unknowns, each with the observation that would
  resolve it.
- **Where the case lives** — the conditions, with the closed lanes marked closed and the
  unresearched ones marked unresearched.
- **Competition, honestly mapped** — including the players who do parts of this better.
- **The strongest argument against**, written at full strength, in the opponent's voice, before
  any answer. If your answer is incomplete, say which part is unanswered.
- **What would end this** — the kill list, in the user's own words.
- **Claim ledger appendix.**

**Never fuse two separately-sourced facts.** Two true numbers about different windows or
different measurements, joined into one sentence, produce a false number. Keep them in separate
sentences and say explicitly that they are separate measurements. A skeptic checking the more
striking version will find the arithmetic does not work and will stop reading.

**Never state a law from n=1.** "The curve bends up when X happens" derived from one observed
instance is an anecdote. Offer it as "the one instance we have, observed after the fact, not a
law ours will follow."

---

## Objection pack

One document, one section per objection, grouped by theme (thesis / market / moat / evidence /
product / founder / diligence). Aim for 25–40 — the count matters, because the exercise of
reaching 35 forces you past the comfortable ones.

Each entry:

```
### N. "<the objection in the skeptic's own voice, verbatim and harsh>"

**Response.** <honest answer; concede what is true first>

**Evidence.** <file path or URL>

**Status: answered | partially answered | unresolved** <with a named falsifier, and how
often it is re-tested>
```

Write the objection at full hostility. A softened objection produces a softened answer that
will not survive the real version. And leave the genuinely unresolved ones marked
`unresolved` — an honest unresolved with a named falsifier is stronger than a manufactured
answer, because the manufactured one will be tested and fail in the room.

The red-team pass (`red-team.md`) generates new objections; every kill-memo question that the
pack does not already cover becomes a new numbered entry, marked with its honest status.

---

## Deck outline

Not slides — an outline where each slide carries four things:

- **Assertion** — the single sentence the slide makes.
- **On the slide** — the minimum content, with the numbers.
- **Visual** — real output, never a mock.
- **Speaker note** — what is said out loud, including the concession said *in the same breath*
  as the claim it qualifies.
- **Preempts** — the question this slide answers before it is asked.

Two structural rules learned the hard way:

**Put the unknowns slide before the market slides.** Same weakness-first logic as the narrative.

**An unsized box is the most valuable box on the slide.** If one lane is quantified and another
is not, the reader fills the empty one with their own optimism, and you have accidentally led
with your least-evidenced claim. Either size it or take it off the slide and keep it in the
long-form document with its status stated.

**Print the good threshold beside the bad one.** If the deck quotes the stop criterion verbatim
it must also quote the go criterion, and compare current numbers to both. Quoting only one
direction is the exact sin the honesty posture exists to avoid.

---

## Claim ledger

An appendix table on every external-facing deliverable. Use `assets/claim-ledger-template.md`.

| Claim | Source | Verified |
|---|---|---|
| the number or assertion, as stated in the document | URL, or repository path for internal facts | ISO date |

Rules that make it work:

- **Build it while writing, not afterwards.** A ledger assembled at the end is an exercise in
  finding sources for claims already committed to, which is how unsourced claims get
  rationalized instead of deleted.
- **An unsourced claim is deleted, not softened.** Softening ("roughly", "we believe") keeps an
  unchecked assertion in circulation with a hedge attached. Delete it, or go source it.
- **Every externally checkable number gets a row.** If a slide carries five numbers and the
  ledger has none for it, the ledger's own closing rule has been violated — spot-check for
  exactly this before shipping.
- **Stale claims carry `[last verified YYYY-MM-DD]` inline**, at the point of use, not only in
  the appendix. A measurement taken against a version of the product that has since changed nine
  times is stale by the user's own rules; disclose it where it is read.
- **When two of your own reports disagree on a number, do not silently take the larger.** Note
  the disagreement in the ledger row. The disagreement is a finding.
- **Supersede explicitly.** When a new report replaces a number, the ledger row says so:
  *supersedes the figure in \<older report\>*. This is how a living document stays trustworthy
  while its inputs change.

Spot-check the ledger before any deliverable ships: pick a dozen rows at random and re-verify
them. In a real engagement, 15 of 18 spot-checked rows were exact — and the three failures
were a fused pair of facts, a disagreement between two reports resolved in the flattering
direction, and a slide's worth of numbers with no rows at all. Those are the three failure
shapes to look for.
