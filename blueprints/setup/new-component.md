# New Component Prompt

Attaches a folder to a project. A codebase, a site, a folder of photography, the working material of
a workstream such as marketing or SEO: all the same operation, all this prompt.

It writes two stubs into the folder and one block into the parent registry. That is the whole job.

Run it on the first day of a project or years later. The prompt is the same either way, and an
existing folder answers most of the interview by itself.

Run it somewhere that can write to both the component and the project scope. The case that catches
people out is a folder inside a Linux environment on a Windows machine: its files have no drive
letter, and tools that address the machine by Windows path cannot see them. Use an assistant running
inside that environment, where both folders are ordinary paths.

---

## Prompt

Replace the three addresses before pasting. Copy from the raw text of this file, not from the
rendered page.

```text
Attach a component to a project using the AI Project Template framework: a library of blueprints for
organizing project documentation and AI instructions.

The framework is here:
<path to a local checkout, or https://github.com/kostritsaalex/ai-project-template>

The component is here:
<path to the folder being attached>

Its parent project scope is here:
<path to the folder holding PROJECT.md>

Read these two files in the framework and follow them:

- blueprints/setup/procedure.md, the whole file
- blueprints/setup/new-component.md, the section "Notes for this scope"

Interview me as the procedure describes, then write the files.
```

---

## Notes for this scope

**Blueprint:** `blueprints/component/`  
**Files written into the component:** `AGENTS.md` and `CLAUDE.md`, identical apart from the heading.  
**Files written into the parent:** one block in the registry.  
**Depends on:** an existing project scope, whose address this copies.

**If no project scope exists,** stop and say `new-project.md` runs first. A component with no parent
is not covered: the parent is the only thing it is told about.

**Attach the folder you were given and no other.** Subfolders inside it are not components and are
not candidates. They are files, and they take this component's posture.

**The interview is three questions.** What this component is called, which posture the folder has,
and whether it has any rule of its own yet. The name and the address you already have from the
prompt; confirm the name rather than asking for it blind.

**The posture question, asked plainly:** in this folder, will an assistant mostly change things, or
mostly find them and leave them as they are. Change is `Repository`. Keep is `Assets`, and the
preserve rules go into the registry block with it.

Do not ask what the folder contains, what platform it runs, or whether it is under version control.
None of that decides the posture and all of it is visible.

**A rule of its own is the exception, not the expectation.** Ask once. If the answer is no, which is
usual, the component gets two stubs and nothing else, and you are done. If the answer is yes, add
`REPOSITORY.md` or `ASSETS.md` from the matching override blueprint and use the stubs from that
folder instead, which carry one extra line pointing at it.

**Then wire it.** Step 7 of the procedure. Both halves or neither: a stub with no registry block
leaves a folder claiming a parent that has never heard of it.
