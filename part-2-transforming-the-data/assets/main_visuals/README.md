# Main Visuals — Part 2: Transforming the Data

This folder contains the primary visual outputs from Part 2 of the **Access to Drinking Water** project.

The analysis moves beyond a static view of water access and focuses on progress over time using the **Annual Rate of Change (ARC)**. These visuals examine year representation, rural-versus-urban progress, regional differences, and the relationship between population scale and improvement in access to at least basic drinking water.

---

## Visuals Included

### 01 — Year Distribution Histogram

![Year Distribution Histogram](./01_year_distribution_histogram.png)

This histogram examines how observation years are represented in the dataset.

Most records are concentrated in **2015** and **2020**, while only a small number of observations appear in the intermediate years.

**Main insight:**

The dataset is not a continuous annual time series. It is primarily structured around two major observation periods, which makes the calculation of `y_diff` essential for measuring the actual time interval between records.

Using the year difference ensures that Annual Rates of Change are calculated fairly across countries with different observation periods.

---

### 02 — Average Rural–Urban ARC Difference by Region

![Average ARC Difference by Region](./02_average_arc_diff_by_region.png)

This visual compares the average difference between rural and urban Annual Rates of Change across regions.

The metric is calculated as:

`ARC_diff = ARC_r - ARC_u`

A positive value indicates that rural access improved faster than urban access.

**Main insight:**

All regional average differences are positive, showing that rural access improved faster than urban access on average across every region.

The strongest rural catch-up patterns appear in:

- Middle East & North Africa
- Latin America & Caribbean

However, a positive ARC difference reflects the **speed of progress**, not the final level of access. Rural populations may still have lower access despite improving faster.

---

### 03 — Average Rural and Urban ARC by Region

![Average Rural and Urban ARC by Region](./03_rural_vs_urban_arc_by_region.png)

This grouped column chart compares average rural and urban ARC values directly for each region.

It reveals the individual rural and urban rates behind the regional `ARC_diff` values.

**Main insight:**

Average rural ARC is higher than average urban ARC in every region.

Middle East & North Africa records the highest average rural ARC, while Latin America & Caribbean also shows a strong rural catch-up pattern.

Sub-Saharan Africa records meaningful improvement in both rural and urban access, although its remaining access deficit may still be substantial because of lower baseline access levels.

---

### 04 — Regional Progress in Basic Water Access

![Regional Progress in Basic Water Access](./04_regional_progress_arc_population.png)

This visual combines:

- regional population size
- average national ARC
- average rural ARC

The purpose is to compare the speed of progress with the population scale represented by each region.

**Main insight:**

Regional population size does not show a direct relationship with the speed of improvement in basic water access.

South Asia combines a very large population with strong national and rural progress. Sub-Saharan Africa also shows relatively high ARC values across a large population, while Middle East & North Africa records the strongest rural improvement despite its smaller population.

The chart highlights the importance of considering both:

- the rate of progress
- the number of people potentially affected

---

## Analytical Storyline

Together, the four visuals support the following analytical narrative:

1. The dataset is concentrated around selected observation years rather than being a complete annual time series.
2. Annual Rate of Change provides a normalized measure of progress across different observation intervals.
3. Rural access improved faster than urban access across all regions on average.
4. Faster rural progress does not necessarily mean that the rural access gap has already closed.
5. Population size alone does not determine the speed of improvement.
6. Regional ARC values must be interpreted alongside baseline access, population scale, and country-level variation.

---

## Metric Definitions

### National Annual Rate of Change

`ARC_n` measures the average yearly change in national access to at least basic drinking water.

### Rural Annual Rate of Change

`ARC_r` measures the average yearly change in rural access to at least basic drinking water.

### Urban Annual Rate of Change

`ARC_u` measures the average yearly change in urban access to at least basic drinking water.

### Rural–Urban ARC Difference

`ARC_diff` compares rural and urban progress:

`ARC_diff = ARC_r - ARC_u`

Interpretation:

- `ARC_diff > 0`: rural access improved faster
- `ARC_diff < 0`: urban access improved faster
- `ARC_diff ≈ 0`: rural and urban progress were similar

All ARC values are interpreted in **percentage points per year**.

---

## Notes

- These visuals were exported from the Google Sheets workbook used for data transformation, ARC calculation, regional aggregation, and visual analysis.
- The spreadsheet remains the main analytical workspace where calculations and summaries were performed.
- The visuals in this folder communicate the primary findings from Part 2.
- Detailed country-level regional tables are stored separately in the `regional_arc_tables/` folder.
- Regional ARC values are based on average country-level observations and should not automatically be interpreted as population-weighted measures.
