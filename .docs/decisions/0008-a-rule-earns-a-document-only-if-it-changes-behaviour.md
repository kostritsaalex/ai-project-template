# 0008. A rule earns a document only if it changes behaviour

**Date:** 2026-08-29  
**Status:** accepted

---

## Context

[Decision 0004](0004-documents-carry-what-cannot-be-seen.md) gave the framework a razor and it cuts
one thing: facts. A document carries what cannot be seen, and the platform, the file layout and the
installed tooling all go, because an assistant can open the folder and look.

Rules are invisible by construction. Nothing is visible about "escape output at the boundary" the
way a `.git` folder is visible, so the razor never touches a rule, and since `0.6.0` the backlog has
carried the gap as an open item with a candidate test attached: **a rule earns a document only if an
assistant would do otherwise without it.** It was argued for and never run, which by this project's
own account is the state that produces wrong rules.

The subject was the `WordPress 7 Engine`'s `REPOSITORY.md`: nine bullets, eight of them ordinary
WordPress practice by the backlog's own description.

**The experiment.** Two copies of the component, differing in whether it has an override. The
difference is one variable rather than two: the file, and the three stub lines that name it, because
a component with no rules of its own does not carry lines pointing at rules it does not have. The
first attempt got this wrong, took the file away and left the stubs naming it, and measured a broken
component instead of the question. The arms were then confirmed identical by `diff -r` across both
trees rather than by construction, the entire output being the override and those three lines.

The task was chosen to be one somebody would plausibly ask for, since a task built to trip the
bullets proves only that they can be tripped: *add a list of the three most recently updated posts to
the footer of the site, with each title linking to the post.* It meets five of the nine bullets on
its own merits, because the active theme is third-party, is a block theme with no `footer.php`, and
the posts have to be queried and printed.

The interpretation was pre-registered before the control ran. Same work meant the bullets are
decoration; a difference meant the rule earned its keep; same work with no reason given was declared
in advance to be the first of those and not a third, because a framework that judges by the work
cannot credit a rule for an explanation no run gave.

**The result. The control did the same work.** Both arms wrote a plugin and left the third-party
theme untouched. Both reached for the Block Hooks API through the `hooked_block_types` filter, both
worked out independently that `block.json`'s `blockHooks` field cannot express a template-part area,
and both cited core by file and line while saying so. Both registered from `block.json` with a
server-rendered template and no build step. Both wrote `WP_Query` with the same nine arguments in the
same order; diffed, the two calls differ in a variable name and in where the post count comes from.

Escaping was the bullet neither summary settled and the one expected to differ. It did not. Both
escape the link with `esc_url`, print the title through `wp_kses_post` behind an identical
`wp_strip_all_tags` emptiness fallback, escape the heading with `esc_html`, and pass
`get_block_wrapper_attributes()` through with the same phpcs-ignore justification. The only asymmetry
is that the arm with the file exposes a post count as a block attribute and sanitizes it with
`absint` and a clamp, while the control hard-codes the count and so has no input boundary at all. A
different surface, not a different standard.

The control also named a reason, which the pre-registration had already refused to count as a third
outcome. The reason it named was the registry entry for the component: the parent, not the file under
test.

## Decision

**A rule earns a place in a document only if an assistant would do otherwise without it.**

This is the second razor, and it stands beside the first rather than replacing it. `0004` cuts facts.
This cuts rules. Between them nothing enters a document because it is true, sensible or good practice.

Applied immediately:

- **The Engine's nine bullets go.** The file goes with them, since nothing is left in it, and the two
  stubs lose the three lines that name it. That is the shape of the control arm, which is the one
  configuration in this experiment that has actually been run.
- **`blueprints/repository/platforms/wordpress.md` goes,** and the Repository Blueprint stops
  offering platform fragments. The `platforms/` folder is removed along with the four places that
  point at it.

**The prediction that follows, recorded so a future case can refute it.** Platform fragments are
decoration by construction. A platform rule is a rule about how one works with a widely used
platform, and that is exactly the kind of thing anyone competent at that platform already does. The
property that makes it a platform rule is the property that makes it decoration. An override should
carry only what is true of the particular folder: a generated directory, a vendored dependency, a
build output that is written rather than edited, how work here is verified. Not "escape output".

If a platform rule ever changes an assistant's work in a measured run, this prediction is wrong and
this record is where to say so.

**The registry's rule about platform core is not touched.** It was present in both arms, so the
experiment says nothing about it, and untested rules are not cut. The asymmetry with `0.6.0` is
deliberate and is the same principle in both directions: there, four preserve rules were cut for
never having been run; here, nine bullets are cut for having been run and made no difference. In
neither case did an argument decide it.

## Consequences

**The Release item asking where platform rules live is settled, and not by answering it.** It asked
for a mechanism: a platform rule follows from a platform rather than a folder, so a fragment gets
copy-pasted into every WordPress component and nothing owns it. The answer is that the rule does not
need to live anywhere, because it does not need to exist. A question about where to put something is
closed by finding that it should be thrown away.

**What ships gets smaller again, and this time in the part that varies.** The framework's fixed text
was already cut twice, by `0003` and `0004`. `Local rules` was the one section left where an owner
could write freely, and the blueprint had begun pre-filling it. It goes back to being empty by
default, which is what the blueprints always said it usually is.

**The accepted cost, stated plainly.** A person writing an override now has no ready-made source to
start from, so a folder with a genuinely non-obvious rule depends on somebody knowing their folder
well enough to write it. That is the right dependency and it is still a cost: the fragment was easy,
and easy is why it spread.

**The larger cost is that this razor is a prediction about a model.** "Would an assistant do
otherwise" is not a property of the rule; it is a claim about whoever reads it, and the answer can
change when the reader changes. A rule that is decoration for a capable model may not be for a weaker
one, or for the same model in a domain it knows less well, and nothing in this framework re-runs the
test. The first razor does not have this problem: what is visible in a folder stays visible.
Accepted, because a rule nobody follows and nobody notices is not free either, and because the
alternative is keeping every rule anyone ever proposed.

**On the evidence.** One task, one tool, one run per arm, in a domain the model knows well. WordPress
is among the best-represented stacks anywhere, which is the most favourable possible ground for the
conclusion that a WordPress rule is redundant, and the least favourable for the opposite.

The comparison was an override against no override, not a framework against none. The registry was
reachable in both arms and both carried its rule about platform core, and the control quoting that
registry entry back is what makes the distinction visible rather than a caveat asserted after the
fact. The layer the framework judges indispensable did fire. The layer under test did not.

**What remains untested is the whole category the first razor exists to protect.** Every bullet this
run touched was ordinary practice, so nothing here shows what happens when a rule is genuinely local:
that a directory is generated, that a dependency is vendored, that work in this folder is verified in
some particular way. Those are rules about something an assistant cannot otherwise know, they are the
reason `Local rules` exists at all, and the razor must not cut them. The experiment did not go near
them, so the razor is adopted on evidence from one side of its own boundary.

## Origin

Alex, 2026-08-29, on the day the experiment finally ran, after it had sat in the backlog since
`0.6.0` as the item with the most leverage on the list.

Two of his corrections shaped the measurement rather than the conclusion. The control had been
specified as the file "renamed away", and he accepted that this was the wrong control once the first
run spent its answer reporting a missing file: a component without rules does not carry lines
pointing at rules it does not have, so removing them is the same variable and not a second one. And
he required the arms to be confirmed by `diff -r` rather than by construction, on the grounds that
building two trees carefully is a story about what they hold and only a diff survives a result
somebody dislikes.

He also insisted the interpretation be fixed in writing before the control ran, which is why the
outcome that would have been most tempting to argue about afterwards, the control doing the same work
without naming a reason, was ruled out as a separate outcome in advance.
