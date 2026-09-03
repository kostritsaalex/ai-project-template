# 0014. The razor runs over the questions, one at a time

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`0013`](0013-the-interview-ships-as-text.md) shipped the interview as text and named
[`0004`](0004-documents-carry-what-cannot-be-seen.md) as the basis of the split: **propose what can
be seen, ask only what cannot.** It then took its seven questions from what unspecified runs happened
to ask.

**The razor was applied to the file and never to its contents.** So the questions inherited whatever
the unspecified interview had been asking, including the parts that were never questions. The owner
found it by reading a live interview and asking why he was being asked things the assistant was
standing next to.

`0.11.0`'s seven questions lasted one release. The reason is worth more than the correction: **an
audit skipped is not an audit failed, and nothing in the release recorded that it had not happened.**

## Decision

**Each question is judged against `0004` on its own: could an assistant that read the folder have
proposed this?** Four survive.

| | `0.11.0` | Verdict | `0.12.0` |
| --- | --- | --- | --- |
| Name | asked | **seen** — the folder name | proposal |
| What it is | asked | not seen | question 1 |
| Boundary | asked | not seen | question 2 |
| Principles | asked | not seen | question 3 |
| Address | asked | **usually seen** | proposal, with a fallback |
| Components | asked | not seen — [`0005`](0005-the-registry-carries-the-component.md) | question 4 |
| Document owner | asked | — | **cut** |

**Every proposal names its source in the assistant note, and a proposal with no named source is not
one.** That rule comes from this batch's own history: `<DOCUMENT_OWNER>` was listed among the
proposals with no source named, and the unnamed source is exactly where the defect was.

**The address derivation, because it is the one that could do damage.** `new-project.md` calls the
address the value most worth getting right — every component copies it, and a wrong one leaves each
of them knowing a parent exists and unable to reach it. So the rule is narrow and names its own
fallback: a synced-store root gives `OneDrive, <path within the store>`; a git remote gives that
remote **normalised to a URL with its scheme**, and if it cannot be normalised to one of `0007`'s
four forms the assistant asks instead of writing it; with neither, the answer is `0007`'s fourth
form, `none` with the reason, never a blank and never a local path in the address slot.

**The last clause no longer holds. Superseded by [`0023`](0023-a-project-scope-address-is-required.md),
2026-09-03:** a project scope's address is required, the fourth form is for components only, and where
neither rule fires the interview asks. **Only that clause moves.** The rest of this paragraph is the
rule as it stands, and so is the rest of this record: the razor, the four questions and the cut are
untouched, and `0023` was decided by the method this record established.

**`<DOCUMENT_OWNER>` is cut, and this is a reasoned cut recorded as reasoned rather than measured.**
`0008` asks whether an assistant does anything differently for knowing a line. `Document Owner` names
a person to ask when the document is ambiguous, which is a convenience for a human reader; an
assistant meeting an ambiguous `PROJECT.md` reports the ambiguity and stops, named owner or not. The
backlog required this to be run or cut with the reasoning on the record, and no run was made. **It is
the only change in this release with no measurement behind it**, and it is the one to revisit first
if a project turns out to need the line.

**The boundary is answered in kinds of work, and the example says so.** See below — this is a
correction to `0011` as much as a change to the question.

## What carried this, and what did not

**Sixteen runs, pre-registered in
[`../predictions/interview-after-the-audit.md`](../predictions/interview-after-the-audit.md), plus
three before the tag.**

**Fidelity.** Zero added prose in every script run, `difflib` similarity 1.000 — eleven runs of the
mechanism now, across four subjects and five scopes.

**Four questions, never five**, on three scopes.

**The address, on all three branches, twice each.** Both git-remote runs normalised the SSH remote
and **cited `0007` unprompted**; both no-address runs produced the `none` form with a reason. The
registered falsifier — a proposed address satisfying none of the four forms — did not fire. It had
fired once before shipping, on this repository, which is why the git branch normalises and asks
rather than proposing the remote as found.

**The name proposal is justified by the razor and not by a run**, and it is the only part of the
question set of which that is true. Nothing in a scratch run can observe an owner correcting a
proposed name. It is stated here rather than left to borrow credibility from the measured changes.

**Not carried by folder-driven variance.** That argument was offered after an earlier experiment came
out indeterminate, and **a control arm on a deliberately different scope refuted it at −3.5%**. It is
named here because a finding that quietly disappears between two documents is the failure this
repository has spent three days cataloguing.

## Consequences

**The interview reaches a floor, and the floor is stated so it can be seen being crossed.** What
remains is what the project is, its boundary, its principles, and which folders are components —
exactly the set that lives only in the owner's head, which is what `0004` said a document carries.
**The convergence was not designed; it fell out of applying the razor question by question.** It
breaks if a placeholder ever needs a human answer and is not one of these four, or if one of the four
turns out derivable — components being the candidate, and `0005` currently forbidding it.

**The shipped metric falls by a line, to 40 and 22**, `<DOCUMENT_OWNER>` having left the header.
First movement in that number since `0.7.0`.

**A third shape of stale fact is named, and nothing is built for it.** `0004` cuts facts and `0008`
cuts rules; **an example is neither.** It demonstrates rather than states and can contradict its rule
while both read correctly alone. `0.10.0` inverted the boundary and changed its worked example from
three kinds of work to two places, recorded the rule change and not the example change, and **every
adoption for four releases followed the example.** The instrument is a reader, the same one the
existing shape two needs.

**Fidelity is not sufficiency, and this release does not close it.** No run answered these questions
and no `PROJECT.md` was produced. The placeholder map closes the part needing no adoption — eleven
placeholders, all sourced, twice — and the rest waits on an adoption. **`0.12.0` is provisional in
exactly the way `0.10.0` through `0.11.0` are, and all five wait on the owner's approval of this
question set rather than on scheduling.**

**The posture is untouched and that is deliberate.** A sharpened posture rule was measured, worked,
and was **pulled from this batch** because the owner reversed the posture axis the same day and the
sharpened rule says the opposite of the new one. Shipping and reversing it would put a rule in front
of him he has already decided against. The axis change itself waits on whether the core rule earns
its place, which two experiments have failed to establish.

## Origin

**Decided by the owner, 2026-08-30.** He read `0.11.0`'s interview in a live adoption and gave five
comments; four of them were one finding, which is that the audit above had never been done.

The framework is reviewed by a second assistant whose prompts reach a working session through him, so
a message here may be his words, the review's relayed, or both. What is certain is the decision. Two
of its constraints are his in substance: that the boundary and components questions not be merged
despite feeling duplicated, and that he approve the question set before any adoption runs.

What arrived with the review and is recorded as arriving rather than as anyone's: that the address
should be derived; that the duplication's cause is worth more than the merge; and that the name
proposal's justification be stated as razor rather than measurement.

Two corrections this session made to what arrived: **the SSH remote satisfies none of `0007`'s four
forms**, so "propose the remote URL" was wrong on that branch and it normalises or asks instead; and
**the example-category swap is established in git** rather than suspected, which is what turned a
guess about `0011` into a fifth stale-fact instance and then into a third shape.
