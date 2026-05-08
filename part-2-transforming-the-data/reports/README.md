# Reports

This folder contains the analytical report outputs produced for **Part 2 — Transforming the Data** of the **Access to Drinking Water (SDG 6)** project.

The reports document the second stage of the analysis using the **WHO/UNICEF Joint Monitoring Programme (JMP) drinking-water access estimates (2000–2020)**. The objective of this stage was to transform the dataset into an analysis-ready structure for measuring progress in access to at least basic drinking-water services over time.

While Part 1 focused on understanding the 2020 snapshot of access inequalities, Part 2 focuses on calculating and interpreting change. This was done through year-difference checks, Annual Rate of Change calculations, full-access classifications, rural–urban progress comparisons, and regional enrichment.

## What this folder contains

### `Estimates of the use of water (2000-2020).pdf`
[Estimates of the use of water (2000-2020).pdf](https://github.com/user-attachments/files/27533980/Estimates.of.the.use.of.water.2000-2020.pdf)

This report exports the main transformed working dataset used in Part 2.

It contains the original WHO/UNICEF JMP drinking-water indicators together with the engineered variables created during the transformation workflow, including:

- year-difference checks,
- Annual Rate of Change calculations,
- rounded basic-access indicators,
- full-access classifications,
- regional grouping,
- rural–urban ARC difference.

This report provides the row-level evidence behind the Part 2 analysis and shows how the original dataset was converted into an analysis-ready structure for measuring progress between 2015 and 2020.

---

### `Summary.pdf`
[Summary.pdf](https://github.com/user-attachments/files/27534167/Summary.pdf)

This report presents the main analytical summary for Part 2.

It documents:

- year representation in the dataset,
- year-difference statistics,
- Annual Rate of Change summaries,
- missing ARC values,
- full-access cases,
- countries with positive, zero, or negative ARC,
- rural–urban ARC differences,
- regional aggregation of population and ARC values,
- charts used to interpret progress across regions.

A key result from this report is that the dataset is mainly structured around 2015 and 2020 observations, meaning that Part 2 is best interpreted as a mostly five-year comparison rather than a complete annual time-series analysis.

The report also shows that rural ARC is higher on average than urban ARC. This suggests that rural access often improved faster during the period, although this must be interpreted carefully because many urban areas were already close to, or had already reached, full basic access.

---

### `Regions.pdf`
[Regions.pdf](https://github.com/user-attachments/files/27534216/Regions.pdf)

This report documents the country-to-region lookup table used in Part 2.

It assigns each country or area in the dataset to a regional group, including:

- East Asia & Pacific,
- Europe & Central Asia,
- Latin America & Caribbean,
- Middle East & North Africa,
- North America,
- South Asia,
- Sub-Saharan Africa.

This regional lookup layer made it possible to enrich the transformed dataset with a region field and to compare progress across regions. It supports the regional summary tables and visualizations presented in the summary report.

---

## Analytical value of this reporting stage

These reports document the transition from basic dataset exploration to transformation-driven analysis.

This second stage was important for:

- checking whether the dataset could support time-based comparison,
- creating reliable year-difference fields,
- calculating Annual Rates of Change for national, rural, and urban access,
- distinguishing countries with no ARC value from countries already at full access,
- avoiding misleading interpretation of zero change,
- comparing rural and urban progress,
- enriching the dataset with regional classifications,
- and summarizing progress at the regional level.

In practical terms, Part 2 shows that progress in drinking-water access is not only about current coverage levels. It is also about the **speed of improvement** and whether regions with larger access gaps are improving fast enough.

## Key takeaways from Part 2

- The dataset is mainly concentrated around 2015 and 2020 observations.
- The average year difference is close to five years, so the analysis is mostly a five-year comparison.
- Annual Rate of Change was calculated for national, rural, and urban access to at least basic drinking-water services.
- Full-access countries needed to be treated separately so that zero change would not be misread as lack of progress.
- Rural ARC is generally higher than urban ARC, suggesting rural catch-up in several regions.
- Regional comparison shows that progress is uneven across the world.
- Sub-Saharan Africa and South Asia are especially important because they combine large populations, major access challenges, and relatively strong improvement rates.

## Role of these reports

Together, these reports provide the formal documentation of the Part 2 transformation workflow.

They show how the original JMP dataset was converted into a progress-analysis dataset through year-difference checks, ARC calculations, full-access classifications, rural–urban comparison, and regional enrichment.
