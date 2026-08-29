# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-08-29, after the interview was measured rather than repaired.

---

## Where we are, 2026-08-29

**`0.11.0` is released, tagged and pushed.** Tagged on `2150f70`, after V1 to V4 passed on the
committed tree and after the released text was run twice — once at six questions, once at seven after
a placeholder check added one.

**Three items wait for the batch after it, none blocking:** the two `release.md` clauses below, and
the `<DOCUMENT_OWNER>` razor case, which may take the seventh question straight back out.

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

**Should the backlog name a version at all?** V3 has now gone silent twice from one cause: it greps
the backlog for a phrase, and the phrase gets rewritten by ordinary editing. Loosening the grep bought
one degree of freedom and no more.

The question underneath is whether that line should be checked at all. `release.md` step 0 says a
change under `.docs/` never causes a release, which makes the backlog's version line a convenience
rather than something a tag depends on. Two ways out, and they are different claims. Make V3 read the
version by pattern rather than by wording, which keeps the cross-check and stops it depending on
prose. Or drop the backlog from V3 entirely and let that line lag, on the ground that a convenience
does not need verifying and the changelog is the claim. Not now.

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
