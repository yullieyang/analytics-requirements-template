# Release Review Notes — 2026Q2 quarterly model release

> **Illustrative example.** All names, dates, counts, and outcomes
> below are fictional. This is a worked example of how the templates
> in this repository compose into a single release review record.

---

## Release identifying information

- **Release tag:** `2026Q2`
- **Model version:** `v3.4.0` (was `v3.3.0`)
- **Mapping version:** `v1.2` (was `v1.1`)
- **Linked change request:** `examples/example_model_output_change_request.md`
- **Linked acceptance criteria:** `examples/example_acceptance_criteria.md`
- **Reviewer:** _C. Auditor (fictional)_
- **Review date:** 2026-05-14

## Summary

The 2026Q2 release adds one new scenario (`interest_rate_stress_v2`)
to the quarterly model-output extract. No existing scenario was
modified. All required test cases passed. The reviewer signed off
with two follow-up items recorded below.

## What changed

- One new scenario value in the `scenario` enum domain.
- Mapping version bumped from v1.1 to v1.2.
- Model version bumped from v3.3.0 to v3.4.0.
- Methodology note updated with the segment-specific rate-shift
  calibration.
- Data dictionary updated to list the new enum value.

## What did not change

- Schema of the output extract (column names, dtypes, order).
- Row counts for any non-v2 scenario.
- Bucket file for `risk_grade` (still `risk_grade_buckets_v3.csv`).
- Downstream `model-output-qa-dashboard` filter logic (the new value
  is picked up automatically through the existing scenario filter).
- All non-v2 rows are byte-equal to the 2026Q1 release for the same
  input.

## QA evidence

- All 6 required test cases passed; see
  `examples/example_acceptance_criteria.md`.
- 50 new v2 rows produced for 50 entities × 1 quarter.
- 0 violations of the `pd_score` bound check.
- 0 violations of the scenario-enum domain check.
- Regression check vs the 2026Q1 release: clean (no changes outside
  the v2 rows).

## Risks raised at review

- The `quarterly_review_deck.qmd` template was updated by hand to add
  a v2 row to the per-scenario panel. A future change to the deck
  template should automate this from the scenario list rather than
  hard-coding the panel layout.
- One downstream consumer (an internal Excel workbook used by the
  review committee) still references the v1 scenario only. The
  workbook owner has been notified; remediation tracked separately.

## Follow-ups

| # | Item | Owner | Due |
|---|------|-------|-----|
| 1 | Automate scenario-row generation in `quarterly_review_deck.qmd` | _developer (fictional)_ | 2026-08-15 |
| 2 | Confirm the Excel workbook owner has updated their consumer | _analyst (fictional)_ | 2026-06-01 |

## Reviewer notes

The new scenario behaves as documented across all three segments. The
segment ordering (small ≤ mid ≤ large for the v2 vs v1 `pd_score`) is
preserved on the slice means and is consistent with the methodology
note. The reviewer notes that this is a descriptive observation, not
a validation of the calibration itself — model methodology review
remains out of scope for the release-QA workflow.

---

_All names, dates, counts, and outcomes in this document are
fictional. This is an illustrative example, not a real release
record._
