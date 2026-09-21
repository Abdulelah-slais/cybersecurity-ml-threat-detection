# Cybersecurity Machine Learning – Threat Classification & Anomaly Detection

## Overview

This project applies machine learning techniques to cybersecurity network traffic analysis.

The project focuses on classifying network traffic into multiple categories and detecting unusual network behavior using both supervised and unsupervised machine learning techniques.

The complete workflow includes data validation, preprocessing, feature engineering, model training, hyperparameter tuning, model evaluation, anomaly detection, and feature analysis.

---

## Project Objectives

The main objectives of this project were to:

- Prepare and validate cybersecurity network traffic data
- Perform data cleaning and feature engineering
- Build machine learning models for multi-class traffic classification
- Compare the performance of KNN and Linear SVM
- Tune KNN using cross-validation
- Detect unusual network traffic using Isolation Forest
- Evaluate classification performance
- Analyse important network traffic features
- Interpret anomaly detection results

---

## Dataset

The project uses a cybersecurity network traffic dataset containing:

- **21,185 network flows**
- **84 original attributes**
- **10 traffic classes**

The traffic classes include:

- Benign
- Generic
- DoS
- Reconnaissance
- Fuzzers
- Exploits
- Shellcode
- Backdoor
- Analysis
- Worms

The dataset contains network characteristics such as packet statistics, timing information, TCP flags, ports, and other network flow attributes.

The Jupyter Notebook references the original dataset as:

```text
Dataset-Brief 1 Cyber.csv
```

The original dataset is not included in this repository. However, the repository includes the generated CSV output files from the completed machine learning analysis.

---

## Data Preparation

Before training the machine learning models, the dataset was validated and prepared.

The process included:

- Checking for missing values
- Checking for duplicate records
- Checking for infinite values
- Validating data types
- Processing timestamp information
- Removing identifier-based features
- Removing constant features
- Preparing numeric features for machine learning

The final machine learning feature matrix contained **73 numeric features**.

---

## Feature Engineering

The timestamp attribute was transformed into:

- `ts_hour`
- `ts_dayofweek`
- `ts_month`

Identifier-based fields were removed to reduce the possibility of data leakage or memorisation:

- Flow ID
- Source IP
- Destination IP

Constant features that provided no useful variation for classification were also removed.

---

## Machine Learning Models

Three main machine learning approaches were used in the project.

### K-Nearest Neighbours (KNN)

KNN was used as a supervised multi-class classification model.

Because KNN relies on distance calculations, the numeric features were scaled before model training.

The baseline model used:

```text
K = 5
```

Hyperparameter tuning was then performed using **5-fold Stratified Cross-Validation**.

The following values were evaluated:

```text
K = 1, 3, 5, 7, 9, 11, 15
```

The selected tuned model used:

```text
K = 9
```

---

### Linear Support Vector Machine (SVM)

Linear SVM was used as the second supervised machine learning model.

The model was trained using the prepared and scaled network traffic features and evaluated using the same test data as KNN.

Linear SVM achieved the strongest overall supervised classification performance in the project.

---

### Isolation Forest

Isolation Forest was used for unsupervised anomaly detection.

Unlike the supervised models, Isolation Forest focuses on identifying network flows that are statistically unusual.

The model used:

```text
contamination = 0.05
```

This allowed the analysis to identify the most unusual **5% of network flows** for further investigation.

---

## Model Evaluation

An **80/20 stratified train/test split** was used for supervised model evaluation.

The models were evaluated using:

- Accuracy
- Macro Precision
- Macro Recall
- Macro F1 Score
- Classification Reports
- Confusion Matrices

### Supervised Model Results

| Model | Accuracy | Macro Precision | Macro Recall | Macro F1 |
|---|---:|---:|---:|---:|
| KNN (k=5) | 0.5702 | 0.5131 | 0.5120 | 0.5024 |
| KNN (k=9 tuned) | 0.5733 | 0.5279 | 0.5092 | 0.5039 |
| Linear SVM | **0.6408** | **0.5739** | **0.5697** | **0.5430** |

Linear SVM achieved the strongest overall supervised performance:

```text
Accuracy: 64.08%
Macro F1: 54.30%
```

---

## Anomaly Detection Results

Isolation Forest identified:

```text
1,060 anomalous network flows
```

The detected anomalies were analysed according to their known traffic labels and anomaly scores.

Traffic categories represented among the detected anomalies included:

- Generic
- DoS
- Exploits
- Other unusual network flows

Some benign traffic was also identified as statistically unusual, demonstrating that anomaly detection can support further security investigation rather than acting as a definitive malicious/benign classifier.

---

## Feature Analysis

The project also analysed which network features influenced the classification models.

### SVM Feature Importance

Linear SVM coefficients were analysed to identify features that influenced classification decisions.

### Permutation Importance

Permutation importance was used to measure how model performance changed when individual features were shuffled.

Feature groups analysed included:

- TCP flag counts
- Packet length statistics
- Segment sizes
- Destination ports
- Protocol information
- Timing-related features

---

## Machine Learning Workflow

```text
Cybersecurity Network Traffic
            |
            v
     Data Validation
            |
            v
      Data Cleaning
            |
            v
    Feature Engineering
            |
            v
     Train/Test Split
            |
      +-----+-----+
      |           |
      v           v
     KNN      Linear SVM
      |           |
      v           v
   Tuning     Evaluation
      |           |
      +-----+-----+
            |
            v
     Model Comparison

            +

     Isolation Forest
            |
            v
     Anomaly Detection
            |
            v
      Anomaly Analysis
```

---

## Generated Results

The repository includes the CSV output files generated from the completed machine learning analysis:

| File | Description |
|---|---|
| `supervised_model_comparison.csv` | Performance comparison between supervised models |
| `knn_per_class_report.csv` | KNN classification performance for each traffic class |
| `svm_per_class_report.csv` | Linear SVM classification performance for each traffic class |
| `svm_global_feature_importance.csv` | Global feature importance results from Linear SVM |
| `svm_permutation_importance.csv` | Feature importance calculated using permutation analysis |
| `anomaly_rate_by_label.csv` | Anomaly detection rate for each traffic label |
| `anomaly_label_distribution_pct.csv` | Distribution of detected anomalies across traffic classes |
| `top200_anomalies.csv` | Top 200 anomalous network flows identified by the anomaly detection model |

These files provide the generated results and evaluation evidence from the completed analysis.

---

## Technologies & Techniques

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Machine Learning
- K-Nearest Neighbours (KNN)
- Linear Support Vector Machine (SVM)
- Isolation Forest
- Feature Scaling
- Stratified Train/Test Split
- Cross-Validation
- Hyperparameter Tuning
- Multi-Class Classification
- Anomaly Detection
- Feature Engineering
- Feature Importance
- Cybersecurity Traffic Analysis

---

## Repository Contents

```text
cybersecurity-ml-threat-detection/
|
├── Ai.project.docx
├── abdulelah.ipynb
├── anomaly_label_distribution_pct.csv
├── anomaly_rate_by_label.csv
├── knn_per_class_report.csv
├── supervised_model_comparison.csv
├── svm_global_feature_importance.csv
├── svm_per_class_report.csv
├── svm_permutation_importance.csv
├── top200_anomalies.csv
└── README.md
```

### Main Files

- **`abdulelah.ipynb`** – Jupyter Notebook containing the machine learning implementation and analysis.
- **`Ai.project.docx`** – Full project documentation and report.
- **CSV result files** – Generated model evaluation, feature importance, classification, and anomaly detection outputs.

---

## Running the Notebook

The implementation is available in:

```text
abdulelah.ipynb
```

The notebook can be viewed directly through GitHub.

To reproduce the complete analysis, the original dataset referenced by the notebook is required:

```text
Dataset-Brief 1 Cyber.csv
```

The original dataset is not included in this repository. The generated output files from the completed analysis are included for review and demonstration.

---

## Key Learning Outcomes

This project provided practical experience in:

- Applying machine learning to cybersecurity data
- Network traffic analysis
- Data preprocessing and validation
- Feature engineering
- Multi-class classification
- KNN and Linear SVM
- Hyperparameter tuning
- Cross-validation
- Model evaluation
- Anomaly detection using Isolation Forest
- Feature importance analysis
- Interpreting cybersecurity machine learning results
- Technical project documentation

---

## Documentation

The repository includes:

- The complete Jupyter Notebook
- Full project report
- Supervised model comparison results
- Per-class classification reports
- Feature importance analysis
- Anomaly detection results
- Top detected anomalies

---

## Author

**Abdulelah Slais**  
Cybersecurity Student
