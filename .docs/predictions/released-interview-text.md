# Pre-registration: one run of the text that actually ships

**Written 2026-08-30, before the run and before the release commit. Committed first.**

---

## Why this run exists at all

The proposal was validated against a draft. The release repairs one clause of that draft, so **the
text about to ship is not the text any run has used.** That is precisely the state `0.9.0` reached
and was called out for: its `n/a` rule went into the release commit itself, after the last run, so
every run that validated `registry-check` validated a prompt three lines different from the one that
shipped.

The owner's judgement, and the reasoning is recorded because it decides the size of this test:
**fidelity is a property of the mechanism, and it is measured at 1.000 across four runs and two
scopes. A one-clause edit changes what is asked, not whether it is kept.** So this does not need the
six-run design again. It needs one run of the released bytes, and the objection is gone.

## The repair being validated

Draft question 5 ended: *"Your local path is already settled and is in the table below."* **There is
no table below.** The summary table is Step 5 and comes after the answers. All four script runs
reproduced the false clause verbatim, which is a shipped script shipping its defect with perfect
fidelity.

Repaired to: *"Your local path is already settled and I will show it in the summary table."*

## What is run

One run, `claude -p`, `--model opus`, fresh session, `Write`/`Edit`/`NotebookEdit` disabled, against
**the working tree that the release commit will contain** — not a scratch copy of it. The run happens
before the commit so that the bytes it validates and the bytes that ship are the same bytes, and the
log goes into the release commit.

Scope 1, rebuilt from the recipe in
[`does-a-shipped-script-stay-shipped.md`](does-a-shipped-script-stay-shipped.md), path-relative
checksum `cfe0628965b1cb30db3af0bff174dee0`.

## Predictions

**R1.** Added prose is **zero**. Measured as before: `difflib.SequenceMatcher` over
whitespace-normalised, case-folded word lists, released `interview.md` question block against the
run's question block. Any non-zero result means the repair changed the mechanism's behaviour, which
would be a surprise worth stopping the release for.

**R2.** The run reproduces the **repaired** clause and not the old one. `grep` for "table below"
returns nothing; `grep` for "summary table" returns the question-5 sentence. This is the only thing
this run genuinely tests that the previous four did not.

**R3.** Six questions, and no seventh.

**R4.** Nothing is written into the scope; checksum unchanged.

## What this run does not establish, stated in advance

**Fidelity, not sufficiency.** The run stops at the questions, nobody answers them, and no
`PROJECT.md` is produced. It shows the released text arrives intact. It does not show the six
questions are enough to write a complete document from. That is the ArtGlina adoption's job, and the
release entry says so rather than letting this run stand in for it.

## If R1 or R2 fails

The release does not get cut. The failure goes in this file and the interview returns to the draft
folder.
