# CleanRhizo 🧹

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21894026.svg)](https://doi.org/10.5281/zenodo.21894026)
[![Launch app](https://img.shields.io/badge/Launch-CleanRhizo-3A6B35)](https://www.mauromaver.eu/CleanRhizo/)

**▶ Use it online: <https://www.mauromaver.eu/CleanRhizo/>**

CleanRhizo is a free, browser-based application for cleaning, organizing, and exploring root morphology data exported from [WinRhizo](https://www.regentinstruments.com/assets/winrhizo_mostrecent.html) (Regent Instruments). The tool is built with R and Shiny and deployed as a static web application via the shinylive and WebR frameworks, meaning it runs entirely within the user's browser without requiring any server-side infrastructure, software installation, or data upload to external services.

CleanRhizo addresses a recurring bottleneck in root phenotyping workflows: the raw WinRhizo output file requires multiple preprocessing steps (column selection, sub-header removal, treatment name decoding from sample identifiers, and format conversion) before it is suitable for downstream statistical analysis. The application automates these steps through a guided, step-by-step interface and produces tidy datasets in wide or long format, along with exploratory bar charts. CleanRhizo is available in English, Italian, Spanish, and French.

## Privacy

Your data never leave your computer. The file you load is processed locally by R compiled to WebAssembly (WebR); nothing is sent to a server. The first launch may take a few seconds while the R environment loads.

## Workflow

1. **Load** the `.txt` file exported by WinRhizo.
2. **Select columns** to keep. The main morphological traits are preselected: `Length(cm)`, `SurfArea(cm2)`, `AvgDiam(mm)`, `RootVolume(cm3)`, `Tips`, `Forks`, `Crossings`.
3. **Clean**: sub-header rows are removed and columns are renamed (`SampleId`, `datetime`).
4. **Assign treatments and replicates** decoded from the sample name (see below). Each detected treatment can be renamed manually.
5. **Export** a tidy CSV in wide or long format (`parameter`, `value`).
6. **Explore** with bar charts (mean ± SE per treatment, optional individual points), downloadable as PNG at 300 dpi.

## Naming your samples in WinRhizo

CleanRhizo reads treatment and replicate information from the sample identifier. Three schemes are supported:

| Scheme | Example | Result |
|---|---|---|
| Treatment_Replicate | `UREA_3` | treatment `UREA`, replicate 3 |
| Treatment.Pot.Plant | `100_PPM_UREA.2.1` | treatment `100_PPM_UREA`, pot 2, plant 1 |
| Manual | any structure | you assign a role (treatment, pot, plant, ignore) to each part of the name |

Recommended convention: use `_` to join the words of the treatment name and `.` to introduce the replicate numbers. This keeps the boundary between name and numbers unambiguous (`100_PPM_UREA_1_2` is ambiguous, `100_PPM_UREA.1.2` is not).

### Biological vs technical replicates

With the Pot/Plant scheme the **pot** is the biological replicate (the experimental unit) and the **plant** is a technical replicate. In the exploratory chart, plants from the same pot are first averaged, so mean, SE and *n* refer to pots. The exported CSV keeps one row per plant, so you can model the pot level explicitly in your own analysis (e.g. by averaging per pot or with a mixed model including pot as a random effect).

The chart is meant for quick quality control and is not a substitute for proper statistical analysis.

## Input file

- Tab-delimited `.txt` exported by WinRhizo; the first column (`RHIZO <version>`, e.g. `RHIZO 2021a`) holds the sample identifier.
- Any WinRhizo version and any number of sub-header rows are accepted; data rows are detected from their content.
- Decimal point or decimal comma are both accepted (commas are converted to points).

## Output

| File | Content |
|---|---|
| `<name>_clean.csv` | selected columns, cleaned |
| `<name>_treatments.csv` | plus `treatment` and `replicate` (or `pot` and `plant`) columns |
| `<name>_final.csv` | final dataset, wide or long format |
| `<name>_chart.png` | exploratory chart, 300 dpi |

CSV files use `;` as separator and `.` as decimal mark.

## How to cite

If you use CleanRhizo in your research, please cite it:

> Maver, M. (2026). *CleanRhizo: a browser-based tool for WinRhizo root morphology data cleaning and exploration*. Zenodo. <https://doi.org/10.5281/zenodo.21894026>

```bibtex
@software{maver_cleanrhizo_2026,
  author    = {Maver, Mauro},
  title     = {CleanRhizo: a browser-based tool for WinRhizo root morphology data cleaning and exploration},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.21894026},
  url       = {https://doi.org/10.5281/zenodo.21894026}
}
```

The DOI above always resolves to the latest version. Version 1.0 has its own DOI: [10.5281/zenodo.21894027](https://doi.org/10.5281/zenodo.21894027).

## Run or build locally

The whole app lives in `CleanRhizo.qmd` (a single `shinylive-r` chunk). To rebuild the site you need [Quarto](https://quarto.org) and the R packages `shinylive`, `shiny` and `bslib`:

```bash
quarto render      # writes the static site to docs/
quarto preview     # local preview (WebR needs a web server, not file://)
```

The site in `docs/` is published with GitHub Pages.

## Related apps

CleanRhizo is part of a small family of browser-based tools for plant phenotyping data:

- [CleanEX](https://www.mauromaver.eu/CleanEX/) ([repository](https://github.com/Stramon1um/CleanEX)): Dualex leaf optical data
- [CleanSpeX](https://www.mauromaver.eu/CleanSpeX/) ([repository](https://github.com/Stramon1um/CleanSpeX)): PlantEye F600 (Phenospex) multispectral 3D data

## Changes

See [CHANGELOG.md](CHANGELOG.md).

## Contact

Mauro Maver, University of Verona ([mauromaver.eu](https://www.mauromaver.eu), ORCID [0000-0002-8162-3618](https://orcid.org/0000-0002-8162-3618)).
Bug reports and suggestions: [GitHub issues](https://github.com/Stramon1um/CleanRhizo/issues) or [email](mailto:mauro.maver@univr.it).

## License

This project is licensed under the [MIT License](LICENSE).
