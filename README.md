# Thailand and Korea Population by Province, Age Group, and Sex

This repository provides population data for the **My City in 2040** student
data competition.

The source files from Thailand and Korea were converted into consistent,
analysis-ready CSV files. Each record represents a province, year, sex, and
five-year age group.

## Files

| File | Years included | Data rows | Description |
|---|---:|---:|---|
| `data/THA/population_age_sex.csv` | Every year from 1997 to 2025 | 79,884 | Thailand annual data |
| `data/THA/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 | 16,524 | Thailand five-year snapshots |
| `data/KOR/population_age_sex.csv` | Every year from 1993 to 2025 | 19,368 | Korea annual data |
| `data/KOR/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 | 3,564 | Korea five-year snapshots |

Row counts exclude the CSV header. The five-year dataset contains observations
from selected years; it is not a sum or average of five-year periods.

## Geographic Coverage

The files contain all available province-level regions: 76 Thai provinces
through 2010 and 77 from 2011 onward, and 15–17 Korean province-level regions
depending on the year.

## Column Structure

All CSV files use the same five columns.

| Column | Description |
|---|---|
| `year` | Gregorian calendar year |
| `province_name_en` | Province name in English |
| `sex` | `male` or `female` |
| `age_group` | `0-4`, `5-9`, ..., `80-84`, `85+` |
| `population` | Population value |

## Load the Data in Google Colab

```python
!git clone <REPOSITORY_URL>
%cd <REPOSITORY_DIRECTORY>

import pandas as pd

annual = pd.read_csv("data/THA/population_age_sex.csv")
five_year = pd.read_csv("data/THA/population_age_sex_5year.csv")

korea_annual = pd.read_csv("data/KOR/population_age_sex.csv")
korea_five_year = pd.read_csv("data/KOR/population_age_sex_5year.csv")
```

## Important Notes

- These datasets contain registered population, which is not the same as census
  population or projected population.
- Thailand totals calculated from these files exclude DOPA records that are
  not assigned to an age (`not_age_classified`). They are therefore lower than
  DOPA's official registered-population totals by the excluded amount.
- The decrease in registered population in 2004 is partly caused by DOPA's
  correction and removal of duplicate or inaccurate registration records. It
  should not be interpreted only as deaths or migration.
- DOPA lists historical age files for 1994-1996, but their single-age fields are
  empty and their totals are incomplete. The analysis-ready dataset therefore
  starts in 1997.
- Thailand had 76 provinces through 2010. Bueng Kan was established in 2011,
  after which the dataset contains 77 provinces.
- Korea has 15 province-level regions from 1993 through 1996, 16 from 1997
  through 2011, and 17 from 2012 onward.
- The 1992 Korean source groups everyone aged 80 or older together, so it
  cannot be converted into the common `80-84` and `85+` groups and is excluded.
- In four observations from the 1993-2010 Korean source, the published
  age-group sum differs from the published sex total by one or two people. The
  analysis-ready files preserve the published age-group values.
- Historical Korean names are normalized to current names for stable grouping:
  `Gangwon State`, `Jeonbuk State`, and `Jeju`.

## Sources

Department of Provincial Administration (DOPA), Ministry of Interior,
Thailand:

- [Annual population by age and province](https://stat.bora.dopa.go.th/new_stat/webPage/statByProvince.php)
- [Monthly population by age](https://stat.bora.dopa.go.th/new_stat/webPage/statByAgeMonth.php)

Korean Statistical Information Service (KOSIS):

- [Registered population by region, sex, and five-year age group](https://kosis.kr/statHtml/statHtml.do?orgId=101&tblId=DT_1B04005)

The CSV files use UTF-8 encoding and can be opened with Python, Google Colab,
Excel, Tableau, Power BI, or similar tools.
