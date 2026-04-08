# FITFR statistical consulting — collaboration project

This repository contains a full **R** workflow for **FITFR clinical trial** data: cleaning, exploratory analysis, primary models for continuous **AF** and binary **PR**, treatment arms A/B/C, covariates (age, sex), and exploratory **SNP** (`rs*`) analysis with FDR control. **Use the presentation R Markdown as the main deliverable**; the working draft is kept for comparison and extensions.

## Which file should I open?

| File | Purpose |
|------|---------|
| **`Rmd/analysis_presentation.Rmd`** | **Primary analysis / recommended for reproduction**: structured sections, baseline tables and group comparisons, AF/PR models, diagnostics and sensitivity, interactions and SNPs; exports to **`output/tables/`** (CSV, bullet summary) and **`output/figs/`** (PNG). |
| `Rmd/analysis.rmd` | **Working draft**: alternate EDA and modelling for the same data; figures go to **`figs/`** by default—useful for plot tweaks or experiments, not the same as the “official” export layout in `output/`. |

The repository root holds only the README and the RStudio project file. **All analysis source lives in `Rmd/`**; data and result folders remain at the **project root** (`raw-data/`, `derived-data/`, `figs/`, `output/`). Paths in the Rmd files do not use `../raw-data` thanks to `root.dir` in the setup chunk.

## Repository layout

```
collaboration-project/
├── README.md
├── collaboration-project.Rproj   # Open from repo root in RStudio
├── Rmd/
│   ├── analysis_presentation.Rmd # ← Prefer Knit / render
│   └── analysis.rmd              # Working draft
├── raw-data/
│   └── FITFR-final-data-v3.xlsx  # Shipped for full reproducibility
├── derived-data/                 # Intermediate cleaned objects (safe to delete and rebuild)
├── figs/                         # Figures from the working-draft Rmd (`analysis.rmd`)
├── output/                       # Presentation build: tables/, figs/
└── docs/                         # Reference PDFs (e.g. course materials)
```

## Requirements

- **R** (≥ 4.2 recommended) and [**Pandoc**](https://pandoc.org/installing.html) for Knit → HTML  
- Core packages: `readxl`, `dplyr`, `tidyr`, `stringr`, `ggplot2`, `broom`, `emmeans`, `forcats`, `scales`, `knitr`, `rmarkdown`  
- Optional: `logistf` (Firth logistic regression for PR if needed; code skips if missing)

```r
install.packages(c(
  "readxl", "dplyr", "tidyr", "stringr", "ggplot2", "broom",
  "emmeans", "forcats", "scales", "knitr", "rmarkdown"
), repos = "https://cloud.r-project.org")
```

## Reproduction

1. Clone the repo and confirm `raw-data/FITFR-final-data-v3.xlsx` is present.  
2. In RStudio, open **`collaboration-project.Rproj`**, then open `Rmd/analysis_presentation.Rmd` and click **Knit**.  
   Or from an R session whose working directory is the **project root**:
   ```r
   rmarkdown::render("Rmd/analysis_presentation.Rmd")
   rmarkdown::render("Rmd/analysis.rmd") # optional: working draft
   ```
3. The Rmd setup sets chunk `root.dir` to the project root, so relative paths such as `raw-data/` and `output/` remain valid when knitting from `Rmd/`.  
4. Without Pandoc, you can `knitr::purl("Rmd/analysis_presentation.Rmd")` and `source()` the extracted script from the project root (check figure paths in each file).

## Data availability

This **public** repository includes **`raw-data/FITFR-final-data-v3.xlsx`** for end-to-end reproduction. Use the data according to any terms set by the provider; do not attempt re-identification of individuals.

## License

License for the analysis code is at the maintainers’ discretion; data use is governed by the data provider’s agreement.
