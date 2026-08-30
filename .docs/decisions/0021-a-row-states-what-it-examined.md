# 0021. A row states what it examined

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`release.md`](../release.md) step 7, rows V1 and V2. Both pass vacuously, and both were demonstrated
rather than argued.

**V1.** `PREV=$(git describe --tags --abbrev=0)` fails in a tree with no tag reachable from `HEAD`,
leaving `git diff --name-only $PREV..HEAD`, which the shell expands to `git diff --name-only ..HEAD`
and git reads as `HEAD..HEAD`. On a `--no-tags` clone of this repository it exits **0** printing
**zero bytes** — the same output as a release that touched nothing, read against a criterion that
asks whether every file the changelog claims is in the list. `git describe`'s `fatal:` on stderr is
the only thing separating them, and the step's own instruction is to read the evidence, of which
there is none.

**V2.** On a scratch copy of `HEAD` with `Version:` lowercased in all six blueprint `README.md`s —
12 lines touched, every number still correct, no defect introduced —
`grep -rn "Blueprint Version:\|Framework Version:"` prints **zero bytes**.

**The partial case is worse than the demonstrated one.** With only `**Blueprint Version:**` reworded
to `**Blueprint Ver:**` in all six, V2 prints six `Framework Version` lines that look perfectly
healthy, and **every `Blueprint Version` in the framework has silently left the check**. Zero bytes
is at least visibly odd. This is not.

**How much of it is guarded elsewhere, checked rather than assumed.** V3 catches the *full*
rewording — `grep -L` finds its string in no file and lists all six blueprints. V3 does **not** catch
the partial one; run against that tree it printed `CHANGELOG 0.16.0` and listed nothing, because V3
never reads `Blueprint Version:` at all. **Nothing in step 7 reads that field but V2.** And nothing
in step 7 touches `$PREV`, so V1's case is unguarded outright.

## Decision

**Every row states positively what it examined and how much of it, and it is one requirement for the
step rather than a clause per row.** The class is the same in V1, V2 and the two repaired the same
week: a row that prints only its failures cannot tell a clean pass from an examination that never
happened, because both are the empty string. Written per row it would have been said four times in a
file that had grown from 138 to 145 non-blank lines with nothing removed. It is stated once, in the
paragraph a session reads immediately before running the block.

**The sentence does not repair the commands, and that was not expected of it.** No prose makes
`git diff --name-only $PREV..HEAD` print its range. Both commands changed. What the requirement buys
is that the change is one rule with four conformances instead of four unrelated patches, and that its
justification stops being copied into each row.

**The line is not the verdict.** It says there was something to read; the reading is still the
reader's. That distinction is in the step's wording because a control tested exactly the risk of
losing it — see below.

**V1 and V2 are one change.** They share the class and not the mechanism: V1's is a variable that can
be empty making a range degenerate, V2's is a literal key that can drift out of the document. If the
mechanisms were the deliverable they would be two. The deliverable is the requirement, which belongs
to neither row, and splitting would mean writing it twice or hanging it arbitrarily on whichever went
first. There is no build here to bisect. **The cost is that a wrong repair to one lands in a commit
with the other**, and it was paid down by verifying and reporting each row's arms separately — which
is how the one defect in this pass was found and fixed before the commit.

**What came out in exchange, under principle 7.** Two passages that existed only to say per row what
the requirement now says once, or to restate a linked record verbatim:

- V4's *"The third prints a count line in every outcome"* and the four lines of history after it,
  which are [`0020`](0020-a-check-that-cannot-fail-is-not-a-check.md)'s Context quoted inside a row
  that already links to it. That row goes from 9 non-blank lines to 7.
- V3's *"It compares two fields because it used to grep prose. The old row matched a fixed phrase in
  the backlog. It fired five times, caught nothing…"*, the same from
  [`0019`](0019-a-check-compares-fields-not-prose.md). That row goes from 11 to 10.

**And the accounting, honestly.** The step goes from **145 non-blank lines to 158**, +13. The V1 and
V2 command lines go from 5 to 11; V1's commentary 9 to 11 and V2's 9 to 12; V3's and V4's come down
by 3 between them. Principle 7 asks what was removed in exchange and the answer is 3 lines against
19 added. The argument is in this record and not beside the commands, which is why it is 13 and not
30, but it is still a step that grew. The queued subtraction pass over step 7 inherits a larger file
than it was promised.

## Consequences

**Pre-registered in
[`release-v1-v2-positive-output.md`](../predictions/release-v1-v2-positive-output.md)** before the
edit existed. Six arms and three controls.

**P1, P2, P3a, P3b and P4 held.** No previous tag prints `V1 range NO-PREVIOUS-TAG..HEAD, 0 files
changed` under two `fatal:` lines, where the old command printed zero bytes and exited 0. A normal
release prints `V1 range v0.16.0..HEAD, 8 files changed` above the list. Both labels reworded gives
`6 blueprint READMEs, 0 with Blueprint Version, 0 with Framework Version`; the `Blueprint` label
alone gives `0 … 6`, above the six lines that look healthy. The tree as it stands gives `6, 6, 6`.

**P5 falsified its own prediction, and the falsification is the best finding in this pass.** It was
registered that *"V2 fires at no tag whose tree has blueprint `README.md`s."* **V2 fires at ten of
the twenty tags**, `v0.1.0` through `v0.10.2`, and every one is a **real omission**:
`blueprints/setup/README.md` shipped for ten releases carrying no `Blueprint Version` at all, and
`blueprints/checks/README.md` for the first two. `0.11.0`'s own changelog records it — *"A `Blueprint
Version` for `blueprints/setup/`, which had never had one, so no release could record"* — so it was
found by hand, years of releases late, and the old V2 could never have found it, because **a file
that contributes no lines to a `grep -rn` is invisible without a count of the files themselves.**

**All ten firings are retroactive**, since the count line did not exist. But they are a different
kind from `v0.9.0`'s, and the difference matters to [`0020`](0020-a-check-that-cannot-fail-is-not-a-check.md)'s
corrected basis. `v0.9.0`'s defect was found by hand and the command written afterwards in response
to it. This one was **not the case the repair was written for** — the repair was aimed at reworded
labels — and the omission fell out of the denominator on its own. A retroactive true positive the
instrument was not shaped around is evidence the instrument reads something real. Live true positives
remain zero for every row in this step.

**V1 fires once in twenty tags, at `v0.1.0`**, which has no previous tag. True, retroactive, and
arguably vacuous by nature rather than a defect: there was genuinely no release to diff against. The
old command printed nothing there and the new one names the range.

**C1 held after being corrected twice, and both corrections were mine, not the command's.** Run
against all twenty tags, the repaired V1's file list is identical to the old one at every tag and the
repaired V2 prints exactly the old lines plus its count line. The first sweep reported a difference at
`v0.1.0`; the sweep was wrong, not the command — it substituted the tag for `HEAD` in the range and
left the old form's empty left side resolving against the real `HEAD`. Rerun with each tag deleted and
its commit checked out detached, which is the state step 7 actually runs in, it agreed. The second
sweep reported a difference at 19 of 20 tags, which was **ordering only**: `grep -rn` returns these
six files in a different order on repeated identical invocations of the *unchanged* command. Compared
as sets, all twenty agree.

**C2 held, and it is the arm that justifies one sentence of the step's wording.** A tree with every
label intact and one blueprint's `Framework Version` set back to `0.15.0` prints `6, 6, 6` — a
passing count line above output containing a real defect, which V3 catches and the count line does
not. That is correct and is the whole point: **the positive line says there was something to read, not
that what was read is right.** Had the count been allowed to read as a verdict, the repair would have
replaced a check that said nothing with one that says the wrong thing, which is worse than what it
replaced. The step says so explicitly for that reason.

**C3 held, and it covers the case the sentinel does not.** With a stray tag on an older commit,
`git describe` resolves to a real tag that is not the previous release. Nothing fails, the count is
non-zero, and the row prints `V1 range v0.16.1-hotfix..HEAD, 5 files changed`. The wrong baseline is
invisible in a list of filenames and visible in the range, so printing the range bought something
over printing a count.

**An unregistered control found a defect in the repair after every registered arm had held. That is
the sixth time in this project's log, the second consecutive change, and the first application of the
rule added to [`../handover.md`](../handover.md) in this same pass.** With no `blueprints/*/README.md`
in the tree, `BPR` is empty, and `grep -l 'Blueprint Version:' $BPR` receives no file operand and
**reads stdin**. Run the way an operator runs step 7 — pasted into a terminal — it blocks
indefinitely. Confirmed with stdin held open: `rc=124`, timed out. The case it hangs on is
`0 blueprint READMEs`, which is precisely the *"there was nothing to check"* outcome the whole
requirement exists to make visible. The repair deadlocked on the vacuity it was written to expose.

**The command shipped is not byte-identical to the command pre-registered.** Both `grep -l` calls
gained a `/dev/null` operand, which can never match and forces a file list to exist. P3a, P3b, P4,
P5's twenty tags, C1 and C2 were re-run against the shipped form and all agree with what is recorded
above. The prediction file was not edited.

**Three things found and deliberately not acted on.**

- **Step 2 of this same file says "all four blueprint READMEs" and there are six.** A stale count in
  a procedure, the same class this pass is about, one step above it. Not in the registered change.
- **`grep -rn` returns the six files in an unstable order** on repeated identical runs, which
  predates this change and is untouched by it.
- **[`registry-check.md`](../../blueprints/checks/registry-check.md) line 258 names this class in
  prose** — *"A green table can mean nothing was audited… If no row says `pass`, nothing was
  checked"* — with a warning to the reader in place of an output that distinguishes the two. That is
  the shipped checks' version of the same defect, and it belongs to the queued subtraction pass over
  `blueprints/`.

**Not a release.** Everything here is under `.docs/`. Step 0: no version bump, no `Blueprint Version`
bump, no tag.
