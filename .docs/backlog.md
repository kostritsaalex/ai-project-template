# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-08-29, after the move into WSL, the repair of the documents it made stale, and the
`0.8.0` release.

---

## Where we are

`0.9.3` is released, tagged and pushed. Working tree clean, nothing half-done.

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

**Should the check prompts be measured?** Worth having, on one instance and the project's own
precedent. The shipped-line metric covers the project scope and the component blueprints, 41 and 22.
`blueprints/checks/` is outside it and is now the fastest-growing part of the framework: `0.9.1`
added lines to a prompt while its changelog claimed a removal, `0.9.2` took them back out, and no
measurement saw either. Principle 7 is prose, and prose is exactly what got it wrong at `0.9.1`.

The cost is small and known, because the existing metric already pays it. A command in
[`release.md`](release.md) step 3 counting the lines inside each prompt block, a number in the
`README`, and a re-derivation every release. It would be a second number rather than an extension of
the first: what ships into an adopted project and what a person pastes into a session are different
things, and adding them together would measure nothing.

The real cost is the one this repository keeps rediscovering. A number in a document is a derived
fact, and a derived fact with no trigger goes stale. This one would have a trigger, `release.md`
step 3, which is the arrangement already working for the metric it would sit beside.

Not decided. It needs one sentence from the owner, and the argument against it is that two numbers
invite being summed.

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

**The naming question, closed but worth watching.** The pair stays, decided 2026-08-24. Hours later
the owner's reasoning for calling a theme folder `Assets` included "a repository is technically out
of place here because we host this on OneDrive", the storage-based reading the names invite. If a
second instance appears, reopen.

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

**Start here: is `structure-check` under-specified too?** The cheapest item with the widest reach.
Read all three prompts for rows that cannot be evidenced as written, and for rows that depend on an
earlier row without saying what happens when it fails. Both defects are now known to exist, and both
were found by reading in minutes. Anything suspicious gets a pre-registration and a run, on the
pattern in [`predictions/`](predictions/), which is three files now and works.

**Then: the moved-parent case.** `registry-check` 4 has never failed on a real defect. Move a scope,
or build a component pointing at where one used to be, and see whether the row catches it. That is
the other half of what the check claims.

**Then: ArtGlina.** Still on the pre-`0.5.0` shape, never migrated. It is the
only project with a real `Assets` component holding material rather than code, so it is where that
posture gets its second test and where the assets override may get its first real case. Expect the
`Unsorted/` folder to be the interesting one.

**Do not start with:** a full framework re-read, or a fourth run of `registry-check` against a
correct scope. It has been run five times, three of them pre-registered, and a sixth positive run
would tell nobody anything.
