# Data Mapping Example — Quarterly model-output extract

> **Illustrative example.** All field names, formats, and rules below
> are fictional. This is a worked example of the
> `templates/data_mapping_template.md` shape, not a real mapping.

---

## Mapping summary

- **Source:** `raw_quarterly_extract.csv` from the upstream modeling
  team
- **Target:** `data/processed/current_model_outputs.csv` consumed by
  the `model-output-qa-dashboard` project
- **Frequency:** quarterly (~6 weeks after quarter-end)
- **Run owner:** quarterly modeling team, with the data team as
  technical owner
- **Mapping version:** v1.2 (the v1.2 bump adds the
  `interest_rate_stress_v2` enum value)

## Field mapping

| Source field | Target field | Transformation rule | Data type | Required / optional | Validation rule | Notes |
|---|---|---|---|---|---|---|
| `loan_id` | `entity_id` | strip whitespace; prepend `"ENT_"` if the source value is purely numeric | str | required | `^ENT_\d{3,6}$` | Source IDs from prior to 2024Q1 may already include the prefix; do not double-prefix. |
| `seg_code` | `portfolio_segment` | lookup via `staging.segment_codes` (key: `seg_code`, value: long-form segment) | str | required | in `{large_balance, mid_market, small_balance}` | Missing lookup → drop row, emit QA flag, do **not** default. |
| `prop_class` | `property_type` | lowercase; map `MF→multifamily`, `OF→office`, `RT→retail`, `IN→industrial`, `HP→hospitality` | str | required | in `{multifamily, office, retail, industrial, hospitality}` |  |
| `scen_id` | `scenario` | lookup via `staging.scenario_lookup` | str | required | in `{baseline, interest_rate_stress, interest_rate_stress_v2, commodity_price_stress, downside_macro}` | New `*_v2` value added in v1.2. |
| `period` | `quarter` | format as `YYYYQn` from the source ISO date | str | required | `^\d{4}Q[1-4]$` |  |
| `pd_model_score` | `pd_score` | pass through | float | required | in `[0, 1]` | Out-of-range rejected, not clipped. |
| _derived_ | `risk_grade` | bucket `pd_score` per `risk_grade_buckets_v3.csv` | str | required | in `{A, B, C, D, E}` | Bucket version recorded in run metadata. |
| `el_amount` | `expected_loss` | pass through | float | required | `≥ 0` | Negative values rejected. |
| `mdl_ver` | `model_version` | pass through | str | required | `^v\d+\.\d+\.\d+$` |  |
| `run_ts` | `run_date` | truncate timestamp to date; ISO 8601 | date | required | parseable ISO date |  |

## Out-of-scope source fields

The following source fields exist but are not part of v1.2 of the
extract. Listing them keeps the implementation from silently dropping
something the analyst expected to see:

- `loan_servicer_code` — not used downstream as of v1.2.
- `originator_id` — out of scope; sensitive to disclosure rules.
- `geo_region` — under consideration for a future change request; not
  in the current extract.

## Versioning rules

- A new `scenario` enum value, a new segment code, or a new property
  type is a **mapping version bump**. v1.2 reflects the addition of
  `interest_rate_stress_v2`.
- Renames, type changes, or new validation rules are also a bump.
- A new mapping version triggers an updated data dictionary and a
  bumped model-output schema version. The two are kept in lockstep.

## Sample row (after mapping)

```
entity_id,portfolio_segment,property_type,scenario,quarter,pd_score,risk_grade,expected_loss,model_version,run_date
ENT_001,large_balance,office,interest_rate_stress_v2,2026Q2,0.0612,C,184201.40,v3.4.0,2026-05-15
```

---

_Template version: v1.0. Mapping version v1.2._
