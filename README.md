# Multiple Myeloma Segmentation using SegPC 2021

## Overview

This repository implements a deep learning approach for segmenting cell nuclei in multiple myeloma using techniques adapted from the **SegPC 2021 challenge**. The project uses U-Net architecture for instance segmentation of pathological cells in medical imaging data.

## Dataset

### SegPC 2021 Dataset Citation

This project utilizes methodologies from the **SegPC 2021 (Segmentation of Nuclei in Papanicolaou stained Cytology images)** challenge.

**Citation:**
```bibtex
@article{SegPC2021,
  title={Segmentation of Nuclei in Pap Stained Cytology Images: The SegPC-2021 Grand Challenge},
  year={2021},
  url={https://segpc-2021.grand-challenge.org/}
}
```
## Dataset Features

The SegPC 2021 dataset provides high-quality cytology images specifically curated for nuclei segmentation tasks. Key features include:

- **High-resolution Papanicolaou-stained cytology images**
- **Expert-annotated nuclei masks** providing precise pixel-level ground truth
- **Instance segmentation task** focusing on overlapping and clustered nuclei
- **Benchmark suitability** for evaluating nuclear segmentation algorithms and deep learning models

## Model Architecture

### U-Net: Encoder–Decoder Network

The segmentation model is based on **U-Net**, a convolutional neural network with **skip connections** specifically designed for biomedical image segmentation.

### Architecture Overview

```
Input Image (512x512x3)
        ↓
    ENCODER
        ↓
  Conv Block 1 → MaxPool → (256x256)
        ↓
  Conv Block 2 → MaxPool → (128x128)
        ↓
  Conv Block 3 → MaxPool → (64x64)
        ↓
  Conv Block 4 → MaxPool → (32x32)
        ↓
  Bottleneck (32x32)
        ↓
    DECODER
        ↓
  UpSample + Skip Connection → (64x64)
        ↓
  UpSample + Skip Connection → (128x128)
        ↓
  UpSample + Skip Connection → (256x256)
        ↓
  UpSample + Skip Connection → (512x512)
        ↓
  Output Segmentation Mask (512x512x1)
```

### Key Components

- **Encoder** — Extracts features through convolutional blocks and downsampling
- **Bottleneck** — Captures semantic information at lowest resolution
- **Decoder** — Reconstructs spatial information through upsampling
- **Skip Connections** — Preserve fine-grained details from encoder to decoder
- **Loss Function** — Dice Loss + Cross-Entropy for balanced segmentation

### Model Specifications

| Parameter | Value |
|-----------|-------|
| Parameters | ~30M |
| Input Size | 512×512 pixels |
| Output | Binary segmentation mask |
| Architecture | FCN with 4 encoding blocks |

---

## Requirements

```
Python 3.7+
torch>=1.9.0
torchvision>=0.10.0
opencv-python>=4.5.0
numpy>=1.19.0
pandas>=1.1.0
matplotlib>=3.3.0
scikit-learn>=0.24.0
jupyter>=1.0.0
```

---

## Installation

```bash
# Clone repository
git clone https://github.com/anjishnusaw91/Multiple-Myeloma-Segmentation.git
cd Multiple-Myeloma-Segmentation

# Create virtual environment
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

> **Note:** Download the SegPC 2021 dataset from [https://segpc-2021.grand-challenge.org/](https://segpc-2021.grand-challenge.org/)

---

## Directory Structure

```
Multiple-Myeloma-Segmentation/
├── README.md
├── Segmentation Notebook SegPC2021.ipynb
├── requirements.txt
└── data/
    ├── train/
    │   ├── images/
    │   └── masks/
    ├── val/
    │   ├── images/
    │   └── masks/
    └── test/
        └── images/
```

---

## Usage

```bash
# Start Jupyter
jupyter notebook

# Open and run: Segmentation Notebook SegPC2021.ipynb
```

### Notebook Sections

1. Data Loading and Exploration
2. Data Preprocessing and Augmentation
3. U-Net Model Definition
4. Model Training
5. Evaluation and Metrics
6. Inference and Visualization

---

## Evaluation Metrics

| Metric | Formula |
|--------|---------|
| Dice Coefficient | `2 * \|X ∩ Y\| / (\|X\| + \|Y\|)` |
| Intersection over Union (IoU) | `\|X ∩ Y\| / \|X ∪ Y\|` |
| Pixel-wise Accuracy | Overall classification accuracy |
| Hausdorff Distance | Boundary distance metric |

---

## Results

Expected performance on SegPC 2021 dataset:

| Metric | Score |
|--------|-------|
| Dice Coefficient | 0.88 – 0.92 |
| IoU | 0.80 – 0.85 |
| Accuracy | 0.95+ |

---

## References

1. **U-Net: Convolutional Networks for Biomedical Image Segmentation**
   Ronneberger, O., Fischer, P., & Brox, T. (2015)
   [https://arxiv.org/abs/1505.04597](https://arxiv.org/abs/1505.04597)

2. **SegPC 2021 Challenge**
   [https://segpc-2021.grand-challenge.org/](https://segpc-2021.grand-challenge.org/)

3. **Generalised Dice Overlap as a Deep Learning Loss Function**
   Sudre, C. H., et al. (2017)
   [https://arxiv.org/abs/1707.00478](https://arxiv.org/abs/1707.00478)

---

## Author

**Anjishnusaw91**
GitHub: [@anjishnusaw91](https://github.com/anjishnusaw91)

---

## Acknowledgments

- SegPC 2021 Challenge Organizers
- IEEE ISBI for the challenge framework
- PyTorch, OpenCV, and open-source community

---

*Last Updated: March 8, 2026 | Status: Active*
