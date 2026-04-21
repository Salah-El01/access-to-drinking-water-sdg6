# Reports

This folder contains the analytical report outputs produced for **Part 1 — Understanding the Data** of the **Access to Drinking Water (SDG 6)** project.

The reports document the first stage of the analysis using the **WHO/UNICEF Joint Monitoring Programme (JMP) 2020** drinking-water dataset. The objective of this stage was to understand the structure, consistency, and distribution of drinking-water access across countries before moving into deeper transformation and analytical work.

Rather than treating the dataset only as a table of percentages, this reporting stage was used to validate coverage, compare service levels across national, urban, and rural contexts, and identify the first major structural patterns in global access to drinking water.

## What this folder contains

### `Global_2020_Report.pdf`
This report presents the global descriptive analysis of the dataset.

It focuses on:
- dataset coverage and population consistency checks,
- national, rural, and urban drinking-water service indicators,
- measures of central tendency and spread,
- interpretation of variability across countries,
- first comparative insights across area types.

A key result from this report is that the dataset is highly consistent with official global population estimates, with only a very small difference from the estimated 2020 world population. It also shows that while national and especially urban basic access are generally high, inequality remains visible because a smaller group of countries still records low access levels or higher reliance on lower-quality services. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

---

### `Urban_2020_Report.pdf`
This report isolates the **urban** service-level structure and examines how drinking-water access behaves when grouped by urban population share.

It highlights that:
- urban basic access is generally very high,
- the urban distribution is relatively tight across countries,
- limited, unimproved, and surface-water reliance are usually low,
- only a small number of countries deviate substantially from the dominant pattern. :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

This report supports one of the core conclusions of Part 1: **urban areas tend to show stronger and more homogeneous access outcomes than rural areas**.

---

### `Rural_2020_Report.pdf`
This report focuses on the **rural** side of the dataset and is essential for understanding where deprivation is concentrated.

Its main contribution is to show that:
- rural access is much more uneven across countries,
- rural basic service can still be high in some cases,
- but limited, unimproved, and surface-water categories appear much more strongly in rural areas,
- the spread and variation are substantially larger than in urban settings. :contentReference[oaicite:4]{index=4}

This report makes clear that the **rural gap is the principal source of inequality in drinking-water access** across the dataset. That point is also reflected in the final executive summary. :contentReference[oaicite:5]{index=5}

---

### `Pivot_Table.pdf`
This report summarizes the relationship between **income group** and national drinking-water service levels.

It shows a strong income gradient:
- low-income countries have the lowest average basic access,
- lower-middle-income countries improve but still retain sizeable unsafe-service shares,
- upper-middle-income and high-income countries approach universal basic access,
- limited, unimproved, and surface-water shares decrease sharply as income rises. :contentReference[oaicite:6]{index=6}

The pattern is very clear in the results:
- low income: basic access ≈ **62.8%**
- lower middle income: basic access ≈ **82.2%**
- upper middle income: basic access ≈ **96.4%**
- high income: basic access ≈ **99.6%** :contentReference[oaicite:7]{index=7} :contentReference[oaicite:8]{index=8}

This report provides the strongest quantitative evidence in Part 1 that **income level is closely associated with water-service quality**.

---

### `Part1_Full_Report.pdf`
This is the consolidated report for Part 1.

It brings together:
- the data cleaning and validation logic,
- descriptive statistics,
- area-based comparisons,
- population-share visualizations,
- income-group analysis,
- and an executive summary of the main findings.

The full report defines the scope as **214 countries/areas** and summarizes the main conclusions of Part 1:
- urban access is consistently stronger than rural access,
- rural deprivation is the main driver of the overall gap,
- low-income countries face the highest concentration of unsafe service categories,
- and the service-level shares pass a key quality check by summing to approximately 100% where data are complete. :contentReference[oaicite:9]{index=9}

It also records the main deliverables completed in this phase:
- cleaning and validating the JMP export,
- engineering population features,
- producing descriptive statistics and 100% stacked composition charts,
- and building the income-group pivot analysis. :contentReference[oaicite:10]{index=10}

---

## Analytical value of this reporting stage

These reports do more than summarize charts. Together, they establish the analytical foundation for the rest of the project.

This first stage was important for:
- verifying that the dataset is trustworthy enough for analysis,
- identifying the dominant structural inequalities in access,
- distinguishing area effects from population-size effects,
- quantifying the income gradient in drinking-water service quality,
- and documenting the logic of the exploratory work in a reproducible way.

In practical terms, Part 1 shows that the global drinking-water challenge is not simply a matter of average access. The real issue lies in **distribution**:
- between urban and rural areas,
- between richer and poorer countries,
- and between countries close to universal coverage and those still facing serious basic-service deficits.

## Key takeaways from Part 1

- The dataset provides near-complete global coverage and is highly consistent with 2020 population benchmarks. :contentReference[oaicite:11]{index=11}
- National access to at least basic drinking water is high in many countries, but this masks strong disparities. :contentReference[oaicite:12]{index=12}
- Urban access is generally stronger and more stable across countries than rural access. :contentReference[oaicite:13]{index=13}
- Rural areas contain a much larger share of the “problem” service levels: limited, unimproved, and surface water. :contentReference[oaicite:14]{index=14}
- Income group is one of the strongest explanatory dimensions in the dataset, with clear improvement in service quality as income rises. :contentReference[oaicite:15]{index=15}

## Position of this folder in the project

This folder represents the **reporting layer** of Part 1. It captures the outputs of the exploratory and descriptive analysis conducted before the transformation-focused work in Part 2.

If the `data/` folder stores the cleaned analytical material and the `assets/` folder stores the visual outputs, the `reports/` folder is where the project’s first analytical conclusions are formally documented.
