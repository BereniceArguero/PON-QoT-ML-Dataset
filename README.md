# PON-QoT-ML-Dataset

Machine-learning dataset, code, results, and figures for traffic classification experiments in a Passive Optical Network (PON) scenario.

## Overview

This repository provides the data and reproducible analysis used to evaluate machine-learning models for traffic classification in a synthetic PON scenario.

The study compares three supervised learning algorithms:

- K-Nearest Neighbors (KNN)
- Random Forest (RF)
- Support Vector Machine (SVM)

The repository includes the synthetic dataset, Jupyter notebook, generated results, and figures used in the analysis.

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

### Features used for classification

Although the dataset contains 18 variables, the classification experiments use the following three traffic-related features:

- `packet_size_bytes`
- `packets_per_sec`
- `traffic_rate_mbps`

These variables are used as the input feature vector, while `traffic_type` is used as the prediction target.

## Machine-Learning Models

The following models are evaluated:

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

Computational times depend on hardware, operating system, software versions, and runtime conditions; therefore, these values should be interpreted as measurements from the reported experimental execution.

## Repository Structure

```text
PON-QoT-ML-Dataset/
│
├── README.md
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

Create and activate a Python virtual environment if desired, then install the required packages:

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

## Requirements

The main Python dependencies are listed in `requirements.txt`.

Core libraries include:

- NumPy
- pandas
- Matplotlib
- seaborn
- scikit-learn
- JupyterLab

## Citation

If you use this dataset, code, or results in academic work, please cite the associated publication.

A formal citation will be added here when the corresponding paper is published.

Suggested temporary repository citation:

```text
Arguero Tello, J. B. PON-QoT-ML-Dataset: Synthetic PON traffic dataset
and machine-learning traffic classification experiments. GitHub repository.
```

## Data Notice

The dataset included in this repository is synthetically generated for research and methodological evaluation. It should not be described as traffic captured from an operational PON deployment.

## License

Add the selected repository license here once defined.
