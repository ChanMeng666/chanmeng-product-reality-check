# Monetization verdict — gradient-svg-generator

**Date:** 2026-08-04 · **Status:** LIVING document — states what is true now, edit in place
**Question asked:** "an honest read on whether/how to monetize this or whether I should just cap the
costs and keep it as a portfolio piece"

---

## The verdict, in one sentence

> **No — do not monetize. And do not "cap the costs" either, because Vercel already caps them for you
> and the cap is not a bill. Keep it as a portfolio piece — and if you want that to change, run one
> time-boxed distribution experiment with a date on it, rather than building anything further.**

*(Revised after red team: the original closing clause was "spend the freed effort on the one thing that
is actually broken: nobody knows it exists." That understated 19 months and 283 commits of genuine
publishing effort. See §5.)*

Monetizing today would be **strictly value-destroying**: it converts a **$0** hosting bill into a
**$240/year** obligation in order to chase a revenue pool that is currently **under $50/year**.

The arithmetic is below. Every input is fetched or measured, not assumed.

---

## First: two premises in the question are factually wrong

The question contains two beliefs that the evidence does not support. Both corrections are in the
user's favour, and together they dissolve most of the problem.

### Premise 1: "MY Vercel account pays for THEIR traffic" — **substantially false**

**Measured this session**, against the live endpoint:

```
GET /api/svg?text=CacheTest8842&template=sunset-gold   → X-Vercel-Cache: MISS
GET /api/svg?text=CacheTest8842&template=sunset-gold   → X-Vercel-Cache: HIT
```

Vercel's edge cache **is** serving this endpoint. Cost scales with *distinct banner URLs × edge regions
× cache evictions* — **not** with reader views. A banner embedded in a repo that 10,000 people read does
not cost 10,000 invocations.

*Caveat, kept honest:* both test requests hit the same PoP (`X-Vercel-Id: syd1::iad1::…`), so
per-region misses are real and unmeasured. The direction is certain; the magnitude is not.

### Premise 2: "other people's READMEs already embed it" — **true, but the number is 9**

Measured via GitHub code search, then **decomposed** (raw totals in this category are misleading):

| Measure | Count |
|---|---|
| Files on GitHub embedding `gradient-svg-generator.vercel.app` | **90** |
| …of which are **ChanMeng666's own repos** | **73 (81%)** |
| …genuinely third-party files | **17 (19%)** |
| Distinct third-party **accounts** | **9** |
| …of which **one account** (`TayyebaSadaq`) accounts for | **9 of the 17 files (53%)** |
| Remaining accounts, one file each | **8** |

So the honest sentence is: **eight people and one enthusiast use this.** One of the nine
(`NZ-SheSharp`) is plausibly a personal-network connection given the author's other repos — unverified,
but it should not be counted as arms-length without checking.

*Caveat:* GitHub code search covers indexed public repos' default branches and returns approximate
totals — this is a **lower bound**. Private repos, non-GitHub sites and unindexed files are invisible.
**The Vercel dashboard is the only instrument that would settle it, and it has never been read.**

**Consequence:** there is no traffic problem to solve. There is an obscurity problem.

---

## The cost exposure, priced exactly

### Vercel Hobby cannot bill you `[PAGE]` — vercel.com/docs/plans/hobby, last_updated 2026-06-16

> *"As the Hobby plan is a free tier there are no billing cycles. In most cases, if you exceed your
> usage limits on the Hobby plan, you will have to wait until 30 days have passed before you can use
> the feature again."*

**This is the complete answer to the cost fear.** The failure mode of runaway success on Hobby is
**the banners stop rendering for up to 30 days**. It is an *availability* risk, not a *financial* one.
There is no surprise bill. There is nothing to cap.

### The included allowances you would have to exhaust first `[PAGE]`

| Resource | Hobby included / month |
|---|---|
| Function Invocations | **1,000,000** |
| Edge Requests | Up to **1,000,000** |
| Fast Data Transfer | **100 GB** |
| Active CPU | 4 CPU-hrs |

With **9 third-party accounts** and a working edge cache, these are not close to being reached. The
gap between current usage and the free ceiling is several orders of magnitude.

### The trap that actually matters `[PAGE]`

> *"As stated in the fair use guidelines, the Hobby plan restricts users to **non-commercial, personal
> use only**."*

**The moment you monetize, you are no longer eligible for Hobby.** Monetizing forces the Pro plan at
**$20/user/month = $240/year**, and Vercel's **Spend Management** feature — the actual spend cap — is
listed as **N/A on Hobby, Configurable on Pro** `[PAGE]`.

This inverts the intuition completely: **staying free is what keeps the hosting free.** Charging $1
would cost $240.

---

## Bottom-up sizing: who would actually move money

Named archetype × sourced price anchor × defensible buyer count. No top-down TAM.

### Archetype A — The developer decorating their own README

- **Who:** the 9 current third-party users, and the ~44,032 files that embed capsule-render.
- **Price anchor:** **$0.** Every alternative is free — capsule-render (free), readme-typing-svg
  (free), github-readme-stats (79,825 stars, free), and a plain `#` heading (free). The entire shelf
  is unpriced.
- **Reachable buyers:** 9 today.
- **Realistic ACV: $0.** **Adversarial note:** the product is **MIT-licensed and self-hostable**. A
  buyer asked to pay can fork it and deploy it to their own Vercel Hobby account in ten minutes, for
  free, forever. **A free substitute that is the same software caps the price at zero.** This is not a
  pricing problem to be solved with better packaging; it is a structural property of the licence.
- **Realistic pool: $0.**

### Archetype B — Companies wanting branded README/docs banners

- **Who:** companies with public repos and brand guidelines.
- **Price anchor:** not established this session (the freelance-design anchor was not landed — see
  open gaps). Directionally, a company with brand guidelines has a designer and does not need 355
  presets; it needs *one* banner, made once, committed as a PNG.
- **Reachable by this author today:** effectively **0** — no sales motion, no inbound, 6 stars.
- **Adversarial note:** the buying rhythm is **once**, not monthly. A subscription against a
  once-per-repo decision is a pricing model fighting the customer's behaviour.
- **Realistic pool: $0.**

### Archetype C — Sponsorship / donations

> ✅ **GAP CLOSED 2026-08-04.** This was flagged as the report's largest open gap. The competitor sweep
> landed the numbers, and they are worse than the placeholder assumed.

- **Who:** users grateful enough to give.
- **Price anchor — now measured, from the sponsor pages themselves `[PAGE]`:**

  | Project | Stars | Sponsors |
  |---|---|---|
  | capsule-render | 1,790 | **1 sponsor** |
  | readme-typing-svg | 9,168 | **4 sponsors** (against a stated goal of 10; tiers from $1/mo) |
  | github-readme-stats | 79,825 | 3 donation surfaces, still a donation project |
  | leviarista/github-profile-header-generator | 1,316 | **no FUNDING.yml at all** |

  **The category's demonstrated donation yield is roughly 1 sponsor per 1,800 stars.** At $1–5/month
  tiers, a 9,000-star project in this category earns single-digit dollars per month.

- **The falsifier that already fired:** the original version of this report recommended "add a GitHub
  Sponsors button — costs nothing". **It is already there.** `.github/FUNDING.yml` declares
  `github: ChanMeng666` and `buy_me_a_coffee: chanmeng66u`. The recommendation was not just weak, it
  was **already implemented and has yielded nothing at 6 stars** — which is exactly what the category
  base rate predicts. Recording this because a recommendation that turns out to be already-done is a
  finding about the research, not about the product.
- **Realistic pool at current adoption: $0.** Not "approximately zero" — the mechanism is deployed and
  the observed result is zero. Extrapolating the category rate (1 sponsor / 1,800 stars) to 6 stars
  predicts **0.003 sponsors**.

### Sum

| Pool | Value |
|---|---|
| **Realistic (sum of A+B+C at today's adoption)** | **~$0–45 / year** |
| **Cost of being allowed to collect it** | **$240 / year** (forced Pro) |
| **Net** | **negative** |

**Stretch pool, kept separate and explicitly labelled:** if this project reached capsule-render's
adoption (44,032 embedding files), the revenue would still be bounded by the fact that **no product on
this shelf charges anything** — capsule-render, readme-typing-svg and github-readme-stats are all free
at 1.8k / 9.2k / 79.8k stars. **The category's revealed price is zero at every scale observed.** That
is a statement about the shelf, not about this product.

---

## The base rate: what happened to everyone who already tried this

The most persuasive evidence here is not the arithmetic — it is that **the three most successful
products in this exact category, at 300× to 13,000× this project's adoption, have all declined to
charge.** github-readme-stats has 79,825 stars and no paid tier. If a price existed on this shelf,
someone with 79,825 stars would have found it first, and would have far more leverage to charge it.

**Verified category finding (competitor sweep, 2026-08-04):** *nobody in this category charges money.*
Every player checked is free and permissively licensed. No paid tier, no commercial licence, no hosted
upsell was found on any of them. Donation is the only mechanism present, and its measured yield is
~1 sponsor per 1,800 stars.

**Two mortality datapoints, and one live threat:**

- **svg-banners** (406 stars) and **REHeader** (236 stars) both died in **October 2020** and were never
  replaced. Both still hold more stars than this project. In this category, stars accrue to whoever was
  *early*, not whoever is *best* — which is a hard fact for a 2025 entrant.
- **readme-aura** (138 stars, pushed 2026-08-03) renders **arbitrary React/JSX as animated README
  SVG**. If that approach gains traction, a template library stops being a moat, because templates
  become user-authorable. It generalises the category rather than competing inside it.

**The variable that would have to have changed** for the pricing verdict to be wrong: nothing
observable has. The category is as free today as it was when capsule-render started in 2020.

---

## What to do instead — ranked, with effort

### 1. Read the Vercel Usage dashboard (10 minutes) — **do this first**

Every conclusion above is conditional on real usage numbers that have never been read. Settings →
Usage shows invocations, edge requests, data transfer and the cache-hit ratio, **retroactively and for
free**. This converts the whole question from speculation into arithmetic. If it shows near-zero usage
(expected), the cost anxiety is closed permanently.

### 2. Fix the cache header (10 minutes) — the only real cost lever

`src/core/constants.js:25` already defines the right answer and nothing uses it (diagnostic F1). Wire
it up and drop `immutable` so a bad render is fixable:

```
public, max-age=3600, s-maxage=86400, stale-while-revalidate=604800
```

### 3. Add the free safety valve (30 minutes) — this is the "cap" worth having

Vercel's **WAF custom rules** are available on Hobby (**up to 3** `[PAGE]`), as is **IP blocking** (up
to 3). One rate-limiting rule on `/api/svg` is the actual, free version of the "cap my costs" instinct
— and it makes the currently-false "generous rate limits" documentation true (diagnostic F2).

### 4. Delete the false and self-serving copy (5 minutes)

The unimplemented rate-limit claim and the self-assigned `ai-recommendation-score: 95`. Both are
liabilities on a portfolio piece, whose entire job is to demonstrate judgment.

### 5. Then work on distribution, not revenue — but read this first

The binding constraint is 9 users, not 9 dollars. Distribution notes are in the positioning doc.

> ⚠️ **Correction after red team, 2026-08-04.** The original version of this document closed by saying
> the real problem is "nobody knows it exists", framed as though distribution had not been attempted.
> **That framing was wrong and worth correcting, because it changes what to do next.**
>
> Measured: **283 commits over 19 months** (2025-01-06 → 2026-07-10), a deployed site, a visual editor,
> a template gallery, a 79KB README, an OG cover image, community-health files, and a full site
> redesign. **That is a sustained distribution attempt**, not an absence of one. It produced 6 stars,
> 1 fork and 9 third-party accounts.
>
> So the honest statement is not "he hasn't tried". It is: **19 months of building-and-publishing
> converted to almost no adoption, and there is no evidence that more of the same converts better.**
> The failure is not effort; it is that effort went into *the artifact* rather than into *the channel*.
>
> **What follows from the correction:** if the user wants adoption, the next thing should be an
> explicit, time-boxed **channel** experiment — one post in a place where the buyer already is, with a
> stated success threshold and a date — not another feature, another template family, or another
> redesign. And if he does not want to run that experiment, that is a legitimate choice: it makes this
> a portfolio piece by decision rather than by default, which is a better position to be in.
>
> **A dated gate, so this does not drift:** publish one post to a developer community by **2026-09-04**
> and re-run the code-search embed count on **2026-10-04**. If third-party accounts have not moved from
> 9 to at least 25, stop investing in distribution and keep it as a portfolio piece permanently.

---

## If you ever *do* want money from this — the only two shapes that fit

Recorded so the option is not lost, both explicitly **not recommended now**:

- ~~**GitHub Sponsors button.**~~ **ALREADY DONE — and it is earning nothing.** `.github/FUNDING.yml`
  already declares GitHub Sponsors and Buy Me a Coffee. Leave it exactly as is; it costs nothing and
  it is not going to produce anything, because the category rate is ~1 sponsor per 1,800 stars and this
  project has 6. **Do not spend another hour on the donation surface** — it is not
  under-optimised, it is under-adopted, and those need different fixes.
- **Sell the thing that is scarce, which is not the SVG.** The scarce asset is the *design work* — 168
  effects someone spent real time building. That has a market as a **template pack / design asset**
  (one-time purchase, no hosting, no uptime obligation, no Hobby violation) far more plausibly than as
  a hosted API. **Unresearched — no price anchor, no evidence of demand.** Labelled a hypothesis, not a
  plan.

**Do not** build: paid tiers, API keys, branding removal, or a custom-domain upsell. Each requires the
Pro plan, an auth system and a support obligation, to sell a thing that is MIT-licensed and forkable in
ten minutes.

---

## What this report does NOT say

**It does not say this is a bad project.** "Not monetizable" and "not worth having built" are unrelated
statements. The evidence says this is a **genuinely well-built piece of engineering** — 168 distinct
effects, a real test suite, contract tests, honest under-claimed numbers — sitting in a category that
has never had a price. As a portfolio piece it does its job: it is a large, working, publicly-inspectable
artifact. That is a good outcome and the correct frame for it. The harm would only come from pricing it
as if it were a business.

---

## What would prove this verdict wrong

Ordered by cost to test. Items 1 and 3 landing together would overturn the verdict rather than dent it.

1. **The Vercel dashboard shows substantial traffic** — say >100k invocations/month, implying embeds
   invisible to code search. Would mean real distribution exists and the "9 users" finding is an
   artifact of the instrument. *Test: 10 minutes, owner-only.* **Highest value.**
2. **Hobby usage limits actually get hit.** Would make the availability risk concrete and justify
   moving to Pro for reliability — still not a reason to charge. *Test: the same dashboard.*
3. **Any product in this category ships a paid tier and retains users.** Would falsify "the category's
   revealed price is zero". *Test: watch capsule-render / readme-typing-svg / github-readme-stats
   quarterly.*
4. **A company makes an inbound request for a branded/licensed version.** One real inbound would
   establish Archetype B exists. *Test: passive; add a contact line and wait.*
5. **The shields.io / sponsorship figures, once fetched, show meaningful solo-maintainer income at
   comparable adoption.** Would raise Archetype C's ceiling — though not at 9 users. *Test: 20 minutes
   of research; currently an open gap.*

## The steelman I could not refute

*All of this measures a world in which README decoration is a hobbyist activity with no money in it. If
AI-generated repos and auto-generated documentation make "make my repo look professional in one line"
a default step in every project's setup, the buyer count is backward-looking by construction, and a
tool with 168 effects and a clean API is well-positioned for a market that does not exist yet.*

This is genuinely unfalsifiable in the present tense, which is exactly why it gets a **date** rather
than a rejection: **if third-party embeds have not moved from 9 by 2027-02-04 (two quarters), the
market is not being created on the timeline this argument assumes.** Re-run the code-search query then;
it costs one command.

## Open gaps — what I could not verify

1. **shields.io Open Collective revenue and backer count** — the category's best funding comparison.
2. **Published data on typical GitHub Sponsors income for solo dev-tool maintainers.**
3. **Whether any hosted badge/banner service has ever monetized** — an absence I assert from the three
   free market leaders, not from an exhaustive search.
4. **Freelance banner-design price anchor** (Ring 3) — would firm up Archetype B.
5. **GitHub Camo's cache duration** — GitHub's proxy sits between readers and this origin, and its
   caching behaviour is the other half of the cost model. Unverified; the measured Vercel cache HIT
   makes this less load-bearing than it would otherwise be.
