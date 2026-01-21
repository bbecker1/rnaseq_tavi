# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

RNA-seq differential expression analysis project using R, Quarto, and DESeq2. Analyzes transcript-level quantification from Salmon to identify differentially expressed genes across timepoints (A, V1, V2) in aortic valve samples.

## Key Commands

**Render the Quarto document:**
```bash
quarto render DEanalysis.qmd
```

**Run interactively in RStudio:**
Open `DEanalysis.Rproj` and execute code chunks in `DEanalysis.qmd`

## Architecture

### Data Pipeline
1. **Salmon quantification files** (`../../dat/salmon_files/*_quant.sf`) →
2. **tximport** (transcript to gene aggregation) →
3. **DESeq2** (normalization, DE testing) →
4. **clusterProfiler** (GO enrichment analysis)

### Analysis Flow in DEanalysis.qmd
- **Setup**: Load packages from external setup script (`../../org/setup_packages.R`)
- **Data Import**: Read Salmon files via tximport, metadata from Excel
- **QC**: PCA, sample correlation heatmaps using VST-transformed data
- **DE Analysis**:
  - Wald tests for pairwise comparisons (V1 vs A, V2 vs A, V2 vs V1)
  - LRT (Likelihood Ratio Test) for global timepoint effect
  - LFC shrinkage with apeglm/ashr
- **Functional Analysis**: GO ORA with clusterProfiler

### Caching Strategy
Heavy computations are cached as RDS files in `../../res/cache/`:
- `txi_salmon_tximport.rds` - tximport results
- `dds_DESeq_fitted.rds` - Fitted DESeq2 object (Wald)
- `dds_DESeq_LRT_fitted.rds` - Fitted DESeq2 object (LRT)
- `DESeq2_results_*.rds` - DE results
- `DESeq2_LFCshrink_*.rds` - Shrinkage results

Code checks for cache existence before recomputing.

### Directory Structure (relative to this folder)
- `../../dat/` - Input data (Salmon files, metadata Excel, tx2gene)
- `../../res/` - Output results (CSV tables, normalized counts)
- `../../res/cache/` - RDS cache files
- `../../org/` - Shared setup scripts

## Key R Packages
- DESeq2, tximport, apeglm, ashr - DE analysis
- clusterProfiler, org.Hs.eg.db - GO enrichment
- tidyverse, janitor - Data wrangling
- pheatmap, ggrepel, cowplot - Visualization
- DEGreport - Pattern clustering

## Design Notes
- Paired design: `~ pid + timepoint` accounts for patient-specific baselines
- Timepoint factor levels: A (baseline), V1, V2
- padj cutoff: 0.05
- Prefiltering: genes with rowSums(counts) >= 10
