# echook — Product Reality Check

**Date:** 2026-08-04 · **Subject:** `ChanMeng666/echook` (`D:\github_repository\claude-code-audio-hooks`)
**Repo state audited:** HEAD `c095e28` = tag `v6.4.0` (nothing unreleased on `master`; zero commits in 16 days)
**Method:** hostile-outsider read. Every internal claim carries a `path:line`. External claims carry a URL fetched this session.
**Constraint honoured:** nothing in the echook repo was modified. All git operations were read-only.

---

## Executive summary — the pattern

**The quality of this project runs backwards from the order a stranger reads it.**

Everything a machine checks is correct. Everything a human maintains by hand is a fossil.

- `scripts/bump-version.sh:8-16` rewrites **exactly 8 version locations** — and all 8 are right.
- `.github/workflows/smoke.yml` runs 3 OS × 3 Python + a plugin-sync job — 90.2% pass rate over 51 runs.
- 292 tests pass (`python -m unittest discover tests` → `Ran 292 tests … OK`).
- `_build_manifest()` (`bin/audio-hooks.py:2824`) derives its hook list from the live `HOOK_CATALOG`, so `audio-hooks manifest` **cannot** lie about the event count.

And then:

- `README.md:11` — the first line under the title — says **v6.2.0** and **39 hook events**. Both wrong.
- `README.md:137` — the feature table — says **37 hook events** and **6 on by default**. One right, one wrong (it is 3).
- `.claude-plugin/marketplace.json:8` — the text shown in the plugin marketplace — says **26 hooks**.
- The GitHub repo description — the text **Google indexes**, and Google is the #1 referrer — says **26 hooks**.

Four surfaces, three different values, for the single headline feature.

The damning part is not that they are wrong. It is that **every one of them was true once**. I verified the provenance directly:

```
v6.1.0: 26 events   v6.2.0: 39 events   v6.3.3: 39 events   v6.3.4: 37 events   v6.4.0: 37 events
```
(`git show <tag>:bin/audio-hooks.py`, counting `HOOK_CATALOG` entries)

`v6.3.4` (`85bfd6a`) deleted `worktree_create` and `worktree_remove` to stop hijacking Claude Code's provider hook. 39 → 37. The README's "26 → 39 total" at `README.md:68` was **accurate the day it was written**. Nobody went back.

So the README is not a document containing errors. It is a **stratigraphy** — a readable cross-section of v6.1, v6.2 and v6.4 deposited in layers, with the newest facts only where the author happened to touch that paragraph. The same is true of `docs/ARCHITECTURE.md`, which describes `bin/audio-hooks.py` as *"~1100 lines, 27 subcommands"* (`docs/ARCHITECTURE.md:165`) — the file is 3,103 lines with 39 declared subcommands.

**What the outsider concludes in 90 seconds:** *"This person ships faster than they can describe what they shipped. I cannot use any number on this page. And if the numbers are stale, what else is?"*

That last sentence is the real cost, and it lands on the **one genuinely differentiated asset the project has**. The agent-operable surface is real and above average — a single JSON CLI, machine-readable error codes with a runnable `suggested_command`, a self-describing manifest, a 508-line SKILL that documents its own failure modes. But an outsider who has just caught three contradictory hook counts in the first 140 lines will not extend credit to *"AI-operated, not AI-assisted."* **The drift taxes the asset.** The best-maintained artifact in the repo (the manifest) is invisible until after the reader has already decided, based on the worst-maintained one.

Two structural consequences follow, and both are worse than any individual finding:

1. **This will recur at v6.5.0.** `bump-version.sh` covers 8 machine files and zero prose strings. Fixing the "39" today changes nothing about the mechanism that produced it. The pattern is self-reproducing.
2. **The author cannot tell whether any of it matters.** There is **no install telemetry of any kind** (§5). Zero release assets across all 53 releases means no download counter has ever existed. So "did the stale README cost installs?" is not a hard question — it is an *unanswerable* one, along with every other funnel question.

---

## Top 12 must-fix, ranked by narrative damage

Ranked by what an outsider concludes, not by engineering effort. "Blocks-outsider-reading" = does this stop a senior engineer before they reach the good part?

### 1. The GitHub repo description says "26 hooks" — 30% understated, and it is the Google snippet
**Evidence:** `gh api repos/ChanMeng666/echook` → `description` contains `26 hooks`. Ground truth: `bin/audio-hooks.py:162-203`, 37 entries. Also duplicated at `.claude-plugin/marketplace.json:8` and `plugins/audio-hooks/.claude-plugin/plugin.json:4` — both of which carry a correct `"version": "6.4.0"` on the *adjacent line* (`:9` and `:3`), because `bump-version.sh` rewrites the version field and never the description beside it.
**Why this ranks first:** Google is the **#1 referrer — 51 visits / 27 uniques in 14 days** (`traffic/popular/referrers`), ahead of reddit (32/9). The repo description *is* the search snippet and the marketplace listing. This is the only finding that costs the author reach **before anyone clicks**, and it undersells the product by 11 events.
**Outsider concludes:** *"Either they don't know what they built, or they haven't looked at their own listing in three releases."*
**Fix:** Edit the description in GitHub settings; sed two JSON files. **2 minutes.** **Blocks reading: yes (pre-click).**

### 2. `README.md:11` — subtitle frozen at v6.2.0 / 39 events
**Evidence:** `README.md:11` — `**v6.2.0** — 39 hook events across all three editors…`. Repo is v6.4.0 (`bin/audio-hooks.py:159`, `git tag`, `CHANGELOG.md:12`). `README.md:68` — `**Latest: v6.2.0 …** 13 new lifecycle events (26 → 39 total)` — the "What's New" section is 2 minors + 4 patches behind and **omits v6.3.4 entirely**, which is the emergency rollback of a bug that broke git-worktree isolation for every user.
**Outsider concludes:** *"The 'Latest' section doesn't mention the release that fixed the thing that broke my worktrees. What else did I not get told?"*
**Fix:** Rewrite 2 lines. **10 minutes.** **Blocks reading: yes.**

### 3. Three hook counts on one page for the headline feature
**Evidence:** `README.md:11` = **39** · `README.md:68` = **39** ("26 → 39 total") · `README.md:137` = **37** · `README.md:143` = **37** · `README.md:199` = **37** · `llms.txt:30` = **39** ("complete 39-event hook surface") · `AGENTS.md:25` = **37**. True value **37**.
**Note the compounding failure:** `llms.txt` is the file the README designates as an agent's source of truth (`README.md:45`). It hands agents the pre-rollback count.
**Outsider concludes:** *"They can't count their own features. This is the number in the title."*
**Fix:** Three edits. **10 minutes.** **Blocks reading: yes.**

### 4. "6 on by default" is 3 — and 3 rows of the events table promise sounds that ship silent
**Evidence:** `README.md:137` says *"6 on by default"*. Ground truth: `config/default_preferences.json` has 74 `enabled_hooks` keys, **exactly 3 true** (`notification`, `stop`, `permission_request`), matching `HOOK_CATALOG` (`bin/audio-hooks.py:163,164,166`) and `AGENTS.md:38`. The events table marks three more as **on** that ship **off**: `README.md:150` `subagent_stop`, `:152` `permission_denied`, `:153` `task_created`.
**Provenance (this is the interesting part):** those three are exactly the v5.1.4 default set. v5.1.4 flipped them true; **v5.1.5 reverted it the same day** (`docs/TROUBLESHOOTING.md:126`; tags `v5.1.5` and `v5.1.4` both dated 2026-05-01). The README's table and its "6" were never reverted. A fossil comment survives in the code too: `hooks/hook_runner.py` still reads `# Default enabled hooks (v5.0 adds permission_denied + task_created)` directly above `default_enabled = {"notification", "stop", "permission_request"}` — a comment contradicting the line beneath it. `docs/ARCHITECTURE.md:145` documents the reverted behaviour as current.
**Why this ranks above the others:** it is the only doc bug a **user** hits rather than a reader. They read the table, install, and half the promised sounds never fire. That reads as a broken product, not a stale doc.
**Outsider concludes:** *"I'd have filed a bug against this and been wrong. The docs would have wasted my afternoon."*
**Fix:** Correct 4 cells. **10 minutes.** **Blocks reading: yes** — a careful reader diffs the table against `config/`.

### 5. "Python 3.6+ is the only runtime requirement" is false, and the installer enforces the false number
**Evidence:** `README.md:313`. True floor is **3.7**, and it is a hard `SyntaxError` at import, not a graceful degradation: `hooks/user_preferences.py:12` — `from __future__ import annotations` (PEP 563, added 3.7.0). `hooks/hook_runner.py:39` imports that module at top level, so **every hook fire dies at import on 3.6**. 24 of 26 `.py` files carry the same future import. Secondary 3.7 blockers: `subprocess.run(capture_output=…, text=…)` at `bin/audio-hooks.py:1449, 1910, 2610, 2675, 2683, 2693` and `hooks/hook_runner.py:1221-1231, 1272-1275`.
**The aggravating detail:** `scripts/install-complete.sh:136-142` — `# Verify minimum version (3.6+)` … `if [[ "$major" -ge 3 ]] && [[ "$minor" -ge 6 ]]` — **actively accepts 3.6 and installs a build that cannot import.** And `hooks/hook_runner.py:2328-2330` contains a `sys.version_info < (3, 6)` guard that is both wrong *and* unreachable, sitting ~2,290 lines after the import that already crashed.
**CI proves nothing here:** `.github/workflows/smoke.yml:14` — `python-version: ["3.9", "3.12", "3.13"]`. 3.6, 3.7 and 3.8 are never exercised. The claim is repeated at `docs/INSTALLATION_GUIDE.md:151` and `docs/TROUBLESHOOTING.md:144`.
**Outsider concludes:** *"A 30-second grep falsifies a compatibility claim they repeat in three places. They are guessing about their own runtime."* This is the finding a senior engineer will personally verify, because it is trivially checkable and it is exactly the kind of claim people get wrong.
**Fix:** Change 3 docs to `3.9+` (match CI) and fix the installer gate. **15 minutes.** **Blocks reading: yes.**

### 6. `homepageUrl` is a raw video attachment — the highest-value free field, wasted
**Evidence:** `gh api repos/ChanMeng666/echook` → `homepage: "https://github.com/user-attachments/assets/f57249be-a524-4e6f-8225-6b9500f1aea4"`. That is an uploaded asset blob, not a site. GitHub renders it as the "Website" link in the sidebar and in social cards.
**Outsider concludes:** Nothing consciously — which is the point. It is a silently forfeited slot on the highest-attention surface the project owns.
**Fix:** Point it at the releases page, the installation guide, or `chanmeng.org`. **1 minute.** **Blocks reading: no.**

### 7. A documented remedy that silently does one-third of what it says
**Evidence:** `docs/TROUBLESHOOTING.md:129` prescribes the fix for the v5.1.4 noise regression as `audio-hooks hooks disable subagent_stop permission_denied task_created`. `cmd_hooks` in `bin/audio-hooks.py` does `name = rest[0]` and discards the rest. **It disables one hook and returns `ok: true`.** `docs/CLI_REFERENCE.md:21` and the manifest (`bin/audio-hooks.py:2849`) both correctly declare `<name>` singular — so the docs contradict each other *and* the code.
**Outsider concludes:** *"Their troubleshooting guide fails silently and reports success. That's the worst failure mode there is."*
**Fix:** Loop over `rest`, or correct the doc. **20 minutes.** **Blocks reading: no** (deep), but severe when found.

### 8. `logs tail --invoker` is called "the canonical filter" and does not exist
**Evidence:** `docs/ARCHITECTURE.md:348` — *"`audio-hooks logs tail --invoker cursor` is the canonical filter"*. `cmd_logs` parses only `--n` and `--level`; any other token falls through and is **silently ignored**. The agent receives an unfiltered log and no error. Same class as #7: documented, silently wrong, reports success.
**Outsider concludes:** *"The architecture doc describes a program that doesn't exist."*
**Fix:** Implement the flag or delete the sentence. **20 minutes.** **Blocks reading: no.**

### 9. "The only thing a human ever types by hand is one `/reload-plugins`" — contradicted by the tool's own output
**Evidence:** `README.md:45`, restated more strongly at `docs/INSTALLATION_GUIDE.md:5` (*"no human-only steps"*). But `bin/audio-hooks.py:1424-1434` — `install --plugin` **installs nothing**; it prints an instruction sheet:
```python
"next_steps": [
    "Run inside Claude Code: /plugin marketplace add ChanMeng666/echook",
    "Run inside Claude Code: /plugin install audio-hooks@chanmeng-audio-hooks",
    "Verify: audio-hooks status",
],
"hint": "Plugin installation is performed by Claude Code itself; this command only documents the steps.",
```
That is **two** human-typed slash commands on the flagship path. Uninstall is a third (`bin/audio-hooks.py:1897`). Of seven real install paths, five require an **editor restart** the README never mentions (`docs/INSTALLATION_GUIDE.md:61` "restart Cursor", `:103` "restart Codex", `scripts/install-complete.sh:715`, `scripts/install-windows.ps1:495`), and the Cursor bridge additionally needs a GUI toggle (`docs/INSTALLATION_GUIDE.md:47` — "Enable Cursor Settings → 'Third-party skills'").
**Outsider concludes:** *"The single sentence that states the product's whole thesis is disproved by the product's own stdout."*
**Fix:** *"On Claude Code the human types `/reload-plugins` at install and `/plugin uninstall` at removal; every other path costs one editor restart, which no agent can perform for you."* **15 minutes.** **Blocks reading: yes** — this is the differentiating claim.

### 10. A third party's real email address republished as a test fixture
**Evidence:** `ai@gavigo.com` in four tracked locations, introduced by `ba5fc4b` (v5.1.4, 2026-05-01): `CHANGELOG.md:358` (*"reported in chat by ai@gavigo.com"*), and `tests/test_cursor_bridge.py:388, 405, 407` as a literal `"user_email"` fixture. The correct pattern is already in use **52 lines earlier** in the same file: `tests/test_cursor_bridge.py:336` — `"user_email": "test@example.com",  # must be redacted`.
**Outsider concludes:** *"They put a stranger's email in a test fixture and shipped it. Small thing — but it's a judgement signal, and I'm evaluating judgement."* Note the irony: the file is the **redaction** test suite.
**Fix:** Swap 3 occurrences to `test@example.com`; credit the reporter by handle in the CHANGELOG. **5 minutes.** **Blocks reading: no.**

### 11. Two documented error codes are unreachable; the most-emitted code is undocumented
**Evidence:** `TTS_FAILED` (`hooks/hook_runner.py:85`, hinted at `:131-134`, published to users at `docs/CLI_REFERENCE.md:104`) is **never emitted anywhere** — exhaustive grep finds only the declaration and the hint table. Same for `WEBHOOK_TIMEOUT` (`docs/CLI_REFERENCE.md:101`) and `SELF_UPDATE_FAILED`. Conversely `INVALID_USAGE` is emitted at **24 sites** in `bin/audio-hooks.py` and appears in zero documentation. Eleven CLI-emitted codes are absent from the manifest, because `_build_manifest` sources `error_codes` from `dir(HR.ErrorCode)` alone (`bin/audio-hooks.py:2826-2836`) — which makes `docs/CLI_REFERENCE.md:111`'s promise (*"See `audio-hooks manifest` → `error_codes` for the complete, live list including Cursor/Codex-specific codes"*) false: `CURSOR_NOT_FOUND` and `DUPLICATE_BRIDGE` are precisely the Cursor-specific codes, and the manifest can never print them.
**Outsider concludes:** *"The error catalogue describes the design, not the build. So when TTS goes silent on my Linux box, nothing tells me why."* — and that is literally true: `hooks/hook_runner.py:1851-1852` logs the no-engine case at `debug` level, which is suppressed unless `CLAUDE_HOOKS_DEBUG=1`.
**Fix:** Emit the codes or delete them; widen the manifest's source. **1 hour.** **Blocks reading: no.**

### 12. "Fire-and-forget… fully detached" — no detach primitive exists in the repository
**Evidence:** `hooks/hook_runner.py:1990-1992` — *"Survives main process exit because the child is fully detached."* Grep for `start_new_session`, `setsid`, `DETACHED_PROCESS`, `CREATE_NEW_PROCESS_GROUP`, `preexec_fn`, `threading`, `daemon=True` across `hooks/` and `bin/`: **zero hits**. Windows spawns use `CREATE_NO_WINDOW` only, which hides a console — it does not detach.
**Where the claim actually breaks:** the WSL audio path runs **three timeout-less blocking calls plus a cross-filesystem copy on the hook hot path** — `hooks/hook_runner.py:1221` (`subprocess.check_output(["wslvar","TEMP"], text=True)`), `:1228`, `:1272`, and `:1267` `shutil.copy` of the MP3 across the `/mnt` 9p mount **on every fire**. `check_output` waits by definition and none passes `timeout=`. The discipline exists elsewhere in the same codebase — `bin/audio-hooks-statusline.py:175-180` uses `subprocess.run(…, timeout=3)` — it just isn't applied on the hot path. Also: Claude Code hooks get `"async": true` (`plugins/audio-hooks/hooks/hooks.json`), but `cursor-hooks/hooks.json` and `codex-hooks/hooks.json` have **no `async` at all** — so on Cursor/Codex the editor waits, bounded only by its own 10 s timeout. Cursor-in-WSL runs the unbounded sequence inside that budget.
**Outsider concludes:** *"The non-blocking guarantee is delivered by the editor's config flag, not by their code, and the comment asserting otherwise is false. On WSL it's just not true."*
**Fix:** Add `timeout=` to the three WSL calls; correct the comment; add `async` to the Cursor/Codex templates. **1 hour.** **Blocks reading: no.**

---

## Cheap fixes that materially improve the story inside a week

Ordered by narrative-improvement-per-hour. **The top six total under 45 minutes**, and they change the first-90-seconds impression completely. That is the encouraging half of this report and it is worth saying plainly: this project's presentation problem is unusually cheap to fix, because the underlying artifact is sound.

| # | Fix | Time | What it buys |
|---|---|---|---|
| 1 | Repo **description** → 37 hooks + current framing; **homepage** → a real URL | **3 min** | Fixes the Google snippet (#1 referrer, 51 visits) and the marketplace listing. The only fix that works *before* the click. |
| 2 | `README.md:11` + `:68` → v6.4.0 / 37 events; mention v6.3.4 | **10 min** | The first two lines a human reads stop being wrong. |
| 3 | `marketplace.json:8` + `plugin.json:4` "26 hooks" → 37 | **5 min** | The plugin-marketplace listing text. |
| 4 | `README.md:137` "6 on by default" → 3; fix the 3 wrong `on` cells at `:150/:152/:153` | **10 min** | Stops shipping a first-run expectation failure. |
| 5 | `README.md:313` + `INSTALLATION_GUIDE.md:151` + `TROUBLESHOOTING.md:144` → Python **3.9+**; fix `install-complete.sh:136-142` | **15 min** | Removes the claim a senior engineer will personally falsify. |
| 6 | `tests/test_cursor_bridge.py:388,405,407` → `test@example.com`; CHANGELOG credit by handle | **5 min** | Removes the only genuine privacy blemish. |
| | **— subtotal —** | **~48 min** | |
| 7 | **Attach a release asset** (a `.tar.gz` of the plugin) to v6.4.0 and every future release | **10 min + 1 min/release** | **Creates the only public adoption counter that exists.** See §5. Today there are zero assets across all 53 releases, so the number is unmeasurable *by construction*. |
| 8 | Rewrite `README.md:45` to the honest form (see finding #9) | **15 min** | Converts the thesis sentence from falsifiable to defensible. |
| 9 | Scheduled Action: append `traffic/clones` + `views` + `referrers` to a CSV in-repo, daily | **30 min** | GitHub's traffic API is a **rolling 14-day window it never backfills**. Every day this isn't running, history is destroyed permanently. Cheapest possible instrument. |
| 10 | **A `docs-drift` job in `smoke.yml`**: `audio-hooks manifest` → assert the hook count and version appear in `README.md`, `llms.txt`, both plugin manifests | **2 h** | **The only fix that stops the pattern recurring.** Everything above is a one-time cleanup; this is the mechanism. The project already has the two halves — a machine-readable manifest and a working CI — they've just never been connected. |
| 11 | One-paragraph public notes on the four *good* decisions currently invisible (see §7) | **1 h** | Turns four things that look like risks into evidence of judgement. |

**If only three things get done: #1, #2, #4.** Twenty-three minutes, and the first screen a stranger sees stops contradicting itself.

---

## Evidence machinery — reporting zeros as zeros

### Is there ANY install or usage telemetry? **No. None. Verified exhaustively.**

| Possible counter | Exists? | Verified by |
|---|---|---|
| GitHub release-asset downloads | **NO** | `gh api repos/ChanMeng666/echook/releases --paginate` → **53 releases, `assets: 0` on every one**. GitHub counts downloads only for uploaded assets; auto-generated source tarballs are counted nowhere. |
| PyPI | **NO** | `https://pypi.org/pypi/echook/json` → **404**; `audio-hooks` → 404; `claude-code-audio-hooks` → 404 [PAGE] |
| npm | **NO** | `https://registry.npmjs.org/echook` → **404**. (`audio-hooks` on npm returns 200 but is `hey-lee/audio-hooks`, an unrelated React library — do not cite it.) [PAGE] |
| Claude Code plugin installs | **NO** | Distribution is `.claude-plugin/marketplace.json` pulling straight from this GitHub repo. Anthropic publishes no per-plugin install metric. |
| In-product telemetry | **NO** | Exhaustive grep for `urlopen`, `urllib`, `requests`, `http.client`, `socket`, `curl`, `Invoke-WebRequest` across `hooks/`, `bin/`, `scripts/` yields **three** egress sites: `hooks/hook_runner.py:2001` (the user's own webhook, default `enabled: false`), `bin/audio-hooks.py:1083` (`webhook test`, user-invoked), and `scripts/generate-audio.py:59` (a maintainer build tool). **No analytics, no crash reporting, no update check.** |
| GitHub clones | **Partial, and contaminated** | 14-day rolling window only, maintainer-visible only, never backfilled, and inflated by CI (§below). |

**What follows, stated plainly.** The author cannot answer *"how many people use this?"* — not approximately, not within an order of magnitude. Nor: how many installs survive a week · which of the 37 events anyone enables · whether TTS, webhooks or the status line are used at all · whether the natural-language control loop (the differentiating feature) is ever exercised · whether the June–July shipping sprint helped or hurt · whether the "6 on by default" doc bug is costing installs.

Consequently **no decision gate of the form "if X users, then Y" can ever be evaluated.** Any roadmap containing one is decorative. This is the single highest-leverage gap in the whole diagnostic, and it is roughly a day of work.

### The local NDJSON log — confirmed, and it already contains most of the answer

`hooks/hook_runner.py:70-73`:
```python
LOG_SCHEMA = "audio-hooks.v1"
LOG_FILE_NAME = "events.ndjson"
LOG_ROTATE_BYTES = 5 * 1024 * 1024   # 5 MB
LOG_KEEP_FILES = 3
```
Written synchronously per hook fire via `log_event()` (`:279-307`); rotation shifts `.2→.3, .1→.2, base→.1` (`:201-209`), capping disk at ~20 MB; `debug` events dropped unless `CLAUDE_HOOKS_DEBUG=1` (`:284-285`). Read only by `bin/audio-hooks.py:1356` (`logs tail`). **Never transmitted anywhere.**

So the instrument is already built and already recording the right events — it just has no return path. That is a much better starting position than "no telemetry" usually implies.

### The 4–5 events that would answer "does anyone actually use this, and keep using it?"

Minimum viable payload on each: a locally-generated random `install_id` (never derived from anything identifying), `version`, `os`, `editor`.

| Event | Fields | The question it answers |
|---|---|---|
| **1. `install_completed`** | `install_id, version, editor, install_mode, os, python_version` | *How many installs?* — the activation number that does not exist today. `python_version` also settles finding #5 empirically. |
| **2. `daily_active`** | `install_id, version, editor, hooks_fired_count, distinct_hooks_fired` — one row per install per UTC day | **The only one that really matters.** D1 / D7 / D30 retention. An audio notifier that people mute is indistinguishable from one they love, without this. |
| **3. `config_mutated`** | `install_id, key, direction (enable\|disable)` | *Is the natural-language control loop used at all?* This is the differentiating claim of the whole product and there is currently zero evidence anyone touches it. Also reveals which of the 37 events people actually want on — which would have caught the "6 vs 3" question from the demand side. |
| **4. `silenced`** | `install_id, kind (snooze\|disable\|uninstall), scope, days_since_install` | Churn, and specifically *the noise hypothesis*. Distinguishes silent abandonment from "installed, too loud, muted forever" — two situations with opposite fixes. |
| **5. `error_emitted`** | `install_id, error_code, os, editor, version` | Would have surfaced issue #10 (`NameError: Tuple` — **every command broken on v5.0.3 and v5.1.0**) within hours instead of waiting for a stranger to file it. Six days elapsed between v5.0.3 and that report. |

Events 2–5 are already being written to `events.ndjson`. The work is a rollup and a send.

### Norms and backlash risk — and the option that carries none

Opt-out telemetry is the industry default for developer tools, but it is the *high-variance* choice:

- **Homebrew** is opt-out: *"Homebrew displays a notice before analytics are enabled so a user can opt out before sending an event."* Disable via `brew analytics off` or `HOMEBREW_NO_ANALYTICS=1`. It collects no user identifier and no IP. — https://docs.brew.sh/Analytics [PAGE]
- **Next.js** is opt-out, with an unusually clear negative list: *"We **do not** collect any metrics which may contain sensitive data. This includes, but is not limited to: environment variables, file paths, contents of files, logs, or serialized JavaScript errors."* Disable via `npx next telemetry disable` or `NEXT_TELEMETRY_DISABLED=1`. — https://nextjs.org/telemetry [PAGE]

Both survived their launches by pairing opt-out with (a) a prominent first-run notice, (b) one documented env var, and (c) an explicit list of what is *not* collected. Both nevertheless took real reputational damage at introduction.

**For echook specifically, opt-out is the wrong trade.** The project currently has a genuinely clean privacy story — verified above: nothing leaves the machine, ever, except a webhook the user configured. That is a real asset for a tool that sits inside the user's coding session and can see `last_assistant_message` and `tool_input`. Spending it for a metric would be a bad exchange at 78 stars.

**Recommended, in ascending order of ask:**

1. **`audio-hooks stats` (zero risk, ~2 hours).** Roll up the existing NDJSON locally and print an anonymized, copy-pasteable summary. Ask for it in the issue template and in `SUPPORT.md`. Costs nothing, breaks no promise, and turns every support conversation into a data point.
2. **Release assets (zero risk, 10 minutes).** The only free public counter that exists. Start now; it is not retroactive.
3. **Opt-in telemetry with a first-run prompt (low risk, ~1 day).** Ship the five events above behind an explicit yes. Expect a low opt-in rate — but a low rate on a real number beats a perfect rate on a number that does not exist, and it preserves the privacy story intact. Publish the negative list Next.js-style.

### Customer conversations — 8 issues, 3 external PRs, 7 forks, 0 discussions

**Issues: 8 ever, all 8 filed by external users, 7 unique reporters, zero labels, 1 open.**

| Class | Count |
|---|---|
| Bug reports | 5 (#1, #4, #5, #10, #14) |
| Feature requests | 2 (#6, #7) |
| Praise | 1 (#3 — "Good job!", the only open issue) |
| Spam | 0 |

**The response record is the strongest signal in the entire dataset, and it is completely invisible.** Median first-response latency **~2.5 hours**; slowest was 7 days. **Every actionable issue was fixed and shipped in a tagged release, usually the same day.** #1 → v3.3.3 in 25 minutes. #10 (critical) → v5.1.1 in ~1 hour, *plus* the maintainer created `.github/workflows/smoke.yml` specifically to prevent recurrence. #14 → v5.1.2 with a before/after millisecond table. Replies are long, technical, credit the reporter by name, and explain rejected alternatives.

The one blemish: **issue #3 is the only open issue and has never received a maintainer reply** in 585 days, despite three strangers piling on with praise (each of which the maintainer heart-reacted to). So the single thing an outside visitor sees in the issue tracker is an unanswered thread. It is praise, so nothing is broken — but it reads as an abandoned tracker.

**Discussions: enabled, `totalCount: 0`.** Zero threads in nine months (`gh api graphql` on `discussions`). **Watchers: 1** — the maintainer. echook has users and effectively no community.

**"3 external PRs, none merged" — this is TRUE and substantively FALSE, and the correction matters.** I fetched the closing actor on each:

- **PR #2** (`PaddyPatPat`, +57/−3) — closed **by the maintainer** 15 minutes after opening, with a long comment explaining he'd already cut v3.3.2 that day and was integrating the fix directly into **v3.3.3** rather than merging onto a stale base. He enumerated the attribution: code applied to `scripts/install-complete.sh`, CHANGELOG credit, **commit co-authorship**, release-notes highlight. Tone effusive, explicitly invited more contributions. **This contributor's work shipped. Counting it as a rejection is simply wrong.**
- **PR #8** (`roganhope`, +42/−0) — **closed by roganhope himself after 3 minutes 29 seconds.** Zero maintainer comments, zero reviews. Superseded by his own PR #9.
- **PR #9** (`roganhope`, +50/−2) — **closed by roganhope himself after 24 minutes 49 seconds.** The only comment is his own, 2 minutes after opening: *"Thank you!! I hope this is proper etiquette. I have never had the need to (try) to contribute to an open source project."* The maintainer never saw it. Context: the maintainer had shipped the same feature in v4.4.0 ~16 hours earlier, so the contributor likely discovered mid-flight he'd been scooped.

**There is not one instance of an external PR being ignored, sat on, or rejected without explanation.** The honest phrasing: *zero external PRs were merged via the merge button; one external contribution shipped in a release with co-authorship; two were withdrawn by their own author within half an hour.*

**But one fair criticism survives, and it is worth naming.** Hand-integrating instead of merging means GitHub's contributor graph shows **no external commits**, `PaddyPatPat`'s contribution is invisible in the UI, and the project *looks* single-author-closed to anyone scanning it. That perception cost is self-inflicted and avoidable — merge the PR, then fix forward.

**Forks: `forks_count` = 7, but the enumerable list returns 9.** Six of the nine pushed after forking — two-thirds of forkers actually modified the code, which is a healthier engagement rate than the raw count suggests. Six still carry the pre-rebrand name.

---

## Metrics decomposition

### Stars — briefing arithmetic corrected

`gh api repos/ChanMeng666/echook/stargazers --paginate -H "Accept: application/vnd.github.star+json"`, bucketed by `starred_at`:

| Month | Actual | Briefing | | Releases that month |
|---|---|---|---|---|
| 2025-11 | 7 | 7 | ✅ | 14 |
| 2025-12 | 4 | 4 | ✅ | 1 |
| 2026-01 | 2 | 2 | ✅ | 0 |
| 2026-02 | 9 | 9 | ✅ | 12 |
| 2026-03 | **10** | 11 | ❌ **off by one** | 6 |
| 2026-04 | 19 ← peak | 19 | ✅ | 8 |
| 2026-05 | 12 | 12 | ✅ | 3 |
| 2026-06 | 9 | 9 | ✅ | 9 |
| 2026-07 | 4 | 4 | ✅ | 2 |
| 2026-08 (4 days) | 2 | 2 | ✅ | 0 |
| **Total** | **78** | 79 | ❌ **off by one** | 55 tags |

78 is triple-confirmed (`wc -l` on the paginated list, the `stargazers_count` field, and the bucket sum).

### "Shipped hardest, acquired fewest" — the honest interpretation

The briefing's framing is directionally right but the mechanism is not the one it implies. **Shipping volume does not predict star acquisition at all** — November shipped 14 releases for 7 stars; May shipped 3 for 12. Across nine months the correlation is essentially zero. So "shipping hardest caused the decline" is not supported.

What *does* track is **external contact**:

- Issues were filed in Nov (1), Feb (3), Mar (1), Apr (2) — and **none since 2026-04-20**.
- Stars: Nov 7 · Feb 9 · Mar 10 · **Apr 19 (peak)** · then monotonic decay: May 12 → Jun 9 → Jul 4 → Aug 2.

**Stars peaked in the last month a stranger talked to the project, and have fallen every month since — through the heaviest shipping period in its history.** June–July produced ten releases (v5.3.0 → v6.4.0) and thirteen stars. April produced eight releases and nineteen.

The causal direction is unproven and cannot be proven without §5's instruments. But the practical conclusion is unambiguous and does not depend on causality: **shipping is not a distribution channel for this project.** Ten releases in eight weeks bought 13 stars, and the last 16 days have produced zero commits and zero stars-per-day improvement. Whatever grew this repo in Feb–Apr, more code was not it.

A second reading worth holding alongside it: v6.x is *maturation* work — per-variant toggles, matcher completeness, a status line, a worktree-hijack rollback. Real engineering, invisible from outside. The pattern in the executive summary is the compounding factor: the one surface that could have communicated ten releases' worth of progress — the README — still describes v6.2.0.

### Traffic — the de-spiked, de-CI'd baseline

14-day window 2026-07-18 → 2026-07-31 (`gh api .../traffic/clones`, `.../traffic/views`; both returned 200 — push access confirmed, no 403).

**Clones: 137 total / 78 uniques.** Daily counts: `17, 44, 13, 6, 6, 7, 4, 3, 5, 2, 6, 5, 7, 12`.

**CI contamination, corrected:** the briefing says `3 OS × 3 Python = 9 checkouts`. **It is 10** — the matrix produces 9 `import-smoke` jobs *plus* a standalone `plugin-in-sync` job. Verified against run `29689965777`: `total_count: 10`, all success. Exactly one workflow run occurred on 2026-07-19, and **none since**, so CI contributes **10 clones to the window, all on the spike day**.

| Baseline | Clones/day | Unique cloners/day | Basis |
|---|---|---|---|
| Raw (as GitHub reports) | **9.8** | **5.6** | 137/14, 78/14 |
| De-CI'd only | 9.1 | — | (137−10)/14 |
| **De-spiked (drop release day) — the honest headline** | **7.2** | **4.8** | 93/13, 63/13 |
| Last 7 days (steady state) | **5.7** | **3.9** | 40/7, 27/7 |

**Views: 174 total / 85 uniques.** Daily: `19, 4, 12, 10, 6, 9, 33, 11, 10, 12, 14, 15, 13, 6`. Views are *not* CI-contaminated (Actions doesn't render pages). One spike on 2026-07-24 (33 views / 8 uniques — one person refreshing, or a crawler). De-spiked: **10.8 views/day, 5.9 unique visitors/day** — barely different from raw, so this baseline is robust.

**Honest headline: ~6 unique visitors and ~5 unique cloners per day. Call it 7 clones/day and 6 visitors/day.**

**A caveat that undercuts even that.** Unique cloners (78) ≈ unique viewers (85) — a 92% clone-per-viewer ratio. For a repo where **64% of views never leave the front page** (`/ChanMeng666/echook` = 112 of 174 views, 72 of the uniques), a near-1:1 clone-to-visitor ratio is not credible for humans. Mirrors, scrapers, AI crawlers and package bots clone without ever rendering a page. **So the single quantitative signal the author has is measuring machines to an unknown but probably large degree.** This is the strongest possible argument for §5: the one instrument that exists is uninterpretable.

**What this baseline CAN support:**
- Order-of-magnitude sizing: this is a **tens-of-users** project, not hundreds. Any plan assuming otherwise is unfounded.
- Relative comparison going forward, *if* daily snapshots start today (the API window is 14 days and is never backfilled).
- The funnel shape: **~6 visitors/day → 5 unique visitors opened `INSTALLATION_GUIDE.md` in 14 days** (0.36/day). Whatever is failing, it is failing at or before the README.

**What it CANNOT support:** any statement about installs, active users, retention, or growth rate. Clones are not installs; they are not even reliably humans.

### Referrers (14 days)

| Source | Visits | Uniques |
|---|---|---|
| **Google** | **51** | 27 |
| reddit.com | 32 | 9 |
| github.com | 18 | 10 |
| **gist.github.com** | **16** | 9 |
| linkedin.com | 2 | 2 |

**Google is the #1 source.** That single fact promotes finding #1 to the top of the list: the repo description is the search snippet, and it says "26 hooks."

**The gist lead: real, but I could not identify the source.** Reported plainly, per the sourcing rules. Attempted and failed: the maintainer's own gists (`gh api users/ChanMeng666/gists` → **exactly one**, "👋 Chan Meng", `about-me.md`, no echook mention) · `gist.github.com/search?q=echook` (fuzzy stem matches, no real hits) · `?q=claude-code-audio-hooks` (zero occurrences) · `?q=audio-hooks` (choco-bot spam) · ten candidate gists from `?q=claude+code+audio`, each fetched and grepped (hits=0) · `gh api search/code` (GitHub code search does not index gists) · DuckDuckGo `site:gist.github.com echook` (0 results). **Two structural reasons this may be permanently unresolvable:** secret gists are unlisted and unindexed but still send a `gist.github.com` referrer when clicked; and GitHub's gist search is notoriously partial. **Status: [UNVERIFIED] — referrer confirmed real, source gist unidentified.**

One adjacent find worth flagging: **`barikpegankabari-max/acousti-notify`**, a repo whose entire description reads *"Best AI Audio Notification Hooks 2026 - Install echook for Claude Code & Cursor IDE"* — SEO/affiliate-style scaffolding around echook's name, by an unrelated account. It may share an origin with the gist referrals. [SNIPPET — description verbatim from `search/repositories`; contents not audited.]

---

## Full findings table

**H** = an outsider changes their mind about the person · **M** = costs credibility in the room · **L** = a nit that accumulates.

| # | Finding | Sev | Verified in | What the outsider concludes | Fix | Blocks reading |
|---|---|---|---|---|---|---|
| 1 | Repo description says "26 hooks" (true: 37); duplicated in both plugin manifests | **H** | `gh api repos/…/echook` · `.claude-plugin/marketplace.json:8` · `plugins/audio-hooks/.claude-plugin/plugin.json:4` vs `bin/audio-hooks.py:162-203` | "They haven't read their own listing in three releases" | Edit 1 setting + 2 JSON lines | **Yes** (pre-click) |
| 2 | README subtitle frozen at v6.2.0 | **H** | `README.md:11`, `:68` vs `bin/audio-hooks.py:159` | "Ships faster than they tell the truth about what they shipped" | Rewrite 2 lines | **Yes** |
| 3 | Three hook counts on one page (39/37/26) | **H** | `README.md:11,68` (39) · `:137,143,199` (37) · `llms.txt:30` (39) · `AGENTS.md:25` (37) | "They can't count the feature in their own title" | 3 edits | **Yes** |
| 4 | "6 on by default" is 3; 3 table rows marked `on` ship `off` | **H** | `README.md:137,150,152,153` vs `config/default_preferences.json` (3 true) · `bin/audio-hooks.py:163-166` | "The docs would have wasted my afternoon" | 4 cells | **Yes** |
| 5 | "Python 3.6+" false — hard 3.7 floor; installer accepts 3.6 | **H** | `README.md:313` · `hooks/user_preferences.py:12` · `hooks/hook_runner.py:39` · `scripts/install-complete.sh:136-142` · `smoke.yml:14` (3.9 floor) | "A 30-second grep falsifies a claim they repeat three times" | 3 docs + installer gate | **Yes** |
| 6 | "Only one `/reload-plugins`" vs `install --plugin` printing 2 slash commands; 5 of 7 paths need a restart | **H** | `README.md:45` · `docs/INSTALLATION_GUIDE.md:5,47,61,103` vs `bin/audio-hooks.py:1424-1434,1897` | "The thesis sentence is disproved by their own stdout" | Rewrite 1 sentence | **Yes** |
| 7 | `homepageUrl` = raw `user-attachments` video blob | M | `gh api repos/…/echook` → `homepage` | (nothing — a silently forfeited slot) | 1 setting | No |
| 8 | `hooks disable a b c` (prescribed remedy) silently drops args 2..n, returns `ok:true` | **H** | `docs/TROUBLESHOOTING.md:129` vs `cmd_hooks` `name = rest[0]` in `bin/audio-hooks.py` | "Their troubleshooting guide fails silently and reports success" | Loop over `rest` | No |
| 9 | `logs tail --invoker` called "the canonical filter", silently ignored | **H** | `docs/ARCHITECTURE.md:348` vs `cmd_logs` (parses `--n`/`--level` only) | "The architecture doc describes a program that doesn't exist" | Implement or delete | No |
| 10 | `TTS_FAILED` / `WEBHOOK_TIMEOUT` / `SELF_UPDATE_FAILED` documented, never emitted | **H** | `hooks/hook_runner.py:85,131-134` · `docs/CLI_REFERENCE.md:101,104` | "The error catalogue describes the design, not the build" | Emit or delete | No |
| 11 | Manifest's `error_codes` cannot see 11 CLI-emitted codes; `docs/CLI_REFERENCE.md:111` promises otherwise | M | `bin/audio-hooks.py:2826-2836` vs `INVALID_USAGE` at 24 sites, `CURSOR_NOT_FOUND:1467`, `DUPLICATE_BRIDGE:1475` | "Their self-describing surface under-describes itself" | Widen the source | No |
| 12 | `ai@gavigo.com` — third party's real email as a test fixture | M | `tests/test_cursor_bridge.py:388,405,407` · `CHANGELOG.md:358`; correct pattern at `:336` | "Judgement signal, and I'm evaluating judgement" | 3 swaps | No |
| 13 | "Fully detached" comment false — no detach primitive in the repo | M | `hooks/hook_runner.py:1990-1992`; grep for `setsid`/`start_new_session`/`DETACHED_PROCESS` → 0 | "The guarantee comes from the editor's config, not their code" | Fix comment | No |
| 14 | WSL audio path: 3 timeout-less `check_output` + per-fire cross-FS copy on the hot path | M | `hooks/hook_runner.py:1221,1228,1267,1272` vs `bin/audio-hooks-statusline.py:175-180` (`timeout=3`) | "'Never blocks' is just not true on WSL" | Add `timeout=` | No |
| 15 | Cursor/Codex hook templates have no `async` — editor waits, 10 s budget | M | `cursor-hooks/hooks.json`, `codex-hooks/hooks.json` (grep `async` → 0) vs `plugins/audio-hooks/hooks/hooks.json` | "The non-blocking property is editor-specific and undocumented" | Add the flag | No |
| 16 | Webhook URL + auth headers passed as **argv** — process-visible | M | `hooks/hook_runner.py:2010` (`sys.executable -c`, url = `argv[1]`, headers = `argv[2]`) | "A Slack webhook URL *is* the credential, readable by any local process" | Pass via stdin | No |
| 17 | Webhook: no retries; `except Exception: pass`; every runtime failure unobservable | M | `hooks/hook_runner.py:2002-2003`, `stdout/stderr=DEVNULL` | "If it stops delivering I will never know" | Log to NDJSON | No |
| 18 | `webhook test` ignores `format` and configured headers — doesn't test the real path | M | `bin/audio-hooks.py:1076-1083` vs `hook_runner.py:1905-1917` | "The verification command verifies a different thing" | Reuse the builder | No |
| 19 | 3 of 5 webhook "integrations" are the same string under a different key | M | `hooks/hook_runner.py:1905-1911` (slack/discord/teams); `teams` uses the legacy connector shape | "Five integrations is three format keys over one line of text" | Say so, or build them | No |
| 20 | Rate-limit alerts gated behind an enabled, non-snoozed carrier hook | M | `hooks/hook_runner.py:2206,2211,2222`; `stop_failure` ships **off** | "Sold as a standalone safety net; it's a rider on an unrelated toggle" | Document or ungate | No |
| 21 | Linux TTS silently no-ops with no log when `espeak`/`spd-say` absent (neither is default on Ubuntu) | M | `hooks/hook_runner.py:1842-1852`; `log_debug` suppressed unless `CLAUDE_HOOKS_DEBUG=1` (`:329-331`) | "Advertised unconditionally, fails invisibly" | Emit `TTS_FAILED` (#10) | No |
| 22 | Windows/WSL TTS uses a weaker escaper than the audio path; `"` breaks it | M | `hooks/hook_runner.py:1705` (`replace('"','\\"')` — PowerShell doesn't honour `\`) vs the correct `:398-404` | "Model-generated text reaching a `-Command` parse stream" | Reuse `escape_powershell_string` | No |
| 23 | `INSTALLATION_GUIDE.md:161` — "healthy = `present: 26, expected: 26`"; actual is 37/37 | M | `docs/INSTALLATION_GUIDE.md:161` vs `bin/audio-hooks.py:1251` (`len(HOOK_CATALOG)`) | "Following the guide, a healthy install reads as broken" | 1 line | No |
| 24 | `ARCHITECTURE.md:165` — "~1100 lines, 27 subcommands"; actual 3,103 lines / 39 | M | `docs/ARCHITECTURE.md:165` · `:54` ("~1700 lines", actual 2,392) | "Nobody has re-read this doc in a year" | Regenerate | No |
| 25 | `update` / `upgrade` / `backup {list,show,restore,prune}` implemented, absent from `CLI_REFERENCE.md` | M | dispatch `bin/audio-hooks.py:3062-3083` · manifest `:2876-2881` vs `docs/CLI_REFERENCE.md` | "The disaster-recovery commands aren't in the reference" | Add 6 rows | No |
| 26 | `hooks list --variants` real + documented in prose, absent from manifest `args` | M | `bin/audio-hooks.py:878` (real), `:2848` (`args: []`) vs `AGENTS.md:28`, `SKILL.md:475` | "An agent trusting the manifest cannot find the flag" | 1 array | No |
| 27 | Install guide says Cursor registers **11** native events; actual is **19** | M | `docs/INSTALLATION_GUIDE.md:73` vs `cursor-hooks/hooks.json` (19) · `AGENTS.md:65` | "The guide omits v6.2's headline feature" | 1 line | No |
| 28 | "All 37 events register" on Claude Code; the template registers **28** | M | `docs/INSTALLATION_GUIDE.md:25` · `AGENTS.md:65` vs `plugins/audio-hooks/hooks/hooks.json` | "Claude Code gets 28 of 37, and both docs say 37" | Correct both | No |
| 29 | `README.md:162` lists 5 `stop_failure` matchers; there are 8 — README's own variant total then sums to 27, not 30 | M | `README.md:162` vs `_variant_catalog()` / `hooks/hook_runner.py:742-788` · `AGENTS.md:25` | "Even the sub-counts don't add to their own total" | Add 3 | No |
| 30 | `_defaults_baseline.json` never regenerated after v6.2 → the no-default-flip guard has a 13-hook hole | M | `tests/test_defaults_stability.py` (`if k not in template: continue`); baseline 48 keys vs `default_preferences.json` 74 | "The guard against exactly this bug can't see the newest 13 events" | Regenerate baseline | No |
| 31 | `config/example_preferences_*.json` are schema-invalid and referenced by nothing | M | Both set `enabled_hooks` to an **array**; `config/user_preferences.schema.json` declares `object`; `"subagent"` isn't a hook name | "Shipped config examples that would fail validation" | Fix or delete | No |
| 32 | `WIDTH_SAFETY_MARGIN`: ARCHITECTURE says 4, STATUS_LINE says 8, code says 8 | L | `docs/ARCHITECTURE.md:260` vs `docs/STATUS_LINE.md:114-116` vs `bin/audio-hooks-statusline.py:98` | — | 1 line | No |
| 33 | Subagent-capture sample size: SKILL says 5, evidence file says 14 | L | `SKILL.md:95` vs `docs/EVENT_BEHAVIOR_NOTES.md:57,64` | "The inference rests on the sample size and they disagree" | 1 line | No |
| 34 | "Agent dumb zone" at 60% in one line, 50% three lines later and everywhere else | L | `SKILL.md:151` vs `:153-155`, `README.md:99-103`, `docs/ARCHITECTURE.md:250` | — | 1 line | No |
| 35 | `AGENTS.md` and `CLAUDE.md` byte-identical (9,620 B, same MD5), no generator, no CI check | M | `diff` empty; `bump-version.sh` doesn't list them; `smoke.yml` doesn't check them | "~10 numeric facts must be hand-edited twice, forever" | Symlink or CI check | No |
| 36 | `bump-version.sh` covers 8 machine files, **0 prose strings** — the mechanism behind the whole pattern | **H** | `scripts/bump-version.sh:8-16` vs 9 stale version strings across README/docs/SKILL/config | "This will be stale again at v6.5.0" | Extend, or CI drift gate | No |
| 37 | 39 of 53 releases shipped with **no CI at all** (created 2026-04-17 in response to issue #10) | L | `gh run list` — first run 2026-04-17; PR #12 added `smoke.yml` | *Positive* if framed; invisible if not | Say it in the README | No |
| 38 | Sole open issue (#3, praise) never answered in 585 days | L | `gh issue view 3` — 3 external comments, maintainer heart-reacted, never replied | "The tracker looks abandoned" | One reply | No |
| 39 | External contributions hand-integrated, never merged → contributor graph shows zero external commits | M | PR #2 closed by maintainer 15 min in, code shipped in v3.3.3 with co-authorship | "Looks single-author-closed to anyone scanning" | Merge, then fix forward | No |
| 40 | `install-complete.sh --help` still advertises "INTERACTIVE MODE (default)"; the script is non-interactive | L | heredoc ~`:800-820` vs `:31` (`NON_INTERACTIVE=true`) · `AGENTS.md:10` | "An agent reading `--help` concludes it prompts" | 1 heredoc | No |
| 41 | 3 orphaned images in `docs/images/` (referenced nowhere), pre-rename | L | `plugin-installed.png`, `plugin-marketplace-detail.png`, `skill-registration.png` | — | Delete | No |
| 42 | `audio/` duplicated wholesale into `plugins/audio-hooks/audio/` — 148 tracked MP3s, 74 distinct | L | `git ls-files audio \| wc -l` → 75; same again under `plugins/` | — | Confirm it's required | No |
| 43 | Stale branch `feat/painless-upgrades-5.1.5` on origin, shipped 3 months ago | L | `git branch -a` | — | Delete | No |
| 44 | 4 author-email identities incl. an employer address on 11 commits | L | `git log --all --format='%ae'`: `chanmeng.dev@gmail.com` (123), `chanmeng666@outlook.com` (18), `c.meng@crimsonacademies.school` (11) | Privacy/attribution, not security | `.mailmap` | No |
| 45 | **Broken internal links: 0** | — | All relative links + images in README/AGENTS/CLAUDE/llms.txt/docs resolved against disk | *Positive* | — | No |

**Hard counts:** 9 stale version strings · 22 docs-vs-docs contradictions (4 intra-document) · 3 defaults-table mismatches · 3 documented-but-unimplemented CLI behaviours · 6 implemented-but-undocumented subcommands · **0 broken internal links** · **0 real secrets in 152 commits.**

---

## Corrections to the briefing

Where the framing handed to me was wrong, and — separately — where reality is **better** than it implied.

### Wrong

1. **Stars: 78, not 79.** 2026-03 is **10**, not 11. Triple-confirmed.
2. **CI checkouts on release day: 10, not 9.** The 3×3 matrix produces 9 `import-smoke` jobs **plus** a standalone `plugin-in-sync` job (run `29689965777`, `total_count: 10`).
3. **"39 in the subtitle, 37 in the table, 26 in the description" — all confirmed, but the framing "three counts for the headline feature" understates it and misattributes the cause.** It is four surfaces (add `llms.txt:30` = 39), and **every value was correct when written**: `v6.1.0` = 26, `v6.2.0` = 39, `v6.3.4` = 37 (verified via `git show <tag>:bin/audio-hooks.py`). `README.md:68`'s "26 → 39 total" was accurate the day it shipped; v6.3.4's worktree-hijack rollback deleted two events and nobody updated the prose. **This is stratigraphy, not carelessness** — which matters, because it changes the fix from "be more careful" to "connect the manifest to CI."
4. **"The Cursor-without-Claude-Code path literally instructs a human to clone a repo and run a python command" — imprecise.** The text at `README.md:212` does say that, but the column header is **"Tell your AI agent"** and the cell is an italicised prompt addressed to the agent, not the human. `SKILL.md:347-352` gives the agent the same runbook. The clone and the python command are genuinely agent-executed. **The real defect on that path is different and better:** it ends in a **human restarting Cursor** (`docs/INSTALLATION_GUIDE.md:61`) that `README.md:212` never mentions. Finding #6 is stated on the corrected basis.
5. **"3 external PRs, all closed unmerged" — literally true, substantively false.** One was closed by the maintainer in 15 minutes *with the code shipped in v3.3.3 and co-authorship credited*; two were self-closed by the contributor within 3 and 25 minutes with zero maintainer involvement. **No external PR was ever ignored or rejected without explanation.** The fair criticism that survives is merge *hygiene* (hand-integration hides contributors), not responsiveness.
6. **Forks: 7 vs 9.** `forks_count` reads 7; the enumerable list returns 9. Six of nine pushed after forking.
7. **"GitHub Sponsors link" — configured but not visible in the README.** `.github/FUNDING.yml` sets `github: ChanMeng666` and `buy_me_a_coffee: chanmeng66u`; only the Buy Me a Coffee button appears in the README body (`README.md:389-390`). Sponsors surfaces only via GitHub's own button.
8. **"Discussions enabled" is not a customer-conversation surface here.** `totalCount: 0` — zero threads in nine months. Watchers: 1.
9. **The `WEBHOOK_TIMEOUT`/`TTS_FAILED` issue is not "partial implementation" — it is the reverse.** The features are fully implemented; the *diagnostics* for them are declared and never fired. That inverts the usual read: the code is ahead of its own observability, not behind its docs.

### Better than implied — and each deserves the one-paragraph public version

The briefing framed several of these as risks. Each has a documented, defensible reason that a diligence reader would find **after** they found the risk. Write the paragraph so the order reverses.

1. **GitGuardian #34199726 was a false positive, and the handling was correct.** `e3e8f4b` (2026-06-23) rewrote five credential-shaped fixtures in `tests/test_sanitize.py` to be assembled at runtime. The flagged values were the **jwt.io homepage demo token** and **AWS's own documented `AKIAIOSFODNN7EXAMPLE`**, plus `sk-ABCDE…UVWX` (the literal alphabet), `ghp_0123456789…` (a counting sequence) and `password=hunter2`. None is provider-issued. The commit message says so accurately. History still carries the old blob (`fa1ae0e`, reachable from `master` and nine tags) — but **a rewrite is not warranted**: it would break nine published tags to erase public documentation samples. *Write four sentences in `SECURITY.md` titled "Why we did not rewrite history for GG#34199726." A diligence reader who greps for `AKIA` will find it and stop.*
2. **The secret sweep over all 152 commits is clean.** Zero real credentials in any ref, ever. No `.env` ever committed. No private keys. No `__pycache__`/`.pyc`/`.DS_Store` tracked. `.gitignore` is thoughtful (it even excludes plugin runtime config with a comment explaining why). `.git` is 6.9 MB.
3. **The issue-response record is exceptional and completely invisible.** Median first response **~2.5 hours**; every actionable issue fixed and shipped, usually same-day; reporters credited by name. This is the single most persuasive artifact the project owns and it is buried in closed issues. *Put it in the README: "Median first response to an issue: under 3 hours. Every bug ever reported was fixed and released — see #1, #4, #5, #10, #14."*
4. **CI exists because of an incident, not because of a template.** `smoke.yml` was created 2026-04-17 in direct response to issue #10 (a `NameError` that broke every command on two releases). That is exactly the story engineers respect, and nothing in the repo tells it.
5. **The agent-operable surface genuinely delivers.** 20 dispatch verbs / 39 subcommand forms, all non-interactive JSON (`bin/audio-hooks.py:3062-3083`); `emit_error` returns `{code, message, hint, suggested_command}` where `suggested_command` is a **runnable string** an agent can loop on (`:123-134`); `_build_manifest()` self-describes subcommands, the live hook catalog, variants, gating precedence, config keys and env vars (`:2824-3045`); a bare `audio-hooks` or `--help` returns the manifest, so an agent that guesses wrong lands on the introspection surface. The install *story* fails the "AI-operated" claim; **the operating surface passes it.** Say the narrower thing and it becomes defensible.
6. **The privacy posture is a real, unusual asset.** Nothing leaves the machine, ever, except a user-configured webhook (default `enabled: false`). No telemetry, no analytics, no crash reporting, no update check. The `raw` webhook payload deliberately strips `transcript_path` and makes `user_email` opt-in (`hooks/hook_runner.py:1948-1952`). *One paragraph in the README — and it is the reason to choose opt-in over opt-out in §5.*
7. **The engineering honesty in the source is above average and invisible from outside.** `SYNTHETIC_VARIANT_DEFAULTS` (`hooks/hook_runner.py`) ships four v6.4 notification variants **off** with a comment explaining they *could not be observed firing* during a ~1h capture, and calls the registration "a completeness and forward-compatibility move, not a feature we can demonstrate." `AGENTS.md:67` warns that a file which *looks* generated isn't. `HOOK_CATALOG`'s `stop` entry documents that it fires on every turn and explicitly tells the reader **not** to use it for "task complete." That is the register of someone who has been burned and learned. *This is what should be in the README instead of "39 hook events."*
8. **The v6.3.4 rollback is a credit, not a blemish.** Shipping a fix that *deletes* two of your own advertised features because they broke someone's git-worktree isolation is the correct call and a rare one. It currently reads as "the README's count went stale." *One line in the CHANGELOG summary and it reads as discipline.*
9. **The v5.1.4 → v5.1.5 same-day default revert** is the origin of the "6 on by default" fossil. Documented, it becomes evidence of judgement — the author shipped noisier defaults, heard about it, and reverted within hours.
10. **Two-thirds of forkers modified the code** (6 of 9 pushed after forking). For a 78-star repo that is a healthier engagement signal than the star count suggests.

---

## What would prove this wrong

The diagnostic rests on four load-bearing claims. Each has a specific, cheap test.

1. **"Shipping is not a distribution channel here."** — Falsified if star acquisition is category-wide-declining rather than project-specific. **Test:** pull monthly star curves for 5–10 comparable Claude Code hook/notification repos over Nov 2025 – Jul 2026. If they all peak in April and decay, this is market seasonality (or Claude Code's own growth curve), not echook. ~1 hour. *I did not run this, and it is the single most important open question in the report.*

2. **"There is no usage telemetry, so no funnel question is answerable."** — Falsified if Anthropic exposes per-plugin install counts to marketplace authors, or if the author has private data (referral logs, a mailing list, direct user contact). **Test:** ask the author directly; check the Claude Code plugin-author surface. 15 minutes.

3. **"~7 clones/day is contaminated by machines."** — The 92% clone-per-unique-viewer ratio is my inference, not a measurement. **Test:** start the daily traffic snapshot (cheap fix #9) and watch whether clone counts move with *release* events (human) or stay flat and periodic (bots/mirrors). Two weeks of data settles it. If clones turn out to be predominantly human, the funnel is materially healthier than this report says and the "tens of users" sizing is too pessimistic.

4. **"The stale README is costing installs."** — This is the report's least-supported claim and I want to flag it as such. It is *plausible* (Google is the #1 referrer and the snippet is wrong; 64% of visitors never leave the front page) but **unproven and currently unprovable**. **Test:** fix findings #1–#5, then compare 14-day unique-visitor and unique-cloner rates before and after. This is the first experiment the project has ever been in a position to run — and it only becomes possible once the daily traffic snapshot exists. Which is the argument for doing #9 this week rather than next quarter.

5. **The gist referrer (16 visits / 9 uniques).** If it turns out to be a widely-shared dotfiles or "Claude Code setup" gist, discovery is less stalled than the star curve implies and there is a warm channel to cultivate. **Test:** only the author can resolve this — check whether anyone has shared echook in a gist they know about, or add a `?ref=gist` style marker. Unresolvable externally if the gist is secret.

---

### Sources

Internal: all `path:line` references above, verified against `D:\github_repository\claude-code-audio-hooks` at HEAD `c095e28` (= `v6.4.0`).

External, fetched 2026-08-04:
- [docs.brew.sh/Analytics](https://docs.brew.sh/Analytics) [PAGE] — Homebrew opt-out analytics model
- [nextjs.org/telemetry](https://nextjs.org/telemetry) [PAGE] — Next.js opt-out telemetry, negative-collection list
- [pypi.org/project/echook](https://pypi.org/project/echook/) [PAGE] — 404, not published
- GitHub REST/GraphQL API via `gh` (repo metadata, 53 releases, 8 issues, 8 PRs, 9 forks, discussions, traffic clones/views/referrers/paths, stargazers with timestamps, 51 workflow runs) [PAGE]
- [gist.github.com/search?q=echook](https://gist.github.com/search?q=echook) [PAGE] — no identifying result; gist referrer source remains [UNVERIFIED]
