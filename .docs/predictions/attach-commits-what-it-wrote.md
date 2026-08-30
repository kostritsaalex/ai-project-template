# Prediction: the attach commits what it wrote, and a folder with no version control does nothing

**Written:** 2026-08-30, before the edit and before any run of the changed step.
**Subject:** [`blueprints/setup/procedure.md`](../../blueprints/setup/procedure.md) — one instruction
added to Step 8, nothing else in the file touched.

---

## The facts this rests on, established in this working tree rather than from the report

**Two live instances, both on 2026-08-30.** On ArtGlina the stubs sat uncommitted after the attach
and were committed by hand afterwards, outside the procedure. On NorsePath, after the attach and
after both checks and a behaviour test, `git status --short` in the component still printed
`?? AGENTS.md` and `?? CLAUDE.md`. Recorded as defect 8 of nine in
[`backlog.md`](../backlog.md) line 217, where none of the nine is yet repaired.

**No step asks for a commit.** `procedure.md` is 182 lines. Step 7 (line 129) defines attachment —
*"A component is attached when both halves are written, and writing one without the other is worse
than writing neither"* (line 133) — and says nothing about committing. Step 8 (line 173) searches for
placeholders (line 175), then reports files written, unknowns and which checks run next (line 178),
and says nothing about committing either.

**The blueprints already assume the commit that no step asks for.** `grep -rni 'commit' blueprints/`
returns four hits in this tree, all the same sentence and all in adoption READMEs:
`component/README.md:114`, `project/README.md:152`, `assets/README.md:91`,
`repository/README.md:104` — *"Before committing, search for `<!--` and for `<` followed by a capital
letter."* The report that prompted this change greps three folders and finds two of the four; the
other two say the same thing for the two remaining postures. **All four state an order**: the
placeholder search comes before the commit.

**Neither check can see the difference.** `structure-check` and `registry-check` read the working
tree, where an untracked file is indistinguishable from a committed one. A clone of the component
therefore arrives with no parent pointer, and a sweep of untracked files removes both stubs, with no
row failing in either case.

## The three decisions, each with the line it was decided on

**1. Step 8, not Step 7.** Decided on `component/README.md:114` and its three siblings: *"Before
committing, search for `<!--`…"*. That search is Step 8's first instruction, so a commit placed in
Step 7 runs before the search four shipped READMEs require to precede it. Two further reasons, both
from the file: Step 7 opens *"Skip this for a project scope, which has no parent"* (line 131), so an
instruction there is unreachable for a project adoption, which writes files into the same kind of
folder and leaves them untracked the same way; and repairing Step 7's definition of *attached* means
editing the sentence at line 133, which is a change to what attachment means rather than the one
instruction this release is allowed.

**2. The session commits; it does not only report.** Decided on `procedure.md:178`: Step 8 already
requires the session to *"say which files you wrote or changed"*. Both runs produced that report and
the stubs stayed untracked in both. *Report that the files need committing* is therefore a weaker
form of an instruction that already exists and has already failed twice, and under
[`0008`](../decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) it would not earn
its line. The objection — that a setup session should not start making commits nobody asked for —
is answered by scope rather than by omission: the session already writes into the person's folders,
and the commit is what makes that write survive; the instruction is bounded to the files the session
itself wrote.

**3. The wording assumes no version control, and no particular version control.** Decided on
[`0001`](../decisions/0001-project-scope-need-not-be-a-repository.md) — *"A project scope outside
version control loses history and review… which belongs to the project that chooses it"* — and on
[`0007`](../decisions/0007-a-component-with-no-address-says-so.md), *"Local version control and
reachability are separate questions"*, whose whole point is that `git init` decides nothing here. The
instruction is conditioned on the folder being under version control, names no tool, and its correct
outcome in a folder under none is that nothing happens.

## What ships

One paragraph, inserted in Step 8 between the placeholder search and the hand-back report:

> **Commit the files you wrote, and only those, in each folder you wrote into that is under version
> control.** A folder under none needs nothing here; an uncommitted stub is absent from a fresh clone
> and removed by a sweep of untracked files, and no check sees the difference, because a written file
> reads in the working tree exactly like a committed one.

Nothing is removed, and nothing else in the step or the file changes.

## Registered arms

**A1. A component attach into a folder under version control.** Predicted: the session writes the two
stubs, searches for placeholders, and then commits both, plus the parent's registry edit if the
parent folder is also under version control. `git status --short` in the component prints nothing
about `AGENTS.md` or `CLAUDE.md` at hand-back, and the hand-back names the commit.

**A2. The same, with the parent scope in a synced store rather than a repository.** Predicted: the
component's stubs are committed, the parent's `PROJECT.md` edit is not, and the session does not
invent a way to commit it. This is the ArtGlina shape.

**A3. Negative half — the instruction removed, same folder, fresh session.** Predicted: the stubs are
written and left untracked, reproducing both live instances. A positive run alone would not
distinguish the instruction from a session that would have committed anyway; both live runs say it
would not have, and A3 is what makes that a measurement rather than a recollection.

## Controls, not derived from the hypothesis

**C1. A project scope adopted in a folder that is not under version control.** The case the
hypothesis has no reason to handle: Step 8 runs for a project scope, so the instruction is read by a
session for which it must produce **no action and no confusion** — no `git init`, no question about
version control in the interview or the summary table, no line in the hand-back reporting that the
files are uncommitted, and no hedged sentence about it either. Failure here is not a wrong verdict
but an adoption that grows a step, which is the cost the method says lands where nothing measures it.
**Run twice**, because its evidence is an absence.

**C2. A component folder under version control with unrelated modified files already in it.** The
case the change would break if the understanding behind it — that a commit is a small and obviously
correct completion of the write — were wrong. Predicted: the commit contains the two stubs and
nothing else. A session that stages the person's work in progress alongside them has done something
materially worse than leaving the stubs untracked, and *"and only those"* is the clause under test.

**C3. A session that cannot run commands, only write files.** Predicted: it says the files are
written and not committed, and names what remains to be done. The failure it guards against is a
session reporting a commit it did not make, which is the *"judge by the artefact, not the report"*
failure already three times in this project's log.

## Not yet run, and this is disclosed rather than deferred quietly

**The instruction ships as unrun text.** No arm above has been run: each needs a fresh session against
a real or scratch scope, and this session performed the change. That is precisely defect 2 of the
nine — *"The shipped procedure was unrun text"* — repeated once more, against principle 6. It is
named here, in the changelog and in the backlog rather than left to be noticed. The arms stand
registered against the next attach, and A3 stays runnable from any tag before this release.

**What would retract the change.** C1 producing any action or any hedge in a folder with no version
control, or C2 producing a commit that contains a file the session did not write. Either would mean
the wording is wrong in the direction the framework cares about most, which is a document that costs
something in the cases it was not written for.
