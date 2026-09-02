# Main Visuals — Part 2: Transforming the Data

This folder contains the four principal visual outputs from Part 2 of the **Access to Drinking Water** project.

The visuals examine:

* the distribution of observation years;
* rural–urban differences in Annual Rate of Change;
* regional rural and urban progress;
* regional population alongside national and rural progress.

Annual Rate of Change is abbreviated as **ARC** and is expressed in:

> Percentage points per year.

---

## Visuals Included

| Number | Visual                                             | Main analytical purpose                              |
| -----: | -------------------------------------------------- | ---------------------------------------------------- |
|     01 | Distribution of Observations by Year               | Examine the temporal structure of the dataset        |
|     02 | Average Rural–Urban ARC Difference by Region       | Compare paired rural and urban ARC differences       |
|     03 | Average Rural and Urban ARC by Region              | Compare independently aggregated rural and urban ARC |
|     04 | Regional Population and Average National/Rural ARC | Compare regional population scale with ARC           |

---

## 01 — Distribution of Observations by Year

![Distribution of Observations by Year](./01_year_distribution_histogram.png)

### Purpose

This visual examines how the 462 country-year observations are distributed across the analysed years.

Although the file name uses the word `histogram`, the visual technically functions as a **frequency column chart** because each year is treated as a separate category.

### Verified results

|      Year | Observations |    Share |
| --------: | -----------: | -------: |
|      2015 |          231 |   50.00% |
|      2016 |            3 |    0.65% |
|      2017 |            9 |    1.95% |
|      2018 |            2 |    0.43% |
|      2019 |            4 |    0.87% |
|      2020 |          213 |   46.10% |
| **Total** |      **462** | **100%** |

The 2015 and 2020 observations account for approximately **96.1%** of all records.

All 231 countries and areas have a 2015 baseline observation.

Their later observations are distributed as follows:

* 213 countries or areas have a 2020 observation;
* 18 have a later observation between 2016 and 2019.

### Main finding

The dataset is not a complete annual time series. It is primarily a paired-observation dataset containing:

* one 2015 baseline;
* one later observation between 2016 and 2020.

This temporal structure explains why the `y_diff` variable is required.

```text
y_diff = later year - earlier year
```

The verified comparison intervals range from one to five years, with a median interval of five years.

### Interpretation limitation

The chart shows when observations were recorded. It does not show:

* access levels;
* the direction of access change;
* national, rural or urban ARC;
* regional performance.

The height of each column represents the number of observations, not progress in drinking-water access.

---

## 02 — Average Rural–Urban ARC Difference by Region

![Average Rural–Urban ARC Difference by Region](./02_average_arc_diff_by_region.png)

### Purpose

This visual compares the average country-level difference between rural and urban ARC within each region.

The country-level metric is:

```text
ARC_diff = ARC_r - ARC_u
```

The regional calculation is:

```text
Regional average ARC_diff =
AVERAGE(valid country-level ARC_r - ARC_u)
```

Only countries with both valid rural and urban ARC values contribute to this calculation.

### Interpretation

| Result         | Meaning                                        |
| -------------- | ---------------------------------------------- |
| `ARC_diff > 0` | Rural ARC is numerically higher than urban ARC |
| `ARC_diff < 0` | Urban ARC is numerically higher than rural ARC |
| `ARC_diff = 0` | Rural and urban ARC are equal                  |
| Missing        | Rural ARC, urban ARC or both are unavailable   |

A positive difference usually indicates faster rural improvement. However, if both rates are negative, it may indicate that rural access declined more slowly than urban access.

### Verified regional results

| Rank | Region                     | Average paired `ARC_diff` |
| ---: | -------------------------- | ------------------------: |
|    1 | Middle East & North Africa |                    0.6130 |
|    2 | Latin America & Caribbean  |                    0.5928 |
|    3 | Sub-Saharan Africa         |                    0.3338 |
|    4 | South Asia                 |                    0.2937 |
|    5 | East Asia & Pacific        |                    0.2674 |
|    6 | Europe & Central Asia      |                    0.1736 |
|    7 | North America              |                    0.1396 |

All seven regional averages are positive.

### Main finding

Rural ARC is numerically higher than urban ARC on average in every region among countries with valid paired measurements.

The largest average paired differences occur in:

* Middle East & North Africa;
* Latin America & Caribbean.

This pattern is consistent with rural catch-up, but it does not prove that rural access has reached urban access.

### Country-level context

Across the complete dataset:

| `ARC_diff` result | Countries or areas |
| ----------------- | -----------------: |
| Positive          |                112 |
| Negative          |                 23 |
| Zero              |                 30 |
| Missing           |                 66 |
| **Total**         |            **231** |

Therefore, positive regional averages do not mean that every country within each region has a positive difference.

### Methodological note

This visual represents:

```text
AVERAGE(country-level ARC_r - ARC_u)
```

It must not automatically be interpreted as:

```text
regional AVERAGE(ARC_r)
-
regional AVERAGE(ARC_u)
```

The second calculation can use different rural and urban country samples because of missing values.

---

## 03 — Average Rural and Urban ARC by Region

![Average Rural and Urban ARC by Region](./03_rural_vs_urban_arc_by_region.png)

### Purpose

This grouped column chart compares average rural and urban ARC across the seven regions.

The two series are calculated independently:

```text
Regional rural ARC = AVERAGE(valid ARC_r values)
```

```text
Regional urban ARC = AVERAGE(valid ARC_u values)
```

### Verified results

| Region                     | Average rural ARC | Average urban ARC |
| -------------------------- | ----------------: | ----------------: |
| South Asia                 |            0.5591 |            0.2655 |
| Europe & Central Asia      |            0.2244 |            0.0470 |
| Middle East & North Africa |            0.7370 |            0.1240 |
| East Asia & Pacific        |            0.5078 |            0.2330 |
| Sub-Saharan Africa         |            0.6042 |            0.2704 |
| Latin America & Caribbean  |            0.6803 |            0.0715 |
| North America              |            0.1423 |            0.0020 |

### Main findings

Average rural ARC is higher than average urban ARC in every region.

The highest rural ARC values are:

1. Middle East & North Africa — `0.7370`;
2. Latin America & Caribbean — `0.6803`;
3. Sub-Saharan Africa — `0.6042`.

The highest urban ARC values are:

1. Sub-Saharan Africa — `0.2704`;
2. South Asia — `0.2655`;
3. East Asia & Pacific — `0.2330`.

North America has the lowest rural and urban averages. Its urban ARC is not missing or exactly zero; the verified value is approximately `0.0020`.

### Interpretation

The chart is consistent with stronger rural progress across all regions.

However, higher rural ARC does not mean:

* rural access is higher than urban access;
* the rural–urban access gap has disappeared;
* every country has faster rural progress;
* universal rural access has been achieved.

ARC measures the direction and speed of change, not the final access level.

### Missing-data limitation

The overall valid observations are:

| Measure   | Valid | Missing |
| --------- | ----: | ------: |
| Rural ARC |   167 |      64 |
| Urban ARC |   181 |      50 |

Because rural and urban ARC have different missing-value patterns, the two regional columns may not represent exactly the same countries.

Consequently, this visual does not directly decompose the paired `ARC_diff` values shown in Visual 02.

### Aggregation limitation

The regional values are unweighted country averages.

A small country and a highly populated country contribute equally to their regional average.

The chart therefore represents the average country-level pattern rather than the progress experienced by the average resident.

---

## 04 — Regional Population and Average National/Rural ARC

![Regional Population and Average National/Rural ARC](./04_regional_progress_arc_population.png)

### Purpose

This dual-axis chart combines four dimensions:

* region;
* regional population;
* average national ARC;
* average rural ARC.

The chart provides population context alongside the average speed of progress.

### How to read the chart

| Series          | Measure              | Axis       |
| --------------- | -------------------- | ---------- |
| Black columns   | Regional population  | Left axis  |
| Brown columns   | Average national ARC | Right axis |
| Reddish columns | Average rural ARC    | Right axis |

Population is expressed in **millions of people**.

ARC is expressed in **percentage points per year**.

Because population and ARC use different axes and units, their physical column heights must not be compared directly.

### Verified results

| Region                     | Population, millions | National ARC | Rural ARC |
| -------------------------- | -------------------: | -----------: | --------: |
| East Asia & Pacific        |              2,247.5 |        0.278 |     0.508 |
| Europe & Central Asia      |              1,017.5 |        0.112 |     0.224 |
| Latin America & Caribbean  |                642.5 |        0.144 |     0.680 |
| Middle East & North Africa |                311.1 |        0.346 |     0.737 |
| North America              |                368.9 |        0.017 |     0.142 |
| South Asia                 |              2,082.3 |        0.480 |     0.559 |
| Sub-Saharan Africa         |              1,124.0 |        0.558 |     0.604 |

### Population findings

East Asia & Pacific has the largest represented population, followed by South Asia.

Together, these two regions represent approximately **55.6%** of the population contained in the regional Summary.

### ARC findings

* Sub-Saharan Africa has the highest national ARC.
* Middle East & North Africa has the highest rural ARC.
* Latin America & Caribbean has the second-highest rural ARC.
* North America has the lowest national and rural ARC.
* Rural ARC is higher than national ARC in all seven regions.

### Main interpretation

No clear descriptive relationship between regional population size and ARC is visible.

Examples include:

* East Asia & Pacific has the largest population but not the highest ARC;
* South Asia combines a large population with strong national and rural ARC;
* Middle East & North Africa has the smallest population but the highest rural ARC;
* Europe & Central Asia has a substantial population but comparatively low ARC;
* Sub-Saharan Africa has the highest national ARC without having the largest population.

Population represents the scale of the regional context, while ARC represents the average speed of change.

### Important limitations

The chart does not calculate:

* population-weighted ARC;
* the number of people who gained access;
* the remaining population without access;
* a statistical or causal relationship between population and progress.

The ARC columns are unweighted country averages. The population column provides context but is not used to weight those averages.

National and rural averages may also use different valid-country samples because national ARC has fewer missing observations than rural ARC.

---

## Analytical Storyline

Together, the four visuals support the following interpretation:

1. The dataset is concentrated in 2015 and 2020 rather than containing complete annual observations.
2. Countries have comparison intervals ranging from one to five years.
3. ARC standardises access changes into percentage points per year.
4. Most valid paired rural–urban differences are positive.
5. Rural ARC is higher than urban ARC on average in every region.
6. Faster rural change does not mean that rural access has reached urban access.
7. Regional averages hide country-level variation.
8. Population size does not show a clear descriptive relationship with ARC.
9. Regional ARC values are unweighted country averages.
10. ARC must be interpreted alongside baseline access, final access, missing data and population context.

---

## Metric Definitions

### National Annual Rate of Change

`ARC_n` measures the average yearly change in national access to at least basic drinking water.

```text
ARC_n =
(later national access - earlier national access)
/
year difference
```

### Rural Annual Rate of Change

`ARC_r` measures the average yearly change in rural access to at least basic drinking water.

```text
ARC_r =
(later rural access - earlier rural access)
/
year difference
```

### Urban Annual Rate of Change

`ARC_u` measures the average yearly change in urban access to at least basic drinking water.

```text
ARC_u =
(later urban access - earlier urban access)
/
year difference
```

### Rural–Urban ARC Difference

`ARC_diff` compares rural and urban ARC for the same country pair.

```text
ARC_diff = ARC_r - ARC_u
```

All ARC values are expressed in **percentage points per year**.

---

## Visual Coverage Note

This folder currently contains four principal charts.

A country-level histogram of the 165 valid `ARC_diff` values is not currently included.

Such a visual would complement Visual 02 by showing:

* the distribution of country-level differences;
* concentration around zero;
* positive and negative values;
* distribution spread;
* extreme country-level differences.

The regional average chart cannot provide this country-level distribution.

---

## Supporting Evidence

Detailed country-level regional tables are available in:

[Regional ARC Tables](../regional_arc_tables/)

Full variable definitions are available in:

[Data Dictionary](../../data/data_dictionary.md)

The complete analytical report is available in:

[Part 2 Analytical Report](../../reports/analytical_report/Part2_Analytical_Report.md)

PDF exports of the Google Sheets outputs are available in:

[Sheet Exports](../../reports/sheet_exports/)

---

## Notes

* The visuals were exported from the Google Sheets analytical workbook.
* The spreadsheet remains the primary calculation environment.
* Regional ARC values are unweighted country averages unless stated otherwise.
* Rural, urban and national averages may have different valid-country counts.
* Positive regional averages do not mean that every country has positive ARC.
* ARC measures change, not final access.
* Population provides scale but does not measure the number of beneficiaries.
* The analysis is descriptive and does not establish causality.

---

## Navigation

* [Back to Assets](../README.md)
* [Open Regional ARC Tables](../regional_arc_tables/)
* [Open Data Documentation](../../data/)
* [Open Reports](../../reports/)
* [Back to Part 2](../../README.md)
