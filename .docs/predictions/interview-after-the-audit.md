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
