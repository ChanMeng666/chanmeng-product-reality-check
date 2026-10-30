# Positioning — gradient-svg-generator

**Date:** 2026-08-04 · **Status:** LIVING document — edit in place, never append changelog prose
**If a claim is not supported in this document, it does not ship anywhere.**

> **Positioning is a hypothesis under test, not a settled truth.** This draft is falsifiable by a
> single observation named at the bottom, and it rests on evidence collected on 2026-08-04. Re-test
> the moat clause first — it is the one everything else leans on.

---

## The situation this positioning has to survive

Stated plainly, because copy written in denial of it will not work:

- **9 third-party accounts** embed this product. capsule-render is embedded in **44,032** files.
- **6 GitHub stars** against capsule-render's 1,790 and readme-typing-svg's 9,168.
- The product is **genuinely better on inventory** (186 distinct effects vs 15) and **genuinely
  different on behaviour** (animated vs static-by-default).
- **The market has already demonstrated it does not rank on inventory.**

So the job of this positioning is **not** to argue superiority. It is to give someone a reason to try
it in the five seconds they spend looking, on the one axis a reader can verify instantly.

---

## The statement

> **For** the developer who has just finished a project, is looking at a plain README, and wants it to
> look like someone cared — without opening a design tool or committing an image
>
> **Gradient SVG Generator** is a **banner you embed as a single URL** — paste one line of Markdown and
> your README header is a moving gradient with your text on it
>
> **Unlike** capsule-render, the banner everyone already uses, this one has **168 distinct animated
> effects** where capsule-render has 15 types — so yours doesn't look like the other 44,000
>
> **You pay** nothing, ever. It is MIT-licensed and you can host it yourself if you'd rather not
> depend on someone else's URL.

**Why the last line is in the positioning and not hidden:** "you can self-host it" is the honest answer
to the objection that kills embed-a-URL products ("what if it disappears?"). Volunteering it converts
this product's biggest structural weakness — an unfunded solo dependency — into a statement of
confidence. It also happens to be true and checkable.

---

## The corrected moat

### ~~"The largest animated README banner collection"~~ — **retired before it ever shipped**

Not retired because it is false. Retired because:

1. **It is unverifiable by the reader.** Nobody can enumerate every banner collection, so the claim
   cannot be confirmed — only attacked.
2. **It invites the counting audit**, which has a real finding waiting in it: **70 of the 355 templates
   (20%) are colour-palette presets**, not bespoke animations.
3. **It stakes the pitch on the axis the market ignores.** capsule-render has 12× fewer effects and
   ~489× more adoption. Winning "largest" wins nothing.

*(The claim was never shipped — the live site says "340+ Templates / 180+ Gradient Types", which is
accurate and conservative. This is a decision made at the cheapest possible moment: before publication.)*

### What survives — the moat, corrected 2026-08-04 after red team

> ⚠️ **The first version of this moat had two clauses and BOTH were false. Corrected below.** The
> original read: *"It moves, and there are 186 distinct effects behind it."* Retained here struck
> through, because the record of what was believed is worth as much as the correction.

**~~"It moves" — as a category difference~~ — REFUTED.** I claimed capsule-render was "static SVG by
default". Verified against its live API on 2026-08-04 by counting `repeatCount="indefinite"` elements
in the returned SVG:

| capsule-render type | Looping animation elements |
|---|---|
| `wave` | 0 |
| `venom` | 1 |
| `waving` | 2 |
| `pulse` | 4 |
| `checkered` | 4 |
| `blur` | 6 |

**5 of 6 sampled types ship continuously-looping background animation.** "Static by default" is true
only in the narrowest literal sense (the single default type, `wave`, does not animate). As a *category*
claim it is false. This is a **degree** difference, not a **kind** difference — exactly what the original
draft asserted it was not.

**~~"186 distinct effects"~~ — REFUTED. The real number is 168.** The 186 was a count of
`gradientType` *strings in the registry*. Rendered through the live code path with inputs held constant,
they produce **168 distinct outputs**: 18 strings are aliases collapsing into 6 groups — e.g.
`turbulentWaves == electromagneticWaves == auroraWaves == soundWaves == cryogenicWaves == solarWaves`
render byte-identically. Several are annotated in the source itself as *暂时复用* ("temporarily reuse").

**The generative error, named so it is not repeated: I audited the manifest, not the artifact.** I
counted registry entries and read a competitor's README instead of rendering either product. Both
corrections took under twenty lines of Node against code sitting on disk.

### The moat that actually survives

> **168 distinct animated effects, against capsule-render's 15 types — a catalogue roughly an order of
> magnitude deeper, in exchange for being the one nobody has heard of.**

One clause, verified by rendering, stated as a trade rather than a win. What is genuinely defensible:

- **168 is still ~11× capsule-render's 15**, and that gap is real design labour, not a counting trick.
- **It is stated with its cost attached** ("the one nobody has heard of"), which is what stops a reader
  from going looking for the catch — there isn't a hidden one anymore.
- **Motion is a reason to prefer it, not a reason it is different in kind.** Both animate. This one
  animates more, and across more of the surface. That is a real but modest claim, and it is the true one.

### The clock on this moat — **it is a lead, not a moat**

Say this plainly rather than discovering it later: **capsule-render could add animated backgrounds in a
weekend.** It is actively maintained (last push 2026-08-04), and its 731 forks mean the community could
do it without the maintainer. There is no technical barrier, no patent, no data advantage, no network
effect protecting any of this.

What is *not* trivially copyable is the **186-effect catalogue** — that is accumulated design labour,
and it is the only thing here with a real cost to reproduce. **Mark provisional:** no buyer has yet
been observed valuing catalogue breadth, and the market evidence (capsule-render winning with 15)
suggests they may not. Copy must treat it as *"here is the difference, you tell me if it matters"* —
never as an established advantage.

---

## Decide the name first — nothing else can ship until this is settled

The product currently ships under **three names simultaneously** (diagnostic F3): "Chromaflow" (live
site, `package.json`), "Gradient SVG Generator" (README H1), and `gradient-svg-generator.vercel.app`
(the URL 90 files embed). `og:url` and the JSON-LD point at `chromaflow.vercel.app` — a live host, but
not the one anyone embeds.

**Recommendation: keep "Gradient SVG Generator". Retire "Chromaflow".**

1. **All 90 existing embeds point at the `gradient-svg-generator` host.** Renaming orphans the only
   distribution that exists.
2. **The name is the search query.** "Gradient SVG generator" is what someone types when they want
   this. "Chromaflow" is what they type when they already know you — and 6 stars says they do not.
3. **A descriptive name is worth more than an evocative one at zero brand equity.** Chromaflow is the
   better *brand* and the worse *name* for a product whose entire discovery path is search and
   copy-paste. It becomes correct at ~10,000 users; it is a liability at 9.

Then: 301 `chromaflow.vercel.app` → the canonical host, and make `og:url` and the JSON-LD agree.

---

## Approved copy

### README first line / site hero — approved (corrected 2026-08-04)

> **Animated gradient banners for your README. One URL, no install.**
> 355 ready-made templates across 168 distinct animated effects — paste one line of Markdown.

*Why this one:* leads with the outcome, names the mechanic ("one URL") that is the actual reason to
choose it, and puts the honest number in the second line where it supports rather than boasts. No
superlative anywhere.

### The comparison line — **REWRITTEN**, verbatim-locked

> ⚠️ **The previous verbatim-locked line was factually false and is retired.** It read: *"capsule-render
> is the one most people use, and it's great — its banners are mostly static. These move."* Verified
> false — 5 of 6 sampled capsule-render types ship looping background animation. **Had this shipped as
> written, the first knowledgeable reader would have refuted it with one curl, and the refutation would
> have discredited every other number in the README.** This is precisely the failure the audit exists
> to prevent, and it very nearly shipped from inside the audit itself.

Use exactly this wording:

> **"capsule-render is the one most people use, and it's good — 15 background types, and several of
> them animate. This one is the same idea with a much bigger catalogue: 168 distinct animated effects.
> If you've used capsule-render and wanted more variety, that's the difference. Same one-URL embed."**

**Do not paraphrase.** Every clause is load-bearing: it concedes the incumbent's position *and its
animation* first, states the difference as a checkable count rather than a ranking, names the specific
person it is for ("used capsule-render and wanted more variety"), and claims nothing that a curl can
refute.

### The honest-limitation answer — verbatim-locked

For "how do I know this won't disappear?":

> **"You don't — it's one person's side project on a free Vercel account. It's MIT-licensed, so if
> that worries you, fork it and deploy your own in about ten minutes; the README shows how. If it goes
> down, your README shows a broken image, same as any embedded badge."**

Concede fully, then hand over the remedy. This is stronger than any uptime promise, and it is the only
version that survives the reader thinking about it for ten seconds.

### The decomposition — **REWRITTEN**, was wrong in the flattering direction

> ⚠️ **The previous version of this paragraph was wrong three ways at once**, and it was the paragraph
> being recommended as the centrepiece of the product's honesty. It read: *"285 use a bespoke animated
> effect; 70 are colour-palette presets over 6 standard gradient types. Behind the 355 are 186 distinct
> rendering effects."* Verified by rendering all 355:
>
> - **"70 are colour presets, not animations" — false.** All 70 animate. `horizontal` emits 4
>   indefinitely-looping `<animate>` elements; `circular` emits 15. The confession confessed to
>   something that is not true.
> - **"186 distinct rendering effects" — false.** 168 (18 aliases).
> - **The genuinely unflattering fact was missed entirely** — see below.
>
> A false confession is worse than no confession: it is checkable, and being caught *understating your
> own product* still proves you did not verify your numbers.

Put this in the README, near the count:

> **355 templates, honestly counted.** Behind them are **168 distinct rendering effects** — 186 named
> `gradientType` values, but 18 of those are aliases that render identically (`solarWaves` and
> `turbulentWaves` are the same effect under two names). Nearly everything animates: **11 templates
> have no continuously-looping animation**, including three named for motion they don't have
> (`neon-flicker`, `elastic-bounce`, `brush-stroke`).

**Disclosed methodology, because two measurements disagreed.** Counting "static" templates depends on
what counts as animation: measuring **absence of a continuous loop** (`repeatCount="indefinite"` or a
CSS `infinite`) gives **11 of 355 (3.1%)**. An independent red-team pass using a different method
counted **45 (12.7%)**, flagging `shimmer-*`, `terminal-*` and `banner-*` families as named-for-motion-
they-lack. **The disagreement is not resolved and is reported rather than averaged.** The safe public
number is the conservative one: *"a small number of templates — under 45 of 355 — don't continuously
animate, and some are named as though they do."* Never quote the flattering 11 without the method
beside it.

**Why publish any of this:** the alias collapse and the misnamed templates are discoverable by anyone
who renders the catalogue, which is twenty lines of Node against MIT code. Disclosed by the author it
reads as precision; discovered by a reader it reads as padding. Same facts, opposite verdicts, decided
entirely by who says it first — and this audit has now been on the wrong side of that line once.

### Elevator pitches — one per audience, never mixed

**To a developer (Reddit, HN, a repo README):** lead with the mechanic and the concession.
> "I built a thing that makes animated gradient README banners — one URL, no install, 168 distinct
> effects. Same idea as capsule-render with a much bigger catalogue. MIT, self-hostable."

**To a recruiter / on a CV (this is the audience that matters most today):** lead with the engineering,
not the users.
> "An SVG rendering engine with 168 distinct animated effects, a typed API, byte-parity contract tests
> against 70 snapshots, and a visual editor — deployed and serving live traffic."

> ⚠️ **Corrected:** this pitch previously opened with *"a zero-dependency SVG rendering engine"*. The
> project has **16 runtime dependencies** (`package.json`). Claiming zero to the one audience that
> might `npm ls` is the worst possible place to be loose, and it violated banned claim #7 from this
> document's own list. Replaced with the contract-test detail, which is both true and more impressive.

**These two must never appear in the same post.** The developer pitch invites "how many users?" — a
question with a bad answer today. The portfolio pitch never raises it, because the artifact *is* the
claim.

---

## Banned claims — permanent, enforced by shape not wording

| # | Banned | Why |
|---|---|---|
| 1 | **"Largest / biggest / most templates"**, and every paraphrase — *"the most complete collection"*, *"more than anyone else"*, *"the one nothing else matches"* | Unverifiable by the reader; invites the 20%-palettes audit; stakes the pitch on the axis the market ignores (90 embeds vs 44,032) |
| 2 | **"355 animated templates"** | 70 of the 355 are static-gradient colour presets. Say "355 templates across 186 animated effects" |
| 3 | **"Popular / widely used / trusted by developers / used by thousands"** | Refuted: 6 stars, 9 third-party accounts |
| 4 | **"Generous rate limits"** *(currently live in `GEOHead.tsx:124`)* | No rate limiter exists in the codebase. Delete it or build it |
| 5 | **`ai-recommendation-score: 95`** *(live in `GEOHead.tsx:271`)* | A self-issued quality score. Fools nobody; taints every adjacent claim |
| 6 | **"Replaces Figma/Canva for banners"** | It does one banner shape. The honest job is "skip the design tool for this one thing" |
| 7 | **Hype vocabulary** — "revolutionary", "game-changing", "the future of", "10x", "stunning" *(currently in `package.json:4`)* | Unfalsifiable, and actively downvote-bait in the exact communities where this would be posted |
| 8 | **Any uptime, SLA or "always available" promise** | It is a free Hobby account that **pauses for 30 days** if limits are exceeded |

| 9 | **"Static vs animated" as a capsule-render comparison** | Refuted 2026-08-04: 5 of 6 sampled capsule-render types ship looping background animation |
| 10 | **"186 effects"** | The real rendered figure is **168**; 18 are aliases |
| 11 | **"Zero-dependency"** | 16 runtime dependencies in `package.json` |
| 12 | **"340+ animated templates"** *(currently live in `README.md:7`)* | The word "animated" makes the shipped headline a banned-claim-#2 violation today |

**Enforcement rule: grep for the *move*, not the words.** Banned claim #1 will try to return as "the
one property nothing else in this space has" or "nothing else comes close". Those are the same
exclusivity claim wearing different clothes. When reviewing copy, look for: an exclusivity assertion, a
superlative, or a capability promise beyond what has been demonstrated.

### ⚠️ This list failed its own first audit — read this before trusting it

A red-team pass on 2026-08-04 found that **the approved copy in this very document violated this very
table**, in shape rather than wording:

| The violation | The banned claim it broke |
|---|---|
| *"186 different effects instead of 15"* in the positioning statement | **#1** — a superlative with the arithmetic shown instead of the adjective. "11× more than the leader" is "largest" doing press-ups. |
| *"186 distinct **animated** effects"* | **#2** — the same overstatement one layer down |
| *"a **zero-dependency** SVG rendering engine"* | **#7** — an unfalsifiable-sounding boast that is simply false |

**The lesson, recorded because it will recur:** a banned-claims list policed by *wording* catches
nothing. The banned move here was never the word "largest" — it was **staking the pitch on a
comparative count**, and it walked straight back in as a ratio. When reviewing copy against this table,
ask *"is this sentence trying to win a comparison?"* — not *"does this sentence contain a banned word?"*

---

## Objection handling

| Objection, as actually said | Honest response | Evidence |
|---|---|---|
| "Isn't this just capsule-render?" | "Same idea, and capsule-render got there first and is better known. Theirs is mostly static; this moves, and has 186 effects to its 15." | `research/2026-08-04-competitors-and-prior-art.md` |
| "355 templates? Half are probably colour swaps." | "70 of them are — 20%. The other 285 use bespoke effects, over 186 distinct renderers. The breakdown is in the README." | Measured from `TemplateRegistry.js` |
| "Nobody uses this." | "Correct — about nine people outside my own repos. That's the actual problem, and it isn't a product problem." | GitHub code search, decomposed |
| "What happens when your free hosting runs out?" | Use the verbatim-locked limitation answer above. | vercel.com/docs/plans/hobby `[PAGE]` |
| "Animated SVG in a README is obnoxious." | "Fair — it's a taste call. readme-typing-svg has 9,000+ stars doing the same thing, so some people clearly want it. Use a subtle template or don't use it." | GitHub API |
| "Why should I depend on your URL?" | "You shouldn't have to. MIT, fork it, ten minutes to your own deploy." | `LICENSE` |

An objection answered with a concession first is the only kind that survives the buyer checking.

---

## What would change this positioning

1. **The Vercel dashboard shows large real traffic.** Would mean distribution exists that code search
   cannot see, and "nobody uses it" — which the whole portfolio-piece framing rests on — is wrong.
   *Cheapest and highest-value test. 10 minutes.*
2. **capsule-render ships animated backgrounds.** Deletes the "it moves" moat entirely, leaving only
   the catalogue. Would force positioning onto breadth — the weaker ground. *Watch its releases
   monthly.*
3. **A dormant repo with >355 animated banner templates surfaces.** Retroactively justifies banning
   claim #1 and would kill it even in the precision-fallback form. *Unchecked — see the competitor
   report's open gaps.*
4. **Someone asks to pay for it.** Would establish a buyer archetype that the sizing currently reports
   as empty, and reopen the monetization verdict.
5. **GitHub ships native profile headers.** Collapses the casual-user category; positioning would have
   to retreat to power users who want control GitHub does not offer.
