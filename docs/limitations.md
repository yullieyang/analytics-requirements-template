# Limitations

This document is explicit about what this kit is and what it isn't, so
that no one — author, reviewer, or reader — overestimates what it
delivers.

## What this kit is

A small, opinionated set of Markdown templates and worked examples for
documenting analytical / model / data changes in a way that an analyst,
a developer, a QA reviewer, and an approving manager can all read off
the same page. The kit is documentation; it is not a tool.

## What this kit is not

- **Not a production system.** Nothing here is hardened, monitored, or
  maintained on a release schedule. The templates are versioned but
  the kit itself is not deployed software.
- **Not a tool stack.** The templates are Markdown so they work in any
  collaboration tool (GitHub, GitLab, Notion, a wiki). There is no
  workflow engine, no ticket integration, and no approval automation.
- **Not a substitute for analyst, developer, modeler, or reviewer
  judgment.** A signed reviewer checklist is the reviewer's call. The
  kit makes the call visible; it does not make the call.
- **Not a methodology document.** The kit describes the *shape* of a
  change request; the *content* of a change is methodology, which
  lives in the affected repository.
- **Not a sign-off ceremony.** The sign-off sections in the templates
  exist so the responsibility is visible, not to add procedural
  weight. If a release does not need a separate approving-manager
  sign-off, leave the row empty and say so.

## Specific limitations to keep in mind

1. **Templates can drift.** A template that is updated without bumping
   the matching worked example creates an inconsistency a reader
   will notice. The repository convention is: update both.
2. **Worked examples are fictional.** Every name, count, scenario, and
   date in `examples/` is illustrative. Do not cite them.
3. **The kit does not enforce versioning.** The mapping document has a
   versioning rule that says a new scenario triggers a version bump.
   The kit does not check that you actually bumped the version; that
   discipline lives with the analyst.
4. **Reviewer accountability is by name only.** The kit relies on
   reviewers filling in their name and date. There is no audit log
   beyond Git history.
5. **No data leaves the kit.** The kit ships no sample data and
   processes no data. It is documentation only.

## How to use this kit honestly

- Describe the repository as a **portfolio-style documentation kit**.
- Describe AI assistance as **drafting help, not authorship**.
- Describe the templates as **starting points** that the analyst,
  developer, and QA reviewer adapt to the specific change.
- Keep the "What this kit is not" framing visible in any derived
  workflow.
