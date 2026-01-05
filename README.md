# 🩺 Breast Cancer Cell Classification using SVM

## 📌 Overview
A machine learning project for binary classification of breast cancer cells as **Benign** or **Malignant** using Support Vector Machines (SVM). This model analyzes cytological features from fine needle aspirates to assist in early cancer diagnosis with high accuracy.

## 📊 Dataset
The project uses the **Breast Cancer Wisconsin (Diagnostic) Dataset** containing 699 cell samples with the following features:

### **Features (10 cytological characteristics)**
1. **ID**: Sample identification number
2. **Clump**: Clump thickness (1-10)
3. **UnifSize**: Uniformity of cell size (1-10)
4. **UnifShape**: Uniformity of cell shape (1-10)
5. **MargAdh**: Marginal adhesion (1-10)
6. **SingEpiSize**: Single epithelial cell size (1-10)
7. **BareNuc**: Bare nuclei (1-10)
8. **BlandChrom**: Bland chromatin (1-10)
9. **NormNucl**: Normal nucleoli (1-10)
10. **Mit**: Mitoses (1-10)

### **Target Variable**
- **Class**: Diagnosis classification
  - **2**: Benign (non-cancerous)
  - **4**: Malignant (cancerous)

## 🚀 Features
- **Data Visualization**: Scatter plots for feature analysis
- **Data Cleaning**: Handling missing values in 'BareNuc' column
- **Feature Scaling**: StandardScaler for normalization
- **SVM Classification**: RBF kernel for non-linear separation
- **Comprehensive Evaluation**: Multiple metrics (accuracy, F1, Jaccard)
- **Confusion Matrix**: Visual interpretation of model performance

## 🛠️ Installation & Usage

### **Prerequisites**
```bash
pip install pandas numpy matplotlib scikit-learn
```

### **Running the Project**
1. Clone the repository:
```bash
git clone Breast-Cancer-Detection.git
cd Breast-Cancer-Detection.git
```

2. Place the dataset in the project directory:
```
breast-cancer-classification/
├── cell_samples.csv           # Dataset
├── Cancer_Detection.ipynb  # Main notebook
├── README.md                  # Documentation
└── requirements.txt           # Dependencies
```

3. Run the Jupyter notebook:
```bash
jupyter notebook breast_cancer_classifier.ipynb
```

## 📈 How It Works

### **1. Data Preprocessing**
```python
# Clean missing values
cell_df = cell_df[cell_df["BareNuc"] != "?"]
cell_df["BareNuc"] = cell_df["BareNuc"].astype(float)

# Feature scaling
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

### **2. Model Training**
- **Algorithm**: Support Vector Machine (SVM)
- **Kernel**: Radial Basis Function (RBF)
- **Data Split**: 80% training, 20% testing
- **Stratification**: Preserves class distribution

### **3. Model Evaluation**
- **Confusion Matrix**: Visual error analysis
- **Jaccard Score**: Similarity metric for binary classification
- **F1 Score**: Harmonic mean of precision and recall

## 🔍 Model Architecture

### **SVM Configuration**
```python
svm_model = SVC(
    kernel="rbf",        # Non-linear kernel for complex patterns
    C=1.0,              # Regularization parameter (default)
    gamma='scale',      # Kernel coefficient
    random_state=None   # No specific seed for default behavior
)
```

### **Data Splitting Strategy**
```python
X_train, X_test, y_train, y_test = train_test_split(
    X_scaled,
    y,
    test_size=0.2,
    random_state=4,
    stratify=y  # Maintain class proportions
)
```

## 📊 Results

### **Model Performance**
- **Test Set Size**: 137 samples
- **Confusion Matrix**:
  - **True Positives (Benign)**: 83
  - **False Positives**: 6
  - **False Negatives**: 2
  - **True Positives (Malignant)**: 46
- **Jaccard Score**: **0.9121** (Benign as positive class)
- **Weighted F1 Score**: **0.9421**

### **Visualizations**
![Clump vs UnifSize Scatter Plot](clump_unifsize_scatter.png)
*Scatter plot showing separation between benign (blue) and malignant (orange) cells*

![Confusion Matrix](confusion_matrix.png)
*Visual representation of model predictions vs actual labels*

## 💡 Interpretation

### **Key Findings**
1. **High Accuracy**: Model achieves excellent separation between classes
2. **Low False Negatives**: Only 2 malignant cases misclassified as benign (critical for medical applications)
3. **Feature Importance**: Clump thickness and uniformity size show clear separation patterns

### **Medical Implications**
- **Early Detection**: Model can assist in identifying malignant cells early
- **Reduced Biopsies**: Accurate predictions could reduce unnecessary invasive procedures
- **Clinical Support**: Provides second opinion for pathologists

## 🏗️ Project Structure
```
breast-cancer-classification/
│
├── cell_samples.csv                     # Original dataset
├── Cancer_Detection.ipynb       # Main analysis notebook
├── README.md                            # Documentation
├── requirements.txt                     # Python dependencies
├── models/                              # Trained models
│   ├── svm_model.pkl
│   └── scaler.pkl
├── visuals/                             # Generated plots
│   ├── confusion_matrix.png
│   ├── scatter_plot.png
│   └── feature_importance.png
├── reports/                             # Evaluation reports
│   ├── classification_report.txt
│   └── performance_metrics.json
└── src/                                 # Source code modules
    ├── preprocessing.py
    ├── visualization.py
    └── evaluation.py
```

## 🔧 Customization

### **Adjust SVM Parameters**
```python
# Customize SVM for different requirements
custom_svm = SVC(
    kernel='rbf',
    C=10.0,              # Higher C = less regularization
    gamma=0.01,          # Kernel width parameter
    class_weight='balanced',  # Handle class imbalance
    probability=True      # Enable probability estimates
)
```

### **Try Different Kernels**
```python
kernels = ['linear', 'poly', 'rbf', 'sigmoid']
for kernel in kernels:
    model = SVC(kernel=kernel)
    # Train and evaluate each kernel
```

## 📈 Performance Improvement Tips

### **1. Feature Engineering**
- Create composite features from existing ones
- Apply PCA for dimensionality reduction
- Feature selection using mutual information

### **2. Model Enhancement**
- Hyperparameter tuning with GridSearchCV
- Ensemble methods (SVM + Random Forest)
- Cross-validation for robust evaluation

### **3. Medical-Specific Improvements**
- Cost-sensitive learning (higher penalty for false negatives)
- ROC curve analysis for different thresholds
- Calibration of probability outputs

## 🎯 Use Cases

### **Medical Applications**
1. **Pathology Support**: Assist pathologists in cytological analysis
2. **Telemedicine**: Remote diagnosis support
3. **Medical Education**: Teaching tool for cytology students
4. **Screening Programs**: Mass screening automation

### **Research Applications**
1. **Feature Analysis**: Identify most discriminative cytological features
2. **Algorithm Comparison**: Benchmark against other ML models
3. **Dataset Augmentation**: Generate synthetic cell samples

## 🔄 Future Enhancements

### **Planned Features**
- [ ] **Web Interface**: Streamlit dashboard for predictions
- [ ] **API Endpoint**: REST API for integration with hospital systems
- [ ] **Explainable AI**: SHAP/LIME for model interpretability
- [ ] **Multi-class Classification**: Subtype classification of malignancies

### **Technical Improvements**
- [ ] **Hyperparameter Optimization**: Bayesian optimization
- [ ] **Feature Importance**: Permutation importance analysis
- [ ] **Model Deployment**: Docker container with FastAPI
- [ ] **Continuous Learning**: Model updates with new data

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request


## ⚠️ Medical Disclaimer

**Important**: This model is for **educational and research purposes only**. It should **NOT** be used for actual medical diagnosis, treatment decisions, or clinical practice. Always consult with qualified healthcare professionals and follow established medical protocols for cancer diagnosis and treatment.

## 📚 References

1. Breast Cancer Wisconsin (Diagnostic) Data Set - UCI Machine Learning Repository
2. Scikit-learn Documentation: [SVM](https://scikit-learn.org/stable/modules/svm.html)
3. American Cancer Society: Breast Cancer Facts & Figures
4. Clinical Applications of Machine Learning in Pathology

## ✉️ Contact

[Parsa Khaghani - email@example.com](https://www.linkedin.com/in/parsa-khaghani-a22847326/)

Project Link: https://github.com/nowherewalrus/Breast-Cancer-Detection.git

## 🙏 Acknowledgments

- University of Wisconsin Hospitals for the dataset
- Scikit-learn development team
- Medical researchers in oncology and pathology
- Open source community contributors

## 🚀 Quick Start

### **For Basic Usage:**
```python
# Load and preprocess
cell_df = pd.read_csv('cell_samples.csv')
cell_df = cell_df[cell_df["BareNuc"] != "?"]

# Train model
svm_model = SVC(kernel="rbf")
svm_model.fit(X_train, y_train)

# Make prediction
prediction = svm_model.predict([patient_features])
```

### **For Production Deployment:**
```python
# Save model
import joblib
joblib.dump(svm_model, 'breast_cancer_svm_model.pkl')
joblib.dump(scaler, 'feature_scaler.pkl')

# Load and predict
model = joblib.load('breast_cancer_svm_model.pkl')
scaler = joblib.load('feature_scaler.pkl')
scaled_features = scaler.transform([new_sample])
prediction = model.predict(scaled_features)
```

---

**Note**: The warning about `numexpr` version is non-critical. To resolve:
```bash
pip install --upgrade numexpr
```

---

**Early Detection Saves Lives! 🎗️🔬**
