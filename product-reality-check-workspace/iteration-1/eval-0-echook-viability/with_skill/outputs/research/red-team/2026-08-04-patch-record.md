# Patch record — red-team findings, 2026-08-04

**APPEND-ONLY.** The kill memo (`2026-08-04-kill-memo.md`) is **not** rewritten to reflect these fixes.
The record of what was found is worth as much as the fixes. This file records which findings were
patched into the living documents and which stand as open evidence.

The research reports (`competitors/`, `market/`, `product/`) are dated point-in-time records and were
**not** edited. Where a report contains a figure this record corrects, the correction lives here, in
`research/README.md`, and in the living documents — never by overwriting the report.

---

## PATCHED

| # | Finding | Where it landed |
|---|---|---|
| **R1** | The quote *"Skills are authored for agents rather than humans"*, cited `[PAGE]` in five documents, **does not appear on the cited Anthropic page** (143,670 bytes, zero hits; two other quotes from the same citation matched exactly). | Citation **withdrawn, not softened**, in `VERDICT.md` §1 with the withdrawal shown in place; ledger row 32 struck and marked FAILED; BC-1 rewritten to stand on the 601,280 `SKILL.md` files and peon-ping. |
| **R2** | **The worst finding.** S1 ("per-event granularity") was stated against the wrong comparator. Anthropic's *mobile push* has two toggles, but the **hook** surface echook runs on ships eight `Notification` matchers including `agent_completed` and `agent_needs_input`. The falsifier `positioning.md` called "the single most likely event on the list" **had already fired**, the competitor sweep's own scorecard said `ABSORBED`, and the friendlier fact was in the headline, the positioning statement *and* the approved-copy list. | **Verified independently by me** at `code.claude.com/docs/en/hooks` before patching. S1 rewritten in both `VERDICT.md` and `positioning.md` with the error shown struck rather than deleted; the positioning statement's "Unlike" clause rebuilt; approved-comparison sentence withdrawn; new **BC-13**; ledger row 24c added. |
| **R3** | "Chime requests: zero issues" is **false** (search returns 2), asserted in four documents. | Removed from `VERDICT.md`, `positioning.md`, ledger row 24; new **BC-14**. The finding was *strengthened* by the red team's full-population check (all 38 sound issues ≈ 68 reactions) — added as rows 24a/24b. |
| **R4** | "2,016 stars across nine projects", sold as checkable in a minute, does not reconstruct — the seven enumerated total **1,770**. And "convergent invention is evidence the gap is real" is asserted where the source report says *do not assert either direction*. | Both struck in `VERDICT.md` with the correction stated in place; ledger rows 35a/35b marked FAILED; new **BC-15**. |
| **R5** | Clutch figure mis-transcribed as **$49,999**; the page says **$49,000**. Propagated to 11 sites across 6 files. | Corrected in all four living documents. Left uncorrected in the two dated research reports by the append-only rule, with the correction recorded here and in the ledger. |
| **R6** | **The methodological double standard.** A 40×–100× exists-vs-reachable discount was applied to the product pool being killed, and **no discount at all** to the consulting lane being sold — which is priced off one page of *agency* data with undisclosed sample size. The package's own rule bans an unsized lane carried at full visual weight. | `VERDICT.md`'s one-sentence verdict rewritten to label the consulting lane **explicitly unresearched**, name the agency/solo gap, and state the sin by name. |
| **R7** | `VERDICT.md` called the maintainer lane "the one thing here that has never been measured" while the same document listed five other unmeasured things. | Corrected in the verdict sentence. |
| **R8** | **Undersold:** issue **#73384** — "built-in distinct notification sounds for 'needs input' vs …", echook's pitch almost verbatim — has **zero reactions**, and was buried as an anonymous zero. | Promoted into `VERDICT.md`'s demand section as the sharpest single data point; ledger row 24b. |
| **R9** | **Undersold:** the maintainer shipped `SYNTHETIC_VARIANT_DEFAULTS` **off**, with a comment recording that he could not observe the events firing — refusing to claim a feature he could not verify. Buried fourteen findings deep; the VERDICT's version was the generic "292 tests, three-OS CI." | Added to `VERDICT.md` §"What this document does not say", named as better evidence than any metric in the package and as material for the maintainer-track write-up. |

## STANDING AS OPEN EVIDENCE — not patched

| # | Finding | Why it stands |
|---|---|---|
| **O1** | The package spends its evidentiary budget proving a proposition nobody disputes (a 78-star MIT utility with no payment rail is not a business) and hands the recommendation to an unresearched lane. | **Structurally true and not fixable by editing.** Fixing it requires *researching the consulting lane* — a second engagement, not a patch. Recorded in the decision record as the named next piece of work. |
| **O2** | The demand finding and the donation base rate rest on small samples (a handful of issues; 15 Open Collective ledgers). | Partly mitigated by R3's full-population re-check, which moved the demand finding from n=4 to n=38. The donation base rate remains small-sample and is now labelled as such at point of use. |
| **O3** | Cursor's in-app sound setting is `[UNVERIFIED]`; Reddit was blocked to the research agents; "people just alt-tab" was searched for and not found. | Disclosed as gaps in `VERDICT.md` §"What I do not know" and ledger rows 50–52. Cannot be closed this session. |
| **O4** | Every gate threshold was set by an outside analyst; the owner's own stopping condition was never recorded because there was no live intake. | Disclosed in `viability.md` §"What would prove this instrument wrong". **Only the owner can close this**, and it is listed below. |

---

## Actions only the owner can take

Marked **blocking** where an outsider should not read the package until they are done.

1. **State your own stopping condition** — the gates are currently an outsider's guess. *(blocking for any decision, not for reading)*
2. **Run G1**, the $5 licence test. Nothing in this package substitutes for it.
3. **Verify the Cursor sound setting** from inside Cursor — it is `[UNVERIFIED]` and no Cursor-gap copy may ship until it is checked.
4. **Fix the six shipped surfaces** that state a wrong hook count, and the stale version string. *(blocking — the live README currently violates six of this workspace's own banned claims, which is the most damaging class of finding in the method)*

---

## What the patch loop did not resolve

The kill memo's structural verdict stands: **the package is better at killing the product than at
establishing the alternative.** That asymmetry is now stated in the VERDICT's own voice rather than left
for a reader to discover, which is the honest fix available in one session — but it is a disclosure, not
a remedy. The remedy is to research the consulting lane with the same instruments used on the product,
and that has not been done.
