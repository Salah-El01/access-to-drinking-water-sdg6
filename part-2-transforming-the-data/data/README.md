# Data

This folder documents the data layer used in **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The analysis is based on the **WHO/UNICEF Joint Monitoring Programme (JMP) drinking-water access estimates (2000–2020)**.  
The full working file — including the original dataset, transformation steps, validation checks, derived features, regional lookup, summary tables, and chart preparation — was maintained in Google Sheets.

## Google Sheets (source of truth)

- View-only spreadsheet: [View the spreadsheet](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

## What is included in the spreadsheet

- Original 2000–2020 JMP drinking-water access dataset
- Year representation checks
- Country/year sorting logic
- Year-difference calculation (`y_diff`)
- Annual Rate of Change calculations:
  - `ARC_n` for national access
  - `ARC_r` for rural access
  - `ARC_u` for urban access
- Rounded basic-access indicators:
  - `wat_bas_n_round`
  - `wat_bas_r_round`
  - `wat_bas_u_round`
- Full-access classification fields:
  - `ARC_n_full`
  - `ARC_r_full`
  - `ARC_u_full`
- Rural–urban progress difference:
  - `ARC_diff`
- Region lookup and regional enrichment
- Summary tables by area and region
- Charts used in the analysis

## Why the raw dataset is not stored here

To keep the repository lightweight and to preserve a single working file where formulas, transformations, lookup logic, and chart preparation remain transparent and reproducible.

The Google Sheets workbook remains the source of truth for the transformation process, while this repository stores the documentation, exported reports, and visual outputs.

## Related outputs in this repository

See:

- `part-2-transforming-the-data/reports/` for PDF exports
- `part-2-transforming-the-data/assets/` for figures and table extracts used in the README
