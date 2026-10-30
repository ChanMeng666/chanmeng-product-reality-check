# Monetization: the honest read

**Short answer: don't monetize, and don't cap costs either — because you don't
have a cost problem. You have a distribution problem, and it's a much better
problem to have.**

The rest of this document is the evidence for that, the two things you *should*
fix (both take under an hour), and the conditions under which this answer would
change.

---

## 1. The premise needs correcting first

You wrote:

> "other people's READMEs already embed it, which means MY Vercel account pays for
> THEIR traffic"

I measured this rather than assuming it. GitHub code search for
`gradient-svg-generator.vercel.app` returns **90 files**:

- **73 (81%) are in your own repos** — your profile README alone accounts for 25.
- **17 (19%) are third-party.**
- Those 17 belong to **9 distinct people**, and one of them (`TayyebaSadaq`)
  accounts for 9 of the 17.

So the sentence is *literally* true — nine strangers do embed it — but the
implied scale isn't there. **You are overwhelmingly paying for your own traffic.**

For calibration, measured the same way on the same day:

| Service | Files embedding it |
|---|---|
| capsule-render | **44,032** |
| readme-typing-svg | ~43,840 |
| **yours** | **90** (17 third-party) |

capsule-render is embedded roughly **2,600× more** than this project. And
capsule-render — with 1,790 stars, 731 forks, and three orders of magnitude more
traffic — **has no monetization of any kind.**

That's the frame for everything below: the thing you're worried about paying for
is a cost the market leader doesn't even bother to monetize away, and you're at
0.04% of its volume.

---

## 2. Do you actually have a cost problem? Almost certainly not

Three independent mechanisms are protecting you, and I verified all three:

**GitHub Camo absorbs the views.** README images are proxied through
`camo.githubusercontent.com` (Fastly). Camo caches and honours your upstream
`Cache-Control`. I probed your endpoint through Camo: `MISS` then `HIT` with
`X-Cache-Hits` climbing. A thousand README views are *not* a thousand origin hits.

**Your cache headers are already better than the market leader's.** You send
`public, max-age=31536000, immutable`. capsule-render sends Vercel's default
`max-age=0, must-revalidate` — which means Camo refuses to cache it and it eats an
origin hit on essentially every README view on Earth. You got this right and they
didn't.

**Vercel's CDN is caching you too.** Live probe: `X-Vercel-Cache: MISS` → `HIT`.
A cache hit never invokes the function.

The binding limit on Vercel Hobby is **1,000,000 edge requests/month** — about
33,000/day. (Not bandwidth: at your 9 KB mean response, 1M requests is ~9 GB
against a 100 GB allowance.) With 9 third-party embedders behind a caching proxy,
you are not within orders of magnitude of that ceiling.

**Action:** open your Vercel dashboard and read the actual usage number. It takes
one click and it beats every estimate in this document. I could not see your
billing data, and I'd rather you check than trust my model. If it shows anything
above ~10% of the edge-request allowance, re-read this section sceptically.

---

## 3. Should you monetize? No — and the evidence is unusually clean

I looked for anyone, anywhere, successfully charging for README image generation.
**There is no such case.**

| Project | Stars | License | Revenue model |
|---|---|---|---|
| github-readme-stats | 79,824 | MIT | donation links only |
| readme-typing-svg | 9,169 | MIT | none |
| capsule-render | 1,790 | MIT | none |
| shields.io | — | — | ~$1,437/yr + donated CDN |

**The shields.io number is the one to internalise.** It serves **over 1.6 billion
images per month** — the most-recognised badge service in software — and its
[Open Collective](https://opencollective.com/shields) shows an estimated **annual
budget of $1,437**. Total raised across its entire history: $17,672. It survives
on *donated Cloudflare CDN*, not cash.

If the category's most famous product converts 1.6 billion monthly impressions
into roughly $120/month, a 355-template gradient generator with nine third-party
users is not going to convert its way to meaningful revenue. The ceiling isn't
low because your product is weak; it's low because **this category has no
willingness to pay.**

### Four structural blockers, in descending order of how fatal they are

**1. MIT + stateless = a one-click escape hatch.** Ghost proves MIT plus paid
hosting can work ($10.9M ARR on an MIT core) — but Ghost sells away an *ongoing
operational burden*: a database, mail, backups, uptime. Your product is a pure
function: string in, SVG out. Self-hosting it is one fork and one deploy, forever,
with no operational tail. capsule-render has **731 forks against 1,790 stars — a
41% fork ratio.** That is what "users will just host it themselves" looks like as a
measured number.

Relicensing wouldn't save it either. AGPL triggers on distributing modified
source; a fork deployed to Vercel complies by publishing the fork. And **the SVG
output is not a derivative work of the generator.** There is no copyleft mechanism
that reaches the thing you'd want to charge for.

**2. The buyer is wrong.** Hosted image generation *is* a real paid category —
ScreenshotOne $17–259/mo, Urlbox $19–498/mo, Bannerbear $49–299/mo — but every one
of those sells to a *business* automating OG images inside a product, at
~$0.004–0.009 per image. Your user is an individual decorating a personal profile
who currently pays $0 and has three free substitutes one fork away.

**3. Watermark-as-paywall backfires.** No README service has ever done it. The
mechanics are unfavourable: a visible nag converts a small fraction to payers and
converts the loudest fraction into forkers *who then host the free alternative for
everyone else*. You'd be manufacturing your own competitor. (Tasteful attribution
as a *marketing* channel is fine and is roughly what WakaTime does — but that's
distribution, not revenue.)

**4. You have no audience to monetize.** Six stars. Nine third-party users. Even
if every blocker above vanished, the arithmetic of monetizing nine users doesn't
work. **This is the real finding: the constraint isn't revenue model, it's reach.**

---

## 4. The one thing you must fix, regardless of what you decide

> "Hobby teams are restricted to **non-commercial personal use only.**"
>
> **"Note: Asking for Donations fall under commercial usage."**
>
> — [Vercel Fair Use Guidelines](https://vercel.com/docs/limits/fair-use-guidelines)

**On your current deployment, adding a "Buy me a coffee" or GitHub Sponsors button
to the site would be a terms violation.** So would ads or affiliate links. The
cheapest possible monetization attempt raises your cost floor to $20/mo Pro before
it earns a dollar.

This also means: **any monetization decision is a hosting-migration decision.**
They are not separable.

Related, and worth fixing on its own merits: your endpoint currently advertises
`X-Api-Usage: free-unlimited-usage`. On Hobby, that is a promise you cannot keep —
exceeding the limit is a **hard 30-day lockout with no pay-to-continue option**,
during which every embedding README shows a broken image. Either soften the header
or move somewhere it's true.

---

## 5. What I actually recommend

### Do these two things now (under an hour, total)

**(a) Add `s-maxage` to the cache header.** `src/pages/api/svg.ts:22` sets only
`max-age`. Vercel's [caching docs](https://vercel.com/docs/edge-network/caching)
say edge caching requires `s-maxage` — yet the live probe shows it caching anyway.
You are relying on undocumented behaviour for the exact mechanism that keeps your
bill at zero. Vercel strips `s-maxage` from the client-facing header, so Camo sees
no change. There is no downside.

```ts
res.setHeader('Cache-Control', 'public, max-age=31536000, s-maxage=31536000, immutable');
```

While you're there: `src/core/constants.js:25` defines a second, unused policy
(`max-age=3600, s-maxage=86400`). Two cache policies, one live. Reconcile them.

**(b) Ship the category-standard disclaimer.** Every comparable project has one.
capsule-render's wording, which you can adapt almost verbatim:

> This service is provided on a best-effort basis and may be unstable due to usage
> limits or traffic spikes. For guaranteed availability, fork the repository and
> deploy your own instance.

This costs you nothing, matches what every user of this category already expects,
and converts a future outage from a broken promise into a documented limitation.

### Do this only if usage actually grows

**Move the `/api/svg` endpoint to Cloudflare Workers.** Not now — now it's
premature optimisation on a problem you don't have. But it's the right move the
moment the Vercel dashboard shows real load, because the shape of this workload
(pure compute, tiny cacheable response, no database, no upstream API) is the ideal
Workers case:

| | Vercel Hobby | Cloudflare Workers Free | Workers Paid |
|---|---|---|---|
| Requests | 1M invocations/mo | **~3M/mo** (100k/day) | 10M/mo, then $0.30/M |
| Egress | 100 GB | **not metered** | **not metered** |
| Price | $0 | $0 | **$5/mo** |
| Donations allowed | **No** | yes | yes |

At 100M requests/month this models to roughly **$32 on Workers vs $208+ on Vercel
Pro**, because Vercel meters requests *and* bytes while Cloudflare meters only
requests. It also legalises a donate button.

### Don't do these

- **A paid tier.** No precedent, wrong buyer, one-click fork escape.
- **A watermark paywall.** Manufactures competitors.
- **Rate limiting.** You have nine external users. Adding friction to a product
  with a distribution problem is backwards.
- **A donate button on the current host.** Terms violation (§4).

---

## 6. If you want money from this, sell something else

Two verified patterns, neither of which is "charge for the SVGs":

**Sponsorware — the only fast-converting solo-dev model with hard numbers.** Caleb
Porzio [documented](https://calebporzio.com/sponsorware) releasing new work to
sponsors first, then open-sourcing it at a sponsor threshold: **$573/mo → $2,633/mo
in two days.** Applied here, that means *future* template drops, not the existing
355. Everything still ends up MIT.

The same author's [$1M breakdown](https://calebporzio.com/i-just-cracked-1-million-on-github-sponsors-heres-my-playbook)
is the sharpest datapoint in this whole report: pure "buy me a coffee" donations
were **0.5%** of his million. Screencasts he *sold* were 72.5%. His conclusion:
*"People want to support you, but aren't going to send you a job-quitting amount
for no reason. You have to give them a reason. SELL THEM SOMETHING."*

**Sponsor placements on the gallery site, not in the image.** This is what
star-history does — sponsor products on the website, the embedded chart left
alone. Requires traffic you don't yet have, and requires leaving Vercel Hobby.

Both are gated on the same thing: **reach**. Which is why the honest ordering is
*distribution first, revenue never or much later.*

---

## 7. So: portfolio piece, or product?

**Portfolio piece — but a much stronger one than you're currently getting credit
for.** Keep it free, keep it MIT, and stop treating hosting cost as the live risk.

The measured case for it as a portfolio artifact is genuinely good, and it's
better than the star count suggests: 355 templates across 19 categories, **186
distinct rendering effects**, **352 of them genuinely animating**, 355/355
rendering without error, zero-install embedding, a visual editor, a typed Zod
request schema, and cache headers that are *correct in a way the 1,790-star market
leader's are not*. That last one is a real, checkable engineering judgment call you
won on the merits.

What's missing isn't quality. It's that **six people have seen it.** The gap
between this project and capsule-render is not 186 effects versus their handful —
it's 44,032 embeds versus 17. If you want a better outcome here, every hour goes
into distribution, and none into billing.

`02-positioning-copy.md` is the copy for doing that, with each claim graded on
whether it survives a sceptic.

---

## 8. What would change this verdict

Written down so you can check against them later rather than re-litigating:

- **Vercel dashboard shows >10% of the edge-request allowance.** Then the cost
  question is real; migrate to Workers (§5) — but that's still cost-capping, not
  monetizing.
- **Third-party embeds pass ~1,000 files** (currently 17). That's roughly 2% of
  capsule-render, the first point at which sponsor placement on the gallery site
  becomes discussable.
- **Someone asks to pay you, unprompted.** One inbound request is worth more than
  this entire analysis. Nine users is too small a sample to have produced one yet.
- **You want to test willingness-to-pay directly.** I could not verify it — Fiverr
  and Upwork both blocked automated access, so the intended price-point evidence
  for "GitHub profile README design" gigs is missing. If that market shows real
  prices, it's the one signal that would reopen the question. Worth ten minutes of
  manual browsing before you accept my "no."
