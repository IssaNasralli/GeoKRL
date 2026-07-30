# GeoKRL: A Geospatial Knowledge Representation Learning Framework

GeoKRL is a self-supervised multimodal foundation learning framework for geospatial representation learning. It is designed to learn transferable latent representations from heterogeneous Earth observation data that can subsequently be adapted to multiple downstream geospatial prediction tasks.

This repository accompanies the paper:

> **GeoKRL: A Self-Supervised Multimodal Foundation Model for Geospatial Representation Learning**  
> *(Paper information will be updated after publication.)*

---

## Repository Structure

```
GeoKRL/
│
├── data_collection/
│   ├── Biomass.js
│   ├── Climate.js
│   ├── dem_slope.js
│   ├── LC.js
│   ├── NDVI.js
│   ├── NTL.js
│   ├── rgb.js
│   └── shape_file.js
│
├── data_preprocessing/
│   ├── compute_global_normalization_statistics.py
│   ├── extract_roi_from_worldpop_files.py
│   ├── extract_roi_from_wsf_tiles.py
│   └── ProjectRasterSnapRaster_same_as_rgb_files.py
│
├── model/
│   ├── GeoKRL.py
│   ├── train.py
│   ├── train_task.py
│   ├── config.py
│   ├── dataset_index.py
│   ├── raster_manager.py
│   ├── sample_generator.py
│   ├── sample_generator_task.py
│   ├── modality_sampler.py
│   ├── batch_generator.py
│   ├── batch_generator_task.py
│   ├── hyperparameters.py
│   ├── task_hyperparameters.py
│   ├── best_pretraining_config.py
│   ├── auto_train_models/
│   └── task_auto_train_models/
│
└── README.md
```

---

# Workflow

The complete GeoKRL pipeline consists of three sequential stages.

```
Google Earth Engine
        │
        ▼
Data Collection
(JavaScript)
        │
        ▼
GeoTIFF Layers
        │
        ▼
Data Preprocessing
(ArcPy)
        │
        ▼
GeoKG Dataset
        │
        ▼
GeoKRL Pretraining
(Self-supervised)
        │
        ▼
Pretrained Backbone
        │
        ▼
Downstream Prediction
```

---

# 1. Data Collection

The `data_collection` directory contains Google Earth Engine (GEE) JavaScript scripts used to download all datasets employed in GeoKRL.

Available scripts include:

| Script | Dataset |
|---------|----------|
| `rgb.js` | Sentinel-2 RGB imagery |
| `NDVI.js` | Normalized Difference Vegetation Index |
| `NTL.js` | Nighttime Lights |
| `LC.js` | Land Cover |
| `Climate.js` | Climate variables |
| `Biomass.js` | Above-ground biomass |
| `Canopy.js` | Forest canopy height |
| `dem_slope.js` | DEM and terrain slope |
| `shape_file.js` | Study-area polygons |

---

# 2. Data Preprocessing

The `data_preprocessing` directory contains ArcPy scripts for preparing the downloaded raster datasets.

These scripts perform operations such as:

- ROI extraction
- raster alignment
- reprojection
- snapping all rasters to the RGB grid
- computation of global normalization statistics

The output is the GeoKG dataset used for both pretraining and downstream experiments.

---

# 3. GeoKRL Model

The `model` directory contains the complete implementation of the proposed framework.

Main components include:

| File | Description |
|------|-------------|
| `GeoKRL.py` | GeoKRL backbone implementation |
| `train.py` | Self-supervised backbone pretraining |
| `train_task.py` | Downstream task training |
| `dataset_index.py` | Hierarchical dataset indexing |
| `raster_manager.py` | Dynamic raster loading |
| `sample_generator.py` | On-demand sample generation |
| `sample_generator_task.py` | Downstream sample generation |
| `modality_sampler.py` | Multimodal sampling strategy |
| `batch_generator.py` | Pretraining batch generator |
| `batch_generator_task.py` | Downstream batch generator |
| `config.py` | Dataset configuration |
| `hyperparameters.py` | Backbone hyperparameters |
| `task_hyperparameters.py` | Downstream hyperparameters |

---

# Model Checkpoints

Pretrained models are automatically saved in

```
model/auto_train_models/
```

Task-specific models are automatically saved in

```
model/task_auto_train_models/
```

---

# Installation

Clone the repository

```bash
git clone https://github.com/USERNAME/GeoKRL.git

cd GeoKRL
```

Install the required dependencies

```bash
pip install -r requirements.txt
```

---

# Running the Framework

## Backbone Pretraining

```bash
python model/train.py
```

---

## Downstream Task Training

```bash
python model/train_task.py
```

---

# Dataset

GeoKRL is trained using the **GeoKG** multimodal geospatial dataset introduced in the accompanying paper.

The dataset consists of multiple co-registered raster modalities collected over several countries, including:

- RGB imagery
- DEM
- Terrain slope
- NDVI
- Nighttime lights
- Climate variables
- Biomass
- Forest canopy
- Land cover
- Population
- Building footprints

Dataset availability will be announced upon publication.

---

# Citation

If you use this repository in your research, please cite:

```bibtex
Citation will be added after publication.
```

---

# License

This repository is released under the MIT License.

---

# Contact

For questions regarding the implementation, please open a GitHub issue or contact the corresponding author.

---

**GeoKRL** is developed for scalable self-supervised geospatial representation learning and reproducible multimodal Earth observation research.
