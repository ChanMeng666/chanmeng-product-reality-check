<!--
Claim ledger. An appendix on every external-facing deliverable (narrative, deck, launch post,
landing copy). Build it WHILE writing, not afterwards - a ledger assembled at the end becomes an
exercise in finding sources for claims already committed to.

Rule: an unsourced claim is DELETED, not softened. "Roughly" and "we believe" keep an unchecked
assertion in circulation with a hedge attached.
-->

## Appendix - Claim ledger

Every externally checkable number in this document, its source, and when it was verified.
Internal product facts cite a repository path instead of a URL.

| Claim | Source | Verified |
|---|---|---|
| <the number or assertion, worded as it appears in the document> | <URL fetched, or `path/to/file.md` section> | YYYY-MM-DD |
| <a claim superseding an older figure> | <source> - **supersedes** the figure in `<older report>` | YYYY-MM-DD |
| <two facts that a reader might fuse - keep them as SEPARATE rows and say so> | <source>; **a separate measurement from the row above; never fused** | YYYY-MM-DD |
| <a claim two of your own reports disagree on> | <source A> vs `<report B>`; **the reports disagree; the disagreement is noted rather than resolved silently** | YYYY-MM-DD |

### Rules this ledger enforces

- **Every externally checkable number gets a row.** Before shipping, walk the document and check
  that no section carries numbers with no rows - that is the commonest ledger failure.
- **Stale claims carry `[last verified YYYY-MM-DD]` inline**, at the point of use, not only here.
  A measurement taken against a version of the product that has since changed is stale by the
  project's own rules; disclose it where it is read.
- **Never fuse two separately-sourced facts.** Two true numbers about different windows, joined
  into one sentence, produce a false number - and a reader who checks the striking version will
  find the arithmetic fails and stop reading.
- **Never silently take the larger of two disagreeing figures.** Note the disagreement.
- **Spot-check before shipping.** Pick a dozen rows at random and re-verify. The three failure
  shapes to look for: a fused pair, a self-disagreement resolved in the flattering direction, and
  a section with no rows at all.

### Spot-check record

| Date | Rows checked | Exact | Failures found | Fixed |
|---|---|---|---|---|
| YYYY-MM-DD | 18 | 15 | <what, in one clause each> | yes/no |
