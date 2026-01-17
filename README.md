# Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network (LANTERN)

<img src='docs/sample_fig.png' width=100%>

**LANTERN** (Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network) - This repository includes codes and data used for spatial analysis of lung adenocarcinoma tumor-immune microenvironments.

## Summary

Single-cell technologies have revealed the complexity of the tumour immune microenvironment with unparalleled resolution. Most clinical strategies rely on histopathological stratification of tumour subtypes, yet the spatial context of single-cell phenotypes within these stratified subgroups is poorly understood. This project applies imaging mass cytometry to characterize the tumour and immunological landscape of 416 lung adenocarcinoma patient tumours across five histological patterns. We resolve >1.6 million cells, enabling spatial analysis of immune lineages and activation states with distinct clinical correlates, including survival. Using deep learning, we can predict with high accuracy which patients will progress after surgery using a single 1 mm² tumour core, which could be informative for clinical management following surgical resection.

This dataset represents a valuable resource for the NSCLC research community and exemplifies the utility of spatial resolution within single-cell analyses. This study also highlights how artificial intelligence can improve our understanding of microenvironmental features that underlie cancer progression and may influence future clinical practice.

## Repository Structure

This repository contains all three analysis components from the original Nature paper:

```
LANTERN/
├── cell_segmentation/      # Cell Segmentation Module (MATLAB + Python)
│   ├── Lib/                # Segmentation libraries (MaskRCNN, etc.)
│   ├── ConfigFiles/        # Configuration files
│   └── README.md           # Segmentation module documentation
├── cell_phenotyping/       # Cell Phenotyping Module (MATLAB)
│   ├── Lib/                # Phenotyping libraries
│   ├── ConfigFiles/        # Configuration files and rule tables
│   └── README.md           # Phenotyping module documentation
├── micro_environment_prediction/  # Micro Environment Prediction (Python/Jupyter)
│   ├── prediction_416.ipynb      # Main prediction analysis for all 416 samples
│   ├── prediction_416_freq.ipynb # Frequency-based analysis
│   ├── prediction_stage1.ipynb  # Stage 1 specific analysis
│   ├── prediction_stage1_freq.ipynb  # Stage 1 frequency analysis
│   └── resnet_architecture.ipynb    # ResNet deep learning architecture
├── data/                   # Data directory (see Data Setup)
│   ├── LANTERN_MaskTif/    # Masked multiplex images (536 .tif files)
│   ├── LANTERN_Segmentation/  # Nuclei segmentation data (1072 .mat files)
│   ├── LANTERN_CellType/   # Cell type information (536 .mat files)
│   └── LANTERN_Clinical_Data.xlsx  # Clinical data for all samples
├── docs/                   # Documentation and figures
│   ├── sample_fig.png
│   ├── INSTALLATION.md
│   └── CONTRIBUTING.md
├── REPRODUCIBILITY.md     # Guide for reproducing Nature paper visualizations
└── README.md
```

### Analysis Components

1. **Cell Segmentation** (`cell_segmentation/`): Nuclei segmentation from imaging mass cytometry data using MaskRCNN and MATLAB-based processing.

2. **Cell Phenotyping** (`cell_phenotyping/`): Cell type assignment based on marker expression patterns using rule-based classification in MATLAB.

3. **Micro Environment Prediction** (`micro_environment_prediction/`): Machine learning models for predicting patient progression using spatial features. **This module replicates the machine learning accuracy results from the Nature paper** (Extended Data Fig. 10). The notebooks compute prediction accuracy scores but do not generate the same visualizations as Figures 1-3 in the Nature paper, which require additional analysis of cell type distributions and neighborhood patterns.

## Getting Started

### Prerequisites

- Python 3.9 or 3.11 (Python 3.13 has compatibility issues with TensorFlow)
- Jupyter Notebook
- Required Python packages (see installation below)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/rohantennety/LANTERN.git
   cd LANTERN
   ```

2. **Install dependencies:**
   ```bash
   pip install tensorflow torch torchvision numpy pandas scipy scikit-learn imbalanced-learn matplotlib seaborn plotly Pillow opencv-python umap-learn tqdm jupyter ipywidgets keract torchinfo openpyxl xlrd
   ```

   **Note for Windows users:** TensorFlow requires Windows Long Path support. See `docs/INSTALLATION.md` for details.

3. **Set up data:**
   - See detailed instructions in the [Data Setup](#data-setup) section below
   - Data must be downloaded from Google Drive: [Download here](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)
   - Requires ~10GB of disk space

### Running the Analysis

1. **Start Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

2. **Run the analysis pipeline:**

   **For Micro Environment Prediction (replicates Nature paper results):**
   - Navigate to `micro_environment_prediction/`
   - Open and run notebooks in order:
     - `prediction_416.ipynb` - Main prediction analysis for all 416 samples (replicates main Nature paper results)
     - `prediction_416_freq.ipynb` - Frequency-based analysis
     - `prediction_stage1.ipynb` - Stage 1 specific analysis
     - `prediction_stage1_freq.ipynb` - Stage 1 frequency analysis
     - `resnet_architecture.ipynb` - ResNet deep learning architecture

   **For Cell Segmentation:**
   - See `cell_segmentation/README.md` for MATLAB-based segmentation pipeline
   - Requires MATLAB with Computer Vision and Image Processing Toolboxes
   - Requires Python 3.7.9+ for MaskRCNN components

   **For Cell Phenotyping:**
   - See `cell_phenotyping/README.md` for MATLAB-based phenotyping pipeline
   - Requires MATLAB with Computer Vision and Image Processing Toolboxes
   - Requires output from cell segmentation module

## Data

### Data Structure

The data should be organized in the `data/` directory:

- `data/LANTERN_MaskTif/`: Masked multiplex images (536 .tif files)
- `data/LANTERN_Segmentation/`: Nuclei segmentation data (1072 .mat files)
- `data/LANTERN_CellType/`: Cell type information (536 .mat files)
- `data/LANTERN_Clinical_Data.xlsx`: Clinical data for all samples
- `data/processed/`: Processed data files (generated automatically during analysis - see below)

### Data Setup

**Important:** The data files are large (~10GB total) and are not included in this repository. You must download them separately from Google Drive.

#### Download Data

**Download the data files here:** [Google Drive](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)

#### Step 1: Access Google Drive

1. Click the link above to access the Google Drive folder
2. You will see the following folders and files available for download

#### Step 2: Download Required Files

Download the following files/folders from Google Drive:

1. **LANTERN_MaskTif/** (folder)
   - Contains 536 `.tif` files (masked multiplex images)
   - File size: ~3-4 GB

2. **LANTERN_Segmentation/** (folder)
   - Contains 1072 `.mat` files (nuclei segmentation data)
   - File size: ~2-3 GB

3. **LANTERN_CellType/** (folder)
   - Contains 536 `.mat` files (cell type annotations)
   - File size: ~1-2 GB

4. **LUAD Clinical Data.xlsx** (single file) → **Rename to:** `LANTERN_Clinical_Data.xlsx`
   - Clinical data for all 416 samples
   - File size: <1 MB
   - **Note:** In Google Drive, this file is named "LUAD Clinical Data.xlsx". You must rename it to "LANTERN_Clinical_Data.xlsx" after downloading.

#### Step 3: Organize Data in Project Directory

After downloading, organize the files as follows:

```
LANTERN/
└── data/
    ├── LANTERN_MaskTif/          # Extract downloaded folder here
    ├── LANTERN_Segmentation/     # Extract downloaded folder here
    ├── LANTERN_CellType/         # Extract downloaded folder here
    ├── LANTERN_Clinical_Data.xlsx # Place the Excel file here
    └── processed/                 # Will be created automatically during analysis
```

**Instructions:**
- If you downloaded ZIP files, extract them to the `data/` directory
- Ensure folder names match exactly: `LANTERN_MaskTif`, `LANTERN_Segmentation`, `LANTERN_CellType`
- **Important:** The Excel file in Google Drive is named "LUAD Clinical Data.xlsx". After downloading, rename it to `LANTERN_Clinical_Data.xlsx` and place it directly in the `data/` folder (not in a subfolder)

#### Step 4: Verify Data Structure

After organizing, verify your data structure:

```bash
# Check that all directories exist and contain files
ls data/LANTERN_MaskTif/          # Should show 536 .tif files
ls data/LANTERN_Segmentation/     # Should show 1072 .mat files
ls data/LANTERN_CellType/         # Should show 536 .mat files
ls data/LANTERN_Clinical_Data.xlsx # Should exist
```

**Expected file counts:**
- `LANTERN_MaskTif/`: 536 files
- `LANTERN_Segmentation/`: 1072 files
- `LANTERN_CellType/`: 536 files

#### About the Processed Data Folder

The `data/processed/` folder contains pre-processed data files that are **automatically generated** when you run the analysis notebooks. 

**Important:** The processed data file (`allResponsesOriented_orig.pickle`) is **not** included in the Google Drive download. It will be created automatically during the first notebook run.

**What happens:**
1. When you first run `prediction_416.ipynb` or `prediction_stage1.ipynb`, the notebook will:
   - Load the raw data from `LANTERN_MaskTif/`, `LANTERN_Segmentation/`, and `LANTERN_CellType/`
   - Process and combine the cell data into a unified format
   - Generate `allResponsesOriented_orig.pickle` in `data/processed/`
   - Save it for future use (subsequent runs will load it directly)

2. **First run:** May take 10-30 minutes to generate the processed file (depending on your hardware)

3. **Subsequent runs:** Will load the existing pickle file quickly (seconds)

**Note:** If you delete the `data/processed/` folder or the pickle file, it will be regenerated on the next notebook run. The processed file is created from the raw segmentation and cell type data, so as long as you have those folders, the processed data can always be regenerated.

#### Troubleshooting Data Setup

- **Missing files:** Re-download from Google Drive and verify the download completed successfully
- **Wrong folder names:** Ensure exact capitalization matches (case-sensitive)
- **File count mismatch:** Some files may be in subdirectories; check nested folders
- **Permission errors:** Ensure you have read/write permissions in the `data/` directory

For more detailed information, see `data/README.md`.

## Analysis Workflow

The complete analysis pipeline consists of three sequential steps:

1. **Cell Segmentation** (`cell_segmentation/`): Segment nuclei from IMC images using MaskRCNN and MATLAB-based processing
2. **Cell Phenotyping** (`cell_phenotyping/`): Assign cell types to segmented nuclei based on marker expression patterns
3. **Micro Environment Prediction** (`micro_environment_prediction/`): 
   - Load processed cell data and clinical information
   - Extract spatial features from cell neighborhoods
   - Train machine learning models (SVM, Gaussian Process Classifier) for progression prediction
   - Generate UMAP visualizations and performance metrics
   - Optional: ResNet-based deep learning analysis on raw images

**Note:** To replicate the Nature paper results, you can start directly with the `micro_environment_prediction/` module using the data from Google Drive. The notebooks will automatically generate the processed data file (`allResponsesOriented_orig.pickle`) on the first run. The segmentation and phenotyping steps are only needed if you want to process new IMC images.

## Citation

If you use this code or data, please cite:

```
LANTERN: Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network
Author: Rohan Tennety
Repository: https://github.com/rohantennety/LANTERN
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

**Rohan Tennety**

- GitHub: [@rohantennety](https://github.com/rohantennety)
- Repository: https://github.com/rohantennety/LANTERN

## Related Publication

This repository contains code to replicate the analysis from:

**Sorin, M., Rezanejad, M., Karimi, E. et al.** Single-cell spatial landscapes of the lung tumour immune microenvironment. *Nature* **614**, 548–554 (2023). (coming soon)

The `micro_environment_prediction/` module specifically replicates the main results and figures from this Nature paper, including:
- Progression prediction using spatial features from 416 lung adenocarcinoma samples
- UMAP visualizations of the tumor-immune microenvironment
- Deep learning models for predicting patient outcomes

## Acknowledgments

This work is based on the original IMC-Lung project by walsh-quail-labs. Data is available through [Google Drive](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing).

