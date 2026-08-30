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
