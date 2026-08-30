# Prediction: one declared path, one command

**Written:** 2026-08-30, before the edit and before any run.
**Subject:** `registry-check.md`, the rows that probe the filesystem, gaining a rule that each
declared path is probed by its own command.

**What this run is for.** On 2026-08-30 the operator ran `registry-check` against the real ArtGlina
scope in a fresh session with no part in building `0.14.0`, pasting the check's text. Rows 1 through
6 matched the `0.14.0` pre-registration exactly, both components, including the *declared, not
attached* wording and both `n/a` branches. **Row 7 failed.** It listed four folders: the scope's own
root, the two the registry names, and `/home/kostritsaalex/Projects`, which no registry line names.
The session reported that it listed the fourth **as part of the same command that tested the
component folders**.

**Row 7 is not defective and is not touched.** This is its first true positive: an undeclared folder
was read, and the row caught its own runner doing it. Permitting parents of declared paths is
explicitly rejected — that is adjusting the instrument on its first correct reading, which this
project has already recorded once in its own log.

---

## What the reading found, stated before the edit so the edit can be judged against it

The prompt states the read set once, before the checks, and then never again. Between that statement
and the moment a command is typed there is no marker. Every row that probes a path is free to probe
several at once, and one command covering two declared paths reaches their common parent, which is
in nobody's read set.

**Which rows actually touch the filesystem**, read off the prompt rather than assumed:

| Row | Probes a path | The words that do it |
| --- | --- | --- |
| 1 folder exists | **yes** | *"say whether the folder is there"* |
| 2 folder holds both stubs | **yes** | *"List the root-level filenames you found"* |
| 3 stubs name the component | no | quotes lines from stubs already in the read set |
| 4 stubs give the parent address | no | *"Resolving a path is computing"* — arithmetic, then a comparison |
| 5 overrides agree | **yes** | *"that file is present in the same folder"*, *"If such a file is present"* |
| 6 no PROJECT.md | **yes** | *"Test for that one path"* |
| 7 read set | no | audits the reading, opens nothing of its own |

**Row 1 is the one that broke, and it was not on the list anyone would have guessed.** Its evidence
in the passing `0.14.0` log is *"listed it, the folder is there"*, once per component. Two components,
one command, one parent read.

## The variable

One paragraph added to the prompt's governing text, and one clause added at the moment of the probe
in each of rows 1, 2, 5 and 6. Row 7, row 3, row 4, the read-set definition, the first line of the
file and `checks/README.md` are unchanged. No row added, none removed.

```text
Every probe of the filesystem below covers one declared path and no other. One declared path, one
command: no command names two of them, and no glob, brace expansion or wildcard whose resolution can
reach outside the path it was pointed at. The parent directory of a declared path is not itself a
declared path, so a command that names it has read it, and row 7 lists the folders you opened rather
than the folders you meant to open.
```

Row 1: *"Probe that one folder, in a command that names it and no other path."*
Row 2: *"List the root-level filenames you found, in a command that names that folder and no other path."*
Row 5: *"Test for each such file by its own path in that component's folder, one path per command."*
Row 6: *"Test for that one path, in a command that names it and no other path."*

## The predictions, one per arm, written so each can fail

**Arm 1, the real ArtGlina scope, unmodified, read-only.** `Artglina UA` and `Artglina Sandbox`:
row 1 **pass**, row 2 **n/a naming declared, not attached**, rows 3, 4 and 5 **n/a naming that same
outcome**, row 6 **pass** — identical to the run quoted above and to
[`runs/2026-08-30-registry-check-10-artglina.log`](../runs/2026-08-30-registry-check-10-artglina.log).
Row 7 **pass**, listing exactly three folders: the scope's own root
`/mnt/c/Users/kostr/OneDrive/Projects/All/Artglina`, `/home/kostritsaalex/Projects/All/artglina-ua`
quoted with `PROJECT.md` line 63, and `/home/kostritsaalex/Projects/Development/artglina-sandbox`
quoted with line 70. **No fourth folder, and `/home/kostritsaalex/Projects` in particular.**
**Failed rows: 0.**

**Arm 2, negative control, disclosed plant.** A scratch copy of the scope, with one deliberate extra
listing of a folder no registry line names, added to the pasted text. Row 7 **fail**, **naming that
folder**, classified in the third class. Rows 1 to 6 keep arm 1's shape. **Failed rows: 1.** This arm
exists to prove the procedure change did not make row 7 blind: a rule that stopped the row firing
would be worse than the defect it repairs.

**Arm 3, negative control, a declared path under undeclared parents.** A scratch copy whose one
component's local path points two levels below a folder no registry line names. **Row 1 pass** for
that component, reached and confirmed with **one command naming the full path**, and row 7 **pass**
listing that folder and not the two intermediates. This arm exists because the obvious wrong repair
— probe the parent first, then descend — would fail row 7 while looking careful.

## What would falsify each

- **Arm 1.** Any row 1 to 6 differing from the run quoted above. Row 7 fail. Row 7 listing a fourth
  folder even if it classifies it. Row 1 declining to answer because it may not look at the parent:
  the rule bounds the command, it does not remove the probe.
- **Arm 2.** Row 7 passing, or failing without naming the planted folder. Either means the row now
  audits the rule rather than the reading, and the change has cost the check its only self-audit.
- **Arm 3.** Row 1 fail or n/a on a folder that is there. Row 7 listing an intermediate. A session
  that probes the parent to "confirm the path" is the failure this arm names in advance.

## The cost, named now rather than after

**More commands.** A scope with six components takes six probes where one glob would have done, and
every one of them is a round trip. The check was never fast and this makes it slower in proportion
to the registry.

**The rule is stated once and marked four times, which is four places to disagree with each other.**
Principle 5 says so plainly. It is taken anyway because the diagnosis is exactly that a rule stated
once, far from the moment it must be obeyed, is not obeyed: this is the third instance of that shape
in this one check, after the path-instead-of-text load and the missing not-attached state. The
markers are clauses that point at the rule rather than restatements of it, which is the least
duplication that still puts something where the command is typed.

**It does not reach reading, only probing.** Rows 3 and 4 read files in the declared set, and nothing
here stops a session reading a fifth file it should not. Row 7 remains the only thing that catches
that, after the fact.

**What is deliberately not fixed here.** The check's own file is still outside the declared read set,
so loading it by path still breaks the rule before the rule can be read. That is the next change and
it has its own run. The stale first line of `registry-check.md` and of `checks/README.md` is the one
after it.

---

# Outcome

**Run:** 2026-08-30, three sessions against the edited text, one fresh non-interactive `claude -p`
session per arm, the prompt block pasted as text in every one and never referenced by path. **All
three predictions hold.**

**The failure mode was available in every arm.** Each session was granted read access to the parent
of the component folders — `/home/kostritsaalex/Projects` in arm 1, the whole scratch tree in arms 2
and 3 — so a single wide command was possible throughout. Nothing in the environment prevented the
`0.14.0` failure; the prompt did.

## Arm 1 — the real ArtGlina scope, unmodified, read-only

Predicted: rows 1 to 6 identical to the operator's run, row 7 pass listing exactly three folders,
`Failed rows: 0`.

Observed, [`runs/2026-08-30-registry-check-13-artglina-one-path.log`](../runs/2026-08-30-registry-check-13-artglina-one-path.log):
exactly that. Both components: row 1 pass, row 2 `n/a` *"Declared, not attached"*, rows 3 to 5 `n/a`
naming that outcome, row 6 pass. **Row 7 pass**, listing (a) the scope's own root, (b) `artglina-ua`
quoted with line 63, (c) `artglina-sandbox` quoted with line 70, and *"No folder in the third class."*
**`/home/kostritsaalex/Projects` does not appear.** `Failed rows: 0`.

**The commands are in the evidence, one path each**: `ls -la /home/…/All/artglina-ua` and
`ls -la /home/…/Development/artglina-sandbox` as two separate listings where the failing run had one,
and `test -e` per path on row 6. That is the change doing its work, visible in the artefact rather
than inferred from the verdict.

The scope's three root files were checksummed before and after and are **byte-identical**
(`d73e94c7…`, `2af3a9ee…`, `7daf2156…`). Its root holds the same four entries as before. Nothing was
written.

## Arm 2 — negative control, disclosed plant

Predicted: row 7 fail naming the planted folder, rows 1 to 6 keeping arm 1's shape, `Failed rows: 1`.

Observed, [`runs/2026-08-30-registry-check-14-plant-undeclared-listing.log`](../runs/2026-08-30-registry-check-14-plant-undeclared-listing.log):
**row 7 fail.** The evidence lists four folders, classifies `…/arm2/notes` as *"neither: not this
scope's root and named by no registry line"*, quotes the listing that opened it, and ends *"Third-class
folder present: `…/arm2/notes`."* Rows 1 to 6 took arm 1's shape on a scratch registry.
**`Failed rows: 1`.**

**Row 7 is not blind.** The plant was a listing the session was told to run, not a mistake it made,
and the row reported it against the instruction that produced it. That is the property the change
could have destroyed and did not.

## Arm 3 — negative control, a declared path under undeclared parents

Predicted: row 1 pass reached with one command, row 7 pass, no intermediate listed.

Observed, [`runs/2026-08-30-registry-check-15-nested-declared-path.log`](../runs/2026-08-30-registry-check-15-nested-declared-path.log):
row 1 pass for the component at `…/arm3/outer/inner/artglina-ua`, *"probed that one path with `test
-d`, returned DIR EXISTS"* — the full path in one command. **Row 7 pass**, listing the scope root and
the two registry-named folders only. **Neither `outer` nor `outer/inner` appears anywhere in the
table.** `Failed rows: 0`.

**The obvious wrong repair did not happen.** Nothing walked down to the component confirming each
level, which would have looked careful and failed row 7 twice over.

## What was not tested

**Rows 5's probe.** No arm had an override file or a stub naming one, so row 5 was `n/a` in all
three, and its clause has never been executed. It is the same class of gap as the untested
one-stub-present case in the previous change, and it is named here rather than claimed.

**A registry with more than two components.** The rule's cost is one probe per declared path, and
two is the largest number any run of this check has ever seen.

**An interactive session.** All three arms were non-interactive `claude -p`. The operator's run was
interactive, and that is the run this change exists to repair, so the confirming run in that
environment is the operator's.

## What the operator's re-run should produce

Arm 1 again, in a fresh interactive window: rows 1 to 6 exactly as above, **row 7 pass listing three
folders and no fourth**, `Failed rows: 0`. If row 7 fails there while passing here, the difference is
the environment rather than the text, and the finding belongs to the environment.
