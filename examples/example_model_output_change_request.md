# Analytical Change Request — Add `interest_rate_stress_v2` scenario

> **Status:** Approved — illustrative example. The names, dates, and
> values below are fictional. They are not based on any real model
> release, client portfolio, or methodology.

---

## 1. Title

Add `interest_rate_stress_v2` scenario to the quarterly model-output
extract.

## 2. Background

The current `interest_rate_stress` scenario shifts the policy-rate path
up by 200 basis points over four quarters. Recent reviewer feedback is
that the 200bp shift is too symmetric across portfolio segments. The
modeler proposed a refreshed scenario that varies the shift by segment
(150bp for `small_balance`, 250bp for `large_balance`, 200bp for
`mid_market`).

This change adds the refreshed scenario as a parallel `*_v2` so the old
and new can be reviewed side by side for at least two quarters before
the old one is retired.

## 3. Business / analytical context

The quarterly review committee reads the model-output extract to discuss
sensitivity by segment. Adding the v2 scenario lets the committee see
the segment-specific stress path without removing the historical
comparison.

## 4. Current behavior

The extract today contains four scenarios:

```
baseline, interest_rate_stress, commodity_price_stress, downside_macro
```

Schema is documented in `data_mapping_template.md`.

## 5. Requested change

- Add a new enum value `interest_rate_stress_v2` to the `scenario`
  column.
- Compute `pd_score` and `expected_loss` for the new scenario using the
  segment-specific rate-shift path (defined by the modeler in the
  methodology note).
- Do **not** modify the existing `interest_rate_stress` rows.
- Do **not** retire any existing scenario as part of this release.

## 6. Expected output behavior

For each `(entity_id, quarter)` already present in the extract, one
additional row appears with `scenario = "interest_rate_stress_v2"`. The
`pd_score` for the v2 scenario satisfies:

- For `small_balance`: `pd_score` typically slightly below the v1
  scenario (smaller shift).
- For `large_balance`: `pd_score` typically slightly above the v1
  scenario (larger shift).
- For `mid_market`: `pd_score` similar to the v1 scenario.

The sign convention and bounds are unchanged.

## 7. Impacted fields

| Field | Impact | Direction |
|-------|--------|-----------|
| `scenario` | new enum value `interest_rate_stress_v2` | domain expansion |
| `pd_score` | new rows generated under the new scenario | additive |
| `risk_grade` | new rows generated; bucket logic unchanged | additive |
| `expected_loss` | new rows generated | additive |
| `model_version` | bumped to next minor version (e.g. `v3.4.0`) | required by release policy |

## 8. Impacted tables, files, or models

- Source table: `raw_quarterly_extract.csv` (no change required — the
  upstream already exposes the v2 scenario)
- Intermediate table: `staging.scenario_lookup` — add the new value
- Output extract: `data/processed/current_model_outputs.csv`
- Downstream consumers:
  - `model-output-qa-dashboard` — should pick up the new scenario via
    the existing scenario filter without code changes
  - `quarterly_review_deck.qmd` — needs a manual update to add a row
    for the new scenario

## 9. Assumptions

- The modeler has confirmed the v2 scenario uses the same exposure
  inputs as v1; only the rate-shift path differs.
- Historical runs (pre-2026Q1) will not be back-populated with the v2
  scenario.
- The v1 scenario stays in the extract for at least two more quarterly
  releases.

## 10. Open questions

- Q1: After two quarters, who decides whether the v1 scenario is
  retired? Default answer: the quarterly review committee, with a
  separate change request to retire.
- Q2: Should the QA dashboard display v1 and v2 side by side in a
  dedicated panel, or just within the existing scenario filter?
  Answer: existing scenario filter is sufficient for the first
  release; a dedicated panel can be considered later.

## 11. Dependencies

- The scenario-codes lookup file (`staging.scenario_lookup`) must be
  updated before the modeler's run is executed.
- The methodology note must be updated with the v2 calibration.

## 12. Risks

- The downstream `quarterly_review_deck.qmd` template hard-codes the
  four-scenario panel layout. Without the manual update, the deck will
  silently omit the v2 scenario. Mitigation: linked acceptance
  criteria includes a "deck shows v2" check.
- Adding a new enum value can break consumers that hard-code a
  four-scenario assumption. Mitigation: search downstream code for
  literal scenario-name strings before approving the release.

## 13. Reviewers

| Role | Name | Decision | Date |
|------|------|----------|------|
| Analyst (author) | _A. Reviewer_ | author | 2026-05-08 |
| Developer | _B. Implementer_ | approved | 2026-05-12 |
| QA reviewer | _C. Auditor_ | approved | 2026-05-14 |
| Approving manager | _D. Manager_ | approved | 2026-05-15 |

## 14. Approval status

- [x] Draft
- [x] Under review
- [x] Approved
- [x] Implemented
- [x] Verified in production

---

_All names are fictional. This is an illustrative example of how a
change request should read; the content is not based on any real
release._
