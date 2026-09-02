# Access to Drinking Water - SDG 6 Data Analysis Project

## From Descriptive Access Analysis to Progress Monitoring

This repository presents a two-part data analysis project examining global access to drinking water in connection with **United Nations Sustainable Development Goal 6: Clean Water and Sanitation**.

The analysis uses country- and area-level estimates from the **WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene (JMP)**.

The project progresses through two complementary stages:

1. **Part 1: Understanding the Data**
   A descriptive analysis of drinking-water access in 2020.

2. **Part 2: Transforming the Data**
   A paired-observation analysis of changes in access between 2015 and 2020 using Annual Rates of Change.

Together, the two parts move from understanding current access inequalities to measuring how access changes over time.

---

## Project Navigation

| Resource                                                                                                                              | Description                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [Part 1: Understanding the Data](./part-1-understanding-the-data/README.md)                                                           | Descriptive analysis of the 2020 access landscape               |
| [Part 1 Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing) | Dynamic Part 1 analytical workspace                             |
| [Part 1 Analytical Report](./part-1-understanding-the-data/reports/analytical_report/Part1_Analytical_Report.md)                      | Complete Part 1 methodology, findings, and interpretation       |
| [Part 1 Visual Assets](./part-1-understanding-the-data/assets/)                                                                       | Charts and supporting visual outputs                            |
| [Part 1 Sheet Exports](./part-1-understanding-the-data/reports/sheet_exports/)                                                        | PDF exports of the Part 1 spreadsheet analysis                  |
| [Part 2: Transforming the Data](./part-2-transforming-the-data/README.md)                                                             | Progress analysis using Annual Rates of Change                  |
| [Part 2 Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing) | Dynamic Part 2 analytical workspace                             |
| [Part 2 Analytical Report](./part-2-transforming-the-data/reports/analytical_report/Part2_Analytical_Report.md)                       | Complete Part 2 methodology, verified findings, and limitations |
| [Part 2 Visual Assets](./part-2-transforming-the-data/assets/README.md)                                                               | Documentation of charts and regional ARC tables                 |
| [Part 2 Data Dictionary](./part-2-transforming-the-data/data/data_dictionary.md)                                                      | Definitions, units, formulas, and derived-variable logic        |
| [WHO/UNICEF JMP data downloads](https://washdata.org/data/downloads)                                                                  | Official source-data portal                                     |

---

## 1. Project Overview

Access to safe and reliable drinking water is a central public-health and development issue.

This project examines drinking-water access through several analytical dimensions:

* national, rural, and urban populations;
* basic, limited, unimproved, and surface-water service levels;
* country income groups;
* national population size;
* urban and rural population shares;
* regional classifications;
* changes in access over time.

The main analytical questions are:

1. What does drinking-water access look like across countries in 2020?
2. How does access differ between national, rural, and urban populations?
3. Which service-level inequalities are most visible?
4. Is drinking-water access associated with country income group?
5. Does population size clearly explain access quality?
6. How did access to at least basic drinking water change between observations?
7. Are rural areas progressing faster than urban areas?
8. Which regions show stronger or weaker rates of progress?
9. How should ARC be interpreted alongside access levels, missingness, and population scale?

---

## 2. Analytical Progression

| Dimension                  | Part 1                                                     | Part 2                                                                              |
| -------------------------- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Title                      | Understanding the Data                                     | Transforming the Data                                                               |
| Time perspective           | 2020 snapshot                                              | Paired observations from 2015 to 2020                                               |
| Primary focus              | Access levels and inequalities                             | Direction and speed of change                                                       |
| Main analytical grain      | One country or area in 2020                                | Two observations and one comparison per country or area                             |
| Main comparison dimensions | Area, service level, income group, population              | Area, time interval, ARC, region, population                                        |
| Principal methods          | Cleaning, validation, descriptive statistics, pivot tables | Feature engineering, paired calculations, ARC, classification, regional aggregation |
| Central outcome            | Understanding the access landscape                         | Monitoring progress over time                                                       |

The two parts answer different but connected questions:

```text
Part 1: What does access look like?
                 |
                 v
Part 2: How is access changing?
                 |
                 v
Combined interpretation:
Where are inequalities present, and how quickly are they changing?
```

---

## 3. Repository Structure

```text
access-to-drinking-water-sdg6/
|
|-- part-1-understanding-the-data/
|   |-- assets/
|   |-- data/
|   |-- reports/
|   `-- README.md
|
|-- part-2-transforming-the-data/
|   |-- assets/
|   |   |-- main_visuals/
|   |   `-- regional_arc_tables/
|   |
|   |-- data/
|   |   |-- README.md
|   |   `-- data_dictionary.md
|   |
|   |-- reports/
|   |   |-- analytical_report/
|   |   `-- sheet_exports/
|   |
|   `-- README.md
|
`-- README.md
```

Each project part contains its own documentation, visual assets, data notes, reports, and supporting exports.

---

# Part 1: Understanding the Data

## 4. Part 1 Objective

[Open Part 1](./part-1-understanding-the-data/README.md)

Part 1 examines the 2020 drinking-water access dataset as a descriptive snapshot.

The primary question is:

> What does access to drinking water look like in 2020, and how does it differ across population areas, income groups, and population-size patterns?

The analysis begins with importing and validating the data before examining population representation, service-level distributions, rural-urban inequalities, and income-group patterns.

---

## 5. Part 1 Analytical Workspace

[Open the Part 1 Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

The Part 1 workbook contains:

* the imported source data;
* validation and cleaning checks;
* population calculations;
* national, rural, and urban access analysis;
* descriptive statistics;
* income-group aggregations;
* charts and supporting outputs.

---

## 6. Part 1 Dataset

Part 1 uses the 2020 drinking-water access dataset.

The original dataset contains 16 variables covering identification, population, income classification, and drinking-water service levels.

### Principal variables

| Variable group                        | Description                                       |
| ------------------------------------- | ------------------------------------------------- |
| `name`                                | Country or area name                              |
| `income_group`                        | Country income classification                     |
| `pop_n`                               | National population estimate, stored in thousands |
| `pop_u`                               | Urban share of the national population            |
| `wat_bas_n`, `wat_bas_r`, `wat_bas_u` | Access to at least basic drinking-water services  |
| `wat_lim_*`                           | Access to limited drinking-water services         |
| `wat_unimp_*`                         | Reliance on unimproved drinking-water sources     |
| `wat_sur_*`                           | Reliance on surface water                         |

### Derived Part 1 variables

Part 1 created additional fields including:

* `value_cnt`;
* `pop_u_val`;
* `pop_r`;
* `pop_n (m)`;
* rounded national population values;
* rounded national basic-access values;
* rounded urban and rural population shares.

These features support import validation, population calculations, chart readability, and descriptive interpretation.

---

## 7. Part 1 Workflow

```text
Import source data
    |
    v
Validate row and column structure
    |
    v
Create population features
    |
    v
Calculate descriptive statistics
    |
    v
Compare national, rural, and urban access
    |
    v
Examine population-size patterns
    |
    v
Aggregate by income group
    |
    v
Create charts and analytical documentation
```

---

## 8. Part 1 Analysis Areas

### Data import and validation

The dataset was imported into Google Sheets and checked for separator and column-structure problems.

The helper variable `value_cnt` counts non-empty values in each row and helps identify incorrectly imported records.

### Population representation

The analysis compares dataset population totals with external global population estimates.

Urban population values are estimated using:

```text
pop_u_val = pop_n * (pop_u / 100)
```

Because `pop_n` is stored in thousands, the analysis requires unit conversion before comparison with population totals expressed in millions or billions.

### Urban and rural population shares

Rural population share is calculated as:

```text
pop_r = 100 - pop_u
```

This supports direct comparison between the urban and rural composition of each country or area.

### Access by population area

Part 1 compares national, rural, and urban access across four service levels:

* at least basic;
* limited;
* unimproved;
* surface water.

The descriptive measures include:

* minimum;
* maximum;
* mean;
* median;
* mode;
* first quartile;
* third quartile;
* interquartile range;
* standard deviation.

### Access by population size

Stacked visualisations examine whether national population size and urban-rural composition clearly explain water-service patterns.

### Access by income group

A pivot-style summary compares income groups using:

* total national population;
* average urban population share;
* average national basic access;
* average national limited access;
* average national unimproved access;
* average national surface-water reliance.

Income groups are placed in an ordered sequence to support clearer comparison.

---

## 9. Part 1 Main Findings

The Part 1 results show that:

1. Many countries have high national access to at least basic drinking water.
2. Urban access is generally higher and less variable than rural access.
3. Rural populations show greater inequality and higher exposure to limited, unimproved, and surface-water services.
4. Population size alone does not provide a clear explanation of drinking-water access quality.
5. Income group shows a strong descriptive association with national water-access quality.
6. Lower-income groups generally have lower average basic access.
7. Lower-income groups have greater exposure to limited, unimproved, and surface-water categories.
8. Higher-income groups generally have near-universal basic access and very low exposure to lower service levels.

These results describe associations and distributional patterns. They do not establish that income or population characteristics cause the observed access outcomes.

---

## 10. Part 1 Outputs

| Output                       | Link                                                                                                                       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Part 1 project documentation | [Open Part 1 README](./part-1-understanding-the-data/README.md)                                                            |
| Part 1 analytical report     | [Open analytical report](./part-1-understanding-the-data/reports/analytical_report/Part1_Analytical_Report.md)             |
| Part 1 assets                | [Open visual assets](./part-1-understanding-the-data/assets/)                                                              |
| Part 1 reports               | [Open reports](./part-1-understanding-the-data/reports/)                                                                   |
| Part 1 sheet exports         | [Open sheet exports](./part-1-understanding-the-data/reports/sheet_exports/)                                               |
| Part 1 workbook              | [Open Google Sheets](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing) |

---

# Part 2: Transforming the Data

## 11. Part 2 Objective

[Open Part 2](./part-2-transforming-the-data/README.md)

Part 2 extends the project from a descriptive snapshot to a paired-observation progress analysis.

The primary question is:

> Is access to at least basic drinking water improving, declining, or remaining unchanged across countries, population areas, and regions?

The central measure is the **Annual Rate of Change**, abbreviated as **ARC**.

---

## 12. Part 2 Analytical Workspace

[Open the Part 2 Google Sheets workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

The Part 2 workbook contains:

* the source drinking-water variables;
* the transformed analytical dataset;
* paired country observations;
* year-difference calculations;
* national, rural, and urban ARC;
* missing-value handling;
* approximate full-access flags;
* rural-urban ARC comparisons;
* regional classifications;
* Summary calculations;
* regional aggregations;
* four existing charts.

---

## 13. Verified Part 2 Dataset Scope

Although the transformed worksheet is titled:

```text
Estimates of the use of water (2000-2020)
```

the observations retained in the completed analysis cover **2015 to 2020**.

| Measure                                          | Verified result |
| ------------------------------------------------ | --------------: |
| Countries or areas                               |             231 |
| Observations                                     |             462 |
| Observations per country or area                 |               2 |
| Earliest analytical year                         |            2015 |
| Latest analytical year                           |            2020 |
| Countries or areas with a 2015 baseline          |             231 |
| Countries or areas with a 2020 later observation |             213 |

The Part 2 dataset is not a complete annual panel. It is primarily a paired-observation dataset.

### Observation-year distribution

|      Year | Observations |
| --------: | -----------: |
|      2015 |          231 |
|      2016 |            3 |
|      2017 |            9 |
|      2018 |            2 |
|      2019 |            4 |
|      2020 |          213 |
| **Total** |      **462** |

Approximately 96.1% of all observations belong to either 2015 or 2020.

---

## 14. Part 2 Transformation Workflow

```text
Source observations
    |
    v
Sort by country and year
    |
    v
Match paired country observations
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
Calculate paired rural-urban differences
    |
    v
Assign regions
    |
    v
Create Summary tables and visualisations
    |
    v
Prepare analytical reporting
```

---

## 15. Part 2 Derived Measures

### Observation interval

```text
y_diff = later year - earlier year
```

| Statistic             |     Result |
| --------------------- | ---------: |
| Average `y_diff`      | 4.80 years |
| Median `y_diff`       |    5 years |
| Minimum `y_diff`      |     1 year |
| Maximum `y_diff`      |    5 years |
| Zero-year comparisons |          0 |

### Annual Rate of Change

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

| Variable | Meaning                                      |
| -------- | -------------------------------------------- |
| `ARC_n`  | Annual change in national basic-water access |
| `ARC_r`  | Annual change in rural basic-water access    |
| `ARC_u`  | Annual change in urban basic-water access    |

### Approximate full-access flags

The following variables separate continued full access from zero progress below full access:

* `ARC_n_full`;
* `ARC_r_full`;
* `ARC_u_full`.

The source access values are rounded to zero decimal places. Both paired values must round to 100.

These fields therefore identify **approximate full access**, not necessarily unrounded values of exactly 100.000%.

### Rural-urban ARC difference

```text
ARC_diff = ARC_r - ARC_u
```

| Result   | Interpretation                                |
| -------- | --------------------------------------------- |
| Positive | Rural ARC is numerically higher               |
| Negative | Urban ARC is numerically higher               |
| Zero     | Rural and urban ARC are equal                 |
| Missing  | Rural ARC, urban ARC, or both are unavailable |

A positive value normally indicates faster rural improvement. If both ARC values are negative, it can instead indicate that rural access declined more slowly.

---

## 16. Part 2 ARC Results

### Summary statistics

| Statistic      | National ARC | Rural ARC | Urban ARC |
| -------------- | -----------: | --------: | --------: |
| Valid values   |          229 |       167 |       181 |
| Missing values |            2 |        64 |        50 |
| Average        |        0.277 |     0.484 |     0.155 |
| Median         |        0.079 |     0.290 |     0.030 |
| Minimum        |       -1.022 |    -1.227 |    -1.620 |
| Maximum        |        2.750 |     2.668 |     2.668 |

Rural ARC has the highest mean and median.

This describes a higher rate of change, not a higher level of rural access.

### Progress classifications

| Classification                 | National |   Rural |   Urban |
| ------------------------------ | -------: | ------: | ------: |
| Missing ARC                    |        2 |      64 |      50 |
| Full access                    |       62 |      29 |      55 |
| Zero ARC below full access     |       16 |       5 |       7 |
| Negative ARC below full access |       16 |      17 |      26 |
| Positive ARC below full access |      135 |     116 |      93 |
| **Total**                      |  **231** | **231** | **231** |

Positive ARC below full access is the largest category for national, rural, and urban populations.

### Paired rural-urban results

| Metric                  | Result |
| ----------------------- | -----: |
| Valid `ARC_diff` values |    165 |
| Missing paired values   |     66 |
| Positive differences    |    112 |
| Negative differences    |     23 |
| Zero differences        |     30 |
| Average `ARC_diff`      |  0.321 |
| Median `ARC_diff`       |  0.212 |
| Minimum `ARC_diff`      | -2.489 |
| Maximum `ARC_diff`      |  2.329 |

Rural ARC is numerically higher in approximately 67.9% of the valid paired comparisons.

---

## 17. Part 2 Regional Results

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
* Europe & Central Asia has the largest country or area count.
* Middle East & North Africa has the highest average rural ARC.
* Sub-Saharan Africa has the highest average national and urban ARC.
* South Asia combines a large population with comparatively strong progress.
* North America has the lowest ARC in all three population areas.

The regional ARC values are unweighted country averages. Each valid country contributes equally, regardless of population size.

The population values do not represent the number of people who gained access.

---

## 18. Part 2 Visual Outputs

The detailed visual documentation is available in:

[Part 2 Main Visuals](./part-2-transforming-the-data/assets/main_visuals/README.md)

The four existing charts are:

1. observation frequency by year;
2. average paired rural-urban ARC difference by region;
3. independently calculated rural and urban ARC by region;
4. regional population with national and rural ARC.

Supporting regional screenshots are documented in:

[Part 2 Regional ARC Tables](./part-2-transforming-the-data/assets/regional_arc_tables/README.md)

### Current Part 2 completion notes

The current Summary sheet does not yet display:

* median national ARC;
* median rural ARC;
* median urban ARC;
* the required country-level `ARC_diff` histogram.

The medians have been verified and are documented in the Part 2 analytical report.

The existing regional average `ARC_diff` chart does not replace the missing country-level histogram because it cannot show the distribution of the 165 valid country values.

---

## 19. Part 2 Outputs

| Output                       | Link                                                                                                                       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Part 2 project documentation | [Open Part 2 README](./part-2-transforming-the-data/README.md)                                                             |
| Part 2 analytical report     | [Open analytical report](./part-2-transforming-the-data/reports/analytical_report/Part2_Analytical_Report.md)              |
| Part 2 data documentation    | [Open data README](./part-2-transforming-the-data/data/README.md)                                                          |
| Part 2 data dictionary       | [Open data dictionary](./part-2-transforming-the-data/data/data_dictionary.md)                                             |
| Part 2 assets                | [Open visual assets](./part-2-transforming-the-data/assets/README.md)                                                      |
| Part 2 reports               | [Open reports](./part-2-transforming-the-data/reports/README.md)                                                           |
| Part 2 sheet exports         | [Open sheet exports](./part-2-transforming-the-data/reports/sheet_exports/README.md)                                       |
| Part 2 workbook              | [Open Google Sheets](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing) |

---

# Combined Analytical Story

## 20. What Part 1 Establishes

Part 1 establishes the descriptive access landscape.

It shows that:

* urban access is generally stronger and less variable than rural access;
* rural populations face greater exposure to lower service levels;
* income group is strongly associated with access quality;
* population size alone does not clearly explain access patterns.

These findings identify where inequality is visible.

---

## 21. What Part 2 Adds

Part 2 adds the time dimension.

It shows that:

* positive change below full access is common;
* rural ARC is generally higher than urban ARC;
* rural ARC is numerically higher in most valid paired country comparisons;
* all seven regional paired `ARC_diff` averages are positive;
* full-access cases must be separated from stagnation;
* regional progress patterns differ;
* country-level variation remains important;
* population size alone does not explain the speed of progress.

These findings describe how access is changing.

---

## 22. Combined Interpretation

Together, the two parts show that drinking-water access inequality cannot be explained by a single factor.

The results must be interpreted through:

* population area;
* service level;
* income group;
* baseline access;
* final access;
* observation interval;
* regional context;
* population scale;
* missing-data patterns;
* rate of change.

The combined analytical progression is:

```text
Understand current access
          |
          v
Identify inequalities
          |
          v
Measure progress over time
          |
          v
Interpret progress within context
```

A higher rate of rural improvement is consistent with rural catch-up, but it does not mean that rural access has reached the urban level.

Similarly, low ARC does not automatically indicate poor performance. It can reflect limited remaining room for improvement when access is already close to universal.

---

## 23. Tools Used

The project uses:

* Google Sheets;
* spreadsheet formulas;
* conditional logic;
* lookup functions;
* pivot tables;
* charts;
* PDF worksheet exports;
* PNG visual assets;
* Markdown;
* GitHub.

The Google Sheets workbooks remain the dynamic analytical workspaces for formula and calculation inspection.

---

## 24. Skills Demonstrated

This project demonstrates:

* spreadsheet-based data cleaning;
* import validation;
* feature engineering;
* unit conversion;
* missing-value handling;
* descriptive statistics;
* quartile and spread analysis;
* population calculations;
* area-based comparison;
* income-group aggregation;
* paired-observation logic;
* time-interval calculation;
* Annual Rate of Change methodology;
* approximate full-access classification;
* rural-urban progress comparison;
* lookup-based regional enrichment;
* regional aggregation;
* visual analysis;
* analytical interpretation;
* data storytelling;
* methodological documentation;
* critical assessment of limitations;
* GitHub portfolio organisation.

---

## 25. Methodological Limitations

This project is descriptive and exploratory. It identifies patterns and associations but does not establish causality.

### Part 1 limitations

* Part 1 is a 2020 snapshot.
* Cross-sectional associations do not show how access changed over time.
* Country-level averages can hide within-country inequality.
* Income-group patterns should not be interpreted as causal effects.
* Population size alone does not describe infrastructure, geography, governance, or investment.

### Part 2 limitations

* The completed analytical observations cover 2015 to 2020.
* The data contains paired observations rather than a complete annual panel.
* Rural and urban variables contain substantial missingness.
* Full-access flags use values rounded to zero decimal places.
* Independent rural and urban averages can use different country samples.
* Regional ARC values are unweighted country averages.
* Population-weighted ARC was not calculated.
* Regional population totals do not measure beneficiaries.
* ARC measures the speed of change, not the final access level.
* High ARC can partly reflect a low starting level.
* Low ARC can partly reflect an access ceiling.
* Regional averages hide country-level variation.
* The country-level `ARC_diff` histogram is not yet present.
* The verified ARC medians are not yet displayed in the Summary sheet.

### Repository limitations

* PDF exports provide fixed spreadsheet evidence but do not expose formulas.
* PNG regional tables are screenshots rather than machine-readable tables.
* Larger regional screenshots can display only visible excerpts.
* Part 2 does not currently contain machine-readable CSV or XLSX exports of its transformed calculations.
* Direct formula inspection requires the Google Sheets workbooks.

---

## 26. Reproducibility

The repository documents the analytical workflow through:

* project READMEs;
* data documentation;
* data dictionaries;
* analytical reports;
* sheet exports;
* chart images;
* supporting table screenshots;
* links to the Google Sheets workbooks.

Reproducibility would be improved by adding:

* machine-readable exports of the transformed datasets;
* machine-readable Summary and aggregation tables;
* a formula-reference document;
* country-level `ARC_diff` data;
* reproducible Python or R scripts;
* versioned source-data snapshots;
* automated validation checks.

---

## 27. Recommended Future Improvements

The project could be extended by:

1. adding the verified Part 2 ARC medians to the Summary sheet;
2. creating the required country-level `ARC_diff` histogram;
3. adding valid sample sizes to regional ARC charts;
4. exporting transformed data in CSV or XLSX format;
5. calculating population-weighted regional ARC as a separate measure;
6. comparing baseline and final access levels directly;
7. ranking countries by the strongest improvement and decline;
8. reproducing the workflow in Python or R;
9. building an interactive dashboard;
10. mapping access levels and ARC geographically;
11. incorporating socioeconomic and infrastructure indicators;
12. adding uncertainty estimates where available;
13. creating country-level profiles for priority cases;
14. developing a portfolio presentation or interactive case study.

Population-weighted and unweighted results should remain separate because they answer different analytical questions.

---

## 28. Recommended Review Order

For the clearest understanding of the complete project:

1. Read the [Part 1 README](./part-1-understanding-the-data/README.md).
2. Review the [Part 1 Analytical Report](./part-1-understanding-the-data/reports/analytical_report/Part1_Analytical_Report.md).
3. Read the [Part 2 README](./part-2-transforming-the-data/README.md).
4. Review the [Part 2 Analytical Report](./part-2-transforming-the-data/reports/analytical_report/Part2_Analytical_Report.md).
5. Consult the Part 2 [Data Dictionary](./part-2-transforming-the-data/data/data_dictionary.md).
6. Review the visual and spreadsheet evidence in each part.
7. Open the Google Sheets workbooks when formula-level inspection is required.

---

## 29. Final Conclusion

This repository analyses global drinking-water access from two complementary perspectives.

Part 1 describes the 2020 access landscape and identifies inequalities across population areas, service levels, income groups, and population structures.

Part 2 measures the direction and speed of change between paired observations from 2015 to 2020.

The combined evidence shows that access to at least basic drinking water improved in many countries. Rural ARC is generally higher than urban ARC, which is consistent with rural catch-up.

However, faster improvement does not mean that inequality has disappeared.

The main conclusion is:

> Drinking-water access must be interpreted through both current conditions and change over time. Access levels show the remaining inequality, while ARC shows the direction and speed of progress.

The project demonstrates a complete spreadsheet-based analytical workflow, from data cleaning and transformation to statistical description, regional comparison, visual analysis, reporting, and portfolio-ready GitHub documentation.
