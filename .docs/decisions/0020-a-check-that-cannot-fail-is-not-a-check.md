# 0020. A check that cannot fail is not a check

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`release.md`](../release.md) step 7, row V4, third command. It existed to guarantee one fact about
the repository: **at the moment before the tag, every run log named in `.docs/runs/README.md` exists
in the tree the tag will name.** The index is the only record of what each log is evidence for, and a
name in it with no file behind it is a citation to nothing.

**What it literally compared** was the set of filenames on lines of `.docs/runs/README.md` beginning
with 32 hex characters and exactly two spaces — the checksum block, hand-maintained in `md5sum`'s
output format — against `git ls-files` for each. It printed `NOT TRACKED: <name>` per failure and
**nothing at all otherwise**.

**Its output could not distinguish "every log is tracked" from "there was nothing to check."** Both
are zero bytes. Run against `v0.8.0`, whose tree has no `.docs/runs/README.md` at all, and against
`v0.16.0`, whose block names 99 logs that are all tracked, the two outputs are byte-identical and
both are empty.

**And that is not only historical.** On a scratch copy of `HEAD` with the block's two spaces changed
to one — 99 lines touched, every log still present and still tracked, no defect introduced — the
command again printed zero bytes. The key was a whitespace convention in a block a person maintains
by hand, and one `sed` blinded the check without altering a single fact it guards.

**How often it has fired, established by running it against all twenty tags rather than from the
record.** Once, at `v0.9.0`, on five names — and that one is a true positive: the index named five
logs the tree did not contain. It is also retrospective. The command was written into `release.md`
for `0.9.2`, in commit `5af7bf7`, *in response* to that defect, which had been found by hand. In the
nine releases where it was actually in force it has never fired. `v0.1.0`–`v0.8.0` produced the
vacuous pass, `v0.9.1`–`v0.16.0` a genuine one, and nothing in the output separated them.

**The fact is guaranteed nowhere else in step 7.** `git status --porcelain` sees a log present but
not added (`??`) and a tracked log deleted from disk (` D`); the ignored sweep sees a log present and
excluded by a rule. None of the three sees a name in the index whose file is neither on disk nor in
git, which is exactly the `v0.9.0` defect. V1 lists this release's changed files and would not show a
log named by an earlier one. Nothing else reads `.docs/runs/README.md`.

## Decision

**A check that cannot fail is not a check, and the remedy is a second side, not a louder warning.**
Where a row reads one artefact and reports what it did not find, silence is its pass and silence is
also its blind spot. Giving it a second, independently-derived side makes the two outcomes different
objects rather than different readings of the same empty string.

**Razor [`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md): the command stays,
and is repaired.** Removal was on the table on its merits and is rejected on the record. It has one
true positive across twenty tags against V3's zero; the defect it caught produced a bad tag that
nothing else in the step would have caught; and the artefact it guards is hand-maintained and has
grown from 5 names to 99, which is where a clerical omission hides. This is the opposite shape from
[`0019`](0019-a-check-compares-fields-not-prose.md), where the half with a record of catching nothing
was cut. The record decided both, in opposite directions.

**The key stays; the vacuity goes.** The checksum block's format remains what the index is read by —
it is the only machine-readable form the index has. What changes is that the other side now comes
from `git ls-files` rather than from nothing. A person can still break the key by reformatting; they
can no longer break it *silently*, because the tree's count does not move when the block's format
does. A blinded key now reads `0 named, 99 tracked` and lists every log.

**Every outcome prints a line, and the lines are labelled.** A pass is two equal counts with no names
under them. Nothing to check is `0 named, 0 tracked`, which says so in words. The reader never has to
remember which column they are looking at, which was the whole complaint.

**`TRACKED, NOT NAMED` is declared in scope, and it is the mechanism.** A committed log the index does
not name is invisible to every other command in the row, because the log is committed and
`git status` is clean. It is the same failure read the other way: an undocumented log is evidence
nobody can date. And without it the reformat case reports a bare count mismatch with no names, which
is a weaker failure than the one the repair exists for.

**What the row still does not do.** `git ls-files` reads the index, so a named log that is tracked
but deleted from disk passes this command; the first command in the same row prints ` D` for it. The
three are read together, and that was confirmed by running it rather than asserted.

## Consequences

**The predictions were written before the edit existed**, in
[`release-v4-tracked-logs.md`](../predictions/release-v4-tracked-logs.md), and all five held: the
tree as it stands prints `99 named, 99 tracked` and nothing else; the reformatted block fails with
100 lines; a removed log fails naming it; a tracked log the block does not name fails naming it; and
across twenty tags `v0.9.0` still fires with its five names while every tag from `v0.9.1` on passes
with equal counts.

**An unregistered control found a defect in the repair before it was committed, and this is the fifth
time in this project's log that a check's defect surfaced that way rather than by review.** The first
version resolved both sides to bare filenames, `sed 's|.*/||'`. A log moved into a subfolder of
`.docs/runs/` with the block still naming it by its bare filename therefore **passed** — a case the
old command caught, because `git ls-files .docs/runs/<name>` resolved the name against that directory
exactly. The repair had quietly lost coverage the thing it replaced already had. It now strips only
the `.docs/runs/` prefix, and that arm fails naming both sides:

```text
runs index: 99 named, 99 tracked
NAMED, NOT TRACKED: 2026-08-30-v3-aM1.log
TRACKED, NOT NAMED: 2026/2026-08-30-v3-aM1.log
```

**The counts are equal there and the sets disagree**, which is why the count line alone is not the
check and the two labelled lists earn their place. **The command shipped is not byte-identical to the
command pre-registered**: they differ by that one `sed` expression, changed after P1–P5 had been run
and re-run against the corrected form. Recorded here rather than by editing the prediction.

**The step grows, and the amount was measured.** `release.md` goes from 138 non-blank lines to 145.
The command block is 3 lines before and 5 after; V4's commentary goes from 3 lines to 8. Principle 7
asks what was removed in exchange and the honest answer for this pass is nothing. The argument lives
here instead of beside the command, which is the only reason the growth is 7 lines and not 12.

**The rule generalises, and two rows in this same file share the class.** V1's `$PREV..HEAD` yields an
empty diff — *"this release changed nothing"* — if `git describe` fails and `$PREV` is empty, and V2
prints nothing at all if the two field labels it greps are ever reworded. Both were demonstrated, not
argued, and neither is touched here.
