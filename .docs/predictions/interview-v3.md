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

**Eight runs** — two arm V, four arm W, two W-ans. `claude -p`, `--model opus`, fresh session each.
Writing disabled for all of them; nothing here measures work, only what is asked and what is
proposed.

*Corrected after the runs: this line first said "ten", which the table above never supported. The
count in the table is what was run. A stated total that disagrees with its own table is the defect
this repository keeps cataloguing, so it is fixed and noted rather than quietly re-typed.*

**The supplied answers for W-ans deliberately describe a business without saying whether it is
software.** *"A pottery studio. We make and sell ceramics, run a shop site and take commissions."*
That is the case Q1 must now carry on its own.

## Predictions

**P1. Fidelity.** Zero added prose in the four arm-W question runs, `difflib` similarity 1.000
against the script. The two W-ans runs skip to Step 5 and reproduce no question block, so they are
not scored on this. Over 10% in any run fails.

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

---

# Results, scored 2026-08-30

Eight runs, logs `2026-08-30-v3-*.log`.

**P1 holds.** Zero added prose in all four arm-W question runs, similarity 1.000.

**P2 holds.** Four questions in every run, both arms, both scopes.

**P3 holds, and it holds by derivation rather than by luck.** Both `W-ans` runs were given *"A pottery
studio. We make and sell ceramics, run a shop site and take commissions"* — a description that never
uses the word software — and both wrote the fact into `<PROJECT_PURPOSE>` anyway:

> *"…runs a shop site and takes commissions. **Software is one part of it, not all of it.**"*
> — source given as *"The shop site makes software a part rather than the whole"* (`aM1`) and
> *"software-is-a-part derived from 'shop site'"* (`aT1`).

**Both named the derivation unprompted**, which is what separates this from a lucky guess. **The
clause was cut and the fact survived**, which is `0004` working on a question rather than on a
document: it was derivable, so asking for it was unnecessary, and asking for it was what made him
enumerate.

**P4 holds.** Exactly one occurrence of the undecided clause per run — the question's own. No run
restructured around it, promoted it, or asked it separately.

**P5 holds.** Zero hits across all four runs for candidate-offering or split-the-folder language.

**P6 holds.** Both scope checksums unchanged.

## An incidental finding, not caused by this change

`wM2` listed the scope's file contents in its Step 2 report — *"The folder holds only
`supplier-notes/kilns.md`, `storefront/package.json`…"* — to justify its "no AI instruction files"
answer. **`procedure.md` Step 2 forbids it**: *"Do not survey the contents to describe them; nothing
in these documents describes contents."*

**P5 is not violated**: it listed contents, not candidates, and asked nothing about them. But an
adjacent rule was breached by one run of four, on a question this change does not touch, so it is
recorded rather than folded in. One instance, no rate.

`wM2` also flagged that it could verify the simulated store's symlink only through the sandbox root
and had not resolved the literal `~/` spelling, and said it would bring that to the summary rather
than paper over it. That is the simulated-store confound from an earlier experiment appearing again,
and the run handled it correctly.

## What is still unmeasured, and it is the part that matters

**Whether the swap is fixed.** Registered as unmeasurable here before the run and it stayed that way.
His answers to Q2 and Q4 landed in each other's places; the fix is one sentence telling him that
naming costs nothing today. **Only his acceptance test shows whether it worked**, and it is his: he
answers all four from his head, in one message, without hesitating or asking what a question means.

**Whether the shortened examples stop being copied.** Nothing in a scratch run answers the questions,
so nothing here can copy an example the way he did. The change rests on one observation and is
recorded as unmeasured.

**Nothing is released.** `blueprints/` is untouched by every arm here, and the draft waits on him.

---

# Registered before he answers: are question 2's examples needed at all?

**Written 2026-08-30, before the owner's acceptance test, so the reading is not chosen afterwards.**

**The shortening treats the symptom.** The examples were cut from two full sentences joined by *or* to
three short fragments after he answered question 2 with both of the old ones verbatim. **A short
example is copied as readily as a long one.** What that observation showed is not that the examples
were too long — it is that **an example in that question gets answered instead of the question.**

So the question is whether they are needed at all. `0004` says a document carries what cannot be seen;
by the per-question audit's extension, **a question carries what the person cannot supply without
it.** An example that has now taught the wrong thing twice — once to an assistant, across four
releases of folder-list boundaries, and once to the person answering — is a candidate for cutting
rather than trimming.

**His acceptance test settles it at no cost.** He has been asked to notice whether he could have
answered question 2 with no example present.

- **If he could: the examples are cut.** They fail the razor, he supplied the answer without them, and
  they have a measured history of being copied instead of read.
- **If he could not: they stay**, and the record says why, which is more than they have now. Today
  they are in the question because an earlier draft put them there.

**Registered as a razor case and not as a wording preference**, so neither outcome can be read as the
other afterwards. The shortened form is what he is testing; the question is whether any form survives.

## The Step 2 breach stays a note

One run of four listed the scope's file contents, which `procedure.md` Step 2 forbids. One instance,
an adjacent rule, and this change does not touch it. **It is not repaired inside this work** — it
belongs to whatever pass looks at Step 2, and fixing it here would put an unrun change into a release
the owner is about to read.

## Amendment before the test: question 2 gains a purpose clause

**The reframe was tried in conversation and rejected by the answer it produced** — see the backlog.
What replaced it is one clause saying what the line is for: *this is the sentence an assistant quotes
when it declines work that is not part of this project.*

**Paid for by trimming two clauses in the same question**, so the question is no longer than the
version he first read.

**No scratch run measures this.** A purpose clause changes whether a person knows what he is being
asked for, and nothing in these arms answers the questions. **His acceptance test is the only
instrument**: whether he answers question 2 from his head, in one message, without hesitating.

**One risk to the examples question, registered now.** He is being asked explicitly whether he could
have answered question 2 with no example present, and he is being asked **before** he answers.
Knowing the question is being asked may make him read past the examples deliberately, which would
bias the answer toward cutting them. Asking afterwards avoids that bias and loses the answer, since
he cannot un-read them. **The bias is accepted and named**, and if he reports that he could have
answered without them, the record notes that he knew the question was coming.
