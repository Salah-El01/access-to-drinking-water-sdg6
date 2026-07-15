# Data — Part 2: Transforming the Data

This folder documents the data layer used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis is based on country- and area-level drinking-water access estimates from the **WHO/UNICEF Joint Monitoring Programme (JMP)** covering observations between 2000 and 2020.

The full analytical workflow was developed in Google Sheets, including data validation, row-level transformations, Annual Rate of Change calculations, regional enrichment, summary tables, and chart preparation.

---

## Working Spreadsheet

The complete analytical workbook is available here:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook acts as the primary analytical workspace for:

* original source data;
* transformation formulas;
* validation checks;
* derived variables;
* regional lookup logic;
* summary tables;
* chart preparation;
* final spreadsheet outputs.

---

## Dataset Scope

The dataset contains drinking-water access observations for countries and territories across multiple years between 2000 and 2020.

The analytical grain is:

> One country or area observation for a specific year.

The dataset is not a complete annual panel. Most observations are concentrated in 2015 and 2020, while a smaller number of countries use other intermediate years.

Because observation intervals differ across countries, the analysis uses a year-difference field to normalize change over time.

---

## Main Data Dimensions

The original dataset includes:

| Dimension              | Description                                          |
| ---------------------- | ---------------------------------------------------- |
| Country or area        | Geographic observation name                          |
| Year                   | Observation year                                     |
| National population    | Population estimate, recorded in thousands           |
| Urban population share | Percentage of the population living in urban areas   |
| National water access  | Basic, limited, unimproved, and surface-water access |
| Rural water access     | Rural access across the four service levels          |
| Urban water access     | Urban access across the four service levels          |

The main Part 2 analysis focuses on access to **at least basic drinking water services** at national, rural, and urban levels.

---

## Transformation Workflow

The data preparation process follows this structure:

```text
Source data
    ↓
Country and year sorting
    ↓
Year-difference validation
    ↓
Annual Rate of Change calculations
    ↓
Missing-value and error handling
    ↓
Full-access classification
    ↓
Rural–urban ARC comparison
    ↓
Regional lookup and enrichment
    ↓
Summary tables and visual analysis
```

---

## Derived Features

### `y_diff`

Calculates the number of years between two observations for the same country.

```text
y_diff = later year - earlier year
```

This field is used to:

* validate observation intervals;
* detect duplicate country-year rows;
* normalize Annual Rate of Change calculations.

---

### `ARC_n`

Annual Rate of Change in national access to at least basic drinking water.

```text
ARC_n =
(later national basic access - earlier national basic access)
/
year difference
```

---

### `ARC_r`

Annual Rate of Change in rural access to at least basic drinking water.

---

### `ARC_u`

Annual Rate of Change in urban access to at least basic drinking water.

All ARC values are interpreted in:

> Percentage points per year.

---

### Rounded Basic-Access Features

The following variables were created to identify approximate full access:

* `wat_bas_n_round`
* `wat_bas_r_round`
* `wat_bas_u_round`

Rounding is necessary because some estimated access values are very close to, or marginally above, 100%.

---

### Full-Access Classification

The following fields identify countries where access was approximately 100% in both observation years:

* `ARC_n_full`
* `ARC_r_full`
* `ARC_u_full`

These fields distinguish between:

* zero ARC because access was already complete;
* zero ARC because access did not improve below full coverage.

This prevents countries already at full access from being misclassified as stagnant.

---

### `ARC_diff`

Compares rural and urban progress:

```text
ARC_diff = ARC_r - ARC_u
```

Interpretation:

* `ARC_diff > 0` — rural access improved faster;
* `ARC_diff < 0` — urban access improved faster;
* `ARC_diff ≈ 0` — rural and urban progress were similar.

---

### `region`

Adds a regional classification to each country through a lookup against the regional reference table.

This field supports:

* country counts by region;
* average national ARC by region;
* average rural ARC by region;
* average urban ARC by region;
* regional population and progress comparisons.

---

## Main Spreadsheet Sheets

The workbook includes the following core sheets:

### `Source Data`

Contains the original imported drinking-water dataset.

### `Estimates of the use of water (2000-2020)`

Contains the transformed analytical dataset, including:

* `y_diff`;
* national, rural, and urban ARC;
* rounded basic-access fields;
* full-access flags;
* rural–urban ARC difference;
* regional classification.

### `Regions`

Contains the country-to-region reference data used to enrich the transformed dataset.

### `Summary`

Contains:

* year-distribution analysis;
* year-difference statistics;
* ARC summary statistics;
* progress-status counts;
* rural–urban ARC comparisons;
* regional summaries;
* analytical visualizations.

---

## Data Quality Considerations

The following issues were considered during transformation:

### Unequal Observation Intervals

Countries are not necessarily observed over the same time period.

The `y_diff` field ensures that access changes are converted into comparable annual rates.

### Missing Values

Some source values are represented as text values such as `Null`.

These values require controlled error handling before performing arithmetic calculations.

### Duplicate Country-Year Records

A year difference of zero for the same country can indicate a duplicate or erroneous observation.

### Estimated Values Near 100%

Some basic-access estimates are slightly below or above 100% because of estimation precision.

Rounded features are used when classifying approximate full access.

### Exact Country-Name Matching

Row comparisons and regional lookups depend on consistent country names.

Differences in spelling or formatting can prevent valid matches.

### Row-Order Dependency

The ARC formulas depend on the data being correctly sorted by country and year.

Changing the row order without revalidating the formulas can produce incorrect comparisons.

---

## Why the Raw Dataset Is Not Duplicated Here

The full working dataset is not duplicated in this folder because the Google Sheets workbook already preserves:

* the original data;
* transformation formulas;
* lookup logic;
* validation steps;
* derived variables;
* summaries;
* chart preparation.

Keeping one primary analytical workspace reduces duplication and prevents different versions of the transformed data from becoming inconsistent.

The repository stores:

* data documentation;
* analytical reports;
* sheet exports;
* visual assets;
* country-level regional extracts.

This structure keeps the repository lightweight while preserving transparency into the analytical workflow.

> Full reproducibility depends on continued access to the linked Google Sheets workbook. The repository itself provides documentation and exported evidence of the completed analysis.

---

## Related Project Outputs

### Visual Assets

[`../assets/`](../assets/)

Contains:

* primary analytical charts;
* regional ARC tables;
* country-level supporting evidence.

### Reports

[`../reports/`](../reports/)

Contains:

* the Part 2 analytical report;
* spreadsheet sheet exports;
* reporting documentation.

### Main Part 2 README

[`../README.md`](../README.md)

Provides the full Part 2 project overview, methodology, findings, and navigation.

---

## Recommended Supporting Documentation

A separate data dictionary can be used to document every original and derived variable:

[`data_dictionary.md`](./data_dictionary.md)

Suggested fields include:

* variable name;
* source or derived status;
* definition;
* data type;
* unit;
* transformation formula;
* analytical use;
* missing-value behavior.

---

## Notes

* `pop_n` is stored in thousands in the original dataset.
* Population values may also be converted into millions for regional visualization.
* ARC measures the speed of progress, not the final level of access.
* Regional ARC values are generally based on country-level averages unless otherwise specified.
* Simple regional averages are not automatically population-weighted.
* Missing values are retained transparently rather than treated as zero.
* The analysis is descriptive and exploratory and does not establish causality.
