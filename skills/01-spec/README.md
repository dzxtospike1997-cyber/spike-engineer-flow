# 01-spec — spec stage

The entry for a new requirement: first interview to clarify and record decisions and terms, then write the formal spec.

- **`interrogate`** (landed): interviews the engineer to think a fuzzy requirement through, producing ADRs + a glossary as it asks; hands off to `spec` when done.
- **`spec`** (landed): turns the shared understanding into a formal spec — assigns each requirement a REQ-ID + acceptance criteria, and creates the `docs/traceability.md` matrix (with the `@req` / `@covers` annotation convention).
