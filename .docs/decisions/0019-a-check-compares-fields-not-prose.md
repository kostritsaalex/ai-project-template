# 0019. A check compares fields, not prose

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`release.md`](../release.md) step 7 runs four verification rows between the commit and the tag. V3
existed to guarantee one fact about the repository: **at the moment before the tag, the version this
release calls itself is the same in both places that name it.** Those two places were `CHANGELOG.md`'s
top entry heading and one sentence in `.docs/backlog.md`.

**What it literally compared was nothing.** It ran two commands —
`head -40 CHANGELOG.md | grep -m1 '^## \['` and
`grep -m1 "released, tagged and pushed" .docs/backlog.md` — and printed two lines for a person to
read. The first matched a heading whose syntax the changelog format fixes. The second matched a fixed
phrase inside running prose.

**It fired five times and caught nothing.** Established by running both commands against all twenty
tags rather than from the record, which counted four and missed one:

| Occasion | The backlog half returned | Release correct? |
| --- | --- | --- |
| `v0.9.1`, retrospectively — V3 did not exist yet | nothing | no |
| `0.10.1` | nothing: the line had become *"are released"* | yes |
| `0.11.0` | a sentence quoting the phrase, naming no version | yes |
| `0.15.0` | a sentence *about* this drift, naming no version | yes |
| `0.16.0` | the `0.15.0` sentence about this drift | yes |

Four firings during a release, four correct releases, zero true positives. The `0.11.0` occurrence
was in no record before this pass.

**The one occasion the guarded fact was genuinely absent is `v0.9.1`**, whose backlog named `0.9.0`
while its changelog named `0.9.1`. There V3 returned *nothing at all* — the same output as its four
false alarms. The defect was found by opening the backlog and reading it.

**By `0.16.0` the failure had become self-sustaining.** The grep's first hit was the sentence written
in the `0.15.0` section to complain about this drift, which quotes the phrase in order to complain
about it. The step answered its own question with its own complaint, and every record written about
the problem became another false hit for the next release.

**The changelog half has never fired.** At all twenty tags the top heading names the tag's own
version and equals the `Framework Version` in every blueprint `README.md`.

## Decision

**A check compares fields, not prose.** Where a row asks whether two places agree, both sides must be
something the procedure itself dictates the form of, and that a person cannot legitimately write two
ways. A `grep` for a phrase in running prose is not that: the phrase is a wording, wordings get
rewritten by ordinary editing, and a document that discusses the check becomes a source of hits.

V3 is repaired by subtraction, in two parts.

**The backlog grep is deleted**, along with the five paragraphs of commentary that existed only to
warn about it. Nothing now checks the backlog's version line, and it may lag. This is accepted on
step 0's own ground: a change under `.docs/` never causes a release, so that line is a convenience and
not something a tag depends on. It is also not shipped — no adopting project ever sees it.

**What survives becomes an actual comparison**, between `CHANGELOG.md`'s top heading `## [X.Y.Z]` and
the `Framework Version:` field in every blueprint `README.md`. Both are fields. Step 5 writes the
first and step 2 writes the second, from one decided number. The row prints the changelog's version
and then lists every blueprint that does not carry it, so a pass is an empty list; the reader
supplies only whether that number is the intended one, which no command can know.

**A heading that is not a version must not pass.** If the changelog yields nothing the row searches
for a literal that cannot occur and lists every blueprint, rather than searching for an empty string
and matching them all. A comparison that cannot distinguish *"all agree"* from *"nothing to compare"*
is precisely what is being removed here.

**This closes a gap rather than restating V2.** V2's criterion is *"every `Framework Version` reads
the new number"*, and V2's output nowhere says what the new number is — the reader supplies it from
memory. A release whose changelog named a version the four fields did not carry passed V1, V2 and V4
as written. V3 is now where that referent comes from.

**Removal was on the table and was rejected on this ground alone.** Razor [`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md)
asks whether a release would go wrong without the step. Without the backlog half: no, five firings
prove it. Without the changelog half: yes, in the class this project has already produced twice —
`0.6.0` bumped four blueprint versions when one blueprint had changed, and V2's own criterion had to
be rewritten at `0.11.0` because as written it was wrong. Clerical disagreement between version fields
is a live failure mode here. So the half with a record of catching nothing goes, and the half with
nothing to compare against gets something to compare against.

## Consequences

**The step shrinks, and the amount was measured.** `release.md` falls from 140 non-blank lines to
138. V3's command block is three lines before and three after; its commentary falls from twelve to
ten. The paragraphs explaining how to interpret a drifting grep are gone, and nothing replaced them.

**The first attempt at this decision grew the file by eight lines while claiming a cut of six.** The
replacement was a seven-line shell loop printing one annotated line per blueprint. It was correct and
it was the thing this project keeps doing: justification accumulating beside a rule. `grep -L` does
the same comparison in one line and reports only the failures.

**The backlog's version line is now uncheckable by design.** If it is ever wanted back, it must
arrive as a field, not as a sentence.

**Run against all twenty tags, the repaired row has two true positives where the old one had none.**
`v0.1.0`–`v0.8.0` fail on `blueprints/checks/README.md` and `v0.1.0`–`v0.10.2` on
`blueprints/setup/README.md`: two blueprint folders that shipped without a version counter, gaining
one at `0.9.0` and `0.11.0` respectively. Both holes were found by hand at the time and one is still
open in the backlog. The row reproduces both, with the right dates, from the tree alone. Every tag
from `v0.11.0` on passes, including three of the four trees that broke the old row.

**The row's first committed form had the defect it exists to remove**, and an unregistered negative
control found it: taking the version from the first *version-shaped* heading meant a top entry that
was not a version was skipped and the previous release's number compared instead, so a changelog with
no current entry passed. It now reads the first `##` heading whatever it is. A comparison must fail
when it has nothing to compare, and writing that down in this record did not prevent writing the
opposite into the command.

**The rule generalises and is not applied here.** V1 compares a file list against changelog prose and
says so in its own text; it is the same shape. Whether that is repairable or is irreducibly a
judgement call is a separate question with its own evidence, and it is not touched in this pass.
