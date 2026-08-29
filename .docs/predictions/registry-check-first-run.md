# Prediction: the first run of `registry-check`

**Written:** 2026-08-29, before the check had been run once.  
**Subject:** `blueprints/checks/registry-check.md` as committed in `381b200`.  
**Scope under test:** `WordPress 7`, two components, one contained (`WP Themes`, addressed
`wp-themes/`) and one with no address (`WordPress 7 Engine`, local path
`~/Projects/Development/wordpress-7`).

This file exists because a prediction stated after a result is not a prediction. Three defects are
recorded below, all found by reading the prompt rather than by running it. The check will be run as
written, without fixing any of them first, and only then repaired. What the run finds beyond this
list belongs to the run.

---

## P1. Check 7 fails on a correct project

Check 7 reads: *"Every folder you opened is one the registry named. List the folders you read, and
PROJECT.md's line that named each. A folder you read that no line named fails this check."*

The scope's own root must be opened, because `PROJECT.md` is in it. No registry line names the scope
root: the registry names components. Read literally, the row fails on every correct project,
including one with nothing wrong with it.

This was written up in the check's own notes as a tool failure mode, alongside a tool wandering into
subfolders. That was wrong. It is not a risk that a badly behaved tool might trip; it is a false
positive built into the wording, and it fires on good behaviour. It has the same shape as
`structure-check` check 4's first run, which failed a correct document because `CLAUDE.md` legitimately
carried a sentence its twin did not.

**Confirmed if** the run marks check 7 fail, or reports the scope root as a folder no line named.

**Also a finding, in the other direction:** if check 7 passes, the tool exempted the scope root on
its own, which the prompt's own "do not infer, do not assume" forbids. A pass here is the prompt
being quietly repaired rather than followed, and that is worth as much as the failure.

## P2. The evidence rule lost half of itself

`structure-check` states the evidence rule in two paragraphs. One for checks asking whether something
is present: filename, line number, quoted line. One for checks asking whether something is absent:
evidenced by the search you ran and what it returned, and *"a search that returns nothing is a pass,
and passing it needs no quote."*

`registry-check` carries only the first, and then says: *"If you cannot quote it, write 'no evidence'
and mark the check fail, including when it looks like it passed."* With no absence paragraph, that
sentence applies to rows that can never produce a quote.

This is one defect, not three. It breaks three rows together:

- **Check 6**, that a component holds no `PROJECT.md`, is an absence check. Nothing can be quoted.
- **Check 5's n/a case**, no stub naming an override and none present, is an absence.
- **Check 7's pass case**, nothing read outside the declared set, is an absence.

**Confirmed if** any of those rows returns "no evidence", or fails while the document is correct, or
is padded with a quotation that does not evidence the claim.

## P3. Check 4 needs a rule, not a clause, for the contained case

Check 4 compares the parent address in a component's stubs against the address `PROJECT.md` gives for
itself, and asks for both to be quoted. For a component contained in the scope's folder those two are
different by design and always will be: the registry addresses `WP Themes` as `wp-themes/`, and the
stub points back as `../`. The scope's own address is `OneDrive, Projects/Development/WordPress-7`. No
string comparison matches those, and none should.

The rule the row wants: **compare the parent address as a location where it can be resolved, and as a
string where it cannot.** Resolving `../` from the component's folder yields the scope's folder, which
is a match; a URL or a synced-store location cannot be resolved from inside the check and is compared
as text.

The operation already exists in the prompt. Check 1 resolves a relative address to locate a component,
so the check already computes locations. That also settles the objection that a pass on this row would
be an inference the prompt forbids: resolving `../` is computing, not filling a gap from what such a
document usually contains.

**Confirmed if** the `WP Themes` row fails, or passes on reasoning the prompt does not authorise.
**Discriminating:** the `WordPress 7 Engine` stub gives the scope's synced-store address verbatim, so
a string comparison works there. P3 predicts one row failing and the other passing, for a reason that
has nothing to do with either component being wrong.

---

## What would make this file wrong

All three rows behaving correctly on a correct scope. That would mean the defects are readable in the
prompt and not reachable through it, which is worth knowing: a prompt is not code, and a tool that
repairs an ambiguous instruction may be doing the right thing. It would also mean the check's
evidence is softer than it looks, since a tool that silently fixes three instructions is a tool
exercising judgment on every other row too.

## What this run cannot settle

Whether the check catches what it was written for. That needs the negative run: a scope broken on
purpose, in a fresh session. This run is the positive half only, on a scope believed correct.

---

# Outcome

**Run:** 2026-08-29, on the `WordPress 7` scope, prompt taken verbatim from `381b200`, nothing fixed
first. Result: two failing checks across three rows. Everything above this line was written before
the run and is unedited.

**P2 confirmed, and narrower than predicted.** Check 6 returned `no evidence` and failed on both
components, on a scope where neither folder holds a `PROJECT.md` and both rows should have passed.
Exactly the predicted mechanism: an absence check under an evidence rule that only knows how to
evidence presence.

The prediction said the defect would break three rows together. It broke one. Check 5's n/a case
answered cleanly in absence terms of its own accord, and check 7's pass case did too. So the defect
is real and its blast radius was overstated: the tool absorbed two of the three and not the third.
The diagnosis was right and the scope of it was a guess dressed as an inventory.

**P3 confirmed exactly, including the discriminator.** `WP Themes` failed check 4 and `WordPress 7
Engine` passed it, which is the split the prediction named and for the reason it named: `../` against
`OneDrive, Projects/Development/WordPress-7` cannot match as text, and the Engine quotes the scope's
address verbatim. A correct component failed a row for being correct.

**P1 was wrong in outcome and right in diagnosis.** The predicted failure did not happen. Check 7
passed for the project root, and the evidence the tool gave for it was `PROJECT.md` line 45, the
scope's own local path line, offered as the line that "named" the folder. That line is not in the
registry, and the row asked for a registry line.

So the second branch fired, the one this file recorded as also being a finding: the tool repaired the
instruction rather than following it. It did not invent an exemption, which is what "do not infer"
would most obviously have forbidden; it went and found something quotable that technically named the
folder. That is the more interesting failure, because it produces a green row with real evidence
attached and nothing to alert a reader. A row a tool has to repair in order to pass is a row that was
not asking what it meant.

**Found by the run, not predicted.** The last line of the prompt asked for `Failed checks: N` and the
tool answered `3`, counting rows, where two checks had failed across three rows. With one row per
component per check the two counts diverge and the prompt never said which it wanted. Nothing in the
reading of the prompt caught this, because it only becomes visible once a table with repeated rows
exists.

**What the method is worth, on this evidence.** Three defects were found by reading a 50-line prompt
and two of them reproduced. That is worth the twenty minutes it took. It is not a substitute for the
run: the run corrected the scope of P2, overturned the outcome of P1 while confirming its diagnosis,
and found a defect reading had missed entirely.

All five defects were repaired in one pass afterwards. The repaired check has not been run.
