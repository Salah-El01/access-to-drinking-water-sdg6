# Data Dictionary — Access to Drinking Water

This data dictionary documents the main variables used in Part 1 of the **Access to Drinking Water** analysis.

The dataset contains country-level estimates for population and drinking water access in 2020.

---

## Original Variables

| Variable | Description | Type / Format |
|---|---|---|
| `name` | Country or area name | Text |
| `year` | Reference year of the estimate | Number |
| `income_group` | Country income classification | Text |
| `pop_n` | National population size estimate, measured in thousands | Numeric |
| `pop_u` | Urban population share, expressed as a percentage | Numeric |
| `wat_bas_n` | National share of population with at least basic drinking water access | Percentage |
| `wat_lim_n` | National share of population with limited drinking water access | Percentage |
| `wat_unimp_n` | National share of population with unimproved drinking water access | Percentage |
| `wat_sur_n` | National share of population relying on surface water | Percentage |
| `wat_bas_r` | Rural share of population with at least basic drinking water access | Percentage |
| `wat_lim_r` | Rural share of population with limited drinking water access | Percentage |
| `wat_unimp_r` | Rural share of population with unimproved drinking water access | Percentage |
| `wat_sur_r` | Rural share of population relying on surface water | Percentage |
| `wat_bas_u` | Urban share of population with at least basic drinking water access | Percentage |
| `wat_lim_u` | Urban share of population with limited drinking water access | Percentage |
| `wat_unimp_u` | Urban share of population with unimproved drinking water access | Percentage |
| `wat_sur_u` | Urban share of population relying on surface water | Percentage |

---

## Service-Level Definitions

### At Least Basic

Represents the share of the population with access to at least basic drinking water services.

In this analysis, this is treated as the highest access category available in the dataset.

Related variables:

- `wat_bas_n`
- `wat_bas_r`
- `wat_bas_u`

---

### Limited

Represents the share of the population with limited drinking water access.

Limited access indicates that water is available, but service conditions are below the at least basic threshold.

Related variables:

- `wat_lim_n`
- `wat_lim_r`
- `wat_lim_u`

---

### Unimproved

Represents the share of the population relying on unimproved drinking water sources.

This category indicates lower-quality access and is used as an important indicator of water access inequality.

Related variables:

- `wat_unimp_n`
- `wat_unimp_r`
- `wat_unimp_u`

---

### Surface Water

Represents the share of the population relying directly on surface water sources.

This is the lowest service category in the analysis and indicates the most severe access limitations.

Related variables:

- `wat_sur_n`
- `wat_sur_r`
- `wat_sur_u`

---

## Area-Level Variable Groups

### National Access Variables

| Variable | Description |
|---|---|
| `wat_bas_n` | National at least basic access |
| `wat_lim_n` | National limited access |
| `wat_unimp_n` | National unimproved access |
| `wat_sur_n` | National surface-water access |

These variables describe drinking water access for the total national population.

---

### Rural Access Variables

| Variable | Description |
|---|---|
| `wat_bas_r` | Rural at least basic access |
| `wat_lim_r` | Rural limited access |
| `wat_unimp_r` | Rural unimproved access |
| `wat_sur_r` | Rural surface-water access |

These variables describe drinking water access for rural populations.

---

### Urban Access Variables

| Variable | Description |
|---|---|
| `wat_bas_u` | Urban at least basic access |
| `wat_lim_u` | Urban limited access |
| `wat_unimp_u` | Urban unimproved access |
| `wat_sur_u` | Urban surface-water access |

These variables describe drinking water access for urban populations.

---

## Derived Variables

| Derived Variable | Formula / Logic | Purpose |
|---|---|---|
| `value_cnt` | `COUNTA(row_range)` | Counts non-empty cells in each row to validate row completeness |
| `pop_u_val` | `pop_n * pop_u / 100` | Estimates the urban population count |
| `pop_r` | `100 - pop_u` | Calculates rural population share |
| `pop_n (m)` | rounded national population in millions | Improves readability in population-based charts |
| `pop_u (rounded)` | rounded urban population share | Supports grouped urban visualization |
| `pop_r (rounded)` | rounded rural population share | Supports grouped rural visualization |
| cleaned access fields | numeric cleaned versions of service-level variables | Supports stable visualization and analysis |

---

## Important Unit Notes

### National Population

`pop_n` is measured in **thousands**.

Example:

If `pop_n = 53,771`, the estimated population is approximately:

`53,771,000 people`

This unit is important when comparing dataset population values with external population estimates or when calculating derived population counts.

---

### Urban Population Share

`pop_u` is a percentage.

When using it in calculations, it must be divided by 100.

Example:

`pop_u_val = pop_n * pop_u / 100`

---

### Rural Population Share

Rural population share is derived from urban population share.

Formula:

`pop_r = 100 - pop_u`

This works because the population is treated as divided into two complementary area types:

- urban
- rural

---

## Cleaned Water Access Fields

Cleaned water-access variables were used for visualizations to reduce issues caused by:

- missing values
- text values such as `NAN`
- non-numeric entries
- inconsistent percentage values
- charting errors

These cleaned fields helped ensure that the visual outputs represented valid numeric access shares.

---

## Analytical Use of Variables

| Analysis Area | Main Variables Used |
|---|---|
| Population structure | `pop_n`, `pop_u`, `pop_r`, `pop_n (m)` |
| Urban access analysis | `pop_u (rounded)`, `wat_bas_u`, `wat_lim_u`, `wat_unimp_u`, `wat_sur_u` |
| Rural access analysis | `pop_r (rounded)`, `wat_bas_r`, `wat_lim_r`, `wat_unimp_r`, `wat_sur_r` |
| National access analysis | `pop_n`, `wat_bas_n`, `wat_lim_n`, `wat_unimp_n`, `wat_sur_n` |
| Income-group analysis | `income_group`, `pop_n`, `pop_u`, `wat_bas_n`, `wat_lim_n`, `wat_unimp_n`, `wat_sur_n` |
| Summary statistics | all national, rural, and urban water access variables |

---

## Notes

- The dataset is analyzed at country or area level.
- Water access values are expressed as percentage shares.
- The four service levels are treated as components of the full access distribution.
- The analysis is descriptive and exploratory.
- The working spreadsheet remains the main place where transformations, calculations, and visualizations were performed.
