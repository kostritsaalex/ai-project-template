# 0006. The postures carry one rule between them

**Date:** 2026-08-24  
**Status:** accepted

---

## Context

[Decision 0005](0005-the-registry-carries-the-component.md) made the posture the one thing a
component is ever told about itself. For `Assets` that word carried four preserve rules: do not
reorganize, do not rename, do not move, preserve the existing organization. They were inherited from
the `ASSETS.md` that `0005` demoted, and they were never examined again on the way across.

Read against a real folder, they describe something this project does not have. An assets component
here is business material: photographs for a site and for social media, presentations, spreadsheets.
New material arrives constantly and existing material gets updated. It is the most alive folder in
the project. The framework calls it "find them and leave them as they are" in five places, which
reads as do not touch, and an assistant that believes it will refuse ordinary work.

The rules were also never run. The assets posture has not been used end to end on `0.5.0`: both
WordPress 7 components are `Repository`, and ArtGlina is still on the pre-`0.5.0` shape. So four
rules that shape every assets component in every adopted project rest on no observation at all.

At the same time the one rule a code folder does need was in the wrong shape.
`blueprints/repository/REPOSITORY.md` prompts its owner for "what may never be edited in place".
WordPress moving from 6 to 7 replaces core wholesale, and "never edited" forbids that. The axis is
ownership rather than immutability: core belongs to its updater, and the updater is allowed to
change it.

## Decision

**Both postures inherit the project's principles. `Assets` adds nothing. `Repository` adds one
rule.**

Being listed in the registry is what gives a component the principles in `PROJECT.md`. That is the
floor for both postures and it is the whole of `Assets`:

```text
## Northwind Brand Assets

Assets. Live material. Work here as the task requires.
Address: assets/brand
```

`Repository` adds one line and nothing else:

```text
## Northwind Storefront

Repository. Things get changed here. Platform or framework core changes only through its own update
mechanism, never by hand.
Address: https://github.com/acme/northwind-storefront
```

A folder that needs more than its posture gives it takes `ASSETS.md` or `REPOSITORY.md`, exactly as
before. The registry stays authoritative where the two disagree.

## Consequences

The four preserve rules are removed from the framework.

**The accepted cost, stated plainly.** Nothing now stops an assistant reorganizing a folder of
material on its own initiative. Renaming a photographer's files or flattening a folder tree is not
forbidden anywhere. This is accepted for two reasons. The rules were never run, so removing them
costs no observed behavior. And an assets folder in this project is live, so a rule written for a
museum was going to be broken by ordinary work, and a rule that ordinary work breaks teaches an
assistant that the document can be ignored. A folder that genuinely needs its arrangement protected
is what `ASSETS.md` is for, and that is now the first real case the assets override would take.

The postures stop being opposites. `0005` described them as two directions, change against preserve.
They are now a floor and one optional layer on top of it, and one of them is empty. The prose that
calls `Assets` "mostly find them and leave them as they are" goes with the rules it described.

Cold start question 3 changes axis. It asked whether things get changed in this folder or found and
left alone. It now asks whether any rule limits what may be changed here, and where that rule is
written. An assets component answers "none beyond the project's principles" and still has to reach
the parent to say it, so the chain is tested either way.

The posture stops being asked blind. Platform code is visible from inside the folder, so an
assistant proposes the posture and shows it in the summary table as a settled row the person can
overturn, which is already how the procedure treats every value it settles from a source. `0004`
forbids asking about what can be read, and this is the reading that answers it. The question stays
visible in the summary rather than disappearing, because a component may be attached years after its
registry block was written, and that table is the only moment anyone looks at the word again.

**The pair stays, and that question is now closed.** The difference between the two postures bites
only where platform code lives: in a folder of the project's own code with no vendored core, both
words behave identically today. That is an argument for one flag, and it was considered and
rejected. `Repository` carries a layer that is expected to grow, and a layer that grows needs
somewhere to grow into. Two words and two override files stay. The naming question left open in the
notes behind `0005` is closed with them.

## Origin

Alex, 2026-08-24, working through a backlog built from two outside reviews of `0.5.0`.

Both reviews reached for the opposite answer. The first found that the preserve rules say nothing
about editing a file in place and asked for the gap to be closed, or for a third posture. The second
argued against widening the posture before a mixed component had been run. Neither asked what an
assets folder actually is, and the four rules survived both.

What settled it was Alex describing one: live material, new content constantly, and no reason for
any rule beyond the project's principles. The `Repository` half came from his counter-question about
upgrading WordPress from 6 to 7, which the previous wording forbade.
