# Reports — Part 2: Transforming the Data

This folder contains the reporting layer of **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

Part 2 transforms a multi-year drinking-water dataset into a progress-monitoring framework using **Annual Rate of Change (ARC)**. The reports folder separates the professional analytical interpretation from the spreadsheet exports used as supporting evidence.

---

## Folder Structure

```text
reports/
├── analytical_report/
│   └── Part2_Analytical_Report.md
│
├── sheet_exports/
│   ├── Estimates of the use of water (2000-2020).pdf
│   ├── Summary.pdf
│   └── README.md
│
└── README.md
```

---

## Analytical Report

The main written report is available here:

[Part2_Analytical_Report.md](./analytical_report/Part2_Analytical_Report.md)

This report provides the full analytical interpretation of Part 2.

It explains:

- the objective of the transformation phase;
- the structure of the 2000–2020 drinking-water dataset;
- the year-representation analysis;
- the feature engineering process;
- the Annual Rate of Change methodology;
- the national, rural, and urban ARC comparison;
- the full-access classification logic;
- the rural–urban progress difference;
- the regional aggregation methodology;
- the main findings;
- the analytical limitations;
- future improvement opportunities.

The analytical report is the main document to read for a complete understanding of the Part 2 analysis.

---

## Sheet Exports

The spreadsheet exports are available here:

[sheet_exports/](./sheet_exports/)

These files are PDF exports of the main Google Sheets tabs used in the analysis.

They preserve the final spreadsheet outputs, including:

- transformed data;
- calculated fields;
- validation checks;
- summary tables;
- regional aggregations;
- visual outputs.

The sheet exports are included for transparency, documentation, and portfolio review.

---

## Files Included in Sheet Exports

### Estimates of the use of water (2000-2020).pdf

[Open the transformed dataset export](<./sheet_exports/Estimates of the use of water (2000-2020).pdf>)

This export contains the transformed dataset used in Part 2.

It documents the row-level calculation layer, including:

- country or area name;
- regional classification;
- observation year;
- national population estimate;
- national, rural, and urban water-access variables;
- year-difference calculation;
- national Annual Rate of Change (`ARC_n`);
- rural Annual Rate of Change (`ARC_r`);
- urban Annual Rate of Change (`ARC_u`);
- rounded basic-access indicators;
- full-access classification fields;
- rural–urban ARC difference (`ARC_diff`).

This file shows how the original dataset was transformed into an analysis-ready structure.

---

### Summary.pdf

[Open the summary export](./sheet_exports/Summary.pdf)

This export contains the main analytical summary and dashboard outputs.

It documents:

- year representation;
- year-difference statistics;
- ARC summary statistics;
- access-by-area progress classification;
- missing, full-access, zero, positive, and negative ARC counts;
- rural–urban ARC comparison;
- regional aggregation;
- year histogram;
- regional ARC charts;
- population and ARC comparison visual.

This file shows how the transformed data was summarized and interpreted.

---

## Reporting Logic

The reporting layer separates interpretation from evidence.

```text
Analytical report = professional interpretation
Sheet exports      = spreadsheet evidence
Visual assets      = chart and table outputs
Data folder        = dataset and variable documentation
```

This structure makes the project easier to review because each folder has a clear role.

---

## How to Review This Section

For the best review experience:

1. Start with the analytical report:  
   [Part2_Analytical_Report.md](./analytical_report/Part2_Analytical_Report.md)

2. Review the spreadsheet exports:  
   [sheet_exports/](./sheet_exports/)

3. Review the visual assets:  
   [../assets/](../assets/)

4. Review the data documentation:  
   [../data/](../data/)

---

## Relationship to the Project Workflow

The reports folder documents the final outputs of the Part 2 workflow:

```text
Source data
    ↓
Data transformation
    ↓
Feature engineering
    ↓
ARC calculation
    ↓
Regional enrichment
    ↓
Summary tables
    ↓
Visual analysis
    ↓
Analytical reporting
```

The sheet exports preserve the spreadsheet outputs, while the analytical report explains the methodology and findings in a structured narrative.

---

## Main Analytical Themes Covered

The reporting layer covers five major analytical themes:

### 1. Year Representation

The analysis checks how observation years are distributed and confirms that the dataset is mainly concentrated around 2015 and 2020.

### 2. Annual Rate of Change

The project calculates `ARC_n`, `ARC_r`, and `ARC_u` to measure annual progress in national, rural, and urban access to at least basic drinking water.

### 3. Full-Access Classification

The analysis separates countries already at full access from countries with zero progress below full coverage.

This prevents misleading interpretation of zero ARC values.

### 4. Rural–Urban Progress Difference

The project uses `ARC_diff` to compare rural and urban progress directly.

```text
ARC_diff = ARC_r - ARC_u
```

A positive value means rural access improved faster than urban access.

### 5. Regional Progress Analysis

The analysis groups countries by region to compare progress across geographic areas and connect ARC values with population scale.

---

## Main Findings Documented

The reports section supports the following conclusions:

1. The dataset is not a complete annual panel; it is mainly structured around selected observation years.
2. ARC provides a fairer comparison because it normalizes access change by the number of years between observations.
3. Rural access improved faster than urban access on average.
4. Urban ARC is often lower because many urban areas already had high or full access.
5. Full-access flags improve the interpretation of zero ARC values.
6. Regional averages hide strong country-level variation.
7. Population size alone does not explain progress patterns.
8. ARC should be interpreted alongside baseline access, full-access status, and population scale.

---

## Related Folders

### Data Documentation

[Open the data folder](../data/)

Contains the data README and data dictionary documenting the dataset structure, variables, derived features, units, and data-quality considerations.

### Visual Assets

[Open the assets folder](../assets/)

Contains the main visual outputs and regional ARC tables used to support the Part 2 analysis.

---

## Notes

- The analytical report provides the professional narrative of the project.
- The sheet exports document the final state of the Google Sheets analysis tabs.
- The Google Sheets workbook remains the source of truth for formulas, transformations, and chart preparation.
- The exported PDFs are included for portfolio transparency and workflow documentation.
- The analysis is descriptive and exploratory.
- The analysis identifies patterns and associations but does not establish causality.
- ARC measures the speed of progress, not the final level of access.
- Regional averages should be interpreted alongside country-level records and population scale.
