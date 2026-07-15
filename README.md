# Access to Drinking Water — SDG 6 Data Analysis Project

## Project Overview

This repository presents a two-part data analysis project focused on global access to drinking water, connected to **United Nations Sustainable Development Goal 6: Clean Water and Sanitation**.

The project analyzes drinking-water access using country- and area-level estimates from the **WHO/UNICEF Joint Monitoring Programme (JMP)**.

The work is divided into two complementary parts:

1. **Part 1 — Understanding the Data**  
   A 2020 snapshot analysis focused on data cleaning, population representation, service-level access, urban-rural differences, population-size patterns, and income-group comparison.

2. **Part 2 — Transforming the Data**  
   A 2000–2020 progress analysis focused on feature engineering, Annual Rate of Change calculation, full-access classification, rural-urban progress comparison, regional aggregation, and visual storytelling.

Together, both parts move from descriptive analysis to progress-monitoring analysis.

---

## Analytical Goal

The main goal of this project is to understand and communicate patterns in access to drinking water across countries, areas, income groups, population sizes, and regions.

The project answers questions such as:

- How well does the dataset represent global population and urbanization?
- How does access to drinking water differ between national, rural, and urban populations?
- Are lower service levels more concentrated in rural areas?
- Is income group associated with drinking-water access quality?
- How has access to at least basic drinking water changed over time?
- Are rural areas catching up with urban areas?
- Which regions show stronger or weaker progress?
- How should progress be interpreted alongside baseline access and population scale?

---

## Repository Structure

```text
access-to-drinking-water-sdg6/
├── part-1-understanding-the-data/
│   ├── assets/
│   ├── data/
│   ├── reports/
│   └── README.md
│
├── part-2-transforming-the-data/
│   ├── assets/
│   ├── data/
│   ├── reports/
│   └── README.md
│
└── README.md
```

---

# Part 1 — Understanding the Data

[Open Part 1](./part-1-understanding-the-data/)

## Objective

Part 1 focuses on understanding the 2020 drinking-water access dataset.

The analysis begins with data import and cleaning, then moves into population analysis, service-level distributions, urban-rural comparison, population-size patterns, and income-group analysis.

The main purpose of Part 1 is to answer:

> What does access to drinking water look like in 2020, and how does it differ across population areas, income groups, and population-size patterns?

---

## Part 1 Working Spreadsheet

[Open Part 1 Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1pCvSjxteW4hK8SEjsLpVBqPaN8d4gcre0Xm61JzAP44/edit?usp=sharing)

---

## Part 1 Dataset Scope

Part 1 uses the 2020 drinking-water access dataset.

The original dataset contains 16 features, including:

| Variable group | Description |
|---|---|
| `name` | Country or area name |
| `income_group` | Country income classification |
| `pop_n` | National population estimate, stored in thousands |
| `pop_u` | Urban population share |
| `wat_bas_n`, `wat_bas_r`, `wat_bas_u` | At least basic drinking-water access |
| `wat_lim_*` | Limited drinking-water access |
| `wat_unimp_*` | Unimproved drinking-water access |
| `wat_sur_*` | Surface-water reliance |

The analysis created additional features such as:

- `value_cnt`
- `pop_u_val`
- `pop_r`
- `pop_n (m)`
- `wat_bas_n (rounded)`
- `pop_u (rounded)`
- `pop_r (rounded)`

These features support validation, population calculations, chart readability, and service-level interpretation.

---

## Part 1 Main Analysis Areas

### 1. Data Import and Cleaning

The dataset was imported into Google Sheets and validated to ensure the values were correctly separated into rows and columns.

A helper field, `value_cnt`, was created to count non-empty values per row and detect incorrectly imported records.

This helped identify rows affected by separator issues and ensured that all rows matched the expected 16-column structure.

---

### 2. Population Representation

The analysis compared the dataset population totals with estimated global population values.

Key transformations included:

```text
pop_u_val = pop_n × (pop_u / 100)
```

This enabled comparison between:

- dataset national population
- estimated world population
- dataset urban population
- estimated world urban population

Because `pop_n` is stored in thousands, unit conversion was necessary before comparing it with world population estimates.

---

### 3. Urban and Rural Population Share

A rural population share feature was created:

```text
pop_r = 100 - pop_u
```

This allowed comparison between urban and rural population shares.

A line chart was created to compare national population size with urban and rural population shares.

To improve readability, population values were also transformed into rounded millions using:

```text
pop_n (m)
```

---

### 4. Access by Area

The analysis compared the distribution of drinking-water access across:

- national populations
- rural populations
- urban populations

For each area, the analysis considered four service levels:

- at least basic
- limited
- unimproved
- surface water

Measures of central tendency and spread were calculated, including:

- maximum
- minimum
- mean
- median
- mode
- first quartile
- third quartile
- interquartile range
- standard deviation

A box-and-whisker style visual was used to compare distribution patterns across all 12 access features.

---

### 5. Access by Population Size

The analysis used 100% stacked column charts to examine how access to water service levels relates to:

- national population size
- urban population share
- rural population share

This helped assess whether access patterns were clearly explained by population size or area-type share.

The findings showed that population size alone does not strongly explain drinking-water access quality.

---

### 6. Access by Income Group

A pivot table was created to summarize income groups by:

- total national population
- average urban population share
- average national basic access
- average national limited access
- average national unimproved access
- average national surface-water access

Income groups were converted into ordered numerical categories to improve visualization and interpretation.

This analysis showed a strong relationship between income group and drinking-water access quality.

---

## Part 1 Key Visual Outputs

The Part 1 visual assets are stored here:

[Part 1 Assets](./part-1-understanding-the-data/assets/)

Main visuals include:

- population versus urban and rural share
- urban service-level distribution
- rural service-level distribution
- income group versus service-level access
- key findings summary table

---

## Part 1 Main Findings

1. **Most countries have high national access to at least basic drinking water.**

2. **Urban populations generally show stronger and more stable access than rural populations.**

3. **Rural areas show greater inequality and higher exposure to limited, unimproved, and surface-water services.**

4. **Population size alone does not clearly explain water-access patterns.**

5. **Income group is one of the strongest explanatory dimensions for national water-access quality.**

6. **Low-income countries show lower average basic access and higher exposure to limited, unimproved, and surface-water categories.**

7. **High-income countries show near-universal basic access and very low exposure to lower service levels.**

---

## Part 1 Reports

The Part 1 reporting section is available here:

[Part 1 Reports](./part-1-understanding-the-data/reports/)

Main analytical report:

[Part1_Analytical_Report.md](./part-1-understanding-the-data/reports/analytical_report/Part1_Analytical_Report.md)

Sheet exports:

[Part 1 Sheet Exports](./part-1-understanding-the-data/reports/sheet_exports/)

---

# Part 2 — Transforming the Data

[Open Part 2](./part-2-transforming-the-data/)

## Objective

Part 2 extends the analysis from a 2020 snapshot into a multi-year progress analysis.

The focus shifts from describing access levels to measuring change over time.

The main question becomes:

> Is access to at least basic drinking water improving, declining, or stagnating across countries, population areas, and regions?

The central metric used in Part 2 is **Annual Rate of Change (ARC)**.

---

## Part 2 Working Spreadsheet

[Open Part 2 Google Sheets Workbook](https://docs.google.com/spreadsheets/d/1weIUAGJtGo6sjmPyZFFgbhWa5AapxfpWcgB-moQ2_-s/edit?usp=sharing)

---

## Part 2 Dataset Scope

Part 2 uses a multi-year drinking-water access dataset covering observations between 2000 and 2020.

The dataset differs from Part 1 in two important ways:

| Part 1 | Part 2 |
|---|---|
| 2020 snapshot | 2000–2020 observations |
| Includes `income_group` | Removes `income_group` |
| No year-to-year comparison | Adds `year` |
| Descriptive access analysis | Progress-monitoring analysis |

The analytical grain is:

> One country or area observed in one specific year.

The dataset is not a complete annual panel. Most observations are concentrated around 2015 and 2020, with a small number of observations from intermediate years.

---

## Part 2 Transformation Workflow

```text
Source data
    ↓
Country and year sorting
    ↓
Year-difference calculation
    ↓
Annual Rate of Change calculation
    ↓
Missing-value and error handling
    ↓
Full-access classification
    ↓
Rural–urban ARC comparison
    ↓
Regional lookup and enrichment
    ↓
Summary tables and visual analysis
    ↓
Analytical reporting
```

---

## Part 2 Key Derived Features

### `y_diff`

Measures the number of years between two observations for the same country.

```text
y_diff = later year - earlier year
```

This feature supports:

- observation interval validation
- duplicate detection
- ARC calculation

---

### `ARC_n`

Annual Rate of Change in national access to at least basic drinking water.

```text
ARC_n =
(later national basic access - earlier national basic access)
/
year difference
```

---

### `ARC_r`

Annual Rate of Change in rural access to at least basic drinking water.

---

### `ARC_u`

Annual Rate of Change in urban access to at least basic drinking water.

All ARC values are interpreted in:

> Percentage points per year.

---

### Full-Access Flags

The following fields identify cases where access was approximately full in both observation years:

- `ARC_n_full`
- `ARC_r_full`
- `ARC_u_full`

These flags separate:

- zero ARC because access was already complete
- zero ARC because access did not improve below full coverage

This prevents misleading interpretation of zero values.

---

### `ARC_diff`

Compares rural and urban progress:

```text
ARC_diff = ARC_r - ARC_u
```

Interpretation:

- `ARC_diff > 0` — rural access improved faster
- `ARC_diff < 0` — urban access improved faster
- `ARC_diff ≈ 0` — rural and urban progress were similar

---

### `region`

Adds regional classification through lookup-based enrichment.

Regions analyzed:

- East Asia & Pacific
- Europe & Central Asia
- Latin America & Caribbean
- Middle East & North Africa
- North America
- South Asia
- Sub-Saharan Africa

---

## Part 2 Key Visual Outputs

The Part 2 visual assets are stored here:

[Part 2 Assets](./part-2-transforming-the-data/assets/)

Main visuals:

- year distribution histogram
- average rural-urban ARC difference by region
- average rural and urban ARC by region
- regional progress in basic water access with population scale

Supporting regional ARC tables are also included:

[Part 2 Regional ARC Tables](./part-2-transforming-the-data/assets/regional_arc_tables/)

---

## Part 2 Main Findings

1. **The dataset is mainly concentrated around 2015 and 2020.**

2. **The dataset is not a complete annual time series, so `y_diff` is required before calculating ARC.**

3. **Average rural ARC is higher than average urban ARC.**

4. **Rural access improved faster than urban access across all regions on average.**

5. **Faster rural progress does not mean rural access has surpassed urban access.**

6. **Urban ARC can be lower because many urban populations already had high or full access.**

7. **Full-access classification improves interpretation of zero ARC values.**

8. **Regional averages hide strong country-level variation.**

9. **Population size alone does not explain the speed of progress.**

10. **Sub-Saharan Africa and South Asia combine large population scale with meaningful progress indicators.**

---

## Part 2 Regional Summary

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

---

## Part 2 Reports

The Part 2 reporting section is available here:

[Part 2 Reports](./part-2-transforming-the-data/reports/)

Main analytical report:

[Part2_Analytical_Report.md](./part-2-transforming-the-data/reports/analytical_report/Part2_Analytical_Report.md)

Sheet exports:

[Part 2 Sheet Exports](./part-2-transforming-the-data/reports/sheet_exports/)

Data documentation:

[Part 2 Data Documentation](./part-2-transforming-the-data/data/)

Data dictionary:

[Part 2 Data Dictionary](./part-2-transforming-the-data/data/data_dictionary.md)

---

# Cross-Part Analytical Story

Part 1 and Part 2 work together as a complete data analysis project.

## Part 1 contribution

Part 1 establishes the baseline understanding of the 2020 dataset.

It shows that:

- urban access is generally stronger than rural access;
- rural populations are more exposed to lower service levels;
- income group is strongly associated with water-access quality;
- population size alone does not explain access patterns.

## Part 2 contribution

Part 2 adds the time dimension.

It shows that:

- access is generally improving;
- rural areas often improve faster than urban areas;
- full-access cases must be separated from stagnation;
- regional progress differs strongly;
- country-level variation remains important.

## Combined interpretation

Together, the two parts show that drinking-water access inequality is not explained by one factor alone.

Access patterns depend on:

- area type
- income group
- baseline access level
- rural-urban structure
- regional context
- population scale
- rate of change over time

The combined project moves from:

```text
Understanding current access
        ↓
Measuring progress over time
        ↓
Interpreting inequality through context
```

---

## Skills Demonstrated

This project demonstrates the following data analysis skills:

- spreadsheet-based data cleaning
- data validation
- feature engineering
- unit conversion
- missing-value handling
- row-level transformation
- conditional logic
- lookup-based enrichment
- pivot tables
- summary statistics
- interquartile range and spread analysis
- Annual Rate of Change calculation
- progress classification
- regional aggregation
- visual analytics
- data storytelling
- analytical documentation
- GitHub portfolio organization

---

## Tools Used

- Google Sheets
- GitHub
- Markdown
- CSV data
- Spreadsheet formulas
- Pivot tables
- Charts and exported visual assets

---

## Main Repository Outputs

| Output | Link |
|---|---|
| Part 1 project folder | [part-1-understanding-the-data/](./part-1-understanding-the-data/) |
| Part 1 analytical report | [Part1_Analytical_Report.md](./part-1-understanding-the-data/reports/analytical_report/Part1_Analytical_Report.md) |
| Part 1 sheet exports | [Part 1 sheet_exports/](./part-1-understanding-the-data/reports/sheet_exports/) |
| Part 2 project folder | [part-2-transforming-the-data/](./part-2-transforming-the-data/) |
| Part 2 analytical report | [Part2_Analytical_Report.md](./part-2-transforming-the-data/reports/analytical_report/Part2_Analytical_Report.md) |
| Part 2 sheet exports | [Part 2 sheet_exports/](./part-2-transforming-the-data/reports/sheet_exports/) |
| Part 2 data dictionary | [data_dictionary.md](./part-2-transforming-the-data/data/data_dictionary.md) |

---

## Limitations

This project is descriptive and exploratory.

It identifies patterns and associations but does not establish causality.

Main limitations include:

- the Part 1 dataset is a 2020 snapshot;
- the Part 2 dataset is not a complete annual panel;
- most Part 2 observations are concentrated around 2015 and 2020;
- missing rural and urban values affect some ARC calculations;
- regional ARC values are simple country-level averages unless otherwise specified;
- population-weighted ARC was not calculated;
- ARC measures speed of progress, not final access level;
- high ARC may reflect low baseline access;
- low ARC may reflect already high or full access;
- country-level context is needed for deeper interpretation.

---

## Future Improvements

The project could be extended by:

- reproducing the workflow in Python or R;
- building an interactive dashboard;
- calculating population-weighted regional ARC;
- comparing baseline and final access levels directly;
- ranking countries by strongest improvement and strongest decline;
- mapping access and ARC geographically;
- adding socioeconomic indicators;
- analyzing additional years if available;
- creating country-level profiles for high-priority cases;
- developing a final LinkedIn carousel or portfolio case-study presentation.

---

## Final Conclusion

This project shows how drinking-water access can be analyzed from two complementary perspectives.

Part 1 explains the 2020 access landscape.

Part 2 measures progress over time.

The main conclusion is:

> Access to at least basic drinking water has generally improved, especially in rural areas, but improvement speed alone does not mean inequality has disappeared. Drinking-water progress must be interpreted through area type, income group, regional context, baseline access, population scale, and the rate of change over time.

This repository presents the full workflow from spreadsheet-based data cleaning and transformation to visual analysis, analytical reporting, and portfolio-ready documentation.
