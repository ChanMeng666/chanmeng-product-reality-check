# Product diagnostic

Read the user's product the way a hostile outsider reads it: the live site, the pricing page,
the README, the code that makes a promise, and the numbers they quote. The deliverable is a
ranked list of what damages the story, with evidence, a fix, and an effort estimate.

Run this even when the user only asked about the market. A pricing page that contradicts
itself poisons every number they present afterwards, and it is a ten-minute fix.

## What you are hunting: contradictions

Findings come from gaps between two things the user has already written. Check every pair:

**Marketing copy vs. code.** Read the pricing page and then read the code that implements it.
This is the highest-yield check in the diagnostic. A landing page promising three free
generations against a service that grants one is not a copy nit — it is a false promise about
money that any non-technical reader can verify in thirty seconds without repo access, and the
conclusion they draw is not "sloppy" but "this person's numbers are decorative."

**A page vs. itself.** Headlines, feature bullets, FAQ and footer are written at different
times by different moods. Read the whole page for internal consistency: a hero that promises
an export the pricing tiles omit, a tier list where the paid plan appears to lose a feature.
The buyer cannot tell what they are paying for, and the differentiator goes missing from the
purchase decision.

**Copy vs. the user's own doctrine.** If the workspace has a positioning doc or a banned-claims
list, grep the live site against it. Finding the landing page leading with a claim the user's
own research already refuted is the most damaging single class of finding, because it proves
the discipline is performative — they knew and shipped it anyway.

**Decision records vs. what happened.** Every committed follow-up in every decision record is a
checkable assertion. Unexecuted ones are findings. The pattern to name explicitly: *decisions
get written and not propagated* — which converts the user's genuine strength (rigorous records)
into evidence against them.

**Claims vs. capability.** What does the product actually do, versus what the headline implies?
Overclaims cluster around regulated or consequential outcomes — safety, compliance, legality,
medical, financial, "ready to use for X." These are simultaneously dishonest and strategically
fatal: they invite the "you still need the professional anyway" rebuttal on the skeptic's
terms. The honest reframe usually converts the ceiling into the actual job: *"get a solid
starting point for $10 so that when you do pay the professional $1,750, you are paying them to
finish something real rather than to figure out what you want."*

**Docs vs. docs.** Two living documents disagreeing on a fact about a competitor, or an
operational doc stating the opposite of its own operating flow, means neither can be relied on.
Low severity individually, corrosive in aggregate.

**Repository hygiene against the user's own rules.** A real personal email committed as a test
account, credentials in a config, dev pointed at the live database holding user data, retired
URLs still linked from the live site. Each is small; the pattern is what reads badly.

## Unit-economics honesty

The margin most indie developers quote is computed on the billed event alone. It is almost
always wrong, and the correction usually matters more than any marketing fix.

**Compute fully loaded, per completed customer journey, not per billed action.** The exposure
lives in the *free* actions surrounding the paid one: the retries, the edits, the previews, the
regenerations, the support. A product can be at 90% margin on the charged action and 50–70%
fully loaded across a realistic session — and the second number is the business.

**Enumerate every cost path, including the ones nobody looked at.** Grep the codebase for every
outbound paid API call and check each against the cost model. There is nearly always one that
was never costed — a transcription endpoint, an image resize, a webhook retry storm.

**Check the backstop.** "We have rate limiting" deserves a look at the implementation. An
in-memory limiter that resets on deploy is not a spend cap. Ask: what is the worst a single
paying customer can cost in a day, and what stops it? If the answer is "nothing, but nobody has
done it," that is a real finding on a live payments product — worth an alert, not necessarily a
hard cap.

**Distinguish an accounting artifact from a property of the business.** A margin that only
holds if users behave in an unmeasured way is a hypothesis. State the assumption it rests on
and whether any telemetry exists to confirm it. Usually none does, and the break-even point
(e.g. "roughly 20–35 free edits per paid credit") is worth computing so the user knows what to
instrument.

## The evidence machinery

The most common finding in a diagnostic of a pre-traction product: **the instrument was built
and abandoned.** Empty metrics files, header-only CSVs, an empty interviews directory, an
analytics package that was never installed, and a self-imposed checkpoint arriving in two
weeks whose instrumentation row is a binary pass/fail currently reading FAIL.

Check, and report the zeros as zeros:

- **Is there any product analytics at all?** If not, every funnel question is unanswerable —
  which means no gate that depends on a funnel number can be evaluated, no matter how carefully
  it was written.
- **Which four or five events would answer the questions the gates ask?** Name them. This is
  usually a day of work and unblocks everything downstream.
- **Can any of it be reconstructed retroactively** from an existing database? Often yes, via a
  SQL view over rows that already exist. Say so — it turns "we have no data" into "we have data
  as of two hours from now."
- **Have any customer conversations happened?** Count them. Zero is a finding, and it is
  usually the real explanation for "why is nobody using my product."

## Real metrics versus vanity metrics

Decompose every number before it is quoted anywhere. The default composition of a flattering
metric is not what the framing implies:

- **Downloads / installs** — split by day and check what falls on the user's own release days
  and CI runs. In one real engagement, 66% of a package's monthly downloads sat on five of the
  maintainer's own release days, three weeks of the window were all-zero, and the remaining
  baseline was declining. The headline was accurate to the digit; the story it was telling was
  false. For a library, **dependent count** is the metric that means what downloads pretend to.
- **Signups** — how many are the user, their friends, and people they personally recruited?
  Define "non-network" explicitly and count only those. This distinction is usually the whole
  point of the gate it feeds.
- **Stars / followers / impressions** — measure interest in a post, not demand for a product.
  Useful for channel selection, useless as validation.
- **Traffic** — separate referral spikes from a launch, from a baseline. A launch spike tells
  you the post worked.
- **Revenue** — report the count of *distinct non-network payers* alongside the dollar figure.
  A number without its denominator is uninterpretable, and a plausible-looking total can be one
  friend buying five times.
- **Usage totals** — divide by days and by users. "43 generations over 25 days including the
  founder's own QA" is a very different sentence from "43 generations."

Any number that survives decomposition is worth quoting and carries far more weight for having
been decomposed in public.

## Writing the report

Use `assets/report-template.md`. Structure specific to this report type:

**Executive summary** — the single most damaging *pattern*, not the single worst item. Patterns
change behaviour; individual bugs get fixed and recur. Typical patterns: decisions recorded but
never propagated; claims the user's own doctrine already refutes; an evidence machine built and
abandoned.

**Top N must-fix, ranked by narrative damage — not engineering effort.** For each: the evidence
with file paths and line numbers, **what the outsider concludes** (this is the field that makes
a finding land — not "the copy is wrong" but "this founder writes decisions down and does not
execute them"), the fix, the effort, and a **blocks-outsider-reading: yes/no** flag.

**Cheap fixes that materially improve the story inside a week.** Order by ratio of narrative
improvement to hours. Most diagnostics find that the top three findings are under an hour each
— which is the encouraging half of a discouraging report, and worth stating.

**Full findings table** with severity: **H** = an outsider changes their mind about the person.
**M** = it costs credibility in the room. **L** = a nit that accumulates. Columns: finding,
severity, verified-in, what-the-outsider-concludes, fix, blocks-reading.

**Corrections to the briefing that prompted this report.** If the user's framing of their own
situation was wrong in a way the investigation revealed, say so here. Some findings are also
*better* than the briefing implied — a risk that turns out to have a documented, defensible
reason behind it should be reported as "write the one-paragraph version so a diligence reader
finds the reasoning before they find the risk."

**What would prove this wrong.** As always.
