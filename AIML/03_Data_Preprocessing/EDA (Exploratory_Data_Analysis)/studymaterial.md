The Complete Guide to Exploratory Data Analysis (EDA)
From Absolute Beginner to Advanced Practitioner
Table of Contents
Introduction to EDA
Setting Up Your Environment
Understanding Data Types
Loading and Inspecting Data
Data Cleaning Fundamentals
Univariate Analysis
Bivariate Analysis
Multivariate Analysis
Feature Engineering Through EDA
Advanced EDA Techniques
EDA for Different Data Types
Statistical Tests in EDA
EDA Best Practices and Checklist
Real-World Case Studies
1. Introduction to EDA
1.1 What is EDA?
Exploratory Data Analysis (EDA) is the process of investigating datasets to:

Discover patterns
Spot anomalies
Test hypotheses
Check assumptions
Understand relationships between variables
Think of EDA as detective work: Before building any machine learning model, you need to understand what story your data is telling.

1.2 Why is EDA Critical for ML?
text

Without EDA → Garbage In → Garbage Out
With EDA → Quality In → Quality Out
Real-world impact:

80% of ML project time is spent on data preparation and EDA
70% of ML model failures are due to poor data understanding
Good EDA can improve model accuracy by 20-40%
1.3 The EDA Workflow
text

Raw Data
    ↓
1. Ask Questions (What do I want to know?)
    ↓
2. Collect Data (Gather from sources)
    ↓
3. Clean Data (Handle missing values, outliers)
    ↓
4. Explore Data (Visualize, summarize)
    ↓
5. Analyze Patterns (Find relationships)
    ↓
6. Communicate Findings (Tell the story)
    ↓
ML Model Building
1.4 Two Types of EDA
1. Descriptive EDA:

Summarizes main characteristics
Uses statistics (mean, median, mode)
Answers: "What happened?"
2. Inferential EDA:

Makes predictions about populations
Uses hypothesis testing
Answers: "Why did it happen? What will happen?"
2. Setting Up Your Environment
2.1 Essential Libraries
Python

# Data manipulation
import pandas as pd
import numpy as np

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# Statistical analysis
from scipy import stats
from scipy.stats import chi2_contingency, normaltest, skew, kurtosis

# Machine learning preprocessing
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.decomposition import PCA

# Warnings (optional)
import warnings
warnings.filterwarnings('ignore')
2.2 Setting Default Styles
Python

# Make plots look professional
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")

# Display settings
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', 100)
pd.set_option('display.float_format', '{:.2f}'.format)

# Figure size
plt.rcParams['figure.figsize'] = (12, 6)
2.3 Installation Commands
Bash

# Using pip
pip install pandas numpy matplotlib seaborn plotly scipy scikit-learn

# Using conda
conda install pandas numpy matplotlib seaborn plotly scipy scikit-learn
3. Understanding Data Types
3.1 Two Main Categories
text

Data Types
    |
    |-------- Numerical (Quantitative)
    |              |
    |              |--- Continuous (Height: 5.7, 6.2, 5.9 feet)
    |              |--- Discrete (Children: 0, 1, 2, 3)
    |
    |-------- Categorical (Qualitative)
                   |
                   |--- Nominal (Colors: Red, Blue, Green)
                   |--- Ordinal (Rating: Low, Medium, High)
3.2 Detailed Breakdown
3.2.1 Numerical Data
Continuous:

Can take ANY value within a range
Examples: Temperature (98.6°F), Weight (65.5 kg), Time (3.45 seconds)
Visualization: Histogram, Box plot, Density plot
Discrete:

Can only take SPECIFIC values (usually integers)
Examples: Number of children (0, 1, 2), Dice roll (1-6)
Visualization: Bar chart, Count plot
Python

# Identifying numerical columns
numerical_cols = df.select_dtypes(include=['int64', 'float64']).columns
print(f"Numerical columns: {list(numerical_cols)}")
3.2.2 Categorical Data
Nominal:

No inherent order
Examples: Gender (Male/Female), Country (USA/UK/India)
Encoding: One-hot encoding
Ordinal:

Has meaningful order
Examples: Education (High School < Bachelor < Master < PhD)
Encoding: Label encoding with order preservation
Python

# Identifying categorical columns
categorical_cols = df.select_dtypes(include=['object', 'category']).columns
print(f"Categorical columns: {list(categorical_cols)}")
3.3 Special Data Types
DateTime:

Python

# Converting to datetime
df['date'] = pd.to_datetime(df['date'])

# Extracting components
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day_of_week'] = df['date'].dt.day_name()
Text/String:

Python

# Text length
df['text_length'] = df['description'].str.len()

# Word count
df['word_count'] = df['description'].str.split().str.len()
Boolean:

Python

# Converting to boolean
df['is_active'] = df['status'].map({'active': True, 'inactive': False})
4. Loading and Inspecting Data
4.1 Loading Data from Different Sources
4.1.1 CSV Files
Python

# Basic loading
df = pd.read_csv('data.csv')

# With parameters
df = pd.read_csv('data.csv', 
                 sep=',',                    # Delimiter
                 encoding='utf-8',           # Encoding
                 na_values=['NA', '?', ''],  # Missing value markers
                 parse_dates=['date_column'], # Parse dates
                 index_col='id')             # Set index
4.1.2 Excel Files
Python

# Single sheet
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# Multiple sheets
excel_file = pd.ExcelFile('data.xlsx')
df1 = excel_file.parse('Sheet1')
df2 = excel_file.parse('Sheet2')
4.1.3 SQL Databases
Python

import sqlite3

# Connect and query
conn = sqlite3.connect('database.db')
df = pd.read_sql_query("SELECT * FROM table_name", conn)
conn.close()
4.1.4 JSON Files
Python

# Simple JSON
df = pd.read_json('data.json')

# Nested JSON
df = pd.json_normalize(data, record_path=['nested_field'])
4.2 First Look at Data
4.2.1 The Essential Five Commands
Python

# 1. First rows
print(df.head(10))  # Shows first 10 rows

# 2. Last rows
print(df.tail(10))  # Shows last 10 rows

# 3. Dataset shape
print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")

# 4. Column information
print(df.info())

# 5. Statistical summary
print(df.describe())
4.2.2 Understanding df.info()
Python

df.info()
Output interpretation:

text

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999          # ← 1000 rows
Data columns (total 5 columns):              # ← 5 columns
 #   Column    Non-Null Count  Dtype        
---  ------    --------------  -----        
 0   age       950 non-null    float64      # ← 50 missing values
 1   salary    1000 non-null   int64        # ← No missing values
 2   name      1000 non-null   object       # ← Text data
 3   date      1000 non-null   datetime64   # ← Date data
 4   city      980 non-null    object       # ← 20 missing values
dtypes: datetime64(1), float64(1), int64(1), object(2)
memory usage: 39.2+ KB
Key insights:

Non-Null Count ≠ Total rows → Missing values present
Dtype tells you data type
Memory usage indicates dataset size
4.2.3 Understanding df.describe()
Python

df.describe()
For numerical columns:

text

              age        salary
count      950.00      1000.00    # Number of non-null values
mean        35.50     50000.00    # Average
std         10.20     15000.00    # Standard deviation (spread)
min         18.00     20000.00    # Minimum value
25%         28.00     40000.00    # 25th percentile (Q1)
50%         35.00     48000.00    # Median (Q2)
75%         43.00     60000.00    # 75th percentile (Q3)
max         65.00    120000.00    # Maximum value
What this tells you:

count < total rows → Missing values exist
mean vs median → If very different, data is skewed
std → High value means data is spread out
min/max → Check for unrealistic values
Python

# For categorical columns (use include='all')
df.describe(include='all')

# Additional statistics
df.describe(include='object')  # Only categorical
For categorical columns:

text

         city
count    980        # Non-null count
unique   50         # Number of unique values
top      NYC        # Most common value
freq     150        # Frequency of most common value
4.3 Detailed Inspection
4.3.1 Column Names and Types
Python

# All column names
print("Columns:", df.columns.tolist())

# Data types
print("\nData types:")
print(df.dtypes)

# Specific type columns
print("\nNumerical:", df.select_dtypes(include=[np.number]).columns.tolist())
print("Categorical:", df.select_dtypes(include=['object']).columns.tolist())
print("Datetime:", df.select_dtypes(include=['datetime64']).columns.tolist())
4.3.2 Memory Usage
Python

# Overall memory
print(f"Total memory: {df.memory_usage(deep=True).sum() / 1024**2:.2f} MB")

# Per column
print("\nMemory per column (MB):")
print(df.memory_usage(deep=True) / 1024**2)

# Optimize memory (for large datasets)
def reduce_memory(df):
    """Reduce memory usage by downcasting numeric types"""
    for col in df.select_dtypes(include=['int']).columns:
        df[col] = pd.to_numeric(df[col], downcast='integer')
    
    for col in df.select_dtypes(include=['float']).columns:
        df[col] = pd.to_numeric(df[col], downcast='float')
    
    return df

df = reduce_memory(df)
4.3.3 Unique Values
Python

# Unique value counts for all columns
for col in df.columns:
    unique_count = df[col].nunique()
    total_count = len(df)
    print(f"{col}: {unique_count} unique values ({unique_count/total_count*100:.2f}%)")

# Identify potential ID columns (high uniqueness)
potential_ids = [col for col in df.columns if df[col].nunique() == len(df)]
print(f"\nPotential ID columns: {potential_ids}")

# Identify potential categorical columns (low uniqueness)
potential_categorical = [col for col in df.columns 
                        if df[col].nunique() < 20 and df[col].dtype == 'object']
print(f"Potential categorical columns: {potential_categorical}")
4.3.4 Sample Inspection
Python

# Random sample (reproducible)
print(df.sample(n=10, random_state=42))

# Stratified sample (proportional representation)
print(df.groupby('category').sample(n=5, random_state=42))

# Look at specific rows
print(df.iloc[100:110])  # Rows 100-109
print(df.loc[df['age'] > 60])  # Conditional selection
5. Data Cleaning Fundamentals
5.1 Missing Values
5.1.1 Detecting Missing Values
Python

# Count missing values
print("Missing values per column:")
print(df.isnull().sum())

# Percentage of missing values
print("\nMissing percentage:")
missing_percent = (df.isnull().sum() / len(df) * 100).round(2)
print(missing_percent[missing_percent > 0])

# Visualize missing values
import missingno as msno

# Matrix plot (shows pattern of missingness)
msno.matrix(df, figsize=(12, 6))
plt.show()

# Bar plot (shows count)
msno.bar(df, figsize=(12, 6))
plt.show()

# Heatmap (shows correlation of missingness)
msno.heatmap(df, figsize=(12, 6))
plt.show()
5.1.2 Understanding Missing Data Patterns
Three types of missing data:

MCAR (Missing Completely At Random)

No pattern in missing values
Example: Survey participant randomly skips a question
Action: Safe to delete or impute
MAR (Missing At Random)

Missingness related to OTHER variables
Example: High earners don't report income (related to income level)
Action: Careful imputation needed
MNAR (Missing Not At Random)

Missingness related to the value itself
Example: Very sick patients can't report health status
Action: Domain knowledge required
Python

# Check if missingness is related to other variables
# Example: Is age missing more often for certain cities?
print(df.groupby('city')['age'].apply(lambda x: x.isnull().sum()))
5.1.3 Handling Missing Values
Decision Framework:

text

Missing < 5% → Safe to delete rows
Missing 5-20% → Impute carefully
Missing > 20% → Consider dropping column OR advanced imputation
Method 1: Deletion

Python

# Delete rows with ANY missing value
df_clean = df.dropna()

# Delete rows with missing values in specific columns
df_clean = df.dropna(subset=['important_column'])

# Delete columns with too many missing values
threshold = 0.7  # Keep columns with <70% missing
df_clean = df.dropna(axis=1, thresh=int(threshold * len(df)))

# Delete rows with missing in ALL columns
df_clean = df.dropna(how='all')
Method 2: Simple Imputation

Python

# Mean/Median/Mode imputation
from sklearn.impute import SimpleImputer

# For numerical: use median (robust to outliers)
num_imputer = SimpleImputer(strategy='median')
df[numerical_cols] = num_imputer.fit_transform(df[numerical_cols])

# For categorical: use most frequent
cat_imputer = SimpleImputer(strategy='most_frequent')
df[categorical_cols] = cat_imputer.fit_transform(df[categorical_cols])

# Constant value
df['column'].fillna(0, inplace=True)  # Fill with 0
df['column'].fillna('Unknown', inplace=True)  # Fill with 'Unknown'
Method 3: Advanced Imputation

Python

# Forward fill (use previous value)
df['column'].fillna(method='ffill', inplace=True)

# Backward fill (use next value)
df['column'].fillna(method='bfill', inplace=True)

# Interpolation (for time series)
df['column'].interpolate(method='linear', inplace=True)

# KNN Imputation
from sklearn.impute import KNNImputer
knn_imputer = KNNImputer(n_neighbors=5)
df[numerical_cols] = knn_imputer.fit_transform(df[numerical_cols])

# Iterative Imputation (MICE)
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
iter_imputer = IterativeImputer(max_iter=10, random_state=42)
df[numerical_cols] = iter_imputer.fit_transform(df[numerical_cols])
Method 4: Create Missing Indicator

Python

# Sometimes, the fact that data is missing is informative
df['age_missing'] = df['age'].isnull().astype(int)
# Then impute the original column
df['age'].fillna(df['age'].median(), inplace=True)
5.2 Duplicate Values
5.2.1 Detecting Duplicates
Python

# Check for duplicate rows
print(f"Duplicate rows: {df.duplicated().sum()}")

# See duplicate rows
duplicates = df[df.duplicated(keep=False)]  # keep=False shows all duplicates
print(duplicates.sort_values(by=list(df.columns)))

# Check duplicates based on specific columns
print(f"Duplicate IDs: {df.duplicated(subset=['id']).sum()}")
5.2.2 Handling Duplicates
Python

# Remove duplicate rows (keep first occurrence)
df_clean = df.drop_duplicates(keep='first')

# Remove duplicates based on specific columns
df_clean = df.drop_duplicates(subset=['id', 'name'], keep='last')

# Remove ALL duplicate occurrences
df_clean = df.drop_duplicates(keep=False)

# Mark duplicates without removing
df['is_duplicate'] = df.duplicated()
5.3 Outliers
5.3.1 Detecting Outliers
Visual Methods:

Python

# Box plot (shows outliers as points)
plt.figure(figsize=(12, 6))
df.boxplot(column=['age', 'salary'])
plt.title('Box Plot - Outlier Detection')
plt.show()

# Scatter plot
plt.figure(figsize=(10, 6))
plt.scatter(df.index, df['salary'])
plt.xlabel('Index')
plt.ylabel('Salary')
plt.title('Scatter Plot - Outlier Detection')
plt.show()
Statistical Methods:

1. IQR Method (Interquartile Range)

Python

def detect_outliers_iqr(df, column):
    """
    IQR Method:
    - Q1 = 25th percentile
    - Q3 = 75th percentile
    - IQR = Q3 - Q1
    - Outliers: < Q1 - 1.5*IQR OR > Q3 + 1.5*IQR
    """
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    
    print(f"Column: {column}")
    print(f"Lower bound: {lower_bound:.2f}")
    print(f"Upper bound: {upper_bound:.2f}")
    print(f"Outliers: {len(outliers)} ({len(outliers)/len(df)*100:.2f}%)")
    
    return outliers

# Usage
outliers = detect_outliers_iqr(df, 'salary')
2. Z-Score Method

Python

def detect_outliers_zscore(df, column, threshold=3):
    """
    Z-Score Method:
    - Z-score = (value - mean) / std
    - Outliers: |z-score| > threshold (usually 3)
    """
    from scipy import stats
    
    z_scores = np.abs(stats.zscore(df[column].dropna()))
    outliers = df[np.abs(z_scores) > threshold]
    
    print(f"Column: {column}")
    print(f"Outliers (z-score > {threshold}): {len(outliers)} ({len(outliers)/len(df)*100:.2f}%)")
    
    return outliers

# Usage
outliers = detect_outliers_zscore(df, 'salary', threshold=3)
3. Isolation Forest (ML-based)

Python

from sklearn.ensemble import IsolationForest

def detect_outliers_isolation_forest(df, columns, contamination=0.1):
    """
    Isolation Forest:
    - ML algorithm that isolates anomalies
    - contamination: expected proportion of outliers
    """
    iso_forest = IsolationForest(contamination=contamination, random_state=42)
    outlier_labels = iso_forest.fit_predict(df[columns])
    
    # -1 for outliers, 1 for inliers
    outliers = df[outlier_labels == -1]
    
    print(f"Outliers detected: {len(outliers)} ({len(outliers)/len(df)*100:.2f}%)")
    
    return outliers

# Usage
outliers = detect_outliers_isolation_forest(df, ['age', 'salary'], contamination=0.05)
5.3.2 Handling Outliers
Decision Framework:

text

1. Are outliers DATA ERRORS? → Remove or correct
2. Are outliers VALID but rare? → Keep but handle carefully
3. Are outliers DOMAIN-SPECIFIC? → Consult expert
Method 1: Remove Outliers

Python

# Using IQR
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1
df_clean = df[(df['salary'] >= Q1 - 1.5*IQR) & (df['salary'] <= Q3 + 1.5*IQR)]
Method 2: Cap Outliers (Winsorization)

Python

# Cap at 5th and 95th percentile
lower = df['salary'].quantile(0.05)
upper = df['salary'].quantile(0.95)
df['salary_capped'] = df['salary'].clip(lower, upper)
Method 3: Transform Data

Python

# Log transformation (for right-skewed data)
df['salary_log'] = np.log1p(df['salary'])  # log1p handles zeros

# Square root transformation
df['salary_sqrt'] = np.sqrt(df['salary'])

# Box-Cox transformation (automatically finds best transformation)
from scipy.stats import boxcox
df['salary_boxcox'], lambda_param = boxcox(df['salary'] + 1)  # +1 to handle zeros
Method 4: Treat Separately

Python

# Create binary flag
df['is_outlier'] = 0
df.loc[(df['salary'] < lower_bound) | (df['salary'] > upper_bound), 'is_outlier'] = 1

# Use in modeling as separate feature
5.4 Data Type Issues
5.4.1 Incorrect Data Types
Python

# Check current types
print(df.dtypes)

# Convert to correct types
df['age'] = df['age'].astype(int)
df['salary'] = df['salary'].astype(float)
df['date'] = pd.to_datetime(df['date'])
df['category'] = df['category'].astype('category')  # Saves memory

# Handle errors during conversion
df['numeric_column'] = pd.to_numeric(df['numeric_column'], errors='coerce')  # Invalid → NaN
5.4.2 Inconsistent Formatting
Python

# String cleaning
df['name'] = df['name'].str.strip()  # Remove whitespace
df['name'] = df['name'].str.lower()  # Lowercase
df['name'] = df['name'].str.title()  # Title Case

# Remove special characters
df['name'] = df['name'].str.replace('[^a-zA-Z\s]', '', regex=True)

# Standardize categories
df['gender'] = df['gender'].replace({'M': 'Male', 'm': 'Male', 
                                      'F': 'Female', 'f': 'Female'})

# Date formatting
df['date'] = pd.to_datetime(df['date'], format='%Y-%m-%d')
5.5 Data Validation
Python

def validate_data(df):
    """Comprehensive data validation"""
    
    print("=" * 50)
    print("DATA VALIDATION REPORT")
    print("=" * 50)
    
    # 1. Check shape
    print(f"\n1. SHAPE: {df.shape[0]} rows × {df.shape[1]} columns")
    
    # 2. Check missing values
    print("\n2. MISSING VALUES:")
    missing = df.isnull().sum()
    if missing.sum() == 0:
        print("   ✓ No missing values")
    else:
        print(missing[missing > 0])
    
    # 3. Check duplicates
    print("\n3. DUPLICATES:")
    dup_count = df.duplicated().sum()
    if dup_count == 0:
        print("   ✓ No duplicates")
    else:
        print(f"   ✗ {dup_count} duplicate rows found")
    
    # 4. Check data types
    print("\n4. DATA TYPES:")
    print(df.dtypes)
    
    # 5. Check value ranges (for numerical columns)
    print("\n5. VALUE RANGES:")
    print(df.describe())
    
    # 6. Check unique values (for categorical columns)
    print("\n6. UNIQUE VALUES (Categorical):")
    cat_cols = df.select_dtypes(include=['object', 'category']).columns
    for col in cat_cols:
        print(f"   {col}: {df[col].nunique()} unique values")
    
    # 7. Check for negative values where not expected
    print("\n7. NEGATIVE VALUE CHECK:")
    num_cols = df.select_dtypes(include=[np.number]).columns
    for col in num_cols:
        neg_count = (df[col] < 0).sum()
        if neg_count > 0:
            print(f"   ✗ {col}: {neg_count} negative values")
    
    print("\n" + "=" * 50)

# Usage
validate_data(df)
6. Univariate Analysis
Univariate Analysis = Analyzing ONE variable at a time

Goal: Understand the distribution, central tendency, and spread of individual variables

6.1 Numerical Variables
6.1.1 Measures of Central Tendency
Python

column = 'age'

# Mean (average)
mean = df[column].mean()
print(f"Mean: {mean:.2f}")
# When to use: Symmetric distribution, no extreme outliers
# Example: Average test score

# Median (middle value)
median = df[column].median()
print(f"Median: {median:.2f}")
# When to use: Skewed distribution, presence of outliers
# Example: Median house price (not affected by mansions)

# Mode (most frequent value)
mode = df[column].mode()[0]
print(f"Mode: {mode:.2f}")
# When to use: Categorical data, finding most common value
# Example: Most common shoe size

# Comparison
print(f"\nMean vs Median difference: {abs(mean - median):.2f}")
if mean > median:
    print("→ Right-skewed (long tail on right)")
elif mean < median:
    print("→ Left-skewed (long tail on left)")
else:
    print("→ Symmetric distribution")
Visual representation:

Python

plt.figure(figsize=(12, 5))

# Distribution with mean, median, mode
plt.subplot(1, 2, 1)
plt.hist(df[column], bins=30, edgecolor='black', alpha=0.7)
plt.axvline(mean, color='red', linestyle='--', label=f'Mean: {mean:.2f}')
plt.axvline(median, color='green', linestyle='--', label=f'Median: {median:.2f}')
plt.axvline(mode, color='blue', linestyle='--', label=f'Mode: {mode:.2f}')
plt.xlabel(column)
plt.ylabel('Frequency')
plt.title(f'Distribution of {column}')
plt.legend()

# Box plot
plt.subplot(1, 2, 2)
plt.boxplot(df[column].dropna())
plt.ylabel(column)
plt.title(f'Box Plot of {column}')

plt.tight_layout()
plt.show()
6.1.2 Measures of Spread (Dispersion)
Python

# Range (difference between max and min)
data_range = df[column].max() - df[column].min()
print(f"Range: {data_range:.2f}")
# Problem: Sensitive to outliers

# Interquartile Range (IQR)
Q1 = df[column].quantile(0.25)
Q3 = df[column].quantile(0.75)
IQR = Q3 - Q1
print(f"IQR: {IQR:.2f}")
# Advantage: Robust to outliers (middle 50% of data)

# Variance (average squared deviation from mean)
variance = df[column].var()
print(f"Variance: {variance:.2f}")
# Problem: Not in original units

# Standard Deviation (square root of variance)
std = df[column].std()
print(f"Standard Deviation: {std:.2f}")
# Interpretation: On average, data points deviate by {std} from mean

# Coefficient of Variation (CV)
cv = (std / mean) * 100
print(f"Coefficient of Variation: {cv:.2f}%")
# Interpretation: Lower CV = less variability
# CV < 15% → Low variability
# CV 15-30% → Moderate variability
# CV > 30% → High variability
Understanding Standard Deviation:

text

68% of data falls within ±1 standard deviation of mean
95% of data falls within ±2 standard deviations of mean
99.7% of data falls within ±3 standard deviations of mean
(For normal distribution)
Python

# Calculate percentage of data within 1, 2, 3 std
within_1std = ((df[column] >= mean - std) & (df[column] <= mean + std)).sum() / len(df) * 100
within_2std = ((df[column] >= mean - 2*std) & (df[column] <= mean + 2*std)).sum() / len(df) * 100
within_3std = ((df[column] >= mean - 3*std) & (df[column] <= mean + 3*std)).sum() / len(df) * 100

print(f"Within 1 std: {within_1std:.2f}% (Expected: 68%)")
print(f"Within 2 std: {within_2std:.2f}% (Expected: 95%)")
print(f"Within 3 std: {within_3std:.2f}% (Expected: 99.7%)")
6.1.3 Measures of Shape
Skewness (Asymmetry)

Python

from scipy.stats import skew

skewness = skew(df[column].dropna())
print(f"Skewness: {skewness:.2f}")

# Interpretation
if skewness > 1:
    print("→ Highly right-skewed (long tail on right)")
elif skewness > 0.5:
    print("→ Moderately right-skewed")
elif skewness > -0.5:
    print("→ Approximately symmetric")
elif skewness > -1:
    print("→ Moderately left-skewed")
else:
    print("→ Highly left-skewed (long tail on left)")
Visual:

Python

plt.figure(figsize=(15, 4))

# Right-skewed
plt.subplot(1, 3, 1)
right_skewed = np.random.exponential(2, 1000)
plt.hist(right_skewed, bins=30, edgecolor='black')
plt.title('Right-Skewed\n(Mean > Median)')

# Symmetric
plt.subplot(1, 3, 2)
symmetric = np.random.normal(0, 1, 1000)
plt.hist(symmetric, bins=30, edgecolor='black')
plt.title('Symmetric\n(Mean ≈ Median)')

# Left-skewed
plt.subplot(1, 3, 3)
left_skewed = -np.random.exponential(2, 1000)
plt.hist(left_skewed, bins=30, edgecolor='black')
plt.title('Left-Skewed\n(Mean < Median)')

plt.tight_layout()
plt.show()
Kurtosis (Tailedness)

Python

from scipy.stats import kurtosis

kurt = kurtosis(df[column].dropna())
print(f"Kurtosis: {kurt:.2f}")

# Interpretation
if kurt > 3:
    print("→ Leptokurtic (heavy tails, more outliers)")
elif kurt < 3:
    print("→ Platykurtic (light tails, fewer outliers)")
else:
    print("→ Mesokurtic (normal distribution)")
6.1.4 Comprehensive Numerical Analysis Function
Python

def analyze_numerical(df, column):
    """Complete univariate analysis for numerical variable"""
    
    print("=" * 60)
    print(f"UNIVARIATE ANALYSIS: {column}")
    print("=" * 60)
    
    # Basic statistics
    print("\n1. BASIC STATISTICS:")
    print(f"   Count: {df[column].count()}")
    print(f"   Missing: {df[column].isnull().sum()} ({df[column].isnull().sum()/len(df)*100:.2f}%)")
    print(f"   Unique values: {df[column].nunique()}")
    
    # Central tendency
    print("\n2. CENTRAL TENDENCY:")
    mean = df[column].mean()
    median = df[column].median()
    mode = df[column].mode()[0] if len(df[column].mode()) > 0 else np.nan
    print(f"   Mean: {mean:.2f}")
    print(f"   Median: {median:.2f}")
    print(f"   Mode: {mode:.2f}")
    
    # Spread
    print("\n3. SPREAD:")
    print(f"   Min: {df[column].min():.2f}")
    print(f"   Max: {df[column].max():.2f}")
    print(f"   Range: {df[column].max() - df[column].min():.2f}")
    print(f"   IQR: {df[column].quantile(0.75) - df[column].quantile(0.25):.2f}")
    print(f"   Std Dev: {df[column].std():.2f}")
    print(f"   Variance: {df[column].var():.2f}")
    
    # Shape
    print("\n4. SHAPE:")
    print(f"   Skewness: {skew(df[column].dropna()):.2f}")
    print(f"   Kurtosis: {kurtosis(df[column].dropna()):.2f}")
    
    # Percentiles
    print("\n5. PERCENTILES:")
    for p in [10, 25, 50, 75, 90, 95, 99]:
        print(f"   {p}th: {df[column].quantile(p/100):.2f}")
    
    # Outliers
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    print(f"\n6. OUTLIERS (IQR method):")
    print(f"   Count: {len(outliers)} ({len(outliers)/len(df)*100:.2f}%)")
    print(f"   Lower bound: {lower_bound:.2f}")
    print(f"   Upper bound: {upper_bound:.2f}")
    
    # Visualizations
    fig, axes = plt.subplots(2, 2, figsize=(15, 10))
    
    # Histogram
    axes[0, 0].hist(df[column].dropna(), bins=30, edgecolor='black', alpha=0.7)
    axes[0, 0].axvline(mean, color='red', linestyle='--', label=f'Mean: {mean:.2f}')
    axes[0, 0].axvline(median, color='green', linestyle='--', label=f'Median: {median:.2f}')
    axes[0, 0].set_xlabel(column)
    axes[0, 0].set_ylabel('Frequency')
    axes[0, 0].set_title(f'Histogram of {column}')
    axes[0, 0].legend()
    
    # Box plot
    axes[0, 1].boxplot(df[column].dropna(), vert=True)
    axes[0, 1].set_ylabel(column)
    axes[0, 1].set_title(f'Box Plot of {column}')
    axes[0, 1].grid(True, alpha=0.3)
    
    # Density plot
    df[column].dropna().plot(kind='density', ax=axes[1, 0])
    axes[1, 0].set_xlabel(column)
    axes[1, 0].set_title(f'Density Plot of {column}')
    axes[1, 0].grid(True, alpha=0.3)
    
    # Q-Q plot (check normality)
    from scipy import stats
    stats.probplot(df[column].dropna(), dist="norm", plot=axes[1, 1])
    axes[1, 1].set_title(f'Q-Q Plot of {column}')
    axes[1, 1].grid(True, alpha=0.3)
    
    plt.tight_layout()
    plt.show()
    
    print("\n" + "=" * 60)

# Usage
analyze_numerical(df, 'age')
6.2 Categorical Variables
6.2.1 Frequency Analysis
Python

column = 'city'

# Value counts
print("FREQUENCY TABLE:")
freq_table = df[column].value_counts()
print(freq_table)

# Relative frequency (percentage)
print("\nRELATIVE FREQUENCY:")
rel_freq = df[column].value_counts(normalize=True) * 100
print(rel_freq)

# Combined table
freq_df = pd.DataFrame({
    'Count': df[column].value_counts(),
    'Percentage': df[column].value_counts(normalize=True) * 100
})
print("\nCOMBINED TABLE:")
print(freq_df)

# Cumulative frequency
freq_df['Cumulative %'] = freq_df['Percentage'].cumsum()
print("\nWITH CUMULATIVE:")
print(freq_df)
6.2.2 Visualizations for Categorical Data
Bar Chart (for nominal data)

Python

plt.figure(figsize=(12, 6))

# Vertical bar chart
plt.subplot(1, 2, 1)
df[column].value_counts().plot(kind='bar', edgecolor='black')
plt.xlabel(column)
plt.ylabel('Count')
plt.title(f'Bar Chart of {column}')
plt.xticks(rotation=45)

# Horizontal bar chart (better for long labels)
plt.subplot(1, 2, 2)
df[column].value_counts().plot(kind='barh', edgecolor='black')
plt.ylabel(column)
plt.xlabel('Count')
plt.title(f'Horizontal Bar Chart of {column}')

plt.tight_layout()
plt.show()
Pie Chart (for showing proportions)

Python

plt.figure(figsize=(10, 8))

# Basic pie chart
df[column].value_counts().plot(kind='pie', autopct='%1.1f%%')
plt.ylabel('')
plt.title(f'Distribution of {column}')
plt.show()

# Note: Use pie charts sparingly - humans are bad at comparing angles
# Bar charts are usually better for comparison
Count Plot (Seaborn)

Python

plt.figure(figsize=(12, 6))
sns.countplot(data=df, x=column, order=df[column].value_counts().index)
plt.xlabel(column)
plt.ylabel('Count')
plt.title(f'Count Plot of {column}')
plt.xticks(rotation=45)
plt.show()
6.2.3 Comprehensive Categorical Analysis Function
Python

def analyze_categorical(df, column, top_n=10):
    """Complete univariate analysis for categorical variable"""
    
    print("=" * 60)
    print(f"UNIVARIATE ANALYSIS: {column}")
    print("=" * 60)
    
    # Basic statistics
    print("\n1. BASIC STATISTICS:")
    print(f"   Count: {df[column].count()}")
    print(f"   Missing: {df[column].isnull().sum()} ({df[column].isnull().sum()/len(df)*100:.2f}%)")
    print(f"   Unique values: {df[column].nunique()}")
    print(f"   Most common: {df[column].mode()[0] if len(df[column].mode()) > 0 else 'N/A'}")
    
    # Frequency table
    print(f"\n2. FREQUENCY TABLE (Top {top_n}):")
    freq_df = pd.DataFrame({
        'Count': df[column].value_counts().head(top_n),
        'Percentage': (df[column].value_counts(normalize=True).head(top_n) * 100).round(2),
        'Cumulative %': (df[column].value_counts(normalize=True).head(top_n).cumsum() * 100).round(2)
    })
    print(freq_df)
    
    # Cardinality check
    unique_ratio = df[column].nunique() / len(df)
    print(f"\n3. CARDINALITY:")
    print(f"   Unique ratio: {unique_ratio:.4f}")
    if unique_ratio > 0.9:
        print("   ⚠ High cardinality - might be an ID column")
    elif unique_ratio < 0.05:
        print("   ✓ Low cardinality - good for categorical")
    
    # Imbalance check
    print("\n4. CLASS IMBALANCE:")
    most_common_pct = df[column].value_counts(normalize=True).iloc[0] * 100
    least_common_pct = df[column].value_counts(normalize=True).iloc[-1] * 100
    imbalance_ratio = most_common_pct / least_common_pct
    print(f"   Most common: {most_common_pct:.2f}%")
    print(f"   Least common: {least_common_pct:.2f}%")
    print(f"   Imbalance ratio: {imbalance_ratio:.2f}")
    if imbalance_ratio > 10:
        print("   ⚠ Severe imbalance detected")
    
    # Visualizations
    fig, axes = plt.subplots(1, 3, figsize=(18, 5))
    
    # Bar chart
    df[column].value_counts().head(top_n).plot(kind='bar', ax=axes[0], edgecolor='black')
    axes[0].set_xlabel(column)
    axes[0].set_ylabel('Count')
    axes[0].set_title(f'Bar Chart (Top {top_n})')
    axes[0].tick_params(axis='x', rotation=45)
    
    # Pie chart
    df[column].value_counts().head(top_n).plot(kind='pie', ax=axes[1], autopct='%1.1f%%')
    axes[1].set_ylabel('')
    axes[1].set_title(f'Pie Chart (Top {top_n})')
    
    # Horizontal bar with percentages
    freq_data = df[column].value_counts().head(top_n)
    axes[2].barh(range(len(freq_data)), freq_data.values)
    axes[2].set_yticks(range(len(freq_data)))
    axes[2].set_yticklabels(freq_data.index)
    axes[2].set_xlabel('Count')
    axes[2].set_title(f'Horizontal Bar Chart (Top {top_n})')
    axes[2].invert_yaxis()
    
    # Add value labels
    for i, v in enumerate(freq_data.values):
        axes[2].text(v, i, f' {v}', va='center')
    
    plt.tight_layout()
    plt.show()
    
    print("\n" + "=" * 60)

# Usage
analyze_categorical(df, 'city', top_n=10)
6.3 Complete Univariate Analysis Pipeline
Python

def complete_univariate_analysis(df):
    """Analyze all variables in dataset"""
    
    print("\n" + "="*80)
    print("COMPLETE UNIVARIATE ANALYSIS")
    print("="*80)
    
    # Separate numerical and categorical
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    categorical_cols = df.select_dtypes(include=['object', 'category']).columns
    
    print(f"\nNumerical columns ({len(numerical_cols)}): {list(numerical_cols)}")
    print(f"Categorical columns ({len(categorical_cols)}): {list(categorical_cols)}")
    
    # Analyze numerical columns
    print("\n" + "="*80)
    print("NUMERICAL VARIABLES")
    print("="*80)
    for col in numerical_cols:
        analyze_numerical(df, col)
        print("\n")
    
    # Analyze categorical columns
    print("\n" + "="*80)
    print("CATEGORICAL VARIABLES")
    print("="*80)
    for col in categorical_cols:
        analyze_categorical(df, col)
        print("\n")

# Usage
complete_univariate_analysis(df)
7. Bivariate Analysis
Bivariate Analysis = Analyzing relationships between TWO variables

Goal: Understand how variables relate to and influence each other

7.1 Numerical vs Numerical
7.1.1 Scatter Plot
Python

# Basic scatter plot
plt.figure(figsize=(10, 6))
plt.scatter(df['age'], df['salary'], alpha=0.5)
plt.xlabel('Age')
plt.ylabel('Salary')
plt.title('Age vs Salary')
plt.grid(True, alpha=0.3)
plt.show()

# Enhanced scatter plot with seaborn
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x='age', y='salary', hue='department', size='experience')
plt.title('Age vs Salary (by Department and Experience)')
plt.show()
7.1.2 Correlation Analysis
Pearson Correlation Coefficient (r)

Python

# Calculate correlation
corr = df['age'].corr(df['salary'])
print(f"Pearson correlation: {corr:.3f}")

# Interpretation
"""
r = +1: Perfect positive correlation
r = +0.7 to +1: Strong positive correlation
r = +0.3 to +0.7: Moderate positive correlation
r = 0 to +0.3: Weak positive correlation
r = 0: No correlation
r = -0.3 to 0: Weak negative correlation
r = -0.7 to -0.3: Moderate negative correlation
r = -1 to -0.7: Strong negative correlation
r = -1: Perfect negative correlation
"""

if corr > 0.7:
    print("→ Strong positive correlation")
elif corr > 0.3:
    print("→ Moderate positive correlation")
elif corr > -0.3:
    print("→ Weak or no correlation")
elif corr > -0.7:
    print("→ Moderate negative correlation")
else:
    print("→ Strong negative correlation")
Important: Correlation ≠ Causation!

text

Ice cream sales correlate with drowning deaths
→ Doesn't mean ice cream causes drowning
→ Both increase in summer (confounding variable)
Correlation Matrix

Python

# Calculate correlation matrix for all numerical columns
corr_matrix = df[numerical_cols].corr()
print(corr_matrix)

# Visualize with heatmap
plt.figure(figsize=(12, 10))
sns.heatmap(corr_matrix, 
            annot=True,           # Show correlation values
            cmap='coolwarm',      # Color scheme
            center=0,             # Center at 0
            square=True,          # Square cells
            linewidths=1,         # Grid lines
            cbar_kws={"shrink": 0.8})
plt.title('Correlation Matrix Heatmap')
plt.tight_layout()
plt.show()
Advanced Correlation Methods

Python

# 1. Spearman correlation (for monotonic relationships, robust to outliers)
from scipy.stats import spearmanr
spearman_corr, p_value = spearmanr(df['age'], df['salary'])
print(f"Spearman correlation: {spearman_corr:.3f} (p-value: {p_value:.4f})")

# 2. Kendall's Tau (for small samples, ordinal data)
from scipy.stats import kendalltau
kendall_corr, p_value = kendalltau(df['age'], df['salary'])
print(f"Kendall correlation: {kendall_corr:.3f} (p-value: {p_value:.4f})")

# When to use which:
"""
Pearson: Linear relationships, normal distribution, no outliers
Spearman: Monotonic relationships, ordinal data, outliers present
Kendall: Small samples, ordinal data
"""
7.1.3 Regression Analysis
Python

# Simple linear regression
from scipy.stats import linregress

slope, intercept, r_value, p_value, std_err = linregress(df['age'], df['salary'])

print(f"Slope: {slope:.2f}")
print(f"Intercept: {intercept:.2f}")
print(f"R-squared: {r_value**2:.3f}")
print(f"P-value: {p_value:.4f}")

# Equation: salary = slope * age + intercept
print(f"\nEquation: salary = {slope:.2f} * age + {intercept:.2f}")

# Visualize regression line
plt.figure(figsize=(10, 6))
plt.scatter(df['age'], df['salary'], alpha=0.5, label='Data')
plt.plot(df['age'], slope * df['age'] + intercept, 'r-', 
         label=f'Regression line (R²={r_value**2:.3f})')
plt.xlabel('Age')
plt.ylabel('Salary')
plt.title('Age vs Salary with Regression Line')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
R-squared Interpretation:

text

R² = 0.8 → 80% of variance in salary is explained by age
R² = 0.5 → 50% of variance explained (moderate fit)
R² = 0.2 → 20% of variance explained (weak fit)
7.1.4 Joint Plot (Comprehensive View)
Python

# Seaborn joint plot (combines scatter + distributions)
sns.jointplot(data=df, x='age', y='salary', kind='reg', height=8)
plt.show()

# Different kinds
for kind in ['scatter', 'reg', 'hex', 'kde']:
    sns.jointplot(data=df, x='age', y='salary', kind=kind, height=6)
    plt.suptitle(f'Joint Plot - {kind.upper()}', y=1.02)
    plt.show()
7.1.5 Comprehensive Numerical-Numerical Analysis
Python

def analyze_numerical_numerical(df, col1, col2):
    """Complete bivariate analysis for two numerical variables"""
    
    print("=" * 60)
    print(f"BIVARIATE ANALYSIS: {col1} vs {col2}")
    print("=" * 60)
    
    # Remove missing values
    clean_df = df[[col1, col2]].dropna()
    
    # Correlation analysis
    print("\n1. CORRELATION:")
    pearson_corr = clean_df[col1].corr(clean_df[col2])
    spearman_corr, _ = spearmanr(clean_df[col1], clean_df[col2])
    
    print(f"   Pearson: {pearson_corr:.3f}")
    print(f"   Spearman: {spearman_corr:.3f}")
    
    if abs(pearson_corr) > 0.7:
        print("   → Strong correlation")
    elif abs(pearson_corr) > 0.3:
        print("   → Moderate correlation")
    else:
        print("   → Weak correlation")
    
    # Regression
    print("\n2. LINEAR REGRESSION:")
    slope, intercept, r_value, p_value, std_err = linregress(clean_df[col1], clean_df[col2])
    print(f"   Equation: {col2} = {slope:.2f} * {col1} + {intercept:.2f}")
    print(f"   R-squared: {r_value**2:.3f}")
    print(f"   P-value: {p_value:.4e}")
    
    if p_value < 0.05:
        print("   → Statistically significant relationship")
    else:
        print("   → NOT statistically significant")
    
    # Visualizations
    fig, axes = plt.subplots(2, 2, figsize=(15, 12))
    
    # Scatter plot
    axes[0, 0].scatter(clean_df[col1], clean_df[col2], alpha=0.5)
    axes[0, 0].set_xlabel(col1)
    axes[0, 0].set_ylabel(col2)
    axes[0, 0].set_title('Scatter Plot')
    axes[0, 0].grid(True, alpha=0.3)
    
    # Scatter with regression line
    axes[0, 1].scatter(clean_df[col1], clean_df[col2], alpha=0.5)
    axes[0, 1].plot(clean_df[col1], slope * clean_df[col1] + intercept, 'r-')
    axes[0, 1].set_xlabel(col1)
    axes[0, 1].set_ylabel(col2)
    axes[0, 1].set_title(f'With Regression Line (R²={r_value**2:.3f})')
    axes[0, 1].grid(True, alpha=0.3)
    
    # Hexbin plot (for large datasets)
    axes[1, 0].hexbin(clean_df[col1], clean_df[col2], gridsize=20, cmap='YlOrRd')
    axes[1, 0].set_xlabel(col1)
    axes[1, 0].set_ylabel(col2)
    axes[1, 0].set_title('Hexbin Plot')
    
    # 2D KDE plot
    sns.kdeplot(data=clean_df, x=col1, y=col2, ax=axes[1, 1], fill=True, cmap='Blues')
    axes[1, 1].set_title('2D Density Plot')
    
    plt.tight_layout()
    plt.show()
    
    print("\n" + "=" * 60)

# Usage
analyze_numerical_numerical(df, 'age', 'salary')
7.2 Categorical vs Categorical
7.2.1 Contingency Table (Cross-tabulation)
Python

# Create contingency table
ct = pd.crosstab(df['department'], df['gender'])
print("CONTINGENCY TABLE:")
print(ct)

# With margins (totals)
ct_with_totals = pd.crosstab(df['department'], df['gender'], margins=True)
print("\nWITH TOTALS:")
print(ct_with_totals)

# Normalized (proportions)
print("\nROW PROPORTIONS:")
print(pd.crosstab(df['department'], df['gender'], normalize='index'))

print("\nCOLUMN PROPORTIONS:")
print(pd.crosstab(df['department'], df['gender'], normalize='columns'))

print("\nOVERALL PROPORTIONS:")
print(pd.crosstab(df['department'], df['gender'], normalize='all'))
7.2.2 Chi-Square Test (Independence Test)
Python

from scipy.stats import chi2_contingency

# Chi-square test
ct = pd.crosstab(df['department'], df['gender'])
chi2, p_value, dof, expected = chi2_contingency(ct)

print("CHI-SQUARE TEST:")
print(f"Chi-square statistic: {chi2:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Degrees of freedom: {dof}")

# Interpretation
alpha = 0.05
if p_value < alpha:
    print(f"\n→ REJECT null hypothesis (p < {alpha})")
    print("→ Variables are DEPENDENT (associated)")
else:
    print(f"\n→ FAIL TO REJECT null hypothesis (p ≥ {alpha})")
    print("→ Variables are INDEPENDENT (not associated)")

# Expected frequencies
print("\nEXPECTED FREQUENCIES:")
print(pd.DataFrame(expected, 
                   index=ct.index, 
                   columns=ct.columns))
Understanding Chi-Square:

text

Null hypothesis: Variables are independent (no association)
Alternative: Variables are dependent (association exists)

P-value < 0.05 → Reject null → Variables are associated
P-value ≥ 0.05 → Don't reject null → No evidence of association
7.2.3 Cramér's V (Effect Size)
Python

def cramers_v(confusion_matrix):
    """Calculate Cramér's V statistic for categorical-categorical association"""
    chi2 = chi2_contingency(confusion_matrix)[0]
    n = confusion_matrix.sum().sum()
    min_dim = min(confusion_matrix.shape) - 1
    return np.sqrt(chi2 / (n * min_dim))

v = cramers_v(ct)
print(f"Cramér's V: {v:.3f}")

# Interpretation
"""
V = 0: No association
V = 0.1: Weak association
V = 0.3: Moderate association
V = 0.5+: Strong association
"""

if v < 0.1:
    print("→ No or very weak association")
elif v < 0.3:
    print("→ Weak association")
elif v < 0.5:
    print("→ Moderate association")
else:
    print("→ Strong association")
7.2.4 Visualizations for Categorical-Categorical
Grouped Bar Chart

Python

# Side-by-side bars
ct.plot(kind='bar', figsize=(10, 6))
plt.xlabel('Department')
plt.ylabel('Count')
plt.title('Department vs Gender')
plt.legend(title='Gender')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Stacked bar chart
ct.plot(kind='bar', stacked=True, figsize=(10, 6))
plt.xlabel('Department')
plt.ylabel('Count')
plt.title('Department vs Gender (Stacked)')
plt.legend(title='Gender')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
Heatmap

Python

plt.figure(figsize=(10, 6))
sns.heatmap(ct, annot=True, fmt='d', cmap='YlGnBu')
plt.title('Department vs Gender Heatmap')
plt.tight_layout()
plt.show()
Mosaic Plot

Python

from statsmodels.graphics.mosaicplot import mosaic

plt.figure(figsize=(10, 6))
mosaic(df, ['department', 'gender'])
plt.title('Mosaic Plot: Department vs Gender')
plt.tight_layout()
plt.show()
7.2.5 Comprehensive Categorical-Categorical Analysis
Python

def analyze_categorical_categorical(df, col1, col2):
    """Complete bivariate analysis for two categorical variables"""
    
    print("=" * 60)
    print(f"BIVARIATE ANALYSIS: {col1} vs {col2}")
    print("=" * 60)
    
    # Contingency table
    ct = pd.crosstab(df[col1], df[col2])
    print("\n1. CONTINGENCY TABLE:")
    print(ct)
    
    ct_with_totals = pd.crosstab(df[col1], df[col2], margins=True)
    print("\nWITH TOTALS:")
    print(ct_with_totals)
    
    # Chi-square test
    print("\n2. CHI-SQUARE TEST:")
    chi2, p_value, dof, expected = chi2_contingency(ct)
    print(f"   Chi-square: {chi2:.4f}")
    print(f"   P-value: {p_value:.4f}")
    print(f"   Degrees of freedom: {dof}")
    
    if p_value < 0.05:
        print("   → Statistically significant association (p < 0.05)")
    else:
        print("   → No significant association (p ≥ 0.05)")
    
    # Cramér's V
    print("\n3. EFFECT SIZE (Cramér's V):")
    v = cramers_v(ct)
    print(f"   V = {v:.3f}")
    
    if v < 0.1:
        print("   → Negligible association")
    elif v < 0.3:
        print("   → Weak association")
    elif v < 0.5:
        print("   → Moderate association")
    else:
        print("   → Strong association")
    
    # Proportions
    print("\n4. PROPORTIONS:")
    print("Row-wise (% within each row):")
    print(pd.crosstab(df[col1], df[col2], normalize='index').round(3))
    
    # Visualizations
    fig, axes = plt.subplots(2, 2, figsize=(15, 12))
    
    # Grouped bar chart
    ct.plot(kind='bar', ax=axes[0, 0])
    axes[0, 0].set_xlabel(col1)
    axes[0, 0].set_ylabel('Count')
    axes[0, 0].set_title('Grouped Bar Chart')
    axes[0, 0].legend(title=col2)
    axes[0, 0].tick_params(axis='x', rotation=45)
    
    # Stacked bar chart
    ct.plot(kind='bar', stacked=True, ax=axes[0, 1])
    axes[0, 1].set_xlabel(col1)
    axes[0, 1].set_ylabel('Count')
    axes[0, 1].set_title('Stacked Bar Chart')
    axes[0, 1].legend(title=col2)
    axes[0, 1].tick_params(axis='x', rotation=45)
    
    # Heatmap
    sns.heatmap(ct, annot=True, fmt='d', cmap='YlGnBu', ax=axes[1, 0])
    axes[1, 0].set_title('Count Heatmap')
    
    # Proportional heatmap
    ct_prop = pd.crosstab(df[col1], df[col2], normalize='index')
    sns.heatmap(ct_prop, annot=True, fmt='.2f', cmap='YlOrRd', ax=axes[1, 1])
    axes[1, 1].set_title('Proportion Heatmap (Row-wise)')
    
    plt.tight_layout()
    plt.show()
    
    print("\n" + "=" * 60)

# Usage
analyze_categorical_categorical(df, 'department', 'gender')
7.3 Numerical vs Categorical
7.3.1 Group Statistics
Python

# Group by category and calculate statistics
print("GROUP STATISTICS:")
print(df.groupby('department')['salary'].describe())

# Specific statistics
print("\nMEAN BY GROUP:")
print(df.groupby('department')['salary'].mean().sort_values(ascending=False))

print("\nMEDIAN BY GROUP:")
print(df.groupby('department')['salary'].median().sort_values(ascending=False))

# Multiple aggregations
print("\nMULTIPLE STATISTICS:")
print(df.groupby('department')['salary'].agg(['count', 'mean', 'median', 'std', 'min', 'max']))
7.3.2 Box Plot
Python

# Basic box plot
plt.figure(figsize=(12, 6))
df.boxplot(column='salary', by='department')
plt.suptitle('')  # Remove default title
plt.xlabel('Department')
plt.ylabel('Salary')
plt.title('Salary Distribution by Department')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Seaborn box plot (more features)
plt.figure(figsize=(12, 6))
sns.boxplot(data=df, x='department', y='salary', order=df.groupby('department')['salary'].median().sort_values().index)
plt.xlabel('Department')
plt.ylabel('Salary')
plt.title('Salary by Department (sorted by median)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
7.3.3 Violin Plot
Python

# Violin plot (combines box plot + distribution)
plt.figure(figsize=(12, 6))
sns.violinplot(data=df, x='department', y='salary')
plt.xlabel('Department')
plt.ylabel('Salary')
plt.title('Salary Distribution by Department (Violin Plot)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# With inner box plot
plt.figure(figsize=(12, 6))
sns.violinplot(data=df, x='department', y='salary', inner='box')
plt.xlabel('Department')
plt.ylabel('Salary')
plt.title('Salary by Department with Inner Box Plot')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
7.3.4 Statistical Tests
T-Test (for 2 groups)

Python

from scipy.stats import ttest_ind

# Example: Compare salary between two departments
group1 = df[df['department'] == 'Engineering']['salary'].dropna()
group2 = df[df['department'] == 'Sales']['salary'].dropna()

t_stat, p_value = ttest_ind(group1, group2)

print("INDEPENDENT T-TEST:")
print(f"T-statistic: {t_stat:.4f}")
print(f"P-value: {p_value:.4f}")

if p_value < 0.05:
    print("\n→ Significant difference between groups (p < 0.05)")
else:
    print("\n→ No significant difference (p ≥ 0.05)")

# Effect size (Cohen's d)
def cohens_d(group1, group2):
    """Calculate Cohen's d for effect size"""
    mean1, mean2 = group1.mean(), group2.mean()
    std1, std2 = group1.std(), group2.std()
    n1, n2 = len(group1), len(group2)
    
    pooled_std = np.sqrt(((n1-1)*std1**2 + (n2-1)*std2**2) / (n1+n2-2))
    d = (mean1 - mean2) / pooled_std
    return d

d = cohens_d(group1, group2)
print(f"\nCohen's d: {d:.3f}")

if abs(d) < 0.2:
    print("→ Small effect size")
elif abs(d) < 0.5:
    print("→ Medium effect size")
else:
    print("→ Large effect size")
ANOVA (for 3+ groups)

Python

from scipy.stats import f_oneway

# Compare salary across all departments
groups = [df[df['department'] == dept]['salary'].dropna() 
          for dept in df['department'].unique()]

f_stat, p_value = f_oneway(*groups)

print("ONE-WAY ANOVA:")
print(f"F-statistic: {f_stat:.4f}")
print(f"P-value: {p_value:.4f}")

if p_value < 0.05:
    print("\n→ At least one group is significantly different (p < 0.05)")
else:
    print("\n→ No significant difference between groups (p ≥ 0.05)")
Post-hoc Test (if ANOVA is significant)

Python

from scipy.stats import tukey_hsd

# Tukey's HSD test
result = tukey_hsd(*groups)
print("\nTUKEY'S HSD POST-HOC TEST:")
print(result)
7.3.5 Comprehensive Numerical-Categorical Analysis
Python

def analyze_numerical_categorical(df, num_col, cat_col):
    """Complete bivariate analysis for numerical vs categorical"""
    
    print("=" * 60)
    print(f"BIVARIATE ANALYSIS: {num_col} vs {cat_col}")
    print("=" * 60)
    
    # Group statistics
    print("\n1. GROUP STATISTICS:")
    group_stats = df.groupby(cat_col)[num_col].agg([
        'count', 'mean', 'median', 'std', 'min', 'max'
    ]).round(2)
    print(group_stats)
    
    # Statistical test
    groups = [df[df[cat_col] == cat][num_col].dropna() 
              for cat in df[cat_col].unique()]
    
    if len(groups) == 2:
        print("\n2. INDEPENDENT T-TEST:")
        t_stat, p_value = ttest_ind(groups[0], groups[1])
        print(f"   T-statistic: {t_stat:.4f}")
        print(f"   P-value: {p_value:.4f}")
        
        if p_value < 0.05:
            print("   → Significant difference (p < 0.05)")
        else:
            print("   → No significant difference (p ≥ 0.05)")
        
        # Effect size
        d = cohens_d(groups[0], groups[1])
        print(f"\n   Cohen's d: {d:.3f}")
    
    elif len(groups) > 2:
        print("\n2. ONE-WAY ANOVA:")
        f_stat, p_value = f_oneway(*groups)
        print(f"   F-statistic: {f_stat:.4f}")
        print(f"   P-value: {p_value:.4f}")
        
        if p_value < 0.05:
            print("   → At least one group differs (p < 0.05)")
        else:
            print("   → No significant differences (p ≥ 0.05)")
    
    # Visualizations
    fig, axes = plt.subplots(2, 2, figsize=(15, 12))
    
    # Box plot
    sns.boxplot(data=df, x=cat_col, y=num_col, ax=axes[0, 0])
    axes[0, 0].set_title('Box Plot')
    axes[0, 0].tick_params(axis='x', rotation=45)
    
    # Violin plot
    sns.violinplot(data=df, x=cat_col, y=num_col, ax=axes[0, 1])
    axes[0, 1].set_title('Violin Plot')
    axes[0, 1].tick_params(axis='x', rotation=45)
    
    # Strip plot (individual points)
    sns.stripplot(data=df, x=cat_col, y=num_col, ax=axes[1, 0], alpha=0.5)
    axes[1, 0].set_title('Strip Plot')
    axes[1, 0].tick_params(axis='x', rotation=45)
    
    # Bar plot with error bars (mean ± std)
    means = df.groupby(cat_col)[num_col].mean()
    stds = df.groupby(cat_col)[num_col].std()
    axes[1, 1].bar(range(len(means)), means.values, yerr=stds.values, capsize=5)
    axes[1, 1].set_xticks(range(len(means)))
    axes[1, 1].set_xticklabels(means.index, rotation=45)
    axes[1, 1].set_ylabel(num_col)
    axes[1, 1].set_title('Mean ± Std Dev')
    
    plt.tight_layout()
    plt.show()
    
    print("\n" + "=" * 60)

# Usage
analyze_numerical_categorical(df, 'salary', 'department')
8. Multivariate Analysis
Multivariate Analysis = Analyzing relationships among THREE or more variables

Goal: Understand complex interactions and patterns

8.1 Three Variables
8.1.1 Two Numerical + One Categorical
Python

# Scatter plot with hue (color by category)
plt.figure(figsize=(12, 6))
sns.scatterplot(data=df, x='age', y='salary', hue='department', 
                style='department', s=100, alpha=0.7)
plt.title('Age vs Salary by Department')
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()

# With size (4th variable)
plt.figure(figsize=(12, 6))
sns.scatterplot(data=df, x='age', y='salary', hue='department', 
                size='experience', sizes=(50, 500), alpha=0.7)
plt.title('Age vs Salary by Department and Experience')
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()

# Pair plot (all combinations)
sns.pairplot(df, hue='department', vars=['age', 'salary', 'experience'])
plt.suptitle('Pair Plot', y=1.02)
plt.show()
8.1.2 One Numerical + Two Categorical
Python

# Grouped box plot
plt.figure(figsize=(14, 6))
sns.boxplot(data=df, x='department', y='salary', hue='gender')
plt.title('Salary by Department and Gender')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Facet grid (subplots)
g = sns.FacetGrid(df, col='department', hue='gender', height=4, aspect=1.2)
g.map(sns.histplot, 'salary', kde=True, alpha=0.7)
g.add_legend()
plt.suptitle('Salary Distribution by Department and Gender', y=1.02)
plt.show()
8.1.3 Three Categorical Variables
Python

# Three-way contingency table
ct_3way = pd.crosstab([df['department'], df['gender']], df['city'])
print("THREE-WAY CONTINGENCY TABLE:")
print(ct_3way)

# Stacked bar chart
ct_3way.plot(kind='bar', stacked=True, figsize=(14, 6))
plt.xlabel('Department - Gender')
plt.ylabel('Count')
plt.title('Department, Gender, and City Distribution')
plt.legend(title='City', bbox_to_anchor=(1.05, 1))
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
8.2 Correlation Analysis (Multiple Variables)
Python

# Select numerical columns
numerical_cols = df.select_dtypes(include=[np.number]).columns

# Correlation matrix
corr_matrix = df[numerical_cols].corr()

# Visualize with heatmap
plt.figure(figsize=(12, 10))
sns.heatmap(corr_matrix, 
            annot=True, 
            fmt='.2f',
            cmap='coolwarm',
            center=0,
            square=True,
            linewidths=1,
            cbar_kws={"shrink": 0.8},
            vmin=-1, 
            vmax=1)
plt.title('Correlation Matrix Heatmap', fontsize=16, pad=20)
plt.tight_layout()
plt.show()

# Find highly correlated pairs
def find_high_correlations(corr_matrix, threshold=0.7):
    """Find variable pairs with correlation > threshold"""
    high_corr = []
    
    for i in range(len(corr_matrix.columns)):
        for j in range(i+1, len(corr_matrix.columns)):
            if abs(corr_matrix.iloc[i, j]) > threshold:
                high_corr.append({
                    'var1': corr_matrix.columns[i],
                    'var2': corr_matrix.columns[j],
                    'correlation': corr_matrix.iloc[i, j]
                })
    
    return pd.DataFrame(high_corr).sort_values('correlation', 
                                                ascending=False, 
                                                key=abs)

high_corr_df = find_high_correlations(corr_matrix, threshold=0.7)
print("HIGHLY CORRELATED PAIRS (|r| > 0.7):")
print(high_corr_df)
8.3 Pair Plot (Pairwise Relationships)
Python

# Basic pair plot
sns.pairplot(df[numerical_cols])
plt.suptitle('Pair Plot - All Numerical Variables', y=1.02)
plt.show()

# With categorical coloring
sns.pairplot(df, hue='department', 
             vars=numerical_cols,
             diag_kind='kde',  # Distribution on diagonal
             plot_kws={'alpha': 0.6})
plt.suptitle('Pair Plot by Department', y=1.02)
plt.show()

# Advanced: with regression lines
sns.pairplot(df, hue='department',
             vars=numerical_cols,
             kind='reg',  # Add regression lines
             diag_kind='kde',
             plot_kws={'scatter_kws': {'alpha': 0.5}})
plt.suptitle('Pair Plot with Regression Lines', y=1.02)
plt.show()
8.4 Dimensionality Reduction
8.4.1 Principal Component Analysis (PCA)
Python

from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

# Prepare data (PCA requires scaling)
X = df[numerical_cols].dropna()
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Apply PCA
pca = PCA()
X_pca = pca.fit_transform(X_scaled)

# Explained variance
explained_var = pca.explained_variance_ratio_
cumulative_var = np.cumsum(explained_var)

print("EXPLAINED VARIANCE:")
for i, (ev, cv) in enumerate(zip(explained_var, cumulative_var)):
    print(f"PC{i+1}: {ev:.3f} ({cv:.3f} cumulative)")

# Scree plot
fig, axes = plt.subplots(1, 2, figsize=(15, 5))

# Variance explained
axes[0].bar(range(1, len(explained_var)+1), explained_var)
axes[0].set_xlabel('Principal Component')
axes[0].set_ylabel('Variance Explained')
axes[0].set_title('Scree Plot')
axes[0].set_xticks(range(1, len(explained_var)+1))

# Cumulative variance
axes[1].plot(range(1, len(cumulative_var)+1), cumulative_var, 'bo-')
axes[1].axhline(y=0.8, color='r', linestyle='--', label='80% threshold')
axes[1].axhline(y=0.9, color='g', linestyle='--', label='90% threshold')
axes[1].set_xlabel('Number of Components')
axes[1].set_ylabel('Cumulative Variance Explained')
axes[1].set_title('Cumulative Variance Plot')
axes[1].legend()
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

# Determine optimal number of components (e.g., 80% variance)
n_components = np.argmax(cumulative_var >= 0.8) + 1
print(f"\nOptimal components (80% variance): {n_components}")

# Visualize first two principal components
pca_2d = PCA(n_components=2)
X_pca_2d = pca_2d.fit_transform(X_scaled)

plt.figure(figsize=(10, 6))
plt.scatter(X_pca_2d[:, 0], X_pca_2d[:, 1], alpha=0.5)
plt.xlabel(f'PC1 ({pca_2d.explained_variance_ratio_[0]:.2%})')
plt.ylabel(f'PC2 ({pca_2d.explained_variance_ratio_[1]:.2%})')
plt.title('First Two Principal Components')
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

# With categorical coloring
if 'department' in df.columns:
    plt.figure(figsize=(12, 6))
    for dept in df['department'].unique():
        mask = df['department'] == dept
        plt.scatter(X_pca_2d[mask, 0], X_pca_2d[mask, 1], 
                   label=dept, alpha=0.6, s=50)
    plt.xlabel(f'PC1 ({pca_2d.explained_variance_ratio_[0]:.2%})')
    plt.ylabel(f'PC2 ({pca_2d.explained_variance_ratio_[1]:.2%})')
    plt.title('PCA by Department')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.tight_layout()
    plt.show()

# Component loadings (variable contributions)
loadings = pd.DataFrame(
    pca_2d.components_.T,
    columns=['PC1', 'PC2'],
    index=numerical_cols
)
print("\nCOMPONENT LOADINGS:")
print(loadings)

# Visualize loadings
plt.figure(figsize=(10, 6))
sns.heatmap(loadings, annot=True, cmap='coolwarm', center=0, 
            cbar_kws={'label': 'Loading'})
plt.title('PCA Component Loadings')
plt.tight_layout()
plt.show()
8.4.2 t-SNE (for visualization)
Python

from sklearn.manifold import TSNE

# Apply t-SNE
tsne = TSNE(n_components=2, random_state=42, perplexity=30)
X_tsne = tsne.fit_transform(X_scaled)

# Visualize
plt.figure(figsize=(12, 6))
if 'department' in df.columns:
    for dept in df['department'].unique():
        mask = df['department'] == dept
        plt.scatter(X_tsne[mask, 0], X_tsne[mask, 1], 
                   label=dept, alpha=0.6, s=50)
    plt.legend()
else:
    plt.scatter(X_tsne[:, 0], X_tsne[:, 1], alpha=0.6)

plt.xlabel('t-SNE Component 1')
plt.ylabel('t-SNE Component 2')
plt.title('t-SNE Visualization')
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()
8.5 Clustering Analysis
Python

from sklearn.cluster import KMeans

# Determine optimal number of clusters (Elbow method)
inertias = []
silhouette_scores = []
K_range = range(2, 11)

for k in K_range:
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    kmeans.fit(X_scaled)
    inertias.append(kmeans.inertia_)
    
    from sklearn.metrics import silhouette_score
    score = silhouette_score(X_scaled, kmeans.labels_)
    silhouette_scores.append(score)

# Plot elbow curve
fig, axes = plt.subplots(1, 2, figsize=(15, 5))

axes[0].plot(K_range, inertias, 'bo-')
axes[0].set_xlabel('Number of Clusters (k)')
axes[0].set_ylabel('Inertia')
axes[0].set_title('Elbow Method')
axes[0].grid(True, alpha=0.3)

axes[1].plot(K_range, silhouette_scores, 'go-')
axes[1].set_xlabel('Number of Clusters (k)')
axes[1].set_ylabel('Silhouette Score')
axes[1].set_title('Silhouette Analysis')
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

# Apply K-Means with optimal k
optimal_k = 3  # Choose based on elbow/silhouette
kmeans = KMeans(n_clusters=optimal_k, random_state=42, n_init=10)
clusters = kmeans.fit_predict(X_scaled)

# Visualize clusters (using PCA)
pca_2d = PCA(n_components=2)
X_pca_2d = pca_2d.fit_transform(X_scaled)

plt.figure(figsize=(12, 6))
scatter = plt.scatter(X_pca_2d[:, 0], X_pca_2d[:, 1], 
                     c=clusters, cmap='viridis', 
                     alpha=0.6, s=50)
plt.xlabel(f'PC1 ({pca_2d.explained_variance_ratio_[0]:.2%})')
plt.ylabel(f'PC2 ({pca_2d.explained_variance_ratio_[1]:.2%})')
plt.title(f'K-Means Clustering (k={optimal_k})')
plt.colorbar(scatter, label='Cluster')
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

# Cluster profiles
df_with_clusters = df[numerical_cols].copy()
df_with_clusters['Cluster'] = clusters

print("\nCLUSTER PROFILES:")
print(df_with_clusters.groupby('Cluster').mean())
8.6 Parallel Coordinates Plot
Python

from pandas.plotting import parallel_coordinates

# Normalize data for better visualization
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
df_normalized = pd.DataFrame(
    scaler.fit_transform(df[numerical_cols]),
    columns=numerical_cols
)

if 'department' in df.columns:
    df_normalized['department'] = df['department'].values

plt.figure(figsize=(14, 6))
parallel_coordinates(df_normalized, 'department', alpha=0.5)
plt.title('Parallel Coordinates Plot')
plt.xlabel('Variables')
plt.ylabel('Normalized Values')
plt.xticks(rotation=45)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()
9. Feature Engineering Through EDA
Feature Engineering = Creating new features from existing data to improve model performance

9.1 Creating New Features
9.1.1 Mathematical Transformations
Python

# Ratios
df['salary_per_year_experience'] = df['salary'] / (df['experience'] + 1)

# Differences
df['age_minus_experience'] = df['age'] - df['experience']

# Products
df['age_experience_interaction'] = df['age'] * df['experience']

# Polynomials
df['age_squared'] = df['age'] ** 2
df['age_cubed'] = df['age'] ** 3

# Log transformations (for skewed data)
df['log_salary'] = np.log1p(df['salary'])  # log1p = log(1 + x)

# Square root
df['sqrt_salary'] = np.sqrt(df['salary'])

# Binning (continuous → categorical)
df['age_group'] = pd.cut(df['age'], 
                         bins=[0, 25, 35, 45, 100],
                         labels=['Young', 'Middle', 'Senior', 'Expert'])

# Quantile binning (equal-sized groups)
df['salary_quartile'] = pd.qcut(df['salary'], 
                                q=4, 
                                labels=['Q1', 'Q2', 'Q3', 'Q4'])
9.1.2 Date/Time Features
Python

# Assuming df has a 'date' column
df['date'] = pd.to_datetime(df['date'])

# Extract components
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['day_of_week'] = df['date'].dt.dayofweek  # Monday=0, Sunday=6
df['day_name'] = df['date'].dt.day_name()
df['week_of_year'] = df['date'].dt.isocalendar().week
df['quarter'] = df['date'].dt.quarter
df['is_weekend'] = df['date'].dt.dayofweek.isin([5, 6]).astype(int)
df['is_month_start'] = df['date'].dt.is_month_start.astype(int)
df['is_month_end'] = df['date'].dt.is_month_end.astype(int)

# Time-based features
df['days_since_start'] = (df['date'] - df['date'].min()).dt.days
df['days_until_end'] = (df['date'].max() - df['date']).dt.days

# Cyclical encoding (for periodic features)
df['month_sin'] = np.sin(2 * np.pi * df['month'] / 12)
df['month_cos'] = np.cos(2 * np.pi * df['month'] / 12)
df['day_of_week_sin'] = np.sin(2 * np.pi * df['day_of_week'] / 7)
df['day_of_week_cos'] = np.cos(2 * np.pi * df['day_of_week'] / 7)
9.1.3 Text Features
Python

# Assuming df has a 'description' column
df['text_length'] = df['description'].str.len()
df['word_count'] = df['description'].str.split().str.len()
df['avg_word_length'] = df['text_length'] / df['word_count']
df['uppercase_count'] = df['description'].str.count(r'[A-Z]')
df['digit_count'] = df['description'].str.count(r'\d')
df['special_char_count'] = df['description'].str.count(r'[^a-zA-Z0-9\s]')

# Specific word presence
df['contains_urgent'] = df['description'].str.contains('urgent', case=False).astype(int)

# Sentiment analysis (requires textblob)
# pip install textblob
from textblob import TextBlob
df['sentiment_polarity'] = df['description'].apply(lambda x: TextBlob(str(x)).sentiment.polarity)
9.1.4 Aggregation Features
Python

# Group statistics
df['dept_avg_salary'] = df.groupby('department')['salary'].transform('mean')
df['dept_max_salary'] = df.groupby('department')['salary'].transform('max')
df['dept_min_salary'] = df.groupby('department')['salary'].transform('min')
df['salary_vs_dept_avg'] = df['salary'] - df['dept_avg_salary']
df['salary_rank_in_dept'] = df.groupby('department')['salary'].rank(ascending=False)

# Count features
df['dept_size'] = df.groupby('department')['department'].transform('count')

# Multiple group statistics
df['city_dept_avg_salary'] = df.groupby(['city', 'department'])['salary'].transform('mean')
9.1.5 Interaction Features
Python

# Categorical × Categorical
df['dept_gender'] = df['department'] + '_' + df['gender']

# Numerical × Categorical (already shown in aggregation features)

# Polynomial interactions (all combinations)
from sklearn.preprocessing import PolynomialFeatures

poly = PolynomialFeatures(degree=2, include_bias=False, interaction_only=True)
numerical_subset = df[['age', 'experience', 'salary']].fillna(0)
interactions = poly.fit_transform(numerical_subset)

# Get feature names
feature_names = poly.get_feature_names_out(['age', 'experience', 'salary'])
interactions_df = pd.DataFrame(interactions, columns=feature_names)

print("Interaction features:")
print(interactions_df.head())
9.2 Encoding Categorical Variables
9.2.1 Label Encoding (for ordinal data)
Python

from sklearn.preprocessing import LabelEncoder

# Ordinal categorical (has order)
education_order = {'High School': 1, 'Bachelor': 2, 'Master': 3, 'PhD': 4}
df['education_encoded'] = df['education'].map(education_order)

# Or use LabelEncoder (automatic assignment)
le = LabelEncoder()
df['department_encoded'] = le.fit_transform(df['department'])

# Save mapping for later use
label_mapping = dict(zip(le.classes_, le.transform(le.classes_)))
print("Label mapping:", label_mapping)
9.2.2 One-Hot Encoding (for nominal data)
Python

# Pandas get_dummies (simple)
df_encoded = pd.get_dummies(df, columns=['department', 'city'], prefix=['dept', 'city'])
print(df_encoded.head())

# Sklearn OneHotEncoder (more control)
from sklearn.preprocessing import OneHotEncoder

ohe = OneHotEncoder(sparse_output=False, drop='first')  # drop='first' to avoid multicollinearity
encoded = ohe.fit_transform(df[['department']])

# Get feature names
feature_names = ohe.get_feature_names_out(['department'])
encoded_df = pd.DataFrame(encoded, columns=feature_names)
print(encoded_df.head())
9.2.3 Target Encoding (mean encoding)
Python

# Encode category by target mean (useful for high-cardinality features)
# WARNING: Can cause overfitting - use with cross-validation!

def target_encode(df, column, target, smoothing=1):
    """
    Target encoding with smoothing
    smoothing: higher = more regularization
    """
    # Global mean
    global_mean = df[target].mean()
    
    # Group means and counts
    agg = df.groupby(column)[target].agg(['mean', 'count'])
    
    # Smooth the means
    smoothed_mean = (agg['mean'] * agg['count'] + global_mean * smoothing) / (agg['count'] + smoothing)
    
    # Map to original dataframe
    return df[column].map(smoothed_mean)

df['city_target_encoded'] = target_encode(df, 'city', 'salary', smoothing=10)
9.2.4 Frequency Encoding
Python

# Encode by frequency (count)
freq_map = df['city'].value_counts().to_dict()
df['city_frequency'] = df['city'].map(freq_map)

# Normalize to percentage
total = len(df)
df['city_frequency_pct'] = df['city_frequency'] / total
9.3 Feature Scaling
Python

from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

# StandardScaler (mean=0, std=1)
scaler = StandardScaler()
df['salary_standardized'] = scaler.fit_transform(df[['salary']])

# MinMaxScaler (range 0-1)
scaler = MinMaxScaler()
df['salary_normalized'] = scaler.fit_transform(df[['salary']])

# RobustScaler (uses median and IQR - robust to outliers)
scaler = RobustScaler()
df['salary_robust'] = scaler.fit_transform(df[['salary']])

# Compare
print("Original:", df['salary'].describe())
print("\nStandardized:", df['salary_standardized'].describe())
print("\nNormalized:", df['salary_normalized'].describe())
print("\nRobust:", df['salary_robust'].describe())
9.4 Feature Selection
9.4.1 Variance Threshold
Python

from sklearn.feature_selection import VarianceThreshold

# Remove low-variance features
selector = VarianceThreshold(threshold=0.01)  # Remove features with variance < 0.01
X_high_var = selector.fit_transform(df[numerical_cols])

# Get selected features
selected_features = df[numerical_cols].columns[selector.get_support()]
print("Selected features:", list(selected_features))
print("Removed features:", list(set(numerical_cols) - set(selected_features)))
9.4.2 Correlation-Based Selection
Python

def remove_correlated_features(df, threshold=0.9):
    """Remove features with correlation > threshold"""
    corr_matrix = df.corr().abs()
    
    # Upper triangle of correlation matrix
    upper = corr_matrix.where(np.triu(np.ones(corr_matrix.shape), k=1).astype(bool))
    
    # Find features with correlation > threshold
    to_drop = [column for column in upper.columns if any(upper[column] > threshold)]
    
    return df.drop(columns=to_drop), to_drop

df_reduced, dropped_features = remove_correlated_features(df[numerical_cols], threshold=0.9)
print("Dropped features:", dropped_features)
9.4.3 Mutual Information
Python

from sklearn.feature_selection import mutual_info_regression, mutual_info_classif

# For regression
mi_scores = mutual_info_regression(df[numerical_cols], df['target'])
mi_scores = pd.Series(mi_scores, index=numerical_cols).sort_values(ascending=False)

print("Mutual Information Scores:")
print(mi_scores)

# Visualize
plt.figure(figsize=(10, 6))
mi_scores.plot(kind='bar')
plt.xlabel('Features')
plt.ylabel('Mutual Information Score')
plt.title('Feature Importance (Mutual Information)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
9.4.4 Recursive Feature Elimination (RFE)
Python

from sklearn.feature_selection import RFE
from sklearn.ensemble import RandomForestRegressor

# RFE with Random Forest
model = RandomForestRegressor(n_estimators=100, random_state=42)
rfe = RFE(estimator=model, n_features_to_select=5)

X = df[numerical_cols].fillna(0)
y = df['target']

rfe.fit(X, y)

# Get selected features
selected_features = X.columns[rfe.support_]
print("Selected features:", list(selected_features))

# Feature ranking
ranking = pd.Series(rfe.ranking_, index=X.columns).sort_values()
print("\nFeature ranking:")
print(ranking)
9.5 Feature Engineering Pipeline
Python

def create_features(df):
    """Comprehensive feature engineering pipeline"""
    
    df = df.copy()
    
    print("Starting feature engineering...")
    
    # 1. Mathematical features
    if 'salary' in df.columns and 'experience' in df.columns:
        df['salary_per_experience'] = df['salary'] / (df['experience'] + 1)
    
    if 'age' in df.columns:
        df['age_squared'] = df['age'] ** 2
    
    # 2. Date features (if date column exists)
    if 'date' in df.columns:
        df['date'] = pd.to_datetime(df['date'])
        df['year'] = df['date'].dt.year
        df['month'] = df['date'].dt.month
        df['day_of_week'] = df['date'].dt.dayofweek
        df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
    
    # 3. Aggregation features
    if 'department' in df.columns and 'salary' in df.columns:
        df['dept_avg_salary'] = df.groupby('department')['salary'].transform('mean')
        df['salary_vs_dept_avg'] = df['salary'] - df['dept_avg_salary']
    
    # 4. Binning
    if 'age' in df.columns:
        df['age_group'] = pd.cut(df['age'], bins=[0, 25, 35, 45, 100],
                                 labels=['Young', 'Middle', 'Senior', 'Expert'])
    
    # 5. Encoding
    if 'department' in df.columns:
        df = pd.get_dummies(df, columns=['department'], prefix='dept', drop_first=True)
    
    # 6. Scaling (numerical columns)
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    scaler = StandardScaler()
    df[numerical_cols] = scaler.fit_transform(df[numerical_cols].fillna(0))
    
    print(f"Feature engineering complete. New shape: {df.shape}")
    
    return df

# Usage
df_engineered = create_features(df)
10. Advanced EDA Techniques
10.1 Distribution Analysis
10.1.1 Normality Tests
Python

from scipy.stats import shapiro, normaltest, anderson

def test_normality(data):
    """Comprehensive normality testing"""
    
    print("="*60)
    print("NORMALITY TESTS")
    print("="*60)
    
    # 1. Shapiro-Wilk Test
    stat, p = shapiro(data)
    print(f"\n1. Shapiro-Wilk Test:")
    print(f"   Statistic: {stat:.4f}")
    print(f"   P-value: {p:.4f}")
    if p > 0.05:
        print("   → Data appears normal (p > 0.05)")
    else:
        print("   → Data does NOT appear normal (p ≤ 0.05)")
    
    # 2. D'Agostino's K-squared Test
    stat, p = normaltest(data)
    print(f"\n2. D'Agostino's K-squared Test:")
    print(f"   Statistic: {stat:.4f}")
    print(f"   P-value: {p:.4f}")
    if p > 0.05:
        print("   → Data appears normal (p > 0.05)")
    else:
        print("   → Data does NOT appear normal (p ≤ 0.05)")
    
    # 3. Anderson-Darling Test
    result = anderson(data)
    print(f"\n3. Anderson-Darling Test:")
    print(f"   Statistic: {result.statistic:.4f}")
    for i in range(len(result.critical_values)):
        sl, cv = result.significance_level[i], result.critical_values[i]
        if result.statistic < cv:
            print(f"   → Normal at {sl}% significance level")
        else:
            print(f"   → NOT normal at {sl}% significance level")
    
    # Visual tests
    fig, axes = plt.subplots(1, 3, figsize=(18, 5))
    
    # Histogram with normal curve
    axes[0].hist(data, bins=30, density=True, alpha=0.7, edgecolor='black')
    mu, sigma = data.mean(), data.std()
    x = np.linspace(data.min(), data.max(), 100)
    axes[0].plot(x, (1/(sigma * np.sqrt(2*np.pi))) * np.exp(-0.5*((x-mu)/sigma)**2), 
                'r-', linewidth=2, label='Normal curve')
    axes[0].set_xlabel('Value')
    axes[0].set_ylabel('Density')
    axes[0].set_title('Histogram vs Normal Distribution')
    axes[0].legend()
    
    # Q-Q plot
    from scipy import stats
    stats.probplot(data, dist="norm", plot=axes[1])
    axes[1].set_title('Q-Q Plot')
    axes[1].grid(True, alpha=0.3)
    
    # Box plot
    axes[2].boxplot(data)
    axes[2].set_ylabel('Value')
    axes[2].set_title('Box Plot')
    axes[2].grid(True, alpha=0.3)
    
    plt.tight_layout()
    plt.show()

# Usage
test_normality(df['salary'].dropna())
10.1.2 Distribution Fitting
Python

from scipy import stats

def fit_distributions(data):
    """Fit multiple distributions and find best fit"""
    
    # List of distributions to try
    distributions = [
        stats.norm,
        stats.lognorm,
        stats.expon,
        stats.gamma,
        stats.beta,
        stats.weibull_min
    ]
    
    results = []
    
    for dist in distributions:
        try:
            # Fit distribution
            params = dist.fit(data)
            
            # Kolmogorov-Smirnov test
            ks_stat, ks_p = stats.kstest(data, dist.name, args=params)
            
            # Anderson-Darling test (if available)
            try:
                ad_result = stats.anderson(data, dist=dist.name)
                ad_stat = ad_result.statistic
            except:
                ad_stat = np.nan
            
            results.append({
                'Distribution': dist.name,
                'Parameters': params,
                'KS_Statistic': ks_stat,
                'KS_P_value': ks_p,
                'AD_Statistic': ad_stat
            })
        except:
            pass
    
    # Create results dataframe
    results_df = pd.DataFrame(results).sort_values('KS_P_value', ascending=False)
    
    print("DISTRIBUTION FITTING RESULTS:")
    print(results_df)
    
    # Plot best fit
    best_dist_name = results_df.iloc[0]['Distribution']
    best_params = results_df.iloc[0]['Parameters']
    best_dist = getattr(stats, best_dist_name)
    
    plt.figure(figsize=(12, 6))
    plt.hist(data, bins=30, density=True, alpha=0.7, edgecolor='black', label='Data')
    
    x = np.linspace(data.min(), data.max(), 100)
    plt.plot(x, best_dist.pdf(x, *best_params), 'r-', linewidth=2, 
            label=f'Best fit: {best_dist_name}')
    
    plt.xlabel('Value')
    plt.ylabel('Density')
    plt.title(f'Best Fitting Distribution: {best_dist_name}')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.tight_layout()
    plt.show()
    
    return results_df

# Usage
fit_distributions(df['salary'].dropna())
10.2 Time Series Analysis
Python

def analyze_time_series(df, date_col, value_col):
    """Comprehensive time series EDA"""
    
    # Ensure datetime
    df[date_col] = pd.to_datetime(df[date_col])
    df = df.sort_values(date_col)
    
    print("="*60)
    print(f"TIME SERIES ANALYSIS: {value_col}")
    print("="*60)
    
    # Basic statistics
    print(f"\nDate range: {df[date_col].min()} to {df[date_col].max()}")
    print(f"Number of observations: {len(df)}")
    print(f"Frequency: {pd.infer_freq(df[date_col])}")
    
    # Trend analysis
    from scipy.stats import linregress
    x = np.arange(len(df))
    slope, intercept, r_value, p_value, std_err = linregress(x, df[value_col])
    
    print(f"\nTrend analysis:")
    print(f"   Slope: {slope:.4f}")
    print(f"   R-squared: {r_value**2:.4f}")
    if slope > 0:
        print("   → Upward trend")
    elif slope < 0:
        print("   → Downward trend")
    else:
        print("   → No trend")
    
    # Seasonality detection
    df['month'] = df[date_col].dt.month
    monthly_avg = df.groupby('month')[value_col].mean()
    seasonality_strength = monthly_avg.std() / monthly_avg.mean()
    
    print(f"\nSeasonality strength: {seasonality_strength:.4f}")
    if seasonality_strength > 0.2:
        print("   → Strong seasonality detected")
    elif seasonality_strength > 0.1:
        print("   → Moderate seasonality")
    else:
        print("   → Weak or no seasonality")
    
    # Visualizations
    fig, axes = plt.subplots(3, 2, figsize=(16, 14))
    
    # 1. Time series plot
    axes[0, 0].plot(df[date_col], df[value_col])
    axes[0, 0].plot(df[date_col], slope * x + intercept, 'r--', label='Trend')
    axes[0, 0].set_xlabel('Date')
    axes[0, 0].set_ylabel(value_col)
    axes[0, 0].set_title('Time Series Plot')
    axes[0, 0].legend()
    axes[0, 0].grid(True, alpha=0.3)
    
    # 2. Moving average
    df['MA_7'] = df[value_col].rolling(window=7).mean()
    df['MA_30'] = df[value_col].rolling(window=30).mean()
    axes[0, 1].plot(df[date_col], df[value_col], alpha=0.3, label='Original')
    axes[0, 1].plot(df[date_col], df['MA_7'], label='7-day MA')
    axes[0, 1].plot(df[date_col], df['MA_30'], label='30-day MA')
    axes[0, 1].set_xlabel('Date')
    axes[0, 1].set_ylabel(value_col)
    axes[0, 1].set_title('Moving Averages')
    axes[0, 1].legend()
    axes[0, 1].grid(True, alpha=0.3)
    
    # 3. Seasonal plot
    monthly_avg.plot(kind='bar', ax=axes[1, 0])
    axes[1, 0].set_xlabel('Month')
    axes[1, 0].set_ylabel(f'Average {value_col}')
    axes[1, 0].set_title('Seasonal Pattern (Monthly)')
    axes[1, 0].grid(True, alpha=0.3)
    
    # 4. Box plot by month
    df.boxplot(column=value_col, by='month', ax=axes[1, 1])
    axes[1, 1].set_xlabel('Month')
    axes[1, 1].set_ylabel(value_col)
    axes[1, 1].set_title('Distribution by Month')
    plt.sca(axes[1, 1])
    plt.xticks(rotation=0)
    
    # 5. Autocorrelation
    from pandas.plotting import autocorrelation_plot
    autocorrelation_plot(df[value_col], ax=axes[2, 0])
    axes[2, 0].set_title('Autocorrelation Plot')
    
    # 6. Histogram
    axes[2, 1].hist(df[value_col], bins=30, edgecolor='black')
    axes[2, 1].set_xlabel(value_col)
    axes[2, 1].set_ylabel('Frequency')
    axes[2, 1].set_title('Distribution')
    axes[2, 1].grid(True, alpha=0.3)
    
    plt.tight_layout()
    plt.show()

# Usage
analyze_time_series(df, 'date', 'sales')
10.3 Outlier Detection (Advanced Methods)
Python

def advanced_outlier_detection(df, column):
    """Multiple outlier detection methods"""
    
    data = df[column].dropna()
    
    print("="*60)
    print(f"ADVANCED OUTLIER DETECTION: {column}")
    print("="*60)
    
    # 1. IQR method
    Q1, Q3 = data.quantile([0.25, 0.75])
    IQR = Q3 - Q1
    lower_iqr = Q1 - 1.5 * IQR
    upper_iqr = Q3 + 1.5 * IQR
    outliers_iqr = data[(data < lower_iqr) | (data > upper_iqr)]
    
    # 2. Z-score method
    from scipy.stats import zscore
    z_scores = np.abs(zscore(data))
    outliers_zscore = data[z_scores > 3]
    
    # 3. Modified Z-score (using MAD)
    median = data.median()
    mad = np.median(np.abs(data - median))
    modified_z_scores = 0.6745 * (data - median) / mad
    outliers_mad = data[np.abs(modified_z_scores) > 3.5]
    
    # 4. Isolation Forest
    from sklearn.ensemble import IsolationForest
    iso_forest = IsolationForest(contamination=0.1, random_state=42)
    outlier_labels = iso_forest.fit_predict(data.values.reshape(-1, 1))
    outliers_iso = data[outlier_labels == -1]
    
    # 5. Local Outlier Factor
    from sklearn.neighbors import LocalOutlierFactor
    lof = LocalOutlierFactor(n_neighbors=20, contamination=0.1)
    outlier_labels_lof = lof.fit_predict(data.values.reshape(-1, 1))
    outliers_lof = data[outlier_labels_lof == -1]
    
    # Summary
    print("\nOUTLIER DETECTION SUMMARY:")
    print(f"Total data points: {len(data)}")
    print(f"\n1. IQR Method: {len(outliers_iqr)} outliers ({len(outliers_iqr)/len(data)*100:.2f}%)")
    print(f"2. Z-Score Method: {len(outliers_zscore)} outliers ({len(outliers_zscore)/len(data)*100:.2f}%)")
    print(f"3. Modified Z-Score (MAD): {len(outliers_mad)} outliers ({len(outliers_mad)/len(data)*100:.2f}%)")
    print(f"4. Isolation Forest: {len(outliers_iso)} outliers ({len(outliers_iso)/len(data)*100:.2f}%)")
    print(f"5. Local Outlier Factor: {len(outliers_lof)} outliers ({len(outliers_lof)/len(data)*100:.2f}%)")
    
    # Visualization
    fig, axes = plt.subplots(2, 3, figsize=(18, 10))
    
    # Original data
    axes[0, 0].hist(data, bins=50, edgecolor='black')
    axes[0, 0].set_title('Original Distribution')
    axes[0, 0].set_xlabel(column)
    axes[0, 0].set_ylabel('Frequency')
    
    # IQR
    axes[0, 1].boxplot(data)
    axes[0, 1].scatter(np.ones(len(outliers_iqr)), outliers_iqr, c='red', label='Outliers')
    axes[0, 1].set_title(f'IQR Method\n({len(outliers_iqr)} outliers)')
    axes[0, 1].legend()
    
    # Z-score
    axes[0, 2].scatter(range(len(data)), data, alpha=0.5)
    axes[0, 2].scatter(outliers_zscore.index, outliers_zscore, c='red', label='Outliers')
    axes[0, 2].set_title(f'Z-Score Method\n({len(outliers_zscore)} outliers)')
    axes[0, 2].set_xlabel('Index')
    axes[0, 2].set_ylabel(column)
    axes[0, 2].legend()
    
    # Modified Z-score
    axes[1, 0].scatter(range(len(data)), data, alpha=0.5)
    axes[1, 0].scatter(outliers_mad.index, outliers_mad, c='red', label='Outliers')
    axes[1, 0].set_title(f'Modified Z-Score\n({len(outliers_mad)} outliers)')
    axes[1, 0].set_xlabel('Index')
    axes[1, 0].set_ylabel(column)
    axes[1, 0].legend()
    
    # Isolation Forest
    axes[1, 1].scatter(range(len(data)), data, c=outlier_labels, cmap='coolwarm', alpha=0.6)
    axes[1, 1].set_title(f'Isolation Forest\n({len(outliers_iso)} outliers)')
    axes[1, 1].set_xlabel('Index')
    axes[1, 1].set_ylabel(column)
    
    # LOF
    axes[1, 2].scatter(range(len(data)), data, c=outlier_labels_lof, cmap='coolwarm', alpha=0.6)
    axes[1, 2].set_title(f'Local Outlier Factor\n({len(outliers_lof)} outliers)')
    axes[1, 2].set_xlabel('Index')
    axes[1, 2].set_ylabel(column)
    
    plt.tight_layout()
    plt.show()
    
    return {
        'iqr': outliers_iqr,
        'zscore': outliers_zscore,
        'mad': outliers_mad,
        'isolation_forest': outliers_iso,
        'lof': outliers_lof
    }

# Usage
outliers_dict = advanced_outlier_detection(df, 'salary')
10.4 Imbalance Analysis (for Classification)
Python

def analyze_class_imbalance(df, target_col):
    """Analyze and visualize class imbalance"""
    
    print("="*60)
    print(f"CLASS IMBALANCE ANALYSIS: {target_col}")
    print("="*60)
    
    # Class distribution
    class_counts = df[target_col].value_counts()
    class_percentages = df[target_col].value_counts(normalize=True) * 100
    
    print("\nCLASS DISTRIBUTION:")
    for cls, count in class_counts.items():
        pct = class_percentages[cls]
        print(f"   {cls}: {count} ({pct:.2f}%)")
    
    # Imbalance ratio
    majority_count = class_counts.max()
    minority_count = class_counts.min()
    imbalance_ratio = majority_count / minority_count
    
    print(f"\nIMBALANCE RATIO: {imbalance_ratio:.2f}")
    
    if imbalance_ratio < 1.5:
        print("   → Balanced dataset")
    elif imbalance_ratio < 3:
        print("   → Slightly imbalanced")
    elif imbalance_ratio < 10:
        print("   → Moderately imbalanced")
    else:
        print("   → Severely imbalanced")
        print("   ⚠ Consider resampling techniques:")
        print("      - Oversampling (SMOTE)")
        print("      - Undersampling")
        print("      - Class weights")
    
    # Visualization
    fig, axes = plt.subplots(1, 3, figsize=(18, 5))
    
    # Bar chart
    class_counts.plot(kind='bar', ax=axes[0], edgecolor='black')
    axes[0].set_xlabel(target_col)
    axes[0].set_ylabel('Count')
    axes[0].set_title('Class Distribution (Count)')
    axes[0].tick_params(axis='x', rotation=45)
    
    # Pie chart
    axes[1].pie(class_counts, labels=class_counts.index, autopct='%1.1f%%', startangle=90)
    axes[1].set_title('Class Distribution (Percentage)')
    
    # Imbalance ratio visualization
    axes[2].barh(['Imbalance Ratio'], [imbalance_ratio])
    axes[2].axvline(x=1.5, color='g', linestyle='--', label='Balanced')
    axes[2].axvline(x=3, color='y', linestyle='--', label='Slight')
    axes[2].axvline(x=10, color='r', linestyle='--', label='Severe')
    axes[2].set_xlabel('Ratio (Majority / Minority)')
    axes[2].set_title('Imbalance Severity')
    axes[2].legend()
    
    plt.tight_layout()
    plt.show()

# Usage
analyze_class_imbalance(df, 'target_class')
11. EDA for Different Data Types
11.1 Tabular Data (Structured)
Already covered in previous sections

11.2 Image Data
Python

import cv2
from PIL import Image

def analyze_image_dataset(image_paths):
    """Analyze image dataset"""
    
    print("="*60)
    print("IMAGE DATASET ANALYSIS")
    print("="*60)
    
    # Collect image properties
    widths, heights, channels, sizes = [], [], [], []
    
    for path in image_paths:
        img = Image.open(path)
        width, height = img.size
        widths.append(width)
        heights.append(height)
        
        # Convert to numpy array
        img_array = np.array(img)
        channels.append(img_array.shape[2] if len(img_array.shape) == 3 else 1)
        
        # File size
        import os
        sizes.append(os.path.getsize(path) / 1024)  # KB
    
    # Statistics
    print(f"\nNumber of images: {len(image_paths)}")
    print(f"\nDimensions:")
    print(f"   Width: min={min(widths)}, max={max(widths)}, avg={np.mean(widths):.1f}")
    print(f"   Height: min={min(heights)}, max={max(heights)}, avg={np.mean(heights):.1f}")
    print(f"\nChannels: {set(channels)}")
    print(f"\nFile sizes (KB): min={min(sizes):.1f}, max={max(sizes):.1f}, avg={np.mean(sizes):.1f}")
    
    # Visualizations
    fig, axes = plt.subplots(2, 2, figsize=(15, 12))
    
    # Width distribution
    axes[0, 0].hist(widths, bins=30, edgecolor='black')
    axes[0, 0].set_xlabel('Width (pixels)')
    axes[0, 0].set_ylabel('Frequency')
    axes[0, 0].set_title('Image Width Distribution')
    
    # Height distribution
    axes[0, 1].hist(heights, bins=30, edgecolor='black')
    axes[0, 1].set_xlabel('Height (pixels)')
    axes[0, 1].set_ylabel('Frequency')
    axes[0, 1].set_title('Image Height Distribution')
    
    # Aspect ratio
    aspect_ratios = np.array(widths) / np.array(heights)
    axes[1, 0].hist(aspect_ratios, bins=30, edgecolor='black')
    axes[1, 0].set_xlabel('Aspect Ratio (Width/Height)')
    axes[1, 0].set_ylabel('Frequency')
    axes[1, 0].set_title('Aspect Ratio Distribution')
    
    # File size
    axes[1, 1].hist(sizes, bins=30, edgecolor='black')
    axes[1, 1].set_xlabel('File Size (KB)')
    axes[1, 1].set_ylabel('Frequency')
    axes[1, 1].set_title('File Size Distribution')
    
    plt.tight_layout()
    plt.show()
    
    # Sample images
    fig, axes = plt.subplots(2, 5, figsize=(15, 6))
    for i, path in enumerate(image_paths[:10]):
        img = Image.open(path)
        axes[i//5, i%5].imshow(img)
        axes[i//5, i%5].axis('off')
        axes[i//5, i%5].set_title(f'{img.size[0]}×{img.size[1]}')
    plt.suptitle('Sample Images')
    plt.tight_layout()
    plt.show()

# Usage
# image_paths = glob.glob('images/*.jpg')
# analyze_image_dataset(image_paths)
11.3 Text Data
Python

def analyze_text_data(df, text_column):
    """Comprehensive text data analysis"""
    
    print("="*60)
    print(f"TEXT DATA ANALYSIS: {text_column}")
    print("="*60)
    
    # Basic statistics
    df['text_length'] = df[text_column].str.len()
    df['word_count'] = df[text_column].str.split().str.len()
    df['avg_word_length'] = df['text_length'] / df['word_count']
    
    print("\nBASIC STATISTICS:")
    print(f"   Total documents: {len(df)}")
    print(f"   Avg text length: {df['text_length'].mean():.1f} characters")
    print(f"   Avg word count: {df['word_count'].mean():.1f} words")
    print(f"   Avg word length: {df['avg_word_length'].mean():.1f} characters")
    
    # Word frequency
    from collections import Counter
    all_words = ' '.join(df[text_column]).lower().split()
    word_freq = Counter(all_words)
    most_common = word_freq.most_common(20)
    
    print("\nMOST COMMON WORDS:")
    for word, count in most_common[:10]:
        print(f"   {word}: {count}")
    
    # Visualizations
    fig, axes = plt.subplots(2, 3, figsize=(18, 10))
    
    # Text length distribution
    axes[0, 0].hist(df['text_length'], bins=30, edgecolor='black')
    axes[0, 0].set_xlabel('Text Length (characters)')
    axes[0, 0].set_ylabel('Frequency')
    axes[0, 0].set_title('Text Length Distribution')
    
    # Word count distribution
    axes[0, 1].hist(df['word_count'], bins=30, edgecolor='black')
    axes[0, 1].set_xlabel('Word Count')
    axes[0, 1].set_ylabel('Frequency')
    axes[0, 1].set_title('Word Count Distribution')
    
    # Average word length
    axes[0, 2].hist(df['avg_word_length'], bins=30, edgecolor='black')
    axes[0, 2].set_xlabel('Average Word Length')
    axes[0, 2].set_ylabel('Frequency')
    axes[0, 2].set_title('Avg Word Length Distribution')
    
    # Word frequency bar chart
    words, counts = zip(*most_common[:20])
    axes[1, 0].barh(range(len(words)), counts)
    axes[1, 0].set_yticks(range(len(words)))
    axes[1, 0].set_yticklabels(words)
    axes[1, 0].set_xlabel('Frequency')
    axes[1, 0].set_title('Top 20 Most Common Words')
    axes[1, 0].invert_yaxis()
    
    # Word cloud
    from wordcloud import WordCloud
    wordcloud = WordCloud(width=800, height=400, background_color='white').generate(' '.join(df[text_column]))
    axes[1, 1].imshow(wordcloud, interpolation='bilinear')
    axes[1, 1].axis('off')
    axes[1, 1].set_title('Word Cloud')
    
    # Sentiment distribution (if applicable)
    try:
        from textblob import TextBlob
        df['sentiment'] = df[text_column].apply(lambda x: TextBlob(str(x)).sentiment.polarity)
        axes[1, 2].hist(df['sentiment'], bins=30, edgecolor='black')
        axes[1, 2].set_xlabel('Sentiment Polarity')
        axes[1, 2].set_ylabel('Frequency')
        axes[1, 2].set_title('Sentiment Distribution')
        axes[1, 2].axvline(0, color='r', linestyle='--', label='Neutral')
        axes[1, 2].legend()
    except:
        axes[1, 2].text(0.5, 0.5, 'Sentiment analysis\nnot available', 
                       ha='center', va='center', transform=axes[1, 2].transAxes)
        axes[1, 2].axis('off')
    
    plt.tight_layout()
    plt.show()

# Usage
# analyze_text_data(df, 'description')
11.4 Geospatial Data
Python

def analyze_geospatial_data(df, lat_col='latitude', lon_col='longitude'):
    """Analyze geospatial data"""
    
    print("="*60)
    print("GEOSPATIAL DATA ANALYSIS")
    print("="*60)
    
    # Basic statistics
    print(f"\nCoordinate ranges:")
    print(f"   Latitude: {df[lat_col].min():.4f} to {df[lat_col].max():.4f}")
    print(f"   Longitude: {df[lon_col].min():.4f} to {df[lon_col].max():.4f}")
    
    # Calculate center
    center_lat = df[lat_col].mean()
    center_lon = df[lon_col].mean()
    print(f"\nCenter point: ({center_lat:.4f}, {center_lon:.4f})")
    
    # Visualizations
    fig, axes = plt.subplots(1, 2, figsize=(16, 6))
    
    # Scatter plot
    axes[0].scatter(df[lon_col], df[lat_col], alpha=0.5, s=20)
    axes[0].scatter(center_lon, center_lat, c='red', s=200, marker='*', 
                   label='Center', edgecolors='black', linewidths=2)
    axes[0].set_xlabel('Longitude')
    axes[0].set_ylabel('Latitude')
    axes[0].set_title('Geographical Distribution')
    axes[0].legend()
    axes[0].grid(True, alpha=0.3)
    
    # Heatmap (density)
    axes[1].hist2d(df[lon_col], df[lat_col], bins=50, cmap='YlOrRd')
    axes[1].set_xlabel('Longitude')
    axes[1].set_ylabel('Latitude')
    axes[1].set_title('Density Heatmap')
    plt.colorbar(axes[1].collections[0], ax=axes[1], label='Count')
    
    plt.tight_layout()
    plt.show()
    
    # Interactive map (if folium is available)
    try:
        import folium
        from folium.plugins import HeatMap
        
        # Create base map
        m = folium.Map(location=[center_lat, center_lon], zoom_start=10)
        
        # Add markers
        for idx, row in df.sample(min(100, len(df))).iterrows():
            folium.CircleMarker(
                location=[row[lat_col], row[lon_col]],
                radius=5,
                popup=f"Point {idx}",
                color='blue',
                fill=True,
                fillColor='blue'
            ).add_to(m)
        
        # Add heatmap
        heat_data = [[row[lat_col], row[lon_col]] for idx, row in df.iterrows()]
        HeatMap(heat_data).add_to(m)
        
        # Save and display
        m.save('geospatial_map.html')
        print("\n✓ Interactive map saved as 'geospatial_map.html'")
        
    except ImportError:
        print("\n⚠ Install folium for interactive maps: pip install folium")

# Usage
# analyze_geospatial_data(df, 'lat', 'lon')
12. Statistical Tests in EDA
12.1 Hypothesis Testing Framework
text

1. State hypotheses (H₀ and H₁)
2. Choose significance level (α, usually 0.05)
3. Select appropriate test
4. Calculate test statistic and p-value
5. Make decision:
   - If p < α: Reject H₀ (significant)
   - If p ≥ α: Fail to reject H₀ (not significant)
6. Interpret results in context
12.2 Common Statistical Tests
12.2.1 Comparison Tests
1. Independent t-test (two groups, numerical)

Python

from scipy.stats import ttest_ind

def independent_ttest(df, group_col, value_col, group1, group2):
    """Compare means of two independent groups"""
    
    data1 = df[df[group_col] == group1][value_col].dropna()
    data2 = df[df[group_col] == group2][value_col].dropna()
    
    # Test
    t_stat, p_value = ttest_ind(data1, data2)
    
    # Effect size (Cohen's d)
    mean_diff = data1.mean() - data2.mean()
    pooled_std = np.sqrt((data1.std()**2 + data2.std()**2) / 2)
    cohens_d = mean_diff / pooled_std
    
    print("INDEPENDENT T-TEST")
    print(f"{group1} mean: {data1.mean():.2f} ± {data1.std():.2f}")
    print(f"{group2} mean: {data2.mean():.2f} ± {data2.std():.2f}")
    print(f"Mean difference: {mean_diff:.2f}")
    print(f"T-statistic: {t_stat:.4f}")
    print(f"P-value: {p_value:.4f}")
    print(f"Cohen's d: {cohens_d:.4f}")
    
    if p_value < 0.05:
        print("→ Significant difference (p < 0.05)")
    else:
        print("→ No significant difference (p ≥ 0.05)")

# Usage
# independent_ttest(df, 'gender', 'salary', 'Male', 'Female')
2. Paired t-test (before-after comparison)

Python

from scipy.stats import ttest_rel

def paired_ttest(df, before_col, after_col):
    """Compare paired observations (e.g., before/after)"""
    
    data_before = df[before_col].dropna()
    data_after = df[after_col].dropna()
    
    # Ensure same length
    common_idx = data_before.index.intersection(data_after.index)
    data_before = data_before.loc[common_idx]
    data_after = data_after.loc[common_idx]
    
    # Test
    t_stat, p_value = ttest_rel(data_before, data_after)
    
    print("PAIRED T-TEST")
    print(f"Before mean: {data_before.mean():.2f} ± {data_before.std():.2f}")
    print(f"After mean: {data_after.mean():.2f} ± {data_after.std():.2f}")
    print(f"Mean change: {(data_after - data_before).mean():.2f}")
    print(f"T-statistic: {t_stat:.4f}")
    print(f"P-value: {p_value:.4f}")
    
    if p_value < 0.05:
        print("→ Significant change (p < 0.05)")
    else:
        print("→ No significant change (p ≥ 0.05)")

# Usage
# paired_ttest(df, 'score_before', 'score_after')
3. One-way ANOVA (3+ groups)

Python

from scipy.stats import f_oneway

def one_way_anova(df, group_col, value_col):
    """Compare means across multiple groups"""
    
    groups = [df[df[group_col] == g][value_col].dropna() 
              for g in df[group_col].unique()]
    
    # Test
    f_stat, p_value = f_oneway(*groups)
    
    print("ONE-WAY ANOVA")
    print(f"Groups: {df[group_col].unique()}")
    print(f"F-statistic: {f_stat:.4f}")
    print(f"P-value: {p_value:.4f}")
    
    if p_value < 0.05:
        print("→ At least one group differs significantly (p < 0.05)")
        
        # Post-hoc: Tukey's HSD
        from scipy.stats import tukey_hsd
        result = tukey_hsd(*groups)
        print("\nTukey's HSD post-hoc test:")
        print(result)
    else:
        print("→ No significant difference between groups (p ≥ 0.05)")

# Usage
# one_way_anova(df, 'department', 'salary')
12.2.2 Association Tests
1. Chi-square test (categorical vs categorical)

Python

from scipy.stats import chi2_contingency

def chi_square_test(df, col1, col2):
    """Test association between two categorical variables"""
    
    # Contingency table
    ct = pd.crosstab(df[col1], df[col2])
    
    # Test
    chi2, p_value, dof, expected = chi2_contingency(ct)
    
    # Cramér's V (effect size)
    n = ct.sum().sum()
    min_dim = min(ct.shape) - 1
    cramers_v = np.sqrt(chi2 / (n * min_dim))
    
    print("CHI-SQUARE TEST")
    print(f"\nContingency table:")
    print(ct)
    print(f"\nChi-square: {chi2:.4f}")
    print(f"P-value: {p_value:.4f}")
    print(f"Degrees of freedom: {dof}")
    print(f"Cramér's V: {cramers_v:.4f}")
    
    if p_value < 0.05:
        print("→ Significant association (p < 0.05)")
    else:
        print("→ No significant association (p ≥ 0.05)")

# Usage
# chi_square_test(df, 'department', 'gender')
2. Correlation test

Python

from scipy.stats import pearsonr, spearmanr

def correlation_test(df, col1, col2, method='pearson'):
    """Test correlation between two numerical variables"""
    
    data1 = df[col1].dropna()
    data2 = df[col2].dropna()
    
    # Align indices
    common_idx = data1.index.intersection(data2.index)
    data1 = data1.loc[common_idx]
    data2 = data2.loc[common_idx]
    
    # Test
    if method == 'pearson':
        corr, p_value = pearsonr(data1, data2)
        test_name = "Pearson"
    else:
        corr, p_value = spearmanr(data1, data2)
        test_name = "Spearman"
    
    print(f"{test_name.upper()} CORRELATION TEST")
    print(f"Correlation: {corr:.4f}")
    print(f"P-value: {p_value:.4f}")
    
    if p_value < 0.05:
        print("→ Significant correlation (p < 0.05)")
        if abs(corr) > 0.7:
            print(f"→ Strong {'positive' if corr > 0 else 'negative'} correlation")
        elif abs(corr) > 0.3:
            print(f"→ Moderate {'positive' if corr > 0 else 'negative'} correlation")
        else:
            print(f"→ Weak {'positive' if corr > 0 else 'negative'} correlation")
    else:
        print("→ No significant correlation (p ≥ 0.05)")

# Usage
# correlation_test(df, 'age', 'salary')
12.2.3 Normality Tests
Python

from scipy.stats import shapiro, normaltest, kstest

def normality_tests(data):
    """Multiple normality tests"""
    
    print("NORMALITY TESTS")
    
    # Shapiro-Wilk
    stat, p = shapiro(data)
    print(f"\n1. Shapiro-Wilk: statistic={stat:.4f}, p-value={p:.4f}")
    print(f"   → {'Normal' if p > 0.05 else 'NOT normal'}")
    
    # D'Agostino's K-squared
    stat, p = normaltest(data)
    print(f"\n2. D'Agostino's K²: statistic={stat:.4f}, p-value={p:.4f}")
    print(f"   → {'Normal' if p > 0.05 else 'NOT normal'}")
    
    # Kolmogorov-Smirnov
    stat, p = kstest(data, 'norm', args=(data.mean(), data.std()))
    print(f"\n3. Kolmogorov-Smirnov: statistic={stat:.4f}, p-value={p:.4f}")
    print(f"   → {'Normal' if p > 0.05 else 'NOT normal'}")

# Usage
# normality_tests(df['salary'].dropna())
13. EDA Best Practices and Checklist
13.1 EDA Workflow Checklist
Markdown

## 📋 COMPREHENSIVE EDA CHECKLIST

### 1. DATA LOADING & INITIAL INSPECTION
- [ ] Load data successfully
- [ ] Check data shape (rows × columns)
- [ ] Display first/last rows
- [ ] Check data types
- [ ] Identify target variable (if applicable)
- [ ] Estimate memory usage

### 2. DATA QUALITY ASSESSMENT
- [ ] Check for missing values
- [ ] Check for duplicates
- [ ] Identify data type mismatches
- [ ] Check for placeholder values (-999, 'NA', etc.)
- [ ] Validate data ranges (negative values where shouldn't be)
- [ ] Check for inconsistent formatting

### 3. UNIVARIATE ANALYSIS
**Numerical variables:**
- [ ] Calculate central tendency (mean, median, mode)
- [ ] Calculate spread (std, IQR, range)
- [ ] Calculate shape (skewness, kurtosis)
- [ ] Create histograms
- [ ] Create box plots
- [ ] Check for outliers
- [ ] Test for normality

**Categorical variables:**
- [ ] Calculate frequency distributions
- [ ] Check cardinality (number of unique values)
- [ ] Identify dominant categories
- [ ] Check for class imbalance
- [ ] Create bar charts
- [ ] Create pie charts (if appropriate)

### 4. BIVARIATE ANALYSIS
**Numerical vs Numerical:**
- [ ] Calculate correlations
- [ ] Create scatter plots
- [ ] Identify linear/non-linear relationships
- [ ] Check for multicollinearity

**Categorical vs Categorical:**
- [ ] Create contingency tables
- [ ] Perform chi-square tests
- [ ] Calculate Cramér's V
- [ ] Create stacked/grouped bar charts

**Numerical vs Categorical:**
- [ ] Calculate group statistics
- [ ] Create box plots by group
- [ ] Perform t-tests/ANOVA
- [ ] Calculate effect sizes

### 5. MULTIVARIATE ANALYSIS
- [ ] Create correlation matrix
- [ ] Create pair plots
- [ ] Perform PCA (if needed)
- [ ] Identify interaction effects
- [ ] Check for multicollinearity

### 6. FEATURE ENGINEERING
- [ ] Create derived features
- [ ] Encode categorical variables
- [ ] Scale numerical features
- [ ] Handle imbalanced data
- [ ] Create interaction terms

### 7. DOMAIN-SPECIFIC ANALYSIS
- [ ] Validate business rules
- [ ] Check temporal patterns (if time series)
- [ ] Verify geographical patterns (if spatial)
- [ ] Consult domain experts

### 8. DOCUMENTATION
- [ ] Document all findings
- [ ] List data quality issues
- [ ] Recommend preprocessing steps
- [ ] Suggest feature engineering ideas
- [ ] Identify potential model challenges

### 9. VISUALIZATION
- [ ] All charts have titles
- [ ] All axes are labeled
- [ ] Legends are included (where needed)
- [ ] Colors are meaningful
- [ ] Plots are easy to interpret

### 10. FINAL REVIEW
- [ ] All hypotheses tested
- [ ] All assumptions verified
- [ ] Ready for modeling
- [ ] EDA report prepared
13.2 Common EDA Mistakes to Avoid
Python

"""
❌ COMMON EDA MISTAKES

1. NOT CHECKING DATA QUALITY FIRST
   - Always check missing values, duplicates, types BEFORE analysis
   
2. IGNORING OUTLIERS
   - Don't just remove - understand WHY they exist
   
3. CONFUSING CORRELATION WITH CAUSATION
   - High correlation ≠ causal relationship
   
4. USING MEAN FOR SKEWED DATA
   - Use median for skewed distributions
   
5. FORGETTING ABOUT MULTICOLLINEARITY
   - Check correlations between features
   
6. NOT VISUALIZING DATA
   - Numbers alone can be misleading
   
7. OVERFITTING EDA TO TRAINING DATA
   - Validate findings on test/validation set
   
8. IGNORING DOMAIN KNOWLEDGE
   - Context is crucial for interpretation
   
9. NOT DOCUMENTING FINDINGS
   - Keep detailed notes of discoveries
   
10. RUSHING TO MODELING
    - Thorough EDA prevents future headaches
"""
13.3 EDA Report Template
Python

def generate_eda_report(df, target_col=None):
    """Generate comprehensive EDA report"""
    
    report = f"""
# EXPLORATORY DATA ANALYSIS REPORT
Generated: {pd.Timestamp.now().strftime('%Y-%m-%d %H:%M:%S')}

## 1. DATASET OVERVIEW

- **Shape:** {df.shape[0]} rows × {df.shape[1]} columns
- **Memory Usage:** {df.memory_usage(deep=True).sum() / 1024**2:.2f} MB
- **Duplicate Rows:** {df.duplicated().sum()} ({df.duplicated().sum()/len(df)*100:.2f}%)
- **Target Variable:** {target_col if target_col else 'N/A'}

## 2. VARIABLE SUMMARY

**Numerical Variables ({len(df.select_dtypes(include=[np.number]).columns)}):**
{', '.join(df.select_dtypes(include=[np.number]).columns)}

**Categorical Variables ({len(df.select_dtypes(include=['object', 'category']).columns)}):**
{', '.join(df.select_dtypes(include=['object', 'category']).columns)}

## 3. DATA QUALITY

### Missing Values:
{df.isnull().sum()[df.isnull().sum() > 0].to_string() if df.isnull().sum().sum() > 0 else 'No missing values'}

### Data Type Issues:
{df.dtypes.to_string()}

## 4. KEY FINDINGS

### Numerical Variables:
"""
    
    # Add numerical variable summaries
    for col in df.select_dtypes(include=[np.number]).columns:
        report += f"\n**{col}:**\n"
        report += f"- Mean: {df[col].mean():.2f}, Median: {df[col].median():.2f}\n"
        report += f"- Std: {df[col].std():.2f}, Range: [{df[col].min():.2f}, {df[col].max():.2f}]\n"
        
        # Check skewness
        skewness = df[col].skew()
        if abs(skewness) > 1:
            report += f"- ⚠ Highly skewed (skewness: {skewness:.2f})\n"
        
        # Check outliers
        Q1, Q3 = df[col].quantile([0.25, 0.75])
        IQR = Q3 - Q1
        outliers = df[(df[col] < Q1 - 1.5*IQR) | (df[col] > Q3 + 1.5*IQR)]
        if len(outliers) > 0:
            report += f"- ⚠ {len(outliers)} outliers detected ({len(outliers)/len(df)*100:.2f}%)\n"
    
    report += "\n### Categorical Variables:\n"
    
    # Add categorical variable summaries
    for col in df.select_dtypes(include=['object', 'category']).columns:
        report += f"\n**{col}:**\n"
        report += f"- Unique values: {df[col].nunique()}\n"
        report += f"- Most common: {df[col].mode()[0]} ({df[col].value_counts().iloc[0]} occurrences)\n"
        
        # Check cardinality
        unique_ratio = df[col].nunique() / len(df)
        if unique_ratio > 0.9:
            report += f"- ⚠ High cardinality (unique ratio: {unique_ratio:.2%})\n"
        
        # Check imbalance
        if df[col].nunique() < 20:
            imbalance = df[col].value_counts().iloc[0] / df[col].value_counts().iloc[-1]
            if imbalance > 10:
                report += f"- ⚠ Severe class imbalance (ratio: {imbalance:.1f})\n"
    
    report += """
## 5. RECOMMENDATIONS

### Data Cleaning:
"""
    
    # Recommendations
    if df.isnull().sum().sum() > 0:
        report += "- Handle missing values (imputation or removal)\n"
    
    if df.duplicated().sum() > 0:
        report += "- Remove duplicate rows\n"
    
    # Check for high-cardinality categoricals
    high_card_cols = [col for col in df.select_dtypes(include=['object', 'category']).columns
                     if df[col].nunique() / len(df) > 0.5]
    if high_card_cols:
        report += f"- Consider dropping high-cardinality columns: {', '.join(high_card_cols)}\n"
    
    report += """
### Feature Engineering:
- Create derived features from existing variables
- Encode categorical variables appropriately
- Scale numerical features for modeling
- Consider interaction terms

### Modeling Considerations:
"""
    
    # Modeling recommendations based on findings
    skewed_cols = [col for col in df.select_dtypes(include=[np.number]).columns
                   if abs(df[col].skew()) > 1]
    if skewed_cols:
        report += f"- Apply transformations to skewed features: {', '.join(skewed_cols)}\n"
    
    # Check for multicollinearity
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    if len(numerical_cols) > 1:
        corr_matrix = df[numerical_cols].corr().abs()
        high_corr = (corr_matrix > 0.9) & (corr_matrix < 1.0)
        if high_corr.sum().sum() > 0:
            report += "- Address multicollinearity (highly correlated features detected)\n"
    
    if target_col and target_col in df.columns:
        if df[target_col].dtype in ['object', 'category']:
            # Classification
            imbalance = df[target_col].value_counts().iloc[0] / df[target_col].value_counts().iloc[-1]
            if imbalance > 3:
                report += "- Handle class imbalance (use SMOTE, class weights, or resampling)\n"
    
    report += "\n---\nEnd of Report\n"
    
    return report

# Usage
# report = generate_eda_report(df, target_col='target')
# print(report)
# 
# # Save to file
# with open('eda_report.md', 'w') as f:
#     f.write(report)
14. Real-World Case Studies
14.1 Case Study 1: Customer Churn Analysis
Python

"""
SCENARIO: Telecom company wants to predict customer churn

BUSINESS QUESTIONS:
1. What factors influence churn?
2. Can we identify high-risk customers?
3. What actions can reduce churn?
"""

def customer_churn_eda(df):
    """EDA for customer churn dataset"""
    
    print("="*70)
    print("CUSTOMER CHURN ANALYSIS")
    print("="*70)
    
    # 1. Data Overview
    print("\n1. DATASET OVERVIEW")
    print(f"   Total customers: {len(df)}")
    print(f"   Churned customers: {df['Churn'].sum()} ({df['Churn'].mean()*100:.1f}%)")
    print(f"   Retained customers: {(~df['Churn']).sum()} ({(~df['Churn']).mean()*100:.1f}%)")
    
    # 2. Churn rate by categorical features
    print("\n2. CHURN RATE BY CATEGORIES")
    categorical_features = ['Contract', 'PaymentMethod', 'InternetService']
    
    for feature in categorical_features:
        if feature in df.columns:
            churn_rate = df.groupby(feature)['Churn'].mean().sort_values(ascending=False)
            print(f"\n{feature}:")
            for cat, rate in churn_rate.items():
                print(f"   {cat}: {rate*100:.1f}%")
    
    # 3. Numerical features analysis
    print("\n3. NUMERICAL FEATURES COMPARISON")
    numerical_features = ['tenure', 'MonthlyCharges', 'TotalCharges']
    
    for feature in numerical_features:
        if feature in df.columns:
            churned_mean = df[df['Churn'] == True][feature].mean()
            retained_mean = df[df['Churn'] == False][feature].mean()
            print(f"\n{feature}:")
            print(f"   Churned avg: {churned_mean:.2f}")
            print(f"   Retained avg: {retained_mean:.2f}")
            print(f"   Difference: {churned_mean - retained_mean:.2f}")
    
    # 4. Visualizations
    fig, axes = plt.subplots(2, 3, figsize=(18, 10))
    
    # Churn distribution
    df['Churn'].value_counts().plot(kind='pie', ax=axes[0, 0], autopct='%1.1f%%')
    axes[0, 0].set_title('Churn Distribution')
    axes[0, 0].set_ylabel('')
    
    # Tenure distribution by churn
    df.boxplot(column='tenure', by='Churn', ax=axes[0, 1])
    axes[0, 1].set_title('Tenure by Churn Status')
    axes[0, 1].set_xlabel('Churned')
    
    # Monthly charges by churn
    df.boxplot(column='MonthlyCharges', by='Churn', ax=axes[0, 2])
    axes[0, 2].set_title('Monthly Charges by Churn')
    axes[0, 2].set_xlabel('Churned')
    
    # Churn by contract type
    ct = pd.crosstab(df['Contract'], df['Churn'], normalize='index')
    ct.plot(kind='bar', stacked=True, ax=axes[1, 0])
    axes[1, 0].set_title('Churn Rate by Contract Type')
    axes[1, 0].set_xlabel('Contract Type')
    axes[1, 0].set_ylabel('Proportion')
    axes[1, 0].legend(['Retained', 'Churned'])
    
    # Churn by payment method
    ct = pd.crosstab(df['PaymentMethod'], df['Churn'], normalize='index')
    ct.plot(kind='bar', stacked=True, ax=axes[1, 1])
    axes[1, 1].set_title('Churn Rate by Payment Method')
    axes[1, 1].set_xlabel('Payment Method')
    axes[1, 1].tick_params(axis='x', rotation=45)
    axes[1, 1].legend(['Retained', 'Churned'])
    
    # Correlation heatmap
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    corr_matrix = df[numerical_cols].corr()
    sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', ax=axes[1, 2])
    axes[1, 2].set_title('Feature Correlations')
    
    plt.tight_layout()
    plt.show()
    
    # 5. Key Insights
    print("\n5. KEY INSIGHTS:")
    
    # Contract type insight
    month_to_month_churn = df[df['Contract'] == 'Month-to-month']['Churn'].mean()
    if month_to_month_churn > 0.3:
        print(f"   ⚠ Month-to-month customers have {month_to_month_churn*100:.1f}% churn rate")
        print("   → Recommend: Incentivize longer contracts")
    
    # Tenure insight
    short_tenure_churn = df[df['tenure'] < 12]['Churn'].mean()
    long_tenure_churn = df[df['tenure'] >= 12]['Churn'].mean()
    if short_tenure_churn > long_tenure_churn * 2:
        print(f"   ⚠ New customers (<1 year) churn at {short_tenure_churn*100:.1f}%")
        print("   → Recommend: Focus on first-year retention programs")
    
    # Monthly charges insight
    high_charge_churn = df[df['MonthlyCharges'] > df['MonthlyCharges'].median()]['Churn'].mean()
    low_charge_churn = df[df['MonthlyCharges'] <= df['MonthlyCharges'].median()]['Churn'].mean()
    if high_charge_churn > low_charge_churn:
        print(f"   ⚠ High-paying customers churn more ({high_charge_churn*100:.1f}% vs {low_charge_churn*100:.1f}%)")
        print("   → Recommend: Review pricing strategy")

# Example usage:
# churn_df = pd.read_csv('telecom_churn.csv')
# customer_churn_eda(churn_df)
14.2 Case Study 2: Sales Forecasting
Python

"""
SCENARIO: Retail company wants to forecast sales

BUSINESS QUESTIONS:
1. What are sales trends over time?
2. Are there seasonal patterns?
3. Which products drive sales?
4. What external factors affect sales?
"""

def sales_forecasting_eda(df, date_col='Date', sales_col='Sales'):
    """EDA for sales forecasting"""
    
    # Ensure datetime
    df[date_col] = pd.to_datetime(df[date_col])
    df = df.sort_values(date_col)
    
    print("="*70)
    print("SALES FORECASTING ANALYSIS")
    print("="*70)
    
    # 1. Time series overview
    print("\n1. TIME SERIES OVERVIEW")
    print(f"   Date range: {df[date_col].min().date()} to {df[date_col].max().date()}")
    print(f"   Total periods: {len(df)}")
    print(f"   Average sales: ${df[sales_col].mean():,.2f}")
    print(f"   Total sales: ${df[sales_col].sum():,.2f}")
    
    # 2. Trend analysis
    print("\n2. TREND ANALYSIS")
    from scipy.stats import linregress
    x = np.arange(len(df))
    slope, intercept, r_value, p_value, std_err = linregress(x, df[sales_col])
    
    growth_rate = (slope * len(df) / df[sales_col].mean()) * 100
    print(f"   Overall trend: {'Upward' if slope > 0 else 'Downward'}")
    print(f"   Growth rate: {growth_rate:.2f}% over period")
    print(f"   R-squared: {r_value**2:.3f}")
    
    # 3. Seasonality
    print("\n3. SEASONALITY ANALYSIS")
    df['Month'] = df[date_col].dt.month
    df['DayOfWeek'] = df[date_col].dt.dayofweek
    df['Quarter'] = df[date_col].dt.quarter
    
    # Monthly pattern
    monthly_avg = df.groupby('Month')[sales_col].mean()
    peak_month = monthly_avg.idxmax()
    low_month = monthly_avg.idxmin()
    seasonality = (monthly_avg.max() - monthly_avg.min()) / monthly_avg.mean()
    
    print(f"   Peak month: {peak_month} (${monthly_avg.max():,.2f})")
    print(f"   Lowest month: {low_month} (${monthly_avg.min():,.2f})")
    print(f"   Seasonality strength: {seasonality:.2%}")
    
    # Day of week pattern
    dow_avg = df.groupby('DayOfWeek')[sales_col].mean()
    dow_names = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    print(f"\n   Average by day:")
    for day, avg in zip(dow_names, dow_avg):
        print(f"      {day}: ${avg:,.2f}")
    
    # 4. Visualizations
    fig = plt.figure(figsize=(18, 12))
    gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)
    
    # Time series plot
    ax1 = fig.add_subplot(gs[0, :])
    ax1.plot(df[date_col], df[sales_col], alpha=0.7, label='Actual')
    ax1.plot(df[date_col], slope * x + intercept, 'r--', label='Trend', linewidth=2)
    ax1.set_xlabel('Date')
    ax1.set_ylabel('Sales ($)')
    ax1.set_title('Sales Over Time with Trend')
    ax1.legend()
    ax1.grid(True, alpha=0.3)
    
    # Moving average
    ax2 = fig.add_subplot(gs[1, 0])
    df['MA_7'] = df[sales_col].rolling(window=7).mean()
    df['MA_30'] = df[sales_col].rolling(window=30).mean()
    ax2.plot(df[date_col], df[sales_col], alpha=0.3, label='Daily')
    ax2.plot(df[date_col], df['MA_7'], label='7-day MA')
    ax2.plot(df[date_col], df['MA_30'], label='30-day MA')
    ax2.set_xlabel('Date')
    ax2.set_ylabel('Sales ($)')
    ax2.set_title('Moving Averages')
    ax2.legend()
    ax2.grid(True, alpha=0.3)
    
    # Monthly seasonality
    ax3 = fig.add_subplot(gs[1, 1])
    monthly_avg.plot(kind='bar', ax=ax3)
    ax3.set_xlabel('Month')
    ax3.set_ylabel('Average Sales ($)')
    ax3.set_title('Monthly Seasonality')
    ax3.tick_params(axis='x', rotation=0)
    ax3.grid(True, alpha=0.3)
    
    # Day of week pattern
    ax4 = fig.add_subplot(gs[1, 2])
    ax4.bar(dow_names, dow_avg.values)
    ax4.set_xlabel('Day of Week')
    ax4.set_ylabel('Average Sales ($)')
    ax4.set_title('Day of Week Pattern')
    ax4.grid(True, alpha=0.3)
    
    # Distribution
    ax5 = fig.add_subplot(gs[2, 0])
    ax5.hist(df[sales_col], bins=50, edgecolor='black')
    ax5.axvline(df[sales_col].mean(), color='r', linestyle='--', label='Mean')
    ax5.axvline(df[sales_col].median(), color='g', linestyle='--', label='Median')
    ax5.set_xlabel('Sales ($)')
    ax5.set_ylabel('Frequency')
    ax5.set_title('Sales Distribution')
    ax5.legend()
    ax5.grid(True, alpha=0.3)
    
    # Box plot by quarter
    ax6 = fig.add_subplot(gs[2, 1])
    df.boxplot(column=sales_col, by='Quarter', ax=ax6)
    ax6.set_xlabel('Quarter')
    ax6.set_ylabel('Sales ($)')
    ax6.set_title('Sales by Quarter')
    plt.sca(ax6)
    plt.xticks(rotation=0)
    
    # Autocorrelation
    ax7 = fig.add_subplot(gs[2, 2])
    from pandas.plotting import autocorrelation_plot
    autocorrelation_plot(df[sales_col], ax=ax7)
    ax7.set_title('Autocorrelation')
    
    plt.show()
    
    # 5. Recommendations
    print("\n5. RECOMMENDATIONS:")
    
    if seasonality > 0.2:
        print("   📊 Strong seasonality detected")
        print("   → Use seasonal models (SARIMA, Prophet)")
        print(f"   → Stock up for peak month ({peak_month})")
    
    if growth_rate > 5:
        print("   📈 Positive growth trend")
        print("   → Expect continued growth")
    elif growth_rate < -5:
        print("   📉 Negative growth trend")
        print("   → Investigate causes, take corrective action")
    
    # Check for outliers
    Q1, Q3 = df[sales_col].quantile([0.25, 0.75])
    IQR = Q3 - Q1
    outliers = df[(df[sales_col] < Q1 - 1.5*IQR) | (df[sales_col] > Q3 + 1.5*IQR)]
    
    if len(outliers) > 0:
        print(f"   ⚠ {len(outliers)} outlier days detected")
        print("   → Investigate special events (promotions, holidays)")

# Example usage:
# sales_df = pd.read_csv('daily_sales.csv')
# sales_forecasting_eda(sales_df, 'Date', 'Sales')
14.3 Complete EDA Template
Python

def complete_eda(df, target_col=None):
    """
    Master EDA function - runs complete analysis
    
    Parameters:
    -----------
    df : pandas DataFrame
        Input dataset
    target_col : str, optional
        Target variable name (for supervised learning)
    """
    
    print("="*80)
    print(" "*25 + "COMPLETE EDA ANALYSIS")
    print("="*80)
    
    # ============================================================
    # SECTION 1: DATA OVERVIEW
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 1: DATA OVERVIEW")
    print("="*80)
    
    print(f"\nDataset shape: {df.shape[0]} rows × {df.shape[1]} columns")
    print(f"Memory usage: {df.memory_usage(deep=True).sum() / 1024**2:.2f} MB")
    print(f"\nFirst 5 rows:")
    print(df.head())
    
    print(f"\nData types:")
    print(df.dtypes.value_counts())
    
    print(f"\nColumn list:")
    for i, col in enumerate(df.columns, 1):
        print(f"{i:3d}. {col} ({df[col].dtype})")
    
    # ============================================================
    # SECTION 2: DATA QUALITY
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 2: DATA QUALITY")
    print("="*80)
    
    # Missing values
    missing = df.isnull().sum()
    if missing.sum() > 0:
        print("\nMissing values:")
        missing_df = pd.DataFrame({
            'Column': missing[missing > 0].index,
            'Missing': missing[missing > 0].values,
            'Percentage': (missing[missing > 0] / len(df) * 100).round(2)
        }).sort_values('Missing', ascending=False)
        print(missing_df.to_string(index=False))
    else:
        print("\n✓ No missing values")
    
    # Duplicates
    dup_count = df.duplicated().sum()
    if dup_count > 0:
        print(f"\n⚠ {dup_count} duplicate rows ({dup_count/len(df)*100:.2f}%)")
    else:
        print("\n✓ No duplicate rows")
    
    # ============================================================
    # SECTION 3: UNIVARIATE ANALYSIS - NUMERICAL
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 3: UNIVARIATE ANALYSIS - NUMERICAL VARIABLES")
    print("="*80)
    
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    print(f"\nNumerical columns ({len(numerical_cols)}): {list(numerical_cols)}")
    
    if len(numerical_cols) > 0:
        print("\nStatistical summary:")
        print(df[numerical_cols].describe().T)
        
        # Skewness and kurtosis
        print("\nShape metrics:")
        shape_df = pd.DataFrame({
            'Skewness': df[numerical_cols].skew(),
            'Kurtosis': df[numerical_cols].kurtosis()
        }).round(2)
        print(shape_df)
        
        # Visualizations
        n_cols = len(numerical_cols)
        n_rows = (n_cols + 2) // 3
        
        fig, axes = plt.subplots(n_rows, 3, figsize=(18, 5*n_rows))
        axes = axes.flatten() if n_cols > 1 else [axes]
        
        for i, col in enumerate(numerical_cols):
            axes[i].hist(df[col].dropna(), bins=30, edgecolor='black')
            axes[i].set_xlabel(col)
            axes[i].set_ylabel('Frequency')
            axes[i].set_title(f'Distribution of {col}')
            axes[i].grid(True, alpha=0.3)
        
        # Hide empty subplots
        for j in range(i+1, len(axes)):
            axes[j].axis('off')
        
        plt.tight_layout()
        plt.show()
    
    # ============================================================
    # SECTION 4: UNIVARIATE ANALYSIS - CATEGORICAL
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 4: UNIVARIATE ANALYSIS - CATEGORICAL VARIABLES")
    print("="*80)
    
    categorical_cols = df.select_dtypes(include=['object', 'category']).columns
    print(f"\nCategorical columns ({len(categorical_cols)}): {list(categorical_cols)}")
    
    if len(categorical_cols) > 0:
        for col in categorical_cols:
            print(f"\n{col}:")
            print(f"  Unique values: {df[col].nunique()}")
            print(f"  Most common: {df[col].mode()[0] if len(df[col].mode()) > 0 else 'N/A'}")
            
            # Top 10 values
            top10 = df[col].value_counts().head(10)
            print(f"  Top 10 values:")
            for val, count in top10.items():
                pct = count / len(df) * 100
                print(f"    {val}: {count} ({pct:.1f}%)")
        
        # Visualizations
        n_cols_cat = min(len(categorical_cols), 6)  # Limit to 6 for visualization
        fig, axes = plt.subplots(2, 3, figsize=(18, 10))
        axes = axes.flatten()
        
        for i, col in enumerate(categorical_cols[:6]):
            df[col].value_counts().head(10).plot(kind='bar', ax=axes[i], edgecolor='black')
            axes[i].set_xlabel('')
            axes[i].set_ylabel('Count')
            axes[i].set_title(f'Top 10 - {col}')
            axes[i].tick_params(axis='x', rotation=45)
        
        # Hide empty subplots
        for j in range(i+1, 6):
            axes[j].axis('off')
        
        plt.tight_layout()
        plt.show()
    
    # ============================================================
    # SECTION 5: BIVARIATE ANALYSIS
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 5: BIVARIATE ANALYSIS")
    print("="*80)
    
    if len(numerical_cols) > 1:
        # Correlation matrix
        print("\nCorrelation matrix:")
        corr_matrix = df[numerical_cols].corr()
        print(corr_matrix.round(2))
        
        # Heatmap
        plt.figure(figsize=(12, 10))
        sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', center=0,
                   square=True, linewidths=1, cbar_kws={"shrink": 0.8})
        plt.title('Correlation Matrix')
        plt.tight_layout()
        plt.show()
        
        # Pair plot (if not too many columns)
        if len(numerical_cols) <= 5:
            sns.pairplot(df[numerical_cols])
            plt.suptitle('Pair Plot', y=1.01)
            plt.show()
    
    # Target analysis (if provided)
    if target_col and target_col in df.columns:
        print(f"\n" + "="*80)
        print(f"TARGET VARIABLE ANALYSIS: {target_col}")
        print("="*80)
        
        if df[target_col].dtype in ['int64', 'float64']:
            # Numerical target (regression)
            print("\nTarget statistics:")
            print(df[target_col].describe())
            
            # Plot target distribution
            plt.figure(figsize=(12, 5))
            
            plt.subplot(1, 2, 1)
            plt.hist(df[target_col].dropna(), bins=50, edgecolor='black')
            plt.xlabel(target_col)
            plt.ylabel('Frequency')
            plt.title(f'Distribution of {target_col}')
            
            plt.subplot(1, 2, 2)
            plt.boxplot(df[target_col].dropna())
            plt.ylabel(target_col)
            plt.title(f'Box Plot of {target_col}')
            
            plt.tight_layout()
            plt.show()
            
        else:
            # Categorical target (classification)
            print("\nTarget distribution:")
            target_counts = df[target_col].value_counts()
            print(target_counts)
            print(f"\nPercentages:")
            print((target_counts / len(df) * 100).round(2))
            
            # Check imbalance
            if len(target_counts) > 1:
                imbalance = target_counts.max() / target_counts.min()
                print(f"\nImbalance ratio: {imbalance:.2f}")
                if imbalance > 10:
                    print("⚠ Severe class imbalance detected!")
            
            # Plot
            fig, axes = plt.subplots(1, 2, figsize=(12, 5))
            
            target_counts.plot(kind='bar', ax=axes[0], edgecolor='black')
            axes[0].set_xlabel(target_col)
            axes[0].set_ylabel('Count')
            axes[0].set_title('Target Distribution')
            axes[0].tick_params(axis='x', rotation=45)
            
            axes[1].pie(target_counts, labels=target_counts.index, autopct='%1.1f%%')
            axes[1].set_title('Target Distribution (%)')
            
            plt.tight_layout()
            plt.show()
    
    # ============================================================
    # SECTION 6: RECOMMENDATIONS
    # ============================================================
    print("\n" + "="*80)
    print("SECTION 6: RECOMMENDATIONS")
    print("="*80)
    
    recommendations = []
    
    # Missing values
    if df.isnull().sum().sum() > 0:
        high_missing = missing[missing / len(df) > 0.5]
        if len(high_missing) > 0:
            recommendations.append(f"❗ Consider dropping columns with >50% missing: {list(high_missing.index)}")
        else:
            recommendations.append("📋 Implement imputation strategy for missing values")
    
    # Duplicates
    if dup_count > 0:
        recommendations.append("🔄 Remove duplicate rows")
    
    # High cardinality categoricals
    high_card = [col for col in categorical_cols 
                if df[col].nunique() / len(df) > 0.5]
    if high_card:
        recommendations.append(f"🏷️  High cardinality columns may need special encoding: {high_card}")
    
    # Skewed features
    highly_skewed = [col for col in numerical_cols 
                    if abs(df[col].skew()) > 2]
    if highly_skewed:
        recommendations.append(f"📊 Apply transformations to highly skewed features: {highly_skewed}")
    
    # Multicollinearity
    if len(numerical_cols) > 1:
        high_corr_pairs = []
        for i in range(len(corr_matrix.columns)):
            for j in range(i+1, len(corr_matrix.columns)):
                if abs(corr_matrix.iloc[i, j]) > 0.9:
                    high_corr_pairs.append((corr_matrix.columns[i], corr_matrix.columns[j]))
        if high_corr_pairs:
            recommendations.append(f"⚠️  Address multicollinearity: {high_corr_pairs}")
    
    # Class imbalance
    if target_col and target_col in df.columns and df[target_col].dtype not in ['int64', 'float64']:
        target_counts = df[target_col].value_counts()
        if len(target_counts) > 1 and target_counts.max() / target_counts.min() > 5:
            recommendations.append("⚖️  Handle class imbalance (SMOTE, class weights, or resampling)")
    
    # Print recommendations
    if recommendations:
        for i, rec in enumerate(recommendations, 1):
            print(f"\n{i}. {rec}")
    else:
        print("\n✅ Data looks good! Ready for modeling.")
    
    print("\n" + "="*80)
    print("EDA COMPLETE!")
    print("="*80)

# Usage example:
# complete_eda(df, target_col='target')
Conclusion
Congratulations! 🎉 You've completed this comprehensive guide to Exploratory Data Analysis.

Key Takeaways:
EDA is Essential: 80% of ML success depends on data understanding
Be Systematic: Follow a structured workflow
Visualize Everything: A picture is worth a thousand numbers
Question Assumptions: Always validate your hypotheses
Document Findings: Keep detailed notes for reproducibility
Domain Knowledge: Context is crucial for interpretation
Iterate: EDA is not a one-time activity
Your EDA Journey:
text

Beginner → Intermediate → Advanced → Expert
   ↓            ↓             ↓          ↓
Learn      Practice      Analyze    Innovate
Basics     Techniques    Complex    Create New
                         Data       Methods
Next Steps:
Practice: Apply EDA on diverse datasets (Kaggle, UCI ML Repository)
Build Portfolio: Document your analyses on GitHub
Learn ML Models: Apply insights from EDA to build better models
Read Papers: Study how researchers perform EDA
Join Community: Participate in data science forums and competitions
Resources for Continued Learning:
Books: "Python for Data Analysis" by Wes McKinney
Courses: Fast.ai, Coursera Data Science Specialization
Practice: Kaggle Learn, DataCamp
Community: Stack Overflow, Reddit r/datascience
Remember:

"The purpose of visualization is insight, not pictures." - Ben Shneiderman

"Torture the data, and it will confess to anything." - Ronald Coase (Be ethical!)

Happy Analyzing! 📊🔍✨