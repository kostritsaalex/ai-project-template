# Releasing

Read this before cutting a release of the framework itself. It is not about adopted projects; the
checks in `blueprints/checks/` cover those and cover nothing here.

It exists because releases have gone wrong twice in ways nothing would have caught. `0.6.0` bumped
all four blueprint versions when one blueprint had changed. `0.8.0` came within a sentence of
shipping a measurement nobody had re-taken.

---

## The steps

**0. A change under `.docs/` never causes a release.** A version number describes what an adopting
project receives, which is `blueprints/`. This procedure, the backlog, the decisions, the
predictions and the logs are the framework's own workshop, and bumping a version for them would
announce a change nobody adopting it can see. Such a change may be described in a release that is
happening anyway, as `0.9.3` described the move of the verification step, but it never causes one.

**1. Bump the blueprints that changed, and only those.** A blueprint version records that *that*
blueprint moved. Bumping one that did not moves a number for a document nobody edited, and the next
reader has no way to tell which of the four actually changed. `git diff <last tag>..HEAD -- blueprints/`
answers it.

**2. Bump `Framework Version` in all four blueprint READMEs.** That one is the release, so it moves
everywhere, including in blueprints that did not change.

**3. Re-measure the shipped-line metric and write it into the `README`.** Do not carry the previous
number forward, and do not reason that nothing can have changed it. Run:

```bash
python3 - <<'EOF'
import io, re
def shipped(path):
    s = re.sub(r'<!--.*?-->', '', io.open(path, encoding='utf-8').read(), flags=re.S)
    lines = s.split('\n'); i = 0
    if lines and lines[0].startswith('> **BLUEPRINT FILE.'):
        while i < len(lines) and (lines[i].startswith('>') or not lines[i].strip()):
            i += 1
        if i < len(lines) and lines[i].strip() == '---':
            i += 1
    return len([l for l in lines[i:] if l.strip()])
scope = ['blueprints/project/PROJECT.md', 'blueprints/project/AGENTS.md', 'blueprints/project/CLAUDE.md']
comp  = ['blueprints/component/AGENTS.md', 'blueprints/component/CLAUDE.md']
for label, files in (('project scope', scope), ('component', comp)):
    print(label, sum(shipped(f) for f in files), [shipped(f) for f in files])
EOF
```

The metric is non-blank lines, with the blueprint notice and every HTML comment stripped, summed
across the files a scope actually ships. An override is not in it: it exists only when a folder has
something to add, and since `0.8.0` that is rarer than it was.

**4. If the release changes a rule, confirm its decision record exists** and that the `CHANGELOG`
entry links to it. A rule that changed without a record is a rule nobody can argue with later.

**5. Write the `CHANGELOG` entry, and name what the release removed.** Principle 7 is not
decoration. A release that only adds should say so explicitly rather than leaving the omission to be
noticed.

**6. Commit.** Everything the release changes, in one commit.

**One exception, and it is not a licence to split a release.** A pre-registration committed between
the work and the release is not squashed into it. `0.11.0` is two commits with one between them: the
release was committed and verified, a placeholder check was then pre-registered and run, and its
finding was committed on top. Amending over the pre-registration would have destroyed the only thing
that makes a prediction worth writing, which is that it demonstrably preceded its runs. Step 7
verifies `HEAD` either way, so nothing is lost by the split. Nothing is verified before this point,
because until the work is committed there is no tree to verify: `$PREV..HEAD` cannot see uncommitted
files and a dirty `git status` is expected rather than diagnostic.

**7. Verify the committed tree, before the tag.**

A release is the moment a document's claim about the tree is most likely to be false, and it was the
one moment nothing checked. Two tags prove it: `v0.9.0` points at a tree whose `runs/` index names
five logs the tree does not contain, and `v0.9.1` at a tree whose backlog announces `0.9.0`.

**The position is the whole design.** This ran before the commit once and had to be completed by the
operator to pass: `$PREV..HEAD` showed nothing, so a `--cached` command was invented on the spot, and
`git status` printed ten modified files against a criterion that said it must print none, and the
release went ahead anyway. Between commit and tag, `HEAD` is exactly the tree the tag will name,
`$PREV..HEAD` is the release's own diff, and a clean `git status` means something. Verifying after the
tag, which is the only other place these commands work, can report a defect that is already
permanent.

Run all four. Each prints its own evidence; read it rather than trusting an exit code. If a command
here does not answer its question and you find yourself typing another one, stop: the step is wrong
and the command you reached for is the finding.

```bash
PREV=$(git describe --tags --abbrev=0)

# V1. What this release actually changed.
git diff --name-only $PREV..HEAD

# V2. Every version string, so the new number is where it belongs and nowhere else.
grep -rn "Blueprint Version:\|Framework Version:" blueprints/*/README.md

# V3. The version this release calls itself, against the version it ships.
CL=$(grep -m1 '^## ' CHANGELOG.md | grep -oE '[0-9]+\.[0-9]+\.[0-9]+'); echo "CHANGELOG ${CL:-MISSING}"
grep -L "Framework Version:\*\* ${CL:-NO-VERSION}" blueprints/*/README.md

# V4. Nothing this release documents is untracked, ignored, or uncommitted.
git status --porcelain
git status --porcelain --ignored=matching .docs/ blueprints/ | grep '^!!'
IDX=$(grep -oE '^[0-9a-f]{32}  \S+' .docs/runs/README.md | awk '{print $2}' | sort -u)
TREE=$(git ls-files .docs/runs/ | grep '\.log$' | sed 's|^\.docs/runs/||' | sort -u)
echo "runs index: $(grep -c . <<<"$IDX") named, $(grep -c . <<<"$TREE") tracked"
comm -23 <(grep . <<<"$IDX") <(grep . <<<"$TREE") | sed 's/^/NAMED, NOT TRACKED: /'
comm -13 <(grep . <<<"$IDX") <(grep . <<<"$TREE") | sed 's/^/TRACKED, NOT NAMED: /'
```

What each has to show:

- **V1.** Every file the changelog's top entry claims to have changed appears in the list, and
  nothing in the list is unaccounted for by the entry. This is read, not computed: the entry is
  prose.
  **When a check prompt is in the list, diff its prompt block and read the diff against what the
  entry says about it.** `git diff $PREV..HEAD -- blueprints/checks/` is the command. An entry
  claiming a removal while the block grew is a failure of this step, not a wording preference:
  `0.9.1` shipped exactly that, stating the cascade as one condition and then restating the three
  cases it replaced, so three lines became five under a heading that said `Removed`.
- **V2.** Every `Framework Version` reads the new number. **A `Blueprint Version` reads the new
  number if and only if that blueprint changed in some file other than its `README.md`'s version
  lines**, and the old one otherwise.
  That wording is deliberate and replaces "appears in V1's list", which contradicted step 1 in this
  same file: step 2 bumps `Framework Version` in every blueprint `README.md`, so every blueprint
  always appears in V1's list, and the old wording therefore demanded that every `Blueprint Version`
  move on every release. Every release had silently read it the way it is now written. Found by
  running the step rather than by reading it, on `0.11.0`.
- **V3.** The version prints, and no file is listed under it. Any blueprint `README.md` that appears
  does not carry that number; a top entry that is not a version prints `MISSING` and lists every
  blueprint, which is why the version is taken from the first `##` heading and not from the first one
  that happens to look like a version. Whether the number is the intended one is the reader's, and the only judgement here.
  **It compares two fields because it used to grep prose.** The old row matched a fixed phrase in the
  backlog. It fired five times, caught nothing, and by `0.16.0` was returning the sentence written to
  complain about it. The backlog is no longer read here and its version line may lag: a `.docs/`
  change never causes a release, so that line is a convenience. What replaced it supplies V2's missing
  referent — V2 asks whether every `Framework Version` reads the new number, and V2's own output never
  says what the new number is. See [`0019`](decisions/0019-a-check-compares-fields-not-prose.md).
- **V4.** The first two commands print nothing. A file present on disk and excluded by an ignore
  rule is the case worth catching, because `git add` does not report what it declined to add.
  **The third prints a count line in every outcome**, and a pass is two equal counts with no names
  under either label. It compares two sets because it used to compare one set against nothing: keyed
  on the checksum block's two-space format alone, it printed the empty string both when every log
  was tracked and when the block matched nothing at all, so one `sed` over that whitespace blinded
  it without touching a fact it guards. Both directions are in scope. This is the check `v0.9.0`
  failed. See [`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md).

If anything fails here, amend the commit and run it again. That is what this step is placed before
the tag to make possible.

**If anything is edited after this step runs, the step runs again before the tag.** That is the whole
reason it sits where it sits. `0.10.1` was tagged after step 7 had passed and after the backlog had
been edited, and the step as it then stood would have failed on that edit. It was found by hand afterwards, when the tag already
existed.

**8. Tag and push both.** `git tag -a vX.Y.Z`, then push `main` and the tag. A tag that stays local
is a release nobody else has.

---

## Why this file exists at all

It is the first document written after [`0008`](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md)
adopted the razor, so it is the first thing the razor should have been aimed at. A razor whose first
opportunity is skipped is a razor adopted on paper.

It passes. A releasing session demonstrably does not take these steps unprompted: `0.6.0` bumped four
blueprint versions when one blueprint had changed, and `0.8.0` was a sentence away from shipping a
number nobody had re-taken. Both were done by a session that knew the framework well. That is the
difference between a rule and a habit, and it is the only justification this file has.

---

## What this does not cover

Whether the release is a good idea, whether the version number is right, and whether anything in it
was measured rather than argued. Those are judgment, and this file is for the mechanical part that
has already failed twice without one.
