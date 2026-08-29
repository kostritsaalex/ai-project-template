# New Project Prompt

Sets up a project scope by adopting the Project Blueprint through a short interview.

Run this before any component prompt. Components copy an address that only exists once this scope
publishes it.

---

## Prompt

Replace the two addresses before pasting.

```text
Set up a project scope using the AI Project Template framework: a library of blueprints for
organizing project documentation and AI instructions.

The framework is here:
<path to a local checkout, or https://github.com/kostritsaalex/ai-project-template>

The project scope goes here:
<path to the folder that will hold PROJECT.md>

Read these two files in the framework and follow them:

- blueprints/setup/procedure.md, the whole file
- blueprints/setup/new-project.md, the section "Notes for this scope"

Interview me as the procedure describes, then write the files.
```

A local checkout is the reliable form. Reading from GitHub works only where the assistant can fetch
raw files, and not at all for a private copy.

---

## Notes for this scope

**Blueprint:** `blueprints/project/`  
**Entry point:** `PROJECT.md`  
**Depends on:** nothing. Run this first.

**Check which state the project is in.** A folder with nothing settled enough to write down and no
second place in sight needs no documents at all, and saying so is a better answer than an interview.
A project that has settled on something and still lives in one folder takes this scope with an empty
registry, and that is a finished setup rather than half of one. So does a project that has recorded
nothing yet and knows a second place is coming. A project already working in a second place takes
this scope and a component for each place.

Never offer the component blueprint instead of this one. A component with no parent is not covered,
and `new-component.md` sends the person straight back here.

**Fill the address first.** Every component copies it. Written wrong, each of them knows a parent
exists and cannot reach it.

**The root holds `PROJECT.md` and its two adapters and nothing else.** Components inside this folder
occupy their own subfolders and carry their own stubs there.

**Say what a component is before asking for the first one.** A folder belonging to this project,
whether code or material; this folder is not one, it is the project scope. Without that sentence the
person counts the project folder as component one and has to correct themselves mid-block.

**Ask which folders they declare, and take the answer as complete.** Do not walk the tree looking
for candidates and do not offer any. A folder they did not name is files inside whichever component
contains it. This is also the answer to "should this folder be one component or several": neither,
until they say.

**Settle each component's posture while you are there.** The word is settled by one question:
**does this folder contain code that something other than a person replaces wholesale — a platform, a
framework, a package manager, a generator?** If yes, `Repository`, and the rule about core goes into
the block with it. If no, `Assets`, which adds nothing to the project's principles.

**A folder of your own source code is `Assets`, even when it is a git repository.** `Repository` is
not about version control and not about where the folder is stored. It marks a folder whose contents
an updater owns, so that hand edits to that code would be overwritten. This framework's own adopted
registry carries a folder of theme source code as `Assets` for exactly that reason.

You cannot look inside a component you have not been given, so propose from what the person has told
you and show the word in the summary table as settled, where it can be overturned in a sentence. That
word is the only thing the component will ever be told about itself, so no block is written without
one.

**Settle the path note whatever the components turn out to be.** Resolve the local path yourself
first, in the form you mean to write. If it holds because of a symlink or a mount, name the
arrangement and give the command that creates it. This has nothing to do with components: a project
living in one folder reached through a mount needs the line just as much. A path that is true only on
the machine it was written on is the failure the whole address rule exists to prevent, and it is the
one form of it that survives every other check.

**Ask about the session note only after the components are named,** and only if any of them sits on
the far side of a mount boundary from this folder. Where to start a session so that every component
resolves is invisible in any file and cannot be inferred, and it cannot be decided before you know
what has to resolve. If everything sits on one side, delete the line and say that adding a component
elsewhere brings it back.

**Finish by saying what comes next.** List the components that are in the registry but not yet
attached, and name `new-component.md` as the prompt for each. A registry block with no stubs in the
folder is a map to a place that has never heard of the map.
