# Data Directory

This directory contains the LANTERN dataset files.

## Directory Structure

```
data/
├── LANTERN_MaskTif/          # Masked multiplex images (536 .tif files)
├── LANTERN_Segmentation/     # Nuclei segmentation data (1072 .mat files)
├── LANTERN_CellType/         # Cell type information (536 .mat files)
├── LANTERN_Clinical_Data.xlsx # Clinical data for all samples
└── processed/                # Processed data files (generated during analysis)
```

## Downloading Data

The data is available on Zenodo:

**DOI**: [10.5281/zenodo.7760826](https://doi.org/10.5281/zenodo.7760826)

### Instructions

1. Visit the Zenodo repository using the DOI link above
2. Download the following:
   - `LANTERN_MaskTif/` folder → Extract to `data/LANTERN_MaskTif/`
   - `LANTERN_Segmentation/` folder → Extract to `data/LANTERN_Segmentation/`
   - `LANTERN_CellType/` folder → Extract to `data/LANTERN_CellType/`
   - `LANTERN_Clinical_Data.xlsx` → Place in `data/`

### File Descriptions

- **LANTERN_MaskTif/**: Contains masked multiplex images of the IMC cores (536 .tif files)
- **LANTERN_Segmentation/**: Contains nuclei segmentation information (1072 .mat files)
- **LANTERN_CellType/**: Contains cell type information for each IMC core (536 .mat files)
- **LANTERN_Clinical_Data.xlsx**: Contains clinical data corresponding to the images

## Note

The data files are large and are not included in the Git repository. They must be downloaded separately from Zenodo.

