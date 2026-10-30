# Positioning copy that survives scrutiny

---

## Part 1 — The question you actually asked

> Can I honestly claim to be "the largest animated README banner collection"?

**As phrased: no — it will blow up, and I can show you exactly how.**
**Scoped precisely: yes — but you still shouldn't lead with it.**

### Why the unscoped claim fails

"Largest collection" is only true if "collection" means *curated named presets*.
Under any other reading it is **false**, and the falsification is one source file
away.

capsule-render has 15 types × **69 named colour presets** (31 gradients + 29
solids + 9 themes, counted from its source JSON) × 5 text animations × `reversal`
× `section` = **over 20,000 distinct named-parameter visuals** — before anyone
supplies a custom hex, which its `checkCustomColor` accepts in unlimited
multi-stop form.

**A sceptic doesn't need to work hard here. "capsule-render does 20,000+
combinations, you have 355" is a two-minute reply that makes your headline look
like it was written without checking.** That is the blow-up you were worried
about, and it is real.

### The second problem: your own numbers disagree

Three counts for the same product are already in circulation:

- **340+** — your README tagline and `package.json`
- **355** — your gallery screenshot caption, and the true unique count
- **359** — what you get counting entries across the 19 category files, because
  **4 keys are duplicated** (`luminance-glow`, `rainbow-wave`, `neon-pulse` in
  specialty vs animation; `gold-luxury` in material vs githubProfile)

Whichever you pick, **the inconsistency is itself the credibility problem** — and
it is the first thing anyone verifying a size claim will hit. Pin it with a test
that counts unique keys and fails when the README number drifts. That turns your
weakest claim into your most defensible one, because the number becomes
machine-checked rather than asserted.

### Where the claim *is* true

Scoped to curation it holds, and nothing in the field disputes it:

| Measure | You | capsule-render |
|---|---:|---:|
| Curated **named templates** | **355** | **0** — it names colours, not looks |
| Distinct rendering **effects** | **186** | **15** |
| Genuinely animated | **352 of 355** | 5 animated types |

No competitor ships a named-preset library above ~100. That part survives.

### But don't lead with it anyway

Even the true scoped version makes a reader go *check* — and the check lands them
on a comparison you lose badly:

- **6 stars vs capsule-render's 1,790.** 17 third-party embeds vs 44,032.
- A superlative from a 6-star repo reads as *bravado*, not information. The
  instinctive reply is "largest according to whom?" — and the honest answer,
  "according to my own count," is a weak place to be standing.
- "Largest collection" is the same sentence every abandoned template repo on
  GitHub uses. It carries **no information** because everyone claims it. A
  sceptical reader has learned to discount it entirely.
- It picks a fight with a maintainer who is **actively shipping** (capsule-render
  was pushed today) and whose users like it. That's a bad trade for you.

### What to say instead

**Drop the superlative and state the number.** The number is more impressive than
the adjective, and it is checkable — which is precisely what makes it land:

> **355 animated gradient banners for your GitHub README. One URL, no install.**

This is stronger, not weaker. "Largest" is a claim a reader must take on trust.
"355" is a fact they can verify in ten seconds, and verification builds more
credibility than any superlative. You are trading an assertion nobody believes for
a number nobody can dispute.

**If you want the comparative punch, make it specific and attributed:**

> 186 distinct animated effects — more than any other README banner generator I
> could find (capsule-render, the most widely used, has 15).

That version survives contact with a hostile reader because every part of it is
checkable, it names the competitor rather than vaguely gesturing past it, and the
hedge ("I could find") is honest rather than weaselly. It reads as someone who did
the homework — which you did.

---

## Part 2 — Claims ledger

Every claim you might make, graded. **Green** = verified, say it freely.
**Amber** = true with a caveat, phrase carefully. **Red** = don't.

| # | Claim | Grade | Evidence / risk |
|---|---|---|---|
| 1 | "355 templates" | 🟢 | Measured: 355 unique keys across 19 categories |
| 2 | "340+ animated templates" | 🟢 | Measured: **352** genuinely animate. True and conservative |
| 3 | "186 distinct animated effects" | 🟢 | Measured: 186 distinct `gradientType` values |
| 4 | "19 categories" | 🟢 | Measured |
| 5 | "One URL, no install, no signup" | 🟢 | Verified live |
| 6 | "Works anywhere Markdown renders" | 🟢 | Camo-verified on GitHub; standard SVG elsewhere |
| 7 | "Animations survive GitHub's image proxy" | 🟢 | Probed: SMIL + CSS keyframes intact through Camo |
| 8 | "More animated effects than any other README banner generator" | 🟡 | True vs everything found — but *attribute it* (claim 3 phrasing) |
| 9 | "Free and MIT" | 🟡 | True — but don't pair with an uptime promise (see 13) |
| 10 | "Every template animates" | 🟡 | **352/355.** `rainbow-layer`, `egg-shape`, `rounded-corners` are static. Say "352 of 355" or fix them |
| 11 | "**The largest** animated README banner collection" (unscoped) | 🔴 | **Falsifiable.** capsule-render reaches 20,000+ named combinations. See Part 1 |
| 11b | "The largest curated **library of named** animated banner presets" | 🟡 | True — no rival above ~100 — but still invites a comparison you lose |
| 12 | "Trusted by developers" / "used across GitHub" | 🔴 | **9 third-party users.** This would be the one that blows up |
| 13 | "Unlimited free usage" (`X-Api-Usage: free-unlimited-usage`) | 🔴 | You're on Vercel Hobby — exceeding it is a **30-day hard lockout**. You cannot keep this promise |
| 14 | "Production-ready" / "enterprise-grade" | 🔴 | Single Hobby deployment, no SLA, no rate limiting |
| 15 | "Fastest" / "most performant" | 🔴 | Unmeasured. Don't claim what you haven't benchmarked |

### The two red flags to fix in code, not copy

**Claim 13 is live right now.** `src/pages/api/svg.ts` sends
`X-Api-Usage: free-unlimited-usage` on every response. Change it to something you
can keep — `X-Api-Usage: free-best-effort` — and pair it with the disclaimer in
`03-monetization-verdict.md` §5.

**Claim 10 is a five-minute fix.** Three templates don't animate. Either animate
them or exclude them from the animated count. Right now "340+ animated" is safe
because 352 > 340; "all 355 animate" would not be.

---

## Part 3 — Ready-to-use copy

### GitHub repo description (the 350-char field)

Your current one undersells badly — it says "multiple gradient types" when the
measured answer is 186. Replace with:

```
355 animated gradient SVG banners for your GitHub README — 186 distinct effects
across 19 categories. Embed one URL, no install. Free, MIT, with a visual editor.
```

### README one-liner

```markdown
355 animated gradient SVG banners for your GitHub README — embed a single URL,
no install required.
```

(Your current "340+" is fine and conservative. 355 is the true number and is
stronger. Pick one and use it everywhere — right now the README says "340+" in the
tagline and "355 templates" in a screenshot caption, which reads as sloppy.)

### Site hero

```
Your README, designed in one line.

355 animated gradient banners. 186 distinct effects. 19 categories.
Paste one URL — no install, no signup, no build step.

[ Browse templates ]  [ Open the editor ]
```

### The paragraph for a Show HN / r/github post

This is the version built to survive a hostile comment thread. Note what it does:
leads with the honest origin, names the competitor first and fairly, gives
checkable numbers, and volunteers its own limitation before anyone else can.

```
I built a gradient banner generator for GitHub READMEs.

capsule-render is the tool most people use for this and it's good — I used it for
a year. But it's a shape generator: 15 types, 5 of which animate, and you assemble
the look yourself from URL parameters. I wanted a browsable library of finished
looks instead of a parameter reference.

So this is 355 curated presets across 19 categories, built on 186 distinct
animated effects — aurora, caustics, glitch, holographic UI, liquid metal,
stained glass, terminal typing, and so on. 352 of the 355 genuinely animate
(three are static and I should fix that). Every one is a single URL:

![](https://gradient-svg-generator.vercel.app/api/svg?text=Hello&template=neural-network)

There's a visual editor if you'd rather click than read docs.

Two honest caveats: it's a personal Vercel deployment, so treat it as best-effort
and fork it if you need guaranteed uptime — it's MIT. And it does rectangles with
effects inside them; if you want capsule-render's wave and shark silhouettes, use
capsule-render, it's better at that.

Would genuinely like feedback on which templates look cheap — curation is the
whole product here and I'm too close to it.
```

**Why this works:** the strongest move available to a 6-star project is *not*
claiming to be the biggest. It's being visibly honest — naming the incumbent
generously, disclosing limitations unprompted, and asking a real question. That
earns the benefit of the doubt that a superlative spends.

### Social / short form

```
355 animated gradient banners for your GitHub README.
186 distinct effects. One URL. No install.
Free + MIT.
```

---

## Part 4 — The positioning that actually differentiates you

Not "largest". **"Curated, not configured."**

capsule-render hands you 15 shapes and 69 colours and asks you to design something
from them. You hand people 355 finished looks and ask them to pick one. Those are
different products for different users, and the second one is a legitimately
better answer for someone who wants their README to look good in thirty seconds
and has no interest in learning a parameter reference.

That framing has three advantages over "largest":

1. **It doesn't invite a scoreboard comparison you lose.**
2. **It's a positioning claim, not a size claim** — it can't be falsified by
   someone shipping a 400-template competitor next month.
3. **It's actually true**, and it explains why 355 templates matters. A number
   alone is trivia; "curated so you don't have to configure" is a reason to care.

Supporting proof points, in the order a reader will accept them:

- **186 distinct effects** — the range is real, not 355 colour swaps of one gradient.
- **Browsable gallery + visual editor** — curation you can actually see.
- **One URL, no install** — the category's table stakes; state it, don't sell it.
- **Cache headers Camo actually honours** — a real engineering detail the
  1,790-star incumbent gets wrong. Worth one line in a technical audience,
  omit it for everyone else.

---

## Part 5 — Wording rules

**Stop saying:** largest · best · most popular · trusted by developers · unlimited ·
production-ready · enterprise-grade · blazing fast.

**Say instead:** the counts (355, 186, 19, 352) · "one URL, no install" · "curated,
not configured" · "free and MIT" · "best-effort — fork it for guaranteed uptime".

**Three consistency fixes before you publish anything:**

1. **Pick one number and pin it with a test.** "340+" and "355" both appear in the
   README today, and a naive count of the category files gives **359** (4
   duplicate keys). Use **355**, and add a test that counts unique keys so the
   number can't drift again. A machine-checked count is a far stronger claim than
   an asserted one.
2. **Fix the `package.json` name mismatch.** It says `"chromaflow"` while
   everything public says "Gradient SVG Generator". Pick one identity — a reader
   who notices reads it as an abandoned rename.
3. **Update the GitHub description.** The current one ("multiple gradient types")
   was written when that was true. It now describes a product roughly 10× smaller
   than the one you have, and it's the first thing anyone reads.
