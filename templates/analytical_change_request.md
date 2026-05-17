# Analytical Change Request — Template

> Use this template when an analyst is requesting a data or model
> behavior change that another engineer will implement. The goal is to
> describe the change in enough detail that a developer can scope it,
> QA can write acceptance criteria, and a reviewer can approve it
> without a follow-up meeting.

---

## 1. Title

_Short, imperative phrasing. e.g. "Add `interest_rate_stress_v2`
scenario to the quarterly model-output extract."_

## 2. Background

_Two-to-four sentences. What changed upstream / what is being asked, and
why now. Avoid restating policy._

## 3. Business / analytical context

_Who needs this and what decision it informs. Cite the dashboard,
report, or downstream workflow the change feeds into._

## 4. Current behavior

_State the behavior as it exists today. Reference the schema, table,
column, or function name explicitly. If a sample row helps, include it._

## 5. Requested change

_Describe the change as a list of concrete deltas, not as prose._

- _Add column `..."_
- _Rename `...` to `..."_
- _Update transformation from `...` to `..."_

## 6. Expected output behavior

_For each delta in §5, describe what the output should look like
afterwards. Include sample rows or expected values when possible._

## 7. Impacted fields

| Field | Impact | Direction |
|-------|--------|-----------|
| _e.g. `pd_score`_ | _recomputed_ | _no schema change_ |
| _e.g. `scenario`_ | _new enum value `interest_rate_stress_v2`_ | _domain expansion_ |

## 8. Impacted tables, files, or models

_List every artifact that the change touches. Include downstream
consumers if known._

- _Source table:_
- _Intermediate table(s):_
- _Output extract / file:_
- _Downstream dashboards / reports:_

## 9. Assumptions

_State every assumption the change relies on. A future reviewer should
be able to test each one._

- _e.g. The new scenario uses the same exposure inputs as
  `interest_rate_stress`._
- _e.g. Historical runs of the older scenario will continue to be
  produced for back-comparison through 2026Q4._

## 10. Open questions

_Questions whose answers will change the implementation. Leave open
items here rather than guessing._

- _Q1: Should the new scenario back-populate prior quarters or apply
  forward only?_

## 11. Dependencies

_Other change requests, releases, or upstream changes this depends on._

## 12. Risks

_What could go wrong. Be specific. "Edge cases" is not a risk; "the
domain change will break the existing `scenario` enum check in the
downstream reporting view" is._

## 13. Reviewers

| Role | Name | Decision | Date |
|------|------|----------|------|
| Analyst (author) |  | — | — |
| Developer |  |  |  |
| QA reviewer |  |  |  |
| Approving manager |  |  |  |

## 14. Approval status

- [ ] Draft
- [ ] Under review
- [ ] Approved
- [ ] Implemented
- [ ] Verified in production

---

_Template version: v1.0. Edit this template, not the request. If you
catch a missing section, update both this template and the example
under `examples/`._
