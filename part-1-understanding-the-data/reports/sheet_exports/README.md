# Sheet Exports

This folder contains PDF exports of the four main Google Sheets analysis tabs used in Part 1 of my **Access to Drinking Water** project.

I included these exports to make the visible spreadsheet outputs directly accessible from the repository. They document the final tables, summary statistics, findings, pivot results, and visualizations produced during the analysis.

The PDFs support the analytical report but do not replace the original Google Sheets workbook, which remains the source of truth for formulas, data transformations, filters, and chart configurations.

## Project navigation

- [Part 1 Analytical Report](../analytical_report/Part1_Analytical_Report.md)
- [Data documentation](../../data/README.md)
- [Data dictionary](../../data/Data_dictionary.md)
- [Open the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit)

---

## Files included

| Sheet export | Source sheet | Main analytical purpose |
|---|---|---|
| [Global 2020 Report.pdf](<./Global 2020 Report.pdf>) | Global 2020 Report | National overview, population analysis, distribution statistics, and national–urban–rural comparison |
| [Urban 2020 Report.pdf](<./Urban 2020 Report.pdf>) | Urban 2020 Report | Analysis of urban drinking-water service levels |
| [Rural 2020 Report.pdf](<./Rural 2020 Report.pdf>) | Rural 2020 Report | Analysis of rural drinking-water access and inequality |
| [Pivot_Table.pdf](./Pivot_Table.pdf) | Pivot Table | Income-group aggregation and socioeconomic comparison |

---

## Global 2020 Report

[View the Global 2020 Report export](<./Global 2020 Report.pdf>)

I used the **Global 2020 Report** sheet as the main analytical reporting layer for the 2020 country-level data.

The export contains:

- The prepared national dataset
- Source and derived population variables
- Cleaned national, urban, and rural service-level variables
- National population-size analysis
- Urban and rural population-share comparison
- Summary statistics for drinking-water access
- A box-and-whisker-style comparison of service distributions
- National service-level distribution analysis
- Written interpretations of the principal findings

The sheet compares four drinking-water service levels:

- At least basic
- Limited
- Unimproved
- Surface water

It also provides the main evidence for the urban–rural comparison developed in the analytical report.

---

## Urban 2020 Report

[View the Urban 2020 Report export](<./Urban 2020 Report.pdf>)

I used the **Urban 2020 Report** sheet to isolate urban drinking-water estimates and analyze how service-level access varied across urban population-share groups.

The export contains:

- Urban population-share categories
- Cleaned urban service-level variables
- Aggregated urban service-level averages
- A 100% stacked service-distribution chart
- A supporting interpretation table
- A conclusion summarizing the urban findings

The sheet shows that urban areas generally recorded high at-least-basic access, while limited, unimproved, and surface-water services represented comparatively small shares of the average urban distribution.

---

## Rural 2020 Report

[View the Rural 2020 Report export](<./Rural 2020 Report.pdf>)

I used the **Rural 2020 Report** sheet to examine drinking-water access among rural populations.

The export contains:

- Rural population-share categories
- Cleaned rural service-level variables
- Complete-case rural observations
- Aggregated rural service-level averages
- A 100% stacked service-distribution chart
- A supporting interpretation table
- A conclusion summarizing the rural findings

This sheet highlights the lower average level and greater variability of rural at-least-basic access. It also shows the greater rural contribution of limited, unimproved, and surface-water services.

---

## Pivot Table

[View the Pivot Table export](./Pivot_Table.pdf)

I used the **Pivot Table** sheet to summarize population, urbanization, and national drinking-water access by income group.

The export contains:

- Income-group categories
- Income-group sorting through `income_group_num`
- Sum of national population
- Average urban population share
- Average national at-least-basic access
- Average national limited access
- Average national unimproved access
- Average national surface-water access
- A chart comparing average service levels across income groups
- Written interpretations of the pivot-table findings

The pivot table identifies a clear descriptive association between income classification and drinking-water access. Higher-income groups recorded higher average at-least-basic access and lower average reliance on limited, unimproved, and surface-water services.

The averages are country-level group averages and should not be interpreted as population-weighted global coverage estimates.

---

## How the exports support the project

I included the sheet exports for three main reasons:

### 1. Transparency

The exports allow reviewers to inspect the visible Google Sheets outputs behind the analytical report.

### 2. Traceability

Each PDF corresponds to one of the four principal analytical sheets, making it easier to connect the methodology, calculations, visualizations, and findings.

### 3. Portfolio accessibility

The PDFs allow the project outputs to be reviewed directly from GitHub without requiring immediate access to the complete Google Sheets interface.

---

## Important interpretation notes

- The PDFs are static snapshots of the completed Google Sheets tabs.
- The original Google Sheets workbook remains the primary analytical workspace.
- The workbook should be consulted when reviewing exact formulas, cell references, filters, pivot-table settings, or chart configurations.
- Blank results were retained where the required source values were incomplete.
- Aggregated service-level averages are generally unweighted country-level averages unless otherwise specified.
- Rounded population measures were used for grouping and visualization, not as replacements for the original population values.
- The income-group comparison is descriptive and does not establish causality.
- The `NAN` income category represents observations without a verified income classification and is not treated as an ordered income level.

---

## Related documentation

For the complete explanation of the methodology and findings, see:

- [Part 1 Analytical Report](../analytical_report/Part1_Analytical_Report.md)
- [Data README](../../data/README.md)
- [Data Dictionary](../../data/Data_dictionary.md)
