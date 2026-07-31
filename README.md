# GeoKRL: A Self-Supervised Multimodal Foundation Model for Geospatial Representation Learning

GeoKRL is a self-supervised multimodal foundation learning framework designed to learn transferable geospatial representations from heterogeneous Earth observation data. The learned backbone can be transferred to multiple downstream geospatial prediction tasks, including population estimation, biomass estimation, and building mapping.

This repository accompanies the paper:

> **GeoKRL: A Self-Supervised Multimodal Foundation Model for Geospatial Representation Learning**  
> *(Paper information will be updated after publication.)*

---

# Repository Structure

```
GeoKRL/
│
├── GeoKG_dataset/
│   └── README.md
│
├── data_collection/
│   ├── Biomass.js
│   ├── Canopy.js
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
│   ├── dataset_index.py
│   ├── raster_manager.py
│   ├── sample_generator.py
│   ├── sample_generator_task.py
│   ├── modality_sampler.py
│   ├── batch_generator.py
│   ├── batch_generator_task.py
│   ├── config.py
│   ├── hyperparameters.py
│   ├── task_hyperparameters.py
│   ├── best_pretraining_config.py
│   ├── auto_train_models/
│   └── task_auto_train_models/
│
└── README.md
```

---

# Overall Workflow

The complete GeoKRL framework consists of four sequential stages.

```
Google Earth Engine
        │
        ▼
Data Collection
(JavaScript)
        │
        ▼
Data Preprocessing
(ArcPy)
        │
        ▼
GeoKG Dataset
        │
        ▼
GeoKRL Self-Supervised Pretraining
        │
        ▼
Pretrained Backbone
        │
        ▼
Downstream Prediction Tasks
```

---

# 1. Data Collection

The `data_collection` directory contains Google Earth Engine (GEE) JavaScript scripts used to download all remote sensing datasets employed in this work.

The scripts automatically export two 50 km × 50 km regions of interest (ROIs) for each study country.

Available scripts include:

| Script | Dataset |
|---------|----------|
| `rgb.js` | Sentinel-2 RGB imagery |
| `NDVI.js` | Normalized Difference Vegetation Index |
| `NTL.js` | Nighttime Lights |
| `LC.js` | ESA WorldCover Land Cover |
| `Climate.js` | ERA5-Land climate variables |
| `Biomass.js` | Above-ground biomass |
| `Canopy.js` | Forest canopy height |
| `dem_slope.js` | DEM and terrain slope |
| `shape_file.js` | ROI polygons |

---

# 2. Data Preprocessing

The `data_preprocessing` directory contains ArcPy scripts that transform the downloaded datasets into a unified multimodal benchmark.

The preprocessing pipeline performs:

- extraction of ROI-specific rasters;
- clipping of global datasets;
- raster reprojection;
- raster alignment;
- snapping every modality onto the RGB grid;
- generation of global normalization statistics.

The output of this stage is the **GeoKG** dataset used throughout the paper.

---

# 3. GeoKG Dataset

The `GeoKG_dataset` directory provides access to the complete benchmark dataset used in this study.

GeoKG is obtained after executing all data collection and preprocessing steps contained in this repository.

The dataset contains co-registered multimodal raster patches collected over multiple countries and includes:

- Sentinel-2 RGB imagery
- Digital Elevation Model (DEM)
- Terrain slope
- NDVI
- Nighttime lights
- Climate
- Above-ground biomass
- Forest canopy height
- Land cover
- Population density
- Building footprints

Every modality is perfectly aligned on the same spatial grid, allowing direct multimodal learning.

> **Note**
>
> Because the complete GeoKG dataset is several gigabytes in size, it is distributed separately from the source code repository.
>
> The `GeoKG_dataset` folder contains instructions and links for downloading the dataset.

---

# 4. GeoKRL Model

The `model` directory contains the complete implementation of the proposed framework.

| File | Description |
|------|-------------|
| `GeoKRL.py` | GeoKRL backbone implementation |
| `train.py` | Self-supervised backbone pretraining |
| `train_task.py` | Downstream task training |
| `dataset_index.py` | Hierarchical dataset indexing |
| `raster_manager.py` | Dynamic raster loading |
| `sample_generator.py` | On-demand sample generation |
| `sample_generator_task.py` | Downstream task sample generation |
| `modality_sampler.py` | Multimodal sampling strategy |
| `batch_generator.py` | Pretraining batch generator |
| `batch_generator_task.py` | Downstream batch generator |
| `config.py` | Dataset configuration |
| `hyperparameters.py` | Backbone hyperparameter search space |
| `task_hyperparameters.py` | Downstream hyperparameter search space |

---

# Model Checkpoints

Pretrained GeoKRL backbone weights are automatically saved in

```
model/auto_train_models/
```

Task-specific prediction models are automatically saved in

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

# Citation

If you use GeoKRL or the GeoKG dataset in your research, please cite:

```bibtex
Citation information will be added after publication.
```

---

# License

This project is released under the MIT License.

---

# Contact

For questions, bug reports, or suggestions, please open a GitHub Issue or contact the corresponding author.

---

**GeoKRL** provides a complete and reproducible pipeline covering:

- multimodal geospatial data collection;
- large-scale dataset preprocessing;
- construction of the GeoKG benchmark;
- self-supervised foundation model pretraining;
- downstream geospatial prediction using transferable representations.
