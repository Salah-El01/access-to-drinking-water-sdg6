# Sheet Exports - Part 2: Transforming the Data

This folder contains PDF exports of the two principal Google Sheets tabs used in **Part 2: Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The exports provide a fixed visual record of:

* the transformed country-level dataset;
* the derived Annual Rate of Change variables;
* the Summary calculations;
* the regional aggregations;
* the four completed charts.

They support the analytical report by showing the spreadsheet outputs from which the documented results were obtained.

---

## Files Included

| File                                                                                                             | Pages | Orientation | Primary role                                            |
| ---------------------------------------------------------------------------------------------------------------- | ----: | ----------- | ------------------------------------------------------- |
| [`Estimates of the use of water (2000-2020).pdf`](Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf) |     4 | Landscape   | Transformation and calculation layer                    |
| [`Summary.pdf`](Summary.pdf)                                                                                     |     4 | Landscape   | Reporting, aggregation, and visual interpretation layer |

---

## 1. Transformed Dataset Export

### [`Estimates of the use of water (2000-2020).pdf`](Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf)

This PDF is an export of the transformed worksheet named:

```text
Estimates of the use of water (2000-2020)
```

The worksheet title refers to the broader source-data period. However, the observations retained in the completed Part 2 analysis cover **2015 to 2020**.

The analytical dataset contains:

* 231 countries or areas;
* 462 observations;
* exactly two observations per country or area;
* a 2015 baseline for every country or area;
* one later observation between 2016 and 2020.

### Main contents

The export includes the original identification, population, and drinking-water variables, together with the derived fields used in Part 2.

| Variable group              | Examples                                                |
| --------------------------- | ------------------------------------------------------- |
| Identification              | `name`, `year`                                          |
| Population                  | `pop_n`, `pop_u`                                        |
| National water access       | `wat_bas_n`, `wat_lim_n`, `wat_unimp_n`, `wat_sur_n`    |
| Rural water access          | `wat_bas_r`, `wat_lim_r`, `wat_unimp_r`, `wat_sur_r`    |
| Urban water access          | `wat_bas_u`, `wat_lim_u`, `wat_unimp_u`, `wat_sur_u`    |
| Observation interval        | `y_diff`                                                |
| Annual Rates of Change      | `ARC_n`, `ARC_r`, `ARC_u`                               |
| Rounded access values       | `wat_bas_n_round`, `wat_bas_r_round`, `wat_bas_u_round` |
| Full-access classifications | `ARC_n_full`, `ARC_r_full`, `ARC_u_full`                |
| Rural-urban comparison      | `ARC_diff`                                              |
| Regional enrichment         | `region`                                                |

### Analytical role

This worksheet is the transformation layer of the project.

It shows how the source observations were enriched with:

* country-pair comparison logic;
* observation intervals;
* annualised access changes;
* controlled missing-value outputs;
* approximate full-access flags;
* rural-urban ARC differences;
* regional classifications.

The four landscape pages divide the large worksheet into printable sections. They should be read as consecutive parts of the same transformed dataset.

---

## 2. Summary Export

### [`Summary.pdf`](Summary.pdf)

This PDF is an export of the `Summary` worksheet.

The Summary sheet is the reporting and interpretation layer of Part 2. It links the country-level derived results to calculation blocks, regional summaries, and charts.

### Main contents

The export contains:

* a linked analytical table with country and regional values;
* population values converted to millions;
* year-frequency calculations;
* observation-interval statistics;
* national, rural, and urban ARC summaries;
* missing-value counts;
* approximate full-access counts;
* zero, negative, and positive ARC classifications;
* country-level `ARC_diff` values;
* regional country and population totals;
* average national, rural, and urban ARC by region;
* average paired rural-urban ARC difference by region;
* four completed visualisations.

### Four existing visualisations

The current Summary export contains:

1. **Histogram of Year**
2. **Average Rural-Urban ARC Difference by Region**
3. **Average ARC Values for Rural Versus Urban Areas per Region**
4. **Regional Progress in Basic Water Access: ARC and Population**

The first visual uses discrete year categories and is more accurately interpreted as a year-frequency column chart.

### Current Summary limitations

The Summary export documents the current workbook state, including two incomplete project requirements:

* median national, rural, and urban ARC values are not displayed in the Summary calculation block;
* the required country-level `ARC_diff` histogram is not present.

The existing regional average `ARC_diff` chart does not replace the missing country-level histogram. The two visuals answer different analytical questions:

| Visual                             | Question answered                                              |
| ---------------------------------- | -------------------------------------------------------------- |
| Regional average `ARC_diff` chart  | How does the average paired difference compare across regions? |
| Country-level `ARC_diff` histogram | How are the 165 valid country-level differences distributed?   |

The verified ARC medians and country-level `ARC_diff` statistics are documented in the analytical report.

---

## 3. What the PDFs Can Verify

The exports provide visual evidence of:

* the spreadsheet structure;
* the names and order of variables;
* the transformed values;
* missing and `Null` outputs;
* full-access labels;
* the Summary calculation blocks;
* classification counts;
* regional aggregation values;
* chart titles, axes, series, and displayed values;
* the spreadsheet state at the time of export.

They are useful for:

* portfolio review;
* analytical documentation;
* visual validation;
* checking reported values against the workbook outputs;
* preserving a fixed record of the spreadsheet layout.

---

## 4. What the PDFs Cannot Verify

The exports are static documents. They do not provide the same functionality as the original Google Sheets workbook.

They cannot independently show:

* the formulas stored inside cells;
* cell references and lookup ranges;
* dynamic recalculation;
* data-validation rules;
* chart source ranges;
* filters and sorting controls;
* pivot-table settings;
* hidden rows or columns;
* revision history;
* complete machine-readable data extraction.

The PDFs display calculated results, but they do not provide full formula-level reproducibility.

For formula logic and variable definitions, consult the project documentation:

* [Data documentation](../../data/README.md)
* [Data dictionary](../../data/data_dictionary.md)
* [Part 2 analytical report](../analytical_report/Part2_Analytical_Report.md)

---

## 5. Important Interpretation Rules

When reviewing the exports, the following distinctions must be preserved.

### Analytical coverage

Although the transformed worksheet filename contains `2000-2020`, the observations analysed in the completed dataset cover **2015 to 2020**.

### ARC unit

`ARC_n`, `ARC_r`, `ARC_u`, and `ARC_diff` are expressed in:

```text
percentage points per year
```

They are not percentage growth rates.

### Blank, `Null`, and zero

| Displayed value         | Meaning                                                       |
| ----------------------- | ------------------------------------------------------------- |
| Blank                   | No calculation is expected for that row                       |
| `Null` or missing value | A calculation was expected, but required data was unavailable |
| `0`                     | The calculation was completed and no change was measured      |

### Full access

Full-access flags use access values rounded to zero decimal places. Both paired values must round to 100.

The flags therefore represent **approximate full access**, not necessarily an original unrounded value of exactly 100.000%.

### Regional averages

Regional ARC values are unweighted country averages. Each country with a valid value contributes equally, regardless of population size.

The regional averages describe the average country pattern, not the rate experienced by the average regional resident.

### Paired and independent averages

The regional `ARC_diff` chart averages valid paired country-level differences:

```text
AVERAGE(ARC_r - ARC_u)
```

The rural-versus-urban chart calculates rural and urban averages independently. Because their missing-value patterns differ, the two series may not contain exactly the same countries.

---

## 6. Relationship to the Analytical Report

The full methodology, verified statistics, findings, limitations, and conclusions are documented in:

[Part 2 Analytical Report](../analytical_report/Part2_Analytical_Report.md)

The relationship between the files is:

```text
Transformed-sheet export
    |
    v
Documents country-level calculations
    |
    v
Summary-sheet export
    |
    v
Documents aggregations and visuals
    |
    v
Analytical report
    |
    v
Explains methodology, findings, and limitations
```

The exports provide supporting spreadsheet evidence. The analytical report provides the structured interpretation.

---

## 7. Related Visual Documentation

Individual chart images and detailed interpretation notes are available in:

* [Main visual documentation](../../assets/main_visuals/README.md)
* [Regional ARC table documentation](../../assets/regional_arc_tables/README.md)
* [Assets index](../../assets/README.md)

The PNG assets are more suitable than the full-sheet PDFs when an individual chart or regional table needs to be displayed directly in GitHub documentation.

---

## 8. Reproducibility Note

The Google Sheets workbook remains the main analytical workspace:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The repository currently contains PDF and PNG documentation but does not include machine-readable CSV or XLSX exports of the transformed data.

Reproducibility would be improved by adding:

* a CSV or XLSX export of the transformed dataset;
* a machine-readable export of the Summary table;
* a regional aggregation table;
* the 165 valid country-level `ARC_diff` values;
* a formula-reference document or reproducible Python/R workflow.

Until those files are added, the Google Sheets workbook is required for direct inspection of formulas and dynamic calculations.

---

## 9. File Maintenance

When the Google Sheets workbook is updated:

1. recalculate and validate all formulas;
2. confirm that classification totals still equal 231;
3. verify missing and valid ARC counts;
4. verify the regional aggregation table;
5. update or add the required visuals;
6. export both sheets again;
7. replace the corresponding PDFs without changing their filenames;
8. check every exported page for clipped columns, unreadable text, or missing charts;
9. update the analytical report if any result changes.

Keeping stable filenames ensures that links from the analytical report and other repository documentation continue to work.
