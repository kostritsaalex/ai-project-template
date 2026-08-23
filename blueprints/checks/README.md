# Adoption Checks

Two prompts for verifying a blueprint after it has been adopted. They apply to every blueprint, so
they live here rather than being repeated in each one.

| Check | Question it answers | When to run |
| --- | --- | --- |
| [Structure check](structure-check.md) | Are the files filled in correctly? | Right after adoption. Any session. |
| [Cold start check](cold-start-check.md) | Does an assistant opening this folder actually pick up the context? | Once the structure check passes. New session only. |

Run them in that order. The structure check finds leftovers and broken addresses in a minute, and
there is no point testing behavior while a placeholder is still sitting in the file.

---

## Why two

They fail differently, and each one is blind to the other's failures.

The structure check is mechanical. Every row is a quote you can open and verify, so its result does
not depend on the tool's judgment.

The cold start check is behavioral. Nothing about it is mechanical, which is why its conditions are
strict: a new session, no hints, sources named for every answer. Loosen any of them and it returns
a comfortable answer that means nothing.

---

## What neither check covers

Whether the content is right. Both checks confirm the machinery works: the addresses resolve, the
stubs point where they should, the assistant follows the chain. Whether a component was given the
right posture, or the platform rules match how the team actually works, is a question for whoever
owns the document.

Neither sees a component that exists on disk and appears in no registry. The structure check reads
one folder and the cold start check starts from one folder, so a folder nobody attached is invisible
to both. A prompt that reads a project and its components together is the obvious gap.
