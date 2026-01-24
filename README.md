# Access to Drinking Water (SDG 6) — WHO/UNICEF JMP 2020 (Google Sheets Analysis)

## Objective
Analyze global disparities in drinking-water access across **national / urban / rural** areas and across **income groups**, using WHO/UNICEF JMP 2020 estimates.

## Dataset
- Source: WHO/UNICEF Joint Monitoring Programme (JMP), 2020
- Coverage: 214 countries/areas
- Service levels: **At least basic**, **Limited**, **Unimproved**, **Surface water**

## Tools
- Google Sheets (cleaning, feature engineering, pivot tables, visuals)
- PDF exports for reporting

## Google Sheet (view-only)
The full working file (data cleaning steps, formulas, pivot tables, and charts) is available here:
- **Google Sheet:** [View the spreadsheet](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

> Note: This repository contains exported deliverables (PDFs) and figures. The spreadsheet remains the source of truth for the calculations and transformations.

## Workflow
- Cleaned and validated the dataset (delimiter inconsistencies, completeness checks, composition sums ≈ 100%)
- Engineered features (urban/rural shares, population binning)
- Produced descriptive statistics and distribution summaries
- Built 100% stacked composition visuals (urban vs rural)
- Built an income-group pivot table to quantify the gradient

## Key insights (2020)
- Urban access is consistently higher than rural access; rural gaps drive most deprivation.
- Low-income groups show much lower “at least basic” access and higher unsafe categories than high-income groups.
- Unimproved and surface water shares are concentrated in rural contexts and low-income countries.

## Deliverables (PDF exports)
- **Full report (Part 1):** [Part 1 – Full Report](reports/Part1_Full_Report.pdf)
- **Global (National) report:** [Global 2020 Report](reports/Global_2020_Report.pdf)
- **Urban report:** [Urban 2020 Report](reports/Urban_2020_Report.pdf)
- **Rural report:** [Rural 2020 Report](reports/Rural_2020_Report.pdf)
- **Income group pivot summary:** [Pivot Table](reports/Pivot_Table.pdf)

## Next steps
- Rebuild Part 1 outputs as an interactive dashboard (Power BI/Tableau) with filters and a “worst-off” ranking view.
