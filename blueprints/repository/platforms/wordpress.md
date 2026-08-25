# WordPress Platform Fragment

**Fragment Version:** 0.2.0  
**For:** Repository Blueprint `0.6.0`  
**Applies to:** WordPress

Copy the block below into `Local rules` in the adopted `REPOSITORY.md`, replacing the `<LOCAL_RULES>`
placeholder and the comment above it. Drop the lines that cannot fire on work done from that folder.

---

```markdown
- Third-party plugin and theme code is owned by its updater. Extend it through hooks rather than
  editing it.
- Prefer hooks, filters and documented extension points.
- Prefer native platform functionality when it is sufficient.
- Avoid adding a plugin when a small, maintainable implementation will do.
- Keep business logic separate from presentation where practical.
- Minimize dependencies and preserve upgrade compatibility.
- Follow existing repository patterns unless there is a clear reason to improve them.
- Escape output and sanitize input at the boundary, using the platform's own functions.
- Route database access through the platform's data layer instead of raw queries where practical.
```

---

## Notes

**The rule about WordPress core is not here, and must not be added.** Since `0.6.0` the word
`Repository` in the parent registry carries it: platform or framework core changes only through its
own update mechanism, never by hand. Writing it here as well puts one rule in two places. The first
line above covers what the registry's rule does not, which is third-party code shipped inside the
installation rather than the installation itself.

**The axis is ownership rather than immutability.** Core and third-party code do change; they change
when their updater replaces them. A hand edit in the same files is undone by the next update, and an
assistant has no way to see that from the files.

**Keep the fragment short.** Detailed conventions belong in the repository's own `.docs/`, where they
can be read only when relevant.

**Most of this list is ordinary WordPress practice.** Whether a rule an assistant would follow
anyway earns a place in a document is an open question in this framework, and this fragment is the
natural place to settle it: run one real task with the file and one without, and judge by the work.

**Version history.** `0.1.0` targeted Repository Blueprint `0.2.0` and told its reader to fill a
`Platform Principles` section and a `<PLATFORM_PRINCIPLES>` placeholder, neither of which has existed
since `0.5.0`. It stayed that way for three releases and produced no error when used: an assistant
told to apply it mapped the names onto the current ones silently and said nothing. A stale fragment
gives no signal, which is why this one now carries the blueprint version it was written against.
