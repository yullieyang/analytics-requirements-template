# Developer Handoff — Template

> Use this template when a change request has been approved and is
> being handed off to a developer for implementation. Pair this with
> the originating change request; do not duplicate context.

---

## 1. Summary of requested change

_One paragraph. Restate the change in implementation terms._

## 2. Linked change request

_Path or link to the corresponding `analytical_change_request.md`._

## 3. Input data requirements

_For each input the implementation needs:_

| Input | Source | Frequency | Schema | Owner |
|-------|--------|-----------|--------|-------|
| _e.g. `quarterly_model_run.csv`_ | _internal model team_ | _quarterly_ | _10 cols; see linked dictionary_ | _modeler name_ |

_State explicitly which fields are required vs optional, and what the
implementation should do if an optional field is absent._

## 4. Transformation logic

_Describe the transformation as a numbered sequence. Each step should be
testable in isolation._

1. _Read the input as described in §3._
2. _Filter rows where `scenario == "..."`._
3. _Compute `new_field = ...`._
4. _Validate that `new_field` is in the documented range._
5. _Write the result to ..._

_If a formula matters, write it out. If a precedence rule matters,
write that out too. Developers should not infer business logic from
context._

## 5. Output requirements

| Output | Path | Schema | Format | Retention |
|--------|------|--------|--------|-----------|
| _e.g. `current_model_outputs.csv`_ | _`data/processed/`_ | _10 cols; see dictionary_ | _CSV, UTF-8_ | _kept through 2027Q4_ |

_Be explicit about file naming, partitioning, and overwrite behavior._

## 6. Edge cases

_For each edge case, describe both the trigger and the expected
behavior._

- _Empty input file:_
- _Missing required column:_
- _Out-of-range value in `pd_score`:_
- _Duplicate `(entity_id, scenario)` row:_
- _Scenario value not in the documented domain:_

## 7. Error-handling expectations

_State explicitly how the implementation should fail and what the
operator should see._

- _Fail loud and early on schema mismatches; do not coerce silently._
- _Log a single human-readable summary at INFO; details at DEBUG._
- _Exit non-zero on any failure so the orchestrator surfaces it._

## 8. Testing notes

_What the developer should test before handing back to QA._

- _Run the transformation against the sample input in `data/`._
- _Confirm row counts match the documented expectation._
- _Confirm derived fields fall in the documented range._

## 9. Implementation notes

_Anything the developer should know that isn't in the change request.
Examples: previous attempts, related refactors, performance targets,
preferred libraries, repository conventions._

## 10. Questions for the analyst

_Open items the developer flagged during implementation. The analyst is
responsible for answering these before sign-off._

- _Q1:_
- _Q2:_

---

_Template version: v1.0._
