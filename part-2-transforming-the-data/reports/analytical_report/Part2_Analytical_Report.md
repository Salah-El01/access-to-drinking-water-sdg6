# Part 2 Analytical Report: Transforming the Data

## Access to Drinking Water (SDG 6)

This report documents **Part 2: Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

Part 1 examined drinking-water access as a descriptive snapshot. Part 2 introduces a time-based analytical framework by calculating the **Annual Rate of Change (ARC)** in national, rural, and urban access to at least basic drinking-water services.

The main analytical question is:

> Is access to at least basic drinking water improving, declining, or remaining unchanged across countries, population areas, and regions?

---

## 1. Executive Summary

The transformed dataset contains **462 observations for 231 countries or areas**, with exactly two observations per country or area.

Although the source worksheet is titled `Estimates of the use of water (2000-2020)`, the records retained for this analysis cover **2015 to 2020**. The dataset is therefore not a complete annual panel. It is primarily a paired-observation dataset in which a 2015 baseline is compared with one later observation.

The analysis created the following principal indicators:

* `y_diff`: the number of years between paired observations;
* `ARC_n`: annual change in national basic-water access;
* `ARC_r`: annual change in rural basic-water access;
* `ARC_u`: annual change in urban basic-water access;
* `ARC_diff`: the rural ARC minus the urban ARC;
* full-access flags for national, rural, and urban populations;
* regional classifications and aggregated regional summaries.

### Main findings

1. All 231 countries or areas have a 2015 observation.
2. A total of 213 countries or areas have their second observation in 2020.
3. Approximately **96.1% of all records** belong to either 2015 or 2020.
4. The median comparison interval is five years, while the average is approximately 4.8 years.
5. Average rural ARC is higher than average national and urban ARC.
6. Positive ARC below full access is the largest classification in all three population areas.
7. Rural full access is less common than national or urban full access.
8. Among the 165 valid rural-urban comparisons, 112 have a positive `ARC_diff`.
9. Average paired `ARC_diff` is positive in every region.
10. Middle East & North Africa has the highest average rural ARC.
11. Sub-Saharan Africa has the highest average national and urban ARC.
12. Population size alone does not explain regional ARC patterns.
13. Regional ARC values are unweighted country averages and should not be interpreted as population-weighted progress.
14. ARC measures the speed of change, not the final level of access.
15. Faster rural progress is consistent with rural catch-up, but it does not prove that the rural-urban access gap has been eliminated.

---

## 2. Data Source and Analytical Workspace

The project uses country- and area-level drinking-water estimates from the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

* [WHO/UNICEF JMP data downloads](https://washdata.org/data/downloads)
* [View the project Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The workbook contains:

* the source drinking-water data;
* the transformed analytical dataset;
* a regional lookup table;
* derived ARC variables;
* rounded access variables;
* full-access flags;
* the `ARC_diff` comparison;
* Summary calculations;
* regional aggregations;
* charts and supporting tables.

The repository also contains PDF exports of the transformed and Summary sheets. These exports provide fixed visual records of the workbook but are not substitutes for machine-readable data.

---

## 3. Dataset Scope and Grain

The analytical dataset contains:

| Measure                          | Result |
| -------------------------------- | -----: |
| Countries or areas               |    231 |
| Observations                     |    462 |
| Observations per country or area |      2 |
| Earliest observation year        |   2015 |
| Latest observation year          |   2020 |

The source-row grain is:

> One country or area observed in one specific year.

The derived ARC grain is:

> One comparison between the earlier and later observations for the same country or area.

The dataset is sorted first by country or area and then by year. This ordering allows the two observations belonging to the same country to be compared.

### Principal source variables

| Variable    | Description                                               | Unit                |
| ----------- | --------------------------------------------------------- | ------------------- |
| `name`      | Country or area name                                      | Not applicable      |
| `year`      | Observation year                                          | Calendar year       |
| `pop_n`     | National population estimate                              | Thousands of people |
| `pop_u`     | Urban share of the population                             | Percentage          |
| `wat_bas_n` | National access to at least basic drinking-water services | Percentage          |
| `wat_bas_r` | Rural access to at least basic drinking-water services    | Percentage          |
| `wat_bas_u` | Urban access to at least basic drinking-water services    | Percentage          |

Additional limited, unimproved, and surface-water indicators remain in the source data, but the main Part 2 calculations use the three at-least-basic access variables.

---

## 4. Transformation Workflow

The transformation process follows this sequence:

```text
Source data
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
Calculate paired rural-urban ARC difference
    |
    v
Assign regions
    |
    v
Build Summary calculations and visuals
```

This process converts the original observations into a structured progress-monitoring dataset.

---

## 5. Year Representation

Before calculating ARC, the distribution of observation years was examined.

![Distribution of observations by year](../../assets/main_visuals/01_year_distribution_histogram.png)

### Year frequencies

|      Year | Observations | Share of all records |
| --------: | -----------: | -------------------: |
|      2015 |          231 |               50.00% |
|      2016 |            3 |                0.65% |
|      2017 |            9 |                1.95% |
|      2018 |            2 |                0.43% |
|      2019 |            4 |                0.87% |
|      2020 |          213 |               46.10% |
| **Total** |      **462** |          **100.00%** |

The 2015 and 2020 observations together account for:

```text
(231 + 213) / 462 = 96.10%
```

All 231 countries or areas have a 2015 baseline. Of these, 213 have their later observation in 2020, while 18 have their later observation between 2016 and 2019.

Approximately **92.2% of countries or areas** therefore use a five-year comparison from 2015 to 2020.

### Interpretation

The dataset should be treated as a **paired-observation dataset**, not as a complete annual time series.

The year visual is more accurately described as a frequency column chart than a statistical histogram because it displays six discrete year categories. The years should also be presented chronologically when the chart is revised.

The visual describes when observations were recorded. It does not show whether drinking-water access increased or decreased.

---

## 6. Observation Interval: `y_diff`

The derived variable `y_diff` measures the number of years between the earlier and later observations for the same country.

```text
y_diff = later year - earlier year
```

### Verified interval statistics

| Metric                        |     Result |
| ----------------------------- | ---------: |
| Average `y_diff`              | 4.80 years |
| Median `y_diff`               |    5 years |
| Minimum `y_diff`              |     1 year |
| Maximum `y_diff`              |    5 years |
| Comparisons with `y_diff = 0` |          0 |

The absence of zero-year comparisons indicates that no paired calculation compares the same country and year.

Because the comparison interval ranges from one to five years, using a raw access difference would not produce a fair cross-country comparison. Annualisation is therefore necessary.

---

## 7. Annual Rate of Change

ARC measures the average annual change in access to at least basic drinking-water services.

```text
ARC =
(later access percentage - earlier access percentage)
/
(later year - earlier year)
```

ARC is expressed in:

> Percentage points per year.

Three ARC measures were created:

| Variable | Definition                                           |
| -------- | ---------------------------------------------------- |
| `ARC_n`  | Annual Rate of Change in national basic-water access |
| `ARC_r`  | Annual Rate of Change in rural basic-water access    |
| `ARC_u`  | Annual Rate of Change in urban basic-water access    |

### Interpretation

| ARC result        | Interpretation                         |
| ----------------- | -------------------------------------- |
| Positive          | Access increased                       |
| Negative          | Access decreased                       |
| Zero              | No measured change                     |
| Missing or `Null` | The calculation could not be completed |

A zero ARC needs additional classification because it can describe either stagnation below full access or continued full access.

---

## 8. Missing-Value Handling

Rural and urban estimates are less complete than national estimates.

A blank cell, a text value such as `Null`, and a numeric zero have different meanings:

| Value                 | Meaning                                                       |
| --------------------- | ------------------------------------------------------------- |
| Blank                 | No paired calculation is expected on that row                 |
| `Null` or missing ARC | A calculation was expected, but required data was unavailable |
| `0`                   | The ARC was calculated and no change was measured             |

Missing rural or urban values are not converted to zero. Doing so would incorrectly classify unavailable data as no change.

### ARC completeness

| Measure  | Valid ARC values | Missing ARC values |
| -------- | ---------------: | -----------------: |
| National |              229 |                  2 |
| Rural    |              167 |                 64 |
| Urban    |              181 |                 50 |

The rural results have the smallest valid sample and should therefore be interpreted with particular attention to missingness.

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

The current Summary sheet displays the average, minimum, and maximum ARC values. The medians above were verified separately and should be added to the Summary sheet.

### Interpretation

Rural ARC has the highest average and median. This indicates that rural access generally changed more rapidly than national and urban access among the valid observations.

However, the averages are substantially higher than the medians, especially for national and urban ARC. This suggests that a smaller number of high positive values increase the averages. Reporting both mean and median therefore provides a more balanced view of the distributions.

A higher rural ARC does not mean rural access is higher than urban access. It only describes the rate of change.

---

## 10. Full-Access Classification

A zero ARC can occur when access remains unchanged below full coverage or when access is already approximately universal.

The transformed dataset therefore includes:

* `ARC_n_full`;
* `ARC_r_full`;
* `ARC_u_full`.

The classification is based on access estimates rounded to zero decimal places. A country is classified as having full access in an area when both paired access values round to 100.

```text
If earlier rounded access = 100
and later rounded access = 100:
    classify as "full access"
```

This is an **approximate full-access classification**. For example, an estimate close enough to 100 to round to 100 can qualify even if its original value is slightly below 100.

The full-access flags prevent countries already at approximately universal access from being misclassified as stagnant below full coverage.

---

## 11. Access-by-Area Classification

The ARC results were divided into five mutually exclusive categories:

1. missing ARC;
2. full access;
3. zero ARC below full access;
4. negative ARC below full access;
5. positive ARC below full access.

### Verified classification counts

| Classification                 | National |   Rural |   Urban |
| ------------------------------ | -------: | ------: | ------: |
| Missing ARC                    |        2 |      64 |      50 |
| Full access                    |       62 |      29 |      55 |
| Zero ARC below full access     |       16 |       5 |       7 |
| Negative ARC below full access |       16 |      17 |      26 |
| Positive ARC below full access |      135 |     116 |      93 |
| **Total**                      |  **231** | **231** | **231** |

### Interpretation

Positive ARC below full access is the largest category in every population area. This indicates that improvement was more common than stagnation or decline among countries that had not already reached approximately full access.

National full access has the highest count, at 62 cases. Urban full access is also common, at 55 cases, while rural full access is much less common, at 29 cases.

The smaller number of rural full-access cases is consistent with the continued rural disadvantage identified in the broader project.

Urban areas have the largest number of negative ARC cases, at 26. This does not mean that urban access is generally lower than rural access. It means that more valid urban comparisons recorded a decline during the observed interval.

Each column sums to 231, confirming that every country or area is assigned to exactly one category for each population area.

---

## 12. Rural-Urban ARC Difference

The paired rural-urban comparison is:

```text
ARC_diff = ARC_r - ARC_u
```

### Interpretation rules

| Result         | Interpretation                                 |
| -------------- | ---------------------------------------------- |
| `ARC_diff > 0` | Rural ARC is numerically higher than urban ARC |
| `ARC_diff < 0` | Urban ARC is numerically higher than rural ARC |
| `ARC_diff = 0` | Rural and urban ARC are equal                  |
| Missing        | Rural ARC, urban ARC, or both are unavailable  |

A positive `ARC_diff` usually represents faster rural improvement. However, if both rural and urban ARC are negative, a positive result can instead mean that rural access declined more slowly.

### Verified country-level results

| Metric                   | Result |
| ------------------------ | -----: |
| Valid paired comparisons |    165 |
| Missing comparisons      |     66 |
| Positive differences     |    112 |
| Negative differences     |     23 |
| Zero differences         |     30 |
| Average `ARC_diff`       |  0.321 |
| Median `ARC_diff`        |  0.212 |
| Minimum `ARC_diff`       | -2.489 |
| Maximum `ARC_diff`       |  2.329 |

Among the 165 valid paired comparisons:

* 67.9% have a positive difference;
* 13.9% have a negative difference;
* 18.2% have a zero difference.

These results show that rural ARC is numerically higher than urban ARC in most countries with valid paired measurements.

### Missing required visual

The current Summary sheet does not contain the required country-level `ARC_diff` histogram.

The regional average chart below is useful, but it does not show:

* the distribution of the 165 country-level values;
* concentration around zero;
* the balance of positive and negative values;
* the distribution's shape;
* country-level extremes.

A country-level histogram should therefore be added separately.

---

## 13. Average Paired ARC Difference by Region

![Average rural-urban ARC difference by region](../../assets/main_visuals/02_average_arc_diff_by_region.png)

This visual averages valid country-level `ARC_diff` values within each region.

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

This result is consistent with a rural catch-up pattern, but it does not prove that every country has a positive difference or that rural access has reached the urban level.

The regional values are:

* based only on countries with valid rural and urban ARC;
* unweighted by population;
* unable to show within-region variation;
* potentially based on different regional sample sizes.

---

## 14. Average Rural and Urban ARC by Region

![Average rural and urban ARC by region](../../assets/main_visuals/03_rural_vs_urban_arc_by_region.png)

| Region                     | Average rural ARC | Average urban ARC |
| -------------------------- | ----------------: | ----------------: |
| East Asia & Pacific        |             0.508 |             0.233 |
| Europe & Central Asia      |             0.224 |             0.047 |
| Latin America & Caribbean  |             0.680 |             0.072 |
| Middle East & North Africa |             0.737 |             0.124 |
| North America              |             0.142 |             0.002 |
| South Asia                 |             0.559 |             0.266 |
| Sub-Saharan Africa         |             0.604 |             0.270 |

Rural ARC is higher than urban ARC in every region.

Middle East & North Africa has the highest independently calculated rural ARC. Sub-Saharan Africa has the highest urban ARC, closely followed by South Asia.

### Important methodological distinction

The rural and urban averages in this chart are calculated independently.

Overall, rural ARC has 167 valid observations, while urban ARC has 181. The two regional series may therefore contain different country samples.

Consequently:

```text
regional average ARC_r - regional average ARC_u
```

is not necessarily equal to:

```text
average of paired country-level ARC_diff values
```

For example, Latin America & Caribbean has independently calculated averages of:

```text
0.680 - 0.072 = 0.608
```

while its paired average `ARC_diff` is approximately:

```text
0.593
```

The paired `ARC_diff` chart should be used for direct rural-urban comparison. The two-series chart should be used to examine independently calculated rural and urban regional averages.

---

## 15. Regional Summary

| Region                     | Countries or areas | Population (millions) | Average national ARC | Average rural ARC | Average urban ARC |
| -------------------------- | -----------------: | --------------------: | -------------------: | ----------------: | ----------------: |
| East Asia & Pacific        |                 40 |               2,247.5 |                0.278 |             0.508 |             0.233 |
| Europe & Central Asia      |                 64 |               1,017.5 |                0.112 |             0.224 |             0.047 |
| Latin America & Caribbean  |                 48 |                 642.5 |                0.144 |             0.680 |             0.072 |
| Middle East & North Africa |                 10 |                 311.1 |                0.346 |             0.737 |             0.124 |
| North America              |                  5 |                 368.9 |                0.017 |             0.142 |             0.002 |
| South Asia                 |                 11 |               2,082.3 |                0.480 |             0.559 |             0.266 |
| Sub-Saharan Africa         |                 53 |               1,124.0 |                0.558 |             0.604 |             0.270 |
| **Total or overall value** |            **231** |           **7,793.8** |            **0.277** |         **0.484** |         **0.155** |

The ARC columns are simple, unweighted country averages. A small country and a highly populated country contribute equally to a regional ARC average.

The population column represents the regional population total used in the Summary. It does not represent the number of people who gained access.

### Regional highlights

* **East Asia & Pacific** has the largest regional population total.
* **South Asia** has the second-largest population and comparatively strong national, rural, and urban ARC.
* **Sub-Saharan Africa** has the highest national and urban ARC.
* **Middle East & North Africa** has the highest rural ARC.
* **North America** has the lowest ARC in all three population areas.
* **Europe & Central Asia** also has comparatively low ARC values.

Lower ARC in regions with high existing access may reflect a ceiling effect rather than poor performance. High ARC in regions with lower starting access can indicate strong progress while a substantial access deficit remains.

---

## 16. Regional Population and ARC Visual

![Regional progress in basic water access](../../assets/main_visuals/04_regional_progress_arc_population.png)

This dual-axis chart combines:

* regional population totals;
* average national ARC;
* average rural ARC;
* regional categories.

The visual shows that population size and ARC do not follow a simple descriptive relationship.

For example:

* East Asia & Pacific has the largest population but not the highest ARC.
* South Asia combines a large population with comparatively strong ARC.
* Middle East & North Africa has a smaller population but the highest rural ARC.
* Sub-Saharan Africa has a substantial population and the highest national ARC.

The chart does not establish that population causes higher or lower ARC. It also does not measure the number of people who gained access.

Because the ARC values are not population-weighted, the chart should be interpreted as a comparison of regional size and average country-level progress, not as a population-level impact analysis.

---

## 17. Region-Level Interpretation

### East Asia & Pacific

East Asia & Pacific contains 40 countries or areas and has the largest regional population total.

Its average ARC values are positive in all three population areas. Rural ARC is higher than urban ARC, while urban ARC remains comparatively strong relative to several other regions.

The region's large population does not translate automatically into the highest rate of progress.

### Europe & Central Asia

Europe & Central Asia contains 64 countries or areas, the largest country count in the regional classification.

Its national, rural, and urban ARC values are comparatively low. This can be consistent with high starting access and limited remaining potential for measurable improvement.

The regional average should not be treated as evidence that every country followed the same pattern.

### Latin America & Caribbean

Latin America & Caribbean has the second-highest rural ARC and one of the largest paired rural-urban ARC differences.

The positive difference is consistent with strong rural catch-up. However, it does not show that rural access has become equal to urban access.

### Middle East & North Africa

Middle East & North Africa has the highest average rural ARC and the highest average paired `ARC_diff`.

This indicates a particularly strong rural advantage in the rate of change among the valid observations. The result should be interpreted cautiously because the region contains only ten countries or areas and the chart does not display its valid paired sample size.

### North America

North America has the lowest national, rural, and urban ARC averages.

The urban average is close to zero. This is consistent with a strong ceiling effect in areas where access is already approximately universal.

The region contains only five countries or areas, so its average is also based on a small group.

### South Asia

South Asia combines the second-largest regional population with strong national, rural, and urban ARC.

Its rural ARC is higher than its urban ARC, while its urban ARC is the second highest among the regions.

Because the regional ARC values are unweighted, the chart does not quantify the number of South Asian residents affected by these changes.

### Sub-Saharan Africa

Sub-Saharan Africa has the highest national and urban ARC and the third-highest rural ARC.

These results indicate comparatively strong progress across population areas. However, high ARC measures the rate of improvement rather than the final access level. Strong progress can coexist with a large remaining service deficit.

Country-level variation also means that the regional average should not be treated as the experience of every country in the region.

---

## 18. Country-Level Evidence

The regional ARC screenshots provide supporting country-level examples for the aggregated results.

[View the regional ARC table documentation](../../assets/regional_arc_tables/README.md)

The tables include:

* country or area name;
* regional classification;
* observation year;
* population;
* national ARC;
* rural ARC;
* urban ARC.

These screenshots help show that regional averages can contain:

* positive ARC;
* negative ARC;
* zero ARC;
* full-access cases;
* missing rural or urban values;
* unusually high or low country results.

For larger regions, the screenshots display only visible excerpts rather than every country. They should therefore be treated as supporting visual evidence, not as complete machine-readable regional tables.

---

## 19. Interpretation of the Workbook Sheets

### Transformed dataset

The `Estimates of the use of water (2000-2020)` sheet is the transformation layer.

It contains:

* the original water-access variables;
* `y_diff`;
* `ARC_n`;
* `ARC_r`;
* `ARC_u`;
* rounded basic-access variables;
* full-access flags;
* `ARC_diff`;
* regional classifications.

Despite the worksheet title, the analytical observations used in the completed project cover 2015 to 2020.

[Open the transformed-sheet PDF export](../sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf)

### Summary sheet

The `Summary` sheet is the reporting and interpretation layer.

It contains:

* a linked analytical table;
* year frequencies and interval statistics;
* ARC summary statistics;
* progress-status classifications;
* regional aggregations;
* four visualisations.

The current Summary does not yet display the verified ARC medians and does not contain the required country-level `ARC_diff` histogram.

[Open the Summary-sheet PDF export](../sheet_exports/Summary.pdf)

---

## 20. Main Analytical Conclusions

### 1. The analysis is primarily a 2015-2020 comparison

The dataset contains two observations per country or area. Most later observations occur in 2020, while a small group uses a shorter interval ending between 2016 and 2019.

The analysis therefore measures change between paired observations rather than continuous annual trends.

### 2. Annualisation is necessary

The comparison intervals range from one to five years.

`y_diff` allows access changes to be divided by the actual observation interval, making the ARC results more comparable across countries.

### 3. Improvement is common below full access

Positive ARC below full access is the largest status category for national, rural, and urban populations.

This indicates that many countries recorded improvement while still remaining below approximately full access.

### 4. Rural ARC is generally higher

Rural ARC has the highest overall mean and median. Rural ARC is also higher than urban ARC in every independently aggregated regional comparison.

The country-level paired results support the same broad pattern: 112 of 165 valid `ARC_diff` values are positive.

### 5. Rural catch-up is not the same as rural equality

A higher rural ARC is consistent with rural catch-up because rural access generally started from a lower level.

However, the analysis does not demonstrate that rural access has reached the urban level or that rural-urban inequality has disappeared.

### 6. Full-access flags improve interpretation

Countries already at approximately full access should not be grouped with countries experiencing zero progress below full access.

The rounded full-access flags make this distinction explicit.

### 7. Missingness affects area-based comparisons

Rural and urban ARC contain more missing observations than national ARC.

Regional rural and urban averages may therefore be based on different sets of countries, while paired `ARC_diff` calculations require both values to be valid for the same country.

### 8. Regional averages conceal variation

Every region contains countries with different progress patterns.

Regional averages are useful summaries, but they cannot replace country-level examination.

### 9. Population and progress measure different concepts

Population indicates regional scale. ARC indicates the average annual speed of change.

The current analysis does not calculate population-weighted ARC or the number of people who gained access.

---

## 21. Analytical Limitations

This analysis is descriptive and exploratory. It identifies patterns but does not establish their causes.

The principal limitations are:

* the analytical observations cover only 2015 to 2020;
* the dataset contains paired observations rather than a complete annual panel;
* rural and urban estimates have substantial missingness;
* full access is identified using values rounded to zero decimal places;
* regional ARC values are unweighted country averages;
* regional rural and urban averages may use different country samples;
* the regional population chart does not calculate beneficiaries;
* ARC measures change rather than final access;
* high ARC may partly reflect a low starting level;
* low ARC may partly reflect an access ceiling;
* regional averages hide country-level variation;
* the country-level `ARC_diff` histogram is not yet present;
* ARC medians are not yet displayed on the Summary sheet;
* the repository does not currently include machine-readable data files;
* causal explanations require additional socioeconomic, infrastructure, policy, and geographic evidence.

These limitations do not invalidate the analysis, but they define what can and cannot be concluded from it.

---

## 22. Reproducibility

The following repository files support review of the analysis:

* [Data documentation](../../data/README.md)
* [Data dictionary](../../data/data_dictionary.md)
* [Main visual documentation](../../assets/main_visuals/README.md)
* [Regional ARC table documentation](../../assets/regional_arc_tables/README.md)
* [Sheet export documentation](../sheet_exports/README.md)
* [Transformed-sheet PDF](../sheet_exports/Estimates%20of%20the%20use%20of%20water%20%282000-2020%29.pdf)
* [Summary-sheet PDF](../sheet_exports/Summary.pdf)
* [Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The Google Sheets workbook remains the principal analytical workspace.

The PDF exports and PNG assets document the outputs but do not provide fully reproducible source data. Reproducibility would be improved by adding machine-readable exports, such as CSV or XLSX files, for:

* the transformed dataset;
* the Summary calculations;
* the regional aggregation table;
* the country-level `ARC_diff` values.

---

## 23. Recommended Improvements

The next improvements should be:

1. add median national, rural, and urban ARC to the Summary sheet;
2. create the required country-level `ARC_diff` histogram;
3. sort the year-frequency visual chronologically;
4. add valid regional sample sizes to the paired-difference chart;
5. add valid rural and urban sample sizes to the independent regional comparison;
6. export the transformed and Summary data in machine-readable formats;
7. calculate population-weighted regional ARC as a separate measure;
8. compare ARC with baseline and final access levels;
9. identify the largest positive and negative country-level changes;
10. build a reproducible Python or R version of the workflow;
11. create geographic maps or an interactive dashboard;
12. incorporate uncertainty estimates if they become available.

Population-weighted and unweighted results should remain separate because they answer different analytical questions.

---

## 24. Skills Demonstrated

This part of the project demonstrates:

* spreadsheet-based data transformation;
* sorting and paired-observation logic;
* feature engineering;
* time-interval calculation;
* Annual Rate of Change calculation;
* error and missing-value handling;
* full-access classification;
* mutually exclusive status classification;
* rural-urban comparison;
* regional lookup and enrichment;
* aggregation and validation;
* chart interpretation;
* methodological documentation;
* analytical storytelling;
* critical assessment of limitations.

---

## 25. Final Conclusion

Part 2 transforms country-level drinking-water observations into a structured progress-monitoring framework.

The verified results show that access to at least basic drinking-water services improved in many countries. Rural ARC is generally higher than urban ARC, both in the overall summary and across regional comparisons. This pattern is consistent with rural catch-up.

However, a higher rural rate of change does not mean that rural access is already higher or that the rural-urban access gap has disappeared. ARC must be interpreted alongside starting access, final access, full-access status, missingness, population scale, and country-level variation.

The central conclusion is:

> ARC measures the speed and direction of change, while access levels and population context determine the broader development significance.

This analysis strengthens the project by moving from a descriptive access snapshot toward a more rigorous examination of progress over time.
