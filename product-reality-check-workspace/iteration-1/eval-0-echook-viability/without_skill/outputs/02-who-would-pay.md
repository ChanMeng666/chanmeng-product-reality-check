# echook — Who Exactly Would Pay?

**Date:** 2026-08-04 · Companion to `00-VERDICT.md`

You asked "who exactly would pay." This file works through every candidate buyer I could construct,
scores each one, and shows the arithmetic. The short version: **four of the five segments are
non-buyers, and the one segment with real money cannot be served by a solo maintainer.**

---

## Scoring method

Each segment is scored on five dimensions, 1–5:

- **Pain** — how badly it hurts today
- **Frequency** — how often it hurts
- **Budget** — is there money, and whose
- **Substitute gap** — how bad the free/native alternative is (5 = no good alternative)
- **Reachable** — can a solo maintainer actually find and sell to these people

A segment needs roughly 4+ on *all five* to be a business. Anything with a 1 or 2 on Budget or
Substitute gap is dead regardless of the other columns.

---

## Segment A — The solo developer who wants a sound when the agent finishes

*"I walk away and don't know when it's done."*

| Pain | Freq | Budget | Substitute gap | Reachable | Verdict |
|---:|---:|---:|---:|---:|---|
| 3 | 5 | **1** | **1** | 4 | **Dead** |

This is echook's current core user, and it is the worst segment in the analysis.

The pain is real and constantly re-expressed — I found HN comments roughly every 2–3 weeks from Aug
2025 through Jul 2026 asking for exactly this. But the substitute gap has collapsed to zero:

- Anthropic's own hooks docs ship a copy-paste desktop-notification example and a one-line terminal
  bell, with an `agent_completed` matcher.
- Ghostty has native Claude Code "finished" push notifications.
- macOS users pipe `afplay`; Linux users use `notify-send`; several people just use `piper` for TTS.
- ~25 free OSS repos do it, four of them larger than echook.

And the willingness-to-pay evidence is not merely absent, it is actively negative. The cleanest quote
in the entire corpus is dbbk on HN, 2026-03-20: *"It would have surely taken less time to just set up
notifications for Claude Code."*

**Price this segment will pay: $0.** Not "low." Zero. Any paywall here converts them into users of
one of the free alternatives, and you lose the portfolio value too.

---

## Segment B — The multi-agent power user (5+ parallel agents)

*"I'm running six worktrees and I can't tell which one just stopped."*

| Pain | Freq | Budget | Substitute gap | Reachable | Verdict |
|---:|---:|---:|---:|---:|---|
| 4 | 4 | 3 | **4** | 2 | **Marginal — the only one worth a second look** |

This is the interesting segment and the only place echook has a genuine, unmet, independently
requested capability.

**Why the substitute gap is real here.** Anthropic's `terminalSequence` gives one bell for one
session. It cannot tell you *which* of your six agents needs you. Three independent sources asked for
exactly this:

- FlorisFok, 2026-03-29 — wants notification *"when one of them is done with stereo and pitch that
  identifies"*
- Voxlert — gives each Claude Code session a distinct character voice
- `cmux-skills` — signals green/yellow/red per workspace tab with sound and optional voice

echook already has the machinery for this: 39 events, per-tool-type sounds, two themes, TTS, webhook
fan-out. **Distinct audio identity per parallel agent is a feature the platform structurally will not
ship**, because Anthropic is optimizing one session at a time.

**Why it is still marginal.** Three problems:

1. **The segment is small and self-limiting.** A practitioner quote worth taking seriously: *"3–5
   parallel engineers is the sweet spot. Beyond that, the codebase itself becomes the bottleneck for
   absorbing parallel changes."* The "I run 20 agents" scenario is mostly aspirational.
2. **It is crowded from above.** Conductor ($50/mo), Omnara ($20/mo), plus free `happy` (23,083
   stars), `cmux`, `jmux`, Claude Squad, Harness, Silo, Boxes.dev. And Vibe Kanban — 27,652 stars,
   the most-upvoted tool in this exact category — **shut down because it saw no path to
   profitability.**
3. **You cannot reach them.** They are a diffuse few thousand people worldwide with no channel you
   own. Score of 2 on Reachable is the binding constraint.

**Realistic price if you pursued it: $5–10/mo, to maybe 20–100 people. $100–1,000/month gross, after
another several months of work, in a segment where the leader just died.**

---

## Segment C — The engineering manager who wants agent observability

*"What are my ten engineers' agents doing, and what is this costing me?"*

| Pain | Freq | Budget | Substitute gap | Reachable | Verdict |
|---:|---:|---:|---:|---:|---|
| 4 | 4 | **5** | **1** | **1** | **Real money, unreachable, already free** |

This is where the money in this space actually is, and it is the clearest "no" of all.

**The budget is real.** LinearB charges **$29/contributor/mo (Essentials, 30-seat minimum)** and
**$59 (Enterprise, 50-seat minimum)**, annual billing only, with AI Impact Measurement in both tiers.
Jellyfish's AI Impact module runs roughly **$35–50/engineer/mo** and explicitly tracks Claude Code.
DX and Faros sell into the same budget. The underlying spend they are attacking is large — one vendor
claims Claude Code users average $340/month/developer, seniors $600–800 during intensive work.

**Three separate reasons you cannot have it:**

1. **Anthropic gives it away.** Free first-party Claude Code analytics for Team/Enterprise: daily
   active users and sessions, lines accepted, accept rate, **PR and LoC attribution via a GitHub
   app**, a **top-contributor leaderboard**, **CSV export**, **OpenTelemetry** per-user token and cost
   export, per-user spend reports, and a `read:analytics` **Analytics API** on Enterprise. This is
   more authoritative than anything a third party can derive from local files, because it comes from
   the billing system.
2. **The incumbents have the relationship and the seat minimums.** 30–50 seats and annual contracts
   are a sales motion, not a GitHub README.
3. **echook does not do this.** It is a per-developer local notifier. Building a team dashboard is
   starting a different company, with auth, hosting, data retention, SOC 2 questions, and a security
   review for every prospect.

---

## Segment D — Accessibility: blind and low-vision developers

*"I can't see a status line. Audio is not a convenience for me, it's the interface."*

| Pain | Freq | Budget | Substitute gap | Reachable | Verdict |
|---:|---:|---:|---:|---:|---|
| **5** | 5 | 2 | **4** | 2 | **Highest mission value, lowest revenue** |

I am including this because it is the one segment where echook's audio-first design is not a
convenience layer but the primary interface, and where the substitute genuinely does not work: a
visual context bar and a colour-coded quota meter are useless to a screen-reader user, while TTS of
the agent's actual final message plus distinct event sounds are exactly right.

Honest assessment: the market is small, it is chronically under-served, and it overwhelmingly expects
free or subsidized tooling — charging here would be both commercially pointless and a bad look.
**But it is a strong reason to keep echook alive and free, and a genuinely good story for the README
and for any grant, conference talk, or employer conversation.** If you want the project to *matter*
rather than earn, this is the direction with the most integrity.

I did not find primary research on this segment in this pass — it is an inference from the product's
shape, not an evidenced demand finding. Treat it as a hypothesis worth one conversation with an
actual blind developer before you lean on it.

---

## Segment E — Your future employer or consulting client

*"Show me something you built."*

| Pain | Freq | Budget | Substitute gap | Reachable | Verdict |
|---:|---:|---:|---:|---:|---|
| n/a | n/a | **5** | n/a | **5** | **The value that is actually already banked** |

Not a product buyer, but the honest place the nine months converted into value.

The evidence is decent: a study of ~22,900 developers (ifo Institute / *Labour Economics*) found OSS
activity elevated ~16% during job-search periods, with effects concentrated in **high-visibility
repositories**. That measures developer behaviour rather than employer response — it shows OSS is a
rational career investment, not a proven wage premium — but it is the best evidence available, and
the widely-quoted "71% of hiring managers check GitHub" stat is content marketing you should not
repeat.

**The important consequence:** this value is *already fully realized*. A six-major-version,
three-editor, 39-event, CI-tested project with a promo video signals everything a seventh major
version would. **Additional features add approximately zero to this segment.** That is the strongest
possible argument for freezing.

---

## The arithmetic, in one place

Best case, assuming you did everything right and the market cooperated:

```
Lifetime users (generous)                 1,500
× dev-tool free→paid conversion (1–3%)    15–45 paying customers
× $5/mo                                   $75–225/month gross
− payment fees, tax, support time         → call it $50–170/month net
```

For context on that conversion rate: freemium generally runs 2–5% median; **developer tools
specifically run 1–3%**; open-source→paid is conventionally targeted at **1%**, and InfluxData's CEO
frames hitting 1% as *a good outcome*. And every one of those 15–45 people has a free, actively
maintained alternative one `npm install` away, plus a native platform feature.

Realistic case, given 78 stars, ~6 visitors/day, and zero WTP evidence in the category: **$0–50/month.**

GitHub Sponsors as an alternative: the lifetime mean across all maintainers who ever received a
Sponsors dollar is **~$17/month**; the median is **$0**; ~75% receive nothing. core-js — **9 billion
downloads, used by 75–80% of the top 100 websites** — collects ~$400/month and its maintainer has
said publicly he cannot support his family on it. **Usage does not convert to sponsorship. Only an
audience does.**

---

## The one buyer profile that would change my mind

If such a person exists in numbers, I am wrong:

> A developer or small team running **4+ agents in parallel across at least two different editors**
> (e.g. Claude Code *and* Codex), who has been burned by missing an agent's permission prompt, who
> needs to know *which* agent stopped without looking, and who is already paying $100–200/mo for Max
> or Ultra.

That person cannot be served by Anthropic's native hook (Claude-only, one bell, no identity), cannot
be served by `claude-hud` or `ccusage` (Claude-only, visual, single-session), and would find the
$50/mo Conductor tier overkill.

**They are also the only person echook is uniquely built for — and echook's README does not currently
speak to them at all.** See `03-positioning-and-recommendation.md`. Whether there are 50 of them or
5,000 is the single unknown worth spending two weeks to resolve, via the fake-door test in the
verdict — and my prediction is that there are closer to 50.
</content>
