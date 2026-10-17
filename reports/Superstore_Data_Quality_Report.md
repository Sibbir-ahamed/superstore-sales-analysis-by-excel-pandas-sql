# SUPERSTORE — DATA QUALITY REPORT

**Dataset:** `SampleSuperstore.xlsx`

---

## 1. Overall Checks

| Check Item | Result | Notes |
|---|---:|---|
| Total data rows | 9,994 | Count of records; header excluded |
| Total columns | 13 | Expected columns in source file |
| Total missing cells | 47 | Sum of blank/NA cells across all columns |
| Rows with at least one missing value | 47 | A row is counted once even if several cells are missing |
| Exact duplicate rows | 17 | Entire-row duplicates; inspect before removing |

## 2. Missing Values by Column

| Column | Missing Cells | Data Type in File | Review Notes |
|---|---:|---|---|
| Ship Mode | 12 | `object` | No missing values found in this column; review other quality rules if relevant. |
| Segment | 0 | `object` | Inspect affected records; fill only if the correct value can be verified. |
| Country | 0 | `object` | Check source/record context before deciding how to handle blanks. |
| City | 0 | `object` | No missing values found in this column; review other quality rules if relevant. |
| State | 10 | `object` | Review missing locations; do not guess values without reliable evidence. |
| Postal Code | 11 | `int64` | Currently numeric. Consider Text format for identifiers, especially where leading zeros matter. |
| Region | 1 | `object` | No missing values found in this column; review other quality rules if relevant. |
| Category | 9 | `object` | Verify from source or related product information before filling. |
| Sub-Category | 4 | `object` | No missing values found in this column; review other quality rules if relevant. |
| Sales | 0 | `float64` | Numeric; check for unexpected values as a separate validation step. |
| Quantity | 0 | `int64` | Whole-number numeric field; check for unexpected negative/zero values as a separate step. |
| Discount | 0 | `float64` | Numeric; verify the allowed range for this dataset. |
| Profit | 0 | `float64` | Negative values can represent losses and are not automatically errors. |

## 3. Data Type Review

| Column | Observed Type | Expected / Appropriate Type | Assessment |
|---|---|---|---|
| Ship Mode | `object` | Text/category | Looks appropriate based on observed type. |
| Segment | `object` | Text/category | Looks appropriate based on observed type. |
| Country | `object` | Text/category | Looks appropriate based on observed type. |
| City | `object` | Text/category | Looks appropriate based on observed type. |
| State | `object` | Text/category | Looks appropriate based on observed type. |
| Postal Code | `int64` | Text identifier (recommended) | Review: currently stored as integer; preserve leading zeros if relevant. |
| Region | `object` | Text/category | Looks appropriate based on observed type. |
| Category | `object` | Text/category | Looks appropriate based on observed type. |
| Sub-Category | `object` | Text/category | Looks appropriate based on observed type. |
| Sales | `float64` | Numeric / decimal | Looks appropriate; check valid ranges and business rules. |
| Quantity | `int64` | Whole number | Looks appropriate; validate unusual values separately. |
| Discount | `float64` | Numeric / decimal | Looks appropriate; check valid ranges and business rules. |
| Profit | `float64` | Numeric / decimal | Looks appropriate; negative values can represent losses and are not automatically errors. |

## 4. Recommended Next Actions

1. Investigate the 47 missing cells across Segment, Country, State, and Category; do not fill values by guessing.
2. Inspect the 17 exact duplicate rows and confirm whether they are accidental duplicates before removing any.
3. Review Postal Code storage as a text identifier where appropriate.
4. Record each change made and keep an untouched copy of the original data.
5. After review, update this report with decisions, evidence, and final status.
