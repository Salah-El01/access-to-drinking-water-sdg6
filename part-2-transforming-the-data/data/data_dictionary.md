# Data Dictionary — Part 2: Transforming the Data

This document defines the original and derived variables used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis uses country- and area-level drinking-water access estimates from the **WHO/UNICEF Joint Monitoring Programme (JMP)**. The transformed dataset supports time-based analysis through year differences, Annual Rates of Change, full-access classification, rural–urban comparison, and regional enrichment.

---

## Dataset Grain

Each source row represents:

> One country or area observed in one specific year.

Most countries are represented by two observations, generally an earlier year and a later year. The dataset is sorted by:

1. country or area name;
2. observation year in ascending order.

This ordering allows row-to-row calculations between observations belonging to the same country.

---

## Naming Conventions

Water-access variables use suffixes to identify the population area:

| Suffix | Population area |
| ------ | --------------- |
| `_n`   | National        |
| `_r`   | Rural           |
| `_u`   | Urban           |

Service-level abbreviations include:

| Abbreviation | Service level  |
| ------------ | -------------- |
| `bas`        | At least basic |
| `lim`        | Limited        |
| `unimp`      | Unimproved     |
| `sur`        | Surface water  |

Example:

`wat_bas_r` represents the rural population share with access to at least basic drinking-water services.

---

# Original Variables

## Identification and Population Variables

| Variable | Status   | Data type | Unit                | Definition                                             | Missing-value behavior                                                |
| -------- | -------- | --------- | ------------------- | ------------------------------------------------------ | --------------------------------------------------------------------- |
| `name`   | Original | Text      | Not applicable      | Country or area name                                   | Expected to be present because country matching depends on this field |
| `year`   | Original | Integer   | Calendar year       | Year associated with the observation                   | Missing years prevent time-based comparison                           |
| `pop_n`  | Original | Numeric   | Thousands of people | National population estimate                           | May be unavailable for selected observations                          |
| `pop_u`  | Original | Numeric   | Percentage          | Share of the national population living in urban areas | Missing values remain unavailable and are not treated as zero         |

---

## National Water-Access Variables

| Variable      | Status   | Data type | Unit       | Definition                                                                      | Analytical use                     |
| ------------- | -------- | --------- | ---------- | ------------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_n`   | Original | Numeric   | Percentage | National population share with access to at least basic drinking-water services | Used to calculate `ARC_n`          |
| `wat_lim_n`   | Original | Numeric   | Percentage | National population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_n` | Original | Numeric   | Percentage | National population share relying on unimproved drinking-water sources          | Retained for service-level context |
| `wat_sur_n`   | Original | Numeric   | Percentage | National population share relying on surface water                              | Retained for service-level context |

---

## Rural Water-Access Variables

| Variable      | Status   | Data type | Unit       | Definition                                                                   | Analytical use                     |
| ------------- | -------- | --------- | ---------- | ---------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_r`   | Original | Numeric   | Percentage | Rural population share with access to at least basic drinking-water services | Used to calculate `ARC_r`          |
| `wat_lim_r`   | Original | Numeric   | Percentage | Rural population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_r` | Original | Numeric   | Percentage | Rural population share relying on unimproved drinking-water sources          | Retained for service-level context |
| `wat_sur_r`   | Original | Numeric   | Percentage | Rural population share relying on surface water                              | Retained for service-level context |

---

## Urban Water-Access Variables

| Variable      | Status   | Data type | Unit       | Definition                                                                   | Analytical use                     |
| ------------- | -------- | --------- | ---------- | ---------------------------------------------------------------------------- | ---------------------------------- |
| `wat_bas_u`   | Original | Numeric   | Percentage | Urban population share with access to at least basic drinking-water services | Used to calculate `ARC_u`          |
| `wat_lim_u`   | Original | Numeric   | Percentage | Urban population share with limited drinking-water access                    | Retained for service-level context |
| `wat_unimp_u` | Original | Numeric   | Percentage | Urban population share relying on unimproved drinking-water sources          | Retained for service-level context |
| `wat_sur_u`   | Original | Numeric   | Percentage | Urban population share relying on surface water                              | Retained for service-level context |

---

# Derived Variables

## `y_diff`

| Property       | Description                                                                       |
| -------------- | --------------------------------------------------------------------------------- |
| Status         | Derived                                                                           |
| Data type      | Integer                                                                           |
| Unit           | Years                                                                             |
| Definition     | Difference between the later and earlier observation years for the same country   |
| Analytical use | Validates observation intervals and provides the denominator for ARC calculations |

### Transformation logic

```text
If next country name = current country name:
    y_diff = next year - current year
Else:
    return blank
```

Generic Google Sheets structure:

```text
=IF(next_name=current_name, next_year-current_year, "")
```

### Interpretation

* `y_diff > 0` indicates a valid time interval.
* `y_diff = 0` may indicate a duplicate country-year record.
* A blank value normally indicates that the next row belongs to another country.

---

## `ARC_n`

| Property       | Description                                                               |
| -------------- | ------------------------------------------------------------------------- |
| Status         | Derived                                                                   |
| Data type      | Numeric                                                                   |
| Unit           | Percentage points per year                                                |
| Definition     | Annual Rate of Change in national access to at least basic drinking water |
| Analytical use | Measures the direction and speed of national progress                     |

### Formula

```text
ARC_n =
(later wat_bas_n - earlier wat_bas_n)
/
(later year - earlier year)
```

### Interpretation

* `ARC_n > 0`: national basic access improved.
* `ARC_n = 0`: no measured change or already full access.
* `ARC_n < 0`: national basic access declined.
* `Null`: the calculation could not be completed because a required source value was unavailable.

---

## `ARC_r`

| Property       | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| Status         | Derived                                                                |
| Data type      | Numeric                                                                |
| Unit           | Percentage points per year                                             |
| Definition     | Annual Rate of Change in rural access to at least basic drinking water |
| Analytical use | Measures the direction and speed of rural progress                     |

### Formula

```text
ARC_r =
(later wat_bas_r - earlier wat_bas_r)
/
(later year - earlier year)
```

### Interpretation

* `ARC_r > 0`: rural basic access improved.
* `ARC_r = 0`: no measured change or already full access.
* `ARC_r < 0`: rural basic access declined.
* `Null`: the calculation could not be completed.

---

## `ARC_u`

| Property       | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| Status         | Derived                                                                |
| Data type      | Numeric                                                                |
| Unit           | Percentage points per year                                             |
| Definition     | Annual Rate of Change in urban access to at least basic drinking water |
| Analytical use | Measures the direction and speed of urban progress                     |

### Formula

```text
ARC_u =
(later wat_bas_u - earlier wat_bas_u)
/
(later year - earlier year)
```

### Interpretation

* `ARC_u > 0`: urban basic access improved.
* `ARC_u = 0`: no measured change or already full access.
* `ARC_u < 0`: urban basic access declined.
* `Null`: the calculation could not be completed.

---

## ARC Formula Error Handling

The source dataset contains missing values represented as text, such as `Null`.

Arithmetic involving text values can produce spreadsheet errors. ARC formulas therefore use controlled error handling.

Generic structure:

```text
=IFERROR(
    IF(next_name=current_name,
       (later_access-earlier_access)/(later_year-earlier_year),
       ""
    ),
    "Null"
)
```

A blank value and a `Null` value have different meanings:

| Value  | Meaning                                                                             |
| ------ | ----------------------------------------------------------------------------------- |
| Blank  | No calculation is expected because the row does not begin a valid same-country pair |
| `Null` | A calculation was expected but one or more required values were unavailable         |

---

## `wat_bas_n_round`

| Property       | Description                                                   |
| -------------- | ------------------------------------------------------------- |
| Status         | Derived                                                       |
| Data type      | Integer                                                       |
| Unit           | Percentage                                                    |
| Definition     | National basic-access estimate rounded to zero decimal places |
| Formula        | `ROUND(wat_bas_n, 0)`                                         |
| Analytical use | Supports approximate full-access classification               |

Values such as `99.6%` are rounded to `100%`.

---

## `wat_bas_r_round`

| Property       | Description                                                |
| -------------- | ---------------------------------------------------------- |
| Status         | Derived                                                    |
| Data type      | Integer                                                    |
| Unit           | Percentage                                                 |
| Definition     | Rural basic-access estimate rounded to zero decimal places |
| Formula        | `ROUND(wat_bas_r, 0)`                                      |
| Analytical use | Supports rural full-access classification                  |

---

## `wat_bas_u_round`

| Property       | Description                                                |
| -------------- | ---------------------------------------------------------- |
| Status         | Derived                                                    |
| Data type      | Integer                                                    |
| Unit           | Percentage                                                 |
| Definition     | Urban basic-access estimate rounded to zero decimal places |
| Formula        | `ROUND(wat_bas_u, 0)`                                      |
| Analytical use | Supports urban full-access classification                  |

---

## `ARC_n_full`

| Property       | Description                                                                                  |
| -------------- | -------------------------------------------------------------------------------------------- |
| Status         | Derived classification                                                                       |
| Data type      | Text                                                                                         |
| Possible value | `full access` or blank                                                                       |
| Definition     | Identifies countries with approximately full national basic access in both observation years |
| Analytical use | Separates countries already at full access from countries with zero ARC below full access    |

### Transformation logic

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

| Property       | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| Status         | Derived classification                                                                    |
| Data type      | Text                                                                                      |
| Possible value | `full access` or blank                                                                    |
| Definition     | Identifies countries with approximately full rural basic access in both observation years |
| Analytical use | Separates full rural access from rural stagnation                                         |

---

## `ARC_u_full`

| Property       | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| Status         | Derived classification                                                                    |
| Data type      | Text                                                                                      |
| Possible value | `full access` or blank                                                                    |
| Definition     | Identifies countries with approximately full urban basic access in both observation years |
| Analytical use | Separates full urban access from urban stagnation                                         |

---

## `ARC_diff`

| Property       | Description                                               |
| -------------- | --------------------------------------------------------- |
| Status         | Derived                                                   |
| Data type      | Numeric                                                   |
| Unit           | Percentage points per year                                |
| Definition     | Difference between rural and urban Annual Rates of Change |
| Analytical use | Determines whether rural or urban access improved faster  |

### Formula

```text
ARC_diff = ARC_r - ARC_u
```

### Interpretation

| Result         | Meaning                                        |
| -------------- | ---------------------------------------------- |
| `ARC_diff > 0` | Rural access improved faster than urban access |
| `ARC_diff < 0` | Urban access improved faster than rural access |
| `ARC_diff ≈ 0` | Rural and urban progress were similar          |
| `Null`         | Rural or urban ARC was unavailable             |

Generic error-handling structure:

```text
=IFERROR(ARC_r-ARC_u, "Null")
```

---

## `region`

| Property       | Description                                                                       |
| -------------- | --------------------------------------------------------------------------------- |
| Status         | Derived through lookup                                                            |
| Data type      | Text                                                                              |
| Definition     | Regional classification assigned to each country or area                          |
| Source         | Separate `Regions` reference sheet                                                |
| Analytical use | Supports regional grouping, summaries, visualizations, and country-level extracts |

Possible lookup methods include:

* `VLOOKUP`;
* `XLOOKUP`;
* `INDEX` and `MATCH`.

### Regions used in the analysis

* East Asia & Pacific
* Europe & Central Asia
* Latin America & Caribbean
* Middle East & North Africa
* North America
* South Asia
* Sub-Saharan Africa

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
| Analytical use | Improves readability in regional tables and population visualizations |

Example:

```text
pop_n = 1,463,140.5 thousand
pop_n (Millions) = 1,463.1405 million
```

This field is used in supporting regional tables and may not be part of the core 28-feature transformed dataset.

---

# Summary Classification Logic

The Summary sheet classifies national, rural, and urban ARC observations into five categories.

| Category     | Definition                                       |
| ------------ | ------------------------------------------------ |
| No ARC value | ARC is unavailable or marked `Null`              |
| Full access  | Basic access rounds to 100% in both observations |
| ARC = 0      | No measured change, excluding full-access cases  |
| ARC < 0      | Declining access, excluding full-access cases    |
| ARC > 0      | Improving access, excluding full-access cases    |

The categories should collectively account for all valid country pairs.

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

# Regional Aggregation Fields

The Summary sheet uses the transformed variables to calculate regional indicators.

| Regional indicator       | Source fields        | Aggregation |
| ------------------------ | -------------------- | ----------- |
| Number of countries      | `name`, `region`     | Count       |
| Regional population size | `pop_n`, `region`    | Sum         |
| Average national ARC     | `ARC_n`, `region`    | Average     |
| Average rural ARC        | `ARC_r`, `region`    | Average     |
| Average urban ARC        | `ARC_u`, `region`    | Average     |
| Average ARC difference   | `ARC_diff`, `region` | Average     |

Unless otherwise specified, ARC regional values are **simple country-level averages** and are not population-weighted.

---

# Missing-Value Conventions

| Representation | Meaning                                                                         |
| -------------- | ------------------------------------------------------------------------------- |
| Blank cell     | No row-level calculation is expected                                            |
| `Null`         | A required source value was unavailable or a calculation could not be completed |
| `0`            | A valid measured value of zero, not a missing value                             |

Missing ARC values must not be replaced with zero because doing so would incorrectly classify unavailable observations as no change.

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
| ARC variables          | Percentage points per year |
| `ARC_diff`             | Percentage points per year |

---

# Analytical Relationships

The main relationships used in Part 2 are:

```text
y_diff = later year - earlier year
```

```text
ARC_n = change in national basic access / y_diff
```

```text
ARC_r = change in rural basic access / y_diff
```

```text
ARC_u = change in urban basic access / y_diff
```

```text
ARC_diff = ARC_r - ARC_u
```

```text
pop_n (Millions) = pop_n / 1000
```

---

# Data Quality Considerations

## Country-Name Consistency

Country names must match exactly between observations and between the transformed dataset and the regional lookup table.

Formatting differences can cause:

* failed same-country comparisons;
* missing region assignments;
* incorrect ARC calculations.

## Row Ordering

The calculations depend on the dataset being sorted by country and year.

Changing the row order without revalidating formulas can create incorrect country comparisons.

## Unequal Observation Intervals

Countries do not necessarily use identical start and end years.

The `y_diff` field ensures that raw changes are converted into comparable annual rates.

## Duplicate Observations

A same-country year difference of zero can indicate a duplicate country-year record.

## Estimated Values Near 100%

Water-access estimates may be marginally below or above 100% because of estimation precision.

Rounded fields are used for approximate full-access classification.

## Regional Averages

Simple averages give each country equal weight regardless of population size.

Regional average ARC should therefore not automatically be interpreted as the average experience of all people living in the region.

---

# Related Documentation

## Data Overview

[README.md](./README.md)

Explains the dataset scope, transformation workflow, analytical sheets, and data-quality considerations.

## Visual Assets

[../assets/](../assets/)

Contains the main analytical charts and regional country-level ARC tables.

## Reports

[../reports/](../reports/)

Contains the analytical report and spreadsheet exports for Part 2.

## Working Spreadsheet

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

---

# Notes

* The dataset is descriptive and observational.
* ARC measures the speed and direction of change, not the final access level.
* A high ARC can coexist with low final access.
* A low ARC can reflect high baseline access and limited remaining room for improvement.
* Full-access flags should be reviewed before interpreting zero ARC values.
* Missing values are retained transparently and are not treated as zero.
* Regional summaries should be interpreted alongside country-level tables and population scale.
