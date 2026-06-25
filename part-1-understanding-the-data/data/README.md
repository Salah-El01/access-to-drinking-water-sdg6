# Data — Part 1: Understanding the Data

This folder documents the dataset used in Part 1 of the **Access to Drinking Water** project.

The analysis was performed in Google Sheets using a country-level drinking water access dataset for 2020. The dataset includes population estimates, urban population share, income group classification, and drinking water access percentages across national, rural, and urban population groups.

The working spreadsheet contains the original dataset, cleaned fields, derived features, summary tables, pivot tables, and visualizations used throughout the analysis.

---

## Working Spreadsheet

The full Google Sheets workbook is available here:

[Open Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

The main dataset is stored in the sheet:

`Estimates-on-the-use-of-water-(2020)`

---

## Dataset Scope

The dataset focuses on drinking water access estimates for 2020.

The analysis uses country-level observations and compares access across:

- national population
- urban population
- rural population
- income groups
- drinking water service levels

The main service levels analyzed are:

- **At least basic**
- **Limited**
- **Unimproved**
- **Surface water**

These service levels make it possible to compare higher-quality and lower-quality drinking water access across different population groups.

---

## Main Data Dimensions

The dataset includes the following analytical dimensions:

| Dimension | Description |
|---|---|
| Country / area | Country or area name |
| Income group | Socioeconomic classification of each country or area |
| National population | Population size estimate, measured in thousands |
| Urban population share | Percentage of the population living in urban areas |
| National water access | Drinking water access distribution at the national level |
| Rural water access | Drinking water access distribution for rural populations |
| Urban water access | Drinking water access distribution for urban populations |

---

## Data Preparation Summary

Several preparation steps were completed before analysis:

- checked the imported dataset structure
- validated row completeness using a count field
- handled missing values and non-numeric entries
- created derived population features
- created rural population share from urban population share
- created rounded variables for aggregation and visualization
- created cleaned water-access fields for more stable visual outputs
- summarized access variables using descriptive statistics
- built pivot tables for income-group analysis

---

## Key Derived Features

Several new features were created during the analysis.

| Feature | Purpose |
|---|---|
| `value_cnt` | Counts non-empty values in each row to support row validation |
| `pop_u_val` | Estimates the urban population count from national population and urban share |
| `pop_r` | Calculates rural population share as the complement of urban share |
| `pop_n (m)` | Converts national population into a rounded million-based feature for visualization |
| `pop_u (rounded)` | Rounds urban population share for grouped visual analysis |
| `pop_r (rounded)` | Rounds rural population share for grouped visual analysis |
| cleaned water-access fields | Improve chart reliability by reducing issues caused by missing or inconsistent values |

---

## Data Quality Considerations

The dataset required several checks before analysis.

Main data quality considerations included:

- missing values represented as text
- possible formatting issues during import
- percentage values requiring validation
- water access categories needing clean numeric values for charting
- population values requiring unit awareness because `pop_n` is measured in thousands

These checks helped ensure that the analysis was based on consistent and interpretable fields.

---

## Relationship to the Project

The data documented here supports the full Part 1 analysis, including:

- global population and access analysis
- urban drinking water access analysis
- rural drinking water access analysis
- income-group segmentation
- visual analysis
- analytical reporting

For detailed variable definitions, see:

[data_dictionary.md](./data_dictionary.md)
