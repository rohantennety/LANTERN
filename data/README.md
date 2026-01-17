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

**Download the data files here:** [Google Drive](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)

### Step-by-Step Download Instructions

#### Step 1: Access Google Drive

1. Click the link above to access the Google Drive folder
2. You will see the following folders and files available for download

#### Step 2: Download Required Files

From the Google Drive folder, locate and download:

1. **LANTERN_MaskTif/** 
   - Look for a folder or ZIP file named `LANTERN_MaskTif`
   - Contains: 536 `.tif` files (~3-4 GB)
   - Download method: Click download button or use "Download all" option

2. **LANTERN_Segmentation/**
   - Look for a folder or ZIP file named `LANTERN_Segmentation`
   - Contains: 1072 `.mat` files (~2-3 GB)
   - Download method: Click download button or use "Download all" option

3. **LANTERN_CellType/**
   - Look for a folder or ZIP file named `LANTERN_CellType`
   - Contains: 536 `.mat` files (~1-2 GB)
   - Download method: Click download button or use "Download all" option

4. **LUAD Clinical Data.xlsx** → **Rename to:** `LANTERN_Clinical_Data.xlsx`
   - Single Excel file (<1 MB)
   - Download method: Right-click and select "Download"
   - **Important:** After downloading, rename this file from "LUAD Clinical Data.xlsx" to "LANTERN_Clinical_Data.xlsx"

**Alternative:** If available, use the "Download all" option to get everything at once (may be faster but requires more disk space).

#### Step 3: Extract and Organize

After downloading:

1. **If you downloaded ZIP files:**
   - Extract each ZIP to a temporary location first
   - Then copy the extracted folders to `data/` directory
   - Ensure folder names are exactly: `LANTERN_MaskTif`, `LANTERN_Segmentation`, `LANTERN_CellType`

2. **If you downloaded folders directly:**
   - Copy each folder into the `data/` directory
   - Maintain exact folder names (case-sensitive)

3. **For the Excel file:**
   - The downloaded file is named `LUAD Clinical Data.xlsx`
   - **Rename it to:** `LANTERN_Clinical_Data.xlsx`
   - Place the renamed file directly in the `data/` folder (not in a subfolder)

#### Step 4: Verify Download

Check that you have:
- ✅ `data/LANTERN_MaskTif/` with 536 `.tif` files
- ✅ `data/LANTERN_Segmentation/` with 1072 `.mat` files  
- ✅ `data/LANTERN_CellType/` with 536 `.mat` files
- ✅ `data/LANTERN_Clinical_Data.xlsx` file exists

### File Descriptions

- **LANTERN_MaskTif/**: Contains masked multiplex images of the IMC cores (536 .tif files)
- **LANTERN_Segmentation/**: Contains nuclei segmentation information (1072 .mat files)
- **LANTERN_CellType/**: Contains cell type information for each IMC core (536 .mat files)
- **LANTERN_Clinical_Data.xlsx**: Contains clinical data corresponding to the images

## Note

**Why are the data folders empty?**

The data folders (`LANTERN_MaskTif/`, `LANTERN_Segmentation/`, `LANTERN_CellType/`) are intentionally empty in this repository because:

1. **File size**: The data files are very large (~10GB total)
2. **Git limitations**: Large files are not suitable for Git repositories
3. **Download required**: Users must download the data separately from Google Drive

The folders are included in the repository structure (with `.gitkeep` files) so you know where to place the downloaded data. Once you download the data from Google Drive and place the files in these folders, they will contain:
- `LANTERN_MaskTif/`: 536 `.tif` files
- `LANTERN_Segmentation/`: 1072 `.mat` files
- `LANTERN_CellType/`: 536 `.mat` files
- `LANTERN_Clinical_Data.xlsx`: Clinical data file

**To get started:** Follow the download instructions above to populate these folders with the actual data files.

