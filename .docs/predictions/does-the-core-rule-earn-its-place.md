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
