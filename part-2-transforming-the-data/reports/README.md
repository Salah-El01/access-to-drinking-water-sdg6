# Reports - Part 2: Transforming the Data

This folder contains the reporting and documentary evidence for **Part 2: Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

Part 2 transforms paired country-level drinking-water observations into a progress-monitoring framework based on the **Annual Rate of Change (ARC)**.

The reports section separates:

* the written analytical interpretation;
* the fixed PDF exports of the spreadsheet calculations and visuals.

---

## Folder Structure

```text
reports/
|
|-- analytical_report/
|   `-- Part2_Analytical_Report.md
|
|-- sheet_exports/
|   |-- Estimates of the use of water (2000-2020).pdf
|   |-- Summary.pdf
|   `-- README.md
|
`-- README.md
```

---

## Quick Access

| Resource                                                                                                 | Purpose                                                                                  |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [Part 2 Analytical Report](./analytical_report/Part2_Analytical_Report.md)                               | Complete methodology, verified results, interpretation, limitations, and conclusions     |
| [Sheet Exports Documentation](./sheet_exports/README.md)                                                 | Explanation of the exported worksheets and their reproducibility limitations             |
| [Transformed Dataset PDF](./sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf) | Fixed export of the transformation and calculation layer                                 |
| [Summary PDF](./sheet_exports/Summary.pdf)                                                               | Fixed export of the Summary calculations, regional aggregation, and four existing charts |
| [Part 2 Data Documentation](../data/README.md)                                                           | Dataset scope, transformation approach, and data-quality notes                           |
| [Part 2 Data Dictionary](../data/data_dictionary.md)                                                     | Definitions, units, formula logic, and interpretation of variables                       |
| [Part 2 Visual Assets](../assets/README.md)                                                              | Index of chart images and regional ARC table screenshots                                 |

---

## 1. Analytical Report

The principal written report is:

[Part2_Analytical_Report.md](./analytical_report/Part2_Analytical_Report.md)

This report provides the complete analytical narrative for Part 2.

It documents:

* the project objective;
* the data source and analytical workspace;
* the verified dataset scope;
* the paired-observation structure;
* the distribution of observation years;
* the `y_diff` calculation;
* the national, rural, and urban ARC methodology;
* missing-value handling;
* approximate full-access classification;
* access-by-area progress classifications;
* the paired rural-urban ARC difference;
* regional aggregations;
* the four existing visualisations;
* verified descriptive statistics;
* analytical limitations;
* reproducibility constraints;
* recommended improvements;
* final conclusions.

The analytical report is the primary document for understanding what was calculated, what the results mean, and what the analysis cannot establish.

---

## 2. Sheet Exports

The spreadsheet exports are stored in:

[sheet_exports/](./sheet_exports/)

This folder contains two PDF files exported from the Google Sheets workbook.

| Export                                          | Pages | Role                                                            |
| ----------------------------------------------- | ----: | --------------------------------------------------------------- |
| `Estimates of the use of water (2000-2020).pdf` |     4 | Country-level transformation and calculation layer              |
| `Summary.pdf`                                   |     4 | Reporting, classification, aggregation, and visualisation layer |

These PDF files are supporting evidence. They display the spreadsheet outputs but do not expose the underlying formulas, lookup ranges, chart source ranges, or dynamic recalculation logic.

Detailed documentation is available in:

[Sheet Exports README](./sheet_exports/README.md)

---

## 3. Transformed Dataset Export

[Open the transformed dataset PDF](./sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf)

The worksheet is titled:

```text
Estimates of the use of water (2000-2020)
```

The title refers to the broader source-data period. However, the observations retained in the completed Part 2 analysis cover **2015 to 2020**.

The transformed analytical dataset contains:

| Measure                          | Result |
| -------------------------------- | -----: |
| Countries or areas               |    231 |
| Observations                     |    462 |
| Observations per country or area |      2 |
| Earliest analytical year         |   2015 |
| Latest analytical year           |   2020 |

The export documents:

* country or area names;
* observation years;
* regional classifications;
* population estimates;
* national, rural, and urban drinking-water variables;
* `y_diff`;
* `ARC_n`;
* `ARC_r`;
* `ARC_u`;
* rounded basic-access variables;
* approximate full-access flags;
* `ARC_diff`.

The four landscape pages are consecutive printable sections of the same large worksheet.

---

## 4. Summary Export

[Open the Summary PDF](./sheet_exports/Summary.pdf)

The Summary worksheet is the reporting and interpretation layer of the spreadsheet analysis.

It contains:

* a linked country-level analytical table;
* population values converted to millions;
* observation-year frequencies;
* year-difference statistics;
* ARC summary statistics;
* missing-value counts;
* approximate full-access counts;
* zero, negative, and positive ARC classifications;
* country-level `ARC_diff` values;
* regional country counts;
* regional population totals;
* average national, rural, and urban ARC by region;
* average paired `ARC_diff` by region;
* four completed charts.

### Existing charts

The current Summary export contains:

1. **Histogram of Year**
2. **Average Rural-Urban ARC Difference by Region**
3. **Average ARC Values for Rural Versus Urban Areas per Region**
4. **Regional Progress in Basic Water Access: ARC and Population**

The year chart is more accurately interpreted as a categorical frequency column chart because it displays separate year categories.

### Current incomplete elements

The Summary sheet does not yet display:

* median national ARC;
* median rural ARC;
* median urban ARC;
* the required country-level `ARC_diff` histogram.

The medians have been independently verified and are documented in the analytical report.

The existing regional average `ARC_diff` chart is an additional regional comparison. It does not replace the missing country-level histogram.

---

## 5. Reporting Architecture

Each project component has a distinct function.

| Component              | Function                                                       |
| ---------------------- | -------------------------------------------------------------- |
| Analytical report      | Explains methodology, results, interpretation, and limitations |
| Sheet exports          | Preserve fixed visual records of the spreadsheet outputs       |
| Visual assets          | Provide reusable chart and table images                        |
| Data documentation     | Explains dataset scope, processing, and reproducibility        |
| Data dictionary        | Defines variables, units, formulas, and classifications        |
| Google Sheets workbook | Provides the dynamic formula and calculation workspace         |

This separation makes the project easier to review and prevents the written interpretation from being confused with the supporting spreadsheet evidence.

---

## 6. Relationship to the Part 2 Workflow

```text
Source observations
    |
    v
Country and year sorting
    |
    v
Paired-observation calculations
    |
    v
Year-difference calculation
    |
    v
National, rural, and urban ARC
    |
    v
Missing-value and full-access classification
    |
    v
Paired rural-urban comparison
    |
    v
Regional enrichment and aggregation
    |
    v
Summary calculations and charts
    |
    v
Analytical reporting
```

The transformed-sheet export documents the calculation layer.

The Summary export documents the aggregation and visualisation layer.

The analytical report explains the evidence and places the results within their methodological limits.

---

## 7. Core Analytical Measures

### Observation interval

```text
y_diff = later year - earlier year
```

`y_diff` accounts for comparison intervals ranging from one to five years.

### Annual Rate of Change

```text
ARC =
(later access percentage - earlier access percentage)
/
(later year - earlier year)
```

ARC is expressed in:

```text
percentage points per year
```

The three area-based measures are:

* `ARC_n`: national ARC;
* `ARC_r`: rural ARC;
* `ARC_u`: urban ARC.

### Rural-urban ARC difference

```text
ARC_diff = ARC_r - ARC_u
```

A positive `ARC_diff` means rural ARC is numerically higher than urban ARC.

This usually represents faster rural improvement. However, if both ARC values are negative, it can instead mean that rural access declined more slowly than urban access.

---

## 8. Verified Findings Documented in the Reports

The reports support the following conclusions:

1. The completed dataset contains paired observations rather than a complete annual panel.
2. All 231 countries or areas have a 2015 baseline.
3. A total of 213 countries or areas have their later observation in 2020.
4. Approximately 96.1% of all records belong to either 2015 or 2020.
5. The median observation interval is five years.
6. Average and median rural ARC are higher than the corresponding national and urban measures.
7. Positive ARC below full access is the largest classification in all three population areas.
8. Rural full access is less common than national or urban full access.
9. Among 165 valid paired comparisons, 112 have a positive `ARC_diff`.
10. Every regional average paired `ARC_diff` is positive.
11. Middle East & North Africa has the highest average rural ARC.
12. Sub-Saharan Africa has the highest average national and urban ARC.
13. East Asia & Pacific has the largest regional population total.
14. Regional ARC values are unweighted country averages.
15. Population size alone does not explain regional ARC patterns.

These findings are descriptive. They do not demonstrate causality.

---

## 9. Interpretation Rules

### ARC measures change, not access level

A high ARC does not mean that current access is high.

A region can make rapid progress while still having a substantial access deficit.

### Low ARC does not automatically mean poor performance

Low ARC can result from a ceiling effect when access is already close to universal.

### Full access is approximate

The full-access flags use access values rounded to zero decimal places. Both paired values must round to 100.

The flags therefore identify approximate full access, not necessarily original values of exactly 100.000%.

### Missing values are not zero

| Value                 | Interpretation                                                |
| --------------------- | ------------------------------------------------------------- |
| Blank                 | No calculation is expected on that row                        |
| `Null` or missing ARC | A calculation was expected, but required data was unavailable |
| Numeric zero          | A valid calculation produced no measured change               |

### Regional averages are unweighted

Each valid country contributes equally to its regional ARC average, regardless of population size.

The results describe the average country-level pattern, not the average experience of a regional resident.

### Rural and urban samples can differ

Rural ARC has 167 valid observations, while urban ARC has 181.

Independent regional rural and urban averages may therefore be based on different sets of countries. Direct comparison should use the paired country-level `ARC_diff` wherever possible.

---

## 10. Recommended Review Order

For the clearest review of Part 2:

1. Read the [Part 2 Analytical Report](./analytical_report/Part2_Analytical_Report.md).
2. Review the [Summary PDF](./sheet_exports/Summary.pdf).
3. Review the [Transformed Dataset PDF](./sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf).
4. Consult the [Data Dictionary](../data/data_dictionary.md) for variable definitions and formula logic.
5. Review the [Main Visual Documentation](../assets/main_visuals/README.md).
6. Review the [Regional ARC Table Documentation](../assets/regional_arc_tables/README.md).
7. Open the Google Sheets workbook when formula-level inspection is required.

---

## 11. Google Sheets Workbook

The dynamic analytical workbook is available here:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook is required to inspect:

* cell formulas;
* lookup ranges;
* dynamic calculations;
* chart source ranges;
* sorting and filters;
* the relationships between the transformed and Summary sheets.

The PDF exports provide fixed documentation but cannot replace the workbook for formula-level verification.

---

## 12. Reproducibility Limitations

The repository currently contains:

* Markdown documentation;
* PNG chart and table assets;
* PDF worksheet exports.

It does not currently contain machine-readable CSV or XLSX exports of the transformed dataset.

Full reproducibility would be improved by adding:

* a CSV or XLSX export of the transformed data;
* a machine-readable Summary table;
* a regional aggregation file;
* the country-level `ARC_diff` values;
* a formula-reference document;
* a reproducible Python or R workflow.

Until these additions are made, the Google Sheets workbook remains necessary for direct formula and calculation inspection.

---

## 13. Related Part 2 Folders

### Data documentation

[Open the data folder](../data/)

Contains:

* the Part 2 data README;
* the data dictionary;
* variable definitions;
* transformation logic;
* missing-value explanations;
* reproducibility notes.

### Visual assets

[Open the assets folder](../assets/)

Contains:

* the four main visualisations;
* detailed chart documentation;
* seven regional ARC table screenshots;
* limitations concerning screenshot completeness.

---

## 14. Final Reporting Note

The reports folder provides the evidence and interpretation layer for Part 2.

The analytical report should be used for conclusions. The sheet exports should be used to verify the visible spreadsheet outputs. The Google Sheets workbook should be used when formulas and dynamic calculations need to be inspected.

All results should be interpreted with the following limitations in mind:

* the analytical observations cover 2015 to 2020;
* the dataset is not a complete annual panel;
* rural and urban data contain substantial missingness;
* full access is based on rounded estimates;
* regional ARC values are unweighted;
* aggregated values conceal country-level variation;
* ARC measures the rate of change rather than the final access level;
* the analysis identifies descriptive patterns but does not establish causality.
