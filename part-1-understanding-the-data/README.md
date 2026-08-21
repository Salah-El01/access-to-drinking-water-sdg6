# Access to Drinking Water — Part 1: Understanding the Data

## Project Overview

In Part 1 of this project, I analyzed country-level drinking-water access estimates for 2020 using Google Sheets.

My objective was to understand how drinking-water access differed:

- Between national, urban, and rural populations
- Across the four drinking-water service levels
- According to national population and urban–rural structure
- Across World Bank income groups

I used Google Sheets as the main analytical workspace for data validation, cleaning, feature engineering, aggregation, summary statistics, pivot-table analysis, visualization, and reporting.

This analysis forms the descriptive foundation for Part 2, where the project is extended to examine changes in drinking-water access from 2000 to 2020.

---

## Key Project Links

- [Open the Google Sheets workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit)
- [Read the complete Part 1 Analytical Report](./reports/analytical_report/Part1_Analytical_Report.md)
- [Review the Google Sheets PDF exports](./reports/sheet_exports/)
- [Read the Sheet Exports documentation](./reports/sheet_exports/README.md)
- [Read the data documentation](./data/README.md)
- [Consult the Data Dictionary](./data/Data_dictionary.md)
- [Review the visual assets](./assets/)

---

## Analytical Objective

The purpose of this part of the project was to understand the structure of the 2020 drinking-water dataset and identify the principal patterns associated with unequal access.

I focused on four analytical questions:

1. How does national population size relate to urban and rural population shares?
2. How are drinking-water service levels distributed nationally and between urban and rural populations?
3. Do rural and urban populations experience different levels of access and cross-country inequality?
4. How does income classification relate to national drinking-water service levels?

---

## Data Source and Scope

I used country-level estimates from the WHO/UNICEF Joint Monitoring Programme for Water Supply, Sanitation and Hygiene.

The analysis focuses on the year **2020** and covers four drinking-water service levels:

| Service level | Meaning |
|---|---|
| At least basic | Drinking water from an improved source with a collection time of no more than 30 minutes for a round trip, including queuing |
| Limited | Drinking water from an improved source requiring more than 30 minutes for a round trip |
| Unimproved | Drinking water from sources such as unprotected wells or unprotected springs |
| Surface water | Drinking water collected directly from rivers, dams, lakes, ponds, streams, canals, or irrigation channels |

Official references:

- [JMP data portal](https://washdata.org/data)
- [JMP drinking-water service levels](https://washdata.org/topics/drinking-water)
- [JMP estimation methods](https://washdata.org/topics/methods/estimation-methods)

---

## Dataset Variables

I maintained a distinction between source variables, derived features, and cleaned analytical fields.

### Source variables

| Variable group | Examples | Purpose |
|---|---|---|
| Country identification | `name` and country code | Identifying country-level observations |
| Geographic classification | Region | Supporting geographic interpretation |
| Economic classification | `income_group` | Comparing results across income categories |
| Population | `pop_n`, `pop_u` | Measuring national population and urban population share |
| National access | `wat_bas_n`, `wat_lim_n`, `wat_unimp_n`, `wat_sur_n` | Measuring national service-level distribution |
| Urban access | `wat_bas_u`, `wat_lim_u`, `wat_unimp_u`, `wat_sur_u` | Measuring urban service-level distribution |
| Rural access | `wat_bas_r`, `wat_lim_r`, `wat_unimp_r`, `wat_sur_r` | Measuring rural service-level distribution |

`pop_n` is recorded in thousands, while the population-share and drinking-water variables are expressed as percentages.

The complete variable definitions are available in the [Data Dictionary](./data/Data_dictionary.md).

---

## Data Validation

I created `value_cnt` to verify that every imported row contained the expected number of populated source fields.

The Google Sheets formula was:

```gs
=COUNTA(A2:P2)
```

A correctly structured record was expected to contain **16 populated fields**.

This validation identified five malformed rows. I corrected their column structure using:

> Data → Split text to columns

I then repeated the validation before continuing with the calculations.

This step reduced the risk of using shifted or incorrectly imported values in the analysis.

---

## Feature Engineering

I created several derived features to support validation, grouping, aggregation, and visualization.

| Derived feature | Verified Google Sheets logic | Purpose |
|---|---|---|
| `value_cnt` | `=COUNTA(A2:P2)` | Validates the number of populated fields in each imported row |
| `pop_u_val` | `=pop_n_cell*pop_u_cell/100` | Estimates the urban population value |
| `pop_r` | `=100-pop_u_cell` | Calculates the rural population share |
| `pop_n (m)` | `=ROUNDUP(pop_n_cell/1000,0)` | Converts national population from thousands into rounded millions |
| `pop_u (rounded)` | `=IFERROR(ROUND(pop_u_cell,0),"NAN")` | Creates whole-number urban-share groups |
| `pop_r (rounded)` | `=IFERROR(ROUND(pop_r_cell,0),"NAN")` | Creates whole-number rural-share groups |
| `income_group_num` | Ordered mapping from 0 to 4 | Maintains the intended income-group sorting order |

The income-group sorting order was:

| Value | Category |
|---:|---|
| 0 | NAN |
| 1 | Low income |
| 2 | Lower middle income |
| 3 | Upper middle income |
| 4 | High income |

I treated `NAN` as an unclassified category and did not interpret it as part of the ordered income progression.

Because the relevant source fields occupy different positions across the working sheets, I documented the verified formula logic without inventing unverified cell references.

---

## Cleaning the Service-Level Variables

I created cleaned national, urban, and rural service-level fields.

Examples include:

- `wat_bas_n_clean`
- `wat_lim_n_clean`
- `wat_unimp_n_clean`
- `wat_sur_n_clean`
- `wat_bas_u_clean`
- `wat_lim_u_clean`
- `wat_unimp_u_clean`
- `wat_sur_u_clean`
- `wat_bas_r_clean`
- `wat_lim_r_clean`
- `wat_unimp_r_clean`
- `wat_sur_r_clean`

A representative Google Sheets formula was:

```gs
=IF(COUNT($D2:$G2)=4,MIN(100,MAX(0,$D2)),)
```

I copied the formula across the four service-level columns and then down the report dataset.

In each report sheet, `$D2:$G2` represents the corresponding four service-level values for the observation.

The formula:

1. Confirms that all four service values are numeric.
2. Prevents percentages from falling below 0%.
3. Prevents percentages from exceeding 100%.
4. Returns a blank result when the four related service values are incomplete.

I applied this complete-case rule because the four service levels represent components of the same drinking-water distribution. Calculating a grouped distribution from only part of the service ladder could produce a misleading result.

---

## Summary Statistics

I used the following Google Sheets functions to examine central tendency and cross-country dispersion:

```gs
=MIN(range)
=QUARTILE(range,1)
=MEDIAN(range)
=AVERAGE(range)
=QUARTILE(range,3)
=MAX(range)
```

The mean and median helped me evaluate typical access levels, while the quartiles and interquartile range helped identify inequality and dispersion across countries.

---

## Google Sheets Reporting Structure

I organized the analysis into four reporting sheets:

| Sheet | Analytical role |
|---|---|
| Global 2020 Report | Main 2020 dataset, feature preparation, summary statistics, and national–urban–rural comparison |
| Urban 2020 Report | Analysis of drinking-water service levels across urban population-share groups |
| Rural 2020 Report | Analysis of rural access, lower service levels, and rural inequality |
| Pivot Table | Income-group aggregation of population, urbanization, and national service levels |

The individual sheet exports are available in the [reports/sheet_exports](./reports/sheet_exports/) folder.

---

## Repository Structure

```text
part-1-understanding-the-data/
├── assets/
│   ├── 01_population_vs_urban_rural_share.png
│   ├── 02_access_by_area_and_service_level.png
│   ├── 03_national_service_levels_distribution.png
│   ├── 04_urban_service_levels_distribution.png
│   ├── 05_rural_service_levels_distribution.png
│   └── 06_income_group_vs_service_levels.png
│
├── data/
│   ├── README.md
│   └── Data_dictionary.md
│
├── reports/
│   ├── analytical_report/
│   │   └── Part1_Analytical_Report.md
│   │
│   ├── sheet_exports/
│   │   ├── Global 2020 Report.pdf
│   │   ├── Urban 2020 Report.pdf
│   │   ├── Rural 2020 Report.pdf
│   │   ├── Pivot_Table.pdf
│   │   └── README.md
│   │
│   └── README.md
│
└── README.md
```

---

# Key Visualizations and Findings

## 1. National Population Versus Urban and Rural Share

![National population versus urban and rural population share](./assets/01_population_vs_urban_rural_share.png)

### Methodology

I grouped countries by rounded national population size in millions and plotted:

- Average urban population share
- Average rural population share

Urban and rural shares are complementary and therefore combine to approximately 100%.

The horizontal axis represents population-size categories rather than time. I therefore interpreted the chart as a comparison between population groups and not as a chronological trend.

### Finding

The chart does not show a consistent relationship between national population size and urban–rural structure.

Countries with similar population sizes can have substantially different urban and rural population shares. Population size alone is therefore insufficient to explain a country's settlement structure or drinking-water infrastructure requirements.

---

## 2. Access by Area and Service Level

![Access to drinking water by area and service level](./assets/02_access_by_area_and_service_level.png)

### Methodology

I used a candlestick chart to produce a box-and-whisker-style comparison.

For every area and service level, I configured:

- Low as the minimum
- Open as the first quartile
- Close as the third quartile
- High as the maximum

The box represents the interquartile range.

The chart does not display the mean or median directly, so I calculated those statistics separately in the supporting interpretation table.

### Key statistics

| Area and service level | Mean | Median | Interquartile range |
|---|---:|---:|---:|
| National — at least basic | 89.86% | 97.35% | 14.24 |
| Rural — at least basic | 81.34% | 90.73% | 34.29 |
| Urban — at least basic | 94.69% | 98.11% | 7.39 |
| Rural — surface water | 4.22% | 0.22% | 6.16 |
| Urban — surface water | 0.31% | 0.00% | 0.16 |

### Finding

Urban at-least-basic access had the highest average and the narrowest interquartile range.

Rural at-least-basic access had a lower average and a substantially wider interquartile range. This demonstrates that rural access was not only lower but also more unequal across countries.

Urban surface-water reliance was almost nonexistent in most observations. Rural surface-water reliance was also low in the typical country, but a smaller group of countries recorded substantially higher dependence.

---

## 3. National Service-Level Distribution

![National distribution of drinking-water access by service level](./assets/03_national_service_levels_distribution.png)

### Methodology

I created a 100% stacked column chart using:

- Rounded national population size in millions as the grouping dimension
- Average cleaned national service-level percentages as the chart series

Each column represents the average national service distribution of the countries contained in that population-size group.

### Finding

At-least-basic access was the dominant national service category in most population groups.

However, the proportions of limited, unimproved, and surface-water access varied between groups. The chart did not reveal a consistent progression in which drinking-water access automatically improved or declined with national population size.

This supports the conclusion that population size alone does not explain national service quality.

---

## 4. Urban Service-Level Distribution

![Urban distribution of drinking-water access by service level](./assets/04_urban_service_levels_distribution.png)

### Methodology

I grouped countries by rounded urban population share and calculated the average cleaned urban service-level percentages for each represented group.

I then created a 100% stacked column chart to display the complete average service distribution.

### Average urban service distribution

| Urban service level | Average share |
|---|---:|
| At least basic | 94.69% |
| Limited | 3.28% |
| Unimproved | 1.72% |
| Surface water | 0.31% |

### Finding

Urban populations had the strongest overall access profile.

At-least-basic access represented approximately **94.69%** of the average urban distribution. Limited, unimproved, and surface-water services accounted for relatively small average shares.

Although the overall urban results were strong, the chart also identified selected country groups where limited or unimproved services remained relevant.

---

## 5. Rural Service-Level Distribution

![Rural distribution of drinking-water access by service level](./assets/05_rural_service_levels_distribution.png)

### Methodology

I grouped countries by rounded rural population share and calculated the average cleaned rural service-level percentages for each represented group.

The complete-case rural analysis included:

- **159 country records**
- **54 excluded records with incomplete rural service distributions**
- **74 represented rounded rural-share groups**

### Average rural service distribution

| Rural service level | Average share |
|---|---:|
| At least basic | 81.34% |
| Limited | 5.84% |
| Unimproved | 8.73% |
| Surface water | 4.22% |

### Finding

Rural populations had lower at-least-basic access and greater exposure to every lower service category.

Compared with urban areas:

| Service level | Urban average | Rural average | Rural minus urban |
|---|---:|---:|---:|
| At least basic | 94.69% | 81.34% | -13.35 percentage points |
| Limited | 3.28% | 5.84% | +2.56 percentage points |
| Unimproved | 1.72% | 8.73% | +7.01 percentage points |
| Surface water | 0.31% | 4.22% | +3.91 percentage points |

The largest difference was in unimproved access, where the rural average exceeded the urban average by approximately **7.01 percentage points**.

---

## 6. Income Group and Drinking-Water Service Levels

![Average national drinking-water access by income group](./assets/06_income_group_vs_service_levels.png)

### Methodology

I created a pivot table using:

- `income_group` as the row dimension
- Sum of national population
- Average urban population share
- Average national at-least-basic access
- Average national limited access
- Average national unimproved access
- Average national surface-water access

The service values are unweighted country averages. Each included country therefore contributes equally to its income-group average, regardless of population size.

### Pivot-table findings

| Income category | Population represented (millions) | Average urban share | At least basic | Limited | Unimproved | Surface water |
|---|---:|---:|---:|---:|---:|---:|
| NAN | 37.26 | 61.46% | 97.18% | 0.15% | 2.39% | 0.32% |
| Low income | 590.43 | 36.04% | 62.82% | 16.55% | 15.21% | 5.42% |
| Lower middle income | 3,399.31 | 48.79% | 82.21% | 5.69% | 7.90% | 4.29% |
| Upper middle income | 2,547.62 | 64.69% | 96.43% | 1.56% | 1.48% | 0.57% |
| High income | 1,212.08 | 79.36% | 99.56% | 0.18% | 0.24% | 0.02% |

I converted the pivot-table population totals from thousands to millions for readability.

### Finding

The classified income groups displayed a clear descriptive gradient.

Average at-least-basic access increased from **62.82%** in low-income countries to **99.56%** in high-income countries, a difference of approximately **36.74 percentage points**.

Average urban population share also increased from **36.04%** in low-income countries to **79.36%** in high-income countries.

At the same time:

- Limited access declined from 16.55% to 0.18%.
- Unimproved access declined from 15.21% to 0.24%.
- Surface-water access declined from 5.42% to 0.02%.

I retained the `NAN` category for transparency but excluded it from the ordered comparison between income levels.

This analysis identifies a strong descriptive association. It does not establish that income classification independently caused the observed access differences.

---

# Main Findings

## 1. At-least-basic access was the dominant service category

At-least-basic drinking-water access represented the largest share of the service distribution in most national, urban, and rural observations.

However, high national access levels concealed substantial cross-country and urban–rural inequalities.

## 2. Urban areas had the strongest access profile

Urban at-least-basic access averaged approximately **94.69%**, with relatively limited cross-country dispersion.

Urban reliance on surface water was almost nonexistent in most observations.

## 3. Rural populations experienced greater inequality

Rural at-least-basic access averaged approximately **81.34%**, which was **13.35 percentage points** below the urban average.

The rural distribution was also substantially wider, demonstrating greater inequality between countries.

## 4. Lower service levels were concentrated in rural areas

Rural populations recorded higher average limited, unimproved, and surface-water access.

The urban–rural difference was especially large for unimproved services.

## 5. Population size alone did not explain service quality

The population-based visualizations did not reveal a consistent relationship between national population size and drinking-water access quality.

Countries with similar population sizes could have very different service-level distributions.

## 6. Income classification showed a clear descriptive association

Higher income groups had higher average at-least-basic access and lower average dependence on limited, unimproved, and surface-water services.

This relationship was one of the clearest descriptive patterns in the dataset, but it should not be interpreted as proof of causality.

---

# Reports and Supporting Documentation

## Analytical report

The complete methodology, findings, interpretations, limitations, and conclusion are available in:

- [Part 1 Analytical Report](./reports/analytical_report/Part1_Analytical_Report.md)

## Sheet exports

The PDF exports of the four Google Sheets reporting tabs are available in:

- [Sheet Exports folder](./reports/sheet_exports/)
- [Sheet Exports README](./reports/sheet_exports/README.md)
- [Global 2020 Report.pdf](<./reports/sheet_exports/Global 2020 Report.pdf>)
- [Urban 2020 Report.pdf](<./reports/sheet_exports/Urban 2020 Report.pdf>)
- [Rural 2020 Report.pdf](<./reports/sheet_exports/Rural 2020 Report.pdf>)
- [Pivot_Table.pdf](./reports/sheet_exports/Pivot_Table.pdf)

## Data documentation

- [Data README](./data/README.md)
- [Data Dictionary](./data/Data_dictionary.md)

## Visual assets

- [Assets folder](./assets/)

---

# Tools and Skills Demonstrated

This part of the project demonstrates my ability to use Google Sheets for:

- Data import validation
- Detection and correction of malformed records
- Missing-value handling
- Complete-case data cleaning
- Percentage validation
- Feature engineering
- Population-based calculations
- Grouped aggregation
- Summary statistics
- Quartile and interquartile-range analysis
- Pivot-table analysis
- Income-group sorting
- 100% stacked column charts
- Line-chart analysis
- Candlestick-based distribution visualization
- Comparative urban–rural analysis
- Data interpretation
- Analytical documentation
- Portfolio reporting

---

# Limitations

I considered the following limitations when interpreting the results:

1. **The analysis covers one year.**  
   The results describe drinking-water access in 2020 and do not measure change over time.

2. **Most averages are unweighted.**  
   Each included country contributes equally to the country-level averages, regardless of population size.

3. **Missing values affect analytical coverage.**  
   Records without all four required service values were excluded from the corresponding complete-case analysis.

4. **Rounded features reduce precision.**  
   Rounded population and urban–rural shares improve grouping and chart readability but simplify the original continuous values.

5. **Grouped charts conceal country-level variation.**  
   Countries in the same rounded category may have different individual access profiles.

6. **The analysis is descriptive.**  
   The relationships identified between population, urbanization, income group, and drinking-water access do not demonstrate causality.

7. **Other structural factors were not modeled.**  
   Geography, governance, conflict, infrastructure investment, climate conditions, and institutional capacity may contribute to the observed differences.

---

# Future Improvements

I would extend this analysis by:

- Comparing drinking-water access from 2000 to 2020
- Calculating population-weighted access indicators
- Measuring the urban–rural access gap for every country
- Adding regional comparisons
- Identifying countries with the largest populations lacking at-least-basic access
- Ranking countries by surface-water reliance
- Comparing changes across income groups
- Building an interactive dashboard
- Using Python or R for automated validation and reproducible analysis
- Applying appropriate statistical models to evaluate multiple explanatory variables

---

# Final Conclusion

My analysis shows that drinking-water access in 2020 was characterized by substantial inequality despite generally high levels of at-least-basic service.

Urban populations had the highest and most consistent access. Rural populations recorded lower at-least-basic access, greater cross-country variation, and higher average dependence on limited, unimproved, and surface-water services.

The income-group analysis also revealed a clear descriptive gradient. Higher-income groups had higher average at-least-basic access, while low-income countries retained substantially larger shares of lower service levels.

I therefore conclude that national averages alone are insufficient for evaluating progress toward universal drinking-water access. A complete assessment must also consider urban–rural disparities, service-level composition, missing-data coverage, and differences between countries with unequal economic capacity.

These findings establish the analytical foundation for Part 2, where I examine how drinking-water access changed between 2000 and 2020.
