# Responsible AI Use

This document describes how AI coding tools (e.g. Claude Code, GitHub
Copilot, similar pair-programming assistants) can support the workflow
in this repository, and where they should not be used.

## Where AI tools help

- **Drafting template language.** Filling in the prose of a change
  request, a handoff document, or a release review note. AI can
  produce a structured first pass that a human reviewer edits.
- **Consistency checks across documents.** Comparing a change request,
  the developer handoff, the acceptance criteria, and the reviewer
  checklist for the same release, and surfacing inconsistencies (a
  field mentioned in one document but not in the others; a test case
  listed in the acceptance criteria with no matching test in the
  implementation; an edge case described in the handoff but absent
  from the acceptance criteria).
- **Identifying missing acceptance criteria.** Given a change request
  and a draft set of acceptance criteria, asking the AI tool to list
  edge cases or regression checks that are not yet covered.
- **Improving documentation clarity.** Tightening passive prose,
  flagging undefined terms, suggesting where a "what this does NOT
  do" section is missing.

## Where AI tools do not belong

- **Authoring business logic.** The analyst owns the analytical
  intent. Letting an AI tool decide that "small balance gets a 150bp
  shift" is a hand-off of the very judgment the analyst is paid to
  make.
- **Authoring methodology.** Model methodology, calibration choices,
  identification assumptions, and statistical specifications stay
  with the modeler and are reviewed by the modeler's manager. AI can
  draft text that describes a methodology; it should not invent one.
- **Sign-off language.** Reviewer sign-off, conditional approval, and
  rejection language are the reviewer's. The reviewer's name appears
  on the record.
- **Final acceptance criteria.** The pass / fail rules for a release
  are agreed by the analyst and the QA reviewer. An AI tool may
  suggest additional cases; the analyst and QA reviewer decide which
  ones to commit to.

## Operating rules

The same posture applies whenever AI tools are used in or around this
kit:

1. **Treat AI output as a draft.** Every line authored or suggested by
   an AI tool must be read, edited, and committed by a named human.
2. **Source validation is required.** If an AI tool cites a number, a
   field name, or a piece of policy, verify it against the
   authoritative source before letting it land in a document a
   reviewer will sign.
3. **Uncertainty must be explicit.** Drafts produced with AI
   assistance should retain hedged language where the evidence is
   thin ("appears to," "is consistent with," "preliminary") rather
   than letting the model's confidence paper over it.
4. **No confidential or proprietary content in external tools.** Do
   not paste internal methodology, client identifiers, or non-public
   data into an external AI service unless your organization has an
   explicit approved channel for that. Use synthetic or fictional
   examples in this kit.
5. **The human is accountable.** A change request signed by a human
   reviewer is the human reviewer's document, regardless of whether
   an AI tool contributed to the draft.

## How this kit interacts with the wider portfolio

The companion repository
[`llm-research-workflow-assistant`](https://github.com/yullieyang/llm-research-workflow-assistant)
contains the reusable prompt templates and the human-in-the-loop
checklist that codify this posture. Combining the two:

- This kit (`analytics-requirements-template`) provides the **shape**
  of the documents the workflow produces.
- The companion kit (`llm-research-workflow-assistant`) provides the
  **prompts** an analyst can use when asking an AI tool to help
  draft, review, or audit one of those documents.

The two kits are independent and either can be adopted without the
other.
