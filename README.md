# Single-Cell DNA Methylation Heterogeneity Analysis

An exploratory computational analysis of observed cell-to-cell DNA methylation variability using single-cell bisulfite sequencing (scBS-seq) data from mouse muscle stem cells.

The project develops a reproducible Python workflow for assessing CpG coverage, constructing methylation matrices, identifying shared high-coverage CpGs, quantifying observed methylation variability, and comparing variability between individual mice.

---

## Project Overview

DNA methylation is an important epigenetic regulatory mechanism. Single-cell measurements allow methylation patterns to be examined across individual cells rather than only as averages across a population.

This project explores **observed cell-to-cell methylation variability** using publicly available single-cell DNA methylation data.

The workflow includes:

1. Processing `.cov.gz` methylation files
2. Assessing CpG coverage across cells
3. Constructing cell × CpG methylation matrices
4. Applying CpG coverage criteria
5. Quantifying CpG-level methylation variability using standard deviation
6. Comparing methylation variability between individual cells
7. Identifying CpGs shared across analyzed mice
8. Comparing observed variability between individual mice
9. Generating summary tables and visualizations
10. Documenting methodological limitations and interpretation

---

## Data Source

**GEO accession:** GSE121436  
**Organism:** *Mus musculus*  
**Data type:** Single-cell bisulfite sequencing (scBS-seq)

The original study contains data from:

- **3 old mice:** O1, O5, O8
- **3 young mice:** Y2, Y7, Y8
- **10 cells per mouse**
- **60 cells in total**

The original `.cov.gz` data are approximately 1.6 GB and are **not included in this repository**.

The data can be obtained from GEO accession **GSE121436**.

### Original study

Hernando-Herraez I, et al. *Ageing affects DNA methylation drift and transcriptional cell-to-cell variability in mouse muscle stem cells.* Nature Communications (2019).

---

## Data Analyzed in This Project

This repository contains an analysis of a **subset of the original dataset**.

The final analysis focused on:

- **O1 — old mouse**
- **O8 — old mouse**
- **Y2 — young mouse**

The other mice in the original study (**O5, Y7, and Y8**) were **not included in the final analysis presented in this repository**.

For each analyzed mouse, the available single-cell `.cov.gz` files were processed to assess CpG coverage and methylation variability.

### Matched-CpG analysis

CpGs were retained for the final cross-mouse comparison when they were covered in at least **8 cells** within each of the three analyzed mice.

This resulted in:

**102 CpGs shared across O1, O8, and Y2.**

Because cells are nested within individual mice, the **mouse is treated as the biological replicate** rather than treating individual cells as independent biological replicates.

---

## Methods

### CpG Coverage

CpG observations were extracted from the `.cov.gz` files.

Coverage was assessed across cells, and CpGs meeting the predefined coverage criterion were retained for downstream analysis.

For the final matched comparison, a CpG had to be observed in at least **8 cells** within each analyzed mouse.

Missing CpG observations were retained as missing values rather than being interpreted as unmethylated.

### Methylation Variability

For each matched CpG, observed methylation variability was quantified as the **standard deviation (SD)** of methylation percentages across cells.

The analysis therefore describes:

> **Observed methylation variability**

rather than assuming that every observed difference represents biological epigenetic heterogeneity.

---

## Results

Across the **102 CpGs shared by O1, O8, and Y2**, the mean observed methylation variability was:

| Mouse | Age group | Matched CpGs | Mean SD (percentage points) | Median SD |
|---|---|---:|---:|---:|
| O1 | Old | 102 | 6.92 | 0.00 |
| O8 | Old | 102 | 5.25 | 0.00 |
| Y2 | Young | 102 | 7.98 | 0.00 |

Y2 showed the highest mean observed methylation variability among the three analyzed mice, while O8 showed the lowest.

These results are **descriptive comparisons between individual mice** and do not establish an age-associated effect.

The median SD was 0 for all three mice, indicating that many of the matched CpGs showed little or no observed cell-to-cell variability.

---

## Visualizations

The repository contains two figures:

### O1 vs O8 matched-CpG variability

A scatter plot comparing CpG-level methylation variability between O1 and O8 across the matched CpGs.

### Three-mouse comparison

A bar plot comparing mean observed methylation variability across the 102 CpGs shared by O1, O8, and Y2.

Both figures are available in the [`figures/`](figures/) directory.

---

## Statistical Considerations

The original study contains three biological replicates per age group.

With only **3 mice per group**, the smallest possible two-sided exact Mann–Whitney U p-value is **0.1**. Therefore, mouse-level statistical inference is severely limited.

The present analysis is consequently **descriptive and exploratory**.

The 102 matched CpGs should not be interpreted as 102 independent biological replicates because they represent measurements nested within individual mice.

---

## Limitations

- The final analysis includes only **three individual mice: O1, O8, and Y2**.
- O5, Y7, and Y8 from the original study were not included in the final analysis.
- The analysis therefore does not provide a complete comparison of all mice in the original dataset.
- Cells are nested within mice and cannot be treated as independent biological replicates for age-level inference.
- Single-cell bisulfite sequencing data are sparse, with many CpGs observed in only a subset of cells.
- Sequencing depth can influence observed methylation percentages and variability.
- Missing CpG observations were retained as missing rather than treated as unmethylated.
- The matched analysis was restricted to CpGs satisfying the coverage criterion in all three analyzed mice.
- Coverage thresholds and filtering choices can influence the resulting CpG set and variability estimates.
- The final matched analysis represents a subset of the CpGs observed in the original dataset.
- The results are exploratory and do not establish a statistically significant age-associated effect.

---

## Reproducibility

The final analysis notebook is provided as:

[`sc_epigenetic_drift.ipynb`](sc_epigenetic_drift.ipynb)

To reproduce the analysis:

1. Obtain the required `.cov.gz` files for the analyzed samples from GEO accession **GSE121436**.
2. Place the files in the appropriate data directory.
3. Open `sc_epigenetic_drift.ipynb` in Google Colab or a compatible Jupyter environment.
4. Set the `DATA_DIR` variable to the location of the downloaded data.
5. Install the required Python packages if necessary.
6. Run the notebook cells from top to bottom.

### Software

The analysis uses Python and the following scientific-computing libraries:

- Python
- NumPy
- pandas
- Matplotlib
- SciPy

---

## Repository Structure

```text
sc-epigenetic-drift/
│
├── README.md
├── sc_epigenetic_drift.ipynb
│
└── figures/
    ├── o1_vs_o8_matched_variability.png
    └── o1_o8_y2_variability_comparison.png
