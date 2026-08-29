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

**6. Commit.** Everything the release changes, in one commit. Nothing is verified before this point,
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

# V3. The version this release calls itself, in both places that name it.
head -40 CHANGELOG.md | grep -m1 '^## \['
grep -m1 "is released, tagged and pushed" .docs/backlog.md

# V4. Nothing this release documents is untracked, ignored, or uncommitted.
git status --porcelain
git status --porcelain --ignored=matching .docs/ blueprints/ | grep '^!!'
grep -oE '^[0-9a-f]{32}  \S+' .docs/runs/README.md | awk '{print $2}' | while read f; do
  git ls-files --error-unmatch ".docs/runs/$f" >/dev/null 2>&1 || echo "NOT TRACKED: $f"
done
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
- **V2.** Every `Framework Version` reads the new number. A `Blueprint Version` reads the new number
  if and only if that blueprint appears in V1's list, and the old one otherwise.
- **V3.** Both lines name the version about to be tagged. This is the check `v0.9.1` failed, and it
  failed it in a way worth knowing: run against that tag, the backlog grep returns nothing at all,
  because the section had been rewritten and no longer contained the phrase. So the row fires on an
  absent line as readily as on a wrong number, which is the right behaviour and is also a warning.
  The command is keyed on a phrase a person can rewrite without noticing. If it returns nothing, look
  at the backlog before concluding anything: the line may be missing, or it may simply be worded
  differently now.
- **V4.** All three commands print nothing. A file present on disk and excluded by an ignore rule is
  the case worth catching, because `git add` does not report what it declined to add. This is the
  check `v0.9.0` failed.

If anything fails here, amend the commit and run it again. That is what this step is placed before
the tag to make possible.

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
