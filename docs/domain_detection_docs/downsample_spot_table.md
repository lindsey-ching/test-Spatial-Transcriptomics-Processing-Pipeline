# Downsample Spot Table
---
This module spatially bins MERFISH transcript spots into a  grid and performs QC filtering.

## Overview
The downsample spot table step includes:

- Spatial Gridding - Bin transcript spots into grid cells
- QC Metrics Calculation - Calculate gene counts, transcript counts, and blank percentages per grid
- Quality Control Filtering - Apply configurable thresholds to identify high-quality grids for STAligner 
- Results Saving - Save gridded data as AnnData object with QC annotations

## Input Files
- `merfish_output/{experiment_id}/region_{region}/detected_transcripts.csv` - Detected transcripts CSV file from S3 bucket (or `legacy_output/` for specific experiments)
- `*.json` - Section metadata JSON file containing barcode, region, and experiment_id

## Output Files
`../results/downsampled/{section}_gridded.h5ad` - Gridded AnnData file with QC annotations

### Added Metadata Columns:

- `x_coords`: X-coordinate of grid cell center
- `y_coords`: Y-coordinate of grid cell center
- `obsm['spatial']`: Spatial coordinates matrix for grids
- `section`: Section identifier from metadata
- `n_genes_by_counts`: Number of genes detected per grid (including blanks)
- `total_counts`: Total transcript count per grid (including blanks)
- `pct_counts_blank`: Percentage of counts of blanks
- `n_genes_by_counts_no_blanks`: Gene count excluding blanks
- `total_counts_no_blanks`: Transcript count excluding blanks

QC Filter Columns:
- `n_genes_by_counts_qc_passed`: Boolean indicating if gene count threshold passed
- `total_counts_qc_passed`: Boolean indicating if transcript count threshold passed
- `pct_counts_blank_qc_passed`: Boolean indicating if blank percentage threshold passed
- `qc_passed`: Boolean indicating if all QC filters passed

## Configuration Parameters
The parameters are specified as command-line arguments:
- `--grid_size`: Grid cell size in micrometers
- `--bucket_name`: S3 bucket name containing transcript data
- `--object_key_template`: S3 object key template to transcripts file
- `--genes_thr`: Minimum number of genes required per grid
- `--transcripts_thr`: Minimum total transcript count per grid
- `--blanks_thr`: Maximum percentage of blanks per grid allowed
