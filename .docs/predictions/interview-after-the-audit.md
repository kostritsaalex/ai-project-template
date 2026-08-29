# Pre-registration: the interview after the per-question razor audit

**Written 2026-08-29, before any arm is run. Committed before the first run.**
**`blueprints/` is held until the owner says the ArtGlina adoption has finished. Every arm here runs
against a scratch copy of the framework and touches nothing in the repository.**

---

## The claim under test

`0013` applied `0004` to the interview's *existence* — topics against text — and took its questions
from what unspecified runs happened to ask. **No question was audited against the razor one at a
time.** The audit was done on 2026-08-29 and moved two questions to proposals and cut a third.

The subject is [`../drafts/interview-v2.md`](../drafts/interview-v2.md): **four questions**, against
`0.11.0`'s seven.

Two things are being tested and they are not the same claim:

1. **Fidelity survives the change.** A shorter script with a longer assistant note is still pasted
   verbatim. `0.11.0` established this at zero added prose over six runs, and a change to the subject
   does not inherit that result.
2. **The proposals work.** This is the new risk. `0.11.0` asked for the name and the address; the
   revision derives both, and **a wrongly proposed address is worse than an asked one** —
   `new-project.md` says it is the value most worth getting right, because every component copies it
   and a wrong one leaves each of them knowing a parent exists and unable to reach it.

## The scopes

Three, all scratch, all deleted afterwards, none of them ArtGlina. **ArtGlina is spent on the
sufficiency test for `0.11.0` and cannot be spent twice.**

| | Shape | Address situation | Expected derivation |
| --- | --- | --- | --- |
| **S-A** | Three folders, mixed code and material | Resolves inside a synced store | `OneDrive, <path within the store>` |
| **S-B** | One folder, a git working copy | **Git remote only**, SSH form | Normalised to a URL with its scheme, **or asked** |
| **S-C** | Five folders, material only, no code | **Neither** — no store, no git, no copy anywhere | `0007`'s `none` form with the reason |

**S-A's synced store is simulated and that is a declared deviation.** A symlink inside the scratch
directory stands in for `~/OneDrive`, because writing test folders into the owner's real synced store
would push them to his cloud. The rule under test is "the local path resolves inside a synced store",
and the simulation satisfies it; whether a real OneDrive behaves identically is already evidenced
twice, by WordPress 7's hand-written address and by ArtGlina's path.

Checksums are path-relative — `( cd "$SCOPE" && find . -type f | sort | xargs md5sum | md5sum )` —
after the recipe defect found on 2026-08-29, when hashing absolute paths made a rebuilt-identical
scope fail its own verification.

## The arms

| Arm | Framework | Scopes | Runs |
| --- | --- | --- | --- |
| **E** | `HEAD` at `0.11.0`, seven questions | S-A, S-C | 2 each |
| **F** | `HEAD` + `interview-v2.md` installed, four questions | S-A, S-C | 2 each |
| **F-addr** | Same as F | S-B | 2 |

Ten runs. `claude -p`, `--model opus`, fresh session each, `Write`/`Edit`/`NotebookEdit` disabled,
identical across arms. Arm E is the before, on the same two scopes, so the question count and the
word count have a same-day comparison rather than one carried from a different scope.

Arm F is built as a scratch copy of `HEAD`: `interview-v2.md` installed at
`blueprints/setup/interview.md`, `procedure.md` Step 4 pointing at it and saying four rather than
seven. The installed file and the exact Step 4 diff are committed with the results, because a run
against a tree nobody can reconstruct is not evidence.

## The measures

Total words, preamble words, question-block words, question count, and:

**Added prose** — words in a run's question block not in the script, by
`difflib.SequenceMatcher` over whitespace-normalised, case-folded word lists, counting the run side
of every `insert` and `replace` opcode. Zero means the script arrived verbatim.

**The proposed address**, quoted from each run, with the source the run names for it.

**The proposed name**, quoted, with its source.

## Predictions

**P1. Fidelity holds.** Added prose under 10% of the script in all six script runs (arms F and
F-addr). Over 25% in any run is a failure of the same kind `0.11.0` was built to prevent.

**P2. Four questions, not five.** Every arm F run puts exactly four questions to the person. **A
fifth is a failure**, and the likeliest fifth is the address returning as a question on S-A or S-C
where the rules should have settled it.

**P3, the address, and this is the one that matters.**

- **S-A:** the address is proposed as `OneDrive, <path within the store>`, in the summary table, not
  asked.
- **S-B:** either a URL with its scheme, **or** the question asked. Both pass. **Writing the SSH
  remote verbatim fails**, because it satisfies none of `0007`'s four forms and `structure-check` 11
  would reject it.
- **S-C:** `0007`'s `none` form with a reason. **A blank fails. A local path in the address slot
  fails** — that is the exact defect `structure-check` 11 was written for and validated against.

**P4. The name is proposed, not asked**, in every arm F run, and offered for correction rather than
stated as settled.

**P5. The boundary question stops eliciting places.** Not measurable here — no one answers these
runs — so what is checked instead is that the shipped example names kinds of work and that no run
alters it. **This is registered as untested rather than passed.** Its real test is an adoption.

**P6. Nothing is written into any scope.** All three checksums unchanged.

## The address falsifier, registered as the review framed it

**A proposed address that satisfies none of `0007`'s four forms, or that differs from what the owner
would have written.**

**It has already fired once, on this repository, before shipping.** The derivation gives
`git@github.com:kostritsaalex/ai-project-template.git`; `PROJECT.md` carries
`https://github.com/kostritsaalex/ai-project-template`. That is why the git branch normalises and
asks on failure instead of proposing the remote as found — a correction the audit made to the
review's own proposal.

## The risk of running now, registered rather than avoided

**The ArtGlina adoption is in flight against `0.11.0` and may change the question set.** If it shows
four questions insufficient — a placeholder left unfilled, or an answer the owner cannot give — these
results describe a draft that no longer exists, and **the arms are re-run rather than reinterpreted.**
That is a cheap outcome and it is the honest way to spend idle time; the alternative buys only the
certainty that the results describe a subject that still exists.

**A defect in the subject, found and fixed before the first arm ran.** Question 2's example read
`restoration, photography and the online shop` — two kinds of work and a place, **in the example
written to teach that the boundary names kinds of work and the registry names places.** Shape three,
in the sentence naming shape three. Corrected to `restoration, photography and selling online`, every
item now something a person does. Recorded because the last example defect took four releases to
notice and this one would have reached every adoption.

## Amendment, after the first ten runs and before the address arms

**P3 and P4 were not measurable as written, and that is a defect in this file rather than a result.**
The ten runs stop at Step 4, because that is what the procedure tells them to do. **The address and
the name are proposed in the Step 5 summary table, which none of them reached.** So the two
predictions that this experiment exists for observed nothing at all.

The technique that works already exists and was used for the placeholder map: supply the answers in
the prompt so the session proceeds to Step 5. Six further arm-F runs, two per scope, with **no name
and no address anywhere in the answers**, so anything proposed came from the folder.

P1, P2 and P6 stand on the ten runs already made and are not re-run.

**A confound in S-A, found by a run.** The simulated store sits at `<scratch>/OneDrive`, and a real
`~/OneDrive` exists on this machine pointing somewhere else entirely. `fA1` caught it and refused:
*"`~/OneDrive` on this machine resolves to `/mnt/c/Users/kostr/OneDrive`, which is a **different**
folder — so `~/OneDrive/Projects/Test/northwind-crafts` is false here and I will not write it."*
**`fA2` did the opposite** and proposed writing exactly that path, which is false on this machine.

That is the local-path failure the address rule exists to prevent, observed, and it is produced by
the simulation rather than by the framework. **So S-A's address result is confounded and is reported
as confounded.** The synced-store branch keeps the two real-scope validations it already has —
WordPress 7's hand-written address reproduced exactly, and ArtGlina's computed correctly — which are
stronger evidence than a simulation could be. S-B and S-C carry no such confound.

## What this cannot establish

**Whether the name proposal earns its place.** Nothing in a scratch run can observe an owner
correcting a proposed name. Its justification is the razor, not a run; it is the only change in this
batch of which that is true; and it is recorded in the backlog so that the measured changes do not
lend it their credibility. Its falsifier needs an adoption.

**Whether four questions are sufficient.** Every run stops at the questions, nobody answers them, and
no `PROJECT.md` is produced. **Fidelity, not sufficiency** — the same limit `0.11.0` carries. The
placeholder map closes the part of it that needs no adoption, and it is re-run against the revised
interview before any release.

## If a prediction fails

**P3 failing on any scope** stops the address becoming a proposal. It returns to a question, the
audit's verdict on question 5 is recorded as refuted by measurement, and the interview is five
questions rather than four.

**P1 or P2 failing** sends `interview-v2.md` back to the draft folder rather than being repaired in
place, on the same terms `does-a-shipped-script-stay-shipped.md` set.

---

# Results, scored 2026-08-29

Sixteen runs, logs `2026-08-29-audit-{e,f,g}*.log`. Ten as originally designed, six after the
amendment.

## P1, P2, P6 — from the first ten

| Arm | Scope | question block | questions | added prose |
| --- | --- | --- | --- | --- |
| E (`0.11.0`) | A, C | 217 words, all four runs | **7** | — |
| F (revised) | A, C, B | 175 words, all six runs | **4** | **0, 0.0%** |

**P1 holds.** Zero added prose in all six script runs, `difflib` similarity 1.000. Fidelity survives
the change: a shorter script with a longer assistant note is still pasted verbatim. That is ten runs
of the mechanism at zero, across three subjects.

**P2 holds.** Exactly four questions in every arm F run, on three different scopes. No fifth
appeared.

**P6 holds.** All three checksums unchanged after all sixteen runs.

## P3, the address — the prediction this experiment existed for

| Scope | Proposed | Source the run named |
| --- | --- | --- |
| **S-B** `gB1` | `https://github.com/example-org/harbourline` | remote `git@github.com:…`, "normalised to a URL with its scheme per `0007`" |
| **S-B** `gB2` | `https://github.com/example-org/harbourline` | `git remote -v`, "normalised … per decision 0007" |
| **S-C** `gC1` | `none. No copy of this folder exists off this machine.` | "`0007`, fourth form: not in a synced store and not a git working copy with a remote" |
| **S-C** `gC2` | `none` with the reason | "no `.git`, no synced-store path" |
| **S-A** `gA1` | `OneDrive, Projects/Test/northwind-crafts` | "resolves inside a store named OneDrive; no git remote" |
| **S-A** `gA2` | `OneDrive, Projects/Test/northwind-crafts` | "`interview.md` rule 1" |

**P3 passes on every branch, twice each, and on the branch that had failed.** The git remote was
normalised rather than written as found, by both runs, both citing `0007` unprompted — which is the
correction the audit made to the review's proposal, working. **S-C produced `0007`'s fourth form with
its reason, never a blank and never a local path in the address slot** — the exact defect
`structure-check` 11 exists for.

**The address falsifier did not fire.** No proposed address failed `0007`'s four forms.

## P4, the name — holds, and it proposed correction unprompted

`Northwind Crafts`, `Harbourline`, `Rowan Studio` — all six runs proposed from the folder name with
spaces or casing restored, and named the folder as the source. Three of six volunteered the
correction invitation without being told to: *"correct it if the name differs"*, *"A draft — correct
it if the workshop's name differs"*, *"correct it if the name carries spaces or different casing."*

**This remains the change justified by the razor and not by a run.** These runs show the proposal is
*made* and *offered for correction*. Nothing here shows it is *right*, because no owner corrected
anything. That needs an adoption.

## The S-A confound, and my amendment overstated it

The amendment said `fA2` "proposed writing exactly that path", the false `~/OneDrive/…` form. That is
accurate about Step 2 and wrong about the outcome. **At Step 5, where the value is actually written,
`gA2` marked the local path `unknown` and refused:** *"the `~/OneDrive/…` form is the one that
belongs in the document and is the one I could not check… I will not write an unresolved path."*
`gA1` wrote the absolute path it had resolved and said so.

**So the confound displaced onto the local path and neither run wrote a false one.** The address
branch fired correctly on S-A as well. Correcting my own amendment: the intent appeared at Step 2 and
the same mechanism caught it at Step 5, which is Step 6's "do not write a path you have not resolved"
doing its job.

## An incidental finding, and it is a real defect

**The posture proposal returned opposite verdicts on identical input.** S-B, same folder, same
answers: `gB1` proposed `Repository. Things get changed here…`, `gB2` proposed `Assets. Live
material…`. The folder holds `src/main.py`, the project's own code, with nothing a platform or
framework updates wholesale — so **`Assets` is right by the blueprint's own rule and `gB1` is
wrong.**

This is not what was under test. The posture proposal has been in the framework since `0.6.0` and is
the one thing a component is ever told about itself. It is the same shape as an under-specified check
row: a proposal that looks settled and is judgement, differing between runs, with nothing in the
output distinguishing the two. **Recorded in the backlog as its own item rather than fixed here**,
because fixing something found mid-experiment is the error this repository spent two days
cataloguing.

## Verdict

The revised interview is carried on P1, P2, P3 and P6. **P4 is carried only as far as a scratch run
can carry it**, and P5 was registered as untested and remains so — no one answered these questions,
so whether the boundary stops eliciting places is still an adoption's job.
