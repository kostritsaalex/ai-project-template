# 0026. A record carries its subject only when the folder cannot

**Date:** 2026-09-05
**Status:** accepted

---

## Context

[`0025`](0025-a-decisions-folder-belongs-to-a-declared-component.md) allows a record about a
subfolder to live in the nearest declared scope's decisions folder until that subfolder is
promoted. One folder can therefore hold records about several subjects, and the present naming
convention, `NNNN-slug.md`, says nothing about which.

Three properties of the present convention are at stake. `handover.md:90`: *"`decisions/` is
newest last, one file per decision, and superseded records are marked rather than deleted."*
The 23 records here cite each other by bare number, 34 times. And a reader arriving at a
multi-subject folder is looking for a subject, not for a position in a sequence.

## Decision

**The filename carries the subject only when the folder cannot.**

A record about the folder's own scope is `NNNN-slug.md`, unprefixed. The folder already says
whose scope it is, and repeating that in every filename is writing the visible, which `0004`
forbids.

A record about a subfolder that has no component of its own is `<subject>-NNNN-slug.md`, where
`<subject>` is that folder's name as it sits on disk, lowercase, hyphenated.

**Numbering is per sequence, not per folder.** The scope's own records run `0001` upward. Each
subject runs its own `0001` upward. One folder may therefore hold several sequences.

**Citation.** A bare number inside the folder for the scope's own records, unchanged: `0007`. A
subject record by its full stem: `booking-0002`. Across a folder boundary, the path first.

**No `Subject` field.** The name has one carrier, and it is the filename, because a filename is
visible in a listing and in a citation and a field is visible in neither. Two carriers would be
one fact in two places, which principle 5 says will eventually disagree with itself.

## Options considered

| Option | What it buys | What it costs and how it fails | Decision |
| --- | --- | --- | --- |
| `<subject>-NNNN-slug.md`, per-subject counters | Listing groups by subject, so "what did we decide about booking" is two adjacent lines. Citations are self-describing across folders. **Records survive promotion without renumbering**, because the number was never the host's | "Newest last" stops being true for the folder and holds only inside a sequence, so a written rule has to be amended. Fails if a folder accumulates so many subjects that the grouping itself becomes the noise | **Chosen** |
| `NNNN-subject-slug.md`, one counter per folder | Strict chronology preserved; one sequence to reason about | Numbers belong to the host, so promotion forces renumbering and breaks every citation of the moved records. The path and the slug also disagree in a cross-folder citation, `wp-engine/0006-booking-...`. Fails at promotion, which `0025` expects to happen | Rejected |
| `NNNN-slug.md` plus a `Subject` field | Filenames unchanged; extraction is machine-readable by field | Subject invisible in a listing and in a citation; findable only by grep. Duplicates a fact the filename could carry. Same renumbering failure at promotion | Rejected |

The deciding property is the third line of the chosen row. Everything else is preference;
promotion is the event `0025` exists to make possible, and only one of these three survives it
intact.

## Consequences

**A written rule is amended, not quietly broken.** `handover.md:90` says `decisions/` is newest
last. After this record that is true inside a sequence and false for a folder holding more than
one. The line is edited in the same change that adopts this record. Leaving it would be a rule
disagreeing with practice, found later by whoever trusts it.

**Digits sort before letters, so the listing reads as an index.** The scope's own records come
first in order, then one group per subject. This is a property of ASCII ordering rather than
something the framework enforces, and a file manager sorting differently would lose the grouping
without losing anything else.

**The 23 records here are untouched, and not because renaming is expensive.** This folder has one
subject. A constant `ai-project-template-` prefix on 23 files would differentiate nothing, which
is the same razor that produced the rule.

**The cost is two forms where there was one.** Mitigated by the branch being determined rather
than chosen: the writer answers "is this record about this scope or about something inside it",
and `0025` already forces that question first. No judgement is added at writing time.

**Recovery.** Both directions are a rename. Collapsing to one form means prefixing or stripping
filenames and fixing the citations that point at them, which is mechanical and complete: nothing
outside the filenames and the links encodes the subject.

**Revisit trigger.** The first promotion that actually moves records, which is what tests the
zero-renumbering claim this record was decided on. If that promotion renumbers anything, the
reason it was chosen did not hold.

## Origin

The problem was raised by the owner in a working session, as the observation that a numbering
scheme was needed and that no good one was to hand. The `<name>-<ID>` shape is the owner's
proposal. The session first argued against it on sort order and on the cost of renaming 23
records and 34 links, and the owner rejected the cost argument as not a real constraint.
Re-argued on readability and on behaviour at promotion, the owner's shape won, and the
session's earlier position is the one that changed.
