# 0015. The boundary becomes agent boundaries

**Date:** 2026-08-30  
**Status:** accepted. Supersedes part of [0011](0011-the-boundary-is-a-closed-inclusion.md).

---

## Context

Three attempts at the closed-inclusion form, with one owner, produced: a list of folders; both of the
question's own examples verbatim; and finally *"there is no clear boundary now."*

His true answer is **"everything is allowed as per request."** A closed inclusion forces him to invent
a closure he does not believe, and **a document with an invented boundary is worse than one with an
honest absence** — the invention is quotable, and an assistant will quote it.

Asked instead *"is there anything an agent should never do in this project?"* he answered
immediately, and the answer was a real constraint rather than a shape.

## The finding that decides it, and it was not known when `0011` was written

**The one measurement justifying a boundary at all was taken on a prohibition, not on a closed
inclusion.**

`cold-start-check.md` cites it: an assistant asked to set up a staging deployment did the work without
opening `PROJECT.md`, *"where hosting sat under what the project does not cover"* — an exclusions
list. `WordPress 7` still carries that line, and the refusal that followed quoted it.

**`0011` inverted the form and inherited the evidence without re-taking it**, and ran on it for three
releases. So the owner's reversal is not a preference traded against measured behaviour. **It returns
the line to the shape its evidence was gathered on**, and it is `0011` that was running on borrowed
evidence.

Found while listing every place that mentions the boundary, which is a pass this framework started
doing because `0.10.0` changed the form in four places and missed three.

## Decision

**`PROJECT.md` carries agent boundaries: anything an agent should never do in this project, each
written as a prohibition in the owner's words.**

```text
Agent boundaries: never set up deployment, never spend money on my behalf, never publish anything
publicly.
```

**The interview asks it in his words:** *"Is there anything an agent should never do in this project?"*
with three examples from deliberately different categories — deployment, money, publishing — so that a
reader sees the kind rather than a line to copy.

**Where nothing is forbidden, the section says so in visible text and is never deleted.** That no work
is currently forbidden, and that an assistant meeting something which looks outside the project asks
before starting it. **This is the branch most likely to be got wrong** and it is what
[`0010`](0010-the-path-note-stays-optional.md) is about: silence reads as correct to every check, and
a deleted section tells the next assistant nothing.

## The cost, stated rather than traded away

**A prohibition list fails open.** Work nobody thought to forbid is permitted, so an assistant does it
and nobody finds out. A closed inclusion failed the other way: an unlisted activity was outside, so an
assistant asked. **Failing towards asking is the direction this framework chose**, in the stub's *"if
you cannot reach it, say so and stop"*, and this reverses that on one line.

**What answers it, partly.** The required absence sentence carries the instruction to ask, so an empty
list is an instruction rather than a licence, and the check now scores exactly that. A populated list
does not carry it, and that is the residue: a project with three prohibitions and a fourth nobody
thought of behaves as `0011` warned.

**Accepted, and not because the cost is small.** It is accepted because the alternative was an invented
closure — and an invented boundary fails in both directions at once, permitting what it forgot to list
and forbidding what its author never meant.

**What the check loses.** Under a closed inclusion the cold-start question could ask a reader to derive
something outside the covered set, a second and harder test of whether the boundary was understood. **A
prohibition list supports no such derivation.** That half of the row is gone and the row now tests
reading rather than reasoning. Declared in the check itself.

## Consequences

**Twelve sites, listed before any was edited**, because `0.10.0` changed this line in four places and
missed three, and the repair for that missed a fourth. Six were known; six were found by the list,
including the project-scope prompt's question 2, which is the same question as the component prompt's
question 4 and had never been named.

**One of them had been wrong for three releases.** `cold-start-check.md`'s project-scope reading row
still read *"one item from each list"*, the two-list wording from before `0011`. It was found on
2026-08-29, deferred knowingly because checks were out of scope, and repaired here rather than shipped
wrong a third time. **The deferral was right and repeating it would not have been**: the file is being
rewritten regardless, so this is the same edit surface rather than a passenger.

**`<SCOPE_COVERS>` becomes `<AGENT_BOUNDARIES>`.** The placeholder's name no longer described what goes
there, which is a smaller version of the defect that made the example teach the opposite of its rule.

**The interview's question block falls to 146 words** from 175 at `0.12.0`, against 235 in the draft
this replaces. His two questions are shorter than the ones they replace, which is the first time in
this sequence that a change to the interview has cut rather than added.

## Origin

**Decided by the owner, 2026-08-30**, after answering the closed-inclusion form three times and
failing to produce a boundary he believed. Both questions are his wording. The examples are his.

The framework is reviewed by a second assistant whose prompts reach the working session through him,
so a message here may be his words, the review's relayed, or both. What is certain is the decision and
the wording.

What arrived with the review and is recorded as arriving: that the fail-open cost belongs in the record
rather than a commit message; that the empty case must be visible text and not a deleted section; and
that the twelve sites be listed before any was edited.

What this session added: the six unlisted sites, and **the finding that `0011` inherited its
evidence** — which the review then made this record's strongest line, and which changes the decision
from a trade against measurement into a return to the form the measurement was taken on.
