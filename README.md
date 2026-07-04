# Neurosurgery Operations Analysis — Regional Variation Study

Statistical analysis of neurosurgery operations across Saudi Arabia's regions, using real-world open data from King Faisal Specialist Hospital and Research Centre (KFSH&RC).

## Overview

This project investigates whether the number of neurosurgery operations differs significantly across Saudi Arabia's regions, using ANOVA and post-hoc Tukey HSD testing. The analysis also addresses a common statistical pitfall: raw operation counts are confounded by regional population size, so the study extends beyond the original scope to include population-normalized comparisons.

**Research question:** Does region have a statistically significant effect on the number of neurosurgery operations?

## Dataset

- **Source:** [Saudi Open Data Portal](https://od.data.gov.sa/) — published by KFSH&RC
- **Size:** 749 records (725 after cleaning)
- **Period:** January–March 2025
- **Fields:** year/month of operation, gender, nationality, marital status, region, facility, department

## Methodology

1. **Data cleaning** — removed missing/invalid region values (e.g. "Unknown", "Undefined")
2. **Descriptive statistics** — distributions across region, gender, marital status, and facility
3. **Hypothesis testing** — one-way ANOVA to test for regional differences in monthly operation counts
4. **Post-hoc analysis** — Tukey HSD to identify which specific regions differ from each other
5. **Population normalization** *(extension beyond the original analysis)* — operations per 100,000 residents, to control for the fact that larger regions naturally report more raw cases

## Key Findings

- ANOVA showed a statistically significant difference in monthly operations across regions (F = 17.39, p < 0.001)
- Tukey HSD identified the Central and Western regions as significantly different from the Eastern, Northern, and Southern regions
- **Population-adjusted results reverse the picture:** when normalized per 100,000 residents, the Northern Region has the highest rate of neurosurgery operations (5.13 per 100k) despite having the second-lowest raw count — while the Eastern Region, which ranked in the middle by raw count, drops to the lowest per-capita rate (1.40 per 100k)

| Region | Raw Operations | Operations per 100k |
|---|---|---|
| Central | 240 | 2.73 |
| Western | 210 | 2.69 |
| Southern | 120 | 3.43 |
| Northern | 82 | **5.13** |
| Eastern | 73 | 1.40 |

- This reversal suggests the raw-count ANOVA result is heavily confounded by regional population size and hospital capacity — most cases are concentrated at a single facility in Riyadh, so raw counts largely reflect where patients travel to for care rather than where neurosurgical need is highest. The per-capita view raises a more interesting open question: whether the Northern Region's elevated rate reflects genuine differences in incidence (e.g. trauma-related cases) or referral/reporting patterns, which raw counts alone cannot answer

## Tech Stack

- **Python:** pandas, numpy, matplotlib, seaborn, scipy, statsmodels
- **Original analysis:** R (dplyr, ggplot2, aov, TukeyHSD) — see `/r_version` for the original coursework version

## Project Structure

```
├── Neurosciences.ipynb          # Main Python analysis notebook
├── data/
│   └── A_list_of_OR_For_Neurosciences.xlsx
├── outputs/
│   ├── operations_by_region.png
│   ├── gender_distribution.png
│   ├── marital_distribution.png
│   └── tukey_hsd.png
├── r_version/
│   └── neurosurgery_analysis.Rmd
└── README.md
```

## How to Run

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels openpyxl
```

Then open `Neurosciences.ipynb` in Jupyter Notebook, JupyterLab, VS Code, or Google Colab, and run all cells in order.

## Limitations

- Data covers only 3 months (Q1 2025), limiting seasonal generalizability
- Raw operation counts are not adjusted for hospital capacity differences between facilities
- Population normalization uses regional population estimates; per-facility catchment area would give a more precise denominator
- Analysis is observational — it identifies association, not causation, between region and operation volume

## Author

Leena Alsaif — Data Science Student
Originally developed as coursework for a Statistical Analysis course; extended independently with Python implementation and population-adjusted analysis.
