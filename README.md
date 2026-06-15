# ZEROVA-AI
# 🛡️ Zerova: AI-Powered Vulnerability Detection

Zerova is a multi-modal deep learning framework designed to detect security vulnerabilities (CWEs) in C/C++ source code. It combines traditional static analysis with state-of-the-art Large Language Models (LLMs) and Graph Neural Networks (GNNs).

## 🚀 Features
- **Hybrid Detection**: Combines 20+ hand-crafted static features with semantic deep learning.
- **Triple-Model Architecture**:
  - **ML Ensemble**: XGBoost, LightGBM, and CatBoost soft-voting.
  - **CodeBERT**: Fine-tuned Transformer for deep semantic understanding.
  - **GNN**: Token co-occurrence graph analysis for structural pattern recognition.
- **High Precision**: Reached ~100% F1-score on synthetic benchmarks and high AUC on structural graphs.
- **Explainability**: Integrated feature importance and CWE signature mapping.

## 📊 Performance Summary
| Model | Accuracy | F1 Score | AUC |
| :--- | :--- | :--- | :--- |
| **ML Ensemble** | 100.0% | 100.0% | 100.0% |
| **CodeBERT** | 100.0% | 100.0% | 100.0% |
| **GNN (Structural)**| 84.0% | 81.8% | 97.6% |

## 🛠️ Installation

```bash
git clone https://github.com/your-username/zerova.git
cd zerova
pip install -r requirements.txt
```

## 💻 Usage

To predict vulnerabilities in a code snippet:

```python
from zerova.pipeline import VulnAIPipeline

code = "void vuln() { char b[10]; gets(b); }"
pipeline = VulnAIPipeline.load_pretrained("models/")
result = pipeline.predict(code)

print(f"Risk: {result['risk_level']} ({result['risk_score']}%)")
print(f"Detected CWEs: {result['detected_cwes']}")
```

## 📂 Project Structure
- `notebooks/`: Research and model training (Colab).
- `models/`: Exported model artifacts (.pkl, .pt).
- `web_app/`: Backend API and React frontend for real-time analysis.

## ⚖️ License
MIT License
