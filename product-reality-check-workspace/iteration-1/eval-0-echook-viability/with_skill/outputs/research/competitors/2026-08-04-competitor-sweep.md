# echook — Competitor Sweep (four rings)

**Date:** 2026-08-04 · **Subject:** `github.com/ChanMeng666/echook` (MIT, Python, solo, 78★/7 forks per `gh api` today — the brief said 79; use 78), created 2025-11-01, last push **2026-07-19**.

**Source grades used throughout:** `[PAGE]` = URL opened this session, number read, quotable · `[SNIPPET]` = search result not opened, **not quotable** · `[UNVERIFIED]` = aggregator only, **treat as false**. GitHub numbers are `gh api repos/OWNER/NAME` / `gh api search/repositories` executed 2026-08-04 and are graded `[PAGE]`.

---

## Executive summary — most decision-relevant first

**1. The headline differentiator is table stakes, and a 4,973★ competitor already ships it better.**
`PeonPing/peon-ping` (4,973★, 367 forks, MIT, pushed 2026-07-24) ships **five Agent Skills** — `peon-ping-config`, `-log`, `-rename`, `-toggle`, `-use` — plus a `CLAUDE.md`, a `GEMINI.md`, an MCP server, and a Homebrew formula. Its `peon-ping-config/SKILL.md` frontmatter reads, verbatim `[PAGE]` (`gh api repos/PeonPing/peon-ping/contents/skills/peon-ping-config/SKILL.md`):

> `description: Update peon-ping configuration — volume, pack rotation, categories, active pack, and other settings. Use when user wants to change peon-ping settings like volume, enable round-robin, add packs to rotation, toggle sound categories, or adjust any config.`

That is echook's entire "natural language forever" mechanism, in echook's exact product category, at **63× the stars**. echook's differentiator is not unclaimed; it is the second implementation of it in this niche, and the smaller one.

**2. Anthropic ships the substitute in its own documentation, and has formally closed the feature request as done.**
`code.claude.com/docs/en/terminal-config` `[PAGE]` contains a copy-pasteable `afplay` Notification hook and a **three-line** `{"preferredNotifChannel": "terminal_bell"}` setting, under a page whose own symptom index carries the line *"No sound or alert when Claude finishes"*. Issue `anthropics/claude-code#1288` "Feature: Sound notifications" (44 reactions) was closed **`completed`** on 2025-08-22 with, verbatim `[PAGE]`: *"You can either use `preferredNotifChannel` … or hooks … to set up sound notifications."* The free substitute is not a gist. It is the vendor's documentation, and the vendor has adjudicated the category as shipped.

**3. Both of echook's tracks are absorbed, and the statusline track is absorbed hardest.**
Claude Code now hands any statusline script `context_window.used_percentage` (shipped 2.1.6, 2026-01-13) and `rate_limits.*.used_percentage`/`resets_at` (2.1.80, 2026-03-19) `[PAGE]` CHANGELOG × npm publish dates. echook's context/quota bars are **formatting, not measurement**. And `/statusline` accepts natural-language instructions and writes the script for you `[PAGE]` `code.claude.com/docs/en/statusline`.

**4. Cursor absorbed the cross-editor value prop with a checkbox.**
`cursor.com/docs/reference/third-party-hooks.md` `[PAGE]`, verbatim: *"Cursor can load and execute hooks configured for Claude Code, allowing you to use the same hook scripts across both tools."* A user who installed echook for Claude Code already has audio in Cursor. echook's Cursor adapter competes with a compatibility layer that costs the user zero.

**5. There is no revenue in this ring at all.** Every one of the ~30 direct competitors found is $0. The two biggest (`claude-hud` 27,066★, `ccstatusline` 12,205★/72,918 npm downloads per week) are MIT and free. Ring 2 (paid observability) is a **different buyer** — org admins, per-seat/per-GB, $29–$2,499/mo — with no graduation path from a solo dev who wants a chime.

**6. The one honest survivor:** echook's **39 hook events across three harnesses** is finer-grained per-event coverage than any competitor found. peon-ping covers 21 harnesses but collapses everything into **7 sound categories** (`session.start`, `task.acknowledge`, `task.complete`, `task.error`, `input.required`, `resource.limit`, `user.spam`) `[PAGE]`. Depth-per-harness is real and checkable. Breadth-of-harness is lost 21-to-3.

---

## Ring 1 — Direct competitors

### 1a. Notification / sound tools (the same job as echook)

Sorted by stars. All figures `gh api` 2026-08-04 `[PAGE]`.

| Project | ★ | Forks | Last push | License | Price | What it is | `positioning_vs_you` (buyer's view) |
|---|---:|---:|---|---|---|---|---|
| **PeonPing/peon-ping** | **4,973** | 367 | 2026-07-24 | MIT | $0 | Game-character voice lines + overlay banners; **21 harness adapters**; 5 Agent Skills; MCP server; Homebrew; `peonping.com` | Theirs is funny and your colleagues have heard of it. Ours is a config surface. They also install with `brew install` and configure by talking to the agent — the same way ours does. |
| **manaflow-ai/cmux** | 25,549 | 2,141 | 2026-08-04 | NOASSERTION | $0 | Ghostty-based macOS terminal **with agent notifications built in** | Theirs replaces your terminal and the notification comes free. Ours is a thing you install into a terminal you already have. |
| **farouqaldori/vibe-notch** | 2,479 | 351 | **2026-04-20** | Apache-2.0 | $0 | macOS notch session manager — "notifications without the context switch" | Theirs is visual and always-on-screen; ours is audible. Theirs has been quiet 3.5 months. |
| **JessyTsui/Claude-Code-Remote** | 1,275 | 135 | **2025-12-06** | MIT | $0 | Control CC remotely via email/Discord/Telegram | Theirs lets you *reply* from your phone; ours only tells you. Dead 8 months. |
| **hoangsonww/Claude-Code-Agent-Monitor** | 867 | 193 | 2026-08-03 | MIT | $0 | Real-time SQLite/React dashboard for CC + Codex incl. status notifications | Theirs gives you a screen to look at; ours gives you a sound so you don't have to. |
| **777genius/claude-notifications-go** | 773 | 104 | 2026-07-16 | NOASSERTION | $0 | Go plugin, 6 notification types, click-to-focus, **"1 line installation"** | Theirs is a single Go binary with click-to-focus (ours can't focus your window). "1 line installation" is the same promise as our slash command. |
| **tuchg/Lucarne** | 324 | 15 | 2026-08-02 | MIT | $0 | Notify + **approve** + resume for Codex/Pi/Grok/Claude | Theirs lets you approve the permission prompt from the notification. Ours makes a noise and you walk back. |
| **mylee04/code-notify** | 280 | 23 | **2026-08-04** | MIT | $0 | Cross-platform desktop notifications, CC + Codex + Gemini CLI, Homebrew/npm/script | Same cross-harness pitch, `brew install`, shipping today. npm 41 downloads/wk `[PAGE]`. |
| **warpdotdev/claude-code-warp** | 224 | 49 | 2026-07-16 | MIT | $0 | **Official Warp terminal** integration — native notifications | This is a terminal *vendor* shipping it. If your terminal does it, you never look for us. |
| **dazuiba/CCNotify** | 216 | 23 | **2025-10-14** | MIT | $0 | Desktop notifications | Dead ~10 months. |
| **sondera-ai/sondera-coding-agent-hooks** | 219 | 31 | **2026-06-05** | MIT | $0 | Hook implementations across Claude/Cursor/Gemini | Same multi-harness hook framing, quiet 2 months. |
| **shirenchuang/agentbro** | 201 | 28 | 2026-08-04 | Apache-2.0 | $0 | macOS Dynamic Island for CC/Codex/Gemini/Cursor + hooks + skills | Theirs is ambient-visual on the notch; ours is audible. |
| **eddmann/ClaudeMeter** | 130 | 20 | 2026-05-19 | MIT | $0 | macOS menu-bar 5h/7d/session quota tracker | Theirs is the rate-limit half of ours, as a menu-bar app you never configure. |
| **ctoth/claudio** | 110 | 8 | 2026-07-15 | none | $0 | **"Hook-based audio feedback for Claude Code and OpenAI Codex CLI"** (Go, soundpacks) | The closest architectural twin. Ours adds Cursor and a statusline; theirs has soundpacks and no license file. |
| **trentmcnitt/cc-notifier** | 108 | 9 | 2026-07-06 | none | $0 | macOS + push notifications | — |
| **dongxutang918-afk/agentwatch** | 104 | 14 | 2026-06-23 | MIT | $0 | **Apple Watch** notifications | Theirs buzzes your wrist in another room. Ours needs you within earshot. |
| **kaida-palooza/ccpoke** | 102 | 42 | **2026-03-18** | MIT | $0 | Phone bridge — notifications, 2-way chat, permissions | — |
| **wyattjoh/claude-code-notification** | 94 | 8 | 2026-07-25 | MIT | $0 | Lightweight macOS notification hook | — |
| **kdush/Claude-Code-Notifier** | 94 | 8 | **2026-02-01** | Apache-2.0 | $0 | Multi-channel notifications | Dead 6 months. |
| **soulee-dev/claude-code-notify-powershell** | 92 | 6 | **2026-01-11** | MIT | $0 | PowerShell toasts, zero deps | Dead 7 months. |
| **dzzzgnr/taphaptic** | 88 | 5 | 2026-07-26 | MIT | $0 | Apple Watch haptics | — |
| **citedy/game-sounds** | 86 | 15 | **2026-04-14** | MIT | $0 | Warcraft peon lines for CC | A peon-ping clone that stopped. |
| **ChanMeng666/echook** | **78** | **7** | **2026-07-19** | MIT | $0 | 39 hook events × 3 editors, 2 themes, TTS, webhooks, statusline, NL config | — |
| **thephw/claude-meseeks** | 78 | 2 | 2026-07-14 | NOASSERTION | $0 | Mr. Meeseeks voice line when CC waits | Tied with us on stars; built in one week (created 2026-07-08). |
| **maddada/agent-manager-x** | 72 | 2 | **2026-05-05** | none | $0 | macOS monitor with **voice or beep** for CC/Codex/OpenCode | — |
| **Aurealibe/claude-config** | 68 | 10 | 2026-07-10 | MIT | $0 | CC framework: agents + commands + **audio notifications** | Audio bundled into a bigger config framework — the "already in my setup" competitor. |
| **educlopez/codevator** | 63 | 1 | **2026-05-31** | MIT | $0 | Background sounds *while* CC works, stop when it needs you | Inverted design — silence is the alert. Genuinely different idea. |
| **simonbs/brrr-cli** | 55 | 0 | 2026-08-03 | none | $0 | Notifications for agent CLIs via `brrr.now` | — |
| **Gentleman-Programming/gentle-agent-state** | 49 | 5 | 2026-07-01 | MIT | $0 | Colored dot per agent in the **tmux tab bar** | Zero-attention ambient state; no sound, no install into the agent. |
| **6m1w/claude-sound-fx** | 43 | 3 | **2026-03-14** | none | $0 | 12 themes (JARVIS, GLaDOS, Pikachu) for CC/OpenCode | **12 themes vs our 2.** |
| **htjun/claude-code-hooks-scv-sounds** | 41 | 3 | **2025-08-15** | none | $0 | StarCraft SCV sounds | Dead 12 months — the earliest twin found. |
| **rubenflamshepherd/claude-code-notif-manager** | 39 | 4 | **2026-02-13** | none | $0 | SC/WC/AoE unit sounds + audio & notification management | Dead 6 months. |
| **EryouHao/claude-code-sound-notification** | 30 | 0 | **2026-03-18** | MIT | $0 | Sound notification setup | — |
| **samhayek-code/claude-audio-hooks** | 26 | 3 | 2026-06-20 | none | $0 | Game SFX on session start / complete / permission | Near-identical name to echook's former name. |
| **kaihochak/tallr** | 25 | 0 | **2026-06-18** | MIT | $0 | Monitor CC/Gemini/Codex sessions, state detection, native notifications | — |
| **DevinoSolutions/anotifier-for-claude-codex-cursor** | 18 | 0 | 2026-08-04 | AGPL-3.0 | $0 | Desktop + phone notifications for **CC, Codex, Gemini, Cursor** + native VS Code | Exactly our harness set plus Gemini, shipping today, 18★. |
| **sokojh/ai-notifier-swift** | 13 | 2 | **2026-01-21** | MIT | $0 | Native macOS app for CC/Gemini/Codex | Dead 6 months. |
| **settinghead/voxlert** | 12 | 3 | 2026-07-28 | MIT | $0 | **LLM-generated voice notifications** for CC, Cursor, Codex, pi, OpenClaw | Our TTS + our harness set, generated per-event. 12★. |
| **DefaultPerson/agent-setup** | 11 | 1 | **2026-07-06** | MIT | $0 | Universal CC + Codex setup: security guard, **TTS notifications, status line**, slash commands | The closest thing to our exact bundle (TTS + statusline + multi-harness), at 11★. |

**Field size, `gh api search/repositories` `[PAGE]`:** `claude code notification` → **1,500** repos · `claude code sound notification` → **183** · `claude code hooks` → **7,088** · `codex notification` → **409**.

**14 of the 39 rows above have more stars than echook.** Nine of them do the multi-harness thing echook claims.

### 1b. Statusline / context-usage projects (echook's second track)

| Project | ★ | Last push | License | Notes |
|---|---:|---|---|---|
| **jarrodwatts/claude-hud** | **27,066** (1,257 forks) | 2026-08-01 | MIT | *"context usage, active tools, running agents, todo progress"* — echook's statusline half at **347×** the stars |
| **sirmalloc/ccstatusline** | **12,205** (534 forks) | 2026-08-03 | MIT | **72,918 npm downloads last week** `[PAGE]` npm downloads API. Powerline, themes. Ships `AGENTS.md`. |
| Haleclipse/CCometixLine | 3,440 | **2026-03-14** | none | Rust; stalled 5 months |
| GaoSSR/best-claude-hud | 2,347 | 2026-07-30 | Apache-2.0 | Rust HUD |
| nilbuild/claude-statusline | 1,360 | **2026-04-03** | MIT | |
| Owloops/claude-powerline | 1,144 | 2026-08-02 | MIT | |
| chongdashu/cc-statusline | 624 | **2026-02-16** | MIT | |
| **Nanako0129/coralline** | 530 | 2026-08-03 | MIT | *"paste one prompt and your AI interviews you, then installs"* — **agent-operated install, in the statusline niche** |
| rz1989s/claude-code-statusline | 473 | 2026-08-01 | MIT | |
| stormzhang/token-tracker | 463 | 2026-08-03 | MIT | CC + Codex token tracking |
| stephenleo/cship | 412 | 2026-07-27 | Apache-2.0 | Starship-style TOML |
| **leeguooooo/claude-code-usage-bar** | 342 | 2026-08-02 | MIT | *"5h/7d rate-limit usage, reset countdowns, model + context window"* — echook's exact statusline feature list |
| NYCU-Chung/cc-statusline | 261 | **2026-05-22** | MIT | quota bars, agent tracker, MCP health |
| tmck-code/yet-another-statusline | 237 | 2026-08-03 | BSD-3 | |
| Wangnov/claude-code-statusline-pro | 235 | 2026-07-27 | MIT | |
| Astro-Han/claude-pace | 217 | 2026-07-28 | MIT | rate-limit + pace-aware quota |
| **kairyou/agent-tools** | 159 | 2026-08-04 | MIT | *"Reusable Agent Skills, plus integrations (statusline, provider usage) that install into Codex, Claude…"* — **skills + statusline + multi-harness**, echook's architecture exactly |
| gwittebolle/claude-carbon | 155 | 2026-08-03 | MIT | |

**`gh api search/repositories?q=claude+code+statusline` → 2,161 repos `[PAGE]`.** **Eighteen** statusline projects have more stars than echook has in total. The context-usage status line is not a differentiator; it is the single most crowded artifact in the Claude Code ecosystem.

---

## Ring 2 — Adjacent up/down-market

| Platform | Tiers (verbatim) | Alerting? | Source |
|---|---|---|---|
| **Langfuse** | Hobby free (50k units/mo, **2 monitors**) · Core **$29/mo** · Pro **$199/mo** · Enterprise **$2,499/mo** | Yes — "Monitors and alerts", spend-threshold email | `[PAGE]` langfuse.com/pricing |
| **Helicone** | Hobby free (10k requests) · Pro **$79/mo** · Team **$799/mo** · Enterprise | "Alerts & reports" Pro+ | `[PAGE]` helicone.ai/pricing |
| **LangSmith** | Developer **$0/seat** (5k traces) · Plus **$39/seat/mo** · Enterprise. Usage **$1.50/LCU**, **$1.00/LSU** | Strongest — thresholds → **Slack, PagerDuty, Dynatrace, webhooks** | `[PAGE]` langchain.com/pricing + docs.langchain.com/langsmith/alerts |
| **Braintrust** | Starter **$0** ($4/GB, $2.50/1k scores) · Pro **$249/mo** · Enterprise. "Unlimited users" | None found on pricing page (docs/guides/monitoring 404s — **unprobed, not negative**) | `[PAGE]` braintrust.dev/pricing |
| **Anthropic Claude Code Analytics** | `claude.ai/analytics/claude-code` requires **Teams/Enterprise + Admin/Owner**; Analytics API **Enterprise only** ("not available on the Teams plan") | **No alerting** — retrospective LoC/accept-rate/DAU/spend dashboard | `[PAGE]` code.claude.com/docs/en/analytics |
| **Claude Code OpenTelemetry export** | Free, built-in. 8 metrics, 15+ events, OTLP/Prometheus | Explicitly punts: *"Alerting would be implemented in your backend."* | `[PAGE]` code.claude.com/docs/en/monitoring-usage |

**Down-market (the free thing they use instead):** Langfuse is MIT-Expat with an `ee/` carve-out, self-host free and "unlimited units" (32,449★, pushed 2026-08-03); Helicone Apache-2.0 self-host (6,032★); LangSmith and Braintrust gate self-hosting behind Enterprise. `[PAGE]` all.

**Verdict — Ring 2 is not adjacent. echook has no up-market graduation path.** Three independent reasons: (i) **different buyer** — these price per seat/GB/trace and Anthropic's own dashboard needs an Owner role; echook's buyer is one person who wants a chime and will never file a $2,499/mo PO; (ii) **different job** — observability alerts are aggregate, threshold, fleet-scoped and route to PagerDuty; echook's alert is per-session, immediate, and routes to one human's ears two feet away; (iii) **different unit** — they trace LLM calls, echook watches a terminal session's state transitions.

**The one genuine collision is sideways, not upward.** Langfuse ships a Claude Code integration that installs *"a Python hook script, registered globally"* via `.claude/settings.json` `[PAGE]` langfuse.com/integrations/other/claude-code — the exact hook slot echook occupies, backed by a 32k-star repo. It does not make a sound today. If it ever adds "notify me when this session ends", it becomes a Ring-1 competitor overnight.

**Where the buyer actually graduates: laterally, into other free MIT terminal tools.** `ccusage` (17,700★, **123,955 npm downloads/wk**), `CodexBar` (19,589★), `claude-hud` (27,066★), `codeburn` (9,123★), `Claude-Code-Usage-Monitor` (8,582★) — all $0, all MIT, all pushed within days `[PAGE]`. That cohort is echook's real competition and its ceiling is attention, not revenue.

---

## Ring 3 — The substitute that is not a product

### It is free, and it is Anthropic's own documentation.

| Substitute | Cost | Lines of config | Source |
|---|---:|---:|---|
| Claude Code built-in desktop notification in Ghostty / Kitty / iTerm2 | **$0** | **0** | `[PAGE]` code.claude.com/docs/en/terminal-config |
| `{"preferredNotifChannel": "terminal_bell"}` | **$0** | **3** | `[PAGE]` same |
| Official `afplay` Notification hook | **$0** | **9** | `[PAGE]` same |
| Official 3-platform desktop-notification hook (`osascript` / `notify-send` / PowerShell) | **$0** | ~15 | `[PAGE]` code.claude.com/docs/en/hooks-guide |
| macOS `afplay` (pre-installed, free system sounds in `/System/Library/Sounds`) | **$0** | 1 | `[PAGE]` ss64.com/mac/afplay.html — *"No installation is required—`afplay` comes pre-installed with macOS"* |
| macOS `say` (**this is echook's TTS**) | **$0** | 1 | `[PAGE]` HN comment, story 46985151, kurishutofu 2026-02-12: *"you can just use the say command directly"* |
| `terminal-notifier` | **$0** | 1 | `[PAGE]` gh api — 7,271★, pushed 2025-11-02 |
| BurntToast (Windows toasts) | **$0**, MIT | 1 | `[PAGE]` gh api — 1,724★, pushed 2025-11-17 |
| ntfy.sh hosted (**this is echook's webhooks**) | **$0** free tier, no signup; Supporter $5–6/mo, Pro $10–12/mo, Business $20–25/mo | 1 curl | `[PAGE]` ntfy.sh/#pricing, docs.ntfy.sh/faq |
| Codex CLI `tui.notification_method = bel` | **$0** | 1 | `[PAGE]` learn.chatgpt.com/docs/config-file/config-reference |

Anthropic's page frames it as echook's exact job-to-be-done, verbatim `[PAGE]`:

> "When Claude finishes a task or pauses for a permission prompt, it fires a notification event. Surfacing this as a terminal bell or desktop notification lets you switch to other work while a long task runs."

And the whole competitor, quoted in full `[PAGE]`:

```json
{ "hooks": { "Notification": [ { "hooks": [
  { "type": "command", "command": "afplay /System/Library/Sounds/Glass.aiff" }
] } ] } }
```

**The DIY artifact trail is deep.** Seven blog posts opened and read this session, each teaching an 11–24-line version: understandingdata.com/posts/audio-notification-hooks (13 lines, `afplay`), andrew-seaford.co.uk (18, `pw-play`), andreagrandi.it 2025-07-12 (24, `terminal-notifier`), pascal-poredda.com 2025-07-10 (11, cross-platform), alexop.dev 2025-11-23 (13, `osascript`), daveschumaker.net 2025-07-06, explainx.ai 2026-06-25 — all `[PAGE]`. Twenty gists found across two fetched search pages, dated 2025-07 → 2026-06; four opened: danlandau321/268483ac (15 lines), carychen/dadf138dd, abhagsain/7fa11278 (14 lines), andreagrandi/7e578684 — all `[PAGE]`.

Two quotes that price the category:

> *"No scripts. No files to manage. No allowlist tax."* — gist author carychen, 2026-05-22 `[PAGE]`

> *"The best part? It works on Mac, Windows, and Linux without installing anything extra. It uses the audio players that are already on your computer."* — pascal-poredda.com `[PAGE]`

**What this does to willingness-to-pay: it takes it to zero, and the market already ran the experiment.** The three npm packages that *are* the 5-line version packaged — `cat-ccnotify-hook`, `@dagim_s/claude-code-notification`, `@zhangziheng/mac-notify` — pull **2, 1 and 6 downloads per week** `[PAGE]` npm downloads API, week of 2026-07-27. `code-notify` (280★) pulls **41/wk**. That is the demand curve for paying even the transaction cost of `npm i` rather than pasting a config. There is no price echook can charge above $0, because the substitute is not a rival product you can out-feature — it is documentation.

**The one thing that did win in this category won on personality, not features.** peon-ping's Show HN scored **1,006 points / 301 comments** on 2026-02-12. On the same day, echook's Show HN ("Cross-platform audio notifications for Claude Code", HN id 46985098) scored **3 points, 0 comments** `[PAGE]` hn.algolia.com. Same category, same day, same $0 price, **335× the attention**.

**Honest gap:** Reddit was unfetchable (blocked on `www.reddit.com` and `old.reddit.com`); **no Reddit evidence is asserted**. "People just alt-tab and watch the window" was searched for and **not found** — do not use that line; the sourced version of the same argument is that Ghostty/Kitty/iTerm2 users already get a free desktop notification with zero config.

---

## Ring 4 — Platform absorption

### Claude Code

- **31 documented hook events** `[PAGE]` code.claude.com/docs/en/hooks: SessionStart, Setup, UserPromptSubmit, UserPromptExpansion, PreToolUse, PermissionRequest, PermissionDenied, PostToolUse, PostToolUseFailure, PostToolBatch, Notification, MessageDisplay, SubagentStart, SubagentStop, TaskCreated, TaskCompleted, Stop, StopFailure, TeammateIdle, InstructionsLoaded, ConfigChange, CwdChanged, DirectoryAdded, FileChanged, WorktreeCreate, WorktreeRemove, PreCompact, PostCompact, Elicitation, ElicitationResult, SessionEnd.
- **The `Notification` hook has 8 first-party matchers** `[PAGE]` hooks-guide: `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`, `agent_completed`. **This is echook's event taxonomy, shipped as a config string.**
- **A documented audio setting exists** — correcting the brief's prior: `preferredNotifChannel` accepts `"sound" | "vibration" | "visual" | "none"` (settings page, managed-settings/mobile scope) **and `"terminal_bell"`** (terminal-config page, local terminal) `[PAGE]` both.
- **Trajectory: expanding monotonically.** ≥13 hook events added in ~8 months `[PAGE]` CHANGELOG × npm publish dates: `SubagentStart` 2025-11-17 · `Setup` 2026-01-17 · `TeammateIdle`+`TaskCompleted` 2026-02-06 · `ConfigChange` 2026-02-19 · `WorktreeCreate`/`Remove` 2026-02-20 · `InstructionsLoaded` 2026-03-04 · `StopFailure` 2026-03-17 · `CwdChanged`+`FileChanged` 2026-03-24 · `MessageDisplay` 2026-05-26 · `DirectoryAdded` 2026-07-24.
- **Statusline: the measurement was absorbed.** `exceeds_200k_tokens` 2025-08-22 · **`context_window.used_percentage`/`remaining_percentage` 2026-01-13 (2.1.6)** · `added_dirs` 2026-02-18 · **`rate_limits` 5h/7d + `resets_at` 2026-03-19 (2.1.80)** · `git_worktree` 2026-04-08 · `effort.level`/`thinking.enabled` 2026-04-23 · GitHub PR info 2026-05-19 · `COLUMNS`/`LINES` 2026-05-27 `[PAGE]`.
- **Snooze was absorbed too:** `CLAUDE_CLIENT_PRESENCE_FILE` (2.1.181, 2026-06-17) suppresses push while you are at the machine `[PAGE]`.
- **`terminalSequence`** hook output field (2.1.141, 2026-05-13) lets a hook emit OSC 9/99/777 notifications and BEL without a controlling terminal `[PAGE]`.
- **Feature-request demand is for *notification*, not for *sound*.** Open issues by reactions `[PAGE]` gh api: notification #29438 (69R), #8985 (65R), #28765 (42R), #13922 (40R), #12046 (37R), #29928 (30R), #26581 (30R). Sound: #62444 (**1R**), #25422 (1R), #73384 (**0R**), #47061 (**0R**). Bell: #36850 (9R). Chime: **zero issues**. Users want to be *told*; they are indifferent to *how it sounds*.
- **The adjudication.** #1288 "Feature: Sound notifications" (44R) closed **`completed`** 2025-08-22: *"You can either use `preferredNotifChannel` … or hooks … to set up sound notifications"* `[PAGE]`.
- **Caveat that cuts the other way, and I am keeping it:** #11535 (18R), #14058 (15R), #12520 (14R) are *still open* asking for context-window data in the statusline that shipped in January 2026. Open-issue counts in this repo **overstate** unmet need. Do not read 81 open statusline issues as 81 gaps.

### Cursor

- **21 documented agent-hook events** `[PAGE]` cursor.com/docs/hooks.md, including `stop` — *"Handle agent completion"*.
- **Zero notification/sound documentation.** `cursor.com/llms.txt` `[PAGE]` (full doc index) contains no notifications page; `/docs/configuration/notifications`, `/docs/settings/notifications`, `/docs/agent/notifications` all **404**. Cursor's in-app "play sound on finish" setting is widely reported but **no Cursor-official URL was found** — `[UNVERIFIED]`, claim it in neither direction.
- **The absorption:** `[PAGE]` cursor.com/docs/reference/third-party-hooks.md — *"Cursor can load and execute hooks configured for Claude Code, allowing you to use the same hook scripts across both tools."* Load paths `.claude/settings.local.json`, `.claude/settings.json`, `~/.claude/settings.json`; *"Cursor automatically maps Claude hook names to their Cursor equivalents."*

### OpenAI Codex CLI

- **`notify`** `[PAGE]` learn.chatgpt.com/docs/config-file/config-reference: *"Command invoked for notifications; receives a JSON payload from Codex."* Config `notify = ["python3", "/path/to/notify.py"]`; payload `type` (**only `agent-turn-complete` today**), `thread-id`, `turn-id`, `cwd`, `input-messages`, `last-assistant-message`. The doc's own example shells out to `terminal-notifier`. **No bundled sound.**
- **Native TUI notifications:** `tui.notifications` (bool or event array), `tui.notification_condition` (`unfocused|always` — a native snooze), `tui.notification_method` (`auto|osc9|**bel**`) `[PAGE]`.
- **Native status line:** `tui.status_line` — *"Ordered list of TUI footer status-line item identifiers"* `[PAGE]`. Item identifiers not enumerated on the reference page — `[UNVERIFIED]`.
- **11 Claude-Code-shaped hook events** in PascalCase `[PAGE]` learn.chatgpt.com/docs/hooks.

### Absorption scorecard

| echook capability | Claude Code | Cursor | Codex CLI |
|---|---|---|---|
| Sound on completion | **ABSORBED** (`afplay` hook + `terminal_bell`) | Undocumented — **but Claude hooks execute natively** | **ABSORBED** (`notify` + `bel`) |
| Desktop notification | **ABSORBED** (3-platform examples + `terminalSequence`) | Not documented | **ABSORBED** |
| Per-event granularity | **ABSORBED** (31 events, 8 matchers) | 21 events, no notif semantics | 11 events; `notify` has **one** type — *narrowest gap* |
| Statusline context % | **ABSORBED** (pre-computed since 2026-01-13) | Not documented | Native `tui.status_line` |
| Rate-limit display | **ABSORBED** (since 2026-03-19) | Not documented | Not documented |
| Snooze / mute | **PARTIAL** (`CLAUDE_CLIENT_PRESENCE_FILE`) | — | `notification_condition = unfocused` |
| Cross-harness single install | **Eroding** — Cursor reads `.claude/settings.json`; Codex copied Claude's event names | | |
| Curated theme packs, TTS, debounce, NL config | **Not absorbed by any platform** — but all three are claimed by peon-ping | | |

---

## The correction that comes out of this sweep

Stated bluntly, because the softened version is not useful.

1. **"AI-operated" is not the differentiator.** It is the platform's documented default (Agent Skills), and a 4,973★ competitor in the same niche ships five of them. See the prior-art audit.
2. **The statusline is not a differentiator.** Eighteen statusline projects have more stars than echook has, total, and Anthropic pre-computes every number echook's bars display.
3. **The sound is not a differentiator.** It is nine lines in Anthropic's docs, and Anthropic closed the feature request as `completed`.
4. **What is actually left, and it is small but real:** echook is the **only project found that combines (a) per-event granularity at 39 distinct lifecycle events with (b) a first-class Cursor and Codex install path and (c) a validated JSON-in/JSON-out CLI (`audio-hooks manifest` / `set` / `status` / `diagnose` / `test`) designed so an agent never hand-edits config.** peon-ping has 21 harnesses but 7 sound categories. `claudio` has audio for CC+Codex but no Cursor and no statusline. `agent-tools` (159★) has skills+statusline+multi-harness but not the event depth. Nobody found has all three.
5. **So the honest positioning is depth-per-event and refusal-to-hand-edit, not "AI-operated".** And the honest commercial read is that depth-per-event is a **hobbyist-grade differentiator** — the demand data says users want to be told, not told precisely (sound feature requests: 1, 1, 0, 0 reactions).
6. **There is no monetization here.** Ring 1 is uniformly $0 with no paid tier anywhere in ~39 projects. Ring 2 sells to a different person. The winner in Ring 1 won on a Warcraft joke, not on features.

---

## Threat ranking — by TRAJECTORY, not current size

| # | Threat | Now | Trajectory | Why it ranks here |
|---|---|---|---|---|
| **1** | **Anthropic first-party absorption** | Already ate both tracks | **Accelerating** — ≥13 hook events + 8 statusline fields in 8 months, and `/statusline` now writes your script from natural language | Every release narrows what a wrapper can add. This is not a competitor you out-execute; it is the floor rising. |
| **2** | **peon-ping** | 4,973★, 21 harnesses, 5 skills, MCP, Homebrew, own domain, 1,006-point HN post | **Compounding** — 367 forks, a pack registry, community sound packs | Owns the mindshare *and* the mechanism echook claims. If it adds a statusline, echook has nothing left. |
| **3** | **The free 5-line hook (Anthropic's own docs)** | $0, 0–9 lines, first result a user hits | **Static but permanent** | Caps willingness-to-pay at zero forever. Does not need to improve to win. |
| **4** | **claude-hud / ccstatusline** | 27,066★ / 12,205★ + 72,918 npm/wk | **Growing, shipping daily** | They own the statusline slot. echook's second track cannot be reached from here. |
| **5** | **Cursor's third-party-hooks compat layer** | Shipped | **Expanding** (Codex already copied Claude's PascalCase event names) | Converts "works in three editors" from a feature into a checkbox someone else ticks. |
| **6** | **Terminal vendors** (Warp official integration 224★; cmux 25,549★) | Shipping | **Rising** — the terminal is a better place for this than a hook | If your terminal notifies you, you never search GitHub. |
| **7** | **Langfuse's Claude Code hook integration** | 32,449★ repo, occupies the same hook slot, silent today | **Watch item** | One feature away from being Ring 1 with a 32k-star company behind it. |
| **8** | **The long tail** (~39 free clones, ~9 multi-harness) | Individually tiny | **High churn — many die** | Not a threat to survival; a threat to *attention*. Nothing here is scarce. |

---

## What would prove this wrong

Checkable observations, ordered by cost to test.

| # | Observation that would falsify a conclusion | Which conclusion it kills | Method | Cadence |
|---|---|---|---|---|
| 1 | **peon-ping's skills are decorative** — e.g. `user_invocable: false` on all five means the agent never actually reaches them in practice, or issues show they don't fire | "Ours isn't the only agent-operated one" | Read all 5 `skills/*/SKILL.md`; search peon-ping issues for `skill`; install and try `"mute peon-ping"` in a live Claude Code session | Once, ~1h. Re-check on peon-ping minor releases |
| 2 | **The sound-request reaction counts are an artifact of duplicate-closing**, and demand for *audio specifically* is real | "Users want to be told, not told precisely" | `gh api` all closed sound/audio/chime issues incl. `not_planned`; sum reactions across duplicates; compare to the notification cluster | Once, ~30min. Quarterly |
| 3 | **Someone monetizes this ring** — any Ring-1 project ships a paid tier, sponsorship above trivial, or a hosted plan | "There is no revenue in this ring" | Check GitHub Sponsors + pricing pages for peon-ping, claude-hud, ccstatusline, code-notify, Lucarne, vibe-notch | Monthly, ~15min |
| 4 | **echook's 39 events actually get used** — installs concentrate on events no competitor exposes | "Depth-per-event is a hobbyist differentiator" | Ship anonymous opt-in event-fire telemetry, or read config diffs in issues/forks; if >20% of users enable events outside the 8 Claude matchers, depth is load-bearing | One release + 60 days |
| 5 | **Anthropic stops expanding the surface** — two consecutive quarters with no new hook event and no new statusline field | Threat #1 ranking | Diff `anthropics/claude-code` CHANGELOG for `hook event` / `status line` additions | Quarterly, ~20min |
| 6 | **Cursor's third-party-hooks flag is off by default and rarely enabled** | "Cursor absorbed the cross-editor prop" | Fetch the Cursor docs default; poll Cursor forum/issues for enablement reports; check whether echook's Cursor installs exceed its Claude installs | Once + monthly re-fetch |
| 7 | **A Cursor-native notification setting genuinely does not exist** (currently `[UNVERIFIED]`) | The one platform gap echook can still claim | Install Cursor, open Settings, screenshot; or find a Cursor-official changelog entry | Once, ~30min — **do this before writing any Cursor-gap copy** |
| 8 | **A statusline project starts consuming echook's hook events**, or an audio project ships a statusline | "Nobody found has all three" | Watch releases of claude-hud, ccstatusline, agent-tools, peon-ping for the crossover feature | Monthly |
| 9 | **The DIY substitute has a real failure rate** — the 5-line hook is widely reported broken (VS Code native-UI mode, WSL, tmux, headless) enough that packaging is worth paying for | "Willingness-to-pay is zero" | Count comments on `anthropics/claude-code#8985` (65R, "Notification hook doesn't work in VS Code native UI mode") and #5186 (32R, 10s delay); survey 20 DIY blog comment threads for "didn't work" | ~2h. This is the single most promising falsifier — a broken free substitute is the only path back to willingness-to-pay |
| 10 | **Reddit contradicts the HN signal** — r/ClaudeAI shows sustained organic discussion of echook | Ring 3's attention verdict | Reddit was **blocked this session**; retry with an authenticated client or the Pushshift-style API | Once, then quarterly |

**Explicitly not tested and therefore not claimed:** Reddit sentiment (fetch blocked), PyPI package landscape (search page is a JS shell), Cursor's in-app sound setting, Codex `tui.status_line` item identifiers, Helicone/LangSmith/Braintrust Claude-Code-specific marketing (search budget exhausted — unprobed, not negative).
