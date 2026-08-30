# Prediction: step 7 states what it examined, and V1 and V2 stop passing vacuously

**Written:** 2026-08-30, before the edit and before any run of the repaired commands.
**Subject:** [`release.md`](../release.md) step 7 — the paragraph before the block, and rows V1 and V2.

---

## The facts this rests on, established by running the current commands

**V1 passes vacuously when `$PREV` is empty.** `PREV=$(git describe --tags --abbrev=0)` fails in a
tree with no tag reachable from `HEAD`, leaving `git diff --name-only $PREV..HEAD`, which the shell
expands to `git diff --name-only ..HEAD` and git reads as `HEAD..HEAD`. Confirmed on a `--no-tags`
clone of this repository:

```text
$ PREV=$(git describe --tags --abbrev=0)
fatal: No names found, cannot describe anything.
$ echo "rc=$? PREV=[$PREV]"
rc=128 PREV=[]
$ git diff --name-only $PREV..HEAD
$ echo "rc=$? bytes=0"
rc=0 bytes=0
```

**Exit code 0 and zero bytes**, which is the same output V1 gives on a release that touched nothing —
and V1's criterion, *"every file the changelog's top entry claims to have changed appears in the
list"*, is then read against no list at all. The `fatal:` goes to stderr, above the block's other
output, and is the only thing distinguishing the two; the step's own instruction is to read the
evidence rather than the exit code, and there is no evidence to read.

**V2 passes vacuously when either field label is reworded.** On a scratch copy of `HEAD` with
`Version:` lowercased in all six blueprint `README.md`s — 12 lines touched, every version number
still correct, no defect introduced — `grep -rn "Blueprint Version:\|Framework Version:"` prints
**zero bytes**. Confirmed.

**The partial case is worse than the demonstrated one, and it is why the repair needs a denominator.**
On a scratch copy of `HEAD` with only `**Blueprint Version:**` reworded to `**Blueprint Ver:**` in all
six, V2 prints:

```text
blueprints/checks/README.md:4:**Framework Version:** 0.16.0
blueprints/assets/README.md:6:**Framework Version:** 0.16.0
blueprints/repository/README.md:6:**Framework Version:** 0.16.0
blueprints/component/README.md:7:**Framework Version:** 0.16.0
blueprints/project/README.md:6:**Framework Version:** 0.16.0
blueprints/setup/README.md:4:**Framework Version:** 0.16.0
```

Six healthy-looking lines, and **every `Blueprint Version` in the framework has silently left the
check**. The full rewording at least prints nothing, which is visibly odd. This one does not.

**How much of it is guarded elsewhere, checked rather than assumed.** V3 catches the *full*
rewording: `grep -L "Framework Version:\*\* 0.16.0"` lists all six blueprints, because the string it
looks for is gone. V3 does **not** catch the partial one — run against the tree above it printed
`CHANGELOG 0.16.0` and listed nothing. V3 never reads `Blueprint Version:` at all, and nothing else
in step 7 does either. So the `Framework Version` half has a second reader and the `Blueprint
Version` half has none.

**Nothing in step 7 guards V1's case at all.** V3 reads `CHANGELOG.md` and the blueprints, V4 reads
`git status` and the runs index. None of them touches `$PREV`, and none would notice that V1 had
compared `HEAD` against itself.

## The decision, and why it is one change and not three

**One governing requirement for the step, not a clause per row.** The class is the same in V1, V2 and
the two already repaired: a row that prints only its failures cannot distinguish a clean pass from an
examination that never happened. Patching each row on its own merits means writing that reason a
third and a fourth time, in a step that has grown from 138 to 145 non-blank lines with nothing
removed. The requirement is stated once, in the paragraph a session reads immediately before running
the block, and each row's prose says only what *its* positive line contains.

**The sentence does not repair the commands by itself, and that is not a reason against it.** A
requirement in prose cannot make `git diff --name-only $PREV..HEAD` print its range; both commands
still change. What the sentence buys is that the change is one rule with four conformances rather
than four unrelated patches, and that the justification for it stops being copied into each row.

**What it lets come out.** Two passages, both of which exist only to say per-row what the governing
sentence now says once, or to restate a linked decision record verbatim:

- V4's *"**The third prints a count line in every outcome**"* and the four lines after it, *"It
  compares two sets because it used to compare one set against nothing… without touching a fact it
  guards"* — that history is [`0020`](../decisions/0020-a-check-that-cannot-fail-is-not-a-check.md)'s
  Context, quoted in a row that already links to it.
- V3's *"**It compares two fields because it used to grep prose.** The old row matched a fixed phrase
  in the backlog. It fired five times, caught nothing…"* — the same, from
  [`0019`](../decisions/0019-a-check-compares-fields-not-prose.md).

Principle 5, applied to a file that duplicates the records it links. The rest of the step's prose is
left to the subtraction pass already queued over it; this change removes only what it directly
replaces.

**V1 and V2 are one change, not two.** They share the class and not the mechanism — V1's is a
variable that can be empty making a range degenerate, V2's is a literal key that can drift out of the
document — and if the mechanisms were the deliverable they would be two. The deliverable is the
governing requirement, which cannot be attributed to either row: splitting would mean writing it
twice or arbitrarily hanging it on whichever went first. There is no build here to bisect, so the
usual argument for splitting does not apply. **The cost is that a wrong repair to one lands in a
commit with the other**, and it is paid down by verifying and reporting each row's arms separately.

## The commands, as they will be written

```bash
PREV=$(git describe --tags --abbrev=0) || PREV=NO-PREVIOUS-TAG
CHANGED=$(git diff --name-only "$PREV..HEAD")
echo "V1 range $PREV..HEAD, $(grep -c . <<<"$CHANGED") files changed"
grep . <<<"$CHANGED"
```

```bash
BPR=$(ls blueprints/*/README.md)
echo "V2 $(grep -c . <<<"$BPR") blueprint READMEs, \
$(grep -l 'Blueprint Version:' $BPR | grep -c .) with Blueprint Version, \
$(grep -l 'Framework Version:' $BPR | grep -c .) with Framework Version"
grep -rn "Blueprint Version:\|Framework Version:" blueprints/*/README.md
```

**V1's sentinel is the repair.** `NO-PREVIOUS-TAG..HEAD` is not a range git can resolve, so the diff
fails loudly instead of succeeding emptily, and the range appears in the row's own output line where
a reader cannot mistake it for a release diff.

**V2's denominator is the repair.** Three numbers rather than one, because the demonstrated failure
takes out one field and leaves the other, and because a blueprint `README.md` carrying neither field
contributes nothing to a `grep -rn` and is invisible without a count of the files themselves.

## The runs, pre-registered

**P1 — V1 with no previous tag.** A `--no-tags` clone of this repository. **Must not print anything a
reader can take as a clean pass.** Expected: `git describe`'s `fatal:` on stderr, then
`V1 range NO-PREVIOUS-TAG..HEAD, 0 files changed`, and a second `fatal:` from the diff. The old
command prints zero bytes here.

**P2 — V1 on a normal release.** `HEAD` with tags intact, and at `v0.16.0`. **Must pass and must name
what it compared.** Expected a line beginning `V1 range v0.16.0..HEAD,` with a non-zero count,
followed by exactly the file list the old command printed.

**P3a — V2 with both labels reworded.** Scratch copy of `HEAD`, `Version:` lowercased in all six
blueprint `README.md`s, every number correct. **Must not report success.** Expected
`V2 6 blueprint READMEs, 0 with Blueprint Version, 0 with Framework Version` and no further lines.

**P3b — V2 with only the `Blueprint Version` label reworded.** Scratch copy of `HEAD`,
`**Blueprint Version:**` → `**Blueprint Ver:**` in all six, every number correct. **Must not report
success**, and this is the arm the denominator exists for. Expected
`V2 6 blueprint READMEs, 0 with Blueprint Version, 6 with Framework Version` above six lines that on
their own look healthy.

**P4 — V2 on the tree as it stands.** **Must pass and print what it counted.** Expected
`V2 6 blueprint READMEs, 6 with Blueprint Version, 6 with Framework Version` followed by the same 12
lines the old command prints.

**P5 — both against all twenty tags.** Firings reported with, for each, whether it is a real omission
and whether it is live or retroactive. Expected: **V1 fires at `v0.1.0`**, which has no previous tag,
printing `NO-PREVIOUS-TAG..HEAD` where the old command printed nothing — a true firing, retroactive,
and arguably vacuous by nature rather than a defect. **V1 fires nowhere else**, and at every other tag
its file list is identical to the old command's. **V2 fires at no tag whose tree has blueprint
`README.md`s**, with all three counts equal at each. At any tag with no `blueprints/*/README.md` it
must print `0 blueprint READMEs` rather than nothing, which is the vacuity being removed.

## The controls, not derived from the hypothesis

The hypothesis is *"a row that prints only its failures cannot tell a pass from an absence, and the
remedy is a line stating what was examined and how much."* Every arm above is derived from it. These
are not, and each names a way the repair fails **if that understanding is wrong**.

**C1 — the repaired rows still catch everything the old ones caught.** The shape that has now found a
defect twice: a repair that quietly loses its predecessor's coverage while every registered arm
holds. Run old and new V1 against all twenty tags and diff the file lists; run old and new V2 against
`HEAD` and diff the printed lines. **Any difference other than the new leading line falsifies the
change**, whichever direction it goes.

**C2 — counts correct, fact wrong.** Scratch copy of `HEAD` with one blueprint's `Framework Version`
set back to `0.15.0`, every label intact. The repaired V2 prints `6, 6, 6` — a passing count line
above output that contains a real defect. **The count line must not be readable as the row's
verdict.** If a reader can stop at it, the repair has replaced a check that said nothing with one
that says the wrong thing, which is worse than what it replaced. This tests the understanding
directly: it asserts a positive line *supplements* the reading, and this is the case where it could
displace it.

**C3 — `$PREV` non-empty and wrong.** A scratch clone with an extra tag placed on an older commit, so
`git describe --tags --abbrev=0` resolves to a tag that is not the previous release. The range is
valid, the count is non-zero, and nothing fails. **The repair must make this visible** — the range is
printed and a reader sees the wrong tag name — and if it does not, then printing the range bought
nothing over printing a count, and the sentinel handles only the one case it was written for.

**What would falsify the change.** P1 printing something readable as a clean pass; P3a or P3b
reporting success; P4 failing; C1 showing any list differ; C2's defect being invisible in the row's
output; any tag under P5 whose file list changes.

**Not a release.** Everything here is under `.docs/`. Step 0 applies: no version bump, no
`Blueprint Version` bump, no tag.
