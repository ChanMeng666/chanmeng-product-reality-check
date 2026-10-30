# Research index — echook viability engagement

Engagement opened 2026-08-04. Subject: **echook** (github.com/ChanMeng666/echook), MIT audio-notification
+ status-line utility for Claude Code / Cursor / Codex. Question asked: *is there a business here, who
would pay, how should it be positioned, and should the owner keep going?*

## Reports

| Report | Date | Area | Status | Superseded by |
|---|---|---|---|---|
| [`competitors/2026-08-04-competitor-sweep.md`](competitors/2026-08-04-competitor-sweep.md) | 2026-08-04 | Competitors, four rings | Current | — |
| [`competitors/2026-08-04-prior-art-audit.md`](competitors/2026-08-04-prior-art-audit.md) | 2026-08-04 | Prior art / uniqueness | Current | — |
| [`market/2026-08-04-who-pays-and-sizing.md`](market/2026-08-04-who-pays-and-sizing.md) | 2026-08-04 | Bottom-up sizing | Current | — |
| [`market/2026-08-04-base-rates.md`](market/2026-08-04-base-rates.md) | 2026-08-04 | Monetization base rates | Current | — |
| [`product/2026-08-04-product-diagnostic.md`](product/2026-08-04-product-diagnostic.md) | 2026-08-04 | Product / copy / evidence | Current | — |
| [`red-team/2026-08-04-kill-memo.md`](red-team/2026-08-04-kill-memo.md) | 2026-08-04 | Adversarial review | Current | — |
| [`red-team/2026-08-04-patch-record.md`](red-team/2026-08-04-patch-record.md) | 2026-08-04 | What was patched vs left standing | Current | — |

Data: [`../data/competitors.json`](../data/competitors.json) — 37 entries, `last_verified` 2026-08-04.
Staleness rule: any entry older than 30 days may not be cited without re-verification. The entries most
likely to rot are the platform ones (Anthropic ships weekly); re-verify those first.

---

## Cross-report corrections

Where two reports disagreed, or where a report corrected the brief it was given. **None of these were
resolved in the flattering direction.** The disagreement is itself a finding.

### C1. "Anthropic ships no native audio" — HALF WRONG, both ways

- **The brief I gave the agents** asserted, from `code.claude.com/docs/en/settings`, that *no audio,
  sound or terminal-bell setting is documented*. **That was wrong.** I had fetched the wrong page.
- **The sizing report** then found "a sweep of 24 months of Claude Code changelogs found **zero native
  audio features**" and concluded the audio track has no first-party equivalent.
- **The competitor sweep** found the opposite: `code.claude.com/docs/en/terminal-config` documents
  `preferredNotifChannel: "terminal_bell"`, ships desktop notifications by default in Ghostty, Kitty
  and iTerm2, and gives a copy-pasteable `afplay` Notification-hook example — on a page whose symptom
  index reads verbatim *"No sound or alert when Claude finishes."*
- **Resolved by me directly** (`code.claude.com/docs/en/terminal-config`, fetched 2026-08-04) `[PAGE]`:
  **both are partly right, and the synthesis is worse for echook than either alone.** Anthropic ships
  no audio *feature* — no sound files, no themes, no per-event mapping. It ships the *terminal bell,
  desktop notifications on three terminals, and a documented four-line recipe for a custom sound.*
  So Ring 3's "substitute that is not a product" **is the vendor's own documentation page**, which is
  the cheapest, most discoverable, most trusted substitute a competitor can have. Anthropic also closed
  issue #1288 "Sound notifications" (44 reactions) as `completed`.
- **Consequence:** any copy claiming Claude Code "can't make a sound" is banned. See BC-8.

### C2. Star count: 79 vs 78 — the count went DOWN during the engagement

- I read `stargazers_count` = **79** at the start of this session and the per-month series summed to 79
  (March = 11). The diagnostic agent read **78** (March = 10). I re-ran both queries at the end of the
  session: **both now return 78.**
- This is not an arithmetic dispute. **A star was removed during the ~4 hours of this engagement.** The
  honest number is 78 as of 2026-08-04, and the direction is worth recording rather than smoothing over.
- All figures in the deliverables use **78**. Any document citing 79 is stale.

### C3. CI checkouts on the clone-spike day: 9 vs 10

- My brief said the `smoke.yml` matrix is 3 OS × 3 Python = 9 checkouts. The diagnostic read the
  workflow and found **10** — the matrix plus a separate `plugin-in-sync` job. **Diagnostic is correct**;
  it read the file, I inferred from the matrix. De-spiked baselines use 10.

### C4. Platform absorption is NOT the main risk — this reverses the intuitive read of my own finding

- I opened the engagement having established that Anthropic now ships a native statusLine fed
  pre-computed `context_window.used_percentage` and `rate_limits.*`, plus mobile push on task
  completion. The natural inference — *the platform absorbed the category, that is what killed it* —
  **is contradicted by the data.**
- The base-rates report found that **`ccstatusline` grew ~25× and `ccusage` ~6× AFTER** the native
  features shipped. `ccstatusline` now does 407,682 monthly installs.
- **Therefore:** the native features created the category rather than closing it, and echook's problem
  is **distribution and demand, not absorption**. This materially changes the recommendation: "the
  platform ate your lunch" would have been a comfortable, wrong story. The uncomfortable, right one is
  that the category is thriving and echook is not in it.
- The absorption risk is real but **specific**: it applies to the *status-line* track (where Anthropic
  now supplies the measurement and echook supplies only formatting), not to the audio track.

### C5. The "locked-out enterprise" archetype INVERTS — my own best idea, killed

- I proposed, and asked the sizing agent to size, an archetype of orgs on Bedrock / Vertex / Microsoft
  Foundry / LLM gateways / API-key auth / Zero-Data-Retention, who are **named in Anthropic's own docs**
  as unable to use native mobile push. I thought it was the strongest lane in the engagement.
- The report killed it: **hooks work on every provider**, so a compliance-constrained org writes its own
  20-line notifier in an afternoon — and is the *least* plausible buyer of an unaudited 78-star repo
  that fans out webhooks off ZDR machines. The exclusion from *push* is not an exclusion from
  *notification*.
- Sized at **$0**. Recorded here because a lane I generated and believed in did not survive, and the
  record of that is worth more than the lane was.

### C6. "3 external PRs, none merged" — literally true, substantively false

- My brief characterized the external-contribution record as three PRs, all closed unmerged, and invited
  a reading about maintainer responsiveness. The diagnostic checked each one: **one was closed by the
  maintainer within 15 minutes with the code shipped in v3.3.3 and co-authorship credited**; the other
  two were **self-closed by the contributor** within 3 and 25 minutes with no maintainer involvement.
- The framing was mine and it was unfair. Corrected everywhere. This is a case where the evidence is
  **better** than the brief implied.

### C7. GitGuardian #34199726 was synthetic, not a leak

- The brief flagged commit `e3e8f4b` as a possible credential incident. It was a **synthetic test
  fixture** — the public `jwt.io` demo token and AWS's own documentation placeholder
  `AKIAIOSFODNN7EXAMPLE`. The forward-fix was correct and a history rewrite is **not** warranted.
- The residual risk is presentational: a diligence reader grepping history finds an `AKIA` string
  before they find the explanation. Fix is one paragraph in `SECURITY.md`, not an engineering task.

### C8. The one instrument that exists may be measuring machines

- The diagnostic found 78 unique cloners against 85 unique viewers in the same 14-day window — a **92%
  clone-to-view ratio**, while 64% of viewers never leave the front page. Humans do not behave like
  that. Some unknown share of the clone traffic is bots, mirrors and scrapers.
- **Consequence:** clone counts may not be cited as adoption anywhere, in any document, including
  informally. They are the only usage-shaped number that exists, and they do not mean what they look
  like. This is the single most important measurement caveat in the engagement.

---

### C9. The red team corrected the synthesis itself — four figures failed

The kill memo spot-checked 24 ledger rows: **18 exact, 2 with dated same-day drift, 4 failed.** The
failures were mine, introduced during synthesis, not the research agents':

- A quote attributed `[PAGE]` to an Anthropic page **it does not appear on** — withdrawn, not softened.
- **$49,999** where the source says **$49,000** — propagated to 11 sites across 6 files.
- **"Chime requests: zero issues"** — false; a search returns two.
- **"2,016 stars"** across nine convergent projects — the seven enumerated total **1,770**.

And the worst: **S1, the surviving differentiator, was stated against the wrong comparator.** I compared
echook to Anthropic's *mobile push* (two toggles, no per-event config) when echook runs on the **hook**
surface, where `Notification` already matches on eight types including `agent_completed`. **The falsifier
I wrote for S1 had already fired**, and the competitor sweep's own scorecard said `ABSORBED` — I led with
the friendlier fact in three documents. Verified directly at `code.claude.com/docs/en/hooks` `[PAGE]`
before patching. Full accounting in the patch record.

**The pattern worth naming:** every one of these errors moved in the *flattering* direction, in a package
whose entire purpose is to resist that. That is the argument for running a red team that has not seen
your reasoning.

---

## Claims refuted more than once → escalated to the banned-claims list

Per the method, a claim refuted independently by two reports goes on the permanent ban list in
[`../marketing/copy/messaging-library.md`](../marketing/copy/messaging-library.md).

| Claim | Refuted in | Ban |
|---|---|---|
| "AI-operated, not AI-assisted" as a *differentiator* | prior-art audit, competitor sweep | BC-1 |
| "One slash command, then natural language forever" as unique | prior-art audit, competitor sweep | BC-2 |
| "Complete hook coverage" | prior-art audit, product diagnostic | BC-3 |
| The context-usage status line as distinctive | competitor sweep, prior-art audit | BC-4 |
| Any hook-event count other than 37 | product diagnostic (×6 surfaces) | BC-5 |
