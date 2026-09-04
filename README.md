# PON-QoT-ML-Dataset

Machine-learning dataset, code, results, and figures for traffic classification experiments in a Passive Optical Network (PON) scenario.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22311774.svg)](https://doi.org/10.5281/zenodo.22311774)

## Overview

This repository provides the data and reproducible analysis used to evaluate machine-learning models for traffic classification in a synthetic PON scenario.

The study compares three supervised learning algorithms:

- K-Nearest Neighbors (KNN)
- Random Forest (RF)
- Support Vector Machine (SVM)

The repository includes the synthetic dataset, Jupyter notebook, generated results, figures, licensing information, and citation metadata.

## Dataset

The dataset is **synthetic** and contains **50,000 samples** and **18 variables** representing traffic, network, and optical-related parameters.

The target variable is:

- `traffic_type`

The four traffic classes are:

- `gaming`
- `iot`
- `video`
- `web`

Class distribution:

| Traffic class | Samples |
|---|---:|
| Gaming | 9,049 |
| IoT | 9,913 |
| Video | 16,118 |
| Web | 14,920 |
| **Total** | **50,000** |

### Features Used for Classification

Although the dataset contains 18 variables, the classification experiments use the following three traffic-related features:

- `packet_size_bytes`
- `packets_per_sec`
- `traffic_rate_mbps`

These variables are used as the input feature vector, while `traffic_type` is used as the prediction target.

## Machine-Learning Models

The following models are evaluated.

### K-Nearest Neighbors

- `n_neighbors = 7`
- StandardScaler preprocessing

### Random Forest

- `n_estimators = 120`
- `max_depth = 6`
- `min_samples_split = 20`
- `min_samples_leaf = 10`
- `max_features = "sqrt"`
- `random_state = 42`

### Support Vector Machine

- RBF kernel
- `C = 0.3`
- `gamma = "scale"`
- `class_weight = "balanced"`
- StandardScaler preprocessing

## Train-Test Split

The dataset is divided using a stratified hold-out split:

- Training set: **70%**
- Test set: **30%**
- `random_state = 42`
- Stratification by traffic class

## Main Results

The following test results were obtained:

| Model | Test Accuracy | Test F1-score | Overfitting Gap |
|---|---:|---:|---:|
| KNN | 0.7991 | 0.7982 | 0.0439 |
| Random Forest | **0.8112** | 0.8073 | 0.0129 |
| SVM | 0.8043 | **0.8077** | **0.0072** |

Random Forest achieved the highest test accuracy, while SVM obtained the highest test F1-score and the smallest train-test gap.

### Feature Importance

Random Forest feature importance:

| Feature | Importance |
|---|---:|
| `traffic_rate_mbps` | 0.4344 |
| `packet_size_bytes` | 0.3091 |
| `packets_per_sec` | 0.2565 |

### Computational Complexity

| Model | Training Time (s) | Inference Time per Sample (ms) | Model Size (KB) |
|---|---:|---:|---:|
| KNN | 0.0609 | 0.0298 | 1528.85 |
| Random Forest | 0.4896 | **0.0037** | 1394.29 |
| SVM | 17.8900 | 1.2186 | **717.69** |

Computational times depend on hardware, operating system, software versions, and runtime conditions. These values should therefore be interpreted as measurements from the reported experimental execution.

## Repository Structure

```text
PON-QoT-ML-Dataset/
│
├── README.md
├── LICENSE
├── DATA_LICENSE.md
├── CITATION.cff
├── requirements.txt
├── .gitignore
│
├── data/
│   └── pon_synthetic_dataset_50000_overlap.csv
│
├── notebooks/
│   └── PON_ML_case_study.ipynb
│
├── results/
│   ├── computational_complexity_results.csv
│   ├── overfitting_analysis_results.csv
│   └── feature_importance_results.csv
│
└── figures/
    ├── training_time_comparison.png
    ├── inference_time_comparison.png
    └── model_size_comparison.png
```

## Installation

Clone the repository:

```bash
git clone https://github.com/BereniceArguero/PON-QoT-ML-Dataset.git
cd PON-QoT-ML-Dataset
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

## Running the Experiment

Open JupyterLab:

```bash
jupyter lab
```

Then open:

```text
notebooks/PON_ML_case_study.ipynb
```

The notebook expects the dataset at:

```text
../data/pon_synthetic_dataset_50000_overlap.csv
```

Run all cells in order to reproduce the classification experiments, performance evaluation, overfitting analysis, computational complexity analysis, feature importance analysis, and figures.

## Reproducibility

For reproducibility:

- the train-test split uses `random_state = 42`;
- Random Forest uses `random_state = 42`;
- the split is stratified by `traffic_type`;
- KNN and SVM are implemented using pipelines with feature standardization.

Execution times may vary across computers.

## DOI

This release is archived on Zenodo and can be referenced using the following DOI:

**DOI:** [10.5281/zenodo.22311774](https://doi.org/10.5281/zenodo.22311774)

## Citation

If you use this dataset, code, or results in academic work, please cite the Zenodo record:

```text
Arguero Tello, J. B. (2026).
PON-QoT-ML-Dataset: Synthetic PON Traffic Dataset for Machine-Learning Traffic Classification.
Zenodo.
https://doi.org/10.5281/zenodo.22311774
```

The repository also includes a `CITATION.cff` file so GitHub can display a **Cite this repository** option.

A formal publication citation can be added when the associated paper is published.

## Data Notice

The dataset included in this repository is **synthetically generated** for research and methodological evaluation.

It should not be described as traffic captured from an operational PON deployment.

## License

This repository uses separate licenses for code and data.

### Source Code and Notebooks

The source code and Jupyter notebooks are licensed under the **MIT License**.

See:

```text
LICENSE
```

### Dataset

The synthetic dataset located in the `data/` directory is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

See:

```text
DATA_LICENSE.md
```

The dataset may be shared and adapted for any purpose provided appropriate attribution is given and any modifications are indicated.

Dataset covered by this license:

```text
data/pon_synthetic_dataset_50000_overlap.csv
```

When using the dataset in academic work, please provide appropriate attribution and cite the Zenodo DOI.

## Author

**Johanna Berenice Arguero Tello**
