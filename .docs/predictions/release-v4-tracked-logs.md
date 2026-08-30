# Prediction: V4's third command compares two sets, not one set against nothing

**Written:** 2026-08-30, before the edit and before any run of the repaired command.
**Subject:** [`release.md`](../release.md) step 7, row V4, third command.

---

## The facts this rests on, established by reading the file and the tags

**What the command is there to guarantee, as a fact about the repository:** at the moment before the
tag, every run log named in `.docs/runs/README.md` exists in the tree the tag will name. The index is
the only record of what each log is evidence for, and a name in it with no file behind it is a
citation to nothing.

**What it literally compares.** It runs

```bash
grep -oE '^[0-9a-f]{32}  \S+' .docs/runs/README.md | awk '{print $2}' | while read f; do
  git ls-files --error-unmatch ".docs/runs/$f" >/dev/null 2>&1 || echo "NOT TRACKED: $f"
done
```

The left side is the set of filenames on lines of `.docs/runs/README.md` that begin with 32 hex
characters followed by exactly two spaces — the checksum block, hand-maintained, `md5sum`'s output
format. The right side is `git ls-files` on each of those names. It prints `NOT TRACKED: <name>` per
failure and **nothing at all otherwise**.

**Its output does not distinguish "every log is tracked" from "there was nothing to check."** Both
are the empty string. Run against the trees of `v0.8.0` (no `.docs/runs/README.md` in the repository
at all) and `v0.16.0` (99 names, 99 tracked logs):

```text
----- v0.8.0 -----
[end of output; byte count: 0]
----- v0.16.0 -----
[end of output; byte count: 0]
```

They are byte-identical, and both are zero bytes. **This is not only historical.** On a scratch copy
of `HEAD` with the checksum block's two spaces changed to one — 99 lines touched, every log still
present and still tracked, no defect of any kind introduced — the command again prints zero bytes.
The key is a whitespace convention in a hand-maintained block, and one `sed` blinds the check without
changing a single fact it guards.

**How often it has fired, and how often it caught a real omission.** Run against all twenty tags:

| Occasion | Names in the block | Fired | Real omission? |
| --- | --- | --- | --- |
| `v0.1.0`–`v0.8.0` | 0 — no `.docs/runs/` in the tree | no | vacuous: nothing to check |
| `v0.9.0`, retrospective — the command did not exist yet | 5 | **yes, 5 names** | **yes** — the index named five logs the tree did not contain |
| `v0.9.1`–`v0.16.0` | 9 → 99 | no | no |

**One firing in twenty tags, and it is a true positive.** It is also retrospective: the command was
written into `release.md` for `0.9.2` (commit `5af7bf7`) in response to that defect, which had been
found by hand. In the nine releases where it was actually in force it has never fired. That is the
opposite shape from V3, which fired five times and caught nothing.

**The fact is guaranteed nowhere else in step 7.** `git status --porcelain` sees a log present on
disk but not added (`??`) and a tracked log deleted from disk (` D`); the ignored sweep sees a log
present and excluded by a rule. None of the three sees a name in the index whose file is neither on
disk nor in git — which is exactly the `v0.9.0` defect. V1 lists this release's changed files and
would not show a log named by an earlier release. Nothing else reads `.docs/runs/README.md`.

## The decision, and the evidence that decides it

**Razor [`0008`](../decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md): the
command stays, and is repaired.** Removal was on the table on its merits and is rejected on the
record, not on principle. It has one true positive across twenty tags, against V3's zero; the defect
it caught produced a bad tag that nothing else would have caught; and the artefact it guards is
hand-maintained and has grown from 5 names to 99, which is exactly where a clerical omission hides.

**What is repaired is the key, and the repair is a second side.** The block's format stays the key —
it is the only machine-readable form the index has — but the other side of the comparison now comes
from git rather than from nothing. A person can still break the key by reformatting; they can no
longer break it *silently*, because the tree's count does not move when the block's format does.

**The command becomes:**

```bash
IDX=$(grep -oE '^[0-9a-f]{32}  \S+' .docs/runs/README.md | awk '{print $2}' | sort -u)
TREE=$(git ls-files .docs/runs/ | grep '\.log$' | sed 's|.*/||' | sort -u)
echo "runs index: $(grep -c . <<<"$IDX") named, $(grep -c . <<<"$TREE") tracked"
comm -23 <(grep . <<<"$IDX") <(grep . <<<"$TREE") | sed 's/^/NAMED, NOT TRACKED: /'
comm -13 <(grep . <<<"$IDX") <(grep . <<<"$TREE") | sed 's/^/TRACKED, NOT NAMED: /'
```

**Every outcome prints a line, and the lines are labelled.** A pass is two equal counts and no names
under them. Nothing to check is `0 named, 0 tracked`, which says so. A blinded key is `0 named, 99
tracked` followed by 99 labelled names. The reader never has to remember which column they are
looking at, which was the whole complaint against a step whose pass and whose blind spot were the
same empty string.

**The second direction is declared in scope, and it is the mechanism.** `TRACKED, NOT NAMED` is a new
fact for this row: a committed log the index does not name. It is in scope for three reasons. It is
invisible to every other command in step 7 — the log is committed, so `git status` is clean. It is
the same failure the index exists to prevent, read the other way: an undocumented log is evidence
nobody can date. And without it the reformat case reports a bare count mismatch with no names, which
is a weaker failure than the one the repair is for.

**What this does not do.** `git ls-files` reads the index, so a named log that is tracked but deleted
from disk still passes this command; `git status --porcelain`, the first command in the same row,
prints ` D` for it. The row is three commands and they are read together.

## The runs, pre-registered

**P1 — the tree as it stands.** `HEAD` unmodified. **Must pass, visibly.** Expected output exactly
`runs index: 99 named, 99 tracked` and no further lines. A pass that is a printed line, not an
absence.

**P2 — negative control, disclosed plant: the reformatted block.** A scratch copy of `HEAD` with the
checksum block's two spaces changed to one, 99 lines touched, **every log genuinely present and
tracked**. The old command prints nothing here, indistinguishable from P1. **The repaired command
must not report a pass**: expected `runs index: 0 named, 99 tracked` followed by 99
`TRACKED, NOT NAMED:` lines. Scratch copy deleted after.

**P3 — negative control, disclosed plant: a named log removed.** A scratch copy of `HEAD` with
`2026-08-30-registry-check-17-artglina-path-load.log` deleted from disk and from the index, its name
left in the block. **Must fail, naming it**: expected `runs index: 99 named, 98 tracked` and one
`NAMED, NOT TRACKED: 2026-08-30-registry-check-17-artglina-path-load.log`. Scratch copy deleted after.

**P4 — negative control, disclosed plant: a tracked log the block does not name.** A scratch copy of
`HEAD` with one new log committed and no line added to the block. **Declared in scope above**, so it
must fail: expected `runs index: 99 named, 100 tracked` and one `TRACKED, NOT NAMED:` line. For the
record of what happens either way, the old command is run against the same tree and is expected to
print nothing, because it never looks at the tree.

**P5 — the twenty tags, retrospectively.** The repaired command against all twenty trees. `v0.9.0`
must still fire with its five names. `v0.9.1`–`v0.16.0` must pass with equal counts. `v0.1.0`–`v0.8.0`
must print `0 named, 0 tracked` rather than nothing, which is the vacuity being removed.

**What would falsify the change.** P1 failing, P2 or P3 or P4 passing, `v0.9.0` no longer firing
under P5, or any tag from `v0.9.1` on failing under P5. Any one of those means the new comparison is
not the comparison it claims to be.

**Not a release.** Everything here is under `.docs/`. Step 0 applies: no version bump, no
`Blueprint Version` bump, no tag.
