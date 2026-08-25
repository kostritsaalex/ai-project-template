# 0007. A component with no address says so

**Date:** 2026-08-25  
**Status:** accepted

---

## Context

A reference to another scope carries an address that resolves from where the reference is read.
Three forms qualify: a repository URL, an account-relative location in a synced store, and a relative
path when the referenced scope contains the referring one. A location on one person's machine does
not qualify.

None of the three fits a folder that exists on one machine only. The case is real. `WordPress 7
Engine` is a WordPress installation in the WSL home filesystem, with no remote and nothing syncing
it, and it is a genuine part of its project.

Attaching it twice, against the same blueprints, produced two different inventions. The first run
wrote `Address: Local only. No remote; this folder is not under version control.` with the local path
on its own line beneath. The second wrote `Address: ~/wordpress-7` and deleted the local path line as
a duplicate. The second is worse: it promotes a machine-local path to the status of an address
silently, and a reader on another machine follows it and lands nowhere with no signal that there was
never anything to follow.

Nothing caught either. `structure-check` 11 asks a registry block for an address without saying what
makes one valid, so it certified the first as a pass. Check 8 defines validity but reads only the
component's own folder, so it never sees the registry. On a cold start the `Address:` line was quoted
back as though it were a rule limiting what may be changed there.

The criterion took a correction to find. It is not version control. A folder can be under `git` and
still exist on one machine only; `git init` changes nothing here. What makes an address possible is a
copy that exists off this machine, and only a remote, or a synced store, or a containing folder that
travels, provides one.

A second and narrower thing surfaced in the same run. When a project spans a filesystem boundary, one
side can usually reach both and the other cannot: from WSL, `/home` and `/mnt/c` are both ordinary
paths, while from the Windows side the WSL filesystem needs a `\\wsl.localhost\...` form that is
local to one machine and resolves, on any other machine, to something else entirely without
erroring. Read from the wrong side, the local paths in a document are not inconvenient. They are
false.

## Decision

**A fourth form: none, said plainly.**

```text
## WordPress 7 Engine

Repository. Things get changed here. Platform or framework core changes only through its own
update mechanism, never by hand.
Address: none. No copy of this folder exists off this machine.
Local path: `~/wordpress-7`
```

The sentence names the one fact that decides the question and nothing beside it. It stays true when
the folder gains local version control, and stops being true only when a copy appears somewhere else,
which is exactly when a real address becomes available.

**`structure-check` 11 requires one of the four.** A registry block carries a URL with its scheme, an
account-relative location in a synced store, a relative path into a containing folder, or a plain
statement that no address exists together with the reason. Anything else fails, including a bare
local path in the `Address:` slot.

**The session note is a precondition rather than a preference,** and it names the side from which
every local path in the document is read. This part applies only to a project whose parts sit in
different filesystems. A project living in one filesystem writes no session note and no path note,
deletes both at adoption, and meets none of this.

## Consequences

The registry can say "unreachable from anywhere else" without an agent inventing wording for it, and
a check can now tell a real address from a local path wearing one.

**A component with no address is still a component.** The gap runs one way. Its stubs point upward
with an address that resolves from anywhere, and that direction is the one the framework exists for:
an assistant standing in the folder reaches the parent, reads the registry and learns how the folder
is to be treated. What is missing is only the walk downward, from the parent to that component, and
only from a machine that does not have it.

**The accepted cost, stated plainly.** A reader on another machine gets a component's name, its
posture and a dead end. That is the truth about the world rather than a defect in the document. No
wording produces a copy of a folder that exists in one place, and a document that implies otherwise
is worse than one that says so.

**What does not fix it: `git init`.** Local version control and reachability are separate questions,
and only a remote answers the second. Naming the machine does not fix it either; that was considered
and rejected, because a machine name reads as an address, invites being followed, and becomes false
the day the machine is replaced.

**On the evidence.** The address half of this decision is general: it holds on any operating system
and any setup. The session note half is not. Everything this framework knows about filesystem
boundaries comes from one project, one machine and one person. Whether a Mac with a network volume
behaves the same way is a reasonable guess and nothing more. That is said out loud in
`.docs/architecture.md` so a reader can weigh it.

## Origin

Alex, 2026-08-25, working through the backlog left by the `0.6.0` validation run.

Two of his corrections shaped it. The first sentence proposed for the `Address:` line said the folder
was "not under version control, and has no remote", and he objected that those are different facts
and only the second decides anything, which is what produced the criterion above. Then he asked
whether the framework was being fitted to his own setup, which is what scoped the session note half
and put the note about the evidence into the architecture document.

A third proposal of his was tested and set aside: reaching the WSL filesystem from Windows through
`\\wsl.localhost\...`. It resolves, and that is the problem. The name is a local alias, so on another
machine it resolves to that machine's WSL and returns a different folder rather than an error.
