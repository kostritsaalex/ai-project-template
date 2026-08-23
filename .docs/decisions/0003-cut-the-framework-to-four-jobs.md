# 0003. Cut the framework to four jobs

**Date:** 2026-08-22  
**Status:** the cut stands; its four jobs are superseded by the single test in
[0004](0004-documents-carry-what-cannot-be-seen.md).

---

## Context

The framework grew for a week and reached a state its own author was reluctant to touch. That is the
finding. Every rule in it had arrived from an observed failure and was defensible on its own, and the
sum was not the thing being built.

Two measurements made the case concrete.

The text that ships into every adopted project stood at 272 non-blank lines across the three
entry-point templates. Reviewed line by line against the question "what does an assistant do
differently if this is gone", about a quarter restated behaviour any competent assistant already
has: inspect before changing, follow the existing style, investigate when sources conflict.

The version machinery cost more than it returned. A counter in the project document, a counter in
each component, a third recording which project version the component was written against, and an
obligatory pass over every component whenever the project document changed for any reason. It was
adopted three days earlier in [decision 0002](0002-project-version-rises-on-any-change.md), which
settled the right question and left the prior one unasked: whether the mechanism should exist at all
for a project run by one or two people.

Against that, the record of what actually changed an assistant's behaviour is short. One clause in a
component's escalation boundary, which stopped an assistant building infrastructure the project
excluded. The reconnaissance step, which caught an entry point copied from an unrelated project
before it was overwritten. Everything else passed its checks, and checks measure what an assistant
says.

## Decision

The framework exists for four jobs:

1. Gather the folders and repositories of one project under a single project folder, so an assistant
   can move between them.
2. Hold the project-wide rules and the map of the project in one document at that folder's root.
3. Let a component specialize those rules for itself.
4. Let a component state what an assistant cannot see by looking.

The first three are the owner's. The fourth was added during the same discussion, because two
proven behaviours fell outside the first three: the address of the parent together with the
condition for following it, and the hazards a folder cannot show.

Text serving none of the four is removed. `Sources of Truth` and most of `Project-Wide AI
Principles` are gone; `Change Principles` and `Verification` keep the lines that are not defaults
and lose the rest.

Version counters are removed entirely. A component records `Parent checked`, the date it was last
read against the parent, and compares it with the parent's `Last Updated`. Editing a project
document obliges nobody to touch anything else.

One case still reaches other components by hand: a changed `Project Location`. Every component
carries a copy of that address, and a stale copy passes both checks and fails only when somebody
follows it.

## Consequences

The shipped text falls from 272 lines to 172, a little over a third.

Decision 0002 is superseded in effect. Its reasoning stands for the mechanism it governed; the
mechanism is gone.

What is lost is a forcing function. The sweep made the owner open every component whenever the
project changed, so a rule that started contradicting a component's text was found on the next
change rather than on the next visit. Without it, a contradiction sits until somebody happens to
work there. At two to five components written by one person that is a fair trade. At twenty across a
team it would not be.

Two adopted projects stay on the old form and will drift from the blueprints until they are brought
across. Nothing breaks in the meantime: the removed fields are inert, not wrong.

## Origin

Alex, 2026-08-22, after a week of daily additions, most of them proposed by the assistant he was
working with. The sentence that settled it: he had begun to fear changing the framework.
