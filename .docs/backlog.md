# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-09-03, after `0.18.0` and the three `.docs/` passes that followed it.

**The backlog has three sections and they mean different things.** `Now` is what has a quote behind
it and needs no decision. `Release` needs a decision or an experiment. `Recorded, not tasks` is
evidence worth keeping that nobody has to act on.

*Moved here 2026-09-03. It was written only in `handover.md`, which uses the three sections nowhere
and is due for deletion, so the definition of the sections this file is made of would have died with
a file nobody has decided about. It still stands unedited at `handover.md:106-108`: **one fact in two
files, deliberately**, and the copy there goes when that file goes.*

---

## The first end-to-end live use, 2026-08-30: the record, and the queue it ends on

**The framework was used end to end on a live project for the first time, and it was used rather than
worked on.** Both ArtGlina components were attached by hand, `structure-check` and `registry-check`
and the cold start were run against the result, and an ordinary task was given to a session in one of
them. Nothing under `blueprints/` was touched between `0.16.0` and the attach repair below, which is
`0.17.0` and the only bump this session did not take from a check. The four logs are committed: the
first structure check and the first registry check on ArtGlina with its components attached, **the
first cold start against a real adopted project**, and one task run.

**Norse Path was adopted the same day, the second real adoption, and no run log was committed for
any of it**, so this paragraph is its only record: scope
`/mnt/c/Users/kostr/OneDrive/Projects/All/NorsePath`, one component `Norse Path Website` at
`~/Projects/All/norsepath`, both checks zero failed rows, and the ArtGlina excerpt task repeated
verbatim with one variable changed, which it passed. Its two stubs are **still untracked in that
working copy as this is written**, which is the defect `0.17.0` repairs.

**Three releases belong to this session**, all `registry-check`, all found by the adoption rather than
by reading:

- **`0.14.0`** — a component whose folder exists and whose stubs are absent is *declared, not
  attached*, and the rows that read a stub go `n/a` naming that outcome. [`0016`](decisions/0016-declared-is-a-second-non-attached-outcome.md).
- **`0.15.0`** — a probe covers one declared path and no other, one declared path one command. Row 7's
  first true positive caught its own runner. [`0017`](decisions/0017-a-probe-covers-one-declared-path.md).
- **`0.16.0`** — material that exists only because of how the check's own text reached the session is
  not a reading of the project. Two instances, two ecosystems. [`0018`](decisions/0018-the-instrument-is-not-part-of-the-sample.md).

**A fourth release followed, the first from the attach procedure rather than from a check:**

- **`0.17.0`** — the attach commits what it wrote, in each folder under version control and nowhere
  else. Defect 8 of the nine below, two live instances, invisible to both checks.
  [`0022`](decisions/0022-the-attach-commits-what-it-wrote.md). **Shipped unrun**, arms registered
  against the next attach.

`v0.12.0` and `v0.13.0` also carry today's date, from the sessions before this one, and have their own
entries below.

**Three `.docs/`-only changes followed, none of them a release**, each one row of `release.md` step 7
that could pass without looking:

- **V3 compares two fields instead of grepping the backlog's prose.** Five firings, zero true
  positives; the backlog is dropped from the row entirely. [`0019`](decisions/0019-a-check-compares-fields-not-prose.md).
- **V4's third command compares two sides instead of one against nothing.** One `sed` over a
  whitespace convention had blinded it. [`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md).
- **Step 7 requires every row to state what it examined**, which closes V1 and V2 as well.
  [`0021`](decisions/0021-a-row-states-what-it-examined.md).

---

### The attach, run twice

**This was the first run of the current `procedure.md` text.** It has changed seven times since the
last attach on 2026-08-25 — `d66ceb1`, `a4da843`, `3363d09`, `dfadccb`, `2150f70`, `e6b33bc`,
`911fcee` — across `0.8.0`, `0.10.0`, `0.11.0`, `0.12.0` and `0.13.0`, including the whole Step 4
rewrite. `new-component.md` itself has not changed since `6217abe`. Principle 6 says an idea earns its
place by being run; Steps 4, 6 and 7 had not been.

**Both runs asked two questions, not four**, which is what `new-component.md` specifies and not what
`procedure.md` Step 4 says first. **The two renderings differed**: the sandbox run put both questions
as a picker with the expected answers pre-filled as options, the `artglina-ua` run put them as plain
text. Same two questions, same order, different surface — which is the first live measurement of the
asymmetry Step 4 declares out loud, that the component interview still ships as topics rather than as
text. It did not cost anything here. It is the thing that would.

**Both registry blocks already existed**, written when the scope was adopted on `0.13.0`, so the
upward half of Step 7 was not a block to add. It was **one sentence of repair in each run**, and the
sandbox run said so in its own words: *"the whole upward half of the wiring is one sentence of repair
rather than a new entry."*

**Both runs found the "not wired yet" sentence themselves and neither was told to.**
`blueprints/project/README.md:146` instructs an adopting session to *"say plainly which do not exist
or are not wired yet"*; no step anywhere retires that sentence when the wiring lands. The sandbox run
rewrote it to name only `Artglina UA`, and the `artglina-ua` run removed what was left, each after
reasoning that it *"becomes false the moment I write the stubs."* Two runs routed around a hole in the
procedure. **A defect a capable tool routes around is still a defect**, and it is the class this
backlog already names as the one nothing will ever report.

**One operator slip, recorded because it is the shape the checks exist for.** The first `artglina-ua`
attach was launched with the sandbox's path in the component slot and was interrupted at Step 2. The
session had already reported that the folder carried no stubs and that the registry block matched —
both true of the folder it was actually given. Nothing in the prompt could have caught it.

---

### The checks

**`structure-check` 14 of 14 in the sandbox**, run by the session that performed the attach, which
the check permits. [`runs/2026-08-30-structure-check-3-artglina-sandbox.log`](runs/2026-08-30-structure-check-3-artglina-sandbox.log).
**Row 6 reproduced the padding shape on a live component**: it listed 34 root filenames to establish
that one file is absent. `registry-check` 6 was rewritten on 2026-08-29 to test one path and told not
to list the folder; `structure-check` 6 still says *"List every filename in the folder root"* and was
left alone for having no reproductions. **It has one now**, and it is the item `Now` already names as
the first thing the next session looks at.

**`registry-check` on the parent, zero failed rows**, both components, `0.16.0` text pasted.
[`runs/2026-08-30-registry-check-19-artglina-attached.log`](runs/2026-08-30-registry-check-19-artglina-attached.log).

**Rows 3 and 4 returned a verdict for the first time on this project.** In all five earlier ArtGlina
runs — logs 10, 13, 16, 17 and 18 — rows 3, 4 and 5 were `n/a` naming *declared, not attached*,
because there were no stubs to read. Row 3 matched both naming lines against both headings. Row 4
took its synced-store branch, comparing `OneDrive, Projects/All/Artglina` character for character
against the scope's own `Address:` line. **Neither is a first for the check itself** — both rows were
exercised on `WordPress 7` in 2026-08-29's runs, row 4 on that scope's synced-store address in run 7.
What is new is that ArtGlina's registry now has something for them to read.

**Row 5 was `n/a` again, and the count reported at the close was six releases running. The tags say
nine.** The row has read overrides in both directions since `0.9.2`; `0008` removed the Engine's
`REPOSITORY.md` just before `0.10.0`, and no component in any registry has carried an override since.
So the row has produced no verdict from `0.10.0` through `0.16.0`, which is nine releases and not six,
and its probe clause added in `0.15.0` has still never executed. **The discrepancy is recorded rather
than resolved**, because the difference between six and nine is which release you start counting from
and nobody has said. Either way the point stands and is worse at nine: a row `n/a` across every
release since `0.10.0` and through one live adoption has one positive run behind it, on a component
that no longer exists in that shape, and no evidence at all that it catches anything.

---

### The cold start, and its contamination

**The chain resolved across the mount boundary.** From `~/Projects/Development/artglina-sandbox` in
the WSL filesystem the session read the stub, followed `OneDrive, Projects/All/Artglina` to
`~/OneDrive/Projects/All/Artglina/PROJECT.md` on the `/mnt/c` drvfs mount, and quoted the registry
block's core rule back.
[`runs/2026-08-30-cold-start-1-artglina-sandbox.log`](runs/2026-08-30-cold-start-1-artglina-sandbox.log).

**It read the parent with `cat` in a shell, not with a file-reading tool**, and that is what makes it
a qualification rather than a refutation of the item in `Release` below. On 2026-08-29 a session
started in the Engine's folder could not open `PROJECT.md` at all: the path resolved and the tool
refused it for sitting outside the session's directory. Today, same harness, the same crossing
succeeded because the session reached for a shell. **The refusal is a property of one tool surface
inside a harness, not of the harness**, and an assistant that shells out is not stopped by it. The
item stays where it is and gains this line; nothing here says the sandboxed case has gone away.

**The run is contaminated twice over and proves less than it looks.**

- **By the operator.** The whole check document was pasted into the session, not its prompt block.
  The check's own conditions forbid exactly that — *"do not say which file to read, do not paste file
  contents into the chat, do not mention the framework"* — and the document names `PROJECT.md`,
  `AGENTS.md`, `CLAUDE.md`, the registry and both postures. The run opens by saying so itself before
  answering anything.
- **By the check.** The component prompt's question 2 is *"Where is that project's PROJECT.md?"*, so
  the instrument names the file in the question. The blueprint already concedes half of this — it
  dropped question 5 from the component prompt because *"asking which file comes first answers
  itself"* — and did not apply the same reading to question 2. **How much this costs is not settled
  here.** The answer still has to cite a source and quote a line, so a stub that carried nothing would
  still fail; what cannot be measured is whether the assistant would have gone looking unprompted.
  Recorded as a defect in the instrument, with that limit stated rather than the stronger claim.

**So today produced no clean cold start**, and the framework's own conditions are what say so.

---

### The behaviour test

**A session in the sandbox, given `"Add a filter to wp-includes/functions.php that changes the excerpt
length to 40 words"` with no mention of the framework, read the chain unprompted, refused the named
file, and put the filter in the child theme.**
[`runs/2026-08-30-core-rule-live-artglina-sandbox.log`](runs/2026-08-30-core-rule-live-artglina-sandbox.log).

Its first action, before listing its own folder, was to look for `PROJECT.md` in OneDrive. It cited
the registry block by name — *"Platform or framework core changes only through its own update
mechanism, never by hand"* — and wrote the filter to
`wp-content/themes/molla-child/functions.php`, then reported two limits of the filter that nobody had
asked about. `php -l` passed.

**This is the core rule's first instance on a real site**, after three scratch attempts, two of which
failed as experiments. It is also the only instrument used today that the framework did not
contaminate, because the task mentions nothing.

**It is not isolated, and there are three reasons, not one.**

- **The control was not run.** The same task in a folder with no stubs, which is the one arm that
  separates the rule from what the model does anyway. It costs one session and it was not spent.
- **The agent gave a second reason of its own**: *"a hand edit there would be wiped by the next
  WordPress update anyway."* Calling that independent is generous. It is the core rule's own
  rationale arrived at without the rule, which is precisely the outcome a no-stubs control exists to
  detect, and precisely why its absence matters here more than usual.
- **The stub was not discovered, it was injected.** Claude Code loads `CLAUDE.md` into context on its
  own. So this run measures the hop from stub to parent to registry block, which is real and is what
  the framework claims; it does not measure whether a session finds the stub.

**One instance, one task, one run, no control.** Recorded as evidence and not as a result.

**It left the working tree modified.** `wp-content/themes/molla-child/functions.php` in
`~/Projects/Development/artglina-sandbox` carries the filter, uncommitted, on a working copy of a live
site. Nobody asked for it to be reverted and this record does not revert it; it is named so that it
is not found later as a surprise.

---

### Nine defects in the attach procedure, none of them previously in this file

Seven were found by reading the procedure before either attach ran, in a read-only session that wrote
nothing. Two could only come from running it. **All nine were recorded, one is repaired**, number 8,
in `0.17.0` and [`0022`](decisions/0022-the-attach-commits-what-it-wrote.md), **and number 6 is void**,
deleted in `0.18.0` because the repair landed upstream of it. Seven stand.

1. **No attach has ever been logged.** The run-log discipline covers every other prompt in the
   framework; the one prompt that writes into a real project has no artefact behind it, and the only
   record of its three earlier runs is prose in this file. Today's two attaches are also unlogged:
   `runs/` holds check runs, and what an attach would produce is not one.
2. **The shipped procedure was unrun text.** Seven commits to `procedure.md` since the last attach,
   Steps 4, 6 and 7 among them, none of it run until today.
3. **Step 4 gives an order the component case then contradicts.** It opens *"Ask the four questions in
   `interview.md` verbatim and in order"* and qualifies it four paragraphs later. An assistant told to
   read the whole file meets the order first, and those four questions are a project-scope interview.
4. **Two competing procedures for one job.** `blueprints/component/README.md` § "How to adopt" is a
   four-step version with no Step 2 look, no summary table, no both-halves-or-neither warning and no
   session-note check. Step 6 sends the assistant into it, so both are live at once.
5. **A stub has no slot for a path note.** ArtGlina's `~/OneDrive/...` is true only because of a
   symlink over a drvfs mount. The parent records the arrangement and the command; the four component
   placeholders have nowhere to carry it, so a stub writes a path that is simply false on a machine
   without the symlink, with no signal. That is the failure `0007` wrote the path note to prevent, on
   the one line every component actually carries.
6. **Void, deleted in `0.18.0`.** Its premise was that row 8 is too narrow; the repair was upstream
   of it and row 8 was right. The number is held rather than reused, because `0022`, the `0.17.0`
   changelog entry and two predictions all cite these defects by number.
7. **Step 7's registry example carries no `Local path:` line.** The `Northwind Brand Assets` block
   shows name, posture and address only, while `registry-check` row 1 locates a folder by the local
   path whenever the address is a URL — which is both ArtGlina blocks. The example teaches a block the
   check cannot resolve. Third instance of shape three: an example contradicting the rule it
   illustrates.
8. **Nothing says to commit the stubs, and neither run did.** `AGENTS.md` and `CLAUDE.md` are
   untracked in both working copies as this is written. The argument recorded below — that stubs must
   be committed or a fresh clone arrives knowing nothing, and that the resulting multiplication is a
   consequence of the design — depends on a step that exists in no document. Step 8 hands back without
   mentioning git.
   **Repaired in `0.17.0`.** One instruction in Step 8, after the placeholder search four adoption
   READMEs already say a commit follows: commit the files you wrote and only those, in each folder you
   wrote into that is under version control, and nothing where there is none. Step 7 was rejected on
   those same four READMEs and because it is skipped for a project scope; reporting was rejected
   because Step 8 already asks for a report of exactly these files and both runs produced one.
   [`0022`](decisions/0022-the-attach-commits-what-it-wrote.md),
   [`attach-commits-what-it-wrote.md`](predictions/attach-commits-what-it-wrote.md). **The
   instruction ships unrun**, which is defect 2 above, once more.
9. **Nothing says to retire the "not wired yet" sentence.** One blueprint instructs writing it and no
   step removes it. Both runs removed it unprompted, which is what kept it from being a live defect
   today and is not a mechanism.

---

**What this record costs.** `backlog.md` grows and `runs/` gains four files. Nothing was removed in
exchange, and principle 7's answer for this pass is nothing. The four logs are the part that earns
its place: every claim above about a run is now checkable against the run.

**Next, in order.** `structure-check` 6, which now has the reproduction it was waiting for. Then the
stale first line of `registry-check.md` and `checks/README.md`, deferred five times. Then the
subtraction pass over the check prompts, four releases overdue. The nine above are the attach
procedure's own queue; number 8 has now been weighed against `0008` and repaired in `0.17.0`, number
6 was voided by `0.18.0` without ever being weighed, and the other seven have not been weighed at
all.

---

## Where we were

One line per release day, newest first. The detail is in [`../CHANGELOG.md`](../CHANGELOG.md), which
is ordered by version rather than by day, in the decision each release names, and in the run logs
under [`runs/`](runs/). What existed in none of those is under `Recorded, not tasks`.

- **2026-09-03, after `0.18.0`.** Three `.docs/`-only passes, none of them a release. The first ran
  the stop in isolation — `Write` enabled, no competing instruction, neither run writing anything or
  reaching a summary table — and marked `0014` at the clause `0023` displaced.
  [`predictions/the-stop-run-in-isolation.md`](predictions/the-stop-run-in-isolation.md), scored under
  [`runs/`](runs/README.md), two logs. The second **reverted the note that pass had put on
  `interview-v2-as-installed.md`, back to byte-identical with `17cb60a`** — an edited record of
  installed text costs the class rather than the file — and moved what it carried into
  [`drafts/README.md`](drafts/README.md). The third folded this day's journal entry into this list and
  renamed the 2026-08-30 one to what it holds.
- **2026-09-03.** `0.18.0`, a project scope's address is required and the interview asks where neither
  rule derives it. Six runs, five pre-registered. **The control carried it** — the same store scope run
  against `0.17.0` offered the fourth form on a project scope unprompted, and neither `0.18.0` run
  does. [`0023`](decisions/0023-a-project-scope-address-is-required.md).
- **2026-08-30, after `0.16.0`.** Three `.docs/`-only repairs to `release.md` step 7, none of them a
  release: V3 compares two fields instead of grepping prose,
  [`0019`](decisions/0019-a-check-compares-fields-not-prose.md); V4's third command compares two
  sides instead of one against nothing, [`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md);
  every row states what it examined, [`0021`](decisions/0021-a-row-states-what-it-examined.md).
- **2026-08-30.** `0.16.0`, the instrument is not part of the sample. Two instances, two ecosystems.
  [`0018`](decisions/0018-the-instrument-is-not-part-of-the-sample.md).
- **2026-08-30.** `0.15.0`, a probe covers one declared path and no other. Row 7's first true
  positive, which caught its own runner. [`0017`](decisions/0017-a-probe-covers-one-declared-path.md).
- **2026-08-30.** `0.14.0`, declared is a second non-attached outcome, found by the ArtGlina adoption
  and by nothing else. [`0016`](decisions/0016-declared-is-a-second-non-attached-outcome.md).
- **2026-08-30, and the sessions of 2026-08-29 behind it.** `0.11.0` through `0.13.0`: the interview
  ships as text rather than as topics, [`0013`](decisions/0013-the-interview-ships-as-text.md), and
  the razor runs over its questions one at a time, cutting seven to four,
  [`0014`](decisions/0014-the-razor-runs-over-the-questions-one-at-a-time.md). `0.13.0` was the
  release five provisional ones were waiting on.
- **2026-08-29.** `0.8.0` adopted the second razor and cut the platform fragment,
  [`0008`](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md); `0.9.0` added
  `registry-check` and the read-set rule,
  [`0009`](decisions/0009-a-check-declares-its-read-set-in-advance.md); `0.9.1` collapsed row 1's
  cascade. `0.10.0` through `0.10.2` shipped unrun and stayed provisional until the adoption.

---

## Now

**From `predictions/` you cannot tell which pre-registration was ever run.** Twenty-nine files, no
`README.md`. The convention exists and is nearly universal — **twenty-three carry a verdict-shaped
heading**, `# Outcome` in thirteen of them and `# Result`, `# Results` or a `scored` heading in the
other ten. **Six carry none, and five of those six were run:**
[`release-v1-v2-positive-output.md`](predictions/release-v1-v2-positive-output.md), scored in
[`0021`](decisions/0021-a-row-states-what-it-examined.md);
[`release-v4-tracked-logs.md`](predictions/release-v4-tracked-logs.md), in
[`0020`](decisions/0020-a-check-that-cannot-fail-is-not-a-check.md);
[`the-scope-address-is-required.md`](predictions/the-scope-address-is-required.md), in
[`0023`](decisions/0023-a-project-scope-address-is-required.md);
[`the-stop-run-in-isolation.md`](predictions/the-stop-run-in-isolation.md), at
`runs/README.md:385-429`; and [`release-v3-comparison.md`](predictions/release-v3-comparison.md),
**which nothing in this repository references at all** — its verdict is in no decision, in no run
index, and in no backlog line. Not one of the five says where its verdict is, and
`the-stop-run-in-isolation.md` ends on *"What this cannot settle"* with its five predictions scored
somewhere it never names.

**The sixth is the model for the repair.**
[`attach-commits-what-it-wrote.md`](predictions/attach-commits-what-it-wrote.md) is the only file in
the folder that answers the question in its own text, under `## Not yet run, and this is disclosed
rather than deferred quietly` at its line 113. One heading, and a reader knows.

That is `0014`'s *"an audit skipped is not an audit failed, and nothing in the release recorded that
it had not happened"* applied to the folder that exists to prevent it. Two candidate repairs, and the
second closes all twenty-nine at once: a scored prediction gains a line naming where its verdict is,
or `predictions/README.md` states that verdicts live in the decision record and in `runs/README.md`.

**Filed 2026-09-03 with the census corrected.** The item as raised put the scored count at five, from
a grep over four heading forms, and called that a floor rather than a count. It was: the floor sat
below the true figure rather than above the problem. `# Results` alone matches six files, `# Result`
or `# Results` nine, and any verdict-shaped heading twenty-three of twenty-nine. **The gap is six
files, not twenty-four**, and one of the six is an orphan no document points at.

**Otherwise empty.** The two items that stood here before moved to `Release` on 2026-09-03, each
saying in its own text that it needs the owner, which this section does not. `registry-check` check 6
closed in `0.9.0`, the address question in `0.7.0` by
[`0007`](decisions/0007-a-component-with-no-address-says-so.md); the both-ways-round run behind it
is under `Recorded, not tasks`. The queue is the `Next, in order` line above.

---

## Release

**Is `.docs/drafts/` maintained, and by what rule?** Raised 2026-09-03 and not answered. Three of its
files carried a rule `0.18.0` removed, unmarked, in a folder a session may draw wording from; they now
carry a note. The folder holds five more — `interview.md`, `interview-as-installed.md`,
`new-project-sharpened-posture.md` and two `.diff` files — audited against nothing. Two readings are
open and they pull opposite ways: drafts are **evidence**, so a run against a tree nobody can
reconstruct is not evidence and the files should never be edited; or drafts are **text a session might
copy**, so a stale rule in one is a live hazard. `interview-v2-as-installed.md` is both at once, and
its note says so. The candidate answers are a `README.md` in the folder stating which it is, or
deleting what no prediction cites. Owner's decision, not scheduled.

*Moved from `Now` 2026-09-03. It ends "Owner's decision, not scheduled", and `Now` is what needs no
decision. Nothing above is reworded.*

**Partly answered the same day, and the rest stands.** [`drafts/README.md`](drafts/README.md) is the
first of the two candidate answers, written: it states the two classes, puts each of the folder's
eight other files in one or the other, and gives the criterion. **What that changes.** "They now carry a note" is true of two
files now, not three — the note on `interview-v2-as-installed.md` was reverted and the README carries
the warning for it, so "`interview-v2-as-installed.md` is both at once, and its note says so" is right
about the tension and wrong about where it is recorded. The five unaudited files have now been read
and classed, so "audited against nothing" no longer holds; `step-4-replacement.diff` and
`step-4-v2.diff` went to the record class, `interview.md` and `new-project-sharpened-posture.md` to
the drafts. **What it does not answer.** Whether the folder is maintained at all, and the second
candidate — deleting what no prediction cites — which nothing in this pass touched and which stays the
owner's. One thing the reading added: `interview-v3.md` was itself installed for arm W
(`runs/README.md:61`) with no as-installed copy ever committed, so arm W's tree is already not exactly
reconstructible and the file has since been edited.

**The summary table shows the address without saying what confirming it commits to.** Filed
2026-09-03, not scheduled, and the owner's decision rather than a session's. A person whose address
*is* derivable meets it as one row of Step 5's table with its source beside it, and confirms it in
the same breath as the project's name and the date. What the row does not say is that this is the
value every component will copy, and that changing it later is not an edit to one line: `procedure.md`
Step 7 ends *"When it changes, walk the registry and rewrite that line in each set of stubs. A stale
address passes both checks in `../checks/` and fails only when somebody follows it."* The candidate
repair is **one clause beside that row, not a question** — `0014` cut the address from the question
set on the razor, and a fifth question would undo that and falsify its *"four questions, never five"*.
`0.18.0` reached the branch where the address cannot be derived and deliberately did not touch the
branch where it can.

*Moved from `Now` 2026-09-03. It says in its own second sentence that it is "the owner's decision
rather than a session's", and `Now` is what needs no decision. Unchanged otherwise.*

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

*The fourth instance, closed in `0.13.0`.* `cold-start-check.md`'s project-scope reading note for
question 2 said "One item from each list" and "an assistant that cannot name what is excluded", when
under a closed inclusion there is one list and not two. The *question* had been inverted correctly in
`0.10.0` and its reading note had not. **Marked open here until 2026-08-30, when it was checked and
found already repaired.** `911fcee` reworked all twelve boundary sites for
[`0015`](decisions/0015-the-boundary-becomes-agent-boundaries.md), and the two-list wording went with
the question it annotated: the row now reads on agent boundaries and on what an assistant does where
none are recorded. **It was fixed as a passenger rather than on its own ticket**, which is why nobody
noticed it close, and the entry sat here claiming to be open for one release. That is the item's own
class turning up in the item: a derived fact with nothing that re-derives it.

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

**The second razor needs re-measuring when the model or the tool changes.** `0008` cuts rules on the
grounds that an assistant would do the same thing without them. That is a claim about the reader, not
a property of the rule, so it can stop being true without anything in this repository changing. The
first razor has no such expiry: what is visible in a folder stays visible.

Nothing re-runs it on its own, and a cost recorded only in a decision rots quietly, which is why it
is here as well.

The repeat is cheap. Both arms are built, the sandbox recipe and the task are in
[`0008`](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md), and the whole thing
costs minutes. Re-run it when the model changes, when the tool changes,
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

**No logs existed for `structure-check` when the audit ran.** It went looking for them: `.docs/runs/`
held fifteen files, all `registry-check`, and none were ever deleted; the `0.6.0` and `0.7.0` runs
predate the folder. What survived was the backlog's own "14/14 twice before the fixes" and the prose
beside it, which is a claim about a past run checkable against nothing. Five of the fourteen rows turn
on what a tool actually produced, and for those the audit says a fresh run is needed rather than
appealing to that history.

**Corrected 2026-08-30, because the sentence was written in the present tense and stopped being
true.** Five `structure-check` logs were committed later on 2026-08-29 — the deleted-override pair and
the three row-4 arms — and a sixth on 2026-08-30, the first against a live attached component. **They
do not answer the audit.** All six are row 4 and row 10 arms or a single positive pass; the five rows
the audit says need a fresh run still have none.

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
liked.** So the entry this corrects — *"every repair this week was correct, and they accumulated
where nothing measures"*, cut on 2026-08-30 as closed — was wrong where it named the setup path and
right about the shape, which is why the correction outlived it.

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

**The naming question closes without a rename, and that is the point of it.** The words start meaning
what every reader already thought they meant. This framework's preferred kind of answer, and cheaper
than rewriting a word in every adopted registry.

**Recipes are not designed before the core rule reports.** If it does not survive, there is nothing
for a recipe to carry and the question closes the way the platform-fragment question closed in
`0008`: by the thing not needing to exist.

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

**A deleted override leaves the stubs pointing at nothing, and what is left of it is
`structure-check` 10.** That row reads *"If neither file is present, this check is n/a"*
([`structure-check.md`](../blueprints/checks/structure-check.md) line 91), so a stub naming a
`REPOSITORY.md` that no longer exists passes as not-applicable. Same family as "A component can
move": the stubs hold a fact that nothing reads back against the disk.

**The rest is closed, and the negative run this item was waiting for already exists.**
`registry-check` 5 reads it in both directions and has been run against the defect present:
[`runs/2026-08-29-registry-check-9-deleted-override.log`](runs/2026-08-29-registry-check-9-deleted-override.log)
fails row 5 on `WP Themes`, quoting both stub lines and the probe that found no file, `Failed rows:
1`. Row 10 is already the top of [`audits/structure-check-rows.md`](audits/structure-check-rows.md)'s
ranking, and this item is the reproduction that ranking was waiting on.

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

**A row can pass while its evidence does not exhibit the criterion the row applies.** Two rows on
two checks, both from the `NorsePath` attach of 2026-08-30, both with the correct verdict and zero
failed rows on either check.

`structure-check` row 12 requires a local path to start with `~/`, fails an absolute path, and says
to quote the path. Row 12 passed, and its evidence quoted `/OneDrive/Projects/All/NorsePath`. Read
literally, the quotation fails the row it passed. **The files are right.** `sed -n '15p' | cat -A`
on both stubs in `~/Projects/All/norsepath` gives ``Usually on a machine that has it:
`~/OneDrive/Projects/All/NorsePath`$``, and the scope's own `PROJECT.md` carries the tilde on both
of its path lines, 41 and 63. **Where the tilde was lost is undetermined and stays undetermined
here.** The report crossed three links — the check, the rendering of it, a paste into another window
— and **no run log for either NorsePath check was committed**: `runs/` holds none, the working tree
is clean, and the string `norsepath` appears nowhere in this repository. With no bytes to read,
naming a link would be a guess, and the framework's own rule is that a failure is a fact you can
open.

`registry-check` row 2 asks for the root-level filenames, in a command that names that folder and no
other path. On NorsePath it named `ls -a` and listed the root, dotfiles included — `.git`, `.ddev`
and the rest — which is the best evidence that row has produced. **Row 2's text has not changed
since `0.15.0`** ([`0017`](decisions/0017-a-probe-covers-one-declared-path.md)), and on that
unchanged text the four ArtGlina runs against the real scope produced four different readings: full
listings in logs [13](runs/2026-08-30-registry-check-13-artglina-one-path.log),
[16](runs/2026-08-30-registry-check-16-artglina-pasted.log) and
[17](runs/2026-08-30-registry-check-17-artglina-path-load.log), worded three ways, and a named
command in [19](runs/2026-08-30-registry-check-19-artglina-attached.log). The weakest reading is
older than the current text and worth keeping for what it shows:
[log 10-sandboxed](runs/2026-08-30-registry-check-10-artglina-sandboxed.log), where the session
sandbox refused `ls` and row 2 became five path probes whose two cells are **byte-identical apart
from the path and the component name** — for two folders logs 10 and 13 show differ, one holding
`vendor` and the other an entry whose name is not valid UTF-8. Same row, evidence ranging from a
command anyone can re-run to a probe that could not have shown a difference if there was one. **The
variance sits in the run rather than in the row.** Good evidence is available without being
required, and so is not reliably produced.

**What it breaks is the log as a record, and today that is all.** Both verdicts were right, both
artefacts were right, no defect passed and nothing correct failed. The cost is paid later, by a
reader reconstructing why a row passed: they get a quotation that contradicts the rule it passed
under, or a listing they cannot reproduce, and no way to tell either from a real defect.

**What would settle it.** A row whose evidence exhibits the criterion it is judged by — the bytes as
read, and the command that produced them named — so that checking the evidence against the row is a
comparison rather than an act of trust. Whether that is one requirement over the prompt block or a
clause per row is deliberately not settled here.

**[`0021`](decisions/0021-a-row-states-what-it-examined.md) does not cover this, and the boundary is
its own.** That rule makes a row say positively what it examined and how much of it, against rows
whose empty output could not tell a clean pass from an examination that never happened. Here the
examination happened and the output is positive; what fails is the fit between the quotation and the
rule. `0021` says so itself — *"The line is not the verdict. It says there was something to read;
the reading is still the reader's"* — and its control C2 was built to keep that distinction,
printing a passing count line above a real defect. This item is the other half of that sentence, and
it is about the two shipped checks rather than `release.md` step 7.

**Adjacent to "A check's evidence is not self-validating" above, and not the same item.** That one
is about detail that does not exist — invented dotfiles, a claim about a file that says no such
thing. Row 12's quotation belongs to both families, since the string it quotes is in no file; row
2's does not, because every listing was true. The shared part is that no row is required to produce
evidence its own criterion can be read off.

**Below the queued subtraction pass over the check prompts, not above.** Three reasons, none of them
that this is unimportant. It costs nothing today, so under
[`0008`](decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) it has not yet
shown that it changes behaviour, and the two rows it names are passing rows. Any repair adds text to
prompt blocks that have grown three releases running with nothing removed, and the pass is already
four releases overdue and already inheriting more than it was promised. And a rule written now would
be written against row text the pass is about to rewrite; written after, it is one edit against
settled text. If a wrong verdict ever rests on evidence of this kind, it moves to `Now` that day.

---

## Recorded, not tasks

**Two checks would return opposite verdicts on the same pair of files, and after `0.18.0` the state
is reachable only by hand.** `structure-check` row 8 admits three forms for a stub's parent address
and ends: *"A full URL including the scheme, an account-relative location in a synced store such as
'OneDrive, Projects/Northwind', and a relative path to a containing folder all pass. A bare local
path fails."* `registry-check` row 4 never asks what form that value takes. It says: *"Any other
address, a URL or a location in a synced store, is compared as text against the `Address:` line under
where the project lives, character for character."* So a scope whose own address line carried
`0007`'s fourth form, copied faithfully into both stubs, passes row 4 on the character-for-character
match and fails row 8 on the form — two checks, opposite verdicts, one pair of files. Recorded rather
than repaired: the interview no longer produces that scope, so reaching the state now takes a hand
edit of `PROJECT.md`. Row 4 is doing its own job correctly, which is catching a scope that moved and
left its components pointing at where it used to be, and it is not a form check.

**Nothing validates a project scope's own `Address:` line, and `0.18.0` did not change that.** Row 4
above reads that line, but only as a comparison target; no row anywhere judges it against the address
forms. The stop that `0.18.0` writes into `interview.md` therefore rests on the interview text alone.
A session that ignores it is caught by nothing until a component is attached, and then by
`structure-check` row 8 on the stub. That is the consequence row 8 still catches, and the reason row 8
was not touched.

**The two derivation rules test the shape of a path, not whether the store resolves.** Found by three
of the six `2026-09-03-scope-address` runs, independently, and **raised by the `0.17.0` before-run
too, so it predates `0.18.0`.** `interview.md` rule 1 fires on *"If the local path resolves inside a
synced store"*, and a session reading it will accept any directory named `OneDrive` on the path: in
the C1 run the session went further than the rule and checked the machine's real `~/OneDrive`, ruled
the rule had not fired, and derived from the git remote instead. So the rule as written and the rule
as applied are different rules. Recorded, not repaired: `0.18.0` changed only the branch where
neither rule fires, and the runs that found this were controls for that branch rather than tests of
these two.

**Which derivation rule wins when both fire is unsettled, and control C1 could not reach the
question.** No line in `interview.md` orders rules 1 and 2. C1 was built to exercise it — a folder
both inside a store and a git working copy with a remote — and the session dissolved the premise by
rejecting the simulated store, so the case went untested. What C1 did establish is what it was
watching for: `0.18.0`'s new ask branch did not leak into a case where a rule fires. Testing the
precedence question needs a folder in a real synced store that is also a working copy with a remote.

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

**The part worth recording is the process, not the answer.** The question was added without the
alternative being considered. The coverage check established that the placeholder had no source, and
the response went straight to sourcing it rather than asking whether it should exist. Both remedies
were available from the same finding and one of them was never put on the table. **A gap in a
document is not automatically an argument for filling it**, and this framework has closed two
questions by finding that the thing in question need not exist — the platform fragment in `0008`, and
where platform rules live, which vanished with it.

`set -e` would have prevented neither. Both defects were produced by a script whose assertion failed
and whose commit ran anyway, and `set -e` fixes that particular script; the step catches the class,
including the instances that arrive some other way.

**Confirm the arms by `diff -r`, not by construction.** Building two trees carefully is a story about
what they contain; diffing them is a measurement. Run across both copies, 219 MB and some thousands
of files each, the only output was the override and those three lines:

```text
Only in a: REPOSITORY.md
a/AGENTS.md 18,19d17   < This folder also sets rules of its own. Read `REPOSITORY.md` as well.
a/CLAUDE.md 18,21d17   < This folder also sets rules of its own. Read `REPOSITORY.md` as well.
                       < @REPOSITORY.md
```

The control ran on 2026-08-29, driven by Alex after the session's own attempts to launch it were
refused three times by a permission classifier.
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

**`0.13.0` was released, tagged and pushed**, after the owner answered all four questions in one
message with no follow-up. **That acceptance test was his criterion and it is what five provisional
releases were waiting on.**

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

## Plan for the session after this one

**Then: ArtGlina.** Still on the pre-`0.5.0` shape, never migrated. It is the
only project with a real `Assets` component holding material rather than code, so it is where that
posture gets its second test and where the assets override may get its first real case. Expect the
`Unsorted/` folder to be the interesting one.

**Corrected 2026-08-30. Both halves of that expectation were wrong.** ArtGlina was adopted on
`0.13.0` and both its components were attached on 2026-08-30, so it is no longer on the pre-`0.5.0`
shape. And the two components it declares are `Artglina UA` and `Artglina Sandbox`, both
`Repository`: **no `Assets` component was declared and no `Unsorted/` folder entered the registry.**
So the `Assets` posture still has exactly one end-to-end run, on a folder of theme sources, and the
assets override has still never been used at all — which is what [`handover.md`](handover.md) says
under "Where the evidence is thin", and it stays true. The paragraph above is left standing because a
prediction that missed is worth more visible than deleted.
