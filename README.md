# CSI 300 and six-city housing data, 2011–2025

This repository contains the input snapshot and three derived datasets used by the accompanying R Markdown analysis. The study covers Beijing, Shanghai, Hangzhou, Guangzhou, Shenzhen and Chengdu, with new and second-hand housing recorded separately. Stock data from September–December 2010 provide the history needed for early-2011 lagged returns.

## Download and run

1. Download this repository using **Code → Download ZIP**, then extract it.
2. Place the separately supplied `Ruiting_36461768_Assignment3.Rmd` in the extracted repository folder, alongside `data/` and this README. Keep the directory structure intact.
3. Open the Rmd in RStudio. Install the required R packages once if needed:

   ```r
   install.packages(c("rmarkdown", "knitr"))
   ```

4. Choose **Knit to HTML**, or run the following in R from this folder:

   ```r
   rmarkdown::render("Ruiting_36461768_Assignment3.Rmd", output_format = "html_document", encoding = "UTF-8")
   ```

R and Pandoc are required; RStudio supplies Pandoc. PDF knitting additionally needs a working LaTeX installation. Microsoft Word is not required: the four legacy documents already have DOCX format copies under `data/interim/housing/legacy_docx/`.

The Rmd reads the downloaded source files, reconstructs the monthly data and runs the analysis. It writes tables under `data/processed/` and figures under `results/report/`. The three supplied processed CSVs are reference outputs; they are not substitutes for the source inputs in the Rmd. The Rmd and written report are submitted separately through Moodle.

## Contents

| Location | Contents |
| --- | --- |
| `data/raw/stock/` | Two official CSI 300 daily JSON snapshots |
| `data/raw/housing/new/` | Two original DOC files and three DOCX files |
| `data/raw/housing/second_hand/` | Two original DOC files and the 2023 DOCX file |
| `data/raw/housing/second_hand/nbs_overall_2024_2025/` | 24 monthly NBS HTML pages and their exact source URLs |
| `data/interim/housing/legacy_docx/` | Four format-only DOCX conversions of the original DOC files |
| `data/processed/` | Stock monthly data (180 rows), housing monthly data (2,160 rows), merged analysis panel (2,160 rows) |
| `data/source_manifest.csv` | Source pages, coverage and original filenames for the included source datasets |
| `DATA_DICTIONARY.md` | Meaning of the processed variables |
| `SHA256SUMS.csv` | File hashes for checking the downloaded data snapshot |

## Original sources and attribution

This repository is a reproducibility mirror, not the original producer of the statistics.

- [CSI 300 official index page, China Securities Index Co., Ltd.](https://www.csindex.com.cn/#/indices/family/detail?indexCode=000300)
- [CIREA compilation of new-housing price indices](https://www.cirea.org.cn/content/4770)
- [CIREA compilation of second-hand housing price indices](https://www.cirea.org.cn/content/4773)
- National Bureau of Statistics monthly releases: exact links are recorded in [`source_urls.csv`](data/raw/housing/second_hand/nbs_overall_2024_2025/source_urls.csv).

Housing indices are the official month-on-month series with **previous month = 100**, not prices per square metre or citywide transaction-average prices. The stock and housing changes are both expressed as log changes in the derived CSVs. Original providers retain rights to their source material; this repository does not assign a new licence to third-party data.

## Preparation notes and limits

- The stock preparation excludes the `2011-01-01` placeholder observation.
- Cities are extracted by their names. HTML tables are selected by the overall second-hand housing title, matching month and month-on-month headers; selection does not depend on table order.
- Original DOC files are included for provenance; the Rmd reads their DOCX format copies.
- Unused floor-area-classified second-hand housing files for 2024–2025 and auxiliary stock validation files are outside this reproducibility package.
- Complete monthly stock coverage does not establish complete daily observations or verify that every selected month-end observation is the actual last trading day.
- For Word inputs, months are assigned sequentially from the declared start month and expected table count. Correct date alignment still depends on the original table order.
