# Data — Part 2: Transforming the Data

This folder documents the data layer used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis is based on country- and area-level drinking-water access estimates from the **WHO/UNICEF Joint Monitoring Programme (JMP)**, with observations covering the period from 2000 to 2020.

The complete analytical workflow was developed in Google Sheets, including source-data inspection, validation, transformation, feature engineering, regional enrichment, summary calculations, and chart preparation.

---

## Working Spreadsheet

The complete analytical workbook is available here:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook is the primary analytical workspace for:

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

> One country or area observed in one specific year.

The dataset is not a complete annual panel. Most observations are concentrated in 2015 and 2020, while a smaller number of countries use intermediate years such as 2016, 2017, 2018, or 2019.

Because the observation interval is not identical for every country, the analysis uses a year-difference field before calculating Annual Rates of Change.

---

## Main Data Dimensions

The original dataset includes the following analytical dimensions:

| Dimension              | Description                                          |
| ---------------------- | ---------------------------------------------------- |
| Country or area        | Geographic observation name                          |
| Year                   | Observation year                                     |
| National population    | Population estimate recorded in thousands            |
| Urban population share | Percentage of the population living in urban areas   |
| National water access  | Basic, limited, unimproved, and surface-water access |
| Rural water access     | Rural access across the four service levels          |
| Urban water access     | Urban access across the four service levels          |

The main Part 2 analysis focuses on access to **at least basic drinking-water services** at national, rural, and urban levels.

---

## Main Spreadsheet Sheets

### `Source Data`

Contains the original imported drinking-water dataset.

### `Estimates of the use of water (2000-2020)`

Contains the transformed analytical dataset, including:

* year differences;
* national, rural, and urban Annual Rates of Change;
* rounded basic-access fields;
* full-access classification fields;
* rural–urban ARC differences;
* regional classifications.

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

## Key Derived Features

### `y_diff`

Calculates the number of years between two observations for the same country.

```text
y_diff = later year - earlier year
```

This field is used to:

* validate observation intervals;
* detect duplicate country-year records;
* provide the denominator for ARC calculations.

---

### `ARC_n`

Measures the Annual Rate of Change in national access to at least basic drinking water.

```text
ARC_n =
(later national basic access - earlier national basic access)
/
year difference
```

---

### `ARC_r`

Measures the Annual Rate of Change in rural access to at least basic drinking water.

```text
ARC_r =
(later rural basic access - earlier rural basic access)
/
year difference
```

---

### `ARC_u`

Measures the Annual Rate of Change in urban access to at least basic drinking water.

```text
ARC_u =
(later urban basic access - earlier urban basic access)
/
year difference
```

All ARC values are interpreted in:

> Percentage points per year.

---

### Rounded Basic-Access Fields

The following variables were created to identify approximate full access:

* `wat_bas_n_round`
* `wat_bas_r_round`
* `wat_bas_u_round`

Rounding is necessary because some estimated access values are very close to, or marginally above, 100%.

---

### Full-Access Classification Fields

The following fields identify countries where access was approximately 100% in both observation years:

* `ARC_n_full`
* `ARC_r_full`
* `ARC_u_full`

These classifications distinguish between:

* zero ARC because access was already complete;
* zero ARC because access remained unchanged below full coverage.

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

Adds a regional classification to each country through a lookup against the `Regions` reference sheet.

This field supports:

* country counts by region;
* average national ARC by region;
* average rural ARC by region;
* average urban ARC by region;
* average rural–urban ARC differences;
* regional population and progress comparisons.

---

### `pop_n (Millions)`

Converts national population from thousands into millions for clearer regional tables and charts.

```text
pop_n (Millions) = pop_n / 1000
```

This field is used mainly for reporting and visualization.

---

## ARC Interpretation

| ARC result | Meaning                                                              |
| ---------- | -------------------------------------------------------------------- |
| `ARC > 0`  | Access improved                                                      |
| `ARC = 0`  | No measured change or already full access                            |
| `ARC < 0`  | Access declined                                                      |
| `Null`     | ARC could not be calculated because required values were unavailable |

ARC measures the speed and direction of change. It does not represent the final level of access.

A country can have:

* a high ARC and still have low final access;
* a low ARC because access was already near 100%;
* a zero ARC because access was already complete;
* a negative ARC indicating declining access.

---

## Summary Classification Logic

The Summary sheet classifies national, rural, and urban ARC observations into five groups:

| Category     | Definition                                       |
| ------------ | ------------------------------------------------ |
| No ARC value | ARC is unavailable or marked `Null`              |
| Full access  | Basic access rounds to 100% in both observations |
| ARC = 0      | No measured change, excluding full-access cases  |
| ARC < 0      | Declining access, excluding full-access cases    |
| ARC > 0      | Improving access, excluding full-access cases    |

The classifications are designed to account for all valid country pairs.

A validation check can confirm:

```text
No ARC
+ Full access
+ ARC = 0
+ ARC < 0
+ ARC > 0
= Total country pairs
```

---

## Regional Aggregation

The transformed data supports the following regional indicators:

| Regional indicator       | Source fields        | Aggregation |
| ------------------------ | -------------------- | ----------- |
| Number of countries      | `name`, `region`     | Count       |
| Regional population size | `pop_n`, `region`    | Sum         |
| Average national ARC     | `ARC_n`, `region`    | Average     |
| Average rural ARC        | `ARC_r`, `region`    | Average     |
| Average urban ARC        | `ARC_u`, `region`    | Average     |
| Average ARC difference   | `ARC_diff`, `region` | Average     |

Unless otherwise stated, regional ARC values are simple country-level averages and are not population-weighted.

This means that a small country and a highly populated country can contribute equally to a regional average.

---

## Missing-Value Conventions

| Representation | Meaning                                                         |
| -------------- | --------------------------------------------------------------- |
| Blank cell     | No row-level calculation is expected                            |
| `Null`         | A required source value was unavailable or a calculation failed |
| `0`            | A valid measured value of zero                                  |

Missing ARC values are not replaced with zero because that would incorrectly classify unavailable observations as no change.

---

## Data Quality Considerations

### Unequal Observation Intervals

Countries are not necessarily observed over the same time interval.

The `y_diff` field ensures that access changes are converted into comparable annual rates.

### Missing Values

Some source values are represented as text values such as `Null`.

These values require controlled error handling before arithmetic calculations can be performed.

### Duplicate Country-Year Records

A same-country year difference of zero may indicate a duplicate or erroneous country-year observation.

### Estimated Values Near 100%

Some basic-access estimates are slightly below or above 100% because of estimation precision.

Rounded features are used when identifying approximate full access.

### Exact Country-Name Matching

Row comparisons and regional lookups depend on consistent country names.

Differences in spelling, punctuation, or formatting can prevent valid matches.

### Row-Order Dependency

ARC formulas depend on the dataset being correctly sorted by country and year.

Changing the row order without revalidating the formulas can produce incorrect comparisons.

### Regional Averaging

Simple regional averages give each country equal weight, regardless of population size.

Regional ARC should therefore not automatically be interpreted as the average progress experienced by every person in that region.

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

Keeping one primary analytical workspace reduces duplication and lowers the risk of inconsistent versions.

The repository stores:

* data documentation;
* the data dictionary;
* analytical reports;
* spreadsheet exports;
* visual assets;
* country-level regional extracts.

This structure keeps the repository lightweight while preserving transparency into the completed workflow.

> Full reproducibility depends on continued access to the linked Google Sheets workbook. The repository itself provides detailed documentation and exported evidence of the analysis.

---

## Data Dictionary

Detailed documentation for all original and derived variables is available here:

[data_dictionary.md](./data_dictionary.md)

The data dictionary documents:

* variable definitions;
* source or derived status;
* data types;
* units;
* transformation logic;
* analytical uses;
* missing-value behavior.

---

## Related Project Outputs

### Visual Assets

[Open the assets folder](../assets/)

Contains:

* primary analytical charts;
* regional ARC tables;
* country-level supporting evidence.

### Reports

[Open the reports folder](../reports/)

Contains:

* the Part 2 analytical report;
* spreadsheet sheet exports;
* reporting documentation.

### Main Part 2 README

[Open the Part 2 project overview](../README.md)

Provides the complete Part 2 overview, methodology, findings, and repository navigation.

---

## Units Summary

| Variable group         | Unit                       |
| ---------------------- | -------------------------- |
| `year`                 | Calendar year              |
| `y_diff`               | Years                      |
| `pop_n`                | Thousands of people        |
| `pop_n (Millions)`     | Millions of people         |
| `pop_u`                | Percentage                 |
| Water-access variables | Percentage                 |
| ARC variables          | Percentage points per year |
| `ARC_diff`             | Percentage points per year |

---

## Notes

* The dataset is descriptive and observational.
* The analysis identifies patterns and associations but does not establish causality.
* ARC measures the speed and direction of change, not the final access level.
* A high ARC can coexist with low final access.
* A low ARC can reflect high baseline access and limited remaining room for improvement.
* Full-access classifications should be reviewed before interpreting zero ARC values.
* Missing values are retained transparently and are not treated as zero.
* Regional summaries should be interpreted alongside population size and country-level records.
