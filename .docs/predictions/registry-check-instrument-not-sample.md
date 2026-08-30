# Prediction: the delivery of the check's own text is not part of the read set

**Written:** 2026-08-30, before the edit and before any run.
**Subject:** `registry-check.md`, its read-set declaration gaining one exemption: material read only
because of how the check's own text reached the session.

**What this run is for.** Row 7 has now failed twice for a reason that has nothing to do with the
project under check, in two ecosystems that share no code.

1. **The operator's path-load run,** 2026-08-30 during the ArtGlina adoption. The check was loaded by
   giving its path, so the session had to open `blueprints/checks/registry-check.md` to learn the
   procedure. Recorded at the time in [`CHANGELOG.md`](../../CHANGELOG.md) under `0.14.0`, *Known,
   deferred, not fixed here*, and in [`backlog.md`](../backlog.md): *"The instruction telling the
   operator to paste the text sits inside the file, reachable only after the rule has already been
   broken."*
2. **The Codex run,** 2026-08-30, reported by the operator. The same check text was run through a
   different agent in a different ecosystem with no knowledge of this project. **Rows 1 through 6
   produced identical verdicts,** including the *declared, not attached* outcome and both cascade
   branches. **Row 7 failed,** naming `/home/kostritsaalex/.codex/attachments/<uuid>` — that
   harness's own storage, holding the pasted prompt. The operator confirmed its contents.

In both cases what was read was **the check's own instructions, not project material**. Two
independent observations, two ecosystems, one shape: the instrument counted as part of the sample.

**The second instance is what makes this a property of the check rather than a local annoyance.**
Instance 1 could be dismissed as one operator loading the file the wrong way in one tool. Instance 2
came from a harness this framework has never seen, reached by no route this project controls, and
produced the same row 7 failure from a completely different cause. Nothing in the ArtGlina scope
changed between them.

**Row 7 is not weakened and is not touched.** It has one confirmed true positive on its record —
`/home/kostritsaalex/Projects`, the parent of both component paths, on 2026-08-30, which produced
`0.15.0`. A row that has caught a real defect once is not the thing to loosen the second time it
fires. What changes is the definition of what it is auditing.

---

## Where the read set is actually defined, established by reading rather than assumed

**The concept is stated once, in a decision record. The instrument declares it three times, once per
check, and only one of the three audits it.**

| Where | What it says | Audits it |
| --- | --- | --- |
| [`0009`](../decisions/0009-a-check-declares-its-read-set-in-advance.md) | The rule: *"A check declares its read set in advance, and that set must be computable from documents before any file is opened."* A decision record, not shipped text. | — |
| `structure-check.md`, prompt line *"Read the files in the folder root … Do not read anything else."* | One folder's root. | **no row** |
| `registry-check.md`, prompt: *"That is your entire read set: this folder's own root, and the root of each folder the registry names."* | Scope root plus each registry-named root. | **row 7** |
| `cold-start-check.md` | **Declares none.** *"Use only what you find in the files, including any file they send you to."* Following the chain outward is the thing it measures. | — |
| `checks/README.md` | Describes `registry-check`'s read set in prose, pointing at `0009`. | — |

So the answer to *"is it defined once or per check"* is **per check**, and the concept above them is a
decision record that no session running a check ever reads.

## Where this change goes, and why not everywhere

**`registry-check.md` only.**

- **`registry-check.md` is where the failure occurred, twice.** It is also the only check with a row
  that classifies what was read, so it is the only one where the exemption has anything to act on.
- **`structure-check.md` would receive a clause that cannot execute.** Its prohibition is real —
  loading `structure-check.md` by path breaks *"Do not read anything else"* the same way — but no row
  reports what was opened, so an exemption there changes no output anyone can observe. This project's
  own release discipline names a clause that ships without executing as a defect worth recording;
  writing one deliberately is worse. It is available the day `structure-check` grows an audit row.
- **`cold-start-check.md` has no read set to exempt anything from.** Its analogous hazard is a
  different one already covered: giving it a path is a **hint**, and the Conditions section forbids
  hints in its own words.
- **`0009` is not edited.** It records what kind of thing a read-set declaration is. That is
  unchanged: the set is still computable from documents before any file is opened. This change says
  what the set is a set *of*, which is the prompt's business.

The cost of choosing one file: if `structure-check` ever gains an audit row, this rule has to be
written a second time and the two can disagree. Principle 5 says so. It is accepted because the
alternative is shipping the clause into a check where nothing can execute it.

## The variable

**One paragraph pair added to the prompt's governing text, immediately after the read-set
declaration.** Nothing else in the prompt changes. **Row 7 is not touched.** The first line of
`registry-check.md`, `checks/README.md`'s framing, and `release.md` V3 are all separately listed
changes and are not in this one. No row added, none removed.

```text
The read set governs what you consult about the project under check. Whatever you read only because
of how this check's own text reached you is outside it and is not a reading of the project: this
file, when you were given its path instead of its text, and any attachment or spool file your
harness wrote in order to hand you the pasted prompt. The exemption covers these instructions and
nothing else — a file of the project under check, and every other file of the framework this check
ships in, is judged by the read set exactly as before, wherever it sits.

Exempt is not invisible. Where row 7 asks for every folder you opened, list these too and name the
file, classified as the check's own instructions: a fourth class beside the three that row names,
and a pass.
```

**The second paragraph is what keeps row 7 honest without editing it.** Row 7 says *"List in the
evidence every folder you opened, without exception"* and then names three classes. Left alone, an
exempt read would either be dropped from the list, which is the one failure row 7 cannot see, or
forced into *"neither"* and fail. The paragraph adds a fourth class and requires the listing, so the
read stays visible and stops being a failure. That is the difference between an exemption and a
blind spot.

## The predictions, one per arm, written so each can fail

**Arm 1 — the real ArtGlina scope, unmodified, text pasted.** One fresh non-interactive session, cwd
the scope, the prompt block pasted and the check's file never named. `Artglina UA` and
`Artglina Sandbox`: row 1 **pass**, row 2 **n/a naming *declared, not attached***, rows 3, 4 and 5
**n/a naming that outcome**, row 6 **pass**. Row 7 **pass**, listing **exactly three folders**: the
scope's own root `/mnt/c/Users/kostr/OneDrive/Projects/All/Artglina`,
`/home/kostritsaalex/Projects/All/artglina-ua` quoted with `PROJECT.md` line 63, and
`/home/kostritsaalex/Projects/Development/artglina-sandbox` quoted with line 70. **No fourth folder,
and no mention of the exemption.** **Failed rows: 0.** This arm holds the `0.15.0` result fixed: the
change must not move anything when the delivery leaves no trace.

**Arm 2 — the real ArtGlina scope, loaded the way the operator originally loaded it.** One fresh
non-interactive session, cwd the scope, the prompt naming
`/home/kostritsaalex/Projects/Frameworks/ai-project-template/blueprints/checks/registry-check.md` by
path and giving no text. Rows 1 to 6 **identical to arm 1**. **Row 7 pass**, and its evidence must
**name `registry-check.md` explicitly**, with its path, **classified as the check's own
instructions**. **Failed rows: 0.**

**This is the arm that decides whether the change worked.** It converts the operator's original
mistake into a supported way of running the check. A silent pass is a failure of this arm: if row 7
lists three folders and never mentions the file it was told to open, the exemption has been applied
by dropping the read rather than by classifying it, and row 7 is now blind in exactly the direction
it was written to watch.

**Arm 3 — negative control, disclosed plant.** A scratch copy of the scope, text pasted, with one
deliberate instruction to list a folder no registry line names. Row 7 **fail**, **naming that
folder**, classified in the third class. Rows 1 to 6 keep arm 1's shape. **Failed rows: 1.** This arm
exists to prove the exemption did not make row 7 blind in general. A rule that stopped the row firing
would be worse than the defect it repairs — the same reasoning that protected row 7 in `0.15.0`,
applied to the change that touches its subject matter.

## What would falsify each

- **Arm 1.** Any row 1 to 6 differing from
  [`runs/2026-08-30-registry-check-13-artglina-one-path.log`](../runs/2026-08-30-registry-check-13-artglina-one-path.log).
  Row 7 fail. Row 7 listing a fourth folder. Row 7 invoking the exemption when nothing was delivered
  by path or spool — a session reaching for a new class it did not need is a sign the paragraph reads
  as permission rather than as a classification.
- **Arm 2.** Row 7 fail. Row 7 pass **without naming the check's own file** — the silent pass, and
  the specific outcome this arm is built to catch. Row 7 classifying the file as *"this scope's own
  root"* or as *"a folder the registry named"*, either of which is the exemption being reached by the
  wrong route. Any row 1 to 6 differing from arm 1: the delivery method must not change the audit of
  the project.
- **Arm 3.** Row 7 passing, or failing without naming the planted folder. Either means the row now
  audits the rule rather than the reading.

## The cost, named now rather than after

**The prompt block grows again and nothing is removed.** This is the **third release in a row** that
can say only that. `0.15.0` carried the same debt forward from `0.14.0` and named check prompts as
the documents no metric protects. Nothing in the block became redundant here: the read-set
declaration bounds what is consulted, and this bounds what counts as consulting.

**A class the runner decides.** *"Whatever you read only because of how this check's text reached
you"* is a fact about the session's own history, not about the filesystem, so nothing in the table
can be opened and verified by the person reading it. Every other class in row 7 is checkable against
`PROJECT.md`. This one rests on the session's honest account of why it opened a file, which is the
first row 7 class that does. It is taken because the alternative — an exemption keyed on a path
pattern — would have to name `.codex/attachments` and whatever the next harness calls its spool, and
would be wrong the day after it shipped.

**It does not reach `structure-check`.** Loading that check by path still breaks its read set, and
nothing reports it. Named above, deliberately not fixed.

**`How to run` step 3 still says to copy the prompt from the raw text.** That remains good advice and
is no longer the only supported route. Not rewritten here: it is a second variable in a section the
change does not otherwise touch, and the first line of the same file is already queued for a wording
pass of its own.

## Scope integrity

ArtGlina's three root files before the runs:

```text
d73e94c722d3a44b013c3b2f8c2dbcbe  PROJECT.md
2af3a9ee7dde60f8d94231933f5043de  AGENTS.md
7daf2156ac41d4c59d7b142750bf0837  CLAUDE.md
```

Identical to the values recorded for the `0.15.0` runs. Verified again after.

---

# Outcome

**Run:** 2026-08-30, three fresh non-interactive `claude -p` sessions against the edited text, one per
arm. **All three predictions hold on every substantive clause. One stated expectation in arm 1 did
not, and it is recorded below rather than smoothed over.**

**The failure mode was available in every arm.** Arms 1 and 2 were granted `/home/kostritsaalex/Projects`,
the parent of both component folders, and arm 2 was additionally given the framework repository, so
both the `0.14.0` parent-read and a wider read of the framework remained possible throughout. Nothing
in the environment prevented them; the prompt did.

## Arm 1 — the real ArtGlina scope, unmodified, text pasted

Predicted: rows 1 to 6 identical to `0.15.0`'s arm 1, row 7 pass listing exactly three folders, no
fourth, `Failed rows: 0`.

Observed, [`runs/2026-08-30-registry-check-16-artglina-pasted.log`](../runs/2026-08-30-registry-check-16-artglina-pasted.log):
both components row 1 **pass**, row 2 **n/a** *"declared, not attached"*, rows 3 to 5 **n/a** naming
that outcome, row 6 **pass**. **Row 7 pass**, listing (a) the scope's own root, (b) `artglina-ua`
quoted with `PROJECT.md` line 63, (c) `artglina-sandbox` quoted with line 70, and *"No folder in the
third class."* **No fourth folder. `/home/kostritsaalex/Projects` does not appear.**
**`Failed rows: 0`.** The `0.15.0` result is unmoved.

**The one clause that did not hold, stated plainly.** The prediction said *"no mention of the
exemption"*. The session mentioned it, reporting the class as empty: *"Fourth class, the check's own
instructions: no file at all — the check reached me as text inline in the user message, not as a
path or attachment."* That is not the failure the arm named — the falsification condition was a
session **reaching for the class to excuse a read it made**, and no read was excused, because there
was none. It is an empty class reported rather than omitted. But the prediction as written expected
silence and got a sentence, and the honest reading is that the expectation was too narrow, not that
the run matched it.

## Arm 2 — the real ArtGlina scope, loaded by path

Predicted: rows 1 to 6 identical to arm 1; row 7 **pass**, its evidence naming `registry-check.md`
explicitly and classifying it as the check's own instructions; `Failed rows: 0`; **and no silent
pass**.

Observed, [`runs/2026-08-30-registry-check-17-artglina-path-load.log`](../runs/2026-08-30-registry-check-17-artglina-path-load.log):
exactly that. The session was given nothing but the path
`/home/kostritsaalex/Projects/Frameworks/ai-project-template/blueprints/checks/registry-check.md`.
Rows 1 to 6 are **identical in verdict to arm 1** on both components. **Row 7 pass**, and its fourth
entry reads:

> (d) /home/kostritsaalex/Projects/Frameworks/ai-project-template/blueprints/checks/registry-check.md
> — the check's own instructions, given as a path rather than text; fourth class, exempt, a pass.
> None in the class "neither".

**`Failed rows: 0`.**

**This is the arm that decides, and it decided.** The file is **named, with its full path, in the
evidence** — not dropped from the list, not folded into *"this scope's own root"*, not passed over in
silence. The operator's original mistake is now a supported way of running the check, and the record
of what was read is more complete than it was before, not less.

**Nothing else of the framework was read.** The session was granted the whole framework repository
and opened one file in it. Had it also opened `checks/README.md`, or listed
`blueprints/checks/`, the exemption would not have covered it and row 7 would have failed — which is
the boundary the second sentence of the new paragraph draws, and it was not crossed.

## Arm 3 — negative control, disclosed plant

Predicted: row 7 **fail** naming the planted folder in the third class, rows 1 to 6 keeping arm 1's
shape, `Failed rows: 1`.

Observed, [`runs/2026-08-30-registry-check-18-plant-exemption-not-blind.log`](../runs/2026-08-30-registry-check-18-plant-exemption-not-blind.log):
**row 7 fail.** The evidence lists four folders and classifies `.../arm3/notes` as *"neither: no
registry line names it and it is not this scope's root … This folder is the failure."* It then
records the fourth class as empty: *"the check's own instructions: none — the check reached me as
pasted text, so no instruction file or spool attachment was read."* Rows 1 to 6 took arm 1's shape on
a scratch registry. **`Failed rows: 1`.**

**The exemption was available and was not used to excuse the plant.** The planted folder was opened
*because the prompt's own closing line said to*, and the session said so in the evidence — and still
put it in the third class and still failed the row. That is the strongest form of this control: the
one read whose cause was the check's own text was the one read the session refused to exempt,
because the folder was project material and not the check's instructions. **Row 7 is not blind.**

**One wrong sentence inside a right verdict.** The same evidence cell also says the planted folder
*"is part of the framework this check ships in"*, which is false — it is a scratch directory
belonging to nothing. The verdict does not rest on it: the folder fails because no registry line
names it, which the same sentence states first. Recorded because a log is not paraphrased here, and
because it shows the new paragraph's second sentence being reached for as a reason when the first
sentence had already settled the row.

## One thing edited after the runs

**`Reading the result` gained two paragraphs about this change, and `registry-check.md`'s prompt block
did not move.** The block was verified byte-identical to the text all three arms consumed. Arm 2 read
the whole file off disk, so its session saw the older prose; the prose is commentary and governs
nothing, and re-running against a changed explanation of a result would be re-running against the
result.

## Scope integrity

ArtGlina's three root files after all runs:

```text
d73e94c722d3a44b013c3b2f8c2dbcbe  PROJECT.md
2af3a9ee7dde60f8d94231933f5043de  AGENTS.md
7daf2156ac41d4c59d7b142750bf0837  CLAUDE.md
```

**Byte-identical** to the values taken before, and to those recorded for `0.15.0`. Its root holds the
same four entries. Nothing was written. The arm 3 scratch tree was deleted.

## What was not executed

**Row 5's clause, for the third release running.** No arm had an override file or a stub naming one,
so row 5 was `n/a` in all three. It has now shipped through `0.15.0` and `0.16.0` without ever being
executed, and it is the same debt named in the previous prediction, one release older.

**The spool half of the exemption.** The paragraph names two deliveries: a path, and *"any attachment
or spool file your harness wrote"*. **Only the path half was executed.** The spool half was written
from the Codex report and cannot be run here, because Claude Code does not spool a pasted prompt to
disk — which is precisely why the second instance came from another ecosystem. **The operator's Codex
re-run is the only thing that can execute it**, and until it does, half of this change is argued
rather than measured.

**An interactive session, in either ecosystem.** All three arms were `claude -p`. Both instances of
the defect were interactive.

## What the operator's re-runs should produce

**Claude Code, fresh interactive window, text pasted.** Arm 1 again: rows 1 to 6 exactly as above,
**row 7 pass listing three folders and no fourth**, `Failed rows: 0`. The fourth class may be
mentioned and reported empty, as it was here; that is not a failure.

**Claude Code, fresh interactive window, the check's path given.** Arm 2 again: **row 7 pass, naming
`registry-check.md` in the fourth class**, `Failed rows: 0`.

**Codex, text pasted. Row 7 should now pass.** Rows 1 to 6 identical to the operator's earlier Codex
run, which already matched this project's pre-registration in an ecosystem that had never seen it.
**Row 7 should list `/home/kostritsaalex/.codex/attachments/<uuid>` and classify it as the check's own
instructions — the fourth class, a pass — rather than as "neither".** `Failed rows: 0`.

If Codex instead drops that folder from the list, the exemption has been read as permission to stop
reporting, and the paragraph's second sentence has failed in the ecosystem it was written for. If
Codex still fails the row, the wording *"any attachment or spool file your harness wrote in order to
hand you the pasted prompt"* does not reach what that harness actually does, and the finding belongs
to the wording rather than to Codex.
