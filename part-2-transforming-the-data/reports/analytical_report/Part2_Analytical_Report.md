# Part 2 Analytical Report — Transforming the Data

## Access to Drinking Water (SDG 6)

This report documents **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The objective of this part is to transform a multi-year drinking-water access dataset into a structured progress-monitoring analysis using **Annual Rate of Change (ARC)**.

While Part 1 focused on understanding the 2020 snapshot of drinking-water access, Part 2 focuses on change over time:

> Is access to at least basic drinking water improving, declining, or stagnating across countries, areas, and regions?

---

## 1. Executive Summary

Part 2 transforms the drinking-water dataset from a descriptive country-level table into an analytical framework for measuring progress.

The main transformation is the creation of **Annual Rate of Change** indicators for:

- national access;
- rural access;
- urban access.

The analysis shows that drinking-water access generally improved between the observed years, but progress differs strongly across population areas and regions.

### Main findings

1. The dataset is mainly concentrated around **2015** and **2020**, so it is not a complete annual time series.
2. The average year difference is approximately **4.8 years**, meaning most country pairs are separated by about five years.
3. Average rural ARC is higher than both national and urban ARC.
4. Rural access improved faster than urban access in every region on average.
5. Full-access countries need to be separated from zero-progress countries to avoid misleading interpretation.
6. Regional averages hide important country-level variation.
7. Sub-Saharan Africa and South Asia combine large population scale with meaningful ARC values.
8. Middle East & North Africa and Latin America & Caribbean show the strongest rural catch-up patterns.
9. ARC measures speed of progress, not final access level.
10. Population size alone does not explain progress patterns.

---

## 2. Project Context

Access to safe and reliable drinking water is a core development issue connected to **Sustainable Development Goal 6**.

This analysis focuses on access to **at least basic drinking-water services**. The project uses country-level estimates to evaluate how access changed over time across national, rural, urban, and regional dimensions.

The goal is not only to describe current access levels, but to measure whether countries and regions are moving toward better access.

---

## 3. Data Source and Analytical Workspace

The analysis was performed in Google Sheets.

Working spreadsheet:

[View the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook contains:

- source data;
- transformed dataset;
- regional lookup data;
- calculated ARC fields;
- full-access flags;
- summary tables;
- regional aggregations;
- charts and exported outputs.

---

## 4. Dataset Structure

The dataset contains country- and area-level drinking-water access observations between 2000 and 2020.

The analytical grain is:

> one country or area observed in one specific year.

The main original variables include:

| Variable group | Description |
|---|---|
| `name` | Country or area name |
| `year` | Observation year |
| `pop_n` | National population estimate, stored in thousands |
| `pop_u` | Urban population share |
| `wat_bas_n` | National access to at least basic drinking water |
| `wat_bas_r` | Rural access to at least basic drinking water |
| `wat_bas_u` | Urban access to at least basic drinking water |
| other water variables | Limited, unimproved, and surface-water access indicators |

The main Part 2 analysis focuses on the **at least basic** access variables because they are used to calculate progress over time.

---

## 5. Transformation Methodology

The transformation workflow follows this structure:

```text
Source data
    ↓
Country and year sorting
    ↓
Year-difference calculation
    ↓
Annual Rate of Change calculation
    ↓
Missing-value handling
    ↓
Full-access classification
    ↓
Rural–urban ARC comparison
    ↓
Regional lookup and enrichment
    ↓
Summary tables and visual analysis
```

This workflow turns the dataset into a progress-monitoring framework.

---

## 6. Year Representation Analysis

Before calculating progress, I checked how years are represented in the dataset.

The year histogram shows that most observations are concentrated in:

- **2015**
- **2020**

Intermediate years such as 2016, 2017, 2018, and 2019 appear only in a small number of cases.

![Year Distribution Histogram](../../assets/main_visuals/01_year_distribution_histogram.png)

### Year summary

| Metric | Value |
|---|---:|
| Minimum year | 2015 |
| Maximum year | 2020 |
| Average `y_diff` | 4.8 |
| Minimum `y_diff` | 1 |
| Maximum `y_diff` | 5 |
| Count of `y_diff = 0` | 0 |

### Interpretation

The dataset is not a complete annual panel. It is mostly structured around a five-year comparison, with some countries having shorter observation gaps.

This is why `y_diff` is necessary.

Instead of assuming that every country is measured over the same time interval, the analysis calculates the actual year difference for each country pair.

---

## 7. Derived Feature: `y_diff`

The first important derived feature is:

```text
y_diff
```

This field measures the number of years between two observations for the same country.

Formula logic:

```text
y_diff = later year - earlier year
```

The purpose of `y_diff` is to:

- validate the time interval between observations;
- detect possible duplicate country-year rows;
- support Annual Rate of Change calculations.

A `y_diff` of zero would indicate a duplicate country-year issue. In this dataset, the count of `y_diff = 0` is zero, which supports the validity of the country-year pairing.

---

## 8. Annual Rate of Change Methodology

The key metric in Part 2 is **Annual Rate of Change**, abbreviated as **ARC**.

ARC measures the average yearly change in access to at least basic drinking water.

The general formula is:

```text
ARC = (later access value - earlier access value) / year difference
```

ARC is interpreted in:

> percentage points per year.

Three ARC indicators were created:

| Variable | Meaning |
|---|---|
| `ARC_n` | Annual Rate of Change in national basic water access |
| `ARC_r` | Annual Rate of Change in rural basic water access |
| `ARC_u` | Annual Rate of Change in urban basic water access |

---

## 9. ARC Summary Statistics

The Summary sheet calculates average, minimum, and maximum ARC values for national, rural, and urban access.

| Metric | `ARC_n` | `ARC_r` | `ARC_u` |
|---|---:|---:|---:|
| Average | 0.2767 | 0.4845 | 0.1548 |
| Minimum | -1.0218 | -1.2274 | -1.6201 |
| Maximum | 2.7503 | 2.6679 | 2.6682 |

### Interpretation

Rural access has the highest average ARC.

This indicates that rural basic water access improved faster than national and urban access on average.

However, this does not mean rural access is higher than urban access. It means rural access improved faster during the observed period.

The lower urban ARC average is partly explained by the fact that many urban areas already had high or full access, leaving less room for improvement.

---

## 10. Why Zero ARC Needs Careful Interpretation

A zero ARC can mean two different things:

1. access did not improve;
2. access was already at full or near-full coverage.

For example:

```text
100% → 100% = ARC of 0
```

This should not be interpreted as poor performance. It indicates that the country or area already had full access.

For that reason, I created full-access classification fields:

- `ARC_n_full`
- `ARC_r_full`
- `ARC_u_full`

These fields separate countries already at full access from countries with no progress below full coverage.

This improves the quality of the interpretation.

---

## 11. Access-by-Area Classification

The Summary sheet classifies countries into progress categories for national, rural, and urban ARC.

The categories are:

- no ARC value;
- full access;
- ARC = 0 excluding full-access cases;
- ARC > 0 excluding full-access cases;
- ARC < 0 excluding full-access cases.

### Missing ARC values

| Area | Count |
|---|---:|
| National | 2 |
| Rural | 64 |
| Urban | 50 |

Rural and urban access have more missing ARC values than national access. This suggests that area-specific estimates are less complete than national estimates.

---

### Full-access countries

| Area | Count |
|---|---:|
| National | 62 |
| Rural | 29 |
| Urban | 55 |

Urban access has a high number of full-access cases. This supports the idea that urban populations are often closer to complete basic water access.

Rural access has fewer full-access cases, confirming that rural populations still face larger access gaps.

---

### ARC = 0 excluding full-access cases

| Area | Count |
|---|---:|
| National | 16 |
| Rural | 5 |
| Urban | 7 |

These are countries with no measured improvement, but not already full access.

This category is important because it identifies stagnation rather than completed access.

---

### Positive ARC excluding full-access cases

| Area | Count |
|---|---:|
| National | 135 |
| Rural | 116 |
| Urban | 93 |

Most valid observations show positive progress.

The positive rural count is especially important because it shows that many rural areas are improving, even though rural full access remains less common.

---

### Negative ARC excluding full-access cases

| Area | Count |
|---|---:|
| National | 16 |
| Rural | 17 |
| Urban | 26 |

Negative ARC values indicate that access declined between observations.

Urban access has the highest number of negative cases among the three area types.

This does not necessarily mean urban access is generally worse. It means selected urban observations experienced declines during the observed period.

---

## 12. Classification Validation

The classification counts are checked against the total number of country pairs.

Total country pairs:

```text
231
```

The category totals validate that the classification logic accounts for the countries included in the transformed dataset.

This validation step is important because it confirms that the progress categories are complete and that countries are not accidentally left outside the summary logic.

---

## 13. Rural–Urban ARC Difference

To compare rural and urban progress directly, I created:

```text
ARC_diff = ARC_r - ARC_u
```

Interpretation:

| Result | Meaning |
|---|---|
| `ARC_diff > 0` | Rural access improved faster than urban access |
| `ARC_diff < 0` | Urban access improved faster than rural access |
| `ARC_diff ≈ 0` | Rural and urban progress were similar |

This field is central to the Part 2 analysis because Part 1 showed that rural populations had lower and more variable access.

Part 2 checks whether rural areas are catching up over time.

---

## 14. Average ARC Difference by Region

![Average ARC Difference by Region](../../assets/main_visuals/02_average_arc_diff_by_region.png)

This chart compares average `ARC_diff` across regions.

| Region | Average `ARC_diff` |
|---|---:|
| Middle East & North Africa | 0.6130 |
| Latin America & Caribbean | 0.5928 |
| Sub-Saharan Africa | 0.3338 |
| South Asia | 0.2937 |
| East Asia & Pacific | 0.2674 |
| Europe & Central Asia | 0.1736 |
| North America | 0.1396 |

### Interpretation

All regions have positive average `ARC_diff`.

This means rural access improved faster than urban access on average in every region.

The strongest rural catch-up patterns appear in:

- Middle East & North Africa;
- Latin America & Caribbean.

However, a positive `ARC_diff` does not mean rural access is now higher than urban access. It only means rural access improved faster during the observed period.

---

## 15. Rural vs Urban ARC by Region

![Average Rural and Urban ARC by Region](../../assets/main_visuals/03_rural_vs_urban_arc_by_region.png)

This visual compares average rural and urban ARC values directly across regions.

The chart shows that rural ARC is higher than urban ARC in every region.

### Interpretation

This supports a broad rural catch-up pattern.

Rural areas generally had lower initial access, which created more room for improvement. Urban areas often had higher baseline access, so their ARC values are lower because they were closer to the upper limit.

This means the rural-urban gap may be narrowing in terms of progress speed, but the final access gap may still remain.

---

## 16. Regional Aggregation

The Summary sheet groups the transformed dataset by region.

| Region | Countries | Population (millions) | Avg `ARC_n` | Avg `ARC_r` | Avg `ARC_u` |
|---|---:|---:|---:|---:|---:|
| East Asia & Pacific | 40 | 2,247.54 | 0.28 | 0.51 | 0.23 |
| Europe & Central Asia | 64 | 1,017.48 | 0.11 | 0.22 | 0.05 |
| Latin America & Caribbean | 48 | 642.51 | 0.14 | 0.68 | 0.07 |
| Middle East & North Africa | 10 | 311.07 | 0.35 | 0.74 | 0.12 |
| North America | 5 | 368.87 | 0.02 | 0.14 | 0.00 |
| South Asia | 11 | 2,082.32 | 0.48 | 0.56 | 0.27 |
| Sub-Saharan Africa | 53 | 1,124.03 | 0.56 | 0.60 | 0.27 |
| Grand Total | 231 | 7,793.82 | 0.2767 | 0.4845 | 0.1548 |

### Interpretation

The regional table shows that progress is not evenly distributed.

Middle East & North Africa has the highest average rural ARC.

Sub-Saharan Africa has the highest average national ARC.

South Asia combines a large population with strong national and rural progress.

Europe & Central Asia and North America have lower ARC values, likely because many countries already have high or near-universal access.

---

## 17. Regional Progress, Population, and ARC

![Regional Progress in Basic Water Access](../../assets/main_visuals/04_regional_progress_arc_population.png)

This chart compares:

- regional population size;
- average national ARC;
- average rural ARC.

### Interpretation

The chart shows that population size alone does not explain progress.

For example:

- East Asia & Pacific has the largest population, but not the highest ARC.
- South Asia has both a large population and strong ARC values.
- Middle East & North Africa has a smaller population but the highest rural ARC.
- Sub-Saharan Africa has a large population and strong national and rural ARC values.

This means ARC and population must be interpreted together.

ARC measures speed of progress, while population indicates potential scale of impact.

---

## 18. Region-Level Interpretation

### East Asia & Pacific

East Asia & Pacific contains 40 countries or areas and represents the largest population group in the regional summary.

The region shows:

- average national ARC of 0.28;
- average rural ARC of 0.51;
- average urban ARC of 0.23.

Rural progress is higher than urban progress, suggesting rural catch-up.

The regional tables show country-level variation, including strong progress in some countries and negative ARC values in others.

---

### Europe & Central Asia

Europe & Central Asia has the largest number of countries in the summary, with 64 countries or areas.

The region shows relatively low ARC values:

- national ARC: 0.11;
- rural ARC: 0.22;
- urban ARC: 0.05.

Low ARC in this region may reflect high baseline access and limited remaining room for improvement.

This is an important example of why low ARC does not automatically mean poor performance.

---

### Latin America & Caribbean

Latin America & Caribbean shows:

- national ARC of 0.14;
- rural ARC of 0.68;
- urban ARC of 0.07.

The region has one of the strongest rural catch-up patterns.

The large gap between rural and urban ARC suggests that improvement was concentrated mainly in rural access.

---

### Middle East & North Africa

Middle East & North Africa records the highest average rural ARC:

```text
0.74 percentage points per year
```

The region also has a strong positive `ARC_diff`.

This suggests that rural access improved much faster than urban access.

Country-level tables show that strong rural improvements in countries such as Morocco and Iraq contribute heavily to this regional pattern.

---

### North America

North America shows the lowest ARC values:

- national ARC: 0.02;
- rural ARC: 0.14;
- urban ARC: 0.00.

These low values likely reflect high baseline access and limited room for additional improvement.

The regional average should therefore be interpreted with baseline access in mind.

---

### South Asia

South Asia combines a very large population with strong progress:

- national ARC: 0.48;
- rural ARC: 0.56;
- urban ARC: 0.27.

This is important because even moderate improvements in highly populated regions can affect large numbers of people.

South Asia shows improvement across both rural and urban areas, with rural access improving faster.

---

### Sub-Saharan Africa

Sub-Saharan Africa includes 53 countries or areas and represents a major population group.

The region shows:

- average national ARC of 0.56;
- average rural ARC of 0.60;
- average urban ARC of 0.27.

This indicates meaningful progress.

However, Sub-Saharan Africa also contains strong country-level variation, including countries with positive progress, mixed results, and negative ARC values.

The region remains analytically important because progress is occurring, but the remaining access gap may still be large.

---

## 19. Country-Level Evidence

The regional ARC tables support the aggregated findings by showing the underlying country-level observations.

These tables include:

- country name;
- region;
- observation year;
- population;
- `ARC_n`;
- `ARC_r`;
- `ARC_u`.

Regional table folder:

[View regional ARC tables](../../assets/regional_arc_tables/)

### Why this matters

Regional averages are useful, but they can hide internal variation.

Countries within the same region may show:

- strong positive progress;
- zero change;
- negative progress;
- missing values;
- full-access conditions.

The country-level tables make the analysis more transparent and allow the regional findings to be checked against the underlying observations.

---

## 20. Sheet-Level Interpretation

### Transformed dataset sheet

The `Estimates of the use of water (2000-2020)` sheet is the transformation layer.

It contains the engineered variables needed for time-based analysis:

- `y_diff`;
- `ARC_n`;
- `ARC_r`;
- `ARC_u`;
- rounded access values;
- full-access flags;
- `ARC_diff`;
- regional classification.

This sheet transforms the original dataset into an analysis-ready structure.

Sheet export:

[Open transformed dataset export](../sheet_exports/Estimates%20of%20the%20use%20of%20water%20(2000-2020).pdf)

---

### Summary sheet

The `Summary` sheet is the interpretation layer.

It contains:

- year representation analysis;
- ARC statistics;
- access-by-area counts;
- full-access counts;
- positive, negative, and zero ARC classifications;
- regional aggregation;
- visuals.

This sheet turns the transformed dataset into analytical findings.

Sheet export:

[Open summary export](../sheet_exports/Summary.pdf)

---

## 21. Main Analytical Findings

### Finding 1 — The dataset is mainly a 2015–2020 comparison

Most observations are concentrated in 2015 and 2020.

This makes the analysis closer to a multi-year comparison than a continuous annual trend study.

---

### Finding 2 — ARC is necessary for fair progress comparison

Countries do not all have the same year gap.

Using `y_diff` allows each change calculation to be normalized by the actual observation interval.

---

### Finding 3 — Rural access improved faster than urban access

Average rural ARC is higher than average urban ARC.

This pattern appears across all regions.

---

### Finding 4 — Urban access often has lower ARC because of high baseline access

Urban access is often already high or full.

Lower urban ARC should therefore not be interpreted automatically as poor performance.

---

### Finding 5 — Full-access flags improve interpretation

Full-access classification prevents countries already at 100% access from being incorrectly classified as stagnant.

This is one of the most important quality-control improvements in the analysis.

---

### Finding 6 — Regional averages hide country-level variation

Within the same region, countries can have very different ARC patterns.

Some countries improve strongly, while others stagnate or decline.

---

### Finding 7 — Population scale matters

A moderate ARC in a highly populated region can represent a large potential impact.

That is why regional population size should be interpreted alongside ARC values.

---

### Finding 8 — Sub-Saharan Africa remains a critical region

Sub-Saharan Africa shows meaningful progress, but it also contains uneven outcomes and a large affected population.

This makes it one of the most important regions for continued analysis.

---

## 22. Analytical Limitations

This analysis is descriptive and exploratory.

It identifies patterns and progress rates, but it does not prove causality.

Main limitations include:

- the dataset is not a complete annual panel;
- most observations are concentrated around 2015 and 2020;
- some rural and urban values are missing;
- regional averages are simple country-level averages;
- averages are not automatically population-weighted;
- ARC measures speed of progress, not final access level;
- high ARC may reflect low baseline access;
- low ARC may reflect already high access;
- country-level context is needed for stronger interpretation.

---

## 23. Future Improvements

This project could be strengthened by:

- calculating population-weighted regional ARC;
- comparing baseline access with final access levels;
- ranking countries by largest positive and negative ARC;
- building an interactive dashboard;
- reproducing the workflow in Python or R;
- adding confidence intervals or uncertainty measures if available;
- analyzing additional years when more data is available;
- connecting water-access progress with socioeconomic indicators;
- mapping ARC geographically;
- creating country-level profiles for priority cases.

---

## 24. Skills Demonstrated

This part of the project demonstrates the following data analysis skills:

- spreadsheet-based data transformation;
- feature engineering;
- time-difference calculation;
- Annual Rate of Change methodology;
- missing-value handling;
- classification logic;
- full-access flagging;
- rural–urban comparison;
- regional lookup and enrichment;
- pivot-style aggregation;
- visual analysis;
- data storytelling;
- analytical documentation;
- portfolio reporting.

---

## 25. Final Conclusion

Part 2 transforms the drinking-water access dataset into a progress-monitoring framework.

The analysis shows that access to at least basic drinking water generally improved across many countries and regions, with rural access improving faster than urban access on average.

However, faster rural improvement does not mean that rural access gaps have disappeared. Rural populations may still start from lower access levels, and many countries still require continued progress.

The strongest analytical conclusion is:

> Drinking-water access progress must be interpreted through both rate of change and baseline context. ARC shows the speed of improvement, while access levels, population scale, and regional variation determine the real development significance.

This Part 2 analysis adds a time-based dimension to the project and strengthens the overall portfolio by moving from descriptive analysis toward structured progress measurement.
