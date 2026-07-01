# Thailand and Korea registered population by age and sex

## Processed competition dataset

### Dataset summary for competition administrators

Row counts below exclude the CSV header.

| File | Target years | Data rows | Columns |
|---|---:|---:|---|
| `THA/population_age_sex.csv` | Every year from 1997 through 2025 (29 years) | 79,884 | 5 |
| `THA/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 (6 years) | 16,524 | 5 |
| `KOR/population_age_sex.csv` | Every year from 1993 through 2025 (33 years) | 19,368 | 5 |
| `KOR/population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 (6 years) | 3,564 | 5 |

All four files use the same column structure:

| Column | Description |
|---|---|
| `year` | Gregorian calendar year |
| `province_name_en` | Province name in English |
| `sex` | `male` or `female` |
| `age_group` | Five-year age group or `85+` |
| `population` | Registered population count |

The Thailand files contain all 76 provinces through 2010 and all 77 provinces
from 2011 onward. The Korea files contain all available province-level regions:
15 from 1993 through 1996, 16 from 1997 through 2011, and 17 from 2012 onward.

Each `population_age_sex_5year.csv` is a smaller version with observed
December 31 snapshots for 2000, 2005, 2010, 2015, 2020 and 2025. These are
selected observed years, not sums or averages across five-year periods.

The processed Thailand files exclude DOPA's `not_age_classified` records so
that every row belongs to a defined age group. Totals calculated from these
files are consequently lower than DOPA's official registered-population
totals by the excluded amount.

## Historical-data limitations

DOPA lists province-level age files beginning in 1994. However, all 228 source
files for 1994-1996 have zeroes in every single-age field, and their purported
province totals do not represent complete registered populations. They are
deliberately excluded from the processed dataset. The first year that passes
structural and arithmetic validation is 1997.

The sharp population decrease in 2004 is a statistical discontinuity. DOPA
reviewed and removed duplicate and otherwise inaccurate household-registration
records. It should not be interpreted solely as deaths or migration.

Bueng Kan was established in 2011. It is correctly absent before 2011;
historical values have not been backcast.
