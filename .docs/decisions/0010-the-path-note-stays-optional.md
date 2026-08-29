# 0010. The path note stays optional, and row 14's silence is a declared limit

**Date:** 2026-08-29  
**Status:** accepted

---

## Context

The audit of `structure-check` ranked row 14 second of fourteen, on the ground that its `n/a` cannot
tell a document that correctly carries no path note from one that needs one and lacks it. Silence
passes either way.

That is the shape [`0007`](0007-a-component-with-no-address-says-so.md) closed for addresses, and it
closed it by refusing silence: a component with no address says so plainly, with the reason, and the
check requires one of four forms rather than accepting nothing.

The same remedy is available here and is easy to state. A document giving a local path either says
what holds that path up, or says plainly that nothing does and the path resolves as written. Row 14
would then have something to require, and its `n/a` would shrink to the case where no local path is
given at all.

The question is not whether that would work. It would. The question is whether it is worth what it
costs, and `0007` having paid a similar price is not an argument, because the two cases are not the
same case.

## Decision

**No. The path note stays optional, and row 14's inability to distinguish correct silence from wrong
silence is recorded as a declared limit rather than closed.**

Four reasons, in the order of how much they weigh.

**The cases are disanalogous in the way that matters.** An address is load-bearing for every reader
from anywhere: without it a component knows a parent exists and cannot reach it, which is the failure
this framework exists to prevent. A path note is load-bearing only where a filesystem boundary
exists. The `README`'s own table puts "everything in one filesystem, nothing to do" as its first row
and expects it to be most projects. A required sentence would land on all of them to serve the few.

**The middle option is closed by experiment rather than by argument.** Requiring the sentence only
where the document also carries a session note is the obvious compromise, and it has been tried.
Until `0.6.0` row 14 was gated on the session note, and it therefore never ran: the first scope to
carry a symlink line had no components, no boundary and no session note, so the one line holding its
path up went unverified. Gating this row on a sibling line has failed once, silently, in exactly the
population it was meant to protect.

**It fails the second razor.** [`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md)
says a rule earns a place only if an assistant would do otherwise without it. An assistant meeting a
local path that does not resolve reports that it cannot reach it, with or without a sentence saying
nothing holds the path up. The sentence changes no assistant's behaviour. Its entire value accrues to
a check, and a rule written into every adopted document to serve a check is a rule paid for by every
reader to benefit one prompt.

**A sentence that is trivially true is a sentence that teaches skimming.**
[`0006`](0006-the-postures-carry-one-rule-between-them.md) removed four preserve rules partly because
a rule ordinary work breaks teaches an assistant the document can be ignored. The mirror of that is a
rule ordinary work makes vacuous. "Nothing holds this path up" in the majority of `PROJECT.md` files
is that rule.

## Consequences

**The accepted cost, stated plainly.** Row 14 cannot catch a document that needs a path note and does
not have one. This is not hypothetical: the framework's own `PROJECT.md` had exactly that defect,
recorded on 2026-08-25 — it gave `~/Repositories/ai-project-template` with nothing saying what held
it up, a form that resolved on one side of a boundary and not the other. A person found it. Row 14
was `n/a` and passed. That will happen again, and the price of this decision is that a person finds it
again.

**The limit is declared where a reader meets it,** in `structure-check`'s own notes, rather than left
to be rediscovered by the next audit. An undeclared limit and a defect look identical from outside.

**What would reopen this.** A second instance, on a project other than this one, where a missing path
note cost real work. One instance on the framework's own document is what this decision is weighed
against; two, with one of them elsewhere, would mean the population argument is wrong and the boundary
case is commoner than the `README` claims.

**What this does not decide.** Whether row 14 should exist at all. It still catches a path note that
names an arrangement without giving the command to create it, which is a real defect and the reason
the row was written. Only the silent case is conceded.

## Origin

**Decided by the owner, 2026-08-29. The reasoning arrived through him and this record cannot say how
much of it is his.**

The framework is reviewed by a second assistant whose prompts reach this session through the owner,
so a message here may carry his own words, the review's relayed, or both, and nothing inside the
session distinguishes them. What is certain is the decision: he asked for the cost to be stated
rather than assumed and refused the third outcome, leaving it in the backlog for another release,
which is what made this a decision rather than a deferral.

What arrived with it, and is recorded as arriving rather than as anyone's: that `0007`'s remedy is
available and identical in shape; that the two cases differ because an address is load-bearing for
every reader and a path note only where a boundary exists; and that either outcome is a result.

The two arguments this session added are the ones it can vouch for: that gating on the session note
was tried before `0.6.0` and caused the row never to run, and that a sentence ordinary work makes
vacuous teaches skimming.

**This ambiguity is not particular to this record.** `0008` and `0009` name a person for reasoning
that reached the session by the same route, and were written before the convention in
[`../handover.md`](../handover.md) existed.
They are left as they are rather than rewritten, because a record altered to look better informed
than it was is worse than one that is plainly of its time.
