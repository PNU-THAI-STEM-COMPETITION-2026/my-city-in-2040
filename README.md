# Thailand Population by Province, Age Group, and Sex

This repository provides registered-population data for the **My City in 2040**
student data competition.

The data were collected from Thailand's Department of Provincial
Administration (DOPA) and converted into consistent, analysis-ready CSV files.
Each record represents a province, year, sex, and five-year age group.

## Files

| File | Years included | Data rows | Description |
|---|---:|---:|---|
| `data/population_age_sex.csv` | Every year from 1997 to 2025 | 84,322 | Complete annual dataset |
| `data/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 | 17,442 | Smaller five-year snapshot dataset |

Row counts exclude the CSV header. The five-year dataset contains observations
from selected years; it is not a sum or average of five-year periods.

## Column Structure

Both CSV files use the same nine columns.

| Column | Description |
|---|---|
| `year` | Gregorian calendar year |
| `province_code` | DOPA province code |
| `province_name_th` | Province name in Thai |
| `province_name_en` | Province name in English |
| `sex` | `male` or `female` |
| `age_group` | `0-4`, `5-9`, ..., `80-84`, `85+`, or `not_age_classified` |
| `population` | Registered population count |
| `population_type` | `registered` |
| `reference_date` | Reference date in `YYYY-12-31` format |

## Load the Data in Google Colab

```python
!git clone <REPOSITORY_URL>
%cd <REPOSITORY_DIRECTORY>

import pandas as pd

annual = pd.read_csv("data/population_age_sex.csv")
five_year = pd.read_csv("data/population_age_sex_5year.csv")
```

## Important Notes

- The dataset contains registered population, which is not the same as census
  population or projected population.
- `not_age_classified` contains registered residents who are included in DOPA's
  reported total but are not assigned to a single year of age in the source
  files. Keep this category when calculating total population.
- Thailand had 76 provinces in this dataset through 2010. Bueng Kan, province
  code `38`, was established in 2011, after which the dataset contains 77
  provinces.
- The decrease in registered population in 2004 is partly caused by DOPA's
  correction and removal of duplicate or inaccurate registration records. It
  should not be interpreted only as deaths or migration.
- DOPA lists historical age files for 1994-1996, but their single-age fields are
  empty and their totals are incomplete. The analysis-ready dataset therefore
  starts in 1997.

## Source

Department of Provincial Administration (DOPA), Ministry of Interior,
Thailand:

- [Annual population by age and province](https://stat.bora.dopa.go.th/new_stat/webPage/statByProvince.php)
- [Monthly population by age](https://stat.bora.dopa.go.th/new_stat/webPage/statByAgeMonth.php)

The CSV files use UTF-8 encoding and can be opened with Python, Google Colab,
Excel, Tableau, Power BI, or similar tools.
