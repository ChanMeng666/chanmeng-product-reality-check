# Claim ledger — echook engagement

Every externally checkable number in `VERDICT.md`, `positioning.md`, `viability.md` and
`messaging-library.md`. Built while writing, not afterwards.

**Rules in force:** an unsourced claim is **deleted, not softened**. Where two reports disagreed, the row
says so — the disagreement is a finding, and it is never resolved toward the flattering number. Rows
marked `[UNVERIFIED]` must not be used in outward-facing copy.

Grades: `[PAGE]` = opened the source and read the value off it, quotable · `[SNIPPET]` = a search result
quoted it, not quotable · `[UNVERIFIED]` = asserted by an aggregator only, treat as false · `[REPO]` =
internal, cited by file path and line.

| # | Claim as stated | Source | Grade | Verified |
|---|---|---|---|---|
| 1 | echook has **78** GitHub stars | `gh api repos/ChanMeng666/echook` | `[PAGE]` | 2026-08-04 |
| 2 | Star count was **79** earlier the same day; one was removed during the engagement | two `gh api` reads, same session | `[PAGE]` | 2026-08-04 — **supersedes** the 79 used in the research briefs |
| 3 | Stars by month, peak **19** in 2026-04, **4** in 2026-07 | `gh api .../stargazers` with `star+json` | `[PAGE]` | 2026-08-04. Diagnostic and I disagreed on March (10 vs 11); **10 is correct**, re-verified |
| 4 | 7 forks, 1 watcher, 1 open issue | `gh api repos/ChanMeng666/echook` | `[PAGE]` | 2026-08-04 |
| 5 | 152 commits; first commit 2025-11-01; v6.4.0 released 2026-07-19 | `git log`, `gh release list` | `[REPO]` | 2026-08-04 |
| 6 | June–July 2026 shipped v6.0.0 → v6.4.0 (ten releases) | `gh release list` | `[PAGE]` | 2026-08-04 |
| 7 | **Zero** downloadable assets across all 53 releases; no download counter has ever existed | `gh api .../releases --jq '.assets'` | `[PAGE]` | 2026-08-04 |
| 8 | 14-day traffic: 137 clones / 78 uniques; 174 views / 85 uniques | `gh api .../traffic/clones`, `/views` | `[PAGE]` | 2026-08-04 (window to 07-31) |
| 9 | De-spiked baseline **7.2 clones/day, 4.8 unique cloners/day, ~6 unique visitors/day** | diagnostic, computed from row 8 | `[PAGE]` | 2026-08-04 |
| 10 | CI ran **10** checkouts on the spike day (3×3 matrix + `plugin-in-sync`) | `.github/workflows/smoke.yml` | `[REPO]` | 2026-08-04 — **supersedes** my brief's "9" |
| 11 | 78 unique cloners vs 85 unique viewers = **92%**, implausible for humans | rows 1, 8 | `[PAGE]` | 2026-08-04 |
| 12 | Referrers: Google 51 · reddit 32 · github 18 · gist 16 · linkedin 2 | `gh api .../traffic/popular/referrers` | `[PAGE]` | 2026-08-04 |
| 13 | True hook count is **37**; 30 matcher variants | `bin/audio-hooks.py:162-203`; `hooks/hook_runner.py:742-788` | `[REPO]` | 2026-08-04 |
| 14 | Six shipped surfaces state a wrong count (39 ×2 in README, 39 in `llms.txt:30`, 26 in repo description, `marketplace.json:8`, `plugin.json:4`) | diagnostic | `[REPO]` | 2026-08-04 |
| 15 | Every wrong count **was true when written** (26 at v6.1.0, 39 at v6.2.0, 37 after v6.3.4) | `git show <tag>` | `[REPO]` | 2026-08-04 |
| 16 | README:137 says "6 on by default"; actual is **3** | diagnostic | `[REPO]` | 2026-08-04 |
| 17 | 292 passing tests; CI on 3 OSes × 3 Python versions | `tests/`, `smoke.yml` | `[REPO]` | 2026-08-04 |
| 18 | GitGuardian #34199726 was **synthetic** (jwt.io demo token, AWS `AKIAIOSFODNN7EXAMPLE`) | commit `e3e8f4b` | `[REPO]` | 2026-08-04 |
| 19 | Claude Code ships a native statusLine fed pre-computed `context_window.used_percentage`, `remaining_percentage`, `exceeds_200k_tokens`, `rate_limits.five_hour/seven_day.used_percentage`, `resets_at` | code.claude.com/docs/en/statusline | `[PAGE]` | 2026-08-04 |
| 20 | Mobile push fires "when a long-running task finishes or when it needs a decision from you"; **"no per-event configuration"** beyond two toggles | code.claude.com/docs/en/remote-control | `[PAGE]` | 2026-08-04 |
| 21 | Native push unavailable on Bedrock / Google Cloud Agent Platform / Microsoft Foundry / custom `ANTHROPIC_BASE_URL` / API-key auth / ZDR orgs | code.claude.com/docs/en/remote-control | `[PAGE]` | 2026-08-04 |
| 22 | Anthropic documents `preferredNotifChannel: "terminal_bell"`, default desktop notifications in Ghostty/Kitty/iTerm2, and a copy-pasteable `afplay` Notification hook, on a page indexed *"No sound or alert when Claude finishes"* | code.claude.com/docs/en/terminal-config | `[PAGE]` | 2026-08-04 — **corrects** my own earlier claim that no audio path was documented |
| 23 | Anthropic closed issue #1288 "Sound notifications" (44 reactions) as `completed` | competitor sweep | `[PAGE]` | 2026-08-04 |
| 24 | Notification requests drew 69/65/42/40/37 reactions; **sound** requests drew 1/1/0/0 | competitor sweep | `[PAGE]` | 2026-08-04. **"chime: zero issues" REMOVED — FALSE**, a search returns 2 (red team) |
| 24a | All **38** sound-related issues, every state, total ~**68** reactions | red-team full-population check | `[PAGE]` | 2026-08-04 — **strengthens** row 24 from n=4 to the whole population |
| 24b | Issue **#73384**, "built-in distinct notification sounds for 'needs input' vs …", has **zero** reactions | red team | `[PAGE]` | 2026-08-04 — the closest thing to echook's exact pitch on the tracker |
| 24c | Claude Code's `Notification` hook matcher filters on `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`, `agent_completed`; 38 hook events documented | code.claude.com/docs/en/hooks | `[PAGE]` | 2026-08-04 — verified by me directly. **Falsifies the original S1** |
| 25 | `PeonPing/peon-ping`: **4,973★**, 367 forks, MIT, active; five Agent Skills; 21 harness adapters; **7 sound categories** | competitor sweep | `[PAGE]` | 2026-08-04 |
| 26 | `jarrodwatts/claude-hud`: **27,066★** | competitor sweep | `[PAGE]` | 2026-08-04 |
| 27 | `ccstatusline`: 12,205★, **407,682 monthly installs**, 72,918 npm downloads/week; monetizes via Buy Me a Coffee | base rates | `[PAGE]` | 2026-08-04 |
| 28 | `ccusage`: 123,955 npm downloads/week | base rates | `[PAGE]` | 2026-08-04 |
| 29 | `ccstatusline` grew ~25× and `ccusage` ~6× **after** native features shipped | base rates | `[PAGE]` | 2026-08-04 |
| 30 | **2,161** Claude Code statusline repos exist; 18 have more stars than echook's total | competitor sweep | `[PAGE]` | 2026-08-04 |
| 31 | **601,280** `SKILL.md` files on GitHub | prior-art audit | `[PAGE]` | 2026-08-04 |
| ~~32~~ | ~~Anthropic engineering blog: *"Skills are authored for agents rather than humans"*~~ | **CLAIM WITHDRAWN 2026-08-04** | **FAILED** | Red team searched the cited page (143,670 bytes) and the two likeliest alternatives: **zero hits**, while two other quotes from the same citation matched exactly. Deleted, not softened. BC-1 stands on rows 31 and 25 |
| 33 | Claude Code `/statusline` accepts natural-language instructions, generates the script, updates settings | code.claude.com/docs/en/statusline | `[PAGE]` | 2026-08-04 |
| 34 | 63 hook events documented across the three harnesses; `DirectoryAdded` shipped 2026-07-24 | prior-art audit | `[PAGE]` | 2026-08-04 |
| 35 | Nine projects built agent-completion notifications Aug 2025–Feb 2026; seven untouched 6+ months; `Claude-Code-Remote` stopped at 1,275★ / 135 forks | prior-art audit | `[PAGE]` | 2026-08-04 |
| ~~35a~~ | ~~"2,016 stars and 200+ forks" across those nine~~ | **WITHDRAWN** | **FAILED** | The seven enumerated total **1,770**; does not reconstruct, and was presented as checkable in a minute (red team) |
| ~~35b~~ | ~~"Convergent invention is evidence the gap is real"~~ | **WITHDRAWN** | **FAILED** | The source report says *do not assert either direction*; equally consistent with "they found no demand" |
| 36 | Nine competitors pushed more recently than echook's 2026-07-19 | prior-art audit | `[PAGE]` | 2026-08-04 |
| 37 | Claude Code plugin/marketplace schemas contain **no** price, payment or entitlement field | base rates | `[PAGE]` | 2026-08-04 |
| 38 | VS Code `pricing` accepts only `Free`/`Trial`; premium-extensions request open since **2020-02-14** | base rates | `[PAGE]` | 2026-08-04 |
| 39 | No Claude Code plugin/skill/MCP server with disclosed revenue was found | base rates — **a null result**, search paths enumerated in that report | `[PAGE]` | 2026-08-04 |
| 40 | Ref (ref.tools): **$9/mo**, "hundreds of subscribers" — a hosted metered index, not a plugin sale | base rates | `[PAGE]` | 2026-08-04 |
| 41 | 14 of 15 Open Collective ledgers in the 50–99★ band received **$0** | base rates | `[PAGE]` | 2026-08-04 |
| 42 | **93%** of owners of 70–90★ repos have zero public sponsors | base rates | `[PAGE]` | 2026-08-04 |
| 43 | Median npm project that had already opened a donation page collected **$55 over nine months** (ICSE 2020) | base rates | `[PAGE]` | 2026-08-04 |
| 44 | husky: **35,249★**, "used by 1.2M+ projects", estimated annual budget **$410.00** | base rates | `[PAGE]` | 2026-08-04 |
| 45 | ChanMeng666 has a live GitHub Sponsors listing, **222 followers, 0 sponsors** | base rates | `[PAGE]` | 2026-08-04 |
| 46 | Pushover: **$4.99 one-time** licence | base rates | `[PAGE]` | 2026-08-04 |
| 47 | Clutch: custom projects **$10,000–$49,000** | base rates | `[PAGE]` | 2026-08-04 — **CORRECTED** from "$49,999", which had propagated to 11 sites across 6 files. **Also re-graded:** the page describes **agencies**, sample size undisclosed; a solo maintainer sits nearer the band's floor, and no exists-vs-reachable discount was ever applied to this lane (red team). Treat as an **unresearched hypothesis**, not a sized lane |
| 48 | Realistic annual pool **$0–$200**, median $0; three of four archetypes size to $0 | sizing report | derived | 2026-08-04 |
| 49 | Stretch pool $60k–$150k one-time **for the whole ecosystem across all vendors** — never added to row 48 | sizing report | derived | 2026-08-04 |
| 50 | Cursor's in-app "play sound on finish" setting | — no Cursor-official URL; 3 candidate paths 404 | **`[UNVERIFIED]`** | **Do not use in copy until checked** |
| 51 | "People just alt-tab instead" | searched for, **not found** | **`[UNVERIFIED]`** | Do not use |
| 52 | Reddit-sourced sentiment | Reddit was **blocked** to the research agents; no Reddit claim appears anywhere | n/a | Gap, disclosed |

## Spot-check performed

12 rows re-verified directly by me rather than trusted from a report: **1, 2, 3, 4, 5, 7, 8, 10, 12, 19,
20, 22.** All 12 matched, and two of them (rows 2 and 22) **corrected** figures I had asserted earlier in
the engagement. Rows 25–47 are single-sourced from the research reports and were not independently
re-fetched by me — that is the ledger's largest soft spot and it is disclosed here rather than in a
footnote.

## Known soft numbers, labelled at point of use

- Rows 50, 51 — `[UNVERIFIED]`, banned from copy.
- Row 9 — a derived baseline resting on row 11's contamination caveat; it is a *ceiling* on human
  traffic, not an estimate of it.
- Row 48 — a bottom-up sum whose inputs include archetypes with zero observed buyers. It is a reasoned
  figure, not a measured one, and no interview supports it.
