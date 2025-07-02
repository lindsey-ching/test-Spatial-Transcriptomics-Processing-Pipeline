# Spatial Transcriptomics Processing Pipeline
---
This repository contains a comprehensive processing pipeline for spatial transcriptomics data analysis.

## Pipeline Overview

The processing pipeline consists of the following sequential steps:

### [Step 1: QC Filtering & Doublet Detection](./docs/1_qc_filtering.md)
Quality control filtering and doublet detection using basic thresholding and SOLO (Semi-supervised Outlier Detection).

### [Step 2: Calculate Incongruous Genes](./docs/2_calculate_inc_genes.md)
Analyze co-expression patterns of gene pairs that should not be expressed together in the same cell.

### [Step 3: Cell Type Mapping](./docs/3_mapping.md)
Perform MapMyCells cell type mapping. 

### [Step 4: Combine Sections](./docs/4_combine_sections.md)
Aggregate individual section-level AnnData files into a single combined dataset for whole-dataset analysis.

### [Step 5: Add Cell Type Colors](./docs/5_add_cell_type_colors.md)
Add color mappings for cell type classifications to AnnData objects using the ABC atlas color scheme.

### [Step 6: DoubleMAD Mapping Filtering](./docs/6_doublemad.md)
Perform quality control on cell type mapping results using Double Median Absolute Deviation (DoubleMAD) statistics to identify and filter cells with poor mapping confidence scores.

### [Step 7: Save Results](./docs/7_save_results.md)
Save final processed results from the pipeline.

## Quick Start

1. **Prerequisites**: Ensure all required dependencies are installed
2. **Configuration**: Update `params.json` with your specific parameters
3. **Execution**: Run steps sequentially, starting with Step 1
4. **Output**: Each step generates intermediate files for the next step

## File Structure

```

```

## Input/Output Flow


## Configuration

All pipeline parameters are centralized in `params.json`. Key parameter categories include:

- **Filtering Parameters**: QC thresholds and doublet detection settings
- **Mapping Parameters**:
- **DoubleMAD Parameters**: 
- **Metadata Parameters**:
- **Domain Detection Parameters**:

## Usage Notes

- Each step can be run independently if intermediate files are available
- All steps save comprehensive metadata and QC metrics
- Results are organized by section in the `results/sections/` directory
- Each step adds specific annotation columns to track processing history

## Dependencies

- Python 3.8+
- scanpy
- anndata
- pandas
- numpy
- scipy
- SOLO (for doublet detection)
- Additional dependencies listed in individual step documentation

## Support

For detailed information about each step, refer to the individual markdown files linked above. Each file contains:
- Detailed methodology description
- Input/output file specifications
- Configuration parameter explanations
- Expected results and metadata columns
