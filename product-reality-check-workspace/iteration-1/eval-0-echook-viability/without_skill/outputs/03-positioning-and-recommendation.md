# echook — Positioning & Recommendation

**Date:** 2026-08-04 · Companion to `00-VERDICT.md`

---

## Part 1 — Why the current positioning no longer works

echook's README leads with:

> **AI-operated audio notification system for Claude Code, Cursor IDE, and Codex CLI.**
> You type one slash command at install time. Then natural language forever.

In November 2025 that was a sharp, differentiated claim. In August 2026 **every clause of it is now
either the platform's default or a free one-liner:**

| The claim | What happened to it |
|---|---|
| "audio notification system" | Anthropic's hooks docs ship a copy-paste desktop-notification example and a one-line terminal bell, with an `agent_completed` matcher and a `terminalSequence` field that works in tmux and on Windows |
| "AI-operated" | `/statusline` accepts natural-language instructions and Claude Code writes the script. The platform is AI-operated by default |
| "one slash command, then natural language forever" | So is everything else now. This is table stakes, not a feature |
| the 29-segment status line | The status-line stdin JSON natively provides context %, cost, `exceeds_200k_tokens`, session name, effort, fast mode, agent name, PR, worktree, vim mode — **and `rate_limits.five_hour` / `.seven_day` with reset timestamps** |

The README is also structured to defend feature *count* — 39 hook events, 30 matcher variants, 29
segments, 2 themes. Feature count is the wrong axis entirely. `Lucarne` is growing four times faster
than echook at 324 stars while positioning on the **opposite** of feature count: *"No hooks, no
skills, no MCP."* Nobody is choosing a notification tool by event coverage.

**What survives the platform's advance — exactly two things:**

1. **Cross-editor parity.** Anthropic's `terminalSequence` is Claude Code only. Cursor's surface is
   different; Codex's status line cannot render custom text at all (you documented this yourself).
   One notification layer that speaks all three is something **no single vendor will ever build**,
   because no vendor is incentivized to make their competitor's product pleasant.
2. **Per-agent audio identity.** The native hook gives one bell for one session. It cannot tell you
   *which* of your six parallel agents needs you. This was independently requested by at least three
   separate sources, and it is structurally outside what Anthropic optimizes for.

Everything else in the README is now a description of features the platform gives away.

---

## Part 2 — The repositioning (concrete copy)

Replace the top of the README with something like this. It is shorter, it is honest, and it targets
the only person echook is uniquely built for.

> # echook
>
> **One notification layer for Claude Code, Cursor, and Codex — so you can tell *which* agent needs
> you without looking.**
>
> Running one agent in Claude Code? You probably don't need this — use the
> [native `Notification` hook](https://code.claude.com/docs/en/hooks), it's four lines and it's
> excellent.
>
> echook is for the case the native hook can't cover: **several agents running at once, across more
> than one editor.** Each agent gets its own sound, so a finished refactor in worktree A and a
> permission prompt in Codex are audibly different events — you know which window to go to before you
> turn your head. Plus TTS of what the agent actually said, phone alerts via webhook, and a status
> line that works the same way in all three editors.
>
> MIT. Zero telemetry. Your AI agent installs and configures it in plain English.

**What changed and why:**

- **Leads with the unmet need**, not the mechanism. "Which agent needs you" is a problem the
  platform does not solve; "plays a sound" is one it does.
- **Tells people not to install it.** This is the single highest-credibility move available to you.
  A tool that names its own limits gets trusted on everything else it claims — and it costs you
  nothing, because that user was never going to be a customer or a contributor anyway.
- **Drops the feature count.** 39 events is an engineering achievement, not a reason to install.
  Move the tables into a collapsed section or the docs.
- **Keeps "your agent installs it"** as a *convenience* claim, not the headline differentiator. It is
  still nice; it is no longer distinguishing.

---

## Part 3 — Recommendation, in priority order

### 1. Freeze at v6.4.0. (This week.)

The product is complete against a platform that has caught up. Declare it done in the README, move
to security-and-breakage maintenance, and budget **a few hours a month, not months**. Every hour of
new feature work from here has a negative expected return: it cannot win the free race, it cannot be
sold, and it adds nothing to the portfolio signal a sixth major version already provides.

Concretely: close the roadmap, stop adding hook events, and let the CHANGELOG end at 6.4.0 with a
"stable / complete" note.

### 2. Rewrite the README's top 200 words. (This week, ~2 hours.)

Per Part 2. This is the highest-value two hours available to you on this project, because it is the
only work that changes who finds it and what they conclude — and it makes the project *more* useful
as a portfolio piece by demonstrating positioning judgement, not just engineering.

### 3. Do not build a paid tier, a licence server, or a cloud dashboard. (Ever.)

You would be competing simultaneously with: a free version of yourself (MIT, already published,
forkable), a free first-party platform feature, ~25 free OSS alternatives, and a YC-funded startup's
free tier. This is precisely the Kite failure mode — heavily funded, ~500k monthly active developers,
widely liked, shut down in 2022 with the founder's postmortem reading: *"our product did not
monetize, and it took too long to figure that out."*

If you ignore this recommendation, ignore it only after the fake-door test in `00-VERDICT.md` clears
30 clicks.

### 4. Harvest the methodology, not the product. (The actual opportunity.)

The genuinely novel thing you built is **not** the sounds. It is the operating pattern:

- `llms.txt` + `AGENTS.md` as the agent-facing source of truth
- a **live `audio-hooks manifest`** command that is authoritative over the docs, so the agent asks
  the program rather than trusting prose
- every capability a **non-interactive, JSON-returning subcommand** — no menus, no `curl | bash`,
  nothing to hand-edit
- an explicit **scope guard** naming what the project refuses to do (no pomodoro, no gamification,
  no URL opening), which stops an agent from "helpfully" expanding it
- config mutation only through validated `set` commands, never file edits

That is a reusable design methodology for *software that an AI agent operates end-to-end*, and it is
ahead of where most of the ecosystem is. It transfers to any project; the mp3s transfer to none. Write
it up with echook as the worked example — a post, a talk, a template repo. That is the Caleb Porzio
pattern (his $112k/yr came from selling screencasts to the audience the OSS built, not from the OSS),
and it is the most replicable value-capture path in the entire monetization dataset.

You have a second worked example of the same methodology sitting in ArchLang. Two independent
instances make it a *pattern* rather than a one-off, which is what makes it publishable.

### 5. Point the next months at a problem with an operational risk surface.

The one dev-tool monetization pattern that reliably works for a solo maintainer is **free core + a
paid tier that de-risks something expensive.** Sidekiq: ~$80,000/month, ~800 customers at
$1,000–2,000/yr, zero employees, 90% inbound — because if your background jobs silently drop, a
company loses money, and Pro/Enterprise buys durability.

Test any future idea against one question: **what breaks, and what does it cost, when this tool is
absent?** Nobody's deploy fails because a status line is wrong. That is why echook cannot be sold,
and it was true on day one — it just wasn't visible until the platform closed the feature gap.

---

## Part 4 — What I would *not* do, and why

To be explicit, since these are the tempting moves:

- **Don't pivot echook to team observability.** Real budget ($29–59/seat), but Anthropic ships free
  first-party analytics with a leaderboard, CSV, OTel and an API, and the incumbents need 30–50 seat
  minimums and a sales motion. It is also a different product, a different company, and a security
  review per prospect.
- **Don't add a mobile app.** Omnara and Conductor are there with funding; `happy` is there for free
  with 23,083 stars; Anthropic shipped Claude Code on the web. You would arrive fourth with no phone
  team.
- **Don't relicense or add a "commercial use" clause.** It is already MIT and forkable, so the clause
  is unenforceable in practice, and changing terms on existing free users of a dev tool is itself a
  reputational event (see the Retool self-hosted-pricing backlash).
- **Don't chase stars with more features.** The star gap to `vibe-notch` (32×) and `claude-hud`
  (350×) is a distribution gap, not a capability gap. More events will not close it.
- **Don't delete or archive it.** It costs nearly nothing frozen, it serves a real niche, and it is
  a genuinely good portfolio artifact. "Stop investing" is not "throw away."

---

## Part 5 — The decision, framed as you asked it

> *"Is there a business here, who exactly would pay, and how should I position it?"*

**Is there a business?** No. Not at 78 stars, not against a native platform feature, not against
25 free competitors, and not in a category whose most-starred product (27,652 stars) shut down for
lack of a path to profitability. The honest revenue ceiling is $0–50/month.

**Who exactly would pay?** Nobody you can currently reach. The only segment with real money
(engineering managers, $29–59/seat) is served free by Anthropic and locked up by incumbents with seat
minimums. The only segment with an unmet need (multi-agent, cross-editor power users) is small,
crowded, and unreachable without a channel you do not have. The strongest evidence in the whole
research corpus is negative: **not one developer, anywhere I looked, said they would pay for agent
notifications** — and several said explicitly they would not.

**How should you position it?** As a finished, free, deliberately narrow tool for the one case the
platform will never cover — several agents, more than one editor, tell me *which* one — and as the
worked example for the agent-first methodology that is the actually valuable thing you invented while
building it.

You asked me to tell you straight before you sink more months in. **Don't sink more months in.** Spend
two hours on the README, close the roadmap, and take the methodology — and the credibility of having
shipped six major versions of something real — to a problem where the tool's absence costs someone
money.
</content>
