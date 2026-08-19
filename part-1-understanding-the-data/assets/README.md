# Visual Assets — Part 1: Understanding the Data

This folder contains the six principal visualizations I created during Part 1 of the **Access to Drinking Water** project.

I produced the visuals in Google Sheets to investigate population structure, drinking-water access by area, service-level distributions and differences between income groups.

Together, these charts document the visual-analysis component required by the Part 1 project instructions.

---

## Visual Inventory

| No. | Visualization | Analytical purpose |
|---:|---|---|
| 01 | Population versus urban/rural share | Examine the relationship between population size and urbanization structure |
| 02 | Access by area and service level | Compare the spread of 12 national, rural and urban access variables |
| 03 | National service-level distribution | Examine national access across grouped population sizes |
| 04 | Urban service-level distribution | Examine urban access across rounded urban-population shares |
| 05 | Rural service-level distribution | Examine rural access across rounded rural-population shares |
| 06 | Income group versus service levels | Compare average national access across income classifications |

---

## 01 — Urban and Rural Population Shares by National Population Size

![Urban and rural population shares by national population size](./01_population_vs_urban_rural_share.png)

### Purpose

I created this line chart to examine whether national population size is associated with the proportion of a country’s population living in urban or rural areas.

### Methodology

The source dataset provides:

- `pop_n`: national population estimate in thousands;
- `pop_u`: urban population share.

I derived rural population share using:

`pop_r = 100 - pop_u`

I also converted national population into the rounded-up million-based feature `pop_n (m)` to reduce the visual effect of extreme population values.

I used `pop_n (m)` on the horizontal axis and applied the **Average** aggregation to the urban and rural population-share series.

### Findings

The urban and rural lines move in opposite directions because:

`pop_u + pop_r = 100%`

However, I did not identify a stable upward or downward relationship between national population size and urbanization. Countries within similar population-size groups can have substantially different urban and rural population shares.

### Interpretation

I concluded that national population size alone does not explain whether a country is predominantly urban or rural. I therefore considered additional dimensions, particularly area type and income classification, in the subsequent drinking-water access analysis.

---

## 02 — Drinking-Water Access by Area and Service Level

![Drinking-water access by area and service level](./02_access_by_area_and_service_level.png)

### Purpose

I created this chart to compare the tendency and spread of 12 drinking-water access variables across national, rural and urban populations.

The variables cover four service levels:

- At least basic
- Limited
- Unimproved
- Surface water

### Methodology

I first calculated descriptive statistics for each service variable, including:

- Minimum
- First quartile
- Median
- Mean
- Third quartile
- Maximum
- Interquartile range
- Standard deviation

I then created a candlestick chart in Google Sheets using:

- **Low:** Minimum
- **Open:** First quartile
- **Close:** Third quartile
- **High:** Maximum

The box therefore represents the interquartile range, while the whiskers represent the complete minimum-to-maximum range.

The chart does not display the median or mean directly. I interpreted the visualization together with the separate descriptive-statistics table.

### Findings

| Area | Mean basic access | Basic-access IQR | Interpretation |
|---|---:|---:|---|
| National | 89.86% | 14.24 | Generally high, with some cross-country inequality |
| Rural | 81.34% | 34.29 | Lowest and most variable basic access |
| Urban | 94.69% | 7.39 | Highest and most consistent basic access |

Urban basic access has the highest and tightest distribution. Rural basic access has a lower box and substantially greater spread.

Limited, unimproved and surface-water distributions remain close to zero in many urban observations but are higher and more dispersed in rural areas.

### Interpretation

I found the following overall ordering for at least basic access:

`Urban > National > Rural`

National results generally fall between the urban and rural distributions because national percentages combine both area types.

The chart demonstrates that the remaining drinking-water access gaps are most pronounced and most variable in rural areas.

---

## 03 — National Distribution of Access by Service Level

![National drinking-water service-level distribution](./03_national_service_levels_distribution.png)

### Purpose

I created this chart to examine whether national drinking-water service quality changes consistently according to national population size.

### Methodology

I used the rounded-up national-population feature `pop_n (m)` to group countries into more readable population-size categories.

For every represented population-size category, I calculated the average national share of:

- `wat_bas_n_clean`;
- `wat_lim_n_clean`;
- `wat_unimp_n_clean`;
- `wat_sur_n_clean`.

I displayed the results as a **100% stacked column chart** because the four service levels represent the complete national access distribution.

### Findings

At least basic service dominates most population-size groups. However, limited, unimproved and surface-water access remain visible in selected categories.

The chart does not show a consistent progression in which basic access automatically increases or decreases with national population size. High basic access appears among small, medium and large population groups.

Some population-size categories also contain substantial non-basic access, but these cases do not form a stable population-size pattern.

### Interpretation

I concluded that national population size alone is not a reliable indicator of drinking-water service quality.

Countries with very different population sizes can achieve strong basic access, while countries with similar population sizes can have substantially different service distributions.

---

## 04 — Urban Distribution of Access by Service Level

![Urban drinking-water service-level distribution](./04_urban_service_levels_distribution.png)

### Purpose

I created this visualization to examine urban drinking-water access across countries with different urban-population shares.

### Methodology

I rounded the urban-population share to the nearest whole percentage and grouped countries with the same rounded value.

I then calculated the average of four cleaned urban service-level variables:

- `wat_bas_u_clean`;
- `wat_lim_u_clean`;
- `wat_unimp_u_clean`;
- `wat_sur_u_clean`.

I used a **100% stacked column chart** to show the average service composition of every represented urban-population-share category.

### Findings

Across the available urban observations:

- At least basic: approximately **94.69%**
- Limited: approximately **3.28%**
- Unimproved: approximately **1.72%**
- Surface water: approximately **0.31%**

At least basic service dominates almost every urban-population-share category. Limited and unimproved access remain visible in selected groups, while surface-water reliance is nearly absent.

The most urbanized categories are almost entirely composed of at least basic service. Nevertheless, strong basic access also appears at lower urban-population shares.

### Interpretation

I found that higher urbanization is generally associated with stronger urban basic access, but the relationship is not perfectly linear.

I therefore interpret urbanization as an associated structural factor rather than as a complete or causal explanation of service quality.

---

## 05 — Rural Distribution of Access by Service Level

![Rural drinking-water service-level distribution](./05_rural_service_levels_distribution.png)

### Purpose

I created this visualization to examine rural drinking-water access across countries with different rural-population shares.

### Methodology

I calculated rural population share as:

`pop_r = 100 - pop_u`

I then rounded `pop_r` to the nearest whole percentage and grouped countries with the same rounded rural-population share.

For each represented category, I calculated the average of:

- `wat_bas_r_clean`;
- `wat_lim_r_clean`;
- `wat_unimp_r_clean`;
- `wat_sur_r_clean`.

### Findings

Across the available rural observations:

- At least basic: approximately **81.34%**
- Limited: approximately **5.84%**
- Unimproved: approximately **8.73%**
- Surface water: approximately **4.22%**

At least basic service remains dominant in many rural categories, but its share is lower and considerably more variable than in the urban chart.

Limited, unimproved and surface-water access are also more visible. Some categories show substantial dependence on unimproved sources or surface water.

### Interpretation

I found that rural populations experience lower average basic access and greater cross-country inequality than urban populations.

However, some highly rural countries retain near-universal basic access. Rural population share is therefore associated with larger service gaps, but it does not determine the outcome by itself.

---

## 06 — Average National Drinking-Water Access by Income Group

![Average national drinking-water access by income group](./06_income_group_vs_service_levels.png)

### Purpose

I created this chart to compare average national drinking-water service levels across income classifications.

### Methodology

I used a pivot table grouped by `income_group` and calculated the average national share of:

- At least basic access
- Limited access
- Unimproved access
- Surface-water access

I used `income_group_num` to arrange the categories logically from low income to high income.

I treated `NAN` separately because it represents countries or territories without an available income classification.

### Findings

| Income group | At least basic | Limited | Unimproved | Surface water |
|---|---:|---:|---:|---:|
| Low income | 62.82% | 16.55% | 15.21% | 5.42% |
| Lower middle income | 82.21% | 5.69% | 7.90% | 4.29% |
| Upper middle income | 96.43% | 1.56% | 1.48% | 0.57% |
| High income | 99.56% | 0.18% | 0.24% | 0.02% |

Average at least basic access increases consistently across the ordered income groups. Limited, unimproved and surface-water access decline sharply over the same progression.

### Interpretation

I found a strong descriptive association between income classification and national drinking-water access.

However, the pivot table does not prove causality or isolate the effect of income from urbanization, infrastructure, governance, geography or other structural conditions.

---

## Visual Storyline

Together, the six visualizations support the following analytical storyline:

1. National population size does not show a stable relationship with urbanization structure.
2. National population size alone does not explain drinking-water service quality.
3. Urban populations generally have the strongest and most consistent access.
4. Rural populations experience the largest and most variable remaining gaps.
5. National results generally fall between urban and rural distributions.
6. Income classification has one of the clearest descriptive associations with national access quality.

Overall, I found that drinking-water inequality is associated more clearly with area type and socioeconomic classification than with population size alone.

---

## Methodological Considerations

I considered the following limitations when interpreting the visuals:

- The analysis uses country or territory observations.
- The service averages are not weighted by population size.
- Rounded population shares group countries into percentage categories.
- Different categories can contain different numbers of countries.
- Records with missing service values may be excluded.
- The analysis covers 2020 only.
- The findings describe associations and do not establish causality.

---

## Notes

- I completed the calculations, transformations, aggregations and visualizations in Google Sheets.
- I used consistent service-level colours across the national, urban, rural and income-group charts.
- I stored the six principal visual outputs in this folder to support transparency and portfolio review.
- I reference these visuals in the main Part 1 README and analytical report.
