# Access to Drinking Water (SDG 6)

## Overview

This project analyzes global access to drinking water using data from the **WHO/UNICEF Joint Monitoring Programme (JMP)**.

The work is organized as a two-part data analysis project. The first part focuses on understanding the structure and inequalities visible in the 2020 drinking-water access data. The second part extends the analysis by transforming a broader 2000–2020 dataset to measure progress over time.

The project was completed in **Google Sheets** and documented through structured reports, visual assets, and GitHub documentation.

---

## Project Objective

The main objective of this project is to explore how access to drinking water varies across countries, area types, income groups, and regions.

More specifically, the project asks:

**How unequal is access to drinking water, and how has access to at least basic drinking-water services changed over time?**

To answer this question, the project is divided into two analytical stages:

- **Part 1 — Understanding the Data**
- **Part 2 — Transforming the Data**

---

## Project Structure

```text
access-to-drinking-water-sdg6/
│
├── part-1-understanding-the-data/
│   ├── assets/
│   ├── data/
│   ├── reports/
│   └── README.md
│
├── part-2-transforming-the-data/
│   ├── assets/
│   ├── data/
│   ├── reports/
│   └── README.md
│
└── README.md
```
---

## Part 1 — Understanding the Data

The first part of the project focuses on understanding, cleaning, and exploring the **2020 JMP drinking-water access dataset**.

This phase investigates how access to drinking water differs across:

- countries,
- national, urban, and rural areas,
- population structures,
- and income groups.

The work includes:

- data import and structure verification,
- cleaning and validation checks,
- population exploration,
- descriptive statistics,
- urban and rural access comparison,
- income-group pivot analysis,
- exported charts and PDF reports.

The main finding from Part 1 is that drinking-water access is shaped by strong inequalities. Urban areas generally show better access than rural areas, and high-income countries are much closer to universal basic access than low-income countries.

More details are available in:

[`part-1-understanding-the-data/`](./part-1-understanding-the-data/)

---

## Part 2 — Transforming the Data

The second part of the project focuses on transforming the **2000–2020 JMP drinking-water dataset** into a structure that can measure progress over time.

This phase introduces time-based analysis through **Annual Rates of Change (ARC)**.

The work includes:

- year representation checks,
- country/year sorting,
- year-difference calculations,
- national, rural, and urban ARC calculations,
- full-access classification,
- rural–urban progress comparison,
- regional enrichment,
- regional summary tables and charts.

The main finding from Part 2 is that progress in drinking-water access is uneven. Rural areas often show higher rates of improvement than urban areas, but this must be interpreted carefully because many urban areas were already close to or at full basic access.

More details are available in:

[`part-2-transforming-the-data/`](./part-2-transforming-the-data/)

---

## Tools Used

- **Google Sheets** — data cleaning, transformation, formulas, pivot tables, and charts
- **GitHub** — project organization and portfolio documentation
- **WHO/UNICEF JMP data** — source data for drinking-water access estimates

---

## Key Skills Demonstrated

This project demonstrates:

- data cleaning,
- data validation,
- spreadsheet-based analysis,
- feature engineering,
- descriptive statistics,
- pivot-table analysis,
- time-based transformation,
- Annual Rate of Change calculation,
- regional aggregation,
- data visualization,
- analytical reporting,
- GitHub documentation,
- and data storytelling.

---

## Main Outputs

The repository contains:

- structured project documentation,
- Google Sheets source-of-truth links,
- exported PDF reports,
- visual assets,
- regional table extracts,
- and separate READMEs for each analytical layer.

The project is organized so that each part can be reviewed independently while still contributing to the full SDG 6 drinking-water analysis.

---

## Data Source

The data used in this project comes from the **WHO/UNICEF Joint Monitoring Programme (JMP)**, which monitors global progress on drinking water, sanitation, and hygiene.

The analysis focuses on drinking-water service levels, especially:

- at least basic service,
- limited service,
- unimproved service,
- surface water.

---

## Portfolio Purpose

This project is part of my data science portfolio.

It shows how spreadsheet-based analysis can be used to build a complete analytical workflow: from understanding raw data, validating quality, and identifying inequalities, to transforming the dataset and measuring progress over time.
