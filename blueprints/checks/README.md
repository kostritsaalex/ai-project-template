# Adoption Checks

Three prompts for verifying a blueprint after it has been adopted. They apply to every blueprint, so
they live here rather than being repeated in each one.

| Check | Question it answers | When to run |
| --- | --- | --- |
| [Structure check](structure-check.md) | Are the files filled in correctly? | Right after adoption. Any session. |
| [Cold start check](cold-start-check.md) | Does an assistant opening this folder actually pick up the context? | Once the structure check passes. New session only. |
| [Registry check](registry-check.md) | Do the components still match what the registry says about them? | From the project scope, once its components are attached. |

Run the first two in that order. The structure check finds leftovers and broken addresses in a
minute, and there is no point testing behavior while a placeholder is still sitting in the file.

The registry check is not part of adopting one folder. It runs from the scope, over everything the
registry declares, and it is the one to run again later: the others answer whether a folder was set
up correctly, and this one answers whether that is still true.

---

## Why three

They fail differently, and each is blind to the others' failures.

The structure check is mechanical. Every row is a quote you can open and verify, so its result does
not depend on the tool's judgment.

The cold start check is behavioral. Nothing about it is mechanical, which is why its conditions are
strict: a new session, no hints, sources named for every answer. Loosen any of them and it returns
a comfortable answer that means nothing.

The registry check is relational. It is mechanical like the first, but it compares two documents in
two folders rather than auditing one, which is why it is the only check that reads outside the folder
it is run in. What lets it do that without becoming unbounded is that its read set is computable
before it opens anything: this scope's root, and the root of each folder the registry names. See
[decision 0009](../../.docs/decisions/0009-a-check-declares-its-read-set-in-advance.md).

---

## What neither check covers

Whether the content is right. Both checks confirm the machinery works: the addresses resolve, the
stubs point where they should, the assistant follows the chain. Whether a component was given the
right posture, or the platform rules match how the team actually works, is a question for whoever
owns the document.

None of them sees a document contradicting another document in the same scope, or a document's
claim about its own files. Those are outside every read set a registry can compute, so no check here
will find them, and the instrument for them is somebody reading. The backlog carries that separately.

A folder that appears in no registry is not a gap either. It is not a component at all, by the rule
in [decision 0005](../../.docs/decisions/0005-the-registry-carries-the-component.md), so there is
nothing for a check to find.
