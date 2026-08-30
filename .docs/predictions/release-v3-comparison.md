# Prediction: V3 compares fields, not prose

**Written:** 2026-08-30, before the edit and before any run.
**Subject:** [`release.md`](../release.md) step 7, row V3.

---

## The facts this rests on, established by reading the file and the tags

**What V3 is there to guarantee, as a fact about the repository:** at the moment before the tag, the
version this release calls itself is the same in both places that name it. As written, those two
places are `CHANGELOG.md`'s top entry heading and one sentence in `.docs/backlog.md`.

**What V3 literally compares:** nothing. It runs two commands and prints two lines —
`head -40 CHANGELOG.md | grep -m1 '^## \['` and `grep -m1 "released, tagged and pushed"
.docs/backlog.md` — and a person reads whether both name the version about to be tagged. The first
is a fixed heading syntax. The second is a fixed phrase inside running prose.

**How often it has fired, and how often it caught anything.** V3 did not exist at `v0.9.0` or
`v0.9.1`; it was written into `release.md` for `0.9.2`. Running the two commands against all twenty
tags gives:

| Occasion | Backlog half returned | Release actually correct? | Real omission? |
| --- | --- | --- | --- |
| `v0.9.1`, retrospective | nothing | no — backlog named `0.9.0`, changelog `0.9.1` | yes, but found by hand |
| `0.10.1` | nothing — *"are released"* did not match *"is released"* | yes | no |
| `0.11.0` | a meta-sentence quoting the phrase, naming no version | yes | no |
| `0.15.0` | a sentence *about* this drift, naming no version | yes | no |
| `0.16.0` | the `0.15.0` sentence about this drift — a quotation of itself | yes | no |

**Five firings, four of them during a release, and zero true positives.** In every release where V3
fired, the release was correct and the step was wrong. The one occasion where the guarded fact was
genuinely absent is the retrospective `v0.9.1` run, and there V3 returned *nothing at all* — the
same output as its four false alarms. The defect was identified by opening the backlog and reading
it. V3's contribution was silence, which it also produces when everything is fine.

**The `0.11.0` occurrence is not in any record.** The backlog counts four, naming `v0.9.1`,
`0.10.1`, `0.15.0` and `0.16.0`. Run against `v0.11.0`, the grep's first hit is line 12 —
*"When it is tagged this line becomes the usual "released, tagged and pushed""* — a sentence about
the phrase, naming no version. Same shape as `0.15.0` and `0.16.0`, one release after the grep was
loosened, and unnoticed at the time.

**The changelog half has never fired.** Across all twenty tags the top heading names the tag's own
version, every time, and equals the `Framework Version` carried by every blueprint `README.md`,
every time.

**Is the fact guaranteed elsewhere?** In two halves, and they answer differently.

- The **backlog** half is guaranteed by nothing, and needs to be guaranteed by nothing. Step 0 says
  a change under `.docs/` never causes a release, which makes that line a convenience rather than
  something a tag depends on. It is not shipped; no adopting project ever sees it.
- The **changelog** half is not guaranteed elsewhere, and this is the gap worth keeping. V2's
  criterion is *"every `Framework Version` reads the new number"* — and V2's output contains no
  statement of what the new number is. The reader supplies it from memory. A release where step 5
  typed a version the four `Framework Version` fields do not carry passes V1, V2 and V4 as written.

## The change

**Repair by subtraction, not removal.** The backlog grep is deleted, with the five paragraphs of
commentary that exist only to warn about it. What survives becomes an actual comparison, between two
things the procedure itself dictates the syntax of and a person cannot legitimately write two ways:
`CHANGELOG.md`'s top heading `## [X.Y.Z]`, and the `Framework Version:` field in every blueprint
`README.md`. The step prints both and the criterion is equality.

**Why a correct release cannot fail it.** Step 2 writes the new number into every blueprint
`README.md`'s `Framework Version`, and step 5 writes the same number into the changelog heading.
Both are fixed fields whose form the procedure specifies. There is no wording a person can choose
that changes either string.

**Why an incorrect one cannot pass it.** Three failures are visible in the printed output and no
judgement separates them: the changelog naming a number the blueprints do not carry, a blueprint
`README.md` missed so two distinct `Framework Version` values print, or a heading that is not a
version at all so nothing prints to compare.

**What is given up, deliberately.** The backlog's version line is no longer checked by anything and
may lag. Accepted on step 0's own ground.

---

## Pre-registered runs and their expected outcomes

**P1 — positive, the tree as it stands after the edit.** V3 prints `0.16.0` from the changelog and
one distinct `Framework Version`, `0.16.0`. Equal. **V3 passes on its own printed evidence.**
V1, V2 and V4 run beside it. V1 will list this pass's own `.docs/` files against a changelog entry
that does not mention them, because this is not a release and `HEAD` is ahead of the last tag by
these commits alone; that is expected and is not a V3 result.

**P2 — negative control, disclosed plant, changelog half.** A scratch copy of the repository with
`CHANGELOG.md`'s top heading changed to `## [0.17.0]` and nothing else touched. **V3 must fail**,
printing `0.17.0` against `0.16.0`. Scratch copy deleted after.

**P3 — negative control, disclosed plant, blueprint half.** A scratch copy with one blueprint
`README.md`'s `Framework Version` set back to `0.15.0`. **V3 must fail**, printing two distinct
`Framework Version` values. Scratch copy deleted after.

**P4 — the four false alarms, retrospectively.** Repaired V3 run against the trees of `0.10.1`,
`0.11.0`, `0.15.0` and `0.16.0`. **All four must pass**, because all four releases were correct.
This is the test of *a correct release cannot fail it*, and the four trees that broke the old step
are the strongest available sample for it.

**P5 — the one genuine historical defect, and the honest limit.** At `v0.9.1` the backlog named
`0.9.0` while the changelog named `0.9.1`. Repaired V3 does not read the backlog. **It will pass at
`v0.9.1`**, and **nothing else in step 7 will catch that defect either.** Predicted before running,
and recorded as an accepted cost rather than as coverage.

**What would falsify the change.** P1 failing, P2 or P3 passing, or any of P4's four trees failing.
Any one of those means the new comparison is not the comparison it claims to be.
