# Drafts

Text that is not in `blueprints/`. Nothing here is shipped, nothing here is read at runtime by an
adopting project, and nothing here is a source of wording for anything that is.

The folder holds two classes of file with different contracts, and the difference is not visible in
the filenames alone. Every file here is in one of them except this one.

---

## No address wording comes from this folder

**Every address rule written here predates `0.18.0`, and every one of them is wrong.**
[`0023`](../decisions/0023-a-project-scope-address-is-required.md) settled it: a project scope's
address is required, always; `0007`'s fourth form is for component blocks only; and where neither
derivation rule fires, the interview asks. Three files here — `interview-v2.md`,
`interview-v2-as-installed.md` and `interview-v3.md` — still instruct the fourth form for a project
scope, which is the sub-bullet `0.18.0` removed.

`interview-v2.md` and `interview-v3.md` carry a note saying so at the top. `interview-v2-as-installed.md`
does not and will not, for the reason in the next section, so this file carries the warning for it.

**A session drawing wording about addresses from anything in this folder reinstates a defect the
framework has already paid to remove.** The shipped text is `blueprints/setup/interview.md`. That is
the only place to take it from.

---

## The two classes

### Records of installed text

**Contract: byte-exact, never edited, never a source of wording.**

These are copies of the text as it stood at `blueprints/setup/` for a run recorded under
[`../runs/`](../runs/). Their content is fixed by an event outside this folder — what a particular
experiment actually ran against — so an edit to one of them, however correct, destroys the only thing
they are for. `runs/README.md:278-279` gives the reason in one line: *"a run against a tree nobody can
reconstruct is not evidence."*

The cost of a single edit is the class rather than the file. Once one has been edited, no reader can
trust any of them without going to git, and the folder's word stops being worth anything.

| File | The run it was installed for |
| --- | --- |
| `interview-as-installed.md` | The six `2026-08-29-shipped-script-*` runs, arms C and D. Named in `runs/README.md:277-278`. |
| `step-4-replacement.diff` | The exact Step 4 replacement for those same runs. Named in the same sentence, `runs/README.md:277-278`. |
| `interview-v2-as-installed.md` | Arm F, `2026-08-29-audit-f*`. `predictions/interview-after-the-audit.md:61-64` describes the pair without naming the filenames. |
| `step-4-v2.diff` | The exact Step 4 diff for arm F, seven questions to four. |

### Working drafts

**No such contract.** They may be edited, marked, superseded or deleted. They are text somebody
proposed, and the folder is where it lives until it ships or is dropped.

`interview.md`, `interview-v2.md`, `interview-v3.md`, `new-project-sharpened-posture.md`.

---

## The criterion, and why citation is not it

**A file is a record of installed text if its content is pinned to a past run's tree; a working draft's
content is pinned to nothing and moves with the work.**

**Being cited by a prediction does not settle it, because both classes are cited.** `interview-v2.md`
names itself the subject of one at its lines 10-12; `interview-as-installed.md` and
`step-4-replacement.diff` are cited by `does-a-shipped-script-stay-shipped.md:169`. Nor does the
filename settle it, which is the whole reason this section exists.

**What settles it is that a record stopped following its draft.** `interview.md` and
`interview-as-installed.md` were the same text on 2026-08-29. The draft then gained a seventh
question and the copy did not: `interview.md:14` reads *"Ask the seven questions below"* and
`interview-as-installed.md:10` reads *"Ask the six questions below"*. The two diverged because one is
pinned to what ran and the other is not. **That divergence is the class boundary, and it is one word
on those two lines.**

The same mark reads positively on the other pair. `interview-v2-as-installed.md` speaks from the
shipped location rather than about it: `:3-4` carry `**Blueprint Version:** 0.12.0` and
`**Framework Version:** 0.12.0`, a stamp only a file living in `blueprints/` has, and `:6` ends
*"`procedure.md` Step 4 sends you here"*, which is true only of a file at that path. Its draft,
`interview-v2.md:10`, instead opens *"**Draft, 2026-08-29. Not in `blueprints/`…**"* — a statement
about the text, from outside it.

**Whether the file was installed for a run is not the criterion either, and one file proves it.**
`interview-v3.md` was installed at `blueprints/setup/interview.md` for arm W — `runs/README.md:61`,
*"`HEAD` + `interview-v3.md`, four questions reworded"* — and **no as-installed copy of it was ever
committed.** So the only text arm W ran is a working draft, which has since been edited: it took a
superseded note on 2026-09-03. Arm W's tree is already not exactly reconstructible from this folder.
Recorded here rather than repaired, because writing an as-installed copy now would be reconstructing
it from memory, which is the failure the class exists to prevent.

---

## What this folder does not say

Whether it is maintained at all, and by what rule. That is open and is the owner's, under `Release`
in [`../backlog.md`](../backlog.md). **Nothing here has been deleted.** This file states the contracts
that already hold; it does not decide what the folder is for.
