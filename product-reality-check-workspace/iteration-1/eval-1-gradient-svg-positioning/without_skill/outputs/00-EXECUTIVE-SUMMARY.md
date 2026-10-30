# gradient-svg-generator — reality check

**Read this page. The other four are the evidence.**

Measured 2026-08-04. Nothing here is inference where a measurement was possible.

---

## The one-paragraph answer

You asked about competitors, positioning, and monetization. The measurements say
your product is **better than you're claiming** and **far less used than you
think**. You have 355 templates and 186 distinct animated effects against the
market leader's 15 — a genuine 12× lead. But you have 6 stars and **9 third-party
users**, and 81% of the "traffic you're paying for" is your own repos. So the
cost problem you're worried about is roughly imaginary, monetization is
premature by two orders of magnitude, and the only real problem is that
**almost nobody knows this exists**. Fix two things in code (an hour), stop
worrying about the bill, and spend everything else on distribution.

---

## (a) The competitive landscape

**One competitor matters: capsule-render.** 1,790 stars, 731 forks, actively
maintained (pushed today), MIT, GitHub Sponsors button, no paid tier.

**And you beat it on capability, decisively:**

| | You | capsule-render |
|---|---:|---:|
| Distinct rendering effects | **186** | **15** (10 static + 5 animated) |
| Genuinely animated templates | **352 of 355** | 5 animated types |
| Curated named templates | **355** | **0** — it names colours, not looks |

**No rival ships a curated preset library above ~100.** That niche is genuinely
uncontested. But note the asymmetry carefully: capsule-render has **69 named
colour presets**, and 15 types × 69 colours × 5 animations × reversal × section =
**over 20,000 named combinations**. Your lead is in *curation* and *effect count*,
**not** in possible outputs — which is exactly the distinction question (b) turns on.

Other entrants: galaxy-profile (461), TypingSVG (301, animated text),
readme-aura (138, pushed yesterday), sweetbanner (63). leviarista (1,316) is a
static PNG design tool, not a URL service.

**But the distribution gap is brutal**, and it's the number that should reframe
everything:

| | You | capsule-render | Ratio |
|---|---:|---:|---:|
| Stars | 6 | 1,790 | 298× |
| Third-party embeds on GitHub | **17** | **44,032** | **2,590×** |

One more thing worth knowing: **your cache headers are correct and
capsule-render's are not.** You send `max-age=31536000, immutable`, which GitHub's
Camo proxy honours (I probed it: MISS → HIT). capsule-render sends Vercel's
default `must-revalidate`, so Camo refuses to cache it and it eats an origin hit
on nearly every README view across 44,032 embeds. That's a real engineering call
you won against a project 300× your size.

→ `01-competitive-landscape.md`

---

## (b) Can you claim "the largest animated README banner collection"?

**As phrased, no — it would blow up, and here's the exact mechanism.**

"Largest collection" is only true if "collection" means *curated named presets*.
Under any other reading it's **false**: capsule-render has 15 types × **69 named
colour presets** × 5 animations × reversal × section = **over 20,000 named
combinations**, before any custom hex. A sceptic's two-minute reply —
*"capsule-render does 20,000+, you have 355"* — makes the headline look
unchecked. That's the blow-up you were worried about, and it's real.

**Your own numbers also disagree**, which is the first thing a verifier hits:
**340+** (README tagline, `package.json`), **355** (screenshot caption, and the
true unique count), **359** (naive count across category files — 4 keys are
duplicated). Pick 355 and **pin it with a test**, so the number is machine-checked
rather than asserted.

**Scoped to curation the claim survives** — 355 named templates and 186 effects
vs capsule-render's 0 named templates and 15 effects, with no rival above ~100.
**But don't lead with it even then**, because it still makes readers check, and
the check surfaces 6 stars vs 1,790. A superlative from a 6-star repo reads as
bravado, and "largest collection" is what every abandoned template repo says.

**Say the number instead. It's stronger:**

> **355 animated gradient banners for your GitHub README. One URL, no install.**

"Largest" must be taken on trust. "355" is verifiable in ten seconds — and
verification buys more credibility than any adjective. If you want the
comparative, attribute it: *"186 distinct animated effects — more than any other
README banner generator I could find; capsule-render, the most widely used, has
15."* Every clause there survives a hostile reader.

**The durable positioning isn't "largest", it's "curated, not configured."**
capsule-render gives you 15 shapes and asks you to design something. You give
people 355 finished looks and ask them to pick one. That can't be falsified by a
400-template competitor next month, and it explains *why* the count matters.

**Two claims to kill immediately** — these are the ones that would actually blow
up:

- 🔴 **"Trusted by developers" / "used across GitHub"** — it's 9 people.
- 🔴 **`X-Api-Usage: free-unlimited-usage`**, which your API sends on *every
  response* right now. You're on Vercel Hobby, where exceeding limits is a **30-day
  hard lockout with no pay-to-continue**. You cannot keep that promise.

→ `02-positioning-copy.md` (claims ledger + ready-to-paste copy incl. a Show HN post)

---

## (c) Monetize, or cap costs and keep it as a portfolio piece?

**Neither. You don't have a cost problem, and monetizing is premature.**

**The premise needs correcting.** You said other people's READMEs embed it, so you
pay for their traffic. Measured: of 90 files embedding your URL, **73 (81%) are
your own repos**. Third-party: **17 files, 9 people** — one of whom accounts for 9
of the 17. You are overwhelmingly paying for your own traffic, behind a caching
proxy, on an allowance of 1M edge requests/month.

**Monetization has no precedent in this category, and the evidence is unusually
clean.** shields.io serves **1.6 billion images/month** on an Open Collective
budget of **$1,437/year**. capsule-render, at 44,032 embeds, has a sponsor button
and nothing else. Nobody charges for README images. Add the structural blockers —
MIT plus a stateless pure function means self-hosting is one fork forever
(capsule-render has a **41% fork ratio**), and no license change reaches the SVG
output — and a paid tier converts your loudest users into competitors.

**The finding that matters: this isn't a revenue-model problem, it's a reach
problem.** Nine users is too few to monetize under any model.

### Do these two things now (under an hour)

1. **Add `s-maxage` to the cache header** (`src/pages/api/svg.ts:22`). You
   currently send only `max-age`; Vercel's docs say edge caching requires
   `s-maxage`, yet it caches anyway — meaning **the mechanism keeping your bill at
   zero is undocumented behaviour**. No downside to fixing it.
2. **Ship the category-standard best-effort disclaimer** (every competitor has
   one) and soften that `free-unlimited-usage` header.

### Know this before you ever add a donate button

> "Hobby teams are restricted to non-commercial personal use only… **Asking for
> Donations fall under commercial usage.**" — [Vercel Fair Use](https://vercel.com/docs/limits/fair-use-guidelines)

**A "Buy me a coffee" button on your current deployment is a terms violation.**
Any monetization decision is therefore also a hosting-migration decision.

### If usage ever grows

Move `/api/svg` to **Cloudflare Workers**: ~3M requests/month free, **egress not
metered at all**, $5/mo for 10M. Modelled at 100M requests: **~$32 vs $208+ on
Vercel Pro**. Not now — that's optimising a problem you don't have.

**Verdict: portfolio piece — but a stronger one than you're getting credit for.**
355 templates, 186 effects, 352 animating, 355/355 rendering without error, a
typed request schema, and cache headers the market leader gets wrong. The quality
is there. Six people have seen it.

→ `03-monetization-verdict.md`

---

## Do this week

| # | Action | Effort |
|---|---|---|
| 1 | **Check your actual Vercel usage.** One click, beats every estimate here | 1 min |
| 2 | Add `s-maxage=31536000` to the cache header | 5 min |
| 3 | Change `X-Api-Usage` to `free-best-effort`; add the disclaimer | 15 min |
| 4 | Update the GitHub description — it describes a product 10× smaller than what you have | 5 min |
| 5 | Fix the `package.json` name (`"chromaflow"` vs "Gradient SVG Generator" everywhere else) | 2 min |
| 6 | Pick one number (**355**) and **pin it with a test** — 340/355/359 are all in circulation | 20 min |
| 7 | Animate or drop the 3 static templates (`rainbow-layer`, `egg-shape`, `rounded-corners`) | 30 min |
| 8 | **Post it somewhere.** The Show HN draft is written for you | 1 hr |

Items 1–7 are hygiene. **Item 8 is the only one that changes your outcome.**

---

## What I could not verify

- **Your actual Vercel usage.** No dashboard access — every cost claim is modelled
  from request volume, not read from your bill. **Check it before acting.**
- **Willingness-to-pay for README cosmetics.** Fiverr and Upwork both blocked
  automated access, so the direct price-point evidence is missing. The
  monetization verdict rests on category base rates instead. Ten minutes of manual
  browsing would be worth more than my inference here.
- **GitHub code search completeness** — totals are approximate and index-capped.
  The 2,590× gap is far larger than any plausible indexing error, but the exact
  figures aren't precise.
- **Camo's exact cache TTL and eviction policy** — undocumented; I verified it
  honours your headers but not how long it holds.

---

## Files

| File | Contents |
|---|---|
| `00-EXECUTIVE-SUMMARY.md` | This page |
| `01-competitive-landscape.md` | Competitors, capsule-render teardown, distribution gap |
| `02-positioning-copy.md` | Claims ledger (🟢🟡🔴) + ready-to-paste copy |
| `03-monetization-verdict.md` | Cost model, why not to monetize, what to fix |
| `04-evidence-log.md` | Every measurement, with reproduction steps |
