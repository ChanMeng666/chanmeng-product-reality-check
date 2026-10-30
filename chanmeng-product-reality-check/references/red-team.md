# Red team: the kill memo and the patch loop

The final pass on any deliverable. A skeptic persona attacks the finished package, produces a
memo, and every finding either patches a document or becomes an honest unresolved row. Nothing
survives as a note in a memo nobody rereads.

## Setting it up

**Pick the specific skeptic who matters.** Not "a critic" — the actual person whose "no" would
hurt: a seed partner with a domain operator on staff, mandated to say no. A senior engineer in
the target field reading a Show HN post. The buyer's manager who has to approve the purchase.
The persona determines which attacks land, and a generic skeptic produces generic findings.

**Give the persona a hostile mandate in writing.** "Your job is to kill this" produces prior
art and contradictions; "evaluate this" produces a balanced summary nobody acts on. If running
this as a subagent, put the mandate in the prompt and give it only the *finished deliverables*
— not your reasoning, not the research that produced them. A red team that watched the argument
being built will not attack it properly, because it already believes the framing.

**Give it the whole package and the underlying evidence**, so it can check claims against
sources rather than just disliking them. The memo's authority comes from verification, not
from tone.

## The memo

Use `assets/kill-memo-template.md`. Six required parts.

### 1. "I pass because ___"

One paragraph, first person, in the skeptic's voice, listing every independent reason —
each phrased as a complete reason on its own. Written as prose, not bullets, because prose
forces the reasons to be connected rather than itemized and dismissed one at a time.

This section's value is that it is quotable back at the user. It is the paragraph they will
reread. Make it accurate, not cruel: every clause must trace to something checkable in the
package.

### 2. The ten questions that would end the meeting

A table: the question, **the founder's honest answer today**, and how the objection pack covers
it (`covered` / `partial` / `MISS`).

The honest-answer column is what makes this useful. A question the user can answer well is not
a threat; a question whose honest answer is "I don't know" or a number they have never stated
is. Rank by how badly the honest answer lands.

Every `MISS` becomes a new numbered entry in the objection pack, same day.

Note the pattern where an objection is *covered but fatally placed*: the real number appears in
an appendix while a more flattering one is on the headline slide. That is a MISS in practice.

### 3. The single load-bearing fact — checked

Identify the **one externally checkable fact that, if false or differently composed, poisons
everything else** in the package. Then actually go check it, during this session, against the
primary source. Report what you found.

This is often the highest-value five minutes of the entire engagement. In one real case the
fact was a package's monthly download count. It verified exactly — and the daily series showed
five of the maintainer's own release days carrying 66% of the total, three weeks of zeros, and
a declining baseline. The headline was honest to the digit and the framing was wrong. The
package was patched to carry the decomposition, which made the remaining number *more*
persuasive because it had been stress-tested in public.

Pick the fact by asking: which number, if it evaporated, would take the most other claims with
it? Usually it is the one traction number, the one price anchor, or the one comparison.

### 4. The three numbers that would change the skeptic's mind

Specific, measurable, with thresholds and durations — not "more traction." Each should name
what is measured, how much, over how long, and by what instrument.

Expect these to **disagree with the user's own gates**, and say so when they do. A gate written
to prove a product works and a number written to prove a business exists are different
instruments; discovering that fully satisfying the user's go-criteria amounts to a trivial sum
of revenue is itself a finding, and one the user needs before they mistake one instrument for
the other.

### 5. Required attacks

Work through a fixed list so nothing is skipped, and report findings per attack:

- **Traction and inevitability leaks** — every sentence that implies momentum without a number
  behind it. "Live and taking payments" in a document that prints zeros elsewhere. A ratio
  framed as vitality. A law asserted from one instance. A superlative restored under paraphrase
  in violation of a banned-claims list. An unexploited-opportunity framing that is more likely
  evidence of no demand (a public API with three years and no builders is a finding *against*).
- **Ledger integrity** — spot-check 15–20 rows against sources. Report the exact/failed count;
  a high pass rate is itself a reportable strength. Look specifically for fused facts,
  self-disagreements resolved in the flattering direction, and sections with no rows at all.
- **The analogy's weakest joint** — if the narrative rests on an analogy, find the joint that
  does not transfer. It is rarely the obvious one. Frequently the mismatch is between *who
  produces* and *who accepts*: a substrate whose adopter never reads it has no adoption
  mechanism of its own, whatever its authoring advantages.
- **The moat under its own logic** — take the thesis's central premise and push it one step
  further than the document does. The property that makes a thesis plausible is often the same
  property that makes it uncapturable, and the package rarely notices that its bull case and
  its moat case are the same sentence pointing in opposite directions.
- **Every stated condition or path** — check each against its own falsifier and against the
  other documents. Common results: a comp that is structurally wrong for the comparison, a
  falsifier that has already fired, a condition that is a restatement of another dressed as a
  separate path, and an unresearched lane carried at full visual weight.
- **Founder, structure and diligence risk** — anything acknowledged-but-unpriced. For many
  readers, acknowledged-and-unpriced is worse than unmentioned, because it proves the user knew
  and did not do the work. Legal exposure on a live product taking money is a finding, not a
  copy fix.
- **Evidence quality** — sample sizes, significance, whether a measurement is stale by the
  user's own re-measurement rule, whether the judge or instrument is the user's own, whether
  the thing measured still exists. Compute the significance rather than describing the effect
  in words; "+4 out of 26 on each metric, overlapping intervals, p ≈ 0.06" is the honest
  framing and it survives, where "more than doubles" does not.
- **Internal consistency** — two documents disagreeing on a number; a stop threshold quoted
  verbatim while the go threshold appears nowhere; a headline figure that contradicts a figure
  in the appendix.

### 6. Verdict on the honesty posture

Judge the disclosure itself, in three parts:

- **What works** — name it specifically. Scope stated before claims, retired claims shown
  struck rather than deleted, append-only records, refusing to claim a result in either
  direction when the experiment was not run, disclosing the user's own failure to execute their
  own decision. None of this reads as surrender: **readers punish discovered weakness, not
  disclosed weakness**, and after a thorough disclosure there is almost nothing left to
  discover.
- **Where it crossed into overclaiming** — the specific leaks, now fixed.
- **Where it undersold** — the genuinely strong work that appears nowhere. This is common and
  worth as much as the criticism: the best-evidenced result in a repository sitting as a
  sidebar to a weaker headline number; a substantial engineering estate with no slide; the one
  concrete piece of evidence for a named lane mentioned nowhere.

Then the **structural verdict** — the thing no amount of honest writing fixes. State it
plainly, and state what follows from it. If the honest conclusion is "do not take this to
anyone yet; go get these three numbers first," that is the recommendation, and it is a
service.

### And: what would prove this memo wrong

The red team gets no exemption from the honesty rule. List what would show the memo's own
attacks were miscalibrated — a discount that was too harsh, a significance test that would
flip under the correct pairing, a reader who engages seriously with the unpatched package
anyway.

## The patch loop

Findings do not count until they land in a document. Same session:

1. **Patch what is patchable.** Fix the leaks, print both thresholds, add the missing ledger
   rows, unfuse the fused facts, add the decomposition to the headline number, state the
   uncomfortable implication in the package's own voice rather than leaving it for a reader to
   discover.
2. **Convert what is not patchable into honest status.** New objection-pack entries marked
   `unresolved` with named falsifiers; conditions marked `falsified — pending contrary
   evidence`; lanes marked `explicitly unresearched`.
3. **Record which is which.** The memo is append-only: mark each finding `PATCHED` or leave it
   standing as open evidence. Do not rewrite the memo to reflect the fixes — the record of what
   was found is worth as much as the fixes.
4. **List the actions only the user can take**, separately and explicitly: re-run a stale
   measurement, state a revenue number, price a legal or structural exposure, get one
   qualified outsider's recorded judgment of the output. Mark these as blocking if the package
   should not be read by an outsider until they are done.
5. **Write a decision record** if the memo changes strategy, not just documents.

## Frequency

Once per major deliverable, and again whenever the central claim changes. A red team on
unchanged documents produces the same memo; a red team on a package that has absorbed the last
one produces new findings, because the fixes create new surfaces.
