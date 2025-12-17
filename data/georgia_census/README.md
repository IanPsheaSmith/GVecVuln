# Georgia Municipal Vulnerability Data

## Overview

This dataset contains socioeconomic vulnerability indicators for **64 municipalities** 
across **11 regions** of Georgia, sourced from the 
[National Statistics Office of Georgia (Geostat)](https://regions.geostat.ge/).

**Data downloaded:** 2025-12-17

## Dataset Summary

- **Total municipalities:** 64
- **Complete municipalities (all 6 components):** 0
- **Total Excel files:** 64

## Regions

| Region | Municipalities | Complete |
|--------|---------------|----------|
| adjara | 6 | 0 |
| guria | 3 | 0 |
| imereti | 12 | 0 |
| javaxeti | 6 | 0 |
| kakheti | 8 | 0 |
| mcxeta-mtianeti | 4 | 0 |
| qvemo-qartli | 7 | 0 |
| racha | 4 | 0 |
| samegrelo | 9 | 0 |
| shida-qartli | 4 | 0 |
| tbilisi | 1 | 0 |

## Vulnerability Components

Each municipality has up to 6 vulnerability indicator files:
1. **population_total.xlsx** - Total population by year (denominator for rate calculations)
2. **healthcare_staff.xlsx** - Healthcare staff per 1000 population
3. **education_graduates.xlsx** - Secondary school graduates per 1000
4. **age_dependency.xlsx** - Age dependency ratios (elderly/working age)
5. **disability_prevalence.xlsx** - Registered disability prevalence
6. **average_wages.xlsx** - Average monthly remuneration (economic vulnerability proxy)

## Folder Structure

```
georgia_census/
├── README.md
├── municipalities.csv      # Metadata for all municipalities
├── components.csv          # Component descriptions
├── adjara/
│   ├── batumi/
│   │   ├── population_total.xlsx
│   │   ├── healthcare_staff.xlsx
│   │   ├── education_graduates.xlsx
│   │   ├── age_dependency.xlsx
│   │   ├── disability_prevalence.xlsx
│   │   └── average_wages.xlsx
│   └── [other municipalities]/
├── guria/
├── imereti/
├── javaxeti/
├── kakheti/
├── mcxeta-mtianeti/
├── qvemo-qartli/
├── racha/
├── samegrelo/
├── shida-qartli/
└── tbilisi/
```

## Loading Data in R

### Option 1: Load from local clone

```r
library(tidyverse)
library(readxl)

# Set path to your local clone
data_path <- "path/to/GVecVuln/data/georgia_census"

# Load metadata
municipalities <- read_csv(file.path(data_path, "municipalities.csv"))

# Load all data for one municipality
load_municipality <- function(region, slug, data_path) {
    muni_path <- file.path(data_path, region, slug)
    files     <- list.files(muni_path, pattern = "\\.xlsx$", full.names = TRUE)
    
    files %>%
        set_names(str_remove(basename(.), "\\.xlsx$")) %>%
        map(read_excel)
}

# Example: Load Tbilisi data
tbilisi <- load_municipality("tbilisi", "tbilisi", data_path)
```

### Option 2: Load directly from GitHub

```r
source("https://raw.githubusercontent.com/IanPsheaSmith/GVecVuln/main/data/georgia_census/load_from_github.R")

# Load all data
georgia_data <- load_georgia_data()

# Or load specific region/municipality
tbilisi <- load_municipality_github("tbilisi", "tbilisi")
```

## Data Source

National Statistics Office of Georgia (Geostat)  
Regional Statistics Portal: https://regions.geostat.ge/

## Notes

- **Occupied territories** (Abkhazia and South Ossetia) are not included as data is unavailable
- **Tbilisi** is structured as a single municipality (capital city)
- Some municipalities may have fewer than 6 components if data was unavailable on source
- File naming uses Georgian transliteration (e.g., "qvemo-qartli" for "Kvemo Kartli")

## Citation

If using this data, please cite the original source:
> National Statistics Office of Georgia. Regional Statistics. https://regions.geostat.ge/
