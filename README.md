# PRISM Drug Repurposing Screen Analysis

This repository contains a reproducible Jupyter notebook for a computational biology take-home assignment using PRISM Repurposing screen data from Corsello et al. 2020.

The goal is to start from raw plate-level MFI measurements and build a transparent workflow from quality control through normalization, hit calling, triage, secondary-screen QC, dose-response modeling framework, biomarker analysis, mechanism interpretation, and final repurposing prioritization.

## Repository Structure

```text
.
├── README.md
├── .gitignore
└── notebooks/
    └── prism_repurposing_analysis.ipynb
```

Raw data are not committed to this repository because the files are large. The notebook expects raw data to be available locally in:

```text
data/raw/
```

## Main Notebook

The complete analysis is in:

```text
notebooks/prism_repurposing_analysis.ipynb
```

The notebook has been run top-to-bottom successfully.

## Completed Analysis Sections

### 1. Primary Screen QC

Completed:

- loaded primary raw MFI and metadata files,
- validated MFI column alignment with treatment metadata,
- checked detection plates, vehicle controls, and positive controls,
- inspected raw MFI and log2 MFI distributions,
- identified control barcode rows,
- excluded non-biological control barcode rows from biological analysis,
- flagged high-missing wells and low-signal cell lines,
- evaluated plate-level control separation.

### 2. Primary Normalization and Hit Calling

Completed:

- computed plate-specific DMSO/vehicle-control baselines,
- normalized primary MFI to log2 fold change and relative viability,
- validated that vehicle controls center near viability 1,
- validated that positive controls show reduced viability,
- collapsed replicate treatment wells by compound and cell line,
- applied a paper-aligned primary sensitivity threshold using median viability `< 0.30`,
- required replicate support for conservative MVP hit calling.

### 3. Hit Triage

Completed:

- summarized compound-level primary activity,
- classified compounds by activity breadth,
- identified MVP triage candidates,
- compared MVP triage candidates to compounds present in the secondary-screen metadata,
- quantified overlap and disagreement between MVP selection and actual secondary follow-up.

### 4. Secondary Screen QC, Normalization, and Batch-Correction Assessment

Completed:

- loaded secondary MFI and metadata files,
- inspected secondary schemas,
- identified that secondary MFI columns use raw plate/well/screen identifiers,
- mapped most secondary MFI plate names to treatment plate names,
- quantified unmapped secondary MFI columns,
- showed that secondary treatment metadata lacks well-position columns,
- documented that well-level compound/dose normalization from raw secondary MFI is unsafe without an explicit secondary plate map.

### 5. Dose-Response Curve Fitting Framework

Completed:

- implemented a reusable four-parameter logistic dose-response model with the top asymptote fixed at 1,
- implemented AUC calculation over log-dose,
- validated the fitting function on a synthetic eight-point dose-response example,
- documented that real secondary dose-response fitting requires compound-cell-line normalized viability values that cannot be safely reconstructed from the provided raw secondary files alone.

### 6. Selective Killing vs Broad Cytotoxicity

Completed:

- classified compounds into no detected activity, rare selective activity, selective/moderate activity, broad activity, and near-pan-active groups,
- distinguished selective activity from broad cytotoxicity,
- identified selective candidates and near-pan-active compounds,
- visualized activity breadth across compounds.

### 7. Biomarkers and Prediction

Completed:

- loaded CCLE mutation, expression, copy-number, and sample metadata tables,
- validated cell-line identifier overlap using DepMap IDs,
- joined PRISM sensitivity calls to lineage annotations,
- performed an MVP lineage-enrichment analysis for a selected compound,
- applied Fisher exact testing and Benjamini-Hochberg correction,
- interpreted results cautiously as hypothesis-generating rather than validated biomarkers.

### 8. Unexpected Mechanisms

Completed:

- combined primary selectivity summaries with compound annotations,
- identified compounds with selective activity and no obvious oncology annotation,
- summarized unexpected mechanism candidates by clinical phase,
- highlighted clinically launched or advanced compounds as repurposing hypotheses,
- documented annotation incompleteness as a key limitation.

### 9. Final Prioritization

Completed:

- integrated selectivity, potency, secondary follow-up status, clinical phase, and repurposing potential,
- created a transparent heuristic priority score,
- generated a final MVP candidate shortlist,
- emphasized that prioritization is for follow-up, not clinical recommendation.

## Key MVP Results

The notebook produces a complete assignment MVP with:

- primary-screen QC and normalization,
- paper-aligned primary hit calling,
- compound-level triage,
- secondary-screen schema validation,
- dose-response fitting framework,
- selectivity analysis,
- lineage biomarker workflow,
- unexpected mechanism candidate search,
- final prioritization table.

Important quantitative outputs include:

- 578 real primary cell-line rows after excluding control barcode rows,
- 4,686 unique primary compounds summarized,
- 1,701 MVP primary triage candidates,
- 1,162 compounds selected by both MVP triage and secondary metadata overlap,
- 1,390 final MVP prioritization candidates,
- 881 final MVP candidates present in secondary follow-up metadata.

## Important Limitation

The secondary raw MFI files could not be safely converted into compound-cell-line dose-response viability profiles because the provided secondary treatment metadata does not include well-position columns.

The secondary MFI matrix encodes raw plate/well/screen identifiers, while the secondary treatment metadata encodes compound/dose/screen/compound-plate annotations. Plate/screen counts do not match one-to-one, so an order-based mapping would risk assigning raw MFI measurements to incorrect compounds or doses.

For that reason, this notebook performs secondary raw-MFI QC and implements a dose-response fitting framework, but does not claim fitted secondary dose-response results from the raw MFI matrix without a well-level secondary plate map.

## Reproducibility

To reproduce the analysis:

1. Clone the repository.
2. Place the raw assignment data in:

```text
data/raw/
```

3. Open:

```text
notebooks/prism_repurposing_analysis.ipynb
```

4. Run the notebook top-to-bottom.

The notebook was developed and run in a local Python/Jupyter environment with standard scientific Python packages, including:

- pandas
- numpy
- scipy
- matplotlib

## Data Policy

Raw data and generated outputs are not committed to Git. The repository tracks only source documentation and the analysis notebook.

Expected local folders:

```text
data/raw/
data/processed/
results/
reports/
```

These folders should remain excluded from Git.
