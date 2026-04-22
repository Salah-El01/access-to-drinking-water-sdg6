# Part 1 — Understanding the Data  
**Project:** Access to Drinking Water (SDG 6)

## Overview
This repository section contains **Part 1** of the *Access to Drinking Water* project, focused on understanding, cleaning, and exploring the 2020 drinking-water access dataset before any deeper transformation or feature engineering work.

The objective of this phase is to build a solid analytical foundation by examining how access to drinking water varies across countries, area types, and income groups, using structured spreadsheet-based analysis and clear reporting outputs.

This part of the project is not only a first exploration of the dataset; it is the stage where data quality issues are identified, key variables are interpreted, summary reports are built, and the first analytical patterns become visible.

---

## Project Goal
The goal of Part 1 is to answer a simple but important question:

**What does the 2020 data reveal about global inequalities in access to drinking water?**

To answer it, this phase focuses on:
- understanding the dataset structure and variables,
- checking import quality and fixing formatting issues,
- identifying missing or inconsistent values,
- building clean summary tables,
- comparing access levels across national, urban, and rural contexts,
- and exploring how drinking-water access changes across income groups.

---

## Dataset Context
The analysis is based on the **WHO/UNICEF Joint Monitoring Programme (JMP) 2020 estimates on the use of water**.

The working dataset includes:
- country name,
- year,
- national population,
- urban population share,
- national drinking-water service levels,
- rural drinking-water service levels,
- urban drinking-water service levels.

The service-level indicators analyzed in this project are:
- **At least basic service**
- **Limited service**
- **Unimproved service**
- **Surface water**

Although JMP commonly distinguishes five service levels, the dataset used here groups safely managed and basic services together under **at least basic service**.

---

## What Was Done in Part 1
Part 1 followed a complete exploratory workflow in Google Sheets:

### 1. Data import and structure verification
- Imported the source CSV into Google Sheets.
- Verified that the dataset was correctly separated into rows and columns.
- Detected formatting issues caused by semicolon-separated entries in some rows.
- Created checks to validate that each row contained the expected number of values.

### 2. Initial cleaning
- Fixed wrongly imported rows.
- Preserved missing values explicitly as `NAN` where relevant.
- Created helper columns to support validation and analysis.
- Addressed impossible or problematic values, such as national basic-service percentages slightly above 100%, by creating cleaned/rounded versions instead of overwriting original raw values.

### 3. Population exploration
- Summarized national population values.
- Compared dataset coverage with the broader global population context.
- Examined the distribution of urban and rural population shares.

### 4. Access analysis by area
- Investigated national drinking-water access across the four service levels.
- Built separate summaries for:
  - national access,
  - urban access,
  - rural access.
- Compared how access composition changes depending on area type.

### 5. Access analysis by population structure
- Explored the relationship between population share and service-level composition.
- Created grouped visual summaries using rounded population-share features.

### 6. Access analysis by income group
- Built a pivot-table summary by income group.
- Compared average water-access levels across:
  - Low income,
  - Lower middle income,
  - Upper middle income,
  - High income economies.
- Highlighted the income gradient in drinking-water access.

### 7. Reporting and documentation
- Exported structured report PDFs from the spreadsheet work.
- Organized assets and report outputs for reproducibility and portfolio presentation.
- Prepared this project structure so that Part 2 can build on a cleaner and better-understood analytical base.

---

## Main Analytical Insight
The clearest pattern emerging from Part 1 is that **drinking-water access strongly improves as income level rises**.

In broad terms:
- **high-income countries** are concentrated in very high basic-service coverage,
- **low-income countries** show much lower average basic access,
- and the shares of **limited**, **unimproved**, and **surface water** are much more present in poorer countries.

A second major finding is the **urban–rural gap**:
- urban areas generally show stronger access conditions,
- while rural areas more often carry the burden of lower-quality service levels.

Together, these patterns show that drinking-water access is shaped by both **economic capacity** and **territorial inequalities**.

---

## Folder Structure
```text
part-1-understanding-the-data/
│
├── assets/
│   ├── 01_population_vs_urban_rural_share.png
│   ├── 02_urban_service_levels_distribution.png
│   ├── 03_rural_service_levels_distribution.png
│   ├── 04_income_group_vs_service_levels.png
│   ├── 05_key_findings_summary_table.png
│   └── README.md
│
├── data/
│   └── README.md
│
├── reports/
│   ├── Global_2020_Report.pdf
│   ├── Urban_2020_Report.pdf
│   ├── Rural_2020_Report.pdf
│   ├── Pivot_Table.pdf
│   ├── Part1_Full_Report.pdf
│   └── README.md
│
└── README.md
