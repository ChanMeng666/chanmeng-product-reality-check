# Workspace conventions

The scaffold a research engagement lives in, and the two or three rules that keep it honest
as it grows. Set this up in Phase 2, before the first report.

## Where it lives

Create a **separate directory or repository** from the product. Two reasons that matter:

1. Strategy inside a product repo goes stale invisibly. Nobody rereads `docs/strategy.md`
   while shipping features, and six months later it describes a company that no longer exists.
2. The two hold different kinds of truth. The product repo is the authority on what the
   software does; the growth workspace is the authority on who it is for. When they disagree,
   you want to *see* the disagreement — that gap is the most valuable finding in the product
   diagnostic. Merging them hides it.

State the boundary explicitly at the top of the workspace's own instructions file: **zero
product truth lives here; link to the product repo, never restate its facts.** When a
positioning change requires a copy change in the product, that is a separate change over
there, noted here.

## Directory layout

```
<product>-growth/
├── CLAUDE.md              the workspace's own rules: living vs append-only, honesty rule,
│                          sourcing rules, data schemas, what this repo is NOT
├── strategy/
│   ├── positioning.md     LIVING — the source of truth for every claim shipped anywhere
│   ├── viability.md       LIVING — the numeric kill/GO gates; the go/no-go instrument
│   ├── master-plan.md     LIVING — the reasoning behind the gates (optional; the long form)
│   └── decisions/         APPEND-ONLY — dated decision records + README.md index
├── research/
│   ├── README.md          the index: report, date, area, status, superseded-by
│   ├── competitors/       APPEND-ONLY dated reports
│   ├── market/            APPEND-ONLY dated reports
│   └── red-team/          APPEND-ONLY dated adversarial reports and kill memos
├── data/
│   ├── competitors.json   entity data, one entry per competitor, each with last_verified
│   ├── channels.json      where the buyer actually is, and the promotion rules there
│   ├── metrics-log.csv    one row per week, time series
│   └── discovery-pipeline.csv   one row per prospect interviewed or attempted
├── discovery/
│   ├── interview-script.md      LIVING — the question set
│   └── interviews/              APPEND-ONLY — one file per interview
└── marketing/               (only when the engagement reaches messaging)
    ├── copy/messaging-library.md    LIVING — approved copy + the banned-claims list
    └── launches/                    launch drafts and a reusable checklist
```

For a quick pass, collapse this to three files: one competitor report, one positioning draft,
one list of what to go find out. Keep the dated filenames — they cost nothing and they are
what makes the next session able to trust or distrust the numbers.

## Living vs. append-only

This is the convention that does the most work. Write it into the workspace's rules file as a
table, so every future file has an obvious home.

| Kind | Paths | Rule |
|---|---|---|
| **Living** | `strategy/positioning.md`, `strategy/viability.md`, `marketing/**`, `data/**`, any narrative or objection pack | States what is true **now**. Edit in place. No changelog prose inside it. |
| **Append-only** | `strategy/decisions/**`, all dated `research/**` reports, `discovery/interviews/**` | Point-in-time records. **Never rewritten.** Supersede with a new dated file and a "superseded by" entry in the index. |

Why append-only matters: a research report is the evidence a decision rested on. Rewrite it
and you can no longer tell whether the decision was reasonable when it was made, or whether
the belief that drove it was ever checked. When a report turns out to be wrong, the correct
move is a new dated report plus a **cross-report corrections** section in the index — which
also gives you a running list of what this engagement got wrong, the single most credibility-
building artifact in the workspace.

Every dated file is named `YYYY-MM-DD-<slug>.md`. ISO dates everywhere, no exceptions —
"last Tuesday" and `08/03` are both unusable six months later.

## The research index

`research/README.md` is a table, maintained on every new report:

| Report | Date | Area | Status | Superseded by |
|---|---|---|---|---|

Plus, below it, **cross-report corrections** — a running list of the specific claims one
report killed in another, in one sentence each with both file names. When the same claim is
refuted twice, that is the signal it needs to enter the banned-claims list.

## Decision records

A decision record is written whenever a choice is made that later work will rest on: what
gets built, what gets said, what the thresholds are, whether to continue. `strategy/decisions/`
holds them, append-only, indexed in its own README with a `superseded-by` / `amended-by`
column.

Each record carries:

- **Title:** `YYYY-MM-DD — <the decision in one line>`
- **Status:** decided by whom, on what date, on the basis of which reports.
- **Trigger** — what prompted the decision. Include the original proposal *as proposed*, even
  when it did not survive; a record that only states the outcome loses the fact that the
  founder's first instinct was wrong, which is the part that teaches.
- **Decisions** — numbered, each specific enough to be checked later. "Retire the word 'only'
  from all copy, permanently" is checkable. "Be more careful with claims" is not.
- **Basis** — the evidence, with file references.
- **The honest status of this decision** — what remains unproven inside it.
- **Committed follow-up** — dated actions the decision requires. Check these at the start of
  the next session; unexecuted follow-ups are a finding, not an oversight.
- **What would reverse this** — the observations that would undo it.

The failure mode this catches is specific and common: a decision is recorded correctly and
never propagated to the artifacts it governs. A pricing decision that never reaches the
pricing page turns a strength (disciplined records) into evidence against the user, because
it proves they write decisions down and do not execute them. **At the start of every session,
grep the decision records for committed follow-ups and check whether they happened.**

## Data schemas

Machine-readable data goes in `data/`, JSON for entities and CSV for time series. Put the
schemas in the workspace rules file and treat them as the source of truth.

**`competitors.json`** — see `assets/competitors.schema.json` for the full shape. The three
fields that are always tempting to skip and never should be: `last_verified` (an ISO date),
`positioning_vs_you` (a sentence naming the actual difference, or "none found"), and the
kills-your-moat verdict (whether this competitor's existence refutes the user's central claim).

**Staleness rule:** any entry with `last_verified` more than **30 days** old is stale and may
not be cited without re-verification. Competitors ship. A moat claim built on a competitor's
missing feature has a shelf life measured in weeks, and the entry most likely to go stale is
always the one the moat depends on — so re-verify that one first.

**`channels.json`** — where the buyer actually congregates, with `promotion_rules`
(`banned | soft | allowed`) per venue. Many communities where a target buyer lives ban
promotion, market research, or AI-tool posts outright. Knowing this before writing launch copy
saves a ban and a reputation.

**`metrics-log.csv`** — one row per week, columns fixed in advance, appended never edited.
Include the metrics that decide the gates, not the ones that feel good. If a column is zero,
the row still gets written with a zero in it.

**`discovery-pipeline.csv`** — one row per prospect: `date_found, handle, channel, segment,
status, interview_file, key_insight`. Status moves
`identified → contacted → scheduled → interviewed → declined`. Declines are data.

## Privacy

Interview notes store a first name or handle and the source channel — nothing more. No email
addresses, no personal data beyond what is needed to follow up, no credentials, no revenue
exports, no API keys. A real personal email committed to a research repo is a finding against
the user in their own diagnostic.
