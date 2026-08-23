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

**Check the scope is needed.** A project with one component and no second one planned has nothing for
a project scope to hold, because the registry is the reason it exists. Say so and offer the component
blueprint alone.

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

**Ask each component's posture while you are there.** One question per component: will an assistant
mostly change things in that folder, or mostly find them and leave them alone. Change writes
`Repository` into the block, keep writes `Assets` and the preserve rules with it. That word is the
only thing the component will ever be told about itself, so it is not optional and it cannot be left
for later.

**Ask about the session note only if the components cross a mount boundary.** Where to start a session
so that every component in the registry resolves is invisible in any file and cannot be inferred. If
everything sits on one side, delete the line.

**When there is a boundary, the note carries a second thing: what makes the local path true.** Resolve
the path yourself first, in the form you mean to write. If it holds because of a symlink, name the
symlink and give the command that creates it. A path that is true only on the machine it was written
on is the failure this whole address rule exists to prevent, and it is the one form of it that
survives every other check.

**Finish by saying what comes next.** List the components that are in the registry but not yet
attached, and name `new-component.md` as the prompt for each. A registry block with no stubs in the
folder is a map to a place that has never heard of the map.
