# echook — Evidence Appendix & Method

**Date:** 2026-08-04 · Supporting `00-VERDICT.md`, `01`, `02`, `03`

---

## Method

Four parallel research workstreams (market sizing, competitive landscape, monetization outcomes,
demand signals), plus first-hand verification by me of the two load-bearing claims — competitive star
counts and what Anthropic ships natively — because those are the two findings the entire verdict
rests on and I did not want them second-hand.

**Confidence tiers used throughout:**

- **[PRIMARY]** — vendor disclosure, official docs I fetched and grepped myself, or an API I queried
- **[SURVEY]** — named survey with a stated n and field dates
- **[ESTIMATE]** — third-party analyst extrapolation, labelled as such by its own author
- **[WEAK]** — single source, SEO-grade, or uncorroborated; used only where flagged

---

## A. echook's own numbers — [PRIMARY], GitHub API, 2026-08-04

```
Repository        ChanMeng666/echook (renamed from claude-code-audio-hooks in v5.2.1)
Created           2025-11-01        Last push   2026-07-19        Age  ~9 months
Stars             78                Forks       7                 Watchers  1
Issues (total)    1                 Pull requests (ever)  0
Commits           152               Contributors  1 (solo)
Latest release    v6.4.0 (2026-07-19)
Licence           MIT               Funding  GitHub Sponsors + Buy Me a Coffee
Repo size         ~277 files; audio/ 2.3M, plugins/ 2.8M, docs/ 460K, tests/ 852K
```

**Traffic, 14-day window ending 2026-08-04:**
```
Views      174 total / 85 unique     (~6 unique visitors per day)
Clones     137 total / 78 unique     (inflated by CI, mirrors, and plugin-install git clones)
```

**Star accrual, most recent 20 stars:** 2026-05-10 → 2026-08-03, i.e. **20 stars in ~86 days
(0.23/day)** — statistically identical to the lifetime average of 0.28/day. There was never an
inflection point. The project has not had a moment.

**Interpretation of the zero-PR, one-issue figure.** Two readings are possible and both are bad for a
business case: either almost nobody uses it, or people use it and it works so uneventfully that they
never engage. Either way there is no community, no word-of-mouth engine, and no user relationship to
convert.

---

## B. Platform-native substitution — [PRIMARY], fetched and grepped 2026-08-04

### B1. Notifications — [code.claude.com/docs/en/hooks](https://code.claude.com/docs/en/hooks)

`Notification` event matchers: `permission_prompt`, `idle_prompt`, `auth_success`,
`elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`,
**`agent_completed`**.

`terminalSequence` field (Claude Code **v2.1.141+**) — allowlisted OSC 0/1/2 (titles), OSC 9 (iTerm2,
ConEmu, Windows Terminal, WezTerm — incl. `9;4` taskbar progress), OSC 99 (Kitty), OSC 777 (urxvt,
Ghostty, Warp), and BEL. Explicitly solves the hooks-have-no-controlling-terminal problem, is
race-free inside tmux and screen, and works on Windows where `/dev/tty` does not exist.

The docs ship a working desktop-notification hook (~8 lines of bash) and a one-line bell.

### B2. Status line — [code.claude.com/docs/en/statusline](https://code.claude.com/docs/en/statusline)

Fields confirmed present in the stdin JSON by grepping the fetched 62.6KB document:

```
context_window.{used_percentage, remaining_percentage, context_window_size, current_usage}
exceeds_200k_tokens
cost.{total_cost_usd, total_duration_ms}    total_lines_added
model      session_name      effort      fast_mode
agent.name        pr.{number, url, review_state}
worktree.{name, path, branch, original_cwd}       vim.mode
rate_limits.five_hour.{used_percentage, resets_at}
rate_limits.seven_day.{used_percentage, resets_at}
```

Verbatim from the document (lines 267–276):
```json
"rate_limits": {
  "five_hour":  { "used_percentage": 23.5, "resets_at": 1738425600 },
  "seven_day":  { "used_percentage": 41.2, "resets_at": 1738857600 }
}
```

**This is the finding that changed the verdict.** My demand research concluded quota visibility was
the one pain Anthropic had not closed and that `ccusage` owned it. Verifying against the primary doc
showed that conclusion is out of date — it is first-party now. If you read only one thing in this
appendix, read the block above and compare it to echook's 29-segment catalog.

Also confirmed: **`/statusline` accepts natural-language instructions and Claude Code generates the
script** (docs' own example: *"/statusline show model name and context percentage with a progress
bar"*). The docs additionally ship a colour-coded context progress bar example — the same traffic-light
pattern echook documents.

### B3. Team analytics — [code.claude.com/docs/en/analytics](https://code.claude.com/docs/en/analytics)

Free to Team/Enterprise/API customers: DAU and sessions, lines accepted, suggestion accept rate, PR
and LoC attribution via a GitHub app, top-contributor leaderboard, CSV export of all users,
OpenTelemetry export of per-user token counts and cost, per-user spend reports, and a `read:analytics`
Analytics API on Enterprise.

### B4. No commerce rail — [PRIMARY]

Full [plugin-marketplace docs](https://code.claude.com/docs/en/plugin-marketplaces) (76,170 bytes) and
[skills docs](https://code.claude.com/docs/en/skills) (73,907 bytes) grepped: **199 occurrences of
"marketplace", 3 of "license", and ZERO of** `pay*`, `monetiz*`, `billing`, `revenue`, `price`,
`purchase`, `commerce`. A marketplace is a `marketplace.json` in a git repo added via
`/plugin marketplace add`. No central store, no accounts, no billing, no install telemetry, no revenue
share.

---

## C. Competitive star counts — [PRIMARY], GitHub API, 2026-08-04

### Notification category

| Repo | Stars | Created | Pushed | Licence |
|---|---:|---|---|---|
| farouqaldori/vibe-notch | 2,479 | 2025-12-09 | 2026-04-20 | Apache-2.0 |
| JessyTsui/Claude-Code-Remote | 1,275 | 2025-07-12 | 2025-12-06 | MIT (abandoned) |
| tuchg/Lucarne | 324 | 2026-05-17 | 2026-08-02 | MIT |
| wyattjoh/claude-code-notification | 94 | — | 2026-08-03 | — |
| **ChanMeng666/echook** | **78** | 2025-11-01 | 2026-07-19 | MIT |
| dongzhenye/claude-code-notifications | 24 | — | 2026-06-27 | — |
| polyphilz/ccnotifs | 20 | — | 2026-08-03 | — |
| eyalzh/claude-code-toast | 17 | — | 2026-03-28 | — |
| rvcas/claude-zellij-whip | 13 | — | 2026-05-28 | — |
| ~15 more at 1–6 stars | | | | |

Plus a documented long tail of 14+ Telegram-notifier repos at 0–22 stars each.

### Status line / context / usage category

| Repo | Stars | Created | Pushed | Licence |
|---|---:|---|---|---|
| jarrodwatts/claude-hud | **27,066** | 2026-01-02 | 2026-08-01 | MIT |
| slopus/happy | **23,083** | 2025-07-18 | 2026-08-03 | MIT |
| ccusage/ccusage | **17,700** | 2025-05-29 | 2026-08-04 | NOASSERTION |
| sirmalloc/ccstatusline | **12,203** | 2025-08-08 | 2026-08-03 | MIT |
| Maciek-roboblog/Claude-Code-Usage-Monitor | **8,582** | 2025-06-19 | 2026-07-05 | MIT |
| **ChanMeng666/echook** | **78** | 2025-11-01 | 2026-07-19 | MIT |

For scale: `BloopAI/vibe-kanban` — **27,652 stars, Apache-2.0, last push 2026-04-24** — is the
multi-agent management tool that **shut down for lack of a path to profitability**.

---

## D. Demand evidence — HN, 2025-08 → 2026-07

### D1. Notification pain is real but has a $0 clearing price

Roughly one comment every 2–3 weeks across the year. Representative:

- **jackcarter**, 2026-01-20 — *"Why don't Claude Code & other AI agents offer an option to make a
  sound or trigger a system notification whenever they prompt for approval?"*
- **patrick4urcloud**, 2026-02-12 — *"Sound notifications for Claude Code are a real pain point"*
- **vadepaysa**, 2026-06-16 — *"literally for notifications when claude is done"*
- **sajithdilshan**, 2026-06-05 — *"some notification hooks so I don't have to switch windows"*

Current substitutes, all cheap: OSC 777 into `/dev/tty` (hombre_fatal, 2026-03-21) · Ghostty native
push (manmal, 2025-08-05) · `piper` TTS (behnamoh, 2026-07-07) · per-event audio cues (mikedotcook,
2026-02-13) · Tailscale + ssh from a phone (mccoyb) · a VPS (rubslopes).

**The decisive counter-quote — dbbk, HN 47448524, 2026-03-20:** *"It would have surely taken less time
to just set up notifications for Claude Code."*

**Market indifference, measured:** Show HN *"Notification when coding agent is done, free"*
(ltononro, 2026-05-28) — **3 points, 0 comments.**

### D2. Context anxiety is the bigger pain (and more commoditized)

- **enobrev**, 2026-01-13 — *"The larger the context gets, the dumber the responses."*
- **consumer451**, 2026-04-14 — *"It is a universal truth that LLMs get dumb the more context you give
  them"* (recommends never exceeding 250k even with 1M available)
- **ewoodrich**, 2025-09-21 — *"after coming up to the end of the context window, I compact… it loses
  the nuanced understanding"*
- Reddit r/ClaudeAI (2025): *"Claude Code is a Beast"* — 412 upvotes / 65 comments, advising early
  `/compact` because auto-compact makes Claude *"lose important context and spiral out of control"*

Revealed preference: `claude-hud` at 27,066 stars in seven months.

### D3. Quota anxiety — loud, but now closed by the platform

- HN **44713757**, 2025-07-28, **609 points** — "Claude Code weekly rate limits"
- **aray07**, 2026-03-26 (Show HN `claude-meter`) — *"Usage limits have always been opaque. A vague
  percentage bar. No dollar figure. No formula. **No way to plan your work around it.**"*
- **tom1337**, 2026-01-26 — *"I just purchased a third $200 MAX plan and instantly hit rate limits"*

`ccusage` (17,700 stars) became the accepted answer and is now infrastructure others wrap:
`claude-analyst`, `vibepulse` (53★), `Nihondo/AgentLimits` (51★), `ccusage-menubar` (27★),
`tmux-ccusage` (22★), `waybar-claude-code` (19★), `viberank` (112★), `better-ccusage` (75★),
`splitrail` (216★).

**But see §B2 — `rate_limits` is now first-party.** This gap is closing.

### D4. Multi-agent — the one live gap

- **FlorisFok**, 2026-03-29 — wants notification *"when one of them is done with stereo and pitch that
  identifies"* ← **strongest single quote for echook's differentiated direction**
- **Zedmor** — *"3-5 parallel engineers is the sweet spot. Beyond that, the codebase itself becomes
  the bottleneck"* ← the ceiling on this segment's size
- **yerik**, 2026-04-25 — *"I like to think in parallel Claude instances the same as software
  threads."*
- `cmux-skills` — green/yellow/red per workspace tab with sound and optional voice
- Voxlert — distinct character voice per Claude Code session

### D5. Willingness to pay — one-sided

**Against (monitoring/notification specifically):** *"$20/month for something an engineer can hack in
a couple hours"* (lalo2302, Omnara Launch HN 2026-02-12) · *"20$ a month seems overly expensive… If it
was 5$ I would've considered it"* (quotz, same) · *"you're just driving people to happy"* (fluidcruft,
2026-02-13) · Vibe Kanban's shutdown.

**For (all about the agent itself, none about monitoring it):** *"I would pay for these tools as much
as I would pay for full-time human programmer(s)"* (paulsutter, 2026-05-01) · *"I would pay as much
for this tool per year as I pay for Intellij"* (mrguyorama, 2025-12-24) · *"I would pay $50/mo… to
have reasonable use of Claude Code"* (raylad, 2025-02-25).

**Zero instances found of anyone offering to pay for agent notifications.**

---

## E. Monetization comparables

**GitHub Sponsors — [PRIMARY]:** $100M cumulative crossed **July 2026**, across **70,000+**
maintainers/orgs and 280,000+ sponsors since 2019 → lifetime mean **~$1,430/maintainer ≈ $17/month**,
and that is the mean among those who received anything. Orgs supply ~40% of funding at ~15× the
average individual sponsorship. ([github.blog](https://github.blog/open-source/maintainers/100-million-for-open-source-a-milestone-built-by-the-community/))

**Tidelift 2024 maintainer survey — [SURVEY]:** 60% of maintainers unpaid hobbyists; only 12%
"professional"; ~75% receive no funding at all.

**The ceiling case — core-js:** 9 **billion** downloads, 250M/month, used by 75–80% of the top 100
websites → peaked ~$2,500/month in donations, fell to ~$400/month; sole maintainer stated publicly he
could not support his family.

**The outliers all had something echook doesn't:** Sindre Sorhus >$10k/mo (~1,000 npm packages) ·
Evan You $16k+/mo (a top-5 JS framework) · Caleb Porzio $112,680/yr (**paywalled screencasts**, i.e.
he sold content, not the library) · Babel $1.85M lifetime (the JS transpiler everyone builds through).

**Conversion benchmarks:** freemium generally 2–5% median (1–10% range) · **developer tools
specifically 1–3%** · open-source→paid conventionally targeted at **1%**, which InfluxData's CEO
frames as a good outcome · free trial without credit card ~6%.

**The one solo success pattern — Sidekiq:** ~$80,000/month, ~800 customers at $1,000–2,000/yr, zero
employees, **90% inbound**. Perham: *"those users of my open source version will naturally convert as
they find that they need those paid features."* The paid tier bought **production durability for
background jobs** — an operational risk surface. A status line has none.

**Team observability pricing:** LinearB $29/contributor/mo (30-seat min) and $59 (50-seat min), annual
only, AI Impact in both tiers · Jellyfish ~$35–50/engineer/mo, explicitly tracks Claude Code · DX
1-year minimum, contact sales · Faros AI contact sales.

**The category postmortem — Kite:** AI code-completion assistant, heavily VC-funded, ~500k monthly
active developers, shut down 2022. Founder: *"our product did not monetize, and it took too long to
figure that out."*

**Sherlocking, quantified:** Apple shipping features natively is estimated to affect ~$393M/year of
third-party app revenue (AllTrails alone ~$307M).

**Career-signal evidence — [PRIMARY, academic]:** Abou El-Komboz & Goldbeck, *"Career Concerns as a
Public Good: The Role of Signaling for Open Source Software"* (ifo Institute; *Labour Economics*), n
≈ 22,900 developers: OSS activity elevated **~16%** during job-search periods, concentrated in
high-visibility repos. **Caveat: measures developer behaviour, not employer response** — it shows OSS
is a rational career investment, not a proven wage premium. The widely-quoted "71% of hiring managers
check GitHub" figure traces only to content-marketing sites with no methodology and should **not** be
repeated.

---

## F. Market context — [PRIMARY] disclosures only

- Claude Code **$1B run-rate, Nov 2025** (Anthropic, 2025-12-03)
- Claude Code **>$2.5B run-rate, Feb 2026**; WAU doubled since Jan 1; business subs **quadrupled**;
  **enterprise >50% of Claude Code revenue**; 4% of all public GitHub commits (Anthropic Series G,
  2026-02-12)
- Cursor $1B annualized Nov 2025; **SpaceX acquiring Anysphere for $60B**, close expected Q3 2026
  (CNBC, 2026-06-16)
- Codex CLI ~600K weekly users early 2026 → **5M+ WAU by Jun 2026** (secondary, medium confidence)
- **[SURVEY]** State of AI Dev 2026 (n=7,258, fielded Apr 8 – May 8 2026): 60.3% of developers pay
  something monthly for AI; 37.8% pay ≥$20/mo; 11.5% pay ≥$100/mo. Claude paid for by 68.8%. **Cursor:
  129 paying respondents** out of 6,675 — developers pay model vendors, not tool vendors.
- **[ESTIMATE, Sacra]** Cursor ~60% enterprise revenue; **individual developer accounts are
  gross-margin negative.**

**Ecosystem scale:** ~23,500 skills, ~12,700 MCP servers, ~2,600 marketplaces (community directory,
self-reported 2026-08-04); official Anthropic directory ~150–256 plugins, all free.

---

## G. Numbers deliberately excluded as unreliable

- **Any Claude Code WAU figure.** Claims range 1.6M–4.2M; none traces to Anthropic. Anthropic has
  only ever disclosed *ratios* ("doubled since Jan 1").
- **Claude Code "$8B run-rate."** A Sacra extrapolation, restated as fact by dozens of SEO sites.
- **Cursor "360,000 paying subscribers, 36% free-to-paid."** Unsourced and arithmetically
  irreconcilable with its ARR.
- **"Anthropic pays a 15% revenue share on paid skills."** Traced to one blog post (500k.io, 2026-05-01)
  citing no primary source, contradicted by 150KB of official docs containing zero monetization
  vocabulary, by the all-free official directory, and by the absence of any newsroom announcement.
  **Treat as false.**
- **Analyst market-size reports** (Grand View $10.3B, Mordor $16.13B, etc.). Bottom-up vendor
  run-rates already exceed the median top-down "market"; the reports lag 12–18 months. Only the
  22–37% CAGR band is worth anything.

---

## H. Limitations of this research

1. **Reddit 2026 is inaccessible from this environment** — reddit.com and old.reddit.com are
   host-blocked, r.jina.ai returns Reddit's 403 wall, and the PullPush archive stops mid-2025.
   Reddit evidence here is 2024–2025 only. **The most recent 12 months of the loudest community is
   not covered.** HN and GitHub are the quantitative backbone instead. This is the most significant
   gap; if any single finding would overturn the verdict, it would come from r/ClaudeCode or
   r/cursor in 2026.
2. **WebSearch budget was exhausted** during the run; most retrieval was via WebFetch against search
   HTML endpoints and direct pages, and one of four workstreams (competitive landscape) was
   terminated early by a session limit. **I re-ran its critical queries myself** via the GitHub API
   and Anthropic's docs — the star counts in §C and the native-feature findings in §B are my own
   first-hand verification, not that agent's partial output.
3. **No primary user research.** Nobody interviewed an echook user, because there is no user list and
   no telemetry. All user-count figures are inferred from GitHub traffic and are order-of-magnitude
   at best.
4. **X/Twitter, dev.to, YouTube not covered** (blocked or out of budget).
5. **Small-utility-tool economics (price points, conversion for menu-bar-class apps) is
   under-researched** — the workstream flagged it as its weakest section. It affects the precision of
   the revenue ceiling in `02`, not its order of magnitude.
6. **The accessibility segment in `02` §D is a hypothesis, not an evidenced finding.** It is inferred
   from the product's shape; it deserves one conversation with an actual blind developer before being
   relied on.

**What would change my verdict:** the fake-door test in `00-VERDICT.md` clearing 30 clicks; or
evidence from 2026 Reddit that the multi-agent cross-editor segment is 10× larger than HN suggests; or
Anthropic reversing course and removing `rate_limits` / `terminalSequence` from the platform. I judge
all three unlikely, and the first is cheap enough that you should run it anyway before taking my word
for any of this.
</content>
