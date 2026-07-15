# Visual Assets — Part 2: Transforming the Data

This folder contains the visual and tabular outputs produced during Part 2 of the **Access to Drinking Water** project.

Part 2 focuses on transforming a multi-year drinking water dataset into a progress-monitoring framework using the **Annual Rate of Change (ARC)**.

The assets are divided into two categories:

1. **Main visuals** — charts communicating the principal analytical findings.
2. **Regional ARC tables** — country-level tables supporting the regional summaries and visual conclusions.

---

## Folder Structure

```text
assets/
├── main_visuals/
│   ├── 01_year_distribution_histogram.png
│   ├── 02_average_arc_diff_by_region.png
│   ├── 03_rural_vs_urban_arc_by_region.png
│   ├── 04_regional_progress_arc_population.png
│   └── README.md
│
├── regional_arc_tables/
│   ├── 01_east_asia_pacific_arc_table.png
│   ├── 02_europe_central_asia_arc_table.png
│   ├── 03_latin_america_caribbean_arc_table.png
│   ├── 04_middle_east_north_africa_arc_table.png
│   ├── 05_north_america_arc_table.png
│   ├── 06_south_asia_arc_table.png
│   ├── 07_sub_saharan_africa_arc_table.png
│   └── README.md
│
└── README.md
```

---

# Main Visuals

The main visual outputs are available here:

[Open the main visuals folder](./main_visuals/)

These charts summarize the most important findings from the transformed dataset.

---

## 01 — Year Distribution Histogram

![Year Distribution Histogram](./main_visuals/01_year_distribution_histogram.png)

This visual examines the distribution of observation years in the dataset.

Most records are concentrated in **2015** and **2020**, while only a small number of observations appear in the intermediate years.

### Main insight

The dataset is not a continuous annual time series. It is mainly structured around two major observation periods.

This makes the `y_diff` feature essential because it measures the actual number of years between observations for each country before calculating ARC.

---

## 02 — Average Rural–Urban ARC Difference by Region

![Average ARC Difference by Region](./main_visuals/02_average_arc_diff_by_region.png)

This chart compares the average rural–urban ARC difference across regions.

The metric is calculated as:

`ARC_diff = ARC_r - ARC_u`

### Interpretation

* `ARC_diff > 0` means rural access improved faster.
* `ARC_diff < 0` means urban access improved faster.
* `ARC_diff ≈ 0` means rural and urban progress were similar.

### Main insight

Every regional average is positive, showing that rural access improved faster than urban access on average across all regions.

The strongest rural catch-up patterns appear in:

* Middle East & North Africa
* Latin America & Caribbean

A positive difference reflects the speed of progress and does not necessarily mean that rural access has surpassed urban access.

---

## 03 — Average Rural and Urban ARC by Region

![Average Rural and Urban ARC by Region](./main_visuals/03_rural_vs_urban_arc_by_region.png)

This grouped chart compares average rural and urban ARC values directly.

It reveals the two components behind the regional `ARC_diff` values.

### Main insight

Average rural ARC is higher than average urban ARC in every region.

This indicates a broad rural catch-up pattern, likely influenced by lower rural starting access levels and greater remaining potential for improvement.

Middle East & North Africa records the highest rural ARC, while Sub-Saharan Africa shows meaningful progress in both rural and urban access.

---

## 04 — Regional Progress in Basic Water Access

![Regional Progress in Basic Water Access](./main_visuals/04_regional_progress_arc_population.png)

This visual combines:

* regional population size
* average national ARC
* average rural ARC

It connects the speed of water-access improvement with the population scale represented by each region.

### Main insight

Regional population size does not show a direct relationship with the rate of improvement.

South Asia combines a very large population with strong national and rural progress. Sub-Saharan Africa also shows substantial ARC values across a large population, while Middle East & North Africa records the strongest rural progress despite representing a smaller population.

The chart shows why ARC and population should be interpreted together:

* ARC measures the speed of progress.
* Population indicates the potential scale of that progress.

---

# Regional ARC Tables

The country-level regional tables are available here:

[Open the regional ARC tables folder](./regional_arc_tables/)

These tables provide the detailed observations behind the regional averages presented in the main visuals.

Each table includes:

* country or area name
* regional classification
* observation year
* national population estimate in thousands
* national population converted to millions
* national ARC
* rural ARC
* urban ARC

---

## Regional Tables Included

### East Asia & Pacific

[View the East Asia & Pacific table](./regional_arc_tables/01_east_asia_pacific_arc_table.png)

The region includes a mixture of positive, zero, negative, and unavailable ARC values.

Notable patterns include positive rural progress in large countries and negative ARC values in selected cases, demonstrating that the regional average does not describe every country equally.

---

### Europe & Central Asia

[View the Europe & Central Asia table](./regional_arc_tables/02_europe_central_asia_arc_table.png)

Many countries show low or zero ARC values, which may reflect high baseline access and limited remaining room for improvement.

The table also contains positive and negative country-level outcomes, showing meaningful internal variation.

---

### Latin America & Caribbean

[View the Latin America & Caribbean table](./regional_arc_tables/03_latin_america_caribbean_arc_table.png)

Several countries record strong rural ARC values compared with national and urban progress.

This supports the region’s large positive rural–urban ARC difference and its strong rural catch-up pattern.

---

### Middle East & North Africa

[View the Middle East & North Africa table](./regional_arc_tables/04_middle_east_north_africa_arc_table.png)

The table includes several strong rural progress cases, including particularly high ARC values in selected countries.

These observations contribute to the region having the highest average rural ARC.

---

### North America

[View the North America table](./regional_arc_tables/05_north_america_arc_table.png)

North America records relatively low ARC values overall.

This likely reflects high baseline access and a ceiling effect rather than weak drinking water service conditions.

---

### South Asia

[View the South Asia table](./regional_arc_tables/06_south_asia_arc_table.png)

South Asia combines substantial population size with strong national and rural improvement.

Several countries show rural ARC values above urban ARC, while a few cases also contain negative urban change.

---

### Sub-Saharan Africa

[View the Sub-Saharan Africa table](./regional_arc_tables/07_sub_saharan_africa_arc_table.png)

Sub-Saharan Africa contains the widest visible range of outcomes.

The region includes:

* countries making strong progress
* countries with mixed rural and urban results
* countries experiencing declining access
* countries with near-zero change

This variation demonstrates why regional averages must be interpreted alongside country-level evidence.

---

# Analytical Storyline

The visual assets support the following analytical narrative:

1. The dataset is concentrated around selected observation years rather than representing a complete annual panel.
2. ARC provides a normalized measure of yearly progress across unequal observation intervals.
3. Rural access improved faster than urban access across all regions on average.
4. Faster rural improvement does not mean that the rural access gap has already closed.
5. Regional population size does not directly determine the rate of progress.
6. Some highly populated regions combine meaningful ARC values with a large potential population impact.
7. Regional averages can hide substantial differences between countries.
8. Positive progress exists alongside cases of stagnation, declining access, and missing data.
9. Baseline access levels must be considered when interpreting ARC.
10. Sub-Saharan Africa shows meaningful progress, but the remaining access challenge remains large and unevenly distributed.

---

# Metric Definitions

## `ARC_n`

Annual Rate of Change in national access to at least basic drinking water.

## `ARC_r`

Annual Rate of Change in rural access to at least basic drinking water.

## `ARC_u`

Annual Rate of Change in urban access to at least basic drinking water.

## `ARC_diff`

Difference between rural and urban ARC:

`ARC_diff = ARC_r - ARC_u`

All ARC values are interpreted in **percentage points per year**.

---

# How to Use This Folder

For the clearest review experience:

1. Start with the charts in the [main visuals folder](./main_visuals/).
2. Review the regional ARC tables to inspect the country-level observations behind the averages.
3. Use the analytical report in the `reports/` folder for the complete interpretation of Part 2.
4. Use the Google Sheets workbook to inspect the formulas, transformations, and source calculations.

---

# Portfolio Value

This assets section demonstrates the ability to:

* validate temporal data structure
* calculate Annual Rates of Change
* compare national, rural, and urban progress
* engineer rural–urban difference metrics
* enrich data with regional classifications
* aggregate country-level results by region
* combine population scale with progress metrics
* identify positive, negative, zero, and missing outcomes
* trace aggregated visual findings back to detailed records
* communicate analytical results through visual storytelling

---

# Notes

* The assets were exported from the Google Sheets workbook used for data transformation, aggregation, and visual analysis.
* The spreadsheet remains the main analytical workspace for formulas and calculations.
* The main visuals communicate the project’s principal findings.
* The regional tables provide supporting country-level evidence.
* Regional ARC values are based on country-level averages unless otherwise specified.
* Regional averages are not automatically population-weighted.
* Missing values are retained as `Null` to preserve transparency.
* ARC measures the speed of progress, not the final level of water access.
* Population size and baseline access should be considered before drawing conclusions from ARC alone.
