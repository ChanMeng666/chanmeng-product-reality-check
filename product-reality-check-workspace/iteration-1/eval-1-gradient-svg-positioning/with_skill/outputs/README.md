# gradient-svg-generator — product reality check

**Engagement date:** 2026-08-04 · **Effort level:** quick pass, extended (three deliverables + prior-art
audit + red team + patch loop)

Answers to the three questions asked: **(a)** the real competitive landscape, **(b)** positioning copy
that survives scrutiny, **(c)** whether to monetize or cap costs.

---

## Read in this order

| # | File | What it is | Kind |
|---|---|---|---|
| 1 | [`strategy/monetization-verdict.md`](strategy/monetization-verdict.md) | **Question (c).** The verdict, the cost arithmetic, bottom-up sizing, what to do instead | LIVING |
| 2 | [`strategy/positioning.md`](strategy/positioning.md) | **Question (b).** Positioning statement, corrected moat, approved copy, banned-claims list | LIVING |
| 3 | [`research/2026-08-04-competitors-and-prior-art.md`](research/2026-08-04-competitors-and-prior-art.md) | **Question (a).** Four-ring sweep + the audit of "largest animated README banner collection" | APPEND-ONLY |
| 4 | [`research/2026-08-04-product-diagnostic.md`](research/2026-08-04-product-diagnostic.md) | Copy-vs-code contradictions, ranked by narrative damage | APPEND-ONLY |
| 5 | [`research/red-team/2026-08-04-kill-memo.md`](research/red-team/2026-08-04-kill-memo.md) | A hostile senior-dev persona attacking the four documents above | APPEND-ONLY |
| — | [`data/competitors.json`](data/competitors.json) | 13 entities with sources, adoption and kills-your-moat verdicts | data |

**Living** documents state what is true now and are edited in place. **Append-only** documents are
point-in-time records — never rewritten, only superseded by a new dated file. Corrections appear inline
and struck through, because the record of what was believed is worth as much as the correction.

---

## The three answers, compressed

**(a) The landscape.** capsule-render is the incumbent: **1,790 stars, 44,032 files embedding it,
pushed today**. This project has **6 stars and 90 embedding files — 73 of them its own repos**, leaving
**17 third-party files across 9 accounts**. On catalogue depth it wins decisively (**168 distinct
rendered effects vs 15 types**). On adoption it loses by three to four orders of magnitude. Two
abandoned 2020 competitors still have more stars than it does.

**(b) Positioning.** **Do not claim "largest".** Not because it's false — it's probably true — but
because it's unverifiable by the reader, invites a counting audit, and stakes the pitch on the one axis
the market has proven it doesn't reward. Approved copy, a 12-entry banned-claims list, and verbatim-
locked answers are in the positioning doc.

**(c) Monetization.** **No — and there is nothing to cap.** Vercel Hobby *pauses, it never bills*
(quoted verbatim in the verdict). Monetizing would force the Pro plan at **$240/year** to chase a pool
of **$0–45/year**. The category's donation yield is ~**1 sponsor per 1,800 stars**, and this project's
Sponsors button is **already deployed and earning nothing**. Keep it as a portfolio piece.

---

## What this engagement got wrong about itself

The red team found real errors in the first draft of these documents, and the patch loop corrected
them. Recorded here because a research package that hides its own corrections has not earned the right
to make claims:

| The claim I shipped | What verification showed | Where it's corrected |
|---|---|---|
| "186 distinct effects" | **168** — 18 of the 186 names are aliases rendering byte-identically | positioning, competitor report, diagnostic F6 |
| "capsule-render is static by default; **this one moves**" | **False.** 5 of 6 sampled types ship looping background animation. This was the strongest positioning clause and it was about to ship as customer-facing copy refutable by one `curl` | positioning (moat + comparison line) |
| "70 of 355 are static colour presets" — offered as an honest confession | **False.** All 70 animate. **A false confession is still a false claim** | positioning (decomposition), diagnostic F6 |
| "489× adoption gap" | **Fused.** Compared his inflated total (incl. 81% own repos) against the competitor's clean one. Like-for-like is ~2,590× | competitor report, headline |
| "Add a GitHub Sponsors button" | **Already there** in `.github/FUNDING.yml`, earning nothing | monetization verdict, Archetype C |
| "Nobody knows it exists" | Understated **283 commits over 19 months** of real publishing effort | monetization verdict §5 |

**The generative error behind the first three: I audited the manifest, not the artifact.** I counted
registry entries and read a competitor's README instead of rendering either product. Every correction
came from ~20 lines of Node against code already on disk. **If you take one methodological lesson from
this package: render the thing before you describe it.**

---

## Claim ledger

Every externally checkable number in these deliverables. Internal claims cite a repo path; external
claims cite a URL. All verified **2026-08-04**.

| Claim | Source | Grade |
|---|---|---|
| 355 templates, 19 categories | `src/core/TemplateRegistry.js` — `getAllTemplates().length` | internal, measured |
| 186 `gradientType` strings → **168 distinct rendered outputs**; 18 aliases in 6 groups | rendered each type, hashed output | internal, measured |
| 24 of 355 templates non-deterministic | rendered ×3, compared hashes; `Math.random` in `advancedEffectGenerator.js`, `templateUtils.js` | internal, measured |
| 11 of 355 lack a continuous loop (red team: 45) | rendered all 355 | internal, **disputed — both reported** |
| 16 runtime dependencies | `package.json` | internal |
| 283 commits, 2025-01-06 → 2026-07-10 | `git rev-list --count HEAD` | internal |
| `.github/FUNDING.yml` declares Sponsors + Buy Me a Coffee | `.github/FUNDING.yml` | internal |
| Unused `SVG_CACHE_CONTROL` with `s-maxage` | `src/core/constants.js:25`; grep shows no consumer | internal |
| Endpoint sets `max-age=31536000, immutable` | `src/pages/api/svg.ts:22` | internal |
| "Rate Limits: Generous limits for all users" with no limiter | `src/components/seo/GEOHead.tsx:124` | internal |
| `ai-recommendation-score: '95'` | `src/components/seo/GEOHead.tsx:271` | internal |
| Vercel CDN caches the endpoint (`MISS` → `HIT`) | live `curl -D -` on `/api/svg` | `[PAGE]` measured |
| gradient-svg-generator: 6 stars, 1 fork, 1 watcher | api.github.com/repos/ChanMeng666/gradient-svg-generator | `[PAGE]` |
| 90 embedding files; 73 own; 17 third-party / 9 accounts | GitHub code search API, decomposed by owner | `[PAGE]` |
| capsule-render: 1,790 stars, 731 forks, pushed 2026-08-04 | api.github.com/repos/kyechan99/capsule-render | `[PAGE]` |
| capsule-render: 15 types, 5 animations | its README | `[PAGE]` |
| capsule-render animates: blur=6, pulse=4, checkered=4, waving=2, venom=1, wave=0 | live `capsule-render.vercel.app/api/` responses | `[PAGE]` measured |
| capsule-render: 44,032 embedding files | GitHub code search API | `[PAGE]` |
| readme-typing-svg: 9,168 stars; **4 sponsors** (goal 10) | GitHub API; github.com/sponsors/DenverCoder1 | `[PAGE]` |
| capsule-render: **1 sponsor** | github.com/sponsors/kyechan99 | `[PAGE]` |
| github-readme-stats: 79,825 stars, free | api.github.com/repos/anuraghazra/github-readme-stats | `[PAGE]` |
| readme-aura: 138 stars, pushed 2026-08-03, JSX→animated SVG | api.github.com/repos/collectioneur/readme-aura | `[PAGE]` |
| Hobby: *"you will have to wait until 30 days have passed"* | vercel.com/docs/plans/hobby | `[PAGE]` |
| Hobby: *"non-commercial, personal use only"* | vercel.com/docs/plans/hobby | `[PAGE]` |
| Hobby: 1M invocations, 100 GB transfer; Spend Management N/A on Hobby | vercel.com/docs/limits, /docs/plans/hobby | `[PAGE]` |
| Pro: $20/user/month | vercel.com/docs/plans/hobby | `[PAGE]` |
| chromaflow.vercel.app resolves (HTTP 200) | `curl` | `[PAGE]` measured |
| Template count 355 vs 359 | registry vs raw-source count | **disputed — both reported** |

---

## The five things only the owner can do

Blocking — the recommendations above are conditional on the first one.

1. **Read the Vercel Usage dashboard** (10 min). Every conclusion about traffic and cost rests on
   numbers nobody has read. **Do this before acting on anything else.**
2. **Fix the 24 non-deterministic templates** (~1 hr, diagnostic F8) — the most serious live defect, and
   it is currently frozen into year-long caches.
3. **Decide the name** — "Gradient SVG Generator" or "Chromaflow". Nothing else in the copy can ship
   until this is settled.
4. **Delete the two false lines** (5 min) — the phantom rate limits and the self-assigned score.
5. **Decide whether to run the distribution experiment** with the dated gate in the verdict (§5), or
   accept portfolio-piece status by choice rather than by drift.

## The biggest gaps still open

- **Whether GitHub is shipping native profile-header customization** — would collapse the category.
  Unchecked; highest-value.
- **Whether animated SVG survives GitHub's Camo proxy as animated** — the product's core premise.
  Inferred from readme-typing-svg's 9,168 stars, never confirmed against a GitHub policy page.
- **Dormant-twin sweep** for a >355-template abandoned collection — the one thing that would kill the
  "largest" claim outright even in its precision-fallback form.
- **Freelance/Fiverr price anchor** for README design (Ring 3), and developer *sentiment* toward
  animated banners — nobody has checked whether people find these appealing or noisy.
