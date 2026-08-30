> **BLUEPRINT FILE. NOT ACTIVE INSTRUCTIONS.**
>
> This file belongs to the AI Project Template blueprint library. It describes no real project
> and must not be followed as project instructions.
>
> To adopt it: copy this file into the project scope, replace every `<PLACEHOLDER>`, adapt the
> content to the actual project, and delete this notice.

---

# <PROJECT_NAME>

> **AI Project Entry Point**
>
> Read this before working anywhere in this project.
>
> **Derived from:** Project Blueprint <PROJECT_BLUEPRINT_VERSION>  
> **Last Updated:** <YYYY-MM-DD>

---

# What this project is

<!--
A few sentences. Say whether the project is only software or whether software is one part of
something larger: an assistant that believes it is looking at a software project treats everything
else as out of scope.

Then the boundary, written as a closed inclusion: what the project covers, and then that anything
else is outside it. The closure sentence is the boundary. Without it the reader has an inventory and
no rule.

This is the only rule in the framework proven to change what an assistant does: without a boundary, a
request the project excludes arrives looking like ordinary work and gets done. It is written as an
inclusion because the complement of a project is endless and nobody can list it, while what a project
covers is usually one sentence. "Currently" is deliberate wherever it appears. It records a present
boundary, not a permanent one.

**Name kinds of work, not places.** `restoration, photography and selling online`, not `the main
folder and the shop repository`. Where the work happens is the registry's job one section down, and a
boundary written as a list of folders duplicates it while answering nothing.

Naming a near miss is allowed and not required: where you already know the adjacent thing people
assume is inside and is not, say so. Do not attempt the rest of the complement.

If the boundary has not been decided, delete the sentence and write in its place that it has not been
decided, what will settle it, and what to do meanwhile. Leaving the topic out altogether is worse
than leaving it open: an assistant asked what falls outside the project will answer from the nearest
sentence that looks like a boundary, and any sentence about a component not being attached will do.
That was measured, and writing a real boundary fixed it.

Do not describe what the folders contain. An assistant can look.

Do not say here which components exist, which are attached, or where they sit. That is the registry's
job, one section down, and a copy here has to be repaired by hand every time the registry changes.
-->

<PROJECT_PURPOSE>

This project currently covers <SCOPE_COVERS>. Anything else is outside it.

---

# Principles

<!--
The rules that hold across this whole project, in your own words. Priorities in order if the order
has been decided, since a list everyone agrees with in any order decides nothing.

Anything that applies to one component only belongs in that component, not here.
-->

<PROJECT_PRINCIPLES>

---

# Where this project lives

<!--
This is the address every component copies. Get it wrong and each of them knows a parent exists and
cannot reach it.

    https://github.com/acme/northwind-project     a repository, full URL, scheme included
    OneDrive, Projects/northwind                  a folder in a synced store, account-relative

Keep spaces out of the folder names. A space resolves fine on any system and costs a pair of quotes
in every shell command that touches the folder, forever. Hyphens or underscores instead. The
project's name keeps its spaces and is the title of this document; the folder does not have to match.

Two more lines can go here, and they answer different questions. Decide them separately.

`<PATH_NOTE>`: what makes the local path above true. A path under a synced store, reached from
another filesystem, usually holds because of a symlink somebody created once. Nothing in any file
records that, so the path is true where it was written and false everywhere else. Name the
arrangement and give the command, so a machine that lacks it can be fixed instead of failing quietly:

    `~/OneDrive` is a symlink to the Windows OneDrive folder, which is what makes the local path
    above true. Create it once on a machine that lacks it:

        ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive

This one has nothing to do with components. A single-folder project reached through a mount needs it
just as much. Delete it only when the path holds on its own.

`<SESSION_NOTE>`: where to start a session so that every component in the registry resolves. This one
does depend on the components, so it cannot be settled before they are known, and it has to be
revisited when one is added:

    Start sessions inside WSL. From there both this folder and `~/wordpress-7` are ordinary paths;
    from the Windows side `~/wordpress-7` does not resolve at all.

Name the side that reaches every component, not the side you happen to prefer. When a project spans
a boundary one side can usually reach both and the other cannot, and read from the wrong side the
local paths in this document are false rather than merely awkward. This is a precondition, so write
it as one.

Delete it while every component sits on the same side as this folder.
-->

Address:

```text
<PROJECT_SCOPE_ADDRESS>
```

Local path:

```text
<PROJECT_LOCAL_PATH>
```

<PATH_NOTE>

<SESSION_NOTE>

---

# Components

<!--
The registry. This is why a project scope exists: no component can hold it, because it describes
the others, and it is what lets an assistant move between folders that sit far apart.

One block each. Name, posture, address:

    ## Northwind Storefront

    Repository. Things get changed here. Platform or framework core changes only through its own
    update mechanism, never by hand.
    Address: https://github.com/acme/northwind-storefront
    Local path: `~/Repositories/northwind-storefront`

    ## Northwind Brand Assets

    Assets. Live material. Work here as the task requires.
    Address: assets/brand

The posture line is the whole of what a component is told about itself, so it belongs here and
nowhere else. Both postures inherit the principles above and nothing else is shared. Assets adds
nothing to them: the folder is live and the task governs what happens in it. Repository adds one
rule, the one written above, and it goes in word for word. A folder that needs more than its posture
gives it takes an override.

The address says where the component is, read from this document. A component that sits inside this
folder gets its path from here, written without a leading slash. The `../` it uses in its own stubs
to point back at this document is the opposite direction and a different value; do not write that
one here.

The heading is the component's name, and the stubs inside the component repeat it. They have to
match: it is how an assistant standing in a folder finds the block that describes it.

No platform, no production URL, no description of contents. An assistant that arrives can look.

Keep this to what reaching a component needs. Whatever an assistant needs in order to work inside
one, rather than to get to it, belongs in that component. This registry is read by everyone, so a
line put here is paid for by every reader.

A folder that is not listed here is not a component. It is files, belonging to whichever component
contains it and taking that component's posture. Being a component is a decision somebody made, not
a property of what is on disk, so nothing gets promoted by being noticed.

Say plainly when something does not exist yet, or has never been wired to this scope. Told nothing,
an assistant assumes the chain works.

A component normally holds two stubs and nothing else, and both point here. One that has rules of
its own also holds `REPOSITORY.md` or `ASSETS.md`. Where such a file and this registry disagree,
this registry is right.
-->

<COMPONENTS>

---

# Documentation and decisions

Project-wide documentation and decisions belong here, in `.docs/` and `.docs/decisions/`. Anything
affecting one component only belongs to that component.

<!-- Say in one visible line if either folder does not exist yet, so nobody reports it as missing. -->
