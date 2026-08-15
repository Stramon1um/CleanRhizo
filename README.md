# CleanRhizo
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

CleanRhizo is a free, browser-based application for cleaning, organizing, and exploring root morphology data exported from WinRhizo (Regent Instruments). The tool is built with R and Shiny and deployed as a static web application via the shinylive and WebR frameworks, meaning it runs entirely within the user's browser without requiring any server-side infrastructure, software installation, or data upload to external services. CleanRhizo addresses a recurring bottleneck in root phenotyping workflows: the raw WinRhizo output file requires multiple preprocessing steps — column selection, sub-header removal, treatment name decoding from sample identifiers, and format conversion — before it is suitable for downstream statistical analysis. The application automates these steps through a guided, step-by-step interface and produces tidy datasets in wide or long format, along with exploratory bar charts. CleanRhizo is available in English, Italian, Spanish, and French.

## License
This project is licensed under the [MIT License](LICENSE).