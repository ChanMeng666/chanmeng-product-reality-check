# Positioning — echook

**LIVING DOCUMENT.** States what is true *now*; edited in place. **If a claim is not supported here, it
does not ship anywhere** — not in the README, not in a Reddit post, not in a reply to an issue.

**Status: this positioning is a hypothesis under test, not a settled truth.** Written 2026-08-04 against
research of the same date. It has been tested against zero buyers. The evidence that would falsify it is
named in the last section, and the first falsifier is scheduled inside 14 days.

**Boundary rule:** zero product truth lives in this workspace. The product repo
(`D:\github_repository\claude-code-audio-hooks`) is the authority on what the software does. This file is
the authority on who it is for. Where they disagree, that gap is a finding — see the product diagnostic.

---

## The statement

> **For** a developer who runs Claude Code, Cursor or Codex on a machine where the vendor's own
> notification path does not reach them — a non-notifying terminal, a locked-down or gateway-routed
> deployment, or a second and third editor the vendor does not cover —
> **echook** is a notification layer that gives you a distinct, ready-made sound per event, at your desk,
> **Unlike** the terminal bell or the four-line `afplay` hook in Anthropic's own docs — which are free,
> documented by the vendor, and enough if one sound for everything suits you — echook ships the sounds
> already mapped to 37 events and works on **Cursor and Codex**, which the vendor's own surface does not
> cover, and is configured by talking to the agent already in the room rather than by hand-editing
> `settings.json`.
> **You pay** — nothing. There is no price and, on this research, no defensible one. See
> `viability.md` for the one paid experiment worth running and the date it reports.

**Note the shape of that statement: it is narrow, and it is defensive.** That is what the research left
standing. A wider claim was available on 2026-08-03 and is now banned.

---

## The corrected moat

### ~~Refuted: "AI-operated, not AI-assisted — you don't read this, your agent does"~~

This was the headline differentiator and it is **dead as a differentiator**. Three independent
refutations:

1. **It is the platform's documented default, not an unclaimed insight.** Anthropic's engineering blog
   (2025-10-16) defines the Skills format echook ships with the sentence *"Skills are authored for
   agents rather than humans"* `[PAGE]`. echook's banner says "you don't read this, your agent does."
   Anthropic wrote the same sentence nine months earlier, as the definition of the file format.
   **601,280 `SKILL.md` files exist on GitHub.**
2. **A competitor in the same niche already ships it, at 63× the adoption.** `PeonPing/peon-ping`
   (**4,973★**, MIT, active) ships **five Agent Skills** — its `peon-ping-config/SKILL.md` description
   reads *"Use when user wants to change peon-ping settings like volume, enable round-robin, add packs
   to rotation, toggle sound categories, or adjust any config."* That is echook's "natural language
   forever," in echook's exact niche.
3. **The vendor ships natural-language configuration in echook's own domain.** Claude Code's
   `/statusline` command accepts natural-language instructions, generates the script, and updates
   settings automatically.

### What actually survives

Two things, and both are narrower than what they replace.

**S1 — ~~Per-event granularity~~ → Batteries-included audio + cross-editor coverage. [CORRECTED
2026-08-04 after red team — the original S1 was wrong.]**

The first version of S1 claimed per-event granularity, comparing echook to Anthropic's **mobile push**
(two toggles, "no per-event configuration"). Wrong comparator: echook runs on the **hook** surface, and
Claude Code's `Notification` matcher already filters on type — `permission_prompt`, `idle_prompt`,
`auth_success`, `elicitation_dialog`, `elicitation_complete`, `elicitation_response`, `agent_needs_input`,
`agent_completed` `[PAGE]`. echook's own README lists those same eight. **It wraps Anthropic's
granularity; it does not add to it.** The falsifier written for S1 had already fired, and the competitor
sweep's own scorecard already said `ABSORBED`.

What survives: Anthropic documents 38 hook events but ships **no sound assets, no themes, and nothing for
Cursor or Codex**. echook's edge is *packaging* (the sounds exist and are mapped) and *coverage* (three
editors). Not capability.
**Status: provisional and thinner than first written.** No buyer has been observed valuing it, and the
demand signal points the other way — see the adverse finding below. Copy must treat it as *"here is the
difference, you tell me if it matters,"* never as established value.

**S2 — The architectural property: there is no interactive path.** Every operation is a non-interactive,
JSON-in/JSON-out CLI command; hand-editing is unsupported by design; the manifest derives its hook list
from live code and therefore **cannot** lie. This is a *property*, not a priority claim, so it survives
any amount of prior art — it is refutable only from inside echook. It is also the thing the diagnostic
found genuinely well-built.
**Status: real, and currently invisible.** It is buried under copy that contradicts itself six times on
the hook count.

### The clock on the moat

**S1 is a lead, not a moat — and it is a short one.** Any of peon-ping, Anthropic or a motivated
weekend contributor could add per-event granularity in under two quarters; peon-ping already has the
harness coverage and would only need to widen its category map. Nothing about echook's per-event work is
hard to copy, only tedious. Treat S1 as a lead measured in months.

**S2 is durable but not commercial.** Architectural discipline does not convert to revenue on its own
evidence; see `viability.md`.

### The adverse finding that governs all of this

**Users want to be *told*, not *serenaded*.** On the Claude Code issue tracker, notification feature
requests drew 69 / 65 / 42 / 40 / 37 reactions. *Sound* requests drew **1 / 1 / 0 / 0**. Across **all 38
sound-related issues in every state, total reactions are roughly 68** — one notification issue outdraws
the entire sound corpus. And issue **#73384**, "built-in distinct notification sounds for 'needs input'
vs …" — echook's pitch almost verbatim — has **zero reactions**.

*(Correction: an earlier draft claimed "chime requests: zero issues." That was false — a search returns
two. The finding survived the correction and got stronger, because the red team ran the full-population
check the first draft had skipped.)*

echook's differentiation is concentrated in exactly the dimension with the weakest demonstrated demand.
This is the strongest single argument against the product and it appears here, in the positioning
document, rather than in an appendix.

---

## Messaging do-NOTs

1. **Do not sell the mechanism to an audience that buys the outcome.** "AI-operated", "39 hook events",
   "manifest-first", "non-interactive CLI" are mechanisms. The outcome is *"you can walk away from a
   long run and be called back for the right reason."* The mechanism pitch is legitimate in exactly one
   room — a contributor or an employer reading the repo as engineering evidence — and the two pitches
   never mix in the same post.
2. **Do not claim Claude Code cannot make a sound.** It can: `preferredNotifChannel: "terminal_bell"`,
   default desktop notifications in Ghostty/Kitty/iTerm2, and a four-line `afplay` hook in Anthropic's
   own docs. Anyone checking finds the vendor's page in one search and stops reading. Lead with
   *granularity and cross-editor*, never with *capability*.
3. **Do not lead with the technology label in communities that resent it.** r/ClaudeAI and similar
   venues have promotion rules; a "look what I built with AI" framing in an AI-tooling subreddit is
   downvote-bait. Lead with the specific annoyance solved.
4. **Do not cite clone counts as adoption.** 78 unique cloners against 85 unique viewers is a 92% ratio
   that no human population produces. The number is contaminated by machines to an unknown degree. It
   may not be used, even informally. (Cross-report correction C8.)

---

## Elevator pitches, one per audience — never mixed

**To a developer (the user):**
> "If your terminal doesn't pop a notification and you don't want the bell for *everything*, echook
> gives you a different sound for 'done' versus 'needs permission' versus 'rate-limited', on Claude
> Code, Cursor and Codex. You set it up by asking your agent, not by editing JSON."

**To an employer or client (the maintainer, not the software):**
> "I maintain a cross-platform notification system for three different AI coding harnesses — 37 events,
> 292 tests, a manifest that derives itself from live code so the docs can't drift, CI on three OSes and
> three Python versions, nine months and 53 releases of sustained maintenance."

These two must not appear in the same post. The first is a product pitch to a market that has not paid;
the second is a competence pitch to a market that **has a sourced price of $10,000–$49,000 per custom
project** and is the highest-value lane in the entire engagement.

---

## Objection handling

| The objection, as a buyer actually says it | Honest response | Evidence |
|---|---|---|
| "Claude Code already does this." | Partly true, and I won't pretend otherwise. It rings a bell or pops a toast, and pushes to your phone on task-finish or permission — with two on/off toggles and no per-event configuration. echook's difference is *which* event, and Cursor and Codex too. If two toggles are enough for you, use them. | `terminal-config`, `remote-control` docs `[PAGE]` |
| "I can do this with four lines in a Stop hook." | Yes — Anthropic publishes exactly those four lines. If one sound for everything is what you want, that is genuinely the right answer and it is free. | `terminal-config` `[PAGE]` |
| "peon-ping has 4,973 stars and does the same thing." | It is more adopted and covers 21 harnesses to my 3. It collapses events into 7 sound categories; I resolve 37. That is the whole difference — decide whether it matters to you. | competitor sweep |
| "Why would I pay for MIT software I can fork?" | You wouldn't, and I'm not asking you to. Nothing here is priced. | this document |
| "Your README contradicts itself three times on the hook count." | It did, and that was a real failure of the hand-maintained surfaces while the generated ones stayed correct. Fixed on \<date\>. | product diagnostic |

---

## What would change this positioning

1. **A paid experiment returns ≥25 buyers in 14 days** (`viability.md` G1) → the "no defensible price"
   clause is falsified and the statement gains a "You pay" line.
2. **Any of the 20 named locked-out orgs asks for a quote** → C5's inversion was wrong and the
   enterprise lane reopens.
3. **peon-ping ships per-event granularity** → S1 dies and only S2 remains. Watch its releases monthly.
4. **Anthropic ships per-event notification configuration** → S1 dies outright. Watch the changelog
   monthly; this is the single most likely event on the list.
5. **A sound-related Claude Code issue crosses ~40 reactions** → the adverse demand finding is
   overturned and the audio track has a real market. Check quarterly.
