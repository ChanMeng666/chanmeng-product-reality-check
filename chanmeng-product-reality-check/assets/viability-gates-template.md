<!--
The go/no-go instrument. Save as strategy/viability.md - a LIVING document.

Set the thresholds BEFORE gathering the evidence they will judge. Thresholds move only via a
dated decision record in strategy/decisions/. Zeros are reported as zeros.
-->

# Viability - the go/no-go instrument

**Living document. Last updated YYYY-MM-DD.** The riskiest assumptions, the one piece of
evidence that decides everything, and the numeric kill / pivot / pass thresholds checked at each
review.

> **Thresholds change only via a dated decision record.** A weekly review must never quietly move
> a number to make a week look better. **Zeros are reported as zeros.**

---

## The one thing this turns on

<One sentence naming the single observation that would settle the question. Be specific about
WHO: e.g. "durable, PAID, REPEAT usage by non-network users who chose this over a free, faster
incumbent, observed within 90 days." Define "non-network" explicitly - not the founder, friends,
family, or anyone personally recruited - because that distinction is the whole point and
network-sourced signal counts toward nothing below.>

---

## Riskiest assumptions, ranked (most lethal first)

| # | Assumption we are betting on | If false... | Evidence source |
|---|---|---|---|
| **A1** | <the one that kills the business> | <what dies> | `research/...` |
| **A2** | <...> | | |
| **A3** | <the one that sets the clock: how long the advantage lasts> | | |

<One line: which of these decide whether this is a business at all, and which are execution
risks that merely block you from learning the answer.>

---

## Kill / pivot / pass criteria

All targets cumulative from <start date> unless noted. Each threshold carries a one-line
rationale so a future reader can judge whether it was calibrated or invented.

### Day 30 - instrument and start listening (checkpoint YYYY-MM-DD)

Mostly a **process** gate: the failure mode to catch here is not instrumenting and not talking
to users. A day-30 stop-check is never a business-stop - it means the method is wrong, fix the
method.

| Metric | PASS | WATCH | STOP-CHECK | Rationale |
|---|---|---|---|---|
| Customer conversations completed | >= N | | < N | <why N> |
| Instrumentation live (name the events) | all live | partial | none | Binary gate. Not tracking is the cardinal sin. |
| Activation rate among non-network users | >= X% | | < Y% | <why> |
| Paying non-network customers | >= 1 is a green flag (not required) | 0 | - | Too early to kill on. |

### Day 60 - is the pattern real? (checkpoint YYYY-MM-DD)

| Metric | PASS | PIVOT-WATCH | FAIL-WATCH | Rationale |
|---|---|---|---|---|
| Conversations (cumulative) | >= N | | < N | |
| Conversations where the core value appears **unprompted** | >= X% | | < Y% | This is the A2 test. If buyers do not independently raise it, it is a maker's value, not a buyer's. |
| Paying non-network customers | >= N | | 0 | |

### Day 90 - the decision gate (checkpoint YYYY-MM-DD)

Read the three columns as **GO / PIVOT / STOP**, decided **together** with a decision record,
never metric by metric.

| Metric | GO | PIVOT | STOP | Rationale |
|---|---|---|---|---|
| **Paying non-network customers (cumulative)** | >= N | | < N | The core count. |
| **Repeat signal** (second purchase OR referred a payer) | >= X% | | < Y% | Beats the generic one-time-buyer base rate with margin. |
| **Depth per customer** (median) | >= X | | < Y | |
| **Adjacent-segment signal** (the pivot's leading indicator) | >= N accounts | 1-2 | 0 | The pivot unlocks WITH evidence, not on a hunch. |
| Activation rate (sustained) | >= X% | | < Y% | |

**How to read the gate:**

- **GO** - <what it means concretely, and what changes next.>
- **PIVOT** - <the named pivot options, each with the signal that selects it. A pivot changes the
  shape, not the fact of continuing.>
- **STOP** - <what stops, and explicitly what does NOT. "Stop" usually means stop pouring
  full-time effort into this positioning, not delete the work.>

### Guardrail metrics (watched, not kill criteria)

- **<cost / latency / quality metric>** - <the threshold that means trouble, and the lever.>
- **<the leading indicator for the pivot lane>** - <what unprompted growth here would trigger.>

---

## What would prove this instrument itself wrong

- **The thresholds are too strict for this situation.** <e.g. if conversations are strongly
  positive but paid counts are near zero purely because there has been no launch yet, re-phase
  the paid thresholds to post-launch - via a decision record, not a silent edit.>
- **The window is too short to observe the real behaviour.** <name the proxy used instead, and
  what would show the proxy is a poor predictor.>
- **The gate over-weights one kind of signal.** <the scenario in which the numbers say STOP and
  STOP is the wrong read. The gate is a decision aid, not an autopilot.>
