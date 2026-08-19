# Data Dictionary — Access to Drinking Water

This data dictionary documents the source variables, classification fields, derived features, validation fields and cleaned visualization fields I used in Part 1 of the **Access to Drinking Water** project.

I completed the analysis in Google Sheets using country and area-level drinking-water estimates for 2020.

---

## Naming Convention

The water-access variables follow this structure:

`wat_[service]_[area]`

### Service abbreviations

| Abbreviation | Meaning |
|---|---|
| `bas` | At least basic |
| `lim` | Limited |
| `unimp` | Unimproved |
| `sur` | Surface water |

### Area suffixes

| Suffix | Meaning |
|---|---|
| `_n` | National |
| `_r` | Rural |
| `_u` | Urban |
| `_clean` | Cleaned numeric feature used for analysis or visualization |

For example:

`wat_unimp_r_clean`

represents the cleaned rural percentage of people using unimproved drinking-water sources.

---

# 1. Source Variables

## Identification, Population and Classification

| Variable | Description | Type | Unit |
|---|---|---|---|
| `name` | Country or area name | Text | Not applicable |
| `year` | Reference year of the estimate | Integer | Year |
| `income_group` | Country or area income classification | Text | Category |
| `pop_n` | National population estimate | Numeric | Thousands of people |
| `pop_u` | Urban population share | Numeric | Percentage |

I used `income_group` for socioeconomic segmentation and pivot-table analysis. It is a categorical variable rather than a direct numerical measurement of national income.

---

## National Access Variables

| Variable | Description | Type | Unit |
|---|---|---|---|
| `wat_bas_n` | National share with at least basic drinking-water access | Numeric | Percentage |
| `wat_lim_n` | National share with limited drinking-water access | Numeric | Percentage |
| `wat_unimp_n` | National share using unimproved drinking-water sources | Numeric | Percentage |
| `wat_sur_n` | National share using surface water | Numeric | Percentage |

These variables describe drinking-water access for the total national population.

---

## Rural Access Variables

| Variable | Description | Type | Unit |
|---|---|---|---|
| `wat_bas_r` | Rural share with at least basic drinking-water access | Numeric | Percentage |
| `wat_lim_r` | Rural share with limited drinking-water access | Numeric | Percentage |
| `wat_unimp_r` | Rural share using unimproved drinking-water sources | Numeric | Percentage |
| `wat_sur_r` | Rural share using surface water | Numeric | Percentage |

These variables describe drinking-water access for rural populations.

---

## Urban Access Variables

| Variable | Description | Type | Unit |
|---|---|---|---|
| `wat_bas_u` | Urban share with at least basic drinking-water access | Numeric | Percentage |
| `wat_lim_u` | Urban share with limited drinking-water access | Numeric | Percentage |
| `wat_unimp_u` | Urban share using unimproved drinking-water sources | Numeric | Percentage |
| `wat_sur_u` | Urban share using surface water | Numeric | Percentage |

These variables describe drinking-water access for urban populations.

---

# 2. Drinking-Water Service Definitions

The dataset uses four mutually exclusive service categories that together describe the drinking-water access distribution.

## At Least Basic

At least basic access combines:

- safely managed service;
- basic service.

It represents drinking water obtained from an improved source where collection requires no more than 30 minutes for a round trip.

Related variables:

- `wat_bas_n`
- `wat_bas_r`
- `wat_bas_u`

## Limited

Limited service represents drinking water obtained from an improved source where collection requires more than 30 minutes for a round trip, including queuing time.

Related variables:

- `wat_lim_n`
- `wat_lim_r`
- `wat_lim_u`

## Unimproved

Unimproved service represents drinking water obtained from an unprotected dug well or unprotected spring.

Related variables:

- `wat_unimp_n`
- `wat_unimp_r`
- `wat_unimp_u`

## Surface Water

Surface-water service represents drinking water collected directly from sources such as:

- rivers;
- dams;
- lakes;
- ponds;
- streams;
- canals;
- irrigation canals.

Related variables:

- `wat_sur_n`
- `wat_sur_r`
- `wat_sur_u`

Official definition:

[JMP Drinking-Water Service Ladder](https://washdata.org/topics/drinking-water)

---

# 3. Validation Feature

## `value_cnt`

| Attribute | Documentation |
|---|---|
| Category | Validation feature |
| Function | `COUNTA()` |
| Representative formula | `=COUNTA(A2:P2)` |
| Expected source-row result | `16` |
| Purpose | Detect incorrectly imported or incomplete source rows |

I used `COUNTA()` rather than `COUNT()` because the source rows contain both text and numeric values.

I filtered `value_cnt` to exclude the expected result of 16. This isolated five rows affected by inconsistent separators during import.

I corrected the affected rows by repositioning the displaced values and using:

`Data > Split text to columns`

After correcting them, I verified that the source rows returned the expected completeness count.

---

# 4. Derived Population Features

## `pop_u_val`

| Attribute | Documentation |
|---|---|
| Category | Derived calculation |
| Logic | `pop_n × pop_u ÷ 100` |
| Google Sheets pattern | `=pop_n_cell*pop_u_cell/100` |
| Unit | Thousands of people |
| Purpose | Estimate the urban population represented by each observation |

Because `pop_n` is measured in thousands, the calculated `pop_u_val` also remains in thousands.

---

## `pop_r`

| Attribute | Documentation |
|---|---|
| Category | Derived percentage |
| Logic | `100 - pop_u` |
| Google Sheets pattern | `=100-pop_u_cell` |
| Unit | Percentage |
| Purpose | Calculate rural population share |

This calculation assumes that the total population is divided into two complementary area types:

`pop_u + pop_r = 100%`

---

## `pop_n (m)`

| Attribute | Documentation |
|---|---|
| Category | Derived grouping feature |
| Function | `ROUNDUP()` |
| Google Sheets pattern | `=ROUNDUP(pop_n_cell/1000,0)` |
| Unit | Millions of people |
| Purpose | Improve population-chart readability and aggregation |

I divided `pop_n` by 1,000 because the source population is measured in thousands.

I used `ROUNDUP()` rather than `ROUND()` because the project required the population estimate to be rounded upward to the nearest million.

I retained `pop_n` as the original measurement and used `pop_n (m)` only for grouping and visualization.

---

## `pop_u (rounded)`

| Attribute | Documentation |
|---|---|
| Category | Derived grouping feature |
| Function | `ROUND()` |
| Google Sheets pattern | `=IFERROR(ROUND(pop_u_cell,0),"NAN")` |
| Unit | Whole percentage point |
| Purpose | Group countries with similar urban-population shares |

I used the rounded feature for chart aggregation while retaining the original `pop_u` value for calculations.

---

## `pop_r (rounded)`

| Attribute | Documentation |
|---|---|
| Category | Derived grouping feature |
| Function | `ROUND()` |
| Google Sheets pattern | `=IFERROR(ROUND(pop_r_cell,0),"NAN")` |
| Unit | Whole percentage point |
| Purpose | Group countries with similar rural-population shares |

I used the rounded feature for chart aggregation while retaining the original `pop_r` value for calculations.

---

# 5. Income-Group Sorting Feature

## `income_group_num`

I created `income_group_num` to arrange the income classifications logically rather than alphabetically.

| `income_group_num` | `income_group` |
|---:|---|
| 0 | NAN |
| 1 | Low income |
| 2 | Lower middle income |
| 3 | Upper middle income |
| 4 | High income |

I used this variable only for sorting. The numerical values do not imply that the distance between income groups is equal.

I treated `NAN` as an unclassified category rather than as an income level. I therefore excluded it from interpretations of the ordered income progression.

---

# 6. Cleaned Access Features

I created cleaned numeric service fields for the national, urban and rural visualizations.

## National Cleaned Variables

- `wat_bas_n_clean`
- `wat_lim_n_clean`
- `wat_unimp_n_clean`
- `wat_sur_n_clean`

## Urban Cleaned Variables

- `wat_bas_u_clean`
- `wat_lim_u_clean`
- `wat_unimp_u_clean`
- `wat_sur_u_clean`

## Rural Cleaned Variables

- `wat_bas_r_clean`
- `wat_lim_r_clean`
- `wat_unimp_r_clean`
- `wat_sur_r_clean`

## Cleaning Logic

A representative Google Sheets formula for the first service value in a four-service row is:

`=IF(COUNT($D2:$G2)=4,MIN(100,MAX(0,$D2)),)`

I copied this logic across the four service columns while changing the final service-cell reference.

The formula performs three controls:

1. `COUNT($D2:$G2)=4` confirms that all four service values are numeric.
2. `MAX(0,$D2)` prevents a percentage below 0%.
3. `MIN(100,...)` prevents a percentage above 100%.

If the four-service row is incomplete, the formula returns a blank cell rather than replacing the missing value with zero.

This distinction is important:

- blank means unavailable or excluded;
- zero means a valid measured percentage of 0%.

---

# 7. Important Unit Notes

## National Population

`pop_n` is measured in thousands.

For example, if:

`pop_n = 53,771`

then the estimated national population is approximately:

`53,771,000 people`

or:

`53.771 million people`

---

## Population Shares

The following variables are percentages:

- `pop_u`
- `pop_r`
- all `wat_*` variables.

A percentage must be divided by 100 when it is used to estimate a population count.

For example:

`pop_u_val = pop_n × pop_u ÷ 100`

---

## Drinking-Water Access Variables

The access fields represent percentage distributions rather than population totals.

An average percentage calculated across countries should not be interpreted as a population-weighted global percentage unless population weighting is applied separately.

---

# 8. Analytical Use of Variables

| Analysis | Main variables |
|---|---|
| Population completeness validation | `value_cnt` |
| Urban population estimation | `pop_n`, `pop_u`, `pop_u_val` |
| Urban-rural population structure | `pop_n (m)`, `pop_u`, `pop_r` |
| National access visualization | `pop_n (m)` and national cleaned service fields |
| Urban access visualization | `pop_u (rounded)` and urban cleaned service fields |
| Rural access visualization | `pop_r (rounded)` and rural cleaned service fields |
| Area-level descriptive statistics | The 12 national, rural and urban source access variables |
| Income-group pivot analysis | `income_group_num`, `income_group`, `pop_n`, `pop_u` and national access variables |

---

# 9. Relationship to the Report Sheets

## Global 2020 Report

I used:

- `pop_n`
- `pop_u`
- `pop_r`
- `pop_n (m)`
- the 12 national, rural and urban access variables
- cleaned national service fields

These variables support population comparisons, summary statistics, the area-level distribution analysis and the national service-level visualization.

## Urban 2020 Report

I used:

- `pop_u`
- `pop_u (rounded)`
- cleaned urban service fields

These variables support the grouped urban service-level visualization.

## Rural 2020 Report

I used:

- `pop_r`
- `pop_r (rounded)`
- cleaned rural service fields

These variables support the grouped rural service-level visualization.

## Pivot Table

I used:

- `income_group_num`
- `income_group`
- `pop_n`
- `pop_u`
- national drinking-water access variables

These variables support income-group ordering, population aggregation and average national access comparisons.

---

# 10. Missing-Value Treatment

Missing or invalid service values can appear as:

- blank cells;
- text such as `NAN`;
- non-numeric imported values.

I did not automatically replace missing values with zero because zero represents a valid access percentage.

For visualizations requiring a complete four-service distribution, I included an observation only when all four relevant service values were numeric.

As a result, the number of observations can differ between national, urban and rural analyses.

---

# 11. Analytical Limitations

- The dataset contains country and area-level estimates.
- The analysis focuses on 2020.
- Some observations contain missing service values.
- Rounded variables reduce detail and are used only for grouping.
- Grouped country averages are not automatically population weighted.
- Unequal numbers of countries may be represented in different rounded categories.
- The analysis identifies descriptive associations rather than causal effects.
- The Google Sheets workbook remains the authoritative record of formulas, transformations and chart configurations.

---

## Official References

- [WHO/UNICEF JMP Data Portal](https://washdata.org/data)
- [JMP Drinking-Water Service Ladder](https://washdata.org/topics/drinking-water)
- [JMP Estimation Methods](https://washdata.org/topics/methods/estimation-methods)
