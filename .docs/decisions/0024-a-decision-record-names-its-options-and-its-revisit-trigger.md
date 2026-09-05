# 0024. A decision record names its options and its revisit trigger

**Date:** 2026-09-05
**Status:** accepted for this repository's own records. Shipping the form into `blueprints/`
is proposed and waits on the measurement named in Consequences.

---

## Context

The framework publishes no ADR template. `blueprints/project/PROJECT.md` names
`.docs/decisions/` as the place and says nothing about what a record contains. The shape the
23 records here take is practice, never written down and never measured, so there is nothing
for another tool to align to. That is what the alignment question surfaced.

**What the 23 records already do, and what they do not.** Counted by keyword search over
`.docs/decisions/*.md` in the session that wrote this record. The instrument is a proxy: it
reports a word, not the thing. It settles direction, not the figures, and the two weak rows
are weak by a margin a better instrument would not reverse.

| What the record carries | Of 23 | Reading |
| --- | --- | --- |
| The cost, what the decision gives up | 20 | Written without a template; `handover.md` already requires it |
| Evidence: what was measured, against what control | 20 | The strongest habit here |
| Options considered and rejected | 8, as a table 2 (`0014`, `0019`) | Mostly absent or buried in prose |
| A revisit trigger | 5 in prose, 0 as a field | Absent as a mechanism |
| A date, `YYYY-MM-DD`, no time | 23 | Already settled; nothing to change |

The two weak rows are the two fields the `wp-adr` template makes mandatory. The two strong
rows are fields that template lacks. It carries `Evidence and links`, a list of issues, tests
and dashboards, which is not the same object as a statement of what was measured against what
control. It has no `Origin`, and `Origin` stands in 19 of the 23 records here.

Neither shape contains the other, so adopting either wholesale loses something that works.

**The precedent that constrains this.** `0.8.0` deleted
`blueprints/repository/platforms/wordpress.md`, a 50-line fragment pasted into every adopted
WordPress component, because measured against a control its rules changed no work. See
[`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md). A template shipped
into every adopted project is structurally the same object. That a form changes what a person
writes, where a rule sheet did not change what an agent did, is plausible and is not evidence.

## Decision

**A record carries six things.** Four are what the 23 already do; two are new.

1. The decision, in one sentence.
2. The context and the constraints that forced it.
3. **The options considered, at least two viable, with what each buys and how each fails.** A
   record with one option is a justification and not a decision.
4. The consequences, including the cost and the risks accepted with no mitigation. The
   recovery path, where the decision has one, sits here rather than in a section of its own.
5. **A revisit trigger: a date, or the condition that would reopen this.** Last line of
   Consequences.
6. `Origin`, naming the channel a decision arrived through and not its author.

The date line stays as it is. No decision here has ever turned on the hour it was taken.

**Three fields of the `wp-adr` template are not adopted.** `Owner`, because it is constant in
this repository and a constant field is noise by
[`0004`](0004-documents-carry-what-cannot-be-seen.md). `Evidence and links` as a link list,
because the local sense of evidence is what was measured against what control, and that is
prose belonging to Context and Consequences. `Delivery and recovery` as its own section, for
the reason given in field 4.

**A record is owed when the trade-off outlives the task that produced it.** Not when the
change felt large. A choice made in ten minutes can bind migration, backup and export for
years, and how long it took is not evidence about how long it lasts.

**In a live project, verification and revisit are fields and not a folder.**
`.docs/predictions/` exists here because this repository's product is rules, and a rule is
judged only against an expectation written before the run. A live project's product is working
software and has no equivalent object to judge. The discipline reaches such a project through
fields 3 and 5, and `predictions/` does not ship.

Where records live is [`0025`](0025-a-decisions-folder-belongs-to-a-declared-component.md).
What they are named is [`0026`](0026-a-record-carries-its-subject-only-when-the-folder-cannot.md).

## Options considered

| Option | What it buys | What it costs and how it fails | Decision |
| --- | --- | --- | --- |
| Keep the present shape | Nothing new to learn; 23 records already consistent | Leaves the two measured gaps open, and leaves nothing for another tool to align to | Rejected |
| Adopt the `wp-adr` template wholesale | One shape shared with the WordPress tooling immediately | Drops `Origin`, which 19 records use, and replaces evidence with a link list. Fails by losing the two things this repository does best | Rejected |
| Merge: its mandatory fields, plus `Origin` and evidence in the local sense | Closes both measured gaps and keeps both strong habits | Two more fields to write every time, the options field being the expensive one. Fails if records stop being written at all | **Chosen** |
| Merge and ship the template into `blueprints/` now | Every adopted project gets the form at once | Ships an unmeasured 40-line artefact into every project, which is `0008` broken in the letter and `0.8.0` repeated | Rejected, pending measurement |

## Consequences

**The 23 existing records are not retrofitted.** Fields 3 and 5 apply from here onward, and
this record is the first to carry both, which is the only way a form is tested by the decision
that adopts it.

**The options field is the expensive one, every time.** The honest version means finding a
second viable option rather than inventing a strawman. Eight records of 23 named an
alternative; the other fifteen may have had none, or may have had one nobody looked for. No
reader can tell those apart, and neither can this record.

**Risk accepted with no mitigation.** Two more fields make records longer, and the failure mode
of a documentation rule is that people stop writing records. Nothing here guards against it.
The first sign would be a release reaching step 4 of `release.md` with no record behind it.

**Recovery, if the fields turn out to be dead weight.** They are additive and unenforced by any
check, so removing them is an edit to this record and nothing else. No blueprint, no check and
no adopted project depends on them while the template stays unshipped.

**What would let the template ship into `blueprints/`.** One real decision, two records, one
written to the six fields and one to the shape the 23 use, judged by the work each produces
rather than by which reads better. A single run proves nothing, and the control matters more
than the treatment here, because the treatment is the thing being sold.

**Revisit trigger.** The measurement above, whenever it runs. Failing that, the first release
that reaches step 4 of `release.md` with no record behind it, which would say the fields cost
more than they return.

## Origin

Proposed by the owner in a working session, as two positions put for argument: that a
three-field record is too thin to be useful, and that the fuller `wp-adr` shape is the one to
lean toward. The counts in Context were taken in that session over this repository's own files,
and no file was modified to produce them. Two of those counts were first reported wrong in the
session, 21 and 0 where the data says 20 and 5, and were corrected before this record was
written. The split between what is accepted and what waits on measurement was argued against
`0008` and the `0.8.0` precedent in that session, and is not what was proposed.
