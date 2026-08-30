# 0017. A probe covers one declared path

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`0009`](0009-a-check-declares-its-read-set-in-advance.md) says a check declares its read set in
advance, and `registry-check` row 7 audits whether the run stayed inside it. On 2026-08-30 that row
produced its first true positive.

The operator ran the check against the real ArtGlina scope in a fresh session with no part in
building `0.14.0`, pasting the check's text. Rows 1 through 6 matched the pre-registration exactly,
both components, both `n/a` branches. **Row 7 failed**, listing four folders where the registry names
two: the scope's own root, the two components, and `/home/kostritsaalex/Projects`, which no registry
line names. The session's own account of how: it listed the fourth **as part of the same command that
tested the component folders**.

The two component paths are `~/Projects/All/artglina-ua` and
`~/Projects/Development/artglina-sandbox`. One command covering both reaches their common parent.
Nothing was inferred, nothing was followed, no subfolder was descended into: the read set was
exceeded by the shape of a command, and by nothing else.

**The read set was declared and correct. The rule was stated once, before the checks, and every row
that types a command was left to remember it.** Between *"That is your entire read set"* and the
moment a command is typed there is nothing.

## Decision

**A probe covers one declared path and no other. One declared path, one command.**

No command names two declared paths. No glob, brace expansion or wildcard whose resolution can reach
outside the path it was pointed at. **The parent directory of a declared path is not itself a declared
path**, so a command that names it has read it.

**The rule is stated once and marked at each moment it must be obeyed.** In `registry-check` those
moments are rows 1, 2, 5 and 6 — the rows that touch the filesystem. Rows 3 and 4 read files already
in the set and compute; row 7 opens nothing of its own. Determining that list from the prompt rather
than assuming it is part of the decision: the row that actually broke was row 1, which nobody would
have named first, and its evidence in the passing `0.14.0` log is the words *"listed it, the folder is
there"* once per component.

## Consequences

**Row 7 is unchanged, and permitting parents of declared paths was rejected outright.** The row read
correctly on its first live case. Widening it to admit the parents of declared paths would have made
every future instance of this invisible, and adjusting an instrument immediately after its first
correct reading is a failure this project has already recorded once in its own log. **The defect was
in the procedure the row measured, so the procedure changed and the instrument did not.**

**A check pays one probe per declared path.** A registry with six components costs six probes where
one glob would have done. That is the price of a read set that is a set of paths rather than a region
of the filesystem, and it rises linearly with the registry.

**A rule stated once, far from where it is obeyed, is not obeyed. This is the third instance of that
one shape in this check.**

- The prompt says to paste its text rather than reference the file, and that instruction sits inside
  the file a session must open in order to read it. Row 7 failed on it.
- The prompt said what a non-attached component is, and had no state for the one `0.13.0`'s interview
  made the normal first state. Six rows failed on it, repaired in
  [`0016`](0016-declared-is-a-second-non-attached-outcome.md).
- The prompt declares a read set, and the rows that act on it carried nothing at the moment of
  acting. Row 7 failed on it, and this record is that repair.

Each time the rule existed, was correct, and was written somewhere other than where it had to be
obeyed. **The general form: a rule that governs an action belongs where the action is taken, and a
statement of it elsewhere is documentation rather than instruction.** That form is worth applying to
the other two checks before their own first true positive arrives.

**The duplication is deliberate and is a cost.** Principle 5 says a rule in two places will disagree
with itself, and this ships the rule in one paragraph plus four clauses that point at it. The
alternative was the arrangement that had just failed. The clauses say where a probe may reach and not
why; the paragraph carries the reasoning, so there is one place to change if the rule changes.

**It bounds probing and not reading.** A session can still read a file it should not, and row 7
remains the only thing that catches that, after the fact.

## Origin

Alex, 2026-08-30, on being shown row 7's failure and refusing the obvious repair. His framing: the
row is not defective, this is its first true positive, and the defect is in a procedure that permits
a command whose blast radius is wider than the declared read set.
