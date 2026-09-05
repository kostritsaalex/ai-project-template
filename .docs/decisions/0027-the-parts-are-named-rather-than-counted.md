# 0027. The parts are named rather than counted, and shared meaning replaces shared shape

**Date:** 2026-09-05
**Status:** accepted. Supersedes the enumeration in
[`0024`](0024-a-decision-record-names-its-options-and-its-revisit-trigger.md) and leaves the
rest of it standing.

---

## Context

[`0024`](0024-a-decision-record-names-its-options-and-its-revisit-trigger.md) settled six
things a record carries. A cross-agent review of that list, conducted with the advisory agent
on the `wordpress-architect` plugin and relayed by the owner, found four defects in it and
one omission. Each is small; together they are the difference between a list and a
specification.

**`Status` was not in the list, and every record here has one.** Twenty-six of twenty-six,
including `0024` itself, whose own status is a sentence. A standard that omits a field its
own records all use leaves an adopter to settle it, and an adopter that settles an undefined
field becomes the standard by accident. That phrasing is the plugin side's and it is the
reason this is fixed here rather than there.

**Two sentences in `0024` contradicted each other.** Field 3 required "at least two viable"
options and said a record with one option is a justification rather than a decision. A later
ruling made a stated and reasoned absence of alternatives a properly filled options field. Read
together, one document could be a correctly filled record and a justification at the same time.

**The list made all six mandatory in the same way**, so a small decision paid for an options
table it had nothing to put in.

**`0024` said nothing about a field one side needs and the other does not.** Defending an
identical shape across two repositories produced two wrong placements of the same fact in
succession: an approver pushed first into Consequences prose, where no reader looks for it,
then into `Status` prose, which is rewritten when standing changes and would have deleted it.

**And the absence of an index of decisions stood as an unresolved gap** when it is arguable
either way and nobody had argued it.

## Decision

**`Status` is a part of the record.** Its first token comes from a closed set, lowercase:
`proposed`, `accepted`, `superseded`, `rejected`, `deprecated`. Everything after the token is
free prose, and where the status depends on another record that prose names it and links it.
Supersession lives here and in no field of its own. `deprecated` means no longer applied with
nothing replacing it; this repository has no instance, and it is in the set because a platform
release can overtake a decision without any decision displacing it.

**Nothing durable may be stored in `Status` prose.** The line is rewritten when standing
changes and prior content usually does not survive. Of the three records here whose status
names a supersession, two lost everything the line held: `0002` no longer carries the word
`accepted` at all, `0011` retains its supersession clause and a date and nothing else. The
third, [`0003`](0003-cut-the-framework-to-four-jobs.md), keeps its standing beside the
supersession and is the counter-example. So content can survive and nothing requires it to,
which is enough: a field where a durable fact survives at the writer's discretion is not a
place to put one.

**The parts are named and nowhere counted.** Two header fields, `Date` and `Status`, then five
sections in this order: Context, Decision, Options considered, Consequences, Origin. The
revisit trigger is the last line of Consequences and not a part of its own. `0024` called this
"six things" and a later draft called it "seven fields"; both were counts over a membership
that moved while the total did not, which is a number concealing a change rather than catching
it.

**Every part is present in every record, and a stated absence fills it.** "No viable
alternative existed: X is the only mechanism available here" is a filled options field. The
rule applies wherever an absence would otherwise read as correct, which is why a missing part
must be spoken for and a missing sub-heading inside a filled prose section need not. **The rule
does not recurse.**

**The options part is restated, and the test moves off the count.** It carries what was
examined, and for each what it buys and how it fails. Where examination found no viable
alternative, it says so and says what was examined to establish that. **A record that names one
option without saying what else was examined is a justification and not a decision.** No number
is specified: a record with two options, one of them a strawman, passes a count and is exactly
the advocacy the part exists to prevent. The contradiction goes with the count.

**Shared meaning replaces shared shape.** The header fields and sections named above are shared
with any side adopting this standard and carry the same meaning there. A side may carry an
additional header field where a written rule of its own domain requires a fact no shared part
holds. An added field may not restate, replace or redefine a shared field or section, and it is
declared to the other side when added. **Identical shape is not the goal. Identical meaning of
the shared parts is.**

**There is no index of decisions, and the absence is argued rather than unresolved.** A bare
filename index writes what a folder listing already shows, which
[`0004`](0004-documents-carry-what-cannot-be-seen.md) forbids. An index carrying status and
summaries becomes a second place where status lives, and principle 5 says a fact in two places
will disagree with itself. What stays open is discovery, not indexing: how a reader finds the
record that governs a question.

## Options considered

| Option | What it buys | What it costs and how it fails | Decision |
| --- | --- | --- | --- |
| Leave `0024` and let each adopter settle `Status` | No work here | The first adopter to define it defines it for everyone, by accident and without argument. Fails silently and is discovered only when two sides disagree | Rejected |
| Fix the count rather than drop it | One number to cite, familiar | The total held at seven while membership moved; the number hid the change instead of catching it. Fails again the next time a part moves | Rejected |
| Split mandatory and optional parts into two tiers | Small records pay less | Two classes of part, a judgement at writing time about which tier applies, and an incentive to file a part as optional. The stated-absence rule gets the same relief for one sentence | Rejected |
| Keep an identical shape across both sides, with no added fields | One form everywhere | Forces a fact one side must record into a part built for something else. Observed twice in one review, the second placement into a field that deletes its contents | Rejected |
| Name the parts, drop the count, admit declared additions | Membership is visible, a stale count cannot hide a change, and a side may record what its own domain requires without forking the form | Two shapes exist rather than one, and an addition rule can be abused into drift if a side stops citing a written domain rule | **Chosen** |

## Consequences

**`0024`'s enumeration is superseded and the rest of it stands.** Its measurement condition is
handled separately, in [`0028`](0028-an-arm-pair-differs-by-one-variable.md). Its razor split,
holding the blueprint template unshipped until measured, is untouched.

**The earlier records are not retrofitted.** Twenty-six records written before this one carry
whatever they carry. This record is the first written to the parts as named here.

**The addition rule can drift and nothing here stops it.** Its only brake is the requirement of
a written domain rule on the adding side, which that side cites and this side cannot verify. A
side that stops citing, or that writes a domain rule in order to justify a field, defeats it.
No mechanism is proposed, because every mechanism this side could think of costs more than the
drift.

**A checker could now exist and would reach almost nothing.** The header lines, the first token
against the closed set, the presence and order of the sections and a revisit line at the end of
Consequences are checkable. Whether an option is real, whether a cost is honest, whether a
search happened are not. Any such checker states that in its own output, or a passing record
reads as a validated one.

**Recovery.** Every part of this record is additive or subtractive on a list; withdrawing any of
it is an edit to a later record and touches no blueprint, no check and no adopted project,
because none of this ships until `0024`'s measurement runs.

**Revisit** when the addition rule is used a third time, which is when drift would first be
visible, or when a part moves again and the note in this record about the older membership stops
being enough to orient a reader.

## Origin

A cross-agent review relayed by the owner, between a working session on this repository and the
advisory agent on the `wordpress-architect` plugin. The `Status` gap was found independently on
both sides. The contradiction in field 3 and the required-versus-optional objection came from
that side; the relocation of the test from the count to the search is this side's answer to it.
The addition rule is this side's, written after that side found that the `Status`-prose
placement it had accepted would delete the fact it carried. The three-of-three measurement first
reported here was wrong and is corrected above to two of three with its counter-example named.
