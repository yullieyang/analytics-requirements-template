# Reviewer Checklist — Template

> Use this checklist when reviewing an implementation against an
> approved change request. The reviewer is accountable for every check
> below; "not applicable" is an acceptable answer when documented.

---

## Identifying information

- **Change request:** _path / link to `analytical_change_request.md`_
- **Implementation PR / commit:** _link_
- **Reviewer:** _name_
- **Review date:** _ISO date_

## Logic

- [ ] _The implementation matches the transformation logic described
  in `developer_handoff.md` §4 step-by-step._
- [ ] _Edge cases described in `developer_handoff.md` §6 are handled
  as documented._
- [ ] _Error-handling behavior matches `developer_handoff.md` §7
  (fails loud, exits non-zero, logs are clear)._

## Data source

- [ ] _The implementation reads the source described in the data
  mapping document._
- [ ] _No source data has been replaced with a sample or fixture in
  production code._
- [ ] _Mapping-version metadata is recorded in the run output (run_date,
  model_version, mapping_version where applicable)._

## Output expectations

- [ ] _Output schema matches the data mapping document field-by-field._
- [ ] _Row count is within the documented expected range for this
  change._
- [ ] _Domain-value columns contain only documented enum values._

## Assumptions

- [ ] _Every assumption listed in the change request is either tested
  in the QA suite or explicitly justified in a comment in the
  implementation._
- [ ] _No new assumptions have been silently introduced in the
  implementation; if they have, they have been added to the change
  request before sign-off._

## Edge cases

- [ ] _Edge cases listed in the change request and handoff have
  matching test cases in the QA acceptance criteria._
- [ ] _The implementation produces a meaningful failure mode for each
  edge case rather than a silent default._

## Developer questions

- [ ] _Every question in `developer_handoff.md` §10 has a recorded
  answer._
- [ ] _Answers that changed implementation behavior have been
  reflected back into the change request._

## QA evidence

- [ ] _QA acceptance criteria document is attached / linked._
- [ ] _Every required test case in the QA document has a recorded
  pass/fail._
- [ ] _Defects are documented as separate change requests, not silently
  fixed during QA._

## Documentation

- [ ] _The data dictionary is up to date._
- [ ] _The methodology note (if any) reflects the change._
- [ ] _The "What this project does not do" section in the affected
  repository README is still accurate._

## Final approval

- [ ] _Approved as-is._
- [ ] _Approved with conditions (recorded below)._
- [ ] _Rejected (recorded below with required follow-ups)._

### Conditions / follow-ups

_If approved with conditions or rejected, list the specific follow-ups
here. Each item should be actionable and assigned._

- _e.g. Add a regression test for the unchanged scenarios before next
  quarterly release (owner: developer name, due: 2026-08-15)._

---

_Template version: v1.0._
