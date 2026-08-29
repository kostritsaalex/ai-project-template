# Releasing

Read this before cutting a release of the framework itself. It is not about adopted projects; the
checks in `blueprints/checks/` cover those and cover nothing here.

It exists because releases have gone wrong twice in ways nothing would have caught. `0.6.0` bumped
all four blueprint versions when one blueprint had changed. `0.8.0` came within a sentence of
shipping a measurement nobody had re-taken.

---

## The steps

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

**6. Commit, tag, push both.** `git tag -a vX.Y.Z`, then push `main` and the tag. A tag that stays
local is a release nobody else has.

---

## What this does not cover

Whether the release is a good idea, whether the version number is right, and whether anything in it
was measured rather than argued. Those are judgment, and this file is for the mechanical part that
has already failed twice without one.
