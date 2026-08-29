# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-08-29, after the move into WSL and the repair of the documents it made stale.

---

## Where we are

`0.7.0` is released, tagged and pushed. Working tree clean, nothing half-done.

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

Empty. The address question was settled in `0.7.0` by
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

**Where platform rules live.** They follow from a platform, not from a folder, which is the shape
`0005` used to move the preserve rules into the registry. There is no mechanism, so a fragment gets
copy-pasted into every WordPress component and nothing owns it. Candidate split: the shape of such a
rule is generic and can sit as a prompt in the `REPOSITORY.md` comment, while the WordPress instance
stays in the fragment. Supporting evidence from the run: the agent generalised the ownership axis to
third-party plugins by itself, writing a bullet the old fragment did not contain, and that bullet is
now the fragment's first line.

**A second razor, for rules.** The razor in `0004` cuts facts. Rules are invisible by construction,
so nothing constrains them. Candidate test: a rule earns a document only if an assistant would do
otherwise without it. Eight of the nine bullets in the Engine's `REPOSITORY.md` are ordinary
WordPress practice, which makes that folder the place to settle it: one task with the file and one
without, judged by the work.

**The third check.** Walk the registry from `PROJECT.md`, open each component's stubs, compare the
parent address and the component name against the block. Registry to disk only. Done by hand twice in
this run, which is what caught the session note and the address wording.

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
would follow without being told. The third check, above, would catch it as a side effect.

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
that nothing reads back against the disk.

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

**The naming question, closed but worth watching.** The pair stays, decided 2026-08-24. Hours later
the owner's reasoning for calling a theme folder `Assets` included "a repository is technically out
of place here because we host this on OneDrive", the storage-based reading the names invite. If a
second instance appears, reopen.

**The framework's own local path had the defect check 14 exists to catch.** `PROJECT.md` gave
`~/Repositories/ai-project-template` with nothing saying what holds it up. That form resolves on the
Windows side and not inside WSL, which is why every prompt this session used
`/mnt/c/Users/kostr/Repositories/...` instead. Fixed on 2026-08-25 by naming both forms. Check 14
would not have caught it: it is `n/a` when a document says nothing about its path, so silence passes.

**A platform fragment now carries a version tied to a blueprint version.**
`platforms/wordpress.md` is the first file in the framework with `For: Repository Blueprint 0.6.0`
in its header. If fragments multiply, somebody has to revisit them each release, and no mechanism
will remind them.

---

## Plan for the session after this one

`0.7.0` is merged to `main`, tagged and pushed. Working tree clean. Nothing is half-done.

**Start here: the second razor.** The item with the most leverage on this list, because it governs
every rule the framework will ever gain, and the experiment is already set up. The Engine's
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

**What this leaves.** The razor now has its first measurement instead of an argument. Whether it
becomes a rule of the framework is a decision, and by this project's own habit a decision that
changes a rule gets a record.

The Engine has since moved inside the WSL home filesystem. Its registry block in the WordPress 7
scope is the authority on where it now is.

**Then: ArtGlina.** Still on the pre-`0.5.0` shape, never migrated. It is the
only project with a real `Assets` component holding material rather than code, so it is where that
posture gets its second test and where the assets override may get its first real case. Expect the
`Unsorted/` folder to be the interesting one.

**Do not start with:** a full framework re-read, or another validation run. `0.6.0` and `0.7.0` were
both validated on 2026-08-25 and nothing in either is suspected.
