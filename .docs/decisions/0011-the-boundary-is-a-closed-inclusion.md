# 0011. The boundary is a closed inclusion

**Date:** 2026-08-29  
**Status:** accepted

---

## Context

`PROJECT.md` has carried the boundary as an exclusions list since the beginning: *this project does
not currently cover X, Y and Z.* It is the only rule in this framework with a measured before and
after. Without it, a request the project excludes arrives looking like ordinary work and gets done.

The complaint came from the person who has to answer it, during the ArtGlina interview. Listing what
a project does not cover could take all day and he can get lost doing it. Naming what it covers took
him one sentence: the main folder and two repositories.

The fix is not swapping one open list for another. An open inclusion list is no better than an open
exclusion list, and it is worse in one way, because it reads as complete while being partial.

**The fix is closing the set.** The project covers these things, and anything else is outside it. One
sentence, bounded, quotable, and answerable by the person who has to answer it.

This is the same move the framework has already made twice. `0007` replaced silence about a missing
address with a plain statement that none exists and why. `structure-check` 11 passes a registry with
no blocks when the document says in visible text that none are declared. Both times an unbounded or
absent answer was replaced by one explicit statement, and in both the statement is what made the
thing checkable.

## Decision

**The boundary is written as a closed inclusion.**

```text
This project covers restoration, photography and selling online. Anything else is outside it.
```

**Corrected 2026-08-30.** This example originally read *"the main folder and the artglina.com.ua
repository"* — a list of places. So did the blueprint's placeholder table, which `0.10.0` changed from
`hosting and deployment, mobile applications, accounting` to `the main folder and the
northwind-storefront repository` in the same release, without recording that the example had changed
category. Every adoption afterwards answered the boundary with a folder list, which duplicates the
registry and answers nothing, and it went four releases before anyone noticed — as a feeling that two
questions overlapped. The rule here was always right; the example beside it taught the opposite. See
the third shape in [`../backlog.md`](../backlog.md).

The closure sentence is not decoration and is not optional. *Anything else is outside it* is what
turns a list into a boundary; without it the reader has an inventory and no rule.

**The argument that decides it is the direction of failure, and it belongs in the record.** The two
forms fail in opposite directions. An exclusions list that misses something leaves that thing in
scope by default, so an assistant does the work and nobody finds out until it is done. A closed
inclusion that misses something leaves it out of scope, so an assistant asks. Failing towards asking
is the direction this framework already chose, in the stub's *"if you cannot reach it, say so and
stop. Do not proceed on guesses."*

**Near misses stay available and stop being required.** Where an owner already knows the adjacent
thing people assume is inside and is not, writing it costs a clause and helps a reader. Where he does
not, the closure sentence carries the weight alone. This is the half of the old question that was
working: WordPress 7's thin first answer was repaired by naming what falls inside, and the exclusions
it eventually wrote were all near misses rather than an attempt at the complement.

**A project already adopted under the old wording stays valid.** WordPress 7 leads with exclusions
and has no closure sentence, and it is not rewritten to remain correct. Both forms answer the same
question and the framework accepts either. What a new adoption writes changes; what an old one holds
does not. A migration would cost every adopted project a rewrite to gain nothing an assistant can
act on, which is the trade `0003` refused when it removed the version sweep.

## Consequences

**The cold start check has to change, and not only in wording.** It reads this line in three places:
the component prompt's question 4, its reading table, and the project scope prompt's question 2.
Question 4 currently asks the reader to *name something this project does not cover*, and its value
is that the answer can only come from having read a specific line.

Under a closed inclusion that stops being true. "Cooking" is a correct answer to "name something this
project does not cover" for almost any project, derivable with no reading at all, and the check would
pass an assistant that never opened `PROJECT.md`. **So the question inverts with the answer:** it has
to ask what the project covers and where that is written, and then for something adjacent that falls
outside. The first half restores the quotable requirement, the second keeps the behaviour the
original question was testing.

This is the substantive part of the change. A boundary that is easier to write is worth little if the
check that made it load-bearing stops being able to tell whether it was read.

**The accepted cost, stated plainly.** A closed inclusion can be wrong by omission, and its failure
mode is an assistant stopping to ask about work that was always inside the project. That is an
interruption, and interruptions have a cost the exclusions form did not impose. It is accepted
because the alternative failure is silent and this one is not, and because a boundary that is wrong
by omission gets corrected the first time it fires, whereas an exclusions list that is wrong by
omission is never corrected at all.

**What this does not change.** The undecided case keeps its provision: a project that has not settled
its boundary writes that it has not, what will settle it, and what to do meanwhile. Leaving the topic
out remains worse than leaving it open, for the reason already measured — an assistant asked what
falls outside will answer from the nearest sentence that looks like a boundary, and any sentence
about a component not being attached will do.

## Origin

**Decided by the owner, 2026-08-29**, from the ArtGlina interview, where the question was put to him
and he said what was wrong with it. The convention in [`../handover.md`](../handover.md) applies: the
decision is his, the reasoning reached this session through him, and it cannot say how much of the
phrasing is his own.

The failure-direction argument arrived with the decision and is recorded as arriving. This session
added the consequence for the cold start check, and the observation that WordPress 7's eventual
exclusions were all near misses rather than an attempt at the complement.
