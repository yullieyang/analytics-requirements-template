# QA Acceptance Criteria — Template

> Use this template once the developer has implemented the change.
> Acceptance criteria are written by the analyst (or the analyst + QA
> reviewer together) before QA begins, not after.

---

## 1. Scope of QA

_What is in scope, what is out._

- _In scope: the new `interest_rate_stress_v2` scenario rows in
  `current_model_outputs.csv`._
- _Out of scope: existing scenarios, model methodology, downstream
  dashboard rendering._

## 2. Required test cases

_For each test case: name, input, expected output, pass/fail rule._

| # | Name | Input | Expected output | Pass rule |
|---|------|-------|-----------------|-----------|
| 1 | _New scenario rows present_ | _sample input with 50 entities_ | _200 new rows (50 × 4 scenarios)_ | _row count equals expected_ |
| 2 | _pd_score in [0, 1]_ | _full output_ | _0 rows out of range_ | _query returns zero_ |
| 3 | _Backfill behavior_ | _historical 2024Q1 input_ | _no new-scenario rows produced_ | _flag matches documented decision_ |

## 3. Data completeness checks

- _All required columns present._
- _No null values in required columns._
- _Domain-value columns (e.g. `scenario`) contain only documented enum
  values._
- _Row counts per `(entity_id, scenario)` match the prior run except
  where explicitly documented._

## 4. Output comparison checks

_For changes that affect existing rows, compare the new output to the
prior output and document expected vs unexpected deltas._

- _Expected: pd_score under `interest_rate_stress_v2` should be on
  average ≥ pd_score under `baseline`._
- _Expected: no change to rows under any other scenario._
- _Unexpected: any change in row count for the unchanged scenarios._

## 5. Regression checks

_Confirm that nothing outside the scope of the change moved._

- _`baseline`, `commodity_price_stress`, and `downside_macro` rows
  byte-equal to the prior release for the same input._
- _All required columns retain their prior dtype and bounds._

## 6. Documentation checks

- [ ] _The data dictionary lists the new scenario value._
- [ ] _The methodology note explains the new scenario's calibration._
- [ ] _The change request's "Expected output behavior" section matches
  what was actually produced._
- [ ] _Any open questions from the change request have been resolved
  and recorded._

## 7. Sign-off checklist

- [ ] _All required test cases pass._
- [ ] _Completeness checks pass._
- [ ] _Regression checks pass._
- [ ] _Documentation checks pass._
- [ ] _QA reviewer has run the implementation against a representative
  input._
- [ ] _Any defects are documented as separate change requests, not
  silently fixed._
- [ ] _Reviewer name and date recorded below._

### Reviewer sign-off

| Role | Name | Date | Outcome |
|------|------|------|---------|
| QA reviewer |  |  | _approved / rejected / approved with conditions_ |
| Approving manager |  |  |  |

---

_Template version: v1.0._
