🎯 The Ultimate Guide to Hyperparameter Tuning
GridSearch, RandomSearch & Bayesian Optimization
From Zero to Hero - Complete Masterclass
📚 Table of Contents
Chapter 1: Foundation - What Are Hyperparameters?
Chapter 2: Why Hyperparameter Tuning Matters
Chapter 3: Grid Search - The Exhaustive Approach
Chapter 4: Random Search - The Smart Gambler
Chapter 5: Bayesian Optimization - The Intelligent Explorer
Chapter 6: Comparison & When to Use What
Chapter 7: Advanced Techniques & Best Practices
Chapter 8: Real-World Projects & Case Studies
Chapter 9: Common Mistakes & How to Avoid Them
Chapter 10: Interview Questions & Answers
Chapter 1: Foundation - What Are Hyperparameters?
1.1 The Restaurant Analogy 🍳
Imagine you're a chef learning to cook the perfect dish.

Parameters = The actual cooking (how the ingredients mix, chemical reactions)

You don't control this directly
It happens automatically based on your settings
Hyperparameters = Your cooking settings (oven temperature, cooking time, flame intensity)

You SET these BEFORE cooking
They CONTROL how the cooking happens
1.2 Formal Definition
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   PARAMETERS: Values that the model LEARNS from data            │
│   Examples: Weights, Biases, Coefficients                       │
│                                                                 │
│   HYPERPARAMETERS: Values that YOU SET before training          │
│   Examples: Learning rate, Number of trees, Max depth           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
1.3 Visual Understanding
text

YOUR INPUT                    TRAINING PROCESS                 OUTPUT
    │                              │                              │
    ▼                              ▼                              ▼
┌─────────┐                 ┌─────────────┐                ┌──────────┐
│  Data   │ ───────────────▶│   Model     │───────────────▶│Predictions│
└─────────┘                 │  Training   │                └──────────┘
                            └─────────────┘
    ▲                              ▲
    │                              │
┌─────────┐                 ┌─────────────┐
│Features │                 │HYPERPARAMS  │
│ Labels  │                 │(You set     │
└─────────┘                 │ these!)     │
                            └─────────────┘
1.4 Types of Hyperparameters
By Data Type:
Type	Description	Examples
Continuous	Any decimal value in a range	Learning rate (0.001 to 0.1)
Discrete/Integer	Whole numbers only	Number of trees (10, 50, 100)
Categorical	Choices from a list	Activation function (relu, sigmoid, tanh)
Binary	True or False	Use dropout (True/False)
By Algorithm:
text

┌──────────────────────────────────────────────────────────────────┐
│                    COMMON HYPERPARAMETERS                        │
├──────────────────┬───────────────────────────────────────────────┤
│ RANDOM FOREST    │ n_estimators, max_depth, min_samples_split,   │
│                  │ min_samples_leaf, max_features                │
├──────────────────┼───────────────────────────────────────────────┤
│ SVM              │ C, kernel, gamma, degree                      │
├──────────────────┼───────────────────────────────────────────────┤
│ NEURAL NETWORK   │ learning_rate, batch_size, epochs,            │
│                  │ hidden_layers, neurons, dropout_rate          │
├──────────────────┼───────────────────────────────────────────────┤
│ XGBoost          │ learning_rate, n_estimators, max_depth,       │
│                  │ subsample, colsample_bytree                   │
├──────────────────┼───────────────────────────────────────────────┤
│ KNN              │ n_neighbors, weights, metric                  │
└──────────────────┴───────────────────────────────────────────────┘
1.5 Code Example: Parameters vs Hyperparameters
Python

from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Load data
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# ╔═══════════════════════════════════════════════════════════════╗
# ║  HYPERPARAMETERS - YOU set these BEFORE training              ║
# ╚═══════════════════════════════════════════════════════════════╝
model = RandomForestClassifier(
    n_estimators=100,      # Hyperparameter: Number of trees
    max_depth=5,           # Hyperparameter: Maximum depth of trees
    min_samples_split=2,   # Hyperparameter: Minimum samples to split
    random_state=42        # Hyperparameter: Random seed
)

# ╔═══════════════════════════════════════════════════════════════╗
# ║  PARAMETERS - Model LEARNS these DURING training              ║
# ╚═══════════════════════════════════════════════════════════════╝
model.fit(X_train, y_train)

# After training, the model has learned PARAMETERS:
# - Feature importances
# - Split points in each tree
# - Leaf node values
print("Feature Importances (LEARNED PARAMETERS):")
print(model.feature_importances_)
1.6 The Key Insight 💡
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   Think of it like this:                                        │
│                                                                 │
│   HYPERPARAMETERS = The RECIPE you choose                       │
│   PARAMETERS = The DISH that gets cooked                        │
│                                                                 │
│   You can change the recipe (hyperparameters) to get            │
│   a better dish (better parameters = better model)              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 2: Why Hyperparameter Tuning Matters
2.1 The Impact Visualization
text

ACCURACY WITH DEFAULT HYPERPARAMETERS:     ████████████░░░░░░░░ 65%

ACCURACY WITH TUNED HYPERPARAMETERS:       ██████████████████░░ 92%

                                           ─────────────────────
                                           IMPROVEMENT: +27% ⬆️
2.2 Real-World Impact
Scenario	Default	Tuned	Business Impact
Fraud Detection	75%	95%	Save millions in fraud
Medical Diagnosis	80%	97%	Save lives
Customer Churn	70%	88%	Retain customers
Spam Filter	85%	99%	Better user experience
2.3 The Goldilocks Problem 🐻
text

UNDERFITTING                    JUST RIGHT                    OVERFITTING
(Too Simple)                    (Optimal)                     (Too Complex)
                                   
     📉                            📈                            📉
    /                             /\                           /\/\/\
   /                             /  \                         /      \
  /                             /    \                       /        \
 /                             /      \                     /          \
                                   
High Bias                    Low Bias                      Low Bias
High Variance Loss           Low Variance Loss             High Variance
                                   
"Model is too dumb"          "Model is perfect"            "Model memorized"


HYPERPARAMETER TUNING HELPS YOU FIND THE "JUST RIGHT" SWEET SPOT!
2.4 What Happens Without Proper Tuning?
Python

# ❌ BAD: Using default hyperparameters blindly
from sklearn.svm import SVC

# Default SVM - might not work well for your data
model = SVC()  # Uses default C=1.0, kernel='rbf', gamma='scale'
model.fit(X_train, y_train)
print(f"Default accuracy: {model.score(X_test, y_test)}")  # Maybe 70%

# ✅ GOOD: Tuned hyperparameters
model_tuned = SVC(C=10, kernel='rbf', gamma=0.1)
model_tuned.fit(X_train, y_train)
print(f"Tuned accuracy: {model_tuned.score(X_test, y_test)}")  # Maybe 95%
2.5 The Search Space Problem
text

Imagine you have just 3 hyperparameters:

Hyperparameter 1: 10 possible values
Hyperparameter 2: 10 possible values  
Hyperparameter 3: 10 possible values

Total combinations = 10 × 10 × 10 = 1,000 combinations!

With 5 hyperparameters (10 values each):
Total = 10^5 = 100,000 combinations!

This is why we need SMART search strategies!
2.6 The Three Main Approaches Overview
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│                    HYPERPARAMETER TUNING                        │
│                                                                 │
│         ┌──────────────┐                                        │
│         │              │                                        │
│         │  Grid Search │ ──▶ Try EVERY combination              │
│         │              │     Exhaustive but slow                │
│         └──────────────┘                                        │
│                │                                                │
│                ▼                                                │
│         ┌──────────────┐                                        │
│         │              │                                        │
│         │Random Search │ ──▶ Try RANDOM combinations            │
│         │              │     Fast but might miss best           │
│         └──────────────┘                                        │
│                │                                                │
│                ▼                                                │
│         ┌──────────────┐                                        │
│         │   Bayesian   │                                        │
│         │ Optimization │ ──▶ LEARN from previous tries          │
│         │              │     Smart and efficient                │
│         └──────────────┘                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 3: Grid Search - The Exhaustive Approach
3.1 What is Grid Search?
Simple Definition: Grid Search tries EVERY possible combination of hyperparameters you specify.

Analogy: Imagine you're finding the perfect pizza. You try:

Every crust type (thin, thick, stuffed)
Every sauce (marinara, white, bbq)
Every cheese amount (light, medium, heavy)
Grid Search = Try ALL 27 combinations (3 × 3 × 3)!

3.2 Visual Representation
text

                    MAX_DEPTH
                    3     5     7     10
                 ┌─────┬─────┬─────┬─────┐
              50 │  ●  │  ●  │  ●  │  ●  │
    N            ├─────┼─────┼─────┼─────┤
    _         100│  ●  │  ●  │  ●  │  ●  │
    E            ├─────┼─────┼─────┼─────┤
    S         150│  ●  │  ●  │  ●  │  ●  │
    T            ├─────┼─────┼─────┼─────┤
    I         200│  ●  │  ●  │  ●  │  ●  │
    M            └─────┴─────┴─────┴─────┘
    A
    T            ● = Each dot is ONE model trained
    O            Total = 4 × 4 = 16 models
    R
    S
    
    Grid Search tries EVERY intersection point!
3.3 How Grid Search Works - Step by Step
text

STEP 1: Define the hyperparameter grid
        ┌────────────────────────────────────┐
        │ n_estimators: [100, 200, 300]      │
        │ max_depth: [5, 10, 15]             │
        │ min_samples_split: [2, 5, 10]      │
        └────────────────────────────────────┘
        Total combinations: 3 × 3 × 3 = 27

STEP 2: Create all combinations
        Combo 1:  n_estimators=100, max_depth=5,  min_samples_split=2
        Combo 2:  n_estimators=100, max_depth=5,  min_samples_split=5
        Combo 3:  n_estimators=100, max_depth=5,  min_samples_split=10
        ... (24 more combinations)

STEP 3: For each combination:
        ┌──────────────────────────────────────────────┐
        │  a) Train model with these hyperparameters   │
        │  b) Evaluate using cross-validation          │
        │  c) Record the score                         │
        └──────────────────────────────────────────────┘

STEP 4: Select the combination with the BEST score
3.4 Basic Grid Search Implementation
Python

from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

# ═══════════════════════════════════════════════════════════════
# STEP 1: Load and prepare data
# ═══════════════════════════════════════════════════════════════
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ═══════════════════════════════════════════════════════════════
# STEP 2: Define the model
# ═══════════════════════════════════════════════════════════════
model = RandomForestClassifier(random_state=42)

# ═══════════════════════════════════════════════════════════════
# STEP 3: Define the hyperparameter grid
# ═══════════════════════════════════════════════════════════════
param_grid = {
    'n_estimators': [50, 100, 200],      # Number of trees
    'max_depth': [3, 5, 10, None],        # Tree depth (None = unlimited)
    'min_samples_split': [2, 5, 10],      # Min samples to split a node
    'min_samples_leaf': [1, 2, 4]         # Min samples in leaf node
}

# Total combinations: 3 × 4 × 3 × 3 = 108 combinations!

# ═══════════════════════════════════════════════════════════════
# STEP 4: Create GridSearchCV object
# ═══════════════════════════════════════════════════════════════
grid_search = GridSearchCV(
    estimator=model,           # The model to tune
    param_grid=param_grid,     # Hyperparameter grid
    cv=5,                      # 5-fold cross-validation
    scoring='accuracy',        # Metric to optimize
    n_jobs=-1,                 # Use all CPU cores
    verbose=2,                 # Print progress
    return_train_score=True    # Also record training scores
)

# ═══════════════════════════════════════════════════════════════
# STEP 5: Run Grid Search
# ═══════════════════════════════════════════════════════════════
print("Starting Grid Search...")
print(f"Total combinations to try: 108")
print(f"With 5-fold CV: 108 × 5 = 540 model trainings!\n")

grid_search.fit(X_train, y_train)

# ═══════════════════════════════════════════════════════════════
# STEP 6: Analyze Results
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*60)
print("GRID SEARCH RESULTS")
print("="*60)

print(f"\n✅ Best Parameters Found:")
for param, value in grid_search.best_params_.items():
    print(f"   {param}: {value}")

print(f"\n📊 Best Cross-Validation Score: {grid_search.best_score_:.4f}")

# Test on held-out test set
test_score = grid_search.best_estimator_.score(X_test, y_test)
print(f"📈 Test Set Score: {test_score:.4f}")
3.5 Understanding Cross-Validation in Grid Search
text

WHY CROSS-VALIDATION?
─────────────────────

Without CV: Train on same data → Evaluate on same data → OVERFITTING!

With CV: Multiple train/test splits → Average performance → RELIABLE!


5-FOLD CROSS-VALIDATION VISUALIZATION:
──────────────────────────────────────

Fold 1: [TEST] [TRAIN] [TRAIN] [TRAIN] [TRAIN]  → Score: 0.92
Fold 2: [TRAIN] [TEST] [TRAIN] [TRAIN] [TRAIN]  → Score: 0.89
Fold 3: [TRAIN] [TRAIN] [TEST] [TRAIN] [TRAIN]  → Score: 0.91
Fold 4: [TRAIN] [TRAIN] [TRAIN] [TEST] [TRAIN]  → Score: 0.93
Fold 5: [TRAIN] [TRAIN] [TRAIN] [TRAIN] [TEST]  → Score: 0.90
                                                   ─────────
                                         Average:    0.91

This average (0.91) is what Grid Search uses to compare hyperparameters!
3.6 Analyzing Grid Search Results in Detail
Python

import pandas as pd
import numpy as np

# Convert results to DataFrame for analysis
results_df = pd.DataFrame(grid_search.cv_results_)

# ═══════════════════════════════════════════════════════════════
# View top 10 performing combinations
# ═══════════════════════════════════════════════════════════════
print("\n🏆 TOP 10 HYPERPARAMETER COMBINATIONS:\n")

top_10 = results_df.nsmallest(10, 'rank_test_score')[
    ['params', 'mean_test_score', 'std_test_score', 'rank_test_score']
]
print(top_10.to_string())

# ═══════════════════════════════════════════════════════════════
# Check for overfitting: Compare train vs test scores
# ═══════════════════════════════════════════════════════════════
print("\n\n📊 OVERFITTING ANALYSIS:")
print("-" * 50)

best_idx = grid_search.best_index_
train_score = results_df.loc[best_idx, 'mean_train_score']
test_score = results_df.loc[best_idx, 'mean_test_score']

print(f"Best Model - Train Score: {train_score:.4f}")
print(f"Best Model - Test Score:  {test_score:.4f}")
print(f"Difference (Gap):         {train_score - test_score:.4f}")

if train_score - test_score > 0.05:
    print("⚠️  WARNING: Possible overfitting detected!")
else:
    print("✅ Good! No significant overfitting.")

# ═══════════════════════════════════════════════════════════════
# Analyze impact of each hyperparameter
# ═══════════════════════════════════════════════════════════════
print("\n\n📈 HYPERPARAMETER IMPACT ANALYSIS:")
print("-" * 50)

for param in param_grid.keys():
    param_col = f'param_{param}'
    grouped = results_df.groupby(param_col)['mean_test_score'].mean()
    print(f"\n{param}:")
    for value, score in grouped.items():
        bar = '█' * int(score * 50)
        print(f"  {str(value):>10}: {score:.4f} {bar}")
3.7 Grid Search Visualization
Python

import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

def visualize_grid_search_2d(grid_search, param1, param2):
    """
    Create a heatmap showing how two hyperparameters affect performance
    """
    results = pd.DataFrame(grid_search.cv_results_)
    
    # Pivot for heatmap
    pivot_table = results.pivot_table(
        values='mean_test_score',
        index=f'param_{param1}',
        columns=f'param_{param2}',
        aggfunc='mean'
    )
    
    plt.figure(figsize=(10, 8))
    sns.heatmap(
        pivot_table, 
        annot=True, 
        fmt='.3f', 
        cmap='YlGnBu',
        cbar_kws={'label': 'Mean CV Score'}
    )
    plt.title(f'Grid Search Results: {param1} vs {param2}')
    plt.xlabel(param2)
    plt.ylabel(param1)
    plt.tight_layout()
    plt.show()

# Usage:
# visualize_grid_search_2d(grid_search, 'n_estimators', 'max_depth')
3.8 Grid Search - Complete Production Code
Python

"""
PRODUCTION-READY GRID SEARCH IMPLEMENTATION
============================================
Complete example with all best practices
"""

import numpy as np
import pandas as pd
from sklearn.model_selection import GridSearchCV, StratifiedKFold
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import warnings
import time
import joblib

warnings.filterwarnings('ignore')

class GridSearchTuner:
    """
    Professional Grid Search implementation with logging and analysis
    """
    
    def __init__(self, model, param_grid, cv=5, scoring='accuracy'):
        self.model = model
        self.param_grid = param_grid
        self.cv = cv
        self.scoring = scoring
        self.grid_search = None
        self.results_df = None
        
    def calculate_total_fits(self):
        """Calculate total number of model fits"""
        total_combinations = 1
        for param, values in self.param_grid.items():
            total_combinations *= len(values)
        return total_combinations * self.cv
    
    def fit(self, X, y):
        """Run grid search with detailed logging"""
        
        # Print search space info
        print("="*70)
        print("GRID SEARCH CONFIGURATION")
        print("="*70)
        print(f"\n📋 Hyperparameter Space:")
        for param, values in self.param_grid.items():
            print(f"   • {param}: {values}")
        
        total_combinations = self.calculate_total_fits() // self.cv
        total_fits = self.calculate_total_fits()
        
        print(f"\n📊 Search Statistics:")
        print(f"   • Total unique combinations: {total_combinations}")
        print(f"   • Cross-validation folds: {self.cv}")
        print(f"   • Total model trainings: {total_fits}")
        print(f"   • Scoring metric: {self.scoring}")
        
        # Estimate time (rough estimate: 0.5 seconds per fit)
        est_time = total_fits * 0.5
        print(f"   • Estimated time: {est_time/60:.1f} minutes")
        
        print("\n" + "="*70)
        print("STARTING GRID SEARCH...")
        print("="*70 + "\n")
        
        # Create and run grid search
        start_time = time.time()
        
        self.grid_search = GridSearchCV(
            estimator=self.model,
            param_grid=self.param_grid,
            cv=StratifiedKFold(n_splits=self.cv, shuffle=True, random_state=42),
            scoring=self.scoring,
            n_jobs=-1,
            verbose=1,
            return_train_score=True,
            error_score='raise'
        )
        
        self.grid_search.fit(X, y)
        
        elapsed_time = time.time() - start_time
        
        # Store results
        self.results_df = pd.DataFrame(self.grid_search.cv_results_)
        
        # Print results
        print("\n" + "="*70)
        print("GRID SEARCH COMPLETED!")
        print("="*70)
        print(f"\n⏱️  Total time: {elapsed_time:.2f} seconds ({elapsed_time/60:.2f} minutes)")
        print(f"\n🏆 BEST PARAMETERS FOUND:")
        for param, value in self.grid_search.best_params_.items():
            print(f"   • {param}: {value}")
        print(f"\n📊 BEST CV SCORE: {self.grid_search.best_score_:.4f}")
        
        return self
    
    def get_best_model(self):
        """Return the best trained model"""
        return self.grid_search.best_estimator_
    
    def analyze_results(self, top_n=10):
        """Detailed analysis of grid search results"""
        
        print("\n" + "="*70)
        print(f"TOP {top_n} HYPERPARAMETER COMBINATIONS")
        print("="*70 + "\n")
        
        # Get top N results
        top_results = self.results_df.nsmallest(top_n, 'rank_test_score')
        
        for idx, row in top_results.iterrows():
            rank = int(row['rank_test_score'])
            print(f"Rank #{rank}:")
            print(f"  Parameters: {row['params']}")
            print(f"  CV Score: {row['mean_test_score']:.4f} (±{row['std_test_score']:.4f})")
            print(f"  Train Score: {row['mean_train_score']:.4f}")
            print()
        
        return top_results
    
    def save_results(self, filepath):
        """Save results to CSV"""
        self.results_df.to_csv(filepath, index=False)
        print(f"✅ Results saved to {filepath}")
    
    def save_best_model(self, filepath):
        """Save the best model"""
        joblib.dump(self.grid_search.best_estimator_, filepath)
        print(f"✅ Best model saved to {filepath}")


# ═══════════════════════════════════════════════════════════════════
# USAGE EXAMPLE
# ═══════════════════════════════════════════════════════════════════

if __name__ == "__main__":
    
    # Load data
    data = load_breast_cancer()
    X, y = data.data, data.target
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y
    )
    
    # Define model and hyperparameter grid
    model = RandomForestClassifier(random_state=42)
    
    param_grid = {
        'n_estimators': [50, 100, 200],
        'max_depth': [5, 10, 15, None],
        'min_samples_split': [2, 5, 10],
        'min_samples_leaf': [1, 2, 4],
        'max_features': ['sqrt', 'log2']
    }
    
    # Run Grid Search
    tuner = GridSearchTuner(
        model=model,
        param_grid=param_grid,
        cv=5,
        scoring='accuracy'
    )
    
    tuner.fit(X_train, y_train)
    tuner.analyze_results(top_n=5)
    
    # Evaluate on test set
    best_model = tuner.get_best_model()
    test_score = best_model.score(X_test, y_test)
    print(f"\n🎯 FINAL TEST SET ACCURACY: {test_score:.4f}")
3.9 Grid Search Pros and Cons
text

┌─────────────────────────────────────────────────────────────────┐
│                     GRID SEARCH                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✅ ADVANTAGES:                                                 │
│  ──────────────                                                 │
│  • Guaranteed to find best combination (in your grid)          │
│  • Simple to understand and implement                          │
│  • Exhaustive - no combination is missed                       │
│  • Results are reproducible                                    │
│  • Easy to parallelize                                         │
│                                                                 │
│  ❌ DISADVANTAGES:                                              │
│  ───────────────                                                │
│  • Computationally expensive (curse of dimensionality)         │
│  • Time grows exponentially with hyperparameters               │
│  • You must pre-define the grid (might miss optimal values)    │
│  • Wastes time on bad regions of search space                  │
│  • Not practical for large search spaces                       │
│                                                                 │
│  📊 COMPLEXITY:                                                 │
│  ──────────────                                                 │
│  Time = O(n₁ × n₂ × n₃ × ... × nₖ × cv_folds)                  │
│                                                                 │
│  Example: 5 hyperparameters, 10 values each, 5-fold CV         │
│  = 10⁵ × 5 = 500,000 model trainings! 😱                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
3.10 When to Use Grid Search
text

✅ USE GRID SEARCH WHEN:
────────────────────────
• You have a SMALL search space (few hyperparameters, few values)
• Computational resources are NOT a constraint
• You need GUARANTEED exhaustive search
• You have strong prior knowledge about good hyperparameter ranges
• Reproducibility is critical

❌ AVOID GRID SEARCH WHEN:
──────────────────────────
• Search space is large (> 1000 combinations)
• Computational time is limited
• You have many continuous hyperparameters
• You're in early experimentation phase
• You want adaptive/intelligent search
Chapter 4: Random Search - The Smart Gambler
4.1 What is Random Search?
Simple Definition: Random Search randomly samples hyperparameter combinations from the search space.

Analogy: Instead of trying every pizza combination, you randomly pick 20 combinations and try those. You might find something great faster!

4.2 The Key Insight: Why Random Search Can Beat Grid Search
text

THE BERGSTRA & BENGIO INSIGHT (2012)
────────────────────────────────────

Important Discovery: Not all hyperparameters matter equally!

Consider 2 hyperparameters:
• Learning Rate: VERY IMPORTANT (affects model significantly)
• Batch Size: LESS IMPORTANT (affects model slightly)


GRID SEARCH PROBLEM:
────────────────────
        Batch Size
        16   32   64
      ┌────┬────┬────┐
0.001 │ ●  │ ●  │ ●  │   Only 3 unique learning
      ├────┼────┼────┤   rates are tested!
0.01  │ ●  │ ●  │ ●  │   
      ├────┼────┼────┤   9 total points, but
0.1   │ ●  │ ●  │ ●  │   exploration of the
      └────┴────┴────┘   important dimension is
                         LIMITED!
L
e
a
r
n
i
n
g

R
a
t
e


RANDOM SEARCH ADVANTAGE:
────────────────────────
        Batch Size
        16   32   64
      ┌────┬────┬────┐
      │●   │    │  ● │   9 total points, but
      │    │ ●  │    │   9 UNIQUE learning
      │  ● │    │●   │   rates are tested!
      │    │  ● │    │   
      │ ●  │    │  ● │   Better exploration of
      │    │ ● │    │   the important dimension!
      └────┴────┴────┘


CONCLUSION: With the same budget, Random Search explores MORE
unique values of IMPORTANT hyperparameters!
4.3 Visual Comparison: Grid vs Random
text

                    GRID SEARCH                         RANDOM SEARCH
                    ───────────                         ─────────────
                    
      │ ● ─ ● ─ ● ─ ● ─ ●               │    ●              ●
      │ │   │   │   │   │               │         ●    ●
      │ ● ─ ● ─ ● ─ ● ─ ●               │  ●          
      │ │   │   │   │   │               │       ●         ●
      │ ● ─ ● ─ ● ─ ● ─ ●               │   ●        ●
      │ │   │   │   │   │               │        ●
      │ ● ─ ● ─ ● ─ ● ─ ●               │ ●              ●
      └─────────────────────            └─────────────────────
      
      Rigid structure                   Flexible exploration
      Misses valleys between points     Can find values anywhere
      Explores in LINES                 Explores the whole SPACE
4.4 How Random Search Works
text

STEP 1: Define the hyperparameter distributions
        ┌────────────────────────────────────────────────────┐
        │ n_estimators: uniform(50, 500)                     │
        │ max_depth: uniform_int(3, 20)                      │
        │ learning_rate: log_uniform(0.0001, 0.1)            │
        │ min_samples_split: uniform_int(2, 20)              │
        └────────────────────────────────────────────────────┘

STEP 2: Randomly sample N combinations
        ┌────────────────────────────────────────────────────┐
        │ Sample 1: n_est=287, depth=7, lr=0.023, split=12   │
        │ Sample 2: n_est=134, depth=15, lr=0.001, split=5   │
        │ Sample 3: n_est=421, depth=9, lr=0.045, split=8    │
        │ ... (continue for N samples)                        │
        └────────────────────────────────────────────────────┘

STEP 3: For each sampled combination:
        a) Train model with these hyperparameters
        b) Evaluate using cross-validation
        c) Record the score

STEP 4: Select the combination with the BEST score
4.5 Types of Distributions for Random Search
text

┌─────────────────────────────────────────────────────────────────┐
│                 PROBABILITY DISTRIBUTIONS                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  UNIFORM (continuous):                                          │
│  ─────────────────────                                          │
│  ████████████████████████████████████████                       │
│  0.0                                  1.0                       │
│  Equal probability everywhere                                   │
│  Use for: batch_size, temperature                               │
│                                                                 │
│  LOG-UNIFORM:                                                   │
│  ────────────                                                   │
│  ████████████████████████                                       │
│  ████████████████                                               │
│  ██████████                                                     │
│  ██████                                                         │
│  ███                                                            │
│  0.0001        0.001        0.01        0.1                     │
│  More samples at smaller values (logarithmic scale)             │
│  Use for: learning_rate, regularization                         │
│                                                                 │
│  UNIFORM INTEGER:                                               │
│  ─────────────────                                              │
│  ██  ██  ██  ██  ██  ██  ██  ██  ██  ██                         │
│  1   2   3   4   5   6   7   8   9  10                          │
│  Equal probability for each integer                             │
│  Use for: n_estimators, max_depth, n_layers                     │
│                                                                 │
│  CATEGORICAL:                                                   │
│  ────────────                                                   │
│  ████████  ████████  ████████                                   │
│   relu     sigmoid    tanh                                      │
│  Equal probability for each category                            │
│  Use for: activation, optimizer, kernel                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
4.6 Basic Random Search Implementation
Python

from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from scipy.stats import randint, uniform
import numpy as np

# ═══════════════════════════════════════════════════════════════
# STEP 1: Load and prepare data
# ═══════════════════════════════════════════════════════════════
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ═══════════════════════════════════════════════════════════════
# STEP 2: Define the model
# ═══════════════════════════════════════════════════════════════
model = RandomForestClassifier(random_state=42)

# ═══════════════════════════════════════════════════════════════
# STEP 3: Define hyperparameter DISTRIBUTIONS (not fixed lists!)
# ═══════════════════════════════════════════════════════════════
param_distributions = {
    # Integer uniform distribution: random integers between low and high
    'n_estimators': randint(50, 500),          # Random int between 50-500
    
    # Integer uniform distribution
    'max_depth': randint(3, 30),               # Random int between 3-30
    
    # Integer uniform distribution
    'min_samples_split': randint(2, 20),       # Random int between 2-20
    
    # Integer uniform distribution  
    'min_samples_leaf': randint(1, 10),        # Random int between 1-10
    
    # Categorical: randomly choose from list
    'max_features': ['sqrt', 'log2', None],    # Random choice
    
    # Boolean choice
    'bootstrap': [True, False]                  # Random choice
}

# ═══════════════════════════════════════════════════════════════
# STEP 4: Create RandomizedSearchCV object
# ═══════════════════════════════════════════════════════════════
random_search = RandomizedSearchCV(
    estimator=model,
    param_distributions=param_distributions,
    n_iter=100,              # Try 100 random combinations
    cv=5,                    # 5-fold cross-validation
    scoring='accuracy',
    n_jobs=-1,
    verbose=2,
    random_state=42,
    return_train_score=True
)

# ═══════════════════════════════════════════════════════════════
# STEP 5: Run Random Search
# ═══════════════════════════════════════════════════════════════
print("Starting Random Search...")
print(f"Sampling 100 random combinations from the distribution space")
print(f"With 5-fold CV: 100 × 5 = 500 model trainings\n")

random_search.fit(X_train, y_train)

# ═══════════════════════════════════════════════════════════════
# STEP 6: Analyze Results
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*60)
print("RANDOM SEARCH RESULTS")
print("="*60)

print(f"\n✅ Best Parameters Found:")
for param, value in random_search.best_params_.items():
    print(f"   {param}: {value}")

print(f"\n📊 Best Cross-Validation Score: {random_search.best_score_:.4f}")

# Test on held-out test set
test_score = random_search.best_estimator_.score(X_test, y_test)
print(f"📈 Test Set Score: {test_score:.4f}")
4.7 Log-Uniform Distribution for Learning Rate
Python

from scipy.stats import loguniform
import numpy as np

# ═══════════════════════════════════════════════════════════════
# WHY LOG-UNIFORM FOR LEARNING RATE?
# ═══════════════════════════════════════════════════════════════
"""
Learning rates typically range from 0.0001 to 0.1

If we use UNIFORM:
- 50% of samples between 0.0001 and 0.05
- 50% of samples between 0.05 and 0.1
- Most samples will be "large" learning rates!

If we use LOG-UNIFORM:
- Equal samples in each ORDER OF MAGNITUDE
- 0.0001-0.001: 25% of samples
- 0.001-0.01: 25% of samples  
- 0.01-0.1: 50% of samples
- Explores small values properly!
"""

# Example: Generate samples to see the difference
uniform_samples = uniform(0.0001, 0.1).rvs(1000)
loguniform_samples = loguniform(0.0001, 0.1).rvs(1000)

print("UNIFORM distribution:")
print(f"  Samples < 0.001: {(uniform_samples < 0.001).sum()}")
print(f"  Samples < 0.01:  {(uniform_samples < 0.01).sum()}")
print(f"  Samples < 0.1:   {(uniform_samples < 0.1).sum()}")

print("\nLOG-UNIFORM distribution:")
print(f"  Samples < 0.001: {(loguniform_samples < 0.001).sum()}")
print(f"  Samples < 0.01:  {(loguniform_samples < 0.01).sum()}")
print(f"  Samples < 0.1:   {(loguniform_samples < 0.1).sum()}")

# Use in Random Search:
param_distributions = {
    'learning_rate': loguniform(1e-5, 1e-1),  # Log-uniform from 0.00001 to 0.1
    'n_estimators': randint(50, 500),
    'max_depth': randint(3, 20),
}
4.8 Determining How Many Iterations (n_iter)
text

THE MATH BEHIND n_iter
──────────────────────

Question: How many random samples needed to find good hyperparameters?

Statistical Insight:
If you want 95% probability of finding a hyperparameter combination
that's in the top 5% of all combinations:

    n_iter >= log(1 - 0.95) / log(1 - 0.05)
    n_iter >= log(0.05) / log(0.95)
    n_iter >= 59

So with n_iter=60, you have 95% chance of finding a top-5% configuration!


PRACTICAL GUIDELINES:
─────────────────────

┌─────────────────┬──────────────┬────────────────────────────────┐
│ n_iter          │ Coverage     │ Use Case                       │
├─────────────────┼──────────────┼────────────────────────────────┤
│ 10-20           │ Quick test   │ Initial exploration            │
│ 50-100          │ Reasonable   │ Standard use case              │
│ 100-200         │ Good         │ Important model                │
│ 200-500         │ Thorough     │ Production model               │
│ 500+            │ Exhaustive   │ Research/competition           │
└─────────────────┴──────────────┴────────────────────────────────┘


FORMULA FOR COVERAGE:
─────────────────────

P(finding top-p% configuration) = 1 - (1-p)^n_iter

Example:
• n_iter=60, p=0.05 → P = 1 - 0.95^60 = 95.4%
• n_iter=100, p=0.05 → P = 1 - 0.95^100 = 99.4%
• n_iter=100, p=0.01 → P = 1 - 0.99^100 = 63.4%
4.9 Complete Random Search Implementation
Python

"""
PRODUCTION-READY RANDOM SEARCH IMPLEMENTATION
==============================================
"""

import numpy as np
import pandas as pd
from sklearn.model_selection import RandomizedSearchCV, StratifiedKFold
from sklearn.ensemble import GradientBoostingClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from scipy.stats import randint, uniform, loguniform
import time
import warnings

warnings.filterwarnings('ignore')

class RandomSearchTuner:
    """
    Professional Random Search implementation
    """
    
    def __init__(self, model, param_distributions, n_iter=100, 
                 cv=5, scoring='accuracy'):
        self.model = model
        self.param_distributions = param_distributions
        self.n_iter = n_iter
        self.cv = cv
        self.scoring = scoring
        self.random_search = None
        self.results_df = None
        
    def fit(self, X, y):
        """Run random search with detailed logging"""
        
        print("="*70)
        print("RANDOM SEARCH CONFIGURATION")
        print("="*70)
        
        print(f"\n📋 Hyperparameter Distributions:")
        for param, dist in self.param_distributions.items():
            if hasattr(dist, 'args'):
                print(f"   • {param}: {type(dist).__name__}{dist.args}")
            else:
                print(f"   • {param}: {dist}")
        
        print(f"\n📊 Search Statistics:")
        print(f"   • Random samples (n_iter): {self.n_iter}")
        print(f"   • Cross-validation folds: {self.cv}")
        print(f"   • Total model trainings: {self.n_iter * self.cv}")
        
        # Probability calculation
        p = 0.05  # Looking for top 5%
        prob = 1 - (1 - p) ** self.n_iter
        print(f"   • Probability of finding top-5% config: {prob:.1%}")
        
        print("\n" + "="*70)
        print("STARTING RANDOM SEARCH...")
        print("="*70 + "\n")
        
        start_time = time.time()
        
        self.random_search = RandomizedSearchCV(
            estimator=self.model,
            param_distributions=self.param_distributions,
            n_iter=self.n_iter,
            cv=StratifiedKFold(n_splits=self.cv, shuffle=True, random_state=42),
            scoring=self.scoring,
            n_jobs=-1,
            verbose=1,
            random_state=42,
            return_train_score=True
        )
        
        self.random_search.fit(X, y)
        
        elapsed_time = time.time() - start_time
        
        self.results_df = pd.DataFrame(self.random_search.cv_results_)
        
        print("\n" + "="*70)
        print("RANDOM SEARCH COMPLETED!")
        print("="*70)
        print(f"\n⏱️  Total time: {elapsed_time:.2f} seconds")
        print(f"\n🏆 BEST PARAMETERS FOUND:")
        for param, value in self.random_search.best_params_.items():
            print(f"   • {param}: {value}")
        print(f"\n📊 BEST CV SCORE: {self.random_search.best_score_:.4f}")
        
        return self
    
    def convergence_analysis(self):
        """Show how the best score evolved over iterations"""
        
        print("\n" + "="*70)
        print("CONVERGENCE ANALYSIS")
        print("="*70)
        
        scores = self.results_df['mean_test_score'].values
        
        # Calculate running best
        running_best = np.maximum.accumulate(scores)
        
        print("\nIteration | Current Score | Best So Far | Improved?")
        print("-" * 55)
        
        for i in range(0, len(scores), max(1, len(scores)//10)):
            improved = "  ✓" if i == 0 or running_best[i] > running_best[i-1] else ""
            print(f"    {i+1:3d}   |    {scores[i]:.4f}    |   {running_best[i]:.4f}    | {improved}")
        
        # Find when we found the best
        best_iteration = np.argmax(scores) + 1
        print(f"\n💡 Best score found at iteration: {best_iteration}")
        
        if best_iteration <= self.n_iter * 0.3:
            print("   ✅ Found optimal early - could potentially use fewer iterations")
        elif best_iteration >= self.n_iter * 0.9:
            print("   ⚠️  Found optimal late - consider using more iterations")
        else:
            print("   ✅ Found optimal in middle range - good n_iter choice")


# ═══════════════════════════════════════════════════════════════════
# USAGE EXAMPLE
# ═══════════════════════════════════════════════════════════════════

if __name__ == "__main__":
    
    # Load data
    data = load_breast_cancer()
    X, y = data.data, data.target
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y
    )
    
    # Define model and hyperparameter distributions
    model = GradientBoostingClassifier(random_state=42)
    
    param_distributions = {
        'n_estimators': randint(50, 500),
        'max_depth': randint(2, 15),
        'learning_rate': loguniform(0.001, 0.3),
        'min_samples_split': randint(2, 20),
        'min_samples_leaf': randint(1, 10),
        'subsample': uniform(0.6, 0.4),  # uniform(loc, scale) = uniform(0.6, 1.0)
        'max_features': ['sqrt', 'log2', None]
    }
    
    # Run Random Search
    tuner = RandomSearchTuner(
        model=model,
        param_distributions=param_distributions,
        n_iter=100,
        cv=5,
        scoring='accuracy'
    )
    
    tuner.fit(X_train, y_train)
    tuner.convergence_analysis()
    
    # Evaluate on test set
    best_model = tuner.random_search.best_estimator_
    test_score = best_model.score(X_test, y_test)
    print(f"\n🎯 FINAL TEST SET ACCURACY: {test_score:.4f}")
4.10 Random Search Pros and Cons
text

┌─────────────────────────────────────────────────────────────────┐
│                     RANDOM SEARCH                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✅ ADVANTAGES:                                                 │
│  ──────────────                                                 │
│  • More efficient than Grid Search for large spaces            │
│  • Can explore continuous hyperparameters better               │
│  • Fixed computational budget (you control n_iter)             │
│  • Often finds good solutions faster than Grid Search          │
│  • Not affected by unimportant hyperparameters                 │
│  • Easy to parallelize                                         │
│  • Anytime algorithm (can stop early)                          │
│                                                                 │
│  ❌ DISADVANTAGES:                                              │
│  ───────────────                                                │
│  • No guarantee to find the absolute best                      │
│  • Random - might miss optimal regions                         │
│  • Doesn't learn from previous evaluations                     │
│  • Same computation might revisit similar regions              │
│  • Results vary with random seed                               │
│                                                                 │
│  📊 COMPLEXITY:                                                 │
│  ──────────────                                                 │
│  Time = O(n_iter × cv_folds)                                   │
│                                                                 │
│  You CONTROL the budget, regardless of search space size!      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 5: Bayesian Optimization - The Intelligent Explorer
5.1 What is Bayesian Optimization?
Simple Definition: Bayesian Optimization learns from previous trials to intelligently decide which hyperparameters to try next.

Analogy: Imagine searching for treasure on a beach.

Grid Search: Dig holes in a perfect grid pattern
Random Search: Dig holes randomly
Bayesian: After each dig, analyze the sand quality and depth to predict WHERE treasure is most likely. Focus digging there!
5.2 The Core Idea
text

THE INTELLIGENT SEARCH LOOP
───────────────────────────

    ┌─────────────────────────────────────────────────────────────┐
    │                                                             │
    │  1. Build a PROBABILITY MODEL of the objective function    │
    │     (Surrogate Model)                                       │
    │                                                             │
    │  2. Use the model to find the MOST PROMISING point         │
    │     (Acquisition Function)                                  │
    │                                                             │
    │  3. Evaluate that point (train the actual model)           │
    │                                                             │
    │  4. Update the probability model with new observation      │
    │                                                             │
    │  5. Repeat until budget exhausted                          │
    │                                                             │
    └─────────────────────────────────────────────────────────────┘


VISUALIZATION:
──────────────

Iteration 1: We know nothing, try a random point
             
Objective        
Function    ???????????????????????????????
             
Surrogate   ─────────────────────────────────── (flat - no info)
Model        

Iteration 2: After 1 observation
             
Objective              ●                        
Function    ???????????│?????????????????????? (one known point)
                       │
Surrogate   ─────────~│~─────────────────────── (slight bump at known point)
Model        
             
Iteration 5: After 4 observations
             
Objective        ●           ●    ●      ●                        
Function    ?????│???????????│????│??????│???? (four known points)
                       
Surrogate   ────/\──────────/\───/\─────/\──── (learning the shape!)
Model        

Iteration 20: After 19 observations
             
Objective   The surrogate model closely approximates the true function!
             
Surrogate   ───/\───/\──/───────\───────/\──── (good approximation)
Model           ↑
                │
                Bayesian search focuses HERE (highest expected improvement)
5.3 Key Components Explained
Component 1: Surrogate Model
text

┌─────────────────────────────────────────────────────────────────┐
│                     SURROGATE MODEL                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PURPOSE: Approximate the expensive objective function         │
│           (training the ML model) with a CHEAP model           │
│                                                                 │
│  MOST COMMON: Gaussian Process (GP)                            │
│                                                                 │
│  WHAT IT DOES:                                                  │
│  • Predicts the score for ANY hyperparameter combination       │
│  • Also predicts UNCERTAINTY of that prediction                │
│  • Updates as we gather more observations                      │
│                                                                 │
│  ANALOGY:                                                       │
│  Instead of baking 1000 cakes to find the best recipe,         │
│  build a "cake quality predictor" based on ingredients.        │
│  Use it to guess which recipe will be best without baking!     │
│                                                                 │
│  OTHER OPTIONS:                                                 │
│  • Tree-structured Parzen Estimators (TPE) - used by Optuna    │
│  • Random Forest - used by SMAC                                │
│  • Bayesian Neural Networks                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Component 2: Acquisition Function
text

┌─────────────────────────────────────────────────────────────────┐
│                   ACQUISITION FUNCTION                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PURPOSE: Decide which point to try next                        │
│                                                                 │
│  THE DILEMMA: Exploration vs Exploitation                       │
│                                                                 │
│  ┌────────────────────┬────────────────────┐                    │
│  │    EXPLORATION     │   EXPLOITATION     │                    │
│  ├────────────────────┼────────────────────┤                    │
│  │ Try new areas we   │ Focus on areas     │                    │
│  │ haven't explored   │ that look good     │                    │
│  │ (high uncertainty) │ (high predicted    │                    │
│  │                    │  value)            │                    │
│  └────────────────────┴────────────────────┘                    │
│                                                                 │
│  COMMON ACQUISITION FUNCTIONS:                                  │
│                                                                 │
│  1. Expected Improvement (EI):                                  │
│     "How much improvement can we expect over current best?"     │
│     Balance: Good balance of exploration & exploitation         │
│                                                                 │
│  2. Probability of Improvement (PI):                            │
│     "What's the probability of beating current best?"           │
│     Balance: More exploitative                                  │
│                                                                 │
│  3. Upper Confidence Bound (UCB):                               │
│     "predicted_value + κ × uncertainty"                         │
│     Balance: κ controls exploration (higher = more exploration) │
│                                                                 │
│  4. Thompson Sampling:                                          │
│     "Sample from posterior and pick the best"                   │
│     Balance: Natural exploration through randomness             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Visualization of Acquisition Function
text

EXPECTED IMPROVEMENT (EI) VISUALIZATION
───────────────────────────────────────

                    Best score so far
                          │
                          ▼
Score     ████████████████████████████████
                    ↑
                Current best = 0.90

Predicted │    ●─────────●
Score     │   / \       / \
          │  /   \     /   \●────●
          │ /     \   /          \
          │/       ●─●            \
          └─────────────────────────────────
              Hyperparameter value

Uncertainty│
          │   ████                 ████
          │  ██████   ███████     ██████
          │ ████████ █████████   ████████
          └─────────────────────────────────
          High uncertainty where we haven't explored

Expected  │
Improvement│       █████
          │      ███████
          │     █████████          ████
          │    ███████████        ██████
          └─────────────────────────────────
                    ↑
                  TRY HERE NEXT!
          (High predicted score + High uncertainty)
5.4 The Complete Bayesian Optimization Algorithm
text

ALGORITHM: Bayesian Optimization

INPUT: 
    - f: objective function (model training + evaluation)
    - S: search space (hyperparameter ranges)
    - n_initial: number of initial random samples
    - n_iter: total iterations

OUTPUT:
    - x*: best hyperparameters
    - f(x*): best score

PROCEDURE:
────────────────────────────────────────────────────────────────

1. INITIALIZATION
   │
   │  // Sample n_initial random hyperparameter combinations
   │  D = {}  // Empty dataset of observations
   │  
   │  for i = 1 to n_initial:
   │      x_i = random_sample(S)         // Random hyperparameters
   │      y_i = f(x_i)                   // Train model, get score
   │      D = D ∪ {(x_i, y_i)}          // Add to observations
   │
   ▼

2. MAIN LOOP
   │
   │  for t = n_initial+1 to n_iter:
   │      
   │      // Step A: Fit surrogate model to observations
   │      model = fit_surrogate(D)       // Usually Gaussian Process
   │      
   │      // Step B: Find point that maximizes acquisition function
   │      x_next = argmax_x α(x; model)  // α = acquisition function
   │      
   │      // Step C: Evaluate objective function at that point
   │      y_next = f(x_next)             // Train actual ML model
   │      
   │      // Step D: Add new observation
   │      D = D ∪ {(x_next, y_next)}
   │
   ▼

3. RETURN BEST
   │
   │  x* = argmax_{(x,y) ∈ D} y
   │  return x*, max(y)

────────────────────────────────────────────────────────────────
5.5 Implementation with Optuna (Modern & Powerful)
Python

"""
BAYESIAN OPTIMIZATION WITH OPTUNA
==================================
Optuna uses TPE (Tree-structured Parzen Estimator) by default
"""

import optuna
from optuna.samplers import TPESampler
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# ═══════════════════════════════════════════════════════════════
# STEP 1: Load and prepare data
# ═══════════════════════════════════════════════════════════════
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# ═══════════════════════════════════════════════════════════════
# STEP 2: Define the objective function
# ═══════════════════════════════════════════════════════════════
def objective(trial):
    """
    Optuna will call this function multiple times with different
    hyperparameter suggestions. We train the model and return the score.
    """
    
    # Suggest hyperparameters
    # Optuna automatically decides what to try based on previous results!
    
    n_estimators = trial.suggest_int('n_estimators', 50, 500)
    max_depth = trial.suggest_int('max_depth', 2, 32)
    min_samples_split = trial.suggest_int('min_samples_split', 2, 20)
    min_samples_leaf = trial.suggest_int('min_samples_leaf', 1, 10)
    max_features = trial.suggest_categorical('max_features', ['sqrt', 'log2', None])
    
    # Create model with suggested hyperparameters
    model = RandomForestClassifier(
        n_estimators=n_estimators,
        max_depth=max_depth,
        min_samples_split=min_samples_split,
        min_samples_leaf=min_samples_leaf,
        max_features=max_features,
        random_state=42,
        n_jobs=-1
    )
    
    # Evaluate with cross-validation
    scores = cross_val_score(model, X_train, y_train, cv=5, scoring='accuracy')
    
    return scores.mean()

# ═══════════════════════════════════════════════════════════════
# STEP 3: Create and run the study
# ═══════════════════════════════════════════════════════════════
study = optuna.create_study(
    direction='maximize',           # We want to maximize accuracy
    sampler=TPESampler(seed=42),   # TPE = Tree-structured Parzen Estimator
    study_name='random_forest_tuning'
)

print("="*70)
print("STARTING BAYESIAN OPTIMIZATION WITH OPTUNA")
print("="*70)
print(f"\nOptimization target: Maximize accuracy")
print(f"Number of trials: 100")
print(f"Sampler: TPE (Tree-structured Parzen Estimator)\n")

study.optimize(
    objective,
    n_trials=100,
    show_progress_bar=True
)

# ═══════════════════════════════════════════════════════════════
# STEP 4: Analyze Results
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("BAYESIAN OPTIMIZATION COMPLETED!")
print("="*70)

print(f"\n🏆 BEST PARAMETERS FOUND:")
for param, value in study.best_params.items():
    print(f"   • {param}: {value}")

print(f"\n📊 BEST CV SCORE: {study.best_value:.4f}")
print(f"📈 NUMBER OF TRIALS: {len(study.trials)}")

# Train final model and evaluate on test set
best_params = study.best_params
final_model = RandomForestClassifier(**best_params, random_state=42)
final_model.fit(X_train, y_train)
test_score = final_model.score(X_test, y_test)

print(f"\n🎯 FINAL TEST SET ACCURACY: {test_score:.4f}")
5.6 Advanced Optuna Features
Python

"""
ADVANCED OPTUNA FEATURES
========================
"""

import optuna
from optuna.samplers import TPESampler
from optuna.pruners import MedianPruner
from sklearn.ensemble import GradientBoostingClassifier
from sklearn.model_selection import StratifiedKFold
import numpy as np

# ═══════════════════════════════════════════════════════════════
# FEATURE 1: Pruning (Early Stopping for Bad Trials)
# ═══════════════════════════════════════════════════════════════
def objective_with_pruning(trial):
    """
    Report intermediate values and allow Optuna to prune bad trials early
    """
    
    params = {
        'n_estimators': trial.suggest_int('n_estimators', 50, 500),
        'max_depth': trial.suggest_int('max_depth', 2, 20),
        'learning_rate': trial.suggest_float('learning_rate', 0.001, 0.3, log=True),
        'min_samples_split': trial.suggest_int('min_samples_split', 2, 20),
        'subsample': trial.suggest_float('subsample', 0.5, 1.0)
    }
    
    model = GradientBoostingClassifier(**params, random_state=42)
    
    # Cross-validation with intermediate reporting
    skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
    scores = []
    
    for fold_idx, (train_idx, val_idx) in enumerate(skf.split(X_train, y_train)):
        X_fold_train, X_fold_val = X_train[train_idx], X_train[val_idx]
        y_fold_train, y_fold_val = y_train[train_idx], y_train[val_idx]
        
        model.fit(X_fold_train, y_fold_train)
        score = model.score(X_fold_val, y_fold_val)
        scores.append(score)
        
        # Report intermediate value
        intermediate_value = np.mean(scores)
        trial.report(intermediate_value, fold_idx)
        
        # Check if trial should be pruned
        if trial.should_prune():
            raise optuna.TrialPruned()
    
    return np.mean(scores)

# Create study with pruner
study_with_pruning = optuna.create_study(
    direction='maximize',
    sampler=TPESampler(seed=42),
    pruner=MedianPruner(n_startup_trials=10, n_warmup_steps=2)
)

# study_with_pruning.optimize(objective_with_pruning, n_trials=100)


# ═══════════════════════════════════════════════════════════════
# FEATURE 2: Conditional Hyperparameters
# ═══════════════════════════════════════════════════════════════
def objective_conditional(trial):
    """
    Hyperparameters that depend on other hyperparameters
    """
    
    # Choose classifier type
    classifier_type = trial.suggest_categorical('classifier', ['rf', 'gb', 'svm'])
    
    if classifier_type == 'rf':
        params = {
            'n_estimators': trial.suggest_int('rf_n_estimators', 50, 500),
            'max_depth': trial.suggest_int('rf_max_depth', 2, 30),
        }
        model = RandomForestClassifier(**params, random_state=42)
        
    elif classifier_type == 'gb':
        params = {
            'n_estimators': trial.suggest_int('gb_n_estimators', 50, 300),
            'learning_rate': trial.suggest_float('gb_lr', 0.01, 0.3, log=True),
            'max_depth': trial.suggest_int('gb_max_depth', 2, 10),
        }
        model = GradientBoostingClassifier(**params, random_state=42)
        
    else:  # svm
        from sklearn.svm import SVC
        kernel = trial.suggest_categorical('svm_kernel', ['rbf', 'poly'])
        params = {
            'C': trial.suggest_float('svm_C', 0.1, 100, log=True),
            'kernel': kernel
        }
        if kernel == 'poly':
            params['degree'] = trial.suggest_int('svm_degree', 2, 5)
        model = SVC(**params, random_state=42)
    
    scores = cross_val_score(model, X_train, y_train, cv=5)
    return scores.mean()


# ═══════════════════════════════════════════════════════════════
# FEATURE 3: Hyperparameter Importance Analysis
# ═══════════════════════════════════════════════════════════════
def analyze_importance(study):
    """
    Analyze which hyperparameters matter most
    """
    print("\n📊 HYPERPARAMETER IMPORTANCE:")
    print("-" * 50)
    
    importances = optuna.importance.get_param_importances(study)
    
    for param, importance in importances.items():
        bar = '█' * int(importance * 40)
        print(f"  {param:25} {importance:.3f} {bar}")


# ═══════════════════════════════════════════════════════════════
# FEATURE 4: Visualization
# ═══════════════════════════════════════════════════════════════
def visualize_study(study):
    """
    Create visualizations for the optimization process
    """
    # Import visualization functions
    from optuna.visualization import (
        plot_optimization_history,
        plot_param_importances,
        plot_contour,
        plot_slice
    )
    
    # Optimization history
    fig1 = plot_optimization_history(study)
    fig1.show()
    
    # Parameter importances
    fig2 = plot_param_importances(study)
    fig2.show()
    
    # Contour plot (2D relationship)
    fig3 = plot_contour(study, params=['n_estimators', 'max_depth'])
    fig3.show()
    
    # Slice plot (1D relationship)
    fig4 = plot_slice(study)
    fig4.show()
5.7 Implementation with Scikit-Optimize (BayesSearchCV)
Python

"""
BAYESIAN OPTIMIZATION WITH SCIKIT-OPTIMIZE
==========================================
Uses Gaussian Process by default
"""

from skopt import BayesSearchCV
from skopt.space import Real, Integer, Categorical
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Define search space using skopt types
search_space = {
    'n_estimators': Integer(50, 500),
    'max_depth': Integer(2, 30),
    'min_samples_split': Integer(2, 20),
    'min_samples_leaf': Integer(1, 10),
    'max_features': Categorical(['sqrt', 'log2', None])
}

# Create BayesSearchCV
bayes_search = BayesSearchCV(
    estimator=RandomForestClassifier(random_state=42),
    search_spaces=search_space,
    n_iter=50,              # Number of iterations
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=2,
    random_state=42
)

# Run the search
print("Starting Bayesian Optimization with Scikit-Optimize...")


Bayesian Optimization
5.7 Implementation with Scikit-Optimize (Continued)
Python

"""
BAYESIAN OPTIMIZATION WITH SCIKIT-OPTIMIZE (CONTINUED)
======================================================
"""

from skopt import BayesSearchCV
from skopt.space import Real, Integer, Categorical
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import numpy as np
import time

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Define search space using skopt types
search_space = {
    'n_estimators': Integer(50, 500),
    'max_depth': Integer(2, 30),
    'min_samples_split': Integer(2, 20),
    'min_samples_leaf': Integer(1, 10),
    'max_features': Categorical(['sqrt', 'log2', None])
}

# Create BayesSearchCV
bayes_search = BayesSearchCV(
    estimator=RandomForestClassifier(random_state=42),
    search_spaces=search_space,
    n_iter=50,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=2,
    random_state=42
)

# Run the search
print("="*70)
print("STARTING BAYESIAN OPTIMIZATION WITH SCIKIT-OPTIMIZE")
print("="*70)

start_time = time.time()
bayes_search.fit(X_train, y_train)
elapsed_time = time.time() - start_time

# Results
print("\n" + "="*70)
print("BAYESIAN OPTIMIZATION COMPLETED!")
print("="*70)

print(f"\n⏱️  Total time: {elapsed_time:.2f} seconds")

print(f"\n🏆 BEST PARAMETERS FOUND:")
for param, value in bayes_search.best_params_.items():
    print(f"   • {param}: {value}")

print(f"\n📊 BEST CV SCORE: {bayes_search.best_score_:.4f}")

# Evaluate on test set
test_score = bayes_search.best_estimator_.score(X_test, y_test)
print(f"🎯 TEST SET ACCURACY: {test_score:.4f}")
5.8 Implementation with Hyperopt
Python

"""
BAYESIAN OPTIMIZATION WITH HYPEROPT
====================================
Uses TPE (Tree-structured Parzen Estimator)
"""

from hyperopt import fmin, tpe, hp, STATUS_OK, Trials
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import numpy as np

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ═══════════════════════════════════════════════════════════════
# STEP 1: Define the search space
# ═══════════════════════════════════════════════════════════════
space = {
    'n_estimators': hp.quniform('n_estimators', 50, 500, 10),  # 50 to 500, step 10
    'max_depth': hp.quniform('max_depth', 2, 30, 1),
    'min_samples_split': hp.quniform('min_samples_split', 2, 20, 1),
    'min_samples_leaf': hp.quniform('min_samples_leaf', 1, 10, 1),
    'max_features': hp.choice('max_features', ['sqrt', 'log2', None])
}

# ═══════════════════════════════════════════════════════════════
# STEP 2: Define the objective function
# ═══════════════════════════════════════════════════════════════
def objective(params):
    """
    Hyperopt MINIMIZES, so we return negative accuracy
    """
    # Convert float to int where needed
    params['n_estimators'] = int(params['n_estimators'])
    params['max_depth'] = int(params['max_depth'])
    params['min_samples_split'] = int(params['min_samples_split'])
    params['min_samples_leaf'] = int(params['min_samples_leaf'])
    
    model = RandomForestClassifier(
        **params,
        random_state=42,
        n_jobs=-1
    )
    
    scores = cross_val_score(model, X_train, y_train, cv=5, scoring='accuracy')
    
    return {
        'loss': -scores.mean(),  # Negative because hyperopt minimizes
        'status': STATUS_OK,
        'cv_scores': scores,
        'cv_mean': scores.mean(),
        'cv_std': scores.std()
    }

# ═══════════════════════════════════════════════════════════════
# STEP 3: Run optimization
# ═══════════════════════════════════════════════════════════════
trials = Trials()  # Stores history of all trials

print("="*70)
print("STARTING BAYESIAN OPTIMIZATION WITH HYPEROPT")
print("="*70)

best = fmin(
    fn=objective,
    space=space,
    algo=tpe.suggest,  # TPE algorithm
    max_evals=100,
    trials=trials,
    verbose=True
)

# ═══════════════════════════════════════════════════════════════
# STEP 4: Process results
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("HYPEROPT OPTIMIZATION COMPLETED!")
print("="*70)

# Convert best params
best_params = {
    'n_estimators': int(best['n_estimators']),
    'max_depth': int(best['max_depth']),
    'min_samples_split': int(best['min_samples_split']),
    'min_samples_leaf': int(best['min_samples_leaf']),
    'max_features': ['sqrt', 'log2', None][best['max_features']]
}

print(f"\n🏆 BEST PARAMETERS FOUND:")
for param, value in best_params.items():
    print(f"   • {param}: {value}")

# Get best score from trials
best_trial_idx = np.argmin([t['result']['loss'] for t in trials.trials])
best_score = -trials.trials[best_trial_idx]['result']['loss']
print(f"\n📊 BEST CV SCORE: {best_score:.4f}")

# Train final model
final_model = RandomForestClassifier(**best_params, random_state=42)
final_model.fit(X_train, y_train)
test_score = final_model.score(X_test, y_test)
print(f"🎯 TEST SET ACCURACY: {test_score:.4f}")

# ═══════════════════════════════════════════════════════════════
# STEP 5: Analyze optimization history
# ═══════════════════════════════════════════════════════════════
print("\n📈 OPTIMIZATION HISTORY:")
print("-" * 50)

losses = [-t['result']['loss'] for t in trials.trials]
running_best = np.maximum.accumulate(losses)

for i in range(0, len(losses), 10):
    print(f"  Trial {i+1:3d}: Current = {losses[i]:.4f}, Best so far = {running_best[i]:.4f}")
5.9 Complete Production-Ready Bayesian Optimization
Python

"""
PRODUCTION-READY BAYESIAN OPTIMIZATION
======================================
Complete implementation with all best practices
"""

import optuna
from optuna.samplers import TPESampler
from optuna.pruners import MedianPruner
import numpy as np
import pandas as pd
from sklearn.model_selection import StratifiedKFold, cross_val_score
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.svm import SVC
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import joblib
import json
import time
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)


class BayesianOptimizationTuner:
    """
    Professional Bayesian Optimization implementation with:
    - Multiple model support
    - Pruning for efficiency
    - Comprehensive logging
    - Result analysis
    - Model persistence
    """
    
    def __init__(self, model_type='random_forest', n_trials=100, cv=5, 
                 scoring='accuracy', direction='maximize'):
        self.model_type = model_type
        self.n_trials = n_trials
        self.cv = cv
        self.scoring = scoring
        self.direction = direction
        self.study = None
        self.best_model = None
        self.X_train = None
        self.y_train = None
        
    def _get_model_params(self, trial):
        """Define hyperparameter search space for each model type"""
        
        if self.model_type == 'random_forest':
            return {
                'n_estimators': trial.suggest_int('n_estimators', 50, 500),
                'max_depth': trial.suggest_int('max_depth', 2, 30),
                'min_samples_split': trial.suggest_int('min_samples_split', 2, 20),
                'min_samples_leaf': trial.suggest_int('min_samples_leaf', 1, 10),
                'max_features': trial.suggest_categorical('max_features', 
                                                          ['sqrt', 'log2', None]),
                'bootstrap': trial.suggest_categorical('bootstrap', [True, False])
            }
            
        elif self.model_type == 'gradient_boosting':
            return {
                'n_estimators': trial.suggest_int('n_estimators', 50, 500),
                'max_depth': trial.suggest_int('max_depth', 2, 15),
                'learning_rate': trial.suggest_float('learning_rate', 0.001, 0.3, 
                                                      log=True),
                'min_samples_split': trial.suggest_int('min_samples_split', 2, 20),
                'min_samples_leaf': trial.suggest_int('min_samples_leaf', 1, 10),
                'subsample': trial.suggest_float('subsample', 0.5, 1.0)
            }
            
        elif self.model_type == 'svm':
            kernel = trial.suggest_categorical('kernel', ['rbf', 'poly', 'sigmoid'])
            params = {
                'C': trial.suggest_float('C', 0.01, 100, log=True),
                'kernel': kernel,
                'gamma': trial.suggest_categorical('gamma', ['scale', 'auto'])
            }
            if kernel == 'poly':
                params['degree'] = trial.suggest_int('degree', 2, 5)
            return params
        
        else:
            raise ValueError(f"Unknown model type: {self.model_type}")
    
    def _create_model(self, params):
        """Create model instance with given parameters"""
        
        if self.model_type == 'random_forest':
            return RandomForestClassifier(**params, random_state=42, n_jobs=-1)
        elif self.model_type == 'gradient_boosting':
            return GradientBoostingClassifier(**params, random_state=42)
        elif self.model_type == 'svm':
            return SVC(**params, random_state=42)
        else:
            raise ValueError(f"Unknown model type: {self.model_type}")
    
    def _objective(self, trial):
        """Objective function for Optuna"""
        
        # Get hyperparameters
        params = self._get_model_params(trial)
        
        # Create model
        model = self._create_model(params)
        
        # Cross-validation with intermediate reporting for pruning
        skf = StratifiedKFold(n_splits=self.cv, shuffle=True, random_state=42)
        scores = []
        
        for fold_idx, (train_idx, val_idx) in enumerate(skf.split(self.X_train, 
                                                                   self.y_train)):
            X_fold_train = self.X_train[train_idx]
            X_fold_val = self.X_train[val_idx]
            y_fold_train = self.y_train[train_idx]
            y_fold_val = self.y_train[val_idx]
            
            model.fit(X_fold_train, y_fold_train)
            score = model.score(X_fold_val, y_fold_val)
            scores.append(score)
            
            # Report intermediate value for pruning
            trial.report(np.mean(scores), fold_idx)
            
            if trial.should_prune():
                raise optuna.TrialPruned()
        
        return np.mean(scores)
    
    def fit(self, X, y):
        """Run Bayesian optimization"""
        
        self.X_train = X
        self.y_train = y
        
        # Print configuration
        print("="*70)
        print("BAYESIAN OPTIMIZATION CONFIGURATION")
        print("="*70)
        print(f"\n📋 Settings:")
        print(f"   • Model type: {self.model_type}")
        print(f"   • Number of trials: {self.n_trials}")
        print(f"   • Cross-validation folds: {self.cv}")
        print(f"   • Scoring metric: {self.scoring}")
        print(f"   • Optimization direction: {self.direction}")
        print(f"   • Sampler: TPE (Tree-structured Parzen Estimator)")
        print(f"   • Pruner: Median Pruner")
        
        print("\n" + "="*70)
        print("STARTING BAYESIAN OPTIMIZATION...")
        print("="*70 + "\n")
        
        start_time = time.time()
        
        # Create study
        self.study = optuna.create_study(
            direction=self.direction,
            sampler=TPESampler(seed=42),
            pruner=MedianPruner(n_startup_trials=10, n_warmup_steps=2)
        )
        
        # Run optimization
        self.study.optimize(
            self._objective,
            n_trials=self.n_trials,
            show_progress_bar=True,
            catch=(Exception,)
        )
        
        elapsed_time = time.time() - start_time
        
        # Print results
        print("\n" + "="*70)
        print("BAYESIAN OPTIMIZATION COMPLETED!")
        print("="*70)
        
        print(f"\n⏱️  Total time: {elapsed_time:.2f} seconds ({elapsed_time/60:.2f} min)")
        print(f"📊 Trials completed: {len(self.study.trials)}")
        print(f"🗑️  Trials pruned: {len([t for t in self.study.trials if t.state == optuna.trial.TrialState.PRUNED])}")
        
        print(f"\n🏆 BEST PARAMETERS FOUND:")
        for param, value in self.study.best_params.items():
            print(f"   • {param}: {value}")
        
        print(f"\n📊 BEST CV SCORE: {self.study.best_value:.4f}")
        
        # Train final model with best parameters
        self.best_model = self._create_model(self.study.best_params)
        self.best_model.fit(X, y)
        
        return self
    
    def predict(self, X):
        """Make predictions using the best model"""
        return self.best_model.predict(X)
    
    def score(self, X, y):
        """Evaluate the best model"""
        return self.best_model.score(X, y)
    
    def get_hyperparameter_importance(self):
        """Analyze which hyperparameters matter most"""
        
        print("\n" + "="*70)
        print("HYPERPARAMETER IMPORTANCE ANALYSIS")
        print("="*70 + "\n")
        
        importances = optuna.importance.get_param_importances(self.study)
        
        for param, importance in importances.items():
            bar = '█' * int(importance * 40)
            print(f"  {param:25} {importance:.4f} {bar}")
        
        return importances
    
    def get_optimization_history(self):
        """Get the optimization history as a DataFrame"""
        
        history = []
        for trial in self.study.trials:
            if trial.state == optuna.trial.TrialState.COMPLETE:
                row = {
                    'trial_number': trial.number,
                    'value': trial.value,
                    **trial.params
                }
                history.append(row)
        
        df = pd.DataFrame(history)
        df['best_so_far'] = df['value'].cummax()
        
        return df
    
    def analyze_convergence(self):
        """Analyze when the best solution was found"""
        
        print("\n" + "="*70)
        print("CONVERGENCE ANALYSIS")
        print("="*70 + "\n")
        
        history = self.get_optimization_history()
        
        if len(history) == 0:
            print("No completed trials to analyze.")
            return
        
        best_trial = history.loc[history['value'].idxmax()]
        best_trial_number = int(best_trial['trial_number'])
        
        print(f"📍 Best score found at trial: {best_trial_number + 1} / {self.n_trials}")
        print(f"📊 Best score: {best_trial['value']:.4f}")
        
        # Show progression
        print("\n📈 Optimization Progression:")
        print("-" * 50)
        
        checkpoints = [0, 9, 24, 49, 74, 99]  # Trials 1, 10, 25, 50, 75, 100
        checkpoints = [c for c in checkpoints if c < len(history)]
        
        for idx in checkpoints:
            row = history.iloc[idx]
            print(f"  Trial {idx+1:3d}: Current = {row['value']:.4f}, "
                  f"Best so far = {row['best_so_far']:.4f}")
        
        # Efficiency analysis
        efficiency_ratio = (best_trial_number + 1) / self.n_trials
        
        print(f"\n💡 Efficiency Analysis:")
        if efficiency_ratio < 0.3:
            print(f"   ✅ Found optimal early ({efficiency_ratio:.0%} through trials)")
            print(f"   💡 Consider using fewer trials next time")
        elif efficiency_ratio > 0.8:
            print(f"   ⚠️  Found optimal late ({efficiency_ratio:.0%} through trials)")
            print(f"   💡 Consider using more trials next time")
        else:
            print(f"   ✅ Found optimal at {efficiency_ratio:.0%} through trials")
            print(f"   💡 Good balance of exploration and exploitation")
    
    def save_study(self, filepath):
        """Save the study results"""
        
        results = {
            'best_params': self.study.best_params,
            'best_value': self.study.best_value,
            'n_trials': len(self.study.trials),
            'model_type': self.model_type
        }
        
        with open(filepath, 'w') as f:
            json.dump(results, f, indent=2)
        
        print(f"✅ Study saved to {filepath}")
    
    def save_model(self, filepath):
        """Save the best model"""
        joblib.dump(self.best_model, filepath)
        print(f"✅ Best model saved to {filepath}")


# ═══════════════════════════════════════════════════════════════════
# USAGE EXAMPLE
# ═══════════════════════════════════════════════════════════════════

if __name__ == "__main__":
    
    # Load data
    data = load_breast_cancer()
    X, y = data.data, data.target
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y
    )
    
    # Run Bayesian Optimization
    tuner = BayesianOptimizationTuner(
        model_type='random_forest',
        n_trials=100,
        cv=5,
        scoring='accuracy'
    )
    
    tuner.fit(X_train, y_train)
    
    # Analysis
    tuner.get_hyperparameter_importance()
    tuner.analyze_convergence()
    
    # Evaluate on test set
    test_score = tuner.score(X_test, y_test)
    print(f"\n🎯 FINAL TEST SET ACCURACY: {test_score:.4f}")
5.10 Understanding TPE (Tree-structured Parzen Estimator)
text

┌─────────────────────────────────────────────────────────────────┐
│              TPE: HOW IT WORKS                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  KEY IDEA: Instead of modeling P(score | hyperparameters),     │
│            TPE models P(hyperparameters | good_score) and      │
│            P(hyperparameters | bad_score)                      │
│                                                                 │
│  STEP 1: Define a threshold (e.g., top 25% of scores)          │
│                                                                 │
│  STEP 2: Split observations:                                   │
│          • l(x) = P(x | y < threshold)  ← "good" trials        │
│          • g(x) = P(x | y >= threshold) ← "bad" trials         │
│                                                                 │
│  STEP 3: Sample points where l(x)/g(x) is high                 │
│          (high probability of being good,                      │
│           low probability of being bad)                        │
│                                                                 │
│                                                                 │
│  VISUALIZATION:                                                 │
│  ──────────────                                                 │
│                                                                 │
│  Hyperparameter value →                                        │
│                                                                 │
│  l(x) - "good"    ████                                         │
│  distribution:    ██████                                       │
│                   ████████                                     │
│                     ↑ Sample here!                             │
│                                                                 │
│  g(x) - "bad"           ██████████                             │
│  distribution:        ████████████████                         │
│                                                                 │
│  TPE picks points where l(x) is HIGH and g(x) is LOW!          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
5.11 Bayesian Optimization Pros and Cons
text

┌─────────────────────────────────────────────────────────────────┐
│                  BAYESIAN OPTIMIZATION                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✅ ADVANTAGES:                                                 │
│  ──────────────                                                 │
│  • LEARNS from previous evaluations (intelligent)              │
│  • Very efficient for expensive objective functions            │
│  • Handles complex search spaces well                          │
│  • Balances exploration and exploitation automatically         │
│  • Works well with small number of trials                      │
│  • Can handle conditional hyperparameters                      │
│  • Provides uncertainty estimates                              │
│  • Often finds better solutions than random search             │
│                                                                 │
│  ❌ DISADVANTAGES:                                              │
│  ───────────────                                                │
│  • More complex to implement and understand                    │
│  • Surrogate model has computational overhead                  │
│  • Can get stuck in local optima (less exploration)            │
│  • Sequential nature makes parallelization harder              │
│  • May not work well in very high dimensions (>20 params)      │
│  • Requires more sophisticated libraries                       │
│  • Sensitive to initial random samples                         │
│                                                                 │
│  📊 BEST USE CASES:                                             │
│  ──────────────────                                             │
│  • Expensive model training (deep learning, large datasets)    │
│  • Limited computational budget                                │
│  • Complex hyperparameter interactions                         │
│  • When you need the best possible model                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 6: Comparison & When to Use What
6.1 Side-by-Side Comparison
text

┌──────────────────┬────────────────┬────────────────┬────────────────┐
│     FEATURE      │  GRID SEARCH   │ RANDOM SEARCH  │   BAYESIAN     │
├──────────────────┼────────────────┼────────────────┼────────────────┤
│                  │                │                │                │
│ Search Strategy  │ Exhaustive     │ Random         │ Informed       │
│                  │                │                │                │
│ Complexity       │ Simple         │ Simple         │ Complex        │
│                  │                │                │                │
│ Efficiency       │ Low            │ Medium         │ High           │
│                  │                │                │                │
│ Parallelizable   │ Yes            │ Yes            │ Limited        │
│                  │                │                │                │
│ Guarantees       │ Best in grid   │ None           │ None           │
│                  │                │                │                │
│ Learns           │ No             │ No             │ Yes            │
│                  │                │                │                │
│ Continuous       │ Poor           │ Good           │ Excellent      │
│ Hyperparameters  │                │                │                │
│                  │                │                │                │
│ High Dimensions  │ Very Poor      │ Good           │ Moderate       │
│                  │                │                │                │
│ Small Budget     │ Poor           │ Good           │ Excellent      │
│                  │                │                │                │
│ Implementation   │ sklearn        │ sklearn        │ optuna/skopt/  │
│                  │                │                │ hyperopt       │
│                  │                │                │                │
└──────────────────┴────────────────┴────────────────┴────────────────┘
6.2 Visual Comparison of Search Patterns
text

SEARCH SPACE VISUALIZATION (2D example)
═══════════════════════════════════════

Hyperparameter 2
    ▲
    │
    │   GRID SEARCH              RANDOM SEARCH           BAYESIAN
    │   ─────────────            ─────────────           ────────
    │
    │   ● ─ ● ─ ● ─ ●            ●     ●                    ●
    │   │   │   │   │                     ●              ●     ●
    │   ● ─ ● ─ ● ─ ●            ●   ●                   ● ● ●
    │   │   │   │   │              ●   ●               ●  ●●● ●
    │   ● ─ ● ─ ● ─ ●                ●     ●           ●●●●●●●●●
    │   │   │   │   │            ●          ●            ●● ●
    │   ● ─ ● ─ ● ─ ●               ●  ●                  ●
    │
    └──────────────────────────────────────────────────────────▶
                                                    Hyperparameter 1
    
    Grid: Regular pattern        Random: Scattered        Bayesian: Clusters
    Tests every point           Tests random points       around promising areas
    in the grid                  
6.3 Time Complexity Comparison
text

NUMBER OF EVALUATIONS VS HYPERPARAMETERS
════════════════════════════════════════

Evaluations
    │
10⁶ ┤                                        ╱ Grid Search
    │                                      ╱
    │                                    ╱
10⁵ ┤                                  ╱
    │                                ╱
    │                              ╱
10⁴ ┤                            ╱
    │                          ╱
    │                        ╱
10³ ┤──────────────────────╱───────────────────── Random Search
    │                    ╱                        (fixed n_iter)
    │                  ╱
10² ┤────────────────╱───────────────────────── Bayesian
    │              ╱                             (typically fewer needed)
    │            ╱
10¹ ┤──────────╱
    │        ╱
    │      ╱
    └──────┬──────┬──────┬──────┬──────┬──────▶
           2      4      6      8     10    Hyperparameters


KEY INSIGHT:
• Grid Search: Grows EXPONENTIALLY with hyperparameters
• Random Search: You control the budget (constant)
• Bayesian: Often needs FEWER evaluations for same quality
6.4 Performance vs Budget Comparison
text

TYPICAL PERFORMANCE CURVES
══════════════════════════

Model
Performance
    │
    │                              ●●●●●●●●●●●●●● Bayesian
    │                         ●●●●●
    │                     ●●●●
    │                  ●●●
    │               ●●●        ○○○○○○○○○○○○○○○○ Random
    │            ●●●      ○○○○○
    │          ●●    ○○○○○
    │        ●●  ○○○○
    │      ●○○○○       □□□□□□□□□□□□□□□□□□□□□ Grid
    │    ○○       □□□□□                        (limited by grid)
    │  ○○    □□□□
    │ ○  □□□□
    │○□□□
    │□
    └──────────────────────────────────────────────────▶
                                              Number of Evaluations

OBSERVATIONS:
• Bayesian: Fastest to improve, highest final performance
• Random: Steady improvement, good with limited budget
• Grid: Limited by pre-defined grid values
6.5 Decision Flowchart
text

                    START: Choose Hyperparameter Tuning Method
                                      │
                                      ▼
                    ┌─────────────────────────────────┐
                    │  How many hyperparameters and   │
                    │  values do you have?            │
                    └─────────────────────────────────┘
                                      │
                    ┌─────────────────┼─────────────────┐
                    │                 │                 │
                    ▼                 ▼                 ▼
              < 100 combos     100-10,000 combos   > 10,000 combos
                    │                 │                 │
                    ▼                 ▼                 ▼
              ┌───────────┐   ┌───────────────┐   ┌───────────────┐
              │   GRID    │   │ Is training   │   │   BAYESIAN    │
              │  SEARCH   │   │ expensive?    │   │ or RANDOM     │
              └───────────┘   └───────────────┘   └───────────────┘
                                      │
                              ┌───────┴───────┐
                              │               │
                              ▼               ▼
                            Yes              No
                              │               │
                              ▼               ▼
                        ┌──────────┐   ┌──────────┐
                        │ BAYESIAN │   │  RANDOM  │
                        │          │   │  SEARCH  │
                        └──────────┘   └──────────┘


QUICK DECISION GUIDE:
─────────────────────
• Few hyperparameters, few values → GRID SEARCH
• Many hyperparameters, quick training → RANDOM SEARCH  
• Expensive training, need best results → BAYESIAN
• Don't know? → Start with RANDOM, then BAYESIAN if needed
6.6 Practical Recommendations by Scenario
text

┌─────────────────────────────────────────────────────────────────┐
│              SCENARIO-BASED RECOMMENDATIONS                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  🎓 LEARNING/PROTOTYPING                                        │
│  ─────────────────────────                                      │
│  → Random Search (n_iter=50)                                    │
│  Why: Fast, simple, good baseline                               │
│                                                                 │
│  💼 PRODUCTION MODEL (Time Available)                           │
│  ─────────────────────────────────────                          │
│  → Bayesian Optimization (n_trials=100-200)                     │
│  Why: Best results, worth the complexity                        │
│                                                                 │
│  ⚡ QUICK BASELINE                                               │
│  ────────────────                                               │
│  → Random Search (n_iter=20-30)                                 │
│  Why: Fast results, better than defaults                        │
│                                                                 │
│  🔬 RESEARCH/COMPETITION                                        │
│  ────────────────────────                                       │
│  → Bayesian + Optuna with pruning                               │
│  Why: Maximum performance, efficient resource use               │
│                                                                 │
│  📊 FEW HYPERPARAMETERS (≤3)                                    │
│  ───────────────────────────                                    │
│  → Grid Search                                                  │
│  Why: Exhaustive is feasible, guaranteed coverage               │
│                                                                 │
│  🧠 DEEP LEARNING                                               │
│  ─────────────────                                              │
│  → Bayesian with early stopping/pruning                         │
│  Why: Training is expensive, need smart search                  │
│                                                                 │
│  🔄 CONTINUOUS HYPERPARAMETERS                                  │
│  ──────────────────────────────                                 │
│  → Random Search or Bayesian (NOT Grid)                         │
│  Why: Can explore infinite values, not just predefined          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6.7 Comprehensive Comparison Code
Python

"""
COMPREHENSIVE COMPARISON: Grid vs Random vs Bayesian
=====================================================
"""

import numpy as np
import pandas as pd
import time
from sklearn.model_selection import GridSearchCV, RandomizedSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from scipy.stats import randint
import optuna
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Define consistent search space
param_grid = {
    'n_estimators': [50, 100, 150, 200, 250],
    'max_depth': [3, 5, 7, 10, 15],
    'min_samples_split': [2, 5, 10, 15],
    'min_samples_leaf': [1, 2, 4, 6]
}

param_distributions = {
    'n_estimators': randint(50, 250),
    'max_depth': randint(3, 15),
    'min_samples_split': randint(2, 15),
    'min_samples_leaf': randint(1, 6)
}

results = {}

# ═══════════════════════════════════════════════════════════════
# METHOD 1: GRID SEARCH
# ═══════════════════════════════════════════════════════════════
print("="*70)
print("1. GRID SEARCH")
print("="*70)

total_combinations = np.prod([len(v) for v in param_grid.values()])
print(f"\nTotal combinations: {total_combinations}")

start_time = time.time()

grid_search = GridSearchCV(
    RandomForestClassifier(random_state=42),
    param_grid,
    cv=5,
    scoring='accuracy',
    n_jobs=-1
)
grid_search.fit(X_train, y_train)

grid_time = time.time() - start_time
grid_score = grid_search.best_score_
grid_test_score = grid_search.best_estimator_.score(X_test, y_test)

print(f"Time: {grid_time:.2f}s")
print(f"Best CV Score: {grid_score:.4f}")
print(f"Test Score: {grid_test_score:.4f}")
print(f"Best Params: {grid_search.best_params_}")

results['Grid Search'] = {
    'time': grid_time,
    'cv_score': grid_score,
    'test_score': grid_test_score,
    'evaluations': total_combinations
}

# ═══════════════════════════════════════════════════════════════
# METHOD 2: RANDOM SEARCH (same number of evaluations)
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("2. RANDOM SEARCH")
print("="*70)

print(f"\nUsing n_iter={total_combinations} (same as grid)")

start_time = time.time()

random_search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_distributions,
    n_iter=total_combinations,  # Same budget as grid
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    random_state=42
)
random_search.fit(X_train, y_train)

random_time = time.time() - start_time
random_score = random_search.best_score_
random_test_score = random_search.best_estimator_.score(X_test, y_test)

print(f"Time: {random_time:.2f}s")
print(f"Best CV Score: {random_score:.4f}")
print(f"Test Score: {random_test_score:.4f}")
print(f"Best Params: {random_search.best_params_}")

results['Random Search'] = {
    'time': random_time,
    'cv_score': random_score,
    'test_score': random_test_score,
    'evaluations': total_combinations
}

# ═══════════════════════════════════════════════════════════════
# METHOD 3: BAYESIAN OPTIMIZATION (same number of evaluations)
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("3. BAYESIAN OPTIMIZATION (Optuna)")
print("="*70)

print(f"\nUsing n_trials={total_combinations} (same as grid)")

def objective(trial):
    params = {
        'n_estimators': trial.suggest_int('n_estimators', 50, 250),
        'max_depth': trial.suggest_int('max_depth', 3, 15),
        'min_samples_split': trial.suggest_int('min_samples_split', 2, 15),
        'min_samples_leaf': trial.suggest_int('min_samples_leaf', 1, 6)
    }
    
    model = RandomForestClassifier(**params, random_state=42, n_jobs=-1)
    from sklearn.model_selection import cross_val_score
    scores = cross_val_score(model, X_train, y_train, cv=5, scoring='accuracy')
    return scores.mean()

start_time = time.time()

study = optuna.create_study(direction='maximize', sampler=optuna.samplers.TPESampler(seed=42))
study.optimize(objective, n_trials=total_combinations, show_progress_bar=True)

bayes_time = time.time() - start_time
bayes_score = study.best_value

# Evaluate best model on test set
best_model = RandomForestClassifier(**study.best_params, random_state=42)
best_model.fit(X_train, y_train)
bayes_test_score = best_model.score(X_test, y_test)

print(f"\nTime: {bayes_time:.2f}s")
print(f"Best CV Score: {bayes_score:.4f}")
print(f"Test Score: {bayes_test_score:.4f}")
print(f"Best Params: {study.best_params}")

results['Bayesian'] = {
    'time': bayes_time,
    'cv_score': bayes_score,
    'test_score': bayes_test_score,
    'evaluations': total_combinations
}

# ═══════════════════════════════════════════════════════════════
# COMPARISON SUMMARY
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("FINAL COMPARISON")
print("="*70)

comparison_df = pd.DataFrame(results).T
comparison_df['evaluations'] = comparison_df['evaluations'].astype(int)

print("\n")
print(comparison_df.to_string())

print("\n" + "-"*70)
print("WINNER ANALYSIS:")
print("-"*70)

best_cv = comparison_df['cv_score'].idxmax()
best_test = comparison_df['test_score'].idxmax()
fastest = comparison_df['time'].idxmin()

print(f"🏆 Best CV Score:    {best_cv} ({comparison_df.loc[best_cv, 'cv_score']:.4f})")
print(f"🏆 Best Test Score:  {best_test} ({comparison_df.loc[best_test, 'test_score']:.4f})")
print(f"⚡ Fastest:          {fastest} ({comparison_df.loc[fastest, 'time']:.2f}s)")
Chapter 7: Advanced Techniques & Best Practices
7.1 Nested Cross-Validation (Proper Evaluation)
text

THE PROBLEM WITH SIMPLE CV:
═══════════════════════════

If you use the SAME data for:
1. Hyperparameter tuning (inner CV)
2. Model evaluation (outer CV)

→ You get OVERLY OPTIMISTIC results!
→ This is called "data leakage"


NESTED CV SOLUTION:
═══════════════════

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  OUTER LOOP (Model Evaluation)                                  │
│  ─────────────────────────────                                  │
│                                                                 │
│  ┌────────┬────────┬────────┬────────┬────────┐                │
│  │ TEST   │ TRAIN  │ TRAIN  │ TRAIN  │ TRAIN  │  Fold 1        │
│  │        │        │        │        │        │                │
│  │        │ INNER LOOP (Hyperparameter Tuning)│                │
│  │        │ ┌─────┬─────┬─────┬─────┐        │                │
│  │        │ │ VAL │TRAIN│TRAIN│TRAIN│        │                │
│  │        │ │TRAIN│ VAL │TRAIN│TRAIN│        │                │
│  │        │ │TRAIN│TRAIN│ VAL │TRAIN│        │                │
│  │        │ │TRAIN│TRAIN│TRAIN│ VAL │        │                │
│  │        │ └─────┴─────┴─────┴─────┘        │                │
│  │        │        │        │        │        │                │
│  └────────┴────────┴────────┴────────┴────────┘                │
│                                                                 │
│  Repeat for each outer fold...                                  │
│                                                                 │
│  Final score = Average of outer fold test scores               │
│  (This is an UNBIASED estimate of model performance!)          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

"""
NESTED CROSS-VALIDATION IMPLEMENTATION
======================================
"""

from sklearn.model_selection import cross_val_score, GridSearchCV, StratifiedKFold
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
import numpy as np

# Load data
data = load_breast_cancer()
X, y = data.data, data.target

# Define hyperparameter grid
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [3, 5, 10],
    'min_samples_split': [2, 5, 10]
}

# Outer CV (for evaluation)
outer_cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

# Inner CV (for hyperparameter tuning)
inner_cv = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)

# Model
model = RandomForestClassifier(random_state=42)

# Create GridSearchCV for inner loop
grid_search = GridSearchCV(
    estimator=model,
    param_grid=param_grid,
    cv=inner_cv,
    scoring='accuracy',
    n_jobs=-1
)

# Nested CV
print("Running Nested Cross-Validation...")
print("="*50)

nested_scores = cross_val_score(
    grid_search, 
    X, 
    y, 
    cv=outer_cv, 
    scoring='accuracy'
)

print(f"\nOuter fold scores: {nested_scores}")
print(f"\n📊 NESTED CV SCORE: {nested_scores.mean():.4f} (±{nested_scores.std():.4f})")
print("\n✅ This is an UNBIASED estimate of model generalization!")

# Compare with non-nested (biased) approach
print("\n" + "="*50)
print("COMPARISON: Non-nested (biased) approach")
print("="*50)

grid_search_simple = GridSearchCV(
    estimator=model,
    param_grid=param_grid,
    cv=5,
    scoring='accuracy',
    n_jobs=-1
)
grid_search_simple.fit(X, y)

print(f"\n⚠️  Simple CV score: {grid_search_simple.best_score_:.4f}")
print("(This is likely OVERESTIMATED due to data leakage!)")
7.2 Halving Search (Efficient Resource Allocation)
text

HALVING SEARCH CONCEPT:
═══════════════════════

Instead of fully training all hyperparameter combinations,
use progressively more resources (data/iterations) as you
eliminate poor candidates.

VISUALIZATION:
─────────────

Round 1: ALL candidates, SMALL resources
         ┌─────────────────────────────────────────────────────────┐
         │ ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ●  (16 candidates)      │
         │                                   (1/4 of data each)   │
         └─────────────────────────────────────────────────────────┘
         Keep top 50% →

Round 2: HALF candidates, MORE resources
         ┌───────────────────────────────────────┐
         │ ● ● ● ● ● ● ● ●  (8 candidates)       │
         │                   (1/2 of data each)  │
         └───────────────────────────────────────┘
         Keep top 50% →

Round 3: QUARTER candidates, EVEN MORE resources
         ┌─────────────────────────────┐
         │ ● ● ● ●  (4 candidates)     │
         │          (3/4 of data each) │
         └─────────────────────────────┘
         Keep top 50% →

Round 4: BEST candidates, FULL resources
         ┌───────────────────┐
         │ ● ●  (2 candidates)│
         │      (all data)    │
         └───────────────────┘
         Select best →  🏆
Python

"""
HALVING SEARCH IMPLEMENTATION
=============================
Available in scikit-learn 0.24+
"""

from sklearn.experimental import enable_halving_search_cv
from sklearn.model_selection import HalvingGridSearchCV, HalvingRandomSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import time

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Large parameter grid
param_grid = {
    'n_estimators': [50, 100, 150, 200, 250, 300],
    'max_depth': [3, 5, 7, 10, 15, 20],
    'min_samples_split': [2, 5, 10, 15, 20],
    'min_samples_leaf': [1, 2, 4, 6, 8]
}

total_combinations = 6 * 6 * 5 * 5  # 900 combinations!

print(f"Total combinations: {total_combinations}")
print("This would take forever with regular GridSearchCV!\n")

# ═══════════════════════════════════════════════════════════════
# METHOD 1: Halving Grid Search
# ═══════════════════════════════════════════════════════════════
print("="*60)
print("HALVING GRID SEARCH")
print("="*60)

start_time = time.time()

halving_grid = HalvingGridSearchCV(
    estimator=RandomForestClassifier(random_state=42),
    param_grid=param_grid,
    factor=3,           # Eliminate 2/3 of candidates each round
    resource='n_samples',  # Use sample size as resource
    min_resources=50,      # Minimum samples per candidate
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=1
)

halving_grid.fit(X_train, y_train)

halving_time = time.time() - start_time

print(f"\n⏱️  Time: {halving_time:.2f}s")
print(f"🏆 Best Score: {halving_grid.best_score_:.4f}")
print(f"📊 Test Score: {halving_grid.best_estimator_.score(X_test, y_test):.4f}")
print(f"🔧 Best Params: {halving_grid.best_params_}")

# ═══════════════════════════════════════════════════════════════
# METHOD 2: Halving Random Search
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*60)
print("HALVING RANDOM SEARCH")
print("="*60)

from scipy.stats import randint

param_distributions = {
    'n_estimators': randint(50, 300),
    'max_depth': randint(3, 20),
    'min_samples_split': randint(2, 20),
    'min_samples_leaf': randint(1, 8)
}

start_time = time.time()

halving_random = HalvingRandomSearchCV(
    estimator=RandomForestClassifier(random_state=42),
    param_distributions=param_distributions,
    n_candidates=100,   # Start with 100 random candidates
    factor=3,
    resource='n_samples',
    min_resources=50,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=1,
    random_state=42
)

halving_random.fit(X_train, y_train)

halving_random_time = time.time() - start_time

print(f"\n⏱️  Time: {halving_random_time:.2f}s")
print(f"🏆 Best Score: {halving_random.best_score_:.4f}")
print(f"📊 Test Score: {halving_random.best_estimator_.score(X_test, y_test):.4f}")
print(f"🔧 Best Params: {halving_random.best_params_}")
7.3 Multi-Fidelity Optimization (Early Stopping)
text

MULTI-FIDELITY CONCEPT:
═══════════════════════

Idea: Don't fully train models that are clearly bad!

Example with neural networks:
─────────────────────────────

Hyperparameters A: After 10 epochs → accuracy 45%  ❌ Stop early!
Hyperparameters B: After 10 epochs → accuracy 72%  ✓ Continue
Hyperparameters C: After 10 epochs → accuracy 38%  ❌ Stop early!
Hyperparameters D: After 10 epochs → accuracy 75%  ✓ Continue

Hyperparameters B: After 50 epochs → accuracy 84%  ✓ Continue
Hyperparameters D: After 50 epochs → accuracy 81%  ❌ Stop!

Hyperparameters B: After 100 epochs → accuracy 91%  🏆 WINNER!

Savings: Didn't fully train A, C, or D!
Python

"""
MULTI-FIDELITY OPTIMIZATION WITH OPTUNA
========================================
Using pruning for early stopping of bad trials
"""

import optuna
from optuna.pruners import HyperbandPruner, MedianPruner
import numpy as np
from sklearn.neural_network import MLPClassifier
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Load and prepare data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Scale features (important for neural networks)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Further split for validation
X_train_final, X_val, y_train_final, y_val = train_test_split(
    X_train_scaled, y_train, test_size=0.2, random_state=42
)

def objective(trial):
    """
    Objective function with intermediate reporting for pruning
    """
    
    # Suggest hyperparameters
    n_layers = trial.suggest_int('n_layers', 1, 3)
    hidden_layer_sizes = tuple(
        trial.suggest_int(f'n_units_l{i}', 16, 256) 
        for i in range(n_layers)
    )
    learning_rate_init = trial.suggest_float('learning_rate', 1e-5, 1e-1, log=True)
    alpha = trial.suggest_float('alpha', 1e-6, 1e-1, log=True)
    
    # Train with increasing number of epochs
    max_epochs = 200
    checkpoint_epochs = [10, 25, 50, 100, 200]
    
    model = MLPClassifier(
        hidden_layer_sizes=hidden_layer_sizes,
        learning_rate_init=learning_rate_init,
        alpha=alpha,
        max_iter=1,  # We'll iterate manually
        warm_start=True,
        random_state=42
    )
    
    for step, n_epochs in enumerate(checkpoint_epochs):
        # Train up to this checkpoint
        while model.n_iter_ < n_epochs:
            model.partial_fit(X_train_final, y_train_final, classes=[0, 1])
        
        # Report intermediate value
        val_score = model.score(X_val, y_val)
        trial.report(val_score, step)
        
        # Check if should prune
        if trial.should_prune():
            raise optuna.TrialPruned()
    
    return model.score(X_val, y_val)


# Create study with Hyperband pruner (state-of-the-art)
study = optuna.create_study(
    direction='maximize',
    pruner=HyperbandPruner(
        min_resource=1,
        max_resource=5,  # 5 checkpoints
        reduction_factor=3
    )
)

print("="*70)
print("MULTI-FIDELITY OPTIMIZATION WITH EARLY STOPPING")
print("="*70)
print("\nUsing Hyperband pruner for efficient search...")

study.optimize(objective, n_trials=50, show_progress_bar=True)

# Results
print("\n" + "="*70)
print("RESULTS")
print("="*70)

n_pruned = len([t for t in study.trials if t.state == optuna.trial.TrialState.PRUNED])
n_complete = len([t for t in study.trials if t.state == optuna.trial.TrialState.COMPLETE])

print(f"\n📊 Trials completed: {n_complete}")
print(f"🗑️  Trials pruned (early stopped): {n_pruned}")
print(f"💰 Resources saved: {n_pruned / len(study.trials) * 100:.1f}%")

print(f"\n🏆 Best validation score: {study.best_value:.4f}")
print(f"🔧 Best parameters:")
for key, value in study.best_params.items():
    print(f"   • {key}: {value}")
7.4 Pipeline Integration
Python

"""
HYPERPARAMETER TUNING WITH PIPELINES
=====================================
Tune preprocessing + model hyperparameters together
"""

from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler, MinMaxScaler
from sklearn.decomposition import PCA
from sklearn.feature_selection import SelectKBest, f_classif
from sklearn.ensemble import RandomForestClassifier
from sklearn.svm import SVC
from sklearn.model_selection import GridSearchCV, RandomizedSearchCV
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from scipy.stats import randint, uniform

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ═══════════════════════════════════════════════════════════════
# Example 1: Simple Pipeline
# ═══════════════════════════════════════════════════════════════
print("="*70)
print("EXAMPLE 1: SIMPLE PIPELINE (Scaler + Classifier)")
print("="*70)

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(random_state=42))
])

# Parameters are named as: step_name__parameter_name
param_grid = {
    'classifier__n_estimators': [50, 100, 200],
    'classifier__max_depth': [5, 10, 15],
    'classifier__min_samples_split': [2, 5, 10]
}

grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring='accuracy', n_jobs=-1)
grid_search.fit(X_train, y_train)

print(f"\n🏆 Best Score: {grid_search.best_score_:.4f}")
print(f"📊 Test Score: {grid_search.best_estimator_.score(X_test, y_test):.4f}")

# ═══════════════════════════════════════════════════════════════
# Example 2: Complex Pipeline with Multiple Options
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("EXAMPLE 2: COMPLEX PIPELINE (Multiple Scalers + Feature Selection)")
print("="*70)

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('feature_selection', SelectKBest(f_classif)),
    ('classifier', SVC(random_state=42))
])

# Tune preprocessing AND model together
param_grid = [
    # Configuration 1: StandardScaler + SVC with RBF
    {
        'scaler': [StandardScaler()],
        'feature_selection__k': [10, 15, 20, 'all'],
        'classifier__C': [0.1, 1, 10],
        'classifier__kernel': ['rbf'],
        'classifier__gamma': ['scale', 'auto']
    },
    # Configuration 2: MinMaxScaler + SVC with Linear
    {
        'scaler': [MinMaxScaler()],
        'feature_selection__k': [10, 15, 20, 'all'],
        'classifier__C': [0.1, 1, 10],
        'classifier__kernel': ['linear']
    }
]

grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring='accuracy', n_jobs=-1)
grid_search.fit(X_train, y_train)

print(f"\n🏆 Best Score: {grid_search.best_score_:.4f}")
print(f"📊 Test Score: {grid_search.best_estimator_.score(X_test, y_test):.4f}")
print(f"\n🔧 Best Pipeline:")
for step_name, step in grid_search.best_estimator_.steps:
    print(f"   • {step_name}: {step}")

# ═══════════════════════════════════════════════════════════════
# Example 3: Pipeline with Optuna
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("EXAMPLE 3: PIPELINE WITH OPTUNA (Full Flexibility)")
print("="*70)

import optuna
from sklearn.model_selection import cross_val_score

def objective(trial):
    # Suggest scaler
    scaler_name = trial.suggest_categorical('scaler', ['standard', 'minmax', 'none'])
    
    if scaler_name == 'standard':
        scaler = StandardScaler()
    elif scaler_name == 'minmax':
        scaler = MinMaxScaler()
    else:
        scaler = 'passthrough'
    
    # Suggest feature selection
    use_pca = trial.suggest_categorical('use_pca', [True, False])
    
    if use_pca:
        n_components = trial.suggest_int('pca_components', 5, 20)
        feature_step = ('pca', PCA(n_components=n_components))
    else:
        k = trial.suggest_int('selectk', 5, 30)
        feature_step = ('select', SelectKBest(f_classif, k=k))
    
    # Suggest classifier
    classifier_name = trial.suggest_categorical('classifier', ['rf', 'svc'])
    
    if classifier_name == 'rf':
        classifier = RandomForestClassifier(
            n_estimators=trial.suggest_int('rf_n_estimators', 50, 300),
            max_depth=trial.suggest_int('rf_max_depth', 3, 20),
            random_state=42
        )
    else:
        classifier = SVC(
            C=trial.suggest_float('svc_C', 0.01, 100, log=True),
            kernel=trial.suggest_categorical('svc_kernel', ['rbf', 'linear']),
            random_state=42
        )
    
    # Build pipeline
    pipeline = Pipeline([
        ('scaler', scaler),
        feature_step,
        ('classifier', classifier)
    ])
    
    # Evaluate
    scores = cross_val_score(pipeline, X_train, y_train, cv=5, scoring='accuracy')
    return scores.mean()

study = optuna.create_study(direction='maximize')
study.optimize(objective, n_trials=50, show_progress_bar=True)

print(f"\n🏆 Best Score: {study.best_value:.4f}")
print(f"🔧 Best Configuration: {study.best_params}")
7.5 Warm Starting and Transfer Learning for Hyperparameters
Python

"""
WARM STARTING: Use previous search results
==========================================
"""

import optuna
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

def objective(trial):
    params = {
        'n_estimators': trial.suggest_int('n_estimators', 50, 500),
        'max_depth': trial.suggest_int('max_depth', 2, 30),
        'min_samples_split': trial.suggest_int('min_samples_split', 2, 20),
    }
    model = RandomForestClassifier(**params, random_state=42)
    scores = cross_val_score(model, X_train, y_train, cv=5)
    return scores.mean()

# ═══════════════════════════════════════════════════════════════
# Method 1: Save and load study
# ═══════════════════════════════════════════════════════════════
print("="*70)
print("WARM STARTING WITH OPTUNA")
print("="*70)

# First search session
study = optuna.create_study(
    direction='maximize',
    study_name='rf_tuning',
    storage='sqlite:///rf_tuning.db',  # Persist to database
    load_if_exists=True
)

print("\nSession 1: Running 30 trials...")
study.optimize(objective, n_trials=30, show_progress_bar=True)
print(f"Best so far: {study.best_value:.4f}")

# Later... continue from where we left off
print("\nSession 2: Running 30 more trials (warm start)...")
study.optimize(objective, n_trials=30, show_progress_bar=True)
print(f"Best after warm start: {study.best_value:.4f}")

# ═══════════════════════════════════════════════════════════════
# Method 2: Enqueue known good hyperparameters
# ═══════════════════════════════════════════════════════════════
print("\n" + "="*70)
print("SEEDING WITH KNOWN GOOD HYPERPARAMETERS")
print("="*70)

new_study = optuna.create_study(direction='maximize')

# Add known good configurations (from literature or previous experiments)
new_study.enqueue_trial({
    'n_estimators': 100,
    'max_depth': 10,
    'min_samples_split': 2
})

new_study.enqueue_trial({
    'n_estimators': 200,
    'max_depth': 15,
    'min_samples_split': 5
})

print("Enqueued 2 known good configurations")
print("Running optimization (will try these first)...")

new_study.optimize(objective, n_trials=50, show_progress_bar=True)
print(f"Best score: {new_study.best_value:.4f}")
7.6 Best Practices Summary
text

┌─────────────────────────────────────────────────────────────────┐
│                      BEST PRACTICES                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📊 DATA HANDLING                                               │
│  ─────────────────                                              │
│  ✓ Always use separate test set (never tune on it!)           │
│  ✓ Use stratified splits for classification                   │
│  ✓ Consider nested CV for unbiased evaluation                 │
│  ✓ Scale features when using distance-based methods           │
│                                                                 │
│  🎯 SEARCH STRATEGY                                             │
│  ──────────────────                                             │
│  ✓ Start with Random Search for exploration                   │
│  ✓ Use Bayesian for refinement                                │
│  ✓ Use log-scale for learning rates, regularization           │
│  ✓ Consider halving search for large search spaces            │
│                                                                 │
│  ⏱️ EFFICIENCY                                                  │
│  ────────────                                                   │
│  ✓ Use early stopping / pruning                                │
│  ✓ Start with small data subset                                │
│  ✓ Parallelize when possible (n_jobs=-1)                       │
│  ✓ Use warm starting for iterative refinement                 │
│                                                                 │
│  📈 EVALUATION                                                  │
│  ─────────────                                                  │
│  ✓ Use cross-validation (not single split)                    │
│  ✓ Check for overfitting (train vs val gap)                   │
│  ✓ Consider multiple metrics                                   │
│  ✓ Report confidence intervals (std)                          │
│                                                                 │
│  🔧 HYPERPARAMETERS                                             │
│  ──────────────────                                             │
│  ✓ Start with default values as baseline                      │
│  ✓ Focus on most important hyperparameters first              │
│  ✓ Use domain knowledge to set reasonable ranges              │
│  ✓ Analyze hyperparameter importance after tuning             │
│                                                                 │
│  📝 REPRODUCIBILITY                                             │
│  ──────────────────                                             │
│  ✓ Set random seeds                                            │
│  ✓ Log all hyperparameters tried                              │
│  ✓ Save best model and configuration                          │
│  ✓ Document the search process                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 8: Real-World Projects & Case Studies
8.1 Case Study 1: XGBoost for Tabular Data
Python

"""
CASE STUDY 1: COMPLETE XGBOOST TUNING
=====================================
Kaggle-style hyperparameter optimization
"""

import numpy as np
import pandas as pd
from xgboost import XGBClassifier
from sklearn.model_selection import StratifiedKFold, cross_val_score
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
import optuna
from optuna.samplers import TPESampler
from optuna.pruners import MedianPruner
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print("="*70)
print("CASE STUDY: COMPLETE XGBOOST TUNING")
print("="*70)

# ═══════════════════════════════════════════════════════════════
# PHASE 1: Quick baseline with defaults
# ═══════════════════════════════════════════════════════════════
print("\n📍 PHASE 1: Baseline (Default Parameters)")
print("-"*50)

baseline_model = XGBClassifier(random_state=42, use_label_encoder=False, eval_metric='logloss')
baseline_scores = cross_val_score(baseline_model, X_train, y_train, cv=5, scoring='accuracy')
print(f"Baseline CV Score: {baseline_scores.mean():.4f} (±{baseline_scores.std():.4f})")

# ═══════════════════════════════════════════════════════════════
# PHASE 2: Coarse search with Random Search
# ═══════════════════════════════════════════════════════════════
print("\n📍 PHASE 2: Coarse Search (Random Search)")
print("-"*50)

from scipy.stats import randint, uniform
from sklearn.model_selection import RandomizedSearchCV

param_distributions = {
    'n_estimators': randint(50, 500),
    'max_depth': randint(2, 15),
    'learning_rate': uniform(0.01, 0.29),  # 0.01 to 0.30
    'subsample': uniform(0.5, 0.5),        # 0.5 to 1.0
    'colsample_bytree': uniform(0.5, 0.5), # 0.5 to 1.0
    'min_child_weight': randint(1, 10),
    'gamma': uniform(0, 0.5)
}

random_search = RandomizedSearchCV(
    XGBClassifier(random_state=42, use_label_encoder=False, eval_metric='logloss'),
    param_distributions,
    n_iter=30,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    random_state=42
)
random_search.fit(X_train, y_train)

print(f"Coarse Search CV Score: {random_search.best_score_:.4f}")
print(f"Best params found: {random_search.best_params_}")

# ═══════════════════════════════════════════════════════════════
# PHASE 3: Fine-tuning with Bayesian Optimization
# ═══════════════════════════════════════════════════════════════
print("\n📍 PHASE 3: Fine-Tuning (Bayesian Optimization)")
print("-"*50)

# Get the best values from coarse search and narrow the ranges
best_params = random_search.best_params_

def objective(trial):
    params = {
        'n_estimators': trial.suggest_int('n_estimators', 
            max(50, best_params['n_estimators'] - 100),
            min(500, best_params['n_estimators'] + 100)
        ),
        'max_depth': trial.suggest_int('max_depth',
            max(2, best_params['max_depth'] - 3),
            min(15, best_params['max_depth'] + 3)
        ),
        'learning_rate': trial.suggest_float('learning_rate',
            max(0.01, best_params['learning_rate'] - 0.05),
            min(0.3, best_params['learning_rate'] + 0.05)
        ),
        'subsample': trial.suggest_float('subsample',
            max(0.5, best_params['subsample'] - 0.1),
            min(1.0, best_params['subsample'] + 0.1)
        ),
        'colsample_bytree': trial.suggest_float('colsample_bytree',
            max(0.5, best_params['colsample_bytree'] - 0.1),
            min(1.0, best_params['colsample_bytree'] + 0.1)


Real-World Projects & Case Studies
8.1 Case Study 1: XGBoost for Tabular Data (Continued)
Python

"""
CASE STUDY 1: COMPLETE XGBOOST TUNING (CONTINUED)
=================================================
"""

        ),
        'min_child_weight': trial.suggest_int('min_child_weight',
            max(1, best_params['min_child_weight'] - 2),
            min(10, best_params['min_child_weight'] + 2)
        ),
        'gamma': trial.suggest_float('gamma',
            max(0, best_params['gamma'] - 0.1),
            min(0.5, best_params['gamma'] + 0.1)
        ),
        # Additional regularization parameters
        'reg_alpha': trial.suggest_float('reg_alpha', 1e-8, 1.0, log=True),
        'reg_lambda': trial.suggest_float('reg_lambda', 1e-8, 1.0, log=True)
    }
    
    model = XGBClassifier(
        **params,
        random_state=42,
        use_label_encoder=False,
        eval_metric='logloss'
    )
    
    scores = cross_val_score(model, X_train, y_train, cv=5, scoring='accuracy')
    return scores.mean()

study = optuna.create_study(
    direction='maximize',
    sampler=TPESampler(seed=42),
    pruner=MedianPruner()
)

study.optimize(objective, n_trials=50, show_progress_bar=True)

print(f"\nFine-tuned CV Score: {study.best_value:.4f}")
print(f"Best params: {study.best_params}")

# ═══════════════════════════════════════════════════════════════
# PHASE 4: Final evaluation
# ═══════════════════════════════════════════════════════════════
print("\n📍 PHASE 4: Final Evaluation")
print("-"*50)

# Train final model with best parameters
final_model = XGBClassifier(
    **study.best_params,
    random_state=42,
    use_label_encoder=False,
    eval_metric='logloss'
)
final_model.fit(X_train, y_train)

# Evaluate on test set
test_score = final_model.score(X_test, y_test)

print(f"\n{'='*50}")
print("FINAL RESULTS SUMMARY")
print(f"{'='*50}")
print(f"Baseline CV Score:     {baseline_scores.mean():.4f}")
print(f"Coarse Search Score:   {random_search.best_score_:.4f}")
print(f"Fine-tuned CV Score:   {study.best_value:.4f}")
print(f"Final Test Score:      {test_score:.4f}")
print(f"\n🎯 Improvement over baseline: +{(study.best_value - baseline_scores.mean())*100:.2f}%")

# Feature importance analysis
print("\n📊 Top 10 Feature Importances:")
feature_importance = pd.DataFrame({
    'feature': [f'feature_{i}' for i in range(X.shape[1])],
    'importance': final_model.feature_importances_
}).sort_values('importance', ascending=False).head(10)

for idx, row in feature_importance.iterrows():
    bar = '█' * int(row['importance'] * 50)
    print(f"  {row['feature']:15} {row['importance']:.4f} {bar}")
8.2 Case Study 2: Neural Network Hyperparameter Tuning
Python

"""
CASE STUDY 2: NEURAL NETWORK TUNING WITH KERAS
==============================================
Complete deep learning hyperparameter optimization
"""

import numpy as np
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout, BatchNormalization
from tensorflow.keras.optimizers import Adam, SGD, RMSprop
from tensorflow.keras.callbacks import EarlyStopping, ReduceLROnPlateau
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import optuna
from optuna.integration import TFKerasPruningCallback
import warnings

warnings.filterwarnings('ignore')
tf.get_logger().setLevel('ERROR')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# Load and prepare data
data = load_breast_cancer()
X, y = data.data, data.target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)
X_train, X_val, y_train, y_val = train_test_split(
    X_train, y_train, test_size=0.2, random_state=42, stratify=y_train
)

# Scale features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_val = scaler.transform(X_val)
X_test = scaler.transform(X_test)

print("="*70)
print("CASE STUDY: NEURAL NETWORK HYPERPARAMETER TUNING")
print("="*70)
print(f"\nData shapes:")
print(f"  Train: {X_train.shape}")
print(f"  Val:   {X_val.shape}")
print(f"  Test:  {X_test.shape}")

def create_model(trial):
    """
    Create a neural network with hyperparameters suggested by Optuna
    """
    
    # Architecture hyperparameters
    n_layers = trial.suggest_int('n_layers', 1, 4)
    
    model = Sequential()
    
    for i in range(n_layers):
        # Number of units in each layer
        n_units = trial.suggest_int(f'n_units_layer_{i}', 16, 256)
        
        if i == 0:
            model.add(Dense(n_units, input_shape=(X_train.shape[1],)))
        else:
            model.add(Dense(n_units))
        
        # Activation function
        activation = trial.suggest_categorical(f'activation_{i}', ['relu', 'elu', 'selu'])
        model.add(keras.layers.Activation(activation))
        
        # Batch normalization
        use_bn = trial.suggest_categorical(f'use_bn_{i}', [True, False])
        if use_bn:
            model.add(BatchNormalization())
        
        # Dropout
        dropout_rate = trial.suggest_float(f'dropout_{i}', 0.0, 0.5)
        if dropout_rate > 0:
            model.add(Dropout(dropout_rate))
    
    # Output layer
    model.add(Dense(1, activation='sigmoid'))
    
    # Optimizer hyperparameters
    optimizer_name = trial.suggest_categorical('optimizer', ['adam', 'sgd', 'rmsprop'])
    learning_rate = trial.suggest_float('learning_rate', 1e-5, 1e-2, log=True)
    
    if optimizer_name == 'adam':
        optimizer = Adam(learning_rate=learning_rate)
    elif optimizer_name == 'sgd':
        momentum = trial.suggest_float('momentum', 0.0, 0.99)
        optimizer = SGD(learning_rate=learning_rate, momentum=momentum)
    else:
        optimizer = RMSprop(learning_rate=learning_rate)
    
    model.compile(
        optimizer=optimizer,
        loss='binary_crossentropy',
        metrics=['accuracy']
    )
    
    return model

def objective(trial):
    """
    Objective function for Optuna
    """
    
    # Clear session to free memory
    keras.backend.clear_session()
    
    # Create model
    model = create_model(trial)
    
    # Training hyperparameters
    batch_size = trial.suggest_categorical('batch_size', [16, 32, 64, 128])
    epochs = 100
    
    # Callbacks
    callbacks = [
        EarlyStopping(
            monitor='val_loss',
            patience=10,
            restore_best_weights=True
        ),
        TFKerasPruningCallback(trial, 'val_accuracy')  # Optuna pruning
    ]
    
    # Train
    history = model.fit(
        X_train, y_train,
        validation_data=(X_val, y_val),
        epochs=epochs,
        batch_size=batch_size,
        callbacks=callbacks,
        verbose=0
    )
    
    # Return best validation accuracy
    return max(history.history['val_accuracy'])

# Run optimization
print("\n🚀 Starting Neural Network Optimization...")
print("-"*50)

study = optuna.create_study(
    direction='maximize',
    sampler=optuna.samplers.TPESampler(seed=42),
    pruner=optuna.pruners.MedianPruner(n_startup_trials=5, n_warmup_steps=10)
)

study.optimize(
    objective, 
    n_trials=50, 
    show_progress_bar=True,
    catch=(Exception,)
)

# Results
print("\n" + "="*70)
print("OPTIMIZATION RESULTS")
print("="*70)

print(f"\n🏆 Best Validation Accuracy: {study.best_value:.4f}")
print(f"\n🔧 Best Hyperparameters:")
for key, value in study.best_params.items():
    print(f"   • {key}: {value}")

# Train final model with best parameters
print("\n📊 Training Final Model...")

keras.backend.clear_session()
final_model = create_model(study.best_trial)

history = final_model.fit(
    X_train, y_train,
    validation_data=(X_val, y_val),
    epochs=100,
    batch_size=study.best_params['batch_size'],
    callbacks=[EarlyStopping(monitor='val_loss', patience=10, restore_best_weights=True)],
    verbose=0
)

# Final evaluation
test_loss, test_accuracy = final_model.evaluate(X_test, y_test, verbose=0)

print(f"\n🎯 FINAL TEST ACCURACY: {test_accuracy:.4f}")

# Hyperparameter importance
print("\n📈 Hyperparameter Importance:")
importances = optuna.importance.get_param_importances(study)
for param, importance in list(importances.items())[:10]:
    bar = '█' * int(importance * 40)
    print(f"   {param:25} {importance:.4f} {bar}")
8.3 Case Study 3: Multi-Model Comparison
Python

"""
CASE STUDY 3: MULTI-MODEL HYPERPARAMETER TUNING
===============================================
Compare multiple models with their best hyperparameters
"""

import numpy as np
import pandas as pd
from sklearn.ensemble import (
    RandomForestClassifier, 
    GradientBoostingClassifier,
    AdaBoostClassifier,
    ExtraTreesClassifier
)
from sklearn.svm import SVC
from sklearn.neighbors import KNeighborsClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.neural_network import MLPClassifier
from sklearn.model_selection import cross_val_score, StratifiedKFold
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import optuna
import time
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# Load data
data = load_breast_cancer()
X, y = data.data, data.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Scale features (needed for some models)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print("="*70)
print("CASE STUDY: MULTI-MODEL HYPERPARAMETER TUNING")
print("="*70)

# Define model configurations
MODEL_CONFIGS = {
    'Random Forest': {
        'model_class': RandomForestClassifier,
        'needs_scaling': False,
        'param_space': lambda trial: {
            'n_estimators': trial.suggest_int('n_estimators', 50, 300),
            'max_depth': trial.suggest_int('max_depth', 3, 20),
            'min_samples_split': trial.suggest_int('min_samples_split', 2, 20),
            'min_samples_leaf': trial.suggest_int('min_samples_leaf', 1, 10),
            'max_features': trial.suggest_categorical('max_features', ['sqrt', 'log2', None])
        }
    },
    'Gradient Boosting': {
        'model_class': GradientBoostingClassifier,
        'needs_scaling': False,
        'param_space': lambda trial: {
            'n_estimators': trial.suggest_int('n_estimators', 50, 300),
            'max_depth': trial.suggest_int('max_depth', 2, 10),
            'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.3, log=True),
            'subsample': trial.suggest_float('subsample', 0.5, 1.0),
            'min_samples_split': trial.suggest_int('min_samples_split', 2, 20)
        }
    },
    'SVM': {
        'model_class': SVC,
        'needs_scaling': True,
        'param_space': lambda trial: {
            'C': trial.suggest_float('C', 0.01, 100, log=True),
            'kernel': trial.suggest_categorical('kernel', ['rbf', 'poly', 'sigmoid']),
            'gamma': trial.suggest_categorical('gamma', ['scale', 'auto'])
        }
    },
    'KNN': {
        'model_class': KNeighborsClassifier,
        'needs_scaling': True,
        'param_space': lambda trial: {
            'n_neighbors': trial.suggest_int('n_neighbors', 1, 30),
            'weights': trial.suggest_categorical('weights', ['uniform', 'distance']),
            'metric': trial.suggest_categorical('metric', ['euclidean', 'manhattan', 'minkowski'])
        }
    },
    'Logistic Regression': {
        'model_class': LogisticRegression,
        'needs_scaling': True,
        'param_space': lambda trial: {
            'C': trial.suggest_float('C', 0.001, 100, log=True),
            'penalty': trial.suggest_categorical('penalty', ['l1', 'l2']),
            'solver': 'saga',
            'max_iter': 1000
        }
    },
    'MLP': {
        'model_class': MLPClassifier,
        'needs_scaling': True,
        'param_space': lambda trial: {
            'hidden_layer_sizes': (
                trial.suggest_int('layer1', 32, 256),
                trial.suggest_int('layer2', 16, 128)
            ),
            'learning_rate_init': trial.suggest_float('lr', 0.0001, 0.1, log=True),
            'alpha': trial.suggest_float('alpha', 0.00001, 0.1, log=True),
            'max_iter': 500
        }
    }
}

def tune_model(model_name, config, n_trials=30):
    """Tune a single model using Optuna"""
    
    X_train_use = X_train_scaled if config['needs_scaling'] else X_train
    
    def objective(trial):
        params = config['param_space'](trial)
        model = config['model_class'](**params, random_state=42)
        scores = cross_val_score(model, X_train_use, y_train, cv=5, scoring='accuracy')
        return scores.mean()
    
    study = optuna.create_study(direction='maximize', sampler=optuna.samplers.TPESampler(seed=42))
    study.optimize(objective, n_trials=n_trials, show_progress_bar=False)
    
    return study.best_value, study.best_params, study

# Run tuning for all models
results = {}

print("\n🔄 Tuning all models...")
print("-"*70)

for model_name, config in MODEL_CONFIGS.items():
    print(f"\n📍 Tuning {model_name}...", end=" ")
    start_time = time.time()
    
    best_score, best_params, study = tune_model(model_name, config, n_trials=30)
    
    elapsed = time.time() - start_time
    print(f"Done! (CV: {best_score:.4f}, Time: {elapsed:.1f}s)")
    
    # Train best model and evaluate on test set
    X_train_use = X_train_scaled if config['needs_scaling'] else X_train
    X_test_use = X_test_scaled if config['needs_scaling'] else X_test
    
    best_model = config['model_class'](**best_params, random_state=42)
    best_model.fit(X_train_use, y_train)
    test_score = best_model.score(X_test_use, y_test)
    
    results[model_name] = {
        'cv_score': best_score,
        'test_score': test_score,
        'best_params': best_params,
        'time': elapsed
    }

# Create comparison table
print("\n" + "="*70)
print("FINAL COMPARISON")
print("="*70)

comparison_df = pd.DataFrame({
    'Model': results.keys(),
    'CV Score': [r['cv_score'] for r in results.values()],
    'Test Score': [r['test_score'] for r in results.values()],
    'Time (s)': [r['time'] for r in results.values()]
}).sort_values('Test Score', ascending=False)

print("\n")
print(comparison_df.to_string(index=False))

# Winner
winner = comparison_df.iloc[0]['Model']
winner_score = comparison_df.iloc[0]['Test Score']

print("\n" + "-"*70)
print(f"🏆 WINNER: {winner} with Test Score: {winner_score:.4f}")
print(f"\n🔧 Best Parameters for {winner}:")
for key, value in results[winner]['best_params'].items():
    print(f"   • {key}: {value}")

# Visualization of results
print("\n📊 Performance Comparison:")
print("-"*70)

for _, row in comparison_df.iterrows():
    model = row['Model']
    score = row['Test Score']
    bar = '█' * int(score * 50)
    print(f"{model:20} {score:.4f} {bar}")
8.4 Case Study 4: Time Series Model Tuning
Python

"""
CASE STUDY 4: TIME SERIES FORECASTING MODEL TUNING
===================================================
Hyperparameter tuning for time series with proper validation
"""

import numpy as np
import pandas as pd
from sklearn.ensemble import RandomForestRegressor, GradientBoostingRegressor
from sklearn.metrics import mean_squared_error, mean_absolute_error
import optuna
import warnings

warnings.filterwarnings('ignore')
optuna.logging.set_verbosity(optuna.logging.WARNING)

# Generate synthetic time series data
np.random.seed(42)
n_samples = 1000

# Create features with time dependencies
time = np.arange(n_samples)
trend = 0.05 * time
seasonality = 10 * np.sin(2 * np.pi * time / 365)
noise = np.random.randn(n_samples) * 5

y = trend + seasonality + noise

# Create lagged features
def create_lagged_features(y, n_lags=10):
    df = pd.DataFrame({'target': y})
    for i in range(1, n_lags + 1):
        df[f'lag_{i}'] = df['target'].shift(i)
    df = df.dropna()
    return df

data = create_lagged_features(y, n_lags=14)
X = data.drop('target', axis=1).values
y = data['target'].values

print("="*70)
print("CASE STUDY: TIME SERIES HYPERPARAMETER TUNING")
print("="*70)
print(f"\nData shape: {X.shape}")

# ═══════════════════════════════════════════════════════════════
# IMPORTANT: Time Series Cross-Validation
# ═══════════════════════════════════════════════════════════════
"""
For time series, we CANNOT use random cross-validation!
We must respect the temporal order of data.

Wrong: Random shuffle → Data leakage (using future to predict past)
Right: Time-based splits → Training always before test
"""

from sklearn.model_selection import TimeSeriesSplit

print("\n📍 Using TimeSeriesSplit for proper validation")
print("-"*50)

tscv = TimeSeriesSplit(n_splits=5)

# Visualize the splits
print("\nTime Series Cross-Validation Splits:")
for fold, (train_idx, test_idx) in enumerate(tscv.split(X)):
    print(f"  Fold {fold+1}: Train[{train_idx[0]:4d}:{train_idx[-1]:4d}] → "
          f"Test[{test_idx[0]:4d}:{test_idx[-1]:4d}]")

# Train/test split (time-based)
split_point = int(len(X) * 0.8)
X_train, X_test = X[:split_point], X[split_point:]
y_train, y_test = y[:split_point], y[split_point:]

print(f"\nFinal split: Train={len(X_train)}, Test={len(X_test)}")

# ═══════════════════════════════════════════════════════════════
# Hyperparameter Tuning with Time Series CV
# ═══════════════════════════════════════════════════════════════
def objective(trial):
    # Model selection
    model_type = trial.suggest_categorical('model', ['rf', 'gb'])
    
    if model_type == 'rf':
        params = {
            'n_estimators': trial.suggest_int('rf_n_estimators', 50, 300),
            'max_depth': trial.suggest_int('rf_max_depth', 3, 20),
            'min_samples_split': trial.suggest_int('rf_min_samples_split', 2, 20),
            'min_samples_leaf': trial.suggest_int('rf_min_samples_leaf', 1, 10)
        }
        model = RandomForestRegressor(**params, random_state=42, n_jobs=-1)
    else:
        params = {
            'n_estimators': trial.suggest_int('gb_n_estimators', 50, 300),
            'max_depth': trial.suggest_int('gb_max_depth', 2, 10),
            'learning_rate': trial.suggest_float('gb_lr', 0.01, 0.3, log=True),
            'subsample': trial.suggest_float('gb_subsample', 0.5, 1.0)
        }
        model = GradientBoostingRegressor(**params, random_state=42)
    
    # Time series cross-validation
    tscv = TimeSeriesSplit(n_splits=5)
    scores = []
    
    for train_idx, val_idx in tscv.split(X_train):
        X_fold_train, X_fold_val = X_train[train_idx], X_train[val_idx]
        y_fold_train, y_fold_val = y_train[train_idx], y_train[val_idx]
        
        model.fit(X_fold_train, y_fold_train)
        y_pred = model.predict(X_fold_val)
        
        # Use negative RMSE (we want to maximize)
        rmse = np.sqrt(mean_squared_error(y_fold_val, y_pred))
        scores.append(-rmse)
    
    return np.mean(scores)

print("\n🚀 Starting Optimization...")
print("-"*50)

study = optuna.create_study(
    direction='maximize',  # Maximize negative RMSE
    sampler=optuna.samplers.TPESampler(seed=42)
)

study.optimize(objective, n_trials=50, show_progress_bar=True)

# Results
print("\n" + "="*70)
print("OPTIMIZATION RESULTS")
print("="*70)

print(f"\n🏆 Best CV RMSE: {-study.best_value:.4f}")
print(f"\n🔧 Best Parameters:")
for key, value in study.best_params.items():
    print(f"   • {key}: {value}")

# Train final model
if study.best_params['model'] == 'rf':
    final_params = {k.replace('rf_', ''): v for k, v in study.best_params.items() 
                    if k.startswith('rf_')}
    final_model = RandomForestRegressor(**final_params, random_state=42)
else:
    final_params = {k.replace('gb_', ''): v for k, v in study.best_params.items() 
                    if k.startswith('gb_')}
    final_model = GradientBoostingRegressor(**final_params, random_state=42)

final_model.fit(X_train, y_train)
y_pred = final_model.predict(X_test)

# Final metrics
test_rmse = np.sqrt(mean_squared_error(y_test, y_pred))
test_mae = mean_absolute_error(y_test, y_pred)

print(f"\n🎯 FINAL TEST METRICS:")
print(f"   • RMSE: {test_rmse:.4f}")
print(f"   • MAE:  {test_mae:.4f}")
Chapter 9: Common Mistakes & How to Avoid Them
9.1 Mistake #1: Data Leakage
text

┌─────────────────────────────────────────────────────────────────┐
│                    MISTAKE #1: DATA LEAKAGE                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ❌ WRONG: Preprocessing before splitting                       │
│  ─────────────────────────────────────────                      │
│                                                                 │
│     # WRONG!                                                    │
│     scaler = StandardScaler()                                   │
│     X_scaled = scaler.fit_transform(X)  # Uses ALL data        │
│     X_train, X_test = train_test_split(X_scaled)               │
│                                                                 │
│     # Test data influenced the scaling! → LEAKAGE              │
│                                                                 │
│  ✅ CORRECT: Preprocessing after splitting                      │
│  ────────────────────────────────────────                       │
│                                                                 │
│     # CORRECT!                                                  │
│     X_train, X_test = train_test_split(X)                      │
│     scaler = StandardScaler()                                   │
│     X_train = scaler.fit_transform(X_train)  # Fit on train    │
│     X_test = scaler.transform(X_test)  # Transform only        │
│                                                                 │
│  BEST: Use Pipeline (handles this automatically)               │
│  ─────────────────────────────────────────────                  │
│                                                                 │
│     pipeline = Pipeline([                                       │
│         ('scaler', StandardScaler()),                          │
│         ('model', RandomForestClassifier())                    │
│     ])                                                          │
│     # GridSearchCV with pipeline handles everything correctly! │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.2 Mistake #2: Testing on Validation Data
text

┌─────────────────────────────────────────────────────────────────┐
│             MISTAKE #2: NO SEPARATE TEST SET                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ❌ WRONG: Using CV score as final performance                  │
│  ────────────────────────────────────────────                   │
│                                                                 │
│     grid_search.fit(X, y)                                       │
│     print(f"Performance: {grid_search.best_score_}")           │
│     # This is OPTIMISTIC! You tuned on this data.              │
│                                                                 │
│  ✅ CORRECT: Hold out a separate test set                       │
│  ──────────────────────────────────────────                     │
│                                                                 │
│     # Step 1: Create held-out test set                         │
│     X_train, X_test, y_train, y_test = train_test_split(...)  │
│                                                                 │
│     # Step 2: Tune on training data only                       │
│     grid_search.fit(X_train, y_train)                          │
│                                                                 │
│     # Step 3: Report unbiased test performance                 │
│     test_score = grid_search.score(X_test, y_test)             │
│     print(f"Unbiased Performance: {test_score}")               │
│                                                                 │
│  DATA FLOW:                                                     │
│  ──────────                                                     │
│                                                                 │
│     ┌──────────────────────┐     ┌──────────────┐              │
│     │     TRAINING SET     │     │   TEST SET   │              │
│     │  (for CV & tuning)   │     │  (untouched) │              │
│     │                      │     │              │              │
│     │   ┌─────┬─────┐     │     │   Only used  │              │
│     │   │Train│ Val │×5   │     │   at the     │              │
│     │   └─────┴─────┘     │     │   very end   │              │
│     └──────────────────────┘     └──────────────┘              │
│              80%                       20%                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.3 Mistake #3: Wrong Search Ranges
text

┌─────────────────────────────────────────────────────────────────┐
│              MISTAKE #3: POOR SEARCH RANGES                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ❌ WRONG: Too narrow ranges                                    │
│  ────────────────────────────                                   │
│                                                                 │
│     param_grid = {                                              │
│         'learning_rate': [0.1, 0.11, 0.12]  # Too narrow!      │
│     }                                                           │
│     # Might miss optimal value of 0.001                        │
│                                                                 │
│  ❌ WRONG: Uniform for log-scale parameters                     │
│  ──────────────────────────────────────────                     │
│                                                                 │
│     'learning_rate': uniform(0.0001, 0.1)                       │
│     # 90% of samples will be > 0.01!                           │
│     # Poorly explores small values                              │
│                                                                 │
│  ✅ CORRECT: Appropriate ranges and distributions               │
│  ─────────────────────────────────────────────                  │
│                                                                 │
│     param_distributions = {                                     │
│         # Use LOG-UNIFORM for learning rate                    │
│         'learning_rate': loguniform(1e-5, 1e-1),               │
│                                                                 │
│         # Use wide ranges initially                            │
│         'n_estimators': randint(10, 1000),                     │
│                                                                 │
│         # Then narrow down based on results                    │
│     }                                                           │
│                                                                 │
│  STRATEGY: Coarse-to-Fine                                       │
│  ────────────────────────                                       │
│                                                                 │
│     Round 1: Wide ranges (exploration)                          │
│         learning_rate: [0.0001, 0.1]                           │
│         Best found: 0.01                                        │
│                                                                 │
│     Round 2: Narrow around best (exploitation)                  │
│         learning_rate: [0.005, 0.02]                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.4 Mistake #4: Ignoring Overfitting
text

┌─────────────────────────────────────────────────────────────────┐
│              MISTAKE #4: IGNORING OVERFITTING                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ❌ WRONG: Only looking at validation score                     │
│  ──────────────────────────────────────────                     │
│                                                                 │
│     Best hyperparameters found!                                 │
│     CV Score: 0.99  ← Looks great!                             │
│     Test Score: 0.75  ← Disaster!                              │
│                                                                 │
│  ✅ CORRECT: Check train-validation gap                         │
│  ─────────────────────────────────────                          │
│                                                                 │
│     grid_search = GridSearchCV(..., return_train_score=True)   │
│                                                                 │
│     # After fitting, check for overfitting:                    │
│     results = pd.DataFrame(grid_search.cv_results_)            │
│                                                                 │
│     train_score = results.loc[best_idx, 'mean_train_score']    │
│     val_score = results.loc[best_idx, 'mean_test_score']       │
│     gap = train_score - val_score                               │
│                                                                 │
│     if gap > 0.05:                                              │
│         print("⚠️ Overfitting detected!")                       │
│         print("Consider: more regularization, less complexity") │
│                                                                 │
│  HEALTHY vs OVERFITTING:                                        │
│  ───────────────────────                                        │
│                                                                 │
│     HEALTHY:         Train: 0.92   Val: 0.90   Gap: 0.02 ✓     │
│     OVERFITTING:     Train: 0.99   Val: 0.80   Gap: 0.19 ✗     │
│     UNDERFITTING:    Train: 0.70   Val: 0.68   Gap: 0.02       │
│                      (Both scores too low!)                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.5 Mistake #5: Not Using Stratification
Python

"""
MISTAKE #5: IGNORING CLASS IMBALANCE IN CV
==========================================
"""

from sklearn.model_selection import (
    KFold, 
    StratifiedKFold,
    cross_val_score,
    GridSearchCV
)
from sklearn.ensemble import RandomForestClassifier
import numpy as np

# Create imbalanced dataset
np.random.seed(42)
X = np.random.randn(1000, 10)
y = np.array([0] * 950 + [1] * 50)  # 95% class 0, 5% class 1

print("="*60)
print("MISTAKE #5: NOT USING STRATIFICATION")
print("="*60)

# ❌ WRONG: Regular KFold
print("\n❌ Regular KFold (WRONG for imbalanced data):")
print("-"*50)

kfold = KFold(n_splits=5, shuffle=True, random_state=42)
for fold, (train_idx, test_idx) in enumerate(kfold.split(X)):
    class_dist = np.bincount(y[test_idx])
    print(f"  Fold {fold+1}: Class 0 = {class_dist[0]}, Class 1 = {class_dist[1]}")
    # Some folds might have very few or no minority class samples!

# ✅ CORRECT: StratifiedKFold
print("\n✅ StratifiedKFold (CORRECT for imbalanced data):")
print("-"*50)

stratified_kfold = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
for fold, (train_idx, test_idx) in enumerate(stratified_kfold.split(X, y)):
    class_dist = np.bincount(y[test_idx])
    print(f"  Fold {fold+1}: Class 0 = {class_dist[0]}, Class 1 = {class_dist[1]}")
    # Each fold maintains the same class distribution!

# In GridSearchCV:
print("\n✅ Using stratification in GridSearchCV:")
print("-"*50)

# By default, GridSearchCV uses StratifiedKFold for classification
# But you can be explicit:
grid_search = GridSearchCV(
    RandomForestClassifier(random_state=42),
    {'n_estimators': [50, 100]},
    cv=StratifiedKFold(n_splits=5, shuffle=True, random_state=42),
    scoring='f1'  # Better metric for imbalanced data
)

print("  GridSearchCV configured with StratifiedKFold and F1 score ✓")
9.6 Mistake #6: Computational Waste
text

┌─────────────────────────────────────────────────────────────────┐
│             MISTAKE #6: COMPUTATIONAL WASTE                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ❌ WRONG: Training on full dataset immediately                 │
│  ─────────────────────────────────────────────                  │
│                                                                 │
│     # Full dataset with massive grid = DAYS of computation     │
│     grid_search.fit(X_full_1million_rows, y)                   │
│                                                                 │
│  ✅ CORRECT: Progressive approach                               │
│  ──────────────────────────────                                 │
│                                                                 │
│     # Step 1: Sample data for quick exploration                │
│     X_sample, _, y_sample, _ = train_test_split(               │
│         X, y, train_size=0.1, stratify=y                       │
│     )                                                           │
│                                                                 │
│     # Step 2: Coarse search on sample (minutes)                │
│     coarse_search.fit(X_sample, y_sample)                      │
│                                                                 │
│     # Step 3: Fine search on sample (minutes)                  │
│     # Narrow ranges based on coarse results                    │
│     fine_search.fit(X_sample, y_sample)                        │
│                                                                 │
│     # Step 4: Validate on larger sample                        │
│     # Check if results hold                                    │
│                                                                 │
│     # Step 5: Final training on full data (once!)              │
│     final_model.fit(X_full, y)                                 │
│                                                                 │
│  OTHER EFFICIENCY TIPS:                                         │
│  ──────────────────────                                         │
│                                                                 │
│     • Use n_jobs=-1 (parallel processing)                      │
│     • Use early stopping / pruning                             │
│     • Use HalvingSearchCV                                       │
│     • Start with fewer CV folds (3 instead of 5)               │
│     • Cache preprocessing steps                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.7 Mistake #7: Ignoring Random Seeds
Python

"""
MISTAKE #7: NOT SETTING RANDOM SEEDS
====================================
Results are not reproducible!
"""

from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import RandomizedSearchCV, cross_val_score
from scipy.stats import randint
import numpy as np

print("="*60)
print("MISTAKE #7: NOT SETTING RANDOM SEEDS")
print("="*60)

# Create sample data
np.random.seed(42)
X = np.random.randn(200, 10)
y = (X[:, 0] + X[:, 1] > 0).astype(int)

# ❌ WRONG: No random seeds
print("\n❌ Without random seeds (different results each time):")
print("-"*50)

for run in range(3):
    model = RandomForestClassifier()  # No random_state!
    scores = cross_val_score(model, X, y, cv=5)
    print(f"  Run {run+1}: {scores.mean():.4f}")
# Results will vary each run!

# ✅ CORRECT: Set all random seeds
print("\n✅ With random seeds (reproducible results):")
print("-"*50)

for run in range(3):
    model = RandomForestClassifier(random_state=42)  # Fixed seed!
    scores = cross_val_score(model, X, y, cv=5)
    print(f"  Run {run+1}: {scores.mean():.4f}")
# Same results every time!

# Complete reproducibility checklist:
print("\n📋 REPRODUCIBILITY CHECKLIST:")
print("-"*50)
print("""
1. Set numpy seed:           np.random.seed(42)
2. Set model random_state:   RandomForestClassifier(random_state=42)
3. Set CV random_state:      StratifiedKFold(random_state=42)
4. Set search random_state:  RandomizedSearchCV(random_state=42)
5. Set split random_state:   train_test_split(random_state=42)

For deep learning also:
6. Set TensorFlow seed:      tf.random.set_seed(42)
7. Set Python seed:          random.seed(42)
""")
9.8 Complete Checklist for Hyperparameter Tuning
text

┌─────────────────────────────────────────────────────────────────┐
│           HYPERPARAMETER TUNING CHECKLIST ✓                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  BEFORE TUNING:                                                 │
│  □ Separate test set created and set aside                    │
│  □ Data preprocessing defined (will use Pipeline)             │
│  □ Baseline model performance recorded                        │
│  □ Evaluation metric chosen appropriate for problem           │
│  □ Random seeds set for reproducibility                       │
│  □ Search ranges based on domain knowledge/literature         │
│                                                                 │
│  DURING TUNING:                                                 │
│  □ Using proper CV (Stratified for classification)            │
│  □ Using Pipeline to avoid data leakage                       │
│  □ Monitoring train vs validation gap                         │
│  □ Using efficient search (Random → Bayesian)                 │
│  □ Using early stopping/pruning when possible                 │
│  □ Logging all experiments                                    │
│                                                                 │
│  AFTER TUNING:                                                  │
│  □ Evaluated on held-out test set                             │
│  □ Checked for overfitting (train-val-test gaps)              │
│  □ Analyzed hyperparameter importance                         │
│  □ Documented best hyperparameters                            │
│  □ Saved final model                                          │
│  □ Results are reproducible                                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 10: Interview Questions & Answers
10.1 Basic Level Questions
Q1: What is the difference between parameters and hyperparameters?
text

ANSWER:
═══════

┌────────────────────────┬────────────────────────────────────────┐
│      PARAMETERS        │          HYPERPARAMETERS               │
├────────────────────────┼────────────────────────────────────────┤
│ Learned FROM data      │ Set BEFORE training                    │
│ Internal to model      │ External configuration                 │
│ Cannot be set manually │ Must be set manually                   │
│ Examples:              │ Examples:                              │
│ - Weights in NN        │ - Learning rate                        │
│ - Coefficients in LR   │ - Number of trees                      │
│ - Split points in tree │ - Max depth                            │
└────────────────────────┴────────────────────────────────────────┘

ANALOGY:
• Hyperparameters = Recipe settings (oven temperature, cooking time)
• Parameters = The actual dish that gets cooked
Q2: Explain Grid Search with an example.
text

ANSWER:
═══════

Grid Search exhaustively tries ALL combinations of hyperparameters.

EXAMPLE:
--------
If we have:
• n_estimators: [100, 200]
• max_depth: [5, 10]
• min_samples_split: [2, 5]

Grid Search tries ALL 2×2×2 = 8 combinations:
1. (100, 5, 2)
2. (100, 5, 5)
3. (100, 10, 2)
4. (100, 10, 5)
5. (200, 5, 2)
6. (200, 5, 5)
7. (200, 10, 2)
8. (200, 10, 5)

Each combination is evaluated with cross-validation.
The combination with the best CV score is selected.

PROS: Guaranteed to find the best in the grid
CONS: Exponentially expensive as dimensions increase
Q3: Why might Random Search be preferred over Grid Search?
text

ANSWER:
═══════

REASON 1: Efficiency
────────────────────
Random Search explores more unique values of important hyperparameters
with the same budget.

REASON 2: The Bergstra & Bengio Insight
───────────────────────────────────────
Not all hyperparameters matter equally. If learning_rate is important
but batch_size isn't:

Grid Search (9 points):    Random Search (9 points):
• Only 3 learning rates    • 9 different learning rates!

REASON 3: Continuous Spaces
───────────────────────────
Random Search can sample from continuous distributions,
finding values like 0.0234 that Grid Search would miss.

REASON 4: Scalability
─────────────────────
Grid: 10 hyperparameters × 10 values = 10^10 combinations
Random: You decide the budget (e.g., 100 trials regardless of dimensions)
Q4: What is cross-validation and why is it used in hyperparameter tuning?
text

ANSWER:
═══════

WHAT: Cross-validation splits data into K folds, trains on K-1 folds,
      and validates on 1 fold. Repeats K times, averaging the scores.

WHY IN HYPERPARAMETER TUNING:
─────────────────────────────
1. RELIABLE EVALUATION
   Single train/test split can be lucky or unlucky.
   CV gives a more stable estimate of performance.

2. AVOID OVERFITTING TO VALIDATION SET
   Using multiple validation sets prevents overfitting
   to a single validation set.

3. BETTER USE OF DATA
   All data is used for both training and validation.

VISUALIZATION (5-Fold CV):
─────────────────────────
Fold 1: [VAL] [TRAIN] [TRAIN] [TRAIN] [TRAIN] → Score 1
Fold 2: [TRAIN] [VAL] [TRAIN] [TRAIN] [TRAIN] → Score 2
Fold 3: [TRAIN] [TRAIN] [VAL] [TRAIN] [TRAIN] → Score 3
Fold 4: [TRAIN] [TRAIN] [TRAIN] [VAL] [TRAIN] → Score 4
Fold 5: [TRAIN] [TRAIN] [TRAIN] [TRAIN] [VAL] → Score 5
                                        ────────
                                        Average → Final Score
10.2 Intermediate Level Questions
Q5: Explain Bayesian Optimization and how it differs from Grid/Random Search.
text

ANSWER:
═══════

BAYESIAN OPTIMIZATION:
──────────────────────
An intelligent search that LEARNS from previous evaluations to decide
which hyperparameters to try next.

KEY COMPONENTS:
1. Surrogate Model: Approximates the objective function (usually GP or TPE)
2. Acquisition Function: Decides where to sample next (e.g., Expected Improvement)

HOW IT DIFFERS:
───────────────
┌────────────────┬─────────────────────────────────────────────────┐
│ Grid/Random    │ Each trial is INDEPENDENT                       │
│                │ No learning from previous trials                │
│                │ Might waste time on bad regions                 │
├────────────────┼─────────────────────────────────────────────────┤
│ Bayesian       │ Each trial INFORMS the next                     │
│                │ Builds a model of "good" vs "bad" regions       │
│                │ Focuses search on promising areas               │
└────────────────┴─────────────────────────────────────────────────┘

WHEN TO USE:
• Expensive objective functions (deep learning, large datasets)
• Limited computational budget
• Complex hyperparameter interactions
Q6: What is the curse of dimensionality in hyperparameter tuning?
text

ANSWER:
═══════

DEFINITION:
───────────
As the number of hyperparameters increases, the search space grows
EXPONENTIALLY, making exhaustive search impractical.

EXAMPLE:
────────
• 1 hyperparameter, 10 values: 10 combinations
• 2 hyperparameters, 10 values: 100 combinations
• 3 hyperparameters, 10 values: 1,000 combinations
• 5 hyperparameters, 10 values: 100,000 combinations
• 10 hyperparameters, 10 values: 10,000,000,000 combinations!

SOLUTIONS:
──────────
1. Use Random Search (fixed budget regardless of dimensions)
2. Use Bayesian Optimization (intelligent search)
3. Reduce search space using domain knowledge
4. Use dimensionality reduction (focus on important hyperparameters)
5. Use Halving Search (progressively eliminate poor candidates)
Q7: Explain the exploration vs exploitation trade-off in hyperparameter tuning.
text

ANSWER:
═══════

EXPLORATION: Trying new, unexplored regions of the search space
            (What if there's something better elsewhere?)

EXPLOITATION: Focusing on regions that have shown good results
             (Let's refine what we know works)

THE DILEMMA:
────────────
• Too much exploration → Waste time on bad regions
• Too much exploitation → Miss the global optimum

HOW EACH METHOD HANDLES IT:
───────────────────────────
Grid Search:    Pure exploration (tries everything equally)
Random Search:  Random exploration (no exploitation)
Bayesian:       BALANCES both through acquisition function

ACQUISITION FUNCTIONS:
──────────────────────
• Expected Improvement (EI): Balanced approach
• Probability of Improvement (PI): More exploitative
• Upper Confidence Bound (UCB): Adjustable via κ parameter
  - High κ → More exploration
  - Low κ → More exploitation
Q8: What is nested cross-validation and when should you use it?
text

ANSWER:
═══════

WHAT:
─────
Two loops of cross-validation:
• Outer loop: Evaluates overall model performance
• Inner loop: Tunes hyperparameters

WHY:
────
Regular CV for hyperparameter tuning gives OPTIMISTIC estimates.
The hyperparameters are "fit" to the validation folds, so the
CV score is biased.

WHEN TO USE:
────────────
• When you need an UNBIASED estimate of model performance
• For academic publications or rigorous comparisons
• When dataset is too small for a separate test set

STRUCTURE:
──────────
┌─────────────────────────────────────────────────────────────┐
│ OUTER FOLD 1:  [TEST] [─────── INNER CV ───────]           │
│ OUTER FOLD 2:  [TEST] [─────── INNER CV ───────]           │
│ OUTER FOLD 3:  [TEST] [─────── INNER CV ───────]           │
│ OUTER FOLD 4:  [TEST] [─────── INNER CV ───────]           │
│ OUTER FOLD 5:  [TEST] [─────── INNER CV ───────]           │
│                                                             │
│ Each INNER CV does hyperparameter tuning.                   │
│ Each OUTER TEST gives unbiased performance estimate.        │
│ Final score = Average of OUTER TEST scores.                │
└─────────────────────────────────────────────────────────────┘
10.3 Advanced Level Questions
Q9: Explain TPE (Tree-structured Parzen Estimator) and how it differs from Gaussian Process-based Bayesian Optimization.
text

ANSWER:
═══════

GAUSSIAN PROCESS (GP) APPROACH:
───────────────────────────────
• Models P(score | hyperparameters) directly
• Predicts score AND uncertainty for any point
• Computationally expensive: O(n³) for n observations
• Works well for continuous, low-dimensional spaces

TPE APPROACH:
─────────────
• Models P(hyperparameters | good_score) and P(hyperparameters | bad_score)
• Splits observations into "good" (top γ percentile) and "bad"
• Builds separate density estimators: l(x) and g(x)
• Samples where l(x)/g(x) is high

TPE ALGORITHM:
1. Define threshold y* (e.g., top 25% of scores)
2. Fit l(x) = P(x | y < y*)  ← density of "good" hyperparameters
3. Fit g(x) = P(x | y >= y*) ← density of "bad" hyperparameters
4. Sample points that maximize l(x)/g(x)

COMPARISON:
───────────
┌────────────────┬─────────────────────┬─────────────────────┐
│                │ Gaussian Process    │ TPE                 │
├────────────────┼─────────────────────┼─────────────────────┤
│ Scalability    │ O(n³), limited      │ O(n log n), better  │
│ Categorical    │ Difficult           │ Handles naturally   │
│ Conditional    │ Complex             │ Native support      │
│ Interpretable  │ More intuitive      │ Less intuitive      │
│ Implementation │ scikit-optimize     │ Optuna, Hyperopt    │
└────────────────┴─────────────────────┴─────────────────────┘
Q10: How would you handle hyperparameter tuning for a model with conditional hyperparameters?
text

ANSWER:
═══════

WHAT ARE CONDITIONAL HYPERPARAMETERS:
─────────────────────────────────────
Hyperparameters that only exist if another hyperparameter has a
certain value.

EXAMPLE:
• SVM kernel = 'poly' → degree is relevant
• SVM kernel = 'rbf' → degree is NOT relevant

SOLUTIONS:

1. OPTUNA (Recommended):
────────────────────────
def objective(trial):
    kernel = trial.suggest_categorical('kernel', ['rbf', 'poly'])
    params = {'kernel': kernel, 'C': trial.suggest_float('C', 0.1, 100)}
    
    if kernel == 'poly':
        params['degree'] = trial.suggest_int('degree', 2, 5)
    
    return evaluate(params)

2. HYPEROPT:
────────────
from hyperopt import hp
space = hp.choice('kernel', [
    {'kernel': 'rbf'},
    {'kernel': 'poly', 'degree': hp.quniform('degree', 2, 5, 1)}
])

3. CONFIGSPACE (for SMAC):
──────────────────────────
cs = ConfigurationSpace()
kernel = CategoricalHyperparameter('kernel', ['rbf', 'poly'])
degree = UniformIntegerHyperparameter('degree', 2, 5)
cs.add_hyperparameters([kernel, degree])
cs.add_condition(EqualsCondition(degree, kernel, 'poly'))
Q11: Describe a complete hyperparameter tuning pipeline for a production ML system.
text

ANSWER:
═══════

PRODUCTION HYPERPARAMETER TUNING PIPELINE:
──────────────────────────────────────────

┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  PHASE 1: DATA PREPARATION                                   │
│  ─────────────────────────                                   │
│  • Split: Train (70%) / Validation (15%) / Test (15%)       │
│  • Create data versioning (DVC, MLflow)                     │
│  • Define preprocessing in Pipeline                         │
│                                                              │
│  PHASE 2: BASELINE                                           │
│  ────────────────────                                        │
│  • Train model with default hyperparameters                 │
│  • Record baseline metrics                                  │
│  • Set performance targets                                  │
│                                                              │
│  PHASE 3: COARSE SEARCH                                      │
│  ───────────────────────                                     │
│  • Use Random Search on data sample (10-20%)                │
│  • Wide hyperparameter ranges                               │
│  • 50-100 iterations                                        │
│  • Identify promising regions                               │
│                                                              │
│  PHASE 4: FINE SEARCH                                        │
│  ─────────────────────                                       │
│  • Use Bayesian Optimization                                │
│  • Narrow ranges around promising regions                   │
│  • Full training data (or larger sample)                    │
│  • 100-200 iterations with pruning                          │
│                                                              │
│  PHASE 5: VALIDATION                                         │
│  ───────────────────                                         │
│  • Evaluate top-K configurations on validation set          │
│  • Check for overfitting (train-val gap)                    │
│  • Statistical significance testing                         │
│                                                              │
│  PHASE 6: FINAL EVALUATION                                   │
│  ─────────────────────────                                   │
│  • Train final model on train+validation                    │
│  • Evaluate ONCE on test set                                │
│  • Record all metrics                                       │
│                                                              │
│  PHASE 7: DOCUMENTATION & DEPLOYMENT                         │
│  ───────────────────────────────────                         │
│  • Log all hyperparameters (MLflow)                         │
│  • Version the model                                        │
│  • Create reproducibility artifacts                         │
│  • Deploy with monitoring                                   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
Q12: How do you handle hyperparameter tuning when training is extremely expensive (e.g., large language models)?
text

ANSWER:
═══════

STRATEGIES FOR EXPENSIVE MODELS:

1. PROXY TASKS
───────────────
• Train on smaller dataset / shorter sequences
• Use smaller model variant for tuning
• Transfer insights to full model

2. EARLY STOPPING / PRUNING
────────────────────────────
• Use learning curve extrapolation
• Stop unpromising runs after few epochs
• Optuna MedianPruner or HyperbandPruner

3. MULTI-FIDELITY OPTIMIZATION
───────────────────────────────
• Successive Halving: Start with many configs, low budget
  Progressively eliminate poor performers
• Hyperband: Combines random search with early stopping

4. TRANSFER LEARNING FOR HYPERPARAMETERS
─────────────────────────────────────────
• Use hyperparameters from similar tasks/models
• Warm-start Bayesian optimization with prior knowledge

5. META-LEARNING
────────────────
• Learn from previous tuning experiments
• Use meta-features to predict good starting points

6. REDUCING SEARCH SPACE
─────────────────────────
• Literature review for common ranges
• Expert knowledge
• Sensitivity analysis to identify key hyperparameters

7. EFFICIENT ARCHITECTURES
───────────────────────────
• Low-rank factorization for tuning
• Parameter-efficient fine-tuning (LoRA, Adapters)

EXAMPLE SETUP:
──────────────
1. Use 1% of data for initial exploration (Random Search, 30 trials)
2. Use 10% of data for refinement (Bayesian, 50 trials with pruning)
3. Train top-3 configurations on full data
4. Select best based on validation performance
10.4 Practical Scenario Questions
Q13: You've run hyperparameter tuning and your CV score is 95% but test score is 75%. What happened and how do you fix it?
text

ANSWER:
═══════

DIAGNOSIS: OVERFITTING TO VALIDATION DATA
──────────────────────────────────────────

This happens when:
1. Too many hyperparameters tuned on limited data
2. Too many trials → found hyperparameters that work well
   by chance on the validation folds
3. Data leakage in preprocessing

FIX STRATEGIES:

1. USE NESTED CROSS-VALIDATION
───────────────────────────────
Outer CV gives unbiased estimate, inner CV for tuning.

2. REDUCE SEARCH SPACE
───────────────────────
Fewer hyperparameters → less chance of overfitting.

3. ADD REGULARIZATION
──────────────────────
Choose hyperparameters that favor simpler models:
• Higher min_samples_leaf
• Lower max_depth
• Higher regularization (alpha, lambda)

4. USE LARGER VALIDATION FOLDS
───────────────────────────────
More data in validation → more stable estimates.

5. EARLY STOPPING
──────────────────
Stop tuning before exhausting the search space.

6. CHECK FOR DATA LEAKAGE
──────────────────────────
Ensure preprocessing is inside CV pipeline.

7. SIMPLER MODEL
────────────────
Consider if a simpler model generalizes better.
Q14: How would you tune hyperparameters when you have very limited data (e.g., 500 samples)?
text

ANSWER:
═══════

CHALLENGES:
───────────
• CV scores will be unstable
• High variance in performance estimates
• Risk of overfitting to specific splits

STRATEGIES:

1. LEAVE-ONE-OUT OR LEAVE-P-OUT CV
───────────────────────────────────
• Maximum data for training in each fold
• More stable estimates (but expensive)

2. REPEATED K-FOLD CV
──────────────────────
• Repeat 5-fold CV multiple times (e.g., 10 repeats)
• Average across all 50 folds
• More stable estimate

3. BOOTSTRAP VALIDATION
────────────────────────
• Sample with replacement for training
• Use out-of-bag samples for validation
• Repeat many times

4. CONSERVATIVE HYPERPARAMETER CHOICES
───────────────────────────────────────
• Favor simpler models
• Strong regularization
• Fewer hyperparameters to tune

5. BAYESIAN APPROACH WITH PRIORS
─────────────────────────────────
• Incorporate prior knowledge
• Regularize towards reasonable values

6. REDUCE SEARCH SPACE
───────────────────────
• Use literature values
• Domain expertise
• Only tune most important 2-3 hyperparameters

RECOMMENDED SETUP:
──────────────────
• Repeated Stratified K-Fold (5 folds × 10 repeats)
• Bayesian optimization (efficient with small budget)
• Focus on 2-3 most important hyperparameters
• Strong regularization by default
Q15: Compare the computational costs of different hyperparameter tuning methods and provide recommendations for different scenarios.
text

ANSWER:
═══════

COMPUTATIONAL COST COMPARISON:
──────────────────────────────

┌──────────────────┬────────────────┬───────────────┬────────────┐
│ Method           │ Time Complexity│ Parallelizable│ Memory     │
├──────────────────┼────────────────┼───────────────┼────────────┤
│ Grid Search      │ O(∏nᵢ × cv)    │ ✓ Excellent   │ Low        │
│ Random Search    │ O(n_iter × cv) │ ✓ Excellent   │ Low        │
│ Bayesian (GP)    │ O(n³ × cv)     │ △ Limited     │ High       │
│ Bayesian (TPE)   │ O(n log n × cv)│ △ Limited     │ Medium     │
│ Halving Search   │ O(n × log n)   │ ✓ Good        │ Low        │
│ Population-based │ O(pop × gen)   │ ✓ Excellent   │ High       │
└──────────────────┴────────────────┴───────────────┴────────────┘

RECOMMENDATIONS BY SCENARIO:
────────────────────────────

┌────────────────────────────┬─────────────────────────────────┐
│ SCENARIO                   │ RECOMMENDATION                   │
├────────────────────────────┼─────────────────────────────────┤
│ Quick prototype            │ Random Search (n_iter=30)        │
│ < 1000 combinations        │ Grid Search                      │
│ Limited time, many params  │ Halving Random Search            │
│ Expensive training         │ Bayesian (TPE) + Pruning         │
│ Unlimited compute          │ Bayesian then Grid refinement    │
│ Parallel cluster           │ Random Search or Population      │
│ Deep learning              │ Bayesian + Early Stopping        │
│ AutoML pipeline            │ Bayesian + Meta-learning         │
└────────────────────────────┴─────────────────────────────────┘

EXAMPLE TIME ESTIMATES (100 combinations, 1 min/train, 5-fold CV):
──────────────────────────────────────────────────────────────────

Grid Search:       100 × 5 × 1 min = 500 min (8.3 hours)
                   With 10 cores: ~50 min

Random Search:     Same as Grid (for same n_iter)

Bayesian (seq):    100 × 5 × 1 min = 500 min (8.3 hours)
                   Cannot fully parallelize!

Halving Search:    ~200 total fits × 1 min = 200 min (3.3 hours)
                   With 10 cores: ~20 min
Quick Reference Card
text

╔═══════════════════════════════════════════════════════════════════╗
║           HYPERPARAMETER TUNING QUICK REFERENCE                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  GRID SEARCH                                                      ║
║  ───────────                                                      ║
║  from sklearn.model_selection import GridSearchCV                 ║
║  grid = GridSearchCV(model, param_grid, cv=5, scoring='accuracy') ║
║  grid.fit(X_train, y_train)                                       ║
║  print(grid.best_params_, grid.best_score_)                       ║
║                                                                   ║
║  RANDOM SEARCH                                                    ║
║  ─────────────                                                    ║
║  from sklearn.model_selection import RandomizedSearchCV           ║
║  from scipy.stats import randint, uniform                         ║
║  search = RandomizedSearchCV(model, param_dist, n_iter=100, cv=5) ║
║  search.fit(X_train, y_train)                                     ║
║                                                                   ║
║  BAYESIAN (OPTUNA)                                                ║
║  ─────────────────                                                ║
║  import optuna                                                    ║
║  def objective(trial):                                            ║
║      param = trial.suggest_int('param', 1, 100)                   ║
║      return cross_val_score(model, X, y).mean()                   ║
║  study = optuna.create_study(direction='maximize')                ║
║  study.optimize(objective, n_trials=100)                          ║
║                                                                   ║
║  DECISION GUIDE                                                   ║
║  ──────────────                                                   ║
║  < 100 combinations → Grid Search                                 ║
║  Quick baseline → Random Search (n_iter=50)                       ║
║  Production → Bayesian (n_trials=100+)                            ║
║  Very large space → Halving Search                                ║
║                                                                   ║
║  COMMON HYPERPARAMETERS                                           ║
║  ──────────────────────                                           ║
║  Learning rate:    loguniform(1e-5, 1e-1)                         ║
║  n_estimators:     randint(50, 500)                               ║
║  max_depth:        randint(2, 30)                                 ║
║  Regularization:   loguniform(1e-6, 1e0)                          ║
║                                                                   ║
║  BEST PRACTICES                                                   ║
║  ──────────────                                                   ║
║  ✓ Always hold out a test set                                    ║
║  ✓ Use Pipeline to avoid data leakage                            ║
║  ✓ Use StratifiedKFold for classification                        ║
║  ✓ Set random_state for reproducibility                          ║
║  ✓ Check train-val gap for overfitting                           ║
║  ✓ Use log-scale for learning rates                              ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
Conclusion
Key Takeaways
text

┌─────────────────────────────────────────────────────────────────┐
│                    KEY TAKEAWAYS                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. HYPERPARAMETERS vs PARAMETERS                               │
│     • Hyperparameters: Set before training (learning rate)     │
│     • Parameters: Learned during training (weights)            │
│                                                                 │
│  2. THREE MAIN METHODS                                          │
│     • Grid Search: Exhaustive, guaranteed, exponential cost    │
│     • Random Search: Efficient, no guarantees, fixed budget    │
│     • Bayesian: Intelligent, learns from trials, most efficient│
│                                                                 │
│  3. CHOOSE BASED ON:                                            │
│     • Search space size                                        │
│     • Training cost                                            │
│     • Available compute                                        │
│     • Required quality                                         │
│                                                                 │
│  4. AVOID COMMON MISTAKES                                       │
│     • Data leakage (use Pipeline!)                             │
│     • No separate test set                                     │
│     • Wrong distributions (use log-scale for LR)               │
│     • Ignoring overfitting                                     │
│                                                                 │
│  5. PRODUCTION WORKFLOW                                         │
│     • Start with baseline (default params)                     │
│     • Coarse search (Random) on sample                         │
│     • Fine search (Bayesian) on full data                      │
│     • Validate and document                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Your Learning Path
text

BEGINNER                 INTERMEDIATE               ADVANCED
─────────────────────────────────────────────────────────────────

1. Understand            1. Use Bayesian            1. Multi-fidelity
   Grid Search              Optimization               optimization
   
2. Implement             2. Create custom           2. Meta-learning
   Random Search            pipelines                  for HPO
   
3. Use sklearn           3. Use Optuna              3. Neural 
   defaults                 with pruning               architecture
                                                       search
                                                    
4. Basic CV              4. Nested CV               4. Population-
                                                       based training
                                                    
5. Single model          5. Multi-model             5. AutoML
   tuning                   comparison                 pipelines



🎓 Congratulations!

You now have a complete understanding of hyperparameter tuning from basics to advanced concepts. This knowledge will serve you well in your ML career, whether you're building models, competing in Kaggle, or working in production ML systems.

Remember: The best hyperparameter tuning strategy depends on your specific situation. Start simple, measure carefully, and iterate!
