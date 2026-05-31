# PRISM Drug Repurposing Screen Analysis

This repository contains a reproducible Jupyter notebook for a computational biology take-home assignment using raw PRISM Repurposing screen data from Corsello et al. 2020.

The goal is to start from raw plate-level MFI measurements and build a transparent workflow from quality control to normalized viability, hit calling, dose-response analysis, biomarker modeling, mechanism interpretation, and repurposing candidate prioritization.

## Analysis Philosophy

This notebook follows several principles:

1. Start from raw per-well MFI data.
2. Preserve raw data unchanged.
3. Inspect schemas before assuming column names.
4. Validate data structure before transformation.
5. Separate technical artifacts from biological signal.
6. Analyze primary and secondary screens as independent experiments.
7. Use simple, defensible methods before advanced models.
8. Avoid overclaiming biological mechanism or biomarker predictivity without validation.

## Current Progress

The notebook currently includes:

- project setup,
- raw file inventory,
- schema preview,
- primary MFI and metadata loading,
- primary well-metadata alignment,
- primary control checks,
- raw MFI distribution QC,
- control barcode NaN handling policy,
- primary cell-line QC,
- primary well-level QC,
- plate-level control separation,
- primary DMSO normalization MVP.

## Assignment Alignment

### 1. Primary Screen QC

Completed MVP:

- confirmed primary MFI columns map to treatment metadata,
- verified all detection plates contain vehicle and positive controls,
- checked global and plate-level separation between vehicle and positive controls,
- identified control barcode rows with 100% missing data,
- excluded control barcode rows from biological analysis rather than imputing,
- flagged high-missing wells and low-signal real cell lines.

### 2. Primary Screen Normalization and Hit Calling

In progress:

- computed plate-specific vehicle-control baselines,
- normalized primary log2 MFI values to DMSO controls,
- converted log2 fold-change to relative viability,
- confirmed vehicle controls center near viability = 1,
- confirmed positive controls shift below viability = 1.

Next step: primary hit calling.

### 3. Hit Triage

Planned.

### 4. Secondary Screen QC, Normalization, and Batch Correction

Planned.

### 5. Dose-Response Curve Fitting and Quality Assessment

Planned.

### 6. Selective Killing vs. Broad Cytotoxicity

Planned.

### 7. Linking and Predicting Drug Sensitivity from Cell Line Features

Planned.

### 8. Discovering Unexpected Mechanisms of Drug Action

Planned.

### 9. Prioritizing Repurposing Candidates

Planned.

## Data Policy

Raw data are not committed to this repository because the files are large. They should be stored locally in:

data/raw/

Generated outputs should be written to:

data/processed/
results/
reports/

These folders are excluded from Git.
