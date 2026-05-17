# analytics-requirements-template

## Tagline

A documentation kit of five Markdown templates and four worked
examples for translating analytical / model / data changes into
reviewable technical requirements.

## Project overview

This is a portfolio-style documentation kit. It assembles the
artifacts an analyst, a developer, a QA reviewer, and an approving
manager all read off the same page during a recurring model or data
release: the change request, the data mapping, the developer handoff,
the QA acceptance criteria, and the reviewer checklist. Each template
is paired with a worked example so a first-time user can see the
expected depth and tone without inventing it. The kit is documentation
only — there is no tool, no workflow engine, and no data to process.

## Why this matters

Most failed releases in analytical workflows are not failures of code;
they are failures of context — an assumption that wasn't written
down, an edge case nobody flagged, a sign-off nobody recorded. A small,
consistent set of templates and a habit of filling them in catches
these problems before they show up in a production-style release.
The cost of adopting the kit is low (every template fits in a single
page); the cost of skipping it is the recurring chase for context
that should have lived in writing.

## What this project demonstrates

- A worked, opinionated answer to the analyst-to-developer-to-QA
  handoff problem.
- Discipline around documented assumptions, named edge cases, and
  pre-implementation acceptance criteria.
- A reviewable trail of named-human sign-offs for every release.
- Responsible use of AI coding tools as a drafting aid, with explicit
  guardrails on where AI does not belong.
- Documentation that travels — Markdown only, no tool lock-in.

## Repository structure

```
analytics-requirements-template/
├── README.md
├── .gitignore
├── templates/
│   ├── analytical_change_request.md
│   ├── developer_handoff.md
│   ├── qa_acceptance_criteria.md
│   ├── data_mapping_template.md
│   └── reviewer_checklist.md
├── examples/
│   ├── example_model_output_change_request.md
│   ├── example_data_field_mapping.md
│   ├── example_acceptance_criteria.md
│   └── example_release_review_notes.md
└── docs/
    ├── workflow_overview.md
    ├── responsible_ai_use.md
    └── limitations.md
```

## Workflow

The kit assumes a six-artifact sequence per release, in order:

1. **Analytical change request** — the analyst captures business
   context, the requested change, impacted fields, assumptions, open
   questions, risks, and the list of reviewers.
2. **Data mapping** — when the change touches a data product, the
   analyst documents the field-by-field mapping between source and
   target. One row per target field.
3. **Developer handoff** — the analyst (or analyst + developer)
   restates the change in implementation terms: inputs,
   transformation logic step-by-step, output requirements, edge
   cases, error-handling expectations, testing notes.
4. **QA acceptance criteria** — the analyst and the QA reviewer agree
   on the test cases, completeness checks, regression checks, and
   documentation checks *before* QA begins.
5. **Reviewer checklist** — the reviewer records the verdict
   (approved / approved with conditions / rejected) against every
   item in the checklist, with named follow-ups where applicable.
6. **Release review notes** — the analyst writes a short record of
   what changed, what didn't, the QA evidence, the risks raised, and
   any follow-ups that survive into the next release.

Each artifact narrows the scope of the next.
[`docs/workflow_overview.md`](docs/workflow_overview.md) explains why
the order matters.

## Data / inputs

The kit processes no data. The four worked examples under `examples/`
are entirely fictional — names, dates, scenario calibrations, row
counts, and reviewer outcomes are all illustrative. Nothing in the
repository is based on any real release, client portfolio, or
proprietary methodology.

## Methods

The kit is documentation, not code. The "method" is the shape of the
templates and the order in which they are filled in.

AI coding tools may support scaffolding, documentation review, and
consistency checks across templates, but the templates' content,
acceptance-criteria language, and reviewer checklists are
analyst-owned and independently verified. The kit itself does not
depend on or invoke any AI service; the templates work in any
Markdown editor. [`docs/responsible_ai_use.md`](docs/responsible_ai_use.md)
sets out the operating rules for using AI assistants alongside the
kit — including the parts of an analytical change request where AI
drafting does not belong.

## Outputs

The kit produces no outputs at runtime — it is a starting point. The
outputs are what you produce when you fill in a template:

- A signed change request document
- A versioned data-mapping document
- A developer-handoff document attached to a PR
- A signed QA acceptance-criteria document
- A signed reviewer checklist
- A release-review-notes record

Every output is Markdown and lives in Git.

## How to run

There is nothing to install or run. The repository is a kit of
Markdown files. To adopt the kit:

```bash
# Copy a template into the repository where the actual work lives.
cp analytics-requirements-template/templates/analytical_change_request.md \
   path/to/your/repo/docs/2026Q2-new-scenario.md

# Edit the copy, fill in the sections, commit alongside the change.
```

You can also clone this repository directly and copy files from it as
needed.

## Reviewability and documentation

- Every template ends with a reviewer sign-off block. No release is
  complete without a named reviewer and a date.
- Templates and worked examples are versioned together. A template
  bump triggers an example bump in the same commit.
- The "What this kit does not do" framing in
  [`docs/limitations.md`](docs/limitations.md) is intentional: the kit
  is explicitly *not* a tool, *not* a workflow engine, and *not* a
  substitute for reviewer judgment.

## Responsible use

- Treat AI-generated draft text as a draft. A human author edits and
  signs.
- Do not paste confidential, proprietary, or non-public data into
  external AI services as part of using this kit. The worked examples
  are fictional for that reason.
- Reviewer sign-off is by name only. The kit relies on the reviewer's
  discipline; there is no audit log beyond Git history.
- See [`docs/responsible_ai_use.md`](docs/responsible_ai_use.md) for
  the full operating rules.

## Portfolio Context

This project translates recurring patterns from analytical work —
analyst-to-developer handoff, documentation, acceptance criteria, and
reviewable technical requirements — into a public, fictional portfolio
prototype. The worked examples are entirely fictional and do not
replicate any proprietary system, internal workflow, or real release.
The goal is to demonstrate reproducible, reviewable workflow design
through documentation discipline.

## What this project does not do

- It does **not** ship a workflow engine, ticket integration, or
  approval automation.
- It does **not** enforce versioning, sign-off, or reviewer
  participation.
- It does **not** contain proprietary information, client identifiers,
  or non-public data.
- It does **not** make any business or modeling decisions.
- It does **not** replace analyst, developer, modeler, or reviewer
  judgment.
- It does **not** call any external AI or LLM service at runtime.
- It does **not** claim production readiness — it is a documentation
  kit, not a deployed system.

## Limitations

- **No enforcement.** The kit is discipline-by-template. If the
  analyst fills in a section with "TBD" and ships, the kit does not
  stop them.
- **No tooling integration.** A team that wants the change request to
  open a ticket automatically must build that integration themselves.
- **Templates drift.** Updating a template without updating the paired
  worked example creates a smell a careful reader will catch.
- **Worked examples are fictional.** They illustrate the expected
  depth and tone; they are not citable.

## Future improvements

- Add a `pre-commit` hook example that lints filled-in templates for
  obvious gaps (unfilled "TBD", missing reviewer name, untouched
  date).
- Add a versioned changelog for the templates so users can see which
  template version their copy was forked from.
- Add a small companion CLI that scaffolds a new release directory
  with the five-artifact sequence pre-populated.
- Add a second worked-example track for a data-only (no model) change.

## Skills demonstrated

- Translating recurring analytical workflows into reviewable
  documentation artifacts.
- Writing for an audience that spans analyst, developer, QA, and
  approving manager without losing precision.
- Documenting "what this is not" with the same discipline as "what
  this is".
- Embedding responsible AI-use rules into a workflow without writing
  prose disclaimers — the rules show up as named sections, sign-off
  blocks, and explicit out-of-scope items.

## Project summary

A Markdown kit of five templates and four worked examples that turns
an analytical change into a reviewable trail of signed documents
across analyst, developer, QA, and approving manager.

### Workflow summary

This is a documentation kit, not a tool. Five Markdown templates —
change request, data mapping, developer handoff, QA acceptance
criteria, reviewer checklist — paired with four worked examples that
show the expected depth. The order of the artifacts matters: each one
narrows the scope of the next, and each ends with a named human
sign-off. The kit does not enforce anything; it makes the discipline
visible. AI tools can draft the prose; they do not author business
logic or sign off.

### Design rationale

- **It captures the failure mode that most release-QA documents
  miss.** Releases fail on context that was not written down, not on
  code. The kit's value is the *order* of the artifacts: the
  acceptance criteria is written before QA begins, not after, so the
  analyst and QA reviewer agree on "done" up front.
- **It is honest about scope.** The kit is documentation, not a
  workflow engine. The README and `docs/limitations.md` say so
  explicitly.
- **It is explicit about scope for AI assistance.** The
  responsible-use doc names the places AI drafting earns its keep
  (boilerplate, consistency checks, drafting prose for a reviewer to
  edit) and the places it does not belong (business logic,
  methodology, sign-off language, and final acceptance criteria —
  all named humans).

### Honest limitations

- No enforcement — the kit is discipline-by-template, not a checker.
- No tool integration — teams wanting ticket-or-Jira automation build
  that themselves.
- Worked examples are fictional and illustrative — they are not
  reusable as-is for any real release.

## GitHub description

> Templates for analytical change requests, developer handoff, QA
> criteria, and reviewable documentation.

(112 chars.)
