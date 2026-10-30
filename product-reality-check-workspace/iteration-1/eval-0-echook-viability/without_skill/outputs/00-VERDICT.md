# echook — Straight Verdict

**Date:** 2026-08-04 · **Subject:** github.com/ChanMeng666/echook (v6.4.0, MIT, 9 months, 152 commits)

---

## The answer you asked for

**No. There is no business in echook as a product, and you should stop investing months in it.**

Not because it is badly built — it is unusually well built, and I will come back to that. Because
three things are all true at once, and any one of them alone would be enough:

1. **The platform now ships both of your tracks natively, for free, and generates them from natural
   language.** As of Claude Code v2.1.141+, the `Notification` hook event carries the exact matchers
   you sell (`agent_completed`, `permission_prompt`, `idle_prompt`), plus a `terminalSequence` field
   with copy-paste examples for a desktop toast and a terminal bell in Anthropic's own docs. And the
   status-line stdin JSON now hands you `context_window.used_percentage`, `cost.total_cost_usd`,
   `exceeds_200k_tokens`, `session_name`, `effort`, `fast_mode`, `agent.name`, `pr`, `worktree`,
   `vim` — **and `rate_limits.five_hour` / `rate_limits.seven_day` with `used_percentage` and
   `resets_at`.** That last one matters: quota visibility was the one gap my research identified as
   still unowned. It is now closed. Anthropic ships it.

2. **Your headline differentiator is now the platform's default.** echook's pitch is "you type one
   slash command, then natural language forever." Claude Code's `/statusline` command "accepts
   natural language instructions describing what you want displayed" and writes the script for you.
   *Being AI-operated is no longer a feature; it is the substrate.* The thing that made echook
   special in November 2025 is a bullet point in the vendor docs in August 2026.

3. **You are not winning the free race, so you certainly won't win the paid one.** echook has 78
   stars. In the same category: `vibe-notch` 2,479 · `Claude-Code-Remote` 1,275 (abandoned) ·
   `Lucarne` 324 · `wyattjoh/claude-code-notification` 94. In the status-line/context category you
   are competing with `claude-hud` (27,066 stars, seven months old), `happy` (23,083),
   `ccusage` (17,700), `ccstatusline` (12,203), `Claude-Code-Usage-Monitor` (8,582). All MIT or
   equivalent. All free. You are roughly 1/350th of the leader in your own second track.

---

## The traction numbers, without flattery

| Signal | Value | Read |
|---|---|---|
| Stars | **78** in 9 months | ~0.28/day, flat |
| Stars last 86 days | **20** | No acceleration — there was never a moment |
| Unique visitors, last 14d | **85** (174 views) | ~6 people/day look at it |
| Unique cloners, last 14d | **78** (137 clones) | Inflated by CI/mirrors; real installs are lower |
| Forks / watchers | **7 / 1** | — |
| Issues ever / PRs ever | **1 / 0** | **Nobody has ever contributed. Nobody has ever complained.** |

That last row is the one to sit with. 152 commits, 39 hook events, three editors, six major
versions — and in nine months not one outside person cared enough to open a pull request or file a
bug. That is not a community. That is you, alone, in a room, building for an audience that has not
arrived.

**Estimated real user base: a few hundred, at the generous end low thousands.** There is no
telemetry, so this is inferred from clone/visitor traffic. Do not model it higher.

---

## "But who would pay?" — the honest answer

I looked hard for a buyer. Here is every candidate and why each one fails.

| Candidate buyer | Would they pay? | Why not |
|---|---|---|
| Solo dev who wants a sound | **No** | It is a documented one-liner in Anthropic's docs. Actual quote from HN: *"It would have surely taken less time to just set up notifications for Claude Code."* |
| Power user running 5+ parallel agents | **Maybe $10–20/mo** | Real emerging pain, and per-agent audio identity is genuinely wanted. But the segment is small and Conductor ($50/mo), Omnara ($20/mo) and free `cmux`/`happy` are already there |
| Engineering manager wanting agent observability | **Yes — but not from you** | Real budget ($29–59/seat: LinearB, Jellyfish). But Anthropic ships **free** first-party Claude Code analytics with a leaderboard, CSV export, OTel and an Analytics API. And the incumbents need 30–50 seat minimums and a sales motion you cannot run solo |
| Enterprise wanting compliance/audit of agent use | **Yes, at real money** | echook does not do this, and building it is a different company |

**Willingness-to-pay evidence, both directions, is lopsided.** I found *zero* instances of a
developer saying they would pay for agent notifications. I found several saying they would not —
including in Omnara's own Launch HN thread, where a YC-funded company with a mobile app and cloud
service raised its price to $20/mo and got told *"$20/month for something an engineer can hack in a
couple hours"* and *"you're just driving people to happy"* (the free MIT competitor).

**The revenue ceiling, if you did everything right:** ~1,500 lifetime users × 1–3% dev-tool
conversion × $5/mo ≈ **$75–225/month gross**, before fees, tax, and support load — and that assumes
users pay rather than switching to one of a dozen free alternatives, which they would. Realistically
you are looking at **$0–50/month.** GitHub Sponsors at 78 stars is a tip jar: the lifetime *mean*
across every maintainer who ever received a Sponsors dollar is ~$17/month, the median is $0, and
~75% of maintainers get nothing. core-js has **nine billion downloads** and its maintainer collects
~$400/month.

---

## What is actually valuable here (this part is real)

I am telling you to stop monetizing echook, not that the last nine months were worthless. Three
things came out of it that are worth more than the product:

1. **The agent-first operating pattern is the real IP.** `llms.txt` + a live `audio-hooks manifest`
   as source of truth + every capability a non-interactive JSON-returning subcommand + zero
   human-interactive paths + a scope guard that names what the project refuses to do. That is a
   *design methodology* for building software that an AI agent operates, and it is genuinely ahead of
   where most people are. The mp3 files are not the interesting part. **That is.**

2. **Cross-editor parity is the one thing the platform will not give anyone.** Anthropic's
   `terminalSequence` is Claude-only. Cursor's and Codex's surfaces are different and worse (you
   documented that Codex's status line cannot even render custom text). One tool that speaks all
   three is a real, if narrow, position — and it is defensible precisely because no single vendor
   will build it.

3. **Career signal.** This is evidenced, not a consolation prize: a study of ~22,900 developers found
   OSS activity elevated ~16% during job-search periods, concentrated in high-visibility repos. A
   six-major-version, three-editor, 39-event, CI-tested, contract-tested project with a promo video
   is a strong artifact to point a hiring manager or a consulting client at. That value is fully
   realized *right now*, and every additional month of features adds approximately nothing to it.

---

## What to do (in priority order)

1. **Freeze echook at v6.4.0.** It is feature-complete against a platform that has caught up. Move to
   security-and-breakage maintenance only. Budget: a few hours a month, not months.

2. **Rewrite the README's top 200 words within the week.** Right now it leads with "AI-operated audio
   notification system," which is the exact thing Anthropic made free and native. Lead instead with
   the two claims that are still true and still unmet: **one notification layer across Claude Code +
   Cursor + Codex**, and **distinct audio identity per parallel agent**. Add one honest line saying
   when you *don't* need echook (single-agent, Claude-only → use the native hook). Being the tool
   that tells you not to install it buys more credibility than another feature.

3. **Do not build a paid tier, a licence server, or a cloud dashboard.** Every hour spent there is
   an hour spent competing with a free version of yourself, a free first-party feature, and a
   funded startup's free tier. This is the Kite failure mode: widely installed, genuinely liked,
   *"our product did not monetize, and it took too long to figure that out."*

4. **Harvest the methodology instead of the product.** Write up "how to build a project an AI agent
   operates end-to-end" — the manifest-first pattern, the no-interactive-paths rule, the scope
   guard — with echook as the worked example. That is a talk, a post, and a consulting calling card.
   The pattern is transferable; the sounds are not. This is the Caleb Porzio move: the OSS is the
   funnel, the sale is something adjacent.

5. **Spend the next months on a problem with an operational risk surface.** The one dev-tool
   monetization pattern that reliably works (Sidekiq: ~$80k/month, one person, zero employees) is
   *free core + paid tier that de-risks something expensive in production*. Nobody's deploy breaks
   because a status line is wrong. Pick a problem where it does.

---

## How to prove me wrong in two weeks, cheaply

I could be wrong, and you should not take my word over the market's. Run this before writing a line
of billing code:

- Put a **"echook Pro — $5/mo, coming soon"** button on the README with three concrete named
  features. Do not build anything. Count clicks for 14 days.
- **Threshold: 30 distinct clicks.** Below that, the answer is settled and you close the file. Above
  it, you have found something my research did not, and it is worth one more look.

My prediction, stated plainly so it is falsifiable: **you will get fewer than 10.**

---

## One-line summary

echook is a well-engineered answer to a question the platform now answers for free, with 78 stars, no
contributors, no willingness-to-pay evidence anywhere in the category, and free competitors 30–350×
its size — so keep it as a finished, frozen portfolio piece and a cross-editor niche tool, harvest
the agent-first methodology as your actual differentiator, and put the next months into a problem
where something breaks when the tool is absent.
</content>
