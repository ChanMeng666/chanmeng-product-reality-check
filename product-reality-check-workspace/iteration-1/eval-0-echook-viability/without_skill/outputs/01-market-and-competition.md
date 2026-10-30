# echook — Market & Competitive Research

**Date:** 2026-08-04 · Companion to `00-VERDICT.md`

---

## 1. The market is real and large. That is not the problem.

The addressable population of developers using agentic AI coding tools is genuinely big and growing
fast. This is the part of the analysis that comes back positive, which is why it is worth being
precise about — the failure is not a small market, it is that the market's needs are met for free.

**Disclosed vendor figures (primary sources, high confidence):**

- Claude Code hit **$1B run-rate revenue in Nov 2025**, six months after GA
  ([Anthropic, 2025-12-03](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone)).
- **Over $2.5B run-rate by Feb 2026**, "more than doubled since the beginning of 2026." Weekly
  active Claude Code users **doubled since Jan 1**; business subscriptions **quadrupled**. Claude Code
  authored **4% of all public GitHub commits worldwide**
  ([Anthropic Series G, 2026-02-12](https://www.anthropic.com/news/anthropic-raises-30-billion-series-g-funding-380-billion-post-money-valuation)).
- **Enterprise is >50% of Claude Code revenue** (same disclosure). This is the single most important
  line for your question.
- Cursor: **$1B annualized (Nov 2025)**; SpaceX is acquiring Anysphere for **$60B**, expected to close
  Q3 2026 ([CNBC, 2026-06-16](https://www.cnbc.com/2026/06/16/spacex-spcx-cursor-acquisition-ipo.html)).
- OpenAI Codex CLI: ~600K weekly users at the start of 2026 → **5M+ WAU by Jun 2026** (secondary
  sources, medium confidence, but the trajectory is corroborated across several).

**The "credit card already out" cohort (strong primary survey):** State of AI Dev 2026, n=7,258
developers, fielded Apr–May 2026 ([2026.stateofai.dev](https://2026.stateofai.dev/)):

| Monthly personal AI spend | Share |
|---|---:|
| $0 | 39.7% |
| $1–20 | 22.4% |
| $20–50 | 19.3% |
| $50–100 | 7.0% |
| $100+ | 11.5% |

**60.3% already pay something monthly. 37.8% pay ≥$20/mo.** Claude is paid for by 68.8% of
respondents.

**So why does this not help you?** Two reasons, both structural:

1. **The payment relationship is with Anthropic and OpenAI, not with tool vendors.** In that same
   survey of 6,675 developers, **Cursor drew only 129 paying respondents** — a company doing roughly
   $4B ARR. Developers pay the model provider. They do not pay the ecosystem around it.
2. **The money is enterprise, and moving further that way.** Anthropic disclosed enterprise >50% of
   Claude Code revenue, and business subs quadrupled in six weeks while WAU only doubled — i.e.
   monetization is shifting toward enterprise *faster than usage is*. Sacra estimates Cursor at ~60%
   enterprise and reports that **Cursor's individual developer accounts are gross-margin negative.**
   The category leader loses money on exactly the cohort echook targets.

**And there is no commerce rail.** I verified this against primary docs rather than trusting search
summaries: the full Claude Code
[plugin-marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces) (76KB) and
[skills documentation](https://code.claude.com/docs/en/skills) (74KB) contain **199 occurrences of
"marketplace" and zero occurrences of** `pay*`, `monetiz*`, `billing`, `revenue`, `price`, or
`purchase`. A marketplace is a `marketplace.json` in a git repo. There is no store, no accounts, no
billing, no install telemetry, no revenue share. (A widely-circulated claim that Anthropic pays a
"15% revenue share on paid skills" is **unsupported and I believe false** — it cites no primary
source and is contradicted by 150KB of official docs.)

> **Net:** ~8–15M agentic-CLI users globally, ~3–6M personally paying ≥$20/mo *to model vendors*, in
> an ecosystem of 23,500+ skills and 12,700+ MCP servers with **zero payment infrastructure** and no
> precedent of a plugin earning money.

---

## 2. Platform absorption — the kill shot, verified against Anthropic's own docs

This is the decisive finding and I checked it firsthand rather than relying on secondary reporting.

### Track 1 — notifications: **absorbed**

From [code.claude.com/docs/en/hooks](https://code.claude.com/docs/en/hooks):

- The `Notification` event supports matchers `permission_prompt`, `idle_prompt`, `auth_success`,
  `elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`, and
  **`agent_completed`**.
- A **`terminalSequence`** field (v2.1.141+) emits OSC 0/1/2/9/99/777 and BEL — desktop
  notifications on iTerm2, Windows Terminal, WezTerm, Kitty, Ghostty, Warp; window titles; taskbar
  progress; terminal bell. It explicitly solves the `/dev/tty` problem hooks used to have, works
  inside tmux/screen, and works on Windows.
- The docs ship **copy-paste examples** for both a desktop notification and a bell.

That is echook's entire first track, documented by the vendor, in about eight lines of bash.

### Track 2 — status line: **absorbed, including the field you thought was open**

From [code.claude.com/docs/en/statusline](https://code.claude.com/docs/en/statusline), the stdin JSON
now includes:

```
context_window.used_percentage      context_window.remaining_percentage
context_window.context_window_size  exceeds_200k_tokens
cost.total_cost_usd                 cost.total_duration_ms   total_lines_added
model                               session_name             effort            fast_mode
agent.name                          pr.{number,url,review_state}
worktree.{name,path,branch,original_cwd}                      vim.mode
rate_limits.five_hour.{used_percentage, resets_at}
rate_limits.seven_day.{used_percentage, resets_at}
```

Compare that list against echook's 29 documented status-line segments. It is substantially the same
list. **Note `rate_limits` in particular:** my demand research concluded that quota visibility was
the one pain the platform had *not* closed and that `ccusage` owned it. That conclusion is now out of
date — Anthropic ships five-hour and seven-day quota percentages and reset timestamps as first-party
stdin JSON.

And the delivery mechanism kills the positioning as well as the features: **`/statusline` accepts
natural language instructions describing what you want displayed, and Claude Code writes the script.**
The docs' own example is *"/statusline show model name and context percentage with a progress bar."*

> echook's core pitch — "one slash command at install, then natural language forever" — is now
> literally how the platform works by default. You cannot differentiate on being AI-operated when the
> platform is AI-operated.

**Sherlocking is a quantified risk, not a hypothetical:** Apple shipping features natively is
estimated to affect ~$393M/year of third-party app revenue. In this case it has already fired, twice,
on both of your tracks.

---

## 3. Competitive landscape — you are mid-pack in the free tier

All figures from the GitHub API, 2026-08-04.

### Notification tools (echook's primary category)

| Repo | Stars | Created | Last push | Licence | Note |
|---|---:|---|---|---|---|
| `farouqaldori/vibe-notch` | **2,479** | 2025-12-09 | 2026-04-20 | Apache-2.0 | macOS notch session manager — *"notifications without the context switch"* |
| `JessyTsui/Claude-Code-Remote` | **1,275** | 2025-07-12 | 2025-12-06 | MIT | **Abandoned** — and still 16× echook |
| `tuchg/Lucarne` | **324** | 2026-05-17 | 2026-08-02 | MIT | Fastest-growing; Telegram/WeChat/Feishu bridge, positions explicitly as *"No hooks, no skills, no MCP"* |
| `wyattjoh/claude-code-notification` | 94 | — | 2026-08-03 | — | macOS toast |
| **`ChanMeng666/echook`** | **78** | 2025-11-01 | 2026-07-19 | MIT | — |
| `dongzhenye/claude-code-notifications` | 24 | — | 2026-06-27 | — | — |
| `polyphilz/ccnotifs` | 20 | — | 2026-08-03 | — | — |
| ~20 more | 1–17 each | — | — | — | Long tail incl. 14+ Telegram notifiers at 0–22 stars |

echook is **4th–5th** in its own category, behind an abandoned project.

### Status-line / context / usage tools (echook's second track)

| Repo | Stars | Created | Last push |
|---|---:|---|---|
| `jarrodwatts/claude-hud` | **27,066** | 2026-01-02 | 2026-08-01 |
| `slopus/happy` | **23,083** | 2025-07-18 | 2026-08-03 |
| `ccusage/ccusage` | **17,700** | 2025-05-29 | 2026-08-04 |
| `sirmalloc/ccstatusline` | **12,203** | 2025-08-08 | 2026-08-03 |
| `Maciek-roboblog/Claude-Code-Usage-Monitor` | **8,582** | 2025-06-19 | 2026-07-05 |
| **`ChanMeng666/echook`** | **78** | 2025-11-01 | 2026-07-19 |

`claude-hud` reached 27,066 stars in **seven months** doing "context usage, active tools, running
agents, and todo progress" — note it is also converging on multi-agent tracking. echook is at
0.29% of it. `ccusage` has become infrastructure other tools build on: at least a dozen menu-bar
apps, tmux plugins and Waybar modules wrap it.

**All of these are free. All are actively maintained. None charges money.**

---

## 4. Has anyone monetized this niche? Barely, and painfully.

| Product | Model | Price | Outcome |
|---|---|---|---|
| **Omnara** (YC S25) | Mobile push + dashboard for agent sessions | 10 sessions free → **$9/mo (Aug 2025) → $20/mo (Feb 2026)** | Closest direct comparable. Strong HN traction (310 pts). Immediately met price objections in its own Launch HN |
| **Conductor** | Multi-agent workspace | Free / **Pro $50/mo** / **Teams $60/user/mo** | macOS-only, VC-backed |
| **Happy Coder** (`slopus/happy`) | Same job as Omnara | **$0, MIT, E2EE** | 23,083 stars — and cited by users as the reason not to pay Omnara |
| **Vibe Kanban** | Multi-agent management | attempted | **27,652 stars — and shut down: "didn't see a path to profitability"** |
| **LimitBar** | macOS menu-bar quota app | Gumroad, price not retrieved | Show HN: **2 points** |

The pattern is unambiguous: the two products with real money behind them are VC-funded, ship a cloud
service and a mobile app, and *still* must give away a free tier because free MIT competitors exist.
The most-starred project in the adjacent category (27.6k stars) **died on monetization.**

**Selling to teams instead?** The category exists at real prices — LinearB **$29–59/contributor/mo**
(30–50 seat minimums, annual only), Jellyfish ~**$35–50/engineer/mo**, DX (1-year minimum, contact
sales) — and it is exactly where a solo maintainer cannot compete. Worse, Anthropic ships **free**
first-party [Claude Code analytics](https://code.claude.com/docs/en/analytics) to Team/Enterprise:
DAU/sessions, lines accepted, PR attribution via a GitHub app, a top-contributor leaderboard, CSV
export, OpenTelemetry per-user token/cost export, and an Analytics API. A manager asking "what are my
agents doing and what do they cost" already has a free, first-party, more authoritative answer.

---

## 5. Willingness to pay — the evidence is one-sided

**Against (all specifically about monitoring/notification tooling):**

- *"$20/month for something an engineer can hack in a couple hours"* — lalo2302, Omnara Launch HN,
  2026-02-12
- *"20$ a month seems overly expensive… If it was 5$ I would've considered it."* — quotz, same thread
- *"10 sessions is too few and adding $20/mo doesn't make sense… you're just driving people to
  happy"* — fluidcruft, 2026-02-13
- *"It would have surely taken less time to just set up notifications for Claude Code"* — dbbk,
  2026-03-20

**For — and note carefully what they are paying for:**

- *"I would pay for these tools as much as I would pay for full-time human programmer(s)."*
- *"I would pay as much for this tool per year as I pay for Intellij."*
- *"I would pay $50/mo or something to be able to have reasonable use of Claude Code"*

**Every "I would pay" quote in the corpus is about the coding agent itself, not about monitoring it.**
I found zero developers saying they would pay for notifications, and several saying explicitly they
would not.

---

## 6. What the demand research *did* find, which is worth keeping

The pain is real, even if its clearing price is $0 — and two findings are genuinely actionable:

1. **Context-window anxiety is a far bigger pain than notification.** Measured by revealed preference,
   it is 20–350× the market. Representative: *"The larger the context gets, the dumber the
   responses"*; *"after coming up to the end of the context window, I compact… it loses the nuanced
   understanding."* This is the pain echook's status line addresses — and it is also the most
   contested and most thoroughly commoditized space in the ecosystem.

2. **Per-agent audio identity is an independently requested, genuinely unmet need.** Three separate
   sources converge on it: FlorisFok (2026-03-29) wanting notifications *"when one of them is done
   with stereo and pitch that identifies"*; Voxlert giving each Claude Code session a distinct
   character voice; `cmux-skills` signalling green/yellow/red per workspace tab with sound and voice.
   Anthropic's `terminalSequence` cannot do this — it is one bell for one session. **This is echook's
   single strongest remaining position**, and it lands in the multi-agent segment, which is the only
   place in this space where paid products exist at all.

---

## 7. Research limitations (stated honestly)

- **Reddit 2026 is inaccessible** — reddit.com and old.reddit.com are host-blocked from this
  environment, and the PullPush archive stops mid-2025. Reddit-sourced evidence is 2024–2025 only.
  The most recent 12 months of the loudest community is therefore **not** covered; HN and GitHub star
  counts are the quantitative backbone instead.
- **One of four research workstreams (competitor landscape) was terminated by a session limit**
  before completing. I re-ran its critical queries myself via the GitHub API and Anthropic's docs;
  the star counts and native-feature findings in §2 and §3 are my own first-hand verification, not
  the terminated agent's.
- **Analyst market-size reports are unusable** and I have deliberately not cited them: bottom-up
  vendor run-rates (Claude Code >$2.5B + Cursor ~$4B + Copilot + Codex) already exceed the median
  top-down 2026 "market" of ~$8B. The reports lag 12–18 months.
- **Numbers I deliberately excluded as unreliable:** any Claude Code WAU figure (no primary source
  exists), Claude Code "$8B run-rate" (a Sacra extrapolation, widely restated as fact), Cursor "360K
  paying subscribers" (unsourced and arithmetically inconsistent with its ARR), and the "Anthropic
  15% revenue share on paid skills" claim (unsupported by 150KB of official docs).
- **echook's real user count is unknown** — there is no telemetry. All user estimates are inferred
  from GitHub traffic and should be treated as order-of-magnitude only.
</content>
