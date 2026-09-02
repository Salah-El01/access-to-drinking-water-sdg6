# Regional ARC Tables — Part 2: Transforming the Data

This folder contains seven regional table screenshots supporting the Annual Rate of Change analysis in Part 2 of the **Access to Drinking Water** project.

The screenshots provide country-level examples behind the regional averages presented in the main visualisations. They help illustrate:

* national, rural and urban ARC;
* positive, zero and negative change;
* missing rural or urban estimates;
* different observation intervals;
* variation among countries within the same region.

These tables are supporting analytical evidence rather than primary visual outputs.

---

## Files Included

| Number | Region                     | Countries or areas in full regional Summary | Image                                       |
| -----: | -------------------------- | ------------------------------------------: | ------------------------------------------- |
|     01 | East Asia & Pacific        |                                          40 | `01_east_asia_pacific_arc_table.png`        |
|     02 | Europe & Central Asia      |                                          64 | `02_europe_central_asia_arc_table.png`      |
|     03 | Latin America & Caribbean  |                                          48 | `03_latin_america_caribbean_arc_table.png`  |
|     04 | Middle East & North Africa |                                          10 | `04_middle_east_north_africa_arc_table.png` |
|     05 | North America              |                                           5 | `05_north_america_arc_table.png`            |
|     06 | South Asia                 |                                          11 | `06_south_asia_arc_table.png`               |
|     07 | Sub-Saharan Africa         |                                          53 | `07_sub_saharan_africa_arc_table.png`       |

---

## Screenshot-Coverage Limitation

The PNG files are screenshots of the Google Sheets regional tables.

The larger regional screenshots do not necessarily display every country or area included in the complete regional Summary. In particular, tables containing many countries may show only the visible upper section of the Google Sheets table.

Therefore, these screenshots:

* illustrate country-level calculations;
* provide selected examples of regional variation;
* do not replace complete machine-readable regional exports;
* should not be used alone to reconstruct every regional average.

The complete spreadsheet and Summary calculations remain the authoritative analytical sources.

For full reproducibility, future versions of the repository should add regional CSV files containing every country-level record.

---

## Variables Included

Each screenshot contains the following fields:

| Variable               | Description                                 |
| ---------------------- | ------------------------------------------- |
| `name`                 | Country or area name                        |
| `region`               | Regional classification used in the project |
| `year`                 | Observation year                            |
| `pop_n (in thousands)` | National population estimate in thousands   |
| `pop_n (Millions)`     | National population converted into millions |
| `ARC_n`                | National Annual Rate of Change              |
| `ARC_r`                | Rural Annual Rate of Change                 |
| `ARC_u`                | Urban Annual Rate of Change                 |

All ARC values are expressed in:

> Percentage points per year.

---

## ARC Interpretation

| Result    | Interpretation                                                                   |
| --------- | -------------------------------------------------------------------------------- |
| `ARC > 0` | Access increased                                                                 |
| `ARC = 0` | No measured change                                                               |
| `ARC < 0` | Access decreased                                                                 |
| `Null`    | ARC could not be calculated because one or more required values were unavailable |
| Blank     | No calculation is displayed on that row                                          |

A zero ARC requires additional context. It may indicate:

* unchanged access below full coverage;
* access already at or near 100%;
* stable estimates between observations.

The full-access classification fields should be consulted before interpreting zero ARC as stagnation.

---

## Table Structure

Each country or area is generally represented by two consecutive rows.

### Earlier observation row

The earlier row usually contains:

* the country or area name;
* region;
* earlier year;
* `ARC_n`;
* `ARC_r`;
* `ARC_u`.

### Later observation row

The later row usually contains:

* the same country or area name;
* region;
* later year;
* national population in thousands;
* national population converted into millions.

The ARC calculation uses both rows:

```text
ARC =
(later access value - earlier access value)
/
(later year - earlier year)
```

The two rows belonging to the same country must therefore be interpreted together.

---

## 01 — East Asia & Pacific

![East Asia & Pacific ARC Table](./01_east_asia_pacific_arc_table.png)

### Visible examples

The displayed excerpt includes several different progress patterns.

* **Cambodia** has positive national, rural and urban ARC.
* **China** has positive national and rural ARC but slightly negative urban ARC.
* **Democratic People's Republic of Korea** has negative national, rural and urban ARC.
* **Fiji** has slightly positive national ARC but negative rural and urban ARC.
* **Australia** has zero national, rural and urban ARC in the displayed comparison.
* Several countries and areas contain `Null` rural or urban values.

Selected visible values:

| Country or area                       | `ARC_n` | `ARC_r` | `ARC_u` |
| ------------------------------------- | ------: | ------: | ------: |
| Cambodia                              |  0.5552 |  0.4712 |  0.3820 |
| China                                 |  0.4997 |  1.0364 | -0.0810 |
| Democratic People's Republic of Korea | -0.2742 | -0.5727 | -0.1150 |
| Fiji                                  |  0.0077 | -0.0581 | -0.0218 |

### Interpretation

The visible excerpt demonstrates that one regional average can contain:

* broad positive progress;
* mixed rural and urban results;
* declines;
* zero change;
* missing area-level values.

China’s comparatively high rural ARC illustrates one source of strong rural progress within the displayed countries. However, the screenshot alone does not measure each country’s exact influence on the complete regional average.

---

## 02 — Europe & Central Asia

![Europe & Central Asia ARC Table](./02_europe_central_asia_arc_table.png)

### Visible examples

* **Albania** has positive national, rural and urban ARC.
* **Armenia** also has positive values across the three measures.
* **Azerbaijan** has particularly high rural ARC.
* **Bulgaria** has negative national, rural and urban ARC.
* **Andorra**, **Austria** and **Belgium** display zero ARC values.
* Some countries and areas contain unavailable rural or urban values.

Selected visible values:

| Country or area | `ARC_n` | `ARC_r` | `ARC_u` |
| --------------- | ------: | ------: | ------: |
| Albania         |  0.3347 |  0.6928 |  0.0437 |
| Armenia         |  0.0837 |  0.1890 |  0.0221 |
| Azerbaijan      |  0.7246 |  1.3565 |  0.1458 |
| Bulgaria        | -0.0370 | -0.1230 | -0.0165 |

### Interpretation

The visible table contains many low or zero values alongside positive and negative cases.

Low ARC may be consistent with limited remaining room for improvement when baseline access is already high. However, baseline access is not displayed in this screenshot, so a ceiling effect should be treated as contextual interpretation rather than a conclusion derived from this table alone.

---

## 03 — Latin America & Caribbean

![Latin America & Caribbean ARC Table](./03_latin_america_caribbean_arc_table.png)

### Visible examples

* **Belize** has positive national and rural ARC but slightly negative urban ARC.
* **Bolivia (Plurinational State of)** has high rural ARC.
* **Brazil** also has particularly high rural ARC.
* Several island states and territories contain zero or missing values.
* The displayed countries use different later observation years, including 2016, 2017, 2019 and 2020.

Selected visible values:

| Country or area                  | `ARC_n` | `ARC_r` | `ARC_u` |
| -------------------------------- | ------: | ------: | ------: |
| Belize                           |  0.2453 |  0.4683 | -0.0253 |
| Bolivia (Plurinational State of) |  0.5856 |  1.2393 |  0.1864 |
| Brazil                           |  0.3035 |  1.4378 |  0.1035 |

### Interpretation

The visible values for Brazil and Bolivia illustrate substantial rural progress relative to their urban ARC.

This pattern is consistent with the region’s high average rural ARC and positive average paired `ARC_diff`. However, the regional result is calculated from all valid countries, not only the examples visible in the screenshot.

---

## 04 — Middle East & North Africa

![Middle East & North Africa ARC Table](./04_middle_east_north_africa_arc_table.png)

### Visible examples

* **Morocco** has very high national and rural ARC.
* **Iraq** also has high rural ARC.
* **Algeria**, **Egypt**, **Oman** and **Sudan** have positive national, rural and urban ARC.
* **Jordan** has negative national, rural and urban ARC.
* **Syrian Arab Republic** has positive national and rural ARC but slightly negative urban ARC.
* **Kuwait** and **Lebanon** contain unavailable rural and urban ARC.

Selected visible values:

| Country or area | `ARC_n` | `ARC_r` | `ARC_u` |
| --------------- | ------: | ------: | ------: |
| Algeria         |  0.2056 |  0.3370 |  0.1029 |
| Iraq            |  0.8225 |  2.0137 |  0.2962 |
| Jordan          | -0.0133 | -0.0102 | -0.0182 |
| Morocco         |  1.3302 |  2.6347 |  0.3055 |
| Oman            |  0.3859 |  0.3768 |  0.1646 |
| Sudan           |  0.2997 |  0.2983 |  0.1374 |

### Interpretation

Morocco and Iraq illustrate the high rural ARC values present within this region.

The complete regional Summary shows that Middle East & North Africa has:

* the highest average rural ARC;
* the highest average paired rural–urban ARC difference.

The table also demonstrates that progress is not universal because negative and missing observations remain present.

The screenshot identifies large country-level values but does not independently calculate how much each country contributes to the regional mean.

---

## 05 — North America

![North America ARC Table](./05_north_america_arc_table.png)

### Visible examples

* **United States of America** has positive national, rural and urban ARC.
* **Canada** has slightly negative national and urban ARC but positive rural ARC.
* **Greenland** has zero national, rural and urban ARC.
* **Bermuda** has missing rural ARC.
* **Saint Pierre and Miquelon** has missing rural and urban ARC.

Verified visible values:

| Country or area          | `ARC_n` | `ARC_r` | `ARC_u` |
| ------------------------ | ------: | ------: | ------: |
| Canada                   | -0.0015 |  0.0489 | -0.0132 |
| Greenland                |  0.0000 |  0.0000 |  0.0000 |
| United States of America |  0.0873 |  0.3781 |  0.0214 |

### Interpretation

North America has the lowest regional national, rural and urban ARC averages.

This may be consistent with high baseline access and limited remaining room for improvement. Nevertheless, the table does not display baseline access percentages, so the explanation requires evidence from the access-level analysis.

The region also illustrates the importance of missing-data treatment because only some countries have complete paired rural and urban measurements.

---

## 06 — South Asia

![South Asia ARC Table](./06_south_asia_arc_table.png)

### Visible examples

* **Afghanistan** has exceptionally high positive national, rural and urban ARC.
* **India** has positive ARC across all three measures, with rural ARC higher than urban ARC.
* **Bangladesh** has positive national and rural ARC but negative urban ARC.
* **Nepal** and **Pakistan** also have positive national and rural ARC but negative urban ARC.
* **Malaysia** has slightly positive national ARC but negative rural and urban ARC.
* **Sri Lanka** has positive national, rural and urban ARC.

Selected visible values:

| Country or area | `ARC_n` | `ARC_r` | `ARC_u` |
| --------------- | ------: | ------: | ------: |
| Afghanistan     |  2.7503 |  2.6679 |  2.6682 |
| Bangladesh      |  0.1193 |  0.2214 | -0.0656 |
| India           |  0.4703 |  0.6421 |  0.0538 |
| Malaysia        |  0.0095 | -0.1442 | -0.0081 |
| Nepal           |  0.4532 |  0.5923 | -0.1434 |
| Pakistan        |  0.1388 |  0.2898 | -0.1557 |

### Interpretation

South Asia combines:

* one of the largest regional populations;
* comparatively high national ARC;
* comparatively high rural ARC;
* substantial variation in urban outcomes.

Afghanistan is an extreme positive observation and may influence unweighted regional averages. However, its exact contribution should be measured using sensitivity analysis rather than inferred from the screenshot alone.

---

## 07 — Sub-Saharan Africa

![Sub-Saharan Africa ARC Table](./07_sub_saharan_africa_arc_table.png)

### Visible examples

* **Botswana** and **Cabo Verde** have high positive rural ARC.
* **Benin**, **Cameroon** and **Chad** have positive national and rural ARC but negative urban ARC.
* **Burkina Faso** has negative national and rural ARC but slightly positive urban ARC.
* **Central African Republic** has substantial negative national, rural and urban ARC.
* **Comoros** has zero rural and urban ARC.
* **Congo** has positive national, rural and urban ARC.

Selected visible values:

| Country or area          | `ARC_n` | `ARC_r` | `ARC_u` |
| ------------------------ | ------: | ------: | ------: |
| Benin                    |  0.1255 |  0.2536 | -0.2078 |
| Botswana                 |  0.7535 |  1.4302 |  0.2165 |
| Burkina Faso             | -0.5845 | -1.2274 |  0.0492 |
| Cabo Verde               |  0.6653 |  1.4564 |  0.1310 |
| Cameroon                 |  0.3493 |  0.3044 | -0.0347 |
| Central African Republic | -1.0218 | -0.7570 | -1.6201 |
| Chad                     |  0.3577 |  0.3993 | -0.1123 |
| Congo                    |  0.5270 |  0.8665 |  0.0599 |

### Interpretation

The visible excerpt illustrates substantial country-level variation:

* strong positive progress;
* mixed rural and urban outcomes;
* zero change;
* major declines.

Sub-Saharan Africa has the highest regional average national ARC and a comparatively high rural ARC. However, the regional average does not represent every country’s trajectory.

The screenshot is only an excerpt of the 53 countries and areas included in the full regional Summary.

---

## Cross-Regional Findings

### 1. Rural ARC is frequently higher than urban ARC

Across the complete dataset:

| Paired `ARC_diff` result | Countries or areas |
| ------------------------ | -----------------: |
| Positive                 |                112 |
| Negative                 |                 23 |
| Zero                     |                 30 |
| Missing                  |                 66 |
| **Total**                |            **231** |

Most valid paired observations therefore have:

```text
ARC_r > ARC_u
```

This pattern is consistent with rural catch-up, but it does not mean that rural access levels have reached urban access levels.

### 2. Regional averages hide country-level variation

Countries within the same region may have:

* positive ARC;
* zero ARC;
* negative ARC;
* missing ARC;
* different national, rural and urban patterns.

Regional means should be treated as summary indicators rather than uniform regional outcomes.

### 3. High ARC does not mean high access

ARC measures the speed and direction of change.

A country can have:

* high ARC and low final access;
* low ARC and high final access;
* zero ARC at full access;
* zero ARC below full access.

Baseline and final access values are therefore needed for complete interpretation.

### 4. Negative ARC identifies declining access

Negative ARC indicates that estimated access decreased between the two observations.

Visible examples include:

* Central African Republic;
* Burkina Faso;
* Bulgaria;
* Democratic People's Republic of Korea.

These cases demonstrate why country-level inspection is necessary.

### 5. Missingness affects rural and urban comparisons

The complete dataset contains:

| Measure           | Valid | Missing |
| ----------------- | ----: | ------: |
| National ARC      |   229 |       2 |
| Rural ARC         |   167 |      64 |
| Urban ARC         |   181 |      50 |
| Paired `ARC_diff` |   165 |      66 |

Area-level results are therefore less complete than national results.

### 6. Population provides context, not measured impact

A large population can increase the possible scale of an access change.

However, these tables do not calculate:

* population-weighted ARC;
* the number of people gaining access;
* the number of people losing access;
* the remaining population without access.

Population and ARC should be considered together as contextual dimensions, not as a calculated measure of human impact.

---

## Regional Summary

| Region                     | Countries or areas | Population, millions | National ARC | Rural ARC | Urban ARC |
| -------------------------- | -----------------: | -------------------: | -----------: | --------: | --------: |
| East Asia & Pacific        |                 40 |              2,247.5 |        0.278 |     0.508 |     0.233 |
| Europe & Central Asia      |                 64 |              1,017.5 |        0.112 |     0.224 |     0.047 |
| Latin America & Caribbean  |                 48 |                642.5 |        0.144 |     0.680 |     0.072 |
| Middle East & North Africa |                 10 |                311.1 |        0.346 |     0.737 |     0.124 |
| North America              |                  5 |                368.9 |        0.017 |     0.142 |     0.002 |
| South Asia                 |                 11 |              2,082.3 |        0.480 |     0.559 |     0.266 |
| Sub-Saharan Africa         |                 53 |              1,124.0 |        0.558 |     0.604 |     0.270 |
| **Grand Total**            |            **231** |          **7,793.8** |    **0.277** | **0.484** | **0.155** |

The ARC values are unweighted country averages.

A small country and a highly populated country contribute equally to their respective regional ARC averages.

---

## Relationship to the Main Visuals

The aggregated charts are stored in:

[Main Visuals](../main_visuals/)

The main visuals summarise:

* the distribution of observations by year;
* average paired rural–urban ARC differences by region;
* independently aggregated rural and urban ARC;
* regional population with national and rural ARC.

The regional screenshots provide supporting country-level examples behind those aggregated results.

They should be interpreted together with the complete Summary rather than as independent regional rankings.

---

## Data-Interpretation Notes

* ARC values are calculated between two observations for the same country or area.
* Observation intervals range from one to five years.
* ARC is expressed in percentage points per year.
* `Null` values were retained to preserve missing-data transparency.
* National, rural and urban ARC have different valid sample sizes.
* Regional ARC values are simple country averages unless stated otherwise.
* Regional averages are not population-weighted.
* Population values are displayed on the later observation row.
* ARC values are generally displayed on the earlier observation row.
* Both rows belonging to the same country should be read together.
* Some screenshots display only a portion of the complete regional table.
* Country examples visible in a screenshot should not be treated as the only contributors to a regional result.
* The tables describe patterns but do not establish causality.

---

## Reproducibility Recommendation

To strengthen this folder, future repository versions should add:

* one complete CSV file for each region;
* all countries and areas included in every regional average;
* `ARC_diff`;
* full-access classification fields;
* baseline access values;
* later access values;
* observation interval;
* valid-value counts for every regional calculation.

Machine-readable files would make it possible to reproduce the regional averages directly from the GitHub repository.

---

## Portfolio Role

These regional tables demonstrate:

* country-level data transformation;
* regional segmentation;
* population-unit conversion;
* country-pair ARC calculation;
* missing-value handling;
* comparison of national, rural and urban change;
* traceability between individual observations and aggregated charts;
* awareness of analytical limitations.

The tables strengthen the portfolio by showing country-level evidence while also documenting the limits of screenshot-based reporting.

---

## Navigation

* [Back to Assets](../README.md)
* [Open Main Visuals](../main_visuals/)
* [Open Data Documentation](../../data/)
* [Open Analytical Report](../../reports/analytical_report/Part2_Analytical_Report.md)
* [Open Sheet Exports](../../reports/sheet_exports/)
* [Back to Part 2](../../README.md)
