# Installation Guide

## System Requirements

- **Operating System**: Windows, macOS, or Linux
- **Python**: 3.9 or 3.11 (recommended). Python 3.13 has compatibility issues with TensorFlow.
- **RAM**: Minimum 8GB, recommended 16GB+
- **Storage**: ~10GB for data files

## Step-by-Step Installation

### 1. Clone the Repository

```bash
git clone https://github.com/rohantennety/LANTERN.git
cd LANTERN
```

### 2. Create a Virtual Environment (Recommended)

```bash
# Using venv
python -m venv lantern_env

# Activate on Windows
lantern_env\Scripts\activate

# Activate on macOS/Linux
source lantern_env/bin/activate
```

### 3. Install Python Dependencies

```bash
pip install tensorflow torch torchvision numpy pandas scipy scikit-learn imbalanced-learn matplotlib seaborn plotly Pillow opencv-python umap-learn tqdm jupyter ipywidgets keract torchinfo openpyxl xlrd
```

### 4. Windows Long Path Support (Required for TensorFlow)

TensorFlow installation on Windows requires Long Path support to be enabled:

1. **Open PowerShell as Administrator** (Right-click → Run as Administrator)
2. **Run this command:**
   ```powershell
   New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
   ```
3. **Restart your computer**
4. **After restart, install TensorFlow:**
   ```bash
   pip install tensorflow
   ```

### 5. Verify Installation

```python
import tensorflow as tf
import torch
import numpy as np
import pandas as pd
import sklearn
print("All packages installed successfully!")
print(f"TensorFlow: {tf.__version__}")
print(f"PyTorch: {torch.__version__}")
```

### 6. Download Data

1. Visit the [Google Drive folder](https://drive.google.com/drive/folders/1gOgEWZ1isWgRr35SQGPovYfI5aBsdLfa?usp=sharing)
2. Open the "LungData" folder inside
3. Download the following folders/files:
   - `LANTERN_MaskTif/` → Place in `data/LANTERN_MaskTif/`
   - `LANTERN_Segmentation/` → Place in `data/LANTERN_Segmentation/`
   - `LANTERN_CellType/` → Place in `data/LANTERN_CellType/`
   - `LUAD Clinical Data.xlsx` → **Rename to** `LANTERN_Clinical_Data.xlsx` → Place in `data/`

### 7. Start Jupyter Notebook

```bash
jupyter notebook
```

Navigate to the `notebooks/` directory and open `prediction_416.ipynb` to begin.

## Troubleshooting

### TensorFlow Installation Issues

**Problem**: `OSError: [Errno 2] No such file or directory` during TensorFlow installation on Windows.

**Solution**: Enable Windows Long Path support (see step 4 above).

### Python Version Issues

**Problem**: `ERROR: Package 'tensorflow' requires a different Python`

**Solution**: Use Python 3.9 or 3.11. Create a new virtual environment with the correct Python version:
```bash
conda create -n lantern python=3.11
conda activate lantern
```

### Missing Data Files

**Problem**: `FileNotFoundError` when running notebooks.

**Solution**: Ensure all data files are downloaded from Google Drive and placed in the correct `data/` subdirectories. See the main README.md for detailed download instructions.

## Alternative Installation Methods

### Using Conda

```bash
conda create -n lantern python=3.11
conda activate lantern
conda install numpy pandas scipy scikit-learn matplotlib seaborn jupyter
pip install tensorflow torch torchvision
```

### Using Docker

A Docker image can be created for consistent environments across systems. (Dockerfile not included in this repository.)

