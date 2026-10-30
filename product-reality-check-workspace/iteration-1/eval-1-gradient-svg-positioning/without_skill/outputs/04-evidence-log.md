# Evidence log — measured facts, and how to re-run them

Everything in the other four documents traces back to this file. Each fact is tagged
**MEASURED** (I ran it), **FETCHED** (primary source retrieved), or **UNVERIFIED**.
Date of measurement: **2026-08-04**.

If you disagree with a conclusion elsewhere, argue with a number here.

---

## 1. What the product actually contains (MEASURED)

Counted by loading every module in `src/features/*/templates.js` through the same
registry list that `src/core/TemplateRegistry.js` uses.

| Fact | Value |
|---|---|
| Sum of per-category template counts | 359 |
| **Unique template keys** | **355** |
| Duplicate keys across categories | 4 |
| Categories | 19 |
| Distinct `gradientType` effect values | **186** |
| Templates that render without error | **355 / 355** |
| Templates emitting SMIL `<animate*>` | 322 |
| Templates emitting CSS `@keyframes` / `animation:` | 95 |
| **Templates with no animation at all** | **3** (`rainbow-layer`, `egg-shape`, `rounded-corners`) |
| **Templates that genuinely animate** | **352** |
| SVG size: min / median / mean / max | 794 B / 9,311 B / 7,900 B / 21,136 B |

The 4 duplicate keys (later category silently loses to earlier in registry order):

- `luminance-glow` — specialty vs animation
- `rainbow-wave` — specialty vs animation
- `neon-pulse` — specialty vs animation
- `gold-luxury` — material vs githubProfile

Per-category counts: specialty 50, githubProfile 41, art 35, nature 32, tech 32,
pride 20, animation 18, fluids 17, basic 11, emotion 12, material 12, shape 12,
lightShadow 12, culinaryLiquid 12, pathText 12, gaming 8, pattern 8, metallic 8,
luxury 7.

**Reproduce it:** the two scripts are in the scratchpad at
`D:\Temp\claude\D--github-repository-archlang\6fdf3599-2ae5-42e2-aa8c-02187f943896\scratchpad\`
(`count.js`, `effects.js`, `anim.js`). They only `require()` the repo; they write nothing.

### Why this matters

The README says **"340+"**. The measured animated count is **352**. The claim is
true *and* conservative — you are under-claiming by 12. The screenshot caption
saying "355 templates" is also correct, because it counts all templates rather
than only animated ones. Both numbers are defensible; they just need to stop
being used interchangeably (see `02-positioning-copy.md`).

---

## 2. Repository traction (FETCHED — GitHub REST API)

`GET https://api.github.com/repos/ChanMeng666/gradient-svg-generator`, 2026-08-04:

| Field | Value |
|---|---|
| `stargazers_count` | **6** |
| `forks_count` | **1** |
| `subscribers_count` | 1 |
| `open_issues_count` | 0 |
| `created_at` | 2025-01-06 |
| `pushed_at` | 2026-07-10 |
| `license` | MIT |
| `homepage` | https://gradient-svg-generator.vercel.app/ |

Local git: **283 commits**, current history rooted 2026-07-10 (the repo was
re-initialised or force-rewritten at that date; GitHub still reports the original
2025-01-06 creation).

---

## 3. Who actually embeds it (MEASURED — GitHub code search)

`gh api search/code -f q='gradient-svg-generator.vercel.app'`

| Metric | Value |
|---|---|
| Total files containing the URL | **90** |
| Files in **your own** repos (`ChanMeng666/*`) | **73** (81%) |
| Files in **third-party** repos | **17** (19%) |
| **Distinct third-party users** | **9** |

The nine third parties: `TayyebaSadaq` (9 repos — one enthusiast, over half the
third-party total), `Aadish-Sanghvi`, `DiogoAug16`, `NZ-SheSharp`,
`ShravanPusdekar`, `SimulationOfMario`, `XaidenLabs`, `iMaDissame`,
`tharunkumarsurya`.

Your own top embedders: `ChanMeng666/ChanMeng666` (profile README, 25 files),
`gradient-svg-generator` itself (11), `2d-portfolio` (5).

### Calibration against the incumbents (MEASURED, same method, same day)

| Service | Files on GitHub containing its URL |
|---|---|
| `capsule-render.vercel.app` | **44,032** |
| `readme-typing-svg.herokuapp.com` | 43,840 |
| `readme-typing-svg.demolab.com` | 37,888 |
| **`gradient-svg-generator.vercel.app`** | **90** (17 third-party) |

capsule-render is embedded roughly **2,600× more** than this project by
third-party count. GitHub code search totals are approximate and index-capped, so
treat these as orders of magnitude, not exact — the three-orders-of-magnitude gap
is far larger than any indexing error.

---

## 4. Live service behaviour (MEASURED — `curl -D -`, 2026-08-04)

```
GET https://gradient-svg-generator.vercel.app/api/svg?text=Test&template=neural-network&height=120

HTTP/1.1 200 OK
Cache-Control: public, max-age=31536000, immutable
Content-Length: 9176
X-Api-Usage: free-unlimited-usage
X-Vercel-Cache: MISS      <- first request
X-Vercel-Cache: HIT       <- second request, ~1s later
```

The service is **up**, and **Vercel's CDN is caching it** despite the header
carrying only `max-age` and no `s-maxage`. Vercel's own caching documentation
says `s-maxage` is required, so this is working-but-undocumented behaviour. See
§6 for why that matters.

### GitHub Camo (verified by an independent probe in this same investigation)

- GitHub rewrites README image URLs through `camo.githubusercontent.com`
  (Fastly/Varnish). [GitHub Docs — About anonymized URLs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-anonymized-urls)
- **Camo caches, and honours upstream `Cache-Control`.** Probed live: this
  endpoint went `X-Cache: MISS` → `HIT` with `X-Cache-Hits` incrementing across
  repeat requests.
- **capsule-render is NOT cached by Camo** — it ships Vercel's default
  `max-age=0, must-revalidate`, so it takes an origin hit on essentially every
  README view worldwide. **Your cache headers are already better than the market
  leader's.**
- Camo's CSP is `default-src 'none'; img-src data:; style-src 'unsafe-inline'`.
  SMIL `<animate>` and CSS `@keyframes` **survive intact** — animation genuinely
  works in GitHub READMEs. `<script>` inside SVG and **external webfonts** are
  blocked.

**Consequence for cost:** README *views* are close to free. What costs money is
**URL cardinality** — every distinct `?text=…&template=…` combination is a new
cache object that must miss at each Fastly POP. A generator with a free-text
parameter has unbounded cardinality by design.

---

## 5. Hosting economics (FETCHED — vendor docs, 2026)

### Vercel Hobby — what you are on

| Resource | Hobby included |
|---|---|
| Function invocations | 1,000,000 / mo |
| Edge requests | up to 1,000,000 |
| Fast Data Transfer | up to 100 GB |
| Fast Origin Transfer | up to 10 GB |

Source: [Hobby plan](https://vercel.com/docs/plans/hobby),
[Fair Use Guidelines](https://vercel.com/docs/limits/fair-use-guidelines).

**Binding constraint is edge requests (1M/mo ≈ 33,000/day), not bandwidth.**
At a 9 KB mean response, 1M requests is only ~9 GB — you would hit the request
ceiling roughly 11× before the 100 GB bandwidth ceiling.

**Overage behaviour is a hard stop, not a bill:**

> "As the Hobby plan is a free tier there are no billing cycles. In most cases, if
> you exceed your usage limits on the Hobby plan, **you will have to wait until 30
> days have passed** before you can use the feature again."

There is no pay-to-continue on Hobby. If you blow the limit, every README
embedding your banner shows a broken image for up to 30 days.

### The clause that governs the whole monetization question

> "Hobby teams are restricted to **non-commercial personal use only**. All
> commercial usage of the platform requires either a Pro or Enterprise plan."
>
> Commercial usage is "any Deployment that is used for the purpose of financial
> gain of anyone involved in any part of the production of the project" —
> explicitly including advertising, affiliate links, and:
>
> **"Note: Asking for Donations fall under commercial usage."**

— [Vercel Fair Use Guidelines](https://vercel.com/docs/limits/fair-use-guidelines)

**A "Buy me a coffee" button on the current deployment is a terms violation.**
This is the single most actionable finding in the whole report, and it is
independent of whether monetizing is a good idea.

Note also: the endpoint currently advertises `X-Api-Usage: free-unlimited-usage`.
That is a promise you cannot keep on Hobby.

### Vercel Pro

$20/mo/seat. Fast Data Transfer first 1 TB then $0.15–$0.35/GB; edge requests
first 10M then $2.00–$3.20/million; invocations $0.60/million.
[Regional pricing](https://vercel.com/docs/pricing/regional-pricing).

Spend Management (Pro only) is **not a hard cap** — Vercel checks usage "every few
minutes", pausing lags the threshold, it pauses *all* projects on the team, and
**projects do not auto-resume**. [Spend Management](https://vercel.com/docs/spend-management).

### Cloudflare Workers — the alternative

| | Vercel Hobby | Cloudflare Workers Free | Workers Paid |
|---|---|---|---|
| Requests | 1M invocations/mo | **100,000/day (~3M/mo)** | 10M/mo, then $0.30/M |
| Egress | 100 GB | **not metered at all** | **not metered at all** |
| Price | $0 | $0 | **$5/mo** |
| Donations/ads allowed | **No** | yes | yes |

[Cloudflare Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/).

At 100M requests/month with ~9 KB responses, the modelled cost is roughly **$32 on
Cloudflare Workers vs ~$208+ on Vercel Pro** — because Vercel meters both requests
and bytes while Cloudflare meters only requests.

---

## 6. The one technical defect worth fixing regardless (MEASURED)

`src/pages/api/svg.ts:22` sets:

```ts
res.setHeader('Cache-Control', 'public, max-age=31536000, immutable');
```

Vercel's [CDN caching docs](https://vercel.com/docs/edge-network/caching) state that
edge caching requires `s-maxage`. The live probe shows it caching anyway — i.e. you
are relying on undocumented behaviour that can change without a changelog entry, on
the exact mechanism that keeps your bill at zero.

Adding `s-maxage=31536000` costs nothing (Vercel strips `s-maxage` from the
client-facing header, so Camo sees no change) and converts this from
undocumented-and-working to documented-and-guaranteed.

Note also `src/core/constants.js:25` defines a *different*, unused policy
(`public, max-age=3600, s-maxage=86400`) — two cache policies in the codebase,
only one of them live. Worth reconciling.

---

## 7. Category precedents (FETCHED)

| Project | Stars | Forks | License | Money |
|---|---|---|---|---|
| github-readme-stats | 79,824 | 36,147 | MIT | donations only |
| readme-typing-svg | 9,169 | 1,594 | MIT | none |
| **capsule-render** (closest analogue) | **1,790** | **731** | MIT | **none** |
| shields.io | — | — | — | ~$1,437/yr + donated CDN |

shields.io serves **>1.6 billion images/month** on an Open Collective budget of
**$1,437/year** ([opencollective.com/shields](https://opencollective.com/shields)),
surviving on donated Cloudflare CDN rather than cash.

Every one of these projects ships the same disclaimer. capsule-render, verbatim:

> "This service is provided on a best-effort basis and may be unstable due to usage
> limits or traffic spikes." … fork it and deploy your own.

github-readme-stats, verbatim:

> "The public Vercel instance … is best-effort and can be unreliable due to rate
> limits and traffic spikes." … "For reliable cards we recommend self-hosting."

**capsule-render's 731 forks against 1,790 stars — a 41% fork ratio — is what
"users will just self-host it" looks like as a measured number.**

---

## 7b. capsule-render, counted from source (FETCHED — `gh api`, repo `main`)

Not from its README prose — from the actual files.

**15 `type` values, in two directories:**

- `model/normalModel/` — **10 static**: wave, egg, shark, slice, rect, soft,
  rounded, cylinder, speech, transparent
- `model/animationModel/` — **5 animated**: waving, venom, blur, pulse, checkered

**69 named colour presets**, counted by parsing the JSON:

| File | Count |
|---|---:|
| `src/gradient.json` | 31 gradients |
| `src/pallete.json` | 29 solids |
| `src/pallete_theme.json` | 9 themes (default, dark, radical, merko, gruvbox, gruvbox_light, tokyonight, onedark, cobalt) |
| **Total** | **69** |

**5 dynamic colour modes:** auto, timeAuto, random, gradient, timeGradient.
**Unbounded custom colour:** `checkCustomColor` in `src/verification.ts` parses any
number of stops (`0:EEFF00,50:…,100:a82da8`).

**5 text animations:** fadeIn, scaleIn, blink, blinking, twinkling.

**Its reachable named space:**

| Axis | Count |
|---|---:|
| 15 types × 69 colours | **1,035** |
| × 5 animations | 5,175 |
| × reversal × section | **20,700** |
| × arbitrary hex | effectively infinite |

**This is why "355 templates > 15 types" does not survive a sceptic.** The
defensible comparisons are effects-to-effects (186 vs 15) and
curation-to-curation (355 named looks vs 0).

**Repo state:** 1,790 stars, 731 forks, MIT, `pushed_at` 2026-08-04 (actively
maintained). `.github/FUNDING.yml` contains `github: [kyechan99]` — it **does**
have a GitHub Sponsors button, but no paid tier, watermark, or rate limiting.

**Rival sweep** (GitHub search API, by stars): leviarista/github-profile-header-generator
1,316 (static PNG tool, not a URL service), vinimlo/galaxy-profile 461 (GPL-3.0),
whiteSHADOW1234/TypingSVG 301 (typing text), collectioneur/readme-aura 138
(JSX→animated SVG, pushed 2026-08-03), sh4den/readme-animated-sweetbanner 63,
asrvd/gitbanner 36 (dead since 2022), mrhx01/TextGlow 24, SVG-Crafter 6,
Waveify 2, READMEForge 1, svg-readme 0. **None ships a curated named-preset
library above ~100.**

---

## 8. What I could NOT verify

- **Your actual Vercel usage.** I have no access to your dashboard. Every cost
  statement here is modelled from request volume, not read from your bill. *Check
  the dashboard before acting on any of it* — it is one click and it beats every
  estimate in this document.
- **Camo's exact TTL and eviction policy.** Undocumented. Verified it honours
  upstream `Cache-Control` and held ≥5 consecutive hits; could not observe
  long-run eviction.
- **Willingness-to-pay for README cosmetics.** Fiverr and Upwork both returned
  403/CAPTCHA. The intended direct price-point evidence could not be gathered, so
  the monetization verdict rests on category base rates instead. Flagged again in
  `03-monetization-verdict.md`.
- **GitHub Sponsors median income data.** The Tidelift survey URL now 404s
  (redirects to Sonar); Octoverse 2025 contains no Sponsors data.
- **Whether any README service ever added a watermark paywall.** No instance
  found. Absence of evidence, not evidence of absence.
- **GitHub code search completeness.** Totals are approximate and index-capped.
