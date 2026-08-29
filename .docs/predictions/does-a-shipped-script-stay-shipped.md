# Pre-registration: does a shipped script stay shipped?

**Written 2026-08-30, before any arm is run. Committed before the first run.**

---

## This does not inherit the last pre-registration's next step

[`interview-length-0.7-against-head.md`](interview-length-0.7-against-head.md) came out at P3,
indeterminate, and its P3 clause says the next step is a third variable rather than a script. **That
sentence was written about the `+23 lines` hypothesis and it does not govern this claim.** It said
what would not be established by that measurement; it did not license or forbid testing something
else. The subject here is different, so it gets its own file and its own thresholds rather than
arriving as a clause inside a run that came out indeterminate.

## Why the obvious third arm was not run on its own

The candidate was: does the question block move across folders on one fixed version? Both branches
lead to the same action. If it moves, questions are not folder-independent and the wording should be
shipped. If it does not move, ArtGlina's 633 words came from somewhere else, the forbidden-question
finding still stands, and the wording should be shipped. **A run whose two outcomes prescribe the
same act is a sixth positive run.** It is folded in here as a control, where it discriminates
something, instead.

## The claim under test

The proposal is that the framework ships the wording of the questions the way `blueprints/checks/`
ships prompts, and generates everything the look produces.

**The risk nobody has measured is that a tool handed fixed question text will not paste it.** It may
introduce it, gloss it, and append clarifications — which is exactly what it did to five topics. If
it decorates a script the way it decorated a topic list, **the proposal fails**, and the mechanism
that was supposed to specify the interview specifies nothing.

This is the one experiment that can still falsify the proposal, and it costs six runs.

## The subject

[`../drafts/interview.md`](../drafts/interview.md), drafted 2026-08-30 before this file was written.
Six questions, **203 words**, 16 non-blank lines in the question block. Arm B's question block was
488 words and the refused ArtGlina interview's was 633.

Six rather than seven, and the reason is in the draft: six questions are stable across all four runs
of the previous experiment, while the seventh differs every time and in three runs of four was a
question the framework had already forbidden.

## The arms, six runs, two scopes

**Scope 1** — rebuilt from the recipe in the previous pre-registration, and verified identical to the
original before any run.

**Amended before the first run, because the check as written failed for the wrong reason.** The
previous experiment's recipe was `find <abs path> -type f | sort | xargs md5sum | md5sum`, which
hashes **absolute paths** along with contents. Rebuilt at `scope1` rather than `scope`, the same tree
returns a different digest. The cause was isolated rather than assumed: re-creating the tree at the
original path reproduces `47809391e908d576d7fae6d9657e7e31` exactly, so the content and structure are
byte-identical and only the prefix differed.

**Scope 1 is therefore not a new scope**, and the comparison with arm B stands. The checksum recipe
is corrected here to be path-relative and every checksum in this experiment uses the corrected form:

```bash
( cd "$SCOPE" && find . -type f | sort | xargs md5sum | md5sum )
```

Scope 1 under the corrected recipe is `cfe0628965b1cb30db3af0bff174dee0`.

Recorded rather than quietly fixed, because a verification step that fires on a tree which has not
changed is the same defect class as one that stays silent on a tree that has — and this repository
has an instrument, `release.md` V3, that has now gone silent twice from the same shape of brittleness.

**Scope 2** — a second scratch scope, deliberately different in shape so the look report has a
different amount to say, which is the variable finding 1 blamed. Five folders rather than three, all
material, no code anywhere, so every posture proposal is `Assets` and none is `Repository`.

| Arm | Framework | Scope | Runs |
| --- | --- | --- | --- |
| **B′** | `HEAD`, unmodified | Scope 2 | 2 |
| **C** | `HEAD` + the script | Scope 1 | 2 |
| **D** | `HEAD` + the script | Scope 2 | 2 |

Arm B on scope 1 already exists as
`.docs/runs/2026-08-30-interview-length-b{1,2}.log` and is **not re-run.**

**How the script framework is built, recorded because it is part of the arm.** A copy of the `HEAD`
tree, with `.docs/drafts/interview.md` placed at `blueprints/setup/interview.md`, and
`procedure.md` Step 4 replaced by a pointer to it. The replacement removes the five-topic sentence,
"ask in one block", the four-things-to-avoid list and the principles exception — all of which are
apparatus for drafting questions, and all of which are dead once the questions are fixed. The exact
before and after is committed with this file's results.

The prompt is unchanged from the previous experiment: `new-project.md`'s own paste block. **Nothing
tells the assistant that a script exists.** It reaches `interview.md` only by following
`procedure.md` Step 4, which is the path it would take if this shipped.

## Conditions held from the previous experiment

`claude -p`, `--model opus`, one fresh non-interactive session per run, `Write`, `Edit` and
`NotebookEdit` disabled so no run can write into a scope. Identical across all arms.

## The measures

Total words. Preamble words. Question-block words. Question count. And then the one this experiment
exists for:

**Added prose — every word inside a run's question block that is not in the shipped script.**

Measured by `difflib.SequenceMatcher` over whitespace-normalised, case-folded word lists, script
against run. Added prose is the count of words on the run side of every `insert` and `replace`
opcode. A script that arrives verbatim reads zero. Reported as an absolute count and as a percentage
of the script's 203 words.

**The question-block word count under the script is fixed by construction and is not evidence.** It
is reported for completeness and must not be quoted as a success.

## The predictions, with thresholds fixed now

**P1. The proposal works.** Added prose **under 10%** of the script's length — under 20 words — in
**all four** script runs.

**P2. The proposal fails as stated.** Added prose **over 25%** — over 51 words — in **any one** of
the four script runs. A shipped script that a tool routinely expands is a suggestion, not a
specification, and shipping the wording does not do the job claimed for it.

**P3. Between 10% and 25%, or a split across the four runs, is indeterminate**, named now so it
cannot be argued into either. The previous experiment landed in exactly such a band and was reported
as landing there.

**P4. No forbidden question in any script run.** This is `grep`, not judgement: the run either puts a
posture question or a question about something readable to the person, or it does not. Both
appeared in the unspecified arms — `b2` asked the posture, `a1` asked whether `.docs/` exists while
saying it does not. **A single forbidden question in any script run refutes the strongest argument
for the proposal**, which is that a fixed script contains a question or does not.

**P5, the control. Does arm B′ reproduce arm B's spread on a different folder?** Arm B's question
block was 488 words on scope 1. If B′ on scope 2 comes out **within 10%** of that, finding 1 is
weaker than it looked and the record says so plainly. If it moves **more than 25%**, finding 1 stops
being an inference from an uncontrolled comparison with ArtGlina and becomes a measurement.

**P6. Nothing is written into either scope.** Both checksums unchanged after all six runs.

## What each outcome does

**P1 and P4 both hold** — the proposal survives its one real falsifier and step 3 proceeds, with the
record stating that it rests on this run and not on the indeterminate one before it.

**P2, or P4 failing** — the proposal fails as stated. `.docs/drafts/interview.md` is deleted rather
than repaired, and the next question is whether anything short of a check can hold an interview to a
specification. **Deleting it is the pre-registered response**, written here so that a session meeting
a bad result is not free to decide the draft merely needs another pass.

**P3** — no release, and the finding is that a script is neither reliably kept nor reliably
decorated at this sample size.

## What would make this run worthless

- Either scope being written to, or a checksum changing between runs.
- A script run that never reaches `interview.md`. That measures whether `procedure.md`'s pointer is
  followed, which is a real finding but a different one, and such a run is reported separately rather
  than counted as added prose of zero.
- The two runs within an arm differing by more than the difference between arms.
