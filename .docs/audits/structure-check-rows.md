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
| 8 | Both stubs give a parent address; **three** forms listed | Why this row lists three address forms while row 11, in the same prompt, lists four. The answer is real and correct — a parent always has an address, the fourth form exists only for a component nobody can reach — but it is in `0007`, and the prompt forbids reading outside the folder | K | Yes, but only by someone who already knows |
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
2. **Row 14.** A wrong answer is an `n/a` on a document missing a path note it needs. Silent, and
   indistinguishable from the correct case by construction.
3. **Row 4.** A wrong answer is a pass on two stubs that differ. Silent, and it defeats the one thing
   the pair of files exists to guarantee: a rule that fires for one tool and not another.
4. **Row 11.** A wrong answer is a pass over a registry whose blocks were not all examined. Silent at
   the scale that matters, because one verdict covers every component.
5. **Row 6.** A wrong answer is a pass produced from a listing rather than a fact. Its twin in
   `registry-check` flipped between runs for a week.
6. **Row 13.** A wrong answer is a pass over a location nobody resolved, or a listing of locations
   that do not exist. The second has been observed three times in this project and is recorded.
7. **Row 5.** As row 6, plus a bundled verdict that does not say which half failed.
8. **Row 8.** A wrong answer is most likely a *fail* on a correct document, because the tool applies
   row 11's four forms here. Loud, and therefore cheap.
9. **Row 7.** A wrong answer needs two stubs naming the component differently enough to matter and a
   tool choosing a lax standard. Quotable either way.
10. **Rows 1, 2, 3, 9, 12.** Evidence is a quotation or a reproducible search. A wrong answer is
    visible to anyone who opens the file.
