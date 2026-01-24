# Data

This project uses the WHO/UNICEF Joint Monitoring Programme (JMP) drinking-water access estimates (2020).
The working dataset and all transformations (cleaning, feature engineering, pivots, and charts) are maintained in Google Sheets.

## Google Sheets (source of truth)
- View-only spreadsheet: https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing

## What’s included there
- Original dataset (kept in the sheet; not uploaded to this repository)
- Cleaning steps and validation checks
- Derived features (urban/rural shares, population binning)
- Pivot tables and charts used in the analysis

## Why the raw dataset is not stored in this repo
To keep the repository lightweight and to preserve a single canonical “working file” where formulas and transformations are transparent and reproducible.

## Outputs published in this repo
See:
- `reports/` for PDF exports
- `assets/` for figures referenced in the main README
