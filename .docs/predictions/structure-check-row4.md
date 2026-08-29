# Prediction: `structure-check` row 4, named comparison and a negative arm

**Written:** 2026-08-29, before either arm runs.  
**Subject:** `structure-check` row 4, rewritten to name the comparison it makes.

## Why

The audit found row 4 under-specified: it said "the same text, apart from their first heading, apart
from any line beginning with the at sign, and ignoring blank lines", and left the tool to choose
line-wise or token-wise comparison and to decide what counts as sameness. Both runs on 2026-08-29
happened to choose character-for-character and to say so, which is a baseline for the old wording and
not a guarantee.

Row 4 ranks first over both axes: a wrong answer is a silent pass on two stubs that differ, and
nothing else covers it except the naming line, which row 7 also holds. A false pass here defeats the
one thing the pair of files exists to guarantee.

## The change

The row now states the procedure and requires the tool to say it performed it: remove each file's
first heading line, every line whose first non-blank character is an at sign, and every blank line;
compare the remainder in order, character for character; report how many lines each side had and what
was removed; on a failure quote the first differing pair with line numbers from both files.

## Arm 1 — positive, no plant

Both stubs of `wp-themes` are correct and identical apart from the heading.

**Predicted:** row 4 passes, and the evidence names the removals and gives a line count for each
side. Every other row as in the two runs of 2026-08-29: `Failed checks: 0`.

**Run twice.** A pass here is evidence of an absence — no difference found — and the rule recorded in
`handover.md` today says repeat the run whose evidence is an absence.

## Arm 2 — negative, one variable

`wp-themes/AGENTS.md` only, the escalation line:

```text
before:  If you cannot reach it, say so and stop. Do not proceed on guesses.
after:   If you cannot reach it, say so and halt. Do not proceed on guesses.
```

One word, in one file. This is what one stub edited and the other forgotten actually looks like, and
it is deliberately **not** the naming line, so that row 4 is the only row that should fire: the
ownership map records rows 4 and 7 both firing on a divergent naming line, and this arm is meant to
isolate 4.

**Predicted:** row 4 fails, quoting both versions of that line with a line number from each file.
Row 7 passes, the component still being named identically in both. Row 9 passes, both stubs still
saying what to do when the parent cannot be reached. Nothing else fires. `Failed checks: 1`.

**Run once.** A failure carrying a quotation is self-verifying.

## What would falsify the change

- **Arm 2's row 4 passing.** Then the named procedure did not make the comparison stricter and the
  rewrite bought nothing.
- **Arm 2's row 9 failing.** The line still says what to do; "halt" is a synonym. A failure there
  means row 9 is matching fixed wording rather than reading a claim, which would be a finding about
  row 9 rather than row 4.
- **Arm 1 failing.** The two stubs are correct; a failure means the procedure is stricter than the
  documents the framework ships.
- **Either arm's row 4 passing or failing without saying it performed the procedure.** The row now
  requires the tool to state the comparison. Silence there is the row not being followed, whatever
  the verdict.

## Restoration

`wp-themes`' two stubs are already snapshotted with checksums. Arm 2 is restored from that snapshot,
not retyped, and verified byte-identical.
