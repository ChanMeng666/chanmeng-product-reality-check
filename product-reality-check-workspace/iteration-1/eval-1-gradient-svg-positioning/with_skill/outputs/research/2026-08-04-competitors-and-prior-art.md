# Competitor sweep + prior-art audit — gradient-svg-generator

**Date:** 2026-08-04 · **Status:** point-in-time record, append-only — supersede with a new dated report, never rewrite
**Scope:** (1) who else serves this buyer, (2) does **"the largest animated README banner collection"** survive an audit
**Sourcing:** `[PAGE]` = fetched and read this session · `[SNIPPET]` = search result only · `[UNVERIFIED]` = no primary source
**All GitHub figures fetched from the GitHub REST API on 2026-08-04.**

---

## The headline finding, before anything else

> **CORRECTED 2026-08-04 after a red-team pass.** Two numbers in the original version of this section
> were wrong, both in the direction that flattered the product. Corrections are inline and struck
> through, not silently swapped. **The generative error: this report audited manifests — a registry
> file and a competitor's README — instead of rendering either product.** Both corrections came from
> ~20 lines of Node against code that was already on disk.

**The claim is defensible on the merits and worthless in practice — and the second half matters more.**

On the most honest counting unit available (distinct rendering effects **verified by rendering**), this
project has **~~186~~ 168** against capsule-render's **15**. That is still not close. "Largest" is
probably *true*.

And it does not matter, because:

| | gradient-svg-generator | capsule-render |
|---|---|---|
| Distinct rendered effects | **168** *(from 186 registry strings; 18 are aliases)* | **15** |
| Files embedding it on GitHub | **90** *(73 the author's own)* | **44,032** *(sampled: none the maintainer's)* |
| Third-party embedding files | **17** | **~44,032** |
| GitHub stars | **6** | **1,790** |

**The adoption gap, stated as two separate measurements — never fused into one.**

- **Raw totals:** 90 vs 44,032 ≈ **489×**.
- **Like-for-like third-party:** 17 vs ~44,032 ≈ **2,590×**.

These measure different things and must not be combined. The original version of this report quoted
489× while *also* noting that 81% of the 90 were the author's own — which silently compared his
inflated total against the competitor's clean one, **flattering by roughly 5.3×**. A red-team sample of
100 capsule-render embeds found **none** belonging to its maintainer, so the like-for-like figure is
the honest one. *(The original also advised trusting the ratio over the absolutes; that was backwards —
both absolutes verified exact, and it was the **ratio** that was fused.)*

**The competitor with ~11× fewer effects has three to four orders of magnitude more adoption.**
Inventory is not what wins this category, so a superlative about inventory is staked on the one axis
the market has already demonstrated it does not rank on. Winning the "largest" argument changes
nothing about the outcome.

That is the actual finding. The prior-art audit below matters less than this table.

---

## Part 1 — The sweep

### Ring 1 — Direct competitors

#### capsule-render (kyechan99/capsule-render) — **threat: HIGH**

- **Stars 1,790 · forks 731 · last push 2026-08-04 (TODAY)** `[PAGE]` — GitHub API
- **15 types**: `wave, egg, shark, slice, rect, soft, rounded, cylinder, waving, venom, speech, blur, pulse, checkered, transparent` `[PAGE]` — its README
- **5 animations**: `fadeIn, scaleIn, blink, blinking, twinkling` `[PAGE]`
- ~~**Output is static SVG by default**; the `animation` parameter applies CSS animation to *text*, not
  the background~~ — **REFUTED 2026-08-04.** This was read off capsule-render's README rather than
  measured. Fetching its live API and counting `repeatCount="indefinite"` elements in the returned SVG:

  | type | looping animation elements |
  |---|---|
  | `wave` (the default) | **0** |
  | `venom` | 1 |
  | `waving` | 2 |
  | `pulse` | 4 |
  | `checkered` | 4 |
  | `blur` | 6 |

  **5 of 6 sampled types ship looping *background* animation.** "Static by default" is literally true
  only of the default `wave` type. The category-level claim — which the positioning doc had built its
  strongest sentence on — is false. **This is the report's most consequential error**, because it was
  about to ship as customer-facing copy that a single `curl` refutes.
- **44,032 files** on GitHub reference `capsule-render.vercel.app` `[PAGE]` — GitHub code search
- Free, no paid tier found

**Honest strengths (this is the market leader and it is better at things this project is not):** it is
the default answer in the category — the thing people already know and copy-paste from someone else's
README; its 731 forks mean it is widely self-hostable and widely *self-hosted*; its parameter surface is
smaller and therefore learnable in one reading; it is actively maintained *today*. Its distribution is
its product.

**positioning_vs_you:** theirs is the banner everyone has already seen; yours is the one nobody has
seen but that actually moves.
**kills_your_moat:** **No, for "largest"** — 15 types vs **168 rendered effects**, so it does not refute
a breadth claim. **Yes, for the framing** — its animated backgrounds refute "we move, they don't".
**Yes, for anything that matters** — 44,032 embeds refute the idea that a bigger collection wins this
category.

#### readme-typing-svg (DenverCoder1/readme-typing-svg) — **threat: MEDIUM**

- **Stars 9,168 · forks 1,594 · last push 2026-07-19** `[PAGE]`
- Genuinely animated SVG (typing effect) in READMEs — free

**Honest strengths:** it does one thing and the thing is unmistakable; ~5× capsule-render's stars.
**positioning_vs_you:** theirs animates *text typing*; yours animates *the whole surface*. Different job,
adjacent shelf.
**kills_your_moat:** **No** for "largest" (it is one effect with parameters). It *does* prove the
category's users want motion, and it is the strongest evidence that **animated SVG renders fine inside
GitHub READMEs** — 9,168 stars for a product that is nothing but animated README SVG. *(Inference from
its adoption, not a fetched GitHub policy statement — see open gaps.)*

### Ring 2 — Adjacent

- **github-readme-stats** (anuraghazra) — **stars 79,825 · forks 36,149 · last push 2026-07-31** `[PAGE]`.
  The category's giant. Same embed-a-URL mechanic, different payload (stats, not decoration). Sets the
  reader's expectation for what a README widget is.
- **shields.io** — the badge standard; the reference case for "free URL-embed service at massive scale"
  and the funding model comparison (see the monetization verdict).

**What Ring 2 tells you:** every successful product on this shelf is *free*, and the biggest is 79,825
stars and still free. The shelf has no price on it.

### Ring 3 — The substitute that is not a product

The real alternative is **not** a competitor tool. It is one of:

1. **A plain Markdown `#` heading** — free, instant, and what ~99% of READMEs actually use. This is the
   true default and the hardest competitor to beat.
2. **Making a PNG in Figma/Canva and committing it** — one-off effort, zero ongoing dependency, no
   third-party uptime risk, and it renders everywhere.
3. **Copying capsule-render's URL out of another README** — the actual acquisition path in this
   category. Nobody visits a gallery; they copy a line from a repo they admire.

**Not priced this session** — the freelance-banner-design price anchor (Fiverr et al.) was assigned to a
research agent that did not land it. Flagged in open gaps. *Its absence does not change the verdict*,
because options 1–3 are all free, and a free substitute that is the same software caps the price at
approximately zero regardless of what a freelancer charges.

### Ring 4 — The platform that could absorb this

**GitHub itself.** GitHub already ships profile READMEs, pinned repos and profile customization. A
first-party "profile header" feature would end this category overnight for the casual user. **Not
verified this session** whether such a feature is shipped or announced — flagged in open gaps as the
highest-value unchecked item, and it belongs on a quarterly watch.

---

## Part 2 — The prior-art / uniqueness audit

### Step 1 — Split the claim

"The largest animated README banner collection" is four claims wearing one coat:

| Distinction | Status |
|---|---|
| **"largest"** — by what unit? templates? effects? animations? | **The whole fight is here.** 355 templates vs **168 rendered effects** vs 186 registry strings are three different numbers, and a hostile reader picks the smallest. |
| ~~**"animated"** — strongest leg~~ | **COLLAPSED 2026-08-04.** Was: "capsule-render is static by default; this is genuinely animated." Refuted — 5 of 6 sampled capsule-render types animate their backgrounds. This leg carries **no weight at all**; both products animate. |
| **"README banner"** | Narrow and honest, but it is a *self-drawn* boundary — see the gerrymander warning below. |
| **"collection"** | **Weakest leg.** A parametric generator with free colour input offers unbounded variants. Any competitor accepting arbitrary colours can claim "infinite templates" with equal honesty. |

### Step 2 — The counting attack (the most likely kill)

Both tools accept free-form colour input. So both can inflate by the same trick:

- **capsule-render:** 15 types × 5 animations = **75** named combinations, × unbounded colour = ∞
- **this project:** 168 rendered effects × unbounded colour = ∞

On the inflated unit, **both are infinite and the claim is meaningless**. On the honest unit —
*distinct rendering effects verified by rendering* — it is **168 vs 15**, and this project wins decisively.

So the claim survives *only* under a specific, stated counting method. A superlative that requires you
to first explain your counting method is a superlative that loses the room before it lands.

**The self-inflicted wound to pre-empt — CORRECTED, and the original was wrong.**

> ⚠️ The original text here read: *"70 of the 355 (20%) are colour-palette presets over 6 standard
> gradient types… a palette, not an animation."* **Verified false by rendering all 355: every one of
> those 70 animates.** `horizontal` emits 4 indefinitely-looping `<animate>` elements; `circular` emits
> 15. The report had invented an unflattering fact about the product and recommended confessing to it.
> A false confession is still a false claim, and it is checkable in the same twenty lines that refute
> a boast.

The real wounds, verified:

1. **18 of the 186 `gradientType` strings are aliases** that render byte-identically — six groups,
   several annotated in the source as *暂时复用* ("temporarily reuse"). The honest effect count is **168**.
2. **A small set of templates are named for motion they do not have** — `neon-flicker`,
   `elastic-bounce`, `brush-stroke` among them. Count disputed by method: **11 of 355** by absence of a
   continuous loop; **45** by an independent red-team method. Unresolved; report the conservative one.

If *he* says "355 animated templates", either discovery reads as inflation. If he says "355 templates
over 168 distinct effects, 186 names of which 18 are aliases", the same discovery reads as precision.
**Same facts, opposite verdicts, entirely decided by who says it first** — and this report was itself
on the wrong side of that line until it was audited.

### Step 3 — Grading the prior art

| Item | Verdict on "largest animated README banner collection" |
|---|---|
| capsule-render (15 types, static-by-default, 44k embeds) | **Does not refute "largest"; refutes its relevance** |
| readme-typing-svg (1 animated effect, 9.2k stars) | Does not refute |
| github-readme-stats (different payload) | Does not refute |
| Animation libraries / marketplaces (LottieFiles, SVGator, Envato) | **Partially refutes** — these host far more than 355 animated assets. They are not README-banner tools, which is exactly why the claim needs the "README banner" qualifier to survive. That qualifier is doing real work, and a skeptic will notice it doing that work. **Not verified this session** — flagged. |
| Dormant twins | **Not verified this session.** The GitHub-wide search for abandoned banner-generator repos did not complete. This is the classic source of a "largest" kill and it remains **unchecked**. |

### Step 4 — The most defensible version

> "355 ready-made templates built on 168 distinct animated SVG effects — as far as I know, the widest
> set of *animated* banner effects available as a single embeddable URL for a GitHub README."

Now the honest caveat, per method: **this is a four-clause conjunction with an "as far as I know" hedge
and a self-drawn category boundary.** A hostile reviewer will say — correctly — that any claim needing
four qualifiers is gerrymandered to be true. **Hold it as a precision fallback under direct
questioning. Never open with it.**

### Step 5 — The arguments that need neither "largest" nor "only"

This is the point of the audit. Three claims that are checkable, need no superlative, and cannot be
refuted by a stranger with one search:

1. ~~**"It moves."**~~ **DEAD — do not use.** This was the report's strongest recommendation and it
   rested on a false premise (capsule-render animates too). Anything built on motion-as-differentiator
   must be discarded, not rephrased.
2. **"One URL, no build step, no account."** A property, not a ranking. True regardless of what any
   competitor ships tomorrow. **This is now the strongest superlative-free claim available** — note
   that capsule-render shares it, so it is a reason to be *adequate*, not a reason to be *chosen*.
3. **"168 distinct effects, and here is the breakdown"** — a *number with its decomposition attached*.
   Stronger than "largest" because it is falsifiable and survives an audit — **but only if the
   decomposition is itself verified.** The original version of this argument shipped an unverified
   decomposition that was wrong in three places. A decomposition offered as proof of rigour, that
   then fails an audit, is worse than no decomposition at all.

### Step 6 — Convergent invention

**Not available as evidence.** The reframe "several people tried this and stopped; I am the one still
maintained" **does not work here**: capsule-render was pushed **today** (2026-08-04) and
readme-typing-svg two weeks ago. The competitors are alive and maintained. Do not use this framing.

---

## Retractions — words now banned

1. **"The largest animated README banner collection"** — as an *opening* line. Not because it is false
   (it likely is not), but because it is unverifiable by the reader, invites the counting audit, and
   stakes the pitch on the axis the market has shown it does not reward (90 embeds vs 44,032).
2. **"355 animated templates"** — say "355 templates across **168** distinct effects". *(The original
   reason given here — "70 are static colour presets" — was itself false; all 70 animate. The claim is
   still banned, for the corrected reason: 186 overstates the effect count by 18 aliases.)*
2b. **"186 effects"** — banned outright. The rendered figure is **168**.
2c. **"capsule-render is static"** — banned outright. Refuted by its live API.
3. **"Most popular / widely used / trusted by developers"** — refuted by the numbers: 6 stars,
   9 third-party accounts.
4. **"Rate limits: generous limits for all users"** — no limiter exists (product diagnostic F2).

## Banned citations

- **"Search for our description and only we come up."** A search phrased in the project's own
  vocabulary is not independent evidence. Never use it.
- **The unqualified "340+/355 templates" as evidence of superiority** without the 186-effect
  decomposition beside it. The raw count invites the audit; the decomposition survives it.
- **GitHub stars, in either direction** — 6 stars is not evidence the product is bad, and citing any
  star count as validation invites the reader to compare it to 1,790.

## The counterexamples a knowledgeable skeptic will throw

**"This is just capsule-render with more colours."**
*Concede:* capsule-render is the incumbent, better distributed, and got there first.
*Hold:* **168 distinct effects to its 15** — roughly 11× the catalogue. *(Do NOT hold "theirs is
static" — refuted.)* Same shelf, much deeper catalogue.

**"355 is padded."**
*Concede:* **yes — 18 of the 186 effect names are aliases that render identically, so the honest effect
count is 168, and a handful of templates are named for motion they don't have.** Say it before they
compute it.
*Hold:* 168 distinct rendered effects is still an order of magnitude past the incumbent's 15, and the
padding is in the *naming*, not the *rendering*.

**"Nobody uses it."**
*Concede:* **true, and the number is 9 third-party accounts.** Do not argue with this one.
*Hold:* nothing. This is the real problem, and the honest response is that distribution is the open
question, not the product.

**"Animated SVG is annoying / people disable it."**
*Partially concede:* a live objection with no data either way here.
*Hold:* readme-typing-svg's 9,168 stars are evidence the category tolerates and seeks motion.

## Additional competitors found (sweep completed 2026-08-04)

Six players the first pass missed. Two change the analysis materially.

| Player | Stars | Last push | Why it matters |
|---|---|---|---|
| **readme-aura** | 138 | **2026-08-03** | **Highest strategic threat found.** Renders arbitrary **React/JSX → animated README SVG**, distributed via npm (no hosting, no outage surface). Doesn't compete on templates — it makes templates *user-authorable*, which is how preset libraries get commoditised. |
| **leviarista/github-profile-header-generator** | **1,316** | 2026-06-08 | Generates a header **you download and commit**. Architecturally immune to the failure mode that threatens every URL-embed tool: no maintainer's bill or downtime can break your README. On GitHub Pages, so it has *no per-request cost at all*. |
| readme-animated-sweetbanner | 63 | 2026-07-06 | A 2026 entrant with the near-identical promise, on github.io. Proves barriers to entry are ~zero. |
| TextGlow | 24 | 2026-06-11 | Another 2026 entrant, same pitch, "no uploads" angle. |
| svg-banners | 406 | **2020-10-13 (dead)** | Died ~6 years ago, still has **68× this project's stars**. |
| REHeader | 236 | **2020-10-10 (dead)** | Died the same month. Still **39× this project's stars**. |

**Two findings that follow, and neither is comfortable:**

1. **Stars in this category accrue to whoever was early, not whoever is best.** Two abandoned 2020
   tools outrank a maintained 2025 tool with ~11× the catalogue by an order of magnitude. Nothing in
   the positioning can fix this; it is a fact about the category's discovery mechanics.
2. **The incumbent has the exact fragility this project fears — and says so publicly.**
   capsule-render's README warns its service *"may be unstable due to usage limits or traffic spikes"*
   and **advises users to fork and self-host**; its issues include **#107 "Deployment Paused"** (closed
   2026-02-03) and **#20 "Vercel link is down"**. The user's cost fear is the category's normal
   condition, the market leader has hit it repeatedly at 44,032 embeds, and it has not killed them.

---

## Cross-report corrections — where my own sources disagree

Recorded rather than silently resolved, per method. **Never take the more flattering number.**

| Fact | Measurement A | Measurement B | Resolution |
|---|---|---|---|
| **Template count** | **355** — `TemplateRegistry.getAllTemplates()`, the registry the gallery reads | **359** — counting `name:` entries across the 19 raw source files | **Unresolved, ~4 templates apart.** Likely 4 defined-but-unregistered templates (consistent with the two-registry inconsistency in diagnostic F6). **Use 355** — it is what the product actually serves. Do not quote 359. |
| **capsule-render last push** | **2026-08-04** (GitHub API, this session) | 2026-07-25 (earlier fetch) | Both correct at their fetch times; a push landed today. **Use 2026-08-04.** The point stands either way: actively maintained. |
| **Non-animating templates** | **11 of 355** (no `repeatCount="indefinite"` / CSS `infinite`) | **45 of 355** (red-team method) | **Unresolved.** Methods differ on what counts as animation. **Quote the conservative 45** publicly, never the flattering 11 without its method. |

## Explicitly unresolved — not verified this session

Named so a skeptic finds them disclosed rather than hidden:

1. **Dormant-twin sweep on GitHub** — abandoned "readme banner generator" repos, unchecked. **This is
   the most likely source of a genuine "largest" refutation and it remains open.**
2. **Whether GitHub ships or has announced a first-party profile-header feature** — the Ring-4
   absorption risk. Highest-value unchecked item.
3. **Animation marketplaces** (LottieFiles/SVGator/Envato) asset counts — would sharpen how much work
   the "README banner" qualifier is doing.
4. **Freelance banner-design price anchor** — Ring 3 not priced.
5. **A fetched GitHub statement that animated SVG is permitted in READMEs** — inferred from
   readme-typing-svg's adoption, not read off a policy page.
6. **Whether the 90/44,032 code-search counts are complete.** GitHub code search indexes public repos'
   default branches and reports approximate totals. Treat both as **lower bounds of the same
   measurement** — the ~489× ratio is the trustworthy part, not the absolute figures.

---

## What would prove this report wrong

Ordered by cost to test.

1. **A dormant repo with >355 animated banner templates exists.** Kills "largest" outright.
   *Test: 30 minutes of GitHub search across the terms in unresolved #1.*
2. **GitHub announces a native profile/README header feature.** Collapses the category for casual
   users; makes distribution unwinnable. *Test: check the GitHub changelog; re-check quarterly.*
3. **The Vercel dashboard shows traffic far above what 9 adopters implies** — meaning embeds exist that
   code search cannot see (private repos, non-default branches, non-GitHub sites). Would overturn the
   "nobody uses it" finding, which several conclusions rest on. *Test: 10 minutes, owner-only.*
   **This is the one most likely to move the verdict.**
4. **capsule-render is archived or abandoned.** Would open the incumbent's position. *Test: 1 minute;
   currently false — pushed today.*

**Watch list (cadence):** capsule-render's last-commit date, monthly. GitHub's changelog for
profile-header features, quarterly. This project's own third-party embed count via code search,
monthly — it is the cheapest real traction instrument available and it costs one query.
