# Messaging library and banned claims — echook

**LIVING DOCUMENT.** The reusable copy bank, and the permanent record of what may never be said again.

Enforcement rule: **ban by SHAPE, not by wording.** A banned "only" claim returns three weeks later as
"the one property nothing else in this space has," which is the same claim under paraphrase and slips
past a grep for the literal word. When reviewing copy, look for the *move* — an exclusivity assertion, a
superlative, a capability promise beyond what was demonstrated — not the vocabulary.

---

## The banned-claims list

| # | Banned claim | Refutation | Source |
|---|---|---|---|
| **BC-1** | "AI-operated, not AI-assisted" / "you don't read this, your agent does" / "the human is upstream of the agent, not downstream of the CLI" — **as a differentiator** | **601,280 `SKILL.md` files exist on GitHub** — shipping an agent-readable instruction file beside a CLI is the ecosystem default. A 4,973★ competitor in the same niche ships five Agent Skills doing exactly this. *(An earlier version of this row quoted Anthropic's engineering blog as saying "Skills are authored for agents rather than humans." The red team could not locate that sentence on the cited page. **Citation withdrawn; do not use the quote.** The ban stands on the other two grounds.)* | prior-art audit; correction R1 |
| **BC-2** | "You type one slash command at install time. Then natural language forever." — as a unique property | Describes what any CLI shipping a skill gets for free in 2026. Claude Code's own `/statusline` takes natural-language instructions and writes the config itself. | prior-art audit |
| **BC-3** | "Complete hook coverage" / "full lifecycle coverage" | 63 events are documented across the three harnesses; echook implements 37. `DirectoryAdded` shipped 2026-07-24, after echook's last push. "Complete" was false when written and drifts further every release. | prior-art audit, diagnostic |
| **BC-4** | The context-usage status line as a distinguishing feature | 2,161 statusline repos exist; 18 of them have more stars than echook has in total. `claude-hud` has 27,066★; `ccstatusline` has 407,682 monthly installs. Anthropic pre-computes `context_window.used_percentage` and `rate_limits.*`, so echook's bars are **formatting, not measurement**. | competitor sweep |
| **BC-5** | Any hook-event count other than **37** | True count is 37 (`bin/audio-hooks.py:162-203`) + 30 matcher variants. Six shipped surfaces say 39 or 26. | diagnostic |
| **BC-6** | "6 hooks on by default" | Actually **3**. Three table rows also promise sounds that ship silent — a v5.1.4 fossil that survived its own same-day v5.1.5 revert. | diagnostic |
| **BC-7** | Any version string other than the current release | README's headline said v6.2.0 while the repo shipped v6.4.0. | diagnostic |
| **BC-8** | "Claude Code can't play a sound" / "there's no native way to be notified" | False. `preferredNotifChannel: "terminal_bell"`, default desktop notifications in Ghostty/Kitty/iTerm2, and a copy-pasteable `afplay` Notification hook — all on one Anthropic page whose symptom index reads *"No sound or alert when Claude finishes."* Anthropic closed issue #1288 "Sound notifications" as `completed`. | cross-report correction C1 |
| **BC-9** | Clone counts, or any derivative, cited as adoption or users | 78 unique cloners vs 85 unique viewers = 92%, which no human population produces. Contaminated by machines to an unknown degree. | correction C8 |
| **BC-10** | "The platform absorbed this category" as an explanation for flat growth | Contradicted by the data: `ccstatusline` grew ~25× and `ccusage` ~6× **after** the native features shipped. The problem is distribution and demand, not absorption. Using this would be a comfortable, false story. | correction C4 |
| **BC-11** | "Enterprises locked out of native push are a market" | Hooks work on every provider; a compliance-constrained org writes its own 20-line notifier and is the least likely buyer of an unaudited 78-star repo that fans out webhooks off ZDR machines. Sized at $0. | correction C5 |
| **BC-12** | Hype vocabulary — "revolutionary", "game-changing", "the future of", "10x", "the missing piece" | Unfalsifiable everywhere, and actively downvote-bait in the technical communities where this buyer lives. | method |
| **BC-13** | "Anthropic has no per-event notification configuration" / "echook is the granular one" | **Added 2026-08-04 after red team.** True only of *mobile push*. On the hook surface echook actually uses, Claude Code's `Notification` matcher filters on `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`, `agent_completed` — and echook's own README lists the same eight. Comparing against the wrong surface is a one-search refutation. | correction R2 |
| **BC-14** | "Chime requests: zero issues" | **False** — a search returns two. The underlying demand finding survives and is stronger: all 38 sound issues in every state total ~68 reactions, and issue #73384, echook's pitch almost verbatim, has **zero**. Use those figures instead. | correction R3 |
| **BC-15** | "2,016 stars across nine convergent projects" / "convergent invention proves the gap is real" | The seven enumerated projects total **1,770**; the figure does not reconstruct and was sold as instantly checkable. And the source report says **do not assert either direction** — capable people building the same thing and stopping is equally consistent with "no demand." | correction R4 |

### Banned citations

- **"A search for our exact description returns only us."** A search phrased in the product's own
  vocabulary is not independent evidence of anything. Never use it, in any form, including as a
  throwaway line.
- **"N GitHub stars"** as evidence of demand in a monetization argument. It measures interest in a post.
  It is fine as a factual descriptor, never as validation.

---

## Verbatim-locked answers

Use **exactly** this wording. Each was written to be defensible to the word; paraphrasing is how the
defensibility gets lost.

**On what Claude Code already does:**
> "Claude Code can already ring the terminal bell, pop a desktop notification in Ghostty, Kitty and
> iTerm2, and push to your phone when a task finishes or it needs a decision. Anthropic also publishes a
> four-line hook that plays any sound you want. If one sound for everything is enough, that is genuinely
> the right answer and it costs nothing. echook is for when you want to hear *which* of 37 things
> happened, and on Cursor and Codex too."

**On price:**
> "It's MIT and free. I haven't found a defensible reason to charge for something you can fork, and I'd
> rather say that than invent one."

**On adoption:**
> "78 stars, and I have no idea how many people actually use it — there's no telemetry, and the clone
> numbers are contaminated by bots. That's a gap in my instrumentation, not a number I'm hiding."

**On the biggest competitor:**
> "peon-ping is more adopted than echook by about 60×, and covers 21 harnesses to my 3. It groups
> everything into 7 sound categories; I resolve 37 distinct events. That's the difference — you decide
> whether it matters."

---

## Approved comparison sentences

Each is exactly what the research supports and no more. Framed as *"here is the difference, you decide"*,
never as a proven verdict.

- ~~"Anthropic's mobile push has two on/off toggles and no per-event configuration. echook resolves 37
  events."~~ **WITHDRAWN 2026-08-04.** True of *mobile push*, but misleading by comparator: echook runs
  on the **hook** surface, where Claude Code's `Notification` matcher already filters on eight
  notification types including `agent_completed` and `agent_needs_input` `[PAGE]`. Using this sentence
  invites a one-search refutation. **New BC-13.**
- "Anthropic ships 38 hook events but no sound files, no themes, and nothing for Cursor or Codex.
  echook ships the sounds already mapped, on all three." — supported by `hooks` docs `[PAGE]` + the sweep
- "peon-ping covers more harnesses; echook distinguishes more events." — supported by the sweep
- "Codex's built-in `notify` emits one event type." — supported by the sweep
- "Every echook operation is a non-interactive CLI command, and the manifest derives its hook list from
  live code, so it can't drift from what actually ships." — supported by the diagnostic, and the one
  claim in this file the diagnostic independently *strengthened*

---

## Copy that is currently shipped and violates this file

As of 2026-08-04 the live README violates BC-1, BC-2, BC-3, BC-5, BC-6 and BC-7. **This is the most
damaging class of finding in the method** — a landing page leading with claims the owner's own research
has refuted proves the discipline is performative. The fixes are listed in the diagnostic; three of them
total 23 minutes.
