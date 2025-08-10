# Predicting Cognitive Trajectories in Alzheimer’s Disease

This project explores how to **predict future cognitive status** (e.g., MMSE, ADAS, CDR) of patients with Alzheimer’s disease using **longitudinal clinical data**.  
The workflow is implemented in a single Jupyter notebook:

> **Notebook**: `Alzheimer's Disease.ipynb`

---

## 🎯 Goals

- Load and explore a longitudinal dataset (`historical_data.csv`).
- Handle **missing values** and inspect **score distributions** (MMSE, ADAS, CDR).
- Build **patient-level sequences** across visits with prediction **horizons** (12/24/36 months).
- Create a **train/validation/test** split that respects patient identities.
- Train and evaluate baseline models for **trajectory forecasting**.

---

## 🧠 Problem Setting (Longitudinal Forecasting)

We model disease progression by using **past visits** to predict **future outcomes** at fixed horizons.  
For each patient, we align visits on a timeline and construct (X, y) pairs:

- **X**: features from past visits (up to `max_visits`, e.g., 5)
- **y**: future cognitive scores at 12, 24, 36 months (if available)

This mirrors common practice in longitudinal modeling for neurodegenerative diseases.

---

## 🗂 Data

- **Input file**: `historical_data.csv` (placed next to the notebook or in a `data/` folder)
- Each row represents a **visit** and typically includes:
  - `PATIENT_ID`, `EXAMDATE` (visit date)
  - Diagnosis / group labels (if available)
  - Cognitive endpoints (e.g., `MMSE_TOT`, `ADAS_TOT13`, `CDR_SOB`)
  - Additional clinical / demographic features

> ⚠️ **Confidentiality notice:** The repo does **not** ship the dataset due to privacy restrictions.  
> You must provide your own CSV locally:
> - Option A: same folder as the notebook
> - Option B: `data/historical_data.csv` and adapt the path in the notebook

---

## 🔎 Notebook Outline

1. **Load & Explore**
   - Read `historical_data.csv`
   - Parse dates (`EXAMDATE`)
   - Create a unique `VISIT_ID` (patient + date)

2. **Missing Values & Distributions**
   - Compute missingness per column
   - Visualize score distributions (histograms)
   - Optionally drop columns with too many missing values (e.g., >30%)

3. **Descriptive Statistics**
   - `df.describe()` for numeric variables
   - Quick checks for ranges/outliers

4. **Build Longitudinal Sequences**
   - Function: `group_visits_by_patient_with_visit_id_and_horizons(...)`
   - Parameters:
     - `max_visits` (e.g., 5)
     - `horizons_months = [12, 24, 36]`
     - `target_cols = ["MMSE_TOT", "ADAS_TOT13", "CDR_SOB"]`
   - Produces aligned past-to-future examples per patient

5. **Train / Validation / Test Split**
   - Split **by patient** (no leakage)
   - Typical ratios: 70/15/15 or similar

6. **Modeling & Evaluation**
   - Baselines (e.g., linear models or simple regressors)
   - Metrics (e.g., MAE / RMSE per target & horizon)
   - Learning curves (optional)

---

## 🧪 How to Run

### 1) Environment
```bash
# Create and activate a virtual environment (Python 3.10+)
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)

# Install minimal dependencies
pip install jupyter pandas numpy matplotlib scikit-learn
```

### 2) Launch the Notebook
```bash
jupyter notebook
# Open "Alzheimer's Disease.ipynb" in your browser
```

### 3) Add Data
Place your `historical_data.csv` alongside the notebook (or adjust the path in the first cell).

---

## 📈 Typical Outputs

- **Missingness summary** (which variables are sparse)
- **Score distribution plots** (MMSE/ADAS/CDR histograms)
- **Train/Val/Test sizes** (by unique patients)
- **Evaluation metrics** per target and horizon (e.g., 12/24/36 months)

> Tip: Save results (metrics or predictions) to CSV for later comparison.

---

## 🧩 Key Functions (from the notebook)

- **`group_visits_by_patient_with_visit_id_and_horizons(df, max_visits, horizons_months, target_cols, ...)`**  
  Builds aligned sequences per patient and generates (X, y) pairs for forecasting at specified horizons.

- **Utility cells** for:
  - Date parsing and sorting visits
  - Column selection / cleaning
  - Simple plotting (matplotlib)

---

## ✅ Good Practices Applied

- **Patient-level split** to avoid data leakage.
- **Explicit horizons** (12/24/36 months) for clinically meaningful forecasts.
- **Transparent preprocessing** (drop/keep logic for missingness).
- **Reproducibility** (single notebook pipeline, clear parameter cells).

---

## 🗺 Roadmap (Optional Extensions)

- Add **imputation** strategies (simple/iterative) for missing values.
- Try **temporal deep learning** (RNN/LSTM/Transformer) for sequences.
- Add **model tracking** (MLflow) and **data versioning** (DVC).
- Create a small **CLI** or **FastAPI** service to run predictions for a new patient.

---

## 📜 Citation / Inspiration

This notebook follows common approaches from longitudinal modeling in Alzheimer’s research (e.g., forecasting clinical endpoints over fixed horizons).  
If you build on scientific articles, add them here for reference.

---

## 📄 License

Specify your preferred license (e.g., MIT) in a `LICENSE` file if you plan to share the code and results publicly.

---

## 👤 Author

**Yassin Belhareth** — AI/NLP Engineer & Researcher  
*This notebook demonstrates a clear, step-by-step pipeline for longitudinal forecasting in Alzheimer’s Disease.*
