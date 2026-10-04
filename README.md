# Investigating the Relationship of Flood Extent and Deep-Learning Segmentation Performance Using Sentinel-1 SAR Imagery

## Project Overview

This repository contains the code, trained models, results, figures and supplementary materials for the DSM500 final project:

**Investigating the Relationship of Flood Extent and Deep-Learning Segmentation Performance Using Sentinel-1 SAR Imagery**

The project investigates how continuous flood extent influences the performance of deep-learning models for flood segmentation using Sentinel-1 Synthetic Aperture Radar (SAR) imagery.

The study uses the Sen1Floods11 dataset and evaluates two semantic-segmentation architectures:

- U-Net
- SegFormer-B0

Flood extent is calculated for individual scenes using flood targets adjusted to exclude permanent surface water identified using the Joint Research Centre (JRC) surface-water data. Model performance is evaluated using:

- Intersection over Union (IoU)
- F1 score
- Precision
- Recall

The relationship between flood extent and segmentation performance is investigated using Pearson correlation, linear regression and LOWESS analysis. A geographically distinct Bolivia flood event is additionally retained as an unseen-event holdout for secondary validation.

The main finding is that flood extent has a positive but moderate and non-uniform association with segmentation performance. Greater flood extent was generally associated with higher segmentation performance, but flood extent alone did not explain the majority of scene-level variation. The results therefore suggest that additional scene characteristics, including spatial configuration, environmental conditions and SAR observability, may contribute to segmentation difficulty.

The project provides a reproducible framework for investigating flood extent as a scene-level factor affecting deep-learning flood-segmentation performance.

---

## Research Question

**How does flood extent influence the performance of deep-learning flood segmentation, and how does this relationship manifest across different segmentation performance measures, distinct architectures and an unseen flood event?**

---

## Project Objectives

The study has three primary objectives:

1. Quantify the relationship between flood extent and segmentation performance by calculating per-scene flood extent and evaluating its association with IoU, F1 score, precision and recall.

2. Characterise performance variation and segmentation failures across different flood extents using statistical analysis and representative qualitative prediction examples.

3. Assess the consistency of the observed relationship across U-Net, SegFormer-B0 and, as a secondary validation, the geographically distinct Bolivia holdout event.

---

## Dataset

The project uses the **Sen1Floods11** dataset, which contains geographically diverse Sentinel-1 flood observations and associated flood-reference data.

The study uses the hand-labelled Sentinel-1 imagery, including the VV and VH SAR channels.

The final modelling workflow additionally incorporates the JRC permanent-water information to distinguish event-associated flood water from permanent surface water.

### Dataset availability

The complete Sentinel-1/Sen1Floods11 dataset is **not included in this repository because of its size**.

The official Sen1Floods11 dataset is available through the Cloud to Street Sen1Floods11 repository and its associated Google Cloud Storage bucket.

The original dataset documentation indicates that the complete dataset is approximately 14 GB and provides instructions for downloading it using `gsutil`.

The dataset should be downloaded separately and placed inside the `Data/` directory using the folder structure expected by the notebooks.

The original dataset should be cited as:

> Bonafilia, D., Tellman, B., Anderson, T. and Issenberg, E. (2020). Sen1Floods11: A georeferenced dataset to train and test deep learning flood algorithms for Sentinel-1. IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops.

---

## Repository Structure

```text
MSc Dissertation GitHub/
│
├── README.md
│
├── Data/
│   └── [Sen1Floods11 dataset - downloaded separately]
│
├── Results/
│   └── tables/
│       ├── chip_dataTable.csv
│       ├── bolivia_holdout_dataTable.csv
│       └── experiment_design_dataTable.csv
│
├── results_new/
│   ├── models/
│   │   ├── unet_best.pt
│   │   └── segformer_b0_best.pt
│   │
│   ├── tables/
│   │   └── [final statistical and model results]
│   │
│   └── figures/
│       └── [final figures and qualitative examples]
│
├── notebooks/
│   ├── 01_RAW_Data_Exploration.ipynb
│   ├── 02_Data_Cleaning.ipynb
│   ├── 03_Experiment_Design.ipynb
│   ├── 04_Model_Training_NEW.ipynb
│   └── 05_Statistical_Analysis_NEW.ipynb
│
└── dissertation/
    └── DSM500 Final Project.pdf
```

---

# Reproducing the Analysis

The notebooks are intended to be run sequentially in the following order.

### 1. Raw Data Exploration

`01_RAW_Data_Exploration.ipynb`

This notebook contains the initial exploratory data analysis (EDA) and quality assessment of the Sen1Floods11 dataset, including inspection of the Sentinel-1 imagery, reference data and permanent-water information.

Notebook 1 is primarily an exploratory and development notebook rather than a clean end-to-end reproduction script. It contains intermediate inspection, diagnostic and exploratory code used during the early stages of the project. Therefore, it is not necessary to reproduce the final dissertation results by running every cell in this notebook sequentially.

The raw Sen1Floods11 dataset is required for the exploratory analysis in this notebook and should be placed in:

Data/Sen1Floods11_raw/

---

### 2. Data Cleaning

**File:** `02_Data_Cleaning.ipynb`

This notebook performs data quality control and generates the intermediate metadata tables required by the subsequent workflow.

The principal outputs are:

```text
Results/tables/chip_dataTable.csv
Results/tables/bolivia_holdout_dataTable.csv
```

---

### 3. Experimental Design

**File:** `03_Experiment_Design.ipynb`

This notebook defines the experimental population and prepares the scene-level metadata used by the modelling workflow.

The principal output is:

```text
Results/tables/experiment_design_dataTable.csv
```

---

### 4. Model Training

**File:** `04_Model_Training_NEW.ipynb`

This notebook contains the final model-training and evaluation workflow used for the dissertation.

Two segmentation architectures are trained:

- **U-Net** — convolutional baseline architecture
- **SegFormer-B0** — Transformer-based semantic-segmentation architecture

Both models use the same Sentinel-1 VV/VH input data and the final JRC-adjusted flood target.

The final trained model checkpoints are provided in:

```text
results_new/models/
```

The notebook also generates model predictions, performance results and figures used in the subsequent statistical analysis.

---

### 5. Statistical Analysis

**File:** `05_Statistical_Analysis_NEW.ipynb`

This notebook contains the final statistical analysis used in the dissertation.

The analysis evaluates the relationship between continuous flood extent and per-scene segmentation performance using:

- Pearson correlation
- Linear regression
- LOWESS analysis
- Regression diagnostics
- Influential-observation analysis
- HC3 heteroskedasticity-consistent regression sensitivity analysis
- Secondary analysis of the Bolivia holdout

The analysis considers:

- IoU
- F1 score
- Precision
- Recall

for both U-Net and SegFormer-B0.

Final statistical results and figures are stored in:

```text
results_new/tables/
results_new/figures/
```

---

# Models

Two final trained model checkpoints are included in the repository:

```text
results_new/models/unet_best.pt
results_new/models/segformer_b0_best.pt
```

These represent the final model states retained for evaluation in the dissertation.

The models are provided for research and reproducibility purposes and should not be interpreted as operational flood-mapping systems.

---

# Results

The repository contains the final quantitative and qualitative results generated during the project.

### Tables

The `results_new/tables/` directory contains the final model results, Pearson correlations, regression results, regression diagnostics, sensitivity analysis and Bolivia holdout results.

The `Results/tables/` directory contains the intermediate metadata tables required by the modelling workflow.

### Figures

The `results_new/figures/` directory contains the figures used for model evaluation, statistical analysis and qualitative error analysis.

---

# Main Findings

The principal test population consisted of **87 usable test scenes**.

The analysis found a **positive but moderate and non-uniform relationship** between flood extent and segmentation performance.

For U-Net, flood extent explained approximately **17.3% of the variance in IoU**.

For SegFormer-B0, flood extent explained approximately **11.9% of the variance in IoU**.

All eight model-metric Pearson correlations in the principal population were positive, although the strength of the relationships differed between metrics and architectures.

The results also demonstrated substantial variation between individual scenes with similar flood extents, indicating that flood extent alone does not determine segmentation difficulty.

A geographically distinct Bolivia holdout provided limited but directionally consistent evidence that the observed relationship can extend beyond the principal test population, although the relationships were weaker and statistical support was limited.

---

# Reproducibility Notes

The final modelling workflow represented in this repository is the **JRC-adjusted workflow** used for the final dissertation results.

An earlier modelling run was superseded after permanent surface water was incorporated into the flood-target definition. The notebooks and model checkpoints provided in this repository correspond to the final adjusted workflow.

The raw Sen1Floods11 dataset is intentionally not redistributed because of its size. Users attempting to reproduce the analysis must obtain the dataset separately.

The repository includes the final notebooks, trained models, figures, tables and intermediate metadata required to inspect and reproduce the final analysis where practical.

---

# Computational Environment

The project was developed using Python and Jupyter notebooks in a VS Code environment.

The main Python packages used include:

- NumPy
- pandas
- Matplotlib
- Rasterio
- PyTorch
- Hugging Face Transformers
- SciPy
- Statsmodels

The model-training workflow uses PyTorch, while SegFormer-B0 is implemented using the Hugging Face Transformers library.

Exact package versions may depend on the computational environment used to reproduce the project.

---

# Dissertation

The complete final dissertation is provided in:

```text
dissertation/DSM500 Final Project.pdf
```

The dissertation contains the full literature review, methodology, results, discussion, limitations, conclusion, references and ethics statement.
NOTE: The full dissertation report is too large for GitHub submit, and can be provided separately on request from the author. 

---

# Author

**Archie Hulse**

MSc Data Science  
DSM500 Final Project
