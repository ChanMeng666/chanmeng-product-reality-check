# echook — is there a business here?

**Straight answer, 2026-08-04.** Written for Chan Meng, against five research reports of the same date.
Every external number carries a source; every internal one carries a file path. What I could not verify
is marked as unverified rather than smoothed over.

---

## The verdict, in one sentence

**No — there is no business in echook as a product, and the research says the answer is already
decided rather than undecided; the best remaining lane is echook as evidence of what you can build,
and that lane is a hypothesis I did not research, not a finding.**

> **Read that last clause literally [corrected after red team].** My first draft called the consulting
> lane "the one thing here that has never been measured" while the same document listed five other
> unmeasured things, and I sized it off a single Clutch page — of **agency** rates, sample size
> undisclosed — without applying the exists-vs-reachable discount I had imposed on every product
> archetype. That is the method's own cardinal sin: **the discipline was pointed at the number I was
> killing and not at the number I was selling.** An unsized lane reads as the most valuable lane on the
> page because the reader fills it with their own optimism. So: the consulting lane is **explicitly
> unresearched**, its price anchor describes agencies rather than solo maintainers, and a realistic
> solo figure is nearer the **bottom** of that band. It is still the best available option. It is not an
> evidenced one.

The realistic annual pool for the software, summed bottom-up across every buyer archetype that survived
scrutiny, is **$0–$200**. Not "small." Not "early." The median outcome is zero, and three of the four
archetypes size to exactly zero.

One sourced comparison makes the shape of this unmistakable: a single custom-project engagement is
priced at **$10,000–$49,000** `[PAGE, Clutch]`. That is **50–250× the entire product pool**, and the
pitch for it is *already shipped* in your README — untracked, unmeasured, with no idea whether anyone
has ever clicked it.

---

## What I do not know, before I tell you what I think

Weakness first, because the conclusions below are only as good as these gaps.

1. **Nobody has been asked.** This engagement interviewed zero buyers. Every archetype is reasoned, not
   observed. That is the largest single weakness in the package.
2. **Nobody knows if echook is used.** There is no telemetry, and 53 releases have carried **zero**
   downloadable assets, so no download counter has ever existed. The one usage-shaped number available
   is clone traffic — and 78 unique cloners against 85 unique viewers is a **92% ratio that no human
   population produces**. It is contaminated by machines to an unknown degree. It cannot be used, and I
   have banned it from every document.
3. **Your own stopping condition was never recorded.** I set the gate thresholds as an outside analyst.
   If your real threshold differs, my instrument is the wrong one and should be replaced in writing.
4. **One competitor claim is unverified.** Cursor's in-app "play sound on finish" setting has no
   Cursor-official URL — three candidate paths 404 and `llms.txt` has no notifications page. Do not
   write any Cursor-gap copy until that is checked.

---

## The four findings that decide it

### 1. Your headline differentiator is the platform's documented default

"AI-operated, not AI-assisted — you don't read this, your agent does" was the strongest claim in the
repo. It is dead. There are **601,280 `SKILL.md` files on GitHub** — the pattern of shipping an
agent-readable instruction file beside a CLI is the ecosystem's default, not an insight. And
`PeonPing/peon-ping` — **4,973 stars**, same niche, MIT, active — ships five Agent Skills whose config
skill description is, near-verbatim, echook's pitch.

> **Citation withdrawn [after red team].** An earlier draft of this section quoted Anthropic's
> engineering blog as writing *"Skills are authored for agents rather than humans."* The red team could
> not find that sentence on the cited page (143,670 bytes, zero hits) or on the two likeliest
> alternatives, though two other quotes from the same citation matched exactly. **I am treating the
> quote as unsourced and removing it rather than softening it.** The conclusion does not depend on it —
> it stands on the 601,280 files and on peon-ping — but a fabricated-looking quote in a document about
> honesty would have discredited everything around it, and it was mine, not the research's.

This is the ordinary outcome of a competitor sweep and it is not a judgment of the work: the
differentiator you led with is table stakes. What survives is narrower and genuinely yours — see §5.

### 2. Nobody has monetized anything in this ecosystem, and there is no rail to do it on

An exhaustive search found **no Claude Code plugin, skill or MCP server with disclosed revenue.** The
Claude Code plugin and marketplace schemas contain **no price, payment or entitlement field** — install
is `git clone`. Cursor uses Open VSX. Codex has no rail at all. VS Code's `pricing` property accepts only
`Free` or `Trial`, and the premium-extensions request has been open since **2020-02-14**.

The single paid case found anywhere adjacent is **Ref (ref.tools) at $9/mo, "hundreds of subscribers"** —
and it is a *hosted metered index*, not a plugin sale. That is the distinction that separates every dev
tool that can charge from every one that cannot: **a service the user cannot self-host.** echook is MIT,
fully local, no server, no data. It has none of the characteristics.

### 3. The donation path has already run for nine months and returned zero

This is not a forecast. Your GitHub Sponsors listing is live, you have **222 followers, and 0 sponsors.**
The experiment completed.

The base rate says that is normal, not personal: of 15 Open Collective ledgers in the 50–99★ band,
**14 received $0**; **93%** of owners of 70–90★ repos have zero public sponsors; and the median npm
project that had *already opened* a donation page collected **$55 over nine months** (ICSE 2020) `[PAGE]`.
The ceiling is not about quality — **husky has 35,249 stars, is "used by 1.2M+ projects," and runs on an
estimated annual budget of $410.00** `[PAGE]`.

### 4. You shipped hardest in the period you grew least

June–July 2026 was the heaviest shipping stretch in the project's history — v6.0.0 through v6.4.0, ten
releases. New stars over the same period: **9 in June, 4 in July.** The peak was **19, in April.**

Building more did not produce more demand. That is the finding that matters most for what you do next,
because it means another feature is not the missing piece. (A star was also removed *during* this
four-hour engagement — 79 to 78.)

**One comfortable story is not available.** "The platform absorbed my category" would explain all of
this, and it is **false**: `ccstatusline` grew ~25× and `ccusage` ~6× *after* Anthropic shipped the
native features, and `ccstatusline` now does **407,682 monthly installs**. The category is thriving.
echook is not in it. The problem is distribution and demand, not absorption — an uncomfortable finding
that points at fixable things rather than at fate.

---

## What actually survives, and is yours

Two things. Both narrower than what they replace, and both real.

**S1 — ~~Per-event granularity~~ → Cross-editor coverage with sounds included. [CORRECTED after red team]**

**I got this wrong in the first draft and the correction matters.** I originally claimed per-event
granularity as the surviving differentiator, comparing echook against Anthropic's *mobile push* — which
genuinely has two toggles and, in their words, *"no per-event configuration."* But that is the wrong
comparator. echook does not run on mobile push; it runs on the **hook** surface. And Claude Code's
`Notification` hook matcher already filters on notification type, with these values documented
verbatim: `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog`,
`elicitation_complete`, `elicitation_response`, `agent_needs_input`, `agent_completed` `[PAGE]`.

**That is per-event notification configuration, shipped free by the vendor.** echook's own README table
lists those same eight matchers — it is *wrapping* Anthropic's granularity, not adding to it. The
falsifier I wrote for S1 ("Anthropic ships per-event notification config") **had already fired before I
wrote it**, and the competitor sweep's own scorecard said so, marking per-event granularity `ABSORBED`.
I led with the friendlier fact in three documents. That was the single worst error in this package.

**What is left of S1, stated honestly:** Anthropic documents 38 hook events but ships **no sound assets,
no themes, and no cross-editor story**. echook's real remaining edge is (a) batteries-included audio —
the sounds exist, mapped, without you sourcing or wiring files — and (b) **Cursor and Codex**, which
Anthropic's surface does not cover at all. That is a packaging-and-coverage advantage, not a capability
one. It is a lead measured in months, not a moat, and it is thinner than the first draft claimed.

**S2 — The architecture.** No interactive path anywhere; every operation is a non-interactive
JSON-in/JSON-out CLI command; hand-editing unsupported by design; **the manifest derives its hook list
from live code and therefore cannot lie.** 292 passing tests, CI across three OSes and three Python
versions, a release script that updates 8 files atomically. This is a *property*, not a priority claim,
so no amount of prior art touches it. The diagnostic — whose job was to attack the product — independently
called this the best-engineered thing in the repo.

**And the argument that needs no superlative at all**, every number `gh api`-checkable in a minute:

> Nine identifiable projects independently built agent-completion notifications for Claude Code between
> August 2025 and February 2026. Seven have not been touched in six months or more; the largest,
> `Claude-Code-Remote`, had 1,275 stars and 135 forks when it stopped. echook is one of the few still
> shipping.

**Two corrections after the red team, both against me.** (1) I wrote "2,016 stars and 200+ forks" and
called every figure checkable in a minute — **the seven enumerated projects total 1,770, and the number
does not reconstruct.** It is struck rather than adjusted, because a figure sold as instantly checkable
that fails on checking is worse than no figure. (2) I wrote *"convergent invention is evidence the gap is
real"* as an assertion; the source report explicitly says **do not assert either direction** — several
capable people building the same thing and stopping is equally consistent with "the gap is real" and
"they discovered there was no demand," and the second reading is the one this package's other findings
support.

*Honest limit, also recorded:* this supports "still shipping," **not** "the maintained one" — echook's
last push (2026-07-19) is older than nine active competitors', several of which pushed on 2026-08-04.

---

## The one demand signal that should worry you most

On the Claude Code issue tracker, **notification** feature requests drew 69 / 65 / 42 / 40 / 37
reactions. ***Sound*** requests drew **1 / 1 / 0 / 0.**

**[STRENGTHENED after red team]** The first draft rested this on four issues, which is a small sample
carrying heavy weight, and it also claimed "chime requests: zero issues" — **that was false**, a search
returns two. The red team ran the falsifier I had listed and skipped: **all 38 sound-related issues, in
every state, total roughly 68 reactions between them.** One notification issue outdraws the entire sound
corpus. The finding is not an artifact of cherry-picked issues; it is the whole population.

And the sharpest single data point is one I had buried as an anonymous zero. Issue **#73384 — "built-in
distinct notification sounds for 'needs input' vs …"** is, almost word for word, echook's pitch. It has
**zero reactions.**

People overwhelmingly want to be **told**. Very few want to be **serenaded**. echook's differentiation
sits in precisely the dimension with the weakest demonstrated demand — and the one issue that describes
echook's exact value proposition attracted nobody at all. **This, not the sizing arithmetic, is the
strongest argument against the product**, and it is now the best-evidenced finding in the package.

---

## What to do

### Do this week — 23 minutes, and it is the highest-return work available

Your README currently contradicts itself on the headline feature. The true hook count is **37**
(`bin/audio-hooks.py:162-203`). README lines 11 and 68 say **39**; `llms.txt:30` says **39**; the GitHub
repo description, `.claude-plugin/marketplace.json:8` and `plugins/audio-hooks/.claude-plugin/plugin.json:4`
all say **26**. README:11 also still says **v6.2.0** while you shipped **v6.4.0**. README:137 says "6 on by
default"; it is **3**, and three table rows promise sounds that ship silent.

There is an unusually sympathetic reason for this, and you should know it before you wince: the diagnostic
verified via `git show <tag>` that the catalog **was** 26 at v6.1.0, **39** at v6.2.0, and **37** after
v6.3.4's rollback. *Every wrong number was true when it was written.* This is not carelessness — it is
stratigraphy. Which is why the fix is not "be careful" but **connect the manifest to CI**, exactly as you
already did for the generated surfaces.

1. **GitHub repo description + `homepageUrl`** — 3 minutes. `homepageUrl` currently points at a
   `user-attachments` video URL. This is the only fix that works *before* the click: Google is your #1
   referrer (51 visits) and the description is the search snippet.
2. **README:11 and :68** — version and count — 10 minutes.
3. **README:137 "6 on by default" → 3**, plus the three wrong table cells — 10 minutes.

Also: add one paragraph to `SECURITY.md` explaining that GitGuardian #34199726 was **synthetic** (the
public jwt.io demo token and AWS's own `AKIAIOSFODNN7EXAMPLE` placeholder) and the forward-fix was
correct. A history rewrite is *not* warranted. Write it so a diligence reader finds the reasoning before
they find the `AKIA` string.

### Then run exactly one commercial test — one afternoon, reports 2026-08-25

Open a **$5 one-time supporter licence** on Polar or Lemon Squeezy. This bypasses the missing payment
rail entirely. Announce once to your 78 stargazers and the plugin directories. Count for 14 days.

- **≥ 25 payers → GO.** Falsifies the assumption carrying ~100% of the realistic pool.
- **≤ 4 payers → stop the commercial track.** Move to the maintainer track below.

Both thresholds are printed on purpose. The anchor is Pushover's **$4.99 one-time** licence `[PAGE]` — and
that is an *upper* bound, because Pushover runs a hosted delivery network and echook is MIT and local.

### And take the maintainer track seriously — it is the actual answer

The highest-value lane in this engagement is **you, not the software**, and it is the only one that is
*unmeasured* rather than *measured-at-zero*:

- Replace the bare `mailto:` in the README hire pitch with a **tracked link** — 1 hour.
- Publish **one** technical write-up of something genuinely hard you solved here — cross-harness hook
  normalization across three editors with incompatible event models, or the width-aware status-line
  reflow. That is a portfolio artifact and a distribution channel at the same time.
- Note the two pitches must never appear in the same post. The product pitch goes to a market that has
  not paid; the competence pitch goes to a market with a **$10,000–$49,000** sourced price.

---

## What this document does not say

**It does not say echook is bad, or that nine months were wasted.** Those are unrelated questions and the
research answers the second one favourably. The engineering here is better than the marketing: a manifest
that cannot lie, 292 tests, three-OS CI, 53 disciplined releases, and a genuinely agent-operable surface
that works — the claim that fails is only that *being agent-operable is distinctive*, not that echook
*is* agent-operable. It is.

**And one thing I undersold badly enough that the red team had to hand it back to me.** Buried fourteen
findings deep in the diagnostic is this: you shipped `SYNTHETIC_VARIANT_DEFAULTS` **off**, with a comment
recording that you could not observe those events firing. You refused to claim a feature you could not
verify. That is the exact discipline this entire package exists to enforce, practised unprompted, in
code, where nobody was going to see it. My summary of your engineering was "292 tests, three-OS CI,"
which is the generic version. **The specific version is better evidence of how you work than any metric
in this document** — and it is precisely the kind of thing the maintainer-track write-up should be
about.

What the research says is narrower and harder: **this specific artifact, in this specific ecosystem, at
this moment, has no payment rail, no demonstrated willingness to pay, a free substitute published by the
platform vendor, and a demand signal pointing at the one axis it does not differentiate on.** Those are
facts about the market, not about the builder.

---

## What would prove all of this wrong

Ordered by cost to test. **Items 1 and 2 landing together overturn the verdict; anything else dents it.**

| # | Signal | Why it decides things | How to test | Cost |
|---|---|---|---|---|
| 1 | **≥25 people pay $5** | Falsifies the assumption carrying ~100% of the realistic pool | Polar/Lemon Squeezy licence, 14-day count | 1 afternoon |
| 2 | **≥2 of 20 named orgs ask for a quote** | Reopens the enterprise lane that correction C5 closed | Email 20 named targets a concrete offer, not a survey | 2 days |
| 3 | **Telemetry shows ≥100 machines/week firing hooks** | Converts "78 stars" into real adoption and reopens every funnel argument | Ship opt-in reporting; the NDJSON log already records the events, it just has no return path | 1 day |
| 4 | **A sound-related Claude Code issue crosses ~40 reactions** | Overturns the adverse demand finding in §"the one demand signal" | Watch the tracker quarterly | minutes |
| 5 | **Anthropic ships per-event notification config** | Kills S1 outright — the most likely event on this list | Watch the changelog monthly | minutes |
| 6 | **peon-ping ships per-event granularity** | Kills S1 | Watch its releases monthly | minutes |

### The steelman I could not refute

*Everything above measures a world that already exists. If fleets of parallel background agents become
the default way people work within two years, then "how many people today want per-event audio" is
backward-looking by construction — the buyer counts are all drawn from a pre-fleet world, and the
notification layer for ten concurrent agents is a different, larger product than the one being sized.*

I cannot refute this and I am not going to pretend to. It is also **unfalsifiable in the present tense**,
which is exactly why the dated tests above exist. So the correct posture is to **date it, not reject it**:
if tests 1–3 have not moved by **2026-11-04**, the market is not being created on the timeline this
argument assumes, and the argument stops being a reason to keep building.
