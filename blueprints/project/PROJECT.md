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
> **Document Owner:** <DOCUMENT_OWNER>

---

# What this project is

<!--
A few sentences. Say whether the project is only software or whether software is one part of
something larger: an assistant that believes it is looking at a software project treats everything
else as out of scope.

Then the boundary. The second half matters more than it looks, and it is the only rule in this
framework proven to change what an assistant does: without it, a request the project excludes arrives
looking like ordinary work and gets done. "Does not currently" is deliberate. It records a present
boundary, not a permanent one.

Do not describe what the folders contain. An assistant can look.
-->

<PROJECT_PURPOSE>

This project does not currently cover <SCOPE_EXCLUDES>.

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

If the components sit on different sides of a mount boundary, two things go here and neither is
visible in any file.

Where to start a session so that all of them resolve.

And what makes the local path above true from there. A path under a synced store, reached from
another filesystem, usually holds because of a symlink somebody created once. Name it and give the
command, so a machine that lacks it can be fixed instead of failing quietly:

    `~/OneDrive` is a symlink to the Windows OneDrive folder, so the path above is true on both
    sides. Create it once on a machine that lacks it:

        ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive

Delete all of this if there is no boundary to cross.
-->

Address:

```text
<PROJECT_SCOPE_ADDRESS>
```

Local path:

```text
<PROJECT_LOCAL_PATH>
```

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
