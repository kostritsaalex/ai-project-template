# Pre-registration: the interview after the owner answered it

**Written 2026-08-30, before any arm is run. Committed before the first run.**
**Nothing is released before the owner reads it. `blueprints/` is not touched by any arm here.**

---

## What changed and what is at risk in each

| | Change | The risk it introduces |
| --- | --- | --- |
| **Q1** | Becomes the owner's wording; the software clause is cut | The document may stop saying whether software is all of the project or part of it — a fact `0004` lists and the cold start check tests |
| **Q2** | The undecided option is surfaced; examples shortened and un-paired | An easy escape hatch may be taken where an answer exists |
| **Q4** | Says naming is not attaching; "declare" removed; "repositories" added | Longer question; and it may now invite folders that are not components |

**Q1 carries the only structural risk.** The other two changes add an option and a reassurance. This
one **removes an instruction and relies on derivation**, which is the razor working as intended and is
also the way to lose a fact nobody notices is missing.

## The acceptance test is the owner's and is not run here

**He answers all four from his head, in one message, without hesitating or asking what a question
means.** No scratch run can measure that. What these arms measure is that the questions arrive
intact, that four is still four, and that **the software fact survives the cut** — which is the one
thing that can be checked without him.

## The arms

Two scratch scopes, rebuilt from the recipes already used, so the comparison is against the same
folders `0.12.0` was measured on:

- **S-mixed** — three folders, code and material, in a simulated synced store.
- **S-material** — five folders, material only, no code anywhere.

| Arm | Framework | Scopes | Runs |
| --- | --- | --- | --- |
| **V** | `HEAD` at `0.12.0` | both | 1 each, as the before |
| **W** | `HEAD` + `interview-v3.md` | both | 2 each |
| **W-ans** | Same as W, answers supplied so it reaches the Step 5 table | both | 1 each |

Ten runs. `claude -p`, `--model opus`, fresh session each. Writing disabled for all of them — nothing
here measures work, only what is asked and what is proposed.

**The supplied answers for W-ans deliberately describe a business without saying whether it is
software.** *"A pottery studio. We make and sell ceramics, run a shop site and take commissions."*
That is the case Q1 must now carry on its own.

## Predictions

**P1. Fidelity.** Zero added prose in all six arm-W runs, `difflib` similarity 1.000 against the
script. Over 10% in any run fails.

**P2. Four questions.** Exactly four in every arm-W run, on both scopes.

**P3, the one that matters. The software fact survives the cut.** In both W-ans runs, the value
proposed for `<PROJECT_PURPOSE>` **states whether software is all of the project or one part of it**,
derived from a business description that never used the word. **If either run writes a purpose that
leaves it open, Q1's cut has lost a fact and the clause goes back** — into the assistant note more
loudly, or into the question.

**P4. The undecided option is not over-offered.** No arm-W run presents "not decided" as the expected
answer, restructures the question around it, or asks it as a separate question. It is one clause of
four.

**P5. Q4 does not invite non-components.** No arm-W run lists candidate folders it found in the
scope, or asks whether a subfolder should be split out. `procedure.md` forbids both and the wording
change touches that question.

**P6. Nothing written into either scope.** Checksums unchanged.

## What this cannot establish

**Whether the swap is fixed.** His answers to Q2 and Q4 landed in each other's places, and the fix is
a sentence telling him that naming costs nothing today. **Only he can show whether it worked**, and
the acceptance test is his. These runs cannot answer it and are not offered as answering it.

**Whether the shortened examples stop being copied.** That observation came from one person on one
reading, the change was made on it alone, and it is recorded in the backlog as unmeasured. **A
scratch run cannot copy an example the way a person did**, because nothing in these runs answers the
questions.

## If P3 fails

Q1 does not revert to the old wording — his is better and the reason it is better stands. The fact
moves rather than the question: the assistant note gets the instruction in stronger terms and the
arms re-run. **Only if that also fails does the clause go back into the question**, and then the
record says the razor was wrong here and why.
