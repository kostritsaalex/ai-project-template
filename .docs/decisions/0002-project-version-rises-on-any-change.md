# 0002. Project Version rises on any change

**Date:** 2026-08-15  
**Status:** superseded by [0003](0003-cut-the-framework-to-four-jobs.md), which removed version
counters and the sweep entirely. Kept as the record of why they existed and what replaced them: a
`Parent checked` date, itself removed in
[0005](0005-the-registry-carries-the-component.md).

---

## Context

`Project Version` was defined twice, and the two definitions disagreed.

`blueprints/project/README.md` said it "tracks this document's own evolution", which reads as any
change to `PROJECT.md`. The same section, and the header comment in `blueprints/project/PROJECT.md`,
said to raise it "whenever this document changes in a way a component would need to know about",
which adds a filter.

The two answers part company on the change that happens most often: a block added to
`Components & Resources` and nothing else. A new asset folder appears in the registry. The rules, the
priorities and the boundaries are untouched.

Under the first definition the version rises and every component gets swept. Under the second the
owner has to decide whether a repository cares that a sibling now exists, and the honest answer in
most cases is that it does not.

The filter was the newer of the two and it looked like the more thoughtful one. It is the one that
breaks.

## Decision

Raise `Project Version` on any change to `PROJECT.md`, including a change that only touches the
registry. Then work through every component: set its `Parent Project Version` to the new version,
compare the address it carries for the project scope against `Project Location`, and update its own
text where the change reaches it.

The filter is removed from both files.

## Consequences

The rule can be applied without judging another scope's interest. Guessing that interest was the
failure: a wrong guess leaves a component whose version matches the parent, which reads as
compatibility checked, when nobody looked.

Most sweeps now end with every component untouched except for one number. That outcome is the point
of the sweep rather than evidence it was unnecessary. The framework's own wording already anticipated
it: components are updated "either way, so a match records that compatibility was checked".

The cost is a pass over every component on a change that may affect none of them. It was weighed
against how often the shape of a project actually moves. Components are added and repositories
registered rarely, while work inside them is continuous, so the sweep fires on the order of a few
times a year rather than weekly.

The sweep now also verifies the parent address, which closes a failure neither check in
`blueprints/checks/` can see. `structure-check.md` validates the form of an address and is forbidden
by its own prompt from reading outside the folder. `cold-start-check.md` asks for the address to be
repeated and never resolves it. A component pointing at a location the project scope has moved away
from passes both and fails only when somebody follows it. Whether a third check should read both
sides is open.

## Origin

Discussion while designing the setup prompts, 2026-08-15. The collision surfaced when the prompt for
attaching a component had to be told what to do after writing a registry block, and the blueprint
gave two answers.
