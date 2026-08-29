# Component Blueprint

How a folder is attached to a project. This is the normal way, and for most components it is the
only thing that ever gets copied into them.

**Blueprint Version:** 0.6.0  
**Framework Version:** 0.10.0  
**Status:** new in `0.5.0`. Replaces the default use of the Repository and Assets blueprints.

---

## Scope

A folder that belongs to a project: a codebase, a site, a folder of photography, the working
material of a workstream. Any of them.

The component carries two stubs and nothing else. Everything that would have gone into a third file
either lives in the parent's registry entry or does not exist.

---

## Files

| File | Role |
| --- | --- |
| `AGENTS.md` | Names the component and points at the parent `PROJECT.md`. |
| `CLAUDE.md` | The same text under the name Claude Code reads automatically. |

Copy both into the component folder. Do not copy this `README.md`.

The two files carry identical text. They exist twice because different tools look for different
names, not because they say different things.

---

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<COMPONENT_NAME>` | Name of this component. Must match its heading in the parent registry exactly. | `Northwind Storefront` |
| `<PROJECT_NAME>` | Name of the parent project. | `Northwind Furniture` |
| `<CANONICAL_PROJECT_SCOPE_ADDRESS>` | Where the parent `PROJECT.md` lives, read from here: a full URL, an account-relative location in a synced store, or `../` when the project scope contains this folder. This is the opposite direction from the address in the parent's registry, which says where this folder is. | `OneDrive, Projects/northwind` |
| `<PARENT_PROJECT_LOCAL_PATH>` | Where that resolves on a machine that has it. Delete the line entirely when the address is `../`. | `~/OneDrive/Projects/northwind` |

The name has to match the registry heading. It is how an assistant standing in this folder finds
the row that describes it.

---

## What is not a component

A folder that has not been declared one. It is files, belonging to whichever component contains it
and taking that component's posture.

Being a component is a decision somebody made and wrote into the registry. It is not a property of
what sits on disk, so nothing is promoted by being noticed, and a folder full of subfolders raises no
question about which of them qualify. The answer is none of them, until somebody says otherwise.

This is what keeps setup short. Without it, every folder in a tree is a candidate, and an assistant
that surveys the tree returns a list of questions their owner has no reason to answer.

The cost is that the registry becomes the only truth about what exists. A folder that should have
been declared and was not is invisible, and neither check will ever find it. That cost was already
paid: the registry has always been the only map.

---

## Why there is no third file

Everything a component used to say about itself is now one line in the parent registry. That line
carries the posture: `Assets`, which adds nothing to the project's principles, or `Repository`,
which adds the one rule about platform and framework core.

A component that says nothing about itself needs no file to say it in.

---

## What this costs

A component cut off from its parent cannot read its posture or the project's principles. It is not
left knowing nothing: it still has its own name, the name of the project, the parent's address, any
local rules it carries, and, from the stub's line about the registry entry, the knowledge that a
posture exists and where it lives. What it cannot do is act on it.

This is accepted rather than mitigated. Copying the posture down into the stub would put the same
rule in two places, and two copies of a rule drift.

The stub is told to fail loudly for exactly this reason. An assistant that cannot reach
`PROJECT.md` is instructed to say so and stop, rather than work on whatever it can see. Observed on
`0.6.0`: with the parent folder moved away, a component reported the failure before answering
anything, found the folder at its new path, refused to open it because following it would be the
guess the stub forbids, and named what it could not know.

---

## When to add a third file

When the component has rules that are its own. Then take
[`../repository/`](../repository/) or [`../assets/`](../assets/), whichever posture fits, and point
the two stubs sideways at it instead of upward.

The registry entry stays, and it stays authoritative. If the registry and the override disagree
about the posture, the registry is right and the override is a bug.

---

## How to adopt

1. Copy `AGENTS.md` and `CLAUDE.md` into the component folder.
2. Delete the blueprint notice at the top of each.
3. Replace every placeholder. The two files end up identical apart from the heading.
4. Add the component's block to the parent registry, naming its posture.

Before committing, search for `<!--` and for `<` followed by a capital letter.

---

## Verify the adoption

[Structure check](../checks/structure-check.md) right after adoption, then
[cold start check](../checks/cold-start-check.md) in a new session, using its component prompt.

The second one is the only test that matters here. It answers whether an assistant arriving cold in
this folder reaches the parent and learns how to treat the place.
