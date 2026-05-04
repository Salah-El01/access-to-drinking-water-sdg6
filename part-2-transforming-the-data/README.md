# Part 2 — Transforming the Data  
**Project:** Access to Drinking Water (SDG 6)

## Overview

This repository section contains **Part 2** of the *Access to Drinking Water* project, focused on transforming the WHO/UNICEF JMP drinking-water dataset into a structure that can measure progress over time.

While Part 1 focused on understanding the 2020 snapshot of drinking-water access, Part 2 extends the analysis by working with a broader 2000–2020 dataset. The objective is to move from static description to transformation-based analysis, especially through the calculation of Annual Rates of Change.

This part of the project prepares the data for progress analysis by checking year representation, calculating change over time, classifying full-access cases, comparing rural and urban progress, and enriching the dataset with regional information.

---

## Project Goal

The goal of Part 2 is to answer the following question:

**How has access to at least basic drinking-water services changed across countries, areas, and regions over time?**

To answer it, this phase focuses on:

- understanding how years are represented in the dataset,
- checking whether the dataset supports time-based comparison,
- calculating Annual Rates of Change for basic drinking-water access,
- comparing national, rural, and urban progress,
- identifying countries already at full access,
- distinguishing real zero change from full-access saturation,
- comparing rural and urban rates of improvement,
- and analyzing progress across world regions.

---

## Dataset Context

The analysis is based on the **WHO/UNICEF Joint Monitoring Programme (JMP) drinking-water access estimates (2000–2020)**.

Compared with Part 1, the dataset used in Part 2 introduces a time dimension through the `year` variable. This makes it possible to compare observations across years and calculate rates of change.

The working dataset includes:

- country or area name,
- year,
- national population,
- urban population share,
- national drinking-water service levels,
- rural drinking-water service levels,
- urban drinking-water service levels.

The main service indicator used for the transformation analysis is:

- **At least basic drinking-water service**

Part 2 focuses especially on changes in at least basic access at three levels:

- national access,
- rural access,
- urban access.

---

## What Was Done in Part 2

Part 2 followed a complete transformation workflow in Google Sheets.

### 1. Data import and structure preparation

- Imported the 2000–2020 JMP drinking-water dataset into Google Sheets.
- Reviewed the structure of the dataset and its main variables.
- Sorted the data by country name and year to prepare for row-pair calculations.
- Preserved missing values such as `Null` where relevant.

### 2. Year representation analysis

- Investigated how years are represented in the dataset.
- Checked the minimum and maximum year values.
- Calculated the year difference between paired country observations.
- Verified whether the dataset behaves like a full annual time series or a mostly interval-based comparison.

The analysis showed that most observations are concentrated around 2015 and 2020, with only a small number of intermediate-year records. This means the dataset is best interpreted as a mostly five-year comparison rather than a complete annual time series.

### 3. Annual Rate of Change calculations

The central transformation of Part 2 was the calculation of Annual Rates of Change.

Three ARC variables were created:

- `ARC_n` for national access,
- `ARC_r` for rural access,
- `ARC_u` for urban access.

These variables estimate the average yearly change in access to at least basic drinking-water services between paired observations for the same country or area.

### 4. Full-access classification

Rounded basic-access indicators were created to identify countries or areas that had already reached full or near-full access.

The following classification fields were created:

- `ARC_n_full`
- `ARC_r_full`
- `ARC_u_full`

This step was important because a country with 100% access may have an ARC value of zero, but that does not mean lack of progress. It means the country may already have reached the maximum possible access level.

### 5. Access analysis by area

The transformed data was used to compare progress across:

- national areas,
- rural areas,
- urban areas.

Countries were classified into several ARC conditions:

- no ARC value,
- full access,
- ARC = 0,
- ARC > 0,
- ARC < 0.

This made it possible to distinguish missing data, stagnation, improvement, decline, and full-access saturation.

### 6. Rural–urban progress comparison

A new variable, `ARC_diff`, was created to compare rural and urban progress:

```text
ARC_diff = ARC_r - ARC_u
