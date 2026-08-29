# Audit: `structure-check`'s fourteen rows

**Read:** 2026-08-29. **Nothing is proposed here and nothing was changed in the same pass.** Every
defect this repository produced today came from a fix written while composing the thing that carried
it. This document ends with a ranked list.

`structure-check` is the check every adopted project actually runs, and it has fourteen rows against
`registry-check`'s seven.

---

## The evidence that does not exist

The plan for this audit was to check each suspicion against `structure-check`'s five logged runs
before proposing anything. **Those logs are not in the repository.** `.docs/runs/` holds fifteen
files and every one is a `registry-check` run; `git log --diff-filter=D` shows none were ever
removed. `structure-check`'s runs happened during the `0.6.0` and `0.7.0` validations, before
`.docs/runs/` existed.

What survives of them is the backlog's prose: "14/14 twice before the fixes, 14/14 after", and the
paragraphs beside it. That is a claim about a past run, restated from memory, checkable against
nothing — the class catalogued this morning, and the one that put a false sentence into three
documents.

So this audit is a reading and only a reading. **Where a suspicion needs evidence of behaviour, it is
marked as needing a fresh run, not settled by appeal to unlogged history.** The rows where I would
have opened a log and could not are 4, 5, 6, 11 and 13: each turns on what a tool actually produced
rather than on what the row says.

---

## Shapes

Two are inherited from `registry-check`'s own defects.

- **E — evidence cannot be produced as written.** The row asks for something no honest reading of it
  can supply, so a tool invents a substitute. `registry-check` check 6 was this.
- **D — depends on an earlier row without saying what happens when that one fails.** `registry-check`
  rows 2 to 6 were this.

Two more were found here and are named as required.

- **B — bundled verdict.** The row carries several distinct claims and returns one result, so a pass
  does not say what was checked and a fail does not say what failed.
- **K — knowledge the prompt does not contain and forbids fetching.** The prompt is self-contained by
  design and reads only the folder. A row whose correct application needs a fact stated nowhere in it
  leaves the tool to supply that fact. One instance, named below, so this is a candidate shape rather
  than an established one.

---

## The rows

| # | What the row asks | What a tool must supply that the row does not say | Shape | Settled by reading alone? |
| --- | --- | --- | --- | --- |
| 1 | No HTML comment in any file | Which files "any file" means. The read list is stated earlier in the prompt, so the gap is small, but the row's own scope is unstated | — | Yes |
| 2 | No unfilled placeholder | Nothing material. The definition is tight and the pass case is covered by the absence paragraph | — | Yes |
| 3 | No blueprint notice | Nothing. It already carries the carve-out for a document's own header, which exists because it once fired wrongly | — | Yes |
| 4 | The two stubs carry the same text | The normalisation. "Ignoring blank lines" is stated; trailing whitespace, differing line wrapping and punctuation are not. A tool must choose line-wise or token-wise comparison and does not say which it chose | E | No — needs a run |
| 5 | Scope holds `PROJECT.md`, holds no override; list every filename | Which of the two claims a failure refers to. Also why a full listing is the evidence for a question about two named files | B, E | No — needs a run |
| 6 | Component holds no `PROJECT.md`; list every filename | Same as 5's second half. The only fact needed is whether one named file is present, and the row asks for the whole folder instead | E | No — needs a run |
| 7 | Both stubs name this component, and name the same one | The matching standard. `registry-check` 3 says "exactly … a difference in wording, case or spacing fails"; this row says only "the same one" | K (mild) | Yes |
| 8 | Both stubs give a parent address; **three** forms listed | Why this row lists three address forms while row 11, in the same prompt, lists four. **Checked against the blueprint, 2026-08-29:** `0001` decides that a project scope may live anywhere "it has an address that resolves from outside the machine it sits on", so a scope may not be addressless and there is no fourth form for a parent. Three is right; the gap is the missing rationale and nothing more | K | Yes, and now settled |
| 9 | Both stubs say what to do when the parent is unreachable | What counts as saying it. The blueprint's sentence is fixed text, so in practice this is quotable, but the row states no acceptance criterion | — | Yes |
| 10 | If an override is present: stubs name it, and it carries no parent address and no posture | **What happens when the stubs name an override that is not present.** The row is one-directional and returns n/a when neither file is present, so that case passes silently. It is a known real defect, recorded in the backlog, and `registry-check` 5 was written to catch it in both directions | D, B | Yes — the defect is visible in the wording |
| 11 | Every registry block: name, posture word, travelling rule, address in one of four forms, `../` rejected, local-path placement, empty-registry case | Which block and which claim a verdict refers to. One row covers the whole registry and every block in it, so a scope with six components gets one result. This is the "a count of checks would hide a component" problem `registry-check` fixed by going per-component | B | No — needs a run |
| 12 | Local paths written `~/`, no username, with the symlink exception | Nothing material. The exception is explicit and the interaction with row 13's exclusions is deliberate: `0.7.0` recorded 12 passing a line 11 failed, both correctly | — | Yes |
| 13 | Every location the documents point to exists, or is said not to | The positive definition. Four exclusions are given; the inclusion is "a documentation folder, a decisions folder, a subfolder holding a component, any other file or folder they say is here". "Any other" is unbounded, so the tool decides what counts as being pointed at | E | No — needs a run |
| 14 | If the document says what makes its local path true, it names the arrangement and the command | **Nothing distinguishes "correctly silent" from "wrongly silent".** A document that should carry a path note and does not gets `n/a`, exactly as one that correctly carries none. The backlog already records this: "it is `n/a` when a document says nothing about its path, so silence passes" | D | Yes — the defect is visible in the wording |

---

## Ranked, by whether a wrong answer would be visible

A row that fails loudly when it is wrong costs little. A row that passes while auditing nothing is
what `registry-check` check 6 was, and what the all-`n/a` table nearly became.

1. **Row 10.** A wrong answer is an `n/a` on a component whose stubs name a file that is gone. Silent,
   and it has already happened in this project.
   **Run 2026-08-29 and confirmed exactly, twice — and the rank overstates the consequence.** Row 13
   caught the same defect in both runs, so the check is not blind to it. Row 10's cost is a verdict
   in the wrong place rather than a miss. See
   [`../predictions/override-deleted-both-checks.md`](../predictions/override-deleted-both-checks.md).
2. **Row 14.** A wrong answer is an `n/a` on a document missing a path note it needs. Silent, and
   indistinguishable from the correct case by construction.
3. **Row 4.** A wrong answer is a pass on two stubs that differ. Silent, and it defeats the one thing
   the pair of files exists to guarantee: a rule that fires for one tool and not another.
4. **Row 11.** A wrong answer is a pass over a registry whose blocks were not all examined. Silent at
   the scale that matters, because one verdict covers every component.
5. **Row 6.** A wrong answer is a pass produced from a listing rather than a fact. Its twin in
   `registry-check` flipped between runs for a week.
6. **Row 13.** Its unbounded definition caught the deleted override that row 10 abstained on, twice,
   which makes the looseness load-bearing rather than merely risky. Any change to this row has to
   keep that. A wrong answer is a pass over a location nobody resolved, or a listing of locations
   that do not exist. The second has been observed three times in this project and is recorded.
7. **Row 5.** As row 6, plus a bundled verdict that does not say which half failed.
8. **Row 8.** A wrong answer is most likely a *fail* on a correct document, because the tool applies
   row 11's four forms here. Loud, and therefore cheap.
9. **Row 7.** A wrong answer needs two stubs naming the component differently enough to matter and a
   tool choosing a lax standard. Quotable either way.
10. **Rows 1, 2, 3, 9, 12.** Evidence is a quotation or a reproducible search. A wrong answer is
    visible to anyone who opens the file.

---

## Settled since the reading

**Row 14 — decided, not fixed.** [`0010`](../decisions/0010-the-path-note-stays-optional.md) rejects
the remedy `0007` used for addresses and records the silence as a declared limit, now written into
`structure-check`'s own notes. The reasoning turns on the two cases being different: an address is
load-bearing for every reader, a path note only where a boundary exists. The compromise of gating the
requirement on the session note is closed by experiment, having been tried before `0.6.0` and having
caused the row never to run.

**Row 8 — settled by reading the blueprint, and K survives as a shape.** The suspicion was that three
forms against row 11's four might mean a *missing form* rather than a missing rationale: if a project
scope could itself be addressless, its components would have nothing valid to write, since a bare
local path fails row 8 and "none" is not among its three.

It cannot. [`0001`](../decisions/0001-project-scope-need-not-be-a-repository.md) decides that a
project scope may live anywhere "it has an address that resolves from outside the machine it sits
on", and `0007` says the gap for an addressless component "runs one way": its stubs still point
upward with an address that resolves from anywhere. So row 8's three forms are right and complete.

What remains is only the unexplained asymmetry, and **the symptom has never been observed, because
`structure-check` has never been logged.** That is not evidence of absence. It stays a suspicion
rather than a defect, and it is free to test the next time this check runs against a component whose
parent is addressed in a synced store.

---

# Ownership map

**Read:** 2026-08-29, after the deleted-override runs. One line per defect the check claims to catch,
naming the row that owns it and any row that also fires. Written because the overlap between rows 10
and 13 was discovered by accident in the nineteenth log, and until ownership is written down, a
repair to one row can silently remove coverage a neighbour was providing or duplicate it.

| Defect | Owns it | Also fires | Note |
| --- | --- | --- | --- |
| A leftover HTML comment | 1 | — | |
| An unfilled placeholder | 2 | — | |
| The blueprint notice left in place | 3 | — | |
| The two stubs have diverged | 4 | 7, partly | 7 catches divergence only in the naming line; every other difference is 4's alone |
| A project scope with no `PROJECT.md` | 5 | — | |
| A project scope holding an override at its root | 5 | — | 10 is component-only and goes n/a here |
| A component holding a `PROJECT.md` | 6 | — | |
| Stubs that do not name the component, or name different ones | 7 | 4 | 4 fires because the naming line is text the two stubs share |
| A parent address missing, or in none of the three forms | 8 | — | |
| Stubs missing the unreachable-parent instruction | 9 | — | |
| An override present that the stubs do not name | 10 | — | |
| An override carrying a parent address | 10 | — | |
| An override stating the folder's posture | 10 | — | |
| **Stubs naming an override that is not present** | **13 in practice; 10 should** | 13 | The mis-routing. Run twice on 2026-08-29: 10 returns n/a, 13 fails and quotes both stubs |
| A registry block missing a name, a posture word or an address | 11 | — | |
| A `Repository` block without the travelling rule | 11 | — | |
| A registry address in none of the four forms, or `../` | 11 | 12, differently | 12 asks what form a path is written in, 11 what slot it sits in. `0.7.0` recorded both reading one line, one failing and one passing, both right |
| An empty registry with no sentence saying so | 11 | — | |
| A local path with a username, or absolute | 12 | — | |
| A location the documents point to that does not exist | 13 | — | |
| A path note naming an arrangement without the command | 14 | — | |

## Where no row fires

- **A component missing one or both stubs entirely.** Rows 4 and 7 would fail for want of something
  to quote, but neither claims the defect, and a failure there reports a divergence or a naming
  problem rather than an absent file. `registry-check` row 2 owns this explicitly; `structure-check`
  has no owner for it.
- **A `Components` section absent altogether from a project scope.** Row 11 covers a registry with no
  blocks and no sentence explaining that, but a document with no such section at all is not clearly
  in its scope.
- **A parent address that is well formed and wrong.** Owned by `registry-check` 4, and already
  declared under "What this check cannot see".

## Where two rows fire and which should

- **Stubs naming an absent override.** Row 10 should own it: it is the row about overrides, and its
  wording already carries the other three override defects. Row 13 currently owns it in fact.
  **Making 10 bidirectional without touching 13 would give one defect two failing rows, and
  "Failed checks: N" would count it twice.** `registry-check` met this and answered with the cascade:
  one defect, one verdict. Any repair here has to decide that first.
- **The naming line.** Rows 4 and 7 both fire when it differs between stubs. This one is benign: 7 is
  a specific claim about a specific line and 4 is the general one, and a document failing both is
  failing for two true reasons.

---

# Re-ranked, over two axes

The first ranking used one axis: whether a wrong answer would be visible. The deleted-override runs
supplied the second: whether another row covers the same defect. **A row can be wrong and harmless.**
Re-derived over both, using the map above. The readings themselves are unchanged.

| Rank | Row | Visible when wrong? | Covered elsewhere? | Moved |
| --- | --- | --- | --- | --- |
| — | **4** | — | — | **repaired and run both ways, 2026-08-29; leaves the ranking** |
| 2 | **11** | No — a pass over a registry whose blocks were not all examined | No | up from 4 |
| 3 | **13** | No | No, and it now carries a second defect nobody else catches | **up from 6** |
| 4 | **6** | No — a pass produced from a listing rather than a fact | No. Row 5 is scope-only | up from 5 |
| 5 | **5** | No, and bundled | No | up from 7 |
| 6 | **10** | No — an n/a on stubs naming a file that is gone | **Yes, by 13, demonstrated twice** | **down from 1** |
| 7 | **8** | Mostly yes: the likely wrong answer is a fail on a correct document | No | 8, unchanged |
| 8 | **7** | Yes — quotable either way | Partly, by 4 | 9, roughly unchanged |
| 9 | **1, 2, 3, 9, 12** | Yes — a quotation or a reproducible search | No, and none needed | unchanged |
| — | **14** | No | No | **removed from the ranking** |

## Which moved and why

**Row 10, first to sixth.** The whole of its rank was the belief that a deleted override passes
unnoticed. It does not: row 13 fails it, twice, quoting both stubs. Row 10 is still wrong, and the
cost of its wrongness is a verdict filed in the wrong place — a real defect for anyone repairing the
check, and nearly nothing for anyone running it.

**Row 13, sixth to third.** It rises for the opposite reason. It is the only row catching two
distinct defects, one of which it acquired by accident, and there is no second net under it. A
mis-repair here removes coverage twice over, and the property that would be most tempting to tighten
— the unbounded "any other file or folder they say is here" — is exactly what does the catching.

**Rows 4 and 11 rise into the top two** without changing at all: they were second-axis winners all
along, and nothing covers either. Row 11 is still the sharpest single item, one verdict over an
entire registry.

**Row 4 then left the ranking the same day.** It was rewritten to name the comparison it makes and
run in both directions, passing twice on correct stubs and failing on one word changed in one file,
quoting the pair with a line number from each. See
[`../predictions/structure-check-row4.md`](../predictions/structure-check-row4.md). **Row 11 is now
the top open item.**

**Row 14 leaves the ranking.** [`0010`](../decisions/0010-the-path-note-stays-optional.md) decided
it: the silence is a declared limit, not an open defect, so it is not competing for repair.

## What the second axis is worth

It reordered half the list and it demoted the item that was first. Neither axis alone was enough:
visibility said row 10 mattered most, coverage says it matters least of the silent rows. **And the
coverage axis could not have been derived by reading** — the overlap it turns on was found by running
a check against a planted defect and watching a row nobody was looking at do the work.
