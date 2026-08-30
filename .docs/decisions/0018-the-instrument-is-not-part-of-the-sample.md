# 0018. The instrument is not part of the sample

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

`registry-check` declares a read set — this scope's own root, and the root of each folder the registry
names — and row 7 audits it by listing every folder the session opened and classifying each. That row
is the only self-audit any check in this framework has.

**It has failed twice for a reason that has nothing to do with the project under check.**

**Instance 1, the operator's path-load run, 2026-08-30.** The check was loaded by giving its path, so
the session had to open `blueprints/checks/registry-check.md` in order to learn the procedure. That
file is not in the read set, so row 7 named it and failed. Recorded at the time in the `0.14.0`
changelog entry under *Known, deferred, not fixed here*, and in the backlog: *"The instruction telling
the operator to paste the text sits inside the file, reachable only after the rule has already been
broken."* The instruction to paste rather than to load is real and correct, and it is unreachable
until after the reader has done the thing it forbids.

**Instance 2, the Codex run, 2026-08-30**, reported by the operator, who confirmed the folder's
contents. The same check text was run through a different agent in a different ecosystem with **no
knowledge of this framework**. Rows 1 through 6 produced **identical verdicts** to this project's own
runs, including the *declared, not attached* outcome and both cascade branches. **Row 7 failed**,
naming `/home/kostritsaalex/.codex/attachments/<uuid>` — that harness's own storage, holding the
pasted prompt it had spooled to disk.

**The second instance is what turned this from a local annoyance into a property of the check.** One
operator loading a file the wrong way in one tool is a mistake to correct in the operator. The same
row failing, from a harness this framework has never seen, reached by no route this project controls,
on an unchanged scope, is the check counting the instrument as part of the sample. Two independent
observations, two ecosystems, one shape.

Rows 1 through 6 agreeing across ecosystems is a separate finding and belongs beside it: the check's
text reads the same way outside the framework that produced it.

## Decision

**The read set governs what a check consults about the project under check. Material that exists only
because of how the check's own text reached the session is outside it.**

That covers exactly two things: the check's own file, when the session was given its path instead of
its text, and a harness's attachment or spool storage holding the pasted prompt.

**The exemption covers the check's own instructions and nothing else.** A file belonging to the
project under check is judged by the read set exactly as before, wherever it sits, and so is every
other file of this framework — the other checks, their README, the blueprints. Reading one of those
is a third-class read and fails row 7.

**Exempt is not invisible.** Row 7 still lists it. The exemption adds a fourth class to the three that
row names, and a read in it is a pass. This is the whole difference between an exemption and a blind
spot: a rule that let the session drop the read from the list would have attacked the one thing row 7
cannot see, which is a folder opened and left off.

## Where it is written, and where it is not

**The read set is declared per check, three times, and audited once.** This was established by reading
the files rather than assumed, after three consecutive wrong guesses about this check's internals:

- [`0009`](0009-a-check-declares-its-read-set-in-advance.md) states the **rule** — a check declares its
  read set in advance, computable from documents before any file is opened. It is a decision record.
  No session running a check ever reads it.
- `structure-check.md` declares one folder's root, in the prompt, as *"Do not read anything else."*
  **No row audits it.**
- `registry-check.md` declares the scope root plus each registry-named root. **Row 7 audits it.**
- `cold-start-check.md` declares **none**. Following the chain outward is what it measures.

**The change goes into `registry-check.md` alone.**

It is the check that failed, twice, and the only one with a row for the exemption to act on. Put into
`structure-check.md` the same words would be a clause that **cannot execute**: its prohibition is real
and loading that check by path breaks it identically, but nothing there reports what was opened, so
no output would differ. This project's release procedure already treats a clause that shipped without
executing as a thing to name and be uneasy about; writing one deliberately is worse. It is available
the day `structure-check` grows an audit row.

`cold-start-check` has no read set, and its analogous hazard — being handed a path — is already
covered under its own name, as a **hint**, which its Conditions section forbids in its own words.

`0009` is not edited. It says what kind of thing a read-set declaration is, and that is unchanged:
the set is still computable from documents before any file is opened. This record says what the set
is a set *of*.

**The accepted cost:** if `structure-check` ever gains an audit row, this rule is written a second
time and the two can disagree. Principle 5 says so plainly. Taken anyway, because the alternative is
shipping text into a check where nothing can run it.

## Weakening row 7 was considered and rejected

The cheaper repairs were on the table and all of them cost the row its edge.

**Permitting any folder the session opened before reading the prompt.** This would have covered both
instances in one clause and would also have covered a session that browsed the project first and read
the check afterwards — the exact shape of the defect row 7 exists to catch, wearing an alibi about
ordering.

**Dropping the "without exception" listing requirement for reads the session judges irrelevant.** The
row's own text says *"A folder you opened and left off the list is the failure this row exists to
catch and the one thing it cannot see."* Any rule that removes something from the list attacks that
sentence.

**Making row 7 advisory, or a warning rather than a failure.** Its verdict is the reason the rest of
the table can be trusted: *"a table that fails it should not be trusted on any other row."* An
advisory self-audit audits nothing.

**Row 7 has one confirmed true positive on its record** — `/home/kostritsaalex/Projects`, the common
parent of both component paths, read by one command that tested both, on 2026-08-30, which produced
`0.15.0` and [`0017`](0017-a-probe-covers-one-declared-path.md). **Adjusting an instrument immediately
after its first correct reading is a failure this project has already recorded once**, and it was
refused then for the same reason it is refused here. The instrument reads correctly. What was wrong
is the definition of what it was reading.

**Row 7's text is not touched by this change.** The fourth class is added in the read-set declaration,
which is where the read set is defined, and the row inherits it.

## Consequences

**Loading the check by giving its path becomes a supported way of running it.** That is the finding's
practical shape: the operator's original mistake was never a mistake about the project, and the check
now says so. `How to run` still recommends pasting the raw text, which remains good advice for a
different reason — a rendered view eats the characters the prompt needs.

**A row 7 class that rests on the session's own account.** *"Whatever you read only because of how
this check's text reached you"* is a fact about the session's history, not about the filesystem. Every
other class in row 7 can be opened and verified against `PROJECT.md` by the person reading the table.
This one cannot. It is accepted because the alternative — an exemption keyed on a path pattern — would
have to name `.codex/attachments` and whatever the next harness calls its spool, and would be wrong
the day after it shipped.

**Half of this change is argued rather than measured, and will stay that way until the operator
re-runs Codex.** Three `claude -p` arms executed the path half: the control is unmoved, the path load
now passes row 7 **naming the file**, and a disclosed plant still fails the row and still names the
folder. **Claude Code does not spool a pasted prompt to disk**, so the spool half of the exemption
cannot be executed in this ecosystem at all — which is exactly why the second instance had to come
from another one.

**A check's evidence about itself got longer, not shorter.** The path-load run now reports one more
opened path than the same run reported before, because a read that used to be a bare failure is now a
classified entry. That is the direction this framework wants: the fix added a class, not a silence.

## Origin

Alex, 2026-08-30, on running the shipped check text through Codex — an agent in another ecosystem
with no knowledge of this project — and reporting that rows 1 to 6 agreed exactly while row 7 failed
on that harness's own attachment folder.

The framing is his: the check's own delivery is not project material, so the instrument should not be
counted as part of the sample. Naming the second instance as evidence about the *check* rather than
about *Codex* is what made it a rule instead of a workaround.
