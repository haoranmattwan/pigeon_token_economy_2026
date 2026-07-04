# Pigeon Token Economy: Token Accumulation and Reinforcer Demand

Reproducible analysis code for:

> **Wan, H., Tan, L., & Hackenberg, T. D. (2026).** Behavioral economic analysis
> of pigeons' token accumulation and reinforcer demand in a laboratory-based
> token economy. *Journal of the Experimental Analysis of Behavior, 125*(2),
> e70095. <https://doi.org/10.1002/jeab.70095>

[![Article DOI](https://img.shields.io/badge/Article-10.1002%2Fjeab.70095-blue)](https://doi.org/10.1002/jeab.70095)
[![Data DOI](https://img.shields.io/badge/Data-10.17605%2FOSF.IO%2FA7523-informational)](https://doi.org/10.17605/OSF.IO/A7523)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## Overview

Six pigeons worked in a **closed token economy**: pecking a token-production key
produced tokens, which could be accumulated in a 60-token "bank" and later
exchanged for food. Across five phases, one economically meaningful variable was
manipulated at a time while the others were held constant:

| Phase | Manipulation | Economic analogue |
|:-----:|:-------------|:------------------|
| 1 | Token-production ratio | Labor requirement / wage (inverse) |
| 2 | Exchange-production ratio | Transaction cost |
| 3 | Token-exchange price | Price of the reinforcer |
| 4 | Number of free tokens | Nonlabor income / subsidy |
| 5 | Token-reinforcement magnitude | Wage |

Two outcomes are modeled with Bayesian multilevel (hierarchical) regression:

- **Token accumulation** (tokens per exchange) — **binomial** models.
- **Reinforcer demand** (food earned per session) — **negative binomial** models.

Effects are summarized by the posterior median (`Estimate`), posterior standard
deviation (`Est.Error`), and the probability of direction (`pd`).

## Repository contents

```
.
├── analysis.qmd        # Reproducible analysis (Quarto): data prep, models, figures, tables
├── osf/
│   └── README.md       # How to obtain the dataset from OSF
├── CITATION.cff        # Citation metadata ("Cite this repository")
├── LICENSE             # MIT License
├── PigeonEcon.Rproj    # RStudio project
└── README.md
```

Running `analysis.qmd` creates two output folders (git-ignored):
`models/` (cached model fits) and `figures/` (rendered figures and the
reconstructed appendix table).

## Data

The dataset is **not** stored in this repository. It is openly available on the
Open Science Framework:

- **OSF project:** <https://osf.io/a7523/>
- **DOI:** [10.17605/OSF.IO/A7523](https://doi.org/10.17605/OSF.IO/A7523)

Download **`Data_PigeonEcon.csv`** and place it in the `osf/` folder:

```
osf/Data_PigeonEcon.csv
```

The file is trial-level (one row per completed trial, plus a `TrialNum == 0`
priming row at the start of each session). `analysis.qmd` reconstructs the
session-level demand measures from the per-session cumulative totals, so no other
files are required.

## Reproducing the analysis

### Requirements

- **R** (≥ 4.2) and **Quarto** (≥ 1.3)
- A working **Stan** toolchain via
  [**cmdstanr**](https://mc-stan.org/cmdstanr/) (recommended, as in the
  published analysis) or **rstan**
- R packages: `tidyverse`, `brms`, `tidybayes`, `posterior`, `here`,
  `patchwork`, `knitr`

```r
install.packages(c("tidyverse", "brms", "tidybayes", "posterior",
                   "here", "patchwork", "knitr"))
# Stan backend (recommended):
install.packages("cmdstanr", repos = c("https://stan-dev.r-universe.dev", getOption("repos")))
cmdstanr::install_cmdstan()
```

### Render

From the repository root (with `osf/Data_PigeonEcon.csv` in place):

```bash
quarto render analysis.qmd
```

or, in R/RStudio, open `PigeonEcon.Rproj` and click **Render**.

The first render fits 14 Bayesian models and may take several minutes; fits are
cached under `models/`, so subsequent renders are fast. Model fitting uses a
fixed seed (`2026`) for reproducibility.

## What the analysis reproduces

- **Token accumulation** effects for all five phases (Figures 3–4 in the paper),
  including the earned-vs-total decomposition for free tokens and reinforcer
  magnitude.
- **Reinforcer demand** effects for all five phases (Figures 5–6).
- **Table 1** (experimental variables and their economic analogues) and a
  reconstruction of **Appendix Table A1** (per-condition performance means).

## How to cite

Please cite the article (above). This code may additionally be cited via
[`CITATION.cff`](CITATION.cff) — GitHub's "Cite this repository" button.

## License

Code in this repository is released under the [MIT License](LICENSE). The dataset
is distributed via OSF under its own terms; the published article is © the
publisher.

## Contact

**Haoran Wan** — <haoran.matt.wan@outlook.com> ·
ORCID [0000-0002-3434-3146](https://orcid.org/0000-0002-3434-3146)
