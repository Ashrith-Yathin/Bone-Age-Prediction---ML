# Bone Age Prediction - PRML Project

Bone age prediction from hand X-ray images using classical ML and deep learning.

## Setup

### Step 1: Clone the Repo
```bash
git clone <your-repo-url>
cd PRML
```

### Step 2: Download Dataset
Place your dataset in this structure:
```
PRML/
├── dataset/
│   ├── boneage-training-dataset/
│   │   └── boneage-training-dataset/  # Images here
│   ├── boneage-training-dataset.csv
│   ├── boneage-test-dataset/
│   └── boneage-test-dataset.csv
```

### Step 3: Create Virtual Environment
```bash
python3 -m venv bone_env
source bone_env/bin/activate  # Mac/Linux
# OR
bone_env\Scripts\activate  # Windows
```

### Step 4: Install Dependencies
```bash
pip install -r requirements.txt
```

**For M1/M2 Mac:**
```bash
pip install tensorflow-macos tensorflow-metal
```

**For Windows/Linux/Intel Mac:**
```bash
pip install tensorflow
```

### Step 5: Register Jupyter Kernel
```bash
pip install ipykernel
python -m ipykernel install --user --name=bone_age --display-name "Bone Age (Python 3.12)"
```

### Step 6: Run Notebook
```bash
jupyter notebook bone_age_prediction.ipynb
```

Or open in VS Code:
1. Open `bone_age_prediction.ipynb`
2. Select kernel: "Bone Age (Python 3.12)"
3. Run All

## Expected Runtime

- First run: 1-2 hours (extracts features + trains models)
- Subsequent runs: 30-40 mins (uses cached features)

## What Gets Generated

After running, these folders are created:
- `models/` - Trained ML models (.pkl, .h5)
- `cache/` - Extracted features (speeds up reruns)
- `results/` - All plots and visualizations
- `report/` - Results summary text file

## Files Already in Repo

- `bone_age_prediction.ipynb` - Complete implementation
- `requirements.txt` - All Python dependencies
- `.gitignore` - Ignores large generated files

## System Requirements

**Minimum:**
- Python 3.10-3.12
- 8GB RAM
- 5GB free disk space

**Recommended:**
- 16GB RAM
- GPU (M1/M2 Mac or NVIDIA CUDA)
- 10GB free disk space

## Results

Check `report/results_summary.txt` after running for:
- Regression metrics (MAE, RMSE, R²)
- Classification metrics (Accuracy, F1, QWK)
- Gender bias analysis
- Model comparison

## Common Issues

**Issue:** Module not found
**Fix:** Make sure virtual environment is activated and requirements installed

**Issue:** GPU not detected
**Fix:** 
- M1 Mac: `pip install tensorflow-macos tensorflow-metal`
- Others: `pip install tensorflow`

**Issue:** Out of memory
**Fix:** Reduce BATCH_SIZE in Cell 2 from 32 to 16

## Architecture

```mermaid
graph TD
    subgraph Input
        A[Hand Radiograph Image] --> B{Preprocessing}
    end

    subgraph "Path A: Classical Machine Learning"
        B -->|Resize & Grayscale| C[Feature Extraction]
        C --> D[HOG Features]
        C --> E[LBP Features]
        D --> F[Feature Concatenation]
        E --> F
        F --> G[PCA Dimensionality Reduction]
        G --> H{Regression Models}
        H --> I[Random Forest]
        H --> J[SVR]
        H --> K[Linear Regression]
        I --> L[Ensemble Prediction]
        J --> L
        K --> L
    end

    subgraph "Path B: Deep Learning (CNN)"
        B -->|Resize & Normalize| M[ResNet50 Backbone]
        M -->|Feature Maps| N[Global Average Pooling]
        N --> O[Dense Layer (256, ReLU)]
        O --> P[Dropout (0.5)]
        P --> Q[Output Layer (Linear)]
    end

    subgraph Output
        L --> R((Predicted Bone Age))
        Q --> R
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style R fill:#9f9,stroke:#333,stroke-width:2px
    style M fill:#bbf,stroke:#333,stroke-width:1px
    style H fill:#bfb,stroke:#333,stroke-width:1px
```

## Project Structure

```
PRML/
├── bone_age_prediction.ipynb  # Main notebook
├── requirements.txt            # Dependencies
├── README.md                   # This file
├── .gitignore                  # Git ignore
├── dataset/                    # Data (not in git)
├── models/                     # Generated models
├── cache/                      # Cached features
├── results/                    # Plots and visualizations
└── report/                     # Results summary
```

## Notes

- Dataset not included in repo (too large)
- Download RSNA Bone Age dataset separately
- Models are saved automatically during training
- Features are cached to speed up reruns

---

**Course:** Pattern Recognition and Machine Learning  
**Project:** Bone Age Prediction from Hand Radiographs