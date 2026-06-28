# Thailand and Korea Population by Province, Age Group, and Sex

This repository provides population data for the **My City in 2040** student
data competition.

The source files from Thailand and Korea were converted into consistent,
analysis-ready CSV files. Each record represents a province, year, sex, and
five-year age group.

## Files

| File | Years included | Data rows | Description |
|---|---:|---:|---|
| `data/population_age_sex.csv` | Every year from 1997 to 2025 | 84,322 | Thailand annual data |
| `data/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 | 17,442 | Thailand five-year snapshots |
| `data/kor/population_age_sex.csv` | Every year from 1993 to 2025 | 19,368 | Korea annual data |
| `data/kor/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 | 3,564 | Korea five-year snapshots |

Row counts exclude the CSV header. The five-year dataset contains observations
from selected years; it is not a sum or average of five-year periods.

## Column Structure

All CSV files use nine columns. The local-language name column is
`province_name_th` for Thailand and `province_name_ko` for Korea.

| Column | Description |
|---|---|
| `year` | Gregorian calendar year |
| `province_code` | Province-level administrative code |
| `province_name_th` | Province name in Thai (Thailand files) |
| `province_name_ko` | Province name in Korean (Korea files) |
| `province_name_en` | Province name in English |
| `sex` | `male` or `female` |
| `age_group` | `0-4`, `5-9`, ..., `80-84`, `85+`; Thailand also has `not_age_classified` |
| `population` | Population value |
| `population_type` | `registered` |
| `reference_date` | Reference date in `YYYY-12-31` format |

## Load the Data in Google Colab

```python
!git clone <REPOSITORY_URL>
%cd <REPOSITORY_DIRECTORY>

import pandas as pd

annual = pd.read_csv("data/population_age_sex.csv")
five_year = pd.read_csv("data/population_age_sex_5year.csv")

korea_annual = pd.read_csv("data/kor/population_age_sex.csv")
korea_five_year = pd.read_csv("data/kor/population_age_sex_5year.csv")
```

## Important Notes

- These datasets contain registered population, which is not the same as census
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
- Korea has data for 15 provinces from 1993 through 1996, 16 from 1997 through
  2011, and 17 from 2012 onward. Ulsan is included from 1997 and Sejong from
  2012.
- The 1992 Korean source groups everyone aged 80 or older together, so it
  cannot be converted into the common `80-84` and `85+` groups and is excluded.
- In four observations from the 1993-2010 Korean source, the published
  age-group sum differs from the published sex total by one or two people. The
  analysis-ready files preserve the published age-group values.
- Historical Korean names are normalized to current names for stable grouping:
  `강원특별자치도` and `전북특별자치도`.

## Sources

Department of Provincial Administration (DOPA), Ministry of Interior,
Thailand:

- [Annual population by age and province](https://stat.bora.dopa.go.th/new_stat/webPage/statByProvince.php)
- [Monthly population by age](https://stat.bora.dopa.go.th/new_stat/webPage/statByAgeMonth.php)

Korean Statistical Information Service (KOSIS):

- [Registered population by region, sex, and five-year age group](https://kosis.kr/statHtml/statHtml.do?orgId=101&tblId=DT_1B04005)

The CSV files use UTF-8 encoding and can be opened with Python, Google Colab,
Excel, Tableau, Power BI, or similar tools.
