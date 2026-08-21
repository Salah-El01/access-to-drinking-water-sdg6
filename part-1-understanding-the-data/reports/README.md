# Reports — Part 1: Understanding the Data

This folder contains the reporting layer of Part 1 of my **Access to Drinking Water** project.

I organized the reporting outputs into two complementary components:

1. **Analytical report** — the complete written explanation of my methodology, analysis, findings, limitations, and conclusions.
2. **Sheet exports** — static PDF exports of the four principal Google Sheets analysis tabs.

The analytical report should be used as the primary interpretation of the project. The sheet exports provide supporting evidence by preserving the visible tables, summaries, visualizations, and pivot-table outputs produced in Google Sheets.

---

## Quick navigation

- [Read the Part 1 Analytical Report](./analytical_report/Part1_Analytical_Report.md)
- [Open the Sheet Exports folder](./sheet_exports/)
- [Read the Sheet Exports documentation](./sheet_exports/README.md)
- [Review the visual assets](../assets/)
- [Read the data documentation](../data/README.md)
- [Consult the Data Dictionary](../data/Data_dictionary.md)
- [Return to the Part 1 overview](../README.md)
- [Open the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit)

---

## Folder structure

```text
reports/
├── analytical_report/
│   └── Part1_Analytical_Report.md
│
├── sheet_exports/
│   ├── Global 2020 Report.pdf
│   ├── Urban 2020 Report.pdf
│   ├── Rural 2020 Report.pdf
│   ├── Pivot_Table.pdf
│   └── README.md
│
└── README.md
```

---

## Reporting components

| Component | Purpose | Recommended use |
|---|---|---|
| [Part 1 Analytical Report](./analytical_report/Part1_Analytical_Report.md) | Explains the complete analytical workflow and findings | Start here for a complete understanding of the project |
| [Sheet Exports](./sheet_exports/) | Preserves the visible outputs of the four Google Sheets reporting tabs | Use as supporting evidence when reviewing the analysis |
| [Sheet Exports README](./sheet_exports/README.md) | Documents the purpose and contents of each PDF export | Use as an index for the exported sheets |

---

# Analytical Report

The main written report is available here:

## [Part 1 Analytical Report — Access to Drinking Water](./analytical_report/Part1_Analytical_Report.md)

I developed this report to explain:

- The project objective
- The source data and analytical scope
- The source variables used
- The structural validation process
- The derived population features
- The service-level cleaning methodology
- The verified Google Sheets formulas and functions
- The aggregation and sorting methodology
- The Global 2020 Report analysis
- The Urban 2020 Report analysis
- The Rural 2020 Report analysis
- The income-group pivot analysis
- The cross-sheet findings
- The analytical limitations
- The final conclusions and recommendations

The analytical report connects the technical work completed in Google Sheets with the overall project objective of understanding inequalities in drinking-water access.

---

# Sheet Exports

The supporting sheet exports are located in the [sheet_exports](./sheet_exports/) folder.

| Export | Analytical focus |
|---|---|
| [Global 2020 Report.pdf](<./sheet_exports/Global 2020 Report.pdf>) | National dataset, derived features, summary statistics, population analysis, and national–urban–rural comparison |
| [Urban 2020 Report.pdf](<./sheet_exports/Urban 2020 Report.pdf>) | Urban service-level distribution and interpretation |
| [Rural 2020 Report.pdf](<./sheet_exports/Rural 2020 Report.pdf>) | Rural service-level distribution, inequality, and interpretation |
| [Pivot_Table.pdf](./sheet_exports/Pivot_Table.pdf) | Population, urbanization, and national service-level averages by income group |

For a more detailed explanation of these files, see the [Sheet Exports README](./sheet_exports/README.md).

---

## Global 2020 Report

[Open the Global 2020 Report export](<./sheet_exports/Global 2020 Report.pdf>)

I used this sheet as the principal 2020 reporting layer.

It contains:

- The prepared global dataset
- Source, derived, and cleaned variables
- Population-size analysis
- Urban and rural population-share comparison
- Summary statistics for the service-level variables
- A box-and-whisker-style distribution analysis
- National service-level visualizations
- Supporting interpretation tables
- The main global findings

---

## Urban 2020 Report

[Open the Urban 2020 Report export](<./sheet_exports/Urban 2020 Report.pdf>)

I used this sheet to analyze urban drinking-water access.

It contains:

- Rounded urban population-share groups
- Cleaned urban service-level variables
- Aggregated urban service-level averages
- A 100% stacked service-distribution chart
- A supporting interpretation table
- The conclusion for the urban findings

---

## Rural 2020 Report

[Open the Rural 2020 Report export](<./sheet_exports/Rural 2020 Report.pdf>)

I used this sheet to examine rural drinking-water access and the greater inequality found in rural service distributions.

It contains:

- Rounded rural population-share groups
- Cleaned rural service-level variables
- Complete-case rural observations
- Aggregated rural service-level averages
- A 100% stacked service-distribution chart
- A supporting interpretation table
- The conclusion for the rural findings

---

## Pivot Table

[Open the Pivot Table export](./sheet_exports/Pivot_Table.pdf)

I used this sheet to summarize the country-level data by income group.

It contains:

- Income-group categories
- Income-group sorting
- Sum of national population
- Average urban population share
- Average national service-level percentages
- A comparison chart by income group
- Written interpretations of the pivot-table findings

The pivot results show a descriptive relationship between income classification and drinking-water access. They do not establish a causal relationship.

---

# How I Recommend Reviewing This Folder

For the clearest review sequence:

1. Start with the [Part 1 Analytical Report](./analytical_report/Part1_Analytical_Report.md).
2. Review the supporting charts in the [assets folder](../assets/).
3. Open the relevant files in the [sheet_exports folder](./sheet_exports/).
4. Use the [Data Dictionary](../data/Data_dictionary.md) to verify variable definitions.
5. Consult the [Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit) when reviewing formulas, filters, pivot settings, or chart configurations.

---

# Relationship Between the Reporting Files

```text
Source data and documentation
            ↓
Data preparation in Google Sheets
            ↓
Global, Urban, and Rural report sheets
            ↓
Income-group Pivot Table
            ↓
Visual assets and PDF sheet exports
            ↓
Part 1 Analytical Report
```

This structure allows me to maintain a clear relationship between the source data, the Google Sheets methodology, the visible spreadsheet outputs, and the final analytical interpretation.

---

# Important Notes

- I completed the data preparation, calculations, aggregation, visualization, and pivot analysis in Google Sheets.
- The analytical report is the primary narrative document for Part 1.
- The PDF exports are static snapshots of the completed Google Sheets tabs.
- The PDFs preserve visible results but do not independently preserve every formula, filter, or chart configuration.
- The Google Sheets workbook remains the source of truth for formula-level inspection.
- Country-level averages are generally unweighted unless otherwise specified.
- Missing values and complete-case exclusions are documented in the analytical report.
- The exported PDFs support transparency, auditability, and portfolio review.
- The analytical findings are descriptive and should not be interpreted as causal conclusions.
