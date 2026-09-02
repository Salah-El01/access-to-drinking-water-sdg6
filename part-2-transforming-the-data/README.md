# Access to Drinking Water - Part 2: Transforming the Data

## Progress Analysis Using Annual Rates of Change

This folder contains **Part 2: Transforming the Data** of the **Access to Drinking Water - SDG 6 Data Analysis Project**.

Part 1 examined drinking-water access as a descriptive snapshot. Part 2 introduces a time-based analytical framework by measuring changes in access to at least basic drinking-water services.

The central question is:

> How did national, rural, and urban access to at least basic drinking water change across countries and regions?

The analysis was completed in Google Sheets using paired country observations, engineered variables, Annual Rates of Change, progress classifications, regional aggregations, and visual analysis.

---

## Project Navigation

| Resource                                                                                                                       | Description                                                           |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| [Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing) | Dynamic analytical workspace containing formulas, tables, and charts  |
| [Part 2 Analytical Report](./reports/analytical_report/Part2_Analytical_Report.md)                                             | Complete methodology, verified findings, limitations, and conclusions |
| [Data Documentation](./data/README.md)                                                                                         | Dataset scope, transformation process, and reproducibility notes      |
| [Data Dictionary](./data/data_dictionary.md)                                                                                   | Definitions, units, formulas, and interpretation of variables         |
| [Visual Assets](./assets/README.md)                                                                                            | Index of the main charts and regional table screenshots               |
| [Reports Documentation](./reports/README.md)                                                                                   | Guide to the report and supporting spreadsheet exports                |
| [Sheet Exports](./reports/sheet_exports/README.md)                                                                             | Documentation of the two exported Google Sheets tabs                  |
| [Part 1: Understanding the Data](../part-1-understanding-the-data/README.md)                                                   | Previous descriptive stage of the project                             |

---

## 1. Project Objective

Part 2 transforms country-level observations into a structured progress-monitoring framework.

It addresses five analytical questions:

1. How are observation years distributed?
2. How can access changes be compared when observation intervals differ?
3. How quickly is national, rural, and urban access changing?
4. Is rural progress faster or slower than urban progress?
5. How do these patterns differ across regions?

The primary metric is the **Annual Rate of Change**, abbreviated as **ARC**.

---

## 2. Data Source

The project uses country- and area-level estimates from the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

* [WHO/UNICEF JMP data downloads](https://washdata.org/data/downloads)
* [Open the project Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook contains:

* the original drinking-water variables;
* the transformed analytical dataset;
* a regional lookup table;
* derived ARC fields;
* approximate full-access classifications;
* rural-urban comparisons;
* Summary calculations;
* regional aggregations;
* charts.

---

## 3. Verified Dataset Scope

Although the source worksheet is titled:

```text
Estimates of the use of water (2000-2020)
```

the observations retained in the completed Part 2 analysis cover **2015 to 2020**.

| Measure                                          | Verified result |
| ------------------------------------------------ | --------------: |
| Countries or areas                               |             231 |
| Total observations                               |             462 |
| Observations per country or area                 |               2 |
| Earliest analytical year                         |            2015 |
| Latest analytical year                           |            2020 |
| Countries or areas with a 2015 baseline          |             231 |
| Countries or areas with a 2020 later observation |             213 |

The source-row grain is:

> One country or area observed in one specific year.

The ARC grain is:

> One comparison between the earlier and later observations for the same country or area.

The dataset is therefore a **paired-observation dataset**, not a complete annual time series.

---

## 4. Observation-Year Distribution

|      Year | Observations | Share of all records |
| --------: | -----------: | -------------------: |
|      2015 |          231 |               50.00% |
|      2016 |            3 |                0.65% |
|      2017 |            9 |                1.95% |
|      2018 |            2 |                0.43% |
|      2019 |            4 |                0.87% |
|      2020 |          213 |               46.10% |
| **Total** |      **462** |          **100.00%** |

The 2015 and 2020 observations represent:

```text
(231 + 213) / 462 = 96.10%
```

Approximately 92.2% of countries or areas use a five-year comparison from 2015 to 2020.

This concentration confirms that the dataset should not be interpreted as a continuous annual trend.

---

## 5. Main Source Variables

| Variable      | Description                                               | Unit                |
| ------------- | --------------------------------------------------------- | ------------------- |
| `name`        | Country or area name                                      | Not applicable      |
| `year`        | Observation year                                          | Calendar year       |
| `pop_n`       | National population estimate                              | Thousands of people |
| `pop_u`       | Urban population share                                    | Percentage          |
| `wat_bas_n`   | National access to at least basic drinking-water services | Percentage          |
| `wat_bas_r`   | Rural access to at least basic drinking-water services    | Percentage          |
| `wat_bas_u`   | Urban access to at least basic drinking-water services    | Percentage          |
| `wat_lim_*`   | Access to limited drinking-water services                 | Percentage          |
| `wat_unimp_*` | Reliance on unimproved drinking-water sources             | Percentage          |
| `wat_sur_*`   | Reliance on surface water                                 | Percentage          |

The principal Part 2 calculations use the national, rural, and urban at-least-basic access variables.

Complete variable documentation is available in the [Data Dictionary](./data/data_dictionary.md).

---

## 6. Transformation Workflow

```text
Source observations
    |
    v
Sort by country and year
    |
    v
Match each country's two observations
    |
    v
Calculate the observation interval
    |
    v
Calculate national, rural, and urban ARC
    |
    v
Handle missing and non-calculable values
    |
    v
Create rounded access and full-access flags
    |
    v
Calculate the paired rural-urban ARC difference
    |
    v
Assign regional classifications
    |
    v
Build Summary calculations and regional aggregations
    |
    v
Create charts and analytical documentation
```

This process converts the original observations into an analysis-ready progress-monitoring structure.

---

## 7. Key Derived Variables

### `y_diff`

`y_diff` measures the number of years between paired observations.

```text
y_diff = later year - earlier year
```

| Statistic             |     Result |
| --------------------- | ---------: |
| Average               | 4.80 years |
| Median                |    5 years |
| Minimum               |     1 year |
| Maximum               |    5 years |
| Zero-year comparisons |          0 |

`y_diff` is required because the later observation does not always occur in 2020.

---

### Annual Rate of Change

ARC measures the average yearly change in access to at least basic drinking-water services.

```text
ARC =
(later access percentage - earlier access percentage)
/
(later year - earlier year)
```

ARC is expressed in:

```text
percentage points per year
```

The three area-based measures are:

| Variable | Meaning                                              |
| -------- | ---------------------------------------------------- |
| `ARC_n`  | Annual Rate of Change in national basic-water access |
| `ARC_r`  | Annual Rate of Change in rural basic-water access    |
| `ARC_u`  | Annual Rate of Change in urban basic-water access    |

### ARC interpretation

| Result            | Interpretation                         |
| ----------------- | -------------------------------------- |
| Positive          | Access increased                       |
| Negative          | Access decreased                       |
| Zero              | No measured change                     |
| Missing or `Null` | The calculation could not be completed |

A zero ARC can describe either stagnation below full access or continued full access. These cases are separated using the full-access flags.

---

### Approximate full-access flags

The transformed dataset includes:

* `ARC_n_full`;
* `ARC_r_full`;
* `ARC_u_full`.

The source access values are rounded to zero decimal places. A country is classified as having full access in an area when both paired rounded values equal 100.

```text
If earlier rounded access = 100
and later rounded access = 100:
    classify as "full access"
```

This is an **approximate full-access classification**. An original value slightly below 100 can qualify if it rounds to 100.

---

### `ARC_diff`

`ARC_diff` compares rural and urban ARC for the same country.

```text
ARC_diff = ARC_r - ARC_u
```

| Result         | Interpretation                                |
| -------------- | --------------------------------------------- |
| `ARC_diff > 0` | Rural ARC is numerically higher               |
| `ARC_diff < 0` | Urban ARC is numerically higher               |
| `ARC_diff = 0` | Rural and urban ARC are equal                 |
| Missing        | Rural ARC, urban ARC, or both are unavailable |

A positive difference usually represents faster rural improvement. However, if both ARC values are negative, it can instead mean that rural access declined more slowly.

---

### `region`

The `region` variable assigns each country or area to one of seven regional groups:

* East Asia & Pacific;
* Europe & Central Asia;
* Latin America & Caribbean;
* Middle East & North Africa;
* North America;
* South Asia;
* Sub-Saharan Africa.

This field supports regional aggregation and comparison.

---

## 8. Missing-Value Rules

Blank cells, `Null` values, and numeric zeroes must remain distinct.

| Value                    | Meaning                                                       |
| ------------------------ | ------------------------------------------------------------- |
| Blank                    | No paired calculation is expected on that row                 |
| `Null` or missing result | A calculation was expected, but required data was unavailable |
| `0`                      | The calculation was completed and produced no measured change |

Missing access estimates are not converted to zero.

### ARC completeness

| Measure  | Valid ARC values | Missing ARC values |
| -------- | ---------------: | -----------------: |
| National |              229 |                  2 |
| Rural    |              167 |                 64 |
| Urban    |              181 |                 50 |

Rural and urban estimates are less complete than national estimates. This affects both the overall and regional comparisons.

---

## 9. ARC Summary Statistics

| Statistic            | National ARC | Rural ARC | Urban ARC |
| -------------------- | -----------: | --------: | --------: |
| Valid observations   |          229 |       167 |       181 |
| Missing observations |            2 |        64 |        50 |
| Average              |        0.277 |     0.484 |     0.155 |
| Median               |        0.079 |     0.290 |     0.030 |
| Minimum              |       -1.022 |    -1.227 |    -1.620 |
| Maximum              |        2.750 |     2.668 |     2.668 |

Rural ARC has the highest average and median.

This shows that rural access generally changed more rapidly among valid observations. It does not mean that rural access is higher than urban access.

The current Summary sheet displays the averages, minima, and maxima. The verified medians should still be added to the Summary calculation block.

---

## 10. Access-by-Area Classification

The ARC results are classified into five mutually exclusive categories.

| Classification                 | National |   Rural |   Urban |
| ------------------------------ | -------: | ------: | ------: |
| Missing ARC                    |        2 |      64 |      50 |
| Full access                    |       62 |      29 |      55 |
| Zero ARC below full access     |       16 |       5 |       7 |
| Negative ARC below full access |       16 |      17 |      26 |
| Positive ARC below full access |      135 |     116 |      93 |
| **Total**                      |  **231** | **231** | **231** |

Positive ARC below full access is the largest category in every population area.

National full access has the highest count, followed by urban full access. Rural full access is substantially less common.

Each column sums to 231, confirming that the classifications account for every country or area.

---

## 11. Country-Level Rural-Urban Comparison

| Metric                         | Result |
| ------------------------------ | -----: |
| Valid paired `ARC_diff` values |    165 |
| Missing paired values          |     66 |
| Positive differences           |    112 |
| Negative differences           |     23 |
| Zero differences               |     30 |
| Average                        |  0.321 |
| Median                         |  0.212 |
| Minimum                        | -2.489 |
| Maximum                        |  2.329 |

Among the 165 valid paired comparisons:

* 67.9% are positive;
* 13.9% are negative;
* 18.2% are zero.

Rural ARC is therefore numerically higher than urban ARC in most valid country-level comparisons.

This pattern is consistent with rural catch-up, but it does not prove that rural access has reached the urban level.

---

## 12. Regional Summary

| Region                     | Countries or areas | Population (millions) | Average `ARC_n` | Average `ARC_r` | Average `ARC_u` |
| -------------------------- | -----------------: | --------------------: | --------------: | --------------: | --------------: |
| East Asia & Pacific        |                 40 |               2,247.5 |           0.278 |           0.508 |           0.233 |
| Europe & Central Asia      |                 64 |               1,017.5 |           0.112 |           0.224 |           0.047 |
| Latin America & Caribbean  |                 48 |                 642.5 |           0.144 |           0.680 |           0.072 |
| Middle East & North Africa |                 10 |                 311.1 |           0.346 |           0.737 |           0.124 |
| North America              |                  5 |                 368.9 |           0.017 |           0.142 |           0.002 |
| South Asia                 |                 11 |               2,082.3 |           0.480 |           0.559 |           0.266 |
| Sub-Saharan Africa         |                 53 |               1,124.0 |           0.558 |           0.604 |           0.270 |
| **Total or overall value** |            **231** |           **7,793.8** |       **0.277** |       **0.484** |       **0.155** |

### Regional highlights

* East Asia & Pacific has the largest regional population total.
* Europe & Central Asia contains the largest number of countries or areas.
* Middle East & North Africa has the highest average rural ARC.
* Sub-Saharan Africa has the highest average national and urban ARC.
* South Asia combines the second-largest population with comparatively strong progress.
* North America has the lowest average ARC in all three population areas.

The ARC values are **unweighted country averages**. Each valid country contributes equally, regardless of population size.

The population total does not represent the number of people who gained access.

---

## 13. Paired Regional ARC Difference

| Rank | Region                     | Average paired `ARC_diff` |
| ---: | -------------------------- | ------------------------: |
|    1 | Middle East & North Africa |                    0.6130 |
|    2 | Latin America & Caribbean  |                    0.5928 |
|    3 | Sub-Saharan Africa         |                    0.3338 |
|    4 | South Asia                 |                    0.2937 |
|    5 | East Asia & Pacific        |                    0.2674 |
|    6 | Europe & Central Asia      |                    0.1736 |
|    7 | North America              |                    0.1396 |

All seven regional paired averages are positive.

These results are based only on countries with valid rural and urban ARC values. The chart does not display the number of valid paired countries in each region.

A positive regional average does not mean that every country in that region has a positive `ARC_diff`.

---

## 14. Main Visuals

Detailed chart documentation is available in:

[Main Visuals README](./assets/main_visuals/README.md)

---

### Visual 1: Observation Frequency by Year

![Observation frequency by year](./assets/main_visuals/01_year_distribution_histogram.png)

The chart shows that observations are strongly concentrated in 2015 and 2020.

The image filename and current chart title use the term `histogram`, but the visual is more accurately described as a categorical frequency column chart.

The years should be sorted chronologically when the chart is revised.

**Main insight:** The data represents paired country observations rather than a continuous annual time series.

---

### Visual 2: Average Paired Rural-Urban ARC Difference by Region

![Average rural-urban ARC difference by region](./assets/main_visuals/02_average_arc_diff_by_region.png)

This chart averages valid country-level `ARC_diff` values within each region.

**Main insight:** Every regional average is positive, with the largest paired differences in Middle East & North Africa and Latin America & Caribbean.

The results are unweighted and hide country-level variation.

---

### Visual 3: Average Rural and Urban ARC by Region

![Average rural and urban ARC by region](./assets/main_visuals/03_rural_vs_urban_arc_by_region.png)

This chart compares independently calculated rural and urban regional averages.

**Main insight:** Rural ARC is higher than urban ARC in every region.

The rural and urban series can contain different country samples because their missing-value patterns differ.

Therefore:

```text
regional average ARC_r - regional average ARC_u
```

is not necessarily equal to:

```text
average of paired country-level ARC_diff
```

---

### Visual 4: Regional Population and ARC

![Regional population and ARC](./assets/main_visuals/04_regional_progress_arc_population.png)

This dual-axis chart combines:

* regional population totals;
* average national ARC;
* average rural ARC;
* regional categories.

**Main insight:** Population size and ARC do not follow a simple descriptive relationship.

The chart does not calculate population-weighted ARC, beneficiaries, or causality.

---

## 15. Missing Required Visual

The completed Summary sheet does not currently contain the required country-level `ARC_diff` histogram.

The existing regional chart summarises seven regional averages. It cannot show:

* the distribution of the 165 valid country-level differences;
* concentration around zero;
* the balance of positive and negative country values;
* the distribution's shape;
* country-level extremes.

A separate country-level histogram should therefore be added.

---

## 16. Regional ARC Tables

Supporting regional screenshots are documented in:

[Regional ARC Tables README](./assets/regional_arc_tables/README.md)

The screenshots contain visible country-level records with:

* country or area name;
* region;
* observation year;
* population;
* national ARC;
* rural ARC;
* urban ARC.

For larger regions, the screenshots display only visible excerpts rather than every country. They should be treated as supporting visual evidence, not as complete machine-readable regional tables.

---

## 17. Repository Structure

```text
part-2-transforming-the-data/
|
|-- assets/
|   |-- main_visuals/
|   |   |-- 01_year_distribution_histogram.png
|   |   |-- 02_average_arc_diff_by_region.png
|   |   |-- 03_rural_vs_urban_arc_by_region.png
|   |   |-- 04_regional_progress_arc_population.png
|   |   `-- README.md
|   |
|   |-- regional_arc_tables/
|   |   |-- 01_east_asia_pacific_arc_table.png
|   |   |-- 02_europe_central_asia_arc_table.png
|   |   |-- 03_latin_america_caribbean_arc_table.png
|   |   |-- 04_middle_east_north_africa_arc_table.png
|   |   |-- 05_north_america_arc_table.png
|   |   |-- 06_south_asia_arc_table.png
|   |   |-- 07_sub_saharan_africa_arc_table.png
|   |   `-- README.md
|   |
|   `-- README.md
|
|-- data/
|   |-- README.md
|   `-- data_dictionary.md
|
|-- reports/
|   |-- analytical_report/
|   |   `-- Part2_Analytical_Report.md
|   |
|   |-- sheet_exports/
|   |   |-- Estimates of the use of water (2000-2020).pdf
|   |   |-- Summary.pdf
|   |   `-- README.md
|   |
|   `-- README.md
|
`-- README.md
```

---

## 18. Folder Guide

### [`assets/`](./assets/)

Contains:

* the four main chart images;
* seven regional ARC table screenshots;
* detailed visual documentation;
* interpretation and design limitations.

### [`data/`](./data/)

Contains:

* dataset and transformation documentation;
* the data dictionary;
* variable definitions;
* units and formula logic;
* missing-value conventions;
* reproducibility notes.

### [`reports/`](./reports/)

Contains:

* the complete analytical report;
* PDF exports of the transformed and Summary sheets;
* reporting and export documentation.

---

## 19. Recommended Review Order

For the clearest understanding of Part 2:

1. Read this README for the project overview.
2. Read the [Part 2 Analytical Report](./reports/analytical_report/Part2_Analytical_Report.md).
3. Review the [Summary PDF](./reports/sheet_exports/Summary.pdf).
4. Review the [Transformed Dataset PDF](./reports/sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf).
5. Consult the [Data Dictionary](./data/data_dictionary.md).
6. Review the [Main Visual Documentation](./assets/main_visuals/README.md).
7. Review the [Regional ARC Table Documentation](./assets/regional_arc_tables/README.md).
8. Open the Google Sheets workbook when formula-level inspection is required.

---

## 20. Reproducibility

The Google Sheets workbook is the principal dynamic analytical workspace:

[Open the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The repository contains:

* Markdown documentation;
* PNG charts;
* PNG regional table screenshots;
* PDF worksheet exports.

It does not currently contain machine-readable CSV or XLSX exports of the transformed data.

The PDFs display calculated results but do not expose:

* formulas;
* cell references;
* lookup ranges;
* chart source ranges;
* filters;
* dynamic recalculation;
* revision history.

Reproducibility would be improved by adding:

* a CSV or XLSX export of the transformed dataset;
* a machine-readable Summary table;
* the regional aggregation table;
* the 165 valid country-level `ARC_diff` values;
* a formula-reference document;
* a reproducible Python or R workflow.

---

## 21. Methodological Limitations

This analysis is descriptive and exploratory.

Its principal limitations are:

* the analytical observations cover only 2015 to 2020;
* the dataset contains paired observations rather than a complete annual panel;
* rural and urban variables have substantial missingness;
* full access is identified using values rounded to zero decimal places;
* independently calculated rural and urban averages can use different samples;
* regional ARC values are unweighted country averages;
* population totals do not represent beneficiaries;
* ARC measures change rather than final access;
* high ARC can partly reflect a low starting level;
* low ARC can partly reflect an access ceiling;
* regional averages conceal country-level variation;
* the country-level `ARC_diff` histogram is missing;
* ARC medians are verified but are not yet displayed in the Summary sheet;
* the repository does not currently include machine-readable analytical data;
* the analysis identifies patterns but does not establish causality.

---

## 22. Recommended Improvements

The principal next improvements are:

1. add the verified ARC medians to the Summary sheet;
2. create the country-level `ARC_diff` histogram;
3. sort the year-frequency chart chronologically;
4. add valid sample sizes to the regional charts;
5. add machine-readable data exports;
6. calculate population-weighted regional ARC as a separate measure;
7. compare baseline access with final access;
8. identify the strongest positive and negative country-level changes;
9. reproduce the workflow in Python or R;
10. build an interactive dashboard or geographic map;
11. incorporate uncertainty measures if they become available.

Population-weighted and unweighted measures should remain separate because they answer different questions.

---

## 23. Skills Demonstrated

Part 2 demonstrates:

* spreadsheet-based data transformation;
* paired-observation logic;
* sorting and validation;
* feature engineering;
* time-interval calculation;
* Annual Rate of Change methodology;
* controlled error handling;
* missing-value treatment;
* approximate full-access classification;
* rural-urban comparison;
* lookup-based regional enrichment;
* aggregation and validation;
* visual analysis;
* data storytelling;
* analytical documentation;
* critical assessment of limitations;
* portfolio reporting.

---

## 24. Final Conclusions

Part 2 transforms paired drinking-water observations into a structured progress-monitoring framework.

The analysis shows that improvement below full access is common and that rural ARC is generally higher than urban ARC. Among the 165 valid paired rural-urban comparisons, 112 have a positive `ARC_diff`, and all seven regional paired averages are positive.

These findings are consistent with rural catch-up. However, faster rural change does not mean that rural access has reached the urban level or that rural-urban inequality has disappeared.

The central conclusion is:

> ARC measures the speed and direction of change, while access levels, population context, missingness, and country-level variation determine the broader development significance.

Part 2 therefore extends the project from a descriptive snapshot toward a more rigorous examination of progress over time.
