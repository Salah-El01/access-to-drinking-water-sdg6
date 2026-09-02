# Visual Assets — Part 2: Transforming the Data

This folder contains the visual outputs supporting Part 2 of the **Access to Drinking Water** project.

Part 2 transforms paired country observations into a progress-monitoring framework using the **Annual Rate of Change (ARC)**.

The assets are divided into two categories:

1. **Main visuals** — four charts communicating the principal analytical findings.
2. **Regional ARC tables** — seven regional screenshots providing country-level examples behind the aggregated results.

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

The four principal charts are available in:

[Open the Main Visuals folder](./main_visuals/)

Detailed methodology, exact values and limitations are documented in:

[Main Visuals README](./main_visuals/README.md)

---

## Visual Inventory

| Number | Visual                                             | Principal purpose                                       |
| -----: | -------------------------------------------------- | ------------------------------------------------------- |
|     01 | Distribution of Observations by Year               | Examine the temporal structure of the dataset           |
|     02 | Average Rural–Urban ARC Difference by Region       | Compare paired rural and urban ARC differences          |
|     03 | Average Rural and Urban ARC by Region              | Compare independently aggregated rural and urban ARC    |
|     04 | Regional Population and Average National/Rural ARC | Compare regional population context with progress rates |

---

## 01 — Distribution of Observations by Year

![Distribution of Observations by Year](./main_visuals/01_year_distribution_histogram.png)

This chart examines how the 462 observations are distributed across the analysed years.

The dataset contains:

* 231 observations in 2015;
* 213 observations in 2020;
* 18 observations distributed between 2016 and 2019.

Approximately **96.1%** of all observations occur in 2015 or 2020.

### Main finding

The dataset is a paired-observation dataset rather than a complete annual time series.

The `y_diff` variable is therefore required to measure the actual interval between observations before calculating ARC.

Although the file name uses the word `histogram`, the visual technically functions as a frequency column chart because each year is treated as a separate category.

---

## 02 — Average Rural–Urban ARC Difference by Region

![Average Rural–Urban ARC Difference by Region](./main_visuals/02_average_arc_diff_by_region.png)

This chart compares the average country-level paired difference between rural and urban ARC.

```text
ARC_diff = ARC_r - ARC_u
```

The regional calculation is:

```text
Regional average ARC_diff =
AVERAGE(valid country-level ARC_r - ARC_u)
```

### Main finding

All seven regional averages are positive.

The highest average paired differences occur in:

* Middle East & North Africa;
* Latin America & Caribbean.

A positive difference means that rural ARC is numerically higher than urban ARC. It does not mean that rural access is higher or that the rural–urban access gap has disappeared.

A positive value may also represent a slower rural decline if both rural and urban ARC are negative.

---

## 03 — Average Rural and Urban ARC by Region

![Average Rural and Urban ARC by Region](./main_visuals/03_rural_vs_urban_arc_by_region.png)

This chart compares independently calculated regional rural and urban ARC averages.

### Main finding

Average rural ARC is higher than average urban ARC in every region.

However, rural and urban ARC have different missing-value patterns:

| Measure   | Valid | Missing |
| --------- | ----: | ------: |
| Rural ARC |   167 |      64 |
| Urban ARC |   181 |      50 |

The two regional series may therefore contain different country samples.

This chart must not be treated as a direct decomposition of the paired `ARC_diff` chart.

---

## 04 — Regional Population and Average National/Rural ARC

![Regional Population and Average National/Rural ARC](./main_visuals/04_regional_progress_arc_population.png)

This dual-axis chart combines:

* region;
* regional population in millions;
* average national ARC;
* average rural ARC.

### Main finding

No clear descriptive relationship between regional population size and ARC is visible.

The chart provides population context but does not calculate:

* population-weighted ARC;
* the number of people gaining access;
* the remaining population without access;
* a statistical or causal relationship between population and progress.

The population columns and ARC columns use different axes and units. Their physical heights must not be compared directly.

---

# Regional ARC Tables

The regional table screenshots are available in:

[Open the Regional ARC Tables folder](./regional_arc_tables/)

Detailed country examples, interpretation notes and screenshot limitations are documented in:

[Regional ARC Tables README](./regional_arc_tables/README.md)

---

## Regional Table Inventory

| Number | Region                     | Countries or areas in the full Summary | Image                                                                         |
| -----: | -------------------------- | -------------------------------------: | ----------------------------------------------------------------------------- |
|     01 | East Asia & Pacific        |                                     40 | [View table](./regional_arc_tables/01_east_asia_pacific_arc_table.png)        |
|     02 | Europe & Central Asia      |                                     64 | [View table](./regional_arc_tables/02_europe_central_asia_arc_table.png)      |
|     03 | Latin America & Caribbean  |                                     48 | [View table](./regional_arc_tables/03_latin_america_caribbean_arc_table.png)  |
|     04 | Middle East & North Africa |                                     10 | [View table](./regional_arc_tables/04_middle_east_north_africa_arc_table.png) |
|     05 | North America              |                                      5 | [View table](./regional_arc_tables/05_north_america_arc_table.png)            |
|     06 | South Asia                 |                                     11 | [View table](./regional_arc_tables/06_south_asia_arc_table.png)               |
|     07 | Sub-Saharan Africa         |                                     53 | [View table](./regional_arc_tables/07_sub_saharan_africa_arc_table.png)       |

---

## Variables Displayed in the Regional Tables

| Variable               | Description                                 |
| ---------------------- | ------------------------------------------- |
| `name`                 | Country or area name                        |
| `region`               | Regional classification used in the project |
| `year`                 | Observation year                            |
| `pop_n (in thousands)` | National population estimate in thousands   |
| `pop_n (Millions)`     | National population converted into millions |
| `ARC_n`                | National Annual Rate of Change              |
| `ARC_r`                | Rural Annual Rate of Change                 |
| `ARC_u`                | Urban Annual Rate of Change                 |

---

## Regional Table Structure

Each country or area is generally represented by two rows.

The earlier observation row usually contains the calculated ARC values.

The later observation row usually contains:

* the later year;
* population in thousands;
* population converted into millions.

Both rows belonging to the same country should be interpreted together.

---

## Screenshot-Coverage Limitation

The regional PNG files are screenshots of Google Sheets tables.

Some larger regional screenshots show only the visible upper section of the complete table. They do not necessarily contain every country or area included in the regional average.

The screenshots should therefore be used to:

* illustrate country-level calculations;
* examine selected positive, zero, negative and missing values;
* understand the two-row table structure;
* provide examples of variation within regions.

They should not be used alone to:

* reconstruct every regional average;
* identify all countries in a region;
* calculate complete regional distributions;
* perform reproducible statistical analysis.

Machine-readable regional CSV files would be required for full repository-based reproducibility.

---

# Relationship Between the Two Asset Groups

The two asset groups perform different roles.

| Main visuals                               | Regional table screenshots                         |
| ------------------------------------------ | -------------------------------------------------- |
| Communicate aggregated findings            | Show selected country-level calculations           |
| Compare years, areas and regions           | Illustrate within-region variation                 |
| Provide the principal analytical narrative | Provide supporting examples                        |
| Hide some country-level detail             | Reveal positive, zero, negative and missing values |
| Designed for rapid interpretation          | Designed for analytical traceability               |

The main charts and regional screenshots should be interpreted together with the Summary sheet and analytical report.

---

# Key Methodological Distinctions

## Paired `ARC_diff`

The regional `ARC_diff` chart uses valid paired country observations:

```text
AVERAGE(country-level ARC_r - ARC_u)
```

## Independent Rural and Urban Averages

The rural-versus-urban chart calculates the two series independently:

```text
AVERAGE(valid ARC_r)
```

```text
AVERAGE(valid ARC_u)
```

Because the valid samples may differ, the difference between these two regional averages is not necessarily equal to the average paired `ARC_diff`.

## Unweighted Regional Averages

Regional ARC values are simple country averages unless stated otherwise.

A small country and a highly populated country contribute equally to their regional ARC average.

The population chart supplies contextual scale but does not weight the ARC calculations.

---

# Metric Definitions

## `ARC_n`

Annual Rate of Change in national access to at least basic drinking water.

## `ARC_r`

Annual Rate of Change in rural access to at least basic drinking water.

## `ARC_u`

Annual Rate of Change in urban access to at least basic drinking water.

## `ARC_diff`

Difference between rural and urban ARC for the same country pair:

```text
ARC_diff = ARC_r - ARC_u
```

All ARC values are expressed in:

> Percentage points per year.

---

# Analytical Storyline

The assets collectively support the following interpretation:

1. The observations are concentrated in 2015 and 2020.
2. The dataset is not a complete annual panel.
3. Observation intervals range from one to five years.
4. ARC annualises access changes across unequal intervals.
5. Most valid paired rural–urban differences are positive.
6. Rural ARC is higher than urban ARC on average in every region.
7. Faster rural change does not mean that rural access has reached urban access.
8. Regional averages hide country-level variation.
9. Rural and urban averages may use different valid-country samples.
10. Regional ARC values are not population-weighted.
11. Population provides contextual scale but does not measure human impact.
12. Baseline and final access levels remain necessary for complete interpretation.

---

# Current Visual-Coverage Note

The folder currently contains four principal charts.

A country-level histogram of the 165 valid `ARC_diff` values is not currently included.

That visual would complement the regional average chart by showing:

* the shape of the country-level distribution;
* concentration around zero;
* positive and negative values;
* distribution spread;
* extreme country-level differences.

The regional average chart cannot provide this information.

---

# How to Use This Folder

For the clearest review sequence:

1. Open the [Main Visuals README](./main_visuals/README.md).
2. Review the four aggregated charts.
3. Open the [Regional ARC Tables README](./regional_arc_tables/README.md).
4. Inspect the country-level table screenshots.
5. Use the Summary sheet for complete calculations.
6. Use the analytical report for the full interpretation.
7. Use the Google Sheets workbook to inspect formulas and source values.

---

# Asset Provenance

* The charts were exported from the Google Sheets analytical workbook.
* The regional tables are screenshots of the Google Sheets calculation layout.
* The spreadsheet remains the primary calculation environment.
* Missing values displayed as `Null` were retained for transparency.
* The images are reporting outputs rather than machine-readable datasets.

---

# Portfolio Value

This assets section demonstrates:

* temporal-data validation;
* country-pair analysis;
* Annual Rate of Change calculation;
* rural–urban comparison;
* regional aggregation;
* missing-value awareness;
* population-unit conversion;
* distinction between paired and independent averages;
* visual communication;
* traceability from aggregated charts to country-level examples;
* documentation of analytical limitations.

---

# Navigation

* [Open Main Visuals](./main_visuals/)
* [Open Regional ARC Tables](./regional_arc_tables/)
* [Open Data Documentation](../data/)
* [Open Analytical Report](../reports/analytical_report/Part2_Analytical_Report.md)
* [Open Sheet Exports](../reports/sheet_exports/)
* [Back to Part 2](../README.md)
