# Data Dictionary — Part 2: Transforming the Data

This document defines the original and derived variables used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis uses country- and area-level drinking-water access estimates associated with the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

The transformed dataset supports:

* country-year pairing;
* observation-interval validation;
* Annual Rate of Change calculations;
* missing-value handling;
* approximate full-access classification;
* rural–urban comparison;
* regional enrichment;
* regional aggregation;
* visual reporting.

---

## Dataset Scope

The transformed analytical subset contains:

| Measure                          | Result |
| -------------------------------- | -----: |
| Countries and areas              |    231 |
| Country-year observations        |    462 |
| Observations per country or area |      2 |
| Earliest analysed year           |   2015 |
| Latest analysed year             |   2020 |
| Country pairs                    |    231 |

The transformed sheet is titled:

```text
Estimates of the use of water (2000-2020)
```

However, the final analysed observations cover **2015–2020**.

---

## Dataset Grain

Each source row represents:

> One country or area observed in one specific year.

The transformed data is sorted by:

1. country or area name;
2. observation year in ascending order.

Each country or area normally has:

* one 2015 baseline row;
* one later row between 2016 and 2020.

This two-row structure allows the earlier observation to be compared with the next row when both rows contain the same country or area name.

---

## Variable Inventory

The core transformed dataset contains:

| Variable category                       | Number of variables |
| --------------------------------------- | ------------------: |
| Identification and population variables |                   4 |
| National water-access variables         |                   4 |
| Rural water-access variables            |                   4 |
| Urban water-access variables            |                   4 |
| Time and ARC variables                  |                   4 |
| Rounded access variables                |                   3 |
| Full-access classification variables    |                   3 |
| Rural–urban difference                  |                   1 |
| Regional classification                 |                   1 |
| **Core total**                          |              **28** |

A separate reporting-only field converts population from thousands to millions.

---

# Naming Conventions

## Population-Area Suffixes

| Suffix | Population area |
| ------ | --------------- |
| `_n`   | National        |
| `_r`   | Rural           |
| `_u`   | Urban           |

## Drinking-Water Service Abbreviations

| Abbreviation | Service level  |
| ------------ | -------------- |
| `bas`        | At least basic |
| `lim`        | Limited        |
| `unimp`      | Unimproved     |
| `sur`        | Surface water  |

Example:

```text
wat_bas_r
```

means the rural population share with access to at least basic drinking-water services.

---

# Original Variables

## Identification and Population Variables

| Variable | Status   | Data type         | Unit                | Definition                                             | Missing-value behaviour                                                 |
| -------- | -------- | ----------------- | ------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------- |
| `name`   | Original | Text              | Not applicable      | Country or area name                                   | Expected to be present because pairing and regional lookup depend on it |
| `year`   | Original | Integer           | Calendar year       | Year associated with the observation                   | A missing year prevents time-based comparison                           |
| `pop_n`  | Original | Numeric or `Null` | Thousands of people | National population estimate                           | Missing population remains unavailable                                  |
| `pop_u`  | Original | Numeric or `Null` | Percentage          | Share of the national population living in urban areas | Missing values are not treated as zero                                  |

---

## National Water-Access Variables

| Variable      | Status   | Data type         | Unit       | Definition                                                                      | Part 2 use                         |
| ------------- | -------- | ----------------- | ---------- | ------------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_n`   | Original | Numeric or `Null` | Percentage | National population share with access to at least basic drinking-water services | Used to calculate `ARC_n`          |
| `wat_lim_n`   | Original | Numeric or `Null` | Percentage | National population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_n` | Original | Numeric or `Null` | Percentage | National population share using unimproved drinking-water sources               | Retained for service-level context |
| `wat_sur_n`   | Original | Numeric or `Null` | Percentage | National population share using surface water                                   | Retained for service-level context |

---

## Rural Water-Access Variables

| Variable      | Status   | Data type         | Unit       | Definition                                                                   | Part 2 use                         |
| ------------- | -------- | ----------------- | ---------- | ---------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_r`   | Original | Numeric or `Null` | Percentage | Rural population share with access to at least basic drinking-water services | Used to calculate `ARC_r`          |
| `wat_lim_r`   | Original | Numeric or `Null` | Percentage | Rural population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_r` | Original | Numeric or `Null` | Percentage | Rural population share using unimproved drinking-water sources               | Retained for service-level context |
| `wat_sur_r`   | Original | Numeric or `Null` | Percentage | Rural population share using surface water                                   | Retained for service-level context |

---

## Urban Water-Access Variables

| Variable      | Status   | Data type         | Unit       | Definition                                                                   | Part 2 use                         |
| ------------- | -------- | ----------------- | ---------- | ---------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_u`   | Original | Numeric or `Null` | Percentage | Urban population share with access to at least basic drinking-water services | Used to calculate `ARC_u`          |
| `wat_lim_u`   | Original | Numeric or `Null` | Percentage | Urban population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_u` | Original | Numeric or `Null` | Percentage | Urban population share using unimproved drinking-water sources               | Retained for service-level context |
| `wat_sur_u`   | Original | Numeric or `Null` | Percentage | Urban population share using surface water                                   | Retained for service-level context |

---

# Derived Variables

## `y_diff`

| Property       | Description                                                                             |
| -------------- | --------------------------------------------------------------------------------------- |
| Status         | Derived                                                                                 |
| Data type      | Integer or blank                                                                        |
| Unit           | Years                                                                                   |
| Definition     | Difference between the later and earlier observation years for the same country or area |
| Analytical use | Validates the comparison interval and provides the ARC denominator                      |

### Logical formula

```text
If next country name = current country name:
    y_diff = next year - current year
Else:
    return blank
```

### Generic Google Sheets structure

```text
=IF(next_name=current_name, next_year-current_year, "")
```

### Interpretation

| Result       | Meaning                                                        |
| ------------ | -------------------------------------------------------------- |
| `y_diff > 0` | Valid positive observation interval                            |
| `y_diff = 0` | Possible duplicate country-year record requiring investigation |
| Blank        | The current row does not begin a valid same-country pair       |

### Verified results

| Metric              |     Result |
| ------------------- | ---------: |
| Mean                | 4.80 years |
| Median              |    5 years |
| Minimum             |     1 year |
| Maximum             |    5 years |
| Zero-year intervals |          0 |

---

## `ARC_n`

| Property       | Description                                                               |
| -------------- | ------------------------------------------------------------------------- |
| Status         | Derived                                                                   |
| Data type      | Numeric, `Null` or blank                                                  |
| Unit           | Percentage points per year                                                |
| Definition     | Annual Rate of Change in national access to at least basic drinking water |
| Analytical use | Measures the direction and speed of national access change                |

### Logical formula

```text
ARC_n =
(later wat_bas_n - earlier wat_bas_n)
/
y_diff
```

### Interpretation

| Result      | Meaning                                                                   |
| ----------- | ------------------------------------------------------------------------- |
| `ARC_n > 0` | National basic access increased                                           |
| `ARC_n = 0` | No measured national change                                               |
| `ARC_n < 0` | National basic access decreased                                           |
| `Null`      | The calculation was expected, but a required source value was unavailable |
| Blank       | The row does not begin a same-country pair                                |

A zero ARC does not independently indicate whether the country is below or at full access. The full-access classification must also be consulted.

---

## `ARC_r`

| Property       | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| Status         | Derived                                                                |
| Data type      | Numeric, `Null` or blank                                               |
| Unit           | Percentage points per year                                             |
| Definition     | Annual Rate of Change in rural access to at least basic drinking water |
| Analytical use | Measures the direction and speed of rural access change                |

### Logical formula

```text
ARC_r =
(later wat_bas_r - earlier wat_bas_r)
/
y_diff
```

### Interpretation

| Result      | Meaning                                       |
| ----------- | --------------------------------------------- |
| `ARC_r > 0` | Rural basic access increased                  |
| `ARC_r = 0` | No measured rural change                      |
| `ARC_r < 0` | Rural basic access decreased                  |
| `Null`      | A required rural source value was unavailable |
| Blank       | The row does not begin a same-country pair    |

---

## `ARC_u`

| Property       | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| Status         | Derived                                                                |
| Data type      | Numeric, `Null` or blank                                               |
| Unit           | Percentage points per year                                             |
| Definition     | Annual Rate of Change in urban access to at least basic drinking water |
| Analytical use | Measures the direction and speed of urban access change                |

### Logical formula

```text
ARC_u =
(later wat_bas_u - earlier wat_bas_u)
/
y_diff
```

### Interpretation

| Result      | Meaning                                       |
| ----------- | --------------------------------------------- |
| `ARC_u > 0` | Urban basic access increased                  |
| `ARC_u = 0` | No measured urban change                      |
| `ARC_u < 0` | Urban basic access decreased                  |
| `Null`      | A required urban source value was unavailable |
| Blank       | The row does not begin a same-country pair    |

---

# ARC Error Handling

Some source values are represented by the text value:

```text
Null
```

Arithmetic involving text can produce spreadsheet errors. The ARC formulas therefore use conditional and error-handling logic.

### Generic structure

```text
=IFERROR(
    IF(next_name=current_name,
       (later_access-earlier_access)/(later_year-earlier_year),
       ""
    ),
    "Null"
)
```

### Output meanings

| Output        | Meaning                                                                       |
| ------------- | ----------------------------------------------------------------------------- |
| Numeric value | Valid ARC calculation                                                         |
| Blank         | No calculation is expected because the row does not begin a same-country pair |
| `Null`        | A calculation was expected, but one or more required values were unavailable  |

Blank, `Null` and numerical zero must remain distinct.

---

# Rounded Access Variables

## `wat_bas_n_round`

| Property        | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| Status          | Derived                                                       |
| Data type       | Integer, `Null` or blank                                      |
| Unit            | Percentage                                                    |
| Definition      | National basic-access estimate rounded to zero decimal places |
| Logical formula | `ROUND(wat_bas_n, 0)`                                         |
| Analytical use  | Supports approximate national full-access classification      |

An estimate such as `99.6` rounds to `100`.

---

## `wat_bas_r_round`

| Property        | Description                                                |
| --------------- | ---------------------------------------------------------- |
| Status          | Derived                                                    |
| Data type       | Integer, `Null` or blank                                   |
| Unit            | Percentage                                                 |
| Definition      | Rural basic-access estimate rounded to zero decimal places |
| Logical formula | `ROUND(wat_bas_r, 0)`                                      |
| Analytical use  | Supports approximate rural full-access classification      |

---

## `wat_bas_u_round`

| Property        | Description                                                |
| --------------- | ---------------------------------------------------------- |
| Status          | Derived                                                    |
| Data type       | Integer, `Null` or blank                                   |
| Unit            | Percentage                                                 |
| Definition      | Urban basic-access estimate rounded to zero decimal places |
| Logical formula | `ROUND(wat_bas_u, 0)`                                      |
| Analytical use  | Supports approximate urban full-access classification      |

---

# Full-Access Classification Variables

The full-access variables use the rounded basic-access estimates.

A country or area is classified as having approximate full access when the rounded estimate equals 100 in both observations.

These flags are analytical classifications. They do not mean that the original unrounded values are exactly 100.

---

## `ARC_n_full`

| Property       | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| Status         | Derived classification                                                 |
| Data type      | Text or blank                                                          |
| Possible value | `full access`                                                          |
| Definition     | Identifies approximate full national basic access in both observations |
| Analytical use | Separates full-access cases from zero national ARC below full access   |

### Logical formula

```text
If country names match
AND earlier wat_bas_n_round = 100
AND later wat_bas_n_round = 100:
    return "full access"
Else:
    return blank
```

---

## `ARC_r_full`

| Property       | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| Status         | Derived classification                                              |
| Data type      | Text or blank                                                       |
| Possible value | `full access`                                                       |
| Definition     | Identifies approximate full rural basic access in both observations |
| Analytical use | Separates full rural access from zero rural ARC below full access   |

### Logical formula

```text
If country names match
AND earlier wat_bas_r_round = 100
AND later wat_bas_r_round = 100:
    return "full access"
Else:
    return blank
```

---

## `ARC_u_full`

| Property       | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| Status         | Derived classification                                              |
| Data type      | Text or blank                                                       |
| Possible value | `full access`                                                       |
| Definition     | Identifies approximate full urban basic access in both observations |
| Analytical use | Separates full urban access from zero urban ARC below full access   |

### Logical formula

```text
If country names match
AND earlier wat_bas_u_round = 100
AND later wat_bas_u_round = 100:
    return "full access"
Else:
    return blank
```

---

# Rural–Urban Difference

## `ARC_diff`

| Property       | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| Status         | Derived                                                          |
| Data type      | Numeric, `Null` or blank                                         |
| Unit           | Percentage points per year                                       |
| Definition     | Difference between rural and urban ARC for the same country pair |
| Analytical use | Compares rural and urban rates of change                         |

### Formula

```text
ARC_diff = ARC_r - ARC_u
```

### Pair-aware logical structure

```text
If next country name = current country name:
    If ARC_r and ARC_u are valid:
        ARC_diff = ARC_r - ARC_u
    Else:
        return "Null"
Else:
    return blank
```

### Generic Google Sheets structure

```text
=IF(
    next_name=current_name,
    IFERROR(ARC_r-ARC_u, "Null"),
    ""
)
```

### Interpretation

| Result         | Meaning                                        |
| -------------- | ---------------------------------------------- |
| `ARC_diff > 0` | Rural ARC is numerically higher than urban ARC |
| `ARC_diff < 0` | Urban ARC is numerically higher than rural ARC |
| `ARC_diff = 0` | Rural and urban ARC are equal                  |
| `Null`         | Rural ARC, urban ARC or both are unavailable   |
| Blank          | The row does not begin a same-country pair     |

A positive `ARC_diff` normally indicates faster rural improvement.

However, if both rural and urban ARC are negative, a positive difference can indicate that rural access declined more slowly than urban access.

`ARC_diff` compares rates of change. It does not compare rural and urban access levels.

---

# Regional Classification

## `region`

| Property       | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| Status         | Derived through lookup                                           |
| Data type      | Text                                                             |
| Unit           | Not applicable                                                   |
| Definition     | Regional classification assigned to each country or area         |
| Source         | Separate `Regions` reference sheet                               |
| Analytical use | Supports regional grouping, tables, summaries and visualisations |

### Transformation logic

```text
Lookup country or area name
in the Regions reference table
and return its regional classification
```

The lookup depends on exact country-name matching.

### Regions used in the project

* East Asia & Pacific;
* Europe & Central Asia;
* Latin America & Caribbean;
* Middle East & North Africa;
* North America;
* South Asia;
* Sub-Saharan Africa.

### Quality consideration

The regional classification reflects the project’s `Regions` lookup table.

It should not be assumed to match another organisation’s regional classification system unless the mappings are explicitly compared.

---

# Reporting-Only Derived Field

## `pop_n (Millions)`

| Property       | Description                                                           |
| -------------- | --------------------------------------------------------------------- |
| Status         | Derived for reporting                                                 |
| Data type      | Numeric                                                               |
| Unit           | Millions of people                                                    |
| Definition     | National population converted from thousands into millions            |
| Formula        | `pop_n / 1000`                                                        |
| Analytical use | Improves readability in regional tables and population visualisations |

### Example

```text
pop_n = 1,463,140.5 thousand
pop_n (Millions) = 1,463.1405 million
```

This field is used in the reporting and Summary layers and may not be part of the core 28-variable transformed dataset.

---

# Summary Classification Logic

The Summary classifies national, rural and urban ARC observations into five mutually exclusive categories.

| Category                       | Definition                                                    |
| ------------------------------ | ------------------------------------------------------------- |
| Missing ARC                    | ARC is unavailable or recorded as `Null`                      |
| Full access                    | Rounded access equals 100 in both observations                |
| Zero ARC below full access     | ARC equals zero and the pair is not classified as full access |
| Negative ARC below full access | ARC is negative and the pair is not classified as full access |
| Positive ARC below full access | ARC is positive and the pair is not classified as full access |

### Validation rule

```text
Missing ARC
+ Full access
+ Zero ARC below full access
+ Negative ARC below full access
+ Positive ARC below full access
= Total country pairs
```

### Verified classification counts

| Classification                 | National |   Rural |   Urban |
| ------------------------------ | -------: | ------: | ------: |
| Missing ARC                    |        2 |      64 |      50 |
| Full access                    |       62 |      29 |      55 |
| Zero ARC below full access     |       16 |       5 |       7 |
| Negative ARC below full access |       16 |      17 |      26 |
| Positive ARC below full access |      135 |     116 |      93 |
| **Total**                      |  **231** | **231** | **231** |

---

# Regional Aggregation Fields

| Regional indicator            | Source fields        | Aggregation                                               |
| ----------------------------- | -------------------- | --------------------------------------------------------- |
| Number of countries and areas | `name`, `region`     | Unique country or area count                              |
| Regional population           | `pop_n`, `region`    | Sum of one reporting population value per country or area |
| Average national ARC          | `ARC_n`, `region`    | Average of valid national ARC                             |
| Average rural ARC             | `ARC_r`, `region`    | Average of valid rural ARC                                |
| Average urban ARC             | `ARC_u`, `region`    | Average of valid urban ARC                                |
| Average paired ARC difference | `ARC_diff`, `region` | Average of valid country-level paired differences         |

Regional ARC values are simple country averages unless explicitly stated otherwise.

They are not population-weighted.

---

## Paired Versus Independent Regional Calculations

The regional average `ARC_diff` is:

```text
AVERAGE(country-level ARC_r - ARC_u)
```

It includes only countries with valid rural and urban ARC.

The rural-versus-urban regional chart independently calculates:

```text
AVERAGE(valid ARC_r)
```

and:

```text
AVERAGE(valid ARC_u)
```

Because these averages may contain different country samples:

```text
AVERAGE(ARC_r - ARC_u)
```

is not necessarily equal to:

```text
AVERAGE(ARC_r) - AVERAGE(ARC_u)
```

---

# Missing-Value Conventions

| Representation | Meaning                                                                  |
| -------------- | ------------------------------------------------------------------------ |
| Blank          | No row-level calculation is expected                                     |
| `Null`         | A required value was unavailable or a calculation could not be completed |
| `0`            | A valid measured numerical value of zero                                 |
| `full access`  | Derived classification based on rounded access values                    |

Missing values must not be replaced with zero.

Replacing `Null` with zero would incorrectly classify unavailable data as no change.

---

# Verified Completeness

| Derived measure | Valid | Missing | Total country pairs |
| --------------- | ----: | ------: | ------------------: |
| `ARC_n`         |   229 |       2 |                 231 |
| `ARC_r`         |   167 |      64 |                 231 |
| `ARC_u`         |   181 |      50 |                 231 |
| `ARC_diff`      |   165 |      66 |                 231 |

Rural and urban observations are less complete than national observations.

---

# Units Summary

| Variable or group      | Unit                       |
| ---------------------- | -------------------------- |
| `name`                 | Not applicable             |
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
| `region`               | Not applicable             |
| Full-access flags      | Text classification        |

---

# Main Analytical Relationships

```text
y_diff = later year - earlier year
```

```text
ARC_n =
(later wat_bas_n - earlier wat_bas_n)
/
y_diff
```

```text
ARC_r =
(later wat_bas_r - earlier wat_bas_r)
/
y_diff
```

```text
ARC_u =
(later wat_bas_u - earlier wat_bas_u)
/
y_diff
```

```text
ARC_diff = ARC_r - ARC_u
```

```text
pop_n (Millions) = pop_n / 1000
```

---

# Data-Quality Considerations

## Country-Name Consistency

Country names must match:

* between the two observations;
* between the transformed data and the `Regions` lookup table.

Formatting differences can cause:

* failed country pairing;
* missing regional assignments;
* invalid row comparisons.

## Row Ordering

Pair-based calculations depend on the dataset being sorted by country and year.

Changing the row order without updating or validating the formulas can create incorrect comparisons.

## Unequal Observation Intervals

Observation intervals range from one to five years.

`y_diff` annualises the raw changes using the actual interval.

## Duplicate Observations

A same-country `y_diff` of zero may indicate a duplicate country-year record.

The verified dataset contains no zero-year pairs.

## Missing Values

National, rural and urban variables have different missing-value patterns.

As a result:

* ARC completeness differs by area;
* regional rural and urban averages may contain different countries;
* paired `ARC_diff` has fewer valid values.

## Estimated Values Near 100%

Rounded variables support approximate full-access classification.

A rounded value of 100 does not prove that the original estimate equals exactly 100.

## Outliers

Extreme positive and negative ARC values can influence averages.

Medians should be interpreted alongside means.

## Regional Averages

Each valid country contributes equally to an unweighted regional ARC average.

The averages do not represent the progress experienced by the average regional resident.

## Population Context

Population provides contextual scale but is not used to weight the ARC values in the current regional charts.

## Baseline and Final Access

ARC measures change rather than the final level of access.

A country can have:

* high ARC and low final access;
* low ARC and high final access;
* zero ARC at approximate full access;
* zero ARC below full access.

## Causality

The data is descriptive and observational.

The analysis identifies patterns but does not establish why access increased or decreased.

---

# Related Documentation

## Data Overview

[Open Data README](./README.md)

Documents the dataset scope, workflow, completeness and data-quality considerations.

## Visual Assets

[Open Assets](../assets/)

Contains the principal charts and regional table screenshots.

## Main Visuals

[Open Main Visuals documentation](../assets/main_visuals/README.md)

Documents the four principal charts.

## Regional ARC Tables

[Open Regional ARC Tables documentation](../assets/regional_arc_tables/README.md)

Documents the regional screenshots and their coverage limitations.

## Analytical Report

[Open Part 2 Analytical Report](../reports/analytical_report/Part2_Analytical_Report.md)

## Sheet Exports

[Open Spreadsheet Exports](../reports/sheet_exports/)

## Working Spreadsheet

[Open Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

## Part 2 Overview

[Back to Part 2](../README.md)

---

# Notes

* The analysed observations cover 2015–2020.
* The transformed sheet title refers to 2000–2020.
* The core transformed dataset contains 28 variables.
* `pop_n (Millions)` is a reporting-only conversion.
* ARC is expressed in percentage points per year.
* Blank, `Null` and zero have different meanings.
* Full-access flags use rounded estimates.
* `ARC_diff` compares rates of change rather than access levels.
* Rural and urban regional averages may use different country samples.
* Regional ARC values are unweighted country averages.
* Population is contextual and does not measure the number of beneficiaries.
* The analysis is descriptive and does not establish causality.

---

# Navigation

* [Back to Data Overview](./README.md)
* [Open Assets](../assets/)
* [Open Analytical Report](../reports/analytical_report/Part2_Analytical_Report.md)
* [Open Sheet Exports](../reports/sheet_exports/)
* [Back to Part 2](../README.md)
