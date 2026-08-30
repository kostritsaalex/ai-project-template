# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-08-30, after `release.md` V4's third command was repaired into a two-sided comparison.

---

## Where we are, 2026-08-30

**`release.md` V4's third command can no longer pass vacuously, and this is not a release.**
Everything in this pass is under `.docs/`, so by step 0 nothing is bumped and nothing is tagged. See
[`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md) and
[`predictions/release-v4-tracked-logs.md`](predictions/release-v4-tracked-logs.md).

**The count that decided it, taken by running the command against all twenty tags rather than by
reading the record.** It has fired **once**, at `v0.9.0`, on five names — and that one is a **true
positive**: the index named five logs the tree did not contain. It is retrospective; the command was
written into `release.md` for `0.9.2`, in `5af7bf7`, in response to that defect after it had been
found by hand. In the nine releases where it was actually in force it has never fired. This is the
opposite of V3's record and it decided the razor the opposite way.

**It could not tell a pass from a blind spot, and both were zero bytes.** `v0.1.0`–`v0.8.0` have no
`.docs/runs/README.md` at all and print nothing; `v0.9.1`–`v0.16.0` have a full index and print
nothing. Byte-identical. **And not only historical**: on a scratch copy of `HEAD` with the checksum
block's two spaces changed to one — 99 lines touched, every log present and tracked, no defect
introduced — it printed zero bytes again. One `sed` over a whitespace convention blinded it.

**Nothing else in step 7 guarantees the fact.** `git status --porcelain` sees a log present but not
added and a tracked log deleted from disk; the ignored sweep sees one present and excluded by a rule.
None of the three sees a name in the index whose file is neither on disk nor in git, which is the
`v0.9.0` defect exactly.

**The repair is a second side, not a louder warning.** The checksum block stays the key — it is the
only machine-readable form the index has — and the other side now comes from `git ls-files`. A person
can still break the key by reformatting; they can no longer break it silently, because the tree's
count does not move when the block's format does. Every outcome prints a labelled count line:
`99 named, 99 tracked` is a pass, `0 named, 0 tracked` says there was nothing to check, and
`0 named, 99 tracked` with 99 names under it is a blinded key. **`TRACKED, NOT NAMED` is declared in
scope**: a committed log the index does not name is invisible to the other two commands, and without
that direction the reformat case would report a bare count with no names.

**An unregistered control found a defect in the repair before it was committed — the fifth time in
this project's log that a check's defect surfaced that way and not by review.** The first version
resolved both sides to bare filenames. A log moved into a subfolder of `.docs/runs/`, with the block
still naming it bare, therefore **passed** — a case the old command caught, because it resolved each
name against `.docs/runs/` exactly. The repair had quietly lost coverage its predecessor had. It now
strips only the `.docs/runs/` prefix, and that arm fails naming both sides, with **equal counts and
disagreeing sets** — which is why the count line alone is not the check. **The shipped command is not
byte-identical to the pre-registered one**; they differ by that one `sed` expression, changed after
P1–P5 were run and re-run against the corrected form. The prediction was not edited.

**All five pre-registered arms held**, and the four plants were run in scratch copies of `HEAD`,
deleted after: tree as it stands `99 named, 99 tracked` and nothing else; reformatted block 100 lines
of failure; one named log removed, failing by name; one tracked log the block does not name, failing
by name. `v0.9.0` still fires with five; every tag from `v0.9.1` on passes with equal counts.

**The step grows by 7 non-blank lines, 138 to 145**, command block 3 to 5 and commentary 3 to 8.
Principle 7 asks what was removed in exchange and the answer for this pass is nothing. The argument
was put in `0020` rather than beside the command, which is the only reason it is 7 and not 12.

**Two more rows in `release.md` share the vacuous-pass class, demonstrated rather than argued, and
deliberately not acted on.** That is the next change if it is wanted.

- **V1 passes vacuously if `$PREV` is empty.** `git describe --tags --abbrev=0` failing leaves
  `git diff --name-only ..HEAD`, which git reads as `HEAD..HEAD` and which prints nothing — reported
  to the reader as *"this release changed nothing."* Confirmed by running it with `PREV=""`.
- **V2 passes vacuously if either field label is ever reworded.** On a scratch copy of `HEAD` with
  `Version:` lowercased in all six blueprint `README.md`s, `grep -rn "Blueprint Version:\|Framework
  Version:"` prints zero bytes, and V2's criterion is read against no output at all.
- **V3 and V4 are now both hardened against it**, V3 by printing `MISSING` and listing every
  blueprint, V4 by printing both counts.
- **Among the shipped checks, `registry-check.md` already names the class in its own text** — *"A
  green table can mean nothing was audited… If no row says `pass`, nothing was checked"* — but its
  remedy is a warning to the reader rather than an output that distinguishes the two. `structure-check.md`
  and `cold-start-check.md` do not share it: both require an absence row's pass to carry the search
  and its result as evidence, which is the correct pattern. Not touched; `blueprints/` is out of scope
  for this pass.

**`release.md` V3 no longer greps prose, and this is not a release.** Everything in this pass is under
`.docs/`, so by step 0 nothing is bumped and nothing is tagged. See
[`0019`](decisions/0019-a-check-compares-fields-not-prose.md) and
[`predictions/release-v3-comparison.md`](predictions/release-v3-comparison.md).

**The count that decided it, taken by running both commands against all twenty tags rather than by
reading the record.** V3 has fired **five** times, not four: retrospectively against `v0.9.1`, then on
`0.10.1`, `0.11.0`, `0.15.0` and `0.16.0`. **Zero true positives.** In all four release-time firings
the release was correct and the step was wrong. **`0.11.0` was in no record** — its grep's first hit
was line 12 of the backlog, a sentence quoting the phrase in order to explain it, naming no version.
The same shape as `0.15.0` and `0.16.0`, one release after the grep was loosened, unnoticed at the
time.

**The one occasion the guarded fact was genuinely absent is `v0.9.1`, and V3 returned nothing there —
the same output as its four false alarms.** The defect was found by opening the backlog. A step whose
signal for *"defect"* is identical to its signal for *"the sentence moved"* was carrying no
information.

**Removal was considered on its merits and half of it was carried out.** The backlog grep is deleted
outright, with the five paragraphs of commentary that existed only to warn about it. Nothing checks
the backlog's version line now and it may lag: accepted, on step 0's own ground that a `.docs/` change
never causes a release, so that line is a convenience and is not shipped to anybody.

**What survives is a comparison between two fields**, `CHANGELOG.md`'s top heading and the
`Framework Version:` in every blueprint `README.md`, computed rather than printed for reading. It
closes a real gap rather than restating V2: **V2's criterion is *"every `Framework Version` reads the
new number"* and V2's output never says what the new number is.** A release whose changelog named a
version the fields did not carry passed V1, V2 and V4 as written.

**The empty case is handled deliberately, because it is the hole this pass exists to close.** A
`CHANGELOG` with no version heading prints `MISSING` and lists every blueprint, rather than matching
everything and passing silently. A comparison that cannot tell *"all agree"* from *"nothing to
compare"* is the defect being removed, and reintroducing it in the replacement would have been the
whole pass wasted.

**One deviation from the pre-registration, recorded rather than tidied away.** The prediction was
written against a seven-line loop printing one line per blueprint; the shipped command is
`grep -L`, which lists only the blueprints that disagree. The committed prediction is **not edited** —
the five expected verdicts are about which trees pass and which fail, and those are independent of
how the row prints. Every one of them was checked against the shipped form.

**Verified both ways round, and running it changed two of the pre-registered answers.**

| Run | Pre-registered | Observed |
| --- | --- | --- |
| The tree as it stands | V3 passes | **Pass.** `CHANGELOG 0.16.0`, no blueprint listed. V1, V2, V4 beside it: V2 and V4 clean, V1 lists this pass's own four `.docs/` files, expected because this is not a release |
| Plant: changelog heading moved to `0.17.0` | V3 fails | **Fail**, all six blueprints listed |
| Plant: one blueprint `README.md` set back to `0.15.0` | V3 fails | **Fail**, exactly that one file listed |
| Unregistered extra: a top entry that is not a version | not registered | **Fail** as intended only after a repair — see below |
| `0.11.0`, `0.15.0`, `0.16.0` — three of the four trees that broke the old step | pass | **Pass** |
| `0.10.1` — the fourth | pass | **Fail**, and correctly |

**The extra control found a defect in the repair, in the form that had already been committed.** The
first shipped command took the version from the first *version-shaped* heading,
`grep -m1 -oE '^## \[[0-9.]+\]'`. Given a top entry that is not a version it silently skipped down to
the previous release's heading and compared against **that**, passing on a changelog whose top entry
names no version at all. The old V3 had the same shape bounded by `head -40`. It now takes the first
`##` heading whatever it is and extracts a version from that, so a non-version top entry yields
`MISSING` and lists every blueprint. **Found by running an unregistered control rather than by
reading the command**, which is the fourth time in this project's log that a check's defect surfaced
that way and not by review.

**`0.10.1` fails, and it is a true positive — the first in V3's life.** Not the backlog: repaired V3
never reads the backlog. It names `blueprints/setup/README.md`, which at that tag carried **no
version fields at all**. That is the hole this backlog already records — *"`blueprints/setup/` is a
blueprint folder with no version, and it just moved. `0.10.0` changed `procedure.md` and no version
records it"* — found by hand at the time and still open. The pre-registration predicted a pass and
was wrong.

**Run against all twenty tags, the repaired step dates both known version-counter holes from the tree
alone.** `v0.1.0` through `v0.8.0` fail on `blueprints/checks/README.md`, which gained its counter at
`0.9.0`; `v0.1.0` through `v0.10.2` fail on `blueprints/setup/README.md`, which gained one at
`0.11.0`. **Every tag from `v0.11.0` on passes.** Two independently-found holes, reproduced with the
right dates by a command that knows nothing about either — which is better evidence that the row
measures a real fact than any of its own runs could be.

**What is still uncaught, stated plainly.** `v0.9.1`'s actual defect was its backlog naming `0.9.0`
while its changelog named `0.9.1`. Repaired V3 does not catch it — that tag fails on `setup/README.md`,
a different defect entirely — and **nothing else in step 7 catches it either.** That is the accepted
cost of dropping the backlog, pre-registered as such before the runs, and it is not dressed up as
coverage by the `v0.9.1` failure.

**A subtraction, measured rather than asserted.** `release.md` goes from 140 non-blank lines to 138.
V3's command block is 3 lines before and 3 after; its commentary falls from 12 to 10. **The first
draft of this pass got it backwards** — the replacement was a seven-line shell loop and the file grew
by 8, while the text claimed a cut of 6. Caught by measuring before committing, which is the only
reason the claim in this paragraph is worth anything.

**Two findings from the V1/V2/V4 sweep, reported and deliberately not acted on.**

- **V1 is the same shape and says so.** It compares a file list against the changelog entry, and its
  own text reads *"This is read, not computed: the entry is prose."* Unlike old V3 it puts both sides
  in front of the reader whole, so it cannot return a confident wrong line — it can only be read
  carelessly. Whether that is repairable or is irreducibly judgement is its own question.
- **V2 is not the same shape.** It greps two fixed field labels, not a wording. Its `0.11.0` defect
  was a wrong criterion, not a drifted phrase.
- **V4 is not prose-keyed but shares the silent-failure class.** Its third command is
  `grep -oE '^[0-9a-f]{32}  \S+' .docs/runs/README.md`, keyed on a hand-maintained two-space checksum
  format. Today it matches 99 rows against 99 logs on disk. If that block is ever reformatted the grep
  matches nothing and **V4 passes vacuously**, with no output distinguishing *"all tracked"* from
  *"nothing to check"* — the same failure that made old V3 useless. A row count printed beside the
  result would close it. Not done here: separate variable. **Done, 2026-08-30, in
  [`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md); the remedy predicted here is
  the one that shipped.**

**`release.md` step 2 says "all four blueprint READMEs" and there are six.** Found by writing V3's
loop. Not corrected in this pass; it is step 2's wording, not V3's.

**Next, in order.** The stale first line of `registry-check.md` and of `checks/README.md`, deferred
four times now. Then the subtraction pass over the check prompts, three releases overdue. Then V4's
vacuous-pass hole and the V1 question above, each on its own.

---

## Where we were, earlier on 2026-08-30

**`0.16.0` is released and tagged. It is not pushed: the operator pushes it.** One exemption added to
`registry-check`'s read set: **material that exists only because of how the check's own text reached
the session is not a reading of the project** — the check's own file when its path was given instead
of its text, and a harness's attachment or spool holding the pasted prompt. See
[`0018`](decisions/0018-the-instrument-is-not-part-of-the-sample.md).

**Two instances, two ecosystems, and the second is why this is a rule.** Row 7 failed on the
operator's path-load run against ArtGlina, and then failed again when the operator ran the same
shipped text through **Codex**, naming `/home/kostritsaalex/.codex/attachments/<uuid>` — that
harness's own storage for the pasted prompt. Codex has no knowledge of this framework. One operator
loading a file the wrong way is a mistake to correct in the operator; the same row failing from a
harness this project has never seen, on an unchanged scope, is the check counting the instrument as
part of the sample.

**Rows 1 to 6 produced identical verdicts in Codex**, including *declared, not attached* and both
cascade branches. That is external evidence that the check's text reads the same way outside the
framework that produced it, and it is a finding in its own right.

**Row 7 was not touched and weakening it was refused.** Three cheaper repairs were on the table —
permitting anything opened before the prompt was read, dropping the *"without exception"* listing
requirement, making the row advisory — and each costs the row the thing it was written for. It has one
confirmed true positive, from `0.15.0`. **Exempt is not invisible:** the exemption adds a fourth class
and still requires the read to be listed and the file named.

**Where the read set is defined, established by reading rather than guessed.** Per check, three times,
audited once: `0009` states the rule but is a decision record no running session reads;
`structure-check` declares one folder's root and **has no row that audits it**; `registry-check`
declares its set and row 7 audits it; `cold-start-check` declares none. **The change went into
`registry-check.md` alone**, because in `structure-check` the same words would be a clause nothing can
execute. Available there the day it grows an audit row.

**Loading the check by its path is now supported.** The operator's original mistake was never a
mistake about the project.

**Half of this change is argued rather than measured.** Three `claude -p` arms executed the **path**
half: control unmoved, path load passing row 7 **and naming the file**, disclosed plant still failing
row 7. **Claude Code does not spool a pasted prompt to disk**, so the spool half cannot be executed in
this ecosystem — which is why the second instance had to come from another. **The operator's Codex
re-run is the only thing that can execute it, and row 7 should pass there**, listing the attachments
folder in the fourth class.

**Three debts, carried and named.** The prompt block went from 87 to 96 non-blank lines with nothing
removed — **third release in a row**, and check prompts remain the documents no metric protects. Row
5's probe clause has now shipped through two releases **without ever executing**. And the shipped-line
metric is unmoved at 40 and 22, re-measured, because it does not cover check prompts at all.

**`release.md` V3 failed again, and this time it returned a quotation of itself.** The step greps the
backlog for a fixed phrase about a release being pushed. This release is deliberately not pushed, so
the phrase is absent here — and the grep's first hit is now the sentence in the `0.15.0` section that
*describes this very drift*, quoting the phrase in order to complain about it. V3 answered its own
question with its own complaint. **Fourth occurrence**, after `v0.9.1`, `0.10.1` and `0.15.0`, and the
first where the step returns a confident wrong line rather than nothing. Both places were read by hand
instead, as the step's own commentary directs, and both name `0.16.0`. Recorded, not repaired: it is a
finding about the step, `.docs/` changes never cause a release, and V3 is queued as its own change
with its own variable.

**Next, in order.** The stale first line of `registry-check.md` and of `checks/README.md`, deferred
three times now for the same reason. Then `release.md` V3, whose grep is keyed on a phrase that has
now drifted twice. Then the shape below, applied to the other two checks before their own first true
positive arrives.

---

## Where we were, earlier on 2026-08-30

**`0.15.0` is released and tagged. It is not pushed: the operator pushes it.** One rule added to
`registry-check`, in the rows that probe the filesystem: **a probe covers one declared path and no
other, one declared path one command**, no glob or brace expansion that can reach outside the path it
was pointed at, and the parent of a declared path is not a declared path. See
[`0017`](decisions/0017-a-probe-covers-one-declared-path.md).

**Row 7 caught its own runner, and that is the whole story.** The operator re-ran `registry-check`
against the real ArtGlina scope in a fresh session with no part in building `0.14.0`. Rows 1 through
6 matched the pre-registration exactly, both components. **Row 7 failed**, naming
`/home/kostritsaalex/Projects` — the common parent of the two component paths, read because one
command tested both at once. **Its first true positive in its life.**

**Row 7 was not touched, and permitting parents of declared paths was refused.** The instrument read
correctly; the procedure it measured was wrong. Adjusting an instrument immediately after its first
correct reading is the failure this log already records once.

**The row that actually broke was row 1**, not the ones anyone would have guessed. The rows that
touch the filesystem are 1, 2, 5 and 6, read off the prompt rather than assumed: 3 quotes stubs
already in the read set, 4 resolves and compares, 7 opens nothing of its own.

**Third instance of one shape, and the shape now has a name.** A rule existed, was correct, and was
written somewhere other than where it had to be obeyed — the paste instruction inside the file it
tells you not to open, the non-attached state the interview made normal, and now the read set the
probing rows act on. **Worth applying to the other two checks before their own first true positive
arrives.**

**Two debts opened by this release, both named in the changelog rather than left to be noticed.**
The prompt block grew from 80 to 87 non-blank lines and nothing was removed in exchange, the second
release in a row that can say only that; check prompts remain the documents no metric protects.
And **row 5's new clause has never been executed** — no arm had an override file or a stub naming
one, so row 5 was `n/a` in all three runs.

**A drift in `release.md` V3, found by running it.** The step greps the backlog for
*"released, tagged and pushed"*, and this release is deliberately not pushed, so the phrase is false
here and the grep returns the `0.14.0` line instead — a wrong version, silently. That is the third
time V3 has been caught on the wording of a line a person may legitimately write differently, after
`v0.9.1` and `0.10.1`. **It is a finding about the step, not about this release**, and it is recorded
here rather than repaired, because `.docs/` changes never cause a release and this one is not being
rewritten otherwise.

**Next, in order.** The check's own file is outside its declared read set, so loading it by path
breaks the rule before the rule can be read; that is the change after this one. Then the stale first
line of `registry-check.md` and `checks/README.md`, deferred twice now for the same reason.

---

## Where we were, earlier on 2026-08-30

**`0.14.0` is released, tagged and pushed.** One condition changed in `registry-check`: a component
whose folder exists and whose two stubs are absent is **declared, not attached**, and the rows that
read a stub are `n/a` naming that outcome instead of failing.

**It was found by the adoption and by nothing else.** ArtGlina was adopted on `0.13.0`, passed
`structure-check` 14 of 14, and then took **7 failed rows from `registry-check`** — six of them
because the check knew exactly one non-attached state, the missing folder, and had none for the
state `0.13.0`'s own interview made normal. The state did not exist in the corpus the check was
built against: `registry-check` was written and validated nine times against `WordPress 7`, where
every declared component was already attached. See
[`0016`](decisions/0016-declared-is-a-second-non-attached-outcome.md).

**Row 1's cascade was not the defect and was not touched.** It is correct for a folder that is not
there, which was confirmed by re-running that case as a negative control. The gap was a missing
second condition, not a wrong first one.

**Next, and it is a separate variable with its own run.** Row 7 failed on that same ArtGlina run
because the operator loaded the check by giving its path, so the session had to open
`blueprints/checks/registry-check.md` to learn the procedure, and that file is outside the declared
read set. **The instruction telling the operator to paste the text sits inside the file, reachable
only after the rule has already been broken.** The proposed fix is to state in the read-set
definition that the check's own file is not a project file, so the instrument is not counted as part
of the sample. Deliberately not implemented in `0.14.0`. All five `0.14.0` runs pasted the text and
row 7 passed in every one, which is the diagnosis confirmed from the other side.

**Known and deferred in `0.14.0`, deliberately.** `registry-check.md`'s first line still says to run
it *"after the components it declares have been attached"*, and `checks/README.md` says the same.
That framing is now narrower than what the check does. Not repaired here: the file was not being
rewritten otherwise, so a wording pass over two files would be a passenger and a second variable.
The criterion is the one `0.13.0` used when it repaired a row while rewriting the file regardless.

**The stronger form of the new condition, not taken.** Row 1 already honours *"unless PROJECT.md says
in visible text that this component is not attached yet"*, and ArtGlina's registry carries exactly
such a sentence. Requiring it on row 2 as well would let the check tell a component never attached
from one attached and then stripped of both stubs, which `0.14.0` cannot do. It was not taken because
the blueprint only encourages that sentence rather than supplying it, so a correct new project whose
owner omitted it would fail on its first run. Worth trying if the case ever costs anything.

---

## Where we were, 2026-08-29

**`0.13.0` was released, tagged and pushed**, after the owner answered all four questions in one
message with no follow-up. **That acceptance test was his criterion and it is what five provisional
releases were waiting on.**

**The adoption is now unblocked and it is the sufficiency test for every provisional release at
once** — `0.10.0`, `0.10.1`, `0.10.2`, `0.11.0` and `0.13.0`. Five releases, one instrument. Four questions, after the per-question razor audit
`0013` never performed. `<DOCUMENT_OWNER>` cut, the boundary example corrected in three places, and
the shipped metric down to 40 and 22 — its first movement since `0.7.0`.

**Five releases are provisional and all five wait on one thing: the owner reading this question set
and accepting it.** He has cancelled every adoption until he has. Nothing is queued and the queue
does not move until he reads them.

**Three items wait for the batch after it, none blocking:** the two `release.md` clauses below, and
the `<DOCUMENT_OWNER>` razor case, which may take the seventh question straight back out.

**Every adoption is cancelled, and the owner's approval of the question set is now a step rather than
an assumption.** Decided 2026-08-29. He will not run an adoption until he has read the interview and
accepted it. The sequence is: **release, he reads the four questions, he approves, then an adoption.**

**So the provisional releases wait on his approval of the interview, not on scheduling.** Four are
provisional today — `0.10.0`, `0.10.1`, `0.10.2` and `0.11.0` — and five once the four-question
release ships. Every one of them is un-provisioned by the same single instrument, an adoption, and
that instrument is now gated on a judgement he has not yet given rather than on finding an evening
for it. **Saying "waiting for the adoption" would misdescribe it**: nothing is queued, and the queue
does not move until he reads the questions.

**This also releases the reason `blueprints/` was held.** The hold existed because a live adoption
reads the framework from disk. With no adoption in flight, that reason is gone, and the batch is
free to land whenever the owner says so. The hold is not silently lifted here — it was his to place
and it is his to lift — but the record should not carry a reason that has stopped applying.

**The interview was measured before it was repaired, and the diagnosis it was going to be repaired
under was wrong.** The framework shipped no interview text at all, so the razor that was about to be
built would have cut nothing. What shipped instead is the wording itself, as
[`0013`](decisions/0013-the-interview-ships-as-text.md) records.

**The framework shipped no interview, and that was the finding.** Before `0.11.0`: zero question
marks in `blueprints/setup/*.md`, zero in `PROJECT.md`'s comments, and Step 4 naming five topics in
one sentence. Every interview was composed fresh by whichever tool held the blueprint. The setup path
had grown four non-blank lines in four releases.

**One harness, near-identical instructions four lines apart: one interview the owner liked at `0.7`,
one he refused at `0.10.2`.** Claude Code rendered both, established by the owner on 2026-08-29, so
the tool is not the variable and the model under it is the remaining candidate. That was not
degradation, it was variance in something never specified — the same finding as an under-specified
check row, on a new surface, with the same consequence that nothing in the output distinguishes
judgement from procedure.

**Settled: the interview ships as text.** Eleven runs, three pre-registrations scored, added prose
zero in five runs of the mechanism. `blueprints/setup/interview.md` holds six questions and 203
words, against about 503 for the unspecified interview it replaces.

**What it rests on and what it does not.** It rests on fidelity measured at 1.000 and on a 60%
reduction across two scopes. **It does not rest on folder-driven variance, which this session argued
and then refuted with its own control** — a deliberately different scope moved the question block by
−3.5%, inside the band pre-registered as weakening it. The length experiment before it came out
indeterminate. Both are named in the changelog rather than left to disappear between documents.

**`0.11.0` is provisional for the same reason the three before it are.** Every run stopped at the
questions with writing disabled, so what is proven is that the six questions arrive verbatim, not
that they are enough to write a `PROJECT.md` from. **Fidelity, not sufficiency.** The ArtGlina
adoption is the single instrument that settles all four releases. Sequence: fix, release, adopt.

**The component interview is untouched**, and a project has one scope and as many components as it
has folders, so the unspecified half is the half met more often. Deliberate: all eleven runs are on
the scope interview and the component interview has never been measured once.

**What the three provisional releases still wait on is unchanged.** `0.10.0`, `0.10.1` and `0.10.2`
are released, tagged and pushed, and nothing in any of them has been run. Only an adoption exercises
them, and the adoption has been refused twice.

**Three stale boundary fragments found, two repaired.** `procedure.md` Step 4 asked for what a
project does not cover, four releases after `0.10.0` made the boundary a closed inclusion everywhere
else — repaired alone in `3363d09`. The rule at the top of the same file still said documents carry
"what the project does not do", **missed by the grep that found the first**, which searched "does not
cover" and "exclu"; repaired in `0.11.0`. `cold-start-check.md` line 133 is still on the old two-list
wording and is **open**, because the checks were out of scope. All three are recorded in the
stale-fact item below.

**`blueprints/setup/` gets a version. Decided by the owner, 2026-08-29.** It had moved twice with no
counter to record it, `0.10.0` and today. The argument for leaving it alone was that nobody adopts
anything out of that folder, and **that argument stops holding the moment the folder ships text a
person reads**, which is what the proposal in front of him would make it do. The counter starts at
the number of the release that introduces it, rather than pretending to a history it cannot
evidence, which is how `blueprints/checks/` got one in `0.9.0`. It is added at the redesign release
and recorded in that release's decision record.

Working tree clean. Nothing half-done.

---

## Where we were, 2026-08-29

**`0.10.0`, `0.10.1` and `0.10.2` are provisional, and there is no instrument to un-provision them.**
They are released, tagged and pushed, and nothing in any of them has been run: `0.10.0`'s boundary
rewrite and the cold-start question that reads it, `0.10.1`'s scoring rule for that question, and
`0.10.2`'s statement of what the razor governs. Only an adoption exercises any of it.

**The adoption did not happen, and this is the second abort.** The first was discarded because the
session had learned too much from its own survey to stay blind. The second never started: the owner
read the interview and refused it, on its length rather than on its questions.

His verdict, in his words, because it is about the whole path and not about one row: **initialization
has degraded. Consistency may have improved; the interview got much worse.** He is not going to
answer it.

So tonight's state is not a day of progress with one loose end. It is a framework whose last three
releases cannot be validated, whose adoption path has now been refused twice by the only person who
can run it, and whose owner says the part a project meets first is worse than it was four releases
ago. That much is unavoidable; shipping without saying so is not,
and the standard was set earlier today when `0.9.0` shipped a prompt no run had used. It stays
provisional until the ArtGlina adoption has been through it. Working tree clean, nothing half-done.

Three releases today. `0.8.0` adopted the second razor and cut the platform fragment. `0.9.0` added
`registry-check` and the rule in `0009` governing every check after it. `0.9.1` collapsed row 1's
cascade from three cases to one condition, which is what a component addressed off this machine
needs. The check has been run nine times, five of them pre-registered, every log committed in
[`runs/`](runs/).

**`0.9.0` was provisional for about ten minutes and is not any more.** It shipped a prompt no run had
ever used: the `n/a` rule went into the release commit itself, after the last negative run, so every
run that validated `registry-check` validated a prompt three lines different from the one that
shipped. That is the state principle 6 exists to prevent. The shipped text was then run twice against
the planted defect and every prediction held. Kept here rather than tidied away, because the failure
mode is easy to repeat: a fix written while composing the release is a fix nothing has run.

The table below is the `0.6.0` validation run, kept as the record it is. The WordPress 7 project was
reset to bare folders and re-adopted from scratch on `0.6.0`, then the Engine component was reset a
second time and re-attached against the fixed blueprints.

| | structure-check | cold-start |
| --- | --- | --- |
| Project scope | 14/14 twice before the fixes, 14/14 after | 5/5 before, 5/5 after |
| WP Themes | 14/14, two tools | 5/5 |
| WordPress 7 Engine | 14/14 before the fixes, 14/14 after | 5/5 |

Five structure checks, five cold starts, no failures anywhere. Two behavioural tests beyond them:

**The cut-off.** With the scope folder moved out from under it, the Engine reported the failure before
answering anything, found the folder at its new path, refused to open it citing the stub's own "do
not proceed on guesses", and named what it could not know.

**The task instead of questions.** Asked in one line to set up a staging deployment, it opened the
parent across the mount boundary, quoted the exclusions line, refused to build, and said that moving
the boundary is an edit to `PROJECT.md` and the owner's decision.

Proven for the first time in this run: the `Assets` posture end to end, the override path, `AGENTS.md`
as the entry stub, and the accepted risk from `0005`.

**All eleven fixes were re-validated by the second attach.** Step 2 reported the platform-code item
in the ownership language; the interview stayed at two questions; the agent noticed the parent had no
session note, explained why it correctly had none before, and added one; it referred to the symlink
line by its new name, the path note; the rewritten WordPress fragment applied with no improvisation
and the core rule stayed out of `Local rules`.

---

## Now

**Check 6 in `registry-check`: fixed and run, 2026-08-29. Done.** Three pointers from independent
experiments at one row, which is a quote behind it and no decision to make. It flipped fail to pass
between the first run and its own control on an unchanged scope; it flipped again between the two
negative runs; and it is why one negative run counted six failures and the other five. The backlog
had already recorded the same shape in `structure-check` 6, that it invites invention by asking for a
full listing when the only fact it needs is whether `PROJECT.md` is present.

**Rewritten, not deleted.** It now tests one path and reports the result, and is told not to list the
folder. Deleting it was considered and rejected: the row carries a claim no other row makes, that a
component holding a `PROJECT.md` is a project scope set up as the wrong thing, and nothing in checks
1 to 5 detects that. Check 2's listing happens to contain the fact but does not judge it, and making
check 2 judge two things is how a row becomes the kind of thing that flips. The claim is unchanged
and only the evidence narrowed, so this takes no decision record.

Validated by the two runs against the shipped text: it returned the same verdict on the same
evidence twice, a single probe of a single path, which is the first time that row has been stable
across a pair.

`structure-check` 6 has the same shape and is untouched, because it has no reproductions and widening
this silently is not the same as fixing it. It is the first thing the next session looks at.

---

Otherwise empty. The address question was settled in `0.7.0` by
[decision 0007](decisions/0007-a-component-with-no-address-says-so.md): a fourth form saying plainly
that no address exists, a check that requires one of the four, and the session note raised to a
precondition.

**Run and confirmed, 2026-08-25**, both ways round on the `WordPress 7` scope.

Positive: 14/14, with check 11 quoting both blocks and accepting two different address forms, the
relative `wp-themes/` and the Engine's `none` with its reason. Check 14 ran for the second time in
its life and passed.

Negative: the Engine's block was deliberately rewritten to `Address: ~/wordpress-7` with the local
path line deleted, reproducing the invention the second attach had produced, and the check was run
again in a fresh session. It failed check 11 and nothing else, with the right diagnosis quoted:
"block address is a bare local path". It noted separately that the block's name, posture word and
travelling rule were all present, so it isolated the defect rather than rejecting the block whole.

Worth keeping: check 12 quoted the same line and passed it, correctly. Twelve asks what form a path
is written in, eleven asks what slot it sits in. Two checks reading one line from different angles,
one failing it and one passing it, both right.

---

## Release

**A derived fact with no trigger goes stale, and it comes in two shapes.** Four instances turned up
on 2026-08-29. The shape is the same in all four: a fact that was true when written, derived from
something outside the document, with nothing that re-derives it and no event that forces a look. The
*instrument that could catch it* differs, and the two halves are not one item.

**Shape one, a scope and a component disagreeing.** The Engine's local path in the registry, stale
the moment the folder moved. The stubs still naming an override after it was deleted. Add the two
this repository already knew about: a stub pointing at a parent that has moved, and a component whose
name no longer matches its registry heading. All four are one document making a claim about another
folder, and a registry-to-disk walk finds every one of them. `registry-check` shipped in `0.9.0` and
is that walk. Its check 1 was run against a deliberately stale local path twice and caught it both
times, so this half of the class is answered by a mechanism rather than by a plan.

**Shape two, a document disagreeing with something that is not a component.** Two instances, and no
walk of the registry sees either. The three-forms wording in `architecture.md` was two documents in
this repository contradicting each other, `architecture.md` against `0007`, with no component
involved anywhere. The shipped-line metric was a document's claim about this repository's own files.
Neither is reachable from the registry, because neither is about a component.

Do not read the third check as covering this half. It does not, and "probably the same item" would be
read next time as "already covered".

**Shape two has two more instances, found 2026-08-29, and they are the first that reached
`blueprints/`.** Both were produced by one release. `0.10.0` inverted the boundary to a closed
inclusion and updated three places — `blueprints/project/PROJECT.md`, the placeholder table in
`blueprints/project/README.md`, and cold-start question 4 — and missed two more.

*The third instance.* `procedure.md` Step 4 named the topics to ask about and still said "what it
does not cover", so the framework spent four releases instructing the tool to ask for exclusions
while the blueprint it reads one step later asks for coverage. **This is the question the owner
refused in the first aborted adoption**, still in the file that produces the interview. Repaired
2026-08-29 in its own commit, `3363d09`, ahead of any redesign.

*The fourth instance, open.* `cold-start-check.md` line 133 is the project-scope reading note for
question 2, and it still says "One item from each list" and "an assistant that cannot name what is
excluded". Under a closed inclusion there is one list, not two. The *question* at line 118 was
inverted correctly and its reading note was not. **Not repaired: the checks were out of scope on
2026-08-29 by instruction, and this needs deciding beside `0.10.1`'s scoring section for the
component's question 4, which is the same question in the other prompt and did get the treatment.**
One question in two prompts, one of which was scored and one of which was left in the old language.

**What these two add to the class, and it is not more of the same.** Every earlier instance was a
workshop document going stale: `architecture.md` against `0007`, the metric against the tree. These
are two shipped files disagreeing with a third shipped file, so the defect is in what an adopting
project meets rather than in what a maintainer reads. And neither is reachable by any check: both
checks are bounded to a folder, `registry-check` walks the registry, and none of the three opens two
blueprints and compares them. **A release that changes a rule in one blueprint has nothing that finds
the other blueprints stating the old one.** That is the gap, stated in the form a future instrument
would have to answer.

**Neither produced an observed failure, and that is the argument for the reader rather than against
it.** The 2026-08-29 ArtGlina interview asked the closed-inclusion form correctly, because the tool
read Step 3's blueprint after Step 4's topic list and followed the blueprint. So the stale clause was
silent in the only run that met it. A defect that a capable tool routes around is still a defect, and
it is exactly the kind nothing will ever report.

**Shape three, an example contradicting the rule it illustrates. Named 2026-08-29, and it is not a
variant of the other two.**

`0004` cuts facts and `0008` cuts rules, and between them they say what a document may contain. **An
example is neither.** It demonstrates rather than states, it teaches more than the rule it sits
beside, and **it can contradict that rule while both read correctly on their own.** Nothing in this
framework governs one.

**The evidence is that it did.** `0.10.0` inverted the boundary. The rule said "what the project
covers, closed". The example, in the same table, changed from `hosting and deployment, mobile
applications, accounting` — three kinds of work — to `the main folder and the northwind-storefront
repository` — two places. `0011`'s own decision text carries the same folder-list example. The
changelog's `Removed` section named the exclusions form and **nobody recorded that the example had
changed category.**

Every adoption since followed the example rather than the rule, which is how the boundary question
began eliciting folder lists and colliding with the registry. **It went four releases.** The person
answering noticed it only as a feeling that two questions were duplicated, and it took a git diff of
one table cell to establish.

**The instrument is a reader, and it is the same reader shape two already needs.** An example is
checked by reading it against the rule it illustrates. No check can do it: the checks are bounded to
a folder, `registry-check` walks the registry, and none of them opens a rule and its example and
compares what each one teaches. **Nothing is being built for this.** It is named so that the next
person changing a rule looks at the example beside it, and so that the next audit has a word for the
shape.

**Shape three, third instance, and the first where the behaviour was a person's. 2026-08-30.**

Reported through the review: **the owner's draft answer to the boundary question was both of the
question's own examples, verbatim, joined by its own "or".** The question offered `restoration,
photography and selling online` or `hosting and deployment, content writing, SEO`, and the answer
came back as those, joined that way. This session did not see the answer and records the observation
as arriving rather than as its own.

The two earlier instances were an example teaching a *tool* the wrong thing: `0.10.0`'s boundary
example turning four releases of adoptions into folder lists, and the same example reaching `0011`.
**This one taught a person**, and it is worth separating because the remedies differ. A tool copying
an example is caught by reading the run. **A person copying an example produces an answer that looks
like his own**, and the only signal was that it matched the prompt too exactly.

**What follows for examples in anything a person reads.** Two full sentences joined by *or* read as a
menu. Question 2's examples are now three short fragments and no *or*, which is a change made on this
observation alone and has not been measured. Recorded as unmeasured.

**And the shortening treats the symptom, so the examples are a razor case.** A short example is copied
as readily as a long one. What the observation showed is that **an example in that question gets
answered instead of the question**, which is an argument for cutting rather than trimming. `0004` says
a document carries what cannot be seen; a question carries what the person cannot supply without it,
and these have now taught the wrong thing twice — to an assistant across four releases, and to the
person answering.

**The owner's acceptance test settles it for free**, and the reading is registered before he answers,
in [`predictions/interview-v3.md`](predictions/interview-v3.md): if he could have answered question 2
with no example present, they are cut; if he could not, they stay and the record says why, which is
more than they have now.

**The general form, and it is why this shape keeps earning its place:** an example is the part of a
document most likely to be copied and the part nothing checks. `0004` cuts facts, `0008` cuts rules,
and neither reaches an example, so the only instrument is a reader comparing it against the rule it
sits beside — and now, where the reader is a person, comparing an answer against the example that
preceded it.

**The instrument for shape two is a reader, and it is a different tool with a different cost.** Three
of the contradictions found on 2026-08-29 were caught by a session reading the whole repository and
cross-checking the documents against each other, which is how the `architecture.md` drift surfaced at
all. That instrument is expensive, needs judgment, and cannot be reduced to a table of quotable rows
the way `structure-check` is. It also does not fit inside any check prompt, because the check prompts
are bounded to a folder and this reads everything. It is worth naming rather than folding in: the
framework's answer to shape two is currently a careful read at the start of a session, and nothing
else.

One instance of shape two now has a trigger rather than an instrument. The metric is re-derived at
every release by [`release.md`](release.md), which covers that one fact and no other.

Candidates for the rest, none settled and not mutually exclusive. Date every derived fact so
staleness is visible. Name, beside each, the event that invalidates it. Or accept that shape two is
found by reading and make the read a step somewhere.

Worth keeping: re-measuring the metric at `0.8.0` found it still correct. That is luck, not evidence
that the class is harmless.

**The setup path is a prediction about a model too, and nobody ever called it one.** Second instance
of the worry recorded immediately below, and written here beside the first rather than as a finding
of its own, because it is the same worry and the framework should stop discovering it fresh.

`0008` is recorded as a claim about the reader rather than a property of a rule, and it can stop
being true with nothing in this repository changing. **`procedure.md` Step 4 is the same kind of
claim and has never been marked as one.** It ships five topics and a paragraph of style constraints
and nothing else, so what a person is actually asked is produced entirely by whoever renders them.
Five topics work exactly as well as the reader.

Established 2026-08-29: the harness was the same for both adoptions. **Claude Code ran the `0.7`
interview the owner accepted and the `0.10.2` interview he refused.** So "the tool changed" is not
the explanation. Claude Code is a harness, not a reader; the model under it can change without the
name changing, and a week passed between the two.

That leaves two candidates and they are separable with the harness held constant, which is what
[`predictions/interview-length-0.7-against-head.md`](predictions/interview-length-0.7-against-head.md)
tests. The consequence either way is already recorded there. What belongs here is the general form:
**every part of this framework that specifies a topic rather than a text is a prediction about a
model, and the framework has two of them and had labelled one.**

**The interview has a floor of four questions, and it is stated here so it can be seen being
crossed.** Written 2026-08-29, as a claim that can fail.

If question 1 and question 5 become proposals and question 7 goes with its razor, what remains is:
**what the project is, its boundary, its principles, and which folders are components.** Nothing else
in `PROJECT.md` needs a person. The placeholder map established that at twelve of twelve — six from
questions, three from proposals, two read, and the twelfth is the one under the razor.

So the interview has converged on exactly the set of things that live only in the owner's head, which
is what `0004` said a document carries in the first place. **The convergence was not designed. It
fell out of applying the razor question by question**, which is the audit `0013` skipped.

**What breaks this claim**, and either would be a finding rather than an embarrassment:

- A placeholder arriving in `PROJECT.md` that needs a human answer and is not one of these four.
- One of these four turning out to be derivable. Components is the likeliest candidate and `0005`
  currently forbids it: being a component is a decision written into the registry, never a property
  of what is on disk. If that is ever relaxed, the floor is three.

**A floor nobody stated is a floor nobody can notice being crossed.** That is the whole reason this
is written down rather than left as a count somebody could recompute.

**`<DOCUMENT_OWNER>` is a razor case, and the seventh question may come straight back out.** The
coverage gap found on 2026-08-29 had two solutions and **only one was weighed.** Add a question, or
**delete the placeholder.**

`0008` asks of any line whether an assistant does anything differently for knowing it. Applied here:
`Document Owner` names a person to ask when the document is ambiguous. That is a convenience for a
human reader rather than something that changes work. An assistant that meets an ambiguous
`PROJECT.md` reports the ambiguity and stops, with or without a name on it — which is the shape of
every line `0008` has cut so far.

If it fails, the field leaves `PROJECT.md`, the interview returns to six questions, and **the shipped
metric drops by a line.** That is the direction this framework has gone every time it has had the
choice, in `0006` and in `0008` both.

**One change in the batch is justified by the razor and not by a run, and the record says so.** The
name proposal — deriving the project's name from the folder name and offering it for correction —
**cannot be measured in a scratch run**, because nothing in a scratch scope can observe an owner
correcting it. `Artglina` against `ArtGlina`, 4 mentions to 48 in this repository, is a good argument
that the proposal must invite correction rather than settle a value. **It is not evidence that the
proposal earns its place.**

Stated separately so that six measured changes do not lend it their credibility. Its falsifier is an
adoption where the proposed name is accepted uncorrected and turns out wrong, and only an adoption
can produce it.

**The part worth recording is the process, not the answer.** The question was added without the
alternative being considered. The coverage check established that the placeholder had no source, and
the response went straight to sourcing it rather than asking whether it should exist. Both remedies
were available from the same finding and one of them was never put on the table. **A gap in a
document is not automatically an argument for filling it**, and this framework has closed two
questions by finding that the thing in question need not exist — the platform fragment in `0008`, and
where platform rules live, which vanished with it.

It gets a run or it gets a reasoned cut recorded as reasoned rather than measured. Not now, and not
as an argument.

**The second razor needs re-measuring when the model or the tool changes.** `0008` cuts rules on the
grounds that an assistant would do the same thing without them. That is a claim about the reader, not
a property of the rule, so it can stop being true without anything in this repository changing. The
first razor has no such expiry: what is visible in a folder stays visible.

Nothing re-runs it on its own, and a cost recorded only in a decision rots quietly, which is why it
is here as well.

The repeat is cheap. Both arms are built, the sandbox recipe and the task are in the plan entry
below, and the whole thing costs minutes. Re-run it when the model changes, when the tool changes,
or against a weaker model than the one that produced the result, which is the case most likely to
break it and the one never tried.

**What would count as a contradiction.** The arm with the rules produces materially different work
from the arm without: it uses the platform's data layer where the control writes a raw query, escapes
where the control does not, extends through a hook where the control edits third-party code. Any one
of those, in either direction, and the razor is wrong for that reader. What does not count is the
control naming fewer reasons, writing less commentary, or explaining itself worse. The pre-registered
reading holds on a repeat: the work decides, not the account of it.

A refutation goes into `0008`, which says where.

**What `registry-check` still cannot do.** Shipped in `0.9.0` after five runs, three
pre-registered, all logged in [`runs/`](runs/). Two gaps remain and neither is closable by wording.

Check 4, the moved-parent case, has never failed on a real defect. Its only failures were the false
ones from comparing `../` as text, since repaired. Building a scope whose components point at a
parent that has moved is the test it has not had.

Check 7 cannot be tested by any honest run. A tool that stays inside its read set passes it whether
the row is well specified or badly specified, which the first run proved by passing a broken version
of it. Nothing distinguishes a working check 7 from a decorative one.

**Are the other two checks under-specified in the same way?** The finding in
[`checks/README.md`](../blueprints/checks/README.md) came from `registry-check`, and nothing suggests
it is peculiar to it. `structure-check` has fourteen rows written before the presence-and-absence
distinction was being watched for, and its check 6 is already recorded here as inviting padding. The
work is to read all three prompts for rows that cannot be evidenced as written, which is cheap, and
then to test the suspicious ones, which is not.

**A row with no basis for a verdict will produce one anyway.** When `registry-check` failed to find
a component's folder, the five rows downstream had nothing to read and returned a verdict each. In
one run all five failed with a bare "no evidence"; in a repeat, four failed and one **passed**, on
the reasoning that a folder which does not exist contains no `PROJECT.md`. True, green, worthless.
One planted defect produced one finding and five rows of noise, which on six components would be one
and twenty-five. Repaired in `registry-check` by a rule making those rows n/a. Kept here because the
shape is general: any check whose rows depend on an earlier row needs to say what happens when the
earlier one fails, and neither of the other two checks says.

**A file can be committed and not be there.** On 2026-08-29 five run logs were copied into
`.docs/runs/`, added, committed and reported as committed. A global `*.log` ignore had excluded every
one of them, `git add -A` said nothing, the commit succeeded, and what landed was an index describing
five files the repository did not contain. Found only by listing `git ls-files` while chasing an
unrelated question.

It is the same shape as everything else in this section: a document making a claim about something
outside itself, with nothing reading the claim back. This instance is worse than the others in one
way, because the tool that could have caught it stayed silent by design. `git add` does not report
what it declined to add. The repository's `.gitignore` now negates the rule for that folder, which
fixes the instance; whether anything should read `runs/README.md` back against the folder it
describes is the open question, and it is the same open question as the metric was.

**A claim that was never established, restated until it looked like one.** The claim that
`structure-check` "passed twice" a stale registry path reached three documents: `registry-check.md`,
a pre-registration, and the `0.9.0` changelog. It is false. Those two passes were on 2026-08-25, when
the path was still correct.

**Provenance, established by `git log -S` rather than by recollection.** It first appears in
`381b200` at 17:41 on 2026-08-29, the commit that created `registry-check.md`, and it was written
there as a finished fact with nothing behind it. That is more than an hour before any reviewer
raised the hypothesis that the registry might already be stale, so the two are not a common cause and
the reviewer's speculation is not the origin. The origin was an unforced invention of the session's
own, in the file it was writing at the time.

**The reverse direction was raised and is closed.** It was suggested that the invented sentence might
have generated the reviewer's hypothesis, a reader meeting "a stale path was passed twice" forming
the natural suspicion that the registry was stale. It did not. The reviewer had not read
`registry-check.md` at that point, and the hypothesis came from the owner's own message that he had
moved the Engine, together with his question about whether to repair the path or watch the system
behave.

So there are two independent origins for one appearance of agreement. A true premise, that a folder
had moved. And an invented claim, about what `structure-check` did when it moved. They arrived from
different places, they were never checked against each other, and each made the other look
corroborated.

The speculation is closed here rather than left standing, because an unresolved "it might have gone
the other way" is the same shape as the item it sits inside: a claim nobody established, kept because
it is plausible.

So the shape is the worse of the two: not a fact restated from memory, but a claim that was never
established at any point, restated twice until repetition made it look settled. Each restatement read
as corroboration of the last.

All three were found in one pass, by reading the artefacts back in order to paste them rather than
summarising them. Nothing else could have: the claim is about a run that happened, so no check reads
it, and it was plausible enough to survive every reading not looking for it. Now that
[`runs/`](runs/) is committed, a claim about a past run is checkable, which is an argument for citing
the log whenever a document asserts what a run did.

**`release.md` V2 contradicts step 1, and the repair is one clause. Decided 2026-08-29, to be made
after the tag.** V2 says a `Blueprint Version` reads the new number *if and only if* that blueprint
appears in V1's list of changed files. But step 2 requires bumping `Framework Version` in every
blueprint `README.md`, so **every blueprint README always appears in that list**, and V2 read
literally then demands every blueprint version move — which is exactly what step 1 forbids in the
same file. Every release has silently read it as "changed substantively" instead.

The repair: a `Blueprint Version` moves if and only if that blueprint changed in some file other than
its README's version lines. It is a `.docs/` change and causes no release, so it goes in after the
tag rather than reopening a verified tree. **Recorded here now so it does not wait on somebody
noticing it again**, which is what happened for the two releases it has already been wrong for.

Found by running the step rather than by reading it, which is the second time step 7 has produced a
finding about itself.

**A second clause `release.md` earned the same day, and it goes in with the first.** Step 6 says
everything a release changes goes in one commit. `0.11.0` is two, with a pre-registration between
them: the release was committed and verified, then a placeholder check was pre-registered and run,
then its finding — a seventh interview question — was committed on top. Amending the second commit
over the first would have squashed the pre-registration and destroyed the only thing that makes a
prediction worth writing, which is that it demonstrably preceded its runs.

The clause: **a pre-registration committed between the work and the release is not squashed into
it.** Step 7 verifies `HEAD` either way, so nothing is lost by the split and the provenance is kept.
Written down so the next session does not have to reach the same conclusion under time pressure, at
the point in a release where it is most tempting to tidy.

**A document's claim about its own date is checkable and went unchecked.** On 2026-08-29 this session
dated fifteen documents, eleven run-log filenames and a changelog entry `2026-08-30`, having taken
the framing that the previous session's work was "yesterday". It was not: `v0.10.2` was tagged at
21:26 and this session began around 22:00 the same evening. Caught by two placeholder-coverage runs
which both wrote `2026-08-29` for the date and disagreed with every document around them.

Corrected before the tag. Kept here because of the shape: **the framework's own instruments found
it, and none of them was looking for it.** No check reads a date, `release.md` has no step for one,
and the finding arrived as a by-product of a run about something else.

**The origin is a one-off instruction in a prompt, and that makes it the second of a pair.** The
save-state prompt said "tomorrow starts with a measurement", the owner opened the next session the
same evening, and "tomorrow" was read literally against a clock that said otherwise.

The first was the ArtGlina interview, where roughly 120 of its 937 words are the "traces of an earlier
arrangement" paragraphs, present because that session was told to stay blind and report any trace it
met without using it. Recorded with the confounds in
[`predictions/interview-length-0.7-against-head.md`](predictions/interview-length-0.7-against-head.md).

**An instruction present in one run and absent from every other is a variable, and it belongs in the
record with the confounds rather than in a footnote.** Both instances were correct instructions.
Neither was wrong to give. Both changed an output in a way that was then read as a property of the
framework — one inflating an interview that was cited as evidence of degradation, the other dating
fifteen documents wrongly — and **both were found by measurement rather than by reading.** Nothing in
this repository records what a session was told beyond what its documents say, so a prompt-borne
variable is invisible to every instrument here by construction. Naming the pair is the whole of what
is currently done about it. The previous session made the
same error once, in
[`predictions/registry-check-negative-run.md`](predictions/registry-check-negative-run.md) line 160,
which is left as written because correcting another session's record silently is worse than leaving
it visible.

**The release procedure now has a verification step, and it was tested against its own failures.**
Added to [`release.md`](release.md) as step 6, before the tag, because a release is the moment a
document's claim about the tree is most likely to be false and it was the one moment nothing checked.
Four commands: what actually changed since the last tag, every version string, the version named in
both the changelog and here, and whether anything a document names is untracked, ignored or
uncommitted.

Run retrospectively against the two tags it was written for, it finds both. Against `v0.9.0` it names
all five logs the `runs/` index claims and the tree does not hold. Against `v0.9.1` it finds the
backlog and the changelog disagreeing about which version this is.

`set -e` would have prevented neither. Both defects were produced by a script whose assertion failed
and whose commit ran anyway, and `set -e` fixes that particular script; the step catches the class,
including the instances that arrive some other way.

**`structure-check`'s rows are audited and nothing is fixed yet.**
[`audits/structure-check-rows.md`](audits/structure-check-rows.md), read 2026-08-29, one row per
check, ranked by whether a wrong answer would be visible. Four shapes: the two `registry-check`
produced, evidence that cannot be produced as written and a row depending on an earlier one, plus
bundled verdicts and, as a candidate with one instance, a row needing knowledge the prompt neither
contains nor permits fetching.

Top of the ranking: row 10, which passes silently when a stub names an override that is gone, a
defect this project has already produced; row 14, whose `n/a` cannot distinguish a document correctly
without a path note from one wrongly without; row 4, whose false pass lets the two stubs diverge,
which is the one thing the pair exists to prevent.

Decisions come one at a time, each with its own pre-registration where it needs a run.

**No logs exist for `structure-check`.** The audit went looking for them. `.docs/runs/` holds fifteen
files, all `registry-check`, and none were ever deleted; the `0.6.0` and `0.7.0` runs predate the
folder. What survives is the backlog's own "14/14 twice before the fixes" and the prose beside it,
which is a claim about a past run checkable against nothing. Five of the fourteen rows turn on what a
tool actually produced, and for those the audit says a fresh run is needed rather than appealing to
that history.

**`.docs/runs/` holds two kinds of file and its index describes one.** Reported by the ArtGlina
session, which found `2026-08-29-artglina-adoption-judgements.md` in the folder and nothing in
`runs/README.md` accounting for it. Not a defect: the index's table and its checksum block are about
`*.log`, and a judgement log is not one. But the index reads as a description of the folder, and a
reader who trusts it will believe the folder holds only run logs.

Two ways to close it, and they are different claims. Widen the index to name every file in the
folder, which makes it true and gives it more to keep current. Or say in it that it covers run logs
only, and where judgement logs live, which keeps it narrow and honest. Not now.

**A blind adoption's blindness rests on a session declining to open a file it can see.** Declared,
not fixed.

Three surfaces, and none of them is closed by anything but instruction. `artglina-ua`'s git history
still carries the removed documents and a short run of commit subjects, one naming where the scope
lives. `.docs/runs/2026-08-29-artglina-adoption-judgements.md` sits in this repository and records
what the discarded session found: which folders held framework documents, that one held an
`ASSETS.md`, that two overrides matched byte for byte. And this backlog entry is in the same
repository as the rest.

**The second of those was avoidable and was not avoided.** The judgement log was written with the
reasoning "this log lives in the framework repository, which the replacement session must read", used
to justify keeping three commit subjects out of it, and the rest of the file was left full of the
same kind of content. The precaution was taken against one sentence and not against the document
holding it.

The framework has no notion of a place to keep notes about a project it is being applied to, and an
adoption meant to be blind needs one that the adopting session is not required to open. Whether that
is a folder outside the repository, a convention about what may be written during a live blind run,
or nothing at all, is unsettled. What is settled is that the current arrangement protects nobody: the
material is one `cat` away, in a repository the session is told to read.

**A measured mitigation stopped working, and nothing changed to make it stop. 2026-08-30.**

`new-project.md` records *"Say what a component is before asking for the first one"* as a measured
finding: without that sentence the person counts the project folder as component one and has to
correct themselves mid-block. The sentence was carried into `interview.md`'s question 4 — *"this
folder is not one, it is the project scope"* — and **the owner read it and named the project folder
as a component anyway.**

**The mitigation was present and did not work.** No wording changed, no release intervened; the same
sentence that had prevented the failure stopped preventing it. His replacement is an instruction
where ours was a statement of fact: *"Main project directory doesn't count."*

**The general shape, and it is worth more than the fix.** A finding measured once is a claim about a
reader on an occasion. It can stop being true with nothing in the repository changing — which is what
`0008` already says about rules and what nobody had said about *mitigations*. And **the only reason
this one was caught is that the person it was written for did the thing it forbids.** Nothing else
would have reported it: every check passes, the sentence is present, and the document is correct.

**The boundary's own evidence was taken on the form `0011` replaced.** Found while listing every
place that mentions the boundary. `cold-start-check.md` cites the staging-deployment run — the single
most evidenced behaviour in this repository — as *"hosting sat under what the project does not
cover"*, and `WordPress 7`'s document still carries the exclusions list it was measured on. **So the
one measurement justifying a boundary at all was taken on a prohibition-shaped line, not on a closed
inclusion.** `0011` inverted the form and inherited the evidence without re-taking it. That is an
argument for the owner's reversal that nobody has made, and it is checkable rather than rhetorical.

**The boundary reframe, tried and rejected 2026-08-30, by the answer it produced.** Cost no run and
is recorded for that reason.

The candidate put to the owner in conversation was *"what kinds of work should an assistant not start
without asking you?"* He said he would answer it faster — and then answered it: **"do not touch core
files in the platform repository."**

**That is not a project boundary.** It is the `Repository` posture's travelling rule, it already lives
in the registry block, and it was measured on 2026-08-30: with it, zero of two arms edited third-party
code; without it, one of two did. **So the reframe pulls a component-level rule up into the
project-level boundary** — the same collision as the folder lists, one layer over. A question phrased
as "what should an assistant not do" elicits rules about how to work, and the registry already owns
those.

Rejected by what it produced rather than by argument, which is the cheapest kind of rejection
available and the kind this framework should prefer.

**What his answer actually shows, and it is the finding.** His second sentence: *"otherwise there are
no boundaries, at least for ArtGlina."* That is a complete boundary and a wide one — the project
covers the pottery business, making, selling, the site, its marketing and photography, and everything
else is outside. **The line still does its job**: asked for accounting, or another client's site, an
assistant quotes it and stops.

**He was not missing an answer. He was missing what the line is for.** Told that it is the sentence an
assistant quotes when it declines work, he produced one in a breath.

**So the change is a purpose clause, not an example and not a reshape.** Question 2 said how to write
the line, what shape it takes, that folders belong to question 4, and that undecided is allowed —
**and nothing about why a person is being asked at all.** By `0004` a purpose is exactly the kind of
thing no amount of looking at the folder reveals, so it belongs in the question.

**The risk, stated rather than assumed:** it adds words to the one thing this sequence has spent three
days cutting, and the evidence is one person on one occasion.

**It was claimed to be paid for by trimming, and it was not.** Measured against `v0.12.0`, the version
he actually read: **Q2 63 → 94 words, Q4 52 → 83, the whole question block 175 → 235, up 34%.** The
trimming was real and cut the purpose clause's cost from twenty words to six; the claim that the
question ended no longer was false and is corrected wherever it was written.

**This is the closing finding happening again, in the place it warned about.** Every addition has a
reason — the undecided clause, the kinds-of-work sharpening, naming-is-not-attaching, the purpose
clause — and two came from watching him fail to answer. The sum is a third more words in the one thing
being cut. **It goes to the owner as a question rather than being fixed by another trim**, because
trimming is what produced the false claim. **The measure is his own acceptance test and
there is no other** — whether he answers question 2 from his head, in one message, without hesitating.
Nothing in a scratch run can see it.

**The exclusions question is unbounded, and the person answering it says so.** From the ArtGlina
interview: it is easier to say what a project covers than what it does not, because the complement is
endless. That is a fair complaint about the question rather than about the line it produces, and the
line has to survive whatever replaces it. The exclusions sentence is the only rule in this framework
with a measured before and after, and WordPress 7's "what falls inside" sentence earned its place as
the other half of the pair rather than as a substitute for it.

Candidate redesign, not a decision: ask for coverage first, then for the near misses only. Not
everything the project excludes, which is infinite, but the adjacent things a reasonable person would
assume are inside and are not. That is bounded, it still produces the quotable line the measurement
was about, and it is what the WordPress 7 case actually needed — its thin first answer was repaired
by naming what falls inside, and the exclusions it eventually wrote were all near misses.

Untested either way. A redesigned question is a change to the interview, which is the part of the
framework with the least evidence behind it.

**A candidate set of default principles, offered by the owner for the project blueprint.** He wants
these shipped as a default rather than the section left blank:

1. Understand the current architecture.
2. Identify the affected scope.
3. Read relevant documentation.
4. Prefer improving existing patterns over introducing new ones.
5. Keep the framework simple and internally consistent.
6. Validate architectural ideas through practical usage whenever possible.
7. Avoid speculative additions.
8. Preserve backward compatibility where practical.

**Condition on shipping any of them: each is judged against `0008` first, and the record says which
survive and why.** A rule earns a place only if an assistant would do otherwise without it.

The doubt, recorded with them: they read as principles for a software project, and this blueprint
serves scopes where software is one part of something larger. 1 and 8 look least likely to change
behaviour in a project that is mostly not code — there is no architecture to understand in a folder
of photographs, and nothing to keep backward compatible.

**The nearest precedent cuts against shipping them, and is not decisive.** `0008` removed the
platform fragment, which was pre-filled content the blueprint offered for a section an owner was
meant to write, and removed it for being what a competent assistant does anyway. A default set of
principles is the same shape in a different section. What makes it not decisive is that `0008` was
measured on a component's override and never on project principles, so whether its evidence transfers
is itself untested.

**Evidence will arrive without anyone arranging it.** They are in use on ArtGlina verbatim, which
makes that project the natural arm: one task run there with the principles present and one with the
section emptied, judged by the work. That is the same design that settled `0008`, and it is available
for the price of two runs whenever somebody wants it.

**`blueprints/setup/` is a blueprint folder with no version, and it just moved.** `0.10.0` changed
`procedure.md` and no version records it. This is the same hole `checks/` had until `0.9.0` gave it a
counter, found the same way, by running `release.md` step 7 and reading V1 against V2. The setup
folder is not a blueprint anyone adopts — nothing is copied out of it — which is the argument for
leaving it alone, and it ships prompts that change between releases, which is the argument against.
Decide it the next time that folder changes.

**Should the backlog name a version at all? Answered 2026-08-30: not by V3.** The second way out was
taken — the backlog is dropped from V3 entirely and its version line is allowed to lag, on step 0's
ground that a `.docs/` change never causes a release. See
[`0019`](decisions/0019-a-check-compares-fields-not-prose.md).

**The first way out, reading the version by pattern rather than by wording, was rejected by the
evidence that arrived after this was written.** At `0.15.0` and `0.16.0` the grep's first hit was a
sentence *about* the phrase, and both such sentences quote a version number. A pattern search over
prose would have matched them too, and returned a wrong version with more confidence than the phrase
search did. Loosening the target does not help when the document itself discusses the check.

**Every repair this week was correct, and they accumulated where nothing measures.** This is the
finding tonight, and it sits above any particular row.

Each change had a reason and most had a run behind them. Each also added justification: a clause
explaining why a row asks what it asks, a sentence naming the case a rule exists to catch, a note
recording what an earlier version got wrong. None of it was wrong and all of it was addressed to
somebody. The sum is an interview the owner will not answer.

**The shape has appeared three times now and this is its clearest instance.** The check prompts grew
outside the 41-and-22 metric, which measures what an adopted project carries and not what a person is
asked to read. `0.9.1` stated a cascade as one condition and then restated the three cases it
replaced, so a release claiming a removal shipped a longer file. And now the setup path, which no
measurement covers at all: `procedure.md` and `new-project.md` are read by an assistant, and the
questions they produce are read by an owner, and nothing counts either.

The common cause is not carelessness. It is that **justification accumulates in the place that is
never measured**, because a reason for a rule always looks like it belongs beside the rule. What the
metric protects is the document an adopted project carries. Nothing protects the document a person
has to sit through.

### Correction, 2026-08-29: the shape is right and the location was wrong

**The setup path did not grow.** Measured across `v0.7.0..HEAD`, non-blank lines:

| | v0.7.0 | now | Δ |
| --- | --- | --- | --- |
| `setup/procedure.md` | 137 | 141 | **+4** |
| `setup/new-project.md` | 65 | 65 | **0** |
| `setup/README.md` | 55 | 55 | **0** |
| `project/README.md` | 109 | 126 | +17 |
| `project/PROJECT.md` | 130 | 136 | +6 |

`new-project.md` has not been touched since `0.6.0` and `setup/README.md` not since `0.7.0`. Across
`v0.7.0..v0.10.2` exactly one file under `setup/` changed at all, by six lines. **The interview the
owner refused was produced by a file four lines longer than the file that produced the interview he
liked.** So the entry above is wrong where it names the setup path, and the paragraph naming it is
left standing above rather than rewritten, because what it got right is worth more than the error.

**Where the justification actually went.** Check prompts, `v0.7.0` to `v0.10.2`: 313 non-blank lines
to 522, **+209 and +67%**. `project/README.md`: +17, of which 23 lines are the principles default
added by `0.10.0` and `0.10.2`. Those are the two unmeasured places, and only the second is spoken
aloud to a person.

**The deeper correction, and it is the reason the diagnosis could not have been right.** The entry
ends "nothing protects the document a person has to sit through". **There is no such document.** The
framework ships no interview text: zero question marks in `blueprints/setup/*.md`, zero in
`PROJECT.md`'s comments, not one sentence anywhere addressed to the person being interviewed.
`procedure.md` Step 4 names five topics in one sentence and constrains style in a paragraph. Every
word of every interview is composed fresh by whichever tool is holding the blueprint.

A razor aimed at words addressed to a person would therefore have cut nothing, and building one was
the next thing planned. Measurement stopped it. **Recorded as the clearest case yet of this
repository's own rule: the diagnosis that survives an argument is not the one that survives a
count.**

**What the transcript adds, measured 2026-08-29.** The refused interview: 937 words, 32 non-blank
lines, 299 words of preamble and 633 of questions, seven questions from five named topics — about 90
words per question. Of those 937 words, **104 (11.1%) are lifted verbatim from `blueprints/` in runs
of six words or more, and every one of those runs comes from a comment or a README passage written to
the assistant.** "The complement of a project is endless", "it records a present boundary, not a
permanent one", "files, belonging to whichever component contains it and taking that component's
posture": design rationale, written to explain the blueprint to its reader, re-emitted to the owner
as explanation he did not ask for.

That is the mechanism, and it is not growth. **A file's justification does not have to grow to reach
the owner. It only has to be in a file the tool was told to read before composing.** `0.10.0` added
23 lines about the principles default and simultaneously told the assistant to offer them aloud,
which is the one place four releases put justification directly in the path of something spoken.

The instance to keep, because it needs no interpretation: `procedure.md` line 98 tells the assistant
"a value you have not observed — ask for it empty… an address taken from it will look plausible and
be wrong", an instruction about its own draft. The interview rendered it to the owner as *"I am
asking this blank rather than drafting it — a plausible guess about your business would read as
fact."* Nothing was wrong with either sentence. The second should never have existed.

**The posture axis is reversed by the owner, 2026-08-30, and it supersedes part of `0006`.**

**A folder declared as a component that holds code is `Repository`. Material is `Assets`.** Code in a
folder nobody declared stays what `0005` already makes it: files, taking the posture of whatever
contains them. A folder of plugins inside an assets folder is `Assets` and always was.

His reasoning, and it outruns an intuition: where the difficulty is knowing what counts as platform
core, **that is a fact about a platform** and belongs in something per-platform rather than in a
criterion every reader has to apply.

**The evidence is measured and it is on his side.** Four independent readers took `Repository` to mean
content rather than ownership — the owner in August, `gB1`, and all three arm H runs, whose stated
reasoning never touched the axis at all. And the remedy that worked reads *"a folder of your own
source code is `Assets` even when it is a git repository"*, **a sentence whose only job is to
counteract the impression the word gives.** A rule everybody reads the same way, where that reading is
coherent and useful, is usually a wrong rule rather than five wrong readers.

**What it forces, and why it reorders the work.** `0006` cut the postures to a floor plus one rule,
and that rule is `Repository`'s core rule. **On a folder of somebody's own source that rule is
empty** — no core, no updater — and `0006` and `0010` both hold that a rule ordinary work makes
vacuous teaches an assistant the document can be ignored. So under the new axis `Repository` carries
nothing, or carries something empty, and that splits two ways:

- **If the core rule earns its place**, it attaches to folders backed by a platform, which is the
  ownership axis. The new axis cannot carry it and the framework needs a third state or an override.
- **If it does not**, `Repository` carries nothing, the two postures differ by a word alone, and
  `0008` cuts a word that changes no behaviour. The postures collapse to one, or to none, and a
  registry block becomes a name and an address.

**Either way the core rule decides the shape, so it runs first**, pre-registered in
[`predictions/does-the-core-rule-earn-its-place.md`](predictions/does-the-core-rule-earn-its-place.md).
The axis change is written up as a decision record only after that reports.

**Two attempts on 2026-08-30, both failed, in opposite directions, and the rule is still untested.**
The first had a task where editing core was the genuine shortcut and an **invalid tree**: the scratch
`pluggable.php` omitted the `apply_filters` calls real WordPress has, so the filter route could not
work, and the single arm that edited core was **the only one whose work functioned**. Scoring that as
"the rule earned its place" would have credited it for suppressing the one competent piece of work in
the experiment.

The second had a valid tree and **a task with no shortcut left in it**: putting the hooks back made
the correct route strictly easier than the core edit, so no arm had reason to touch core and the
outcome that would have saved the rule was unreachable. Eight runs, four each side, and **neither
attempt has yet put the rule in front of a real temptation.**

**Third attempt, 2026-08-30: the subject moved off core and the experiment worked.** A bug in a
third-party plugin, not in core, because WordPress is hooked almost everywhere and a genuine core
temptation has to be manufactured — which is information about the platform rather than a gap in the
design. The fixture was validated by execution before the arms, and **one gate failed and was fixed
before anything ran**, which is attempt 1's failure caught by a gate instead of by an experiment.

**Result: with the rule, zero of two arms edited the plugin. Without it, one of two did**, changing
two lines in the vendor's file for correct output that the next update erases. That is D1, the
outcome the rule exists to prevent, observed.

**So the core rule survives, and `0008`'s "untested rules are not cut" no longer applies to it.** It
is tested, once, and it held. **One instance in two runs is an instance and not a frequency**, and no
rate is claimed. Twelve runs across three attempts have produced one measured instance of the rule
doing its job and zero counter-instances — thin evidence *for* a rule, which is a different thing
from evidence against one.

**So the axis change can be written up**, and it acquires the problem the pre-registration named: a
declared component holding code is `Repository` under the new axis, but only some of those folders
have a platform behind them to protect. That third state is not designed here.

A third attempt needs a task where the framework-respecting route is genuinely harder or absent in a
*realistic* tree. Three candidates are in the pre-registration and none is chosen there, because
choosing the task inside the run that needs it is how both attempts went wrong.

**The naming question closes without a rename, and that is the point of it.** The words start meaning
what every reader already thought they meant. This framework's preferred kind of answer, and cheaper
than rewriting a word in every adopted registry.

**Recipes are not designed before the core rule reports.** If it does not survive, there is nothing
for a recipe to carry and the question closes the way the platform-fragment question closed in
`0008`: by the thing not needing to exist.

**The sharpened posture rule is pulled from the batch.** It says own source is `Assets`; the new axis
says the opposite. Shipping it and reversing it next release would put in front of the owner a rule
he has already decided against, and churn is the thing he has been objecting to. It stays in
`drafts/`.

**Arm J's result stands as it is: superseded, not withdrawn.** The sharpened rule did fix the
misreading under the old axis, on three folder kinds, stable and correct across every pair. It was
overtaken by a decision rather than by a defect, and the distinction matters because the run is still
the evidence that the old wording was stably wrong.

**The posture proposal returned opposite verdicts on identical input.** Found 2026-08-29 as an
incidental result of the interview audit runs, in `2026-08-29-audit-gB1.log` and `-gB2.log`. Same
folder, same supplied answers, one framework: `gB1` proposed `Repository. Things get changed here…`
and `gB2` proposed `Assets. Live material…`.

The folder holds the project's own source and nothing a platform or framework updates wholesale, so
**`Assets` is right by the blueprint's own rule and `gB1` is wrong.**

**This is the same shape as an under-specified check row**, on the one line a component is ever told
about itself. The posture reads as settled, it is judgement, it differs between runs, and nothing in
the output distinguishes the two. It has been in the framework since `0.6.0` and has never been
tested in either direction.

Not fixed where it was found. Fixing something discovered mid-experiment is the error this repository
spent 2026-08-29 cataloguing, and this one was found by an experiment about something else. What it
needs is the treatment `registry-check`'s rows got: state what evidence settles the word, and run it
against a folder of each kind.

**A posture can go stale.** It is settled by whether platform code sits in the folder, and that can
change: a parent theme, a vendored dependency or a generated directory arrives and the word should
flip. Nothing notices.

**A component can move.** The registry carries its local path, and nothing reads that path against
the disk. `structure-check` cannot: it is forbidden from reading outside the folder it audits. The
address rule covers the parent moving, since every stub carries the parent's address; the reverse has
no rule and no check. First instance, 2026-08-29: the WordPress 7 Engine moved inside the WSL home
filesystem and two lines in the parent went stale, the registry block and the session note. The
second is the one worth noting, because an assistant told to fix the block will fix the block. The
component's own stubs needed nothing, the parent not having moved. Whether this earns a rule waits on
the second razor: "when a component moves, update its registry block" may be a line an assistant
would follow without being told. `registry-check` 1 now catches it, validated against exactly this
defect on 2026-08-29, so the open question is only whether the framework should also say something.

**Is a component a folder or a repository?** The framework has never said, and it now has a case
where the answer changes what is true.

**The evidence**, established by the owner running commands rather than by this session inferring
anything, and without any of the documents being opened. Two working copies exist,
`~/Projects/All/artglina-ua` and `~/Projects/Development/artglina-sandbox`. Both have origin
`git@github.com:kostritsaalex/artglina.com.ua.git`. In each, `git ls-files` lists `AGENTS.md`,
`CLAUDE.md` and `REPOSITORY.md` as tracked. The stubs were committed, so the clone carried the
component's identity with it, and each copy now says it is that component.

**Neither check can see this, and both are behaving correctly.** `registry-check` walks outward from
the registry to the folder at the declared local path and never reaches the second copy; the second
copy is not named by anything it reads. `structure-check` run inside that copy passes every row,
because every row is true there: the stubs name a component, carry a parent address that resolves,
and say what to do when it cannot be reached.

**Reading one: identity belongs to the address.** A component is the thing its address names, and
where that address is a repository URL, both working copies are the same component seen twice. The
sandbox is then behaving correctly and so is every check. Nothing needs building. Something needs
saying, because the framework nowhere states that a component with a repository address is the
repository rather than a directory, and a reader has no way to derive it.

**Reading two: identity belongs to the folder.** The registry declares a component by naming where it
is, so the folder at that local path is the component and the other copy is a different folder
carrying a true-looking claim about being it. Then there is a real gap: a component can be
multiplied by an ordinary `git clone`, no check sees the duplicate, and the framework has no way to
say which copy the registry meant.

**What tilts it, and why that is not enough to settle it.** `0005` says a folder that has not been
declared a component is not one, and that being a component is a decision written into the registry
rather than a property of what sits on disk. Read literally that favours reading two: the sandbox is
not in any registry, so it is not a component whatever its stubs say. But `0005` was decided about
folders nobody had cloned, and it did not face a case where the framework's own mechanism — stubs
committed to a repository — manufactures the second claimant. A rule applied outside the case it was
decided in is not the same as a rule that covers it.

**The unsaid thing may already be forced, which narrows the question.** If a repository-backed
component's stubs are not committed, a fresh clone arrives with no stubs at all, and an assistant
opening it knows nothing about the project it belongs to. That is the exact failure this framework
exists to prevent. So the stubs have to be committed, and the multiplication is a consequence of the
design rather than an accident of this project. A question whose two answers are "commit them and get
duplicates" or "do not commit them and lose the point" is not open in the direction it appears to be.

**A candidate resolution that costs no machinery.** Identity may follow the address form `0007`
already settled. A component addressed by a URL is the repository, and every working copy of it is
that component, correctly, a sandbox included. A component addressed by a relative path, or with no
address at all and only a local path, is the folder, because for those there is nothing else identity
could attach to. Under that reading nothing is broken, `0005`'s tilt applies to exactly the cases it
was decided about, and what is missing is one sentence in the project blueprint.

This framework has dissolved questions before rather than building for them, most recently in `0008`,
where asking where platform rules should live was answered by finding they need not exist. That is
the shape to try first here, and trying it is not the same as adopting it.

Not settled here. It was found during an adoption, and an adoption is the wrong place to decide what
a component is.

**It has now reached a real registry.** The Artglina project scope was adopted on 2026-08-30 and both
working copies are in it, as `Artglina UA` and `Artglina Sandbox`, carrying one address between them:
`https://github.com/kostritsaalex/artglina.com.ua`. Until now the case existed only on disk and the
question could be deferred as hypothetical. It cannot be any more: the registry is written, and it is
written under reading one, because that is the only reading that lets two blocks share an address
without one of them being wrong.

The blocks needed a sentence the blueprint does not supply. A reader meeting the same URL twice takes
it for a copy-paste error, so the registry carries visible text beside them saying the repetition is
deliberate and that the local path is what distinguishes the copies. That sentence was the owner's
instruction during the adoption, not something the blueprint asked for, and it is evidence for the
candidate resolution above: what is missing really does appear to be one sentence, and this adoption
had to invent its own version of it.

The posture was confirmed rather than inferred. Both copies take `Repository` with the core rule word
for word, the sandbox included, on the owner's statement that work there is themes, plugins and
extensions and that core is not touched there either. So the sandbox does not need an override, and
the reading that would have made it a differently-governed thing loses its most obvious practical
argument.

One correction to the evidence above. The stubs are no longer tracked in either copy: commit
`7dd69166b`, "Remove framework stubs before re-adoption", removed `AGENTS.md`, `CLAUDE.md` and
`REPOSITORY.md`, and it is present in both copies for the reason under discussion — it is one commit
in one repository. The paragraph above was true when written on 2026-08-29 and describes the state
this question was found in. What the history adds is a demonstration rather than a retraction: a
single commit changed the framework's answer in two places at once, which is the multiplication the
question is about, seen from the other direction.

Still not settled here, and for the same reason as before.

**Reaching the parent takes more than an ordinary path.** The session note names the side from which
every local path resolves, and that turns out to be necessary rather than sufficient. Run in the
Engine's folder on 2026-08-29, a session started there could not read `PROJECT.md` at all: the path
resolved, and the tool refused it for sitting outside the directory the session was started in. Both
arms of the razor experiment stopped there, quoted "do not proceed on guesses" back, and asked for
the folder to be granted. The stub did exactly its job. What no document says is that a component on
the far side of a boundary needs its parent *admitted to the session* as well as reachable on disk.
That is the failure the session note exists to prevent, one layer down from where it is written.

The framework has always assumed that a path which resolves is a file that can be read. For a
sandboxed tool those are two different things, and only the first has ever been written down. This
may be the most consequential thing found today.

It rests on one tool, and it stays in `Release` while it does. If a second tool reproduces it, it
belongs in `Now`: at that point it is a property of how assistants are run rather than a quirk of
one, and the session note is incomplete as written.

**A deleted override leaves the stubs pointing at nothing.** Found by accident while building the
control arm: `REPOSITORY.md` was removed and both stubs still carried "This folder also sets rules of
its own. Read `REPOSITORY.md` as well.", with `CLAUDE.md` still carrying the `@REPOSITORY.md` import.
The run noticed and reported the file missing. `structure-check` 10 does not catch it, because it
reads "if neither file is present, this check is n/a", so a stub pointing at an override that no
longer exists passes as not-applicable. Same family as "A component can move": the stubs hold a fact
that nothing reads back against the disk. `registry-check` 5 now reads it, in both directions, and
has passed a positive run; it has never been run against a component with the defect present.

**When a nested component earns its place.** Worth two stubs and a registry block only when it
carries something the folder would not otherwise have: a posture different from the one it inherits,
or an override of its own. `new-component.md` runs the interview either way. An override **adds** a
rule the project does not state; it does not contradict one.

**Component cold start question 3 loses its edge when an override exists.** The question exists so
the answer can only come from the parent. A component with its own rules can answer from the folder
and prove nothing. On the Engine the agent put the registry first and named both sources, so this is
a risk rather than an observed failure.

**Posture against exclusions, still uncaught, three instances.** A folder can carry a posture and be
full of material the project says it does not cover. The sharpest instance: `wp-themes`'s cold start
quoted "work here as the task requires" and "this project does not cover production sites and client
work" in the same answer, about the same folder, and saw no tension. Half of that was repaired on the
project side by naming what falls inside; the framework still has no mechanism to notice the shape.

**A check's evidence is not self-validating.** Three times in the run a passing report contained a
detail that does not exist: one tool listed `.agents`, `.codex` and `.git` in two different folders
that hold none of them, and a task run claimed `REPOSITORY.md` notes that nothing is deployed, which
it does not. None changed a verdict. Check 6 invites this by asking for a full listing when the fact
it needs is whether `PROJECT.md` is present.

---

## Recorded, not tasks

**Measured before and after, on the project boundary.** With the boundary written as "not decided
yet", two tools independently answered the boundary question by quoting a sentence about a component
not being *attached*. The boundary was written, one variable changed, and the re-run quoted it
correctly. An absent boundary is a decoy rather than a hole.

**The sentence naming what falls inside earned its place.** Added to WordPress 7 the same day, it was
picked up on the next cold start as the "inside" half of the boundary question, where the previous
answer had been thin.

**"Do not proceed on guesses" does real work.** The cut-off run is the evidence. One observation with
no control: no run was made without the line.

**The stub's stop is not too blunt.** Formerly a task. The cut-off run produced exactly the behaviour
the task was meant to produce, so it is a watch item now.

**Attachment status is visible and belongs in no document.** After the sentence about it was removed
as registry duplication, a cold start answered "listed but not attached" by looking at the disk. No
hole appeared, which is the razor working. Small tension worth watching: the cold start prompt says
to use only the files, and some questions are legitimately answered by looking.

**Runs vary on the same prompt.** The first attach of the Engine offered "use the WordPress platform
fragment" as an interview option; the second, on the same prompt and folder, did not. Recorded
because it means the absence of a behaviour in one run proves little.

**A false error is not a reason to retry a write.** An `ENOENT` came back from an edit that had in
fact applied. The agent read the file rather than trusting either the error or a retry, which is why
nothing was written twice. Verified independently: one session note, one path note, one Engine block.

**Where platform rules live, closed by not needing an answer.** The item asked for a mechanism: a
platform rule follows from a platform rather than a folder, so a fragment was copy-pasted into every
WordPress component and nothing owned it. `0008` removed the fragment, so there is nothing left to
own. Recorded because the item was deleted from `Release` rather than marked closed, and a question
that vanishes reads like a question nobody answered.

**A challenge withdrawn, recorded because the answer to it stays.** The `0.9.0` entry originally
said nothing was removed, and was challenged on the grounds that making rows 2 to 6 `n/a` removes
five verdicts. The challenge was withdrawn by the reviewer as thin: `registry-check.md` is a new file
in that release, so its internal rules need no separate itemisation under principle 7. The `Removed`
section written in answer to it stays, because it is true and useful independently of the demand that
produced it. Recorded so the record does not read as though the demand was sound.

**A shipped-line count for the check prompts, rejected 2026-08-29.** Proposed because
`blueprints/checks/` is the fastest-growing part of the framework and sits outside the 41-and-22
metric: `0.9.1` added lines to a prompt while its changelog claimed a removal, and no measurement saw
it.

Rejected on the first razor. A document carries what cannot be seen, and a line count can be computed
from the files at any moment. The existing metric earns its place by being a public commitment about
what an adopted project carries; a count of what somebody pastes into a session promises nobody
anything. A number in the `README` would also be one more derived fact needing re-derivation every
release and able to go stale between them.

The instance behind the proposal is caught more cheaply and more precisely by reading the diff of the
changed prompt against what the entry claims about it, which `release.md` step 7 now requires and
which V1 already lists the file for. And length was not what broke: two of `registry-check`'s seven
rows were under-specified, and a shorter prompt would have been just as capable of that.

**The naming question: the trigger fired, 2026-08-29. Second instance recorded.** The pair was kept
on 2026-08-24 with the condition *"If a second instance appears, reopen."*

The first instance was the owner's, hours after that decision: his reasoning for calling a theme
folder `Assets` included *"a repository is technically out of place here because we host this on
OneDrive"* — the storage-based reading the names invite.

**The second arrived on 2026-08-29 from the other kind of reader.** In
`runs/2026-08-29-audit-gB1.log` a tool saw the project's own source in a git working copy and
proposed `Repository`; its pair `-gB2.log` proposed `Assets` on identical input. `Assets` is right:
the axis is whether a platform or framework replaces the folder wholesale, and **this framework's one
adopted registry carries a folder of theme source code as `Assets`.**

So the two instances agree in direction and differ in reader. A human read `Repository` as being
about storage; a tool read it as being about source code. **Neither read it as the rule defines it**,
which is what the word was kept on the assumption they would.

**Reopened, and the order is a razor order rather than a preference.** First sharpen the rule and
re-run; only if the flip survives a clearer rule does the naming question become live. Renaming is
expensive in the way this framework hates — every registry block in every adopted project, and a word
in the shipped documents — and it is not reached for before the cheap remedy has failed.
Pre-registered as testing remedy 1 and only remedy 1, in
[`predictions/posture-rule-sharpened.md`](predictions/posture-rule-sharpened.md).

**The flip is one pair and is not a frequency.** Two runs disagreeing on identical input establishes
the defect and says nothing about how often. No rate is claimed.

**The framework's own local path had the defect check 14 exists to catch.** `PROJECT.md` gave
`~/Repositories/ai-project-template` with nothing saying what holds it up. That form resolves on the
Windows side and not inside WSL, which is why every prompt this session used
`/mnt/c/Users/kostr/Repositories/...` instead. Fixed on 2026-08-25 by naming both forms. Check 14
would not have caught it: it is `n/a` when a document says nothing about its path, so silence passes.

**A platform fragment carried a version tied to a blueprint version.** `platforms/wordpress.md`
was the first file in the framework with `For: Repository Blueprint 0.6.0` in its header, and the
worry was that fragments would multiply and nobody would be reminded to revisit them. Closed by
[decision 0008](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md), which
removed the fragment and the folder. A problem about maintaining something can be closed by not
having it.

---

## Plan for the session after this one

`0.7.0` is merged to `main`, tagged and pushed. Working tree clean. Nothing is half-done.

**Settled, 2026-08-29: the second razor.** Adopted as
[decision 0008](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md). What
follows is the record of the run that settled it, kept because the method is reusable and because
the prediction it carries has to be refutable. The item with the most leverage on the list, because
it governs every rule the framework will ever gain, and the experiment was already set up. The Engine's
`REPOSITORY.md` holds nine bullets, eight of which any competent WordPress assistant follows
unprompted. Pick a task that touches two or three of them, run it twice in fresh sessions, once with
the file present and once with it renamed away, and compare the work rather than the report. Its
answer also reshapes the platform-rules question below: if most of the fragment turns out to be
decoration, where it lives matters much less.

The task has to be one somebody would plausibly ask for. A task built to trip the bullets proves only
that they can be tripped.

**Status, 2026-08-29: set up, half-run, and not yet answered.** Two copies of the Engine, identical
but for `REPOSITORY.md` and the three stub lines that point at it: the two sentences naming it in
`AGENTS.md` and `CLAUDE.md`, and the `@REPOSITORY.md` import. That is the control the razor wants
rather than the file merely renamed away, and it is still one variable, not two. A component with no
rules of its own does not carry lines pointing at rules it does not have; a component whose override
is taken away while the stubs still name it is a broken component, and running that measures the
breakage instead of the question. The first attempt did exactly that and spent its answer reporting a
missing file.

**Confirm the arms by `diff -r`, not by construction.** Building two trees carefully is a story about
what they contain; diffing them is a measurement. Run across both copies, 219 MB and some thousands
of files each, the only output was the override and those three lines:

```text
Only in a: REPOSITORY.md
a/AGENTS.md 18,19d17   < This folder also sets rules of its own. Read `REPOSITORY.md` as well.
a/CLAUDE.md 18,21d17   < This folder also sets rules of its own. Read `REPOSITORY.md` as well.
                       < @REPOSITORY.md
```

The task: "Add a
list of the three most recently updated posts to the footer of the site, with each title linking to
the post." An ordinary request, and it meets bullets 1, 2, 3, 8 and 9 on its own merits, because the
active theme is third-party, has no `footer.php`, and the posts have to be queried and printed.

The arm with the file honoured all five. It left SellAny untouched and inserted the block through the
Block Hooks API, used `WP_Query` with `orderby => 'modified'` rather than a raw query, and escaped at
every boundary with `esc_url`, `esc_html`, `wp_kses_post` and `absint`. It also declined to invent a
theme edit and said which of its claims it had not verified.

The control ran on 2026-08-29, driven by Alex after the session's own attempts to launch it were
refused three times by a permission classifier.

**Pre-registered, before the control runs, so the reading cannot be fitted to the result.** What
counts is the work, not the explanation. Three outcomes, and only two of them are outcomes:

- The control does the same work. Eight of the nine bullets are decoration, and the file is not
  earning what it costs.
- The control differs in at least one place. That rule earned its keep, and the difference names
  which one.
- The control does the same work without naming any reason for it. This is the first outcome, not a
  third one. A framework that judges by the work does not get to award a rule credit for an
  explanation that arm never gave.

**The result: the control did the same work.** Judged by the code rather than by either summary,
across the five bullets the task touches.

*Third-party code is owned by its updater.* Both wrote a plugin and left SellAny untouched. The
control got there citing the registry entry for `WordPress 7 Engine`, and named the theme as
distributed third-party code that an update would overwrite.

*Hooks and documented extension points.* Both used the Block Hooks API through the
`hooked_block_types` filter, as `last_child` of `core/template-part`, narrowed on the context's
footer area. Both worked out independently that `block.json`'s `blockHooks` field cannot express the
area, both said so in a comment, and both cited core by file and line. The control also accepts the
part's slug when the area term is missing, which is the more robust of the two.

*Native platform functionality.* Both registered from `block.json` with a server-rendered
`render.php` and no build step. Neither added a dependency or reached for a third-party plugin.

*The data layer rather than raw queries.* Both wrote `new WP_Query` with the same nine arguments in
the same order. Diffed, the two calls differ in the variable name and in where the post count comes
from. Neither went near `$wpdb`.

*Escaping at the boundary.* The bullet neither summary settled, and the one most likely to differ. It
did not. Both escape the link with `esc_url`, the title with `wp_kses_post` behind a
`wp_strip_all_tags` emptiness fallback, and the heading with `esc_html`, and both pass
`get_block_wrapper_attributes()` through with the same phpcs-ignore justification. The only asymmetry
is on the input half: the arm with the file exposes the post count and heading as block attributes
and sanitizes the count with `absint` and a clamp, while the control hard-codes the count and has no
input to sanitize. A different surface, not a different standard.

**Under the pre-registration this is the first outcome.** These five bullets did not change the work.
It is not even the silent version the pre-registration had already refused to count as a third
outcome: the control produced the same work *and* named a reason while doing it.

**Two boundaries on that reading, and they matter more than the result.**

The rule about platform core is not in the override. It lives in the registry block, and both arms
carried it, because the registry is the parent and the parent was reachable in both runs. So this
measured an override against no override, not a framework against none. The control quoting that
registry entry back is what makes the distinction visible rather than theoretical, and it is the
single most useful thing the run produced: the layer the framework judges indispensable did fire,
and the layer under test did not.

And it is one task, one tool, one run per arm, on a file whose bullets are ordinary WordPress
practice by the entry's own description. A rule written for something an assistant would not
otherwise know remains untested. What was measured is the case the entry suspected, not the general
one.

**What this leaves.** `0008` cut the fragment and the `platforms/` folder from this repository, and
the Engine's `REPOSITORY.md` went with its three stub lines on 2026-08-29, as one operation, because
the half-done state is what ruined the first control attempt. The Engine is now shaped exactly like
the control arm, which is the one configuration in this experiment that has actually been run. It
holds two stubs, identical apart from their heading, and nothing else.

The Engine has since moved inside the WSL home filesystem. Its registry block in the WordPress 7
scope is the authority on where it now is.

**Start here, and it is a measurement rather than a repair.** Do not rewrite the interview before it
is reported. Three steps, in order.

**1. Diff what was actually asked against what the blueprint contains.** The interview that reached
the owner is not the blueprint; it is the blueprint as one tool rendered it, and the difference has
never been established. Report the split: how many lines are the blueprint's own text, how many the
tool added. Sentences of the "a plausible guess about your business would read as fact" kind may
belong to either. **Repairing a file for prose a tool wrote is the error this repository spent
2026-08-29 cataloguing**, and it is the error most available here.

**2. Check the memory of `0.7` with `git show` rather than by agreeing with it.** The owner recalls
four or five questions with answer options. If the older interview really was shorter, give the
numbers from both versions. **That difference is the cost of four releases of correct repairs, and it
is the most useful number available.** If it turns out the old interview was no shorter, the finding
above is wrong and should be marked so.

**3. Only then, the candidate rule.** One sentence: the blueprint explains to the assistant, and the
assistant asks the owner short questions. Reasoning belongs in the file the assistant reads, not in
the message the owner answers. It is a candidate and not a decision, and it is not applied before
steps 1 and 2 are reported.

**Then: ArtGlina.** Still on the pre-`0.5.0` shape, never migrated. It is the
only project with a real `Assets` component holding material rather than code, so it is where that
posture gets its second test and where the assets override may get its first real case. Expect the
`Unsorted/` folder to be the interesting one.

**Do not start with:** a full framework re-read, or a fourth run of `registry-check` against a
correct scope. It has been run five times, three of them pre-registered, and a sixth positive run
would tell nobody anything.
