# 0028. An arm pair differs by one variable, and the variable is named before the run

**Date:** 2026-09-05
**Status:** accepted. Supersedes the measurement condition in
[`0024`](0024-a-decision-record-names-its-options-and-its-revisit-trigger.md).

---

## Context

[`0024`](0024-a-decision-record-names-its-options-and-its-revisit-trigger.md) holds the record
format unshipped until it is measured, and states the measurement as "one real decision, two
records, one written to the six fields and one to the shape the 23 records here use".

**That condition specifies a confounded design.** "The shape the 23 use" is unspecified,
because those records were written to no specification at all. So an arm built from it receives
bare headings while the other receives a sentence describing each part. The arms then differ in
two ways at once, in which parts exist and in how much the drafter was told about any of them,
and a richer treatment record is explained equally well by the parts under test and by the fact
that one drafter was told more of everything.

**The defect reached a live registration before anyone saw it.** The advisory agent on the
`wordpress-architect` plugin proposed exactly that design, faithfully, because it is what this
repository asked for. It was corrected before the pair ran, but only because a second party read
the registration rather than the record it came from.

**This repository already knew better and did not apply it to itself.**
[`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) built its own arms so
that "the difference is one variable rather than two", records that its first attempt got this
wrong and "measured a broken component instead of the question", and confirmed the arms
"identical by `diff -r` across both trees rather than by construction". The founding experiment
of the razor this measurement serves states the standard the condition failed.

## Decision

**An arm pair differs by one variable, and both arms are specified at the same density.**
Everything the arms share is described in the same words at the same length. The difference
between the two instructions is the thing under test and nothing else.

**Verified by diffing the two instruction texts, not by having built them carefully.** The
entire diff output is the insertion or removal under test. Zero lines altered, zero removed
where an insertion is intended, and any shared material byte-identical by checksum rather than
by reading. The diff is re-run on the live files immediately before drafting and the result is
stated with the finding, because a text that travelled between two people is not the text that
was verified.

**The variable is named before the run and it may be a set.** Where the thing under test is a
set of parts that will ship together, the set is the variable. Its members may be read
separately when their insertions have disjoint targets and distinguishable outputs, and no
claim is supported about any member acting in the absence of the others. **Isolating members
within such a set is closed, not deferred**, where the form ships them together: the isolation
answers a question nothing acts on.

**The instrument may not mandate in both arms what only one arm is supposed to carry.** A
command, template or prompt that requires the thing under test contaminates the arm meant to
lack it. This is [`0018`](0018-the-instrument-is-not-part-of-the-sample.md) applied to the
drafting instruction, and it is the reason a pair cannot be produced by a tool that already
implements the treatment.

**The prediction names the quantity that discriminates.** For a record format that quantity is
whether alternatives are EVALUATED, not whether they are named. This is the correction the one
pair that has run actually produced: the control named genuine alternatives in prose and
evaluated none of them, which a naming prediction cannot see.

**Both arms are judged, by the same questions, by a party that did not draft either.** Asking
only of the treatment decides a comparison by the presence of a heading, which the treatment has
by construction and the control cannot have by construction. A judge blind to which arm is which
is not achievable where the arms differ visibly; a judge blind to the hypothesis, to the
existence of a pair and to the wanted answer is, and that is what is required.

**The registration is written before either record is drafted** and names the control, the
treatment, the expected difference, what outcome would argue against the thing under test, and
the confounds. A registration written after a run is a description.

## Options considered

| Option | What it buys | What it costs and how it fails | Decision |
| --- | --- | --- | --- |
| Keep `0024`'s condition | Nothing to write | It specifies the confounded design, and it already produced one. Fails by yielding a result nobody can attribute | Rejected |
| Match the arms on density, one variable | The result is attributable. Cheaper than the alternative, since it removes an arm rather than adding one | It no longer answers "does a specified form beat no form", which is what shipping into a blueprint eventually needs. That is a second measurement with a second design | **Chosen** |
| Three arms: bare, specified-without-the-parts, specified-with | Answers both questions at once | Three records per subject, and the third arm is a form nobody would ship, so a third of the cost buys a configuration that does not exist | Rejected |
| Accept two variables and report the result as not isolated | Cheapest of all | A result labelled not isolated is retold without the label. `0008`'s first attempt is the precedent, and it was redone rather than caveated | Rejected |

## Consequences

**`0024`'s shipping condition is unchanged in force and changed in shape.** The template still
does not enter `blueprints/` until measured. What counts as that measurement is now this record,
and it still requires at least one pair from outside the domain the first pair came from.

**One pair has run under the corrected design and it settles nothing alone**, which its own
registration says. Its three predictions held; the effect it exposed was on evaluation rather
than on naming, which no prediction had claimed; and the arm without the parts under test
produced the same epistemic disclosure as the arm with them, so that disclosure is not
attributable to those parts.

**The cost accepted with no mitigation.** Matching the arms on density means the pair answers a
narrower question than the one shipping ultimately needs. This record chooses an attributable
answer to a narrow question over an unattributable answer to a broad one, and nothing here
recovers the broad one.

**A dependency is recorded as untested rather than as open.** Both arms of any pair here carry
an instruction to ground every statement in the source and to say where the source does not show
something. Two observed effects rest on it and its own contribution will not be separated,
because isolating it needs an arm no form would ship. The tell that would reopen it: a record
asserting a decision history its source does not support, under a form that carries the clause.

**Revisit** when a pair runs whose thing under test is a single part rather than a set, which is
the case this record's set clause has never faced, or when a measurement here is contested on a
ground this record does not cover.

## Origin

A cross-agent exchange relayed by the owner. The confounded condition was named by this side
after the plugin side had faithfully reproduced it in a registration; the plugin side accepted
the correction and then found that the corrected design was itself two insertions rather than
one, which produced the set clause. The instrument objection came from this side and was
confirmed by that side against its own command. The move from naming to evaluation came out of
the pair rather than out of either side's argument.
