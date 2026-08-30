# 0016. Declared, not attached is a second non-attached outcome

**Date:** 2026-08-30
**Status:** accepted. Extends [0009](0009-a-check-declares-its-read-set-in-advance.md)'s check by one
condition; does not supersede anything.

---

## Context

ArtGlina was adopted on `0.13.0` on 2026-08-30. Two components in the registry, `Artglina UA` and
`Artglina Sandbox`, both folders present, neither carrying stubs. `structure-check` passed it 14 of
14. `registry-check`, run on the same scope on the same day, returned **7 failed rows**: rows 2, 3
and 4 for both components, and row 7 for an unrelated reason recorded in the backlog.

The scope was correct. The interview shipped at `0.13.0` says plainly that naming a component does
not attach it, and ArtGlina's own registry says so in visible text: *"Neither component is wired to
this scope yet. Neither folder carries its stubs."* The failures were pre-registered before the run
and the run matched them, so the check was behaving exactly as written.

## The condition the check had, and the one it meant

`registry-check` had one cascade, at row 1:

```text
Unless this row confirmed the folder exists, rows 2 to 6 for that component are n/a and name this
row as the reason.
```

**That clause is correct for what it covers, and this decision does not touch it.** A missing folder
makes every downstream row unevaluable, row 6 included, because a folder that does not exist
satisfies an absence check for no useful reason. That is the defect `0.9.1` collapsed three cases
into one condition to repair, and the repair was validated over rows 2 to 6 by two runs.

**What was wrong is that it was the only non-attached state the check knew.** The clause recognises
one symptom of not being attached — the folder is not there — and treats it as the condition. A
component whose folder is present and whose stubs are absent is equally not attached, and the check
had no state for it, so five rows with nothing to read produced a verdict each.

**That state did not exist in the corpus the check was built against.** `registry-check` was written
on 2026-08-29 against `WordPress 7`, the framework's own subject, where every declared component was
already attached. Every run that validated it — nine of them, five pre-registered — was on that
scope or on a plant made in it. A scope with a declared, unattached component was never among them,
and a condition can only be attached to a symptom when the cases that separate the two are absent
from the evidence.

**`0.13.0` made it the normal first state.** The interview asks which folders and repositories belong
to the project before anything is written into them, so the registry is populated first and the
stubs follow. Every project adopted from here starts in the state the check called broken. ArtGlina
was the first adoption after that release and it found it immediately.

## Decision

**A component whose folder exists and whose two stubs are both absent is declared, not attached, and
that is not a failure.**

The clause goes on **row 2**, not row 1. Row 2 is the row whose subject is the stubs and whose
evidence is already the root-level listing, so the outcome is determined where the fact that
establishes it is gathered. It cascades to rows 3 to 5, which are the rows that read a stub. Row 6
tests one path and reads no stub, so it still runs and still returns a verdict — the ArtGlina run
confirms it did, passing for both components.

**Exactly one stub present still fails.** A component half attached is a defect under any reading,
and the row now says which stub is missing.

**Two outcomes, two cascades, two reasons.** Each n/a names its own. A deleted folder that reported
"declared, not attached" would be reporting a broken registry as a normal early state, which would
be worse than the defect this repairs, so it is the thing the negative control was built to catch.

## What this gives up, named rather than discovered later

A component that was attached and then had both stubs deleted now reports n/a where it reported
fail. The registry carries no field saying which components are meant to be attached, so no row in a
check that compares two documents can tell that case from a component never attached. Row 2's
evidence still prints the listing showing no stubs, and the n/a states the outcome in words.

**The stronger variant was available and was not taken.** Row 1 already honours a condition of the
right shape — *"unless PROJECT.md says in visible text that this component is not attached yet"* —
and ArtGlina's registry carries exactly such a sentence. Requiring it here would recover the case
above. It is not taken because the blueprint only encourages that sentence and does not supply it,
so a correct new project whose owner did not write it would fail this check on its first run, and
because it is a second variable in a change that has one. It is recorded in the backlog as the next
thing to try if the case ever costs anything.

## The evidence

Pre-registered before the edit existed, in
[`predictions/registry-check-declared-not-attached.md`](../predictions/registry-check-declared-not-attached.md),
with three arms and a falsifier for each: ArtGlina unmodified, a deleted folder, and a real defect
under stubs that are present. All three ran against the shipped text.

## The general shape, which is the part worth keeping

**A cascade condition is only as good as the cases in the corpus that could separate it from its
symptoms.** This one was written correctly, validated nine times, and was still keyed on the wrong
fact, because every run happened on the one scope where the two facts coincide. Neither reading the
clause nor repeating the runs would have found it. Adopting the framework onto a project that was
not its own author did.
