# The real competitive landscape

**The headline:** you are not competing on library size — you already win that
axis by roughly 12×. You are losing on distribution by roughly 2,600×. Every
competitor with more traction than you has *fewer* effects, not more.

All numbers measured 2026-08-04. Method and reproduction in `04-evidence-log.md`.

---

## 1. The map

There are three distinct product shapes here, and they are usually confused with
each other. Knowing which one you're in matters for both positioning and pricing.

| Shape | What it renders | Examples |
|---|---|---|
| **Decorative header/banner** ← *you are here* | A wide image at the top of a README | capsule-render, gradient-svg-generator, sweetbanner, TextGlow |
| **Animated text** | Typing/rotating text as SVG | readme-typing-svg |
| **Data cards** | Rendered *facts* (stats, trophies, skills) | github-readme-stats, github-profile-trophy, skill-icons, shields.io |

The data-card category is by far the largest, but it is not your competition —
those tools answer "show my numbers", you answer "make my README look designed".
The only *direct* competitor with real traction is **capsule-render**.

---

## 2. Direct competitors — decorative banners

| Project | Stars | Embeds on GitHub | Animated? | Named preset library | Distinct effects | Money |
|---|---:|---:|---|---|---:|---|
| **capsule-render** | **1,790** | **44,032** | partly (5 of 15 types) | 69 **colours**, no templates | **15** | Sponsors button |
| leviarista/github-profile-header-generator | 1,316 | — | no (static PNG) | — | — | none |
| whiteSHADOW1234/TypingSVG | 301 | — | yes (typing text) | — | — | none |
| vinimlo/galaxy-profile | 461 | — | yes | — | — | none (GPL-3.0) |
| collectioneur/readme-aura | 138 | — | yes (JSX→SVG) | — | — | none |
| sh4den/readme-animated-sweetbanner | 63 | — | yes | — | — | none |
| mrhx01/TextGlow | 24 | — | yes | — | — | none |
| **gradient-svg-generator (you)** | **6** | **90** (17 third-party) | **yes — 352/355** | **355 templates** | **186** | none |

Smaller entrants: SVG-Crafter (6), Waveify (2), READMEForge (1), svg-readme (0),
gitbanner (36, dead since 2022).

Two of these are not really your competition. **leviarista** (1,316) is a
client-side design tool that exports a static PNG — you download a file, there's
no URL service and no animation. **TypingSVG** (301) is animated text, not
banners. The genuinely comparable newcomers are **galaxy-profile** (461, GPL-3.0)
and **readme-aura** (138) — the latter is the most conceptually interesting
because it compiles React/JSX into animated SVG, and it was pushed 2026-08-03.

### What this table actually says

**No rival ships a large curated preset library.** Nothing in the field has a
named-template collection above ~100, and most have no template concept at all —
they hand you parameters. That specific niche is genuinely uncontested, and it is
the one you occupy.

**But be careful how you say it.** Your lead is in *curation* and in *effect
count* (186 vs 15). It is **not** a lead in "possible outputs" — see §3, where
capsule-render's reachable space turns out to be much larger than its 15 types
suggest. Getting this distinction wrong is the single most likely way your
positioning gets torn apart in public.

---

## 3. capsule-render in detail — the one comparison that counts

Verified from its source tree (`model/normalModel/`, `model/animationModel/`) and
README, not from memory:

**15 `type` values, split into two groups:**

- **10 "normal" models** — `wave`, `rect`, `slice`, `soft`, `rounded`, `cylinder`,
  `egg`, `shark`, `speech`, `transparent`. These are **static shapes**. No animation.
- **5 "animation" models** — `waving`, `venom`, `blur`, `pulse`, `checkered`.
  These are the only animated backgrounds it has.

**5 `animation` values** — `fadeIn`, `scaleIn`, `blink`, `blinking`, `twinkling`.
Note these animate the **text entrance**, not the background artwork.

**69 named colour presets** — counted by parsing its source JSON, not eyeballing:
`src/gradient.json` = **31** gradients, `src/pallete.json` = **29** solids,
`src/pallete_theme.json` = **9** themes (default, dark, radical, merko, gruvbox,
gruvbox_light, tokyonight, onedark, cobalt).

**Plus 5 dynamic colour modes** (`auto`, `timeAuto`, `random`, `gradient`,
`timeGradient`) **and unbounded custom multi-stop colour** — `checkCustomColor` in
`src/verification.ts` parses any number of stops (`0:EEFF00,50:...,100:a82da8`).

### ⚠️ Its real combinatorial space — read this before writing any copy

This is the number that will be used against you:

| Axis | Count |
|---|---:|
| types × named colours | 15 × 69 = **1,035** |
| × 5 text animations | 5,175 |
| × `reversal` × `section` | **20,700** |
| × arbitrary custom hex | **effectively infinite** |

**capsule-render can produce over 20,000 distinct named-parameter visuals without
a single custom hex code.** So "355 templates beats 15 types" is apples-to-oranges
and **will not survive a sceptic.** The honest comparison is effects-to-effects
(186 vs 15) or curation-to-curation (355 finished looks vs 0), never
templates-to-types. `02-positioning-copy.md` is written to that constraint.

**Other params:** `text`, `desc`, `height`, `fontSize`, `descSize`, `fontColor`,
`fontFamily`, `fontAlign`, `fontAlignY`, `descAlign`, `descAlignY`, `rotate`,
`stroke`, `strokeWidth`, `textBg`, `section` (header/footer), `reversal`,
`customColorList`, `theme`.

**Status: actively maintained** — last push 2026-08-04, i.e. today. It is not a
dead project you can out-wait.

**Monetization: a GitHub Sponsors button** (`.github/FUNDING.yml` →
`github: [kyechan99]`) and nothing else. No paid tier, no watermark, no rate
limits at 44,032 embeds.

### The genuine capability gaps — in both directions

capsule-render does things you don't:

- **`section=footer`** — matching header/footer pairs for the top and bottom of a README.
- **`desc` / subtitle** with independent size and alignment.
- **`fontFamily`** selection.
- **Automatic/time-based colors** (`timeAuto`, `random`) — the banner changes on its own.
- **Shape silhouettes** — the wave/egg/shark cut-outs are its whole visual identity.
  Yours are rectangles with effects inside them.

You do things it doesn't:

- **355 curated named presets.** capsule-render names *colours* (69 of them) but
  has **no concept of a named template** — you assemble the look yourself from
  type + colour + animation. Nobody hands you a finished "neural network" banner.
- **186 distinct rendering effects vs its 15.**
- **352 genuinely animated templates vs its 5 animated models.**
- **Correct cache headers** (see below).
- **A visual editor and browsable gallery.** capsule-render has a demo page; the
  discovery experience is a README table.

**The most important asymmetry:** capsule-render is a *shape* generator with a
colour parameter. You are an *effect* generator with a preset library. A sceptic
will (correctly) point out that comparing your 355 templates to its 15 types is
apples-to-oranges — which is exactly why the positioning copy compares
**effects to effects** (186 vs 15) and never "templates to types".

### The one place you are objectively better engineered

capsule-render ships Vercel's default `Cache-Control: max-age=0, must-revalidate`.
That means **GitHub's Camo proxy refuses to cache it**, so it takes an origin hit
on essentially every README view worldwide, across 44,032 embeds.

You ship `public, max-age=31536000, immutable`, which Camo honours — verified by
live probe (`X-Cache: MISS` → `HIT`, hit counter climbing).

This is a real, checkable engineering judgment you won against a project 300× your
size, and it is the single most credible technical claim you own.

---

## 4. Adjacent tools — not competitors, but they set expectations

| Project | Stars | What it does | Why it matters to you |
|---|---:|---|---|
| github-readme-stats | 79,824 | Stat cards | Sets the "best-effort, self-host for reliability" norm |
| readme-typing-svg | 9,169 | Animated typing text | The other animated-SVG service; ~81k embeds |
| shields.io | — | Badges | 1.6B images/mo on **$1,437/yr** — the category's economics |
| skill-icons, github-profile-trophy | large | Icon/trophy rows | Compete for the same README real estate |

These matter for two reasons. First, **every one of them is free and MIT**, which
sets an unshakeable price expectation of zero. Second, **every one of them ships a
best-effort disclaimer and tells heavy users to self-host** — that is the category
norm, and adopting it costs you nothing (see `03-monetization-verdict.md` §5).

---

## 5. The distribution gap, stated plainly

| | You | capsule-render | Ratio |
|---|---:|---:|---:|
| Stars | 6 | 1,790 | 298× |
| Forks | 1 | 731 | 731× |
| Third-party embeds | **17** | **44,032** | **2,590×** |
| Distinct rendering effects | **186** | **15** | **0.08×** (you lead 12×) |

**Read the last row against the first three.** You have twelve times the visual
range of the market leader and 0.04% of its reach. Nothing in this landscape
suggests you need a better product. It says almost nobody knows this one exists.

That is a far more tractable problem than "build something better than
capsule-render", and it is why `03-monetization-verdict.md` recommends spending
zero hours on billing and all of them on distribution.

---

## 6. Where you are genuinely vulnerable

Honest risks, so they don't surprise you later:

- **Its output space dwarfs yours** (20,700+ named combinations vs your 355). Any
  size claim you make invites this counter, and you lose it. Compete on curation
  and effect count only.
- **capsule-render is alive and shipping** (pushed today). It already has 69 named
  colours and a theme system — adding a named-preset layer is a weekend's work for
  them. Your lead is in curation, which is copyable.
- **The niche is crowding, and faster than it looks.** galaxy-profile (461),
  TypingSVG (301) and readme-aura (138) all have more traction than you, and
  readme-aura was pushed yesterday. The idea is not scarce.
- **Your differentiator is taste, not technology.** 186 effects is a content
  moat, and content moats erode when someone with distribution decides to copy
  them. Your advantage is real but it is not durable on its own.
- **Shape silhouettes are capsule-render's identity and you don't have them.**
  For many users "the wave one" *is* the product. Rectangles-with-effects is a
  different aesthetic, not a strictly superior one.
- **Six stars means nothing is validated.** Every claim about what users want
  here — including mine — is inference from competitors, not evidence from yours.
