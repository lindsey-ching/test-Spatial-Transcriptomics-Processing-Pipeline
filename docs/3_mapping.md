# Cell Type Mapping 
---
This module performs hierarchical and/or flat cell type mapping using the MapMyCells framework to assign cell type annotations based on reference atlas data.

### Overview
The mapping step includes:

- Data Validation - Validate input AnnData format and structure
- Gene Filtering - Optional removal of specified genes before mapping
- Cell Type Mapping - Run flat and/or hierarchical mapping algorithms
- Result Integration - Combine mapping results with original data
- Output Generation - Save annotated data with cell type assignments

### Input Files

- `*.h5ad` - Filtered AnnData file from previous processing steps (located in subdirectories of data directory)
- `*precomputed_stats*.h5` - Precomputed reference statistics file
- `*marker*.json` - Serialized marker gene lookup table
- `params.json` - Configuration file with mapping parameters

### Output Files
Single Mapping Mode (`flat` or `hrc`):

- `{section}_{mapping_acronym}_{mapping_type}.h5ad` - Mapped data saved to results/mapping_results/

Both Mapping Mode (`both`):

- `{section}_{mapping_acronym}_flat.h5ad` - Flat mapping results
- `{section}_{mapping_acronym}_hrc.h5ad` - Hierarchical mapping results
- `{section}_{mapping_acronym}_both.h5ad` - Combined flat and hierarchical results

Intermediate Files:

- `results/{mapping_acronym}_output/extended_results_{mapping_type}.json` - Detailed mapping results
- `results/{mapping_acronym}_output/basic_results_{mapping_type}.csv` - Summary mapping results
  
### Configuration Parameters
The mapping parameters are specified in mapping_params.json:
 "mapping_params": {
        "normalization": "raw",
        "drop_level": "CCN20230722_SUPT",
        "mapping_type": "both",
        "bootstrap_iteration": 100,
        "bootstrap_factor": 0.9,
        "n_runner_ups": 0,
        "n_processors": 32,
        "chunk_size": 10000,
        "clobber": true,
        "mapping_acronym": "mmc",
        "drop_genes_list": null
    }
### Parameter Descriptions
#### Core Parameters:

- `mapping_type`: Type of mapping to perform
  - `"flat"`: Flat mapping only
  - `"hrc"`: Hierarchical mapping only 
  - `"both"`: Run both flat and hierarchical mapping, combine results
- `mapping_acronym`: Short identifier for metadata columns (e.g., "mmc")

#### Gene Filtering:

- `drop_genes_list`: Optional comma-separated string of gene names to exclude from mapping
  - Format: "'Gene1','Gene2','Gene3'"
  - Leave empty to skip gene filtering
  
#### Mapping Algorithm:

- `drop_level`: A level to drop from the cell type taxonomy before doing the mapping
- `normalization`: Expression normalization method
  - `"log2CPM"`: Log2 counts per million 
  - `"raw"`: No normalization 
- `bootstrap_iteration`: The number of bootstrapping iterations to run at each node of the taxonomy tree
- `bootstrap_factor`: The factor by which to downsample the population of marker genes for each bootstrapping iteration
- `n_runner_ups`: Number of runner-up cell types to report for each assignment

#### Performance:

- `n_processors`: Number of CPU cores to use for parallel processing
- `chunk_size`: Number of cells to process in each batch
- `clobber`: Whether to overwrite existing output files (true/false)

### Output Columns
The mapping adds multiple columns to adata.obs with the format `{mapping_type}_{mapping_acronym}_{column}`:

'hrc_mmc_class_label'
'hrc_mmc_class_name'
'hrc_mmc_class_bootstrapping_probability'
'hrc_mmc_class_avg_correlation'

