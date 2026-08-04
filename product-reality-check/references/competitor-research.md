# Competitor research and the prior-art audit

Two separate jobs that get confused. The **sweep** maps who else serves this buyer. The
**uniqueness audit** tests whether a specific claim of novelty survives. Do the sweep for
positioning; do the audit before any superlative is allowed to carry weight.

- [Part 1 — The competitor sweep](#part-1--the-competitor-sweep)
- [Part 2 — The prior-art / uniqueness audit](#part-2--the-prior-art--uniqueness-audit)
- [Part 3 — Watching for change](#part-3--watching-for-change)

---

## Part 1 — The competitor sweep

### Find them in four rings

Search each ring separately; people habitually search only the first and miss the ones that
matter.

1. **Direct** — same buyer, same job, same shape of product. Usually 3–8 named players. The
   user already knows most of these.
2. **Adjacent up-market and down-market** — the professional tool the user's buyer graduates
   to, and the free/consumer thing they use instead. Down-market is where "why would I pay"
   actually comes from.
3. **The substitute that is not a product** — a spreadsheet, an agency, a freelancer, a
   Fiverr gig, doing it by hand, or doing nothing. Price these. "They currently pay a
   contractor $1,750" is the single most useful number in a positioning doc.
4. **The platform that could absorb this as a feature** — the incumbent whose customer the
   user is trying to take, and the general-purpose tool (a frontier model, a big SaaS) that
   might ship this next quarter. This ring produces the scariest and most important finding.

Sources that repay the time: the vendors' own pricing pages (always fetch, never recall),
their changelogs and status pages, funding databases, app-store and marketplace review pages
(the one-star reviews are the best product research available anywhere), the communities in
`channels.json`, and — for developer tools — package registries, dependent counts, and
GitHub activity.

### Record each one

Fill `data/competitors.json` against `assets/competitors.schema.json`. What matters:

- **Prices, fetched this session, with the URL.** Price is the fastest-rotting fact in the
  file and the one every downstream argument uses.
- **Strengths written honestly.** A competitor entry that lists only weaknesses is a tell that
  the research was performed to reassure. If the market leader does something better, that
  sentence is what makes the rest of the file trustworthy.
- **`positioning_vs_you`** — one sentence naming the actual difference *as a buyer would
  experience it*, not as the user's architecture describes it. "Ours is deterministic" is a
  mechanism; "theirs produces a file the builder can't open" is a difference.
- **`kills_your_moat`** — an explicit boolean-plus-explanation: does this player's existence
  refute the user's central differentiating claim? Answer it per competitor, in the file.
  This is the field that turns a competitor list into a decision.
- **`threat_level`** — high/medium/low, justified by trajectory, not by current size.

### The correction that comes out of a good sweep

The most common outcome is that the user's headline differentiator is **already table stakes**
for the market leader. Whatever the user says makes them different, check whether the biggest
competitor already ships it. In one real engagement the founder's entire moat was "we export
CAD files, they export pictures" — and the market leader, with a million users, already
exported three CAD formats. The moat had to move up a layer to something narrower and true.

When this happens, do not soften it. Write the refutation as a heading, name what is left,
and put the dead claim on the banned-claims list the same day. The narrower surviving claim
is usually harder to sell and genuinely defensible, which is a better position than a wide
claim that dies in the first conversation with someone who knows the market.

### Check the incumbent's own trajectory before claiming displacement

Before writing any story in which the user rises as an incumbent falls, fetch the incumbent's
actual numbers. The default outcome in software is not displacement — it is that **the
incumbent absorbs the new modality and keeps the customer.** When design tools were widely
declared dead at the hands of AI code generators, the leading design tool grew revenue 46%
year over year, accelerating, with 139% net retention, while shipping its own generator that
became a weekly habit for most of its largest accounts. The stock fell 52% in the same window
— which is why the story felt true.

So: separate the market's *sentiment* about an incumbent from the incumbent's *results*. Both
are real findings and they point in different directions. The honest version of the analogy is
almost never "X was displaced"; it is "the artifact X owned lost its monopoly on being the
thing downstream work starts from" — a narrower claim that survives the numbers.

---

## Part 2 — The prior-art / uniqueness audit

Run this whenever a claim of the shape **"first" / "only" / "no one does X" / "the missing
piece" / "nobody has built"** is load-bearing — meaning something else in the deliverable
depends on it being true.

The reason this is urgent: these claims are the cheapest to check and the most expensive to
be caught on. A skeptic refutes "first" with one search, and the refutation does not just
remove that claim — it makes every other number in the document suspect, because the user has
now demonstrated they assert things they did not check.

### Method

**Step 1 — Split the claim into its distinctions.** A superlative usually collapses two or
three different things. Write them out separately; most of the audit's value appears here. In
one engagement the claim "there is no checkable text format for building design" collapsed
three distinctions: interchange formats vs. *authoring* formats (does a person write it first,
or does a tool emit it and nobody reads it?), checking vs. authoring (a linter is not a
language), and models vs. drawings. Once split, two of the three were plainly refuted and the
third became a precise, survivable claim.

**Step 2 — Search five categories, not one.** Each of these has killed a "first" claim:

- **Adjacent categories** — the same idea aimed at a different domain. Whoever built this for
  a neighbouring industry counts as prior art to a skeptic.
- **Historical work** — the 1970s–90s. Many "new" ideas in tooling have a research-lab
  ancestor with a paper and sometimes a shipped product. Search the academic archives and old
  conference proceedings, not just the web.
- **Academic work** — recent papers, benchmarks and datasets. Also the best source of
  *supporting* evidence: a benchmark showing the state of the art failing at this task is a
  stronger argument for the user's product than any claim of novelty.
- **Dormant twins** — abandoned repos, single-star packages, weekend projects, a plugin in a
  niche ecosystem's package registry. Search package registries and code hosts directly with
  the plainest possible description of the product. These are what a skeptic finds.
- **Standards bodies and the industry's declared roadmap** — if a standards group has an
  in-progress spec pointed at exactly the user's insight, "unclaimed insight" is false, and
  the honest framing becomes "the industry agrees; here is why nobody has shipped it."

**Step 3 — Grade each item against the claim.** Refutes "first" / refutes "only" / partially
refutes / does not refute (and several will actively *support* the claim — record those, they
are the citations the narrative actually needs). Note each item's adoption: stars, downloads,
last commit, whether it ever shipped. Adoption is what separates "this claim is dead" from
"this claim needs a different adjective."

**Step 4 — Write the most defensible version of the claim.** Usually a conjunction of three
to five clauses. Then add the honest caveat *in the report*: a five-clause conjunction is
gerrymandered and a hostile reviewer will say so. Hold it as the precision fallback under
questioning; never open with it.

**Step 5 — Find the arguments that need neither "first" nor "only".** This is the point of the
whole exercise. Superlatives are load-bearing only because the real argument has not been
found yet. Two shapes that recur:

- **Source of truth.** Everywhere else in the field, the artifact is a side effect of a tool;
  here the artifact *is* the thing. This survives any amount of prior art because it is a
  property, not a priority claim.
- **The variable that changed.** Someone tried this before and the market rejected it — find
  out *why*, and check whether that reason still holds. If a textual authoring tool lost to a
  visual one because its intended author was a human who preferred dragging boxes, and the
  intended author is now a model that cannot drag anything, the prior failure is a market-risk
  datum rather than a technical refutation. Say both halves.

**Step 6 — Reframe convergent invention as evidence.** Three abandoned twins do not mean the
idea is worthless. They mean several capable people independently saw the same gap — which is
evidence the gap is real — and stopped. **"Several people had this idea and stopped; we are
the one still here and complete enough to use"** is true, checkable, and a better story than
a false "first." Support it with the comparison numbers: their downloads and last commit
against the user's.

### Mandatory outputs

- **Retractions**, stated unconditionally: exactly which words are now banned, and by what
  evidence. These go straight into the banned-claims list and a decision record.
- **Banned citations** — self-referential "proof of novelty" that must never be used. The
  classic: "a search for our exact description returns only us." A search phrased in the
  user's own vocabulary is not independent evidence of anything.
- **The counterexamples a knowledgeable skeptic will throw**, with the concession and the hold
  for each. Concede the leg that is genuinely occupied; hold the leg that is not. Someone who
  knows the field will name two or three specific prior systems — write those answers before
  the meeting, not during it.
- **Explicitly unresolved** — the items you could not verify this session, named. A skeptic
  who finds an unchecked competitor you did not mention concludes you were hiding it; one who
  reads "we could not reach this vendor's site, this is unchecked" concludes you were careful.

---

## Part 3 — Watching for change

The audit is a snapshot with a short shelf life. Write the watch list into the report's
"what would prove this wrong" section as specific, dated triggers:

- **The nearest twin gains real adoption.** Set a number ("crosses ~500 downloads/month",
  "reaches the package registry", "passes 50 stars"). Check monthly.
- **The incumbent or a standards body ships the missing leg.** Name which product, which leg,
  and where you would see it — a changelog, a release page, an open issue.
- **A distributed general-purpose tool ships this as a feature.** Distribution beats depth; an
  open issue on a widely-installed tool proposing exactly the user's feature is a live threat
  worth a quarterly check with the issue number recorded.
- **A benchmark appears that measures the quality the user claims to provide.** Its arrival is
  the clearest signal the field has caught up — and, until then, its absence is a citable
  argument that the problem is unsolved.
- **A funded company ships the authoring/creation layer** the user believes is missing. Name
  the two or three most probable candidates and where their announcements appear.

Assign each a cadence (monthly / quarterly) and put it in the report. The moat claim most
likely to go stale is always the one everything else rests on — re-verify that one first.
