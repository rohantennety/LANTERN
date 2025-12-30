# Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network (LANTERN)

<img src='docs/sample_fig.png' width=100%>

**LANTERN** (Lung Adenocarcinoma Neighborhood Tumor-immune Environment Recurrence Network) - This repository includes codes and data used for spatial analysis of lung adenocarcinoma tumor-immune microenvironments.

## Summary

Single-cell technologies have revealed the complexity of the tumour immune microenvironment with unparalleled resolution. Most clinical strategies rely on histopathological stratification of tumour subtypes, yet the spatial context of single-cell phenotypes within these stratified subgroups is poorly understood. This project applies imaging mass cytometry to characterize the tumour and immunological landscape of 416 lung adenocarcinoma patient tumours across five histological patterns. We resolve >1.6 million cells, enabling spatial analysis of immune lineages and activation states with distinct clinical correlates, including survival. Using deep learning, we can predict with high accuracy which patients will progress after surgery using a single 1 mm² tumour core, which could be informative for clinical management following surgical resection.

This dataset represents a valuable resource for the NSCLC research community and exemplifies the utility of spatial resolution within single-cell analyses. This study also highlights how artificial intelligence can improve our understanding of microenvironmental features that underlie cancer progression and may influence future clinical practice.

## Repository Structure

```
LANTERN/
├── notebooks/              # Jupyter notebooks for analysis
│   ├── prediction_416.ipynb
│   ├── prediction_416_freq.ipynb
│   ├── prediction_stage1.ipynb
│   ├── prediction_stage1_freq.ipynb
│   └── resnet_architecture.ipynb
├── data/                   # Data directory (see Data Setup)
│   ├── LANTERN_MaskTif/
│   ├── LANTERN_Segmentation/
│   ├── LANTERN_CellType/
│   └── LANTERN_Clinical_Data.xlsx
├── docs/                   # Documentation and figures
│   └── sample_fig.png
└── README.md
```

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
   - Download data from Zenodo (DOI: [10.5281/zenodo.7760826](https://doi.org/10.5281/zenodo.7760826))
   - Organize data in the `data/` directory as described in the Data Structure section

### Running the Analysis

1. **Start Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

2. **Open and run notebooks in order:**
   - `notebooks/prediction_416.ipynb` - Main prediction analysis for all 416 samples
   - `notebooks/prediction_416_freq.ipynb` - Frequency-based analysis
   - `notebooks/prediction_stage1.ipynb` - Stage 1 specific analysis
   - `notebooks/prediction_stage1_freq.ipynb` - Stage 1 frequency analysis
   - `notebooks/resnet_architecture.ipynb` - ResNet deep learning architecture

## Data

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7760826.svg)](https://doi.org/10.5281/zenodo.7760826)

### Data Structure

The data should be organized in the `data/` directory:

- `data/LANTERN_MaskTif/`: Masked multiplex images (536 .tif files)
- `data/LANTERN_Segmentation/`: Nuclei segmentation data (1072 .mat files)
- `data/LANTERN_CellType/`: Cell type information (536 .mat files)
- `data/LANTERN_Clinical_Data.xlsx`: Clinical data for all samples
- `data/processed/`: Processed data files (generated during analysis)

### Downloading Data

The data is available on Zenodo and should be downloaded and placed in the `data/` directory:

1. **LANTERN_MaskTif**: Contains masked multiplex images of the IMC cores
2. **LANTERN_Segmentation**: Contains the nuclei segmentation information
3. **LANTERN_CellType**: Contains the cell type information for each of the IMC cores
4. **LANTERN_Clinical_Data.xlsx**: Contains clinical data with regard to the images listed above

## Analysis Workflow

1. **Data Preprocessing**: Load and prepare clinical and imaging data
2. **Feature Extraction**: Extract features from processed cell data
3. **Model Training**: Train machine learning models for progression prediction
4. **Visualization**: Generate UMAP plots and performance metrics
5. **Deep Learning**: Optional ResNet-based analysis on raw images

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

## Acknowledgments

This work is based on the original IMC-Lung project. Data is available through Zenodo (DOI: 10.5281/zenodo.7760826).

