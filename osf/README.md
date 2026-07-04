# Data

The dataset for this project is hosted on the Open Science Framework (OSF), not
in this Git repository.

- **OSF project:** <https://osf.io/a7523/>
- **DOI:** [10.17605/OSF.IO/A7523](https://doi.org/10.17605/OSF.IO/A7523)

## What to download

Download **`Data_PigeonEcon.csv`** from the OSF project and save it in this
folder, so the path is:

```
osf/Data_PigeonEcon.csv
```

`analysis.qmd` (in the repository root) reads the data from this location.

## About the file

`Data_PigeonEcon.csv` is **trial-level**: one row per completed trial. Key
columns include:

| Column | Meaning |
|:-------|:--------|
| `Pigeon` | Subject ID; a trailing `R` marks a replication condition (e.g., `126R`) |
| `Phase` | Manipulation phase(s); `1 | 2` / `4 | 5` mark transition conditions shared by two phases |
| `TokProdFR`, `ExchProdFR`, `Price`, `FreeToken`, `TokMag` | Condition parameters (token-production ratio, exchange-production ratio, token-exchange price, free tokens, reinforcement magnitude) |
| `TrialNum` | Trial index within a session; resets each session (`0` = priming row) |
| `TokAcc` | Tokens accumulated per exchange (accumulation outcome) |
| `TotalRft`, `TotTokProdResp` | Session cumulative food reinforcers and token-production responses (demand outcomes) |

The analysis reconstructs session boundaries from `TrialNum` and derives all
session-level measures, so this single file is sufficient to reproduce every
result.
