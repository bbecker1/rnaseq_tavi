# RNA-seq Differential Expression Analysis

This repository contains the analysis code for an RNA sequencing (RNA-seq)
project using R, Quarto, and DESeq2.

The goal of the project is to perform differential gene expression analysis
based on transcript-level quantification and downstream
statistical and visualization workflows in R.

## Reproducibility (recommended)

Use `renv` to lock R and Bioconductor package versions.

```r
# Run once in the project root
renv::init()

# After installing/adjusting packages
renv::snapshot()
```

Restore a recorded environment on another machine:

```r
renv::restore()
```

### External artifacts to version or log

- `dat/h.all.v2023.2.Hs.symbols.gmt` (MSigDB Hallmark GMT)
- Enrichr database snapshot/date (logged in `res/logs/enrichr_version.txt`)
- Session info (logged in `res/logs/sessionInfo.txt`)
