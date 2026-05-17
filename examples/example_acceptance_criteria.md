# QA Acceptance Criteria — `interest_rate_stress_v2` scenario release

> **Illustrative example.** Names, counts, and numbers are fictional.
> This is a worked example of `templates/qa_acceptance_criteria.md`
> against the matching change-request example.

---

## 1. Scope of QA

- **In scope:** new `interest_rate_stress_v2` rows in
  `data/processed/current_model_outputs.csv` for 2026Q2.
- **Out of scope:** existing scenario rows (`baseline`,
  `interest_rate_stress`, `commodity_price_stress`, `downside_macro`),
  model methodology, downstream dashboard rendering, the
  `quarterly_review_deck.qmd` template.

## 2. Required test cases

| # | Name | Input | Expected output | Pass rule |
|---|------|-------|-----------------|-----------|
| 1 | New scenario rows present | full 2026Q2 source extract (50 entities) | 50 new rows with `scenario = "interest_rate_stress_v2"` | row count equals 50 |
| 2 | Scenario enum domain check | full 2026Q2 output | only the 5 documented scenario values appear | unexpected values count = 0 |
| 3 | pd_score bounds | full 2026Q2 output | no row with `pd_score < 0` or `pd_score > 1` | 0 violations |
| 4 | v2 vs v1 by segment, monotone behavior | `small_balance`, `mid_market`, `large_balance` slices | mean v2 `pd_score` ≥ baseline, with the segment ordering documented in the methodology note (small ≤ mid ≤ large) | inequalities hold on the slice means |
| 5 | No back-population pre-2026Q2 | 2024Q1 historical input | 0 v2 rows in the output | row count equals 0 |
| 6 | Existing scenarios byte-equal | full 2026Q2 source extract | rows under the four existing scenarios are byte-identical to the prior release for the same input | `diff` shows no changes outside the v2 rows |

## 3. Data completeness checks

- All required columns present in the output.
- No null values in any required column for the new v2 rows.
- Every v2 row has a paired baseline row with the same `entity_id` and
  `quarter`.
- `risk_grade` for v2 rows falls in `{A, B, C, D, E}` and matches the
  bucket implied by the row's `pd_score` and the v3 bucket file.

## 4. Output comparison checks

- For each `(entity_id, quarter)`:
  - `large_balance` v2 `pd_score` ≥ v1 `pd_score`.
  - `small_balance` v2 `pd_score` ≤ v1 `pd_score`.
  - `mid_market` v2 `pd_score` ≈ v1 `pd_score` (within 5% relative).
- No change in any non-v2 row.

## 5. Regression checks

- `baseline`, `commodity_price_stress`, and `downside_macro` rows
  byte-equal to the prior release for the same 2026Q2 input.
- The `interest_rate_stress` (v1) rows byte-equal to the prior release
  for the same 2026Q2 input.
- All required columns retain their prior dtype.
- Row counts per `(entity_id, scenario)` are unchanged for non-v2
  scenarios.

## 6. Documentation checks

- [x] Data dictionary lists `interest_rate_stress_v2` as a scenario
  value.
- [x] Methodology note explains the segment-specific rate-shift path.
- [x] Change request's "Expected output behavior" section matches the
  produced output.
- [x] Open questions from the change request are recorded with
  resolutions.

## 7. Sign-off checklist

- [x] All required test cases pass.
- [x] Completeness checks pass.
- [x] Regression checks pass.
- [x] Documentation checks pass.
- [x] QA reviewer has run the implementation against a representative
  input.
- [x] Defects (if any) are documented as separate change requests.
- [x] Reviewer name and date recorded below.

### Reviewer sign-off

| Role | Name | Date | Outcome |
|------|------|------|---------|
| QA reviewer | _C. Auditor (fictional)_ | 2026-05-14 | approved |
| Approving manager | _D. Manager (fictional)_ | 2026-05-15 | approved |

---

_Illustrative example only. All names, dates, and outputs are
fictional._
