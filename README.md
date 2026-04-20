# GVecVuln

**Vector distribution modelling, social vulnerability and risk assessment for the Republic of Georgia**

This repository accompanies the manuscript *Predicting Areas of Potential Vector Surveillance Priority Across the Country of Georgia Using Mosquito, Tick and Human Census Data* (Pshea‑Smith et al., in preparation). It contains the underlying data, analytical pipeline and supplementary visualisations used in the study.

An interactive landing page summarising the project, with embedded maps and figures, is available at:
**https://ianpsheasmith.github.io/GVecVuln**

---

## Project summary

The project models the habitat suitability of sixteen mosquito and tick species of public health relevance across the country of Georgia (Caucasus region), using boosted regression trees (BRTs) and ensembles of small models (ESMs) scaled by sample size. Species-level suitability predictions are combined into weighted exposure indices for eight pathogen–vector groups, and then integrated with a census-derived social vulnerability index (SVI) to produce a municipality-level risk surface following an INFORM-parallel framework. Outputs are summarised at the scale of Georgia's 64 administrative municipalities (*rayonii*).

---

## Repository contents

| Path | Description |
| --- | --- |
| `index.html` | Landing page for the project (served via GitHub Pages). |
| `Data_and_Code/RCode.Rmd` | R Markdown pipeline covering covariate preparation, species distribution modelling, social vulnerability index construction, Monte Carlo risk aggregation, and figure/map generation. |
| `Data_and_Code/Species_Occurrence_Points.csv` | Cleaned, deduplicated geo-referenced occurrence records for the sixteen modelled vector species. Source records were compiled from VectorMap, the Global Biodiversity Information Facility (GBIF) and a previously published regional tick dataset. |
| `Data_and_Code/Municipality_Data.csv` | Municipality-level covariates and indicators used in the social vulnerability index, aggregated from the Georgian National Statistics Office (regions.geostat.ge) and harmonised to the 64-municipality taxonomy. |
| `Figures/` | Publication-quality figures (TIFF) and web-optimised PNG duplicates. Includes three interactive Leaflet maps (`Fig1.html`, `Fig3.html`, `Fig5.html`) corresponding to the occurrence, social vulnerability and risk figures in the manuscript. |

---

## Reproducing the analysis

The full pipeline is contained in `Data_and_Code/RCode.Rmd` and was developed under R 4.5.1. The primary dependencies include `terra`, `sf`, `exactextractr`, `dismo`, `gbm`, `ecospat`, `biomod2`, `dynamicSDM`, `truncnorm`, `dplyr`, `ggplot2` and `tidyterra`. Climate covariates are sourced from CHELSA v2.1, and administrative boundaries follow the 64-municipality GeoJSON taxonomy distributed by the Georgian National Statistics Office.

To reproduce the analysis, clone the repository, open `RCode.Rmd` in RStudio, and knit the document. Runtime is dominated by BRT fitting across 100 pseudo-absence iterations per species and Monte Carlo risk aggregation across 1,000 iterations; on a modern workstation, end-to-end execution is on the order of several hours.

---

## Interactive maps

Three interactive Leaflet maps are included as standalone HTML files under `Figures/`, and are linked from the landing page:

- `Fig1.html` — Country context and vector occurrence points
- `Fig3.html` — Social vulnerability index with per-indicator dropdowns
- `Fig5.html` — Final integrated risk index

These are hosted directly via GitHub Pages and do not require a local server to view.

---

## Citation

> Pshea‑Smith IA, Kotorashvili A, Kotaria N, Golubiani G, Kirkitadze G, Chunashvili T, Shubashvili A, Di Paola N, Kugelman J, Hulseberg C, Walker B, Musich T, Ash KD, Hamerlinck G, Cleary NG, Bissainte D, Nurczyk B, Reinbold-Wasson D, Denlinger DS, Blackburn JK, von Fricken ME. *Predicting Areas of Potential Vector Surveillance Priority Across the Country of Georgia Using Mosquito, Tick and Human Census Data.* In preparation.

Please cite the manuscript if you reuse code, data, or figures from this repository. The citation block will be updated to include a DOI once the manuscript is published.

---

## Funding

This work was supported by the Armed Forces Health Surveillance Division's Global Emerging Infections Surveillance (AFHSD GEIS) programme (awards P0020_23_GA, P0032_24_GA, P0056_25_GA), and in part through the DoD Information Analysis Center Multiple Award Contract (No. FA807518D0005-FA807523F0016). The complete funding statement and disclaimer accompany the published manuscript.

---

## Contact

**Ian A. Pshea‑Smith** — Spatial Ecology and Epidemiology Research Laboratory, Department of Geography, University of Florida
`ianpsheasmith@ufl.edu`

**Michael E. von Fricken** (corresponding author) — Department of Environmental and Global Health, University of Florida
`mvonf@ufl.edu`
