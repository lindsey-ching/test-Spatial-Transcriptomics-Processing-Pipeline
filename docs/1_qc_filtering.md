# QC Filtering & Doublet Detection
---

### Steps

Calculate genes per cell, mRNA transcripts per cell, Blanks per cell.
Apply filtering thresholds. (genes, mRNA, Blanks)
SOLO doublet detection

### Parameters
Min genes threshold, min transcripts threshold, max Blanks threshold.

### Columns Added

'n_genes_by_counts', 'total_counts', 'total_counts_Blank', 'pct_counts_Blank', 'total_counts_per_cell_volume', 'total_counts_Blank_per_cell_volume', 'genes_filter', 'mrna_filter', 'blanks_filter', 'basic_qc_filter', 'doublets_filter', 'filter', 'doublet', 'singlet', 'prediction', 'dif', 'doublets_thr'
