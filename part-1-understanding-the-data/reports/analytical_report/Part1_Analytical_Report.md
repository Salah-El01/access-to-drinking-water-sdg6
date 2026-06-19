# Part 1 Analytical Report — Access to Drinking Water

## 1. Executive Summary

This report presents the first part of the **Access to Drinking Water** data analysis project. The analysis focuses on understanding global drinking water access in 2020 using spreadsheet-based data cleaning, feature engineering, statistical summaries, pivot table analysis, and visual exploration.

The project investigates how drinking water access varies across:

- national population size
- urban and rural population structures
- service-level categories
- country income groups

The analysis shows that access to at least basic drinking water is generally high at the national and urban levels. However, important inequalities remain, especially in rural areas and lower-income countries. Rural populations show greater exposure to limited, unimproved, and surface-water services, while income group appears to be one of the strongest explanatory dimensions for national water access quality.

---

## 2. Working Spreadsheet

The full analysis was performed in Google Sheets.

[Open Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

The workbook includes the main dataset, transformation columns, summary tables, pivot table analysis, and visualizations used throughout this report.

---

## 3. Analytical Objective

The objective of this analysis was to explore global drinking water access patterns and identify the main differences between population groups and socioeconomic categories.

The analysis focused on four key questions:

1. How does national population size relate to urban and rural population shares?
2. How is drinking water access distributed across national, urban, and rural populations?
3. Are urban and rural populations exposed to different levels of water access inequality?
4. How does income group relate to national drinking water access quality?

---

## 4. Dataset Overview

The dataset contains country-level estimates for drinking water access in 2020.

The main dimensions used in the analysis include:

| Variable | Description |
|---|---|
| `name` | Country or area name |
| `income_group` | Country income classification |
| `pop_n` | National population size estimate, measured in thousands |
| `pop_u` | Urban population share, measured as a percentage |
| `wat_bas_n` | National share with at least basic drinking water access |
| `wat_lim_n` | National share with limited drinking water access |
| `wat_unimp_n` | National share with unimproved drinking water access |
| `wat_sur_n` | National share relying on surface water |
| `wat_bas_r` | Rural share with at least basic drinking water access |
| `wat_lim_r` | Rural share with limited drinking water access |
| `wat_unimp_r` | Rural share with unimproved drinking water access |
| `wat_sur_r` | Rural share relying on surface water |
| `wat_bas_u` | Urban share with at least basic drinking water access |
| `wat_lim_u` | Urban share with limited drinking water access |
| `wat_unimp_u` | Urban share with unimproved drinking water access |
| `wat_sur_u` | Urban share relying on surface water |

The water access variables are grouped into four service levels:

- **At least basic**
- **Limited**
- **Unimproved**
- **Surface water**

These categories allow comparison between higher-quality and lower-quality drinking water access levels across different population groups.

---

## 5. Tools Used

The project was completed using Google Sheets as the main analytical workspace.

Main tools and techniques used:

- spreadsheet data cleaning
- row validation
- formula-based feature engineering
- missing value handling
- percentage-based calculations
- summary statistics
- pivot tables
- 100% stacked column charts
- line charts
- box-and-whisker style analysis
- visual interpretation
- analytical reporting

---

## 6. Data Preparation and Feature Engineering

Several derived features were created to support analysis, validation, aggregation, and visualization.

### 6.1 Row Validation

A row validation field was created to check whether each row contained the expected number of values.

Example logic:

```text
value_cnt = COUNTA(row_range)
