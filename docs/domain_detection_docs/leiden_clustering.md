# Leiden Clustering
--

This module performs Leiden clustering on spatial transcriptomics data using RAPIDS single-cell library with STAligner embeddings for neighbor graph construction.

## Overview

The Leiden clustering step includes:

- Neighbor Graph Construction - Build k-nearest neighbor graph using spatial embeddings
- Leiden Clustering - Apply Leiden algorithm with specified resolution
- UMAP Generation - Create 2D embedding for visualization
- Results Saving - Save clustered data with cluster assignments

## Input Files

- `*staligner*.h5ad` - Preprocessed AnnData file with STAligner embeddings 
- `params.json` - Configuration file with clustering parameters
- `res_params/params_{resolution}.json` - Resolution-specific parameter file

## Output Files

- `{specimen}_{dataset_id}_res_{resolution}_clustered.h5ad` - Clustered AnnData file saved to `results/clustered/`
- Ex: `mouse_638850_res_1.2_clustered.h5ad`

### Added Metadata Columns

**Clustering Results:**
* `leiden_res_{resolution}_knn_{n_neighbors}`: Leiden cluster assignments as categorical variable

**Dimensionality Reduction:**
* `X_umap`: UMAP coordinates stored in `.obsm` for 2D visualization

**Graph Connectivity:**
* Neighbor graph stored in `.obsp` and `.uns` for downstream analysis

## Configuration Parameters

The clustering parameters are specified in configuration files:

    {
    "domain_detection_params": {
        "grid_size": 30,
        "n_neighbors": 8,
        "cluster_key": "STAligner"
    },
    "metadata": {
        "specimen": "mouse",
        "dataset_id": "749485"
    }

**Resolution Parameters (`res_params/params_{resolution}.json`):**

{
    "resolution": "1.2"
}

### Parameter Descriptions

**Domain Detection Parameters:**
- `n_neighbors`: Number of nearest neighbors for graph construction 
- `cluster_key`: Key name for spatial embeddings in `.obsm` (e.g., "STAligner", "STAGATE")

**Resolution Parameter:**
- `resolution`: Leiden clustering resolution controlling cluster granularity

**Metadata Parameters:**
- `specimen`: Species name for output filename
- `dataset_id`: Dataset identifier for output filename
