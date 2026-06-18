# Visual Assets — Part 1: Understanding the Data

This folder contains the main visual outputs created during the exploratory analysis of global drinking water access in 2020.

The visuals were designed to support the analysis of population structure, urban-rural differences, service-level distribution, and the relationship between income group and water access quality.

Each chart contributes to a specific part of the analytical workflow, moving from population-level exploration to service-level comparison and socioeconomic segmentation.

---

## 01 — Population vs Urban/Rural Share

![Population vs Urban/Rural Share](./01-population-vs-urban-rural-share.png)

This visual compares national population size with urban and rural population shares.

The chart shows that population size alone does not explain whether a country is more urban or more rural. Countries with similar population sizes can have very different urban-rural structures. This makes population size an insufficient standalone variable for explaining water access patterns.

**Main insight:**
National population size does not show a stable or direct relationship with urbanization structure. Urban and rural shares vary widely across countries, which means additional factors such as income level, geography, infrastructure, and development conditions are needed to explain water access outcomes.

---

## 02 — Urban Distribution of Access to Water per Service Level

![Urban Service Levels Distribution](./02_urban_service_levels_distribution.png)

This visual shows the distribution of urban drinking water access across four service levels:

* At least basic
* Limited
* Unimproved
* Surface water

The chart highlights that at least basic drinking water access dominates most urban observations. Limited and unimproved access appear only in selected cases, while surface water access is nearly absent in most urban areas.

**Main insight:**
Urban populations generally have strong access to at least basic drinking water services. However, some countries still show urban access gaps, especially through limited and unimproved service categories. This indicates that urbanization improves access conditions in many cases, but it does not automatically guarantee universal basic service.

---

## 03 — Rural Distribution of Access to Water per Service Level

![Rural Service Levels Distribution](./03_rural_service_levels_distribution.png)

This visual shows the distribution of rural drinking water access across the same four service levels:

* At least basic
* Limited
* Unimproved
* Surface water

Compared with the urban distribution, the rural chart shows a much more unequal access pattern. Rural basic access remains important, but limited, unimproved, and surface water categories are more visible and more frequent.

**Main insight:**
Rural populations are more exposed to lower service levels than urban populations. The visual shows that rural access is less stable and more unequal, with stronger presence of limited, unimproved, and surface-water reliance in selected countries.

---

## 04 — Income Group vs Service Levels

![Income Group vs Service Levels](./04_income_group_vs_service_levels.png)

This visual analyzes the relationship between income group and national drinking water access quality.

The chart compares average national access shares across income groups, showing how the distribution of at least basic, limited, unimproved, and surface water access changes as income level increases.

**Main insight:**
Income group is strongly associated with drinking water access quality. Low-income countries show the lowest average basic access and the highest exposure to limited, unimproved, and surface-water categories. As income level increases, basic access rises sharply, while lower service levels decline toward zero.

---

## Visual Storyline

Together, these visuals support a clear analytical storyline:

1. Population size alone does not explain water access patterns.
2. Urban areas generally show stronger and more stable access to at least basic drinking water.
3. Rural areas show greater inequality and higher exposure to lower service levels.
4. Income group is one of the strongest explanatory dimensions for national water access quality.

The visual analysis shows that drinking water access inequality is not only a population issue. It is strongly connected to area type, urban-rural structure, and socioeconomic classification.

---
## Notes

- These visuals were exported from the Google Sheets workbook used for data cleaning, feature engineering, pivot table analysis, and visual exploration.
- The spreadsheet remains the main analytical workspace where calculations, transformations, and aggregations were performed.
- The visuals are included in this folder to document the main findings and support the project reporting structure.
- The original PNG files are stored here to make the analysis easy to review directly from the GitHub repository.
- Some visuals may also be referenced inside README files to ensure they display clearly in the browser.
