# Alzheimer’s Disease Progression Prediction

This notebook implements a complete pipeline to predict the multi-stage progression of Alzheimer’s disease from longitudinal clinical data and incomplete biomarkers.

## Main Steps
- **Data Preprocessing**: Missing value imputation, encoding of categorical features, and consistent normalization between training and test sets.  
- **Feature Selection**: Selection of the most relevant features for prediction.  
- **Sequence Construction**: Generation of input-output pairs (X, y) respecting the temporal structure of patient visits.  
- **Model Training**: BiLSTM neural network for multi-stage prediction.  
- **Evaluation**: Performance metrics on a test set and visualization of results.

## Requirements
Python 3.9+ with:
```bash
pip install pandas numpy scikit-learn tensorflow
```

## Usage
Run the notebook sequentially to reproduce preprocessing, model training, and evaluation steps.
