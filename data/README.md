# DOPA registered population by age and sex

## Processed competition dataset

### Dataset summary for competition administrators

Row counts below exclude the CSV header.

| File | Target years | Data rows | Columns |
|---|---:|---:|---|
| `population_age_sex.csv` | Every year from 1997 through 2025 (29 years) | 84,322 | 9 |
| `population_age_sex_5year.csv` | 2000, 2005, 2010, 2015, 2020, 2025 (6 years) | 17,442 | 9 |

Both files use the same column structure:

| Column | Description |
|---|---|
| `year` | Gregorian calendar year |
| `province_code` | DOPA province code |
| `province_name_th` | Province name in Thai |
| `province_name_en` | Province name in English |
| `sex` | `male` or `female` |
| `age_group` | Five-year age group, `85+`, or `not_age_classified` |
| `population` | Registered population count |
| `population_type` | `registered` |
| `reference_date` | December 31 reference date |

`population_age_sex.csv` contains December 31 registered-population
snapshots by province from 1997 through 2025.

- 1997-2010: 76 provinces, before Bueng Kan was established
- 2011-2025: 77 provinces

`population_age_sex_5year.csv` is a smaller version with observed
December 31 snapshots for 2000, 2005, 2010, 2015, 2020 and 2025. These are
selected observed years, not sums or averages across five-year periods.

`not_age_classified` reconciles the single-age columns with DOPA's reported
sex total. It contains records that are present in the source total but not
assigned to a single age. In the newer files these source categories include
lunar-year births, central-house-registration records, non-Thai nationals,
and records being moved.

## Historical-data limitations

DOPA lists province-level age files beginning in 1994. However, all 228 source
files for 1994-1996 have zeroes in every single-age field, and their purported
province totals do not represent complete registered populations. They are
retained in the raw directory but deliberately excluded from the processed
dataset. The first year that passes structural and arithmetic validation is
1997.

See `quality/historical_population_age_validation.csv` for the annual
validation result, source-file count, classified-age population and reported
population.

The sharp population decrease in 2004 is a statistical discontinuity. DOPA
reviewed and removed duplicate and otherwise inaccurate household-registration
records. It should not be interpreted solely as deaths or migration.

Bueng Kan (province code `38`) was established in 2011. It is correctly absent
before 2011; historical values have not been backcast.

## Source and intermediate files

- Source agency: Department of Provincial Administration (DOPA), Thailand
- Historical annual download page:
  <https://stat.bora.dopa.go.th/new_stat/webPage/statByProvince.php>
- Historical direct URL pattern:
  `https://stat.bora.dopa.go.th/new_stat/file/{BE_YEAR_2_DIGITS}12/{BE_YEAR_2_DIGITS}12cc{PROVINCE_CODE}.txt`
- Monthly download page:
  <https://stat.bora.dopa.go.th/new_stat/webPage/statByAgeMonth.php>
- Monthly direct URL pattern:
  `https://stat.bora.dopa.go.th/new_stat/file/{BE_YEAR_2_DIGITS}/1_{BE_YEAR_2_DIGITS}12.xls`
- `raw/dopa_population_age_historical/`: 1,446 pipe-delimited UTF-8 source
  files for 1994-2012, one per year and province.
- `raw/dopa_population_age/`: 2013-2025 source files. Despite the `.xls`
  extension, these are UTF-8 HTML tables.
- `interim/dopa_population_age_wide/`: direct CSV conversions of the source
  tables, with duplicate embedded tables removed.

Download or resume the historical archive with:

```sh
python scripts/download_historical_dopa_population_age.py
```

Rebuild and validate the combined CSV with:

```sh
python scripts/build_population_age_sex.py
```
