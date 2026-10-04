# Single-Cell DNA Methylation Heterogeneity Analysis

Exploratory analysis of single-cell DNA methylation variability in mouse muscle stem cells using single-cell bisulfite sequencing (scBS-seq) data from GEO accession GSE121436.

## Project Overview

This project investigates observed DNA methylation variability at the single-cell level.

The analysis includes:

- Processing CpG methylation data from `.cov.gz` files
- Assessing CpG coverage across individual cells
- Quantifying observed methylation variability across cells
- Comparing methylation variability between young and old samples
- Exploring cell-level methylation profile divergence
- Evaluating reproducibility across biological samples

## Dataset

Data were obtained from GEO accession GSE121436, containing single-cell DNA methylation sequencing data from mouse muscle stem cells.

## Important Note

Because single-cell methylation data are sparse and biological replicates are limited, the analyses are primarily exploratory and descriptive. Observed variability should not be interpreted as definitive biological heterogeneity or an age effect.

Missing CpG observations are retained as missing values rather than being treated as unmethylated.

## Analysis Workflow

1. Data acquisition and file validation
2. CpG coverage assessment
3. Construction of methylation matrices
4. Quantification of CpG-level methylation variability
5. Cell-level methylation profile comparison
6. Comparison of young and old samples
7. Cross-sample comparison using shared high-coverage CpGs
8. Visualization and statistical exploration

## Reproducibility

The original analysis notebook is retained as part of the project record. A cleaned and documented version can be developed separately after the initial analysis.
