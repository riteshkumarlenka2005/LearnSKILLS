Feature Engineering: The Complete Masterclass
From Zero to Hero - A Comprehensive Guide
📚 Table of Contents
Chapter 1: Foundation - What is Feature Engineering?
Chapter 2: Understanding Your Data
Chapter 3: Handling Missing Values
Chapter 4: Encoding Categorical Variables
Chapter 5: Feature Scaling and Normalization
Chapter 6: Feature Transformation
Chapter 7: Feature Creation
Chapter 8: Feature Selection
Chapter 9: Handling Imbalanced Data
Chapter 10: Time Series Feature Engineering
Chapter 11: Text Feature Engineering
Chapter 12: Image Feature Engineering
Chapter 13: Advanced Techniques
Chapter 14: Automated Feature Engineering
Chapter 15: Best Practices and Real-World Projects
Chapter 1: Foundation - What is Feature Engineering?
1.1 The Simplest Definition
Imagine you're baking a cake. You have raw ingredients: flour, eggs, sugar, butter. But you can't just throw them together randomly. You need to:

Measure them correctly
Mix them in the right order
Sometimes transform them (like melting butter)
Combine them in specific ways
Feature Engineering is EXACTLY like this, but for data.

text

Raw Data (Ingredients) → Feature Engineering (Recipe) → Good Features (Delicious Cake) → ML Model Eats It
1.2 What is a Feature?
A feature is simply a measurable property of your data that you use to make predictions.

Real-Life Example: Predicting House Prices
Feature Name	Example Value	What It Represents
Square_Feet	1500	Size of house
Bedrooms	3	Number of bedrooms
Age	10	Years since built
Location	"Downtown"	Where the house is
Each column in your dataset = One Feature

1.3 Why is Feature Engineering So Important?
The Golden Rule of Machine Learning:
text

╔═══════════════════════════════════════════════════════════════╗
║   "Garbage In, Garbage Out"                                   ║
║   "Good Features In, Great Predictions Out"                   ║
╚═══════════════════════════════════════════════════════════════╝
Proof with Numbers:
Scenario	Model Used	Feature Engineering	Accuracy
A	Complex Deep Learning	None	72%
B	Simple Logistic Regression	Excellent	89%
Scenario B wins! This proves features matter MORE than fancy algorithms.

1.4 The Feature Engineering Pipeline
text

┌─────────────────────────────────────────────────────────────────────────┐
│                    FEATURE ENGINEERING PIPELINE                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐        │
│   │  RAW     │───▶│  CLEAN   │───▶│TRANSFORM │───▶│  SELECT  │        │
│   │  DATA    │    │  DATA    │    │ FEATURES │    │ FEATURES │        │
│   └──────────┘    └──────────┘    └──────────┘    └──────────┘        │
│        │               │               │               │               │
│        ▼               ▼               ▼               ▼               │
│   [Collect]      [Handle         [Create new     [Pick the            │
│                   missing,        features,       best ones]          │
│                   fix errors]     encode,                              │
│                                   scale]                               │
└─────────────────────────────────────────────────────────────────────────┘
1.5 Types of Features
A. Based on Data Type
text

FEATURES
    │
    ├── NUMERICAL (Numbers)
    │       │
    │       ├── Continuous: 1.5, 2.7, 3.14159 (can be any value)
    │       │   Examples: Height, Weight, Temperature, Salary
    │       │
    │       └── Discrete: 1, 2, 3, 4 (only whole numbers)
    │           Examples: Number of children, Number of rooms
    │
    └── CATEGORICAL (Categories/Labels)
            │
            ├── Nominal: No order (Red, Blue, Green)
            │   Examples: Country, Gender, Blood Type
            │
            └── Ordinal: Has order (Low < Medium < High)
                Examples: Education Level, Customer Rating
B. Based on Origin
Type	Definition	Example
Raw Feature	Directly from data	Age = 25
Derived Feature	Created from raw features	Age_Group = "Young Adult"
Interaction Feature	Combination of features	Price_Per_SqFt = Price / Square_Feet
1.6 Your First Feature Engineering Code
Python

# Don't worry if you don't understand everything now
# We will cover each concept in detail

import pandas as pd
import numpy as np

# Sample raw data
data = {
    'name': ['Alice', 'Bob', 'Charlie'],
    'birth_year': [1990, 1985, 2000],
    'salary': [50000, 75000, 35000],
    'city': ['NYC', 'LA', 'NYC']
}

df = pd.DataFrame(data)
print("=== RAW DATA ===")
print(df)

# Feature Engineering Step 1: Create Age from birth_year
df['age'] = 2024 - df['birth_year']

# Feature Engineering Step 2: Create salary category
df['salary_category'] = pd.cut(df['salary'], 
                                bins=[0, 40000, 60000, 100000],
                                labels=['Low', 'Medium', 'High'])

# Feature Engineering Step 3: Encode city
df['is_nyc'] = (df['city'] == 'NYC').astype(int)

print("\n=== AFTER FEATURE ENGINEERING ===")
print(df)
Output:

text

=== RAW DATA ===
      name  birth_year  salary city
0    Alice        1990   50000  NYC
1      Bob        1985   75000   LA
2  Charlie        2000   35000  NYC

=== AFTER FEATURE ENGINEERING ===
      name  birth_year  salary city  age salary_category  is_nyc
0    Alice        1990   50000  NYC   34          Medium       1
1      Bob        1985   75000   LA   39            High       0
2  Charlie        2000   35000  NYC   24             Low       1
1.7 Key Terminology Glossary
Term	Simple Definition	Example
Feature	A column in your dataset	"Age", "Salary"
Target	What you're predicting	"Will customer buy? Yes/No"
Observation	A single row of data	One customer's information
Feature Space	All possible feature combinations	All columns together
Dimensionality	Number of features	10 features = 10 dimensions
Cardinality	Unique values in a feature	Country has HIGH cardinality
Chapter 2: Understanding Your Data
2.1 Why Understanding Data Comes First
text

╔══════════════════════════════════════════════════════════╗
║  You CANNOT engineer features without understanding      ║
║  what your data contains, means, and represents.         ║
╚══════════════════════════════════════════════════════════╝
2.2 The Data Understanding Framework
text

┌────────────────────────────────────────────────────────────┐
│              DATA UNDERSTANDING FRAMEWORK                  │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  Step 1: STRUCTURE  ──▶  What shape? How many rows/cols?  │
│              │                                             │
│              ▼                                             │
│  Step 2: DATA TYPES ──▶  Numeric? Categorical? Text?      │
│              │                                             │
│              ▼                                             │
│  Step 3: STATISTICS ──▶  Mean, median, min, max?          │
│              │                                             │
│              ▼                                             │
│  Step 4: QUALITY    ──▶  Missing? Duplicates? Errors?     │
│              │                                             │
│              ▼                                             │
│  Step 5: PATTERNS   ──▶  Distributions? Correlations?     │
│                                                            │
└────────────────────────────────────────────────────────────┘
2.3 Step 1: Understanding Structure
Python

import pandas as pd
import numpy as np

# Load sample dataset
df = pd.read_csv('your_data.csv')

# Basic structure commands
print(f"Number of rows: {df.shape[0]}")
print(f"Number of columns: {df.shape[1]}")
print(f"Column names: {df.columns.tolist()}")

# See first few rows
print(df.head())

# See last few rows
print(df.tail())

# Random sample
print(df.sample(5))
Structure Checklist
Question	Command	Why It Matters
How many rows?	df.shape[0]	Know your data size
How many columns?	df.shape[1]	Know feature count
Column names?	df.columns	Understand what you have
Sample data?	df.head()	See actual values
2.4 Step 2: Understanding Data Types
Python

# Check data types
print(df.dtypes)

# Detailed info
print(df.info())
Python Data Types Mapping
Python Type	Pandas Type	Example	Feature Category
int	int64	1, 2, 3	Numerical
float	float64	1.5, 2.7	Numerical
str	object	"hello"	Categorical/Text
bool	bool	True/False	Binary
datetime	datetime64	2024-01-01	Temporal
Common Data Type Issues
Python

# Issue 1: Numbers stored as strings
df['price'] = "100"  # Wrong! It's a string
df['price'] = df['price'].astype(float)  # Fixed!

# Issue 2: Categories stored as numbers
df['rating'] = 1  # Is this numerical or categorical?
# If it's rating 1-5, treat as categorical
df['rating'] = df['rating'].astype('category')

# Issue 3: Dates stored as strings
df['date'] = "2024-01-15"  # String
df['date'] = pd.to_datetime(df['date'])  # Now it's datetime
2.5 Step 3: Statistical Summary
Python

# For numerical columns
print(df.describe())

# For ALL columns including categorical
print(df.describe(include='all'))
Understanding describe() Output
text

        age         salary
count   1000.00     1000.00    ← Number of non-null values
mean    35.50       62000.00   ← Average value
std     12.30       25000.00   ← Standard deviation (spread)
min     18.00       20000.00   ← Minimum value
25%     25.00       45000.00   ← 25th percentile
50%     35.00       60000.00   ← 50th percentile (median)
75%     45.00       75000.00   ← 75th percentile
max     65.00       150000.00  ← Maximum value
What Each Statistic Tells You
Statistic	What It Reveals	Red Flags
count	Missing values if < total rows	Different counts across columns
mean	Central tendency	Very different from median = skewed
std	Data spread	Very high = high variance
min/max	Range	Impossible values (age = -5?)
25%, 50%, 75%	Distribution shape	Big gaps = possible outliers
2.6 Step 4: Data Quality Assessment
A. Missing Values
Python

# Count missing values
print(df.isnull().sum())

# Percentage missing
print((df.isnull().sum() / len(df)) * 100)

# Visualize missing values
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.heatmap(df.isnull(), cbar=True, yticklabels=False)
plt.title('Missing Values Heatmap')
plt.show()
Missing Values Decision Framework
text

Missing Percentage
       │
       ├── < 5%  ────────▶  Impute (fill with mean/median/mode)
       │
       ├── 5% - 30% ─────▶  Advanced imputation or create indicator
       │
       ├── 30% - 50% ────▶  Consider if feature is useful
       │
       └── > 50% ────────▶  Probably drop the feature
B. Duplicates
Python

# Check for duplicates
print(f"Duplicate rows: {df.duplicated().sum()}")

# See duplicate rows
print(df[df.duplicated()])

# Remove duplicates
df_clean = df.drop_duplicates()
C. Outliers
Python

# Method 1: IQR (Interquartile Range)
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df['salary'] < lower_bound) | (df['salary'] > upper_bound)]
print(f"Number of outliers: {len(outliers)}")

# Method 2: Z-Score
from scipy import stats
z_scores = stats.zscore(df['salary'])
outliers_z = df[abs(z_scores) > 3]  # More than 3 std from mean
Visual Outlier Detection
Python

# Box plot
plt.figure(figsize=(10, 4))
plt.subplot(1, 2, 1)
df['salary'].plot(kind='box')
plt.title('Box Plot')

# Histogram
plt.subplot(1, 2, 2)
df['salary'].plot(kind='hist', bins=30)
plt.title('Histogram')
plt.tight_layout()
plt.show()
2.7 Step 5: Understanding Patterns
A. Distribution Analysis
Python

# For numerical features
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Histogram
df['age'].hist(ax=axes[0, 0], bins=30)
axes[0, 0].set_title('Age Distribution')

# Density plot
df['age'].plot(kind='kde', ax=axes[0, 1])
axes[0, 1].set_title('Age Density')

# For categorical features
df['city'].value_counts().plot(kind='bar', ax=axes[1, 0])
axes[1, 0].set_title('City Distribution')

# Pie chart
df['category'].value_counts().plot(kind='pie', ax=axes[1, 1])
axes[1, 1].set_title('Category Distribution')

plt.tight_layout()
plt.show()
Distribution Types
text

NORMAL (Bell Curve)          SKEWED RIGHT              SKEWED LEFT
                             (Positive Skew)           (Negative Skew)
      ▲                           ▲                          ▲
     ╱ ╲                         ╱╲                         ╱╲
    ╱   ╲                       ╱  ╲╲                     ╱╱  ╲
   ╱     ╲                     ╱    ╲╲╲                 ╱╱╱    ╲
  ╱       ╲                   ╱       ╲╲╲╲           ╱╱╱╱       ╲
 ──────────────            ─────────────────       ─────────────────
 
 Mean = Median             Mean > Median            Mean < Median
 Example: Height           Example: Salary          Example: Age at death
B. Correlation Analysis
Python

# Correlation matrix
correlation_matrix = df.corr()
print(correlation_matrix)

# Heatmap visualization
plt.figure(figsize=(12, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Heatmap')
plt.show()
Understanding Correlation Values
Value Range	Interpretation	Action
0.9 to 1.0	Very strong positive	May be redundant features
0.7 to 0.9	Strong positive	Important relationship
0.4 to 0.7	Moderate positive	Useful relationship
0.2 to 0.4	Weak positive	Minor relationship
-0.2 to 0.2	No correlation	Independent features
-0.4 to -0.2	Weak negative	Minor inverse relationship
-1.0 to -0.7	Strong negative	Important inverse relationship
2.8 Complete Data Understanding Template
Python

def understand_data(df):
    """
    Complete data understanding function
    Use this for every new dataset
    """
    
    print("="*60)
    print("1. BASIC STRUCTURE")
    print("="*60)
    print(f"Rows: {df.shape[0]}")
    print(f"Columns: {df.shape[1]}")
    print(f"Memory Usage: {df.memory_usage().sum() / 1024**2:.2f} MB")
    
    print("\n" + "="*60)
    print("2. DATA TYPES")
    print("="*60)
    print(df.dtypes)
    
    print("\n" + "="*60)
    print("3. MISSING VALUES")
    print("="*60)
    missing = df.isnull().sum()
    missing_pct = (missing / len(df)) * 100
    missing_df = pd.DataFrame({
        'Missing Count': missing,
        'Missing %': missing_pct
    })
    print(missing_df[missing_df['Missing Count'] > 0])
    
    print("\n" + "="*60)
    print("4. NUMERICAL SUMMARY")
    print("="*60)
    print(df.describe())
    
    print("\n" + "="*60)
    print("5. CATEGORICAL SUMMARY")
    print("="*60)
    cat_cols = df.select_dtypes(include=['object', 'category']).columns
    for col in cat_cols:
        print(f"\n{col}:")
        print(df[col].value_counts().head(10))
    
    print("\n" + "="*60)
    print("6. DUPLICATES")
    print("="*60)
    print(f"Duplicate rows: {df.duplicated().sum()}")
    
    return None

# Usage
understand_data(df)
Chapter 3: Handling Missing Values
3.1 Why Missing Values Matter
text

╔════════════════════════════════════════════════════════════════╗
║  Most ML algorithms CANNOT handle missing values directly.     ║
║  Missing values cause: Errors, Biased results, Poor accuracy   ║
╚════════════════════════════════════════════════════════════════╝
3.2 Types of Missing Data
Understanding WHY data is missing helps decide HOW to handle it.

The Three Types
text

┌─────────────────────────────────────────────────────────────────────┐
│                    TYPES OF MISSING DATA                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. MCAR (Missing Completely At Random)                            │
│     ─────────────────────────────────────                          │
│     • Missingness is pure chance                                   │
│     • No pattern to what's missing                                 │
│     • Example: Survey responses lost due to technical glitch       │
│     • SAFE to delete or impute                                     │
│                                                                     │
│  2. MAR (Missing At Random)                                        │
│     ──────────────────────────                                     │
│     • Missingness depends on OTHER variables                       │
│     • Pattern exists but based on observed data                    │
│     • Example: Men less likely to answer depression questions      │
│     • Use advanced imputation methods                              │
│                                                                     │
│  3. MNAR (Missing Not At Random)                                   │
│     ─────────────────────────────                                  │
│     • Missingness depends on the MISSING value itself              │
│     • Most problematic type                                        │
│     • Example: High earners don't report salary                    │
│     • Need domain knowledge to handle                              │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
3.3 Detecting Missing Values
Python

import pandas as pd
import numpy as np

# Create sample data with missing values
df = pd.DataFrame({
    'age': [25, 30, np.nan, 45, 50],
    'salary': [50000, np.nan, 60000, np.nan, 80000],
    'city': ['NYC', 'LA', None, 'NYC', 'LA'],
    'score': [85.5, 90.0, 75.5, np.nan, 95.0]
})

print("=== ORIGINAL DATA ===")
print(df)

# Method 1: Check for null values
print("\n=== NULL CHECK ===")
print(df.isnull())

# Method 2: Count missing per column
print("\n=== MISSING COUNT PER COLUMN ===")
print(df.isnull().sum())

# Method 3: Total missing in dataset
print(f"\nTotal missing values: {df.isnull().sum().sum()}")

# Method 4: Percentage missing
print("\n=== PERCENTAGE MISSING ===")
print((df.isnull().sum() / len(df) * 100).round(2))

# Method 5: Rows with any missing value
print(f"\nRows with missing values: {df.isnull().any(axis=1).sum()}")
3.4 Strategy 1: Deletion
When to Delete
Scenario	Delete Rows	Delete Columns
Very few missing (< 5%)	✅ Safe	❌ Not recommended
Many missing in one column (> 50%)	❌ Lose too much data	✅ Consider it
Column not important	-	✅ Delete it
MCAR missing type	✅ Safe	-
Code for Deletion
Python

# Delete rows with ANY missing values
df_dropped_rows = df.dropna()
print("After dropping rows with any NaN:")
print(df_dropped_rows)

# Delete rows only if ALL values missing
df_dropped_all = df.dropna(how='all')

# Delete rows with missing in specific column
df_dropped_specific = df.dropna(subset=['age'])

# Delete columns with missing values
df_dropped_cols = df.dropna(axis=1)
print("\nAfter dropping columns with any NaN:")
print(df_dropped_cols)

# Delete column if more than 30% missing
threshold = 0.3
cols_to_keep = df.columns[df.isnull().mean() < threshold]
df_filtered = df[cols_to_keep]
3.5 Strategy 2: Simple Imputation
For Numerical Data
text

┌────────────────────────────────────────────────────────────────┐
│           NUMERICAL IMPUTATION DECISION GUIDE                  │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  Is the data normally distributed?                             │
│         │                                                      │
│         ├── YES ──▶ Use MEAN                                  │
│         │                                                      │
│         └── NO (Skewed) ──▶ Use MEDIAN                        │
│                                                                │
│  Are there outliers?                                           │
│         │                                                      │
│         ├── YES ──▶ Use MEDIAN (robust to outliers)           │
│         │                                                      │
│         └── NO ──▶ Mean or Median both work                   │
│                                                                │
└────────────────────────────────────────────────────────────────┘
Python

# Mean imputation
df['age_mean'] = df['age'].fillna(df['age'].mean())

# Median imputation
df['salary_median'] = df['salary'].fillna(df['salary'].median())

# Mode imputation (most frequent value)
df['city_mode'] = df['city'].fillna(df['city'].mode()[0])

# Constant value imputation
df['score_zero'] = df['score'].fillna(0)
df['city_unknown'] = df['city'].fillna('Unknown')

print(df)
For Categorical Data
Python

# Mode (most frequent)
df['city_mode'] = df['city'].fillna(df['city'].mode()[0])

# New category
df['city_new_cat'] = df['city'].fillna('Missing')

# Forward fill (use previous value)
df['city_ffill'] = df['city'].fillna(method='ffill')

# Backward fill (use next value)
df['city_bfill'] = df['city'].fillna(method='bfill')
3.6 Strategy 3: Advanced Imputation
A. K-Nearest Neighbors (KNN) Imputation
Concept: Find K similar rows and use their values to fill missing.

Python

from sklearn.impute import KNNImputer

# Works only with numerical data
numerical_df = df[['age', 'salary', 'score']]

# Create KNN imputer
knn_imputer = KNNImputer(n_neighbors=3)  # Use 3 nearest neighbors

# Fit and transform
imputed_data = knn_imputer.fit_transform(numerical_df)

# Convert back to DataFrame
df_knn = pd.DataFrame(imputed_data, columns=numerical_df.columns)
print("KNN Imputed Data:")
print(df_knn)
B. Iterative Imputation (MICE)
Concept: Model each feature with missing values as a function of other features.

Python

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

# Create iterative imputer
iterative_imputer = IterativeImputer(max_iter=10, random_state=42)

# Fit and transform
imputed_data = iterative_imputer.fit_transform(numerical_df)

df_iterative = pd.DataFrame(imputed_data, columns=numerical_df.columns)
print("Iterative Imputed Data:")
print(df_iterative)
C. Imputation Comparison Table
Method	Best For	Pros	Cons
Mean	Normal distribution	Simple, fast	Affected by outliers
Median	Skewed distribution	Robust to outliers	Ignores relationships
Mode	Categorical data	Simple	May be biased
KNN	Related features	Considers relationships	Slow for large data
Iterative	Complex relationships	Most accurate	Computationally expensive
3.7 Strategy 4: Using Missing as Information
Sometimes, the FACT that data is missing is informative!

Python

# Create indicator variable for missing
df['salary_was_missing'] = df['salary'].isnull().astype(int)

# Then impute the original column
df['salary'] = df['salary'].fillna(df['salary'].median())

print(df[['salary', 'salary_was_missing']])
Output:

text

   salary  salary_was_missing
0   50000                   0
1   60000                   1  ← This was imputed
2   60000                   0
3   60000                   1  ← This was imputed
4   80000                   0
3.8 Complete Missing Value Handler
Python

import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer, KNNImputer

def handle_missing_values(df, strategy='auto'):
    """
    Comprehensive missing value handler
    
    Parameters:
    -----------
    df : DataFrame
    strategy : 'auto', 'simple', 'knn', 'drop'
    
    Returns:
    --------
    DataFrame with handled missing values
    """
    df_copy = df.copy()
    
    # Get columns by type
    numerical_cols = df_copy.select_dtypes(include=[np.number]).columns
    categorical_cols = df_copy.select_dtypes(include=['object', 'category']).columns
    
    if strategy == 'drop':
        return df_copy.dropna()
    
    elif strategy == 'simple':
        # Numerical: median
        for col in numerical_cols:
            df_copy[col] = df_copy[col].fillna(df_copy[col].median())
        
        # Categorical: mode
        for col in categorical_cols:
            df_copy[col] = df_copy[col].fillna(df_copy[col].mode()[0])
    
    elif strategy == 'knn':
        # Only for numerical
        knn = KNNImputer(n_neighbors=5)
        df_copy[numerical_cols] = knn.fit_transform(df_copy[numerical_cols])
        
        # Categorical still uses mode
        for col in categorical_cols:
            df_copy[col] = df_copy[col].fillna(df_copy[col].mode()[0])
    
    elif strategy == 'auto':
        # Decide based on missing percentage
        for col in df_copy.columns:
            missing_pct = df_copy[col].isnull().mean()
            
            if missing_pct == 0:
                continue
            elif missing_pct > 0.5:
                # Create indicator then impute
                df_copy[f'{col}_missing'] = df_copy[col].isnull().astype(int)
            
            if col in numerical_cols:
                if missing_pct < 0.1:
                    df_copy[col] = df_copy[col].fillna(df_copy[col].median())
                else:
                    # Use KNN for higher missing
                    pass  # Would use KNN here
            else:
                df_copy[col] = df_copy[col].fillna('Unknown')
    
    return df_copy

# Usage
df_clean = handle_missing_values(df, strategy='simple')
print(df_clean)
Chapter 4: Encoding Categorical Variables
4.1 Why Encode Categories?
text

╔════════════════════════════════════════════════════════════════╗
║  Machine Learning algorithms understand NUMBERS, not WORDS.    ║
║  "Red", "Blue", "Green" → Must become 0, 1, 2 or similar      ║
╚════════════════════════════════════════════════════════════════╝
4.2 Types of Categorical Data
text

CATEGORICAL DATA
      │
      ├── NOMINAL (No Order)
      │     Examples:
      │     • Colors: Red, Blue, Green
      │     • Cities: NYC, LA, Chicago
      │     • Blood Type: A, B, AB, O
      │
      ├── ORDINAL (Has Order)
      │     Examples:
      │     • Education: High School < Bachelor < Master < PhD
      │     • Size: Small < Medium < Large
      │     • Rating: Poor < Fair < Good < Excellent
      │
      └── BINARY (Only 2 Values)
            Examples:
            • Gender: Male, Female
            • Yes/No
            • True/False
4.3 Encoding Decision Flowchart
text

                    START
                      │
                      ▼
            Is it Binary?
                /     \
              YES      NO
              │         │
              ▼         ▼
        Label Encode   Is there Order?
        (0 and 1)      /           \
                     YES            NO
                      │              │
                      ▼              ▼
              Ordinal Encode    How many unique values?
                                     /          \
                                  < 10          ≥ 10
                                   │              │
                                   ▼              ▼
                             One-Hot         Target Encoding
                             Encoding        or Hashing
4.4 Method 1: Label Encoding
Best for: Binary variables, Ordinal variables

Python

import pandas as pd
from sklearn.preprocessing import LabelEncoder

# Create sample data
df = pd.DataFrame({
    'gender': ['Male', 'Female', 'Female', 'Male', 'Male'],
    'size': ['Large', 'Small', 'Medium', 'Small', 'Large'],
    'city': ['NYC', 'LA', 'Chicago', 'NYC', 'LA']
})

print("=== BEFORE ===")
print(df)

# Method 1: Using pandas
df['gender_encoded'] = df['gender'].map({'Male': 0, 'Female': 1})

# Method 2: Using sklearn LabelEncoder
le = LabelEncoder()
df['city_encoded'] = le.fit_transform(df['city'])

print("\n=== AFTER ===")
print(df)

# To see the mapping
print(f"\nCity mapping: {dict(zip(le.classes_, range(len(le.classes_))))}")
Output:

text

=== BEFORE ===
   gender    size     city
0    Male   Large      NYC
1  Female   Small       LA
2  Female  Medium  Chicago
3    Male   Small      NYC
4    Male   Large       LA

=== AFTER ===
   gender    size     city  gender_encoded  city_encoded
0    Male   Large      NYC               0             2
1  Female   Small       LA               1             1
2  Female  Medium  Chicago               1             0
3    Male   Small      NYC               0             2
4    Male   Large       LA               0             1

City mapping: {'Chicago': 0, 'LA': 1, 'NYC': 2}
⚠️ WARNING: Label Encoding Problem
text

City: NYC=2, LA=1, Chicago=0

The model might think: NYC > LA > Chicago (WRONG!)
This implies an order that doesn't exist!

Use Label Encoding ONLY when:
1. Variable is binary
2. Variable has natural order
4.5 Method 2: Ordinal Encoding
Best for: Categorical variables WITH meaningful order

Python

from sklearn.preprocessing import OrdinalEncoder
import pandas as pd

df = pd.DataFrame({
    'education': ['High School', 'Bachelor', 'Master', 'PhD', 'Bachelor'],
    'size': ['Large', 'Small', 'Medium', 'Small', 'Large']
})

# Define the order explicitly
education_order = ['High School', 'Bachelor', 'Master', 'PhD']
size_order = ['Small', 'Medium', 'Large']

# Method 1: Manual mapping
education_map = {v: i for i, v in enumerate(education_order)}
df['education_encoded'] = df['education'].map(education_map)

# Method 2: Using OrdinalEncoder
oe = OrdinalEncoder(categories=[size_order])
df['size_encoded'] = oe.fit_transform(df[['size']])

print(df)
Output:

text

     education   size  education_encoded  size_encoded
0  High School  Large                0.0           2.0
1     Bachelor  Small                1.0           0.0
2       Master Medium                2.0           1.0
3          PhD  Small                3.0           0.0
4     Bachelor  Large                1.0           2.0
4.6 Method 3: One-Hot Encoding
Best for: Nominal variables with few unique values (< 10-15)

Concept Visualization
text

Original:                    One-Hot Encoded:
                             
city                         city_NYC  city_LA  city_Chicago
────                         ────────  ───────  ────────────
NYC                             1         0          0
LA                              0         1          0
Chicago                         0         0          1
NYC                             1         0          0
Code Implementation
Python

import pandas as pd

df = pd.DataFrame({
    'city': ['NYC', 'LA', 'Chicago', 'NYC', 'LA'],
    'color': ['Red', 'Blue', 'Red', 'Green', 'Blue']
})

print("=== BEFORE ===")
print(df)

# Method 1: pandas get_dummies
df_encoded = pd.get_dummies(df, columns=['city', 'color'])
print("\n=== ONE-HOT ENCODED ===")
print(df_encoded)

# Method 2: sklearn OneHotEncoder
from sklearn.preprocessing import OneHotEncoder

ohe = OneHotEncoder(sparse=False, drop='first')  # drop='first' to avoid dummy trap
encoded = ohe.fit_transform(df[['city']])

# Get feature names
feature_names = ohe.get_feature_names_out(['city'])
df_ohe = pd.DataFrame(encoded, columns=feature_names)
print("\n=== SKLEARN ONE-HOT ===")
print(df_ohe)
The Dummy Variable Trap
text

If you have 3 categories: A, B, C

Using ALL 3 columns:
city_A + city_B + city_C = 1 (always!)

This is called PERFECT MULTICOLLINEARITY
It can break some models (like Linear Regression)

SOLUTION: Drop one column (use drop='first')

Now: city_B=0 and city_C=0 means city_A=1
We only need N-1 columns for N categories
Python

# Avoid dummy trap
df_safe = pd.get_dummies(df, columns=['city'], drop_first=True)
print(df_safe)
4.7 Method 4: Target Encoding (Mean Encoding)
Best for: High cardinality categorical variables

Concept
Replace each category with the mean of the target variable for that category.

text

Category     Target      Target Encoding
─────────    ──────      ───────────────
NYC            1         
NYC            0          NYC → 0.5 (mean of 1,0)
LA             1         
LA             1          LA  → 1.0 (mean of 1,1)
Chicago        0          Chicago → 0.0 (mean of 0)
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'city': ['NYC', 'NYC', 'LA', 'LA', 'Chicago', 'Chicago'],
    'target': [1, 0, 1, 1, 0, 0]
})

# Calculate mean target for each city
target_means = df.groupby('city')['target'].mean()
print("Target means per city:")
print(target_means)

# Map to original data
df['city_target_encoded'] = df['city'].map(target_means)
print("\nEncoded DataFrame:")
print(df)
⚠️ Target Encoding Warning: Data Leakage
text

PROBLEM: You're using target information to create features
         This can cause overfitting!

SOLUTION: Use K-Fold Target Encoding
         Calculate mean using data NOT in the same fold
Python

from sklearn.model_selection import KFold

def kfold_target_encoding(df, cat_col, target_col, n_splits=5):
    """
    K-Fold Target Encoding to prevent leakage
    """
    df = df.copy()
    df['encoded'] = np.nan
    
    kf = KFold(n_splits=n_splits, shuffle=True, random_state=42)
    
    for train_idx, val_idx in kf.split(df):
        # Calculate mean from training data only
        means = df.iloc[train_idx].groupby(cat_col)[target_col].mean()
        # Apply to validation data
        df.loc[val_idx, 'encoded'] = df.loc[val_idx, cat_col].map(means)
    
    # Fill any remaining NaN with global mean
    global_mean = df[target_col].mean()
    df['encoded'] = df['encoded'].fillna(global_mean)
    
    return df['encoded']

# Usage
df['city_safe_encoded'] = kfold_target_encoding(df, 'city', 'target')
4.8 Method 5: Frequency Encoding
Best for: When frequency of occurrence is meaningful

Python

df = pd.DataFrame({
    'city': ['NYC', 'NYC', 'NYC', 'LA', 'LA', 'Chicago']
})

# Count frequency
freq = df['city'].value_counts()
print("Frequency:")
print(freq)

# Encode
df['city_freq'] = df['city'].map(freq)
print("\nEncoded:")
print(df)
Output:

text

Frequency:
NYC        3
LA         2
Chicago    1

Encoded:
      city  city_freq
0      NYC          3
1      NYC          3
2      NYC          3
3       LA          2
4       LA          2
5  Chicago          1
4.9 Method 6: Binary Encoding
Best for: High cardinality with no target information

text

Category   Label    Binary    Split into columns
────────   ─────    ──────    ──────────────────
NYC          0       00       bin_1=0, bin_0=0
LA           1       01       bin_1=0, bin_0=1
Chicago      2       10       bin_1=1, bin_0=0
Boston       3       11       bin_1=1, bin_0=1
Python

# Using category_encoders library
# pip install category_encoders

import category_encoders as ce

df = pd.DataFrame({
    'city': ['NYC', 'LA', 'Chicago', 'Boston', 'NYC']
})

# Binary Encoder
encoder = ce.BinaryEncoder(cols=['city'])
df_encoded = encoder.fit_transform(df)
print(df_encoded)
4.10 Method 7: Hash Encoding
Best for: Very high cardinality, fixed memory

Python

import category_encoders as ce

df = pd.DataFrame({
    'product_id': ['A123', 'B456', 'C789', 'D012', 'A123', 'E345']
})

# Hash to 3 columns
encoder = ce.HashingEncoder(cols=['product_id'], n_components=3)
df_encoded = encoder.fit_transform(df)
print(df_encoded)
4.11 Encoding Methods Comparison Table
Method	Best For	Cardinality	Preserves Order	Pros	Cons
Label	Binary/Ordinal	Low	Yes	Simple	Implies false order
Ordinal	Ordinal	Low-Medium	Yes	Compact	Needs manual ordering
One-Hot	Nominal	Low (<15)	No	No false order	High dimensions
Target	Any	High	No	Uses target info	Risk of leakage
Frequency	Any	Any	No	Simple, no leakage	Loses info
Binary	Nominal	Medium-High	No	Compact	Slightly complex
Hash	Nominal	Very High	No	Fixed size	Collisions possible
4.12 Complete Encoding Pipeline
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, OneHotEncoder, OrdinalEncoder

def encode_features(df, target_col=None):
    """
    Complete encoding pipeline
    """
    df_encoded = df.copy()
    
    # Get categorical columns
    cat_cols = df_encoded.select_dtypes(include=['object', 'category']).columns
    
    for col in cat_cols:
        if col == target_col:
            continue
            
        unique_values = df_encoded[col].nunique()
        
        # Binary
        if unique_values == 2:
            le = LabelEncoder()
            df_encoded[col] = le.fit_transform(df_encoded[col])
            print(f"{col}: Label Encoded (Binary)")
        
        # Low cardinality - One Hot
        elif unique_values < 10:
            dummies = pd.get_dummies(df_encoded[col], prefix=col, drop_first=True)
            df_encoded = pd.concat([df_encoded.drop(col, axis=1), dummies], axis=1)
            print(f"{col}: One-Hot Encoded")
        
        # High cardinality - Frequency
        else:
            freq = df_encoded[col].value_counts()
            df_encoded[col] = df_encoded[col].map(freq)
            print(f"{col}: Frequency Encoded")
    
    return df_encoded

# Example usage
df = pd.DataFrame({
    'gender': ['Male', 'Female', 'Male'],
    'city': ['NYC', 'LA', 'Chicago'],
    'product_id': ['A1', 'A2', 'A3']  # Assume many unique values
})

df_encoded = encode_features(df)
print(df_encoded)
Chapter 5: Feature Scaling and Normalization
5.1 Why Scale Features?
The Problem
text

Feature 1 (Age):      20, 25, 30, 35, 40
Feature 2 (Salary):   20000, 50000, 75000, 100000, 150000

Without scaling:
- Salary dominates because its numbers are HUGE
- Age becomes almost invisible to the model
- Algorithms using distance (KNN, SVM) will be WRONG
Visual Example
text

BEFORE SCALING:                    AFTER SCALING:
                                   
Age    ●●●●●                       Age    ●    ●    ●    ●    ●
      20 25 30 35 40                     0   0.25 0.5 0.75  1

Salary ●        ●    ●    ●    ●   Salary ●    ●    ●    ●    ●
     20k       50k  75k 100k 150k        0   0.25 0.5 0.75  1

Salary range = 130,000             Both now have same scale!
Age range = 20
Model ignores age!
5.2 When to Scale?
Algorithms That NEED Scaling
Algorithm	Needs Scaling?	Why?
Linear Regression	Sometimes	Coefficients are affected
Logistic Regression	Yes	Uses gradient descent
KNN	YES	Distance-based
SVM	YES	Distance-based
Neural Networks	YES	Gradient descent
K-Means	YES	Distance-based
PCA	YES	Variance-based
Algorithms That DON'T Need Scaling
Algorithm	Needs Scaling?	Why?
Decision Trees	No	Uses thresholds, not distances
Random Forest	No	Same as Decision Trees
XGBoost/LightGBM	No	Tree-based
Naive Bayes	No	Probability-based
5.3 Types of Scaling
text

┌─────────────────────────────────────────────────────────────────────┐
│                    SCALING METHODS                                  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. Min-Max Scaling (Normalization)                                │
│     • Range: [0, 1]                                                │
│     • Formula: (x - min) / (max - min)                             │
│                                                                     │
│  2. Standard Scaling (Standardization / Z-score)                   │
│     • Range: roughly [-3, 3]                                       │
│     • Formula: (x - mean) / std                                    │
│                                                                     │
│  3. Robust Scaling                                                 │
│     • Uses median and IQR                                          │
│     • Formula: (x - median) / IQR                                  │
│                                                                     │
│  4. MaxAbs Scaling                                                 │
│     • Range: [-1, 1]                                               │
│     • Formula: x / max(|x|)                                        │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
5.4 Method 1: Min-Max Scaling
Concept
text

Formula:  X_scaled = (X - X_min) / (X_max - X_min)

Example:  Age = 30, Min = 20, Max = 50
          Scaled = (30 - 20) / (50 - 20) = 10/30 = 0.33
Code
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler

# Create sample data
df = pd.DataFrame({
    'age': [20, 25, 30, 45, 50],
    'salary': [30000, 45000, 55000, 80000, 120000]
})

print("=== BEFORE SCALING ===")
print(df)
print(f"Age range: {df['age'].min()} to {df['age'].max()}")
print(f"Salary range: {df['salary'].min()} to {df['salary'].max()}")

# Apply Min-Max Scaling
scaler = MinMaxScaler()
df_scaled = pd.DataFrame(
    scaler.fit_transform(df),
    columns=df.columns
)

print("\n=== AFTER MIN-MAX SCALING ===")
print(df_scaled)
print(f"Age range: {df_scaled['age'].min():.2f} to {df_scaled['age'].max():.2f}")
print(f"Salary range: {df_scaled['salary'].min():.2f} to {df_scaled['salary'].max():.2f}")
Output:

text

=== BEFORE SCALING ===
   age  salary
0   20   30000
1   25   45000
2   30   55000
3   45   80000
4   50  120000

=== AFTER MIN-MAX SCALING ===
    age    salary
0  0.00  0.000000
1  0.17  0.166667
2  0.33  0.277778
3  0.83  0.555556
4  1.00  1.000000
When to Use Min-Max
Use When	Avoid When
Need bounded range [0,1]	Data has outliers
Neural networks	New data might be outside training range
Image pixel data	Distribution matters
5.5 Method 2: Standard Scaling (Z-Score)
Concept
text

Formula:  X_scaled = (X - mean) / std

Result:
• Mean becomes 0
• Standard deviation becomes 1
• Most values fall between -3 and +3

Example:  Age = 30, Mean = 34, Std = 11.4
          Scaled = (30 - 34) / 11.4 = -0.35
Code
Python

from sklearn.preprocessing import StandardScaler

# Apply Standard Scaling
scaler = StandardScaler()
df_scaled = pd.DataFrame(
    scaler.fit_transform(df),
    columns=df.columns
)

print("=== AFTER STANDARD SCALING ===")
print(df_scaled)
print(f"\nAge - Mean: {df_scaled['age'].mean():.10f}, Std: {df_scaled['age'].std():.2f}")
print(f"Salary - Mean: {df_scaled['salary'].mean():.10f}, Std: {df_scaled['salary'].std():.2f}")
Output:

text

=== AFTER STANDARD SCALING ===
        age    salary
0 -1.265994 -1.089725
1 -0.843996 -0.611847
2 -0.421998 -0.293367
3  0.843996  0.502991
4  1.687992  1.491948

Age - Mean: 0.0000000000, Std: 1.00
Salary - Mean: 0.0000000000, Std: 1.00
When to Use Standard Scaling
Use When	Avoid When
Data is normally distributed	Data is not normal
Using SVM, Logistic Regression	Need bounded range
General purpose scaling	Have many outliers
5.6 Method 3: Robust Scaling
Concept
text

Formula:  X_scaled = (X - median) / IQR

Where IQR = Q3 - Q1 (75th percentile - 25th percentile)

Why it works:
• Median is robust to outliers (unlike mean)
• IQR is robust to outliers (unlike std)
Code
Python

from sklearn.preprocessing import RobustScaler

# Create data with outlier
df_outlier = pd.DataFrame({
    'value': [10, 12, 14, 16, 18, 1000]  # 1000 is an outlier
})

# Compare scalers
scaler_standard = StandardScaler()
scaler_robust = RobustScaler()

df_outlier['standard'] = scaler_standard.fit_transform(df_outlier[['value']])
df_outlier['robust'] = scaler_robust.fit_transform(df_outlier[['value']])

print(df_outlier)
Output:

text

   value  standard    robust
0     10    -0.528    -0.500
1     12    -0.518    -0.167
2     14    -0.508     0.167
3     16    -0.498     0.500
4     18    -0.488     0.833
5   1000     2.540   164.667
Notice how Standard scaling compressed normal values while Robust kept them spread out!

5.7 Method 4: MaxAbs Scaling
Concept
text

Formula:  X_scaled = X / max(|X|)

Result:
• Range becomes [-1, 1]
• Preserves zero entries (important for sparse data)
• Doesn't shift/center the data
Code
Python

from sklearn.preprocessing import MaxAbsScaler

df = pd.DataFrame({
    'value': [-10, -5, 0, 5, 10, 20]
})

scaler = MaxAbsScaler()
df['scaled'] = scaler.fit_transform(df[['value']])

print(df)
Output:

text

   value  scaled
0    -10   -0.50
1     -5   -0.25
2      0    0.00
3      5    0.25
4     10    0.50
5     20    1.00
5.8 Scaling Decision Guide
text

                      START
                        │
                        ▼
                  Has outliers?
                    /       \
                 YES         NO
                  │           │
                  ▼           ▼
            Use ROBUST    Is data normally
             Scaler        distributed?
                            /        \
                         YES          NO
                          │            │
                          ▼            ▼
                    Use STANDARD   Use MIN-MAX
                       Scaler        Scaler
                       
                       
          Is it sparse data (many zeros)?
                        │
                      YES
                        │
                        ▼
                  Use MAXABS Scaler
                  (preserves zeros)
5.9 Important: Fit on Train, Transform on Test
text

╔════════════════════════════════════════════════════════════════╗
║  GOLDEN RULE OF SCALING:                                       ║
║  • fit_transform() on TRAINING data                            ║
║  • transform() only on TEST data                               ║
║  • NEVER fit on test data (causes data leakage!)               ║
╚════════════════════════════════════════════════════════════════╝
Python

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Initialize scaler
scaler = StandardScaler()

# Fit on training data and transform
X_train_scaled = scaler.fit_transform(X_train)

# Only transform test data (use same parameters from training)
X_test_scaled = scaler.transform(X_test)

# WRONG WAY - DON'T DO THIS:
# X_test_scaled = scaler.fit_transform(X_test)  # ❌ Data leakage!
5.10 Complete Scaling Pipeline
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

def scale_features(df, method='standard', columns=None):
    """
    Scale numerical features
    
    Parameters:
    -----------
    df : DataFrame
    method : 'standard', 'minmax', 'robust'
    columns : list of columns to scale (default: all numerical)
    
    Returns:
    --------
    Scaled DataFrame, Scaler object
    """
    df_scaled = df.copy()
    
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns.tolist()
    
    if method == 'standard':
        scaler = StandardScaler()
    elif method == 'minmax':
        scaler = MinMaxScaler()
    elif method == 'robust':
        scaler = RobustScaler()
    else:
        raise ValueError(f"Unknown method: {method}")
    
    df_scaled[columns] = scaler.fit_transform(df_scaled[columns])
    
    return df_scaled, scaler

# Usage
df_scaled, scaler = scale_features(df, method='standard')
print(df_scaled)
Chapter 6: Feature Transformation
6.1 What is Feature Transformation?
text

Feature Transformation = Changing the SHAPE of your data distribution

Original Data          →    Transformed Data
(Skewed, weird shape)       (Normal, better shape)
6.2 Why Transform Features?
Problem: Skewed Data
text

SKEWED RIGHT (Salary):         NORMAL (After Transform):

   ██                                ▲
   ██                               ███
   ████                            █████
   ██████                        ███████
 ███████████████               ███████████
──────────────────             ──────────────
Most values clustered          Spread evenly
at low end, few high           around center
Benefits of Transformation
Benefit	Explanation
Better model performance	Many algorithms assume normality
Reduced impact of outliers	Compression of extreme values
Stabilized variance	Variance becomes constant
Linear relationships	Non-linear becomes linear
6.3 Types of Transformations
text

┌─────────────────────────────────────────────────────────────────┐
│                   TRANSFORMATION TYPES                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. Log Transformation                                         │
│     • log(x) or log(x+1)                                       │
│     • For right-skewed data                                    │
│                                                                 │
│  2. Square Root Transformation                                 │
│     • √x                                                       │
│     • Milder than log                                          │
│                                                                 │
│  3. Box-Cox Transformation                                     │
│     • Finds optimal transformation                             │
│     • Requires positive values                                 │
│                                                                 │
│  4. Yeo-Johnson Transformation                                 │
│     • Like Box-Cox but works with negative values              │
│                                                                 │
│  5. Quantile Transformation                                    │
│     • Forces any distribution to normal                        │
│                                                                 │
│  6. Power Transformation                                       │
│     • x², x³, etc.                                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6.4 Method 1: Log Transformation
When to Use
Data is right-skewed (long tail on right)
Values are strictly positive
Common for: Salary, Price, Population, Revenue
Code
Python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Create skewed data (salary example)
np.random.seed(42)
df = pd.DataFrame({
    'salary': np.random.exponential(50000, 1000)
})

# Log transformation
df['salary_log'] = np.log(df['salary'])

# Log1p (adds 1, useful if data contains zeros)
df['salary_log1p'] = np.log1p(df['salary'])

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

df['salary'].hist(bins=50, ax=axes[0])
axes[0].set_title('Original Salary (Skewed)')

df['salary_log'].hist(bins=50, ax=axes[1])
axes[1].set_title('Log Transformed Salary (More Normal)')

plt.tight_layout()
plt.show()

# Check skewness
print(f"Original skewness: {df['salary'].skew():.2f}")
print(f"Log transformed skewness: {df['salary_log'].skew():.2f}")
Reversing Log Transformation
Python

# To reverse log transformation
original = np.exp(df['salary_log'])

# To reverse log1p transformation
original = np.expm1(df['salary_log1p'])
6.5 Method 2: Square Root Transformation
When to Use
Milder right skew
Count data
Data with zeros
Python

# Square root transformation
df['value'] = [0, 1, 4, 9, 16, 25, 100]
df['value_sqrt'] = np.sqrt(df['value'])

print(df)
Output:

text

   value  value_sqrt
0      0        0.00
1      1        1.00
2      4        2.00
3      9        3.00
4     16        4.00
5     25        5.00
6    100       10.00
6.6 Method 3: Box-Cox Transformation
Concept
text

Box-Cox finds the BEST lambda (λ) that makes data most normal:

            ┌ (x^λ - 1) / λ    if λ ≠ 0
x_boxcox = ┤
            └ log(x)           if λ = 0

The algorithm finds optimal λ automatically!
Code
Python

from scipy import stats
from sklearn.preprocessing import PowerTransformer

# Sample skewed data
np.random.seed(42)
data = np.random.exponential(2, 1000)

# Method 1: scipy
data_boxcox, lambda_value = stats.boxcox(data)
print(f"Optimal lambda: {lambda_value:.4f}")

# Method 2: sklearn PowerTransformer
pt = PowerTransformer(method='box-cox')
data_transformed = pt.fit_transform(data.reshape(-1, 1))

print(f"Original skewness: {stats.skew(data):.4f}")
print(f"Transformed skewness: {stats.skew(data_transformed):.4f}")
⚠️ Box-Cox Limitation
text

Box-Cox ONLY works with POSITIVE values (x > 0)

If you have zeros or negative values, use:
• Log1p: log(x + 1) for zeros
• Yeo-Johnson: works with any value
6.7 Method 4: Yeo-Johnson Transformation
When to Use
Data has zeros or negative values
Same goal as Box-Cox but more flexible
Python

from sklearn.preprocessing import PowerTransformer

# Data with negative values
data = np.array([-10, -5, 0, 5, 10, 50, 100]).reshape(-1, 1)

# Yeo-Johnson
pt = PowerTransformer(method='yeo-johnson')
data_transformed = pt.fit_transform(data)

print("Original vs Transformed:")
for orig, trans in zip(data.flatten(), data_transformed.flatten()):
    print(f"{orig:6.0f} → {trans:6.3f}")
6.8 Method 5: Quantile Transformation
Concept
Forces ANY distribution to follow a normal (or uniform) distribution by mapping to percentiles.

text

Original: Uniform → Transform → Normal
Original: Skewed  → Transform → Normal
Original: Bimodal → Transform → Normal

It maps each value to its percentile in the distribution,
then maps that percentile to the corresponding value in
a normal distribution.
Code
Python

from sklearn.preprocessing import QuantileTransformer

# Create bimodal data (two peaks)
np.random.seed(42)
data = np.concatenate([
    np.random.normal(10, 2, 500),
    np.random.normal(50, 5, 500)
]).reshape(-1, 1)

# Transform to normal
qt = QuantileTransformer(output_distribution='normal', random_state=42)
data_normal = qt.fit_transform(data)

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

axes[0].hist(data, bins=50)
axes[0].set_title('Original (Bimodal)')

axes[1].hist(data_normal, bins=50)
axes[1].set_title('Quantile Transformed (Normal)')

plt.tight_layout()
plt.show()
6.9 Transformation Decision Guide
text

                        START
                          │
                          ▼
                  Data has negative values?
                      /          \
                   YES            NO
                    │              │
                    ▼              ▼
              Use YEO-JOHNSON   Data has zeros?
                                  /       \
                               YES         NO
                                │           │
                                ▼           ▼
                          Use LOG1P    Use LOG or BOX-COX
                          
                          
          Is the skewness very severe?
                    /          \
                 YES            NO
                  │              │
                  ▼              ▼
          Use QUANTILE      Use SQRT
          Transformer      (milder fix)
6.10 Skewness Guide
Python

from scipy.stats import skew

# Check skewness
skewness = skew(df['column'])

"""
Skewness Interpretation:
------------------------
-0.5 to 0.5   : Approximately symmetric (may not need transformation)
0.5 to 1.0    : Moderately skewed (sqrt may work)
> 1.0         : Highly skewed (log or box-cox needed)
< -0.5        : Left skewed (try square or cube transformation)
"""

# Function to fix skewness
def fix_skewness(series, threshold=0.5):
    """
    Automatically fix skewed data
    """
    skewness = skew(series)
    
    if abs(skewness) < threshold:
        print(f"Skewness {skewness:.2f} is acceptable")
        return series
    
    if skewness > 0:  # Right skewed
        if series.min() > 0:
            transformed = np.log1p(series)
        else:
            transformed = np.sqrt(series - series.min() + 1)
    else:  # Left skewed
        transformed = series ** 2
    
    new_skewness = skew(transformed)
    print(f"Skewness: {skewness:.2f} → {new_skewness:.2f}")
    
    return transformed
6.11 Complete Transformation Pipeline
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import PowerTransformer, QuantileTransformer
from scipy.stats import skew

def transform_features(df, columns=None, method='auto'):
    """
    Transform numerical features to reduce skewness
    
    Parameters:
    -----------
    df : DataFrame
    columns : list of columns (default: all numerical)
    method : 'auto', 'log', 'sqrt', 'boxcox', 'yeojohnson', 'quantile'
    
    Returns:
    --------
    Transformed DataFrame
    """
    df_transformed = df.copy()
    
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns.tolist()
    
    for col in columns:
        original_skew = skew(df_transformed[col].dropna())
        
        if method == 'auto':
            # Skip if not very skewed
            if abs(original_skew) < 0.5:
                continue
            
            # Choose method based on data
            if df_transformed[col].min() > 0:
                method_used = 'log1p'
                df_transformed[col] = np.log1p(df_transformed[col])
            else:
                method_used = 'yeojohnson'
                pt = PowerTransformer(method='yeo-johnson')
                df_transformed[col] = pt.fit_transform(
                    df_transformed[[col]]
                ).flatten()
        
        elif method == 'log':
            df_transformed[col] = np.log1p(df_transformed[col])
        
        elif method == 'sqrt':
            df_transformed[col] = np.sqrt(df_transformed[col])
        
        elif method == 'boxcox':
            pt = PowerTransformer(method='box-cox')
            df_transformed[col] = pt.fit_transform(
                df_transformed[[col]]
            ).flatten()
        
        elif method == 'yeojohnson':
            pt = PowerTransformer(method='yeo-johnson')
            df_transformed[col] = pt.fit_transform(
                df_transformed[[col]]
            ).flatten()
        
        elif method == 'quantile':
            qt = QuantileTransformer(output_distribution='normal')
            df_transformed[col] = qt.fit_transform(
                df_transformed[[col]]
            ).flatten()
        
        new_skew = skew(df_transformed[col].dropna())
        print(f"{col}: skewness {original_skew:.2f} → {new_skew:.2f}")
    
    return df_transformed

# Usage
df_transformed = transform_features(df, method='auto')
Chapter 7: Feature Creation
7.1 What is Feature Creation?
text

Feature Creation = Making NEW columns from EXISTING columns

It's the most CREATIVE part of feature engineering!
This is where DATA SCIENTISTS add the most value.
7.2 Why Create New Features?
Before vs After Feature Creation
text

BEFORE (Raw Data):
┌─────────────┬──────────────┐
│ birth_year  │ current_year │
├─────────────┼──────────────┤
│ 1990        │ 2024         │
│ 1985        │ 2024         │
└─────────────┴──────────────┘
Model accuracy: 65%

AFTER (With Created Feature):
┌─────────────┬──────────────┬─────┐
│ birth_year  │ current_year │ AGE │  ← Created!
├─────────────┼──────────────┼─────┤
│ 1990        │ 2024         │ 34  │
│ 1985        │ 2024         │ 39  │
└─────────────┴──────────────┴─────┘
Model accuracy: 82%
7.3 Categories of Feature Creation
text

┌───────────────────────────────────────────────────────────────────────┐
│                    FEATURE CREATION METHODS                           │
├───────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  1. MATHEMATICAL OPERATIONS                                           │
│     • Addition, Subtraction, Multiplication, Division                 │
│     • Ratios and Proportions                                         │
│                                                                       │
│  2. BINNING (Discretization)                                         │
│     • Converting continuous to categorical                           │
│                                                                       │
│  3. POLYNOMIAL FEATURES                                              │
│     • Squares, cubes, interactions                                   │
│                                                                       │
│  4. DATE/TIME FEATURES                                               │
│     • Year, month, day, weekday, hour                                │
│                                                                       │
│  5. AGGREGATIONS                                                     │
│     • Group statistics (mean, sum, count by group)                   │
│                                                                       │
│  6. DOMAIN-SPECIFIC                                                  │
│     • Features based on business knowledge                           │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
7.4 Method 1: Mathematical Operations
Basic Operations
Python

import pandas as pd

df = pd.DataFrame({
    'price': [100, 200, 150, 300],
    'quantity': [10, 5, 8, 3],
    'discount': [0.1, 0.2, 0.15, 0.05],
    'area_sqft': [1000, 1500, 1200, 2000],
    'bedrooms': [2, 3, 2, 4]
})

# Addition
df['total_before_discount'] = df['price'] * df['quantity']

# Subtraction
df['discount_amount'] = df['total_before_discount'] * df['discount']
df['final_price'] = df['total_before_discount'] - df['discount_amount']

# Division (Ratio)
df['price_per_sqft'] = df['price'] / df['area_sqft']
df['sqft_per_bedroom'] = df['area_sqft'] / df['bedrooms']

# Multiplication
df['price_sqft_product'] = df['price'] * df['area_sqft']

print(df)
Common Ratio Features
Domain	Feature Name	Formula
Real Estate	Price per sqft	Price / Square_feet
E-commerce	Revenue per customer	Total_revenue / Customer_count
HR	Salary per experience	Salary / Years_experience
Finance	Debt to income	Total_debt / Annual_income
Health	BMI	Weight / Height²
7.5 Method 2: Binning (Discretization)
Concept
text

Convert continuous values into categories (bins)

Age (Continuous)    →    Age_Group (Categorical)
─────────────────        ─────────────────────────
       23           →         Young (0-30)
       45           →         Middle (31-50)
       67           →         Senior (51+)
Types of Binning
text

┌────────────────────────────────────────────────────────────────┐
│                    BINNING TYPES                               │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  1. Equal Width Binning                                        │
│     • Each bin has same range                                  │
│     • [0-33], [34-66], [67-100]                               │
│                                                                │
│  2. Equal Frequency Binning (Quantile)                        │
│     • Each bin has same number of samples                     │
│     • Useful when data is skewed                              │
│                                                                │
│  3. Custom Binning                                             │
│     • You define the boundaries                                │
│     • Based on domain knowledge                                │
│                                                                │
└────────────────────────────────────────────────────────────────┘
Code for Binning
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'age': [15, 22, 35, 45, 52, 67, 78, 29, 41, 55],
    'income': [20000, 35000, 55000, 75000, 90000, 45000, 30000, 48000, 82000, 120000]
})

print("=== ORIGINAL DATA ===")
print(df)

# Method 1: Equal Width Binning (pd.cut)
df['age_equal_width'] = pd.cut(
    df['age'], 
    bins=3,  # 3 equal-width bins
    labels=['Young', 'Middle', 'Senior']
)

# Method 2: Equal Frequency Binning (pd.qcut)
df['income_quantile'] = pd.qcut(
    df['income'],
    q=4,  # 4 quantiles (quartiles)
    labels=['Low', 'Medium', 'High', 'Very High']
)

# Method 3: Custom Binning
age_bins = [0, 18, 35, 50, 65, 100]
age_labels = ['Teen', 'Young Adult', 'Adult', 'Middle Age', 'Senior']

df['age_custom'] = pd.cut(
    df['age'],
    bins=age_bins,
    labels=age_labels
)

print("\n=== AFTER BINNING ===")
print(df)
Output:

text

=== ORIGINAL DATA ===
   age  income
0   15   20000
1   22   35000
2   35   55000
3   45   75000
4   52   90000
5   67   45000
6   78   30000
7   29   48000
8   41   82000
9   55  120000

=== AFTER BINNING ===
   age  income age_equal_width income_quantile    age_custom
0   15   20000           Young             Low          Teen
1   22   35000           Young             Low   Young Adult
2   35   55000          Middle          Medium   Young Adult
3   45   75000          Middle            High         Adult
4   52   90000          Senior       Very High   Middle Age
5   67   45000          Senior          Medium        Senior
6   78   30000          Senior             Low        Senior
7   29   48000           Young          Medium   Young Adult
8   41   82000          Middle            High         Adult
9   55  120000          Senior       Very High   Middle Age
7.6 Method 3: Polynomial Features
Concept
text

Create higher-degree features and interactions

Original:  x₁, x₂

Polynomial (degree=2):
• x₁²           (square of x1)
• x₂²           (square of x2)
• x₁ × x₂       (interaction)

This helps capture NON-LINEAR relationships!
Visual Understanding
text

LINEAR MODEL:                    WITH POLYNOMIAL:
                                 
y = a*x + b                      y = a*x² + b*x + c

   │    /                           │    ___
   │   /                            │   /   \
   │  /                             │  /     \
   │ /                              │ /       \
   │/                               │/
   └──────────                      └──────────
   
Can only fit lines               Can fit curves!
Code
Python

from sklearn.preprocessing import PolynomialFeatures
import pandas as pd
import numpy as np

df = pd.DataFrame({
    'x1': [1, 2, 3, 4, 5],
    'x2': [2, 4, 6, 8, 10]
})

print("=== ORIGINAL ===")
print(df)

# Create polynomial features
poly = PolynomialFeatures(degree=2, include_bias=False)
poly_features = poly.fit_transform(df)

# Get feature names
feature_names = poly.get_feature_names_out(['x1', 'x2'])

df_poly = pd.DataFrame(poly_features, columns=feature_names)
print("\n=== POLYNOMIAL FEATURES ===")
print(df_poly)
Output:

text

=== ORIGINAL ===
   x1  x2
0   1   2
1   2   4
2   3   6
3   4   8
4   5  10

=== POLYNOMIAL FEATURES ===
    x1    x2  x1^2  x1 x2  x2^2
0  1.0   2.0   1.0    2.0   4.0
1  2.0   4.0   4.0    8.0  16.0
2  3.0   6.0   9.0   18.0  36.0
3  4.0   8.0  16.0   32.0  64.0
4  5.0  10.0  25.0   50.0 100.0
⚠️ Warning: Polynomial Feature Explosion
text

Original features:  10
Degree 2:          65 features
Degree 3:         285 features
Degree 4:        1000+ features

SOLUTION: 
1. Use interaction_only=True (no powers)
2. Select only important polynomial features
3. Use regularization
7.7 Method 4: Date/Time Features
Concept
text

A single datetime column contains LOTS of hidden information!

"2024-06-15 14:30:00"  →  Year: 2024
                          Month: 6
                          Day: 15
                          Hour: 14
                          Minute: 30
                          Day of Week: Saturday
                          Quarter: Q2
                          Is Weekend: True
                          ...and more!
Code
Python

import pandas as pd
import numpy as np

# Create sample data with dates
df = pd.DataFrame({
    'transaction_date': pd.date_range(start='2024-01-01', periods=10, freq='D')
})

# Convert to datetime if not already
df['transaction_date'] = pd.to_datetime(df['transaction_date'])

# Extract date features
df['year'] = df['transaction_date'].dt.year
df['month'] = df['transaction_date'].dt.month
df['day'] = df['transaction_date'].dt.day
df['day_of_week'] = df['transaction_date'].dt.dayofweek  # 0=Monday, 6=Sunday
df['day_name'] = df['transaction_date'].dt.day_name()
df['quarter'] = df['transaction_date'].dt.quarter
df['week_of_year'] = df['transaction_date'].dt.isocalendar().week
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
df['is_month_start'] = df['transaction_date'].dt.is_month_start.astype(int)
df['is_month_end'] = df['transaction_date'].dt.is_month_end.astype(int)

print(df)
Time Features (for datetime with time)
Python

df['order_time'] = pd.to_datetime([
    '2024-01-15 08:30:00',
    '2024-01-15 14:45:00',
    '2024-01-15 19:15:00',
    '2024-01-15 23:30:00'
])

# Time features
df['hour'] = df['order_time'].dt.hour
df['minute'] = df['order_time'].dt.minute

# Time of day category
def time_of_day(hour):
    if 5 <= hour < 12:
        return 'Morning'
    elif 12 <= hour < 17:
        return 'Afternoon'
    elif 17 <= hour < 21:
        return 'Evening'
    else:
        return 'Night'

df['time_of_day'] = df['hour'].apply(time_of_day)

# Is business hours
df['is_business_hours'] = ((df['hour'] >= 9) & (df['hour'] < 17)).astype(int)

print(df)
Date Difference Features
Python

# Time since/until features
df['registration_date'] = pd.to_datetime('2020-01-01')
df['last_login'] = pd.to_datetime([
    '2024-01-01', '2024-02-15', '2024-03-20', '2024-05-01'
])
df['today'] = pd.to_datetime('2024-06-01')

# Days since registration
df['account_age_days'] = (df['today'] - df['registration_date']).dt.days

# Days since last login
df['days_since_login'] = (df['today'] - df['last_login']).dt.days

# Months active
df['months_active'] = df['account_age_days'] / 30

print(df[['registration_date', 'last_login', 'account_age_days', 'days_since_login']])
Cyclical Features (Advanced)
text

Problem: Month 12 (December) and Month 1 (January) are CLOSE in time
         but 12 and 1 are FAR apart numerically!

Solution: Encode as sine and cosine (cyclical encoding)
Python

import numpy as np

# Cyclical encoding for month
df['month'] = [1, 6, 12, 3]  # Jan, Jun, Dec, Mar

# Convert to radians and apply sin/cos
df['month_sin'] = np.sin(2 * np.pi * df['month'] / 12)
df['month_cos'] = np.cos(2 * np.pi * df['month'] / 12)

print(df[['month', 'month_sin', 'month_cos']])
Output:

text

   month  month_sin  month_cos
0      1   0.500000   0.866025  ← January
1      6   0.000000  -1.000000  ← June
2     12   0.000000   1.000000  ← December (close to January!)
3      3   1.000000   0.000000  ← March
7.8 Method 5: Aggregation Features
Concept
text

Calculate statistics within GROUPS and add as features

Example: Customer purchase data
- Average purchase amount PER CUSTOMER
- Total purchases PER CATEGORY
- Max/Min/Count per group
Code
Python

import pandas as pd

# Transaction data
df = pd.DataFrame({
    'customer_id': [1, 1, 1, 2, 2, 3, 3, 3, 3],
    'category': ['Electronics', 'Clothing', 'Electronics', 
                 'Clothing', 'Clothing', 'Electronics', 
                 'Food', 'Food', 'Electronics'],
    'amount': [500, 100, 300, 80, 120, 200, 50, 75, 400]
})

print("=== ORIGINAL DATA ===")
print(df)

# Customer-level aggregations
customer_agg = df.groupby('customer_id').agg({
    'amount': ['mean', 'sum', 'count', 'min', 'max', 'std']
}).reset_index()

# Flatten column names
customer_agg.columns = ['customer_id', 'avg_amount', 'total_amount', 
                        'num_transactions', 'min_amount', 'max_amount', 'std_amount']

print("\n=== CUSTOMER AGGREGATIONS ===")
print(customer_agg)

# Merge back to original data
df = df.merge(customer_agg, on='customer_id', how='left')

print("\n=== DATA WITH AGGREGATION FEATURES ===")
print(df)
Output:

text

=== ORIGINAL DATA ===
   customer_id     category  amount
0            1  Electronics     500
1            1     Clothing     100
2            1  Electronics     300
3            2     Clothing      80
4            2     Clothing     120
5            3  Electronics     200
6            3         Food      50
7            3         Food      75
8            3  Electronics     400

=== CUSTOMER AGGREGATIONS ===
   customer_id  avg_amount  total_amount  num_transactions  min_amount  max_amount   std_amount
0            1      300.00           900                 3         100         500   200.000000
1            2      100.00           200                 2          80         120    28.284271
2            3      181.25           725                 4          50         400   157.272618

=== DATA WITH AGGREGATION FEATURES ===
   customer_id     category  amount  avg_amount  total_amount  ...
0            1  Electronics     500      300.00           900  ...
1            1     Clothing     100      300.00           900  ...
...
Window/Rolling Aggregations
Python

# Time-based rolling features (for time series)
df = pd.DataFrame({
    'date': pd.date_range('2024-01-01', periods=10),
    'sales': [100, 120, 90, 150, 200, 180, 160, 210, 190, 220]
})

df = df.sort_values('date')

# Rolling mean (last 3 days)
df['rolling_mean_3'] = df['sales'].rolling(window=3).mean()

# Rolling sum (last 3 days)
df['rolling_sum_3'] = df['sales'].rolling(window=3).sum()

# Lag features (previous values)
df['sales_lag_1'] = df['sales'].shift(1)  # Yesterday's sales
df['sales_lag_7'] = df['sales'].shift(7)  # Week ago sales

# Difference from previous
df['sales_diff'] = df['sales'].diff()

# Percent change
df['sales_pct_change'] = df['sales'].pct_change()

print(df)
7.9 Method 6: Domain-Specific Features
E-Commerce Example
Python

df = pd.DataFrame({
    'user_id': [1, 1, 2, 2, 2],
    'product_price': [100, 200, 50, 75, 150],
    'cart_additions': [5, 3, 10, 2, 4],
    'purchases': [2, 1, 3, 1, 2],
    'page_views': [50, 30, 100, 20, 40],
    'time_on_site_minutes': [30, 20, 60, 15, 35]
})

# Conversion rate
df['view_to_cart_rate'] = df['cart_additions'] / df['page_views']
df['cart_to_purchase_rate'] = df['purchases'] / df['cart_additions']

# Engagement metrics
df['avg_time_per_page'] = df['time_on_site_minutes'] / df['page_views']

# Value metrics
df['avg_purchase_value'] = df['product_price'] / df['purchases']

print(df)
Real Estate Example
Python

df = pd.DataFrame({
    'price': [300000, 450000, 200000, 550000],
    'sqft': [1500, 2200, 1000, 2800],
    'bedrooms': [3, 4, 2, 5],
    'bathrooms': [2, 3, 1, 4],
    'lot_size': [5000, 8000, 3000, 10000],
    'year_built': [2000, 2015, 1980, 2020]
})

# Price per square foot
df['price_per_sqft'] = df['price'] / df['sqft']

# Room ratios
df['bed_to_bath_ratio'] = df['bedrooms'] / df['bathrooms']
df['sqft_per_bedroom'] = df['sqft'] / df['bedrooms']

# Building to lot ratio
df['building_lot_ratio'] = df['sqft'] / df['lot_size']

# Age of property
df['property_age'] = 2024 - df['year_built']
df['is_new_construction'] = (df['property_age'] <= 5).astype(int)

print(df)
Healthcare Example
Python

df = pd.DataFrame({
    'patient_id': [1, 2, 3, 4],
    'height_cm': [170, 165, 180, 155],
    'weight_kg': [70, 80, 75, 60],
    'systolic_bp': [120, 140, 130, 110],
    'diastolic_bp': [80, 90, 85, 70],
    'age': [35, 55, 45, 28],
    'cholesterol': [180, 240, 200, 170]
})

# BMI
df['height_m'] = df['height_cm'] / 100
df['bmi'] = df['weight_kg'] / (df['height_m'] ** 2)

# BMI Category
def bmi_category(bmi):
    if bmi < 18.5:
        return 'Underweight'
    elif bmi < 25:
        return 'Normal'
    elif bmi < 30:
        return 'Overweight'
    else:
        return 'Obese'

df['bmi_category'] = df['bmi'].apply(bmi_category)

# Blood pressure features
df['pulse_pressure'] = df['systolic_bp'] - df['diastolic_bp']
df['mean_arterial_pressure'] = df['diastolic_bp'] + (df['pulse_pressure'] / 3)

# Risk indicators
df['high_bp'] = (df['systolic_bp'] >= 140).astype(int)
df['high_cholesterol'] = (df['cholesterol'] >= 200).astype(int)

print(df)
7.10 Complete Feature Creation Pipeline
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import PolynomialFeatures

def create_features(df, 
                   date_columns=None,
                   create_polynomials=False,
                   create_ratios=True,
                   binning_columns=None):
    """
    Comprehensive feature creation pipeline
    
    Parameters:
    -----------
    df : DataFrame
    date_columns : list of datetime columns
    create_polynomials : bool, create polynomial features
    create_ratios : bool, create ratio features for numericals
    binning_columns : dict, {column: num_bins}
    
    Returns:
    --------
    DataFrame with new features
    """
    df_new = df.copy()
    numerical_cols = df_new.select_dtypes(include=[np.number]).columns.tolist()
    
    # 1. Date Features
    if date_columns:
        for col in date_columns:
            df_new[col] = pd.to_datetime(df_new[col])
            df_new[f'{col}_year'] = df_new[col].dt.year
            df_new[f'{col}_month'] = df_new[col].dt.month
            df_new[f'{col}_day'] = df_new[col].dt.day
            df_new[f'{col}_dayofweek'] = df_new[col].dt.dayofweek
            df_new[f'{col}_quarter'] = df_new[col].dt.quarter
            df_new[f'{col}_is_weekend'] = df_new[col].dt.dayofweek.isin([5,6]).astype(int)
    
    # 2. Polynomial Features
    if create_polynomials and len(numerical_cols) >= 2:
        poly = PolynomialFeatures(degree=2, interaction_only=True, include_bias=False)
        poly_features = poly.fit_transform(df_new[numerical_cols])
        poly_names = poly.get_feature_names_out(numerical_cols)
        
        # Add only interaction terms (skip original)
        for i, name in enumerate(poly_names):
            if ' ' in name:  # interaction terms have space
                df_new[name.replace(' ', '_x_')] = poly_features[:, i]
    
    # 3. Ratio Features
    if create_ratios and len(numerical_cols) >= 2:
        for i in range(len(numerical_cols)):
            for j in range(i+1, len(numerical_cols)):
                col1, col2 = numerical_cols[i], numerical_cols[j]
                # Avoid division by zero
                if (df_new[col2] != 0).all():
                    df_new[f'{col1}_div_{col2}'] = df_new[col1] / df_new[col2]
    
    # 4. Binning
    if binning_columns:
        for col, bins in binning_columns.items():
            df_new[f'{col}_binned'] = pd.qcut(df_new[col], q=bins, labels=False, duplicates='drop')
    
    # 5. Statistical Features
    if len(numerical_cols) >= 2:
        df_new['row_mean'] = df_new[numerical_cols].mean(axis=1)
        df_new['row_std'] = df_new[numerical_cols].std(axis=1)
        df_new['row_max'] = df_new[numerical_cols].max(axis=1)
        df_new['row_min'] = df_new[numerical_cols].min(axis=1)
    
    print(f"Created {len(df_new.columns) - len(df.columns)} new features")
    print(f"Total features: {len(df_new.columns)}")
    
    return df_new

# Usage Example
df = pd.DataFrame({
    'price': [100, 200, 150, 300],
    'quantity': [10, 5, 8, 3],
    'date': ['2024-01-15', '2024-02-20', '2024-03-10', '2024-04-05']
})

df_features = create_features(
    df,
    date_columns=['date'],
    create_polynomials=True,
    create_ratios=True,
    binning_columns={'price': 3}
)

print(df_features)
Chapter 8: Feature Selection
8.1 Why Select Features?
text

╔════════════════════════════════════════════════════════════════╗
║  MORE features ≠ BETTER model                                  ║
║                                                                 ║
║  Problems with too many features:                              ║
║  • Overfitting (model memorizes noise)                         ║
║  • Slower training and prediction                              ║
║  • Harder to interpret                                         ║
║  • Curse of dimensionality                                     ║
╚════════════════════════════════════════════════════════════════╝
The Curse of Dimensionality
text

As dimensions (features) increase:
• Data becomes sparse
• Distance metrics become meaningless
• Need exponentially more data

2 features  →  Need 100 samples
10 features →  Need 10,000 samples
100 features → Need 10^10 samples (impossible!)
8.2 Feature Selection Methods Overview
text

┌───────────────────────────────────────────────────────────────────────┐
│                    FEATURE SELECTION METHODS                          │
├───────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  1. FILTER METHODS (Independent of model)                            │
│     • Correlation                                                     │
│     • Chi-Square                                                     │
│     • ANOVA                                                          │
│     • Mutual Information                                             │
│     • Variance Threshold                                             │
│                                                                       │
│  2. WRAPPER METHODS (Uses model performance)                         │
│     • Forward Selection                                              │
│     • Backward Elimination                                           │
│     • Recursive Feature Elimination (RFE)                            │
│                                                                       │
│  3. EMBEDDED METHODS (Built into model)                              │
│     • L1 Regularization (Lasso)                                      │
│     • Tree-based feature importance                                  │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
8.3 Filter Method 1: Variance Threshold
Concept
text

Remove features with LOW variance (nearly constant values)

Feature A: [1, 1, 1, 1, 1]     → Variance = 0 → REMOVE
Feature B: [1, 2, 3, 4, 5]     → Variance = 2 → KEEP
Feature C: [1, 1, 1, 1, 2]     → Variance ≈ 0.2 → Maybe remove
Code
Python

from sklearn.feature_selection import VarianceThreshold
import pandas as pd
import numpy as np

df = pd.DataFrame({
    'constant': [1, 1, 1, 1, 1],        # Zero variance
    'low_var': [1, 1, 1, 1, 2],         # Low variance
    'good_var': [1, 2, 3, 4, 5],        # Good variance
    'high_var': [10, 50, 30, 90, 20]    # High variance
})

print("=== BEFORE ===")
print(f"Variances:\n{df.var()}\n")

# Remove features with variance < 0.5
selector = VarianceThreshold(threshold=0.5)
df_selected = selector.fit_transform(df)

# Get selected feature names
selected_features = df.columns[selector.get_support()].tolist()
print(f"Selected features: {selected_features}")

df_filtered = pd.DataFrame(df_selected, columns=selected_features)
print("\n=== AFTER ===")
print(df_filtered)
8.4 Filter Method 2: Correlation Analysis
Concept
text

Two uses of correlation:

1. REMOVE features highly correlated with EACH OTHER
   (Redundant information)
   
2. KEEP features highly correlated with TARGET
   (Useful for prediction)
Code for Removing Correlated Features
Python

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Create sample data
np.random.seed(42)
df = pd.DataFrame({
    'feature_A': np.random.randn(100),
    'feature_B': np.random.randn(100),
    'feature_C': np.random.randn(100),
})
# Make D highly correlated with A
df['feature_D'] = df['feature_A'] * 0.95 + np.random.randn(100) * 0.1

# Calculate correlation matrix
corr_matrix = df.corr().abs()

print("=== CORRELATION MATRIX ===")
print(corr_matrix)

# Visualize
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Feature Correlation')
plt.show()

# Find highly correlated pairs
def get_highly_correlated(df, threshold=0.8):
    """
    Find pairs of features with correlation above threshold
    """
    corr_matrix = df.corr().abs()
    
    # Get upper triangle (to avoid duplicates)
    upper_tri = corr_matrix.where(
        np.triu(np.ones(corr_matrix.shape), k=1).astype(bool)
    )
    
    # Find pairs above threshold
    high_corr_pairs = []
    for col in upper_tri.columns:
        for idx in upper_tri.index:
            if upper_tri.loc[idx, col] > threshold:
                high_corr_pairs.append((idx, col, upper_tri.loc[idx, col]))
    
    return high_corr_pairs

high_corr = get_highly_correlated(df, threshold=0.8)
print(f"\nHighly correlated pairs: {high_corr}")

# Remove one from each correlated pair
def remove_correlated_features(df, threshold=0.8):
    """
    Remove one feature from each highly correlated pair
    """
    corr_matrix = df.corr().abs()
    upper_tri = corr_matrix.where(
        np.triu(np.ones(corr_matrix.shape), k=1).astype(bool)
    )
    
    # Find columns to drop
    to_drop = [col for col in upper_tri.columns 
               if any(upper_tri[col] > threshold)]
    
    return df.drop(columns=to_drop), to_drop

df_filtered, dropped = remove_correlated_features(df, threshold=0.8)
print(f"\nDropped features: {dropped}")
print(f"Remaining features: {df_filtered.columns.tolist()}")
Code for Correlation with Target
Python

# Sample with target
df = pd.DataFrame({
    'feature1': [1, 2, 3, 4, 5],
    'feature2': [5, 4, 3, 2, 1],
    'feature3': [1, 1, 2, 2, 3],
    'feature4': [2, 2, 2, 2, 2],  # No correlation with anything
    'target': [2, 4, 5, 8, 10]
})

# Correlation with target
target_corr = df.corr()['target'].drop('target').abs().sort_values(ascending=False)
print("Correlation with target:")
print(target_corr)

# Select features above threshold
threshold = 0.5
selected_features = target_corr[target_corr > threshold].index.tolist()
print(f"\nFeatures with |correlation| > {threshold}: {selected_features}")
8.5 Filter Method 3: Chi-Square Test
Concept
text

For CATEGORICAL features with CATEGORICAL target

Tests if there is a significant relationship between
the feature and the target

High chi-square value = Feature is likely useful
Code
Python

from sklearn.feature_selection import chi2, SelectKBest
from sklearn.preprocessing import LabelEncoder
import pandas as pd
import numpy as np

# Sample data (categorical features, categorical target)
df = pd.DataFrame({
    'color': ['red', 'blue', 'red', 'green', 'blue', 'red', 'green', 'blue'],
    'size': ['small', 'large', 'small', 'large', 'small', 'large', 'small', 'large'],
    'shape': ['round', 'square', 'round', 'round', 'square', 'round', 'square', 'round'],
    'target': [1, 0, 1, 0, 0, 1, 0, 0]
})

# Encode categorical features (chi-square needs numeric)
le = LabelEncoder()
df_encoded = df.apply(le.fit_transform)

X = df_encoded.drop('target', axis=1)
y = df_encoded['target']

# Apply chi-square test
chi2_scores, p_values = chi2(X, y)

# Create results DataFrame
chi2_results = pd.DataFrame({
    'feature': X.columns,
    'chi2_score': chi2_scores,
    'p_value': p_values
}).sort_values('chi2_score', ascending=False)

print("Chi-Square Results:")
print(chi2_results)

# Select top k features
selector = SelectKBest(chi2, k=2)
X_selected = selector.fit_transform(X, y)

selected_features = X.columns[selector.get_support()].tolist()
print(f"\nTop 2 features: {selected_features}")
8.6 Filter Method 4: ANOVA F-Test
Concept
text

For NUMERICAL features with CATEGORICAL target

Tests if the mean of the feature differs significantly
across target classes

High F-score = Feature separates classes well
Code
Python

from sklearn.feature_selection import f_classif, SelectKBest
import pandas as pd
import numpy as np

# Sample data (numerical features, categorical target)
np.random.seed(42)
df = pd.DataFrame({
    'feature1': np.concatenate([np.random.normal(0, 1, 50), 
                                np.random.normal(3, 1, 50)]),  # Good separator
    'feature2': np.random.randn(100),                          # Poor separator
    'feature3': np.concatenate([np.random.normal(-2, 1, 50), 
                                np.random.normal(2, 1, 50)]),  # Excellent separator
    'target': [0]*50 + [1]*50
})

X = df.drop('target', axis=1)
y = df['target']

# ANOVA F-test
f_scores, p_values = f_classif(X, y)

results = pd.DataFrame({
    'feature': X.columns,
    'f_score': f_scores,
    'p_value': p_values
}).sort_values('f_score', ascending=False)

print("ANOVA F-Test Results:")
print(results)
8.7 Filter Method 5: Mutual Information
Concept
text

Measures how much knowing one variable tells you about another

Works for both:
• Numerical features + Categorical target
• Categorical features + Numerical target

Captures NON-LINEAR relationships (unlike correlation!)
Code
Python

from sklearn.feature_selection import mutual_info_classif, mutual_info_regression
import pandas as pd
import numpy as np

# For classification (categorical target)
np.random.seed(42)
X = pd.DataFrame({
    'linear_feature': np.linspace(0, 10, 100),
    'nonlinear_feature': np.sin(np.linspace(0, 6*np.pi, 100)),
    'random_feature': np.random.randn(100)
})

# Create target with non-linear relationship
y = (X['nonlinear_feature'] > 0).astype(int)

# Calculate mutual information
mi_scores = mutual_info_classif(X, y)

results = pd.DataFrame({
    'feature': X.columns,
    'mi_score': mi_scores
}).sort_values('mi_score', ascending=False)

print("Mutual Information Scores:")
print(results)

# For regression (numerical target)
y_reg = X['nonlinear_feature'] + X['linear_feature'] * 0.5

mi_scores_reg = mutual_info_regression(X, y_reg)

results_reg = pd.DataFrame({
    'feature': X.columns,
    'mi_score': mi_scores_reg
}).sort_values('mi_score', ascending=False)

print("\nMutual Information (Regression):")
print(results_reg)
8.8 Wrapper Method: Recursive Feature Elimination (RFE)
Concept
text

1. Train model with ALL features
2. Rank features by importance
3. Remove LEAST important feature
4. Repeat until desired number of features

Like elimination rounds in a competition!
Code
Python

from sklearn.feature_selection import RFE, RFECV
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import make_classification
import pandas as pd

# Create sample data
X, y = make_classification(n_samples=1000, n_features=20, 
                          n_informative=5, n_redundant=5,
                          random_state=42)

feature_names = [f'feature_{i}' for i in range(20)]
X_df = pd.DataFrame(X, columns=feature_names)

# Initialize model
model = RandomForestClassifier(n_estimators=100, random_state=42)

# RFE - Select top 5 features
rfe = RFE(estimator=model, n_features_to_select=5)
rfe.fit(X_df, y)

# Results
rfe_results = pd.DataFrame({
    'feature': feature_names,
    'ranking': rfe.ranking_,
    'selected': rfe.support_
}).sort_values('ranking')

print("RFE Results:")
print(rfe_results.head(10))

# RFECV - Automatically find optimal number of features
rfecv = RFECV(estimator=model, step=1, cv=5, scoring='accuracy')
rfecv.fit(X_df, y)

print(f"\nOptimal number of features: {rfecv.n_features_}")
print(f"Selected features: {X_df.columns[rfecv.support_].tolist()}")

# Plot number of features vs CV score
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))
plt.plot(range(1, len(rfecv.cv_results_['mean_test_score']) + 1), 
         rfecv.cv_results_['mean_test_score'])
plt.xlabel('Number of Features')
plt.ylabel('CV Accuracy')
plt.title('RFECV - Optimal Feature Count')
plt.show()
8.9 Embedded Method: L1 Regularization (Lasso)
Concept
text

Lasso adds a penalty for having non-zero coefficients

Result: Many coefficients become EXACTLY ZERO
        → Automatic feature selection!

Features with coefficient = 0 are eliminated
Code
Python

from sklearn.linear_model import LassoCV, Lasso
from sklearn.preprocessing import StandardScaler
import pandas as pd
import numpy as np

# Create sample data
np.random.seed(42)
n_samples = 1000
X = pd.DataFrame({
    'important_1': np.random.randn(n_samples),
    'important_2': np.random.randn(n_samples),
    'important_3': np.random.randn(n_samples),
    'noise_1': np.random.randn(n_samples),
    'noise_2': np.random.randn(n_samples),
    'noise_3': np.random.randn(n_samples),
})

# Target depends only on important features
y = 3*X['important_1'] + 2*X['important_2'] - X['important_3'] + np.random.randn(n_samples)*0.5

# Scale features (important for Lasso)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Use LassoCV to find optimal alpha
lasso_cv = LassoCV(cv=5, random_state=42)
lasso_cv.fit(X_scaled, y)

print(f"Optimal alpha: {lasso_cv.alpha_:.4f}")

# Get feature importances (coefficients)
lasso_results = pd.DataFrame({
    'feature': X.columns,
    'coefficient': lasso_cv.coef_
}).sort_values('coefficient', key=abs, ascending=False)

print("\nLasso Coefficients:")
print(lasso_results)

# Selected features (non-zero coefficients)
selected = lasso_results[lasso_results['coefficient'] != 0]['feature'].tolist()
print(f"\nSelected features: {selected}")
8.10 Embedded Method: Tree-Based Feature Importance
Concept
text

Tree-based models calculate feature importance automatically!

Random Forest: Average decrease in impurity across all trees
XGBoost: Gain, weight, or cover metrics
Code
Python

from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.datasets import make_classification
import pandas as pd
import matplotlib.pyplot as plt

# Create sample data
X, y = make_classification(n_samples=1000, n_features=15, 
                          n_informative=5, n_redundant=3,
                          random_state=42)
feature_names = [f'feature_{i}' for i in range(15)]

# Random Forest
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X, y)

# Feature importances
rf_importance = pd.DataFrame({
    'feature': feature_names,
    'importance': rf.feature_importances_
}).sort_values('importance', ascending=False)

print("Random Forest Feature Importance:")
print(rf_importance)

# Visualize
plt.figure(figsize=(10, 6))
plt.barh(rf_importance['feature'], rf_importance['importance'])
plt.xlabel('Importance')
plt.title('Random Forest Feature Importance')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()

# Select features above threshold
threshold = 0.05
selected_features = rf_importance[rf_importance['importance'] > threshold]['feature'].tolist()
print(f"\nFeatures with importance > {threshold}: {selected_features}")
Using XGBoost
Python

import xgboost as xgb

# XGBoost model
xgb_model = xgb.XGBClassifier(n_estimators=100, random_state=42)
xgb_model.fit(X, y)

# Multiple importance types
importance_types = ['weight', 'gain', 'cover']

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for ax, imp_type in zip(axes, importance_types):
    importance = xgb_model.get_booster().get_score(importance_type=imp_type)
    
    # Sort and plot
    sorted_imp = sorted(importance.items(), key=lambda x: x[1], reverse=True)
    
    ax.barh([x[0] for x in sorted_imp], [x[1] for x in sorted_imp])
    ax.set_title(f'XGBoost - {imp_type.capitalize()}')
    ax.invert_yaxis()

plt.tight_layout()
plt.show()
8.11 Feature Selection Summary
Method	Type	Best For	Pros	Cons
Variance Threshold	Filter	All	Fast, simple	Ignores target
Correlation	Filter	Numerical	Intuitive	Only linear relationships
Chi-Square	Filter	Categorical	Statistical rigor	Only categorical
ANOVA	Filter	Num feat, Cat target	Statistical rigor	Assumes normality
Mutual Information	Filter	Any	Captures non-linear	Slow
RFE	Wrapper	Any	Uses model	Very slow
Lasso	Embedded	Regression	Automatic	Assumes linearity
Tree Importance	Embedded	Tree models	Fast, reliable	Model-specific
8.12 Complete Feature Selection Pipeline
Python

import pandas as pd
import numpy as np
from sklearn.feature_selection import (
    VarianceThreshold, SelectKBest, f_classif, 
    mutual_info_classif, RFE
)
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import StandardScaler

def select_features(X, y, methods=['variance', 'correlation', 'importance'], 
                   k_best=10):
    """
    Comprehensive feature selection pipeline
    
    Parameters:
    -----------
    X : DataFrame of features
    y : Series of target
    methods : list of methods to use
    k_best : number of features to select
    
    Returns:
    --------
    Selected features list
    """
    
    results = {}
    
    # 1. Variance Threshold
    if 'variance' in methods:
        selector = VarianceThreshold(threshold=0.01)
        selector.fit(X)
        variance_features = X.columns[selector.get_support()].tolist()
        results['variance'] = variance_features
        print(f"Variance threshold: {len(variance_features)} features")
    
    # 2. Correlation with target
    if 'correlation' in methods:
        correlations = X.apply(lambda col: col.corr(y)).abs()
        correlation_features = correlations.nlargest(k_best).index.tolist()
        results['correlation'] = correlation_features
        print(f"Correlation: {len(correlation_features)} features")
    
    # 3. Mutual Information
    if 'mutual_info' in methods:
        mi_scores = mutual_info_classif(X, y)
        mi_features = X.columns[np.argsort(mi_scores)[-k_best:]].tolist()
        results['mutual_info'] = mi_features
        print(f"Mutual Information: {len(mi_features)} features")
    
    # 4. Tree-based importance
    if 'importance' in methods:
        rf = RandomForestClassifier(n_estimators=100, random_state=42)
        rf.fit(X, y)
        importances = pd.Series(rf.feature_importances_, index=X.columns)
        importance_features = importances.nlargest(k_best).index.tolist()
        results['importance'] = importance_features
        print(f"Tree importance: {len(importance_features)} features")
    
    # 5. RFE
    if 'rfe' in methods:
        rf = RandomForestClassifier(n_estimators=50, random_state=42)
        rfe = RFE(rf, n_features_to_select=k_best)
        rfe.fit(X, y)
        rfe_features = X.columns[rfe.support_].tolist()
        results['rfe'] = rfe_features
        print(f"RFE: {len(rfe_features)} features")
    
    # Find consensus features (appear in multiple methods)
    all_features = []
    for features in results.values():
        all_features.extend(features)
    
    from collections import Counter
    feature_counts = Counter(all_features)
    
    # Features appearing in at least half of methods
    min_count = len(results) // 2
    consensus_features = [f for f, c in feature_counts.items() if c >= min_count]
    
    print(f"\nConsensus features (appear in >= {min_count} methods): {len(consensus_features)}")
    print(consensus_features)
    
    return consensus_features, results

# Usage
from sklearn.datasets import make_classification

X, y = make_classification(n_samples=1000, n_features=20, 
                          n_informative=5, random_state=42)
X_df = pd.DataFrame(X, columns=[f'feature_{i}' for i in range(20)])
y = pd.Series(y)

selected, details = select_features(X_df, y, k_best=8)
Chapter 9: Handling Imbalanced Data
9.1 What is Imbalanced Data?
text

╔════════════════════════════════════════════════════════════════╗
║  Imbalanced Data = One class has MUCH MORE samples than others ║
╚════════════════════════════════════════════════════════════════╝

Example: Fraud Detection
┌─────────────────────────────────────────────────────────┐
│  Normal transactions:    99,000  (99%)                 │
│  Fraudulent transactions: 1,000  (1%)                  │
│                                                         │
│  Normal: ████████████████████████████████████████      │
│  Fraud:  █                                              │
└─────────────────────────────────────────────────────────┘
9.2 Why is Imbalance a Problem?
text

If model predicts EVERYONE as "Not Fraud":
• Accuracy = 99% (looks great!)
• But catches 0% of actual frauds (terrible!)

The model takes the EASY path - predicting majority class always.
Metrics That Fail
Metric	Value	Interpretation
Accuracy	99%	Misleading!
Precision (Fraud)	0%	Terrible
Recall (Fraud)	0%	Terrible
F1-Score	0%	Terrible
9.3 Solutions Overview
text

┌────────────────────────────────────────────────────────────────────┐
│              HANDLING IMBALANCED DATA                              │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  1. RESAMPLING                                                    │
│     ├── Oversampling (increase minority)                          │
│     │     • Random Oversampling                                   │
│     │     • SMOTE                                                 │
│     │     • ADASYN                                                │
│     │                                                              │
│     └── Undersampling (decrease majority)                        │
│           • Random Undersampling                                  │
│           • Tomek Links                                           │
│           • NearMiss                                              │
│                                                                    │
│  2. ALGORITHM-LEVEL                                               │
│     • Class weights                                               │
│     • Cost-sensitive learning                                     │
│                                                                    │
│  3. EVALUATION METRICS                                            │
│     • Use F1, Precision, Recall, AUC-ROC                         │
│     • NOT accuracy!                                               │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
9.4 Resampling: Random Oversampling
Concept
text

BEFORE:                          AFTER:
Majority: ████████████████       Majority: ████████████████
Minority: ██                     Minority: ████████████████ (duplicated)
Code
Python

from imblearn.over_sampling import RandomOverSampler
from collections import Counter
import numpy as np

# Create imbalanced data
np.random.seed(42)
X = np.random.randn(1000, 5)
y = np.array([0]*950 + [1]*50)  # 95% vs 5%

print(f"Before: {Counter(y)}")

# Random oversample
ros = RandomOverSampler(random_state=42)
X_resampled, y_resampled = ros.fit_resample(X, y)

print(f"After:  {Counter(y_resampled)}")
Output:

text

Before: Counter({0: 950, 1: 50})
After:  Counter({0: 950, 1: 950})
⚠️ Warning
text

Random oversampling DUPLICATES minority samples exactly.
This can lead to OVERFITTING!
9.5 Resampling: SMOTE
Concept
text

SMOTE = Synthetic Minority Over-sampling Technique

Instead of duplicating:
1. Take a minority sample
2. Find its k nearest minority neighbors
3. Create NEW synthetic samples between them

Creates NEW samples, not duplicates!
Visual
text

Original minority points: A and B

A ●─────────────────────● B

SMOTE creates synthetic points along the line:

A ●───●───●───●───●────● B
      ↑   ↑   ↑   ↑
      Synthetic samples
Code
Python

from imblearn.over_sampling import SMOTE
from collections import Counter
import numpy as np
import matplotlib.pyplot as plt

# Create imbalanced 2D data for visualization
np.random.seed(42)
X = np.vstack([
    np.random.randn(200, 2) + [2, 2],  # Majority class
    np.random.randn(20, 2) + [-2, -2]  # Minority class
])
y = np.array([0]*200 + [1]*20)

print(f"Before: {Counter(y)}")

# Apply SMOTE
smote = SMOTE(random_state=42)
X_smote, y_smote = smote.fit_resample(X, y)

print(f"After:  {Counter(y_smote)}")

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Before
axes[0].scatter(X[y==0, 0], X[y==0, 1], label='Majority', alpha=0.5)
axes[0].scatter(X[y==1, 0], X[y==1, 1], label='Minority', alpha=0.5)
axes[0].set_title('Before SMOTE')
axes[0].legend()

# After
axes[1].scatter(X_smote[y_smote==0, 0], X_smote[y_smote==0, 1], label='Majority', alpha=0.5)
axes[1].scatter(X_smote[y_smote==1, 0], X_smote[y_smote==1, 1], label='Minority (incl. synthetic)', alpha=0.5)
axes[1].set_title('After SMOTE')
axes[1].legend()

plt.tight_layout()
plt.show()
SMOTE Variants
Variant	Description	When to Use
SMOTE	Basic synthetic oversampling	General use
SMOTE-Borderline	Focus on borderline samples	When classes overlap
SMOTE-SVM	Uses SVM to find important samples	When decision boundary matters
ADASYN	More samples where harder to learn	Adaptive synthetic
9.6 Resampling: Random Undersampling
Concept
text

BEFORE:                          AFTER:
Majority: ████████████████       Majority: ██ (reduced)
Minority: ██                     Minority: ██
Code
Python

from imblearn.under_sampling import RandomUnderSampler
from collections import Counter

# Random undersample
rus = RandomUnderSampler(random_state=42)
X_under, y_under = rus.fit_resample(X, y)

print(f"Before: {Counter(y)}")
print(f"After:  {Counter(y_under)}")
⚠️ Warning
text

Undersampling LOSES information from majority class!
Use only when you have LOTS of data.
9.7 Resampling: Tomek Links
Concept
text

Tomek Link = A pair of samples from different classes
             that are each other's nearest neighbor

These are samples near the decision boundary.

Remove the majority sample from each Tomek Link
→ Creates clearer class separation
Code
Python

from imblearn.under_sampling import TomekLinks

# Apply Tomek Links
tomek = TomekLinks()
X_tomek, y_tomek = tomek.fit_resample(X, y)

print(f"Before: {Counter(y)}")
print(f"After:  {Counter(y_tomek)}")
9.8 Combined: SMOTE + Undersampling
Concept
text

Best of both worlds:
1. First oversample minority with SMOTE
2. Then undersample majority

Result: Balanced dataset without extreme duplication or loss
Code
Python

from imblearn.combine import SMOTEENN, SMOTETomek

# SMOTE + ENN (Edited Nearest Neighbors)
smote_enn = SMOTEENN(random_state=42)
X_combined, y_combined = smote_enn.fit_resample(X, y)

print(f"SMOTE + ENN: {Counter(y_combined)}")

# SMOTE + Tomek Links
smote_tomek = SMOTETomek(random_state=42)
X_combined2, y_combined2 = smote_tomek.fit_resample(X, y)

print(f"SMOTE + Tomek: {Counter(y_combined2)}")
9.9 Class Weights
Concept
text

Instead of changing data, tell the model:
"Minority class mistakes are MORE COSTLY"

Weight = 1 / class_frequency

Minority class gets HIGHER weight → Model pays more attention
Code
Python

from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression
import numpy as np

# Create imbalanced data
np.random.seed(42)
X = np.random.randn(1000, 5)
y = np.array([0]*950 + [1]*50)

# Method 1: class_weight='balanced'
rf_balanced = RandomForestClassifier(class_weight='balanced', random_state=42)
rf_balanced.fit(X, y)

# Method 2: Custom weights
# Weight for class 1 should be higher (it's minority)
custom_weights = {0: 1, 1: 19}  # Ratio is 950:50 = 19:1
rf_custom = RandomForestClassifier(class_weight=custom_weights, random_state=42)
rf_custom.fit(X, y)

# For Logistic Regression
lr_balanced = LogisticRegression(class_weight='balanced', random_state=42)
lr_balanced.fit(X, y)

print("Models trained with class weights!")
How 'balanced' Weights are Calculated
Python

from sklearn.utils.class_weight import compute_class_weight

classes = np.unique(y)
weights = compute_class_weight('balanced', classes=classes, y=y)

print(f"Classes: {classes}")
print(f"Weights: {weights}")
# Class 0: 0.526 (lower because more samples)
# Class 1: 10.0 (higher because fewer samples)
9.10 Proper Evaluation Metrics
Do NOT Use Accuracy!
Python

from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, 
    f1_score, roc_auc_score, confusion_matrix,
    classification_report
)
from sklearn.model_selection import train_test_split

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, stratify=y)

# Train model
model = RandomForestClassifier(class_weight='balanced', random_state=42)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
y_pred_proba = model.predict_proba(X_test)[:, 1]

# Metrics
print("=== CLASSIFICATION REPORT ===")
print(classification_report(y_test, y_pred))

print("\n=== CONFUSION MATRIX ===")
cm = confusion_matrix(y_test, y_pred)
print(cm)
print("""
Interpretation:
[[TN  FP]
 [FN  TP]]

TN = True Negative (correctly predicted 0)
FP = False Positive (predicted 1, was 0)
FN = False Negative (predicted 0, was 1)  ← Most costly in fraud!
TP = True Positive (correctly predicted 1)
""")

print(f"\n=== KEY METRICS ===")
print(f"Accuracy: {accuracy_score(y_test, y_pred):.3f}")
print(f"Precision: {precision_score(y_test, y_pred):.3f}")
print(f"Recall: {recall_score(y_test, y_pred):.3f}")
print(f"F1-Score: {f1_score(y_test, y_pred):.3f}")
print(f"ROC-AUC: {roc_auc_score(y_test, y_pred_proba):.3f}")
Which Metric to Use?
Scenario	Priority Metric	Why
Fraud Detection	Recall	Catch all frauds, even with false alarms
Spam Filter	Precision	Don't mark good emails as spam
Medical Diagnosis	Recall	Don't miss any disease
General	F1-Score	Balance precision and recall
9.11 Complete Imbalanced Data Pipeline
Python

import numpy as np
import pandas as pd
from collections import Counter
from sklearn.model_selection import train_test_split, cross_val_score, StratifiedKFold
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, roc_auc_score
from imblearn.over_sampling import SMOTE
from imblearn.pipeline import Pipeline as ImbPipeline

def handle_imbalanced_data(X, y, method='smote', model=None):
    """
    Complete pipeline for handling imbalanced data
    
    Parameters:
    -----------
    X : feature matrix
    y : target array
    method : 'smote', 'undersample', 'class_weight', 'combined'
    model : sklearn model (default: RandomForestClassifier)
    
    Returns:
    --------
    Trained model, evaluation metrics
    """
    
    if model is None:
        model = RandomForestClassifier(n_estimators=100, random_state=42)
    
    # Split BEFORE resampling (critical!)
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, stratify=y, random_state=42
    )
    
    print(f"Original training distribution: {Counter(y_train)}")
    
    if method == 'smote':
        # Apply SMOTE only to training data
        smote = SMOTE(random_state=42)
        X_train_res, y_train_res = smote.fit_resample(X_train, y_train)
        print(f"After SMOTE: {Counter(y_train_res)}")
        
        model.fit(X_train_res, y_train_res)
    
    elif method == 'class_weight':
        # Use class weights instead of resampling
        if hasattr(model, 'class_weight'):
            model.set_params(class_weight='balanced')
        model.fit(X_train, y_train)
    
    elif method == 'combined':
        from imblearn.combine import SMOTETomek
        combined = SMOTETomek(random_state=42)
        X_train_res, y_train_res = combined.fit_resample(X_train, y_train)
        print(f"After SMOTE + Tomek: {Counter(y_train_res)}")
        
        model.fit(X_train_res, y_train_res)
    
    else:
        model.fit(X_train, y_train)
    
    # Evaluate on ORIGINAL test set
    y_pred = model.predict(X_test)
    y_pred_proba = model.predict_proba(X_test)[:, 1]
    
    print("\n=== EVALUATION ON TEST SET ===")
    print(classification_report(y_test, y_pred))
    print(f"ROC-AUC Score: {roc_auc_score(y_test, y_pred_proba):.3f}")
    
    return model

# Usage
np.random.seed(42)
X = np.random.randn(1000, 10)
y = np.array([0]*950 + [1]*50)

print("=== METHOD: SMOTE ===")
model_smote = handle_imbalanced_data(X, y, method='smote')

print("\n" + "="*50)
print("=== METHOD: CLASS WEIGHT ===")
model_weight = handle_imbalanced_data(X, y, method='class_weight')
Chapter 10: Time Series Feature Engineering
10.1 What Makes Time Series Special?
text

╔════════════════════════════════════════════════════════════════╗
║  Time Series = Data points ordered by TIME                     ║
║                                                                 ║
║  Key Properties:                                               ║
║  • Temporal ordering matters                                   ║
║  • Past values can predict future                              ║
║  • Patterns: Trend, Seasonality, Cycles                        ║
╚════════════════════════════════════════════════════════════════╝
Examples of Time Series
Domain	Example
Finance	Stock prices, Exchange rates
Retail	Daily sales, Inventory levels
Weather	Temperature, Rainfall
Web	Page views, Server load
IoT	Sensor readings
10.2 Time Series Components
text

TIME SERIES DECOMPOSITION
                                    
Original = Trend + Seasonality + Residual

   │\      /\                        TREND
   │ \    /  \    /\                 (Long-term direction)
   │  \  /    \  /  \    
   │   \/      \/    \              
   └─────────────────────────→
   
   │  ∧    ∧    ∧    ∧              SEASONALITY
   │ / \  / \  / \  / \             (Repeating patterns)
   │/   \/   \/   \/   \
   └─────────────────────────→
   
   │  ~  ~   ~  ~ ~   ~~            RESIDUAL
   │~   ~  ~  ~   ~ ~   ~           (Random noise)
   └─────────────────────────→
10.3 Lag Features
Concept
text

Lag = Using past values as features

Today's sales might depend on yesterday's sales!

Date       | Sales | Lag_1 | Lag_2 | Lag_7
─────────────────────────────────────────────
2024-01-01 |  100  |  NaN  |  NaN  |  NaN
2024-01-02 |  120  |  100  |  NaN  |  NaN
2024-01-03 |  90   |  120  |  100  |  NaN
2024-01-04 |  150  |  90   |  120  |  100
...
2024-01-08 |  130  |  110  |  140  |  100  ← 7 days ago
Code
Python

import pandas as pd
import numpy as np

# Create sample time series
dates = pd.date_range('2024-01-01', periods=30, freq='D')
np.random.seed(42)
df = pd.DataFrame({
    'date': dates,
    'sales': np.random.randint(100, 200, 30) + np.arange(30) * 2  # Sales with trend
})

print("=== ORIGINAL DATA ===")
print(df.head(10))

# Create lag features
for lag in [1, 2, 3, 7]:
    df[f'sales_lag_{lag}'] = df['sales'].shift(lag)

print("\n=== WITH LAG FEATURES ===")
print(df.head(10))
10.4 Rolling Window Features
Concept
text

Calculate statistics over a SLIDING WINDOW

Window size = 3:

Day 1: [100]           → Cannot calculate (need 3 values)
Day 2: [100, 120]      → Cannot calculate
Day 3: [100, 120, 90]  → Mean = 103.3
Day 4: [120, 90, 150]  → Mean = 120.0  (window slides forward)
Day 5: [90, 150, 130]  → Mean = 123.3
Code
Python

# Rolling statistics
window_size = 7

# Rolling mean
df['rolling_mean_7'] = df['sales'].rolling(window=window_size).mean()

# Rolling standard deviation
df['rolling_std_7'] = df['sales'].rolling(window=window_size).std()

# Rolling min/max
df['rolling_min_7'] = df['sales'].rolling(window=window_size).min()
df['rolling_max_7'] = df['sales'].rolling(window=window_size).max()

# Rolling sum
df['rolling_sum_7'] = df['sales'].rolling(window=window_size).sum()

print("=== ROLLING FEATURES ===")
print(df[['date', 'sales', 'rolling_mean_7', 'rolling_std_7']].head(15))
Multiple Window Sizes
Python

# Create features for multiple windows
for window in [3, 7, 14, 30]:
    df[f'rolling_mean_{window}'] = df['sales'].rolling(window=window).mean()
    df[f'rolling_std_{window}'] = df['sales'].rolling(window=window).std()

print(df.head(20))
10.5 Expanding Window Features
Concept
text

Expanding window = Includes ALL past data up to current point

Day 1: [100]                    → Mean = 100.0
Day 2: [100, 120]               → Mean = 110.0
Day 3: [100, 120, 90]           → Mean = 103.3
Day 4: [100, 120, 90, 150]      → Mean = 115.0
Day 5: [100, 120, 90, 150, 130] → Mean = 118.0

Window keeps EXPANDING (unlike rolling which is fixed size)
Code
Python

# Expanding statistics
df['expanding_mean'] = df['sales'].expanding().mean()
df['expanding_std'] = df['sales'].expanding().std()
df['expanding_max'] = df['sales'].expanding().max()
df['expanding_min'] = df['sales'].expanding().min()

print(df[['date', 'sales', 'expanding_mean', 'rolling_mean_7']].head(15))
10.6 Date/Time Features for Time Series
Python

# Extract comprehensive datetime features
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['day_of_week'] = df['date'].dt.dayofweek
df['day_of_year'] = df['date'].dt.dayofyear
df['week_of_year'] = df['date'].dt.isocalendar().week
df['quarter'] = df['date'].dt.quarter
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
df['is_month_start'] = df['date'].dt.is_month_start.astype(int)
df['is_month_end'] = df['date'].dt.is_month_end.astype(int)

# Cyclical encoding for periodicity
df['month_sin'] = np.sin(2 * np.pi * df['month'] / 12)
df['month_cos'] = np.cos(2 * np.pi * df['month'] / 12)
df['day_of_week_sin'] = np.sin(2 * np.pi * df['day_of_week'] / 7)
df['day_of_week_cos'] = np.cos(2 * np.pi * df['day_of_week'] / 7)

print(df.head(10))
10.7 Difference Features
Concept
text

Difference = Change from previous time point

Helps capture RATE OF CHANGE and makes data STATIONARY

Date       | Sales | Diff_1 | Diff_7
──────────────────────────────────────
2024-01-01 |  100  |  NaN   |  NaN
2024-01-02 |  120  |  +20   |  NaN
2024-01-03 |  90   |  -30   |  NaN
Code
Python

# First difference
df['sales_diff_1'] = df['sales'].diff(1)

# Second difference (diff of diff)
df['sales_diff_2'] = df['sales'].diff(2)

# Weekly difference
df['sales_diff_7'] = df['sales'].diff(7)

# Percentage change
df['sales_pct_change'] = df['sales'].pct_change()

print(df[['date', 'sales', 'sales_diff_1', 'sales_pct_change']].head(10))
10.8 Exponential Weighted Features
Concept
text

Exponential Weighted = Recent values get MORE weight

Unlike rolling mean where all values in window are equal,
EWM gives higher weight to recent values.

Great for capturing RECENT trends!
Code
Python

# Exponential weighted mean (span = similar to window size)
df['ewm_mean_7'] = df['sales'].ewm(span=7).mean()
df['ewm_mean_14'] = df['sales'].ewm(span=14).mean()

# Exponential weighted std
df['ewm_std_7'] = df['sales'].ewm(span=7).std()

print(df[['date', 'sales', 'rolling_mean_7', 'ewm_mean_7']].head(15))
10.9 Complete Time Series Feature Engineering
Python

import pandas as pd
import numpy as np

def create_time_series_features(df, date_col, value_col, 
                                 lags=[1, 7, 14, 28],
                                 windows=[7, 14, 28],
                                 create_date_features=True):
    """
    Comprehensive time series feature engineering
    
    Parameters:
    -----------
    df : DataFrame
    date_col : name of datetime column
    value_col : name of value column to create features from
    lags : list of lag periods
    windows : list of rolling window sizes
    create_date_features : whether to extract date components
    
    Returns:
    --------
    DataFrame with new features
    """
    df = df.copy()
    df = df.sort_values(date_col)
    
    # 1. Lag features
    print("Creating lag features...")
    for lag in lags:
        df[f'{value_col}_lag_{lag}'] = df[value_col].shift(lag)
    
    # 2. Rolling statistics
    print("Creating rolling features...")
    for window in windows:
        df[f'{value_col}_rolling_mean_{window}'] = df[value_col].rolling(window).mean()
        df[f'{value_col}_rolling_std_{window}'] = df[value_col].rolling(window).std()
        df[f'{value_col}_rolling_min_{window}'] = df[value_col].rolling(window).min()
        df[f'{value_col}_rolling_max_{window}'] = df[value_col].rolling(window).max()
    
    # 3. Expanding statistics
    print("Creating expanding features...")
    df[f'{value_col}_expanding_mean'] = df[value_col].expanding().mean()
    
    # 4. Difference features
    print("Creating difference features...")
    df[f'{value_col}_diff_1'] = df[value_col].diff(1)
    df[f'{value_col}_diff_7'] = df[value_col].diff(7)
    df[f'{value_col}_pct_change'] = df[value_col].pct_change()
    
    # 5. Exponential weighted features
    print("Creating EWM features...")
    df[f'{value_col}_ewm_7'] = df[value_col].ewm(span=7).mean()
    df[f'{value_col}_ewm_14'] = df[value_col].ewm(span=14).mean()
    
    # 6. Date features
    if create_date_features:
        print("Creating date features...")
        df[date_col] = pd.to_datetime(df[date_col])
        
        df['year'] = df[date_col].dt.year
        df['month'] = df[date_col].dt.month
        df['day'] = df[date_col].dt.day
        df['day_of_week'] = df[date_col].dt.dayofweek
        df['day_of_year'] = df[date_col].dt.dayofyear
        df['week_of_year'] = df[date_col].dt.isocalendar().week.astype(int)
        df['quarter'] = df[date_col].dt.quarter
        df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
        df['is_month_start'] = df[date_col].dt.is_month_start.astype(int)
        df['is_month_end'] = df[date_col].dt.is_month_end.astype(int)
        
        # Cyclical encoding
        df['month_sin'] = np.sin(2 * np.pi * df['month'] / 12)
        df['month_cos'] = np.cos(2 * np.pi * df['month'] / 12)
        df['day_of_week_sin'] = np.sin(2 * np.pi * df['day_of_week'] / 7)
        df['day_of_week_cos'] = np.cos(2 * np.pi * df['day_of_week'] / 7)
    
    print(f"\nCreated {len(df.columns) - 2} new features!")
    
    return df

# Usage
dates = pd.date_range('2023-01-01', periods=365, freq='D')
np.random.seed(42)
sales = 100 + np.cumsum(np.random.randn(365)) + 20 * np.sin(np.arange(365) * 2 * np.pi / 365)

df = pd.DataFrame({
    'date': dates,
    'sales': sales
})

df_features = create_time_series_features(df, 'date', 'sales')
print(df_features.head(30))



Chapter 11: Text Feature Engineering
11.1 Why Text Feature Engineering?
text

╔════════════════════════════════════════════════════════════════╗
║  Machine Learning models need NUMBERS, not TEXT                ║
║                                                                 ║
║  "This movie is amazing!" → [0.2, 0.8, 0.1, ..., 0.9]         ║
║                                                                 ║
║  Text Feature Engineering = Converting text to numbers          ║
╚════════════════════════════════════════════════════════════════╝
11.2 Text Preprocessing Pipeline
text

┌─────────────────────────────────────────────────────────────────┐
│              TEXT PREPROCESSING PIPELINE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Raw Text: "The Quick Brown FOX jumps! Over the lazy dog..."  │
│       │                                                         │
│       ▼                                                         │
│  1. LOWERCASE: "the quick brown fox jumps! over the lazy dog" │
│       │                                                         │
│       ▼                                                         │
│  2. REMOVE PUNCTUATION: "the quick brown fox jumps over..."   │
│       │                                                         │
│       ▼                                                         │
│  3. TOKENIZE: ["the", "quick", "brown", "fox", "jumps", ...]  │
│       │                                                         │
│       ▼                                                         │
│  4. REMOVE STOPWORDS: ["quick", "brown", "fox", "jumps", ...] │
│       │                                                         │
│       ▼                                                         │
│  5. STEMMING/LEMMATIZATION: ["quick", "brown", "fox", "jump"] │
│       │                                                         │
│       ▼                                                         │
│  6. VECTORIZATION: [0.2, 0.0, 0.8, 0.1, ...] (numbers!)       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
11.3 Basic Text Preprocessing
Python

import pandas as pd
import numpy as np
import re
import string

# Sample text data
texts = [
    "I LOVE this movie! It's absolutely AMAZING!!!",
    "Terrible film... worst I've ever seen :(",
    "Pretty good, but could be better.",
    "The acting was superb and the plot was engaging."
]

df = pd.DataFrame({'text': texts})
print("=== ORIGINAL TEXT ===")
print(df)

# Step 1: Lowercase
df['text_lower'] = df['text'].str.lower()

# Step 2: Remove punctuation
df['text_no_punct'] = df['text_lower'].str.replace(f'[{string.punctuation}]', '', regex=True)

# Step 3: Remove numbers
df['text_no_numbers'] = df['text_no_punct'].str.replace(r'\d+', '', regex=True)

# Step 4: Remove extra whitespace
df['text_clean'] = df['text_no_numbers'].str.replace(r'\s+', ' ', regex=True).str.strip()

print("\n=== AFTER BASIC CLEANING ===")
print(df[['text', 'text_clean']])
11.4 Tokenization
Python

import nltk
from nltk.tokenize import word_tokenize, sent_tokenize

# Download required NLTK data (run once)
# nltk.download('punkt')

text = "Hello! How are you doing today? I hope you're learning well."

# Word tokenization
words = word_tokenize(text)
print(f"Word tokens: {words}")

# Sentence tokenization
sentences = sent_tokenize(text)
print(f"Sentence tokens: {sentences}")

# Simple split tokenization (basic but fast)
simple_tokens = text.lower().split()
print(f"Simple tokens: {simple_tokens}")
11.5 Stopwords Removal
Python

from nltk.corpus import stopwords

# Download stopwords (run once)
# nltk.download('stopwords')

# Get English stopwords
stop_words = set(stopwords.words('english'))
print(f"Number of stopwords: {len(stop_words)}")
print(f"Sample stopwords: {list(stop_words)[:20]}")

# Remove stopwords from text
def remove_stopwords(text):
    words = text.lower().split()
    filtered_words = [word for word in words if word not in stop_words]
    return ' '.join(filtered_words)

df['text_no_stopwords'] = df['text_clean'].apply(remove_stopwords)

print("\n=== AFTER STOPWORD REMOVAL ===")
print(df[['text_clean', 'text_no_stopwords']])
11.6 Stemming vs Lemmatization
text

╔════════════════════════════════════════════════════════════════╗
║  STEMMING: Crude word reduction (chops off endings)            ║
║    running → run                                                ║
║    better → better (or sometimes "bett")                       ║
║    studies → studi                                              ║
║                                                                 ║
║  LEMMATIZATION: Intelligent word reduction (uses dictionary)   ║
║    running → run                                                ║
║    better → good                                                ║
║    studies → study                                              ║
╚════════════════════════════════════════════════════════════════╝
Python

from nltk.stem import PorterStemmer, WordNetLemmatizer

# Download wordnet (run once)
# nltk.download('wordnet')

stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()

# Test words
words = ['running', 'runs', 'ran', 'better', 'studies', 'studying', 'happily']

print("Word        | Stemmed     | Lemmatized")
print("-" * 45)
for word in words:
    stemmed = stemmer.stem(word)
    lemmatized = lemmatizer.lemmatize(word, pos='v')  # 'v' for verb
    print(f"{word:12} | {stemmed:12} | {lemmatized}")
Output:

text

Word        | Stemmed     | Lemmatized
---------------------------------------------
running      | run          | run
runs         | run          | run
ran          | ran          | run
better       | better       | better
studies      | studi        | study
studying     | studi        | study
happily      | happili      | happily
11.7 Bag of Words (BoW)
Concept
text

Bag of Words = Count occurrences of each word

Document 1: "I love cats"
Document 2: "I love dogs"
Document 3: "I hate cats"

Vocabulary: [I, love, cats, dogs, hate]

        I  love  cats  dogs  hate
Doc 1:  1    1     1     0     0
Doc 2:  1    1     0     1     0
Doc 3:  1    0     1     0     1
Code
Python

from sklearn.feature_extraction.text import CountVectorizer

documents = [
    "I love machine learning",
    "Machine learning is amazing",
    "I love deep learning too",
    "Deep learning is part of machine learning"
]

# Create Bag of Words
vectorizer = CountVectorizer()
bow_matrix = vectorizer.fit_transform(documents)

# Get feature names (vocabulary)
feature_names = vectorizer.get_feature_names_out()

# Convert to DataFrame for better visualization
bow_df = pd.DataFrame(
    bow_matrix.toarray(),
    columns=feature_names,
    index=[f'Doc_{i+1}' for i in range(len(documents))]
)

print("=== BAG OF WORDS ===")
print(bow_df)
Output:

text

=== BAG OF WORDS ===
       amazing  deep  is  learning  love  machine  of  part  too
Doc_1        0     0   0         1     1        1   0     0    0
Doc_2        1     0   1         1     0        1   0     0    0
Doc_3        0     1   0         1     1        0   0     0    1
Doc_4        0     1   1         2     0        1   1     1    0
11.8 TF-IDF (Term Frequency - Inverse Document Frequency)
Concept
text

TF-IDF = How important is a word in a document?

TF (Term Frequency) = How often word appears in document
IDF (Inverse Document Frequency) = How rare is word across all documents

TF-IDF = TF × IDF

Words that appear:
• Often in ONE document → High TF
• Rarely in OTHER documents → High IDF
= HIGH TF-IDF (important word!)

Words like "the", "is", "a":
• Appear everywhere → Low IDF
= LOW TF-IDF (not important)
Formula
text

TF(t, d) = (Number of times term t appears in document d) / (Total terms in d)

IDF(t) = log(Total documents / Documents containing term t)

TF-IDF(t, d) = TF(t, d) × IDF(t)
Code
Python

from sklearn.feature_extraction.text import TfidfVectorizer

documents = [
    "I love machine learning",
    "Machine learning is amazing",
    "I love deep learning too",
    "Deep learning is part of machine learning"
]

# Create TF-IDF
tfidf_vectorizer = TfidfVectorizer()
tfidf_matrix = tfidf_vectorizer.fit_transform(documents)

# Get feature names
feature_names = tfidf_vectorizer.get_feature_names_out()

# Convert to DataFrame
tfidf_df = pd.DataFrame(
    tfidf_matrix.toarray().round(3),
    columns=feature_names,
    index=[f'Doc_{i+1}' for i in range(len(documents))]
)

print("=== TF-IDF ===")
print(tfidf_df)
TF-IDF Parameters
Python

# Common TF-IDF configurations
tfidf = TfidfVectorizer(
    max_features=1000,      # Keep only top 1000 words
    min_df=2,               # Word must appear in at least 2 documents
    max_df=0.95,            # Ignore words in more than 95% of documents
    ngram_range=(1, 2),     # Include unigrams and bigrams
    stop_words='english'    # Remove English stopwords
)

tfidf_matrix = tfidf.fit_transform(documents)
print(f"Shape: {tfidf_matrix.shape}")
11.9 N-Grams
Concept
text

N-gram = Sequence of N consecutive words

"I love machine learning"

Unigrams (n=1): ["I", "love", "machine", "learning"]
Bigrams (n=2):  ["I love", "love machine", "machine learning"]
Trigrams (n=3): ["I love machine", "love machine learning"]

Why N-grams?
• "not good" vs "good" → bigram captures negation!
• "New York" → bigram captures proper noun
• "machine learning" → bigram captures phrase
Code
Python

from sklearn.feature_extraction.text import CountVectorizer

text = ["I love machine learning and deep learning"]

# Unigrams only
unigram_vec = CountVectorizer(ngram_range=(1, 1))
unigrams = unigram_vec.fit_transform(text)
print("Unigrams:", unigram_vec.get_feature_names_out())

# Bigrams only
bigram_vec = CountVectorizer(ngram_range=(2, 2))
bigrams = bigram_vec.fit_transform(text)
print("Bigrams:", bigram_vec.get_feature_names_out())

# Unigrams + Bigrams
combined_vec = CountVectorizer(ngram_range=(1, 2))
combined = combined_vec.fit_transform(text)
print("Combined:", combined_vec.get_feature_names_out())
11.10 Word Embeddings (Word2Vec, GloVe)
Concept
text

Word Embeddings = Dense vector representations of words

Each word becomes a vector of, say, 100-300 numbers
that CAPTURE MEANING!

king - man + woman ≈ queen (vector math with meaning!)

Bag of Words:    [0, 0, 1, 0, 0, 0, 0, 1, 0, ...]  (sparse, no meaning)
Word Embedding:  [0.2, -0.5, 0.8, 0.1, ...]        (dense, captures meaning)
Using Pre-trained Embeddings
Python

# Using Gensim for Word2Vec
# pip install gensim

from gensim.models import Word2Vec
import numpy as np

# Sample sentences (tokenized)
sentences = [
    ['i', 'love', 'machine', 'learning'],
    ['machine', 'learning', 'is', 'amazing'],
    ['deep', 'learning', 'is', 'subset', 'of', 'machine', 'learning'],
    ['i', 'love', 'deep', 'learning', 'too']
]

# Train Word2Vec model
model = Word2Vec(
    sentences=sentences,
    vector_size=50,      # Dimension of embeddings
    window=3,            # Context window
    min_count=1,         # Minimum word frequency
    workers=4,           # Parallel processing
    epochs=100           # Training iterations
)

# Get word vector
learning_vector = model.wv['learning']
print(f"'learning' vector shape: {learning_vector.shape}")
print(f"'learning' vector (first 10): {learning_vector[:10]}")

# Find similar words
similar = model.wv.most_similar('learning', topn=3)
print(f"\nMost similar to 'learning': {similar}")
Document Embedding (Average of Word Vectors)
Python

def document_vector(doc, model):
    """
    Create document embedding by averaging word vectors
    """
    words = doc.lower().split()
    word_vectors = []
    
    for word in words:
        if word in model.wv:
            word_vectors.append(model.wv[word])
    
    if len(word_vectors) == 0:
        return np.zeros(model.vector_size)
    
    return np.mean(word_vectors, axis=0)

# Create document embeddings
documents = [
    "I love machine learning",
    "Deep learning is amazing"
]

doc_vectors = [document_vector(doc, model) for doc in documents]
print(f"Document 1 vector shape: {doc_vectors[0].shape}")
11.11 Basic Text Statistics Features
Python

def extract_text_features(text):
    """
    Extract basic statistical features from text
    """
    features = {}
    
    # Length features
    features['char_count'] = len(text)
    features['word_count'] = len(text.split())
    features['sentence_count'] = text.count('.') + text.count('!') + text.count('?')
    
    # Average lengths
    words = text.split()
    features['avg_word_length'] = np.mean([len(w) for w in words]) if words else 0
    
    # Special character counts
    features['exclamation_count'] = text.count('!')
    features['question_count'] = text.count('?')
    features['uppercase_count'] = sum(1 for c in text if c.isupper())
    features['digit_count'] = sum(1 for c in text if c.isdigit())
    
    # Ratios
    features['uppercase_ratio'] = features['uppercase_count'] / features['char_count'] if features['char_count'] > 0 else 0
    
    return features

# Apply to dataframe
df = pd.DataFrame({
    'text': [
        "I LOVE this movie! It's AMAZING!!!",
        "Terrible film. Very disappointing.",
        "Pretty good overall! Would watch again?"
    ]
})

# Extract features for each text
text_features = df['text'].apply(lambda x: pd.Series(extract_text_features(x)))
df = pd.concat([df, text_features], axis=1)

print(df)
11.12 Complete Text Feature Engineering Pipeline
Python

import pandas as pd
import numpy as np
import re
import string
from sklearn.feature_extraction.text import TfidfVectorizer, CountVectorizer
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
from nltk.tokenize import word_tokenize

class TextFeatureEngineer:
    """
    Complete text feature engineering pipeline
    """
    
    def __init__(self, max_features=1000, ngram_range=(1, 2)):
        self.max_features = max_features
        self.ngram_range = ngram_range
        self.tfidf = None
        self.lemmatizer = WordNetLemmatizer()
        self.stop_words = set(stopwords.words('english'))
    
    def clean_text(self, text):
        """Basic text cleaning"""
        # Lowercase
        text = text.lower()
        # Remove URLs
        text = re.sub(r'http\S+|www\S+', '', text)
        # Remove HTML tags
        text = re.sub(r'<.*?>', '', text)
        # Remove punctuation
        text = text.translate(str.maketrans('', '', string.punctuation))
        # Remove numbers
        text = re.sub(r'\d+', '', text)
        # Remove extra whitespace
        text = ' '.join(text.split())
        return text
    
    def preprocess_text(self, text):
        """Full preprocessing pipeline"""
        # Clean
        text = self.clean_text(text)
        # Tokenize
        tokens = word_tokenize(text)
        # Remove stopwords and lemmatize
        tokens = [self.lemmatizer.lemmatize(t) for t in tokens 
                  if t not in self.stop_words and len(t) > 2]
        return ' '.join(tokens)
    
    def extract_basic_features(self, df, text_col):
        """Extract statistical features"""
        df = df.copy()
        
        # Length features
        df['char_count'] = df[text_col].str.len()
        df['word_count'] = df[text_col].str.split().str.len()
        df['avg_word_length'] = df[text_col].apply(
            lambda x: np.mean([len(w) for w in x.split()]) if x.split() else 0
        )
        
        # Special characters
        df['exclamation_count'] = df[text_col].str.count('!')
        df['question_count'] = df[text_col].str.count('\?')
        df['uppercase_ratio'] = df[text_col].apply(
            lambda x: sum(1 for c in x if c.isupper()) / len(x) if len(x) > 0 else 0
        )
        
        return df
    
    def fit_transform_tfidf(self, texts):
        """Create TF-IDF features"""
        # Preprocess
        processed = [self.preprocess_text(t) for t in texts]
        
        # Fit TF-IDF
        self.tfidf = TfidfVectorizer(
            max_features=self.max_features,
            ngram_range=self.ngram_range,
            min_df=2,
            max_df=0.95
        )
        
        tfidf_matrix = self.tfidf.fit_transform(processed)
        
        # Convert to DataFrame
        feature_names = [f'tfidf_{name}' for name in self.tfidf.get_feature_names_out()]
        tfidf_df = pd.DataFrame(
            tfidf_matrix.toarray(),
            columns=feature_names
        )
        
        return tfidf_df
    
    def transform_tfidf(self, texts):
        """Transform new texts using fitted TF-IDF"""
        processed = [self.preprocess_text(t) for t in texts]
        tfidf_matrix = self.tfidf.transform(processed)
        
        feature_names = [f'tfidf_{name}' for name in self.tfidf.get_feature_names_out()]
        tfidf_df = pd.DataFrame(
            tfidf_matrix.toarray(),
            columns=feature_names
        )
        
        return tfidf_df
    
    def engineer_features(self, df, text_col, fit_tfidf=True):
        """Complete feature engineering"""
        # Basic features
        df_features = self.extract_basic_features(df, text_col)
        
        # TF-IDF features
        if fit_tfidf:
            tfidf_df = self.fit_transform_tfidf(df[text_col])
        else:
            tfidf_df = self.transform_tfidf(df[text_col])
        
        # Combine
        df_final = pd.concat([df_features.reset_index(drop=True), 
                             tfidf_df.reset_index(drop=True)], axis=1)
        
        return df_final


# Usage Example
df = pd.DataFrame({
    'text': [
        "I absolutely LOVE this product! Amazing quality!!!",
        "Terrible experience. Would not recommend to anyone.",
        "Pretty decent for the price. Nothing special though.",
        "Best purchase ever! Fast shipping and great service!"
    ],
    'label': [1, 0, 1, 1]
})

# Initialize and run pipeline
engineer = TextFeatureEngineer(max_features=100, ngram_range=(1, 2))
df_engineered = engineer.engineer_features(df, 'text')

print(f"Original columns: {len(df.columns)}")
print(f"Engineered columns: {len(df_engineered.columns)}")
print(df_engineered.head())
Chapter 12: Image Feature Engineering
12.1 Introduction to Image Features
text

╔════════════════════════════════════════════════════════════════╗
║  Images are grids of pixel values                               ║
║                                                                 ║
║  Grayscale: Each pixel = 0-255 (brightness)                    ║
║  Color (RGB): Each pixel = 3 values (Red, Green, Blue)         ║
║                                                                 ║
║  A 100x100 RGB image = 100 × 100 × 3 = 30,000 features!       ║
╚════════════════════════════════════════════════════════════════╝
12.2 Basic Image Features
Python

import numpy as np
from PIL import Image
import cv2

def extract_basic_image_features(image_path):
    """
    Extract basic statistical features from an image
    """
    # Read image
    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    features = {}
    
    # Shape features
    features['height'] = img.shape[0]
    features['width'] = img.shape[1]
    features['aspect_ratio'] = img.shape[1] / img.shape[0]
    features['num_pixels'] = img.shape[0] * img.shape[1]
    
    # Color statistics (for each channel)
    for i, channel in enumerate(['red', 'green', 'blue']):
        features[f'{channel}_mean'] = np.mean(img_rgb[:, :, i])
        features[f'{channel}_std'] = np.std(img_rgb[:, :, i])
        features[f'{channel}_min'] = np.min(img_rgb[:, :, i])
        features[f'{channel}_max'] = np.max(img_rgb[:, :, i])
    
    # Grayscale statistics
    features['gray_mean'] = np.mean(img_gray)
    features['gray_std'] = np.std(img_gray)
    
    # Brightness (average of all pixels)
    features['brightness'] = np.mean(img_rgb)
    
    # Contrast (standard deviation of grayscale)
    features['contrast'] = np.std(img_gray)
    
    return features

# Example usage (with a sample image)
# features = extract_basic_image_features('sample_image.jpg')
# print(features)
12.3 Color Histogram Features
Python

def extract_color_histogram(image_path, bins=32):
    """
    Extract color histogram features
    """
    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    
    features = []
    
    # Histogram for each channel
    for i, channel in enumerate(['red', 'green', 'blue']):
        hist = cv2.calcHist([img_rgb], [i], None, [bins], [0, 256])
        hist = hist.flatten() / hist.sum()  # Normalize
        features.extend(hist)
    
    return np.array(features)

# This gives you bins * 3 features (e.g., 32 * 3 = 96 features)
12.4 Edge Detection Features
Python

def extract_edge_features(image_path):
    """
    Extract edge-based features
    """
    img = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
    
    features = {}
    
    # Canny edge detection
    edges = cv2.Canny(img, 100, 200)
    features['edge_pixel_ratio'] = np.sum(edges > 0) / edges.size
    features['edge_mean'] = np.mean(edges)
    
    # Sobel gradients
    sobelx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
    sobely = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)
    
    features['gradient_magnitude_mean'] = np.mean(np.sqrt(sobelx**2 + sobely**2))
    features['gradient_direction_mean'] = np.mean(np.arctan2(sobely, sobelx))
    
    return features
12.5 Using Pre-trained CNNs for Feature Extraction
Concept
text

Pre-trained CNN models (like VGG16, ResNet) have learned
to extract meaningful features from millions of images.

We can use these models to extract features:
1. Load pre-trained model (without top classification layer)
2. Pass image through model
3. Get feature vector from last convolutional layer
Code
Python

from tensorflow.keras.applications import VGG16, ResNet50
from tensorflow.keras.preprocessing import image
from tensorflow.keras.applications.vgg16 import preprocess_input
import numpy as np

def extract_cnn_features(image_path, model_name='vgg16'):
    """
    Extract features using pre-trained CNN
    """
    # Load model without top layer
    if model_name == 'vgg16':
        model = VGG16(weights='imagenet', include_top=False, pooling='avg')
        target_size = (224, 224)
    elif model_name == 'resnet50':
        model = ResNet50(weights='imagenet', include_top=False, pooling='avg')
        target_size = (224, 224)
    
    # Load and preprocess image
    img = image.load_img(image_path, target_size=target_size)
    img_array = image.img_to_array(img)
    img_array = np.expand_dims(img_array, axis=0)
    img_array = preprocess_input(img_array)
    
    # Extract features
    features = model.predict(img_array)
    
    return features.flatten()

# Usage
# features = extract_cnn_features('image.jpg', model_name='vgg16')
# print(f"Feature vector shape: {features.shape}")  # (512,) for VGG16 with avg pooling
12.6 Complete Image Feature Pipeline
Python

import numpy as np
import cv2
from pathlib import Path

class ImageFeatureEngineer:
    """
    Complete image feature engineering pipeline
    """
    
    def __init__(self, use_cnn=False, histogram_bins=32):
        self.use_cnn = use_cnn
        self.histogram_bins = histogram_bins
        self.cnn_model = None
        
        if use_cnn:
            from tensorflow.keras.applications import VGG16
            self.cnn_model = VGG16(weights='imagenet', include_top=False, pooling='avg')
    
    def extract_basic_features(self, img):
        """Extract basic statistical features"""
        features = {}
        
        img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        
        features['height'] = img.shape[0]
        features['width'] = img.shape[1]
        features['aspect_ratio'] = img.shape[1] / img.shape[0]
        features['brightness'] = np.mean(img)
        features['contrast'] = np.std(img_gray)
        
        # Per-channel statistics
        for i, ch in enumerate(['blue', 'green', 'red']):
            features[f'{ch}_mean'] = np.mean(img[:, :, i])
            features[f'{ch}_std'] = np.std(img[:, :, i])
        
        return features
    
    def extract_histogram_features(self, img):
        """Extract color histogram features"""
        features = {}
        
        for i, ch in enumerate(['blue', 'green', 'red']):
            hist = cv2.calcHist([img], [i], None, [self.histogram_bins], [0, 256])
            hist = hist.flatten() / hist.sum()
            
            for j, val in enumerate(hist):
                features[f'{ch}_hist_{j}'] = val
        
        return features
    
    def extract_edge_features(self, img):
        """Extract edge features"""
        features = {}
        
        gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        edges = cv2.Canny(gray, 100, 200)
        
        features['edge_ratio'] = np.sum(edges > 0) / edges.size
        features['edge_mean'] = np.mean(edges)
        
        return features
    
    def engineer_features(self, image_path):
        """Complete feature extraction"""
        img = cv2.imread(str(image_path))
        
        if img is None:
            raise ValueError(f"Could not read image: {image_path}")
        
        all_features = {}
        
        # Basic features
        all_features.update(self.extract_basic_features(img))
        
        # Histogram features
        all_features.update(self.extract_histogram_features(img))
        
        # Edge features
        all_features.update(self.extract_edge_features(img))
        
        # CNN features (optional)
        if self.use_cnn and self.cnn_model is not None:
            from tensorflow.keras.preprocessing import image as keras_image
            from tensorflow.keras.applications.vgg16 import preprocess_input
            
            img_resized = cv2.resize(img, (224, 224))
            img_rgb = cv2.cvtColor(img_resized, cv2.COLOR_BGR2RGB)
            img_array = np.expand_dims(img_rgb, axis=0)
            img_array = preprocess_input(img_array.astype('float64'))
            
            cnn_features = self.cnn_model.predict(img_array, verbose=0).flatten()
            
            for i, val in enumerate(cnn_features):
                all_features[f'cnn_{i}'] = val
        
        return all_features
    
    def process_directory(self, image_dir):
        """Process all images in a directory"""
        import pandas as pd
        
        image_dir = Path(image_dir)
        image_files = list(image_dir.glob('*.jpg')) + list(image_dir.glob('*.png'))
        
        all_data = []
        for img_path in image_files:
            try:
                features = self.engineer_features(img_path)
                features['filename'] = img_path.name
                all_data.append(features)
            except Exception as e:
                print(f"Error processing {img_path}: {e}")
        
        return pd.DataFrame(all_data)


# Usage
# engineer = ImageFeatureEngineer(use_cnn=False, histogram_bins=16)
# features = engineer.engineer_features('sample_image.jpg')
# print(f"Number of features: {len(features)}")
Chapter 13: Advanced Techniques
13.1 Feature Crosses (Interaction Features)
Concept
text

Feature Cross = Combining two or more features to create new ones

Example:
• Feature A: City (NYC, LA, Chicago)
• Feature B: Device (Mobile, Desktop)

Cross: City_Device
• NYC_Mobile, NYC_Desktop
• LA_Mobile, LA_Desktop
• Chicago_Mobile, Chicago_Desktop

This captures interactions that individual features miss!
Code
Python

import pandas as pd
import numpy as np
from sklearn.preprocessing import PolynomialFeatures

# Sample data
df = pd.DataFrame({
    'city': ['NYC', 'LA', 'NYC', 'Chicago', 'LA'],
    'device': ['Mobile', 'Desktop', 'Desktop', 'Mobile', 'Mobile'],
    'age': [25, 35, 28, 42, 31],
    'income': [50000, 75000, 60000, 90000, 55000]
})

# Method 1: String concatenation for categorical
df['city_device'] = df['city'] + '_' + df['device']
print("=== CATEGORICAL CROSS ===")
print(df[['city', 'device', 'city_device']])

# Method 2: Numerical interactions
df['age_income'] = df['age'] * df['income']
df['age_income_ratio'] = df['age'] / (df['income'] / 10000)

print("\n=== NUMERICAL INTERACTIONS ===")
print(df[['age', 'income', 'age_income', 'age_income_ratio']])
13.2 Target Encoding with Smoothing
Concept
text

Problem with basic target encoding:
Categories with few samples can have extreme mean values

Solution: SMOOTHING
Blend category mean with global mean based on sample size

smoothed_mean = (n * category_mean + m * global_mean) / (n + m)

Where:
n = samples in category
m = smoothing parameter
Code
Python

import pandas as pd
import numpy as np

def smoothed_target_encoding(df, cat_col, target_col, m=10):
    """
    Target encoding with smoothing
    
    Parameters:
    -----------
    m : smoothing parameter (higher = more regularization)
    """
    # Global mean
    global_mean = df[target_col].mean()
    
    # Category statistics
    agg = df.groupby(cat_col)[target_col].agg(['mean', 'count'])
    
    # Smoothed mean
    agg['smoothed'] = (agg['count'] * agg['mean'] + m * global_mean) / (agg['count'] + m)
    
    # Map to original data
    return df[cat_col].map(agg['smoothed'])

# Example
df = pd.DataFrame({
    'category': ['A', 'A', 'A', 'B', 'B', 'B', 'B', 'B', 'C', 'D'],
    'target': [1, 1, 0, 1, 0, 0, 1, 0, 1, 0]  # C and D have few samples
})

df['encoded'] = smoothed_target_encoding(df, 'category', 'target', m=5)
print(df)

# Compare with raw means
print("\nRaw means:")
print(df.groupby('category')['target'].mean())
print("\nSmoothed means:")
print(df.groupby('category')['encoded'].first())
13.3 Weight of Evidence (WoE) Encoding
Concept
text

WoE measures how much a category separates target classes
Commonly used in credit scoring

WoE = ln(Distribution of Events / Distribution of Non-Events)

• Positive WoE → Category has more events (class 1)
• Negative WoE → Category has more non-events (class 0)
Code
Python

import pandas as pd
import numpy as np

def calculate_woe_iv(df, feature, target):
    """
    Calculate Weight of Evidence and Information Value
    """
    # Get counts
    df_grouped = df.groupby(feature)[target].agg(['sum', 'count'])
    df_grouped.columns = ['events', 'total']
    df_grouped['non_events'] = df_grouped['total'] - df_grouped['events']
    
    # Calculate distributions
    total_events = df_grouped['events'].sum()
    total_non_events = df_grouped['non_events'].sum()
    
    df_grouped['dist_events'] = df_grouped['events'] / total_events
    df_grouped['dist_non_events'] = df_grouped['non_events'] / total_non_events
    
    # Calculate WoE
    # Add small value to avoid division by zero
    df_grouped['woe'] = np.log(
        (df_grouped['dist_events'] + 0.0001) / 
        (df_grouped['dist_non_events'] + 0.0001)
    )
    
    # Calculate IV (Information Value)
    df_grouped['iv'] = (
        (df_grouped['dist_events'] - df_grouped['dist_non_events']) * 
        df_grouped['woe']
    )
    
    total_iv = df_grouped['iv'].sum()
    
    return df_grouped, total_iv

# Example
df = pd.DataFrame({
    'education': ['High School', 'Bachelor', 'Master', 'PhD', 
                  'High School', 'Bachelor', 'Master', 'PhD',
                  'High School', 'Bachelor'],
    'default': [1, 0, 0, 0, 1, 0, 0, 0, 1, 1]
})

woe_df, iv = calculate_woe_iv(df, 'education', 'default')
print("WoE Table:")
print(woe_df)
print(f"\nTotal IV: {iv:.4f}")

"""
IV Interpretation:
< 0.02: Not useful for prediction
0.02 - 0.1: Weak predictor
0.1 - 0.3: Medium predictor
0.3 - 0.5: Strong predictor
> 0.5: Suspicious (may be overfitting)
"""
13.4 Feature Hashing (Hashing Trick)
Concept
text

Problem: High cardinality categorical features create too many columns

Solution: Hash categories to fixed number of buckets

Original: 10,000 unique categories
Hashing: Map to 100 buckets (fixed size)

Pros: Fixed memory, handles new categories
Cons: Hash collisions (different categories → same bucket)
Code
Python

from sklearn.feature_extraction import FeatureHasher
import pandas as pd

# High cardinality feature
df = pd.DataFrame({
    'product_id': ['PROD_001', 'PROD_002', 'PROD_003', 'PROD_001', 'PROD_999']
})

# Convert to dictionary format
dict_data = df['product_id'].apply(lambda x: {x: 1}).tolist()

# Hash to 10 features
hasher = FeatureHasher(n_features=10, input_type='dict')
hashed_features = hasher.transform(dict_data).toarray()

# Result
hashed_df = pd.DataFrame(
    hashed_features,
    columns=[f'hash_{i}' for i in range(10)]
)

print("Original:")
print(df)
print("\nHashed (10 features):")
print(hashed_df)
13.5 Dimensionality Reduction as Feature Engineering
PCA (Principal Component Analysis)
Python

from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
import pandas as pd
import numpy as np

# Create sample high-dimensional data
np.random.seed(42)
df = pd.DataFrame(
    np.random.randn(100, 20),
    columns=[f'feature_{i}' for i in range(20)]
)

# Always scale before PCA
scaler = StandardScaler()
df_scaled = scaler.fit_transform(df)

# Apply PCA
pca = PCA(n_components=5)  # Reduce to 5 components
pca_features = pca.fit_transform(df_scaled)

# Create DataFrame
pca_df = pd.DataFrame(
    pca_features,
    columns=[f'PC_{i+1}' for i in range(5)]
)

print("Original shape:", df.shape)
print("PCA shape:", pca_df.shape)
print(f"\nExplained variance ratio: {pca.explained_variance_ratio_}")
print(f"Total variance explained: {sum(pca.explained_variance_ratio_):.2%}")
t-SNE for Visualization Features
Python

from sklearn.manifold import TSNE
import matplotlib.pyplot as plt

# t-SNE for 2D visualization
tsne = TSNE(n_components=2, random_state=42, perplexity=30)
tsne_features = tsne.fit_transform(df_scaled)

# Plot
plt.figure(figsize=(10, 8))
plt.scatter(tsne_features[:, 0], tsne_features[:, 1], alpha=0.5)
plt.title('t-SNE Visualization')
plt.xlabel('t-SNE 1')
plt.ylabel('t-SNE 2')
plt.show()
13.6 Entity Embeddings for Categorical Variables
Concept
text

Instead of one-hot encoding, learn dense representations
Similar to word embeddings but for any categorical variable

One-hot: [1, 0, 0, 0, 0, 0, 0, 0, 0, 0]  (sparse, 10 dims)
Embedding: [0.2, -0.5, 0.8]              (dense, 3 dims)
Code (using Keras)
Python

import numpy as np
import pandas as pd
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Input, Embedding, Flatten, Dense, Concatenate

def create_embedding_model(cat_features, embedding_dims, num_features):
    """
    Create model with entity embeddings for categorical features
    """
    inputs = []
    embeddings = []
    
    # Embedding layers for each categorical feature
    for cat_name, (num_categories, emb_dim) in cat_features.items():
        inp = Input(shape=(1,), name=f'{cat_name}_input')
        emb = Embedding(num_categories, emb_dim, name=f'{cat_name}_emb')(inp)
        emb = Flatten()(emb)
        inputs.append(inp)
        embeddings.append(emb)
    
    # Numerical input
    num_input = Input(shape=(num_features,), name='numerical_input')
    inputs.append(num_input)
    
    # Concatenate all
    x = Concatenate()(embeddings + [num_input])
    x = Dense(64, activation='relu')(x)
    x = Dense(32, activation='relu')(x)
    output = Dense(1, activation='sigmoid')(x)
    
    model = Model(inputs=inputs, outputs=output)
    return model

# Example configuration
cat_features = {
    'city': (100, 10),     # 100 cities, embed to 10 dims
    'category': (50, 8),   # 50 categories, embed to 8 dims
}
num_features = 5  # 5 numerical features

model = create_embedding_model(cat_features, cat_features, num_features)
model.summary()
13.7 Feature Engineering for Outliers
Python

import pandas as pd
import numpy as np

def engineer_outlier_features(df, columns, method='iqr', threshold=1.5):
    """
    Create features indicating outliers
    """
    df = df.copy()
    
    for col in columns:
        if method == 'iqr':
            Q1 = df[col].quantile(0.25)
            Q3 = df[col].quantile(0.75)
            IQR = Q3 - Q1
            lower = Q1 - threshold * IQR
            upper = Q3 + threshold * IQR
            
            df[f'{col}_is_outlier'] = ((df[col] < lower) | (df[col] > upper)).astype(int)
            
        elif method == 'zscore':
            mean = df[col].mean()
            std = df[col].std()
            z_scores = np.abs((df[col] - mean) / std)
            
            df[f'{col}_is_outlier'] = (z_scores > threshold).astype(int)
            df[f'{col}_zscore'] = z_scores
        
        # Capped version (winsorization)
        if method == 'iqr':
            df[f'{col}_capped'] = df[col].clip(lower, upper)
        
    return df

# Example
df = pd.DataFrame({
    'value': [10, 12, 11, 13, 100, 14, 11, 12, -50, 13]  # 100 and -50 are outliers
})

df = engineer_outlier_features(df, ['value'], method='iqr')
print(df)
Chapter 14: Automated Feature Engineering
14.1 Why Automate Feature Engineering?
text

╔════════════════════════════════════════════════════════════════╗
║  Manual Feature Engineering:                                    ║
║  • Time-consuming                                               ║
║  • Requires domain expertise                                    ║
║  • Prone to missing important features                         ║
║                                                                 ║
║  Automated Feature Engineering:                                 ║
║  • Generates hundreds of features automatically                 ║
║  • Discovers non-obvious relationships                         ║
║  • Saves time for experimentation                              ║
╚════════════════════════════════════════════════════════════════╝
14.2 Using Featuretools
Concept
text

Featuretools uses "Deep Feature Synthesis":
1. Define entities (tables) and relationships
2. Automatically generate features using primitives:
   • Aggregations: sum, mean, count, etc.
   • Transformations: year, month, absolute, etc.
3. Stack primitives to create complex features
Code
Python

# pip install featuretools

import featuretools as ft
import pandas as pd
import numpy as np

# Create sample data
np.random.seed(42)

# Customers table
customers = pd.DataFrame({
    'customer_id': [1, 2, 3, 4, 5],
    'join_date': pd.date_range('2020-01-01', periods=5, freq='M'),
    'age': [25, 35, 45, 30, 55]
})

# Transactions table
transactions = pd.DataFrame({
    'transaction_id': range(1, 21),
    'customer_id': np.random.choice([1, 2, 3, 4, 5], 20),
    'amount': np.random.uniform(10, 500, 20),
    'transaction_date': pd.date_range('2020-06-01', periods=20, freq='D')
})

print("=== CUSTOMERS ===")
print(customers)
print("\n=== TRANSACTIONS ===")
print(transactions.head(10))

# Create EntitySet
es = ft.EntitySet(id='customer_transactions')

# Add dataframes
es = es.add_dataframe(
    dataframe_name='customers',
    dataframe=customers,
    index='customer_id',
    time_index='join_date'
)

es = es.add_dataframe(
    dataframe_name='transactions',
    dataframe=transactions,
    index='transaction_id',
    time_index='transaction_date'
)

# Add relationship
es = es.add_relationship(
    'customers', 'customer_id',
    'transactions', 'customer_id'
)

print("\n=== ENTITY SET ===")
print(es)

# Deep Feature Synthesis
feature_matrix, feature_defs = ft.dfs(
    entityset=es,
    target_dataframe_name='customers',
    agg_primitives=['sum', 'mean', 'count', 'max', 'min', 'std'],
    trans_primitives=['year', 'month', 'day'],
    max_depth=2
)

print(f"\n=== GENERATED FEATURES ({len(feature_defs)}) ===")
print(feature_matrix.head())

# Show feature definitions
print("\n=== FEATURE DEFINITIONS ===")
for feat in feature_defs[:10]:
    print(f"  {feat}")
14.3 Using Feature-engine
Python

# pip install feature-engine

import pandas as pd
import numpy as np
from feature_engine.creation import CyclicalFeatures, MathFeatures
from feature_engine.encoding import OneHotEncoder, TargetEncoder
from feature_engine.imputation import MeanMedianImputer
from sklearn.pipeline import Pipeline

# Sample data
df = pd.DataFrame({
    'month': [1, 6, 12, 3, 9],
    'hour': [8, 14, 20, 2, 17],
    'category': ['A', 'B', 'A', 'C', 'B'],
    'value1': [100, 200, 150, np.nan, 180],
    'value2': [50, 80, 60, 70, np.nan],
    'target': [1, 0, 1, 0, 1]
})

print("=== ORIGINAL DATA ===")
print(df)

# Create pipeline with Feature-engine transformers
pipeline = Pipeline([
    ('imputer', MeanMedianImputer(
        imputation_method='median',
        variables=['value1', 'value2']
    )),
    ('cyclical', CyclicalFeatures(
        variables=['month', 'hour'],
        max_values={'month': 12, 'hour': 24}
    )),
    ('math_features', MathFeatures(
        variables=['value1', 'value2'],
        func=['sum', 'mean', 'prod']
    )),
])

# Fit and transform
df_transformed = pipeline.fit_transform(df.drop('target', axis=1))
df_transformed['target'] = df['target']

print("\n=== TRANSFORMED DATA ===")
print(df_transformed)
14.4 Using tsfresh for Time Series
Python

# pip install tsfresh

import pandas as pd
import numpy as np
from tsfresh import extract_features
from tsfresh.feature_extraction import MinimalFCParameters

# Create sample time series data
np.random.seed(42)

# Multiple time series for different IDs
data = []
for id in range(1, 4):
    for t in range(50):
        data.append({
            'id': id,
            'time': t,
            'value': np.sin(t / 10) + np.random.randn() * 0.1 + id * 0.5
        })

df = pd.DataFrame(data)

print("=== TIME SERIES DATA ===")
print(df.head(10))

# Extract features
# Using minimal parameters for speed (use default for comprehensive)
extracted_features = extract_features(
    df, 
    column_id='id', 
    column_sort='time',
    default_fc_parameters=MinimalFCParameters()
)

print(f"\n=== EXTRACTED FEATURES ===")
print(f"Shape: {extracted_features.shape}")
print(extracted_features.head())
14.5 Custom Automated Feature Generator
Python

import pandas as pd
import numpy as np
from itertools import combinations

class AutoFeatureGenerator:
    """
    Custom automated feature engineering class
    """
    
    def __init__(self, 
                 create_interactions=True,
                 create_ratios=True,
                 create_polynomials=True,
                 create_binning=True,
                 max_interaction_features=50):
        
        self.create_interactions = create_interactions
        self.create_ratios = create_ratios
        self.create_polynomials = create_polynomials
        self.create_binning = create_binning
        self.max_interaction_features = max_interaction_features
        self.generated_features = []
    
    def fit_transform(self, df, target_col=None):
        """
        Generate features automatically
        """
        df_new = df.copy()
        
        # Get numerical columns
        num_cols = df_new.select_dtypes(include=[np.number]).columns.tolist()
        if target_col and target_col in num_cols:
            num_cols.remove(target_col)
        
        # 1. Polynomial features (squares)
        if self.create_polynomials:
            for col in num_cols:
                df_new[f'{col}_squared'] = df_new[col] ** 2
                df_new[f'{col}_sqrt'] = np.sqrt(np.abs(df_new[col]))
                self.generated_features.extend([f'{col}_squared', f'{col}_sqrt'])
        
        # 2. Interaction features (multiplication)
        if self.create_interactions:
            count = 0
            for col1, col2 in combinations(num_cols, 2):
                if count >= self.max_interaction_features:
                    break
                df_new[f'{col1}_x_{col2}'] = df_new[col1] * df_new[col2]
                self.generated_features.append(f'{col1}_x_{col2}')
                count += 1
        
        # 3. Ratio features
        if self.create_ratios:
            count = 0
            for col1, col2 in combinations(num_cols, 2):
                if count >= self.max_interaction_features:
                    break
                # Avoid division by zero
                if (df_new[col2] != 0).all():
                    df_new[f'{col1}_div_{col2}'] = df_new[col1] / df_new[col2]
                    self.generated_features.append(f'{col1}_div_{col2}')
                    count += 1
        
        # 4. Binning features
        if self.create_binning:
            for col in num_cols:
                df_new[f'{col}_binned_5'] = pd.qcut(
                    df_new[col], q=5, labels=False, duplicates='drop'
                )
                self.generated_features.append(f'{col}_binned_5')
        
        # 5. Aggregate features across rows
        if len(num_cols) >= 2:
            df_new['row_mean'] = df_new[num_cols].mean(axis=1)
            df_new['row_std'] = df_new[num_cols].std(axis=1)
            df_new['row_max'] = df_new[num_cols].max(axis=1)
            df_new['row_min'] = df_new[num_cols].min(axis=1)
            df_new['row_range'] = df_new['row_max'] - df_new['row_min']
            self.generated_features.extend(['row_mean', 'row_std', 'row_max', 'row_min', 'row_range'])
        
        print(f"Generated {len(self.generated_features)} new features")
        print(f"Total features: {len(df_new.columns)}")
        
        return df_new


# Usage
df = pd.DataFrame({
    'feature1': np.random.randn(100),
    'feature2': np.random.randn(100) * 10,
    'feature3': np.random.exponential(5, 100),
    'target': np.random.randint(0, 2, 100)
})

auto_gen = AutoFeatureGenerator(max_interaction_features=10)
df_enhanced = auto_gen.fit_transform(df, target_col='target')

print("\nGenerated features:")
print(auto_gen.generated_features)
Chapter 15: Best Practices and Real-World Projects
15.1 Feature Engineering Best Practices
text

╔════════════════════════════════════════════════════════════════════╗
║              TOP 10 FEATURE ENGINEERING BEST PRACTICES             ║
╠════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  1. UNDERSTAND YOUR DATA FIRST                                    ║
║     • Never skip EDA                                              ║
║     • Know your domain                                            ║
║                                                                    ║
║  2. HANDLE MISSING VALUES THOUGHTFULLY                            ║
║     • Understand WHY data is missing                              ║
║     • Create missing indicators when appropriate                  ║
║                                                                    ║
║  3. PREVENT DATA LEAKAGE                                          ║
║     • Split BEFORE feature engineering                            ║
║     • Fit on train, transform on test                             ║
║                                                                    ║
║  4. SCALE APPROPRIATELY                                           ║
║     • Know which algorithms need scaling                          ║
║     • Choose scaler based on data distribution                    ║
║                                                                    ║
║  5. ENCODE CATEGORICALS WISELY                                    ║
║     • Match encoding to cardinality                               ║
║     • Use target encoding with caution                            ║
║                                                                    ║
║  6. CREATE MEANINGFUL FEATURES                                    ║
║     • Domain knowledge > blind generation                         ║
║     • Ratios and interactions often help                          ║
║                                                                    ║
║  7. SELECT FEATURES                                               ║
║     • More features ≠ better model                                ║
║     • Remove redundant and noisy features                         ║
║                                                                    ║
║  8. VALIDATE PROPERLY                                             ║
║     • Use cross-validation                                        ║
║     • Test on truly unseen data                                   ║
║                                                                    ║
║  9. DOCUMENT EVERYTHING                                           ║
║     • Track what features you created                             ║
║     • Document transformations for production                     ║
║                                                                    ║
║  10. ITERATE AND EXPERIMENT                                       ║
║      • Feature engineering is iterative                           ║
║      • Try multiple approaches                                    ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
15.2 Preventing Data Leakage
What is Data Leakage?
text

Data Leakage = Using information that wouldn't be available at prediction time

Example 1: Fitting scaler on entire dataset (including test)
Example 2: Target encoding without cross-validation
Example 3: Using future data in time series
Correct Pipeline
Python

from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier

# CORRECT: Split first, then engineer features
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# CORRECT: Pipeline ensures proper fit/transform
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('model', RandomForestClassifier())
])

# Fit on training data only
pipeline.fit(X_train, y_train)

# Score on test data
score = pipeline.score(X_test, y_test)
15.3 Complete Real-World Project: House Price Prediction
Python

import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.ensemble import RandomForestRegressor, GradientBoostingRegressor
from sklearn.metrics import mean_squared_error, r2_score
import warnings
warnings.filterwarnings('ignore')

# ============================================================
# STEP 1: LOAD AND UNDERSTAND DATA
# ============================================================

# Create sample house data
np.random.seed(42)
n_samples = 1000

df = pd.DataFrame({
    'square_feet': np.random.randint(800, 4000, n_samples),
    'bedrooms': np.random.randint(1, 6, n_samples),
    'bathrooms': np.random.randint(1, 4, n_samples),
    'age': np.random.randint(0, 50, n_samples),
    'lot_size': np.random.randint(2000, 20000, n_samples),
    'neighborhood': np.random.choice(['A', 'B', 'C', 'D'], n_samples),
    'condition': np.random.choice(['Poor', 'Fair', 'Good', 'Excellent'], n_samples),
    'has_garage': np.random.choice([0, 1], n_samples),
    'has_pool': np.random.choice([0, 1], n_samples, p=[0.8, 0.2])
})

# Create price with some realistic relationships
df['price'] = (
    df['square_feet'] * 200 +
    df['bedrooms'] * 10000 +
    df['bathrooms'] * 15000 -
    df['age'] * 1000 +
    df['lot_size'] * 5 +
    df['has_pool'] * 30000 +
    df['has_garage'] * 20000 +
    df['neighborhood'].map({'A': 50000, 'B': 30000, 'C': 10000, 'D': 0}) +
    df['condition'].map({'Poor': 0, 'Fair': 15000, 'Good': 30000, 'Excellent': 50000}) +
    np.random.randn(n_samples) * 20000
)

print("=== DATA OVERVIEW ===")
print(df.info())
print("\n=== STATISTICS ===")
print(df.describe())

# ============================================================
# STEP 2: FEATURE ENGINEERING
# ============================================================

def engineer_house_features(df):
    """
    Create domain-specific features for house price prediction
    """
    df = df.copy()
    
    # Ratio features
    df['price_per_sqft'] = df['square_feet']  # Will be target-related after training
    df['sqft_per_bedroom'] = df['square_feet'] / df['bedrooms']
    df['bed_to_bath_ratio'] = df['bedrooms'] / df['bathrooms']
    df['lot_to_house_ratio'] = df['lot_size'] / df['square_feet']
    
    # Size categories
    df['size_category'] = pd.cut(
        df['square_feet'],
        bins=[0, 1200, 2000, 3000, float('inf')],
        labels=['Small', 'Medium', 'Large', 'XLarge']
    )
    
    # Age categories
    df['age_category'] = pd.cut(
        df['age'],
        bins=[0, 5, 15, 30, float('inf')],
        labels=['New', 'Recent', 'Middle', 'Old']
    )
    
    # Total rooms
    df['total_rooms'] = df['bedrooms'] + df['bathrooms']
    
    # Amenity score
    df['amenity_score'] = df['has_garage'] + df['has_pool']
    
    # Condition encoding (ordinal)
    condition_map = {'Poor': 1, 'Fair': 2, 'Good': 3, 'Excellent': 4}
    df['condition_score'] = df['condition'].map(condition_map)
    
    # Interactions
    df['sqft_x_condition'] = df['square_feet'] * df['condition_score']
    df['age_x_condition'] = df['age'] * df['condition_score']
    
    return df

# Apply feature engineering
df_engineered = engineer_house_features(df)

print("\n=== ENGINEERED FEATURES ===")
print(f"Original columns: {len(df.columns)}")
print(f"Engineered columns: {len(df_engineered.columns)}")
print(f"New features: {set(df_engineered.columns) - set(df.columns)}")

# ============================================================
# STEP 3: PREPARE FOR MODELING
# ============================================================

# Define features and target
target = 'price'
features = [col for col in df_engineered.columns if col != target]

# Identify column types
numerical_features = df_engineered[features].select_dtypes(include=[np.number]).columns.tolist()
categorical_features = df_engineered[features].select_dtypes(include=['object', 'category']).columns.tolist()

print(f"\nNumerical features ({len(numerical_features)}): {numerical_features[:5]}...")
print(f"Categorical features ({len(categorical_features)}): {categorical_features}")

# Split data
X = df_engineered[features]
y = df_engineered[target]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print(f"\nTrain size: {len(X_train)}")
print(f"Test size: {len(X_test)}")

# ============================================================
# STEP 4: CREATE PREPROCESSING PIPELINE
# ============================================================

# Preprocessor
preprocessor = ColumnTransformer(
    transformers=[
        ('num', StandardScaler(), numerical_features),
        ('cat', OneHotEncoder(drop='first', sparse_output=False), categorical_features)
    ]
)

# Full pipeline with model
pipeline_rf = Pipeline([
    ('preprocessor', preprocessor),
    ('model', RandomForestRegressor(n_estimators=100, random_state=42))
])

pipeline_gb = Pipeline([
    ('preprocessor', preprocessor),
    ('model', GradientBoostingRegressor(n_estimators=100, random_state=42))
])

# ============================================================
# STEP 5: TRAIN AND EVALUATE
# ============================================================

print("\n=== MODEL TRAINING ===")

# Random Forest
pipeline_rf.fit(X_train, y_train)
y_pred_rf = pipeline_rf.predict(X_test)

rmse_rf = np.sqrt(mean_squared_error(y_test, y_pred_rf))
r2_rf = r2_score(y_test, y_pred_rf)

print(f"\nRandom Forest:")
print(f"  RMSE: ${rmse_rf:,.0f}")
print(f"  R²: {r2_rf:.4f}")

# Gradient Boosting
pipeline_gb.fit(X_train, y_train)
y_pred_gb = pipeline_gb.predict(X_test)

rmse_gb = np.sqrt(mean_squared_error(y_test, y_pred_gb))
r2_gb = r2_score(y_test, y_pred_gb)

print(f"\nGradient Boosting:")
print(f"  RMSE: ${rmse_gb:,.0f}")
print(f"  R²: {r2_gb:.4f}")

# Cross-validation
cv_scores = cross_val_score(pipeline_gb, X, y, cv=5, scoring='r2')
print(f"\nCross-validation R² scores: {cv_scores.round(4)}")
print(f"Mean CV R²: {cv_scores.mean():.4f} (+/- {cv_scores.std() * 2:.4f})")

# ============================================================
# STEP 6: FEATURE IMPORTANCE
# ============================================================

# Get feature names after preprocessing
feature_names = numerical_features.copy()
ohe = preprocessor.named_transformers_['cat']
cat_feature_names = ohe.get_feature_names_out(categorical_features).tolist()
feature_names.extend(cat_feature_names)

# Feature importance from Random Forest
importances = pipeline_rf.named_steps['model'].feature_importances_
importance_df = pd.DataFrame({
    'feature': feature_names,
    'importance': importances
}).sort_values('importance', ascending=False)

print("\n=== TOP 15 FEATURES ===")
print(importance_df.head(15))
15.4 Feature Engineering Checklist
text

╔════════════════════════════════════════════════════════════════════╗
║              FEATURE ENGINEERING CHECKLIST                         ║
╠════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  □ DATA UNDERSTANDING                                             ║
║    □ Explored data types                                          ║
║    □ Checked distributions                                        ║
║    □ Identified missing values                                    ║
║    □ Found outliers                                               ║
║    □ Understood correlations                                      ║
║                                                                    ║
║  □ DATA CLEANING                                                  ║
║    □ Handled missing values appropriately                         ║
║    □ Dealt with outliers                                          ║
║    □ Fixed data type issues                                       ║
║    □ Removed duplicates                                           ║
║                                                                    ║
║  □ FEATURE CREATION                                               ║
║    □ Created domain-specific features                             ║
║    □ Extracted date/time features (if applicable)                 ║
║    □ Generated interaction features                               ║
║    □ Created ratio features                                       ║
║    □ Binned continuous variables (if needed)                      ║
║                                                                    ║
║  □ ENCODING                                                       ║
║    □ Encoded categorical variables appropriately                  ║
║    □ Used correct encoding for cardinality                        ║
║    □ Handled ordinal variables correctly                          ║
║                                                                    ║
║  □ SCALING                                                        ║
║    □ Scaled features for algorithms that need it                  ║
║    □ Used appropriate scaler for data distribution                ║
║                                                                    ║
║  □ FEATURE SELECTION                                              ║
║    □ Removed low-variance features                                ║
║    □ Removed highly correlated features                           ║
║    □ Used feature importance for selection                        ║
║                                                                    ║
║  □ VALIDATION                                                     ║
║    □ Split data before feature engineering                        ║
║    □ Used cross-validation                                        ║
║    □ Checked for data leakage                                     ║
║    □ Tested on unseen data                                        ║
║                                                                    ║
║  □ DOCUMENTATION                                                  ║
║    □ Documented all transformations                               ║
║    □ Saved fitted transformers                                    ║
║    □ Created reproducible pipeline                                ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
15.5 Summary: Key Takeaways
text

╔════════════════════════════════════════════════════════════════════╗
║                    FEATURE ENGINEERING SUMMARY                     ║
╠════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  "Feature engineering is the process of using domain knowledge    ║
║   to extract features from raw data that make machine learning    ║
║   algorithms work better."                                        ║
║                                                                    ║
║  KEY CONCEPTS:                                                    ║
║  ─────────────                                                    ║
║  1. Good features > Fancy algorithms                              ║
║  2. Understand your data before transforming it                   ║
║  3. Domain knowledge is your superpower                           ║
║  4. Prevent data leakage at all costs                            ║
║  5. Document everything for reproducibility                       ║
║                                                                    ║
║  THE JOURNEY:                                                     ║
║  ────────────                                                     ║
║  Raw Data → Clean → Transform → Create → Select → Model          ║
║                                                                    ║
║  REMEMBER:                                                        ║
║  ─────────                                                        ║
║  • More features ≠ Better model                                   ║
║  • Feature engineering is iterative                               ║
║  • Always validate on unseen data                                 ║
║  • Automate what you can, but understand what you automate       ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
Appendix A: Quick Reference Card
A.1 Missing Values
Method	Code	When to Use
Drop rows	df.dropna()	<5% missing
Fill mean	df.fillna(df.mean())	Numerical, normal dist
Fill median	df.fillna(df.median())	Numerical, skewed
Fill mode	df.fillna(df.mode()[0])	Categorical
KNN Impute	KNNImputer().fit_transform(df)	Related features
A.2 Encoding Categorical
Method	Code	When to Use
Label	LabelEncoder().fit_transform(col)	Binary/Ordinal
One-Hot	pd.get_dummies(df, columns=[...])	Nominal, <10 unique
Target	col.map(df.groupby(col)[target].mean())	High cardinality
Frequency	col.map(col.value_counts())	High cardinality
A.3 Scaling
Method	Code	When to Use
Standard	StandardScaler()	Normal distribution
MinMax	MinMaxScaler()	Need [0,1] range
Robust	RobustScaler()	Has outliers
A.4 Transformation
Method	Code	When to Use
Log	np.log1p(col)	Right skewed, positive
Square Root	np.sqrt(col)	Mild right skew
Box-Cox	PowerTransformer('box-cox')	Positive values
Yeo-Johnson	PowerTransformer('yeo-johnson')	Any values
A.5 Feature Selection
Method	Code	Type
Variance	VarianceThreshold()	Filter
Correlation	df.corr()	Filter
Chi-Square	chi2(X, y)	Filter (categorical)
Mutual Info	mutual_info_classif(X, y)	Filter
RFE	RFE(estimator, n_features)	Wrapper
Tree Importance	model.feature_importances_	Embedded
Appendix B: Common Errors and Solutions
Error	Cause	Solution
"Cannot convert string to float"	Categorical not encoded	Encode before modeling
"Input contains NaN"	Missing values	Handle missing first
"Negative values in log"	Log of negative numbers	Use log1p or Yeo-Johnson
"Different number of features"	Train/test mismatch	Use same pipeline
Poor model performance	Bad features	Create better features
Overfitting	Too many features	Feature selection
Data leakage	Fit on all data	Split before engineering
Congratulations! 🎉

You have completed the comprehensive Feature Engineering guide. You now have:

✅ Deep understanding of all feature engineering concepts
✅ Practical code for every technique
✅ Knowledge of when to use each method
✅ Real-world project experience
✅ Best practices and checklists

Go build amazing ML models with excellent features!