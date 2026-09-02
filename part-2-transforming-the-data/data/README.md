# Data — Part 2: Transforming the Data

This folder documents the data layer used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis uses country- and area-level drinking-water access estimates associated with the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

The analytical workflow was developed in Google Sheets and includes:

* source-data inspection;
* country-year pairing;
* validation;
* feature engineering;
* Annual Rate of Change calculations;
* missing-value handling;
* full-access classification;
* regional enrichment;
* Summary calculations;
* chart preparation.

---

## Folder Contents

```text
data/
├── README.md
└── data_dictionary.md
```

| File                 | Purpose                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------- |
| `README.md`          | Documents the dataset scope, transformation workflow, quality checks and analytical methodology |
| `data_dictionary.md` | Defines the original and derived variables in detail                                            |

The current folder contains documentation rather than machine-readable data files.

---

## Data Source

The project uses drinking-water access estimates associated with the **WHO/UNICEF JMP**.

Official data-download portal:

[WHO/UNICEF JMP Downloads](https://washdata.org/data/downloads)

The transformed project sheet is titled:

```text
Estimates of the use of water (2000-2020)
```

However, the final analytical subset used in this project contains observations from **2015 to 2020**.

The sheet title should not be interpreted as evidence that the completed analysis contains annual observations throughout the full 2000–2020 period.

---

## Working Spreadsheet

The complete analytical workbook is available here:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook is the primary calculation environment for:

* the imported source data;
* sorting and country pairing;
* transformation formulas;
* error handling;
* derived variables;
* regional lookup logic;
* Summary calculations;
* regional tables;
* chart preparation.

PDF exports of the transformed and Summary sheets are available in:

[Spreadsheet Sheet Exports](../reports/sheet_exports/)

PDFs preserve the rendered spreadsheet output but do not preserve the same reproducibility as CSV or spreadsheet files containing formulas.

---

## Analytical Dataset Scope

The final analytical subset contains:

| Measure                          | Result |
| -------------------------------- | -----: |
| Countries and areas              |    231 |
| Country-year observations        |    462 |
| Observations per country or area |      2 |
| Earliest analysed year           |   2015 |
| Latest analysed year             |   2020 |
| Country pairs                    |    231 |

The row-level analytical grain is:

> One country or area observed in one specific year.

Each country or area has:

* one 2015 baseline observation;
* one later observation between 2016 and 2020.

The dataset is therefore a **paired-observation dataset**, not a complete annual panel.

---

## Observation-Year Distribution

|      Year | Observations |    Share |
| --------: | -----------: | -------: |
|      2015 |          231 |   50.00% |
|      2016 |            3 |    0.65% |
|      2017 |            9 |    1.95% |
|      2018 |            2 |    0.43% |
|      2019 |            4 |    0.87% |
|      2020 |          213 |   46.10% |
| **Total** |      **462** | **100%** |

The 2015 and 2020 observations represent approximately **96.1%** of the dataset.

All 231 countries and areas have a 2015 baseline.

Of these:

* 213 have their later observation in 2020;
* 18 have their later observation between 2016 and 2019.

---

## Main Data Dimensions

| Dimension              | Description                                              |
| ---------------------- | -------------------------------------------------------- |
| Country or area        | Geographic observation name                              |
| Year                   | Observation year                                         |
| National population    | Population estimate stored in thousands                  |
| Urban population share | Percentage of the population living in urban areas       |
| National water access  | National access across the drinking-water service levels |
| Rural water access     | Rural access across the drinking-water service levels    |
| Urban water access     | Urban access across the drinking-water service levels    |
| Region                 | Regional classification assigned through a lookup table  |

The main Part 2 calculations focus on access to **at least basic drinking-water services** at national, rural and urban levels.

---

## Main Spreadsheet Layers

### `Source Data`

Contains the imported drinking-water observations before the Part 2 transformations.

### `Estimates of the use of water (2000-2020)`

Contains the transformed analytical dataset, including:

* `y_diff`;
* `ARC_n`;
* `ARC_r`;
* `ARC_u`;
* rounded basic-access fields;
* full-access classification fields;
* `ARC_diff`;
* regional classification.

Although the sheet name refers to 2000–2020, its completed analytical observations cover 2015–2020.

### `Regions`

Contains the country-to-region reference table used to assign regional classifications.

### `Summary`

Contains:

* year-frequency analysis;
* year-difference statistics;
* ARC descriptive statistics;
* progress-status counts;
* rural–urban ARC comparison;
* regional aggregations;
* visualisations.

---

## Transformation Workflow

```text
Imported source observations
        ↓
Country-name validation
        ↓
Country and year sorting
        ↓
Two-row country pairing
        ↓
Year-difference calculation
        ↓
National, rural and urban ARC
        ↓
Missing-value and error handling
        ↓
Rounded access variables
        ↓
Full-access classification
        ↓
Country-level ARC_diff
        ↓
Regional lookup
        ↓
Summary calculations
        ↓
Regional aggregation
        ↓
Visualisation and reporting
```

---

## Country-Pair Structure

The transformed table is sorted by:

1. country or area name;
2. observation year.

Each country or area is normally represented by two consecutive rows.

### Earlier observation row

The earlier row generally contains:

* the 2015 observation;
* `y_diff`;
* `ARC_n`;
* `ARC_r`;
* `ARC_u`;
* full-access classifications;
* `ARC_diff`.

### Later observation row

The later row generally contains:

* the later observation year;
* the population value used in the reporting tables;
* blank pair-level derived fields.

The pair-level calculations compare the earlier row with the next row only when both rows contain the same country or area name.

Changing the row order without revalidating the formulas can produce incorrect country comparisons.

---

# Key Derived Features

## `y_diff`

`y_diff` measures the number of years between two observations for the same country or area.

```text
y_diff = later year - earlier year
```

### Analytical purpose

* validates the observation interval;
* identifies zero-year country pairs;
* supplies the denominator for ARC;
* allows comparisons covering different intervals to be annualised.

### Verified results

| Metric       |     Result |
| ------------ | ---------: |
| Mean         | 4.80 years |
| Median       |    5 years |
| Minimum      |     1 year |
| Maximum      |    5 years |
| `y_diff = 0` |          0 |

The absence of zero-year intervals supports the validity of the country-year pairing.

A zero value would require investigation because it could indicate a duplicate country-year record.

---

## Annual Rate of Change

ARC measures the average yearly change in access:

```text
ARC =
(later access value - earlier access value)
/
(later year - earlier year)
```

ARC is expressed in:

> Percentage points per year.

### `ARC_n`

Measures the Annual Rate of Change in national access to at least basic drinking water.

```text
ARC_n =
(later wat_bas_n - earlier wat_bas_n)
/
y_diff
```

### `ARC_r`

Measures the Annual Rate of Change in rural access to at least basic drinking water.

```text
ARC_r =
(later wat_bas_r - earlier wat_bas_r)
/
y_diff
```

### `ARC_u`

Measures the Annual Rate of Change in urban access to at least basic drinking water.

```text
ARC_u =
(later wat_bas_u - earlier wat_bas_u)
/
y_diff
```

---

## Generic ARC Error-Handling Logic

The spreadsheet uses conditional and error-handling logic to avoid invalid cross-country calculations.

A simplified structure is:

```text
IF next country = current country:
    calculate ARC
ELSE:
    return blank
```

When a same-country calculation is expected but a required source value is unavailable, the result is recorded as `Null`.

A generic spreadsheet structure is:

```text
=IFERROR(
    IF(next_name=current_name,
       (later_access-earlier_access)/(later_year-earlier_year),
       ""
    ),
    "Null"
)
```

The precise cell references depend on the spreadsheet columns.

---

## Rounded Basic-Access Fields

The following derived variables round the at-least-basic access estimates to zero decimal places:

* `wat_bas_n_round`;
* `wat_bas_r_round`;
* `wat_bas_u_round`.

Generic formula:

```text
rounded access = ROUND(original access, 0)
```

These variables support the approximate full-access classification.

For example, an estimated value of `99.6` rounds to `100`.

---

## Full-Access Classification

The following fields identify approximate full access:

* `ARC_n_full`;
* `ARC_r_full`;
* `ARC_u_full`.

A country or area is classified as having full access when its rounded access estimate equals 100 in both observations.

```text
earlier rounded access = 100
AND
later rounded access = 100
```

The full-access fields distinguish:

* zero ARC caused by access already being at or near 100%;
* zero ARC below full access.

This prevents full-access cases from being incorrectly classified as stagnation.

---

## `ARC_diff`

`ARC_diff` compares rural and urban ARC for the same country pair:

```text
ARC_diff = ARC_r - ARC_u
```

### Interpretation

| Result         | Meaning                                        |
| -------------- | ---------------------------------------------- |
| `ARC_diff > 0` | Rural ARC is numerically higher than urban ARC |
| `ARC_diff < 0` | Urban ARC is numerically higher than rural ARC |
| `ARC_diff = 0` | Rural and urban ARC are equal                  |
| `Null`         | Rural ARC, urban ARC or both are unavailable   |

A positive difference generally indicates faster rural improvement.

However, if both ARC values are negative, a positive `ARC_diff` may indicate that rural access declined more slowly than urban access.

---

## `region`

The `region` field is assigned through a lookup against the `Regions` reference sheet.

The seven regional groups used in the project are:

* East Asia & Pacific;
* Europe & Central Asia;
* Latin America & Caribbean;
* Middle East & North Africa;
* North America;
* South Asia;
* Sub-Saharan Africa.

The regional lookup supports:

* country and area counts;
* population totals;
* regional ARC averages;
* regional `ARC_diff` averages;
* regional tables;
* charts.

Country-name consistency is essential because differences in spelling, punctuation or formatting can prevent successful lookup matches.

---

## `pop_n (Millions)`

The source population variable is stored in thousands.

For reporting, it is converted into millions:

```text
pop_n (Millions) = pop_n / 1000
```

This field is used in:

* regional tables;
* population summaries;
* the regional population and ARC chart.

---

# Missing-Value Conventions

| Representation | Meaning                                                                      |
| -------------- | ---------------------------------------------------------------------------- |
| Blank cell     | No row-level calculation is expected                                         |
| `Null`         | A calculation was expected, but one or more required values were unavailable |
| `0`            | A valid numerical result of zero                                             |

These values are not interchangeable.

Missing ARC values are not replaced with zero because doing so would incorrectly classify unavailable observations as no change.

---

## Verified ARC Completeness

| Measure           | Valid | Missing | Total country pairs |
| ----------------- | ----: | ------: | ------------------: |
| National ARC      |   229 |       2 |                 231 |
| Rural ARC         |   167 |      64 |                 231 |
| Urban ARC         |   181 |      50 |                 231 |
| Paired `ARC_diff` |   165 |      66 |                 231 |

Rural and urban access estimates are less complete than national estimates.

Because the valid national, rural and urban samples differ, their averages must be compared cautiously.

---

# ARC Descriptive Results

| Metric         | National ARC | Rural ARC | Urban ARC |
| -------------- | -----------: | --------: | --------: |
| Valid values   |          229 |       167 |       181 |
| Missing values |            2 |        64 |        50 |
| Mean           |        0.277 |     0.484 |     0.155 |
| Median         |        0.079 |     0.290 |     0.030 |
| Minimum        |       -1.022 |    -1.227 |    -1.620 |
| Maximum        |        2.750 |     2.668 |     2.668 |

The rural mean and median are higher than the national and urban values.

This indicates stronger rural change on average, but it does not mean that rural access levels are higher than urban access levels.

---

# Summary Classification Logic

The Summary classifies the 231 country pairs into five mutually exclusive categories.

| Category                       | Definition                                                     |
| ------------------------------ | -------------------------------------------------------------- |
| Missing ARC                    | ARC could not be calculated                                    |
| Full access                    | Rounded basic access equals 100 in both observations           |
| Zero ARC below full access     | No measured change and not classified as full access           |
| Negative ARC below full access | Access declined and the pair is not classified as full access  |
| Positive ARC below full access | Access increased and the pair is not classified as full access |

### Verified counts

| Classification                 | National |   Rural |   Urban |
| ------------------------------ | -------: | ------: | ------: |
| Missing ARC                    |        2 |      64 |      50 |
| Full access                    |       62 |      29 |      55 |
| Zero ARC below full access     |       16 |       5 |       7 |
| Negative ARC below full access |       16 |      17 |      26 |
| Positive ARC below full access |      135 |     116 |      93 |
| **Total**                      |  **231** | **231** | **231** |

Validation rule:

```text
Missing ARC
+ Full access
+ Zero ARC below full access
+ Negative ARC below full access
+ Positive ARC below full access
= 231 country pairs
```

---

# Paired Rural–Urban Results

| Metric                  | Result |
| ----------------------- | -----: |
| Valid `ARC_diff` values |    165 |
| Missing values          |     66 |
| Positive differences    |    112 |
| Negative differences    |     23 |
| Zero differences        |     30 |
| Mean                    |  0.321 |
| Median                  |  0.212 |
| Minimum                 | -2.489 |
| Maximum                 |  2.329 |

Most valid paired observations have a positive `ARC_diff`.

This is consistent with rural ARC being numerically higher in most countries with complete rural and urban measurements.

It does not prove that rural access levels have reached urban access levels.

---

# Regional Aggregation

The transformed variables support the following regional indicators:

| Regional indicator            | Source fields        | Aggregation                         |
| ----------------------------- | -------------------- | ----------------------------------- |
| Number of countries and areas | `name`, `region`     | Count                               |
| Regional population           | `pop_n`, `region`    | Sum                                 |
| Average national ARC          | `ARC_n`, `region`    | Average of valid values             |
| Average rural ARC             | `ARC_r`, `region`    | Average of valid values             |
| Average urban ARC             | `ARC_u`, `region`    | Average of valid values             |
| Average paired ARC difference | `ARC_diff`, `region` | Average of valid paired differences |

Regional ARC values are unweighted country averages unless stated otherwise.

A small country and a highly populated country contribute equally to their regional ARC average.

The regional population field supplies contextual scale but does not weight the ARC calculations.

---

## Paired and Independent Regional Calculations

Two regional rural–urban calculations appear in the project.

### Average paired difference

```text
AVERAGE(country-level ARC_r - ARC_u)
```

This includes only countries with both rural and urban ARC.

### Difference between independent averages

```text
AVERAGE(valid ARC_r)
-
AVERAGE(valid ARC_u)
```

The rural and urban averages may use different country samples.

The two results are therefore not necessarily equal and should not be treated as interchangeable.

---

# Data-Quality Considerations

## Unequal Observation Intervals

Country pairs cover intervals ranging from one to five years.

ARC annualises access change using the actual interval.

## Missing Source Values

Some national, rural or urban source estimates are unavailable.

Controlled error handling preserves these cases as `Null`.

## Country-Name Matching

Country pairing and regional lookups depend on consistent country names.

Changes in:

* spelling;
* punctuation;
* spacing;
* naming conventions

can prevent valid matches.

## Row-Order Dependency

The formulas depend on the data being sorted correctly by country and year.

Sorting the transformed sheet incorrectly without updating the formulas could pair unrelated observations.

## Rounded Full-Access Classification

Full access is based on access values rounded to zero decimal places.

This is an analytical classification and should not be interpreted as proof that the unrounded estimate equals exactly 100%.

## Outliers

Large positive and negative ARC values can affect means.

Medians should be reported alongside averages to provide a more robust measure of central tendency.

## Regional Averaging

Regional ARC values are simple country averages.

They do not represent the progress experienced by the average person in a region.

## Baseline and Final Access

ARC measures change rather than access level.

A high ARC can coexist with low final access, while a low ARC can reflect either stagnation or limited remaining room for improvement.

## Causality

The dataset is descriptive and observational.

The analysis identifies patterns but does not establish why access increased or decreased.

---

# Repository Reproducibility Status

The current `data/` folder contains documentation only.

The machine-readable source and transformed datasets are not currently stored in this GitHub folder.

The repository instead provides:

* the external Google Sheets workbook;
* data documentation;
* a variable dictionary;
* PDF sheet exports;
* visual assets;
* regional table screenshots;
* an analytical report.

This keeps the repository lightweight but creates an external dependency.

Full reproducibility depends on continued access to the linked Google Sheets workbook.

---

## Recommended Reproducibility Improvements

Future repository versions should add:

* source-data export in CSV format;
* transformed dataset in CSV format;
* Summary calculations in CSV format;
* Regions lookup table in CSV format;
* spreadsheet export preserving formulas;
* source download date;
* source dataset version;
* licence or reuse information;
* validation checks for row counts and country pairs.

These additions would allow another analyst to reproduce the project without relying exclusively on the external workbook.

---

# Data Dictionary

Complete variable-level documentation is available here:

[Open the Data Dictionary](./data_dictionary.md)

The data dictionary documents:

* variable names;
* original or derived status;
* definitions;
* data types;
* units;
* formulas;
* missing-value behaviour;
* analytical purpose.

---

# Units Summary

| Variable group         | Unit                       |
| ---------------------- | -------------------------- |
| `year`                 | Calendar year              |
| `y_diff`               | Years                      |
| `pop_n`                | Thousands of people        |
| `pop_n (Millions)`     | Millions of people         |
| `pop_u`                | Percentage                 |
| Water-access variables | Percentage                 |
| `ARC_n`                | Percentage points per year |
| `ARC_r`                | Percentage points per year |
| `ARC_u`                | Percentage points per year |
| `ARC_diff`             | Percentage points per year |

---

# Related Project Outputs

## Visual Assets

[Open the Assets folder](../assets/)

Contains:

* the four principal charts;
* regional table screenshots;
* supporting visual documentation.

## Main Visuals

[Open the Main Visuals documentation](../assets/main_visuals/README.md)

Contains the detailed analysis of the four principal charts.

## Regional ARC Tables

[Open the Regional ARC Tables documentation](../assets/regional_arc_tables/README.md)

Contains country-level examples and screenshot-coverage limitations.

## Reports

[Open the Reports folder](../reports/)

Contains:

* the Part 2 analytical report;
* PDF exports of the spreadsheet sheets;
* reporting documentation.

## Part 2 Project Overview

[Back to the Part 2 project](../README.md)

---

# Notes

* The analysed observations cover 2015–2020.
* The source sheet title refers to 2000–2020.
* The dataset contains 231 country pairs and 462 country-year observations.
* ARC is expressed in percentage points per year.
* Missing values are retained and are not interpreted as zero.
* Full-access classifications use rounded access estimates.
* National, rural and urban averages may contain different valid-country samples.
* Regional ARC values are unweighted country averages.
* ARC measures change rather than final access.
* Population provides context but does not measure the number of beneficiaries.
* The analysis is descriptive and does not establish causality.

---

# Navigation

* [Open Data Dictionary](./data_dictionary.md)
* [Open Assets](../assets/)
* [Open Analytical Report](../reports/analytical_report/Part2_Analytical_Report.md)
* [Open Sheet Exports](../reports/sheet_exports/)
* [Back to Part 2](../README.md)
