# Reproducing Nature Paper Visualizations: LANTERN Setup Guide

This guide will walk you through setting up LANTERN and reproducing the key visualizations from the Nature paper: **"Single-cell spatial landscapes of the lung tumour immune microenvironment"** ([Nature 614, 548–554, 2023](https://www.nature.com/articles/s41586-022-05672-3)).

## Overview

This repository contains code to replicate the analysis from the Nature paper, which analyzed **416 lung adenocarcinoma patients** using imaging mass cytometry (IMC) to resolve **>1.6 million cells** and predict disease progression using deep learning.

## Quick Start

### 1. Prerequisites

- **Python 3.9 or 3.11** (Python 3.13 has compatibility issues with TensorFlow)
- **Jupyter Notebook**
- **8GB+ RAM** recommended
- **Windows users**: Enable Long Path support (see Installation section)

### 2. Installation

#### Clone the Repository
```bash
git clone https://github.com/rohantennety/LANTERN.git
cd LANTERN
```

#### Install Python Dependencies
```bash
pip install tensorflow torch torchvision numpy pandas scipy scikit-learn imbalanced-learn matplotlib seaborn plotly Pillow opencv-python umap-learn tqdm jupyter ipywidgets keract torchinfo openpyxl xlrd
```

**Windows Users - Important:** TensorFlow requires Windows Long Path support. See `docs/INSTALLATION.md` for detailed instructions. You'll need administrator privileges to enable this.

#### Verify Installation
```bash
python -c "import tensorflow as tf; print('TensorFlow version:', tf.__version__)"
python -c "import torch; print('PyTorch version:', torch.__version__)"
```

### 3. Data Setup

**Critical:** The data files are **NOT** included in this repository. You must download them separately from Google Drive (~10GB total).

#### Download Data

**Download the data files here:** [Google Drive](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)

#### Step 1: Access Google Drive

1. Click the link above or copy this URL into your browser: `https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing`
2. You will see a folder named "LungData" containing the following folders and files:
   - `LANTERN_MaskTif/` (folder)
   - `LANTERN_Segmentation/` (folder)
   - `LANTERN_CellType/` (folder)
   - `LUAD Clinical Data.xlsx` (file - note the name)

#### Step 2: Download Required Data Files

From the Google Drive folder, download the following:

1. **LANTERN_MaskTif/** (folder or ZIP)
   - **What it contains:** 536 `.tif` files (masked multiplex images)
   - **Size:** ~3-4 GB
   - **Required for:** All analysis notebooks

2. **LANTERN_Segmentation/** (folder or ZIP)
   - **What it contains:** 1072 `.mat` files (nuclei segmentation data)
   - **Size:** ~2-3 GB
   - **Required for:** All analysis notebooks

3. **LANTERN_CellType/** (folder or ZIP)
   - **What it contains:** 536 `.mat` files (cell type annotations)
   - **Size:** ~1-2 GB
   - **Required for:** All analysis notebooks

4. **LUAD Clinical Data.xlsx** (single file) → **Rename to:** `LANTERN_Clinical_Data.xlsx`
   - **What it contains:** Clinical data for all 416 samples
   - **Size:** <1 MB
   - **Required for:** All analysis notebooks
   - **Important:** In Google Drive, this file is named "LUAD Clinical Data.xlsx". You must rename it to "LANTERN_Clinical_Data.xlsx" after downloading.

**Step-by-Step Download Instructions:**

1. **Open the Google Drive folder** using the link above
2. **You will see a "LungData" folder** - click on it to open
3. **Inside LungData, you will see:**
   - Three folders: `LANTERN_MaskTif`, `LANTERN_Segmentation`, `LANTERN_CellType`
   - One Excel file: `LUAD Clinical Data.xlsx`

4. **To download individual folders:**
   - Right-click on each folder (`LANTERN_MaskTif`, `LANTERN_Segmentation`, `LANTERN_CellType`)
   - Select "Download" from the context menu
   - Google Drive will create a ZIP file for each folder
   - Wait for each download to complete before starting the next one

5. **To download the Excel file:**
   - Right-click on `LUAD Clinical Data.xlsx`
   - Select "Download"
   - The file will download directly (no ZIP)

6. **Alternative - Download all at once:**
   - Select all items in the folder (Ctrl+A or Cmd+A)
   - Right-click and select "Download"
   - Google Drive will create ZIP files for folders and download the Excel file separately
   - **Note:** This may take longer and requires more disk space

**Download Tips:**
- Use a stable internet connection (downloads may take 30-60 minutes for all files)
- Ensure you have at least 15GB free disk space
- If downloads fail, try downloading individual files instead of bulk download
- Large folders may take 10-20 minutes each to download

#### Step 3: Extract and Organize Data

After downloading, organize files in your project directory:

```
LANTERN/
└── data/
    ├── LANTERN_MaskTif/          # Extract/unzip here
    │   ├── file1.tif
    │   ├── file2.tif
    │   └── ... (536 total .tif files)
    ├── LANTERN_Segmentation/     # Extract/unzip here
    │   ├── file1.mat
    │   ├── file2.mat
    │   └── ... (1072 total .mat files)
    ├── LANTERN_CellType/         # Extract/unzip here
    │   ├── file1.mat
    │   ├── file2.mat
    │   └── ... (536 total .mat files)
    ├── LANTERN_Clinical_Data.xlsx # Place directly here
    └── processed/                 # Created automatically (don't create manually)
```

**Detailed Instructions:**

1. **If you downloaded ZIP files:**
   ```bash
   # Extract each ZIP file to the data/ directory
   # Make sure the extracted folder names match exactly:
   # - LANTERN_MaskTif (not "LANTERN_MaskTif-main" or similar)
   # - LANTERN_Segmentation
   # - LANTERN_CellType
   ```

2. **If you downloaded individual folders:**
   - Copy/move each folder into the `data/` directory
   - Ensure folder names match exactly (case-sensitive)

3. **For the Excel file:**
   - The downloaded file is named `LUAD Clinical Data.xlsx`
   - **Rename it to:** `LANTERN_Clinical_Data.xlsx`
   - Place the renamed file directly in `data/` (not in a subfolder)

#### Step 4: Verify Data Structure

After organizing, verify everything is in place:

**On Windows (PowerShell):**
```powershell
# Check file counts
(Get-ChildItem data\LANTERN_MaskTif\*.tif).Count      # Should be 536
(Get-ChildItem data\LANTERN_Segmentation\*.mat).Count # Should be 1072
(Get-ChildItem data\LANTERN_CellType\*.mat).Count     # Should be 536
Test-Path data\LANTERN_Clinical_Data.xlsx              # Should be True
```

**On macOS/Linux:**
```bash
# Check file counts
ls data/LANTERN_MaskTif/*.tif | wc -l      # Should be 536
ls data/LANTERN_Segmentation/*.mat | wc -l # Should be 1072
ls data/LANTERN_CellType/*.mat | wc -l     # Should be 536
ls data/LANTERN_Clinical_Data.xlsx          # Should exist
```

**Expected Results:**
- ✅ `LANTERN_MaskTif/`: 536 `.tif` files
- ✅ `LANTERN_Segmentation/`: 1072 `.mat` files
- ✅ `LANTERN_CellType/`: 536 `.mat` files
- ✅ `LANTERN_Clinical_Data.xlsx`: File exists

#### Step 5: About the Processed Data File

**Important:** The processed data file is **NOT** included in the Google Drive download. It will be **automatically generated** when you run the analysis notebooks for the first time.

**What is the processed file?**
- `data/processed/allResponsesOriented_orig.pickle` - A pre-processed data file containing combined cell responses from all samples
- This file combines data from `LANTERN_MaskTif/`, `LANTERN_Segmentation/`, and `LANTERN_CellType/` into a unified format
- It's used by all prediction notebooks for faster data loading

**How is it generated?**
1. **First notebook run:** When you first run `prediction_416.ipynb` or `prediction_stage1.ipynb`:
   - The notebook detects that `allResponsesOriented_orig.pickle` doesn't exist
   - It automatically processes the raw data from the three data folders
   - Combines cell segmentation, cell type, and marker expression data
   - Generates and saves the pickle file in `data/processed/`
   - **This may take 10-30 minutes** depending on your hardware

2. **Subsequent runs:** 
   - The notebook will detect the existing pickle file
   - Load it directly (takes only seconds)
   - Skip the processing step

**What you need:**
- The raw data folders (`LANTERN_MaskTif/`, `LANTERN_Segmentation/`, `LANTERN_CellType/`)
- The notebooks will handle the rest automatically

**Note:** 
- The `data/processed/` folder will be created automatically when needed
- If you delete the pickle file, it will be regenerated on the next run
- The processed file is derived from the raw data, so it can always be recreated as long as you have the source data folders

#### Troubleshooting Data Setup

**Problem: File count doesn't match**
- **Solution:** Some files may be in nested subdirectories. Check if Google Drive organized files in subfolders and move them to the correct location.

**Problem: "FileNotFoundError" when running notebooks**
- **Solution:** 
  1. Verify file paths match exactly (case-sensitive on Linux/Mac)
  2. Ensure you're running notebooks from the project root directory
  3. Check that `LANTERN_Clinical_Data.xlsx` is in `data/` (not `data/LANTERN_Clinical_Data/`)

**Problem: Download failed or incomplete**
- **Solution:** 
  1. Re-download from Google Drive
  2. Try downloading individual files instead of bulk download
  3. Check your internet connection and disk space

**Problem: ZIP file won't extract**
- **Solution:** 
  1. Try a different extraction tool (7-Zip, WinRAR, built-in extractor)
  2. Verify the ZIP file downloaded completely (check file size)
  3. Re-download if the ZIP appears corrupted

For additional help, see `data/README.md` or the main `README.md`.

## Reproducing Nature Paper Visualizations

### Notebook Execution Order

To reproduce the Nature paper's results and visualizations, run the notebooks in `micro_environment_prediction/` in the following order:

#### Step 1: Main Analysis (All 416 Samples)
**Notebook:** `prediction_416.ipynb`

**What it does:**
- Loads clinical data and processed cell responses for all 416 patients
- Extracts spatial features from cell neighborhoods
- Trains machine learning models (SVM, Gaussian Process Classifier) to predict progression
- Generates UMAP visualizations showing sample clustering
- Produces cross-validation accuracy scores

**Key Visualizations Produced:**
- **UMAP plots** showing how samples cluster based on spatial features (similar to Extended Data Fig. 8-9 in Nature paper)
- **Model performance metrics** comparing different feature sets (similar to Extended Data Fig. 10)
- **Feature importance analysis** identifying key spatial patterns

**Expected Runtime:** 30-60 minutes (depending on hardware)

**To run:**
```bash
cd micro_environment_prediction
jupyter notebook prediction_416.ipynb
```

#### Step 2: Frequency-Based Analysis
**Notebook:** `prediction_416_freq.ipynb`

**What it does:**
- Analyzes cell type frequencies across samples
- Compares frequency-based features to spatial features
- Generates visualizations of cell type distributions

**Key Visualizations Produced:**
- **Cell type frequency distributions** across histological subtypes (similar to Fig. 1e-f in Nature paper)
- **Comparison plots** showing frequency vs. spatial features

**Expected Runtime:** 15-30 minutes

#### Step 3: Stage 1 Specific Analysis
**Notebook:** `prediction_stage1.ipynb`

**What it does:**
- Focuses on Stage I patients (n=286) for progression prediction
- Replicates the main machine learning results from the Nature paper
- Generates stage-specific UMAP visualizations

**Key Visualizations Produced:**
- **Stage I progression prediction results** (main result from Nature paper Fig. 3)
- **UMAP plots** for Stage I patients only
- **Model accuracy comparisons** (baseline vs. clinical variables vs. spatial features)

**Expected Runtime:** 20-40 minutes

#### Step 4: Stage 1 Frequency Analysis
**Notebook:** `prediction_stage1_freq.ipynb`

**What it does:**
- Frequency-based analysis for Stage I patients
- Compares different feature extraction methods

**Expected Runtime:** 10-20 minutes

#### Step 5: Deep Learning Architecture
**Notebook:** `resnet_architecture.ipynb`

**What it does:**
- Implements ResNet-based deep learning model for multi-channel IMC images
- Trains model to predict progression directly from raw imaging data
- Demonstrates how AI can extract features from a single 1 mm² tumor core

**Key Visualizations Produced:**
- **ResNet architecture visualization**
- **Deep learning prediction results** (replicates Nature paper's claim about predicting from single 1 mm² core)

**Expected Runtime:** 1-3 hours (depending on GPU availability)

**Note:** This notebook requires significant computational resources. GPU recommended but not required.

## Understanding the Visualizations

### Figure 1 (Nature Paper): IMC Spatial Landscape

The Nature paper's Figure 1 shows:
- **1b**: Average expression of lineage markers across cell types
- **1c**: Waterfall plot of cell type distribution across histological subgroups
- **1d**: Representative images of antibody staining and segmented cells
- **1e-f**: Prevalence of 17 cell types across 416 patients
- **1g-i**: Immune, myeloid, and lymphoid cell prevalence across 5 histological patterns

**To reproduce:** These visualizations require the full segmentation and phenotyping pipeline. The processed data in `data/processed/` contains the cell type information needed. You can create similar plots by analyzing the cell type data.

### Figure 2 (Nature Paper): Cellular Neighborhoods

Shows 30 distinct cellular neighborhoods and their association with survival and clinical variables.

**To reproduce:** The `prediction_416.ipynb` notebook extracts spatial neighborhood features. You can analyze these features to identify similar neighborhoods.

### Figure 3 (Nature Paper): Machine Learning Predictions

Shows progression prediction accuracy for Stage I patients using different feature sets.

**To reproduce:** Run `prediction_stage1.ipynb` - this directly replicates Figure 3 results.

### Extended Data Figures

- **Extended Data Fig. 8-9**: UMAP visualizations of samples colored by various clinical variables
- **Extended Data Fig. 10**: Machine learning accuracy comparisons

**To reproduce:** These are generated in `prediction_416.ipynb` and `prediction_stage1.ipynb`.

## Troubleshooting

### Common Issues

#### 1. "No module named tensorflow"
**Solution:** 
- Windows users: Enable Long Path support (see `docs/INSTALLATION.md`)
- Reinstall TensorFlow: `pip install --upgrade tensorflow`

#### 2. "FileNotFoundError" for data files
**Solution:** 
- Verify data is downloaded and placed in correct `data/` subdirectories
- Check file paths in notebooks match your data structure
- Ensure `LANTERN_Clinical_Data.xlsx` is in `data/` directory

#### 3. Memory errors during UMAP computation
**Solution:**
- Reduce `n_neighbors` parameter in UMAP
- Use `n_components=2` for 2D visualization
- Process data in batches

#### 4. Slow performance
**Solution:**
- Use GPU for TensorFlow operations (if available)
- Reduce number of samples for testing
- Close other applications to free up RAM

### Getting Help

If you encounter issues:
1. Check the `docs/INSTALLATION.md` for detailed setup instructions
2. Review the notebook error messages carefully
3. Ensure all dependencies are installed correctly
4. Verify data structure matches expected format

## Expected Results

After running all notebooks, you should have:

1. **UMAP visualizations** showing how samples cluster based on spatial features
2. **Model accuracy scores** demonstrating improved prediction using spatial features vs. clinical variables alone
3. **Feature importance analysis** identifying key spatial patterns associated with progression
4. **Deep learning results** showing prediction from raw images

The exact numbers may vary slightly due to random seeds, but the overall patterns and improvements should match the Nature paper.

## Citation

If you use this code or reproduce these results, please cite:

**Nature Paper:**
```
Sorin, M., Rezanejad, M., Karimi, E. et al. Single-cell spatial landscapes 
of the lung tumour immune microenvironment. Nature 614, 548–554 (2023). 
https://doi.org/10.1038/s41586-022-05672-3
```

**This Repository:**
```
LANTERN: Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network
Author: Rohan Tennety
Repository: https://github.com/rohantennety/LANTERN
```

## Additional Resources

- **Original IMC-Lung Repository:** [walsh-quail-labs/IMC-Lung](https://github.com/walsh-quail-labs/IMC-Lung)
- **Data Repository:** [Google Drive](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)
- **Nature Paper:** [https://www.nature.com/articles/s41586-022-05672-3](https://www.nature.com/articles/s41586-022-05672-3)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Author:** Rohan Tennety  
**GitHub:** [@rohantennety](https://github.com/rohantennety)  
**Repository:** https://github.com/rohantennety/LANTERN