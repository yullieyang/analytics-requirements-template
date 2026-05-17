# Workflow Overview

This repository is a documentation kit. It assembles five templates and
four worked examples into a single shape that an analyst, a developer,
and a QA reviewer can all read off the same page. The shape is
deliberately simple: every change goes through the same six artifacts,
in the same order, and is signed off in the same way.

## Roles

- **Analyst.** Authors the change request and the data mapping. Owns
  the analytical intent. Signs off on the implementation matching that
  intent.
- **Developer.** Authors the implementation against the developer
  handoff document. Owns the code. Signs off on the QA evidence.
- **QA reviewer.** Authors the acceptance criteria with the analyst,
  runs them against the implementation, and produces the reviewer
  checklist record. Owns the release sign-off.
- **Approving manager.** Reads the final reviewer checklist and signs
  off (or rejects with conditions) on the release as a whole.

## Artifacts, in order

1. **`templates/analytical_change_request.md`** — authored by the
   analyst when a change is first scoped. Captures business context,
   the requested change, impacted fields, assumptions, open questions,
   risks, and the list of reviewers.
2. **`templates/data_mapping_template.md`** — authored alongside the
   change request when the change touches a data product. One row per
   target field. Versioned independently from the change request.
3. **`templates/developer_handoff.md`** — authored by the analyst (or
   the analyst with the developer) once the change request is
   approved. Restates the change in implementation terms, listing
   inputs, transformation logic step-by-step, output requirements,
   edge cases, and testing notes.
4. **`templates/qa_acceptance_criteria.md`** — authored by the analyst
   and the QA reviewer *before* QA begins. Lists every test case with
   a pass rule, completeness checks, regression checks, and the
   documentation that must be in place at sign-off.
5. **`templates/reviewer_checklist.md`** — authored by the reviewer
   during QA. References the four prior documents and records the
   reviewer's verdict (approved / approved with conditions / rejected)
   with named follow-ups.
6. **A release review notes record** — written once the release ships,
   summarizing what changed, what didn't, the QA evidence, the risks
   raised, and any follow-ups that survive into the next release.
   `examples/example_release_review_notes.md` shows the shape.

## Why this order

The order matters. Each document narrows the scope of the next:

- The **change request** is the broadest. It describes intent and
  business context that subsequent documents do not duplicate.
- The **data mapping** is the most concrete. It fixes the field-level
  schema before any implementation begins.
- The **developer handoff** is the most procedural. It restates the
  change as a numbered sequence of operations.
- The **acceptance criteria** are the most testable. They are written
  *before* the implementation so the analyst and QA reviewer agree on
  what "done" means.
- The **reviewer checklist** is the audit record. It does not
  re-author the change; it records that the change was implemented as
  documented.

Skipping a document or writing it after the fact is a smell. The
reviewer checklist that is written after the release shipped is no
longer a reviewer checklist; it is a memo.

## What the templates intentionally don't do

- They don't define business logic. That lives in the change request
  and the methodology note (in the affected repository).
- They don't replace conversation between analyst, developer, and
  reviewer. They make the conversation more efficient.
- They don't enforce a tool stack. The templates are Markdown so they
  work in GitHub, GitLab, Bitbucket, Notion, or a wiki. The repository
  doesn't depend on any infrastructure.

## How to use the repository

- Copy a template into the repository where the actual work lives;
  fill it in there.
- Reference the worked example under `examples/` if you are unsure
  about the level of detail expected.
- Keep the template versioned: a bump to the template should also
  bump the worked example so the two stay in step.
- Treat the repository as a kit. If you find a missing section while
  using a template, update the template here and add or update the
  matching worked example.

## Where AI-assisted tooling fits

See [`responsible_ai_use.md`](responsible_ai_use.md). AI coding tools
are useful for drafting template language, checking consistency across
related documents, identifying missing acceptance criteria, and
improving documentation clarity. AI should not author business logic,
methodology, or sign-off language. Every document in this kit ends
with a human reviewer's name and date.
