# Part 1 Analytical Report — Access to Drinking Water

## 1. Executive Summary

This report presents the first part of the **Access to Drinking Water** data analysis project. The analysis focuses on understanding global drinking water access in 2020 using spreadsheet-based data cleaning, feature engineering, statistical summaries, pivot table analysis, and visual exploration.

The project investigates how drinking water access varies across:

- national population size
- urban and rural population structures
- service-level categories
- country income groups

The analysis shows that access to at least basic drinking water is generally high at the national and urban levels. However, important inequalities remain, especially in rural areas and lower-income countries.

Rural populations show greater exposure to limited, unimproved, and surface-water services, while income group appears to be one of the strongest explanatory dimensions for national water access quality.

---

## 2. Working Spreadsheet

The full analysis was performed in Google Sheets.

[Open Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

The workbook includes the main dataset, transformation columns, summary tables, pivot table analysis, and visualizations used throughout this report.

---

## 3. Analytical Objective

The objective of this analysis was to explore global drinking water access patterns and identify the main differences between population groups and socioeconomic categories.

The analysis focused on four key questions:

1. How does national population size relate to urban and rural population shares?
2. How is drinking water access distributed across national, urban, and rural populations?
3. Are urban and rural populations exposed to different levels of water access inequality?
4. How does income group relate to national drinking water access quality?

---

## 4. Dataset Overview

The dataset contains country-level estimates for drinking water access in 2020.

The main dimensions used in the analysis include:

| Variable | Description |
|---|---|
| `name` | Country or area name |
| `income_group` | Country income classification |
| `pop_n` | National population size estimate, measured in thousands |
| `pop_u` | Urban population share, measured as a percentage |
| `wat_bas_n` | National share with at least basic drinking water access |
| `wat_lim_n` | National share with limited drinking water access |
| `wat_unimp_n` | National share with unimproved drinking water access |
| `wat_sur_n` | National share relying on surface water |
| `wat_bas_r` | Rural share with at least basic drinking water access |
| `wat_lim_r` | Rural share with limited drinking water access |
| `wat_unimp_r` | Rural share with unimproved drinking water access |
| `wat_sur_r` | Rural share relying on surface water |
| `wat_bas_u` | Urban share with at least basic drinking water access |
| `wat_lim_u` | Urban share with limited drinking water access |
| `wat_unimp_u` | Urban share with unimproved drinking water access |
| `wat_sur_u` | Urban share relying on surface water |

The water access variables are grouped into four service levels:

- **At least basic**
- **Limited**
- **Unimproved**
- **Surface water**

These categories allow comparison between higher-quality and lower-quality drinking water access levels across different population groups.

---

## 5. Tools Used

The project was completed using Google Sheets as the main analytical workspace.

Main tools and techniques used:

- spreadsheet data cleaning
- row validation
- formula-based feature engineering
- missing value handling
- percentage-based calculations
- summary statistics
- pivot tables
- 100% stacked column charts
- line charts
- box-and-whisker style analysis
- visual interpretation
- analytical reporting

---

## 6. Data Preparation and Feature Engineering

Several derived features were created to support analysis, validation, aggregation, and visualization.

---

### 6.1 Row Validation

A row validation field was created to check whether each row contained the expected number of values.

Example logic:

    value_cnt = COUNTA(row_range)

This helped identify rows affected by import or formatting issues.

The purpose of this step was to make sure the dataset structure was consistent before performing calculations and visual analysis.

---

### 6.2 Urban Population Estimate

The dataset provides national population size and urban population share. To estimate the urban population count, a derived variable was created:

    pop_u_val = pop_n * pop_u / 100

Since `pop_n` is measured in thousands, the resulting urban population estimate is also interpreted in thousands.

This feature made it possible to compare the dataset’s urban population with broader population estimates and to analyze urban population distribution more precisely.

---

### 6.3 Rural Population Share

The dataset provides urban population share, but rural population share was derived as the complement of urban share:

    pop_r = 100 - pop_u

This created a direct rural population-share variable and allowed comparison between urban and rural population structures.

Because urban and rural shares represent two complementary population categories, their combined value should equal 100%.

---

### 6.4 Rounded Population Variables

Rounded variables were created to improve chart readability and aggregation.

Examples:

    pop_u_rounded = ROUND(pop_u)

    pop_r_rounded = ROUND(pop_r)

Rounded variables made it easier to group observations in 100% stacked column charts and reduce excessive visual noise caused by too many unique percentage values.

This improved the interpretability of the urban and rural distribution charts.

---

### 6.5 Cleaned Water Access Variables

Cleaned versions of the water access variables were used in visualizations to reduce issues caused by missing values, text values, or inconsistent percentage values.

These cleaned fields supported more stable charts and clearer interpretation.

Examples of cleaned fields include:

- `wat_bas_n_clean`
- `wat_lim_n_clean`
- `wat_unimp_n_clean`
- `wat_sur_n_clean`
- `wat_bas_u_clean`
- `wat_lim_u_clean`
- `wat_unimp_u_clean`
- `wat_sur_u_clean`
- `wat_bas_r`
- `wat_lim_r`
- `wat_unimp_r`
- `wat_sur_r`

Cleaning the variables helped keep the visual outputs focused on valid numeric values and reduced distortion from missing or invalid entries.

---

## 7. Global 2020 Report Analysis

The Global 2020 Report sheet provides the main overview of the dataset. It combines population analysis, urban-rural structure, summary statistics, and national water access distribution.

---

### 7.1 Population vs Urban/Rural Share

![Population vs Urban/Rural Share](../../assets/01-population-vs-urban-rural-share.png)

This visual compares national population size with urban and rural population shares.

The urban and rural share lines move in opposite directions because rural share is derived from urban share:

    rural share = 100 - urban share

The chart shows that countries with similar population sizes can have very different urban-rural structures. Some countries with smaller populations are highly urbanized, while others remain largely rural. The same variation appears among medium and large population countries.

The key finding is that **national population size alone does not explain urbanization structure**.

This is important because water access outcomes cannot be understood only through population size. Other factors such as infrastructure, geography, income level, and development conditions are also important.

---

### 7.2 Statistical Summary of Water Access Features

The global analysis includes summary statistics for the 12 water access variables:

- national basic, limited, unimproved, and surface water access
- rural basic, limited, unimproved, and surface water access
- urban basic, limited, unimproved, and surface water access

The calculated statistics include:

- maximum
- minimum
- mean
- median
- mode
- first quartile
- third quartile
- interquartile range
- standard deviation

This summary provides a deeper understanding of both central tendency and variability.

Key values from the analysis include:

| Feature | Mean | Median | IQR | Interpretation |
|---|---:|---:|---:|---|
| `wat_bas_n` | 89.86% | 97.35% | 14.24 | National basic access is generally high |
| `wat_bas_r` | 81.34% | 90.73% | 34.29 | Rural basic access is lower and more variable |
| `wat_bas_u` | 94.69% | 98.11% | 7.39 | Urban basic access is high and stable |
| `wat_sur_r` | 4.22% | 0.22% | 6.16 | Rural surface-water reliance is low overall but important in selected countries |
| `wat_sur_u` | 0.31% | 0.00% | 0.16 | Urban surface-water reliance is nearly absent |

The strongest statistical insight is that **urban basic access is the most stable**, while **rural basic access shows the greatest variability**.

---

### 7.3 Access by Area Type

The box-and-whisker style analysis compares the distribution of water access across national, rural, and urban populations.

The strongest findings are:

1. **Basic access is generally high across all area types.**  
   Most countries show high access to at least basic drinking water services.

2. **Urban access is the strongest and most consistent.**  
   Urban basic access has the highest average and the smallest spread.

3. **Rural access is the most unequal.**  
   Rural basic access has a much larger interquartile range, showing greater variation between countries.

4. **Surface water is mostly a rural issue.**  
   Urban surface-water access is almost zero in most countries, while rural surface-water access remains visible in selected cases.

The key analytical conclusion is that national averages can hide important rural inequalities. Urban populations generally benefit from stronger and more stable water access, while rural populations remain more exposed to lower service levels.

---

### 7.4 National Distribution of Access to Water per Service Level

The national distribution analysis examines drinking water access across four service levels in relation to national population size.

The chart shows that at least basic access dominates most observations. Limited, unimproved, and surface-water categories are smaller but still visible in selected countries.

The main conclusion is that **population size alone is not a strong predictor of water access quality**. Countries with different population sizes can still show high basic access, while lower service levels appear in specific contexts.

This suggests that structural and socioeconomic factors are more important than population size alone when explaining drinking water access inequality.

---

## 8. Urban 2020 Report Analysis

![Urban Service Levels Distribution](../../assets/02_urban_service_levels_distribution.png)

The Urban 2020 Report isolates urban drinking water access and shows how urban populations are distributed across the four service levels.

---

### 8.1 Main Urban Access Pattern

The strongest pattern is that **urban basic drinking water access dominates almost all observations**.

Most urban populations have access to at least basic drinking water services. Limited, unimproved, and surface-water categories appear as much smaller shares.

This confirms that urban areas generally have stronger access conditions than rural areas.

---

### 8.2 Limited and Unimproved Urban Access

Limited and unimproved access are not widespread across the full urban dataset, but they remain visible in selected countries.

This is analytically important because urbanization does not automatically guarantee universal basic service.

Some countries still show meaningful urban access gaps, especially where infrastructure coverage or service reliability remains limited.

The key interpretation is:

> Urban populations generally have strong access to basic drinking water, but selected countries still face urban service gaps.

---

### 8.3 Surface Water in Urban Areas

Surface water access is almost absent in most urban observations.

This is a positive finding because surface water represents the lowest service level. However, a small number of countries still show measurable urban reliance on surface water.

The main insight is that urban surface-water dependence is rare, but not completely eliminated.

---

### 8.4 Urban Analysis Conclusion

Urban drinking water access is generally strong and stable. At least basic access dominates, while limited, unimproved, and surface-water categories remain concentrated in selected countries.

The analysis suggests that urbanization is associated with better access outcomes, but it is not sufficient on its own to guarantee universal basic access.

---

## 9. Rural 2020 Report Analysis

![Rural Service Levels Distribution](../../assets/03_rural_service_levels_distribution.png)

The Rural 2020 Report focuses on rural drinking water access and highlights the differences between rural and urban service-level distributions.

---

### 9.1 Main Rural Access Pattern

Rural basic access remains the largest category in many observations, but it is less stable than urban basic access.

Compared with the urban chart, the rural visual shows:

- more visible limited access
- more frequent unimproved access
- higher exposure to surface-water reliance
- greater variation between countries

This indicates that rural populations experience more unequal access conditions.

---

### 9.2 Limited Rural Access

Limited access is more visible in the rural distribution than in the urban distribution.

This means that rural populations are more likely to face reduced service quality, even when some level of water access exists.

Limited rural access is not universal, but it appears strongly enough to indicate a structural rural disadvantage.

---

### 9.3 Unimproved Rural Access

Unimproved rural access is one of the clearest inequality signals in the analysis.

The rural chart shows that some countries still have meaningful shares of rural populations relying on unimproved water sources.

This reveals that rural water access problems are not only about coverage, but also about the quality and reliability of available services.

---

### 9.4 Surface Water in Rural Areas

Surface water access is more visible in rural areas than in urban areas.

This matters because surface water represents the lowest service category and often signals severe access limitations.

Although surface water is not dominant in most countries, its presence in rural areas highlights the continued vulnerability of selected rural populations.

---

### 9.5 Rural Analysis Conclusion

Rural water access is significantly more unequal than urban water access.

The main conclusion is:

> Rural populations are more exposed to limited, unimproved, and surface-water services, while urban populations show stronger and more stable access to at least basic drinking water.

This urban-rural gap is one of the central findings of the project.

---

## 10. Income Group and Pivot Table Analysis

![Income Group vs Service Levels](../../assets/04_income_group_vs_service_levels.png)

The pivot table analysis examines how national drinking water access varies across income groups.

Income group is a powerful segmentation variable because it reflects broader socioeconomic capacity, infrastructure investment potential, and service delivery conditions.

---

### 10.1 Pivot Table Methodology

The pivot table groups countries by income classification and calculates:

- total national population by income group
- average urban population share
- average national basic access
- average national limited access
- average national unimproved access
- average national surface-water access

This approach reduces country-level complexity into income-based patterns and makes the relationship between socioeconomic classification and water access easier to interpret.

---

### 10.2 Basic Access by Income Group

The strongest finding is that average basic access increases sharply with income level.

| Income Group | Average Basic Access |
|---|---:|
| Low income | 62.82% |
| Lower middle income | 82.21% |
| Upper middle income | 96.43% |
| High income | 99.56% |

This shows a clear income gradient. Low-income countries have the lowest average basic access, while high-income countries are close to universal basic access.

The key interpretation is:

> Higher income groups are associated with stronger access to at least basic drinking water services.

---

### 10.3 Non-Basic Access by Income Group

Low-income countries show the highest exposure to lower service levels:

| Income Group | Limited | Unimproved | Surface Water |
|---|---:|---:|---:|
| Low income | 16.55% | 15.21% | 5.42% |
| Lower middle income | 5.69% | 7.90% | 4.29% |
| Upper middle income | 1.56% | 1.48% | 0.57% |
| High income | 0.18% | 0.24% | 0.02% |

This confirms that lower-income countries carry the largest burden of limited, unimproved, and surface-water access.

As income level increases, non-basic service categories decline sharply.

---

### 10.4 Urbanization by Income Group

The pivot table also shows that average urban population share increases with income level.

| Income Group | Average Urban Population Share |
|---|---:|
| Low income | 36.04% |
| Lower middle income | 48.79% |
| Upper middle income | 64.69% |
| High income | 79.36% |

This suggests that higher-income countries tend to be more urbanized, and higher urbanization may support stronger infrastructure coverage.

However, income group should not be interpreted only through urbanization. Income level also reflects financial capacity, infrastructure investment, governance, and service maintenance ability.

---

### 10.5 Income Group Analysis Conclusion

The pivot table provides one of the strongest explanatory findings in the project.

Basic access rises consistently from low-income to high-income countries, while limited, unimproved, and surface-water access decline toward zero.

The main conclusion is:

> Income group is strongly associated with national drinking water access quality.

---

## 11. Cross-Sheet Findings

The four analysis sheets together support a clear analytical storyline.

---

### Finding 1: National Basic Access Is Generally High

Across the dataset, at least basic drinking water access is the dominant service level at the national scale.

Most countries show high basic-access shares, while limited, unimproved, and surface-water categories are smaller.

---

### Finding 2: Urban Areas Show the Strongest Access Profile

Urban populations have the highest and most stable access to at least basic drinking water.

Urban surface-water access is nearly absent in most countries, and limited or unimproved access appears mainly in selected cases.

---

### Finding 3: Rural Areas Show Greater Inequality

Rural populations are more exposed to limited, unimproved, and surface-water services.

Rural basic access is common, but it is less stable and more variable than urban basic access.

---

### Finding 4: Population Size Alone Does Not Explain Water Access Quality

The population-based visuals do not show a clear direct relationship between population size and service-level quality.

This suggests that population size is not sufficient as a standalone explanatory factor.

---

### Finding 5: Income Group Is Strongly Associated With Access Quality

Income group shows one of the clearest relationships in the analysis.

Basic access increases from low-income to high-income countries, while lower service levels decline sharply.

---

## 12. Limitations

This analysis is descriptive and exploratory. It identifies patterns and associations, but it does not prove causality.

Key limitations include:

- The analysis is based on 2020 estimates only.
- Missing values may affect some country-level comparisons.
- Some variables required cleaning or transformation before visualization.
- Population size alone does not capture infrastructure quality, governance, geography, or investment capacity.
- Income group is useful for segmentation, but it does not explain all country-level differences.
- Spreadsheet-based analysis is effective for exploration, but more advanced modeling would require a reproducible coding environment such as Python or R.

---

## 13. Future Improvements

Several improvements could strengthen the project further:

- add regional segmentation to compare water access by world region
- calculate population-weighted access indicators
- compare changes across multiple years
- build an interactive dashboard
- reproduce the analysis in Python for stronger reproducibility
- create regression or clustering models to identify stronger predictors of access inequality
- add country-level ranking tables for lowest basic access and highest surface-water reliance

---

## 14. Final Conclusion

This analysis shows that global drinking water access is generally strong at the national and urban levels, but important inequalities remain.

Urban populations usually have the strongest and most stable access to at least basic drinking water. Rural populations show greater variation and higher exposure to limited, unimproved, and surface-water services.

Income group is the strongest explanatory dimension identified in this part of the project. Low-income countries show the lowest average basic access and the highest exposure to lower service levels, while high-income countries approach universal basic access.

The main analytical conclusion is:

> Drinking water access inequality is not explained by population size alone. It is more strongly connected to area type, rural-urban structure, and socioeconomic classification.

This makes the project a useful case study in data cleaning, feature engineering, statistical analysis, pivot table analysis, visualization, and data storytelling using Google Sheets.
