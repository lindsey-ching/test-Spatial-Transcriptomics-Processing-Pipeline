# Create Parameters JSON
--
This module creates a JSON parameter file for the spatial transcriptomics processing pipeline. The script takes command-line arguments and generates structured JSON configuration files that can be used by downstream analysis tools.

#### Filtering Parameters

| Argument | Type | Description |
|----------|------|-------------|
| `--n_genes_lower_thr` | int | Label cells with < n genes |
| `--n_spots_lower_thr` | int | Label cells with < n spots |
| `--n_spots_upper_thr` | int | Label cells with > n spots |
| `--volume_lower_thr` | int | Label cells with < n µm volume |
| `--pct_blanks_upper_thr` | int | Label cells with > n % blanks |
| `--doublets_thr` | str | Set doublets cutoff |
| `--run_incongruous_genes` | str | True to run incongruous genes step, False to skip |

### Mapping Parameters

| Argument | Type | Description |
|----------|------|-------------|
| `--normalization` | str | "raw" or "log2CPM" - normalization type for cell by gene data |
| `--drop_level` | str | Cell type taxonomy level to drop before mapping |
| `--mapping_type` | str | "hrc", "flat", or "both" - type of mapping to run |
| `--bootstrap_iteration` | int | Number of bootstrapping iterations per taxonomy tree node |
| `--bootstrap_factor` | float | Factor for downsampling marker gene population |
| `--n_processors` | int | Number of independent worker processes |
| `--chunk_size` | int | Number of cells per worker process |
| `--n_runners_up` | int | Number of runner-ups to generate |
| `--mapping_acronym` | str | Acronym for mapped column names and file names |
| `--clobber` | bool | True to overwrite existing results |
| `--drop_genes_list` | str | Comma-separated list of genes to drop from mapping |

### DoubleMAD Filtering Parameters

| Argument | Type | Description |
|----------|------|-------------|
| `--run_doublemad` | str | True to run DoubleMAD step, False to skip |
| `--doublemad_multiplier` | int | Integer multiplier for DoubleMAD threshold |

### Metadata Parameters

| Argument | Type | Description |
|----------|------|-------------|
| `--specimen` | str | Specimen type |
| `--dataset_id` | str | Dataset ID for .obs metadata |
| `--age` | str | Age for .obs metadata |
| `--sex` | str | Sex for .obs metadata |

### Domain Detection Parameters

| Argument | Type | Description |
|----------|------|-------------|
| `--grid_size` | int | Grid size for adding spatial clusters to cells |
| `--n_neighbors` | int | Number of neighbors for STAligner graph training |
| `--cluster_key` | str | Clustering key name (e.g., STAligner or STAGATE) |
| `--resolutions` | str | Comma-separated list of resolutions |

## Output Files

The script generates two types of JSON parameter files:

### 1. Main Parameters File
- **Location**: `../results/params/params.json`
- **Content**: Complete parameter configuration organized by category

### 2. Resolution-Specific Files
- **Location**: `../results/res_params/params_{resolution}.json`
- **Content**: Individual parameter files for each resolution specified
- **Purpose**: Enables job splitting by resolution

## JSON Structure

```json
{
    "domain_detection_params": {
        "grid_size": int,
        "n_neighbors": int,
        "cluster_key": "string"
    },
    "filtering_params": {
        "min": {
            "n_genes_by_counts": int,
            "total_counts": int,
            "volume": int
        },
        "max": {
            "total_counts": int,
            "pct_counts_blank": int
        },
        "doublets_cutoff": "string",
        "run_incongruous_genes": "string"
    },
    "mapping_params": {
        "normalization": "string",
        "drop_level": "string",
        "mapping_type": "string",
        "bootstrap_iteration": int,
        "bootstrap_factor": float,
        "n_runner_ups": int,
        "n_processors": int,
        "chunk_size": int,
        "clobber": boolean,
        "mapping_acronym": "string",
        "drop_genes_list": "string"
    },
    "doublemad_params": {
        "run_doublemad": "string",
        "doublemad_multiplier": int
    },
    "metadata": {
        "specimen": "string",
        "dataset_id": "string",
        "age": "string",
        "sex": "string"
    }
}
```
