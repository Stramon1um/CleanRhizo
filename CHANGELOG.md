# Changelog

## v1.1 (in preparation)

### Statistics
- **Exploratory chart: no more pseudoreplication.** With the Pot/Plant scheme (including the manual scheme) plants from the same pot are first averaged per pot; mean, SE and jitter points are computed across pots (biological replicates). In v1.0 the SE treated plants as replicates and was therefore underestimated.
- X-axis labels now show the number of replicates, e.g. `CTRL (n=3)`.
- Explanatory note (in all 4 languages) above the chart when a `pot` column is present.
- No error bar is drawn when n = 1 (previously a zero-length arrow was drawn).

### Reading the WinRhizo file
- The first column is always renamed `SampleId`, whatever the WinRhizo version (`RHIZO 2019a`, `RHIZO 2021a`, ...). In v1.0 only `RHIZO 2021a` was recognized; with other versions the sample identifier was excluded.
- Data rows are detected from their content (numeric values in the morphological columns) instead of a fixed position: no sample is lost and no spurious row is added when there are not exactly 4 sub-header rows.
- Decimal commas (`12,345`) are automatically converted to points.
- A UTF-8 BOM at the start of the file is handled.

### Interface
- When changing language, sample ID scheme or the roles in the manual scheme, the following stay visible and consistent: selected columns, custom treatment names, long/jitter toggles, chart parameters. In v1.0 the controls were reset to their defaults while the app kept using the previous choices.
- IDs of the "custom treatment" fields are based on row and upload: sample IDs such as `A.1` and `A_1` no longer share the same field, and a new file no longer inherits the custom names of the previous one.
- Label of scheme 2 aligned with the recommended convention: `Treatment.Pot.Plant`.

### Export
- Distinct file names for each step: `_clean.csv` (step 3), `_treatments.csv` (step 4), `_final.csv` (step 5).
- CSV: quotes are added only to fields containing `;`, quotes or line breaks.

## v1.0 (2026-08-11)
- First public release. DOI: [10.5281/zenodo.21894027](https://doi.org/10.5281/zenodo.21894027)
