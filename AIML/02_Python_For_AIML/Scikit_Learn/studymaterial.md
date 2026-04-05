Complete Scikit-Learn Mastery Guide
From Absolute Beginner to Expert
Table of Contents
Introduction & Foundation
Installation & Setup
Understanding Data in Scikit-Learn
The Scikit-Learn API Design
Data Preprocessing
Supervised Learning - Regression
Supervised Learning - Classification
Unsupervised Learning
Model Evaluation & Validation
Hyperparameter Tuning
Feature Engineering & Selection
Pipelines
Ensemble Methods
Advanced Topics
Real-World Projects
Chapter 1: Introduction & Foundation
What is Machine Learning?
Imagine you want to teach a child to recognize cats. You don't give them a rulebook saying "cats have pointed ears, whiskers, and fur." Instead, you show them thousands of cat pictures, and eventually, they learn to recognize cats on their own.

Machine Learning works exactly the same way.

text

Traditional Programming:
    Data + Rules → Computer → Output

Machine Learning:
    Data + Output → Computer → Rules (Model)
The Three Types of Machine Learning
text

┌─────────────────────────────────────────────────────────────────────┐
│                    MACHINE LEARNING TYPES                          │
├─────────────────────┬─────────────────────┬─────────────────────────┤
│  SUPERVISED         │  UNSUPERVISED       │  REINFORCEMENT          │
│                     │                     │                         │
│  • Has labels       │  • No labels        │  • Learns from rewards  │
│  • Prediction       │  • Find patterns    │  • Trial and error      │
│                     │                     │                         │
│  Examples:          │  Examples:          │  Examples:              │
│  - Spam detection   │  - Customer groups  │  - Game AI              │
│  - Price prediction │  - Anomaly finding  │  - Robotics             │
└─────────────────────┴─────────────────────┴─────────────────────────┘
What is Scikit-Learn?
Scikit-Learn (also called sklearn) is a free, open-source machine learning library for Python.

Why Scikit-Learn?
Feature	Benefit
Simple API	Same syntax for all algorithms
Comprehensive	100+ algorithms included
Well-documented	Excellent tutorials and examples
Production-ready	Used by Netflix, Spotify, etc.
Integration	Works with NumPy, Pandas, Matplotlib
What Can You Build With Scikit-Learn?
text

┌────────────────────────────────────────────────────────────┐
│                 SCIKIT-LEARN APPLICATIONS                  │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  🏠 House Price Prediction     📧 Spam Email Detection    │
│  🏥 Disease Diagnosis          👤 Customer Segmentation   │
│  💳 Fraud Detection            📊 Stock Market Analysis   │
│  🎬 Movie Recommendations      📝 Text Classification     │
│  🖼️ Image Recognition          🔍 Anomaly Detection       │
│                                                            │
└────────────────────────────────────────────────────────────┘
Chapter 2: Installation & Setup
Installing Scikit-Learn
Method 1: Using pip (Recommended for beginners)
Bash

# Basic installation
pip install scikit-learn

# Install with specific version
pip install scikit-learn==1.3.0

# Upgrade to latest version
pip install --upgrade scikit-learn
Method 2: Using conda (If you use Anaconda)
Bash

# Install via conda
conda install scikit-learn

# Create a new environment with scikit-learn
conda create -n ml_env python=3.9 scikit-learn
conda activate ml_env
Method 3: Install with all dependencies
Bash

# Install complete data science stack
pip install numpy pandas matplotlib scikit-learn jupyter
Verifying Installation
Python

# verify_installation.py

import sklearn
print(f"Scikit-Learn Version: {sklearn.__version__}")

# Check all is working
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier

# Quick test
data = load_iris()
X_train, X_test, y_train, y_test = train_test_split(
    data.data, data.target, test_size=0.2
)
model = KNeighborsClassifier()
model.fit(X_train, y_train)
accuracy = model.score(X_test, y_test)

print(f"Test passed! Model accuracy: {accuracy:.2%}")
print("✅ Scikit-Learn is installed correctly!")
Expected Output:

text

Scikit-Learn Version: 1.3.0
Test passed! Model accuracy: 96.67%
✅ Scikit-Learn is installed correctly!
Understanding the Scikit-Learn Ecosystem
text

┌─────────────────────────────────────────────────────────────────┐
│                    SCIKIT-LEARN ECOSYSTEM                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   NumPy ──────┐                                                │
│               │                                                 │
│   Pandas ─────┼──────► Scikit-Learn ──────► Predictions        │
│               │              │                                  │
│   SciPy ──────┘              │                                  │
│                              ▼                                  │
│                        Matplotlib                               │
│                     (Visualization)                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 3: Understanding Data in Scikit-Learn
The Fundamental Concept: Features and Targets
text

┌─────────────────────────────────────────────────────────────────┐
│                    DATA STRUCTURE IN ML                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   FEATURES (X)                         TARGET (y)               │
│   ┌──────────────────────────────┐    ┌─────────────┐          │
│   │ What we know                 │    │ What we     │          │
│   │ (Input variables)            │    │ predict     │          │
│   │                              │    │ (Output)    │          │
│   │ • House size                 │    │             │          │
│   │ • Number of rooms   ─────────┼───►│ House Price │          │
│   │ • Location                   │    │             │          │
│   │ • Age of house               │    │             │          │
│   └──────────────────────────────┘    └─────────────┘          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Visual Representation of Data Shape
Python

# Understanding data shapes

import numpy as np

# Features (X) - 2D array
# Shape: (n_samples, n_features)
X = np.array([
    [1500, 3, 10],  # Sample 1: 1500 sqft, 3 rooms, 10 years old
    [2000, 4, 5],   # Sample 2: 2000 sqft, 4 rooms, 5 years old
    [1200, 2, 20],  # Sample 3: 1200 sqft, 2 rooms, 20 years old
    [1800, 3, 8],   # Sample 4: 1800 sqft, 3 rooms, 8 years old
])

# Target (y) - 1D array
# Shape: (n_samples,)
y = np.array([300000, 450000, 200000, 350000])  # Prices

print(f"Features shape: {X.shape}")  # (4, 3) - 4 samples, 3 features
print(f"Target shape: {y.shape}")    # (4,) - 4 samples
text

VISUAL REPRESENTATION:

Features (X):                           Target (y):
┌─────────┬───────┬─────┐              ┌──────────┐
│ SqFt    │ Rooms │ Age │              │  Price   │
├─────────┼───────┼─────┤              ├──────────┤
│  1500   │   3   │  10 │  ──────────► │  300000  │
│  2000   │   4   │   5 │  ──────────► │  450000  │
│  1200   │   2   │  20 │  ──────────► │  200000  │
│  1800   │   3   │   8 │  ──────────► │  350000  │
└─────────┴───────┴─────┘              └──────────┘
     (4, 3)                                (4,)
Built-in Datasets in Scikit-Learn
Scikit-Learn provides several datasets for learning and testing:

Types of Built-in Datasets
text

┌─────────────────────────────────────────────────────────────────┐
│                    BUILT-IN DATASETS                            │
├─────────────────────┬───────────────────────────────────────────┤
│  TOY DATASETS       │  Small, for learning                      │
│  (load_*)           │  • load_iris()         - Classification   │
│                     │  • load_digits()       - Classification   │
│                     │  • load_wine()         - Classification   │
│                     │  • load_breast_cancer()- Classification   │
│                     │  • load_boston()       - Regression       │
│                     │  • load_diabetes()     - Regression       │
├─────────────────────┼───────────────────────────────────────────┤
│  REAL-WORLD         │  Larger, more realistic                   │
│  (fetch_*)          │  • fetch_california_housing()             │
│                     │  • fetch_olivetti_faces()                 │
│                     │  • fetch_20newsgroups()                   │
├─────────────────────┼───────────────────────────────────────────┤
│  GENERATED          │  Create synthetic data                    │
│  (make_*)           │  • make_classification()                  │
│                     │  • make_regression()                      │
│                     │  • make_blobs()                           │
│                     │  • make_moons()                           │
└─────────────────────┴───────────────────────────────────────────┘
Loading and Exploring Datasets
Python

# exploring_datasets.py

from sklearn.datasets import load_iris
import pandas as pd

# Load the famous Iris dataset
iris = load_iris()

# What's inside a dataset object?
print("Keys in dataset:", iris.keys())
# Output: dict_keys(['data', 'target', 'frame', 'target_names', 
#                    'DESCR', 'feature_names', 'filename'])

# Understanding each component
print("\n1. FEATURE NAMES (What we measure):")
print(iris.feature_names)
# ['sepal length (cm)', 'sepal width (cm)', 
#  'petal length (cm)', 'petal width (cm)']

print("\n2. TARGET NAMES (What we predict):")
print(iris.target_names)
# ['setosa', 'versicolor', 'virginica']

print("\n3. DATA SHAPE:")
print(f"Features: {iris.data.shape}")  # (150, 4) - 150 flowers, 4 measurements
print(f"Target: {iris.target.shape}")   # (150,) - 150 labels

print("\n4. FIRST 5 SAMPLES:")
df = pd.DataFrame(iris.data, columns=iris.feature_names)
df['species'] = [iris.target_names[t] for t in iris.target]
print(df.head())

print("\n5. DATASET DESCRIPTION:")
print(iris.DESCR[:500])  # First 500 characters of description
Output:

text

1. FEATURE NAMES (What we measure):
['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)', 'petal width (cm)']

2. TARGET NAMES (What we predict):
['setosa' 'versicolor' 'virginica']

3. DATA SHAPE:
Features: (150, 4)
Target: (150,)

4. FIRST 5 SAMPLES:
   sepal length (cm)  sepal width (cm)  petal length (cm)  petal width (cm) species
0                5.1               3.5                1.4               0.2  setosa
1                4.9               3.0                1.4               0.2  setosa
2                4.7               3.2                1.3               0.2  setosa
3                4.6               3.1                1.5               0.2  setosa
4                5.0               3.6                1.4               0.2  setosa
Generating Synthetic Data
Python

# generating_synthetic_data.py

from sklearn.datasets import make_classification, make_regression, make_blobs
import matplotlib.pyplot as plt
import numpy as np

# Create a figure with 3 subplots
fig, axes = plt.subplots(1, 3, figsize=(15, 4))

# 1. Classification Dataset
X_class, y_class = make_classification(
    n_samples=200,        # Number of samples
    n_features=2,         # Number of features (2 for visualization)
    n_informative=2,      # Features that actually help prediction
    n_redundant=0,        # Redundant features (combinations of informative)
    n_clusters_per_class=1,
    random_state=42
)
axes[0].scatter(X_class[:, 0], X_class[:, 1], c=y_class, cmap='viridis', alpha=0.6)
axes[0].set_title('Classification Dataset')
axes[0].set_xlabel('Feature 1')
axes[0].set_ylabel('Feature 2')

# 2. Regression Dataset
X_reg, y_reg = make_regression(
    n_samples=200,
    n_features=1,         # 1 feature for simple visualization
    noise=20,             # Add some noise
    random_state=42
)
axes[1].scatter(X_reg, y_reg, alpha=0.6, color='green')
axes[1].set_title('Regression Dataset')
axes[1].set_xlabel('Feature')
axes[1].set_ylabel('Target')

# 3. Clustering Dataset (Blobs)
X_blobs, y_blobs = make_blobs(
    n_samples=200,
    centers=3,            # Number of cluster centers
    cluster_std=1.0,      # Standard deviation of clusters
    random_state=42
)
axes[2].scatter(X_blobs[:, 0], X_blobs[:, 1], c=y_blobs, cmap='plasma', alpha=0.6)
axes[2].set_title('Clustering Dataset (Blobs)')
axes[2].set_xlabel('Feature 1')
axes[2].set_ylabel('Feature 2')

plt.tight_layout()
plt.savefig('synthetic_datasets.png', dpi=150)
plt.show()

print("Shapes:")
print(f"Classification: X={X_class.shape}, y={y_class.shape}")
print(f"Regression: X={X_reg.shape}, y={y_reg.shape}")
print(f"Blobs: X={X_blobs.shape}, y={y_blobs.shape}")
Chapter 4: The Scikit-Learn API Design
The Beauty of Consistent API
This is the most important concept to understand!

Scikit-Learn uses a consistent API across all algorithms. Once you learn the pattern, you can use ANY algorithm!

text

┌─────────────────────────────────────────────────────────────────┐
│                    THE UNIVERSAL PATTERN                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. IMPORT      →  from sklearn.xxx import ModelName           │
│                                                                 │
│   2. CREATE      →  model = ModelName(parameters)               │
│                                                                 │
│   3. FIT         →  model.fit(X_train, y_train)                 │
│                                                                 │
│   4. PREDICT     →  predictions = model.predict(X_test)         │
│                                                                 │
│   5. EVALUATE    →  score = model.score(X_test, y_test)         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
The Same Pattern for EVERY Algorithm
Python

# universal_pattern.py

from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Load data
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# THE SAME PATTERN FOR ALL ALGORITHMS!
# ═══════════════════════════════════════════════════════════════

# Algorithm 1: K-Nearest Neighbors
from sklearn.neighbors import KNeighborsClassifier
knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(X_train, y_train)
print(f"KNN Accuracy: {knn.score(X_test, y_test):.2%}")

# Algorithm 2: Decision Tree
from sklearn.tree import DecisionTreeClassifier
tree = DecisionTreeClassifier(max_depth=3)
tree.fit(X_train, y_train)
print(f"Decision Tree Accuracy: {tree.score(X_test, y_test):.2%}")

# Algorithm 3: Random Forest
from sklearn.ensemble import RandomForestClassifier
forest = RandomForestClassifier(n_estimators=100)
forest.fit(X_train, y_train)
print(f"Random Forest Accuracy: {forest.score(X_test, y_test):.2%}")

# Algorithm 4: Support Vector Machine
from sklearn.svm import SVC
svm = SVC(kernel='rbf')
svm.fit(X_train, y_train)
print(f"SVM Accuracy: {svm.score(X_test, y_test):.2%}")

# Algorithm 5: Logistic Regression
from sklearn.linear_model import LogisticRegression
logreg = LogisticRegression(max_iter=200)
logreg.fit(X_train, y_train)
print(f"Logistic Regression Accuracy: {logreg.score(X_test, y_test):.2%}")
Output:

text

KNN Accuracy: 100.00%
Decision Tree Accuracy: 100.00%
Random Forest Accuracy: 100.00%
SVM Accuracy: 100.00%
Logistic Regression Accuracy: 100.00%
The Three Main Types of Objects
text

┌─────────────────────────────────────────────────────────────────┐
│                    SCIKIT-LEARN OBJECTS                         │
├───────────────┬─────────────────────────────────────────────────┤
│               │                                                 │
│  ESTIMATORS   │  • Can learn from data                         │
│               │  • Have .fit() method                          │
│               │  • Examples: All ML models                     │
│               │                                                 │
├───────────────┼─────────────────────────────────────────────────┤
│               │                                                 │
│  PREDICTORS   │  • Can make predictions                        │
│               │  • Have .predict() method                      │
│               │  • Have .score() method                        │
│               │  • Examples: Classifiers, Regressors           │
│               │                                                 │
├───────────────┼─────────────────────────────────────────────────┤
│               │                                                 │
│  TRANSFORMERS │  • Can transform data                          │
│               │  • Have .transform() method                    │
│               │  • Have .fit_transform() method                │
│               │  • Examples: Scalers, Encoders, PCA            │
│               │                                                 │
└───────────────┴─────────────────────────────────────────────────┘
Understanding Each Type
Python

# understanding_object_types.py

from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.linear_model import LinearRegression
from sklearn.datasets import load_diabetes
import numpy as np

# Load data
X, y = load_diabetes(return_X_y=True)

# ═══════════════════════════════════════════════════════════════
# 1. TRANSFORMER EXAMPLE: StandardScaler
# ═══════════════════════════════════════════════════════════════
print("=" * 60)
print("TRANSFORMER: StandardScaler")
print("=" * 60)

scaler = StandardScaler()

# fit() - Learn the parameters (mean, std) from data
scaler.fit(X)
print(f"Learned mean: {scaler.mean_[:3]}...")  # First 3 means
print(f"Learned std: {scaler.scale_[:3]}...")   # First 3 stds

# transform() - Apply the transformation
X_scaled = scaler.transform(X)
print(f"Original data mean: {X.mean(axis=0)[:3]}")
print(f"Scaled data mean: {X_scaled.mean(axis=0)[:3]}")  # Should be ~0

# fit_transform() - Do both in one step (more efficient)
X_scaled_v2 = scaler.fit_transform(X)

# ═══════════════════════════════════════════════════════════════
# 2. ESTIMATOR + PREDICTOR EXAMPLE: LinearRegression
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("ESTIMATOR + PREDICTOR: LinearRegression")
print("=" * 60)

model = LinearRegression()

# fit() - Learn the model parameters
model.fit(X_scaled, y)
print(f"Learned coefficients: {model.coef_[:3]}...")
print(f"Learned intercept: {model.intercept_:.2f}")

# predict() - Make predictions
predictions = model.predict(X_scaled[:5])
print(f"Predictions for first 5 samples: {predictions}")

# score() - Evaluate the model (R² for regression)
r2_score = model.score(X_scaled, y)
print(f"R² Score: {r2_score:.4f}")
Attributes vs Methods
text

┌─────────────────────────────────────────────────────────────────┐
│                 ATTRIBUTES vs METHODS                           │
├──────────────────────────┬──────────────────────────────────────┤
│  ATTRIBUTES (end with _) │  METHODS (functions)                 │
├──────────────────────────┼──────────────────────────────────────┤
│  • Set AFTER fitting     │  • Actions you can perform           │
│  • Access learned params │  • Call with parentheses ()          │
│                          │                                      │
│  model.coef_             │  model.fit(X, y)                     │
│  model.intercept_        │  model.predict(X)                    │
│  model.feature_importances_│  model.score(X, y)                 │
│  model.classes_          │  model.get_params()                  │
│  model.n_features_in_    │  model.set_params()                  │
└──────────────────────────┴──────────────────────────────────────┘
Python

# attributes_vs_methods.py

from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Load and split data
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=42)

# Create and train model
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# ═══════════════════════════════════════════════════════════════
# METHODS (Actions)
# ═══════════════════════════════════════════════════════════════
print("METHODS:")
print("-" * 40)

# Get parameters
params = rf.get_params()
print(f"Parameters: n_estimators={params['n_estimators']}")

# Make predictions
predictions = rf.predict(X_test[:3])
print(f"Predictions: {predictions}")

# Get probability predictions
probabilities = rf.predict_proba(X_test[:3])
print(f"Probabilities shape: {probabilities.shape}")

# Get score
accuracy = rf.score(X_test, y_test)
print(f"Accuracy: {accuracy:.2%}")

# ═══════════════════════════════════════════════════════════════
# ATTRIBUTES (Learned values - note the underscore at the end!)
# ═══════════════════════════════════════════════════════════════
print("\nATTRIBUTES:")
print("-" * 40)

print(f"Number of features seen during fit: {rf.n_features_in_}")
print(f"Classes learned: {rf.classes_}")
print(f"Number of trees: {rf.n_estimators}")
print(f"Feature importances: {rf.feature_importances_}")
Chapter 5: Data Preprocessing
Why Preprocessing is Critical
text

┌─────────────────────────────────────────────────────────────────┐
│                 WHY PREPROCESS DATA?                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  RAW DATA PROBLEMS:                                             │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Different scales (age: 0-100, income: 0-1,000,000)    │   │
│  │ • Missing values (NaN, empty cells)                     │   │
│  │ • Categorical data (colors, names, categories)          │   │
│  │ • Outliers (extreme values)                             │   │
│  │ • Inconsistent formats                                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│                          ▼                                      │
│                                                                 │
│  AFTER PREPROCESSING:                                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ All features on same scale                            │   │
│  │ ✓ No missing values                                     │   │
│  │ ✓ All numeric data                                      │   │
│  │ ✓ Outliers handled                                      │   │
│  │ ✓ Clean, consistent format                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Feature Scaling
Why Scale Features?
text

WITHOUT SCALING:
┌──────────────────────────────────────────────────────────────┐
│  Feature: Age (years)      →  Range: 0 to 100               │
│  Feature: Income ($)       →  Range: 0 to 1,000,000         │
│  Feature: Height (m)       →  Range: 1.5 to 2.0             │
│                                                              │
│  Problem: Income dominates because of larger numbers!        │
│  The algorithm thinks income is more "important"             │
└──────────────────────────────────────────────────────────────┘

WITH SCALING:
┌──────────────────────────────────────────────────────────────┐
│  Feature: Age (scaled)     →  Range: 0 to 1                 │
│  Feature: Income (scaled)  →  Range: 0 to 1                 │
│  Feature: Height (scaled)  →  Range: 0 to 1                 │
│                                                              │
│  All features equally contribute to the model!               │
└──────────────────────────────────────────────────────────────┘
Types of Scaling
Python

# feature_scaling.py

import numpy as np
import pandas as pd
from sklearn.preprocessing import (
    StandardScaler,
    MinMaxScaler,
    RobustScaler,
    MaxAbsScaler,
    Normalizer
)

# Sample data with different scales
data = np.array([
    [25, 50000, 1.75],
    [30, 60000, 1.80],
    [35, 80000, 1.65],
    [40, 120000, 1.90],
    [22, 35000, 1.70]
])

feature_names = ['Age', 'Income', 'Height']
df_original = pd.DataFrame(data, columns=feature_names)

print("ORIGINAL DATA:")
print(df_original)
print(f"\nOriginal ranges:")
print(f"  Age: {data[:, 0].min()} - {data[:, 0].max()}")
print(f"  Income: {data[:, 1].min()} - {data[:, 1].max()}")
print(f"  Height: {data[:, 2].min()} - {data[:, 2].max()}")

# ═══════════════════════════════════════════════════════════════
# 1. STANDARD SCALER (Z-score normalization)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("1. STANDARD SCALER")
print("   Formula: z = (x - mean) / std")
print("   Result: mean=0, std=1")
print("=" * 60)

standard_scaler = StandardScaler()
data_standard = standard_scaler.fit_transform(data)

print(pd.DataFrame(data_standard, columns=feature_names).round(3))
print(f"\nMean after scaling: {data_standard.mean(axis=0).round(3)}")
print(f"Std after scaling: {data_standard.std(axis=0).round(3)}")

# ═══════════════════════════════════════════════════════════════
# 2. MIN-MAX SCALER
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("2. MIN-MAX SCALER")
print("   Formula: x_scaled = (x - min) / (max - min)")
print("   Result: All values between 0 and 1")
print("=" * 60)

minmax_scaler = MinMaxScaler()
data_minmax = minmax_scaler.fit_transform(data)

print(pd.DataFrame(data_minmax, columns=feature_names).round(3))
print(f"\nMin after scaling: {data_minmax.min(axis=0)}")
print(f"Max after scaling: {data_minmax.max(axis=0)}")

# ═══════════════════════════════════════════════════════════════
# 3. ROBUST SCALER (Resistant to outliers)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("3. ROBUST SCALER")
print("   Formula: x_scaled = (x - median) / IQR")
print("   Best for: Data with outliers")
print("=" * 60)

robust_scaler = RobustScaler()
data_robust = robust_scaler.fit_transform(data)

print(pd.DataFrame(data_robust, columns=feature_names).round(3))
Visual Comparison of Scalers
text

┌─────────────────────────────────────────────────────────────────┐
│                   WHEN TO USE WHICH SCALER?                     │
├─────────────────────┬───────────────────────────────────────────┤
│  StandardScaler     │  • Normal distribution assumed            │
│                     │  • Most common choice                     │
│                     │  • Use with: SVM, Logistic Regression     │
├─────────────────────┼───────────────────────────────────────────┤
│  MinMaxScaler       │  • Need values in [0, 1]                  │
│                     │  • No outliers in data                    │
│                     │  • Use with: Neural Networks, KNN         │
├─────────────────────┼───────────────────────────────────────────┤
│  RobustScaler       │  • Data has outliers                      │
│                     │  • Uses median and IQR                    │
│                     │  • Outlier-resistant                      │
├─────────────────────┼───────────────────────────────────────────┤
│  MaxAbsScaler       │  • Sparse data (many zeros)               │
│                     │  • Keeps zero as zero                     │
│                     │  • Use with: Sparse matrices              │
├─────────────────────┼───────────────────────────────────────────┤
│  Normalizer         │  • Scale each SAMPLE (row)                │
│                     │  • Not each feature                       │
│                     │  • Use with: Text data, TF-IDF            │
└─────────────────────┴───────────────────────────────────────────┘
Handling Missing Values
Python

# handling_missing_values.py

import numpy as np
import pandas as pd
from sklearn.impute import SimpleImputer, KNNImputer

# Create data with missing values
data_with_nan = np.array([
    [25, 50000, 1.75],
    [30, np.nan, 1.80],
    [np.nan, 80000, 1.65],
    [40, 120000, np.nan],
    [22, 35000, 1.70]
])

feature_names = ['Age', 'Income', 'Height']
df = pd.DataFrame(data_with_nan, columns=feature_names)

print("ORIGINAL DATA WITH MISSING VALUES:")
print(df)
print(f"\nMissing values per column:\n{df.isnull().sum()}")

# ═══════════════════════════════════════════════════════════════
# 1. SIMPLE IMPUTER - Mean Strategy
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("1. SIMPLE IMPUTER - Mean Strategy")
print("   Missing values replaced with column mean")
print("=" * 60)

mean_imputer = SimpleImputer(strategy='mean')
data_mean = mean_imputer.fit_transform(data_with_nan)

print(pd.DataFrame(data_mean, columns=feature_names))

# ═══════════════════════════════════════════════════════════════
# 2. SIMPLE IMPUTER - Median Strategy
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("2. SIMPLE IMPUTER - Median Strategy")
print("   Missing values replaced with column median")
print("   Better for data with outliers")
print("=" * 60)

median_imputer = SimpleImputer(strategy='median')
data_median = median_imputer.fit_transform(data_with_nan)

print(pd.DataFrame(data_median, columns=feature_names))

# ═══════════════════════════════════════════════════════════════
# 3. SIMPLE IMPUTER - Most Frequent (Mode)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("3. SIMPLE IMPUTER - Most Frequent")
print("   Good for categorical data")
print("=" * 60)

mode_imputer = SimpleImputer(strategy='most_frequent')
data_mode = mode_imputer.fit_transform(data_with_nan)

print(pd.DataFrame(data_mode, columns=feature_names))

# ═══════════════════════════════════════════════════════════════
# 4. SIMPLE IMPUTER - Constant Value
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("4. SIMPLE IMPUTER - Constant Value")
print("   Replace with a specific value")
print("=" * 60)

const_imputer = SimpleImputer(strategy='constant', fill_value=-999)
data_const = const_imputer.fit_transform(data_with_nan)

print(pd.DataFrame(data_const, columns=feature_names))

# ═══════════════════════════════════════════════════════════════
# 5. KNN IMPUTER (Advanced)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("5. KNN IMPUTER")
print("   Uses K-nearest neighbors to estimate missing values")
print("   More sophisticated but computationally expensive")
print("=" * 60)

knn_imputer = KNNImputer(n_neighbors=2)
data_knn = knn_imputer.fit_transform(data_with_nan)

print(pd.DataFrame(data_knn, columns=feature_names))
Imputation Strategy Guide
text

┌─────────────────────────────────────────────────────────────────┐
│               WHICH IMPUTATION STRATEGY TO USE?                 │
├─────────────────────┬───────────────────────────────────────────┤
│  STRATEGY           │  WHEN TO USE                              │
├─────────────────────┼───────────────────────────────────────────┤
│  mean               │  • Numerical data                         │
│                     │  • Normal distribution                    │
│                     │  • No outliers                            │
├─────────────────────┼───────────────────────────────────────────┤
│  median             │  • Numerical data                         │
│                     │  • Data has outliers                      │
│                     │  • Skewed distribution                    │
├─────────────────────┼───────────────────────────────────────────┤
│  most_frequent      │  • Categorical data                       │
│                     │  • Can also work for numerical            │
├─────────────────────┼───────────────────────────────────────────┤
│  constant           │  • When you want explicit marker          │
│                     │  • For certain algorithms                 │
├─────────────────────┼───────────────────────────────────────────┤
│  KNN Imputer        │  • Complex relationships in data          │
│                     │  • When accuracy is critical              │
│                     │  • Small to medium datasets               │
└─────────────────────┴───────────────────────────────────────────┘
Encoding Categorical Variables
Python

# encoding_categorical.py

import numpy as np
import pandas as pd
from sklearn.preprocessing import (
    LabelEncoder,
    OrdinalEncoder,
    OneHotEncoder
)

# Sample data with categorical variables
data = pd.DataFrame({
    'Color': ['Red', 'Blue', 'Green', 'Blue', 'Red'],
    'Size': ['Small', 'Medium', 'Large', 'Medium', 'Small'],
    'Brand': ['Nike', 'Adidas', 'Puma', 'Nike', 'Adidas'],
    'Price': [100, 150, 120, 130, 90]
})

print("ORIGINAL DATA:")
print(data)

# ═══════════════════════════════════════════════════════════════
# 1. LABEL ENCODER
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("1. LABEL ENCODER")
print("   Converts categories to numbers: 0, 1, 2, ...")
print("   Use for: TARGET variable (y)")
print("   Warning: Implies order (0 < 1 < 2), which may not be true!")
print("=" * 60)

label_encoder = LabelEncoder()
data_label = data.copy()
data_label['Color_encoded'] = label_encoder.fit_transform(data['Color'])

print(data_label[['Color', 'Color_encoded']])
print(f"\nClasses: {label_encoder.classes_}")
print(f"Mapping: {dict(zip(label_encoder.classes_, range(len(label_encoder.classes_))))}")

# ═══════════════════════════════════════════════════════════════
# 2. ORDINAL ENCODER
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("2. ORDINAL ENCODER")
print("   For categories WITH natural order")
print("   Example: Size (Small < Medium < Large)")
print("=" * 60)

# Define the order explicitly
size_order = [['Small', 'Medium', 'Large']]

ordinal_encoder = OrdinalEncoder(categories=size_order)
size_encoded = ordinal_encoder.fit_transform(data[['Size']])

data_ordinal = data.copy()
data_ordinal['Size_encoded'] = size_encoded

print(data_ordinal[['Size', 'Size_encoded']])
print(f"\nCategories with order: {ordinal_encoder.categories_}")

# ═══════════════════════════════════════════════════════════════
# 3. ONE-HOT ENCODER
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("3. ONE-HOT ENCODER")
print("   Creates binary columns for each category")
print("   Use for: Features WITHOUT natural order")
print("   Best for: Most categorical features")
print("=" * 60)

onehot_encoder = OneHotEncoder(sparse_output=False, drop=None)
color_onehot = onehot_encoder.fit_transform(data[['Color']])

# Create column names
onehot_columns = onehot_encoder.get_feature_names_out(['Color'])

data_onehot = pd.DataFrame(color_onehot, columns=onehot_columns)
print(pd.concat([data[['Color']], data_onehot], axis=1))

# ═══════════════════════════════════════════════════════════════
# 4. ONE-HOT ENCODER with drop='first' (Avoid dummy variable trap)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("4. ONE-HOT ENCODER (drop='first')")
print("   Drops first category to avoid multicollinearity")
print("   Recommended for linear models")
print("=" * 60)

onehot_encoder_drop = OneHotEncoder(sparse_output=False, drop='first')
color_onehot_drop = onehot_encoder_drop.fit_transform(data[['Color']])

onehot_columns_drop = onehot_encoder_drop.get_feature_names_out(['Color'])
data_onehot_drop = pd.DataFrame(color_onehot_drop, columns=onehot_columns_drop)

print(pd.concat([data[['Color']], data_onehot_drop], axis=1))
Visual Guide to Encoding
text

┌─────────────────────────────────────────────────────────────────┐
│                   ENCODING DECISION GUIDE                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    Is it the TARGET (y)?                        │
│                            │                                    │
│                 ┌──────────┴──────────┐                        │
│                YES                    NO                        │
│                 │                      │                        │
│                 ▼                      ▼                        │
│          LabelEncoder          Is there natural ORDER?         │
│                                        │                        │
│                             ┌──────────┴──────────┐            │
│                            YES                    NO            │
│                             │                      │            │
│                             ▼                      ▼            │
│                      OrdinalEncoder         OneHotEncoder       │
│                                                                 │
│   Examples:                                                     │
│   ─────────                                                     │
│   • Color (Red, Blue, Green)     → OneHotEncoder (no order)    │
│   • Size (S, M, L, XL)           → OrdinalEncoder (has order)  │
│   • Education (HS, BS, MS, PhD)  → OrdinalEncoder (has order)  │
│   • Country (USA, UK, Japan)     → OneHotEncoder (no order)    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Complete Preprocessing Example
Python

# complete_preprocessing.py

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

# Create realistic dataset
np.random.seed(42)
n_samples = 1000

data = pd.DataFrame({
    'age': np.random.randint(18, 70, n_samples).astype(float),
    'income': np.random.randint(20000, 200000, n_samples).astype(float),
    'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n_samples),
    'city': np.random.choice(['New York', 'Los Angeles', 'Chicago', 'Houston'], n_samples),
    'experience': np.random.randint(0, 40, n_samples).astype(float),
})

# Add some missing values
data.loc[np.random.choice(n_samples, 50), 'age'] = np.nan
data.loc[np.random.choice(n_samples, 30), 'income'] = np.nan

# Create target (whether they will buy a product)
data['will_buy'] = (
    (data['income'].fillna(data['income'].median()) > 80000) & 
    (data['age'].fillna(data['age'].median()) > 30)
).astype(int)

print("DATASET INFO:")
print("=" * 60)
print(data.info())
print("\nFirst 5 rows:")
print(data.head())
print(f"\nMissing values:\n{data.isnull().sum()}")

# Split features and target
X = data.drop('will_buy', axis=1)
y = data['will_buy']

# Split into train and test
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Define column types
numerical_features = ['age', 'income', 'experience']
categorical_features = ['education', 'city']

# ═══════════════════════════════════════════════════════════════
# CREATE PREPROCESSING PIPELINES
# ═══════════════════════════════════════════════════════════════

# Pipeline for numerical features
numerical_pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),  # Handle missing values
    ('scaler', StandardScaler())                     # Scale features
])

# Pipeline for categorical features
categorical_pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),  # Handle missing
    ('encoder', OneHotEncoder(drop='first', sparse_output=False))  # Encode
])

# Combine both pipelines
preprocessor = ColumnTransformer([
    ('numerical', numerical_pipeline, numerical_features),
    ('categorical', categorical_pipeline, categorical_features)
])

# Fit and transform
X_train_processed = preprocessor.fit_transform(X_train)
X_test_processed = preprocessor.transform(X_test)

print("\n" + "=" * 60)
print("PREPROCESSING RESULTS")
print("=" * 60)
print(f"Original shape: {X_train.shape}")
print(f"Processed shape: {X_train_processed.shape}")
print(f"\nProcessed feature names:")

# Get feature names
num_features = numerical_features
cat_features = preprocessor.named_transformers_['categorical']['encoder'].get_feature_names_out(categorical_features)
all_features = list(num_features) + list(cat_features)
print(all_features)

# Show processed data
processed_df = pd.DataFrame(X_train_processed, columns=all_features)
print(f"\nFirst 5 rows of processed data:")
print(processed_df.head())
Chapter 6: Supervised Learning - Regression
What is Regression?
text

┌─────────────────────────────────────────────────────────────────┐
│                    REGRESSION EXPLAINED                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Regression predicts CONTINUOUS numerical values               │
│                                                                 │
│   Examples:                                                     │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ • House price: $150,000, $275,500, $1,200,000           │  │
│   │ • Temperature: 72.5°F, 68.3°F, 85.1°F                   │  │
│   │ • Stock price: $142.50, $143.75, $141.20                │  │
│   │ • Person's age: 25.5, 32.8, 41.2                        │  │
│   │ • Sales amount: $1,234.56, $5,678.90                    │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   NOT Regression (Classification):                              │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ • Will buy: Yes/No                                      │  │
│   │ • Email type: Spam/Not Spam                             │  │
│   │ • Disease: Positive/Negative                            │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Linear Regression
The Concept
text

┌─────────────────────────────────────────────────────────────────┐
│                    LINEAR REGRESSION                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Formula: y = mx + b   (or y = w₁x₁ + w₂x₂ + ... + b)         │
│                                                                 │
│   Where:                                                        │
│   • y = predicted value (target)                                │
│   • x = input feature(s)                                        │
│   • m (or w) = weight/coefficient (slope)                       │
│   • b = bias/intercept                                          │
│                                                                 │
│   Visual:                                                       │
│       y │                    ╱                                  │
│         │                 ╱ ╱                                   │
│         │              ╱  ╱                                     │
│         │           ╱   ╱                                       │
│         │        ╱    ╱                                         │
│         │     ╱     ╱  ← Best fit line minimizes errors         │
│         │  ╱      ╱                                             │
│         │╱      ╱                                               │
│         └──────────────────── x                                 │
│                                                                 │
│   Goal: Find the line that minimizes prediction errors          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Simple Linear Regression (One Feature)
Python

# simple_linear_regression.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# Create simple dataset: House size vs Price
np.random.seed(42)

# Generate data
house_size = np.random.randint(500, 4000, 100).reshape(-1, 1)  # in square feet
noise = np.random.normal(0, 30000, 100)
house_price = 100 * house_size.flatten() + 50000 + noise  # Base formula with noise

print("SIMPLE LINEAR REGRESSION")
print("=" * 60)
print("Predicting house price based on size")
print("=" * 60)

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    house_size, house_price, test_size=0.2, random_state=42
)

# Create and train model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Model parameters
print(f"\nMODEL PARAMETERS:")
print(f"  Coefficient (slope): {model.coef_[0]:.2f}")
print(f"  Intercept: {model.intercept_:.2f}")
print(f"\n  Formula: Price = {model.coef_[0]:.2f} × Size + {model.intercept_:.2f}")

# Evaluation metrics
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, y_pred)

print(f"\nMODEL PERFORMANCE:")
print(f"  Mean Squared Error (MSE): {mse:,.2f}")
print(f"  Root Mean Squared Error (RMSE): ${rmse:,.2f}")
print(f"  R² Score: {r2:.4f} ({r2*100:.2f}% of variance explained)")

# Make predictions for new houses
new_houses = np.array([[1000], [2000], [3000]])
new_predictions = model.predict(new_houses)

print(f"\nPREDICTIONS FOR NEW HOUSES:")
for size, price in zip(new_houses.flatten(), new_predictions):
    print(f"  {size} sq ft → ${price:,.2f}")

# Visualization
plt.figure(figsize=(10, 6))
plt.scatter(X_train, y_train, color='blue', alpha=0.5, label='Training data')
plt.scatter(X_test, y_test, color='green', alpha=0.5, label='Test data')
plt.plot(X_test, y_pred, color='red', linewidth=2, label='Prediction line')
plt.xlabel('House Size (sq ft)')
plt.ylabel('Price ($)')
plt.title('Simple Linear Regression: House Size vs Price')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('linear_regression_simple.png', dpi=150, bbox_inches='tight')
plt.show()
Multiple Linear Regression (Multiple Features)
Python

# multiple_linear_regression.py

import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.preprocessing import StandardScaler

# Create dataset with multiple features
np.random.seed(42)
n_samples = 500

# Generate realistic house data
data = pd.DataFrame({
    'size_sqft': np.random.randint(500, 5000, n_samples),
    'bedrooms': np.random.randint(1, 7, n_samples),
    'bathrooms': np.random.randint(1, 4, n_samples),
    'age_years': np.random.randint(0, 50, n_samples),
    'distance_downtown': np.random.uniform(0.5, 30, n_samples),
    'garage_spaces': np.random.randint(0, 4, n_samples)
})

# Create price based on features (with some noise)
data['price'] = (
    150 * data['size_sqft'] +
    20000 * data['bedrooms'] +
    15000 * data['bathrooms'] -
    1000 * data['age_years'] -
    5000 * data['distance_downtown'] +
    10000 * data['garage_spaces'] +
    50000 +  # base price
    np.random.normal(0, 30000, n_samples)  # noise
)

print("MULTIPLE LINEAR REGRESSION")
print("=" * 60)
print("Predicting house price based on multiple features")
print("=" * 60)

print("\nDataset Overview:")
print(data.describe().round(2))

# Prepare features and target
X = data.drop('price', axis=1)
y = data['price']

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Scale features (important for multiple regression)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train model
model = LinearRegression()
model.fit(X_train_scaled, y_train)

# Predictions
y_pred = model.predict(X_test_scaled)

# Feature importance (coefficients)
print("\nFEATURE IMPORTANCE (Coefficients):")
print("-" * 40)
feature_importance = pd.DataFrame({
    'Feature': X.columns,
    'Coefficient': model.coef_,
    'Abs_Coefficient': np.abs(model.coef_)
}).sort_values('Abs_Coefficient', ascending=False)

for _, row in feature_importance.iterrows():
    direction = "↑" if row['Coefficient'] > 0 else "↓"
    print(f"  {row['Feature']:20s}: {row['Coefficient']:>12,.2f} {direction}")

print(f"\n  Intercept: {model.intercept_:,.2f}")

# Model evaluation
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, y_pred)

print(f"\nMODEL PERFORMANCE:")
print(f"  RMSE: ${rmse:,.2f}")
print(f"  R² Score: {r2:.4f}")

# Predict for a new house
new_house = pd.DataFrame({
    'size_sqft': [2500],
    'bedrooms': [4],
    'bathrooms': [2],
    'age_years': [10],
    'distance_downtown': [5],
    'garage_spaces': [2]
})

new_house_scaled = scaler.transform(new_house)
predicted_price = model.predict(new_house_scaled)[0]

print(f"\nPREDICTION FOR NEW HOUSE:")
print(new_house.to_string(index=False))
print(f"\n  Predicted Price: ${predicted_price:,.2f}")
Polynomial Regression
Python

# polynomial_regression.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score
from sklearn.pipeline import Pipeline

# Create non-linear data
np.random.seed(42)
X = np.linspace(0, 10, 100).reshape(-1, 1)
y = 3 * X.flatten()**2 - 5 * X.flatten() + 10 + np.random.normal(0, 10, 100)

print("POLYNOMIAL REGRESSION")
print("=" * 60)
print("When data has a curved relationship")
print("=" * 60)

# Try different polynomial degrees
degrees = [1, 2, 3, 5]
colors = ['red', 'green', 'blue', 'purple']

plt.figure(figsize=(12, 8))
plt.scatter(X, y, color='gray', alpha=0.5, label='Data points')

results = []

for degree, color in zip(degrees, colors):
    # Create pipeline with polynomial features and linear regression
    model = Pipeline([
        ('poly', PolynomialFeatures(degree=degree)),
        ('linear', LinearRegression())
    ])
    
    # Fit model
    model.fit(X, y)
    
    # Predict
    y_pred = model.predict(X)
    
    # Calculate R² score
    r2 = r2_score(y, y_pred)
    results.append((degree, r2))
    
    # Plot
    X_plot = np.linspace(0, 10, 200).reshape(-1, 1)
    y_plot = model.predict(X_plot)
    plt.plot(X_plot, y_plot, color=color, linewidth=2, 
             label=f'Degree {degree} (R²={r2:.4f})')

plt.xlabel('X')
plt.ylabel('y')
plt.title('Polynomial Regression: Different Degrees')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('polynomial_regression.png', dpi=150, bbox_inches='tight')
plt.show()

print("\nRESULTS:")
print("-" * 30)
for degree, r2 in results:
    print(f"  Degree {degree}: R² = {r2:.4f}")

print("""
┌─────────────────────────────────────────────────────────────────┐
│                 POLYNOMIAL DEGREE GUIDE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Degree 1: Linear (straight line)                              │
│  Degree 2: Quadratic (parabola)                                │
│  Degree 3: Cubic (S-curve possible)                            │
│  Degree 4+: Complex curves                                      │
│                                                                 │
│  WARNING: High degrees can cause OVERFITTING!                   │
│  The model memorizes training data but fails on new data.       │
│                                                                 │
│  RULE OF THUMB: Start low, increase only if needed              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Regularized Regression (Ridge, Lasso, ElasticNet)
The Overfitting Problem
text

┌─────────────────────────────────────────────────────────────────┐
│                    THE OVERFITTING PROBLEM                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  UNDERFITTING          GOOD FIT            OVERFITTING         │
│  (Too simple)          (Just right)        (Too complex)       │
│                                                                 │
│       •  •  •            •  •  •              • • •             │
│     •          •       •──────•            •╱╲╱╲╱╲•            │
│    •    ────    •     • ──────•           •        •           │
│   •              •   •────────•          •          •          │
│                                                                 │
│  High Bias           Low Bias/Variance    High Variance        │
│  High Training Error Low Errors           Low Training Error   │
│  High Test Error     Low Test Error       HIGH Test Error      │
│                                                                 │
│  REGULARIZATION helps prevent overfitting by penalizing        │
│  large coefficients (complex models)                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Comparing Regularization Methods
Python

# regularization_comparison.py

import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression, Ridge, Lasso, ElasticNet
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import r2_score, mean_squared_error
import matplotlib.pyplot as plt

# Create dataset with many features (some irrelevant)
np.random.seed(42)
n_samples = 200
n_features = 20
n_informative = 5  # Only 5 features actually matter

# Create features
X = np.random.randn(n_samples, n_features)

# Create target using only first 5 features
true_coef = np.zeros(n_features)
true_coef[:n_informative] = [3, -2, 1.5, -0.5, 2]  # Only these matter
y = X @ true_coef + np.random.normal(0, 0.5, n_samples)

# Split and scale
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print("REGULARIZATION COMPARISON")
print("=" * 60)
print(f"Dataset: {n_features} features, only {n_informative} are informative")
print("=" * 60)

# Train different models
models = {
    'Linear Regression': LinearRegression(),
    'Ridge (L2)': Ridge(alpha=1.0),
    'Lasso (L1)': Lasso(alpha=0.1),
    'ElasticNet (L1+L2)': ElasticNet(alpha=0.1, l1_ratio=0.5)
}

results = []
coefficients = {}

for name, model in models.items():
    model.fit(X_train_scaled, y_train)
    y_pred = model.predict(X_test_scaled)
    
    r2 = r2_score(y_test, y_pred)
    rmse = np.sqrt(mean_squared_error(y_test, y_pred))
    n_nonzero = np.sum(np.abs(model.coef_) > 0.01)
    
    results.append({
        'Model': name,
        'R² Score': r2,
        'RMSE': rmse,
        'Non-zero Coefficients': n_nonzero
    })
    
    coefficients[name] = model.coef_

# Display results
results_df = pd.DataFrame(results)
print("\nMODEL COMPARISON:")
print(results_df.to_string(index=False))

# Coefficient comparison
print("\nCOEFFICIENT COMPARISON (first 10 features):")
print("-" * 70)
coef_df = pd.DataFrame(coefficients)
coef_df.index = [f'Feature_{i}' for i in range(n_features)]
coef_df['True_Coef'] = true_coef
print(coef_df.head(10).round(3))

print("""
┌─────────────────────────────────────────────────────────────────┐
│              WHEN TO USE WHICH REGULARIZATION?                  │
├─────────────────────┬───────────────────────────────────────────┤
│  Ridge (L2)         │  • Many small/medium effects              │
│                     │  • All features potentially useful        │
│                     │  • Correlated features                    │
│                     │  • Shrinks coefficients but keeps all     │
├─────────────────────┼───────────────────────────────────────────┤
│  Lasso (L1)         │  • Feature selection needed               │
│                     │  • Many irrelevant features               │
│                     │  • Sparse solution desired                │
│                     │  • Sets some coefficients to exactly 0    │
├─────────────────────┼───────────────────────────────────────────┤
│  ElasticNet         │  • Best of both worlds                    │
│                     │  • Correlated features + selection        │
│                     │  • Large datasets with many features      │
│                     │  • Combines L1 and L2 penalties           │
└─────────────────────┴───────────────────────────────────────────┘
""")
Regression Evaluation Metrics
Python

# regression_metrics.py

import numpy as np
from sklearn.metrics import (
    mean_squared_error,
    mean_absolute_error,
    r2_score,
    mean_absolute_percentage_error
)

# Actual vs Predicted values
y_true = np.array([100, 150, 200, 250, 300])
y_pred = np.array([110, 145, 210, 240, 295])

print("REGRESSION EVALUATION METRICS")
print("=" * 60)
print(f"\nActual values:    {y_true}")
print(f"Predicted values: {y_pred}")
print(f"Errors:           {y_pred - y_true}")

# Calculate metrics
mse = mean_squared_error(y_true, y_pred)
rmse = np.sqrt(mse)
mae = mean_absolute_error(y_true, y_pred)
r2 = r2_score(y_true, y_pred)
mape = mean_absolute_percentage_error(y_true, y_pred) * 100

print(f"""
┌─────────────────────────────────────────────────────────────────┐
│                    METRICS EXPLAINED                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. MSE (Mean Squared Error): {mse:.2f}                           │
│     ─────────────────────────                                   │
│     Formula: mean((y_true - y_pred)²)                           │
│     • Penalizes large errors heavily                            │
│     • Units: squared units (hard to interpret)                  │
│                                                                 │
│  2. RMSE (Root Mean Squared Error): {rmse:.2f}                    │
│     ────────────────────────────────                            │
│     Formula: √MSE                                               │
│     • Same units as target                                      │
│     • Most commonly used                                        │
│     • "Average" error magnitude                                 │
│                                                                 │
│  3. MAE (Mean Absolute Error): {mae:.2f}                          │
│     ──────────────────────────                                  │
│     Formula: mean(|y_true - y_pred|)                            │
│     • Robust to outliers                                        │
│     • Easy to interpret                                         │
│                                                                 │
│  4. R² Score (Coefficient of Determination): {r2:.4f}             │
│     ────────────────────────────────────────                    │
│     Formula: 1 - (SS_res / SS_tot)                              │
│     • Range: -∞ to 1 (1 is perfect)                             │
│     • Proportion of variance explained                          │
│     • {r2*100:.2f}% of variance is explained by the model            │
│                                                                 │
│  5. MAPE (Mean Absolute Percentage Error): {mape:.2f}%             │
│     ───────────────────────────────────────                     │
│     Formula: mean(|y_true - y_pred| / y_true) × 100             │
│     • Percentage error                                          │
│     • Easy to communicate to non-technical people               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

print("""
WHICH METRIC TO USE?
──────────────────────────────────────────────────────────────────
• RMSE: Default choice, penalizes large errors
• MAE: When outliers are expected or should be treated equally  
• R²: When you need to explain "how good" the model is
• MAPE: When communicating to business stakeholders
""")
Chapter 7: Supervised Learning - Classification
What is Classification?
text

┌─────────────────────────────────────────────────────────────────┐
│                   CLASSIFICATION EXPLAINED                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Classification predicts CATEGORIES (classes)                  │
│                                                                 │
│   BINARY CLASSIFICATION (2 classes):                            │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ • Email: Spam / Not Spam                                │  │
│   │ • Transaction: Fraud / Legitimate                       │  │
│   │ • Patient: Has Disease / Healthy                        │  │
│   │ • Customer: Will Buy / Won't Buy                        │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   MULTI-CLASS CLASSIFICATION (3+ classes):                      │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ • Animal: Cat / Dog / Bird / Fish                       │  │
│   │ • Sentiment: Positive / Neutral / Negative              │  │
│   │ • Flower: Setosa / Versicolor / Virginica              │  │
│   │ • Digit: 0 / 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
K-Nearest Neighbors (KNN)
The Concept
text

┌─────────────────────────────────────────────────────────────────┐
│                K-NEAREST NEIGHBORS (KNN)                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   "Tell me who your neighbors are, and I'll tell you who you    │
│    are"                                                         │
│                                                                 │
│   Algorithm:                                                    │
│   1. Given a new point, find K nearest neighbors                │
│   2. Look at the class of each neighbor                         │
│   3. Predict the most common class (majority vote)              │
│                                                                 │
│   Visual Example (K=3):                                         │
│                                                                 │
│         ●        ○ = Class A                                    │
│       ○   ●      ● = Class B                                    │
│      ●  ★  ○     ★ = New point to classify                      │
│        ○   ●                                                    │
│                                                                 │
│   3 nearest neighbors: 2 circles (○), 1 square (●)              │
│   Prediction: Class A (○ wins by majority)                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python


# knn_classification.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
import seaborn as sns

Load data
iris = load_iris()
X, y = iris.data, iris.target
feature_names = iris.feature_names
target_names = iris.target_names

print("K-NEAREST NEIGHBORS (KNN) CLASSIFICATION")
print("=" * 60)
print(f"Dataset: Iris")
print(f"Features: {feature_names}")
print(f"Classes: {target_names}")
print(f"Samples: {X.shape[0]}, Features: {X.shape[1]}")

Split data
X_train, X_test, y_train, y_test = train_test_split(
X, y, test_size=0.2, random_state=42, stratify=y
)

Scale features (IMPORTANT for KNN - distance-based algorithm)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

Train KNN model
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train_scaled, y_train)

Predictions
y_pred = knn.predict(X_test_scaled)
y_pred_proba = knn.predict_proba(X_test_scaled)

Results
print(f"\nRESULTS:")
print(f"Accuracy: {accuracy_score(y_test, y_pred):.2%}")

print(f"\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=target_names))

Confusion Matrix
print("Confusion Matrix:")
cm = confusion_matrix(y_test, y_pred)
print(cm)

Predict a new flower
new_flower = np.array([[5.1, 3.5, 1.4, 0.2]]) # Measurements
new_flower_scaled = scaler.transform(new_flower)
prediction = knn.predict(new_flower_scaled)
probabilities = knn.predict_proba(new_flower_scaled)

print(f"\nNEW PREDICTION:")
print(f"Measurements: {new_flower[0]}")
print(f"Predicted Class: {target_names[prediction[0]]}")
print(f"Probabilities: {dict(zip(target_names, probabilities[0].round(3)))}")

Finding optimal K
print("\n" + "=" * 60)
print("FINDING OPTIMAL K VALUE")
print("=" * 60)

k_values = range(1, 31)
train_scores = []
test_scores = []

for k in k_values:
knn = KNeighborsClassifier(n_neighbors=k)
knn.fit(X_train_scaled, y_train)
train_scores.append(knn.score(X_train_scaled, y_train))
test_scores.append(knn.score(X_test_scaled, y_test))

best_k = k_values[np.argmax(test_scores)]
print(f"Best K: {best_k} with accuracy: {max(test_scores):.2%}")

Plot
plt.figure(figsize=(10, 6))
plt.plot(k_values, train_scores, 'b-', label='Training Score')
plt.plot(k_values, test_scores, 'r-', label='Test Score')
plt.axvline(x=best_k, color='green', linestyle='--', label=f'Best K={best_k}')
plt.xlabel('K (Number of Neighbors)')
plt.ylabel('Accuracy')
plt.title('KNN: Finding Optimal K')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('knn_optimal_k.png', dpi=150, bbox_inches='tight')
plt.show()

text


## Decision Trees

### The Concept
┌─────────────────────────────────────────────────────────────────┐
│ DECISION TREES │
├─────────────────────────────────────────────────────────────────┤
│ │
│ A Decision Tree makes decisions by asking questions │
│ │
│ Example: Should I play tennis today? │
│ │
│ [Outlook?] │
│ / | \ │
│ Sunny Overcast Rain │
│ / | \ │
│ [Humidity?] YES [Windy?] │
│ / \ / \ │
│ High Normal Yes No │
│ | | | | │
│ NO YES NO YES │
│ │
│ Key Concepts: │
│ • Root Node: First question (Outlook) │
│ • Internal Nodes: Questions (Humidity, Windy) │
│ • Leaf Nodes: Final decisions (YES, NO) │
│ • Branches: Possible answers │
│ │
│ How it learns: │
│ • Uses "Information Gain" or "Gini Impurity" │
│ • Finds the best feature to split on at each step │
│ • Recursively builds the tree │
│ │
└─────────────────────────────────────────────────────────────────┘

text


```python
# decision_tree_classification.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree, export_text
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report

# Load data
iris = load_iris()
X, y = iris.data, iris.target
feature_names = iris.feature_names
target_names = iris.target_names

print("DECISION TREE CLASSIFICATION")
print("=" * 60)

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Train Decision Tree
tree = DecisionTreeClassifier(
    max_depth=3,           # Maximum depth of tree
    min_samples_split=5,   # Minimum samples to split a node
    min_samples_leaf=2,    # Minimum samples in a leaf
    random_state=42
)
tree.fit(X_train, y_train)

# Predictions
y_pred = tree.predict(X_test)

print(f"Accuracy: {accuracy_score(y_test, y_pred):.2%}")
print(f"\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=target_names))

# Feature Importance
print("\nFEATURE IMPORTANCE:")
print("-" * 40)
importance = tree.feature_importances_
for name, imp in sorted(zip(feature_names, importance), key=lambda x: x[1], reverse=True):
    print(f"  {name:25s}: {imp:.4f} {'█' * int(imp * 50)}")

# Text representation of the tree
print("\nTREE RULES (Text):")
print("-" * 40)
tree_rules = export_text(tree, feature_names=list(feature_names))
print(tree_rules)

# Visual representation
plt.figure(figsize=(20, 10))
plot_tree(
    tree,
    feature_names=feature_names,
    class_names=target_names,
    filled=True,
    rounded=True,
    fontsize=10
)
plt.title('Decision Tree Visualization')
plt.savefig('decision_tree_visual.png', dpi=150, bbox_inches='tight')
plt.show()

# Effect of max_depth on accuracy
print("\n" + "=" * 60)
print("EFFECT OF MAX_DEPTH ON ACCURACY")
print("=" * 60)

depths = range(1, 20)
train_scores = []
test_scores = []

for depth in depths:
    tree = DecisionTreeClassifier(max_depth=depth, random_state=42)
    tree.fit(X_train, y_train)
    train_scores.append(tree.score(X_train, y_train))
    test_scores.append(tree.score(X_test, y_test))

plt.figure(figsize=(10, 6))
plt.plot(depths, train_scores, 'b-o', label='Training Score')
plt.plot(depths, test_scores, 'r-o', label='Test Score')
plt.xlabel('Max Depth')
plt.ylabel('Accuracy')
plt.title('Decision Tree: Effect of Max Depth')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('decision_tree_depth.png', dpi=150, bbox_inches='tight')
plt.show()

print("As depth increases:")
print("  • Training score approaches 100% (overfitting)")
print("  • Test score may decrease (generalization worsens)")
Logistic Regression (for Classification!)
text

┌─────────────────────────────────────────────────────────────────┐
│                   LOGISTIC REGRESSION                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Despite the name, it's for CLASSIFICATION, not regression!    │
│                                                                 │
│   How it works:                                                 │
│   1. Calculate linear combination: z = w₁x₁ + w₂x₂ + ... + b   │
│   2. Apply sigmoid function: P = 1 / (1 + e^(-z))               │
│   3. Convert to class: If P > 0.5 → Class 1, else → Class 0    │
│                                                                 │
│   The Sigmoid Function:                                         │
│                                                                 │
│   P(y=1)                                                        │
│     1 │                    ____________                         │
│       │                 ╱                                       │
│   0.5 │- - - - - - - -╱- - - - - - - - -                        │
│       │             ╱                                           │
│     0 │____________╱                                            │
│       └──────────────────────────────── z                       │
│                   0                                             │
│                                                                 │
│   Outputs probability between 0 and 1                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# logistic_regression.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, f1_score,
    confusion_matrix, classification_report, roc_curve, auc
)
import seaborn as sns

# Load breast cancer dataset (binary classification)
cancer = load_breast_cancer()
X, y = cancer.data, cancer.target
feature_names = cancer.feature_names
target_names = cancer.target_names

print("LOGISTIC REGRESSION")
print("=" * 60)
print(f"Dataset: Breast Cancer Wisconsin")
print(f"Classes: {target_names}")
print(f"Samples: {X.shape[0]}, Features: {X.shape[1]}")
print(f"Class distribution: {np.bincount(y)}")

# Split and scale
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train Logistic Regression
log_reg = LogisticRegression(max_iter=1000, random_state=42)
log_reg.fit(X_train_scaled, y_train)

# Predictions
y_pred = log_reg.predict(X_test_scaled)
y_pred_proba = log_reg.predict_proba(X_test_scaled)[:, 1]

# Evaluation
print(f"\nMODEL PERFORMANCE:")
print(f"  Accuracy:  {accuracy_score(y_test, y_pred):.4f}")
print(f"  Precision: {precision_score(y_test, y_pred):.4f}")
print(f"  Recall:    {recall_score(y_test, y_pred):.4f}")
print(f"  F1 Score:  {f1_score(y_test, y_pred):.4f}")

print(f"\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=target_names))

# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=target_names, yticklabels=target_names)
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix')
plt.savefig('logistic_confusion_matrix.png', dpi=150, bbox_inches='tight')
plt.show()

# ROC Curve
fpr, tpr, thresholds = roc_curve(y_test, y_pred_proba)
roc_auc = auc(fpr, tpr)

plt.figure(figsize=(8, 6))
plt.plot(fpr, tpr, color='blue', lw=2, label=f'ROC curve (AUC = {roc_auc:.4f})')
plt.plot([0, 1], [0, 1], color='gray', linestyle='--', label='Random classifier')
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.legend(loc='lower right')
plt.grid(True, alpha=0.3)
plt.savefig('logistic_roc_curve.png', dpi=150, bbox_inches='tight')
plt.show()

print(f"\nAUC Score: {roc_auc:.4f}")

# Feature Importance (Coefficients)
print("\nTOP 10 MOST IMPORTANT FEATURES:")
print("-" * 50)
importance = np.abs(log_reg.coef_[0])
indices = np.argsort(importance)[::-1][:10]

for i, idx in enumerate(indices):
    coef = log_reg.coef_[0][idx]
    direction = "↑ malignant" if coef > 0 else "↓ benign"
    print(f"  {i+1}. {feature_names[idx]:30s}: {coef:>8.4f} {direction}")
Support Vector Machines (SVM)
text

┌─────────────────────────────────────────────────────────────────┐
│                 SUPPORT VECTOR MACHINES (SVM)                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Goal: Find the BEST line (hyperplane) to separate classes     │
│                                                                 │
│   "Best" = Maximum margin between classes                       │
│                                                                 │
│   Visual:                                                       │
│         ○ ○                                                     │
│        ○ ○ ○                        ● ●                        │
│       ○ ○ ○ ○    |    ← margin →    |    ● ● ●                 │
│        ○ ○ ○     |                  |     ● ●                  │
│         ○ ○      |__________________|      ●                   │
│                  ↑                  ↑                           │
│             Support             Support                         │
│             Vectors             Vectors                         │
│                                                                 │
│   Support Vectors: Points closest to the decision boundary     │
│   Margin: Distance between boundary and support vectors         │
│                                                                 │
│   KERNEL TRICK:                                                 │
│   When data isn't linearly separable, transform to higher       │
│   dimension where it IS separable!                              │
│                                                                 │
│   Common Kernels:                                               │
│   • 'linear': For linearly separable data                       │
│   • 'rbf': Most common, for non-linear (default)               │
│   • 'poly': Polynomial transformation                           │
│   • 'sigmoid': Similar to neural network                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# svm_classification.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.svm import SVC
from sklearn.datasets import make_classification, make_circles
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score, classification_report

print("SUPPORT VECTOR MACHINES (SVM)")
print("=" * 60)

# ═══════════════════════════════════════════════════════════════
# PART 1: LINEAR SVM
# ═══════════════════════════════════════════════════════════════
print("\n1. LINEAR SVM (Linearly Separable Data)")
print("-" * 40)

# Create linearly separable data
X_linear, y_linear = make_classification(
    n_samples=200, n_features=2, n_informative=2,
    n_redundant=0, n_clusters_per_class=1, random_state=42
)

X_train, X_test, y_train, y_test = train_test_split(
    X_linear, y_linear, test_size=0.2, random_state=42
)

# Train linear SVM
svm_linear = SVC(kernel='linear', C=1.0)
svm_linear.fit(X_train, y_train)

print(f"Accuracy: {svm_linear.score(X_test, y_test):.2%}")
print(f"Number of Support Vectors: {svm_linear.n_support_}")

# ═══════════════════════════════════════════════════════════════
# PART 2: NON-LINEAR SVM (RBF Kernel)
# ═══════════════════════════════════════════════════════════════
print("\n2. NON-LINEAR SVM (Non-Linearly Separable Data)")
print("-" * 40)

# Create non-linearly separable data (circles)
X_circles, y_circles = make_circles(n_samples=300, noise=0.1, factor=0.3, random_state=42)

X_train_c, X_test_c, y_train_c, y_test_c = train_test_split(
    X_circles, y_circles, test_size=0.2, random_state=42
)

# Compare different kernels
kernels = ['linear', 'poly', 'rbf', 'sigmoid']
results = {}

fig, axes = plt.subplots(2, 2, figsize=(12, 12))
axes = axes.flatten()

for idx, kernel in enumerate(kernels):
    svm = SVC(kernel=kernel, C=1.0, gamma='scale')
    svm.fit(X_train_c, y_train_c)
    accuracy = svm.score(X_test_c, y_test_c)
    results[kernel] = accuracy
    
    # Create decision boundary plot
    ax = axes[idx]
    
    # Create mesh grid
    h = 0.02
    x_min, x_max = X_circles[:, 0].min() - 0.5, X_circles[:, 0].max() + 0.5
    y_min, y_max = X_circles[:, 1].min() - 0.5, X_circles[:, 1].max() + 0.5
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h), np.arange(y_min, y_max, h))
    
    Z = svm.predict(np.c_[xx.ravel(), yy.ravel()])
    Z = Z.reshape(xx.shape)
    
    ax.contourf(xx, yy, Z, alpha=0.3, cmap='coolwarm')
    ax.scatter(X_circles[:, 0], X_circles[:, 1], c=y_circles, cmap='coolwarm', edgecolors='black')
    ax.set_title(f'{kernel.upper()} Kernel\nAccuracy: {accuracy:.2%}')
    ax.set_xlabel('Feature 1')
    ax.set_ylabel('Feature 2')

plt.tight_layout()
plt.savefig('svm_kernels_comparison.png', dpi=150, bbox_inches='tight')
plt.show()

print("\nKernel Comparison:")
for kernel, acc in results.items():
    print(f"  {kernel:10s}: {acc:.2%}")

# ═══════════════════════════════════════════════════════════════
# SVM PARAMETERS EXPLAINED
# ═══════════════════════════════════════════════════════════════
print("""
┌─────────────────────────────────────────────────────────────────┐
│                   SVM PARAMETERS                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  C (Regularization Parameter):                                  │
│  • Low C (0.1): Wider margin, more misclassifications allowed   │
│                 (underfitting risk)                             │
│  • High C (100): Narrow margin, fewer misclassifications        │
│                 (overfitting risk)                              │
│                                                                 │
│  gamma (RBF Kernel):                                            │
│  • Low gamma: Far points have influence (smoother boundary)     │
│  • High gamma: Only close points matter (complex boundary)      │
│                                                                 │
│  kernel:                                                        │
│  • 'linear': Use when data is linearly separable                │
│  • 'rbf': Default, works well in most cases                     │
│  • 'poly': For polynomial relationships                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Classification Metrics Deep Dive
Python

# classification_metrics.py

import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, f1_score,
    confusion_matrix, classification_report,
    precision_recall_curve, roc_curve, auc
)

# Example predictions (binary classification)
y_true = np.array([1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0])
y_pred = np.array([1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0])
y_prob = np.array([0.9, 0.8, 0.7, 0.4, 0.85, 0.1, 0.2, 0.6, 0.15, 0.25,
                   0.75, 0.35, 0.1, 0.55, 0.9, 0.2, 0.45, 0.1, 0.8, 0.3])

print("CLASSIFICATION METRICS EXPLAINED")
print("=" * 60)

# Confusion Matrix
cm = confusion_matrix(y_true, y_pred)
tn, fp, fn, tp = cm.ravel()

print(f"""
┌─────────────────────────────────────────────────────────────────┐
│                   CONFUSION MATRIX                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                        PREDICTED                                │
│                    Negative    Positive                         │
│                   ┌──────────┬──────────┐                       │
│          Negative │  TN={tn:2d}   │  FP={fp:2d}   │ ← Type I Error      │
│   ACTUAL          ├──────────┼──────────┤   (False Alarm)       │
│          Positive │  FN={fn:2d}   │  TP={tp:2d}   │ ← Type II Error     │
│                   └──────────┴──────────┘   (Missed Detection)  │
│                                                                 │
│   TN = True Negative:  Correctly predicted negative             │
│   TP = True Positive:  Correctly predicted positive             │
│   FP = False Positive: Predicted positive, actually negative    │
│   FN = False Negative: Predicted negative, actually positive    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Calculate metrics
accuracy = accuracy_score(y_true, y_pred)
precision = precision_score(y_true, y_pred)
recall = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)

print(f"""
┌─────────────────────────────────────────────────────────────────┐
│                   METRICS FORMULAS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. ACCURACY = (TP + TN) / (TP + TN + FP + FN)                 │
│     = ({tp} + {tn}) / ({tp} + {tn} + {fp} + {fn}) = {accuracy:.4f}                          │
│     "What % of ALL predictions were correct?"                   │
│     ⚠️  Misleading with imbalanced classes!                     │
│                                                                 │
│  2. PRECISION = TP / (TP + FP)                                  │
│     = {tp} / ({tp} + {fp}) = {precision:.4f}                                       │
│     "Of all POSITIVE predictions, how many were correct?"       │
│     📧 Use when FALSE POSITIVES are costly                      │
│     Example: Spam filter (don't want to miss important email)   │
│                                                                 │
│  3. RECALL (Sensitivity, TPR) = TP / (TP + FN)                  │
│     = {tp} / ({tp} + {fn}) = {recall:.4f}                                       │
│     "Of all ACTUAL positives, how many did we catch?"           │
│     🏥 Use when FALSE NEGATIVES are costly                      │
│     Example: Disease detection (don't want to miss sick patient)│
│                                                                 │
│  4. F1 SCORE = 2 × (Precision × Recall) / (Precision + Recall)  │
│     = 2 × ({precision:.4f} × {recall:.4f}) / ({precision:.4f} + {recall:.4f}) = {f1:.4f}        │
│     "Harmonic mean of Precision and Recall"                     │
│     ⚖️  Use when you need balance between precision and recall  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Visualize Confusion Matrix
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Confusion Matrix Heatmap
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
            xticklabels=['Negative', 'Positive'],
            yticklabels=['Negative', 'Positive'], ax=axes[0])
axes[0].set_xlabel('Predicted')
axes[0].set_ylabel('Actual')
axes[0].set_title('Confusion Matrix')

# Metrics Bar Chart
metrics = {'Accuracy': accuracy, 'Precision': precision, 
           'Recall': recall, 'F1 Score': f1}
bars = axes[1].bar(metrics.keys(), metrics.values(), color=['blue', 'green', 'orange', 'red'])
axes[1].set_ylim(0, 1)
axes[1].set_ylabel('Score')
axes[1].set_title('Classification Metrics')
for bar, value in zip(bars, metrics.values()):
    axes[1].text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.02,
                f'{value:.3f}', ha='center')

plt.tight_layout()
plt.savefig('classification_metrics.png', dpi=150, bbox_inches='tight')
plt.show()

# When to use which metric
print("""
┌─────────────────────────────────────────────────────────────────┐
│              WHEN TO USE WHICH METRIC?                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SCENARIO                           USE                         │
│  ─────────────────────────────────────────────────────────────  │
│  Balanced classes                   Accuracy                    │
│  Imbalanced classes                 F1, Precision, Recall       │
│  Cost of FP > Cost of FN            Precision                   │
│    (Spam filter, Drug approval)                                 │
│  Cost of FN > Cost of FP            Recall                      │
│    (Disease detection, Fraud)                                   │
│  Need balance                       F1 Score                    │
│  Compare models                     ROC-AUC                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Chapter 8: Unsupervised Learning
What is Unsupervised Learning?
text

┌─────────────────────────────────────────────────────────────────┐
│                  UNSUPERVISED LEARNING                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   NO LABELS! The algorithm finds patterns on its own.           │
│                                                                 │
│   SUPERVISED:                UNSUPERVISED:                      │
│   ┌─────────────────┐       ┌─────────────────┐                │
│   │ Data + Labels   │       │ Data ONLY       │                │
│   │ X → y           │       │ X → ?           │                │
│   │                 │       │                 │                │
│   │ "This is a cat" │       │ "Find groups"   │                │
│   │ "This is a dog" │       │ "Find patterns" │                │
│   └─────────────────┘       └─────────────────┘                │
│                                                                 │
│   Main Types:                                                   │
│   1. CLUSTERING: Group similar items together                   │
│   2. DIMENSIONALITY REDUCTION: Reduce number of features        │
│   3. ANOMALY DETECTION: Find unusual data points                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
K-Means Clustering
The Concept
text

┌─────────────────────────────────────────────────────────────────┐
│                    K-MEANS CLUSTERING                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Goal: Divide data into K groups (clusters)                    │
│                                                                 │
│   Algorithm:                                                    │
│   1. Choose K (number of clusters)                              │
│   2. Randomly place K centroids                                 │
│   3. Assign each point to nearest centroid                      │
│   4. Move centroids to center of their assigned points          │
│   5. Repeat steps 3-4 until centroids stop moving               │
│                                                                 │
│   Visual:                                                       │
│                                                                 │
│   Step 1: Random       Step 2: Assign       Step 3: Move        │
│   Centroids            Points               Centroids           │
│                                                                 │
│     ○  ●  ○              ○  ●  ○              ○  ●  ○           │
│    ○ ★   ●  ○          ○ ★   ●  ○          ○  ★  ●  ○          │
│     ○  ●   ●   →        ○  ●   ●    →       ○   ●   ●          │
│      ○    ●  ★           ○    ●  ★            ○   ★  ●          │
│       ○  ●                ○  ●                  ○  ●            │
│                                                                 │
│   ★ = Centroid,  ○● = Data points in different clusters        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# kmeans_clustering.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

print("K-MEANS CLUSTERING")
print("=" * 60)

# Create sample data
X, y_true = make_blobs(
    n_samples=300,
    centers=4,
    cluster_std=0.60,
    random_state=42
)

# Scale data
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Apply K-Means
kmeans = KMeans(n_clusters=4, random_state=42, n_init=10)
y_kmeans = kmeans.fit_predict(X_scaled)

print(f"Number of clusters: {kmeans.n_clusters}")
print(f"Cluster centers:\n{kmeans.cluster_centers_}")
print(f"Inertia (sum of squared distances): {kmeans.inertia_:.2f}")
print(f"Silhouette Score: {silhouette_score(X_scaled, y_kmeans):.4f}")

# Visualize clusters
plt.figure(figsize=(12, 5))

# Before clustering
plt.subplot(1, 2, 1)
plt.scatter(X_scaled[:, 0], X_scaled[:, 1], c='gray', alpha=0.5)
plt.title('Before Clustering')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')

# After clustering
plt.subplot(1, 2, 2)
plt.scatter(X_scaled[:, 0], X_scaled[:, 1], c=y_kmeans, cmap='viridis', alpha=0.6)
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1],
            c='red', marker='X', s=200, edgecolors='black', label='Centroids')
plt.title('After K-Means Clustering')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.legend()

plt.tight_layout()
plt.savefig('kmeans_clustering.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════
# FINDING OPTIMAL K (ELBOW METHOD)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("FINDING OPTIMAL K")
print("=" * 60)

k_range = range(1, 11)
inertias = []
silhouette_scores = []

for k in k_range:
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    kmeans.fit(X_scaled)
    inertias.append(kmeans.inertia_)
    
    if k > 1:  # Silhouette needs at least 2 clusters
        silhouette_scores.append(silhouette_score(X_scaled, kmeans.labels_))
    else:
        silhouette_scores.append(0)

# Plot Elbow and Silhouette
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Elbow Method
axes[0].plot(k_range, inertias, 'bo-', linewidth=2, markersize=8)
axes[0].set_xlabel('Number of Clusters (K)')
axes[0].set_ylabel('Inertia')
axes[0].set_title('Elbow Method')
axes[0].axvline(x=4, color='red', linestyle='--', label='Optimal K=4')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# Silhouette Method
axes[1].plot(k_range, silhouette_scores, 'go-', linewidth=2, markersize=8)
axes[1].set_xlabel('Number of Clusters (K)')
axes[1].set_ylabel('Silhouette Score')
axes[1].set_title('Silhouette Method')
axes[1].axvline(x=4, color='red', linestyle='--', label='Optimal K=4')
axes[1].legend()
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('kmeans_optimal_k.png', dpi=150, bbox_inches='tight')
plt.show()

print("""
┌─────────────────────────────────────────────────────────────────┐
│              CHOOSING THE RIGHT K                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  METHOD 1: ELBOW METHOD                                         │
│  • Plot K vs Inertia (sum of squared distances)                 │
│  • Look for "elbow" where curve bends                           │
│  • Inertia always decreases; find diminishing returns           │
│                                                                 │
│  METHOD 2: SILHOUETTE SCORE                                     │
│  • Measures how similar points are to own cluster               │
│  • Range: -1 to 1 (higher is better)                            │
│  • Choose K with highest silhouette score                       │
│                                                                 │
│  METHOD 3: DOMAIN KNOWLEDGE                                     │
│  • Sometimes you KNOW how many groups exist                     │
│  • Example: Customer segments, product categories               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Hierarchical Clustering
Python

# hierarchical_clustering.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import AgglomerativeClustering
from sklearn.datasets import make_blobs
from scipy.cluster.hierarchy import dendrogram, linkage
from sklearn.metrics import silhouette_score

print("HIERARCHICAL CLUSTERING")
print("=" * 60)

# Create sample data
X, y_true = make_blobs(n_samples=150, centers=4, random_state=42)

# ═══════════════════════════════════════════════════════════════
# DENDROGRAM - Visual representation of hierarchy
# ═══════════════════════════════════════════════════════════════
print("\n1. DENDROGRAM")
print("-" * 40)

plt.figure(figsize=(14, 6))

# Create linkage matrix
linkage_matrix = linkage(X, method='ward')

# Plot dendrogram
dendrogram(linkage_matrix, truncate_mode='lastp', p=30)
plt.title('Hierarchical Clustering Dendrogram')
plt.xlabel('Sample Index or Cluster Size')
plt.ylabel('Distance')
plt.axhline(y=20, color='r', linestyle='--', label='Cut at distance=20')
plt.legend()
plt.savefig('dendrogram.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════
# AGGLOMERATIVE CLUSTERING
# ═══════════════════════════════════════════════════════════════
print("\n2. AGGLOMERATIVE CLUSTERING")
print("-" * 40)

# Compare different linkage methods
linkage_methods = ['ward', 'complete', 'average', 'single']

fig, axes = plt.subplots(2, 2, figsize=(12, 12))
axes = axes.flatten()

for idx, linkage_method in enumerate(linkage_methods):
    agg_clustering = AgglomerativeClustering(
        n_clusters=4,
        linkage=linkage_method
    )
    y_pred = agg_clustering.fit_predict(X)
    
    silhouette = silhouette_score(X, y_pred)
    
    axes[idx].scatter(X[:, 0], X[:, 1], c=y_pred, cmap='viridis', alpha=0.6)
    axes[idx].set_title(f'Linkage: {linkage_method}\nSilhouette: {silhouette:.4f}')
    axes[idx].set_xlabel('Feature 1')
    axes[idx].set_ylabel('Feature 2')

plt.tight_layout()
plt.savefig('hierarchical_linkage_comparison.png', dpi=150, bbox_inches='tight')
plt.show()

print("""
┌─────────────────────────────────────────────────────────────────┐
│                  LINKAGE METHODS                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  WARD:                                                          │
│  • Minimizes variance within clusters                           │
│  • Creates compact, equal-sized clusters                        │
│  • Most commonly used                                           │
│                                                                 │
│  COMPLETE (Maximum):                                            │
│  • Uses maximum distance between clusters                       │
│  • Creates compact clusters                                     │
│  • Sensitive to outliers                                        │
│                                                                 │
│  AVERAGE:                                                       │
│  • Uses average distance between all points                     │
│  • Good balance between single and complete                     │
│                                                                 │
│  SINGLE (Minimum):                                              │
│  • Uses minimum distance between clusters                       │
│  • Can create long, chain-like clusters                         │
│  • Good for non-spherical clusters                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
DBSCAN (Density-Based Clustering)
text

┌─────────────────────────────────────────────────────────────────┐
│                        DBSCAN                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Density-Based Spatial Clustering of Applications with Noise   │
│                                                                 │
│   Advantages over K-Means:                                      │
│   ✓ Doesn't require specifying number of clusters              │
│   ✓ Can find clusters of any shape                             │
│   ✓ Identifies outliers (noise points)                         │
│                                                                 │
│   Key Parameters:                                               │
│   • eps: Maximum distance between neighbors                     │
│   • min_samples: Minimum points to form a cluster               │
│                                                                 │
│   Point Types:                                                  │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ CORE POINT: Has ≥ min_samples within eps radius         │  │
│   │ BORDER POINT: Within eps of a core point                │  │
│   │ NOISE POINT: Neither core nor border (outlier)          │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# dbscan_clustering.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import DBSCAN
from sklearn.datasets import make_moons, make_blobs
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

print("DBSCAN CLUSTERING")
print("=" * 60)

# Create challenging dataset (moons shape)
X, y_true = make_moons(n_samples=300, noise=0.05, random_state=42)

# Scale data
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Compare DBSCAN vs K-Means on non-spherical data
fig, axes = plt.subplots(1, 3, figsize=(15, 4))

# Original data
axes[0].scatter(X_scaled[:, 0], X_scaled[:, 1], c='gray', alpha=0.6)
axes[0].set_title('Original Data (Moon Shape)')
axes[0].set_xlabel('Feature 1')
axes[0].set_ylabel('Feature 2')

# K-Means (fails on non-spherical data)
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=2, random_state=42)
y_kmeans = kmeans.fit_predict(X_scaled)
axes[1].scatter(X_scaled[:, 0], X_scaled[:, 1], c=y_kmeans, cmap='viridis', alpha=0.6)
axes[1].set_title(f'K-Means (Silhouette: {silhouette_score(X_scaled, y_kmeans):.4f})')
axes[1].set_xlabel('Feature 1')
axes[1].set_ylabel('Feature 2')

# DBSCAN (handles non-spherical data well)
dbscan = DBSCAN(eps=0.3, min_samples=5)
y_dbscan = dbscan.fit_predict(X_scaled)

# Count noise points (label = -1)
n_noise = list(y_dbscan).count(-1)
n_clusters = len(set(y_dbscan)) - (1 if -1 in y_dbscan else 0)

axes[2].scatter(X_scaled[:, 0], X_scaled[:, 1], c=y_dbscan, cmap='viridis', alpha=0.6)
axes[2].set_title(f'DBSCAN\nClusters: {n_clusters}, Noise points: {n_noise}')
axes[2].set_xlabel('Feature 1')
axes[2].set_ylabel('Feature 2')

plt.tight_layout()
plt.savefig('dbscan_vs_kmeans.png', dpi=150, bbox_inches='tight')
plt.show()

print(f"DBSCAN Results:")
print(f"  Clusters found: {n_clusters}")
print(f"  Noise points: {n_noise}")

# ═══════════════════════════════════════════════════════════════
# EFFECT OF PARAMETERS
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("EFFECT OF DBSCAN PARAMETERS")
print("=" * 60)

fig, axes = plt.subplots(2, 3, figsize=(15, 10))

eps_values = [0.1, 0.3, 0.5]
min_samples_values = [3, 5]

for i, min_samples in enumerate(min_samples_values):
    for j, eps in enumerate(eps_values):
        dbscan = DBSCAN(eps=eps, min_samples=min_samples)
        y_pred = dbscan.fit_predict(X_scaled)
        
        n_clusters = len(set(y_pred)) - (1 if -1 in y_pred else 0)
        n_noise = list(y_pred).count(-1)
        
        axes[i, j].scatter(X_scaled[:, 0], X_scaled[:, 1], c=y_pred, cmap='viridis', alpha=0.6)
        axes[i, j].set_title(f'eps={eps}, min_samples={min_samples}\nClusters: {n_clusters}, Noise: {n_noise}')

plt.tight_layout()
plt.savefig('dbscan_parameters.png', dpi=150, bbox_inches='tight')
plt.show()
Principal Component Analysis (PCA)
text

┌─────────────────────────────────────────────────────────────────┐
│              PRINCIPAL COMPONENT ANALYSIS (PCA)                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Dimensionality Reduction: Reduce features while keeping       │
│   the most important information                                │
│                                                                 │
│   Why use PCA?                                                  │
│   • Visualization (reduce to 2D/3D for plotting)               │
│   • Speed up training (fewer features)                          │
│   • Remove noise and redundant features                         │
│   • Handle multicollinearity                                    │
│                                                                 │
│   How it works:                                                 │
│   1. Standardize the data                                       │
│   2. Find directions of maximum variance (principal components) │
│   3. Project data onto these directions                         │
│                                                                 │
│   Visual:                                                       │
│        y│    •  •                                               │
│         │  •  •  •    →    PC1: Direction of max variance       │
│         │•  •  •  •                                             │
│         │  •  •  •         PC2: Perpendicular to PC1            │
│         └──────────x                                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# pca_dimensionality_reduction.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA
from sklearn.datasets import load_digits
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
import time

print("PRINCIPAL COMPONENT ANALYSIS (PCA)")
print("=" * 60)

# Load digits dataset (64 features - 8x8 images)
digits = load_digits()
X, y = digits.data, digits.target

print(f"Original data shape: {X.shape}")
print(f"Number of features: {X.shape[1]}")
print(f"Number of classes: {len(np.unique(y))}")

# Standardize
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# ═══════════════════════════════════════════════════════════════
# PCA FOR VISUALIZATION (2D)
# ═══════════════════════════════════════════════════════════════
print("\n1. PCA FOR VISUALIZATION (64D → 2D)")
print("-" * 40)

pca_2d = PCA(n_components=2)
X_pca_2d = pca_2d.fit_transform(X_scaled)

print(f"Reduced shape: {X_pca_2d.shape}")
print(f"Variance explained: {pca_2d.explained_variance_ratio_.sum():.2%}")

plt.figure(figsize=(10, 8))
scatter = plt.scatter(X_pca_2d[:, 0], X_pca_2d[:, 1], 
                      c=y, cmap='tab10', alpha=0.6, s=10)
plt.colorbar(scatter, label='Digit')
plt.xlabel(f'PC1 ({pca_2d.explained_variance_ratio_[0]:.2%} variance)')
plt.ylabel(f'PC2 ({pca_2d.explained_variance_ratio_[1]:.2%} variance)')
plt.title('Digits Dataset Visualized with PCA (64D → 2D)')
plt.savefig('pca_visualization.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════
# FINDING OPTIMAL NUMBER OF COMPONENTS
# ═══════════════════════════════════════════════════════════════
print("\n2. FINDING OPTIMAL NUMBER OF COMPONENTS")
print("-" * 40)

pca_full = PCA()
pca_full.fit(X_scaled)

# Cumulative variance explained
cumulative_variance = np.cumsum(pca_full.explained_variance_ratio_)

plt.figure(figsize=(10, 5))
plt.plot(range(1, len(cumulative_variance) + 1), cumulative_variance, 'b-', linewidth=2)
plt.axhline(y=0.95, color='r', linestyle='--', label='95% variance')
plt.axhline(y=0.99, color='g', linestyle='--', label='99% variance')

# Find number of components for 95% variance
n_95 = np.argmax(cumulative_variance >= 0.95) + 1
n_99 = np.argmax(cumulative_variance >= 0.99) + 1
plt.axvline(x=n_95, color='r', linestyle=':', alpha=0.5)
plt.axvline(x=n_99, color='g', linestyle=':', alpha=0.5)

plt.xlabel('Number of Components')
plt.ylabel('Cumulative Explained Variance')
plt.title('PCA: Cumulative Variance Explained')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('pca_variance_explained.png', dpi=150, bbox_inches='tight')
plt.show()

print(f"Components for 95% variance: {n_95}")
print(f"Components for 99% variance: {n_99}")

# ═══════════════════════════════════════════════════════════════
# PCA FOR SPEEDUP
# ═══════════════════════════════════════════════════════════════
print("\n3. PCA FOR MODEL SPEEDUP")
print("-" * 40)

X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)

# Without PCA
start = time.time()
model_full = LogisticRegression(max_iter=5000)
model_full.fit(X_train, y_train)
time_full = time.time() - start
acc_full = accuracy_score(y_test, model_full.predict(X_test))

# With PCA (95% variance)
pca = PCA(n_components=n_95)
X_train_pca = pca.fit_transform(X_train)
X_test_pca = pca.transform(X_test)

start = time.time()
model_pca = LogisticRegression(max_iter=5000)
model_pca.fit(X_train_pca, y_train)
time_pca = time.time() - start
acc_pca = accuracy_score(y_test, model_pca.predict(X_test_pca))

print(f"\nWithout PCA ({X_train.shape[1]} features):")
print(f"  Accuracy: {acc_full:.4f}")
print(f"  Training time: {time_full:.4f} seconds")

print(f"\nWith PCA ({n_95} features):")
print(f"  Accuracy: {acc_pca:.4f}")
print(f"  Training time: {time_pca:.4f} seconds")
print(f"  Speedup: {time_full/time_pca:.2f}x")
Chapter 9: Model Evaluation & Validation
Train-Test Split
text

┌─────────────────────────────────────────────────────────────────┐
│                    TRAIN-TEST SPLIT                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   WHY SPLIT DATA?                                               │
│   • Training data: Model learns from this                       │
│   • Test data: Evaluate model on UNSEEN data                    │
│   • Prevents overfitting detection                              │
│                                                                 │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                    ALL DATA (100%)                      │  │
│   │ ┌──────────────────────────┐ ┌────────────────────────┐│  │
│   │ │     TRAINING (80%)       │ │      TEST (20%)        ││  │
│   │ │                          │ │                        ││  │
│   │ │  Model learns from this  │ │ Evaluate final model   ││  │
│   │ │                          │ │ NEVER train on this!   ││  │
│   │ └──────────────────────────┘ └────────────────────────┘│  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   IMPORTANT: Test data should NEVER be seen during training    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# train_test_split_demo.py

import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

print("TRAIN-TEST SPLIT")
print("=" * 60)

# Load data
X, y = load_iris(return_X_y=True)
print(f"Total samples: {len(X)}")

# Basic split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, 
    test_size=0.2,      # 20% for testing
    random_state=42     # For reproducibility
)

print(f"\nAfter split:")
print(f"  Training samples: {len(X_train)} ({len(X_train)/len(X):.0%})")
print(f"  Test samples: {len(X_test)} ({len(X_test)/len(X):.0%})")

# Train and evaluate
model = LogisticRegression(max_iter=200)
model.fit(X_train, y_train)

train_acc = model.score(X_train, y_train)
test_acc = model.score(X_test, y_test)

print(f"\nModel Performance:")
print(f"  Training accuracy: {train_acc:.4f}")
print(f"  Test accuracy: {test_acc:.4f}")

# ═══════════════════════════════════════════════════════════════
# STRATIFIED SPLIT (Important for imbalanced data)
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("STRATIFIED SPLIT")
print("=" * 60)

# Check class distribution before split
print(f"\nClass distribution in original data:")
unique, counts = np.unique(y, return_counts=True)
for cls, count in zip(unique, counts):
    print(f"  Class {cls}: {count} ({count/len(y):.1%})")

# Stratified split maintains class proportions
X_train_strat, X_test_strat, y_train_strat, y_test_strat = train_test_split(
    X, y, 
    test_size=0.2,
    random_state=42,
    stratify=y  # This ensures proportional split
)

print(f"\nClass distribution in test set (stratified):")
unique, counts = np.unique(y_test_strat, return_counts=True)
for cls, count in zip(unique, counts):
    print(f"  Class {cls}: {count} ({count/len(y_test_strat):.1%})")
Cross-Validation
text

┌─────────────────────────────────────────────────────────────────┐
│                    CROSS-VALIDATION                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Problem with single train-test split:                         │
│   • Results depend on which samples end up in test set          │
│   • We might get lucky or unlucky with the split                │
│                                                                 │
│   Solution: K-FOLD CROSS-VALIDATION                             │
│   • Split data into K parts (folds)                             │
│   • Train K times, each time using different fold as test       │
│   • Average the results                                         │
│                                                                 │
│   5-Fold Cross-Validation:                                      │
│   ┌─────┬─────┬─────┬─────┬─────┐                              │
│   │FOLD1│FOLD2│FOLD3│FOLD4│FOLD5│                              │
│   ├─────┼─────┼─────┼─────┼─────┤                              │
│   │TEST │TRAIN│TRAIN│TRAIN│TRAIN│ → Score 1                    │
│   │TRAIN│TEST │TRAIN│TRAIN│TRAIN│ → Score 2                    │
│   │TRAIN│TRAIN│TEST │TRAIN│TRAIN│ → Score 3                    │
│   │TRAIN│TRAIN│TRAIN│TEST │TRAIN│ → Score 4                    │
│   │TRAIN│TRAIN│TRAIN│TRAIN│TEST │ → Score 5                    │
│   └─────┴─────┴─────┴─────┴─────┘                              │
│                                                                 │
│   Final Score = Average(Score1, Score2, Score3, Score4, Score5) │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# cross_validation.py

import numpy as np
from sklearn.model_selection import (
    cross_val_score, cross_val_predict,
    KFold, StratifiedKFold, LeaveOneOut
)
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier

print("CROSS-VALIDATION")
print("=" * 60)

# Load data
X, y = load_iris(return_X_y=True)

# ═══════════════════════════════════════════════════════════════
# BASIC CROSS-VALIDATION
# ═══════════════════════════════════════════════════════════════
print("\n1. BASIC K-FOLD CROSS-VALIDATION")
print("-" * 40)

model = LogisticRegression(max_iter=200)

# 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5)

print(f"Fold scores: {scores}")
print(f"Mean accuracy: {scores.mean():.4f}")
print(f"Std deviation: {scores.std():.4f}")
print(f"95% Confidence Interval: {scores.mean():.4f} ± {1.96 * scores.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# STRATIFIED K-FOLD (Maintains class proportions)
# ═══════════════════════════════════════════════════════════════
print("\n2. STRATIFIED K-FOLD (Recommended for classification)")
print("-" * 40)

skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores_strat = cross_val_score(model, X, y, cv=skf)

print(f"Fold scores: {scores_strat}")
print(f"Mean accuracy: {scores_strat.mean():.4f}")
print(f"Std deviation: {scores_strat.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# COMPARING MULTIPLE MODELS
# ═══════════════════════════════════════════════════════════════
print("\n3. COMPARING MODELS WITH CROSS-VALIDATION")
print("-" * 40)

models = {
    'Logistic Regression': LogisticRegression(max_iter=200),
    'Decision Tree': DecisionTreeClassifier(),
    'Random Forest': RandomForestClassifier(n_estimators=100)
}

results = []

for name, model in models.items():
    scores = cross_val_score(model, X, y, cv=5)
    results.append({
        'Model': name,
        'Mean': scores.mean(),
        'Std': scores.std()
    })
    print(f"{name:25s}: {scores.mean():.4f} ± {scores.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# CROSS-VALIDATION WITH DIFFERENT SCORING METRICS
# ═══════════════════════════════════════════════════════════════
print("\n4. DIFFERENT SCORING METRICS")
print("-" * 40)

model = LogisticRegression(max_iter=200)

scoring_metrics = ['accuracy', 'precision_macro', 'recall_macro', 'f1_macro']

for metric in scoring_metrics:
    scores = cross_val_score(model, X, y, cv=5, scoring=metric)
    print(f"{metric:20s}: {scores.mean():.4f} ± {scores.std():.4f}")
Learning Curves
Python

# learning_curves.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import learning_curve
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_digits

print("LEARNING CURVES")
print("=" * 60)

# Load data
X, y = load_digits(return_X_y=True)

# Calculate learning curves
def plot_learning_curve(estimator, title, X, y, ax):
    train_sizes, train_scores, test_scores = learning_curve(
        estimator, X, y, cv=5,
        train_sizes=np.linspace(0.1, 1.0, 10),
        n_jobs=-1
    )
    
    train_mean = np.mean(train_scores, axis=1)
    train_std = np.std(train_scores, axis=1)
    test_mean = np.mean(test_scores, axis=1)
    test_std = np.std(test_scores, axis=1)
    
    ax.plot(train_sizes, train_mean, 'o-', color='blue', label='Training score')
    ax.fill_between(train_sizes, train_mean - train_std, train_mean + train_std, 
                     alpha=0.1, color='blue')
    ax.plot(train_sizes, test_mean, 'o-', color='green', label='Cross-validation score')
    ax.fill_between(train_sizes, test_mean - test_std, test_mean + test_std, 
                     alpha=0.1, color='green')
    
    ax.set_xlabel('Training Size')
    ax.set_ylabel('Score')
    ax.set_title(title)
    ax.legend(loc='lower right')
    ax.grid(True, alpha=0.3)
    ax.set_ylim(0, 1.1)

fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Compare simple vs complex model
plot_learning_curve(
    LogisticRegression(max_iter=1000),
    'Learning Curve: Logistic Regression',
    X, y, axes[0]
)

plot_learning_curve(
    DecisionTreeClassifier(max_depth=None),
    'Learning Curve: Decision Tree (No Depth Limit)',
    X, y, axes[1]
)

plt.tight_layout()
plt.savefig('learning_curves.png', dpi=150, bbox_inches='tight')
plt.show()

print("""
┌─────────────────────────────────────────────────────────────────┐
│              HOW TO READ LEARNING CURVES                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  GOOD FIT:                                                      │
│  • Training and CV scores converge                              │
│  • Both scores are high                                         │
│  • Small gap between curves                                     │
│                                                                 │
│  HIGH BIAS (Underfitting):                                      │
│  • Both scores are low                                          │
│  • Scores converge quickly                                      │
│  • More data won't help much                                    │
│  → Solution: More complex model                                 │
│                                                                 │
│  HIGH VARIANCE (Overfitting):                                   │
│  • Training score is high                                       │
│  • CV score is much lower                                       │
│  • Large gap between curves                                     │
│  → Solution: More data, simpler model, regularization          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Validation Curves
Python

# validation_curves.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import validation_curve
from sklearn.svm import SVC
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_digits

print("VALIDATION CURVES")
print("=" * 60)
print("Validation curves show how a hyperparameter affects performance")

# Load data
X, y = load_digits(return_X_y=True)

# ═══════════════════════════════════════════════════════════════
# VALIDATION CURVE FOR DECISION TREE (max_depth)
# ═══════════════════════════════════════════════════════════════
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Decision Tree - max_depth
param_range = np.arange(1, 21)

train_scores, test_scores = validation_curve(
    DecisionTreeClassifier(), X, y,
    param_name="max_depth",
    param_range=param_range,
    cv=5, n_jobs=-1
)

train_mean = np.mean(train_scores, axis=1)
train_std = np.std(train_scores, axis=1)
test_mean = np.mean(test_scores, axis=1)
test_std = np.std(test_scores, axis=1)

axes[0].plot(param_range, train_mean, 'o-', color='blue', label='Training score')
axes[0].fill_between(param_range, train_mean - train_std, train_mean + train_std, alpha=0.1, color='blue')
axes[0].plot(param_range, test_mean, 'o-', color='green', label='Cross-validation score')
axes[0].fill_between(param_range, test_mean - test_std, test_mean + test_std, alpha=0.1, color='green')
axes[0].set_xlabel('max_depth')
axes[0].set_ylabel('Score')
axes[0].set_title('Validation Curve: Decision Tree (max_depth)')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# SVM - gamma
param_range = np.logspace(-6, -1, 10)

train_scores, test_scores = validation_curve(
    SVC(), X, y,
    param_name="gamma",
    param_range=param_range,
    cv=5, n_jobs=-1
)

train_mean = np.mean(train_scores, axis=1)
test_mean = np.mean(test_scores, axis=1)

axes[1].semilogx(param_range, train_mean, 'o-', color='blue', label='Training score')
axes[1].semilogx(param_range, test_mean, 'o-', color='green', label='Cross-validation score')
axes[1].set_xlabel('gamma')
axes[1].set_ylabel('Score')
axes[1].set_title('Validation Curve: SVM (gamma)')
axes[1].legend()
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('validation_curves.png', dpi=150, bbox_inches='tight')
plt.show()

print("""
┌─────────────────────────────────────────────────────────────────┐
│              HOW TO READ VALIDATION CURVES                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  LEFT SIDE (Low parameter value):                               │
│  • Model is too simple (underfitting)                           │
│  • Both scores are low                                          │
│                                                                 │
│  RIGHT SIDE (High parameter value):                             │
│  • Model is too complex (overfitting)                           │
│  • Training score high, CV score low                            │
│                                                                 │
│  OPTIMAL VALUE:                                                 │
│  • Where CV score is highest                                    │
│  • Gap between train and CV is reasonable                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Chapter 10: Hyperparameter Tuning
Grid Search
text

┌─────────────────────────────────────────────────────────────────┐
│                       GRID SEARCH                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Tries EVERY combination of hyperparameters                    │
│                                                                 │
│   Example: SVM with C and gamma                                 │
│                                                                 │
│              gamma                                              │
│           0.01   0.1    1                                       │
│         ┌──────┬──────┬──────┐                                 │
│   C  1  │ Try  │ Try  │ Try  │                                 │
│         ├──────┼──────┼──────┤                                 │
│     10  │ Try  │ Try  │ Try  │  ← 9 combinations total         │
│         ├──────┼──────┼──────┤                                 │
│    100  │ Try  │ Try  │ Try  │                                 │
│         └──────┴──────┴──────┘                                 │
│                                                                 │
│   Pros: Thorough, finds optimal in search space                 │
│   Cons: Slow with many parameters (exponential growth)          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# grid_search.py

import numpy as np
from sklearn.model_selection import GridSearchCV
from sklearn.svm import SVC
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split

print("GRID SEARCH HYPERPARAMETER TUNING")
print("=" * 60)

# Load data
X, y = load_digits(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# GRID SEARCH FOR SVM
# ═══════════════════════════════════════════════════════════════
print("\n1. GRID SEARCH FOR SVM")
print("-" * 40)

# Define parameter grid
param_grid_svm = {
    'C': [0.1, 1, 10, 100],
    'gamma': ['scale', 'auto', 0.01, 0.1],
    'kernel': ['rbf', 'poly']
}

# Calculate total combinations
total_combinations = 1

for param, values in param_grid_svm.items():
total_combinations *= len(values)

print(f"Parameter grid: {param_grid_svm}")
print(f"Total combinations to try: {total_combinations}")
print(f"With 5-fold CV: {total_combinations * 5} model fits")

Create GridSearchCV
grid_search_svm = GridSearchCV(
estimator=SVC(),
param_grid=param_grid_svm,
cv=5, # 5-fold cross-validation
scoring='accuracy', # Metric to optimize
n_jobs=-1, # Use all CPU cores
verbose=1, # Show progress
return_train_score=True # Also calculate training scores
)

Fit grid search
print("\nSearching...")
grid_search_svm.fit(X_train, y_train)

Results
print(f"\nBest Parameters: {grid_search_svm.best_params_}")
print(f"Best CV Score: {grid_search_svm.best_score_:.4f}")
print(f"Test Score: {grid_search_svm.score(X_test, y_test):.4f}")

Show top 5 parameter combinations
import pandas as pd
results_df = pd.DataFrame(grid_search_svm.cv_results_)
results_df = results_df.sort_values('rank_test_score')
print("\nTop 5 Parameter Combinations:")
print(results_df[['params', 'mean_test_score', 'std_test_score', 'rank_test_score']].head())

═══════════════════════════════════════════════════════════════
GRID SEARCH FOR RANDOM FOREST
═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("2. GRID SEARCH FOR RANDOM FOREST")
print("-" * 40)

param_grid_rf = {
'n_estimators': [50, 100, 200],
'max_depth': [None, 10, 20, 30],
'min_samples_split': [2, 5, 10],
'min_samples_leaf': [1, 2, 4]
}

total_rf = 1
for values in param_grid_rf.values():
total_rf *= len(values)
print(f"Total combinations: {total_rf}")

grid_search_rf = GridSearchCV(
estimator=RandomForestClassifier(random_state=42),
param_grid=param_grid_rf,
cv=3, # Using 3-fold to speed up
scoring='accuracy',
n_jobs=-1,
verbose=1
)

print("\nSearching...")
grid_search_rf.fit(X_train, y_train)

print(f"\nBest Parameters: {grid_search_rf.best_params_}")
print(f"Best CV Score: {grid_search_rf.best_score_:.4f}")
print(f"Test Score: {grid_search_rf.score(X_test, y_test):.4f}")

text


## Randomized Search
┌─────────────────────────────────────────────────────────────────┐
│ RANDOMIZED SEARCH │
├─────────────────────────────────────────────────────────────────┤
│ │
│ Instead of trying ALL combinations, randomly sample N times │
│ │
│ Advantages: │
│ ✓ Much faster than Grid Search │
│ ✓ Can search continuous distributions │
│ ✓ Good for initial exploration │
│ ✓ Often finds good solutions quickly │
│ │
│ Visual Comparison: │
│ │
│ Grid Search: Randomized Search: │
│ ● ● ● ● ● ● ● │
│ ● ● ● ● ● ● │
│ ● ● ● ● ● ● ● │
│ ● ● ● ● ● ● ● │
│ ● ● ● ● ● ● ● │
│ │
│ 25 evaluations 10 random samples │
│ (systematic) (can explore more space) │
│ │
└─────────────────────────────────────────────────────────────────┘

text


```python
# randomized_search.py

import numpy as np
from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from scipy.stats import randint, uniform

print("RANDOMIZED SEARCH HYPERPARAMETER TUNING")
print("=" * 60)

# Load data
X, y = load_digits(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Define parameter distributions (not fixed values!)
param_distributions = {
    'n_estimators': randint(50, 500),          # Random integer between 50-500
    'max_depth': [None] + list(range(5, 50)),  # None or 5-49
    'min_samples_split': randint(2, 20),       # Random integer between 2-20
    'min_samples_leaf': randint(1, 10),        # Random integer between 1-10
    'max_features': ['sqrt', 'log2', None],    # Categorical options
    'bootstrap': [True, False]                  # Boolean
}

print("Parameter Distributions:")
for param, dist in param_distributions.items():
    print(f"  {param}: {dist}")

# Create RandomizedSearchCV
random_search = RandomizedSearchCV(
    estimator=RandomForestClassifier(random_state=42),
    param_distributions=param_distributions,
    n_iter=50,              # Number of random combinations to try
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=1,
    random_state=42
)

print(f"\nSearching {50} random combinations...")
random_search.fit(X_train, y_train)

print(f"\nBest Parameters: {random_search.best_params_}")
print(f"Best CV Score: {random_search.best_score_:.4f}")
print(f"Test Score: {random_search.score(X_test, y_test):.4f}")

# Compare search time
import time
from sklearn.model_selection import GridSearchCV

# Small grid for comparison
small_grid = {
    'n_estimators': [100, 200],
    'max_depth': [10, 20, None],
    'min_samples_split': [2, 5]
}

print("\n" + "=" * 60)
print("COMPARISON: Grid Search vs Randomized Search")
print("=" * 60)

# Grid Search
start = time.time()
grid = GridSearchCV(RandomForestClassifier(random_state=42), small_grid, cv=3, n_jobs=-1)
grid.fit(X_train, y_train)
grid_time = time.time() - start

# Random Search (same number of iterations as grid combinations)
n_combinations = 1
for v in small_grid.values():
    n_combinations *= len(v)

start = time.time()
random = RandomizedSearchCV(
    RandomForestClassifier(random_state=42), 
    param_distributions, 
    n_iter=n_combinations, 
    cv=3, 
    n_jobs=-1,
    random_state=42
)
random.fit(X_train, y_train)
random_time = time.time() - start

print(f"\nGrid Search:")
print(f"  Combinations tried: {n_combinations}")
print(f"  Time: {grid_time:.2f} seconds")
print(f"  Best score: {grid.best_score_:.4f}")

print(f"\nRandomized Search:")
print(f"  Combinations tried: {n_combinations}")
print(f"  Time: {random_time:.2f} seconds")
print(f"  Best score: {random.best_score_:.4f}")
Bayesian Optimization (Advanced)
Python

# Note: Requires scikit-optimize: pip install scikit-optimize

# bayesian_optimization.py

try:
    from skopt import BayesSearchCV
    from skopt.space import Integer, Real, Categorical
    SKOPT_AVAILABLE = True
except ImportError:
    SKOPT_AVAILABLE = False
    print("Install scikit-optimize: pip install scikit-optimize")

if SKOPT_AVAILABLE:
    import numpy as np
    from sklearn.ensemble import RandomForestClassifier
    from sklearn.datasets import load_digits
    from sklearn.model_selection import train_test_split
    
    print("BAYESIAN OPTIMIZATION")
    print("=" * 60)
    print("""
    Bayesian Optimization:
    • Uses past results to choose next parameters to try
    • More efficient than random/grid search
    • Builds a model of the objective function
    • Best for expensive evaluations
    """)
    
    X, y = load_digits(return_X_y=True)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    
    # Define search space
    search_space = {
        'n_estimators': Integer(50, 500),
        'max_depth': Integer(3, 50),
        'min_samples_split': Integer(2, 20),
        'min_samples_leaf': Integer(1, 10),
        'max_features': Categorical(['sqrt', 'log2'])
    }
    
    # Bayesian search
    bayes_search = BayesSearchCV(
        estimator=RandomForestClassifier(random_state=42),
        search_spaces=search_space,
        n_iter=30,
        cv=3,
        scoring='accuracy',
        n_jobs=-1,
        random_state=42
    )
    
    print("Searching with Bayesian Optimization...")
    bayes_search.fit(X_train, y_train)
    
    print(f"\nBest Parameters: {bayes_search.best_params_}")
    print(f"Best CV Score: {bayes_search.best_score_:.4f}")
    print(f"Test Score: {bayes_search.score(X_test, y_test):.4f}")

print("""
┌─────────────────────────────────────────────────────────────────┐
│              HYPERPARAMETER TUNING SUMMARY                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  METHOD          WHEN TO USE                                    │
│  ─────────────────────────────────────────────────────────────  │
│  Grid Search     • Few hyperparameters                          │
│                  • Small search space                           │
│                  • Need thorough coverage                       │
│                                                                 │
│  Randomized      • Many hyperparameters                         │
│  Search          • Large search space                           │
│                  • Limited computational budget                 │
│                  • Initial exploration                          │
│                                                                 │
│  Bayesian        • Expensive model evaluations                  │
│  Optimization    • Need efficiency                              │
│                  • Continuous hyperparameters                   │
│                                                                 │
│  RECOMMENDED WORKFLOW:                                          │
│  1. Start with Randomized Search (broad exploration)            │
│  2. Use Grid Search to fine-tune (narrow search space)          │
│  3. Use Bayesian for final optimization (if needed)             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Chapter 11: Feature Engineering & Selection
Feature Engineering
text

┌─────────────────────────────────────────────────────────────────┐
│                   FEATURE ENGINEERING                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   The art of creating NEW features from existing data           │
│                                                                 │
│   "Applied machine learning is basically feature engineering"   │
│                                    - Andrew Ng                  │
│                                                                 │
│   Types:                                                        │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ • Mathematical transformations (log, sqrt, square)      │  │
│   │ • Interactions (feature1 × feature2)                    │  │
│   │ • Binning (continuous → categorical)                    │  │
│   │ • Date/Time features (day, month, hour, weekday)        │  │
│   │ • Text features (word count, TF-IDF)                    │  │
│   │ • Aggregations (mean, sum, count per group)             │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# feature_engineering.py

import numpy as np
import pandas as pd
from sklearn.preprocessing import PolynomialFeatures, KBinsDiscretizer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

print("FEATURE ENGINEERING")
print("=" * 60)

# Sample dataset
np.random.seed(42)
data = pd.DataFrame({
    'age': np.random.randint(18, 70, 100),
    'income': np.random.randint(20000, 150000, 100),
    'years_employed': np.random.randint(0, 40, 100),
    'purchase_date': pd.date_range('2023-01-01', periods=100, freq='D')
})

print("Original Data:")
print(data.head())
print(f"Shape: {data.shape}")

# ═══════════════════════════════════════════════════════════════
# 1. MATHEMATICAL TRANSFORMATIONS
# ═══════════════════════════════════════════════════════════════
print("\n1. MATHEMATICAL TRANSFORMATIONS")
print("-" * 40)

# Log transformation (for skewed data)
data['income_log'] = np.log1p(data['income'])

# Square root transformation
data['age_sqrt'] = np.sqrt(data['age'])

# Square transformation
data['years_employed_squared'] = data['years_employed'] ** 2

print("Added: income_log, age_sqrt, years_employed_squared")

# ═══════════════════════════════════════════════════════════════
# 2. INTERACTION FEATURES
# ═══════════════════════════════════════════════════════════════
print("\n2. INTERACTION FEATURES")
print("-" * 40)

# Ratio features
data['income_per_year_employed'] = data['income'] / (data['years_employed'] + 1)

# Product features
data['age_income_product'] = data['age'] * data['income']

print("Added: income_per_year_employed, age_income_product")

# ═══════════════════════════════════════════════════════════════
# 3. POLYNOMIAL FEATURES
# ═══════════════════════════════════════════════════════════════
print("\n3. POLYNOMIAL FEATURES")
print("-" * 40)

# Select numeric columns for polynomial features
X_numeric = data[['age', 'income']].values[:5]  # First 5 rows for demo

poly = PolynomialFeatures(degree=2, include_bias=False)
X_poly = poly.fit_transform(X_numeric)

print(f"Original features: {['age', 'income']}")
print(f"Polynomial features: {poly.get_feature_names_out(['age', 'income'])}")
print(f"Shape: {X_numeric.shape} → {X_poly.shape}")

# ═══════════════════════════════════════════════════════════════
# 4. BINNING (Discretization)
# ═══════════════════════════════════════════════════════════════
print("\n4. BINNING (DISCRETIZATION)")
print("-" * 40)

# Equal-width binning
data['age_bin_equal'] = pd.cut(data['age'], bins=5, labels=['Very Young', 'Young', 'Middle', 'Senior', 'Elder'])

# Custom binning
data['age_group'] = pd.cut(data['age'], 
                           bins=[0, 25, 35, 50, 65, 100], 
                           labels=['Gen Z', 'Millennial', 'Gen X', 'Boomer', 'Silent'])

# Quantile binning (equal-frequency)
data['income_quartile'] = pd.qcut(data['income'], q=4, labels=['Q1', 'Q2', 'Q3', 'Q4'])

print("Age bins distribution:")
print(data['age_group'].value_counts())

# ═══════════════════════════════════════════════════════════════
# 5. DATE/TIME FEATURES
# ═══════════════════════════════════════════════════════════════
print("\n5. DATE/TIME FEATURES")
print("-" * 40)

data['day_of_week'] = data['purchase_date'].dt.dayofweek
data['month'] = data['purchase_date'].dt.month
data['day_of_month'] = data['purchase_date'].dt.day
data['is_weekend'] = data['day_of_week'].isin([5, 6]).astype(int)
data['quarter'] = data['purchase_date'].dt.quarter

print("Date features extracted:")
print(data[['purchase_date', 'day_of_week', 'month', 'is_weekend', 'quarter']].head())

# Final result
print("\n" + "=" * 60)
print("FINAL ENGINEERED DATASET")
print("=" * 60)
print(f"Original columns: 4")
print(f"Final columns: {len(data.columns)}")
print(f"New features: {len(data.columns) - 4}")
print(f"\nAll columns:\n{list(data.columns)}")
Feature Selection
text

┌─────────────────────────────────────────────────────────────────┐
│                    FEATURE SELECTION                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Choosing the MOST IMPORTANT features from your data           │
│                                                                 │
│   WHY?                                                          │
│   • Reduce overfitting                                          │
│   • Improve accuracy                                            │
│   • Reduce training time                                        │
│   • Better interpretability                                     │
│                                                                 │
│   METHODS:                                                      │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ 1. FILTER: Statistical tests (variance, correlation)   │  │
│   │ 2. WRAPPER: Use model performance (RFE)                 │  │
│   │ 3. EMBEDDED: Built into model (Lasso, Tree importance)  │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# feature_selection.py

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.feature_selection import (
    VarianceThreshold,
    SelectKBest, f_classif, chi2, mutual_info_classif,
    RFE, RFECV,
    SelectFromModel
)
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import Lasso, LogisticRegression
from sklearn.metrics import accuracy_score

print("FEATURE SELECTION")
print("=" * 60)

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
feature_names = data.feature_names

print(f"Original features: {X.shape[1]}")

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Scale for some methods
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# ═══════════════════════════════════════════════════════════════
# 1. FILTER METHODS
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("1. FILTER METHODS")
print("=" * 60)

# 1a. Variance Threshold (remove low variance features)
print("\n1a. VARIANCE THRESHOLD")
print("-" * 40)

var_threshold = VarianceThreshold(threshold=0.1)
X_var = var_threshold.fit_transform(X_train)

print(f"Features before: {X_train.shape[1]}")
print(f"Features after: {X_var.shape[1]}")
print(f"Removed: {X_train.shape[1] - X_var.shape[1]} low-variance features")

# 1b. SelectKBest with ANOVA F-test
print("\n1b. SELECT K BEST (ANOVA F-test)")
print("-" * 40)

selector_kbest = SelectKBest(score_func=f_classif, k=10)
X_kbest = selector_kbest.fit_transform(X_train, y_train)

# Get selected features
selected_mask = selector_kbest.get_support()
selected_features = feature_names[selected_mask]

print(f"Top 10 features by ANOVA F-test:")
scores = selector_kbest.scores_
for name, score in sorted(zip(feature_names, scores), key=lambda x: x[1], reverse=True)[:10]:
    print(f"  {name:30s}: {score:.2f}")

# 1c. Mutual Information
print("\n1c. MUTUAL INFORMATION")
print("-" * 40)

selector_mi = SelectKBest(score_func=mutual_info_classif, k=10)
selector_mi.fit(X_train, y_train)

mi_scores = selector_mi.scores_
print("Top 10 features by Mutual Information:")
for name, score in sorted(zip(feature_names, mi_scores), key=lambda x: x[1], reverse=True)[:10]:
    print(f"  {name:30s}: {score:.4f}")

# ═══════════════════════════════════════════════════════════════
# 2. WRAPPER METHODS
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("2. WRAPPER METHODS")
print("=" * 60)

# Recursive Feature Elimination (RFE)
print("\nRECURSIVE FEATURE ELIMINATION (RFE)")
print("-" * 40)

# Use Random Forest as the estimator
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rfe = RFE(estimator=rf, n_features_to_select=10, step=1)
rfe.fit(X_train, y_train)

print(f"Selected features ({sum(rfe.support_)}):")
for name, selected, rank in sorted(zip(feature_names, rfe.support_, rfe.ranking_), key=lambda x: x[2]):
    if selected:
        print(f"  {name:30s} (Rank: {rank})")

# Evaluate
X_train_rfe = rfe.transform(X_train)
X_test_rfe = rfe.transform(X_test)
rf.fit(X_train_rfe, y_train)
accuracy_rfe = rf.score(X_test_rfe, y_test)
print(f"\nAccuracy with RFE features: {accuracy_rfe:.4f}")

# ═══════════════════════════════════════════════════════════════
# 3. EMBEDDED METHODS
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("3. EMBEDDED METHODS")
print("=" * 60)

# 3a. L1 Regularization (Lasso)
print("\n3a. L1 REGULARIZATION (LASSO)")
print("-" * 40)

lasso = LogisticRegression(penalty='l1', solver='saga', C=0.1, max_iter=5000, random_state=42)
lasso.fit(X_train_scaled, y_train)

# Features with non-zero coefficients
non_zero_mask = lasso.coef_[0] != 0
print(f"Non-zero features: {sum(non_zero_mask)}")
print(f"Zero features: {sum(~non_zero_mask)}")

# 3b. Tree-based Feature Importance
print("\n3b. TREE-BASED FEATURE IMPORTANCE")
print("-" * 40)

rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# Get importance
importances = rf.feature_importances_
indices = np.argsort(importances)[::-1]

print("Top 15 features by importance:")
for i in range(15):
    print(f"  {feature_names[indices[i]]:30s}: {importances[indices[i]]:.4f}")

# Visualize
plt.figure(figsize=(12, 6))
plt.bar(range(15), importances[indices[:15]])
plt.xticks(range(15), feature_names[indices[:15]], rotation=45, ha='right')
plt.xlabel('Feature')
plt.ylabel('Importance')
plt.title('Random Forest Feature Importance (Top 15)')
plt.tight_layout()
plt.savefig('feature_importance.png', dpi=150, bbox_inches='tight')
plt.show()

# SelectFromModel
print("\n3c. SELECT FROM MODEL")
print("-" * 40)

selector_model = SelectFromModel(rf, threshold='mean')
X_train_selected = selector_model.fit_transform(X_train, y_train)
X_test_selected = selector_model.transform(X_test)

print(f"Features selected (above mean importance): {X_train_selected.shape[1]}")

# Compare performance
rf_full = RandomForestClassifier(n_estimators=100, random_state=42)
rf_selected = RandomForestClassifier(n_estimators=100, random_state=42)

rf_full.fit(X_train, y_train)
rf_selected.fit(X_train_selected, y_train)

print(f"\nPerformance Comparison:")
print(f"  All {X_train.shape[1]} features: {rf_full.score(X_test, y_test):.4f}")
print(f"  Selected {X_train_selected.shape[1]} features: {rf_selected.score(X_test_selected, y_test):.4f}")
Chapter 12: Pipelines
Why Pipelines?
text

┌─────────────────────────────────────────────────────────────────┐
│                      WHY PIPELINES?                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   WITHOUT PIPELINE:                                             │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ # Messy, error-prone, hard to maintain                  │  │
│   │ scaler = StandardScaler()                               │  │
│   │ X_train_scaled = scaler.fit_transform(X_train)          │  │
│   │ X_test_scaled = scaler.transform(X_test)  # Easy to forget!│  │
│   │                                                          │  │
│   │ pca = PCA(n_components=10)                               │  │
│   │ X_train_pca = pca.fit_transform(X_train_scaled)          │  │
│   │ X_test_pca = pca.transform(X_test_scaled)                │  │
│   │                                                          │  │
│   │ model = SVC()                                            │  │
│   │ model.fit(X_train_pca, y_train)                          │  │
│   │ predictions = model.predict(X_test_pca)                  │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   WITH PIPELINE:                                                │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │ # Clean, organized, prevents data leakage               │  │
│   │ pipe = Pipeline([                                        │  │
│   │     ('scaler', StandardScaler()),                        │  │
│   │     ('pca', PCA(n_components=10)),                       │  │
│   │     ('model', SVC())                                     │  │
│   │ ])                                                       │  │
│   │                                                          │  │
│   │ pipe.fit(X_train, y_train)                               │  │
│   │ predictions = pipe.predict(X_test)                       │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   BENEFITS:                                                     │
│   ✓ Prevents data leakage                                      │
│   ✓ Cleaner code                                               │
│   ✓ Easy to reproduce                                          │
│   ✓ Works with cross-validation and grid search                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# pipelines_basics.py

import numpy as np
from sklearn.pipeline import Pipeline, make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.svm import SVC
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split, cross_val_score

print("SCIKIT-LEARN PIPELINES")
print("=" * 60)

# Load data
X, y = load_breast_cancer(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# 1. BASIC PIPELINE
# ═══════════════════════════════════════════════════════════════
print("\n1. BASIC PIPELINE")
print("-" * 40)

# Method 1: Using Pipeline with explicit names
pipeline_explicit = Pipeline([
    ('scaler', StandardScaler()),     # Step 1: Scale features
    ('pca', PCA(n_components=10)),    # Step 2: Reduce dimensions
    ('classifier', SVC())              # Step 3: Classify
])

# Method 2: Using make_pipeline (auto-generated names)
pipeline_auto = make_pipeline(
    StandardScaler(),
    PCA(n_components=10),
    SVC()
)

# Fit and predict - just like a single model!
pipeline_explicit.fit(X_train, y_train)
accuracy = pipeline_explicit.score(X_test, y_test)

print(f"Pipeline steps: {[step[0] for step in pipeline_explicit.steps]}")
print(f"Accuracy: {accuracy:.4f}")

# ═══════════════════════════════════════════════════════════════
# 2. ACCESSING PIPELINE COMPONENTS
# ═══════════════════════════════════════════════════════════════
print("\n2. ACCESSING PIPELINE COMPONENTS")
print("-" * 40)

# Access by name
scaler = pipeline_explicit.named_steps['scaler']
print(f"Scaler mean (first 5 features): {scaler.mean_[:5]}")

# Access by index
pca = pipeline_explicit.steps[1][1]
print(f"PCA explained variance ratio: {pca.explained_variance_ratio_.sum():.4f}")

# Get all parameters
print(f"\nAll parameters: {list(pipeline_explicit.get_params().keys())[:10]}...")

# ═══════════════════════════════════════════════════════════════
# 3. PIPELINE WITH CROSS-VALIDATION
# ═══════════════════════════════════════════════════════════════
print("\n3. PIPELINE WITH CROSS-VALIDATION")
print("-" * 40)

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(n_estimators=100, random_state=42))
])

# Cross-validation with pipeline - no data leakage!
cv_scores = cross_val_score(pipeline, X, y, cv=5)

print(f"CV Scores: {cv_scores}")
print(f"Mean CV Score: {cv_scores.mean():.4f} ± {cv_scores.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# 4. PIPELINE WITH GRID SEARCH
# ═══════════════════════════════════════════════════════════════
print("\n4. PIPELINE WITH GRID SEARCH")
print("-" * 40)

from sklearn.model_selection import GridSearchCV

# Create pipeline
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('pca', PCA()),
    ('classifier', SVC())
])

# Define parameter grid
# Use stepname__parameter format
param_grid = {
    'pca__n_components': [5, 10, 15],
    'classifier__C': [0.1, 1, 10],
    'classifier__kernel': ['rbf', 'linear']
}

# Grid search
grid_search = GridSearchCV(pipeline, param_grid, cv=3, n_jobs=-1, verbose=1)
grid_search.fit(X_train, y_train)

print(f"\nBest parameters: {grid_search.best_params_}")
print(f"Best CV score: {grid_search.best_score_:.4f}")
print(f"Test score: {grid_search.score(X_test, y_test):.4f}")
Column Transformer (for Mixed Data Types)
Python

# column_transformer.py

import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split, cross_val_score

print("COLUMN TRANSFORMER")
print("=" * 60)
print("Handle different preprocessing for different columns")

# Create mixed dataset
np.random.seed(42)
n_samples = 500

data = pd.DataFrame({
    'age': np.random.randint(18, 80, n_samples).astype(float),
    'income': np.random.randint(20000, 200000, n_samples).astype(float),
    'years_experience': np.random.randint(0, 40, n_samples).astype(float),
    'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n_samples),
    'department': np.random.choice(['Sales', 'Engineering', 'Marketing', 'HR'], n_samples),
    'performance': np.random.choice(['Low', 'Medium', 'High'], n_samples)
})

# Add some missing values
data.loc[np.random.choice(n_samples, 30), 'age'] = np.nan
data.loc[np.random.choice(n_samples, 20), 'income'] = np.nan

# Create target
data['promoted'] = ((data['income'].fillna(data['income'].median()) > 80000) & 
                    (data['years_experience'] > 5)).astype(int)

print("\nDataset Info:")
print(data.info())
print(f"\nMissing values:\n{data.isnull().sum()}")
print(f"\nSample data:\n{data.head()}")

# Prepare data
X = data.drop('promoted', axis=1)
y = data['promoted']

# Define column types
numeric_features = ['age', 'income', 'years_experience']
categorical_features = ['education', 'department', 'performance']

print(f"\nNumeric features: {numeric_features}")
print(f"Categorical features: {categorical_features}")

# Create preprocessor
preprocessor = ColumnTransformer(
    transformers=[
        ('num', Pipeline([
            ('imputer', SimpleImputer(strategy='median')),
            ('scaler', StandardScaler())
        ]), numeric_features),
        
        ('cat', Pipeline([
            ('imputer', SimpleImputer(strategy='most_frequent')),
            ('encoder', OneHotEncoder(drop='first', sparse_output=False))
        ]), categorical_features)
    ]
)

# Create full pipeline
full_pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', RandomForestClassifier(n_estimators=100, random_state=42))
])

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Fit and evaluate
full_pipeline.fit(X_train, y_train)
accuracy = full_pipeline.score(X_test, y_test)

print(f"\n" + "=" * 60)
print("RESULTS")
print("=" * 60)
print(f"Accuracy: {accuracy:.4f}")

# Cross-validation
cv_scores = cross_val_score(full_pipeline, X, y, cv=5)
print(f"CV Scores: {cv_scores.mean():.4f} ± {cv_scores.std():.4f}")

# Get feature names after transformation
full_pipeline.fit(X_train, y_train)
preprocessor_fitted = full_pipeline.named_steps['preprocessor']

# Numeric feature names stay the same
num_features_out = numeric_features

# Get categorical feature names
cat_encoder = preprocessor_fitted.named_transformers_['cat'].named_steps['encoder']
cat_features_out = cat_encoder.get_feature_names_out(categorical_features)

all_features = list(num_features_out) + list(cat_features_out)
print(f"\nFeatures after preprocessing ({len(all_features)}):")
print(all_features)
Complete Pipeline Example
Python

# complete_pipeline_example.py

import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler, OneHotEncoder, FunctionTransformer
from sklearn.impute import SimpleImputer
from sklearn.feature_selection import SelectKBest, f_classif
from sklearn.decomposition import PCA
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split, GridSearchCV, cross_val_score
import joblib

print("COMPLETE PIPELINE EXAMPLE")
print("=" * 60)

# Create realistic dataset
np.random.seed(42)
n_samples = 1000

data = pd.DataFrame({
    # Numeric features
    'age': np.random.randint(18, 80, n_samples).astype(float),
    'income': np.random.exponential(50000, n_samples),
    'credit_score': np.random.randint(300, 850, n_samples),
    'years_customer': np.random.randint(0, 30, n_samples),
    'num_products': np.random.randint(1, 10, n_samples),
    
    # Categorical features
    'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n_samples),
    'employment': np.random.choice(['Full-time', 'Part-time', 'Self-employed', 'Unemployed'], n_samples),
    'marital_status': np.random.choice(['Single', 'Married', 'Divorced'], n_samples),
})

# Add missing values
for col in ['age', 'income', 'credit_score']:
    data.loc[np.random.choice(n_samples, 50), col] = np.nan

# Create target
data['will_churn'] = (
    (data['credit_score'].fillna(600) < 500) |
    (data['years_customer'] < 2) |
    (data['num_products'] < 2)
).astype(int)

print("Dataset shape:", data.shape)
print("Target distribution:", data['will_churn'].value_counts().to_dict())

# Prepare data
X = data.drop('will_churn', axis=1)
y = data['will_churn']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Define columns
numeric_features = ['age', 'income', 'credit_score', 'years_customer', 'num_products']
categorical_features = ['education', 'employment', 'marital_status']

# ═══════════════════════════════════════════════════════════════
# BUILD COMPLETE PIPELINE
# ═══════════════════════════════════════════════════════════════

# Numeric transformer
numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

# Categorical transformer
categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='constant', fill_value='Unknown')),
    ('encoder', OneHotEncoder(drop='first', sparse_output=False, handle_unknown='ignore'))
])

# Preprocessor
preprocessor = ColumnTransformer([
    ('numeric', numeric_transformer, numeric_features),
    ('categorical', categorical_transformer, categorical_features)
])

# Complete pipeline with feature selection
pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('feature_selection', SelectKBest(f_classif, k='all')),  # Will tune k
    ('classifier', RandomForestClassifier(random_state=42))
])

print("\nPipeline structure:")
print(pipeline)

# ═══════════════════════════════════════════════════════════════
# HYPERPARAMETER TUNING
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("HYPERPARAMETER TUNING")
print("=" * 60)

# Parameter grid
param_grid = {
    'feature_selection__k': [5, 10, 'all'],
    'classifier__n_estimators': [50, 100],
    'classifier__max_depth': [5, 10, None],
    'classifier__min_samples_split': [2, 5]
}

# Grid search
grid_search = GridSearchCV(
    pipeline,
    param_grid,
    cv=5,
    scoring='f1',
    n_jobs=-1,
    verbose=1
)

print("Searching best parameters...")
grid_search.fit(X_train, y_train)

print(f"\nBest parameters: {grid_search.best_params_}")
print(f"Best CV F1 score: {grid_search.best_score_:.4f}")

# Evaluate on test set
best_pipeline = grid_search.best_estimator_
test_score = best_pipeline.score(X_test, y_test)

from sklearn.metrics import classification_report, confusion_matrix

y_pred = best_pipeline.predict(X_test)

print(f"\nTest Accuracy: {test_score:.4f}")
print(f"\nClassification Report:")
print(classification_report(y_test, y_pred))

# ═══════════════════════════════════════════════════════════════
# SAVE AND LOAD PIPELINE
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("SAVING AND LOADING PIPELINE")
print("=" * 60)

# Save
joblib.dump(best_pipeline, 'churn_prediction_pipeline.joblib')
print("Pipeline saved to 'churn_prediction_pipeline.joblib'")

# Load
loaded_pipeline = joblib.load('churn_prediction_pipeline.joblib')
print("Pipeline loaded successfully!")

# Verify it works
loaded_score = loaded_pipeline.score(X_test, y_test)
print(f"Loaded pipeline accuracy: {loaded_score:.4f}")

# Make predictions on new data
new_customer = pd.DataFrame({
    'age': [35],
    'income': [75000],
    'credit_score': [720],
    'years_customer': [5],
    'num_products': [3],
    'education': ['Bachelor'],
    'employment': ['Full-time'],
    'marital_status': ['Married']
})

prediction = loaded_pipeline.predict(new_customer)
probability = loaded_pipeline.predict_proba(new_customer)

print(f"\nNew customer prediction:")
print(f"  Will churn: {'Yes' if prediction[0] == 1 else 'No'}")
print(f"  Churn probability: {probability[0][1]:.2%}")
Chapter 13: Ensemble Methods
What are Ensemble Methods?
text

┌─────────────────────────────────────────────────────────────────┐
│                    ENSEMBLE METHODS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   "The wisdom of the crowd"                                     │
│                                                                 │
│   Combine multiple models to get better predictions than        │
│   any single model alone.                                       │
│                                                                 │
│   Visual:                                                       │
│   ┌─────────┐                                                  │
│   │ Model 1 │──┐                                               │
│   └─────────┘  │                                               │
│   ┌─────────┐  │    ┌──────────────┐    ┌────────────┐        │
│   │ Model 2 │──┼───►│   Combine    │───►│ Final      │        │
│   └─────────┘  │    │  Predictions │    │ Prediction │        │
│   ┌─────────┐  │    └──────────────┘    └────────────┘        │
│   │ Model 3 │──┘                                               │
│   └─────────┘                                                  │
│                                                                 │
│   Types:                                                        │
│   • BAGGING: Train same model on different data subsets         │
│   • BOOSTING: Train models sequentially, fixing errors          │
│   • STACKING: Use another model to combine predictions          │
│   • VOTING: Simple majority vote or average                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Bagging (Bootstrap Aggregating)
Python

# bagging_ensemble.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.ensemble import BaggingClassifier, RandomForestClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split, cross_val_score

print("BAGGING (BOOTSTRAP AGGREGATING)")
print("=" * 60)

print("""
┌─────────────────────────────────────────────────────────────────┐
│                    HOW BAGGING WORKS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Original Data: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]               │
│                                                                 │
│   Bootstrap Sample 1: [2, 3, 3, 5, 7, 7, 8, 9, 9, 10] → Model 1│
│   Bootstrap Sample 2: [1, 1, 2, 4, 5, 6, 7, 8, 9, 10] → Model 2│
│   Bootstrap Sample 3: [1, 3, 4, 4, 5, 6, 6, 8, 9, 10] → Model 3│
│                                                                 │
│   Final Prediction = Vote(Model1, Model2, Model3)               │
│                                                                 │
│   KEY IDEA: Different training data → Different models          │
│             Averaging reduces variance (overfitting)            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Create dataset
X, y = make_classification(
    n_samples=1000, n_features=20, n_informative=15,
    n_redundant=5, random_state=42
)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# 1. SINGLE DECISION TREE vs BAGGING
# ═══════════════════════════════════════════════════════════════
print("\n1. SINGLE TREE vs BAGGING")
print("-" * 40)

# Single Decision Tree
single_tree = DecisionTreeClassifier(random_state=42)
single_scores = cross_val_score(single_tree, X, y, cv=5)

# Bagging of Decision Trees
bagging = BaggingClassifier(
    estimator=DecisionTreeClassifier(),
    n_estimators=50,     # Number of trees
    max_samples=0.8,     # 80% of samples per tree
    max_features=0.8,    # 80% of features per tree
    bootstrap=True,      # Sample with replacement
    random_state=42,
    n_jobs=-1
)
bagging_scores = cross_val_score(bagging, X, y, cv=5)

print(f"Single Decision Tree: {single_scores.mean():.4f} ± {single_scores.std():.4f}")
print(f"Bagging (50 trees):   {bagging_scores.mean():.4f} ± {bagging_scores.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# 2. RANDOM FOREST (Bagging + Random Feature Selection)
# ═══════════════════════════════════════════════════════════════
print("\n2. RANDOM FOREST")
print("-" * 40)

print("""
Random Forest = Bagging + Random Feature Subset at each split
• Each tree uses bootstrap sample of data
• At each split, considers random subset of features
• More diverse trees → Better ensemble
""")

rf = RandomForestClassifier(
    n_estimators=100,
    max_depth=None,
    min_samples_split=2,
    max_features='sqrt',  # sqrt(n_features) at each split
    bootstrap=True,
    oob_score=True,        # Out-of-bag score
    random_state=42,
    n_jobs=-1
)

rf.fit(X_train, y_train)

print(f"Training accuracy: {rf.score(X_train, y_train):.4f}")
print(f"Test accuracy: {rf.score(X_test, y_test):.4f}")
print(f"OOB Score: {rf.oob_score_:.4f}")

# Effect of number of trees
print("\n3. EFFECT OF NUMBER OF TREES")
print("-" * 40)

n_estimators_range = [1, 5, 10, 25, 50, 100, 200]
train_scores = []
test_scores = []

for n in n_estimators_range:
    rf = RandomForestClassifier(n_estimators=n, random_state=42, n_jobs=-1)
    rf.fit(X_train, y_train)
    train_scores.append(rf.score(X_train, y_train))
    test_scores.append(rf.score(X_test, y_test))
    print(f"  n_estimators={n:3d}: Train={train_scores[-1]:.4f}, Test={test_scores[-1]:.4f}")

# Plot
plt.figure(figsize=(10, 6))
plt.plot(n_estimators_range, train_scores, 'b-o', label='Training')
plt.plot(n_estimators_range, test_scores, 'r-o', label='Test')
plt.xlabel('Number of Trees')
plt.ylabel('Accuracy')
plt.title('Random Forest: Effect of Number of Trees')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('random_forest_n_estimators.png', dpi=150, bbox_inches='tight')
plt.show()
Boosting
Python

# boosting_ensemble.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.ensemble import AdaBoostClassifier, GradientBoostingClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split, cross_val_score

print("BOOSTING METHODS")
print("=" * 60)

print("""
┌─────────────────────────────────────────────────────────────────┐
│                    HOW BOOSTING WORKS                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Sequential learning - each model fixes errors of previous     │
│                                                                 │
│   Step 1: Train Model 1 on all data                            │
│           Some samples are misclassified (errors)               │
│                                                                 │
│   Step 2: Train Model 2 with more weight on errors             │
│           Focus on what Model 1 got wrong                       │
│                                                                 │
│   Step 3: Train Model 3 with more weight on remaining errors   │
│           ...and so on                                          │
│                                                                 │
│   Final: Weighted combination of all models                     │
│                                                                 │
│   KEY IDEA: Focus on hard examples                              │
│             Reduces bias (underfitting)                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Create dataset
X, y = make_classification(
    n_samples=1000, n_features=20, n_informative=15,
    n_redundant=5, random_state=42
)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# 1. ADABOOST
# ═══════════════════════════════════════════════════════════════
print("\n1. ADABOOST (Adaptive Boosting)")
print("-" * 40)

adaboost = AdaBoostClassifier(
    estimator=DecisionTreeClassifier(max_depth=1),  # Weak learner (stump)
    n_estimators=50,
    learning_rate=1.0,
    random_state=42
)

adaboost.fit(X_train, y_train)
ada_scores = cross_val_score(adaboost, X, y, cv=5)

print(f"CV Score: {ada_scores.mean():.4f} ± {ada_scores.std():.4f}")
print(f"Test Score: {adaboost.score(X_test, y_test):.4f}")

# ═══════════════════════════════════════════════════════════════
# 2. GRADIENT BOOSTING
# ═══════════════════════════════════════════════════════════════
print("\n2. GRADIENT BOOSTING")
print("-" * 40)

gb = GradientBoostingClassifier(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=3,
    min_samples_split=2,
    min_samples_leaf=1,
    subsample=0.8,        # Use 80% of samples (Stochastic GB)
    random_state=42
)

gb.fit(X_train, y_train)
gb_scores = cross_val_score(gb, X, y, cv=5)

print(f"CV Score: {gb_scores.mean():.4f} ± {gb_scores.std():.4f}")
print(f"Test Score: {gb.score(X_test, y_test):.4f}")

# ═══════════════════════════════════════════════════════════════
# 3. XGBOOST, LIGHTGBM (Modern Boosting Libraries)
# ═══════════════════════════════════════════════════════════════
print("\n3. MODERN BOOSTING LIBRARIES")
print("-" * 40)

try:
    from xgboost import XGBClassifier
    
    xgb = XGBClassifier(
        n_estimators=100,
        learning_rate=0.1,
        max_depth=3,
        random_state=42,
        use_label_encoder=False,
        eval_metric='logloss'
    )
    xgb.fit(X_train, y_train)
    xgb_scores = cross_val_score(xgb, X, y, cv=5)
    print(f"XGBoost CV Score: {xgb_scores.mean():.4f} ± {xgb_scores.std():.4f}")
except ImportError:
    print("XGBoost not installed. Install with: pip install xgboost")

try:
    from lightgbm import LGBMClassifier
    
    lgbm = LGBMClassifier(
        n_estimators=100,
        learning_rate=0.1,
        max_depth=3,
        random_state=42,
        verbose=-1
    )
    lgbm.fit(X_train, y_train)
    lgbm_scores = cross_val_score(lgbm, X, y, cv=5)
    print(f"LightGBM CV Score: {lgbm_scores.mean():.4f} ± {lgbm_scores.std():.4f}")
except ImportError:
    print("LightGBM not installed. Install with: pip install lightgbm")

# ═══════════════════════════════════════════════════════════════
# 4. COMPARISON
# ═══════════════════════════════════════════════════════════════
print("\n4. COMPARISON: BAGGING vs BOOSTING")
print("-" * 40)

from sklearn.ensemble import RandomForestClassifier

models = {
    'Decision Tree': DecisionTreeClassifier(random_state=42),
    'Random Forest': RandomForestClassifier(n_estimators=100, random_state=42),
    'AdaBoost': AdaBoostClassifier(n_estimators=100, random_state=42),
    'Gradient Boosting': GradientBoostingClassifier(n_estimators=100, random_state=42)
}

print(f"{'Model':<25} {'CV Score':<15} {'Std':<10}")
print("-" * 50)

for name, model in models.items():
    scores = cross_val_score(model, X, y, cv=5)
    print(f"{name:<25} {scores.mean():.4f}          ±{scores.std():.4f}")

print("""
┌─────────────────────────────────────────────────────────────────┐
│              BAGGING vs BOOSTING COMPARISON                     │
├─────────────────────┬───────────────────────────────────────────┤
│  BAGGING            │  BOOSTING                                 │
├─────────────────────┼───────────────────────────────────────────┤
│  Parallel training  │  Sequential training                      │
│  Reduces variance   │  Reduces bias                             │
│  Hard to overfit    │  Can overfit                              │
│  Less sensitive     │  Sensitive to noise/outliers              │
│  to parameters      │  Many hyperparameters                     │
│  Example: Random    │  Examples: AdaBoost, GradientBoosting,    │
│  Forest             │  XGBoost, LightGBM, CatBoost              │
└─────────────────────┴───────────────────────────────────────────┘
""")
Voting and Stacking
Python

# voting_stacking.py

import numpy as np
from sklearn.ensemble import (
    VotingClassifier, StackingClassifier,
    RandomForestClassifier, GradientBoostingClassifier
)
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC
from sklearn.neighbors import KNeighborsClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split, cross_val_score

print("VOTING AND STACKING ENSEMBLES")
print("=" * 60)

# Create dataset
X, y = make_classification(
    n_samples=1000, n_features=20, n_informative=15,
    n_redundant=5, random_state=42
)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# 1. VOTING CLASSIFIER
# ═══════════════════════════════════════════════════════════════
print("\n1. VOTING CLASSIFIER")
print("-" * 40)

print("""
HARD VOTING: Each model votes, majority wins
SOFT VOTING: Average predicted probabilities, highest average wins

Example (3 classes, 3 models):
Hard Voting:  Model1=A, Model2=B, Model3=A → Final=A (2 votes)
Soft Voting:  Model1=[0.7,0.2,0.1], Model2=[0.3,0.5,0.2], Model3=[0.6,0.3,0.1]
              Average=[0.53, 0.33, 0.13] → Final=A (highest average)
""")

# Define base models
model1 = LogisticRegression(max_iter=1000)
model2 = RandomForestClassifier(n_estimators=50, random_state=42)
model3 = SVC(probability=True)  # Need probability=True for soft voting
model4 = KNeighborsClassifier(n_neighbors=5)

# Hard Voting
hard_voting = VotingClassifier(
    estimators=[
        ('lr', model1),
        ('rf', model2),
        ('svc', model3),
        ('knn', model4)
    ],
    voting='hard'
)

# Soft Voting
soft_voting = VotingClassifier(
    estimators=[
        ('lr', LogisticRegression(max_iter=1000)),
        ('rf', RandomForestClassifier(n_estimators=50, random_state=42)),
        ('svc', SVC(probability=True)),
        ('knn', KNeighborsClassifier(n_neighbors=5))
    ],
    voting='soft'
)

# Compare
print("\nComparing individual models vs voting:")
models = {
    'Logistic Regression': LogisticRegression(max_iter=1000),
    'Random Forest': RandomForestClassifier(n_estimators=50, random_state=42),
    'SVC': SVC(probability=True),
    'KNN': KNeighborsClassifier(n_neighbors=5),
    'Hard Voting': hard_voting,
    'Soft Voting': soft_voting
}

for name, model in models.items():
    scores = cross_val_score(model, X, y, cv=5)
    print(f"  {name:<25}: {scores.mean():.4f} ± {scores.std():.4f}")

# ═══════════════════════════════════════════════════════════════
# 2. STACKING CLASSIFIER
# ═══════════════════════════════════════════════════════════════
print("\n2. STACKING CLASSIFIER")
print("-" * 40)

print("""
STACKING: Use a meta-model to combine base model predictions

Level 0 (Base Models):
┌─────────┐ ┌─────────┐ ┌─────────┐
│ Model 1 │ │ Model 2 │ │ Model 3 │
└────┬────┘ └────┬────┘ └────┬────┘
     │           │           │
     ▼           ▼           ▼
   pred1       pred2       pred3
     │           │           │
     └─────────┬─────────────┘
               │
Level 1 (Meta-Model):
         ┌────▼────┐
         │Meta-Model│  (learns how to combine predictions)
         └────┬────┘
              │
              ▼
        Final Prediction
""")

# Stacking Classifier
stacking = StackingClassifier(
    estimators=[
        ('rf', RandomForestClassifier(n_estimators=50, random_state=42)),
        ('gb', GradientBoostingClassifier(n_estimators=50, random_state=42)),
        ('knn', KNeighborsClassifier(n_neighbors=5))
    ],
    final_estimator=LogisticRegression(),
    cv=5,  # Use 5-fold CV for generating training data for meta-model
    stack_method='auto',  # Use predict_proba if available
    n_jobs=-1
)

stacking_scores = cross_val_score(stacking, X, y, cv=5)
print(f"\nStacking CV Score: {stacking_scores.mean():.4f} ± {stacking_scores.std():.4f}")

# Fit and evaluate
stacking.fit(X_train, y_train)
print(f"Stacking Test Score: {stacking.score(X_test, y_test):.4f}")

print("""
┌─────────────────────────────────────────────────────────────────┐
│              ENSEMBLE METHOD SELECTION GUIDE                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  VOTING:                                                        │
│  • Quick to implement                                           │
│  • Good when base models are equally good                       │
│  • Use soft voting when models output probabilities             │
│                                                                 │
│  STACKING:                                                      │
│  • More powerful than voting                                    │
│  • Meta-model learns optimal combination                        │
│  • Risk of overfitting (use CV)                                 │
│  • Computationally expensive                                    │
│                                                                 │
│  BAGGING (Random Forest):                                       │
│  • When you have high variance (overfitting)                    │
│  • Parallel training possible                                   │
│                                                                 │
│  BOOSTING:                                                      │
│  • When you have high bias (underfitting)                       │
│  • Often gives best performance                                 │
│  • Requires careful tuning                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Chapter 14: Advanced Topics
Custom Transformers
Python

# custom_transformers.py

import numpy as np
import pandas as pd
from sklearn.base import BaseEstimator, TransformerMixin
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

print("CUSTOM TRANSFORMERS")
print("=" * 60)

print("""
Create your own transformers that work seamlessly with sklearn!

Requirements:
1. Inherit from BaseEstimator and TransformerMixin
2. Implement fit() and transform() methods
3. Return self from fit()
""")

# ═══════════════════════════════════════════════════════════════
# EXAMPLE 1: Simple Custom Transformer
# ═══════════════════════════════════════════════════════════════

class LogTransformer(BaseEstimator, TransformerMixin):
    """Apply log transformation to features."""
    
    def __init__(self, add_constant=1):
        self.add_constant = add_constant
    
    def fit(self, X, y=None):
        # Nothing to learn
        return self
    
    def transform(self, X):
        return np.log(X + self.add_constant)

# ═══════════════════════════════════════════════════════════════
# EXAMPLE 2: Feature Engineering Transformer
# ═══════════════════════════════════════════════════════════════

class FeatureEngineer(BaseEstimator, TransformerMixin):
    """Create interaction and polynomial features."""
    
    def __init__(self, create_interactions=True, create_squares=True):
        self.create_interactions = create_interactions
        self.create_squares = create_squares
    
    def fit(self, X, y=None):
        self.n_features_in_ = X.shape[1]
        return self
    
    def transform(self, X):
        X = np.array(X)
        result = [X]
        
        if self.create_squares:
            result.append(X ** 2)
        
        if self.create_interactions:
            # Create pairwise interactions
            interactions = []
            for i in range(X.shape[1]):
                for j in range(i + 1, X.shape[1]):
                    interactions.append((X[:, i] * X[:, j]).reshape(-1, 1))
            if interactions:
                result.append(np.hstack(interactions))
        
        return np.hstack(result)
    
    def get_feature_names_out(self, input_features=None):
        if input_features is None:
            input_features = [f'x{i}' for i in range(self.n_features_in_)]
        
        names = list(input_features)
        
        if self.create_squares:
            names += [f'{f}^2' for f in input_features]
        
        if self.create_interactions:
            for i, f1 in enumerate(input_features):
                for f2 in input_features[i+1:]:
                    names.append(f'{f1}*{f2}')
        
        return names

# ═══════════════════════════════════════════════════════════════
# EXAMPLE 3: Outlier Handler
# ═══════════════════════════════════════════════════════════════

class OutlierHandler(BaseEstimator, TransformerMixin):
    """Cap outliers using IQR method."""
    
    def __init__(self, factor=1.5):
        self.factor = factor
    
    def fit(self, X, y=None):
        X = np.array(X)
        self.lower_bounds_ = []
        self.upper_bounds_ = []
        
        for col in range(X.shape[1]):
            q1 = np.percentile(X[:, col], 25)
            q3 = np.percentile(X[:, col], 75)
            iqr = q3 - q1
            self.lower_bounds_.append(q1 - self.factor * iqr)
            self.upper_bounds_.append(q3 + self.factor * iqr)
        
        return self
    
    def transform(self, X):
        X = np.array(X).copy()
        for col in range(X.shape[1]):
            X[:, col] = np.clip(X[:, col], 
                                self.lower_bounds_[col], 
                                self.upper_bounds_[col])
        return X

# ═══════════════════════════════════════════════════════════════
# TEST CUSTOM TRANSFORMERS
# ═══════════════════════════════════════════════════════════════
print("\nTesting Custom Transformers:")
print("-" * 40)

# Create sample data
np.random.seed(42)
X = np.random.randn(100, 3)
y = (X[:, 0] + X[:, 1] > 0).astype(int)

# Test FeatureEngineer
fe = FeatureEngineer(create_interactions=True, create_squares=True)
X_transformed = fe.fit_transform(X)
print(f"Original features: {X.shape[1]}")
print(f"After FeatureEngineer: {X_transformed.shape[1]}")
print(f"Feature names: {fe.get_feature_names_out()}")

# Use in pipeline
pipeline = Pipeline([
    ('outlier_handler', OutlierHandler(factor=1.5)),
    ('feature_engineer', FeatureEngineer()),
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(n_estimators=50, random_state=42))
])

scores = cross_val_score(pipeline, X, y, cv=5)
print(f"\nPipeline CV Score: {scores.mean():.4f} ± {scores.std():.4f}")
Custom Estimators
Python

# custom_estimators.py

import numpy as np
from sklearn.base import BaseEstimator, ClassifierMixin
from sklearn.utils.validation import check_X_y, check_array, check_is_fitted
from sklearn.utils.multiclass import unique_labels

print("CUSTOM ESTIMATORS")
print("=" * 60)

class SimpleThresholdClassifier(BaseEstimator, ClassifierMixin):
    """
    A simple classifier that predicts based on feature mean.
    If mean of features > threshold → Class 1, else Class 0
    
    This is a toy example to show how to create custom estimators.
    """
    
    def __init__(self, threshold=0.0):
        self.threshold = threshold
    
    def fit(self, X, y):
        """
        Fit the classifier.
        
        Parameters
        ----------
        X : array-like of shape (n_samples, n_features)
            Training data.
        y : array-like of shape (n_samples,)
            Target values.
        
        Returns
        -------
        self : object
            Fitted estimator.
        """
        # Check that X and y have correct shape
        X, y = check_X_y(X, y)
        
        # Store the classes seen during fit
        self.classes_ = unique_labels(y)
        
        # Store number of features
        self.n_features_in_ = X.shape[1]
        
        # Store training data info (for a real classifier, you'd learn something here)
        self.X_ = X
        self.y_ = y
        
        # Return the classifier
        return self
    
    def predict(self, X):
        """
        Predict class labels for samples in X.
        
        Parameters
        ----------
        X : array-like of shape (n_samples, n_features)
            Samples.
        
        Returns
        -------
        y_pred : array of shape (n_samples,)
            Predicted class labels.
        """
        # Check if fit has been called
        check_is_fitted(self)
        
        # Input validation
        X = check_array(X)
        
        # Predict based on mean > threshold
        feature_means = X.mean(axis=1)
        y_pred = (feature_means > self.threshold).astype(int)
        
        return y_pred
    
    def predict_proba(self, X):
        """
        Predict class probabilities for samples in X.
        """
        check_is_fitted(self)
        X = check_array(X)
        
        # Simple probability based on distance from threshold
        feature_means = X.mean(axis=1)
        
        # Use sigmoid to convert to probabilities
        proba_class1 = 1 / (1 + np.exp(-(feature_means - self.threshold)))
        proba_class0 = 1 - proba_class1
        
        return np.column_stack([proba_class0, proba_class1])


# ═══════════════════════════════════════════════════════════════
# A More Realistic Custom Classifier
#

═══════════════════════════════════════════════════════════════
class WeightedKNNClassifier(BaseEstimator, ClassifierMixin):
"""
Custom K-Nearest Neighbors with feature weighting.
Features can be weighted based on their importance.
"""

text

def __init__(self, n_neighbors=5, weights='uniform', feature_weights=None):
    self.n_neighbors = n_neighbors
    self.weights = weights
    self.feature_weights = feature_weights

def fit(self, X, y):
    X, y = check_X_y(X, y)
    self.classes_ = unique_labels(y)
    self.n_features_in_ = X.shape[1]
    self.X_ = X
    self.y_ = y
    
    # Set feature weights
    if self.feature_weights is None:
        self.feature_weights_ = np.ones(X.shape[1])
    else:
        self.feature_weights_ = np.array(self.feature_weights)
    
    return self

def _weighted_distance(self, x1, x2):
    """Calculate weighted Euclidean distance."""
    diff = (x1 - x2) * self.feature_weights_
    return np.sqrt(np.sum(diff ** 2))

def predict(self, X):
    check_is_fitted(self)
    X = check_array(X)
    
    predictions = []
    
    for x in X:
        # Calculate distances to all training points
        distances = np.array([self._weighted_distance(x, x_train) 
                              for x_train in self.X_])
        
        # Find k nearest neighbors
        k_indices = np.argsort(distances)[:self.n_neighbors]
        k_labels = self.y_[k_indices]
        
        if self.weights == 'distance':
            # Weight by inverse distance
            k_distances = distances[k_indices]
            k_distances[k_distances == 0] = 1e-10  # Avoid division by zero
            weights = 1 / k_distances
            
            # Weighted vote
            class_votes = {}
            for label, weight in zip(k_labels, weights):
                class_votes[label] = class_votes.get(label, 0) + weight
            prediction = max(class_votes, key=class_votes.get)
        else:
            # Uniform voting (majority)
            prediction = np.bincount(k_labels).argmax()
        
        predictions.append(prediction)
    
    return np.array(predictions)
═══════════════════════════════════════════════════════════════
TEST CUSTOM ESTIMATORS
═══════════════════════════════════════════════════════════════
print("\nTesting Custom Estimators:")
print("-" * 40)

from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split, cross_val_score

Create data
X, y = make_classification(n_samples=200, n_features=10, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

Test SimpleThresholdClassifier
print("\n1. SimpleThresholdClassifier:")
stc = SimpleThresholdClassifier(threshold=0.0)
stc.fit(X_train, y_train)
print(f" Accuracy: {stc.score(X_test, y_test):.4f}")

Test WeightedKNNClassifier
print("\n2. WeightedKNNClassifier:")
wknn = WeightedKNNClassifier(n_neighbors=5, weights='distance')
scores = cross_val_score(wknn, X, y, cv=5)
print(f" CV Score: {scores.mean():.4f} ± {scores.std():.4f}")

Use with GridSearchCV
from sklearn.model_selection import GridSearchCV

print("\n3. Custom Estimator with GridSearchCV:")
param_grid = {
'n_neighbors': [3, 5, 7, 9],
'weights': ['uniform', 'distance']
}

grid_search = GridSearchCV(WeightedKNNClassifier(), param_grid, cv=3)
grid_search.fit(X_train, y_train)
print(f" Best params: {grid_search.best_params_}")
print(f" Best score: {grid_search.best_score_:.4f}")

text


## Calibration

```python
# probability_calibration.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.calibration import CalibratedClassifierCV, calibration_curve
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.naive_bayes import GaussianNB
from sklearn.svm import SVC

print("PROBABILITY CALIBRATION")
print("=" * 60)

print("""
┌─────────────────────────────────────────────────────────────────┐
│                    WHY CALIBRATION?                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Not all classifiers output well-calibrated probabilities!     │
│                                                                 │
│   Well-calibrated: If model says 70% probability for class 1,  │
│                    70% of such predictions should actually be   │
│                    class 1.                                     │
│                                                                 │
│   Typically well-calibrated:                                    │
│   • Logistic Regression                                         │
│   • Neural Networks (with proper training)                      │
│                                                                 │
│   Often poorly calibrated:                                      │
│   • Random Forest (tends to give probabilities near 0 or 1)    │
│   • SVM (not designed for probability estimation)               │
│   • Naive Bayes (often extreme probabilities)                   │
│   • Gradient Boosting (can be overconfident)                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Create dataset
X, y = make_classification(
    n_samples=10000, n_features=20, n_informative=10,
    n_redundant=5, random_state=42
)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Models to compare
models = {
    'Logistic Regression': LogisticRegression(max_iter=1000),
    'Naive Bayes': GaussianNB(),
    'Random Forest': RandomForestClassifier(n_estimators=100, random_state=42),
    'SVM': SVC(probability=True),
}

# Plot calibration curves
fig, axes = plt.subplots(2, 2, figsize=(12, 10))
axes = axes.flatten()

for idx, (name, model) in enumerate(models.items()):
    # Fit model
    model.fit(X_train, y_train)
    
    # Get probabilities
    if hasattr(model, 'predict_proba'):
        prob_pos = model.predict_proba(X_test)[:, 1]
    else:
        prob_pos = model.decision_function(X_test)
        prob_pos = (prob_pos - prob_pos.min()) / (prob_pos.max() - prob_pos.min())
    
    # Calculate calibration curve
    fraction_of_positives, mean_predicted_value = calibration_curve(
        y_test, prob_pos, n_bins=10
    )
    
    # Plot
    ax = axes[idx]
    ax.plot([0, 1], [0, 1], 'k--', label='Perfectly calibrated')
    ax.plot(mean_predicted_value, fraction_of_positives, 's-', label=name)
    ax.set_xlabel('Mean Predicted Probability')
    ax.set_ylabel('Fraction of Positives')
    ax.set_title(f'{name}')
    ax.legend(loc='lower right')
    ax.grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('calibration_curves.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════
# CALIBRATING A MODEL
# ═══════════════════════════════════════════════════════════════
print("\nCALIBRATING MODELS")
print("-" * 40)

# Compare uncalibrated vs calibrated Random Forest
rf = RandomForestClassifier(n_estimators=100, random_state=42)

# Calibrate using Platt scaling (sigmoid)
rf_sigmoid = CalibratedClassifierCV(rf, method='sigmoid', cv=5)

# Calibrate using isotonic regression
rf_isotonic = CalibratedClassifierCV(rf, method='isotonic', cv=5)

# Fit all models
rf.fit(X_train, y_train)
rf_sigmoid.fit(X_train, y_train)
rf_isotonic.fit(X_train, y_train)

# Compare calibration
fig, ax = plt.subplots(figsize=(10, 8))

ax.plot([0, 1], [0, 1], 'k--', label='Perfectly calibrated')

for model, name in [(rf, 'RF (uncalibrated)'),
                     (rf_sigmoid, 'RF + Sigmoid'),
                     (rf_isotonic, 'RF + Isotonic')]:
    prob_pos = model.predict_proba(X_test)[:, 1]
    fraction_of_positives, mean_predicted_value = calibration_curve(
        y_test, prob_pos, n_bins=10
    )
    ax.plot(mean_predicted_value, fraction_of_positives, 's-', label=name)

ax.set_xlabel('Mean Predicted Probability')
ax.set_ylabel('Fraction of Positives')
ax.set_title('Calibration Comparison: Random Forest')
ax.legend(loc='lower right')
ax.grid(True, alpha=0.3)
plt.savefig('calibration_comparison.png', dpi=150, bbox_inches='tight')
plt.show()

print("""
┌─────────────────────────────────────────────────────────────────┐
│              CALIBRATION METHODS                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SIGMOID (Platt Scaling):                                       │
│  • Fits a logistic regression to the outputs                    │
│  • Works well when calibration curve is sigmoid-shaped          │
│  • Good for SVM                                                 │
│                                                                 │
│  ISOTONIC:                                                      │
│  • Non-parametric, more flexible                                │
│  • Can fit any monotonic function                               │
│  • Needs more data to avoid overfitting                         │
│  • Better for Random Forest, Naive Bayes                        │
│                                                                 │
│  WHEN TO USE:                                                   │
│  • When probability estimates matter (not just ranking)         │
│  • Risk assessment, decision making                             │
│  • When combining models                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")
Handling Imbalanced Data
Python

# imbalanced_data.py

import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import (
    classification_report, confusion_matrix, 
    roc_auc_score, f1_score, precision_recall_curve, auc
)
from sklearn.utils.class_weight import compute_class_weight

print("HANDLING IMBALANCED DATA")
print("=" * 60)

print("""
┌─────────────────────────────────────────────────────────────────┐
│                  IMBALANCED DATA PROBLEM                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Example: Fraud Detection                                      │
│   • 99% legitimate transactions                                 │
│   • 1% fraudulent transactions                                  │
│                                                                 │
│   Problem: Model can achieve 99% accuracy by predicting         │
│            everything as legitimate! (useless)                  │
│                                                                 │
│   Solutions:                                                    │
│   1. Class Weights: Penalize misclassifying minority class      │
│   2. Resampling: SMOTE, oversampling, undersampling            │
│   3. Different Metrics: Use F1, AUC-ROC, Precision-Recall      │
│   4. Threshold Adjustment: Change decision threshold            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
""")

# Create imbalanced dataset
X, y = make_classification(
    n_samples=10000,
    n_features=20,
    n_informative=15,
    n_redundant=5,
    weights=[0.95, 0.05],  # 95% class 0, 5% class 1
    random_state=42
)

print(f"\nClass distribution:")
unique, counts = np.unique(y, return_counts=True)
for cls, count in zip(unique, counts):
    print(f"  Class {cls}: {count} ({count/len(y)*100:.1f}%)")

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# ═══════════════════════════════════════════════════════════════
# 1. BASELINE (No handling)
# ═══════════════════════════════════════════════════════════════
print("\n1. BASELINE (No imbalance handling)")
print("-" * 40)

baseline = LogisticRegression(max_iter=1000)
baseline.fit(X_train, y_train)
y_pred_baseline = baseline.predict(X_test)

print(f"Accuracy: {baseline.score(X_test, y_test):.4f}")
print(f"F1 Score (minority): {f1_score(y_test, y_pred_baseline):.4f}")
print(f"\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred_baseline))

# ═══════════════════════════════════════════════════════════════
# 2. CLASS WEIGHTS
# ═══════════════════════════════════════════════════════════════
print("\n2. CLASS WEIGHTS")
print("-" * 40)

# Compute balanced weights
class_weights = compute_class_weight('balanced', classes=np.unique(y_train), y=y_train)
print(f"Computed weights: {dict(zip(np.unique(y_train), class_weights))}")

weighted_model = LogisticRegression(class_weight='balanced', max_iter=1000)
weighted_model.fit(X_train, y_train)
y_pred_weighted = weighted_model.predict(X_test)

print(f"Accuracy: {weighted_model.score(X_test, y_test):.4f}")
print(f"F1 Score (minority): {f1_score(y_test, y_pred_weighted):.4f}")
print(f"\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred_weighted))

# ═══════════════════════════════════════════════════════════════
# 3. THRESHOLD ADJUSTMENT
# ═══════════════════════════════════════════════════════════════
print("\n3. THRESHOLD ADJUSTMENT")
print("-" * 40)

# Get probabilities
y_proba = baseline.predict_proba(X_test)[:, 1]

# Find best threshold using precision-recall curve
precisions, recalls, thresholds = precision_recall_curve(y_test, y_proba)
f1_scores = 2 * (precisions * recalls) / (precisions + recalls + 1e-10)
best_threshold_idx = np.argmax(f1_scores)
best_threshold = thresholds[best_threshold_idx] if best_threshold_idx < len(thresholds) else 0.5

print(f"Default threshold: 0.5")
print(f"Best threshold for F1: {best_threshold:.4f}")

# Apply new threshold
y_pred_threshold = (y_proba >= best_threshold).astype(int)

print(f"\nWith default threshold (0.5):")
print(f"  F1 Score: {f1_score(y_test, y_pred_baseline):.4f}")
print(f"\nWith optimized threshold ({best_threshold:.4f}):")
print(f"  F1 Score: {f1_score(y_test, y_pred_threshold):.4f}")

# ═══════════════════════════════════════════════════════════════
# 4. RESAMPLING (using imbalanced-learn if available)
# ═══════════════════════════════════════════════════════════════
print("\n4. RESAMPLING TECHNIQUES")
print("-" * 40)

try:
    from imblearn.over_sampling import SMOTE, RandomOverSampler
    from imblearn.under_sampling import RandomUnderSampler
    from imblearn.pipeline import Pipeline as ImbPipeline
    
    # SMOTE
    smote = SMOTE(random_state=42)
    X_train_smote, y_train_smote = smote.fit_resample(X_train, y_train)
    
    print(f"Original training set: {len(y_train)} samples")
    print(f"After SMOTE: {len(y_train_smote)} samples")
    print(f"Class distribution after SMOTE: {np.bincount(y_train_smote)}")
    
    # Train on SMOTE data
    smote_model = LogisticRegression(max_iter=1000)
    smote_model.fit(X_train_smote, y_train_smote)
    y_pred_smote = smote_model.predict(X_test)
    
    print(f"\nWith SMOTE:")
    print(f"  F1 Score: {f1_score(y_test, y_pred_smote):.4f}")
    print(f"  Confusion Matrix:")
    print(confusion_matrix(y_test, y_pred_smote))
    
except ImportError:
    print("Install imbalanced-learn: pip install imbalanced-learn")
    print("SMOTE and other resampling techniques require this library.")

# ═══════════════════════════════════════════════════════════════
# 5. COMPARISON SUMMARY
# ═══════════════════════════════════════════════════════════════
print("\n" + "=" * 60)
print("SUMMARY COMPARISON")
print("=" * 60)

results = {
    'Baseline': y_pred_baseline,
    'Class Weights': y_pred_weighted,
    'Threshold Adjusted': y_pred_threshold,
}

if 'y_pred_smote' in dir():
    results['SMOTE'] = y_pred_smote

print(f"\n{'Method':<20} {'Accuracy':<12} {'F1 (minority)':<15} {'Recall (minority)'}")
print("-" * 65)

for name, y_pred in results.items():
    acc = np.mean(y_pred == y_test)
    f1 = f1_score(y_test, y_pred)
    cm = confusion_matrix(y_test, y_pred)
    recall = cm[1, 1] / (cm[1, 0] + cm[1, 1]) if (cm[1, 0] + cm[1, 1]) > 0 else 0
    print(f"{name:<20} {acc:<12.4f} {f1:<15.4f} {recall:.4f}")
Chapter 15: Real-World Projects
Project 1: Customer Churn Prediction
Python

# project_churn_prediction.py

"""
COMPLETE ML PROJECT: Customer Churn Prediction
==============================================

This project demonstrates a complete machine learning workflow:
1. Data Loading and Exploration
2. Data Preprocessing
3. Feature Engineering
4. Model Training and Selection
5. Hyperparameter Tuning
6. Model Evaluation
7. Model Deployment (saving/loading)
"""

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.impute import SimpleImputer
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.metrics import (
    classification_report, confusion_matrix, roc_auc_score,
    roc_curve, precision_recall_curve
)
import joblib
import warnings
warnings.filterwarnings('ignore')

print("=" * 70)
print("PROJECT: CUSTOMER CHURN PREDICTION")
print("=" * 70)

# ═══════════════════════════════════════════════════════════════════════
# STEP 1: CREATE SYNTHETIC DATASET
# ═══════════════════════════════════════════════════════════════════════
print("\n📊 STEP 1: Data Generation")
print("-" * 50)

np.random.seed(42)
n_samples = 5000

# Generate synthetic customer data
data = pd.DataFrame({
    'customer_id': range(1, n_samples + 1),
    'tenure_months': np.random.randint(1, 72, n_samples),
    'monthly_charges': np.random.uniform(20, 100, n_samples),
    'total_charges': np.random.uniform(100, 8000, n_samples),
    'contract_type': np.random.choice(['Month-to-month', 'One year', 'Two year'], n_samples, p=[0.5, 0.3, 0.2]),
    'payment_method': np.random.choice(['Electronic check', 'Mailed check', 'Bank transfer', 'Credit card'], n_samples),
    'internet_service': np.random.choice(['DSL', 'Fiber optic', 'No'], n_samples, p=[0.4, 0.4, 0.2]),
    'online_security': np.random.choice(['Yes', 'No', 'No internet service'], n_samples),
    'tech_support': np.random.choice(['Yes', 'No', 'No internet service'], n_samples),
    'num_support_tickets': np.random.poisson(2, n_samples),
    'satisfaction_score': np.random.randint(1, 6, n_samples),
})

# Create churn based on realistic factors
churn_probability = (
    0.1 +  # Base rate
    (data['contract_type'] == 'Month-to-month').astype(int) * 0.2 +
    (data['tenure_months'] < 12).astype(int) * 0.15 +
    (data['num_support_tickets'] > 3).astype(int) * 0.1 +
    (data['satisfaction_score'] < 3).astype(int) * 0.2 -
    (data['online_security'] == 'Yes').astype(int) * 0.1 -
    (data['tech_support'] == 'Yes').astype(int) * 0.05
)
churn_probability = np.clip(churn_probability, 0, 1)
data['churn'] = (np.random.random(n_samples) < churn_probability).astype(int)

# Add some missing values
data.loc[np.random.choice(n_samples, 100), 'total_charges'] = np.nan
data.loc[np.random.choice(n_samples, 50), 'satisfaction_score'] = np.nan

print(f"Dataset shape: {data.shape}")
print(f"Churn rate: {data['churn'].mean():.1%}")
print(f"\nFirst few rows:")
print(data.head())

# ═══════════════════════════════════════════════════════════════════════
# STEP 2: EXPLORATORY DATA ANALYSIS
# ═══════════════════════════════════════════════════════════════════════
print("\n📈 STEP 2: Exploratory Data Analysis")
print("-" * 50)

print("\nDataset Info:")
print(data.info())

print(f"\nMissing Values:")
print(data.isnull().sum()[data.isnull().sum() > 0])

print(f"\nChurn Distribution:")
print(data['churn'].value_counts())

print(f"\nNumeric Features Statistics:")
print(data.describe())

# Visualization
fig, axes = plt.subplots(2, 3, figsize=(15, 10))

# Churn distribution
axes[0, 0].pie(data['churn'].value_counts(), labels=['No Churn', 'Churn'], 
               autopct='%1.1f%%', colors=['lightgreen', 'lightcoral'])
axes[0, 0].set_title('Churn Distribution')

# Tenure vs Churn
data.boxplot(column='tenure_months', by='churn', ax=axes[0, 1])
axes[0, 1].set_title('Tenure by Churn Status')
axes[0, 1].set_xlabel('Churn')

# Monthly charges vs Churn
data.boxplot(column='monthly_charges', by='churn', ax=axes[0, 2])
axes[0, 2].set_title('Monthly Charges by Churn Status')
axes[0, 2].set_xlabel('Churn')

# Contract type vs Churn
contract_churn = data.groupby('contract_type')['churn'].mean()
contract_churn.plot(kind='bar', ax=axes[1, 0], color='steelblue')
axes[1, 0].set_title('Churn Rate by Contract Type')
axes[1, 0].set_ylabel('Churn Rate')
axes[1, 0].tick_params(axis='x', rotation=45)

# Support tickets vs Churn
data.boxplot(column='num_support_tickets', by='churn', ax=axes[1, 1])
axes[1, 1].set_title('Support Tickets by Churn Status')
axes[1, 1].set_xlabel('Churn')

# Satisfaction vs Churn
sat_churn = data.groupby('satisfaction_score')['churn'].mean()
sat_churn.plot(kind='bar', ax=axes[1, 2], color='steelblue')
axes[1, 2].set_title('Churn Rate by Satisfaction Score')
axes[1, 2].set_ylabel('Churn Rate')

plt.tight_layout()
plt.savefig('churn_eda.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 3: DATA PREPROCESSING
# ═══════════════════════════════════════════════════════════════════════
print("\n🔧 STEP 3: Data Preprocessing")
print("-" * 50)

# Separate features and target
X = data.drop(['customer_id', 'churn'], axis=1)
y = data['churn']

# Define column types
numeric_features = ['tenure_months', 'monthly_charges', 'total_charges', 
                    'num_support_tickets', 'satisfaction_score']
categorical_features = ['contract_type', 'payment_method', 'internet_service',
                        'online_security', 'tech_support']

print(f"Numeric features: {numeric_features}")
print(f"Categorical features: {categorical_features}")

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining set: {X_train.shape}")
print(f"Test set: {X_test.shape}")

# ═══════════════════════════════════════════════════════════════════════
# STEP 4: BUILD PREPROCESSING PIPELINE
# ═══════════════════════════════════════════════════════════════════════
print("\n🔨 STEP 4: Build Preprocessing Pipeline")
print("-" * 50)

from sklearn.preprocessing import OneHotEncoder

# Numeric transformer
numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

# Categorical transformer
categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='constant', fill_value='Unknown')),
    ('encoder', OneHotEncoder(drop='first', sparse_output=False, handle_unknown='ignore'))
])

# Full preprocessor
preprocessor = ColumnTransformer([
    ('num', numeric_transformer, numeric_features),
    ('cat', categorical_transformer, categorical_features)
])

print("Preprocessing pipeline created!")

# ═══════════════════════════════════════════════════════════════════════
# STEP 5: MODEL TRAINING AND COMPARISON
# ═══════════════════════════════════════════════════════════════════════
print("\n🎯 STEP 5: Model Training and Comparison")
print("-" * 50)

# Define models
models = {
    'Logistic Regression': LogisticRegression(max_iter=1000, random_state=42),
    'Random Forest': RandomForestClassifier(n_estimators=100, random_state=42),
    'Gradient Boosting': GradientBoostingClassifier(n_estimators=100, random_state=42)
}

results = []

for name, model in models.items():
    print(f"\nTraining {name}...")
    
    # Create pipeline
    pipeline = Pipeline([
        ('preprocessor', preprocessor),
        ('classifier', model)
    ])
    
    # Cross-validation
    cv_scores = cross_val_score(pipeline, X_train, y_train, cv=5, scoring='roc_auc')
    
    # Fit and predict
    pipeline.fit(X_train, y_train)
    y_pred = pipeline.predict(X_test)
    y_pred_proba = pipeline.predict_proba(X_test)[:, 1]
    
    # Metrics
    test_auc = roc_auc_score(y_test, y_pred_proba)
    
    results.append({
        'Model': name,
        'CV AUC (mean)': cv_scores.mean(),
        'CV AUC (std)': cv_scores.std(),
        'Test AUC': test_auc
    })
    
    print(f"  CV AUC: {cv_scores.mean():.4f} ± {cv_scores.std():.4f}")
    print(f"  Test AUC: {test_auc:.4f}")

# Results summary
results_df = pd.DataFrame(results)
print("\n" + "=" * 50)
print("MODEL COMPARISON SUMMARY")
print("=" * 50)
print(results_df.to_string(index=False))

# ═══════════════════════════════════════════════════════════════════════
# STEP 6: HYPERPARAMETER TUNING (Best Model)
# ═══════════════════════════════════════════════════════════════════════
print("\n⚙️ STEP 6: Hyperparameter Tuning")
print("-" * 50)

# Select best model for tuning
best_model_name = results_df.loc[results_df['Test AUC'].idxmax(), 'Model']
print(f"Tuning: {best_model_name}")

# Create pipeline for tuning
tuning_pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', GradientBoostingClassifier(random_state=42))
])

# Parameter grid
param_grid = {
    'classifier__n_estimators': [50, 100, 200],
    'classifier__max_depth': [3, 5, 7],
    'classifier__learning_rate': [0.05, 0.1, 0.2]
}

# Grid search
print("Running GridSearchCV...")
grid_search = GridSearchCV(
    tuning_pipeline,
    param_grid,
    cv=3,
    scoring='roc_auc',
    n_jobs=-1,
    verbose=1
)

grid_search.fit(X_train, y_train)

print(f"\nBest parameters: {grid_search.best_params_}")
print(f"Best CV AUC: {grid_search.best_score_:.4f}")

# ═══════════════════════════════════════════════════════════════════════
# STEP 7: FINAL EVALUATION
# ═══════════════════════════════════════════════════════════════════════
print("\n📊 STEP 7: Final Evaluation")
print("-" * 50)

# Get best model
best_model = grid_search.best_estimator_

# Predictions
y_pred_final = best_model.predict(X_test)
y_pred_proba_final = best_model.predict_proba(X_test)[:, 1]

# Classification report
print("\nClassification Report:")
print(classification_report(y_test, y_pred_final, target_names=['No Churn', 'Churn']))

# Confusion Matrix
print("Confusion Matrix:")
cm = confusion_matrix(y_test, y_pred_final)
print(cm)

# ROC AUC
final_auc = roc_auc_score(y_test, y_pred_proba_final)
print(f"\nFinal Test AUC: {final_auc:.4f}")

# Plot ROC Curve and Confusion Matrix
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# ROC Curve
fpr, tpr, _ = roc_curve(y_test, y_pred_proba_final)
axes[0].plot(fpr, tpr, 'b-', label=f'AUC = {final_auc:.4f}')
axes[0].plot([0, 1], [0, 1], 'k--')
axes[0].set_xlabel('False Positive Rate')
axes[0].set_ylabel('True Positive Rate')
axes[0].set_title('ROC Curve')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# Confusion Matrix
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', ax=axes[1],
            xticklabels=['No Churn', 'Churn'],
            yticklabels=['No Churn', 'Churn'])
axes[1].set_xlabel('Predicted')
axes[1].set_ylabel('Actual')
axes[1].set_title('Confusion Matrix')

plt.tight_layout()
plt.savefig('churn_final_evaluation.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 8: FEATURE IMPORTANCE
# ═══════════════════════════════════════════════════════════════════════
print("\n🔍 STEP 8: Feature Importance")
print("-" * 50)

# Get feature names
preprocessor_fitted = best_model.named_steps['preprocessor']
cat_encoder = preprocessor_fitted.named_transformers_['cat'].named_steps['encoder']
cat_feature_names = cat_encoder.get_feature_names_out(categorical_features)
all_feature_names = numeric_features + list(cat_feature_names)

# Get importances
classifier = best_model.named_steps['classifier']
importances = classifier.feature_importances_

# Create importance dataframe
importance_df = pd.DataFrame({
    'Feature': all_feature_names,
    'Importance': importances
}).sort_values('Importance', ascending=False)

print("\nTop 10 Most Important Features:")
print(importance_df.head(10).to_string(index=False))

# Plot
plt.figure(figsize=(10, 8))
plt.barh(importance_df['Feature'][:15], importance_df['Importance'][:15])
plt.xlabel('Importance')
plt.title('Top 15 Feature Importances')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.savefig('churn_feature_importance.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 9: SAVE MODEL
# ═══════════════════════════════════════════════════════════════════════
print("\n💾 STEP 9: Save Model")
print("-" * 50)

# Save the model
joblib.dump(best_model, 'churn_prediction_model.joblib')
print("Model saved to 'churn_prediction_model.joblib'")

# Save feature names for reference
with open('feature_names.txt', 'w') as f:
    f.write('\n'.join(all_feature_names))
print("Feature names saved to 'feature_names.txt'")

# ═══════════════════════════════════════════════════════════════════════
# STEP 10: PREDICTION EXAMPLE
# ═══════════════════════════════════════════════════════════════════════
print("\n🎯 STEP 10: Make Predictions on New Data")
print("-" * 50)

# Load model
loaded_model = joblib.load('churn_prediction_model.joblib')

# Create new customer data
new_customers = pd.DataFrame({
    'tenure_months': [5, 48, 12],
    'monthly_charges': [80, 60, 45],
    'total_charges': [400, 2880, 540],
    'contract_type': ['Month-to-month', 'Two year', 'One year'],
    'payment_method': ['Electronic check', 'Bank transfer', 'Credit card'],
    'internet_service': ['Fiber optic', 'DSL', 'DSL'],
    'online_security': ['No', 'Yes', 'No'],
    'tech_support': ['No', 'Yes', 'No'],
    'num_support_tickets': [5, 0, 2],
    'satisfaction_score': [2, 5, 3]
})

# Predict
predictions = loaded_model.predict(new_customers)
probabilities = loaded_model.predict_proba(new_customers)[:, 1]

print("\nNew Customer Predictions:")
print("-" * 50)
for i in range(len(new_customers)):
    print(f"\nCustomer {i+1}:")
    print(f"  Tenure: {new_customers.iloc[i]['tenure_months']} months")
    print(f"  Contract: {new_customers.iloc[i]['contract_type']}")
    print(f"  Satisfaction: {new_customers.iloc[i]['satisfaction_score']}/5")
    print(f"  ➡️  Churn Prediction: {'Yes' if predictions[i] == 1 else 'No'}")
    print(f"  ➡️  Churn Probability: {probabilities[i]:.1%}")

print("\n" + "=" * 70)
print("PROJECT COMPLETE! ✅")
print("=" * 70)
Project 2: Image Classification (Digits)
Python

# project_digit_classification.py

"""
COMPLETE ML PROJECT: Handwritten Digit Classification
=====================================================

This project demonstrates image classification workflow:
1. Load and visualize digit images
2. Preprocessing and feature extraction
3. Model comparison
4. Dimensionality reduction visualization
5. Error analysis
"""

import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import classification_report, confusion_matrix, accuracy_score
import seaborn as sns

print("=" * 70)
print("PROJECT: HANDWRITTEN DIGIT CLASSIFICATION")
print("=" * 70)

# ═══════════════════════════════════════════════════════════════════════
# STEP 1: LOAD AND EXPLORE DATA
# ═══════════════════════════════════════════════════════════════════════
print("\n📊 STEP 1: Load and Explore Data")
print("-" * 50)

# Load digits dataset
digits = load_digits()
X, y = digits.data, digits.target

print(f"Dataset shape: {X.shape}")
print(f"Number of samples: {X.shape[0]}")
print(f"Number of features: {X.shape[1]} (8x8 pixel images)")
print(f"Number of classes: {len(np.unique(y))} (digits 0-9)")
print(f"\nClass distribution:")
for digit in range(10):
    print(f"  Digit {digit}: {(y == digit).sum()} samples")

# Visualize some digits
fig, axes = plt.subplots(2, 10, figsize=(15, 4))
for digit in range(10):
    # Find first occurrence of each digit
    idx = np.where(y == digit)[0][0]
    
    # Top row: actual image
    axes[0, digit].imshow(digits.images[idx], cmap='gray')
    axes[0, digit].set_title(f'Digit {digit}')
    axes[0, digit].axis('off')
    
    # Bottom row: different sample of same digit
    idx2 = np.where(y == digit)[0][5]
    axes[1, digit].imshow(digits.images[idx2], cmap='gray')
    axes[1, digit].axis('off')

plt.suptitle('Sample Digits from Dataset', fontsize=14)
plt.tight_layout()
plt.savefig('digit_samples.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 2: DATA PREPROCESSING
# ═══════════════════════════════════════════════════════════════════════
print("\n🔧 STEP 2: Data Preprocessing")
print("-" * 50)

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"Training samples: {X_train.shape[0]}")
print(f"Test samples: {X_test.shape[0]}")

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print(f"\nFeature scaling applied:")
print(f"  Mean before: {X_train.mean():.2f}")
print(f"  Mean after: {X_train_scaled.mean():.6f}")
print(f"  Std before: {X_train.std():.2f}")
print(f"  Std after: {X_train_scaled.std():.2f}")

# ═══════════════════════════════════════════════════════════════════════
# STEP 3: DIMENSIONALITY REDUCTION VISUALIZATION
# ═══════════════════════════════════════════════════════════════════════
print("\n📉 STEP 3: Dimensionality Reduction Visualization")
print("-" * 50)

# Apply PCA for visualization
pca_2d = PCA(n_components=2)
X_pca_2d = pca_2d.fit_transform(X_train_scaled)

print(f"Variance explained by 2 components: {pca_2d.explained_variance_ratio_.sum():.2%}")

# Plot
plt.figure(figsize=(12, 8))
scatter = plt.scatter(X_pca_2d[:, 0], X_pca_2d[:, 1], 
                      c=y_train, cmap='tab10', alpha=0.6, s=15)
plt.colorbar(scatter, label='Digit')
plt.xlabel(f'PC1 ({pca_2d.explained_variance_ratio_[0]:.1%} variance)')
plt.ylabel(f'PC2 ({pca_2d.explained_variance_ratio_[1]:.1%} variance)')
plt.title('Digits Projected onto First 2 Principal Components')
plt.savefig('digit_pca_visualization.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 4: MODEL COMPARISON
# ═══════════════════════════════════════════════════════════════════════
print("\n🎯 STEP 4: Model Comparison")
print("-" * 50)

# Define models
models = {
    'Logistic Regression': Pipeline([
        ('scaler', StandardScaler()),
        ('classifier', LogisticRegression(max_iter=5000, random_state=42))
    ]),
    'SVM (RBF)': Pipeline([
        ('scaler', StandardScaler()),
        ('classifier', SVC(kernel='rbf', random_state=42))
    ]),
    'Random Forest': Pipeline([
        ('classifier', RandomForestClassifier(n_estimators=100, random_state=42))
    ]),
    'KNN': Pipeline([
        ('scaler', StandardScaler()),
        ('classifier', KNeighborsClassifier(n_neighbors=5))
    ]),
    'PCA + Logistic': Pipeline([
        ('scaler', StandardScaler()),
        ('pca', PCA(n_components=30)),
        ('classifier', LogisticRegression(max_iter=5000, random_state=42))
    ])
}

results = []

for name, model in models.items():
    print(f"\nEvaluating {name}...")
    
    # Cross-validation
    cv_scores = cross_val_score(model, X_train, y_train, cv=5, n_jobs=-1)
    
    # Train and test
    model.fit(X_train, y_train)
    test_acc = model.score(X_test, y_test)
    
    results.append({
        'Model': name,
        'CV Accuracy (mean)': cv_scores.mean(),
        'CV Accuracy (std)': cv_scores.std(),
        'Test Accuracy': test_acc
    })
    
    print(f"  CV Accuracy: {cv_scores.mean():.4f} ± {cv_scores.std():.4f}")
    print(f"  Test Accuracy: {test_acc:.4f}")

# Summary
results_df = pd.DataFrame(results)
print("\n" + "=" * 60)
print("MODEL COMPARISON SUMMARY")
print("=" * 60)
print(results_df.to_string(index=False))

# ═══════════════════════════════════════════════════════════════════════
# STEP 5: HYPERPARAMETER TUNING
# ═══════════════════════════════════════════════════════════════════════
print("\n⚙️ STEP 5: Hyperparameter Tuning (SVM)")
print("-" * 50)

# Tune SVM
svm_pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', SVC(random_state=42))
])

param_grid = {
    'classifier__C': [0.1, 1, 10],
    'classifier__gamma': ['scale', 0.01, 0.1],
    'classifier__kernel': ['rbf', 'poly']
}

print("Running GridSearchCV...")
grid_search = GridSearchCV(
    svm_pipeline,
    param_grid,
    cv=3,
    scoring='accuracy',
    n_jobs=-1,
    verbose=1
)

grid_search.fit(X_train, y_train)

print(f"\nBest parameters: {grid_search.best_params_}")
print(f"Best CV accuracy: {grid_search.best_score_:.4f}")

# ═══════════════════════════════════════════════════════════════════════
# STEP 6: FINAL EVALUATION
# ═══════════════════════════════════════════════════════════════════════
print("\n📊 STEP 6: Final Evaluation")
print("-" * 50)

# Best model
best_model = grid_search.best_estimator_
y_pred = best_model.predict(X_test)

print(f"\nTest Accuracy: {accuracy_score(y_test, y_pred):.4f}")

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)

plt.figure(figsize=(10, 8))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=range(10), yticklabels=range(10))
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix - Digit Classification')
plt.savefig('digit_confusion_matrix.png', dpi=150, bbox_inches='tight')
plt.show()

# ═══════════════════════════════════════════════════════════════════════
# STEP 7: ERROR ANALYSIS
# ═══════════════════════════════════════════════════════════════════════
print("\n🔍 STEP 7: Error Analysis")
print("-" * 50)

# Find misclassified samples
misclassified = np.where(y_pred != y_test)[0]
print(f"Number of misclassified samples: {len(misclassified)}")

# Show some misclassified examples
n_show = min(10, len(misclassified))
fig, axes = plt.subplots(2, 5, figsize=(12, 5))
axes = axes.flatten()

for i, idx in enumerate(misclassified[:n_show]):
    img = X_test[idx].reshape(8, 8)
    axes[i].imshow(img, cmap='gray')
    axes[i].set_title(f'True: {y_test[idx]}, Pred: {y_pred[idx]}', fontsize=10)
    axes[i].axis('off')

plt.suptitle('Misclassified Examples', fontsize=14)
plt.tight_layout()
plt.savefig('digit_errors.png', dpi=150, bbox_inches='tight')
plt.show()

# Most confused pairs
print("\nMost Commonly Confused Digit Pairs:")
for i in range(10):
    for j in range(10):
        if i != j and cm[i, j] > 1:
            print(f"  Digit {i} confused as {j}: {cm[i, j]} times")

print("\n" + "=" * 70)
print("PROJECT COMPLETE! ✅")
print("=" * 70)
Final Summary
text

┌─────────────────────────────────────────────────────────────────────────┐
│                SCIKIT-LEARN MASTERY SUMMARY                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  CORE CONCEPTS:                                                         │
│  ─────────────                                                          │
│  • Estimators: All objects that learn from data (.fit())                │
│  • Predictors: Make predictions (.predict(), .score())                  │
│  • Transformers: Transform data (.transform())                          │
│  • Consistent API: Same interface for all algorithms                    │
│                                                                         │
│  WORKFLOW:                                                              │
│  ──────────                                                             │
│  1. Load/Prepare Data                                                   │
│  2. Preprocess (scale, encode, impute)                                  │
│  3. Split (train_test_split)                                            │
│  4. Train (model.fit())                                                 │
│  5. Evaluate (cross_val_score, metrics)                                 │
│  6. Tune (GridSearchCV, RandomizedSearchCV)                             │
│  7. Deploy (joblib.dump/load)                                           │
│                                                                         │
│  KEY MODULES:                                                           │
│  ────────────                                                           │
│  • sklearn.preprocessing: Scaling, encoding                             │
│  • sklearn.model_selection: Split, CV, tuning                           │
│  • sklearn.linear_model: Linear/Logistic regression                     │
│  • sklearn.tree: Decision trees                                         │
│  • sklearn.ensemble: Random Forest, Gradient Boosting                   │
│  • sklearn.svm: Support Vector Machines                                 │
│  • sklearn.neighbors: KNN                                               │
│  • sklearn.cluster: K-Means, DBSCAN                                     │
│  • sklearn.decomposition: PCA                                           │
│  • sklearn.pipeline: Pipeline, ColumnTransformer                        │
│  • sklearn.metrics: All evaluation metrics                              │
│                                                                         │
│  BEST PRACTICES:                                                        │
│  ───────────────                                                        │
│  ✓ Always use pipelines                                                 │
│  ✓ Always use cross-validation                                          │
│  ✓ Scale features for distance-based algorithms                         │
│  ✓ Handle missing values explicitly                                     │
│  ✓ Check for class imbalance                                            │
│  ✓ Use appropriate metrics for your problem                             │
│  ✓ Save and version your models                                         │
│                                                                         │
│  ALGORITHM SELECTION GUIDE:                                             │
│  ──────────────────────────                                             │
│  Classification:                                                        │
│    • Start with: Logistic Regression, Random Forest                     │
│    • Complex: Gradient Boosting, SVM                                    │
│                                                                         │
│  Regression:                                                            │
│    • Start with: Linear Regression, Ridge                               │
│    • Complex: Gradient Boosting, Random Forest                          │
│                                                                         │
│  Clustering:                                                            │
│    • Spherical clusters: K-Means                                        │
│    • Arbitrary shapes: DBSCAN                                           │
│    • Hierarchical: AgglomerativeClustering                              │
│                                                                         │
│  Dimensionality Reduction:                                              │
│    • Linear: PCA                                                        │
│    • Visualization: t-SNE, UMAP                                         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

Congratulations on completing this comprehensive Scikit-Learn guide! 🎉

You now have the knowledge to:
• Build end-to-end ML pipelines
• Preprocess any type of data
• Train and evaluate multiple algorithms
• Tune hyperparameters effectively
• Handle real-world challenges
• Deploy models to production

Keep practicing with real datasets and projects!
End of Scikit-Learn Complete Mastery Guide










