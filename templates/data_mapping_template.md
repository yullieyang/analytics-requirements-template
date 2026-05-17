# Data Mapping — Template

> Use this template to document the field-by-field mapping between a
> source data product and a target data product. One row per target
> field. If the mapping is non-trivial (joins, derivations, lookups),
> document the rule in the `Transformation rule` column with enough
> precision that a developer can implement it without follow-up.

---

## Mapping summary

- **Source:** _e.g. `raw_quarterly_extract.csv` from upstream model team_
- **Target:** _e.g. `data/processed/current_model_outputs.csv` consumed
  by `model-output-qa-dashboard`_
- **Frequency:** _quarterly_
- **Run owner:** _analyst name / team_
- **Mapping version:** _v1.0_

## Field mapping

| Source field | Target field | Transformation rule | Data type | Required / optional | Validation rule | Notes |
|--------------|--------------|---------------------|-----------|---------------------|-----------------|-------|
| `loan_id` | `entity_id` | _strip whitespace; prepend `"ENT_"`_ | _str_ | _required_ | _matches `^ENT_\d{3,6}$`_ | _ID format change from upstream is rare; flag any deviation_ |
| `seg_code` | `portfolio_segment` | _lookup via `segment_codes.csv`_ | _str_ | _required_ | _in {large_balance, mid_market, small_balance}_ | _If lookup misses, log + drop the row + emit a QA flag_ |
| `prop_class` | `property_type` | _lowercase; map `"MF"` → `"multifamily"` etc._ | _str_ | _required_ | _in {multifamily, office, retail, industrial, hospitality}_ |  |
| `scen_id` | `scenario` | _lookup via `scenario_codes.csv`_ | _str_ | _required_ | _in {baseline, interest_rate_stress, commodity_price_stress, downside_macro}_ | _New scenarios must be added to the lookup before they appear_ |
| `period` | `quarter` | _format as `YYYYQn`_ | _str_ | _required_ | _matches `^\d{4}Q[1-4]$`_ |  |
| `pd_model_score` | `pd_score` | _pass through_ | _float_ | _required_ | _in [0, 1]_ | _Out-of-range values must be rejected, not clipped_ |
| _derived_ | `risk_grade` | _bucket `pd_score` per `risk_grade_buckets.csv`_ | _str (A-E)_ | _required_ | _in {A, B, C, D, E}_ | _Buckets are versioned; record buckets version in the run metadata_ |
| `el_amount` | `expected_loss` | _pass through_ | _float_ | _required_ | _≥ 0_ |  |
| `mdl_ver` | `model_version` | _pass through_ | _str_ | _required_ | _matches `^v\d+\.\d+\.\d+$`_ |  |
| `run_ts` | `run_date` | _truncate timestamp to date; format as ISO_ | _date_ | _required_ | _ISO 8601 date_ |  |

## Out-of-scope source fields

_Fields present in the source that do not map to the target. Listing
them explicitly prevents the implementation from silently dropping
something the analyst expected to see._

- _e.g. `loan_servicer_code` — not used downstream as of v1.0._

## Versioning rules

- _A new scenario, segment code, or property type is a **mapping
  version bump** and triggers a new mapping document, not an edit to
  this one._
- _Renames, type changes, or new validation rules are also a bump._

---

_Template version: v1.0._
