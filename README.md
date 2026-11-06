# chanmeng-product-reality-check

A Claude agent skill for the developer who built something good and has no users.

It runs the unglamorous half of shipping a product: finding out who would actually pay,
auditing the claims you have been making against prior art, sizing the opportunity from named
buyers rather than a press-release TAM, hunting the contradictions between what your landing
page says and what your code does, and then red-teaming the whole thing in the voice of the
skeptic whose "no" would hurt most.

The posture is validation-first. **The deliverable is truth, not encouragement.** When the
honest answer is "this is a good $1M/year business and not a venture-scale one," or "the
differentiator you have been leading with is already table stakes for the market leader," the
skill says so, then says what is actually left standing. That is not pessimism as a style —
conceding weaknesses openly is what buys credibility for the claims that survive. Readers
punish discovered weakness, not disclosed weakness.

## Why

Most side projects are validated by vibes. You build the thing, you write a README that calls
it the first tool that does X, you post it, nothing happens, and you never find out which of
the three possible reasons it was. This skill makes the agent do the research half properly and
adversarially — before you sink another three months in.

Concretely, it forces five things that hand-waved validation skips:

- **A falsification section on every report.** No conclusion ships without a list of specific,
  cheap-to-check observations that would force it to change.
- **A prior-art audit on every superlative.** "First", "only", "nobody does this" gets checked
  against adjacent categories, historical work, academic papers and dormant twins — because a
  stranger can refute it in one search, and that refutation discredits everything next to it.
- **A claim ledger.** Every externally checkable number carries a source URL fetched during the
  session and a verification date. Numbers without a row get deleted, never softened.
- **Bottom-up sizing.** Named buyer archetypes × sourced price anchors × defensible counts.
  "1% of a $40B market" is not evidence and never appears.
- **A red-team kill memo, then evidence gates with dates.** A hostile persona writes "I pass
  because…", the single load-bearing fact gets checked, every finding patches a document, and
  numeric go/kill thresholds are set *before* the evidence that will be judged against them.

## Install

### Any agent, with the skills CLI

Installs into Claude Code, Cursor, Codex, GitHub Copilot, Gemini CLI and the other agents the CLI supports. Listed on [skills.sh](https://skills.sh/chanmeng666).

```bash
npx skills add ChanMeng666/chanmeng-product-reality-check
```

### As a Claude Code plugin (recommended)

```text
/plugin install chanmeng-product-reality-check --marketplace ChanMeng666/chanmeng-product-reality-check
```

On Claude Code older than 2.1.275, add the marketplace first:

```text
/plugin marketplace add ChanMeng666/chanmeng-product-reality-check
/plugin install chanmeng-product-reality-check@chanmeng-product-reality-check
```

### Manual install

Copy the inner `chanmeng-product-reality-check/` directory into your skills folder:

```bash
git clone https://github.com/ChanMeng666/chanmeng-product-reality-check
cd chanmeng-product-reality-check

# Personal — available in every project
cp -r chanmeng-product-reality-check ~/.claude/skills/

# Or per-project — checked into the repo, shared with the team
mkdir -p .claude/skills && cp -r chanmeng-product-reality-check .claude/skills/
```

The path that matters is `~/.claude/skills/chanmeng-product-reality-check/SKILL.md` — the inner
directory, not this repository's root.

Then just describe the problem. It triggers on the real questions people ask — "who would pay
for this?", "is my side project viable?", "why is nobody using it?", "check my competitors",
"help me position this", "is this pricing sane?", "review my pitch" — without anyone having to
say the words "market research".

## What you get

Six phases, scaled to how much time you have. A **quick pass** (one session) is intake →
competitor sweep → prior-art check → a positioning draft → a 10-question mini red team, and
outputs a few files. A **deep engagement** (days) produces the full workspace.

| Phase | What happens |
|---|---|
| **1 — Intake** | Eight questions, including the two nobody asks: *what would make you stop?* and *what are you afraid is true?* Then it reads your actual landing page, README, pricing page and code rather than believing the intake |
| **2 — Scaffold** | A research workspace — `strategy/`, `research/`, `decisions/`, `data/` — **outside the product repo**, on a living-vs-append-only rule: living docs state what is true now; dated reports are never rewritten, only superseded |
| **3 — Research** | Competitor sweep (named players, prices, funding, honest strengths) · prior-art audit of every superlative · bottom-up sizing · product diagnostic reading your product as a hostile outsider would |
| **4 — Synthesis** | Positioning statement written as a hypothesis under test · a permanent banned-claims list · a narrative sequenced weakness-first · an objection pack with honest `unresolved` statuses · the claim ledger |
| **5 — Red team** | A kill memo in the persona of the skeptic who matters, the ten meeting-ending questions, the single load-bearing fact — then a patch loop that puts every finding back into the documents |
| **6 — Gates** | Numeric kill/GO criteria with dates, set in advance, movable only via a dated decision record. Zeros are reported as zeros |

The skill also tells the agent to **fan the research out across subagents** where the host
supports it, and to give the adversarial ones an adversarial mandate in writing — an agent told
to *evaluate* a claim finds support; an agent told to *kill* it finds prior art. The red team
runs as a separate agent that has seen only the finished deliverables, never your reasoning.

### What is in this repo

```
chanmeng-product-reality-check/
├─ SKILL.md                    the workflow: posture, three rules, six phases, failure modes
├─ references/
│  ├─ workspace-conventions.md directory layout, living vs append-only, decision records, staleness
│  ├─ competitor-research.md   the sweep, the competitor DB, the prior-art / uniqueness playbook
│  ├─ market-sizing.md         bottom-up sizing, "who would pay", pricing sanity checks
│  ├─ product-diagnostic.md    copy-vs-code contradictions, unit economics, evidence machinery
│  ├─ narrative-and-positioning.md  positioning, messaging, narrative, objection packs, ledgers
│  └─ red-team.md              the kill memo and the patch loop
└─ assets/
   ├─ competitors.schema.json  competitor DB schema (sources, verification dates, staleness)
   ├─ report-template.md       dated research report, incl. the mandatory falsification section
   ├─ claim-ledger-template.md claim · source · date verified · evidence grade
   ├─ kill-memo-template.md    "I pass because…", the ten questions, the load-bearing fact
   └─ viability-gates-template.md  numeric gates with dates and decision records
```

Reports come out in whatever language you are writing in; the internal templates are English.

## Scope and honest limits

- **It drives live web research**, so it needs a host with web search and fetch — Claude Code
  with those tools enabled, or any agent runtime that provides them. Without them it degrades
  into recall, which is exactly what the method exists to prevent.
- **Every result is point-in-time.** Prices change, companies pivot, platforms absorb
  categories. Findings carry `verified-on` dates and evidence grades (`[PAGE]` — read off the
  source · `[SNIPPET]` — a search result quoted it · `[UNVERIFIED]` — an aggregator asserts it,
  treat as false), and competitor entries go stale after 30 days on purpose. Do not lift a
  number out of a report without also lifting its grade.
- **It does not interview your buyers.** Everything it produces is desk research and reasoning
  from sourced evidence. Buyer archetypes are hypotheses with named falsifiers, not observed
  customers. The gates exist precisely because the research cannot settle demand on its own.
- **It is a decision aid, not an oracle.** The verdict always ships with the conditions under
  which it flips, and every template has a "what would prove this wrong" section — including
  the gates instrument itself.
- **Research costs tokens.** A deep engagement is search-heavy by design and fans out across
  subagents. If that matters, ask for the quick pass.

## Where the methodology came from

It is distilled from a real engagement: a solo founder with a shipped open-source compiler, a
commercial product on top of it, and effectively no customers. Over several weeks that work
produced a dozen dated research reports, a positioning doc whose central moat claim was refuted
twice and rewritten twice, a bottom-up sizing that concluded the exciting infrastructure
re-positioning relocated the ceiling rather than escaping it, a prior-art audit that killed the
words "first" and "only" permanently by finding a 1975 research language and three dormant
twins, and a kill memo that verified the headline traction number — accurate to the digit — and
found that two thirds of it sat on the founder's own release days. Every move in this skill is
one of those moves, generalized off that product and rewritten to work for any developer's.

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 Chan Meng.
