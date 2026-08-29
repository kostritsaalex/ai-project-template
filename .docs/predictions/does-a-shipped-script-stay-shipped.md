# Pre-registration: does a shipped script stay shipped?

**Written 2026-08-29, before any arm is run. Committed before the first run.**

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

[`../drafts/interview.md`](../drafts/interview.md), drafted 2026-08-29 before this file was written.
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
`.docs/runs/2026-08-29-interview-length-b{1,2}.log` and is **not re-run.**

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

---

# Results, scored 2026-08-29

Six runs, logs committed as `.docs/runs/2026-08-29-shipped-script-*.log`. The installed
`interview.md` and the exact Step 4 replacement are committed as
`.docs/drafts/interview-as-installed.md` and `.docs/drafts/step-4-replacement.diff`.

## Validity

**P6 holds.** Scope 1 `cfe0628965b1cb30db3af0bff174dee0` and scope 2 `d24c2a045ebd3e87e47cb0b199472ded`,
unchanged after all six runs.

**Every script run reached `interview.md`.** None cites it by name, which is why the first check for
it looked like a failure, but all four reproduced its text, so the pointer in Step 4 was followed.
The "reported separately" clause does not fire.

## The measures

| Arm | Framework | Scope | total | preamble | question block |
| --- | --- | --- | --- | --- | --- |
| B | `HEAD` | 1 | 676 / 658 | 172 / 156 | 504 / 502 |
| B′ | `HEAD` | 2 | 609 / 717 | 122 / 233 | 487 / 484 |
| C | `HEAD` + script | 1 | 334 / 325 | 131 / 122 | **203 / 203** |
| D | `HEAD` + script | 2 | 355 / 347 | 152 / 139 | **203 / 208** |

**Added prose: 0 words, 0.0%, in all four script runs.** `difflib` similarity 1.000 against the
script in every one. Nothing was inserted, nothing glossed, nothing appended after question 6.

## Scoring

**P1 confirmed.** Added prose is zero in all four runs, against a threshold of under 10%. **The script
stays shipped.** The proposal survives the one experiment that could refute it.

**P2 did not occur.** No run came near 25%.

**P4 holds, and the automated test for it did not.** The question block in every script run is
byte-identical to the script, so the forbidden-question test reduces to a test of the script itself,
and the script contains no posture question, no `.docs` question and no request for the local path.
**The keyword grep registered as "grep, not judgement" produced false positives on all four runs**,
firing on the declarative sentence "Your local path is already settled" inside question 5. A keyword
match cannot distinguish asking from stating. That is the same defect this repository keeps finding
in its own check rows — a test that looks mechanical and is not — and it is recorded here because it
was written into a pre-registration one day after the last instance was catalogued.

**P5: the control weakens finding 1, and finding 1 was mine.** Arm B's question block on scope 1
averaged 503 words; arm B′ on scope 2 averaged 485.5. **A change of −3.5%**, inside the 10% band that
was pre-registered as weakening it.

So the question block does **not** move materially across folders on one fixed version. Two scopes as
different as three folders of mixed code and material and five folders of pure material moved it by
seventeen words. **The claim that ArtGlina's 633-word question block demonstrated folder-driven
variance is not supported**, and the more likely explanations are the two confounds already recorded
against it: the reviewer's blindness instruction, and a real project with more to say than a scratch
tree.

Finding 1 is therefore marked down. It was offered as the strongest unregistered argument for the
proposal after the previous run came out indeterminate, and a control run against it does not support
it. Recorded here rather than quietly dropped.

**P6 holds.**

## What survives, and it is not what was argued a run ago

The length-variance argument is largely gone. What the six runs support instead:

**The script is 203 words against 503.** A 60% reduction in what a person reads, with the spread
across two very different scopes at 1.2% and within one arm at 0 and 5 words. Whatever else is true,
this is the acceptance criterion met and measured rather than asserted.

**Variance survives in behaviour rather than in length, and the control arm produced the clearest
instance yet.** `bprime2` opens question B with *"From the folder names my guess is a ceramics
practice — tell me what's wrong with that rather than composing from scratch."* The ArtGlina
interview, on the same framework version, said the opposite: *"I am asking this blank rather than
drafting it — a plausible guess about your business would read as fact."* Both are defensible
readings of one instruction, `procedure.md`'s *"Where you can draft an answer, show the draft and ask
what is wrong with it."* One drafts, one refuses to. **That is the variance the proposal was really
about, and it is about what gets asked rather than how long the asking is.**

`bprime2` also invented a seventh topic — *"A. Which state is this project in?"* with three options —
out of `new-project.md`'s note *"Check which state the project is in"*, which is addressed to the
assistant and asks it to determine the state, not to put it to the person. And it numbered its
questions `A`–`F` where every other run used digits.

**The forbidden-question count, stated honestly at this sample size.** Across six unspecified runs:
`a1` asked whether `.docs/` exists while saying it does not, and `b2` asked for each component's
posture. Both `B′` runs are clean. So two violations in six unspecified runs, none in four script
runs. Small numbers, and reported as small numbers.

## A defect in the draft, found by running it

Question 5 ends *"Your local path is already settled and is in the table below."* **There is no table
below.** The summary table is Step 5 and comes after the answers. All four script runs reproduced the
sentence verbatim, which is the experiment working exactly as intended and is also the accepted cost
stated plainly: **a shipped script ships its defects with perfect fidelity.** An unspecified interview
would have silently repaired that sentence; four runs of a specified one repeated it four times.

The repair is one clause and it is not made here, because this file is the record of what was run.

## What was measured is fidelity, not sufficiency

**Every run had writing disabled and stopped at the questions. Nobody answered them and no document
was produced.** So the six questions are proven to arrive verbatim, and they are **not** proven to be
enough to write a complete `PROJECT.md` from.

That distinction has to be stated here in those words, because "the script survives" will otherwise
be read as "the script works". Six questions arriving unaltered is a property of the mechanism. Six
questions being the right six is a different claim and this experiment does not touch it.

The sufficiency test exists and is scheduled. It is the ArtGlina adoption, which is also the only
instrument that un-provisions `0.10.0`, `0.10.1` and `0.10.2`. **Sequence: fix, release, adopt.**

## Verdict

The proposal survives. It does so on P1 and P4 and on a 60% reduction measured across two scopes —
**not** on the folder-variance argument, which its own control has weakened.
