# 0012. Two default principles of eight

**Date:** 2026-08-29  
**Status:** accepted

---

## Context

The owner asked that the project blueprint offer a set of recommended principles rather than leaving
the section blank, and supplied eight. His instruction was that principles are offered as a default,
not that all eight are, and that each be judged against
[`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) first: **a rule earns a place
only if an assistant would do otherwise without it.**

## The judging, one by one

**Two survive. Six do not.** That is a heavier cull than was anticipated, and the reasons are per
principle rather than a general objection.

**1. Understand the current architecture. — Cut.** An assistant asked to change something inspects
what is there. `0003` cut "inspect before changing" by name, as one of the lines that "restated
behaviour any competent assistant already has". In a project that is mostly not code there may be no
architecture to understand, which makes it not merely redundant but occasionally meaningless.

**2. Identify the affected scope. — Cut, twice over.** As a rule it is what any assistant does before
acting. And **`scope` is this framework's own word** for a project scope or a component, so in a
document that carries a registry of scopes the sentence reads as an instruction about the registry
when it means "work out what you are touching". A default principle that collides with the
framework's vocabulary is worse than no default at all.

**3. Read relevant documentation. — Cut.** Default, and already compelled by mechanism: the stubs
send a reader to `PROJECT.md` before any task, and `CLAUDE.md` imports it. A principle restating what
the entry-point machinery already forces is the platform fragment's shape exactly.

**4. Prefer improving existing patterns over introducing new ones. — Cut, on direct precedent.**
`0003` cut "follow the existing style" by name. This is that with a preference against novelty
attached, and the preference is the part most likely to be wrong in a project deliberately trying
something new.

**5. Keep the framework simple and internally consistent. — Cut.** Two halves and neither holds.
"Simple" restates principle 7 without adding a test. "Internally consistent" is a real property, but
it is enforced by mechanism rather than by principle here: `structure-check` already says that where
two documents disagree both are quoted and the row fails. The word "framework" is also this
framework's name for itself and would have to become "the project" before the sentence could ship at
all.

**6. Validate architectural ideas through practical usage whenever possible. — Survives**, with more
evidence behind it than any of the eight. It is this framework's own principle 6, and it is what
produced everything measured on 2026-08-29: pre-registration, runs in both directions, committed
logs. Without it an assistant argues for an idea and ships it; with it, it runs the idea first. That
difference has been observed repeatedly here, most sharply when a reading-based confirmation was
overturned by a control arm.

**7. Avoid speculative additions. — Survives**, and this session is the evidence. On the same day it
added a clause to a check that prescribed nothing and had to cut it, and re-introduced an enumeration
in the sentence that removed it. An assistant does make speculative additions. A principle forbidding
them is not describing default behaviour.

**8. Preserve backward compatibility where practical. — Cut.** Domain-specific to software with
consumers, hedged by "where practical" until it constrains almost nothing, and empty in a folder of
photographs. It is a good principle for a project that ships an interface, which is what the
free-text section is for.

## Decision

**The blueprint offers two principles, 6 and 7, as a recommended default. It offers them; it does not
pre-fill them.**

They are named in `blueprints/project/README.md` as a default the interview may put forward, shown in
the summary table as *proposed* rather than settled, and written into `PROJECT.md` only if the owner
keeps them. The `<PRINCIPLES>` slot stays empty in the blueprint file itself.

**The platform-fragment objection, answered rather than left beside.** `0008` removed pre-filled
content offered for a section an owner was meant to write, and this is that shape. The shape is not
the defect. The fragment failed the razor: a component carrying it and one without produced the same
work, measured. A principle that passes the razor is by definition not what an assistant does anyway,
so the two cases differ exactly where it matters. What `0008` cut was pre-filled content that changed
nothing, not pre-filled content as such.

**The objection the fragment case does not cover, and it is the real one.** A default invites
acceptance without thought. `procedure.md` Step 4 says to ask for a value empty, because a value the
assistant has not observed "will look plausible and be wrong", and a person late in an interview
accepts more than they compose. That is why these are offered aloud and shown as proposed rather than
written into the template: the owner has to say yes to each, and saying nothing leaves the section
empty.

This narrows Step 4 rather than contradicting it, and the narrowing is written into the procedure:
principles are the one value that may be offered rather than asked for empty, because unlike an
address they are not a fact about the world that a wrong guess corrupts, and because an owner with no
principles yet is better served by two to reject than by a blank page.

## Consequences

**Six principles are not shipped, and one of them is the owner's own vocabulary problem.** Number 2's
collision with `scope` would have shipped a word this framework defines into a sentence that uses it
differently, in the one document that carries the registry.

**The two survivors are both about method rather than about subject matter**, which is why they
survive a blueprint serving projects that are not software. Neither mentions code. That is not an
accident of selection: the six cut are the six that assume a codebase, and the two kept are the two
that would mean something to a potter.

**The evidence for both is this framework's own use, and that is a narrow base.** Neither has been
run on a project that is mostly not code. ArtGlina is about to be, with these two offered in its
interview, which makes it the first test rather than a confirmation.

**What would reopen the six.** A measured run in which one of them changes the work. The design is
already known and costs two runs: one task with the principle present, one with it absent, judged by
the work. Any of the six can be readmitted that way, and none should be readmitted by argument.

## Origin

**Decided by the owner, 2026-08-29,** who supplied all eight and set the condition that each be judged
against `0008` before any shipped. The convention in [`../handover.md`](../handover.md) applies: the
decision and the eight are his, and this session cannot say how much of the surrounding reasoning is.

The doubt that they read as software principles for a blueprint serving more than software arrived
with them, and named 1 and 8 as least likely to survive. Both were cut, along with four the doubt did
not name. The per-principle reasoning and the answer to the platform-fragment objection are this
session's.
