# WordPress Platform Fragment

**Fragment Version:** 0.1.0  
**For:** Repository Blueprint `0.2.0`  
**Applies to:** WordPress, with optional WooCommerce

Copy the section below into `Platform Principles` in the adopted `REPOSITORY.md`, replacing the
`<PLATFORM_PRINCIPLES>` placeholder and the comment above it. Drop the WooCommerce lines if the
repository has no store.

---

```markdown
# Platform Principles

- Never modify WordPress core or third-party plugin code.
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

The first rule carries most of the weight. Editing core or a plugin works until the next update
silently reverts it, and the assistant has no way to see that from the files.

The last two rules stay general on purpose. Function names change between platform versions, so the
principle survives longer than a list of names would.

Keep the fragment short. Detailed conventions belong in the repository's own `.docs/`, where they
can be read only when relevant.
