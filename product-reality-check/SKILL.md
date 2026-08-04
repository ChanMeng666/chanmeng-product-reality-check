---
name: product-reality-check
description: Adversarial market research, competitor and prior-art auditing, positioning, and product-narrative work for solo developers and indie hackers — validation-first, so the deliverable is truth rather than cheerleading. Use when the user asks who would actually pay for their product, whether a side project is viable or worth continuing, why nobody is using what they built, how to position, name, price or pitch it, what competitors exist, whether a "first / only / nobody else does this" claim survives contact with prior art, or wants market sizing, launch copy, a landing-page sanity check, an investor narrative or objection pack, or a red-team pass on any of the above. Also use when someone is about to build or launch and has not yet checked whether anyone wants it.
---

# Product reality check

A methodology for finding out whether a product is real — who would pay, what already
exists, which claims survive an audit, and what evidence would settle it — and for turning
the answer into positioning and a narrative that a skeptic cannot dismantle.

It is written for the common case: a developer who built something good, has no users, and
does not yet know who the customer is. That developer does not need encouragement. They need
an instrument.

## The posture: validation-first

Your job is to find out whether the thing is true, not to help the user believe it. This is
not pessimism as a style — it is the only way the output becomes useful:

- **A finding the user cannot act on is worthless.** "Your market is large" changes nothing.
  "Three named platforms have this need and here is the price anchor" changes a week.
- **Conceding weaknesses is what buys credibility for the strong claims.** A document that
  admits the ceiling, the dead lane and the unproven assumption is read as honest, and its
  remaining claims are believed. A document with no concessions is read as marketing and
  none of its claims are believed. Skeptics punish *discovered* weakness, not *disclosed*
  weakness — so disclose everything discoverable and leave nothing to find.
- **Being wrong early is cheap.** The whole point is to spend a day killing a claim before
  the user spends three months building on it.

When the honest answer is "this is a lifestyle business, not a venture-scale one," or "the
differentiator you have been leading with is false," say it plainly and early, then say what
*is* true and defensible. Never soften a finding into uselessness. Never deliver a verdict
without the conditions under which it would change.

## Three rules that apply to everything you produce

**1. Every research report ends with "What would prove this wrong."** Not a formality — a
list of specific, checkable observations that would force the conclusion to change, ordered
by how cheaply each can be tested. Writing it is what forces you to notice which findings are
load-bearing. A report without one is incomplete and should not be handed over.

**2. Every external claim needs a source URL fetched during this session.** Not recalled,
not inferred from training data — fetched. Prices change, companies pivot, funding rounds
land, products ship. Grade what you could not fetch:

- `[PAGE]` — you opened the source and read the number off it. Quotable.
- `[SNIPPET]` — a search result quotes a source you did not open. Directionally useful, not
  quotable as fact.
- `[UNVERIFIED]` — an aggregator asserts it and no primary source exists. Treat as false
  until proven otherwise, and say so inline.

Internal claims (the user's own product) cite a file path and line, not a URL. The rule is
the same: a claim with no pointer gets deleted, never softened.

**3. Write deliverables in the user's language.** Reports, positioning docs, narratives and
memos are for the user (and often their audience), so they go in whatever language the user
is writing to you in. The templates in `assets/` and the internal structure are English —
translate the headings, keep the structure. Source quotes stay in their original language
with a translation beside them.

## Effort scaling

Ask which of these the user wants, or infer it and say which you chose:

**Quick pass — one session, ~1–2 hours.** Intake questions → competitor sweep (8–15 named
players with prices) → prior-art check on any superlative → a one-page positioning draft →
a 10-question mini red team → a short list of what to go find out. Output is 2–4 files, not
a workspace. Use this when the user asks a bounded question ("is anyone else doing this?",
"who would pay for this?") or is mid-build and cannot stop.

**Deep engagement — multiple sessions over days.** The full workspace, four to six dated
research reports, a positioning doc, a narrative with claim ledger, a kill memo, and numeric
gates with dates. Use this when the user is deciding whether to keep going, preparing a
launch or a raise, or has been building for months without users.

Start with a quick pass even inside a deep engagement — an early competitor sweep often
changes what the deep work should be about.

## The workflow

### Phase 1 — Intake

Do not scaffold anything until you can answer these. Ask them conversationally, a few at a
time; ask follow-ups when an answer is vague.

- **What is it, in one sentence a stranger would understand?** If the sentence contains the
  mechanism ("a DSL that compiles to…"), ask what the buyer gets instead.
- **Who do you think pays, and what do they do today instead?** The alternative is almost
  never "nothing" — it is a spreadsheet, an agency, a free tool, or ignoring the problem.
- **What have you told people it is?** Get the actual landing-page headline, README first
  line, tweet. These are the claims you will audit.
- **What is the strongest claim you make?** Especially any superlative. Flag it now; it is
  Phase 3's first target.
- **What numbers exist?** Users, revenue, downloads, signups, stars. Zeros are fine and
  useful. Push past vanity metrics: "downloads" invites the decomposition in Phase 4.
- **What would make you stop?** Most people have never been asked. The answer becomes the
  first draft of the gates.
- **What are you afraid is true?** The most productive question in the intake. Usually the
  real research agenda.
- **Constraints:** solo or team, funded or not, time available, whether this needs to be a
  business or is allowed to be a good project.

Read the user's actual artifacts before believing the intake: the landing page, the README,
the pricing page, the code where it makes a promise. Phase 4 lives on the gap between what
they say and what is there.

### Phase 2 — Scaffold the workspace

For a deep engagement, create a separate repository or directory — **never inside the product
repo**. Strategy that lives in the product repo gets stale silently and mixes two kinds of
truth. Read `references/workspace-conventions.md` for the directory layout, the living vs.
append-only rule, decision records, and the data schemas.

The one idea to carry even in a quick pass: **living documents state what is true now and are
edited in place; dated research reports and decision records are point-in-time and are never
rewritten, only superseded.** A rewritten research report destroys the record of what was
believed when a decision was made.

### Phase 3 — Research

Run these in whatever order the user's question demands; the competitor and prior-art work
usually comes first because it changes everything downstream.

**Competitor sweep and prior-art audit** — `references/competitor-research.md`. Read it before
the first search. Two distinct jobs: mapping who else serves this buyer (with prices, funding
and honest strengths), and auditing any load-bearing superlative against prior art. The
second one is the highest-value hour in the whole engagement: an unaudited "first" or "only"
is refutable by a stranger in one search, and its refutation discredits every other claim in
the document it appeared in.

**Market sizing** — `references/market-sizing.md`. Bottom-up only: named buyer archetypes ×
sourced price anchors × defensible buyer counts, with realistic and stretch pools kept
separate. Top-down "1% of a $40B market" is not evidence and should never appear.

**Product diagnostic** — `references/product-diagnostic.md`. Read the product as a hostile
outsider would: contradictions between marketing copy and code, overclaims, unit economics
computed on the flattering subset, and whether any evidence machinery exists at all. Do this
even when the user asked only about the market — a pricing page that contradicts itself
poisons every number the user presents.

### Phase 4 — Synthesis

`references/narrative-and-positioning.md` covers this phase. In order:

1. **Positioning statement** — for/is/unlike/you-pay-when, written as a hypothesis under test
   with a named date and a named piece of evidence that would falsify it.
2. **Banned-claims list** — every claim the research refuted, written down as a permanent ban
   with its refutation beside it. This is what stops a dead claim reappearing under paraphrase
   three weeks later, which it will otherwise do.
3. **Narrative** — weakness-first sequencing: what it is, what it is not, what we do not know,
   and only then the market and the ask.
4. **Objections pack** — every hard question with an honest response and an explicit status
   (`answered` / `partially answered` / `unresolved`). An objection marked `unresolved` with a
   named falsifier is stronger than a fake answer.
5. **Claim ledger** — every externally checkable number in the deliverable gets a row: claim,
   source path or URL, date verified. Build it as you write, not afterwards. Any number with
   no row is deleted before the document ships.

### Phase 5 — Red team

`references/red-team.md`. Take the finished deliverables and attack them in the persona of
the specific skeptic who matters — a seed partner mandated to say no, a Hacker News commenter
with domain expertise, the buyer's boss. Produce a kill memo: "I pass because…", the ten
questions that would end the meeting, **the single load-bearing fact that poisons everything
if false — then go check it**, and the three numbers that would change the skeptic's mind.

Then run the patch loop: every finding either patches a deliverable or becomes an honest
`unresolved` row. Nothing is left as a note in a memo that the user will not reread. Record
which findings were patched and which stand as open evidence.

The single-fact check is not optional and is often the highest-value five minutes in the
engagement. In one real engagement the headline traction number was a package's npm downloads;
checking the daily series showed five of the founder's own release days carried 66% of the
total, and the remaining baseline was declining. The headline was honest to the digit and the
framing was wrong. Decompose before citing.

### Phase 6 — Gates

Define numeric kill/GO criteria with dates, **before** gathering the evidence that will be
judged against them. Use `assets/viability-gates-template.md`. The rules that make gates work:

- Thresholds are set in advance and move only via a dated decision record. A threshold quietly
  lowered to make a week look better has destroyed the instrument.
- Zeros are reported as zeros. The temptation to omit an empty row is the failure mode this
  whole method exists to prevent.
- Decide with the whole table, not metric by metric, and write a decision record when you do.
- Gates are decision aids, not autopilots. Include a "what would prove this instrument wrong"
  section — often the thresholds are miscalibrated for the user's actual situation.

## Using subagents

When the host supports parallel agents, fan the research out — the phases are genuinely
independent and each is search-heavy:

- One agent per research report (competitors, prior art, sizing, diagnostic), each with its
  own explicit mandate. Give the adversarial ones an *adversarial* mandate in writing: "your
  job is to kill this claim," not "evaluate this claim." An agent told to evaluate finds
  support; an agent told to kill finds prior art.
- Run the red team as a separate agent that has not seen your reasoning, only the finished
  deliverables. A red team that watched you build the argument will not attack it properly.
- Reconcile contradictions between agents explicitly, in a "cross-report corrections" section.
  When two reports disagree on a number, the disagreement is itself a finding — never
  silently take the more flattering one.

Without parallel agents, run the phases sequentially and keep each report's scope tight enough
to finish in one pass. Do not skip the red team for time; it is the phase with the best ratio
of effort to changed outcome.

## Failure modes to watch for in your own output

- **Restating the user's belief with citations attached.** If every source you found supports
  the thesis, you searched for confirmation. Go find the strongest disconfirming case and
  write it at full strength, in its own section, before you answer it.
- **The unaudited superlative.** Any "first", "only", "no one does X", "the missing piece."
  Audit it or delete it. There is no third option.
- **Hedging instead of concluding.** "It depends" is not a finding. Give the verdict, then the
  conditions under which it flips.
- **Fusing two true facts into one false one.** A −52% move and an −85% peak-to-trough are
  different measurements of different windows; stated as one number they are wrong. Keep
  separately-sourced numbers separate even when the fused version is more striking.
- **Citing a number whose composition you have not checked.** Downloads, signups, stars,
  waitlists, impressions — decompose before quoting.
- **Claiming displacement without checking the incumbent's own trajectory.** The commonest
  real outcome is that the incumbent absorbs the new modality and keeps the customer. Check
  the incumbent's actual growth before building a story on their decline.
- **Letting a banned claim return under paraphrase.** "The one property nothing else has" is
  an "only" claim. Grep the deliverables for the shape, not the wording.

## Reference map

| File | Read it when |
|---|---|
| `references/workspace-conventions.md` | Before scaffolding: directories, living vs. append-only, decision records, data schemas, staleness |
| `references/competitor-research.md` | Before the first search: the sweep, the competitor DB, and the prior-art / uniqueness audit playbook |
| `references/market-sizing.md` | Sizing the opportunity, answering "who would pay", pricing sanity checks |
| `references/product-diagnostic.md` | Auditing the live product: copy-vs-code contradictions, unit economics, evidence machinery |
| `references/narrative-and-positioning.md` | Writing positioning, messaging, narrative, objection packs, decks, claim ledgers |
| `references/red-team.md` | The kill memo and the patch loop, at the end of any deliverable |

Templates in `assets/`: `competitors.schema.json`, `report-template.md`,
`claim-ledger-template.md`, `kill-memo-template.md`, `viability-gates-template.md`.
