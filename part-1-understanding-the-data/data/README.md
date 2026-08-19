# Data — Part 1: Understanding the Data

This folder documents the data used in Part 1 of the **Access to Drinking Water** project.

I completed the data preparation, feature engineering, calculations, aggregations and visualizations in Google Sheets. I use this folder to document the dataset, transformations and data-quality decisions rather than to store a separate static copy of the working data.

---

## Data Source

The project uses country and area-level drinking-water estimates associated with the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

The JMP is responsible for producing comparable national, regional and global estimates for drinking water, sanitation and hygiene.

Official references:

- [WHO/UNICEF JMP Data Portal](https://washdata.org/data)
- [JMP Drinking-Water Service Ladder](https://washdata.org/topics/drinking-water)
- [Progress on Household Drinking Water, Sanitation and Hygiene, 2000–2020](https://washdata.org/reports/jmp-2021-wash-households)

The analysis in Part 1 focuses on estimates for **2020**.

---

## Working Spreadsheet

The complete Google Sheets workbook is available here:

[Open the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

The principal source dataset is stored in:

`Estimates-on-the-use-of-water-(2020)`

The workbook also contains the following analytical sheets:

- `Global 2020 Report`
- `Urban 2020 Report`
- `Rural 2020 Report`
- `Pivot Table`

---

## Dataset Scope

I used country and area-level observations to compare:

- national population size;
- urban and rural population shares;
- national drinking-water access;
- rural drinking-water access;
- urban drinking-water access;
- income classifications;
- four drinking-water service levels.

The analysis is descriptive and focuses on differences between countries and groups rather than individual households.

---

## Drinking-Water Service Levels

The project dataset combines safely managed and basic access into the category **at least basic**.

| Service level | Definition used in the analysis |
|---|---|
| At least basic | Drinking water from an improved source where collection requires no more than 30 minutes for a round trip, including safely managed and basic services |
| Limited | Drinking water from an improved source where collection exceeds 30 minutes for a round trip |
| Unimproved | Drinking water from an unprotected dug well or unprotected spring |
| Surface water | Drinking water collected directly from a river, dam, lake, pond, stream, canal or irrigation canal |

These categories describe service levels rather than directly measuring the absolute number of people affected.

---

## Main Data Dimensions

| Dimension | Description |
|---|---|
| Country or area | Geographic unit represented by each observation |
| Reference year | Year associated with the estimate |
| Income group | Socioeconomic classification used for grouped analysis |
| National population | Population estimate measured in thousands |
| Urban population share | Percentage of the population living in urban areas |
| Rural population share | Derived percentage of the population living in rural areas |
| National water access | Service distribution for the total national population |
| Rural water access | Service distribution for rural populations |
| Urban water access | Service distribution for urban populations |

---

## Data Preparation Workflow

### 1. Import validation

I checked whether the original delimited dataset was imported into the expected columns.

Some records contained inconsistent separators, causing values to appear in the wrong cells.

### 2. Row-completeness validation

I created `value_cnt` with `COUNTA()` because the source rows contain both text and numeric values.

Representative Google Sheets formula for the original 16-field import range:

`=COUNTA(A2:P2)`

I expected a result of `16` for a correctly imported source row.

I filtered `value_cnt` to identify values different from 16. This exposed five malformed rows that required correction.

### 3. Import correction

I corrected the affected rows by repositioning the values after the inconsistent separator and using:

`Data > Split text to columns`

After the correction, I confirmed that the original imported rows returned the expected completeness count.

### 4. Population feature engineering

I created new population features to support calculation and visualization:

- urban population estimate;
- rural population share;
- rounded-up national population in millions;
- rounded urban-population share;
- rounded rural-population share.

### 5. Access-variable cleaning

I created cleaned numeric versions of the service-level fields for charting.

The cleaning logic:

- requires all four service-level values to be numeric;
- excludes incomplete four-service distributions;
- restricts valid percentages to the 0–100 range;
- prevents text values from producing charting errors.

### 6. Aggregation and analysis

I used the prepared features to create:

- population comparisons;
- descriptive-statistics tables;
- a candlestick chart representing the five-number-summary components;
- national, urban and rural 100% stacked charts;
- income-group pivot-table analysis.

---

## Key Derived and Validation Features

| Feature | Category | Purpose |
|---|---|---|
| `value_cnt` | Validation | Counts populated cells in the imported source row |
| `pop_u_val` | Derived population feature | Estimates the number of urban residents |
| `pop_r` | Derived population feature | Calculates rural population share |
| `pop_n (m)` | Derived population feature | Groups national population by rounded-up millions |
| `pop_u (rounded)` | Grouping feature | Groups observations by rounded urban share |
| `pop_r (rounded)` | Grouping feature | Groups observations by rounded rural share |
| `income_group_num` | Sorting feature | Orders income classifications logically |
| `wat_*_clean` | Cleaned access feature | Provides validated numeric service values for visualization |

---

## Principal Google Sheets Logic

| Feature | Formula or logic |
|---|---|
| Row validation | `=COUNTA(A2:P2)` |
| Urban population estimate | `=pop_n_cell*pop_u_cell/100` |
| Rural population share | `=100-pop_u_cell` |
| Population in rounded-up millions | `=ROUNDUP(pop_n_cell/1000,0)` |
| Rounded urban share | `=IFERROR(ROUND(pop_u_cell,0),"NAN")` |
| Rounded rural share | `=IFERROR(ROUND(pop_r_cell,0),"NAN")` |
| Clean service value | `=IF(COUNT(service_row_range)=4,MIN(100,MAX(0,service_cell)),)` |

The complete formulas with their actual cell references remain available in the Google Sheets workbook.

---

## Income-Group Ordering

I created `income_group_num` to prevent alphabetical sorting from placing the income categories in an analytically incorrect order.

| `income_group_num` | `income_group` |
|---:|---|
| 0 | NAN |
| 1 | Low income |
| 2 | Lower middle income |
| 3 | Upper middle income |
| 4 | High income |

I treated `NAN` as an unclassified category rather than as an income level.

---

## Data-Quality Considerations

The principal data-quality issues were:

- inconsistent separators during import;
- five malformed source rows;
- missing values represented by text such as `NAN`;
- non-numeric service-level entries;
- incomplete four-service distributions;
- population values recorded in thousands;
- percentages requiring validation within the 0–100 range;
- unequal numbers of valid observations across analyses.

I retained missing values as missing rather than replacing them with zero because zero represents a valid access percentage and would change the analytical meaning.

---

## Relationship to the Four Report Sheets

| Report sheet | Main features used |
|---|---|
| Global 2020 Report | `pop_n`, `pop_u`, `pop_r`, `pop_n (m)` and the 12 national, rural and urban access variables |
| Urban 2020 Report | `pop_u`, `pop_u (rounded)` and cleaned urban service fields |
| Rural 2020 Report | `pop_r`, `pop_r (rounded)` and cleaned rural service fields |
| Pivot Table | `income_group_num`, `income_group`, `pop_n`, `pop_u` and national service fields |

---

## Reproducibility Notes

- I retained Google Sheets as the main analytical source of truth.
- I documented the dataset structure and formulas in this folder.
- I retained missing observations rather than applying unsupported imputation.
- I used cleaned service-level fields for visualization while preserving the source variables.
- I documented rounded variables separately because they support grouping but do not replace the original measurements.
- I interpreted grouped values as country-level averages unless otherwise specified.

For complete variable definitions, see:

[Data Dictionary](./Data_dictionary.md)
