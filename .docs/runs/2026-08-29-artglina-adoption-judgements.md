# ArtGlina adoption: judgements made without being asked

Kept as the run goes, not reconstructed afterwards. A judgement made because the interview did not
raise it is invisible in the finished documents, and reconstruction from memory is the failure mode
this repository catalogued on 2026-08-29.

**Status: the run this log belongs to was discarded and is not the adoption that happened.**

It reached Step 4 and was discarded there. No interview answer was ever received, no summary table was
confirmed, and no document was written: nothing exists in ArtGlina that this run produced. A later
reader should treat everything below as belonging to a survey, not to an adoption.

**Why it was discarded.** By the end of Step 2 the session had established, from its own search,
that framework documents existed in three folders besides the scope, that one of them was an
`ASSETS.md`, and that two `REPOSITORY.md` files matched byte for byte. That is most of what the
adoption was supposed to derive from the owner and from the folders. Knowing the shape of the answer
is not the same as being told it, but it is close enough that the run could no longer be called
blind, so it was stopped rather than continued on a weakened premise.

The findings below stand on their own, because none of them depended on the adoption completing: the
Step 6 conflict, the component-identity question now in the backlog, and the judgements themselves.

## The blindness of the replacement run is bounded by an instruction, not by the disk

The deletion is real: `artglina-ua`, `artglina-sandbox` and the scope root are all clear of framework
documents, and `Artglina/Unsorted` no longer holds any. But `artglina-ua` is a git repository, so the
documents survive in its history along with the commit that removed them.

Checked here by subject line only, no diff opened: **three consecutive commit subjects are legible to
anyone running `git log` in that folder**, and one of them names where the project scope lives. So the
leak is not the single removal commit; it is a short run of subjects, one of which carries adoption
content outright.

**The subjects are deliberately not reproduced in this file.** This log lives in the framework
repository, which the replacement session must read in order to read the blueprints, so quoting them
here would move the leak from a place that session is told to avoid into a place it is required to
open.

What protects the replacement run is therefore an instruction — do not read any folder's history, and
say so if you meet a trace anyway — and not the state of the disk. That is a weaker guarantee than
deletion and it is declared rather than pretended away: a session that runs `git log` for an ordinary
reason, or a tool that surfaces recent commits unbidden, defeats it without anyone intending to.

---

**J1. I looked for the scope folder instead of asking for it.**
`procedure.md` Step 1 says "The prompt that sent you here carries an address for the framework and
for each folder involved." The task prompt named ArtGlina and gave no address for it. I searched by
name rather than opening with a question, so that the question I asked could be concrete.

*Why it matters:* the framework's setup path assumes the address arrives with the prompt, and
`new-project.md`'s pasteable template has a `<path to the folder that will hold PROJECT.md>` slot for
exactly this. A prompt that names a project without its address is outside what the procedure
expects, and the procedure does not say what to do about it. I chose to look; asking first was
equally defensible.

**J2. I checked for existing instruction files by filename and metadata only, never by opening
them.**
Step 2 point 3 requires establishing "whether other AI instruction files are present, of this
framework or another". The task forbids reading any surviving old document. `ls`, `find` and `stat`
satisfy the first without breaching the second.

*Why it matters:* this is only possible because Step 2's question is about presence. Step 6's is not
— see the finding below — and no reading-free method satisfies that one.

**J3. I did not assemble a list of candidate components from the tree.**
The search for the project's name returned several folders that hold framework documents. Under
`procedure.md` Step 4 and `new-project.md`, "a folder is a component because somebody says so, never
because you noticed it", so none of them is treated as a component and none will be offered as one.
They are reported below as documents found, which is a different claim.

**J4. The interview was batched at the owner's request, and that is not the blueprint's shape.**
He asked for every question in a single list, answered in one message, with any question opened by an
answer going into a second list. `procedure.md` Step 4 already says to "ask in one block, not one
question at a time", so the two agree on the first round. Neither says what the second round is, and
the blueprint only implies one: it defers the session note until after the components are named,
which cannot happen in the same block that asks for them.

*Why it matters to a later reader:* **a batched interview and a conversational one are not the same
instrument.** A conversation lets a puzzled answer be chased on the spot, and a batch does not, so a
thin answer stays thin until the next round and an ambiguity travels into the summary table. Anything
this adoption gets right or wrong about the interview was got with the batched form, and the shape
`procedure.md` describes should not be assumed from it.

---

# Finding that stopped the run

**The old documents were not deleted.** The task states they were being deleted before the run. All
of them are in place. Listed by name and size only; none was opened.

| Folder | Documents present | Size / date |
| --- | --- | --- |
| `OneDrive/Projects/All/Artglina/` | `PROJECT.md`, `AGENTS.md`, `CLAUDE.md` | 8313 bytes, 2026-08-16 |
| `OneDrive/Projects/All/Artglina/Unsorted/` | `AGENTS.md`, **`ASSETS.md`**, `CLAUDE.md` | |
| `~/Projects/All/artglina-ua/` | `AGENTS.md`, `CLAUDE.md`, `REPOSITORY.md` | 6513 bytes, 2026-08-16 |
| `~/Projects/Development/artglina-sandbox/` | `AGENTS.md`, `CLAUDE.md`, `REPOSITORY.md` | 6513 bytes, 2026-08-09 |

Two things beyond the deletion not having happened.

**The task said "its one component's override".** Three folders besides the scope carry framework
documents, and two of them carry a `REPOSITORY.md` of identical size.

**One of them is an `ASSETS.md`.** `handover.md` records that "the assets override, `ASSETS.md`, has
never been used at all". A file of that name exists here. It may be the pre-`0.5.0` `ASSETS.md`,
which was an entry point before `0005` demoted it to an override, in which case the record is right
about the current file and wrong-sounding about the name. That cannot be settled without opening it,
which this run must not do.

---

# The conflict this exposes, which is a finding about the framework

**`procedure.md` Step 6 cannot be satisfied blind.**

> If a file you are about to write exists, show what is there and ask before overwriting.

Showing what is there means reading it. A blind adoption over a folder that still holds its old
documents cannot obey that rule and stay blind. The two requirements are individually right and
jointly unsatisfiable, and nothing in the framework says which yields.

Step 2's version of the question — *whether* instruction files are present — is answerable without
reading, and that asymmetry is the whole of the difference. Step 2 asks for presence; Step 6 asks for
contents.

This is not a reason to change anything yet. It is the first time the procedure has met a folder it
was asked to adopt without being allowed to read, and one instance is one instance.

---

# Resolved since the stop

**The two `REPOSITORY.md` files of identical size are two clones of one repository.** Confirmed by
the owner running `git remote` and `git ls-files` in each, not by this session inferring it from the
matching byte count. Both working copies have origin `git@github.com:kostritsaalex/artglina.com.ua.git`
and both track their stubs. No document was opened to establish this.

The framework question it raises — whether a component is a folder or a repository — is recorded in
the backlog as an open question with both readings, and is not settled here. An adoption is the wrong
place to decide what a component is.

It does bear on the adoption still to come, in one practical way: if the owner declares one of these
copies a component, the answer to "where is it" is a repository URL and a local path, and which copy
the local path names is a question the interview has to ask rather than assume.
