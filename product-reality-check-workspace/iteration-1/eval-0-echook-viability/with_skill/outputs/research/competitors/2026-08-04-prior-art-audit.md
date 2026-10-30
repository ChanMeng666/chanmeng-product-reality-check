# echook — Prior-Art Audit (hostile mandate)

**Date:** 2026-08-04 · **Subject:** `github.com/ChanMeng666/echook` — 78★, 7 forks, MIT, created 2025-11-01, last push 2026-07-19 `[PAGE]` gh api.

**Mandate:** kill the novelty claims. A claim survives only if it survives an adversarial read.

**Grades:** `[PAGE]` opened this session, quotable · `[SNIPPET]` not opened, not quotable · `[UNVERIFIED]` treat as false.

**The claims under audit, quoted verbatim from echook's own `README.md` and `llms.txt` (read locally, read-only):**

> "**AI-operated audio notification system for Claude Code, Cursor IDE, and Codex CLI.** You type one slash command at install time. Then natural language forever."
> "🤖 **This is an AI-Agent-first project — you don't read this, your agent does**"
> "**Humans: don't install or configure echook by hand.**"
> "v6.2.0 — **complete hook coverage** … 39 hook events across all three editors"
> "pin a **context-usage status line** so you never lose your place"
> (`llms.txt`) "An AI agent … **clones, installs, configures, tests, and uninstalls the whole project on the user's behalf** — there are no human-interactive menus, no `curl | bash` flows, and nothing to hand-edit."

---

## CLAIM 1 — "AI-operated, not AI-assisted" / "you don't read this, your agent does"

### The split, before any evidence

| Distinction | The claim, isolated | Novel? |
|---|---|---|
| **(a)** Natural-language **configuration** vs natural-language **operation** | "You say 'mute for an hour' and it happens" | **No** |
| **(b)** Agent-**readable** docs (AGENTS.md / llms.txt / SKILL.md) vs agent-**operated** software | "The docs are for the agent, and the agent drives the tool" | **No** |
| **(c)** **Installed**-by-agent vs **controlled**-by-agent | "The agent installs it AND keeps operating it" | **No** |

Splitting it does not save it. Each half is separately refuted, and (c) — the strongest-sounding half — is refuted twice: once by the platform and once by a direct competitor.

### Evidence

**E1 — Anthropic's engineering blog, published 2025-10-16 `[PAGE]` anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills. Verbatim:**

> "organized folders of **instructions, scripts, and resources** that agents can discover and load dynamically to perform better at specific tasks"

> "**Skills are authored for agents rather than humans**—they're bundles containing a SKILL.md file with context that Claude loads into its system prompt at startup"

> "Skills can also **include code for Claude to execute as tools at its discretion**"

echook's banner says "you don't read this, your agent does." Anthropic wrote "authored for agents rather than humans" **as the definition of the file format echook ships**, ~9.5 months earlier.
→ **REFUTES (fatal).** Adoption: this is the platform itself.

**E2 — Agent Skills overview `[PAGE]` platform.claude.com/docs/en/agents-and-tools/agent-skills/overview. Verbatim:**

> "Each Skill packages **instructions, metadata, and optional resources (scripts, templates) that Claude uses automatically when relevant.**"
> "This filesystem-based architecture enables **progressive disclosure**"
> "**Code:** Executable scripts … **that Claude runs using bash**, providing deterministic operations without loading their code into context"

"Instructions plus scripts the model runs" — the exact architecture echook describes as its insight.
→ **REFUTES (fatal).**

**E3 — Claude Code Skills docs `[PAGE]` code.claude.com/docs/en/skills. Verbatim:**

> "Create a `SKILL.md` file with instructions, and Claude adds it to its toolkit. **Claude uses skills when relevant**"
> "`└── scripts/ └── validate.sh    # **Script Claude can execute**`"
> "**Using the same variable in both places lets a skill run a bundled script without a permission prompt.**"
> ```yaml
> allowed-tools: Bash(${CLAUDE_SKILL_DIR}/scripts/render.sh *)
> ```

Anthropic ships a **worked example of echook's exact architecture** — a SKILL.md instructing the agent to invoke a bundled CLI, pre-authorized — as documentation of the *intended* pattern.
→ **REFUTES (architecture-level).**

**E4 — `/statusline` accepts natural language and writes your config `[PAGE]` code.claude.com/docs/en/statusline. Verbatim:**

> "**The `/statusline` command accepts natural language instructions describing what you want displayed. Claude Code generates a script file in `~/.claude/` and updates your settings automatically:**"
> `/statusline show model name and context percentage with a progress bar`
> "Run `/statusline` and **ask it to remove or clear your status line** (e.g. `/statusline delete`, `/statusline clear`, `/statusline remove it`)."

Anthropic ships natural-language configuration of a local tool by an agent — including the "turn it off in plain English" gesture echook markets as *"mute for an hour"* — **for the status line specifically, one of echook's two advertised tracks**.
→ **REFUTES (a), and in-domain.**

**E5 — `/fewer-permission-prompts` `[PAGE]` code.claude.com/docs/en/commands. Verbatim:**

> "`/fewer-permission-prompts` — **Skill.** Scan your transcripts for common read-only Bash and MCP tool calls, then **add a prioritized allowlist to project `.claude/settings.json`**"

A bundled Anthropic Skill that mutates settings on the user's behalf, shipped in the box.
→ **REFUTES (a).**

**E6 — `update-config` skill and `statusline-setup` agent.** Both are registered in this session's live Claude Code runtime; `update-config`'s description reads *"Use this skill to configure the Claude Code harness via settings.json … Examples: 'allow npm commands', 'set DEBUG=true', 'when claude stops show X'"* — i.e. Anthropic ships a natural-language, hook-installing configurator, and its own example is *echook's install flow*. **Sourcing caveat stated plainly:** verified by direct runtime observation, **not** by a docs page fetched this session; the `/commands` fetch did not surface `update-config`. E4 and E5 already carry the refutation without it.
→ **REFUTES (a), documentation status unconfirmed.**

**E7 — the field count `[PAGE]` gh api search/code, executed this session:**

| Metric | Count |
|---|---:|
| Files named `SKILL.md` on GitHub | **601,280** |
| Files named `AGENTS.md` on GitHub | **168,544** |
| Repos matching `claude skills` | **73,195** |
| Repos matching `claude code plugin` | 22,152 |

→ **REFUTES by saturation.** "Agent-first" at 601,280 SKILL.md files is the median, not the edge.

**E8 — THE STRONGEST SINGLE PIECE OF PRIOR ART: `PeonPing/peon-ping` `[PAGE]` gh api.**
4,973★ · 367 forks · MIT · pushed 2026-07-24 · created 2026-02-09 · own domain `peonping.com`.
Repo root contains `skills/`, `CLAUDE.md`, `GEMINI.md`, `mcp/`. `skills/` contains **five** skills: `peon-ping-config`, `peon-ping-log`, `peon-ping-rename`, `peon-ping-toggle`, `peon-ping-use`. `skills/peon-ping-config/SKILL.md` frontmatter, verbatim:

> `description: Update peon-ping configuration — volume, pack rotation, categories, active pack, and other settings. Use when user wants to change peon-ping settings like volume, enable round-robin, add packs to rotation, toggle sound categories, or adjust any config.`

It also ships a **60+ command CLI** (`peon pause`, `peon volume 0.7`, `peon packs use <name>`, `peon notifications template …`) — the agent-drivable non-interactive surface echook cites as its design — **and** an MCP server where *"the agent chooses the sound"* via a `play_sound` tool. Same niche. Same mechanism. **63× the stars.**
→ **REFUTES (a)(b)(c) in-domain, with adoption.** This is the citation a skeptic finds in one search.

**E9 — `Nanako0129/coralline` `[PAGE]` gh api.** 530★, MIT, pushed 2026-08-03. Description verbatim: *"🪸 Powerlevel10k-inspired statusline for Claude Code — **paste one prompt and your AI interviews you, then installs**"*.
→ **REFUTES claim 2's "one slash command at install"** — agent-conducted install, in echook's statusline niche, at 6.8× the stars.

**E10 — `kairyou/agent-tools` `[PAGE]` gh api.** 159★, MIT, pushed 2026-08-04. Description: *"Reusable **Agent Skills**, plus integrations (**statusline**, provider usage, vision) that **install into Codex, Claude**…"*. Repo root has `.claude-plugin/`, `.codex-plugin/`, `skills/`, `AGENTS.md`.
→ **REFUTES the combined claim** — skills + statusline + multi-harness plugin manifests, the same bundle, at 2× the stars.

**E11 — agents.md `[PAGE]`.** *"A simple, open format for guiding coding agents"*, *"used by over 60k open-source projects"*, backed by OpenAI, Google, Cognition, Anthropic, JetBrains, GitHub; *"now stewarded by the Agentic AI Foundation under the Linux Foundation."*
**E12 — llmstxt.org `[PAGE]`**, Jeremy Howard, **2024-09-03**: *"we expect many of these files to be **read by language models and agents**."*
→ Both **REFUTE (b).** "You don't read this, your agent does" was a published convention 23 months earlier and is now a Linux Foundation standard.

**E13 — echook's own README concedes the exception `[PAGE]`, local read:** *"The only thing a human ever types by hand is one `/reload-plugins` slash command."* Meanwhile `[PAGE]` code.claude.com/docs/en/plugins documents `/plugin install` as the platform install path and routes a plugin's `bin/` onto the agent's `PATH` by design.
→ **REFUTES (c)** and softens "one".

### Grades table — Claim 1

| Evidence | Grade | Adoption |
|---|---|---|
| E1 Anthropic blog "authored for agents rather than humans" | **REFUTES — fatal** | Platform |
| E2 Skills = instructions + scripts Claude runs via bash | **REFUTES — fatal** | Platform |
| E3 `${CLAUDE_SKILL_DIR}` + `allowed-tools` bundled-CLI worked example | **REFUTES — architecture** | Platform |
| E4 `/statusline` natural-language configurator | **REFUTES (a) — in-domain** | Platform |
| E5 `/fewer-permission-prompts` settings-mutating skill | **REFUTES (a)** | Platform, bundled |
| E6 `update-config` / `statusline-setup` | **REFUTES (a) — doc-unconfirmed** | Platform, bundled |
| E7 601,280 SKILL.md / 168,544 AGENTS.md | **REFUTES — saturation** | — |
| **E8 peon-ping: 5 skills + CLI + MCP, same niche** | **REFUTES — fatal, in-domain, with adoption** | **4,973★, 367 forks, active** |
| E9 coralline "your AI interviews you, then installs" | **REFUTES claim 2** | 530★, active |
| E10 agent-tools skills+statusline+multi-harness | **REFUTES combined claim** | 159★, active |
| E11 agents.md, 60k projects, Linux Foundation | **REFUTES (b)** | Standard |
| E12 llms.txt, Sept 2024 | **REFUTES (b)** | Standard |
| E13 `/plugin install`; echook's own `/reload-plugins` caveat | **REFUTES (c)** | Platform |
| obra/superpowers, anthropics/skills (very large skill collections) | **DOES NOT REFUTE — ACTIVELY SUPPORTS** "the pattern is mainstream" | Very large |

**ACTIVELY SUPPORTS — the citations the narrative actually needs.** E1/E2/E3 are excellent evidence that **echook is a well-formed, conformant Agent Skill**. Use them to say "echook is built the way Anthropic says to build this." Never use them to say echook invented it.

**VERDICT — Claim 1 is DEAD.** Not crowded. Dead. It paraphrases Anthropic's published definition of the primitive echook ships, and a 63×-larger competitor in the same product category implements it more completely (5 skills + MCP + 60-command CLI vs echook's CLI + skill).

---

## CLAIM 2 — "One slash command at install. Then natural language forever."

- The install gesture: `/plugin install` and `/plugin marketplace add` are **the platform's documented install UX** `[PAGE]` code.claude.com/docs/en/plugins, plugin-marketplaces. → **REFUTES.**
- "Natural language forever": that is what `description` / `when_to_use` trigger-matching does for **all 601,280** SKILL.md files `[PAGE]`. echook's NL control works *because* it conforms to a documented matching mechanism, not because it found one. → **REFUTES.**
- peon-ping does the same via `peon-ping-config` + `peon-ping-toggle` skills, and adds a slash command `/peon-ping-toggle` and CLI aliases `peon mute` / `peon unmute` `[PAGE]`. → **REFUTES, in-domain.**
- `Nanako0129/coralline` (530★): *"paste one prompt and your AI interviews you, then installs"* `[PAGE]`. → **REFUTES.**
- `777genius/claude-notifications-go` (773★) markets *"1 line installation"* `[PAGE]`. → **PARTIALLY REFUTES** (one line, not one NL sentence).
- echook's own README: a human still must type `/reload-plugins` by hand `[PAGE]`. → **Self-refuting on "one".**

**VERDICT — DEAD as a differentiator.** It survives only as an accurate *description* of the install flow, which is a feature statement, not a claim of priority.

---

## CLAIM 3 — "Complete hook coverage" (39 events across three editors)

This is the one that partially survives, and it needs its adjective changed.

**What refutes "complete":**
- Claude Code documents **31 hook events** and 8 `Notification` matchers `[PAGE]` hooks / hooks-guide; Cursor documents **21** `[PAGE]` cursor.com/docs/hooks.md; Codex documents **11** `[PAGE]` learn.chatgpt.com/docs/hooks. That is **63 distinct documented events** across the three harnesses. echook covers 39. **"Complete" is arithmetically false today.**
- The target moves roughly monthly: ≥13 Claude Code hook events added in ~8 months `[PAGE]` CHANGELOG × npm dates, most recently `DirectoryAdded` 2026-07-24. echook's last push was 2026-07-19 — **before** that event existed. A "complete coverage" claim decays between releases by construction.

**What does not refute it, and is the real finding:**
- **peon-ping covers 21 harnesses but collapses everything into 7 sound categories** — `session.start`, `task.acknowledge`, `task.complete`, `task.error`, `input.required`, `resource.limit`, `user.spam` `[PAGE]` `skills/peon-ping-config/SKILL.md`. Breadth without depth.
- `ctoth/claudio` (110★): audio for Claude Code + Codex, **no Cursor**, no statusline `[PAGE]`.
- `DevinoSolutions/anotifier-for-claude-codex-cursor` (18★): CC + Codex + Gemini + Cursor, desktop/phone only `[PAGE]`.
- `settinghead/voxlert` (12★): CC + Cursor + Codex + pi + OpenClaw, LLM-generated voice `[PAGE]`.
- `DefaultPerson/agent-setup` (11★): CC + Codex, TTS + statusline `[PAGE]`.
- **No project found matches echook's per-event granularity on Cursor and Codex simultaneously.** The three that cover the same harness set are at 18, 12 and 11 stars.

**Grade: PARTIALLY REFUTES.** "Complete" is dead. "**The finest per-event granularity found on Cursor and Codex**" is checkable, currently true, and nobody has contested it.

---

## CLAIM 4 — The context-usage status line

**Grade: DEAD, and the most crowded claim of the four.**

| Fact | Evidence |
|---|---|
| `gh api search/repositories?q=claude+code+statusline` → **2,161 repos** | `[PAGE]` |
| **18 statusline projects have more stars than echook has in total** | `[PAGE]` — see sweep §1b |
| `jarrodwatts/claude-hud` — *"context usage, active tools, running agents, todo progress"* — **27,066★, 1,257 forks**, pushed 2026-08-01 | `[PAGE]` — **347×** echook |
| `sirmalloc/ccstatusline` — **12,205★, 534 forks, 72,918 npm downloads last week** | `[PAGE]` gh api + npm downloads API |
| `leeguooooo/claude-code-usage-bar` (342★) — *"5h/7d rate-limit usage, reset countdowns, model + context window"* — echook's exact feature list | `[PAGE]` |
| Claude Code **pre-computes** `context_window.used_percentage` (2.1.6, 2026-01-13) and `rate_limits.*` (2.1.80, 2026-03-19) and hands them to any script | `[PAGE]` CHANGELOG × npm publish dates |
| The statusline doc's **own hero example is a color-coded context bar**; `/statusline` writes it from natural language | `[PAGE]` code.claude.com/docs/en/statusline |

echook's statusline is **formatting, not measurement**, in a niche with 2,161 entrants and a 27,066★ leader.

---

## RETRACTIONS — exactly which words are now BANNED, and by what evidence

| Banned words | Killed by |
|---|---|
| **"AI-operated, not AI-assisted"** | E1 (Anthropic, 2025-10-16: *"Skills are authored for agents rather than humans"*), E8 (peon-ping's 5 skills, 4,973★) |
| **"you don't read this, your agent does"** | E12 (llms.txt, 2024-09-03: *"read by language models and agents"*), E1, E11 (agents.md, 60k projects, Linux Foundation) |
| **"the human is upstream of the agent, not downstream of the CLI"** | E1–E3. This is Claude Code's product thesis, not echook's observation |
| **"This is an AI-Agent-first project"** *as a differentiator* | E7 (601,280 SKILL.md files). Keep it as a usage instruction; delete it as a claim |
| **"One slash command at install. Then natural language forever"** *as novelty* | E13 (`/plugin install` is the platform UX; echook itself requires a manual `/reload-plugins`), E9 (coralline, 530★), peon-ping's `/peon-ping-toggle` |
| **"complete hook coverage"** | 63 documented events across the three harnesses vs echook's 39; `DirectoryAdded` shipped 2026-07-24, after echook's last push |
| **"never lose your place" / the statusline as a selling point** | 2,161 statusline repos; claude-hud 27,066★; Anthropic pre-computes every number |
| **"first"** or **"only"** in any form, about any of the four claims | Every row above |

---

## BANNED CITATIONS

1. **"A search for our exact description returns only us."** Not independent evidence of anything. It measures phrasing uniqueness, not category uniqueness — and this sweep found 39 direct competitors and 18 larger statusline projects using different words for the same thing.
2. **GitHub star count as evidence of differentiation.** At 78★ against 4,973 / 12,205 / 27,066, stars argue the opposite.
3. **"No one else ships a SKILL.md for this."** False: peon-ping ships five `[PAGE]`.
4. **Open-issue counts on `anthropics/claude-code` as proof of unmet demand.** #11535 (18R), #14058 (15R), #12520 (14R) all still ask for statusline context data that **shipped in January 2026** `[PAGE]`. Open issues in that repo systematically overstate the gap.
5. **Anthropic's Agent Skills docs as evidence of novelty.** They are evidence of *conformance*. Cite them for that and only that.

---

## The counterexamples a knowledgeable skeptic will throw

**Skeptic 1: "peon-ping already does all of this, has 4,973 stars, covers 21 harnesses, and is funnier."**
→ **Concede:** everything. It ships five Agent Skills, an MCP server, a 60-command CLI, a pack registry, Homebrew, a domain, and a 1,006-point HN post. It refutes the AI-operated claim outright, and it beat echook 335-to-1 on attention on the same day.
→ **Hold:** it collapses every lifecycle event into **7 sound categories** `[PAGE]`. echook maps 39 distinct events, including Cursor's per-tool-type events and Codex's hook set, with per-event configuration. If you want "a Warcraft peon yells when it's done", peon-ping wins and it isn't close. If you want a different sound for `PostToolUseFailure` than for `PermissionRequest` on Cursor, echook is the only one found that does it.

**Skeptic 2: "Anthropic's own docs have a nine-line `afplay` hook. Why would anyone install anything?"**
→ **Concede:** completely, and this caps willingness-to-pay at $0 permanently. Anthropic closed issue #1288 (44R) as **`completed`** pointing at exactly that `[PAGE]`.
→ **Hold:** the nine-line hook is one sound for one event on one OS. It has no per-event mapping, no debounce, no mute, no cross-platform audio path, and demonstrably breaks in real setups — #8985 *"Notification hook doesn't work in VS Code extension native UI mode"* has **65 reactions**, #5186 *"Notification Hook 10 second delay"* has 32 `[PAGE]`. Packaging is worth something exactly to the extent those breakages are common — **and that is an open empirical question, listed as falsifier #9 in the sweep.**

**Skeptic 3: "Anthropic ships `/statusline`, which does natural-language config already."**
→ **Concede:** fully. E4 is verbatim, and it is in echook's own domain.
→ **Hold:** `/statusline` configures the statusline. It does not configure hook-driven audio, per-event sound mapping, TTS, or webhooks. The *mechanism* is not novel; the *coverage* of that mechanism across echook's config surface is broader. That is a smaller claim and it is the true one.

**Skeptic 4: "There are 18 statusline projects bigger than you. Why ship one at all?"**
→ **Concede:** the statusline is not a differentiator and should not lead any pitch.
→ **Hold:** it is bundled, not competing — a user who installed echook for audio gets the bar without installing a second tool. That is a *convenience* argument, not a *superiority* argument, and must be phrased as such.

**Skeptic 5: "Cursor executes Claude Code hooks natively. Your cross-editor story is a checkbox."**
→ **Concede:** the quote is unambiguous `[PAGE]` cursor.com/docs/reference/third-party-hooks.md, and it erodes the multi-editor pitch.
→ **Hold:** the compat layer maps Claude's event names to Cursor's; it does not create Cursor's **21 native events** or its per-tool-type granularity, which echook targets directly. Also: it is gated behind a settings toggle whose default I could **not** verify — see unresolved.

**Skeptic 6: "Nobody wants sound. Your own platform's data says so."**
→ **Concede:** the reaction counts are brutal — notification requests at 69/65/42/40/37 reactions; **sound requests at 1, 1, 0, 0; chime: zero issues** `[PAGE]`. Users want to be *told*, not *serenaded*.
→ **Hold:** the winner of this category (peon-ping, 4,973★) is a *pure sound* product, so revealed preference contradicts stated preference — but note this cuts against echook too, since peon-ping won on personality and echook has none.

**Skeptic 7: "39 events is feature-count theatre. Show me anyone using event #30."**
→ **Concede:** no usage evidence exists. This is falsifier #4 and it is unmeasured.
→ **Hold:** nothing. This one lands until telemetry exists.

---

## The arguments that need NEITHER "first" NOR "only"

### Shape (a) — a PROPERTY, not a priority claim

1. **"echook has no interactive install path. Every capability is a non-interactive `audio-hooks` subcommand that takes and returns JSON, and hand-editing config is unsupported by design."** This is a **checkable architectural property** of the repo (`llms.txt`, `bin/`, `audio-hooks manifest|set|status|diagnose|test`). It is true whether or not anyone else does it. It does not require the word "first" and cannot be refuted by finding another project that also does it — it can only be refuted by finding an interactive path inside echook.

2. **"39 hook events, of which N are exposed by no other multi-harness notification project."** A number, verifiable by anyone with `gh` and an hour. It survives a competitor shipping 40 tomorrow — you just update N.

3. **"One install covers Claude Code, Cursor and Codex with per-event sound mapping on each."** A capability statement. peon-ping covers more harnesses with less granularity; claudio covers fewer harnesses with comparable granularity. The property is the conjunction, and the conjunction is stated without a superlative.

### Shape (b) — THE VARIABLE THAT CHANGED

The interesting version of "someone tried this and it didn't take" is specific:

- **`htjun/claude-code-hooks-scv-sounds`** (41★) — the earliest twin found, created **2025-08-15**, last push **2025-08-15**. One commit, then nothing. `[PAGE]`
- **`dazuiba/CCNotify`** (216★) — dead 2025-10-14, ~10 months. `[PAGE]`
- **`JessyTsui/Claude-Code-Remote`** (1,275★, 135 forks) — dead 2025-12-06, 8 months. `[PAGE]`
- **`soulee-dev/claude-code-notify-powershell`** (92★) — dead 2026-01-11. `[PAGE]`
- **`kdush/Claude-Code-Notifier`** (94★) — dead 2026-02-01. `[PAGE]`
- **`rubenflamshepherd/claude-code-notif-manager`** (39★) — dead 2026-02-13. `[PAGE]`
- **`sokojh/ai-notifier-swift`** (13★) — dead 2026-01-21. `[PAGE]`

**What changed, and does the reason still hold?** The most defensible read of these deaths is **maintenance cost against a moving platform**: Claude Code added ≥13 hook events in 8 months `[PAGE]`, so a notification tool that is not actively re-synced silently stops covering the lifecycle it advertises. A one-commit sound-pack repo cannot absorb that. **That reason still holds, and it cuts both ways** — echook's own last push (2026-07-19) predates `DirectoryAdded` (2026-07-24). The variable that would make echook durable where they were not is *a generated, manifest-driven event table re-synced per platform release*, and that is an engineering commitment, not a marketing line.

**An alternative explanation I cannot rule out and will not hide:** several of these may have died because the *problem* went away when Anthropic documented `preferredNotifChannel` and the `afplay` hook, and closed #1288 as `completed` (2025-08-22 — nine days after `scv-sounds`' only commit). Under that reading, convergent invention is evidence the gap **was** real and **has since been filled**, which is a worse story. The two readings are distinguishable by falsifier #9 in the sweep (do the free hooks actually work?), and until that is run, **do not assert either**.

### Convergent invention, reframed as evidence — with the honest caveat

The checkable, superlative-free version:

> **"Nine identifiable projects independently built agent-completion notifications for Claude Code between August 2025 and February 2026 — evidence the gap is real and was felt by capable people. Seven of them have not been touched in six months or more; the largest of those, `Claude-Code-Remote`, had 1,275 stars and 135 forks when it stopped. echook is one of the few in that cohort still shipping."**

Every number is `gh api`-verifiable in under a minute.

**But do not overclaim "still maintained and complete", because it does not survive its own test.** echook's last push is **2026-07-19**. Competitors that pushed on **2026-08-04 or 2026-08-03**: `code-notify`, `agent-tools`, `hoangsonww/Claude-Code-Agent-Monitor`, `agentbro`, `anotifier`, `ccstatusline`, `Lucarne` (2026-08-02), `claude-hud` (2026-08-01), `peon-ping` (2026-07-24). **echook is fresher than the abandoned twins and staler than every leader.** The honest sentence is "still shipping", not "the one that's still maintained" — and if freshness is going to be the argument, the fix is to push, not to phrase it more carefully.

---

## EXPLICITLY UNRESOLVED — what I could not verify

1. **Cursor's in-app "play sound on finish" setting.** Widely reported; **no Cursor-official URL found**. `cursor.com/llms.txt` has no notifications page; `/docs/configuration/notifications`, `/docs/settings/notifications`, `/docs/agent/notifications` all 404. `[UNVERIFIED]` — **claim it in neither direction.** This is the single gap echook might still legitimately own, and it is unproven.
2. **The default state of Cursor's "Include third-party Plugins, Skills, and other configs" toggle.** Determines whether the Claude-hook compat layer is on for most users.
3. **Codex `tui.status_line` item identifiers** — not enumerated on the reference page; not found via `gh api search/code` on `openai/codex`. `[UNVERIFIED]`.
4. **`update-config` / `statusline-setup` documentation status.** Runtime-verified this session, **not** doc-verified.
5. **Reddit sentiment.** `www.reddit.com` and `old.reddit.com` both blocked. **No Reddit claim is made anywhere in this audit.**
6. **PyPI landscape.** `pypi.org/search` returned a JS shell. No PyPI claim is made.
7. **"People just watch the window."** Searched, **not found**. Do not use it.
8. **Whether echook's 39 events are used.** No telemetry, no evidence. Feature-count claims are unbacked by usage.
9. **peon-ping skill efficacy.** All five skills carry `user_invocable: false` in the one file I read; whether the agent reliably reaches them in practice is untested. This is the only realistic path to narrowing E8, and it is **narrowing, not reversing** — the skills exist and are documented regardless.
10. **Whether the abandoned twins died from maintenance cost or from the problem being solved.** Both readings fit the dates. Unresolved, and material.

---

## What would prove this audit wrong

| # | Observation | Kills which verdict | Method | Cost |
|---|---|---|---|---|
| 1 | peon-ping's five skills never fire in a real session (agent can't reach them) | Narrows E8 from "fatal" to "partial" | Install peon-ping in Claude Code; say "mute peon-ping"; observe | ~1h |
| 2 | Cursor ships **no** native sound setting AND its third-party-hooks toggle defaults **off** | Restores a real platform gap for echook | Install Cursor, screenshot Settings; find the documented default | ~30min |
| 3 | The free `afplay` hook fails for a large fraction of users (VS Code native UI, WSL, tmux, headless) | Restores nonzero willingness-to-pay | Count reactions/comments on `anthropics/claude-code#8985` (65R) and #5186 (32R); survey 20 DIY blog comment threads | ~2h |
| 4 | A `gh api` sweep finds **no** other notification/statusline project shipping a SKILL.md besides peon-ping and agent-tools | Narrows the saturation argument to "rare in-niche, common in general" | `gh api search/code?q=filename:SKILL.md+notification` and manual triage of the 39 Ring-1 repos | ~1h |
| 5 | echook's 39-event map covers events **no** competitor exposes, and users enable them | Rescues claim 3 as a real differentiator | Diff echook's event table against peon-ping/claudio/anotifier; then opt-in telemetry | 1 release + 60d |
| 6 | Anthropic deprecates or freezes the hooks surface | Reverses the "moving target" reading of the abandoned twins | Diff CHANGELOG quarterly for hook/statusline additions | 20min/quarter |
| 7 | Reddit shows sustained organic echook discussion contradicting the HN 3-vs-1006 signal | Reopens the attention question | Retry Reddit with an authenticated client | ~1h |
