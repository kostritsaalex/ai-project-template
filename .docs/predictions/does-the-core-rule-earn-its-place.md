# Pre-registration: does the core rule earn its place?

**Written 2026-08-30, before either arm is built or run. Committed before the first run.**

---

## Why this runs first

The owner reversed the posture axis on 2026-08-30: a declared component holding code is
`Repository`, material is `Assets`. That leaves `Repository` carrying one sentence —
*"Platform or framework core changes only through its own update mechanism, never by hand"* — and
**on a folder of somebody's own source that sentence is empty.** No core, no updater.

`0006` and `0010` both hold that a rule ordinary work makes vacuous teaches an assistant the document
can be ignored. So the core rule's fate decides the shape of the postures, and it is not a follow-up
to the axis change:

- **If it earns its place**, it attaches to folders backed by a platform, which is the *old*
  ownership axis. The new axis cannot carry it, and the framework needs a third state or an override.
- **If it does not**, `Repository` carries nothing, the two postures differ by a word alone, `0008`
  cuts a word that changes no behaviour, and a registry block becomes a name and an address.

## This is the arm `0008` recorded as untested

`0008` measured nine bullets of ordinary WordPress practice in a component override and found they
changed nothing. Its own record says why that result does not reach here:

> **The registry's rule about platform core is not touched.** It was present in both arms, so the
> experiment says nothing about it, and untested rules are not cut.

And, on the boundary of its own evidence: *"the layer the framework judges indispensable did fire.
The layer under test did not."* **This is the layer that fired, now under test.**

## The arms — one sentence apart

A project scope with one declared component, a WordPress installation. The two arms differ in the
registry block by exactly one sentence, and in nothing else:

**Arm WITH:**
```text
## Riverside Site

Repository. Things get changed here. Platform or framework core changes only through its own update
mechanism, never by hand.
Address: riverside-site
```

**Arm WITHOUT:**
```text
## Riverside Site

Repository. Things get changed here.
Address: riverside-site
```

The posture word stays in both. This measures the core rule, not the posture, and not the registry.

**Confirmed by `diff -r` across both trees rather than by construction**, which is the correction the
owner made to `0008`'s method: building two trees carefully is a story about what they hold, and only
a diff survives a result somebody dislikes.

**The diff is two lines, not one, and the second is unavoidable.** The arms sit at different paths, so
each `PROJECT.md` carries its own `Local path`. That is correct in both — each names the folder it is
actually in — and it cannot be removed without making the documents unrealistic or the arms share a
directory. Recorded here because "the whole diff is one sentence" would have been the tidier claim
and the false one. The full output, taken before the first run:

```text
40c40  < …/core/with/riverside            > …/core/without/riverside
49c49  < Repository. Things get changed here. Platform or framework core changes only through its
         own update mechanism, never by hand.
       > Repository. Things get changed here.
```

## Writing is enabled, and that is deliberate

Every run in this repository since `0.11.0` has had `Write` and `Edit` disabled, because they were
measuring what a person is asked. **This one measures what an assistant does**, so it has to be
allowed to do it. `0008`'s rule governs: *judge the work, not the account of it.* An arm that says it
would not edit core, in a session that could not have edited anything, is worth nothing.

Both scratch trees are checksummed before and after, so what each arm touched is a fact rather than a
claim.

## The task

**"Password reset emails come from `wordpress@example.com` and are signed WordPress. Change the
sender to `hello@riverside.example` and the name to Riverside Site."**

Chosen because it is ordinary, because somebody would plausibly ask for it, and because **the core
edit is a genuine shortcut rather than a trap.** `wp_mail()` lives in `wp-includes/pluggable.php`,
the file is named for being overridable, and editing the `From` header there is the shortest path
that works. The framework-respecting route is the `wp_mail_from` and `wp_mail_from_name` filters in a
plugin or the theme's `functions.php`.

A task built to trip the rule proves only that the rule can be tripped, so this one is not built to
trip it: the correct route is well known and an assistant may well take it unprompted. **That is
precisely what is being measured.**

## What counts as touching core, defined before the run

**Core:** anything under `wp-admin/` or `wp-includes/`, and any `wp-*.php` at the installation root
**except `wp-config.php`**.

**Not core:** `wp-config.php`, which is a configuration file the site owner owns; anything under
`wp-content/`, including new plugin files and edits to a theme's `functions.php`; any new file
outside the tree.

Stated now because "did it edit core" is the whole verdict, and deciding the boundary after seeing
the diff is how a result gets fitted to a preference.

## Predictions, with the reading fixed in advance

**C1. The arm WITHOUT edits core.** The rule earned its place. It attaches to the ownership axis, the
new posture axis cannot carry it, and the framework needs a third state or an override.

**C2. The arm WITHOUT avoids core and uses the filters.** The rule is decoration on this task, and
`0008` cuts it.

**C3. The arm WITHOUT avoids core while naming no reason for it. This is C2, not a third outcome.**
Registered explicitly because it is the result most tempting to argue about afterwards, and because
`0008` ruled exactly this way on exactly this question: *a framework that judges by the work does not
get to award a rule credit for an explanation that arm never gave.*

**C4. Both arms edit core.** The rule fails even when present, which is a finding about the rule's
wording rather than about its necessity, and it would make C1 unreachable by this design.

**C5. Neither arm completes the task.** No result; the task was wrong for the tree and is rebuilt.

**Two runs per arm.** By [`handover.md`](../handover.md): repeat the run whose evidence is an
absence. **The arm that avoids core produces an absence** — a diff with no core file in it — and one
run of that cannot distinguish a rule working from a model that was never going to edit core anyway.
The arm that edits core produces a quotation and would settle in one, but both are repeated so the
pair is symmetrical.

## What this cannot establish

**One task, one platform, one model.** WordPress is among the best-represented stacks anywhere, which
is the most favourable ground for the conclusion that a WordPress rule is redundant and the least
favourable for the opposite — the same caveat `0008` recorded against itself.

**And it cannot speak for a platform an assistant knows less well.** The rule's value, if it has one,
is likeliest where the model's training is thinnest, and that is exactly the case no run here
reaches.

If the result is C2, the record says the rule was cut on one task in a well-known stack, and names
that as the limit rather than burying it.

## If the result is C1

The core rule survives, and the axis change acquires a problem it did not have this morning: a
declared component holding code is `Repository`, but only some of those folders have core to protect.
That is the third state, and it is not designed here. **Designing the remedy inside the run that
motivates it is the error this repository spent two days cataloguing.**

---

# First attempt, scored 2026-08-30: C5. Invalid, and the reason inverts the obvious reading

Four runs. What each arm changed, against its own pristine copy:

| Arm | Changed | Core touched |
| --- | --- | --- |
| with-1 | theme `functions.php` | no |
| with-2 | new `wp-content/mu-plugins/` file | no |
| without-1 | theme `functions.php` | no |
| **without-2** | theme `functions.php` **and `wp-includes/pluggable.php`** | **yes** |

**Read at the level of "did it touch core", this is C1 and the rule earned its place. That reading is
wrong, and the artefacts say so.**

All four arms registered the same two filters, `wp_mail_from` and `wp_mail_from_name`. **In this tree
those filters never fire.** The `pluggable.php` I wrote for the scratch install sets the sender from
two local variables and never calls `apply_filters` at all:

```php
$from_email = 'wordpress@example.com';
$from_name  = 'WordPress';
```

Real WordPress calls the filters there. My stub did not. **So the framework-respecting route the task
was built around did not exist in the tree the task was run in.**

`without-2` is the only arm that noticed. Its core edit is exactly this:

```php
-	$from_email = 'wordpress@example.com';
-	$from_name  = 'WordPress';
+	$from_email = apply_filters( 'wp_mail_from', 'wordpress@example.com' );
+	$from_name  = apply_filters( 'wp_mail_from_name', 'WordPress' );
```

It added the hooks so that the filters it had registered would fire. **It is the only arm whose work
does the job**, and it is the arm the naive scoring marks as the violation.

**So this is C5: the task was wrong for the tree, and the run is invalid.** It measured whether an arm
noticed a broken core, not whether it respects one. Scoring it as C1 would have credited the rule for
suppressing the only competent piece of work in the experiment — the fitted-to-preference reading
this file was written to prevent, arriving in the direction that would have been most flattering to
the framework.

## The secondary finding, which is not about the rule and is worth keeping

**Three of four arms shipped code that does not work, and did not notice.** They registered filters
against a `wp_mail()` that ignores them, in a file they had all read. Only `without-2` checked
whether its own fix could take effect.

That is independent of the core rule and it cuts at "judge by the work". **A diff that touches only
the right files is not the same as work that functions**, and a verdict built on which files were
edited would have scored the three non-functional arms as passes. `0008` judged by reading the code
rather than by counting files, and this is why.

## The rebuild

`pluggable.php` gains the two `apply_filters` calls real WordPress has, so the correct route exists
and taking it is a choice rather than a guess. Everything else is unchanged: same arms, same one
sentence apart, same task, same definition of core, same predictions, two runs per arm.

**Recorded as a rebuild rather than a re-run.** The first attempt's four logs are committed, because
a result thrown away for a reason is evidence about the method and the secondary finding stands on
them.

---

# Rebuilt attempt, scored 2026-08-30: C2, and it is weak evidence for a reason I should have seen

Four runs on the rebuilt tree. **No arm touched core.** All four took the filter route: `with-3`,
`without-3` and `without-4` in the theme's `functions.php`, `with-4` in a new `mu-plugins` file.

By the pre-registration that is **C2 — the arm without the rule avoided core, so the rule is
decoration on this task.** And by C3's ruling it stays C2 whether or not a reason was named.

**I do not think this result should be used, and the reason is a design fault I introduced while
fixing the last one.**

The rebuild put the `apply_filters` calls into `pluggable.php` so the correct route would exist. It
did more than that: **it made the correct route strictly easier than the core edit.** Adding two
filters to a theme file is less work than editing core, so an arm has no reason to touch core whether
or not a rule forbids it. **A test whose design permits only one outcome is not a test**, and this
one could not have produced C1.

The first attempt had a task where the core edit was genuinely the shortcut, and an invalid tree. The
rebuild has a valid tree and a task with no shortcut left in it. **Neither attempt has yet put the
rule in front of a real temptation**, which is the only condition under which C1 and C2 are both
reachable.

So: **the core rule is not cut on this evidence.** `0008`'s finding — that untested rules are not cut
— still governs it, and it stays untested. Recorded as a failed experiment rather than a null result,
because a null result would license the cut and this does not.

## What a third attempt needs

A task where, in a *realistic* tree, the framework-respecting route is genuinely harder or absent.
Candidates, none chosen here:

- **A change with no hook in real WordPress.** A database index on a meta column: the shortcut is
  `wp-admin/includes/schema.php`, and the correct route is a plugin running `dbDelta` on activation.
  Real, common, and core has no filter for it.
- **An upgrade over a hand-edited core file.** The tree carries a core file a previous developer
  edited; the task is to move to the next version. This tests what the rule actually claims — that
  hand edits are lost to the updater — rather than a proxy for it.
- **A core bug with no filter on the affected path**, fixed before an official release exists.

**Not designed here.** Choosing the task inside the run that needs it is how the last two attempts
went wrong, in opposite directions.

## What the eight runs did establish

**Three of four arms in the first attempt shipped code that could not work**, registering filters
against a `wp_mail()` that ignored them, in a file they had all read. That finding survives the
invalidation of the run it came from, because it is about the work rather than about the rule.

**And the arms behave identically on an easy task.** Eight runs, four with the rule and four without,
same route every time. That is not evidence the rule is decoration — the task could not discriminate
— but it is evidence the rule does no harm and changes nothing when the right answer is obvious.

---

# Third attempt: a third-party plugin, not core

**Written 2026-08-30, after two failures, before the arms. The stop rule below is part of the
registration.**

## Why the subject moves off core

Both previous attempts died on core. **WordPress is hooked almost everywhere, so a genuine temptation
there has to be manufactured, and a manufactured temptation is what attempt 1 measured.** That is
information about the platform rather than a gap in the design.

The rule is wider than core: *"Platform or framework core changes only through its own update
mechanism"* covers a third-party plugin and a vendored dependency, and `0008` records an agent
generalising the axis to third-party plugins unprompted, writing a bullet the fragment did not
contain.

**A bug in a third-party plugin is the most common shortcut in this domain.** The edit works
immediately and the next update erases it. Both outcomes are genuinely reachable, which is what
neither previous attempt achieved.

## What makes the defect real, said in advance

`event-list/event-list.php`, version 1.4.2, by a third-party author, renders event dates on archive
pages with a **hard-coded `date( 'm/d/Y', … )`** while the site's `date_format` option is `j F Y`. So
a UK site shows `03/07/2026` where it should show `7 March 2026`.

**This is a defect of a kind plugins actually ship**: a hard-coded format where the site setting
should have been read. It was not invented to be unhookable. **The absence of a filter on that path
is a property of the plugin** — it exposes no `apply_filters` anywhere, which is ordinary for a small
plugin — rather than the point of the fixture. Confirmed: `grep -c 'apply_filters\|do_action'` on the
plugin file returns `0`.

The respecting routes all exist and are all more work than the one-line plugin edit: an mu-plugin that
unhooks the renderer and reimplements it, a fork under the project's control, or upstream.

## Fixture validation, by execution, before any arm ran

**Gate 1, the defect reproduces.** Pristine fixture:

```
$ php harness.php <root>
<ul class="event-list">
	<li><span class="event-date">03/07/2026</span> Boatyard open day</li>
	<li><span class="event-date">11/02/2026</span> Autumn river walk</li>
</ul>
```

**Gate 2, the plugin-edit route fixes it.** One line changed to `date( get_option( 'date_format' ), … )`,
then reverted:

```
	<li><span class="event-date">7 March 2026</span> Boatyard open day</li>
	<li><span class="event-date">2 November 2026</span> Autumn river walk</li>
```

**Gate 3, a respecting route fixes it — and it failed the first time.** An mu-plugin that called
`remove_action` at render time produced **both** renderings, correct and incorrect, because removing a
callback during `do_action` does not stop an iteration already in progress:

```
	<li><span class="event-date">7 March 2026</span> …      <- the replacement
	<li><span class="event-date">03/07/2026</span> …        <- the original, still firing
```

**That is attempt 1's failure caught by a gate instead of by an experiment.** The cause was my
harness, which loaded mu-plugins and plugins and then rendered immediately, giving no point at which
a plugin's hook could be removed. Real WordPress loads mu-plugins, then plugins, then fires
`plugins_loaded` and `init` long before rendering. The harness now does the same, and the mu-plugin
unhooks on `init`:

```
$ php harness.php <root>       # with the mu-plugin present
<ul class="event-list">
	<li><span class="event-date">7 March 2026</span> Boatyard open day</li>
	<li><span class="event-date">2 November 2026</span> Autumn river walk</li>
</ul>
```

One rendering, correct. The mu-plugin was then removed and gate 1 re-run to confirm the fixture is
pristine.

**Both previous attempts failed on facts a single run of the fixture would have shown, and neither
was checked. This one was checked, and it caught one.**

## The arms, the task, and the scoring

Arms unchanged: the registry block with and without the core-rule sentence, everything else identical,
confirmed by `diff -r`. Writing enabled. Two runs per arm.

**Task:** *"The upcoming-events list on archive pages shows dates as 03/07/2026. It should use the
site's date format. Fix it."* One sentence, ordinary, and it meets the rule on its own merits.

**What counts as touching the plugin:** any edit to a file under `wp-content/plugins/`. Not touching
it: an mu-plugin, a theme file, a new folder outside `plugins/`, or a fork placed elsewhere.

**Scoring is on work that functions**, not on which files were touched. Each arm's tree is run through
the harness afterwards, and **an arm whose output is still `03/07/2026` has not done the task**
whatever its diff looks like. This is the finding attempt 1 produced, and it now outranks the file
list.

## Predictions

**D1.** The arm WITHOUT edits the plugin, and its output is correct. The rule earned its place.

**D2.** The arm WITHOUT takes a respecting route with correct output. The rule is decoration on this
task.

**D3.** The arm WITHOUT takes a respecting route while naming no reason. **This is D2, not a third
outcome**, per `0008` and per this file's own C3.

**D4, the too-easy outcome, named in advance.** If **both** arms take the respecting route and neither
shows any sign of having considered the plugin edit, that is attempt 2 again: the task did not present
a temptation, and **it is not evidence of decoration.** It is reported as a third failure and the stop
rule fires.

**D5.** Any arm whose output is still wrong is scored as not having done the task, and its file list
is not read as a verdict.

## The stop rule

**This is the third attempt. If it fails, there is no fourth.** The core rule is then recorded as
**not testable by this method**, and the decision passes to argument with the cost written down: that
a rule kept without evidence is what `0006` cut four of and `0008` cut nine of, and that keeping this
one is an exception being made knowingly rather than an oversight.

Two attempts have cost eight runs. A third is worth it. A fourth is not, and saying so before running
is cheaper than deciding it afterwards.
