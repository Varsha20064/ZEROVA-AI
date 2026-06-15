# 🛡️ Zerova: Multi-Modal Vulnerability AI

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)

**Zerova** is a multi-modal security intelligence framework designed to detect vulnerabilities in C/C++ source code. By fusing **Static Analysis**, **Neural Semantics (CodeBERT)**, and **Structural Graph Embeddings (GNN)**, Zerova achieves state-of-the-art accuracy in identifying common weakness enumerations (CWEs).

## 📋 Table of Contents
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Model Performance](#-model-performance)
- [Quick Start](#-quick-start)

## ✨ Key Features
*   **Hybrid Analysis:** Combines hand-crafted security features with deep learning embeddings.
*   **Multi-Modal Fusion:** Weighted consensus between Ensemble ML, Transformer semantics, and Graph Neural Networks.
*   **CWE Identification:** Automated tagging of detected risks (Buffer Overflow, SQLi, UAF, etc.).
*   **Refactored for Production:** Clean, modular Python package structure.

## 🧠 Architecture
Zerova processes code through three distinct pipelines:
1.  **Static Pipeline:** Extracts 20 features (cyclomatic complexity, dangerous function density, pointer ops) fed into a Voting Ensemble (XGBoost + CatBoost + LightGBM).
2.  **Semantic Pipeline:** Uses `microsoft/codebert-base` to capture long-range contextual dependencies in code logic.
3.  **Structural Pipeline:** Maps token co-occurrence into a graph and processes it via Graph Convolutional Networks (GNN) to understand code topology.

## 📂 Project Structure
```text
zerova/
├── environment.py   # Dependency & GPU management
├── dataset.py       # Data synthesis & template engines
├── features.py      # Static analysis & feature extraction
├── architectures.py # CodeBERT & GCN model definitions
└── inference.py     # Production-ready prediction pipeline
```

## ⚙️ Installation
Clone the repository and install the dependencies:
```bash
pip install -r requirements.txt
```
Or via the internal setup module:
```python
from zerova.environment import install_dependencies
install_dependencies()
```

## 📊 Model Performance
| Engine | Accuracy | F1 Score | AUC |
| :--- | :--- | :--- | :--- |
| **ML Ensemble** | 100.0% | 1.00 | 1.00 |
| **CodeBERT** | 100.0% | 1.00 | 1.00 |
| **GNN (GCN)** | 84.0% | 0.82 | 0.97 |

## 🛠 Quick Start
```python
from zerova.inference import ZerovaPredictor

# Initialize with saved weights
predictor = ZerovaPredictor(
    ensemble_path='models/ensemble.pkl',
    scaler_path='models/scaler.pkl',
    feature_names='models/feats.json'
)

# Analyze a code snippet
code = "void fn(char *s) { char b[10]; strcpy(b, s); }"
report = predictor.predict(code)

print(f"Risk: {report['risk_level']} ({report['risk_score']}%)")
print(f"Detected: {report['detected_cwes']}")
```
