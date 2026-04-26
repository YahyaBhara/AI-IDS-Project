# AI-Based Intrusion Detection System (IDS)

## Overview

This project implements a Machine Learning-based Intrusion Detection System using the NSL-KDD dataset. The system classifies network traffic as either Normal or Attack using two models:

* Logistic Regression
* Neural Network (MLP)

## Features

* Data preprocessing and feature selection (8 key features)
* Model training using Logistic Regression and Neural Network
* Evaluation using Accuracy, Precision, Recall, and F1-score
* Confusion Matrix visualization
* Live prediction demo on sample network traffic

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/YahyaBhara/AI-IDS-Project.git
cd AI-IDS-Project
```

### 2. Install dependencies
pip install -r requirements.txt

### 3. Run the notebook
Open `code.ipynb` and run all cells.

## Dataset

* NSL-KDD dataset is included in the data folder
* File: KDDTrain+.txt

## Tools and Technologies

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib, Seaborn
* Jupyter Notebook

## Evaluation Metrics

* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix

## What Works

* Data loading and preprocessing
* Model training and evaluation
* Visualization (confusion matrix and comparison chart)
* Live attack prediction demo

## Limitations

* Only binary classification (Normal vs Attack)
* Limited feature set (8 features used)
* Not deployed as a real-time IDS system

## References

Foundational Paper
Awajan, A. (2023). A Novel Deep Learning-Based Intrusion Detection System for IoT Networks. Computers, 12(2), 34.

Contemporary Work
Zhang, Y., et al. (2024). Deep Learning Approaches for Network Intrusion Detection: A Survey. IEEE Access.

## Notes for Instructors

* All required data is included in the data folder
* To reproduce results, run all cells in notebook.ipynb
* Visual outputs will be generated automatically


