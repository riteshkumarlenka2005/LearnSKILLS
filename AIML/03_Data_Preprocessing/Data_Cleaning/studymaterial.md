Data Cleaning: From Absolute Beginner to Advanced Expert
A Complete Guide for Machine Learning Practitioners

Table of Contents
Introduction to Data Cleaning
Understanding Data Quality
Setting Up Your Environment
Data Exploration Basics
Handling Missing Data
Dealing with Duplicates
Data Type Conversions
Handling Outliers
Text Data Cleaning
Date and Time Data Cleaning
Data Consistency and Standardization
Feature Engineering During Cleaning
Advanced Techniques
Automation and Pipelines
Best Practices and Common Pitfalls
1. Introduction to Data Cleaning
1.1 What is Data Cleaning?
Simple Definition: Data cleaning is the process of detecting and correcting (or removing) corrupt, inaccurate, or irrelevant records from a dataset.

Real-World Analogy: Think of data cleaning like preparing vegetables before cooking:

You wash them (remove noise)
Remove rotten parts (handle missing values)
Cut them uniformly (standardize format)
Remove duplicates (if you accidentally picked two identical items)
1.2 Why is Data Cleaning Critical for Machine Learning?
The Golden Rule: "Garbage In, Garbage Out" (GIGO)

Impact on ML Models:
text

Clean Data → Accurate Model → Reliable Predictions
Dirty Data → Biased Model → Unreliable Predictions
Real Statistics:

Data scientists spend 60-80% of their time on data cleaning
Poor data quality costs businesses $3.1 trillion annually in the US alone
Clean data can improve model accuracy by 20-50%
1.3 Common Data Quality Issues
Issue	Example	Impact
Missing Values	Age: 25, 30, ?, 45	Model can't process "?"
Duplicates	Same customer appears twice	Biased statistics
Inconsistent Format	"USA", "US", "United States"	Treated as different categories
Outliers	Salaries: 50k, 55k, 60k, 5M	Skews statistical measures
Wrong Data Types	Price stored as text: "$100"	Can't perform calculations
Typos	"Fem ale" instead of "Female"	Creates false categories
2. Understanding Data Quality
2.1 The Six Dimensions of Data Quality
1. Accuracy
Definition: Data correctly represents the real-world entity
Example: Customer's email is actually their email (not phone number)
2. Completeness
Definition: All required data is present
Example: Every customer record has name, email, and purchase date
3. Consistency
Definition: Data doesn't contradict itself
Example: Date of birth and age match each other
4. Timeliness
Definition: Data is up-to-date
Example: Current address, not one from 5 years ago
5. Validity
Definition: Data conforms to defined formats and rules
Example: Email has "@" symbol, age is positive number
6. Uniqueness
Definition: No unwanted duplication
Example: Each customer appears only once
2.2 Types of Data Issues
Structural Issues
text

Problem: Column headers are inconsistent
Before: "customer_name", "CustomerAge", "CUSTOMER EMAIL"
After: "customer_name", "customer_age", "customer_email"
Content Issues
text

Problem: Data values are incorrect
Before: Age = -5, Email = "not@provided", Date = "99/99/9999"
After: Age = 25, Email = NULL, Date = NULL or valid date
Semantic Issues
text

Problem: Data doesn't make logical sense
Before: Start_Date: 2023-01-15, End_Date: 2020-05-10
(End date before start date)
After: Corrected or flagged for review
3. Setting Up Your Environment
3.1 Essential Libraries
Python Setup
Python

# Install required libraries (run in terminal/command prompt)
# pip install pandas numpy matplotlib seaborn scikit-learn

# Import essential libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime
import warnings
warnings.filterwarnings('ignore')

# Display settings for better visibility
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', 100)
pd.set_option('display.width', 1000)
Why Each Library?
Library	Purpose	When to Use
pandas	Data manipulation	Always - your primary tool
numpy	Numerical operations	Mathematical calculations, array operations
matplotlib	Visualization	Basic plots, custom visualizations
seaborn	Statistical visualization	Beautiful statistical plots quickly
scikit-learn	ML preprocessing	Scaling, encoding, imputation
3.2 Understanding Your Workspace
Python

# Create a standard project structure
"""
project/
│
├── data/
│   ├── raw/              # Original, immutable data
│   ├── interim/          # Intermediate transformed data
│   └── processed/        # Final, clean data
│
├── notebooks/            # Jupyter notebooks for exploration
├── src/                  # Source code for cleaning functions
└── reports/              # Generated analysis and figures
"""
4. Data Exploration Basics
4.1 Loading Data
From Different Sources
Python

# CSV file (most common)
df = pd.read_csv('data.csv')

# Excel file
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# JSON file
df = pd.read_json('data.json')

# SQL database
import sqlite3
conn = sqlite3.connect('database.db')
df = pd.read_sql_query("SELECT * FROM table_name", conn)

# From URL
df = pd.read_csv('https://example.com/data.csv')
Handling Common Loading Issues
Python

# Different delimiters
df = pd.read_csv('data.txt', delimiter='\t')  # Tab-separated
df = pd.read_csv('data.txt', delimiter='|')   # Pipe-separated

# Different encodings
df = pd.read_csv('data.csv', encoding='utf-8')
df = pd.read_csv('data.csv', encoding='latin-1')

# Skipping rows
df = pd.read_csv('data.csv', skiprows=2)  # Skip first 2 rows

# Specifying data types
df = pd.read_csv('data.csv', dtype={'age': int, 'salary': float})

# Handling dates
df = pd.read_csv('data.csv', parse_dates=['date_column'])
4.2 First Look at Your Data
The Essential Five Commands
Python

# 1. See the first few rows
print(df.head())
"""
Why: Understand data structure, column names, sample values
What to look for: Unexpected values, format issues, column names
"""

# 2. Get dataset dimensions
print(df.shape)
# Output: (1000, 15) means 1000 rows, 15 columns

# 3. Get column information
print(df.info())
"""
What it shows:
- Column names
- Non-null counts (helps identify missing values)
- Data types
- Memory usage
"""

# 4. Statistical summary
print(df.describe())
"""
For numerical columns shows:
- count, mean, std
- min, 25%, 50%, 75%, max
"""

# 5. See all column names
print(df.columns.tolist())
Comprehensive Example
Python

# Sample dataset
data = {
    'customer_id': [1, 2, 3, 4, 5],
    'name': ['John Doe', 'Jane Smith', None, 'Bob Wilson', 'Alice Brown'],
    'age': [25, 30, 35, -5, 200],  # Contains outliers
    'email': ['john@email.com', 'jane@email', 'bob@email.com', 'bob@email.com', 'alice@email.com'],
    'purchase_amount': [100.5, 200.0, None, 150.75, 300.0],
    'date': ['2023-01-15', '2023-02-20', '2023-03-25', 'invalid', '2023-05-30']
}

df = pd.DataFrame(data)

# Exploration output
print("="*50)
print("DATASET OVERVIEW")
print("="*50)
print(f"\nShape: {df.shape}")
print(f"Total cells: {df.shape[0] * df.shape[1]}")
print(f"\nColumns: {df.columns.tolist()}")

print("\n" + "="*50)
print("FIRST 5 ROWS")
print("="*50)
print(df.head())

print("\n" + "="*50)
print("DATA TYPES AND MISSING VALUES")
print("="*50)
print(df.info())

print("\n" + "="*50)
print("STATISTICAL SUMMARY")
print("="*50)
print(df.describe())
4.3 Deep Dive Exploration
Check for Missing Values
Python

# Method 1: Count of missing values per column
missing_count = df.isnull().sum()
print(missing_count)

# Method 2: Percentage of missing values
missing_percent = (df.isnull().sum() / len(df)) * 100
print(missing_percent)

# Method 3: Detailed missing value report
def missing_value_report(df):
    """
    Creates a comprehensive missing value report
    """
    missing_df = pd.DataFrame({
        'Column': df.columns,
        'Missing_Count': df.isnull().sum().values,
        'Missing_Percentage': (df.isnull().sum().values / len(df)) * 100,
        'Data_Type': df.dtypes.values
    })
    
    # Sort by missing percentage
    missing_df = missing_df.sort_values('Missing_Percentage', ascending=False)
    missing_df = missing_df[missing_df['Missing_Count'] > 0]
    
    return missing_df

print(missing_value_report(df))
Visualizing Missing Data
Python

import matplotlib.pyplot as plt
import seaborn as sns

# Heatmap of missing values
plt.figure(figsize=(12, 6))
sns.heatmap(df.isnull(), cbar=True, yticklabels=False, cmap='viridis')
plt.title('Missing Value Heatmap')
plt.show()

# Bar plot of missing percentages
missing_percent = (df.isnull().sum() / len(df)) * 100
missing_percent = missing_percent[missing_percent > 0].sort_values(ascending=False)

plt.figure(figsize=(10, 6))
missing_percent.plot(kind='bar')
plt.title('Percentage of Missing Values by Column')
plt.ylabel('Percentage')
plt.xlabel('Columns')
plt.xticks(rotation=45)
plt.show()
Check for Duplicates
Python

# Count duplicate rows
duplicate_count = df.duplicated().sum()
print(f"Number of duplicate rows: {duplicate_count}")

# See the duplicate rows
duplicates = df[df.duplicated(keep=False)]
print(duplicates)

# Check duplicates based on specific columns
duplicates_email = df[df.duplicated(subset=['email'], keep=False)]
print(duplicates_email)

# Detailed duplicate report
def duplicate_report(df):
    """
    Creates a comprehensive duplicate report
    """
    total_rows = len(df)
    duplicate_rows = df.duplicated().sum()
    duplicate_percentage = (duplicate_rows / total_rows) * 100
    
    print(f"Total Rows: {total_rows}")
    print(f"Duplicate Rows: {duplicate_rows}")
    print(f"Duplicate Percentage: {duplicate_percentage:.2f}%")
    print(f"Unique Rows: {total_rows - duplicate_rows}")
    
    # Check duplicates by column
    print("\nDuplicates by column:")
    for col in df.columns:
        dup_count = df.duplicated(subset=[col]).sum()
        if dup_count > 0:
            print(f"{col}: {dup_count} duplicates")

duplicate_report(df)
Check Value Distributions
Python

# For categorical columns
for col in df.select_dtypes(include=['object']).columns:
    print(f"\n{col.upper()} - Value Counts:")
    print(df[col].value_counts())
    print(f"Unique values: {df[col].nunique()}")

# For numerical columns
for col in df.select_dtypes(include=['int64', 'float64']).columns:
    print(f"\n{col.upper()} - Statistics:")
    print(df[col].describe())
    
# Visualize distributions
import matplotlib.pyplot as plt

# For numerical columns
numerical_cols = df.select_dtypes(include=['int64', 'float64']).columns
fig, axes = plt.subplots(len(numerical_cols), 2, figsize=(12, 4*len(numerical_cols)))

for i, col in enumerate(numerical_cols):
    # Histogram
    axes[i, 0].hist(df[col].dropna(), bins=30, edgecolor='black')
    axes[i, 0].set_title(f'{col} - Histogram')
    axes[i, 0].set_xlabel(col)
    axes[i, 0].set_ylabel('Frequency')
    
    # Box plot
    axes[i, 1].boxplot(df[col].dropna())
    axes[i, 1].set_title(f'{col} - Box Plot')
    axes[i, 1].set_ylabel(col)

plt.tight_layout()
plt.show()
5. Handling Missing Data
5.1 Understanding Missing Data
Types of Missing Data
1. MCAR - Missing Completely At Random

text

Example: A sensor randomly fails 5% of the time
Impact: Least problematic, no bias introduced
Strategy: Can safely delete or impute
2. MAR - Missing At Random

text

Example: Older people less likely to provide email addresses
Impact: Missing related to observed data, not the missing value itself
Strategy: Imputation based on other features
3. MNAR - Missing Not At Random

text

Example: High earners don't report their income
Impact: Most problematic, systematic bias
Strategy: Need domain knowledge, careful handling
Visual Identification of Missing Patterns
Python

import missingno as msno  # pip install missingno

# Visualize missing data patterns
msno.matrix(df)
plt.show()

# Correlation of missingness
msno.heatmap(df)
plt.show()

# Dendrogram of missing value correlation
msno.dendrogram(df)
plt.show()
5.2 Strategies for Handling Missing Data
Strategy 1: Deletion
A. Row Deletion (Listwise Deletion)
Python

# Remove all rows with any missing value
df_cleaned = df.dropna()

# Remove rows where ALL values are missing
df_cleaned = df.dropna(how='all')

# Remove rows where missing values exceed threshold
# Keep rows with at least 3 non-null values
df_cleaned = df.dropna(thresh=3)

# Remove rows with missing values in specific columns
df_cleaned = df.dropna(subset=['important_column1', 'important_column2'])

# Example with decision logic
def smart_row_deletion(df, threshold=0.5):
    """
    Delete rows based on percentage of missing values
    
    threshold: if a row has more than this percentage missing, delete it
    """
    # Calculate percentage of missing values per row
    missing_percent = df.isnull().sum(axis=1) / len(df.columns)
    
    # Keep rows below threshold
    df_cleaned = df[missing_percent <= threshold]
    
    rows_deleted = len(df) - len(df_cleaned)
    print(f"Rows deleted: {rows_deleted}")
    print(f"Rows remaining: {len(df_cleaned)}")
    
    return df_cleaned

df_cleaned = smart_row_deletion(df, threshold=0.3)
When to Use Row Deletion:

✅ Missing data is MCAR
✅ Small percentage of rows affected (< 5%)
✅ Large dataset where losing rows won't impact analysis
❌ NOT when you have limited data
❌ NOT when missingness is systematic
B. Column Deletion
Python

# Remove columns with any missing values
df_cleaned = df.dropna(axis=1)

# Remove columns with more than 50% missing values
threshold = 0.5
df_cleaned = df.loc[:, df.isnull().mean() < threshold]

# Smart column deletion function
def smart_column_deletion(df, threshold=0.5, keep_columns=None):
    """
    Delete columns based on percentage of missing values
    
    threshold: delete column if missing percentage exceeds this
    keep_columns: list of columns to keep regardless of missing values
    """
    if keep_columns is None:
        keep_columns = []
    
    # Calculate missing percentage per column
    missing_percent = df.isnull().mean()
    
    # Identify columns to drop
    cols_to_drop = missing_percent[missing_percent > threshold].index.tolist()
    
    # Remove protected columns from drop list
    cols_to_drop = [col for col in cols_to_drop if col not in keep_columns]
    
    # Drop columns
    df_cleaned = df.drop(columns=cols_to_drop)
    
    print(f"Columns deleted: {len(cols_to_drop)}")
    print(f"Deleted columns: {cols_to_drop}")
    print(f"Columns remaining: {len(df_cleaned.columns)}")
    
    return df_cleaned

df_cleaned = smart_column_deletion(df, threshold=0.7, keep_columns=['customer_id'])
When to Use Column Deletion:

✅ Column has > 70% missing values
✅ Column is not critical for analysis
✅ Missing data is random
❌ NOT when column is important feature
❌ NOT when you can impute meaningfully
Strategy 2: Imputation (Filling Missing Values)
A. Simple Imputation Methods
Python

# 1. Fill with a constant
df['column_name'].fillna(0, inplace=True)  # Fill with 0
df['column_name'].fillna('Unknown', inplace=True)  # Fill with string

# 2. Fill with mean (for numerical data)
mean_value = df['age'].mean()
df['age'].fillna(mean_value, inplace=True)

# 3. Fill with median (better for skewed data)
median_value = df['salary'].median()
df['salary'].fillna(median_value, inplace=True)

# 4. Fill with mode (most frequent value)
mode_value = df['category'].mode()[0]
df['category'].fillna(mode_value, inplace=True)

# Complete example with decision logic
def simple_imputation(df):
    """
    Apply appropriate simple imputation based on data type
    """
    df_imputed = df.copy()
    
    for column in df_imputed.columns:
        if df_imputed[column].isnull().any():
            
            # Numerical columns
            if df_imputed[column].dtype in ['int64', 'float64']:
                # Check skewness
                skewness = df_imputed[column].skew()
                
                if abs(skewness) < 0.5:  # Approximately normal
                    fill_value = df_imputed[column].mean()
                    method = 'mean'
                else:  # Skewed distribution
                    fill_value = df_imputed[column].median()
                    method = 'median'
                
                df_imputed[column].fillna(fill_value, inplace=True)
                print(f"{column}: Filled with {method} = {fill_value:.2f}")
            
            # Categorical columns
            else:
                mode_value = df_imputed[column].mode()[0]
                df_imputed[column].fillna(mode_value, inplace=True)
                print(f"{column}: Filled with mode = {mode_value}")
    
    return df_imputed

df_imputed = simple_imputation(df)
B. Forward Fill and Backward Fill (For Time Series)
Python

# Forward Fill: Use previous value
df['column'].fillna(method='ffill', inplace=True)

# Backward Fill: Use next value
df['column'].fillna(method='bfill', inplace=True)

# Limit the number of consecutive fills
df['column'].fillna(method='ffill', limit=2, inplace=True)

# Time series example
df_timeseries = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=10),
    'value': [10, np.nan, np.nan, 15, np.nan, 20, np.nan, np.nan, 25, 30]
})

print("Original:")
print(df_timeseries)

# Forward fill
df_ff = df_timeseries.copy()
df_ff['value'].fillna(method='ffill', inplace=True)
print("\nForward Fill:")
print(df_ff)

# Backward fill
df_bf = df_timeseries.copy()
df_bf['value'].fillna(method='bfill', inplace=True)
print("\nBackward Fill:")
print(df_bf)

# Interpolation (smarter for time series)
df_interp = df_timeseries.copy()
df_interp['value'].interpolate(method='linear', inplace=True)
print("\nLinear Interpolation:")
print(df_interp)
C. Advanced Imputation: K-Nearest Neighbors (KNN)
Python

from sklearn.impute import KNNImputer

# Create sample data
data = {
    'age': [25, 30, np.nan, 35, 40, np.nan, 50],
    'salary': [50000, 60000, np.nan, 70000, 80000, 75000, np.nan],
    'years_exp': [2, 5, 7, 8, 12, 10, 15]
}
df = pd.DataFrame(data)

print("Before KNN Imputation:")
print(df)

# KNN Imputation
imputer = KNNImputer(n_neighbors=2)
df_imputed = pd.DataFrame(
    imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter KNN Imputation:")
print(df_imputed)

# Detailed KNN imputation function
def knn_imputation(df, n_neighbors=5):
    """
    Impute missing values using K-Nearest Neighbors
    
    n_neighbors: number of neighbors to use
    """
    # Separate numerical and categorical columns
    numerical_cols = df.select_dtypes(include=['int64', 'float64']).columns
    categorical_cols = df.select_dtypes(include=['object']).columns
    
    df_imputed = df.copy()
    
    # KNN imputation for numerical columns
    if len(numerical_cols) > 0:
        imputer = KNNImputer(n_neighbors=n_neighbors)
        df_imputed[numerical_cols] = imputer.fit_transform(df[numerical_cols])
        print(f"KNN imputation applied to: {list(numerical_cols)}")
    
    # For categorical, use mode
    for col in categorical_cols:
        if df_imputed[col].isnull().any():
            mode_value = df_imputed[col].mode()[0]
            df_imputed[col].fillna(mode_value, inplace=True)
            print(f"{col}: Filled with mode = {mode_value}")
    
    return df_imputed

df_result = knn_imputation(df, n_neighbors=3)
How KNN Imputation Works:

For each missing value, find K nearest rows (based on other features)
Take the average (for numerical) or mode (for categorical) of those K neighbors
Fill the missing value with that calculated value
When to Use KNN:

✅ You have other correlated features
✅ Dataset is not too large (computationally expensive)
✅ Missing data is MAR
❌ Dataset is very large (slow)
❌ Features are independent
D. Advanced Imputation: Iterative Imputer (MICE)
Python

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

# Create sample data
data = {
    'age': [25, 30, np.nan, 35, 40, np.nan, 50, 45],
    'salary': [50000, np.nan, 65000, 70000, np.nan, 75000, 90000, 85000],
    'years_exp': [2, 5, np.nan, 8, 12, 10, 15, 13],
    'education_years': [16, 18, 20, 16, 18, np.nan, 20, 18]
}
df = pd.DataFrame(data)

print("Before MICE Imputation:")
print(df)

# MICE (Multiple Imputation by Chained Equations)
imputer = IterativeImputer(max_iter=10, random_state=42)
df_imputed = pd.DataFrame(
    imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter MICE Imputation:")
print(df_imputed)

# Detailed implementation
def mice_imputation(df, max_iter=10, random_state=42):
    """
    Impute missing values using Multiple Imputation by Chained Equations
    
    max_iter: maximum number of imputation rounds
    random_state: for reproducibility
    """
    # Only for numerical columns
    numerical_cols = df.select_dtypes(include=['int64', 'float64']).columns
    categorical_cols = df.select_dtypes(include=['object']).columns
    
    df_imputed = df.copy()
    
    # MICE for numerical columns
    if len(numerical_cols) > 0:
        imputer = IterativeImputer(max_iter=max_iter, random_state=random_state)
        df_imputed[numerical_cols] = imputer.fit_transform(df[numerical_cols])
        print(f"MICE imputation applied to: {list(numerical_cols)}")
    
    # Mode for categorical
    for col in categorical_cols:
        if df_imputed[col].isnull().any():
            mode_value = df_imputed[col].mode()[0]
            df_imputed[col].fillna(mode_value, inplace=True)
    
    return df_imputed

df_result = mice_imputation(df)
How MICE Works:

Start with simple imputation (mean/median)
For each feature with missing values:
Use other features to predict missing values
Update the imputed values
Repeat step 2 for multiple iterations
Final imputed values are more accurate than simple mean/median
When to Use MICE:

✅ Complex relationships between features
✅ Multiple columns with missing values
✅ MAR or MCAR data
❌ Very large datasets (slow)
❌ MNAR data
Strategy 3: Flagging Missing Values
Python

# Create indicator columns for missing values
def create_missing_indicators(df, columns=None):
    """
    Create binary indicator columns for missing values
    
    columns: list of columns to create indicators for (None = all columns)
    """
    df_with_indicators = df.copy()
    
    if columns is None:
        columns = df.columns
    
    for col in columns:
        if df[col].isnull().any():
            indicator_col = f"{col}_was_missing"
            df_with_indicators[indicator_col] = df[col].isnull().astype(int)
            print(f"Created indicator: {indicator_col}")
    
    return df_with_indicators

# Example
data = {
    'age': [25, 30, np.nan, 35],
    'salary': [50000, np.nan, 65000, 70000]
}
df = pd.DataFrame(data)

df_flagged = create_missing_indicators(df)
print(df_flagged)

# Then impute the original columns
df_flagged['age'].fillna(df_flagged['age'].median(), inplace=True)
df_flagged['salary'].fillna(df_flagged['salary'].median(), inplace=True)
print("\nAfter imputation with flags:")
print(df_flagged)
Why Flag Missing Values:

The fact that a value was missing might be informative
Example: People who don't provide income might have different characteristics
ML model can learn from the missingness pattern
5.3 Comprehensive Missing Data Pipeline
Python

def handle_missing_data(df, strategy='auto', threshold_row=0.5, threshold_col=0.7):
    """
    Comprehensive missing data handling
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    strategy : str
        'auto', 'delete', 'simple', 'knn', 'mice'
    threshold_row : float
        Max percentage of missing values per row before deletion
    threshold_col : float
        Max percentage of missing values per column before deletion
    
    Returns:
    --------
    DataFrame with handled missing values
    """
    print("="*60)
    print("MISSING DATA HANDLING PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    
    # Step 1: Report initial state
    total_missing = df_cleaned.isnull().sum().sum()
    print(f"\nInitial missing values: {total_missing}")
    print(f"Initial shape: {df_cleaned.shape}")
    
    # Step 2: Drop columns with too many missing values
    missing_col_percent = df_cleaned.isnull().mean()
    cols_to_drop = missing_col_percent[missing_col_percent > threshold_col].index.tolist()
    
    if cols_to_drop:
        df_cleaned = df_cleaned.drop(columns=cols_to_drop)
        print(f"\nDropped columns (>{threshold_col*100}% missing): {cols_to_drop}")
    
    # Step 3: Drop rows with too many missing values
    missing_row_percent = df_cleaned.isnull().sum(axis=1) / len(df_cleaned.columns)
    rows_to_keep = missing_row_percent <= threshold_row
    rows_dropped = (~rows_to_keep).sum()
    
    if rows_dropped > 0:
        df_cleaned = df_cleaned[rows_to_keep]
        print(f"\nDropped rows (>{threshold_row*100}% missing): {rows_dropped}")
    
    # Step 4: Handle remaining missing values
    remaining_missing = df_cleaned.isnull().sum().sum()
    
    if remaining_missing > 0:
        print(f"\nRemaining missing values: {remaining_missing}")
        print(f"Applying imputation strategy: {strategy}")
        
        if strategy == 'simple' or strategy == 'auto':
            df_cleaned = simple_imputation(df_cleaned)
        
        elif strategy == 'knn':
            df_cleaned = knn_imputation(df_cleaned)
        
        elif strategy == 'mice':
            df_cleaned = mice_imputation(df_cleaned)
    
    # Step 5: Final report
    final_missing = df_cleaned.isnull().sum().sum()
    print(f"\nFinal missing values: {final_missing}")
    print(f"Final shape: {df_cleaned.shape}")
    print("="*60)
    
    return df_cleaned

# Example usage
data = {
    'id': range(1, 11),
    'age': [25, 30, np.nan, 35, 40, np.nan, 50, 45, np.nan, 55],
    'salary': [50000, np.nan, 65000, 70000, np.nan, 75000, 90000, 85000, 80000, np.nan],
    'city': ['NYC', 'LA', np.nan, 'Chicago', 'NYC', 'LA', np.nan, 'Chicago', 'NYC', 'LA'],
    'useless_col': [np.nan] * 10  # Column with all missing
}
df = pd.DataFrame(data)

# Run pipeline
df_cleaned = handle_missing_data(df, strategy='simple', threshold_col=0.9)
5.4 Decision Framework for Missing Data
Python

def missing_data_strategy_advisor(df):
    """
    Recommends strategy based on data characteristics
    """
    print("MISSING DATA ANALYSIS & RECOMMENDATIONS")
    print("="*60)
    
    total_cells = df.shape[0] * df.shape[1]
    missing_cells = df.isnull().sum().sum()
    missing_percentage = (missing_cells / total_cells) * 100
    
    print(f"Total cells: {total_cells}")
    print(f"Missing cells: {missing_cells}")
    print(f"Missing percentage: {missing_percentage:.2f}%")
    
    # Analyze each column
    print("\nPer-Column Analysis:")
    for col in df.columns:
        missing_pct = (df[col].isnull().sum() / len(df)) * 100
        if missing_pct > 0:
            print(f"\n{col}:")
            print(f"  Missing: {missing_pct:.2f}%")
            
            # Recommendation
            if missing_pct > 70:
                print(f"  ⚠️  RECOMMENDATION: DROP COLUMN")
            elif missing_pct > 30:
                print(f"  💡 RECOMMENDATION: MICE or KNN imputation")
            elif missing_pct > 5:
                print(f"  ✅ RECOMMENDATION: Simple imputation or KNN")
            else:
                print(f"  ✅ RECOMMENDATION: Simple imputation or row deletion")
    
    # Overall recommendation
    print("\n" + "="*60)
    print("OVERALL STRATEGY:")
    if missing_percentage < 1:
        print("✅ Very low missing data - Simple imputation or deletion OK")
    elif missing_percentage < 5:
        print("💡 Low missing data - Simple or KNN imputation recommended")
    elif missing_percentage < 20:
        print("⚠️  Moderate missing data - KNN or MICE imputation recommended")
    else:
        print("🚨 High missing data - Careful analysis needed, consider MICE")
    
    print("="*60)

# Usage
missing_data_strategy_advisor(df)
6. Dealing with Duplicates
6.1 Understanding Duplicates
Types of Duplicates
1. Exact Duplicates

Python

# All columns have identical values
data = {
    'id': [1, 2, 2, 3],  # Row 1 and 2 are identical
    'name': ['John', 'Jane', 'Jane', 'Bob'],
    'age': [25, 30, 30, 35]
}
2. Partial Duplicates

Python

# Some key columns match, others differ
data = {
    'id': [1, 2, 2, 3],  # ID matches
    'name': ['John', 'Jane', 'Jane', 'Bob'],
    'age': [25, 30, 31, 35],  # But age is different
    'timestamp': ['2023-01-01', '2023-01-02', '2023-01-03', '2023-01-04']
}
3. Fuzzy Duplicates

Python

# Similar but not identical (typos, variations)
data = {
    'name': ['John Smith', 'John  Smith', 'Jon Smith'],  # Likely same person
    'email': ['john@email.com', 'john@email.com', 'john@email.com']
}
6.2 Detecting Duplicates
Basic Detection
Python

import pandas as pd
import numpy as np

# Sample data with duplicates
data = {
    'customer_id': [1, 2, 2, 3, 4, 4, 5],
    'name': ['John', 'Jane', 'Jane', 'Bob', 'Alice', 'Alice', 'Charlie'],
    'email': ['j@email.com', 'jane@email.com', 'jane@email.com', 
              'b@email.com', 'alice@email.com', 'alice@email.com', 'c@email.com'],
    'purchase_date': ['2023-01-01', '2023-01-02', '2023-01-02', 
                     '2023-01-03', '2023-01-04', '2023-01-05', '2023-01-06'],
    'amount': [100, 200, 200, 150, 300, 400, 250]
}
df = pd.DataFrame(data)

print("Original DataFrame:")
print(df)

# Check if any row is duplicated
has_duplicates = df.duplicated().any()
print(f"\nHas duplicates: {has_duplicates}")

# Count total duplicate rows
duplicate_count = df.duplicated().sum()
print(f"Number of duplicate rows: {duplicate_count}")

# Get boolean mask of duplicate rows
duplicate_mask = df.duplicated()
print(f"\nDuplicate mask:")
print(duplicate_mask)

# View duplicate rows (keeping first occurrence)
duplicate_rows = df[df.duplicated(keep='first')]
print(f"\nDuplicate rows (excluding first occurrence):")
print(duplicate_rows)

# View ALL instances of duplicated rows (including first occurrence)
all_duplicates = df[df.duplicated(keep=False)]
print(f"\nAll instances of duplicate rows:")
print(all_duplicates)
Detecting Duplicates in Specific Columns
Python

# Check duplicates based on specific columns
duplicate_by_id = df.duplicated(subset=['customer_id'])
print(f"Duplicates by customer_id:")
print(df[duplicate_by_id])

# Check duplicates based on multiple columns
duplicate_by_name_email = df.duplicated(subset=['name', 'email'])
print(f"\nDuplicates by name and email:")
print(df[duplicate_by_name_email])

# Comprehensive duplicate detection function
def detect_duplicates(df, subset=None, report=True):
    """
    Comprehensive duplicate detection
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    subset : list
        Columns to consider for identifying duplicates
    report : bool
        Whether to print detailed report
    
    Returns:
    --------
    DataFrame with duplicate information
    """
    # Detect duplicates
    if subset:
        dup_mask = df.duplicated(subset=subset, keep=False)
        dup_first = df.duplicated(subset=subset, keep='first')
    else:
        dup_mask = df.duplicated(keep=False)
        dup_first = df.duplicated(keep='first')
    
    # Statistics
    total_rows = len(df)
    duplicate_instances = dup_mask.sum()
    duplicate_rows = dup_first.sum()
    unique_rows = total_rows - duplicate_rows
    
    if report:
        print("="*60)
        print("DUPLICATE DETECTION REPORT")
        print("="*60)
        print(f"Total rows: {total_rows}")
        print(f"Unique rows: {unique_rows}")
        print(f"Duplicate rows (excluding first): {duplicate_rows}")
        print(f"All duplicate instances: {duplicate_instances}")
        print(f"Duplication rate: {(duplicate_rows/total_rows)*100:.2f}%")
        
        if subset:
            print(f"\nChecked columns: {subset}")
        else:
            print(f"\nChecked all columns")
        
        print("="*60)
    
    # Return duplicates
    return df[dup_mask]

# Usage
duplicates = detect_duplicates(df, subset=['customer_id', 'name'])
Advanced Duplicate Analysis
Python

def analyze_duplicates(df, subset=None):
    """
    Deep analysis of duplicate patterns
    """
    print("="*60)
    print("ADVANCED DUPLICATE ANALYSIS")
    print("="*60)
    
    # Overall duplicates
    if subset:
        dup_mask = df.duplicated(subset=subset, keep=False)
    else:
        dup_mask = df.duplicated(keep=False)
    
    duplicates_df = df[dup_mask]
    
    if len(duplicates_df) == 0:
        print("No duplicates found!")
        return
    
    # Group duplicates together
    if subset:
        grouped = duplicates_df.groupby(subset)
    else:
        # Create a hash of all columns for grouping
        duplicates_df['_hash'] = duplicates_df.astype(str).sum(axis=1)
        grouped = duplicates_df.groupby('_hash')
    
    print(f"\nNumber of duplicate groups: {grouped.ngroups}")
    print(f"Total duplicate instances: {len(duplicates_df)}")
    
    # Show each duplicate group
    print("\nDuplicate Groups:")
    print("-"*60)
    for name, group in grouped:
        print(f"\nGroup (appears {len(group)} times):")
        print(group)
        print("-"*60)
    
    # Size distribution
    group_sizes = grouped.size()
    print(f"\nDuplicate group size distribution:")
    print(group_sizes.value_counts().sort_index())

# Usage
analyze_duplicates(df, subset=['customer_id'])
6.3 Removing Duplicates
Basic Removal
Python

# Method 1: Keep first occurrence
df_no_dup_first = df.drop_duplicates(keep='first')
print("Keeping first occurrence:")
print(df_no_dup_first)

# Method 2: Keep last occurrence
df_no_dup_last = df.drop_duplicates(keep='last')
print("\nKeeping last occurrence:")
print(df_no_dup_last)

# Method 3: Remove all duplicates (keep none)
df_no_dup_none = df.drop_duplicates(keep=False)
print("\nRemoving all duplicates:")
print(df_no_dup_none)

# Based on specific columns
df_unique_id = df.drop_duplicates(subset=['customer_id'], keep='first')
print("\nUnique by customer_id:")
print(df_unique_id)

# In-place modification
df_copy = df.copy()
df_copy.drop_duplicates(inplace=True)
print("\nAfter in-place removal:")
print(df_copy)
Smart Duplicate Removal
Python

def smart_duplicate_removal(df, subset=None, keep_strategy='first', 
                           sort_by=None, ascending=True):
    """
    Intelligent duplicate removal with sorting
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    subset : list
        Columns to identify duplicates
    keep_strategy : str
        'first', 'last', or 'none'
    sort_by : str or list
        Column(s) to sort by before removing duplicates
    ascending : bool
        Sort order
    
    Returns:
    --------
    DataFrame without duplicates
    """
    df_cleaned = df.copy()
    
    # Sort if specified (useful for keeping best record)
    if sort_by:
        df_cleaned = df_cleaned.sort_values(by=sort_by, ascending=ascending)
    
    # Remove duplicates
    initial_count = len(df_cleaned)
    df_cleaned = df_cleaned.drop_duplicates(subset=subset, keep=keep_strategy)
    final_count = len(df_cleaned)
    removed_count = initial_count - final_count
    
    print(f"Removed {removed_count} duplicate rows")
    print(f"Remaining rows: {final_count}")
    
    return df_cleaned

# Example: Keep the most recent purchase for each customer
df_recent = smart_duplicate_removal(
    df, 
    subset=['customer_id'], 
    keep_strategy='last',
    sort_by='purchase_date',
    ascending=True
)
print(df_recent)

# Example: Keep the highest amount for each customer
df_highest = smart_duplicate_removal(
    df,
    subset=['customer_id'],
    keep_strategy='last',
    sort_by='amount',
    ascending=True
)
print(df_highest)
Handling Duplicates with Aggregation
Python

def aggregate_duplicates(df, id_columns, agg_dict):
    """
    Instead of removing duplicates, aggregate them
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    id_columns : list
        Columns that identify unique entities
    agg_dict : dict
        Aggregation rules {column: aggregation_function}
    
    Returns:
    --------
    DataFrame with aggregated duplicates
    """
    # Identify columns not in id_columns or agg_dict
    other_cols = [col for col in df.columns 
                  if col not in id_columns and col not in agg_dict.keys()]
    
    # For other columns, take first value
    for col in other_cols:
        if col not in agg_dict:
            agg_dict[col] = 'first'
    
    # Group and aggregate
    df_aggregated = df.groupby(id_columns, as_index=False).agg(agg_dict)
    
    print(f"Rows before aggregation: {len(df)}")
    print(f"Rows after aggregation: {len(df_aggregated)}")
    
    return df_aggregated

# Example: Sum amounts for duplicate customer IDs
agg_rules = {
    'amount': 'sum',          # Sum all amounts
    'purchase_date': 'max',   # Keep latest date
    'email': 'first'          # Keep first email
}

df_aggregated = aggregate_duplicates(df, ['customer_id'], agg_rules)
print(df_aggregated)
6.4 Handling Fuzzy Duplicates
String Similarity Detection
Python

from difflib import SequenceMatcher

def string_similarity(str1, str2):
    """
    Calculate similarity between two strings (0 to 1)
    """
    return SequenceMatcher(None, str1.lower(), str2.lower()).ratio()

# Example
print(string_similarity("John Smith", "Jon Smith"))  # Output: ~0.9
print(string_similarity("John Smith", "Jane Doe"))   # Output: ~0.3

# Find fuzzy duplicates
def find_fuzzy_duplicates(df, column, threshold=0.85):
    """
    Find rows with similar values in a column
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    column : str
        Column to check for similarity
    threshold : float
        Similarity threshold (0 to 1)
    
    Returns:
    --------
    List of potential duplicate groups
    """
    values = df[column].dropna().unique()
    fuzzy_groups = []
    checked = set()
    
    for i, val1 in enumerate(values):
        if val1 in checked:
            continue
        
        group = [val1]
        for val2 in values[i+1:]:
            if string_similarity(str(val1), str(val2)) >= threshold:
                group.append(val2)
                checked.add(val2)
        
        if len(group) > 1:
            fuzzy_groups.append(group)
            checked.add(val1)
    
    return fuzzy_groups

# Example with fuzzy names
data = {
    'name': ['John Smith', 'Jon Smith', 'John  Smith', 'Jane Doe', 
             'Jane  Doe', 'Bob Wilson', 'Robert Wilson'],
    'email': ['j@email.com', 'j@email.com', 'j@email.com',
              'jane@email.com', 'jane@email.com', 'b@email.com', 'r@email.com']
}
df_fuzzy = pd.DataFrame(data)

fuzzy_groups = find_fuzzy_duplicates(df_fuzzy, 'name', threshold=0.85)
print("Fuzzy duplicate groups:")
for group in fuzzy_groups:
    print(group)
Advanced: Using FuzzyWuzzy
Python

# Install: pip install fuzzywuzzy python-Levenshtein

from fuzzywuzzy import fuzz, process

def find_fuzzy_duplicates_advanced(df, column, threshold=85):
    """
    Find fuzzy duplicates using fuzzywuzzy library
    
    threshold: 0-100, higher means more strict matching
    """
    values = df[column].dropna().unique()
    fuzzy_groups = []
    processed = set()
    
    for val in values:
        if val in processed:
            continue
        
        # Find all similar strings
        matches = process.extract(val, values, scorer=fuzz.ratio, limit=len(values))
        
        # Filter by threshold
        group = [match[0] for match in matches if match[1] >= threshold]
        
        if len(group) > 1:
            fuzzy_groups.append(group)
            processed.update(group)
    
    return fuzzy_groups

# Example
fuzzy_groups_advanced = find_fuzzy_duplicates_advanced(df_fuzzy, 'name', threshold=85)
print("Advanced fuzzy duplicate groups:")
for group in fuzzy_groups_advanced:
    print(group)

# Standardize fuzzy duplicates
def standardize_fuzzy_duplicates(df, column, threshold=85):
    """
    Replace fuzzy duplicates with standardized value (most common)
    """
    df_cleaned = df.copy()
    fuzzy_groups = find_fuzzy_duplicates_advanced(df, column, threshold)
    
    for group in fuzzy_groups:
        # Find most common variant
        value_counts = df_cleaned[df_cleaned[column].isin(group)][column].value_counts()
        standard_value = value_counts.index[0]
        
        # Replace all variants with standard
        df_cleaned[column] = df_cleaned[column].replace(group, standard_value)
        print(f"Standardized {group} → {standard_value}")
    
    return df_cleaned

df_standardized = standardize_fuzzy_duplicates(df_fuzzy, 'name', threshold=85)
print("\nAfter standardization:")
print(df_standardized)
6.5 Comprehensive Duplicate Handling Pipeline
Python

def handle_duplicates_pipeline(df, config):
    """
    Complete pipeline for handling duplicates
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Configuration dictionary with keys:
        - 'exact_duplicates': {'subset': [...], 'keep': 'first'}
        - 'fuzzy_duplicates': {'column': 'name', 'threshold': 85}
        - 'aggregate': {'id_cols': [...], 'agg_rules': {...}}
    
    Returns:
    --------
    Cleaned DataFrame
    """
    print("="*60)
    print("DUPLICATE HANDLING PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    initial_rows = len(df_cleaned)
    
    # Step 1: Handle fuzzy duplicates
    if 'fuzzy_duplicates' in config:
        print("\n[Step 1] Handling fuzzy duplicates...")
        fuzzy_config = config['fuzzy_duplicates']
        df_cleaned = standardize_fuzzy_duplicates(
            df_cleaned,
            fuzzy_config['column'],
            fuzzy_config.get('threshold', 85)
        )
    
    # Step 2: Handle exact duplicates
    if 'exact_duplicates' in config:
        print("\n[Step 2] Handling exact duplicates...")
        exact_config = config['exact_duplicates']
        
        if 'aggregate' in exact_config and exact_config['aggregate']:
            # Aggregate instead of dropping
            df_cleaned = aggregate_duplicates(
                df_cleaned,
                exact_config['subset'],
                exact_config.get('agg_rules', {})
            )
        else:
            # Drop duplicates
            df_cleaned = smart_duplicate_removal(
                df_cleaned,
                subset=exact_config.get('subset'),
                keep_strategy=exact_config.get('keep', 'first'),
                sort_by=exact_config.get('sort_by'),
                ascending=exact_config.get('ascending', True)
            )
    
    # Final report
    final_rows = len(df_cleaned)
    removed_rows = initial_rows - final_rows
    
    print("\n" + "="*60)
    print("PIPELINE SUMMARY")
    print("="*60)
    print(f"Initial rows: {initial_rows}")
    print(f"Final rows: {final_rows}")
    print(f"Removed rows: {removed_rows}")
    print(f"Reduction: {(removed_rows/initial_rows)*100:.2f}%")
    print("="*60)
    
    return df_cleaned

# Example usage
sample_data = {
    'customer_id': [1, 1, 2, 2, 3, 4, 4],
    'name': ['John Smith', 'Jon Smith', 'Jane Doe', 'Jane Doe', 
             'Bob Wilson', 'Alice Brown', 'Alice Brown'],
    'email': ['john@email.com', 'john@email.com', 'jane@email.com',
              'jane@email.com', 'bob@email.com', 'alice@email.com', 'alice@email.com'],
    'purchase_amount': [100, 150, 200, 250, 300, 400, 450],
    'purchase_date': ['2023-01-01', '2023-01-15', '2023-02-01',
                     '2023-02-15', '2023-03-01', '2023-03-15', '2023-03-20']
}
df_sample = pd.DataFrame(sample_data)

# Configuration
pipeline_config = {
    'fuzzy_duplicates': {
        'column': 'name',
        'threshold': 85
    },
    'exact_duplicates': {
        'subset': ['customer_id', 'name'],
        'keep': 'last',
        'sort_by': 'purchase_date',
        'ascending': True
    }
}

# Run pipeline
df_final = handle_duplicates_pipeline(df_sample, pipeline_config)
print("\nFinal cleaned data:")
print(df_final)
6.6 Best Practices for Duplicate Handling
Decision Framework
Python

def duplicate_handling_advisor(df):
    """
    Provides recommendations for handling duplicates
    """
    print("="*60)
    print("DUPLICATE HANDLING RECOMMENDATIONS")
    print("="*60)
    
    # Check for exact duplicates
    exact_dup = df.duplicated().sum()
    exact_dup_pct = (exact_dup / len(df)) * 100
    
    print(f"\nExact Duplicates:")
    print(f"  Count: {exact_dup}")
    print(f"  Percentage: {exact_dup_pct:.2f}%")
    
    if exact_dup_pct == 0:
        print("  ✅ No exact duplicates found")
    elif exact_dup_pct < 1:
        print("  💡 Low duplication - simple removal recommended")
    elif exact_dup_pct < 10:
        print("  ⚠️  Moderate duplication - investigate patterns")
    else:
        print("  🚨 High duplication - requires careful analysis")
    
    # Check column-wise duplicates
    print("\nColumn-wise Duplicate Analysis:")
    for col in df.columns:
        col_dup = df.duplicated(subset=[col]).sum()
        col_dup_pct = (col_dup / len(df)) * 100
        if col_dup_pct > 0:
            print(f"  {col}: {col_dup_pct:.2f}% duplicates")
    
    # Recommendations
    print("\n" + "="*60)
    print("RECOMMENDATIONS:")
    print("="*60)
    
    if exact_dup_pct == 0:
        print("1. No exact duplicates - check for fuzzy duplicates in text fields")
    elif exact_dup_pct < 5:
        print("1. Use drop_duplicates() with appropriate 'keep' parameter")
        print("2. Consider keeping 'last' if data has timestamps")
    elif exact_dup_pct < 20:
        print("1. Investigate WHY duplicates exist")
        print("2. Consider aggregation instead of deletion")
        print("3. Check if duplicates represent legitimate multiple entries")
    else:
        print("1. CRITICAL: High duplication indicates data quality issues")
        print("2. Investigate data source and collection process")
        print("3. Consider aggregation strategies")
        print("4. May need domain expert consultation")
    
    print("="*60)

# Usage
duplicate_handling_advisor(df_sample)
7. Data Type Conversions
7.1 Understanding Data Types
Common Data Types in Pandas
Type	Pandas dtype	Description	Example
Integer	int64	Whole numbers	1, 100, -50
Float	float64	Decimal numbers	1.5, 3.14, -2.7
String	object	Text data	"Hello", "Data"
Boolean	bool	True/False	True, False
Datetime	datetime64	Date and time	2023-01-15
Category	category	Fixed set of values	"Red", "Blue", "Green"
Checking Current Data Types
Python

import pandas as pd
import numpy as np

# Sample dataset with mixed types
data = {
    'customer_id': [1, 2, 3, 4, 5],
    'age': ['25', '30', '35', 'unknown', '40'],  # Should be int
    'salary': ['50000', '60000.5', '70000', 'N/A', '80000'],  # Should be float
    'join_date': ['2023-01-15', '2023-02-20', '2023-03-25', '2023-04-10', 'Invalid'],
    'is_active': ['True', 'False', 'True', '1', '0'],  # Should be boolean
    'department': ['Sales', 'IT', 'Sales', 'HR', 'IT']  # Could be category
}
df = pd.DataFrame(data)

# Check data types
print("Current Data Types:")
print(df.dtypes)
print("\n")

# Detailed type information
print("Detailed Info:")
print(df.info())
print("\n")

# Check unique values to understand the data
for col in df.columns:
    print(f"{col}: {df[col].unique()}")
Why Data Types Matter for ML
Python

"""
IMPACT ON MACHINE LEARNING:

1. MEMORY EFFICIENCY
   - int8 uses 1 byte: range -128 to 127
   - int64 uses 8 bytes: range -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
   - For age (0-100), int8 is sufficient
   
2. COMPUTATIONAL SPEED
   - Smaller types = faster computations
   - Categorical types = more efficient than strings
   
3. ALGORITHM REQUIREMENTS
   - Most ML algorithms require numerical input
   - Can't use strings directly in sklearn models
   
4. PRECISION
   - float32 vs float64 affects numerical stability
   - Important for financial data, scientific computations
"""

# Example of memory impact
df_large = pd.DataFrame({
    'age_int64': np.random.randint(0, 100, 1000000),
})
df_large['age_int8'] = df_large['age_int64'].astype('int8')

print(f"Memory with int64: {df_large['age_int64'].memory_usage() / 1024:.2f} KB")
print(f"Memory with int8: {df_large['age_int8'].memory_usage() / 1024:.2f} KB")
print(f"Memory saved: {((df_large['age_int64'].memory_usage() - df_large['age_int8'].memory_usage()) / df_large['age_int64'].memory_usage()) * 100:.2f}%")
7.2 Converting to Numerical Types
String to Integer
Python

# Sample data
data = {
    'age': ['25', '30', '35', 'unknown', '40', '45.5', ''],
    'count': ['100', '200', '300', 'NA', '400', '500', '600']
}
df = pd.DataFrame(data)

print("Original:")
print(df)
print(df.dtypes)

# Method 1: Simple conversion (will fail with non-numeric values)
try:
    df['age_int'] = df['age'].astype(int)
except ValueError as e:
    print(f"\nError with simple conversion: {e}")

# Method 2: Using pd.to_numeric with error handling
df['age_numeric'] = pd.to_numeric(df['age'], errors='coerce')  # Invalid → NaN
print("\nAfter to_numeric with errors='coerce':")
print(df)

# Method 3: Replace invalid values first, then convert
df_clean = df.copy()
df_clean['age'] = df_clean['age'].replace(['unknown', '', 'NA'], np.nan)
df_clean['age'] = pd.to_numeric(df_clean['age'], errors='coerce')
df_clean['age'] = df_clean['age'].astype('Int64')  # Nullable integer type
print("\nCleaned version:")
print(df_clean)

# Method 4: Comprehensive conversion function
def convert_to_integer(series, handle_invalid='coerce', fill_value=None):
    """
    Convert series to integer with robust error handling
    
    Parameters:
    -----------
    series : pd.Series
        Input series
    handle_invalid : str
        'coerce': convert invalid to NaN
        'drop': remove invalid rows
        'fill': fill with fill_value
    fill_value : int
        Value to fill invalid entries (if handle_invalid='fill')
    
    Returns:
    --------
    Converted series
    """
    # Convert to numeric first
    series_numeric = pd.to_numeric(series, errors='coerce')
    
    if handle_invalid == 'coerce':
        result = series_numeric
    
    elif handle_invalid == 'fill' and fill_value is not None:
        result = series_numeric.fillna(fill_value)
    
    elif handle_invalid == 'drop':
        result = series_numeric.dropna()
    
    else:
        result = series_numeric
    
    # Convert to integer (use Int64 to support NaN)
    result = result.astype('Int64')
    
    return result

# Usage examples
df['age_coerce'] = convert_to_integer(df['age'], handle_invalid='coerce')
df['age_fill'] = convert_to_integer(df['age'], handle_invalid='fill', fill_value=0)

print("\nWith different handling strategies:")
print(df[['age', 'age_coerce', 'age_fill']])
String to Float
Python

# Sample data with various float representations
data = {
    'price': ['$100.50', '200.75', '300', 'N/A', '1,500.25', '2000.0'],
    'percentage': ['45.5%', '67.8%', '90%', 'unknown', '12.3%', '100.0%']
}
df = pd.DataFrame(data)

print("Original:")
print(df)

# Clean and convert price
def clean_price(series):
    """
    Clean price data (remove $, commas) and convert to float
    """
    # Remove currency symbols and commas
    cleaned = series.str.replace('$', '', regex=False)
    cleaned = cleaned.str.replace(',', '', regex=False)
    
    # Convert to numeric
    cleaned = pd.to_numeric(cleaned, errors='coerce')
    
    return cleaned

df['price_clean'] = clean_price(df['price'])

# Clean and convert percentage
def clean_percentage(series):
    """
    Clean percentage data (remove %) and convert to decimal
    """
    # Remove % symbol
    cleaned = series.str.replace('%', '', regex=False)
    
    # Convert to numeric
    cleaned = pd.to_numeric(cleaned, errors='coerce')
    
    # Convert to decimal (divide by 100)
    cleaned = cleaned / 100
    
    return cleaned

df['percentage_clean'] = clean_percentage(df['percentage'])

print("\nCleaned:")
print(df)

# General numeric cleaning function
import re

def convert_to_float(series, decimal_places=None):
    """
    Robust conversion to float with cleaning
    
    Parameters:
    -----------
    series : pd.Series
        Input series
    decimal_places : int
        Number of decimal places to round to
    
    Returns:
    --------
    Cleaned float series
    """
    # Convert to string first
    cleaned = series.astype(str)
    
    # Remove common non-numeric characters
    cleaned = cleaned.str.replace('$', '', regex=False)
    cleaned = cleaned.str.replace(',', '', regex=False)
    cleaned = cleaned.str.replace('%', '', regex=False)
    cleaned = cleaned.str.replace('€', '', regex=False)
    cleaned = cleaned.str.replace('£', '', regex=False)
    
    # Remove any non-numeric except decimal point and minus sign
    cleaned = cleaned.str.replace(r'[^\d.-]', '', regex=True)
    
    # Convert to numeric
    cleaned = pd.to_numeric(cleaned, errors='coerce')
    
    # Round if specified
    if decimal_places is not None:
        cleaned = cleaned.round(decimal_places)
    
    return cleaned

# Test with various formats
test_data = pd.Series(['$1,234.56', '€789.01', '£456.78', '100', '-50.5', 'N/A'])
print("\nTest conversion:")
print(convert_to_float(test_data))
7.3 Converting to Datetime
Basic Datetime Conversion
Python

# Sample date data in various formats
data = {
    'date_iso': ['2023-01-15', '2023-02-20', '2023-03-25', 'Invalid', '2023-05-30'],
    'date_us': ['01/15/2023', '02/20/2023', '03/25/2023', '04/10/2023', '05/30/2023'],
    'date_eu': ['15/01/2023', '20/02/2023', '25/03/2023', '10/04/2023', '30/05/2023'],
    'date_text': ['Jan 15, 2023', 'Feb 20, 2023', 'Mar 25, 2023', 'Apr 10, 2023', 'May 30, 2023'],
    'timestamp': ['2023-01-15 14:30:00', '2023-02-20 09:15:00', '2023-03-25 18:45:00', 
                  '2023-04-10 12:00:00', '2023-05-30 16:20:00']
}
df = pd.DataFrame(data)

print("Original:")
print(df)
print(df.dtypes)

# Method 1: Simple conversion (auto-detect format)
df['date_iso_converted'] = pd.to_datetime(df['date_iso'], errors='coerce')
print("\nISO format converted:")
print(df['date_iso_converted'])

# Method 2: Specify format (faster and more reliable)
df['date_us_converted'] = pd.to_datetime(df['date_us'], format='%m/%d/%Y', errors='coerce')
df['date_eu_converted'] = pd.to_datetime(df['date_eu'], format='%d/%m/%Y', errors='coerce')
print("\nUS and EU formats converted:")
print(df[['date_us_converted', 'date_eu_converted']])

# Method 3: Infer format automatically
df['date_text_converted'] = pd.to_datetime(df['date_text'], infer_datetime_format=True, errors='coerce')
print("\nText format converted:")
print(df['date_text_converted'])
Common Datetime Format Codes
Python

"""
COMMON DATETIME FORMAT CODES:

%Y - 4-digit year (2023)
%y - 2-digit year (23)
%m - Month as number (01-12)
%d - Day of month (01-31)
%H - Hour 24-hour format (00-23)
%I - Hour 12-hour format (01-12)
%M - Minute (00-59)
%S - Second (00-59)
%p - AM/PM
%B - Full month name (January)
%b - Abbreviated month name (Jan)
%A - Full weekday name (Monday)
%a - Abbreviated weekday name (Mon)

Examples:
'%Y-%m-%d' → '2023-01-15'
'%d/%m/%Y' → '15/01/2023'
'%m/%d/%Y %H:%M:%S' → '01/15/2023 14:30:00'
'%B %d, %Y' → 'January 15, 2023'
"""

# Examples of different formats
date_formats = {
    'ISO 8601': ('2023-01-15', '%Y-%m-%d'),
    'US Style': ('01/15/2023', '%m/%d/%Y'),
    'EU Style': ('15/01/2023', '%d/%m/%Y'),
    'Full Text': ('January 15, 2023', '%B %d, %Y'),
    'Short Text': ('Jan 15, 2023', '%b %d, %Y'),
    'With Time': ('2023-01-15 14:30:00', '%Y-%m-%d %H:%M:%S'),
    '12-Hour': ('01/15/2023 02:30 PM', '%m/%d/%Y %I:%M %p')
}

for name, (date_str, format_str) in date_formats.items():
    converted = pd.to_datetime(date_str, format=format_str)
    print(f"{name:15} | {date_str:25} → {converted}")
Robust Datetime Conversion Function
Python

def convert_to_datetime(series, formats=None, return_invalid=False):
    """
    Robust datetime conversion trying multiple formats
    
    Parameters:
    -----------
    series : pd.Series
        Input series with date strings
    formats : list
        List of datetime formats to try
    return_invalid : bool
        Whether to return rows that failed conversion
    
    Returns:
    --------
    Converted series (and optionally invalid rows)
    """
    if formats is None:
        # Default formats to try
        formats = [
            '%Y-%m-%d',
            '%d/%m/%Y',
            '%m/%d/%Y',
            '%Y-%m-%d %H:%M:%S',
            '%d/%m/%Y %H:%M:%S',
            '%m/%d/%Y %H:%M:%S',
            '%B %d, %Y',
            '%b %d, %Y',
            '%d-%m-%Y',
            '%m-%d-%Y'
        ]
    
    # Try each format
    for fmt in formats:
        try:
            converted = pd.to_datetime(series, format=fmt, errors='coerce')
            # Check how many were successfully converted
            success_rate = converted.notna().sum() / len(series)
            if success_rate > 0.5:  # If > 50% converted, use this format
                print(f"Successfully used format: {fmt} ({success_rate*100:.1f}% converted)")
                
                if return_invalid:
                    invalid_rows = series[converted.isna()]
                    return converted, invalid_rows
                return converted
        except:
            continue
    
    # If no format worked, try auto-detection
    print("No single format worked, trying auto-detection...")
    converted = pd.to_datetime(series, infer_datetime_format=True, errors='coerce')
    
    if return_invalid:
        invalid_rows = series[converted.isna()]
        return converted, invalid_rows
    
    return converted

# Example usage
mixed_dates = pd.Series([
    '2023-01-15',
    '2023-02-20',
    '2023-03-25',
    'Invalid Date',
    '2023-05-30'
])

converted_dates, invalid_dates = convert_to_datetime(mixed_dates, return_invalid=True)
print("\nConverted dates:")
print(converted_dates)
print("\nInvalid dates:")
print(invalid_dates)
Extracting Components from Datetime
Python

# Create datetime column
df['date'] = pd.to_datetime(df['date_iso'], errors='coerce')

# Extract components
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['day_of_week'] = df['date'].dt.dayofweek  # Monday=0, Sunday=6
df['day_name'] = df['date'].dt.day_name()
df['month_name'] = df['date'].dt.month_name()
df['quarter'] = df['date'].dt.quarter
df['week_of_year'] = df['date'].dt.isocalendar().week

print("Datetime components:")
print(df[['date', 'year', 'month', 'day', 'day_name', 'month_name', 'quarter']])

# Useful for feature engineering
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
df['is_month_start'] = df['date'].dt.is_month_start.astype(int)
df['is_month_end'] = df['date'].dt.is_month_end.astype(int)

print("\nDerived features:")
print(df[['date', 'is_weekend', 'is_month_start', 'is_month_end']])
7.4 Converting to Categorical
When to Use Categorical Type
Python

"""
USE CATEGORICAL TYPE WHEN:
1. Limited number of unique values
2. Values repeat frequently
3. Fixed set of possible values

BENEFITS:
- Reduced memory usage
- Faster operations
- Can enforce valid values
- Better for ordered categories

EXAMPLE:
- Gender: Male, Female, Other (3 unique values)
- Department: Sales, IT, HR, Marketing (4 unique values)
- Size: Small, Medium, Large (3 unique values, ordered)
"""

# Example demonstrating memory savings
n = 1000000
df_test = pd.DataFrame({
    'department_string': np.random.choice(['Sales', 'IT', 'HR', 'Marketing'], n),
})
df_test['department_category'] = df_test['department_string'].astype('category')

print("Memory Usage:")
print(f"String type: {df_test['department_string'].memory_usage() / 1024:.2f} KB")
print(f"Category type: {df_test['department_category'].memory_usage() / 1024:.2f} KB")
print(f"Memory saved: {((df_test['department_string'].memory_usage() - df_test['department_category'].memory_usage()) / df_test['department_string'].memory_usage()) * 100:.2f}%")
Converting to Categorical
Python

# Sample data
data = {
    'customer_id': range(1, 11),
    'department': ['Sales', 'IT', 'Sales', 'HR', 'IT', 'Sales', 'Marketing', 'HR', 'IT', 'Sales'],
    'size': ['Small', 'Large', 'Medium', 'Small', 'Large', 'Medium', 'Small', 'Medium', 'Large', 'Small'],
    'rating': ['Good', 'Excellent', 'Poor', 'Good', 'Excellent', 'Good', 'Poor', 'Good', 'Excellent', 'Good']
}
df = pd.DataFrame(data)

print("Original dtypes:")
print(df.dtypes)

# Method 1: Simple conversion
df['department_cat'] = df['department'].astype('category')

# Method 2: With ordered categories (for ordinal data)
size_order = ['Small', 'Medium', 'Large']
df['size_cat'] = pd.Categorical(df['size'], categories=size_order, ordered=True)

rating_order = ['Poor', 'Good', 'Excellent']
df['rating_cat'] = pd.Categorical(df['rating'], categories=rating_order, ordered=True)

print("\nAfter conversion:")
print(df.dtypes)

# Check categories
print("\nDepartment categories:", df['department_cat'].cat.categories)
print("Size categories (ordered):", df['size_cat'].cat.categories)
print("Rating categories (ordered):", df['rating_cat'].cat.categories)

# Ordered categories enable comparisons
print("\nComparisons with ordered categories:")
print(df[df['size_cat'] > 'Small'][['size', 'size_cat']])
print(df[df['rating_cat'] >= 'Good'][['rating', 'rating_cat']])
Comprehensive Categorical Conversion
Python

def convert_to_categorical(df, columns=None, ordered_dict=None, threshold=0.05):
    """
    Convert appropriate columns to categorical type
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Specific columns to convert (None = auto-detect)
    ordered_dict : dict
        {column: list_of_ordered_categories}
    threshold : float
        If unique_values/total_values < threshold, convert to category
    
    Returns:
    --------
    DataFrame with categorical columns
    """
    df_converted = df.copy()
    
    if columns is None:
        # Auto-detect columns suitable for categorical
        columns = []
        for col in df.select_dtypes(include=['object']).columns:
            unique_ratio = df[col].nunique() / len(df)
            if unique_ratio < threshold:
                columns.append(col)
                print(f"{col}: {df[col].nunique()} unique values ({unique_ratio*100:.2f}%) → Converting to category")
    
    # Convert columns
    for col in columns:
        if ordered_dict and col in ordered_dict:
            # Ordered categorical
            df_converted[col] = pd.Categorical(
                df[col],
                categories=ordered_dict[col],
                ordered=True
            )
            print(f"{col} → Ordered categorical")
        else:
            # Unordered categorical
            df_converted[col] = df_converted[col].astype('category')
            print(f"{col} → Categorical")
    
    return df_converted

# Example usage
ordered_categories = {
    'size': ['Small', 'Medium', 'Large'],
    'rating': ['Poor', 'Good', 'Excellent']
}

df_cat = convert_to_categorical(df, ordered_dict=ordered_categories)
print("\nFinal dtypes:")
print(df_cat.dtypes)
7.5 Converting to Boolean
Python

# Sample data with various boolean representations
data = {
    'active_1': ['True', 'False', 'True', 'True', 'False'],
    'active_2': ['1', '0', '1', '1', '0'],
    'active_3': ['yes', 'no', 'yes', 'yes', 'no'],
    'active_4': ['Y', 'N', 'Y', 'Y', 'N'],
    'active_5': ['active', 'inactive', 'active', 'active', 'inactive']
}
df = pd.DataFrame(data)

print("Original:")
print(df)

# Method 1: Direct conversion for 'True'/'False' strings
df['bool_1'] = df['active_1'].map({'True': True, 'False': False})

# Method 2: For 1/0
df['bool_2'] = df['active_2'].astype(int).astype(bool)

# Method 3: For yes/no
df['bool_3'] = df['active_3'].map({'yes': True, 'no': False})

# Method 4: For Y/N
df['bool_4'] = df['active_4'].map({'Y': True, 'N': False})

# Method 5: For custom values
df['bool_5'] = df['active_5'].map({'active': True, 'inactive': False})

print("\nConverted:")
print(df[[col for col in df.columns if col.startswith('bool_')]])

# General boolean conversion function
def convert_to_boolean(series, true_values=None, false_values=None):
    """
    Convert series to boolean with flexible value mapping
    
    Parameters:
    -----------
    series : pd.Series
        Input series
    true_values : list
        Values to map to True
    false_values : list
        Values to map to False
    
    Returns:
    --------
    Boolean series
    """
    if true_values is None:
        true_values = ['True', 'true', 'TRUE', '1', 'yes', 'Yes', 'YES', 'Y', 'y', 'active', 'Active']
    
    if false_values is None:
        false_values = ['False', 'false', 'FALSE', '0', 'no', 'No', 'NO', 'N', 'n', 'inactive', 'Inactive']
    
    # Create mapping dictionary
    mapping = {val: True for val in true_values}
    mapping.update({val: False for val in false_values})
    
    # Convert
    result = series.map(mapping)
    
    # Report unmapped values
    unmapped = series[result.isna()]
    if len(unmapped) > 0:
        print(f"Warning: {len(unmapped)} values could not be mapped:")
        print(unmapped.unique())
    
    return result

# Test
test_series = pd.Series(['yes', 'no', 'YES', 'NO', '1', '0', 'maybe', 'True', 'False'])
converted = convert_to_boolean(test_series)
print("\nTest conversion:")
print(pd.DataFrame({'original': test_series, 'converted': converted}))
7.6 Comprehensive Type Conversion Pipeline
Python

def optimize_dtypes(df, datetime_columns=None, categorical_threshold=0.05, 
                   ordered_categories=None, boolean_columns=None):
    """
    Comprehensive data type optimization
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    datetime_columns : list
        Columns to convert to datetime
    categorical_threshold : float
        Unique ratio threshold for auto-detecting categorical
    ordered_categories : dict
        {column: ordered_list} for ordered categoricals
    boolean_columns : dict
        {column: {'true': [...], 'false': [...]}}
    
    Returns:
    --------
    Optimized DataFrame with memory report
    """
    print("="*60)
    print("DATA TYPE OPTIMIZATION PIPELINE")
    print("="*60)
    
    df_optimized = df.copy()
    initial_memory = df.memory_usage(deep=True).sum() / 1024**2
    
    print(f"\nInitial memory usage: {initial_memory:.2f} MB")
    print(f"Initial shape: {df.shape}")
    print("\nInitial dtypes:")
    print(df.dtypes)
    
    # Step 1: Convert datetime columns
    if datetime_columns:
        print("\n[Step 1] Converting datetime columns...")
        for col in datetime_columns:
            if col in df_optimized.columns:
                df_optimized[col] = pd.to_datetime(df_optimized[col], errors='coerce')
                print(f"  {col} → datetime64")
    
    # Step 2: Convert boolean columns
    if boolean_columns:
        print("\n[Step 2] Converting boolean columns...")
        for col, values in boolean_columns.items():
            if col in df_optimized.columns:
                df_optimized[col] = convert_to_boolean(
                    df_optimized[col],
                    true_values=values.get('true'),
                    false_values=values.get('false')
                )
                print(f"  {col} → bool")
    
    # Step 3: Optimize numeric columns
    print("\n[Step 3] Optimizing numeric columns...")
    for col in df_optimized.select_dtypes(include=['int64']).columns:
        col_min = df_optimized[col].min()
        col_max = df_optimized[col].max()
        
        # Choose appropriate integer type
        if col_min >= 0:
            if col_max < 255:
                df_optimized[col] = df_optimized[col].astype('uint8')
                print(f"  {col} → uint8")
            elif col_max < 65535:
                df_optimized[col] = df_optimized[col].astype('uint16')
                print(f"  {col} → uint16")
            elif col_max < 4294967295:
                df_optimized[col] = df_optimized[col].astype('uint32')
                print(f"  {col} → uint32")
        else:
            if col_min > -128 and col_max < 127:
                df_optimized[col] = df_optimized[col].astype('int8')
                print(f"  {col} → int8")
            elif col_min > -32768 and col_max < 32767:
                df_optimized[col] = df_optimized[col].astype('int16')
                print(f"  {col} → int16")
            elif col_min > -2147483648 and col_max < 2147483647:
                df_optimized[col] = df_optimized[col].astype('int32')
                print(f"  {col} → int32")
    
    # Optimize float columns
    for col in df_optimized.select_dtypes(include=['float64']).columns:
        df_optimized[col] = df_optimized[col].astype('float32')
        print(f"  {col} → float32")
    
    # Step 4: Convert to categorical
    print("\n[Step 4] Converting to categorical...")
    df_optimized = convert_to_categorical(
        df_optimized,
        ordered_dict=ordered_categories,
        threshold=categorical_threshold
    )
    
    # Final report
    final_memory = df_optimized.memory_usage(deep=True).sum() / 1024**2
    memory_saved = initial_memory - final_memory
    memory_saved_pct = (memory_saved / initial_memory) * 100
    
    print("\n" + "="*60)
    print("OPTIMIZATION SUMMARY")
    print("="*60)
    print(f"Initial memory: {initial_memory:.2f} MB")
    print(f"Final memory: {final_memory:.2f} MB")
    print(f"Memory saved: {memory_saved:.2f} MB ({memory_saved_pct:.2f}%)")
    print("\nFinal dtypes:")
    print(df_optimized.dtypes)
    print("="*60)
    
    return df_optimized

# Example usage
sample_data = {
    'id': range(1, 101),
    'age': np.random.randint(18, 80, 100),
    'salary': np.random.uniform(30000, 150000, 100),
    'department': np.random.choice(['Sales', 'IT', 'HR', 'Marketing'], 100),
    'join_date': pd.date_range('2020-01-01', periods=100, freq='3D').astype(str),
    'is_active': np.random.choice(['yes', 'no'], 100),
    'performance': np.random.choice(['Poor', 'Good', 'Excellent'], 100)
}
df_sample = pd.DataFrame(sample_data)

# Run optimization
df_optimized = optimize_dtypes(
    df_sample,
    datetime_columns=['join_date'],
    ordered_categories={
        'performance': ['Poor', 'Good', 'Excellent']
    },
    boolean_columns={
        'is_active': {'true': ['yes'], 'false': ['no']}
    }
)
8. Handling Outliers
8.1 Understanding Outliers
What are Outliers?
Definition: Outliers are data points that significantly differ from other observations.

Types of Outliers:

Python

"""
1. UNIVARIATE OUTLIERS
   - Extreme values in a single variable
   - Example: Age = 150 years (when most ages are 20-60)

2. MULTIVARIATE OUTLIERS
   - Normal individually but unusual in combination
   - Example: 25-year-old CEO earning $5M (each value OK separately)

3. CONTEXTUAL OUTLIERS
   - Unusual in specific context
   - Example: Temperature of 30°C normal in summer, outlier in winter
"""
Why Outliers Matter for ML
Python

"""
IMPACT ON MACHINE LEARNING:

1. STATISTICAL MEASURES
   - Mean: Heavily affected by outliers
   - Standard Deviation: Inflated by outliers
   - Example: Salaries [30k, 35k, 40k, 1M]
     Mean without outlier: 35k
     Mean with outlier: 276k (misleading!)

2. MODEL PERFORMANCE
   - Linear Regression: Very sensitive to outliers
   - Decision Trees: Relatively robust
   - Neural Networks: Can be affected
   - SVM: Sensitive to outliers

3. DATA DISTRIBUTION
   - Skews distributions
   - Violates normality assumptions
   - Affects distance-based algorithms (K-Means, KNN)
"""

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Demonstrate impact on statistics
normal_data = [30, 32, 35, 38, 40, 42, 45, 48, 50]
data_with_outlier = normal_data + [200]

print("WITHOUT outlier:")
print(f"Mean: {np.mean(normal_data):.2f}")
print(f"Median: {np.median(normal_data):.2f}")
print(f"Std Dev: {np.std(normal_data):.2f}")

print("\nWITH outlier:")
print(f"Mean: {np.mean(data_with_outlier):.2f}")
print(f"Median: {np.median(data_with_outlier):.2f}")
print(f"Std Dev: {np.std(data_with_outlier):.2f}")

# Visualize impact
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

axes[0].boxplot(normal_data)
axes[0].set_title('Without Outlier')
axes[0].set_ylabel('Value')

axes[1].boxplot(data_with_outlier)
axes[1].set_title('With Outlier')
axes[1].set_ylabel('Value')

plt.tight_layout()
plt.show()
8.2 Detecting Outliers
Method 1: Visual Detection
Python

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Generate sample data with outliers
np.random.seed(42)
n = 1000

data = {
    'age': np.concatenate([
        np.random.normal(35, 10, n-5),  # Normal data
        [150, 200, -5, 250, 180]  # Outliers
    ]),
    'salary': np.concatenate([
        np.random.normal(60000, 15000, n-3),
        [500000, 600000, -10000]
    ]),
    'experience': np.concatenate([
        np.random.normal(10, 5, n-2),
        [50, 60]
    ])
}

df = pd.DataFrame(data)

# Visualization function
def visualize_outliers(df, columns=None):
    """
    Create comprehensive outlier visualizations
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    n_cols = len(columns)
    fig, axes = plt.subplots(n_cols, 3, figsize=(15, 5*n_cols))
    
    if n_cols == 1:
        axes = axes.reshape(1, -1)
    
    for i, col in enumerate(columns):
        # Histogram
        axes[i, 0].hist(df[col], bins=50, edgecolor='black')
        axes[i, 0].set_title(f'{col} - Histogram')
        axes[i, 0].set_xlabel(col)
        axes[i, 0].set_ylabel('Frequency')
        
        # Box plot
        axes[i, 1].boxplot(df[col])
        axes[i, 1].set_title(f'{col} - Box Plot')
        axes[i, 1].set_ylabel(col)
        
        # Scatter plot (vs index)
        axes[i, 2].scatter(range(len(df)), df[col], alpha=0.5)
        axes[i, 2].set_title(f'{col} - Scatter Plot')
        axes[i, 2].set_xlabel('Index')
        axes[i, 2].set_ylabel(col)
    
    plt.tight_layout()
    plt.show()

visualize_outliers(df)
Method 2: Z-Score Method
Python

def detect_outliers_zscore(df, columns=None, threshold=3):
    """
    Detect outliers using Z-score method
    
    Z-score = (value - mean) / std_dev
    If |Z-score| > threshold, it's an outlier
    
    Common thresholds:
    - 3: Very strict (99.7% of data within)
    - 2: Moderate (95% of data within)
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to check (None = all numeric)
    threshold : float
        Z-score threshold
    
    Returns:
    --------
    DataFrame with outlier information
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    outlier_info = {}
    
    for col in columns:
        # Calculate Z-score
        mean = df[col].mean()
        std = df[col].std()
        z_scores = np.abs((df[col] - mean) / std)
        
        # Identify outliers
        outliers = z_scores > threshold
        outlier_count = outliers.sum()
        outlier_percentage = (outlier_count / len(df)) * 100
        
        outlier_info[col] = {
            'count': outlier_count,
            'percentage': outlier_percentage,
            'outlier_indices': df[outliers].index.tolist(),
            'outlier_values': df.loc[outliers, col].tolist()
        }
        
        print(f"\n{col}:")
        print(f"  Outliers: {outlier_count} ({outlier_percentage:.2f}%)")
        print(f"  Mean: {mean:.2f}, Std: {std:.2f}")
        if outlier_count > 0:
            print(f"  Outlier values: {df.loc[outliers, col].tolist()[:5]}")  # Show first 5
    
    return outlier_info

# Detect outliers
outlier_info = detect_outliers_zscore(df, threshold=3)

# Get boolean mask of rows with any outlier
def get_outlier_mask_zscore(df, columns=None, threshold=3):
    """
    Returns boolean mask for rows containing outliers
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    mask = pd.Series([False] * len(df), index=df.index)
    
    for col in columns:
        mean = df[col].mean()
        std = df[col].std()
        z_scores = np.abs((df[col] - mean) / std)
        mask = mask | (z_scores > threshold)
    
    return mask

outlier_mask = get_outlier_mask_zscore(df)
print(f"\nTotal rows with outliers: {outlier_mask.sum()}")
When to Use Z-Score:

✅ Data is approximately normally distributed
✅ You want a statistical approach
❌ Data is highly skewed
❌ Data has multiple modes
Method 3: IQR (Interquartile Range) Method
Python

def detect_outliers_iqr(df, columns=None, multiplier=1.5):
    """
    Detect outliers using IQR method
    
    IQR = Q3 - Q1
    Lower bound = Q1 - (multiplier × IQR)
    Upper bound = Q3 + (multiplier × IQR)
    
    Common multipliers:
    - 1.5: Standard (moderate outliers)
    - 3.0: Extreme outliers only
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to check
    multiplier : float
        IQR multiplier
    
    Returns:
    --------
    Dictionary with outlier information
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    outlier_info = {}
    
    for col in columns:
        # Calculate quartiles
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        
        # Calculate bounds
        lower_bound = Q1 - (multiplier * IQR)
        upper_bound = Q3 + (multiplier * IQR)
        
        # Identify outliers
        outliers = (df[col] < lower_bound) | (df[col] > upper_bound)
        outlier_count = outliers.sum()
        outlier_percentage = (outlier_count / len(df)) * 100
        
        outlier_info[col] = {
            'count': outlier_count,
            'percentage': outlier_percentage,
            'lower_bound': lower_bound,
            'upper_bound': upper_bound,
            'Q1': Q1,
            'Q3': Q3,
            'IQR': IQR,
            'outlier_indices': df[outliers].index.tolist(),
            'outlier_values': df.loc[outliers, col].tolist()
        }
        
        print(f"\n{col}:")
        print(f"  Q1: {Q1:.2f}, Q3: {Q3:.2f}, IQR: {IQR:.2f}")
        print(f"  Bounds: [{lower_bound:.2f}, {upper_bound:.2f}]")
        print(f"  Outliers: {outlier_count} ({outlier_percentage:.2f}%)")
        if outlier_count > 0:
            print(f"  Sample values: {df.loc[outliers, col].tolist()[:5]}")
    
    return outlier_info

# Detect outliers
outlier_info_iqr = detect_outliers_iqr(df, multiplier=1.5)

# Visualize IQR bounds
def visualize_iqr_bounds(df, column, multiplier=1.5):
    """
    Visualize IQR method on a single column
    """
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - (multiplier * IQR)
    upper_bound = Q3 + (multiplier * IQR)
    
    plt.figure(figsize=(12, 5))
    
    # Histogram with bounds
    plt.subplot(1, 2, 1)
    plt.hist(df[column], bins=50, edgecolor='black', alpha=0.7)
    plt.axvline(lower_bound, color='r', linestyle='--', label=f'Lower Bound ({lower_bound:.2f})')
    plt.axvline(upper_bound, color='r', linestyle='--', label=f'Upper Bound ({upper_bound:.2f})')
    plt.axvline(Q1, color='g', linestyle='--', label=f'Q1 ({Q1:.2f})')
    plt.axvline(Q3, color='g', linestyle='--', label=f'Q3 ({Q3:.2f})')
    plt.xlabel(column)
    plt.ylabel('Frequency')
    plt.title(f'{column} - IQR Method')
    plt.legend()
    
    # Box plot
    plt.subplot(1, 2, 2)
    plt.boxplot(df[column])
    plt.ylabel(column)
    plt.title(f'{column} - Box Plot')
    
    plt.tight_layout()
    plt.show()

visualize_iqr_bounds(df, 'salary')
When to Use IQR:

✅ Works with skewed data
✅ More robust than Z-score
✅ Good for general purpose outlier detection
✅ Works with non-normal distributions
Method 4: Isolation Forest (ML-based)
Python

from sklearn.ensemble import IsolationForest

def detect_outliers_isolation_forest(df, columns=None, contamination=0.1):
    """
    Detect outliers using Isolation Forest algorithm
    
    Isolation Forest is an unsupervised ML algorithm that:
    - Isolates outliers by randomly selecting features and split values
    - Outliers are easier to isolate (fewer splits needed)
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to use for detection
    contamination : float
        Expected proportion of outliers (0.0 to 0.5)
    
    Returns:
    --------
    Outlier predictions and scores
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    # Prepare data (handle missing values)
    X = df[columns].fillna(df[columns].median())
    
    # Train Isolation Forest
    iso_forest = IsolationForest(
        contamination=contamination,
        random_state=42,
        n_estimators=100
    )
    
    # Predict outliers (-1 = outlier, 1 = inlier)
    predictions = iso_forest.fit_predict(X)
    scores = iso_forest.score_samples(X)  # Lower score = more likely outlier
    
    # Create results dataframe
    results = pd.DataFrame({
        'is_outlier': predictions == -1,
        'outlier_score': scores
    }, index=df.index)
    
    outlier_count = (predictions == -1).sum()
    outlier_percentage = (outlier_count / len(df)) * 100
    
    print(f"Detected Outliers: {outlier_count} ({outlier_percentage:.2f}%)")
    print(f"\nColumns used: {list(columns)}")
    print(f"Contamination parameter: {contamination}")
    
    # Show some outlier examples
    outlier_indices = results[results['is_outlier']].index[:5]
    if len(outlier_indices) > 0:
        print(f"\nSample outliers:")
        print(df.loc[outlier_indices, columns])
    
    return results

# Detect outliers
outlier_results = detect_outliers_isolation_forest(df, contamination=0.05)

# Add results to dataframe
df['is_outlier_if'] = outlier_results['is_outlier']
df['outlier_score'] = outlier_results['outlier_score']

print("\nOutliers detected by Isolation Forest:")
print(df[df['is_outlier_if']][['age', 'salary', 'experience', 'outlier_score']].head(10))
When to Use Isolation Forest:

✅ High-dimensional data
✅ Complex outlier patterns
✅ Multivariate outlier detection
✅ No assumptions about data distribution
❌ Small datasets (needs sufficient data)
❌ When you need explainability (black box method)
Method 5: DBSCAN (Density-based)
Python

from sklearn.cluster import DBSCAN
from sklearn.preprocessing import StandardScaler

def detect_outliers_dbscan(df, columns=None, eps=0.5, min_samples=5):
    """
    Detect outliers using DBSCAN clustering
    
    DBSCAN identifies outliers as points that don't belong to any cluster
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to use
    eps : float
        Maximum distance between two samples to be considered neighbors
    min_samples : int
        Minimum number of samples in a neighborhood for a point to be considered core
    
    Returns:
    --------
    Cluster labels and outlier information
    """
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    # Prepare and scale data
    X = df[columns].fillna(df[columns].median())
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)
    
    # Apply DBSCAN
    dbscan = DBSCAN(eps=eps, min_samples=min_samples)
    clusters = dbscan.fit_predict(X_scaled)
    
    # -1 indicates outliers
    is_outlier = clusters == -1
    outlier_count = is_outlier.sum()
    outlier_percentage = (outlier_count / len(df)) * 100
    
    # Count clusters
    n_clusters = len(set(clusters)) - (1 if -1 in clusters else 0)
    
    print(f"Number of clusters: {n_clusters}")
    print(f"Outliers: {outlier_count} ({outlier_percentage:.2f}%)")
    print(f"\nParameters: eps={eps}, min_samples={min_samples}")
    
    results = pd.DataFrame({
        'cluster': clusters,
        'is_outlier': is_outlier
    }, index=df.index)
    
    return results

# Detect outliers
dbscan_results = detect_outliers_dbscan(df, eps=0.5, min_samples=5)

# Visualize (for 2D data)
def visualize_dbscan(df, col1, col2, results):
    """
    Visualize DBSCAN results for two columns
    """
    plt.figure(figsize=(10, 6))
    
    # Plot clusters
    scatter = plt.scatter(
        df[col1],
        df[col2],
        c=results['cluster'],
        cmap='viridis',
        alpha=0.6
    )
    
    # Highlight outliers
    outliers = results['is_outlier']
    plt.scatter(
        df.loc[outliers, col1],
        df.loc[outliers, col2],
        c='red',
        marker='x',
        s=100,
        label='Outliers'
    )
    
    plt.xlabel(col1)
    plt.ylabel(col2)
    plt.title('DBSCAN Outlier Detection')
    plt.colorbar(scatter, label='Cluster')
    plt.legend()
    plt.show()

visualize_dbscan(df, 'age', 'salary', dbscan_results)
When to Use DBSCAN:

✅ Clusters of varying density
✅ Non-spherical clusters
✅ Automatic outlier detection
❌ High-dimensional data (curse of dimensionality)
❌ Varying densities within clusters
8.3 Handling Outliers
Strategy 1: Removal
Python

def remove_outliers(df, method='iqr', columns=None, **kwargs):
    """
    Remove outliers from dataframe
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    method : str
        'zscore', 'iqr', 'isolation_forest', 'dbscan'
    columns : list
        Columns to check for outliers
    **kwargs : dict
        Method-specific parameters
    
    Returns:
    --------
    Cleaned DataFrame and removed rows
    """
    initial_rows = len(df)
    
    if method == 'zscore':
        threshold = kwargs.get('threshold', 3)
        mask = get_outlier_mask_zscore(df, columns, threshold)
    
    elif method == 'iqr':
        multiplier = kwargs.get('multiplier', 1.5)
        if columns is None:
            columns = df.select_dtypes(include=[np.number]).columns
        
        mask = pd.Series([False] * len(df), index=df.index)
        for col in columns:
            Q1 = df[col].quantile(0.25)
            Q3 = df[col].quantile(0.75)
            IQR = Q3 - Q1
            lower = Q1 - (multiplier * IQR)
            upper = Q3 + (multiplier * IQR)
            mask = mask | (df[col] < lower) | (df[col] > upper)
    
    elif method == 'isolation_forest':
        contamination = kwargs.get('contamination', 0.1)
        results = detect_outliers_isolation_forest(df, columns, contamination)
        mask = results['is_outlier']
    
    elif method == 'dbscan':
        eps = kwargs.get('eps', 0.5)
        min_samples = kwargs.get('min_samples', 5)
        results = detect_outliers_dbscan(df, columns, eps, min_samples)
        mask = results['is_outlier']
    
    # Remove outliers
    df_cleaned = df[~mask].copy()
    removed = df[mask].copy()
    
    final_rows = len(df_cleaned)
    removed_count = initial_rows - final_rows
    removed_percentage = (removed_count / initial_rows) * 100
    
    print(f"\nOutlier Removal Summary:")
    print(f"Initial rows: {initial_rows}")
    print(f"Removed rows: {removed_count} ({removed_percentage:.2f}%)")
    print(f"Remaining rows: {final_rows}")
    
    return df_cleaned, removed

# Example usage
df_cleaned, removed_outliers = remove_outliers(df, method='iqr', multiplier=1.5)
When to Remove Outliers:

✅ Data entry errors
✅ Measurement errors
✅ Large dataset (can afford to lose data)
✅ Outliers will harm model performance
❌ Small dataset
❌ Outliers are legitimate rare events
❌ Outliers contain important information
Strategy 2: Capping/Winsorization
Python

def cap_outliers(df, columns=None, method='iqr', **kwargs):
    """
    Cap outliers at boundary values instead of removing
    
    Also called Winsorization: replace outliers with boundary values
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to cap
    method : str
        'iqr', 'percentile', 'zscore'
    **kwargs : dict
        Method-specific parameters
    
    Returns:
    --------
    DataFrame with capped values
    """
    df_capped = df.copy()
    
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    for col in columns:
        if method == 'iqr':
            multiplier = kwargs.get('multiplier', 1.5)
            Q1 = df[col].quantile(0.25)
            Q3 = df[col].quantile(0.75)
            IQR = Q3 - Q1
            lower = Q1 - (multiplier * IQR)
            upper = Q3 + (multiplier * IQR)
        
        elif method == 'percentile':
            lower_percentile = kwargs.get('lower_percentile', 1)
            upper_percentile = kwargs.get('upper_percentile', 99)
            lower = df[col].quantile(lower_percentile / 100)
            upper = df[col].quantile(upper_percentile / 100)
        
        elif method == 'zscore':
            threshold = kwargs.get('threshold', 3)
            mean = df[col].mean()
            std = df[col].std()
            lower = mean - (threshold * std)
            upper = mean + (threshold * std)
        
        # Count capped values
        lower_capped = (df_capped[col] < lower).sum()
        upper_capped = (df_capped[col] > upper).sum()
        
        # Cap values
        df_capped[col] = df_capped[col].clip(lower=lower, upper=upper)
        
        if lower_capped > 0 or upper_capped > 0:
            print(f"{col}:")
            print(f"  Capped at lower bound ({lower:.2f}): {lower_capped} values")
            print(f"  Capped at upper bound ({upper:.2f}): {upper_capped} values")
    
    return df_capped

# Example usage
df_capped = cap_outliers(df, method='percentile', lower_percentile=1, upper_percentile=99)

# Compare before and after
print("\nBefore capping:")
print(df[['age', 'salary']].describe())

print("\nAfter capping:")
print(df_capped[['age', 'salary']].describe())
When to Cap Outliers:

✅ Want to keep all data points
✅ Outliers are real but extreme
✅ Need to preserve dataset size
✅ Reducing impact without removal
❌ Outliers are errors (better to remove)
Strategy 3: Transformation
Python

def transform_to_reduce_outliers(df, columns=None, method='log'):
    """
    Apply mathematical transformations to reduce outlier impact
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    columns : list
        Columns to transform
    method : str
        'log', 'sqrt', 'box-cox', 'yeo-johnson'
    
    Returns:
    --------
    Transformed DataFrame
    """
    df_transformed = df.copy()
    
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    for col in columns:
        if method == 'log':
            # Log transformation (requires positive values)
            min_val = df[col].min()
            if min_val <= 0:
                # Shift to make all values positive
                df_transformed[f'{col}_log'] = np.log1p(df[col] - min_val + 1)
                print(f"{col}: Applied log1p transformation (shifted)")
            else:
                df_transformed[f'{col}_log'] = np.log1p(df[col])
                print(f"{col}: Applied log1p transformation")
        
        elif method == 'sqrt':
            # Square root transformation
            min_val = df[col].min()
            if min_val < 0:
                df_transformed[f'{col}_sqrt'] = np.sqrt(df[col] - min_val)
                print(f"{col}: Applied sqrt transformation (shifted)")
            else:
                df_transformed[f'{col}_sqrt'] = np.sqrt(df[col])
                print(f"{col}: Applied sqrt transformation")
        
        elif method == 'box-cox':
            # Box-Cox transformation (requires positive values)
            from scipy import stats
            min_val = df[col].min()
            if min_val <= 0:
                data = df[col] - min_val + 1
            else:
                data = df[col]
            
            transformed, lambda_param = stats.boxcox(data)
            df_transformed[f'{col}_boxcox'] = transformed
            print(f"{col}: Applied Box-Cox transformation (λ={lambda_param:.3f})")
        
        elif method == 'yeo-johnson':
            # Yeo-Johnson (works with negative values)
            from sklearn.preprocessing import PowerTransformer
            pt = PowerTransformer(method='yeo-johnson')
            df_transformed[f'{col}_yj'] = pt.fit_transform(df[[col]])
            print(f"{col}: Applied Yeo-Johnson transformation")
    
    return df_transformed

# Example: Transform salary (often has outliers)
df_transformed = transform_to_reduce_outliers(df[['salary']], method='log')

# Visualize before and after
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

axes[0].hist(df['salary'], bins=50, edgecolor='black')
axes[0].set_title('Original Salary Distribution')
axes[0].set_xlabel('Salary')

axes[1].hist(df_transformed['salary_log'], bins=50, edgecolor='black')
axes[1].set_title('Log-Transformed Salary Distribution')
axes[1].set_xlabel('Log(Salary)')

plt.tight_layout()
plt.show()

# Compare statistics
print("\nOriginal salary:")
print(df['salary'].describe())

print("\nLog-transformed salary:")
print(df_transformed['salary_log'].describe())
Common Transformations:

Python

"""
1. LOG TRANSFORMATION
   Formula: log(x) or log(x + 1)
   Use: Right-skewed data, multiplicative relationships
   Example: Income, population, website traffic

2. SQUARE ROOT
   Formula: √x
   Use: Count data, right-skewed data (less aggressive than log)
   Example: Number of purchases, reviews

3. BOX-COX
   Formula: (x^λ - 1) / λ for λ ≠ 0, log(x) for λ = 0
   Use: Find optimal transformation automatically
   Limitation: Requires positive values

4. YEO-JOHNSON
   Formula: Similar to Box-Cox but works with negative values
   Use: General-purpose transformation
   Advantage: No positive value requirement
"""
Strategy 4: Binning/Discretization
Python

def bin_outliers(df, column, n_bins=5, strategy='quantile'):
    """
    Convert continuous variable to bins, reducing outlier impact
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    column : str
        Column to bin
    n_bins : int
        Number of bins
    strategy : str
        'uniform': Equal-width bins
        'quantile': Equal-frequency bins
        'kmeans': K-means clustering
    
    Returns:
    --------
    DataFrame with binned column
    """
    from sklearn.preprocessing import KBinsDiscretizer
    
    df_binned = df.copy()
    
    # Create discretizer
    discretizer = KBinsDiscretizer(
        n_bins=n_bins,
        encode='ordinal',
        strategy=strategy
    )
    
    # Fit and transform
    df_binned[f'{column}_binned'] = discretizer.fit_transform(
        df[[column]]
    ).astype(int)
    
    # Get bin edges
    bin_edges = discretizer.bin_edges_[0]
    
    print(f"\nBinning {column} into {n_bins} bins ({strategy} strategy):")
    for i in range(n_bins):
        lower = bin_edges[i]
        upper = bin_edges[i + 1]
        count = (df_binned[f'{column}_binned'] == i).sum()
        print(f"  Bin {i}: [{lower:.2f}, {upper:.2f}] - {count} values")
    
    return df_binned, bin_edges

# Example usage
df_binned, edges = bin_outliers(df, 'salary', n_bins=5, strategy='quantile')

# Visualize bins
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.hist(df['salary'], bins=50, edgecolor='black')
for edge in edges:
    plt.axvline(edge, color='r', linestyle='--', alpha=0.7)
plt.xlabel('Salary')
plt.ylabel('Frequency')
plt.title('Original Salary with Bin Edges')

plt.subplot(1, 2, 2)
df_binned['salary_binned'].value_counts().sort_index().plot(kind='bar')
plt.xlabel('Bin')
plt.ylabel('Count')
plt.title('Distribution Across Bins')

plt.tight_layout()
plt.show()
When to Use Binning:

✅ Want to reduce outlier impact
✅ Create categorical features from continuous
✅ Make model more robust
✅ Simplify relationships
❌ Lose granularity of information
❌ Need precise predictions
8.4 Comprehensive Outlier Handling Pipeline
Python

def handle_outliers_pipeline(df, config):
    """
    Comprehensive outlier handling pipeline
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Configuration dictionary:
        {
            'column_name': {
                'method': 'remove' | 'cap' | 'transform' | 'bin',
                'detection': 'iqr' | 'zscore' | 'isolation_forest',
                'params': {...}
            }
        }
    
    Returns:
    --------
    Cleaned DataFrame
    """
    print("="*60)
    print("OUTLIER HANDLING PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    initial_rows = len(df_cleaned)
    
    for col, settings in config.items():
        if col not in df_cleaned.columns:
            continue
        
        print(f"\n[Processing: {col}]")
        print(f"Method: {settings['method']}")
        
        if settings['method'] == 'remove':
            # Remove outliers
            detection = settings.get('detection', 'iqr')
            params = settings.get('params', {})
            
            if detection == 'iqr':
                Q1 = df_cleaned[col].quantile(0.25)
                Q3 = df_cleaned[col].quantile(0.75)
                IQR = Q3 - Q1
                multiplier = params.get('multiplier', 1.5)
                lower = Q1 - (multiplier * IQR)
                upper = Q3 + (multiplier * IQR)
                mask = (df_cleaned[col] >= lower) & (df_cleaned[col] <= upper)
            
            elif detection == 'zscore':
                threshold = params.get('threshold', 3)
                z_scores = np.abs((df_cleaned[col] - df_cleaned[col].mean()) / df_cleaned[col].std())
                mask = z_scores <= threshold
            
            removed = (~mask).sum()
            df_cleaned = df_cleaned[mask]
            print(f"Removed {removed} outliers")
        
        elif settings['method'] == 'cap':
            # Cap outliers
            params = settings.get('params', {})
            percentile_method = params.get('percentile_method', False)
            
            if percentile_method:
                lower_pct = params.get('lower_percentile', 1)
                upper_pct = params.get('upper_percentile', 99)
                lower = df_cleaned[col].quantile(lower_pct / 100)
                upper = df_cleaned[col].quantile(upper_pct / 100)
            else:
                Q1 = df_cleaned[col].quantile(0.25)
                Q3 = df_cleaned[col].quantile(0.75)
                IQR = Q3 - Q1
                multiplier = params.get('multiplier', 1.5)
                lower = Q1 - (multiplier * IQR)
                upper = Q3 + (multiplier * IQR)
            
            capped_lower = (df_cleaned[col] < lower).sum()
            capped_upper = (df_cleaned[col] > upper).sum()
            df_cleaned[col] = df_cleaned[col].clip(lower=lower, upper=upper)
            print(f"Capped {capped_lower} values at lower bound, {capped_upper} at upper bound")
        
        elif settings['method'] == 'transform':
            # Transform data
            transform_type = settings.get('transform_type', 'log')
            
            if transform_type == 'log':
                min_val = df_cleaned[col].min()
                if min_val <= 0:
                    df_cleaned[col] = np.log1p(df_cleaned[col] - min_val + 1)
                else:
                    df_cleaned[col] = np.log1p(df_cleaned[col])
                print(f"Applied log transformation")
            
            elif transform_type == 'sqrt':
                min_val = df_cleaned[col].min()
                if min_val < 0:
                    df_cleaned[col] = np.sqrt(df_cleaned[col] - min_val)
                else:
                    df_cleaned[col] = np.sqrt(df_cleaned[col])
                print(f"Applied sqrt transformation")
        
        elif settings['method'] == 'bin':
            # Bin data
            params = settings.get('params', {})
            n_bins = params.get('n_bins', 5)
            strategy = params.get('strategy', 'quantile')
            
            discretizer = KBinsDiscretizer(n_bins=n_bins, encode='ordinal', strategy=strategy)
            df_cleaned[f'{col}_binned'] = discretizer.fit_transform(df_cleaned[[col]]).astype(int)
            print(f"Created {n_bins} bins using {strategy} strategy")
    
    # Final summary
    final_rows = len(df_cleaned)
    rows_removed = initial_rows - final_rows
    
    print("\n" + "="*60)
    print("PIPELINE SUMMARY")
    print("="*60)
    print(f"Initial rows: {initial_rows}")
    print(f"Final rows: {final_rows}")
    print(f"Rows removed: {rows_removed}")
    print(f"Reduction: {(rows_removed/initial_rows)*100:.2f}%")
    print("="*60)
    
    return df_cleaned

# Example configuration
pipeline_config = {
    'age': {
        'method': 'cap',
        'params': {
            'percentile_method': True,
            'lower_percentile': 1,
            'upper_percentile': 99
        }
    },
    'salary': {
        'method': 'transform',
        'transform_type': 'log'
    },
    'experience': {
        'method': 'remove',
        'detection': 'iqr',
        'params': {
            'multiplier': 1.5
        }
    }
}

# Run pipeline
df_final = handle_outliers_pipeline(df, pipeline_config)
8.5 Outlier Handling Decision Framework
Python

def outlier_handling_advisor(df, column):
    """
    Provides recommendations for handling outliers in a specific column
    """
    print("="*60)
    print(f"OUTLIER HANDLING RECOMMENDATIONS FOR: {column}")
    print("="*60)
    
    # Basic statistics
    print("\nBasic Statistics:")
    print(df[column].describe())
    
    # Check distribution
    skewness = df[column].skew()
    print(f"\nSkewness: {skewness:.2f}")
    if abs(skewness) < 0.5:
        distribution = "Approximately Normal"
    elif skewness > 0:
        distribution = "Right-Skewed (positive skew)"
    else:
        distribution = "Left-Skewed (negative skew)"
    print(f"Distribution: {distribution}")
    
    # Detect outliers with different methods
    print("\nOutlier Detection Results:")
    
    # IQR method
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_iqr = Q1 - (1.5 * IQR)
    upper_iqr = Q3 + (1.5 * IQR)
    outliers_iqr = ((df[column] < lower_iqr) | (df[column] > upper_iqr)).sum()
    pct_iqr = (outliers_iqr / len(df)) * 100
    print(f"  IQR method: {outliers_iqr} outliers ({pct_iqr:.2f}%)")
    
    # Z-score method
    z_scores = np.abs((df[column] - df[column].mean()) / df[column].std())
    outliers_z = (z_scores > 3).sum()
    pct_z = (outliers_z / len(df)) * 100
    print(f"  Z-score method: {outliers_z} outliers ({pct_z:.2f}%)")
    
    # Recommendations
    print("\n" + "="*60)
    print("RECOMMENDATIONS:")
    print("="*60)
    
    if pct_iqr < 1:
        print("\n1. Very few outliers detected")
        print("   → Consider REMOVAL if they are data errors")
        print("   → Consider KEEPING if they are valid extreme values")
    
    elif pct_iqr < 5:
        print("\n1. Small percentage of outliers")
        print("   → REMOVAL: If errors or if model is sensitive (Linear Regression)")
        print("   → CAPPING: If want to preserve data points")
        print("   → TRANSFORMATION: If distribution is skewed")
    
    elif pct_iqr < 20:
        print("\n1. Moderate percentage of outliers")
        print("   → CAPPING (Winsorization) recommended")
        print("   → TRANSFORMATION if data is heavily skewed")
        print("   → Use robust models (Tree-based) that handle outliers")
    
    else:
        print("\n1. High percentage of outliers")
        print("   → Review data collection process")
        print("   → TRANSFORMATION recommended")
        print("   → BINNING to reduce impact")
        print("   → Use robust algorithms")
    
    if abs(skewness) > 1:
        print("\n2. Distribution is heavily skewed")
        print("   → LOG TRANSFORMATION recommended")
        print("   → BOX-COX or YEO-JOHNSON transformation")
    
    print("\n3. Method selection by use case:")
    print("   → Regression models: TRANSFORMATION or CAPPING")
    print("   → Tree-based models: Less sensitive, can keep outliers")
    print("   → Distance-based models (KNN): SCALING + CAPPING")
    print("   → Neural Networks: NORMALIZATION + CAPPING")
    
    print("="*60)

# Usage
outlier_handling_advisor(df, 'salary')


Data Cleaning: From Absolute Beginner to Advanced Expert (Part 2)
Continuing from Part 1...

9. Text Data Cleaning
9.1 Understanding Text Data Issues
Common Text Data Problems
Python

"""
TEXT DATA PROBLEMS:

1. INCONSISTENT CASE
   "John", "JOHN", "john" → Should be "John"

2. LEADING/TRAILING WHITESPACE
   "  John  " → "John"

3. EXTRA SPACES
   "John   Doe" → "John Doe"

4. SPECIAL CHARACTERS
   "John@#$" → "John"

5. HTML/XML TAGS
   "<p>John</p>" → "John"

6. ENCODING ISSUES
   "JohnÃ¢â‚¬â„¢s" → "John's"

7. TYPOS AND MISSPELLINGS
   "Jonh", "Jhon" → "John"

8. INCONSISTENT FORMATS
   "123-456-7890", "(123) 456-7890" → Standard format

9. ABBREVIATIONS
   "St.", "Street", "ST" → Standard format

10. NULL/EMPTY REPRESENTATIONS
    "N/A", "NA", "null", "" → Proper null
"""

import pandas as pd
import numpy as np
import re
import string

# Sample messy text data
data = {
    'customer_id': range(1, 11),
    'name': ['  John Doe  ', 'JANE SMITH', 'bob wilson', 'Alice   Brown', 
             'Charlie@#$', '<p>David Lee</p>', "Emma's Shop", 'Fank Miller',
             'NULL', 'N/A'],
    'email': ['john@email.com', 'JANE@EMAIL.COM', 'bob@email', 'alice@email.com',
              'charlie@@email.com', 'david@email.com', "emma's@email.com", 'frank@email.com',
              'null', 'n/a'],
    'phone': ['123-456-7890', '(234) 567-8901', '345.567.8901', '456 567 8901',
              '5675678901', '+1-678-567-8901', '789-567-890', 'abc-def-ghij',
              'NA', ''],
    'address': ['123 Main St.', '456 Oak Street', '789 Pine ST', '321 Elm STREET',
                '654 Maple Ave.', '987 Cedar Avenue', '147 Birch AVE', '258 Walnut Dr.',
                'N/A', 'unknown'],
    'description': ['Great customer! 5 stars', 'good customer...', 'EXCELLENT!!!',
                    'Regular buyer', 'Has issues   with   payments', '<b>VIP</b> customer',
                    'Bought 100+ items', 'New customer (2023)', 'null', '']
}

df = pd.DataFrame(data)
print("Original messy data:")
print(df)
9.2 Basic Text Cleaning Operations
Whitespace Handling
Python

# Strip leading and trailing whitespace
df['name_cleaned'] = df['name'].str.strip()

# Remove extra spaces between words
df['name_cleaned'] = df['name_cleaned'].str.replace(r'\s+', ' ', regex=True)

# Comprehensive whitespace function
def clean_whitespace(series):
    """
    Remove all types of whitespace issues
    """
    cleaned = series.copy()
    
    # Convert to string type
    cleaned = cleaned.astype(str)
    
    # Strip leading/trailing whitespace
    cleaned = cleaned.str.strip()
    
    # Replace multiple spaces with single space
    cleaned = cleaned.str.replace(r'\s+', ' ', regex=True)
    
    # Replace various whitespace characters (tabs, newlines)
    cleaned = cleaned.str.replace(r'[\t\n\r\f\v]', ' ', regex=True)
    
    return cleaned

df['name_ws_cleaned'] = clean_whitespace(df['name'])
print("\nAfter whitespace cleaning:")
print(df[['name', 'name_ws_cleaned']])
Case Normalization
Python

# Lower case
df['name_lower'] = df['name'].str.lower()

# Upper case
df['name_upper'] = df['name'].str.upper()

# Title case (first letter capitalized)
df['name_title'] = df['name'].str.title()

# Capitalize (first letter of first word)
df['name_capitalize'] = df['name'].str.capitalize()

# Custom case function for names
def normalize_name_case(series):
    """
    Properly capitalize names
    Handles: "john doe" → "John Doe"
    """
    # First clean whitespace
    cleaned = clean_whitespace(series)
    
    # Apply title case
    cleaned = cleaned.str.title()
    
    # Handle special cases (McDonald, O'Brien, etc.)
    def fix_special_names(name):
        if pd.isna(name):
            return name
        
        # Handle Mc/Mac names
        name = re.sub(r'\b(Mc|Mac)([a-z])', lambda m: m.group(1) + m.group(2).upper(), name)
        
        # Handle O' names
        name = re.sub(r"\b(O')([a-z])", lambda m: m.group(1) + m.group(2).upper(), name)
        
        return name
    
    cleaned = cleaned.apply(fix_special_names)
    
    return cleaned

df['name_proper'] = normalize_name_case(df['name'])
print("\nAfter case normalization:")
print(df[['name', 'name_proper']])
Removing Special Characters
Python

def remove_special_characters(series, keep_chars=''):
    """
    Remove special characters from text
    
    Parameters:
    -----------
    series : pd.Series
        Input series
    keep_chars : str
        Characters to keep (in addition to alphanumeric and space)
    
    Returns:
    --------
    Cleaned series
    """
    cleaned = series.astype(str)
    
    # Build pattern of characters to keep
    # Keep alphanumeric, space, and specified additional characters
    pattern = f'[^a-zA-Z0-9\\s{re.escape(keep_chars)}]'
    
    cleaned = cleaned.str.replace(pattern, '', regex=True)
    
    # Clean up resulting whitespace
    cleaned = cleaned.str.replace(r'\s+', ' ', regex=True).str.strip()
    
    return cleaned

# Remove all special characters
df['name_no_special'] = remove_special_characters(df['name'])

# Keep specific characters (apostrophe for names like O'Brien)
df['name_keep_apostrophe'] = remove_special_characters(df['name'], keep_chars="'")

print("\nAfter removing special characters:")
print(df[['name', 'name_no_special', 'name_keep_apostrophe']])

# More specific character removal functions
def remove_punctuation(series):
    """Remove all punctuation"""
    return series.str.replace(f'[{re.escape(string.punctuation)}]', '', regex=True)

def remove_digits(series):
    """Remove all digits"""
    return series.str.replace(r'\d+', '', regex=True)

def keep_only_letters(series):
    """Keep only letters and spaces"""
    return series.str.replace(r'[^a-zA-Z\s]', '', regex=True)

# Test
print("\nDifferent removal methods:")
test_text = pd.Series(["Hello123! World@#$ 456"])
print(f"Original: {test_text.values[0]}")
print(f"Remove punctuation: {remove_punctuation(test_text).values[0]}")
print(f"Remove digits: {remove_digits(test_text).values[0]}")
print(f"Keep only letters: {keep_only_letters(test_text).values[0]}")
Removing HTML Tags
Python

def remove_html_tags(series):
    """
    Remove HTML/XML tags from text
    """
    cleaned = series.astype(str)
    
    # Remove HTML tags
    cleaned = cleaned.str.replace(r'<[^>]+>', '', regex=True)
    
    # Decode common HTML entities
    html_entities = {
        '&nbsp;': ' ',
        '&amp;': '&',
        '&lt;': '<',
        '&gt;': '>',
        '&quot;': '"',
        '&#39;': "'",
        '&apos;': "'",
    }
    
    for entity, char in html_entities.items():
        cleaned = cleaned.str.replace(entity, char, regex=False)
    
    # Clean whitespace
    cleaned = cleaned.str.replace(r'\s+', ' ', regex=True).str.strip()
    
    return cleaned

df['name_no_html'] = remove_html_tags(df['name'])
df['description_no_html'] = remove_html_tags(df['description'])

print("\nAfter removing HTML tags:")
print(df[['name', 'name_no_html']])
print(df[['description', 'description_no_html']])

# More comprehensive HTML cleaning using BeautifulSoup
def remove_html_tags_advanced(series):
    """
    Remove HTML tags using BeautifulSoup (more robust)
    """
    try:
        from bs4 import BeautifulSoup
        
        def clean_html(text):
            if pd.isna(text):
                return text
            soup = BeautifulSoup(str(text), 'html.parser')
            return soup.get_text(separator=' ').strip()
        
        return series.apply(clean_html)
    
    except ImportError:
        print("BeautifulSoup not installed. Using regex method.")
        return remove_html_tags(series)

# Test
html_text = pd.Series(["<div><p>Hello <b>World</b></p>&nbsp;&amp; Welcome!</div>"])
print(f"\nHTML cleaning test:")
print(f"Original: {html_text.values[0]}")
print(f"Cleaned: {remove_html_tags(html_text).values[0]}")
9.3 Handling Null Representations in Text
Python

def standardize_nulls(series, null_values=None):
    """
    Convert various null representations to proper NaN
    
    Parameters:
    -----------
    series : pd.Series
        Input series
    null_values : list
        List of values to treat as null
    
    Returns:
    --------
    Series with standardized nulls
    """
    if null_values is None:
        null_values = [
            'null', 'NULL', 'Null',
            'none', 'NONE', 'None',
            'na', 'NA', 'N/A', 'n/a', 'N/a',
            'nan', 'NaN', 'NAN',
            'nil', 'NIL', 'Nil',
            '', ' ',
            'unknown', 'Unknown', 'UNKNOWN',
            'undefined', 'Undefined', 'UNDEFINED',
            '-', '--', '---',
            '.', '..', '...',
            '?', '??',
            'missing', 'Missing', 'MISSING',
            'not available', 'Not Available',
            'not applicable', 'Not Applicable'
        ]
    
    cleaned = series.copy()
    
    # Convert to string for comparison
    cleaned_str = cleaned.astype(str).str.strip()
    
    # Replace null representations with NaN
    mask = cleaned_str.isin(null_values)
    cleaned.loc[mask] = np.nan
    
    # Also check for empty strings after stripping
    mask_empty = cleaned_str == ''
    cleaned.loc[mask_empty] = np.nan
    
    return cleaned

# Apply to all text columns
text_columns = df.select_dtypes(include=['object']).columns
for col in text_columns:
    df[f'{col}_null_std'] = standardize_nulls(df[col])

print("\nAfter standardizing nulls:")
print(df[['name', 'name_null_std', 'email', 'email_null_std']].tail())
9.4 Email Validation and Cleaning
Python

def clean_and_validate_email(series):
    """
    Clean and validate email addresses
    
    Returns:
    - Cleaned email
    - Validity flag
    - Error message
    """
    results = pd.DataFrame(index=series.index)
    
    # Basic email pattern
    email_pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    
    cleaned_emails = []
    is_valid = []
    error_messages = []
    
    for idx, email in series.items():
        if pd.isna(email):
            cleaned_emails.append(np.nan)
            is_valid.append(False)
            error_messages.append('Missing value')
            continue
        
        # Convert to string and clean
        email_str = str(email).strip().lower()
        
        # Check for null representations
        if email_str in ['null', 'na', 'n/a', 'none', '']:
            cleaned_emails.append(np.nan)
            is_valid.append(False)
            error_messages.append('Null representation')
            continue
        
        # Remove extra @ symbols
        if email_str.count('@') > 1:
            # Keep first @ only
            parts = email_str.split('@')
            email_str = parts[0] + '@' + ''.join(parts[1:])
        
        # Validate email format
        if re.match(email_pattern, email_str):
            cleaned_emails.append(email_str)
            is_valid.append(True)
            error_messages.append('')
        else:
            cleaned_emails.append(email_str)
            is_valid.append(False)
            
            # Determine error type
            if '@' not in email_str:
                error_messages.append('Missing @ symbol')
            elif '.' not in email_str.split('@')[-1]:
                error_messages.append('Invalid domain')
            elif email_str.startswith('.') or email_str.endswith('.'):
                error_messages.append('Invalid format')
            else:
                error_messages.append('Invalid format')
    
    results['email_cleaned'] = cleaned_emails
    results['email_valid'] = is_valid
    results['email_error'] = error_messages
    
    # Print summary
    valid_count = sum(is_valid)
    print(f"Email Validation Summary:")
    print(f"  Valid: {valid_count} ({(valid_count/len(series))*100:.1f}%)")
    print(f"  Invalid: {len(series) - valid_count} ({((len(series) - valid_count)/len(series))*100:.1f}%)")
    
    return results

# Apply email cleaning
email_results = clean_and_validate_email(df['email'])
df = pd.concat([df, email_results], axis=1)

print("\nEmail cleaning results:")
print(df[['email', 'email_cleaned', 'email_valid', 'email_error']])
9.5 Phone Number Cleaning
Python

def clean_phone_number(series, country_code='+1', format_type='standard'):
    """
    Clean and standardize phone numbers
    
    Parameters:
    -----------
    series : pd.Series
        Input series with phone numbers
    country_code : str
        Default country code
    format_type : str
        'standard': (XXX) XXX-XXXX
        'dashes': XXX-XXX-XXXX
        'dots': XXX.XXX.XXXX
        'compact': XXXXXXXXXX
        'international': +1 XXX XXX XXXX
    
    Returns:
    --------
    DataFrame with cleaned phone and validity
    """
    results = pd.DataFrame(index=series.index)
    
    cleaned_phones = []
    is_valid = []
    
    for idx, phone in series.items():
        if pd.isna(phone):
            cleaned_phones.append(np.nan)
            is_valid.append(False)
            continue
        
        phone_str = str(phone).strip().upper()
        
        # Check for null representations
        if phone_str in ['NULL', 'NA', 'N/A', 'NONE', '', '-']:
            cleaned_phones.append(np.nan)
            is_valid.append(False)
            continue
        
        # Extract only digits
        digits = re.sub(r'\D', '', phone_str)
        
        # Remove country code if present (assuming US)
        if len(digits) == 11 and digits.startswith('1'):
            digits = digits[1:]
        
        # Check if valid length
        if len(digits) != 10:
            cleaned_phones.append(phone_str)  # Return original
            is_valid.append(False)
            continue
        
        # Format the number
        area = digits[:3]
        exchange = digits[3:6]
        subscriber = digits[6:]
        
        if format_type == 'standard':
            formatted = f"({area}) {exchange}-{subscriber}"
        elif format_type == 'dashes':
            formatted = f"{area}-{exchange}-{subscriber}"
        elif format_type == 'dots':
            formatted = f"{area}.{exchange}.{subscriber}"
        elif format_type == 'compact':
            formatted = digits
        elif format_type == 'international':
            formatted = f"{country_code} {area} {exchange} {subscriber}"
        else:
            formatted = f"({area}) {exchange}-{subscriber}"
        
        cleaned_phones.append(formatted)
        is_valid.append(True)
    
    results['phone_cleaned'] = cleaned_phones
    results['phone_valid'] = is_valid
    
    # Print summary
    valid_count = sum(is_valid)
    print(f"Phone Validation Summary:")
    print(f"  Valid: {valid_count} ({(valid_count/len(series))*100:.1f}%)")
    print(f"  Invalid: {len(series) - valid_count}")
    
    return results

# Apply phone cleaning
phone_results = clean_phone_number(df['phone'], format_type='standard')
df = pd.concat([df, phone_results], axis=1)

print("\nPhone cleaning results:")
print(df[['phone', 'phone_cleaned', 'phone_valid']])
9.6 Address Standardization
Python

def standardize_address(series):
    """
    Standardize address format
    - Expand abbreviations
    - Consistent capitalization
    - Standard formatting
    """
    # Common address abbreviations
    abbreviations = {
        # Street types
        r'\bSt\.?\b': 'Street',
        r'\bStr\.?\b': 'Street',
        r'\bAve\.?\b': 'Avenue',
        r'\bBlvd\.?\b': 'Boulevard',
        r'\bDr\.?\b': 'Drive',
        r'\bLn\.?\b': 'Lane',
        r'\bRd\.?\b': 'Road',
        r'\bCt\.?\b': 'Court',
        r'\bPl\.?\b': 'Place',
        r'\bCir\.?\b': 'Circle',
        r'\bPkwy\.?\b': 'Parkway',
        r'\bHwy\.?\b': 'Highway',
        r'\bTer\.?\b': 'Terrace',
        r'\bWay\.?\b': 'Way',
        
        # Directions
        r'\bN\.?\b': 'North',
        r'\bS\.?\b': 'South',
        r'\bE\.?\b': 'East',
        r'\bW\.?\b': 'West',
        r'\bNE\.?\b': 'Northeast',
        r'\bNW\.?\b': 'Northwest',
        r'\bSE\.?\b': 'Southeast',
        r'\bSW\.?\b': 'Southwest',
        
        # Units
        r'\bApt\.?\b': 'Apartment',
        r'\bSte\.?\b': 'Suite',
        r'\bFlr\.?\b': 'Floor',
        r'\bBldg\.?\b': 'Building',
        r'\b#\b': 'Unit ',
    }
    
    cleaned = series.astype(str)
    
    # Standardize nulls first
    cleaned = standardize_nulls(cleaned)
    
    # Process non-null values
    def process_address(addr):
        if pd.isna(addr):
            return addr
        
        addr = str(addr).strip()
        
        # Apply abbreviation expansions (case-insensitive)
        for pattern, replacement in abbreviations.items():
            addr = re.sub(pattern, replacement, addr, flags=re.IGNORECASE)
        
        # Title case
        addr = addr.title()
        
        # Clean whitespace
        addr = re.sub(r'\s+', ' ', addr).strip()
        
        return addr
    
    return cleaned.apply(process_address)

# Apply address standardization
df['address_std'] = standardize_address(df['address'])

print("\nAddress standardization:")
print(df[['address', 'address_std']])
9.7 Text Normalization for NLP/ML
Python

import string
import unicodedata

def normalize_text_for_ml(series, config=None):
    """
    Comprehensive text normalization for ML/NLP
    
    Parameters:
    -----------
    series : pd.Series
        Input text series
    config : dict
        Configuration options:
        - lowercase: bool
        - remove_punctuation: bool
        - remove_numbers: bool
        - remove_stopwords: bool
        - lemmatize: bool
        - remove_accents: bool
    
    Returns:
    --------
    Normalized text series
    """
    if config is None:
        config = {
            'lowercase': True,
            'remove_punctuation': True,
            'remove_numbers': False,
            'remove_stopwords': True,
            'lemmatize': False,
            'remove_accents': True,
            'min_word_length': 2
        }
    
    cleaned = series.astype(str).copy()
    
    # Remove HTML tags
    cleaned = cleaned.str.replace(r'<[^>]+>', '', regex=True)
    
    # Remove URLs
    cleaned = cleaned.str.replace(r'http\S+|www\.\S+', '', regex=True)
    
    # Remove email addresses
    cleaned = cleaned.str.replace(r'\S+@\S+', '', regex=True)
    
    # Remove accents/diacritics
    if config.get('remove_accents', True):
        def remove_accents(text):
            if pd.isna(text):
                return text
            # Normalize to NFD form and remove combining characters
            normalized = unicodedata.normalize('NFD', text)
            return ''.join(char for char in normalized 
                          if unicodedata.category(char) != 'Mn')
        cleaned = cleaned.apply(remove_accents)
    
    # Lowercase
    if config.get('lowercase', True):
        cleaned = cleaned.str.lower()
    
    # Remove punctuation
    if config.get('remove_punctuation', True):
        cleaned = cleaned.str.replace(f'[{re.escape(string.punctuation)}]', ' ', regex=True)
    
    # Remove numbers
    if config.get('remove_numbers', False):
        cleaned = cleaned.str.replace(r'\d+', '', regex=True)
    
    # Remove stopwords
    if config.get('remove_stopwords', True):
        try:
            from nltk.corpus import stopwords
            stop_words = set(stopwords.words('english'))
        except:
            # Basic stopwords if NLTK not available
            stop_words = {'the', 'a', 'an', 'is', 'are', 'was', 'were', 'be', 'been',
                         'being', 'have', 'has', 'had', 'do', 'does', 'did', 'will',
                         'would', 'could', 'should', 'may', 'might', 'must', 'shall',
                         'can', 'need', 'dare', 'ought', 'used', 'to', 'of', 'in',
                         'for', 'on', 'with', 'at', 'by', 'from', 'as', 'into',
                         'through', 'during', 'before', 'after', 'above', 'below',
                         'between', 'under', 'again', 'further', 'then', 'once',
                         'and', 'but', 'or', 'nor', 'so', 'yet', 'both', 'either',
                         'neither', 'not', 'only', 'own', 'same', 'than', 'too',
                         'very', 'just', 'i', 'me', 'my', 'myself', 'we', 'our',
                         'ours', 'ourselves', 'you', 'your', 'yours', 'yourself',
                         'he', 'him', 'his', 'himself', 'she', 'her', 'hers',
                         'herself', 'it', 'its', 'itself', 'they', 'them', 'their',
                         'theirs', 'themselves', 'what', 'which', 'who', 'whom',
                         'this', 'that', 'these', 'those', 'am'}
        
        def remove_stopwords_func(text):
            if pd.isna(text):
                return text
            words = text.split()
            return ' '.join(word for word in words if word.lower() not in stop_words)
        
        cleaned = cleaned.apply(remove_stopwords_func)
    
    # Lemmatization
    if config.get('lemmatize', False):
        try:
            from nltk.stem import WordNetLemmatizer
            lemmatizer = WordNetLemmatizer()
            
            def lemmatize_text(text):
                if pd.isna(text):
                    return text
                words = text.split()
                return ' '.join(lemmatizer.lemmatize(word) for word in words)
            
            cleaned = cleaned.apply(lemmatize_text)
        except ImportError:
            print("NLTK not available for lemmatization")
    
    # Remove short words
    min_length = config.get('min_word_length', 2)
    if min_length > 1:
        def remove_short_words(text):
            if pd.isna(text):
                return text
            words = text.split()
            return ' '.join(word for word in words if len(word) >= min_length)
        cleaned = cleaned.apply(remove_short_words)
    
    # Clean extra whitespace
    cleaned = cleaned.str.replace(r'\s+', ' ', regex=True).str.strip()
    
    return cleaned

# Apply text normalization for ML
df['description_ml'] = normalize_text_for_ml(df['description'])

print("\nText normalization for ML:")
print(df[['description', 'description_ml']])
9.8 Fuzzy String Matching and Deduplication
Python

def find_and_fix_typos(series, reference_list=None, threshold=85):
    """
    Find and fix potential typos using fuzzy matching
    
    Parameters:
    -----------
    series : pd.Series
        Input series with potentially misspelled values
    reference_list : list
        List of correct values to match against
    threshold : int
        Minimum similarity score (0-100)
    
    Returns:
    --------
    Series with corrected values and correction log
    """
    from difflib import SequenceMatcher
    
    def similarity(a, b):
        return SequenceMatcher(None, a.lower(), b.lower()).ratio() * 100
    
    # If no reference list, use most frequent values
    if reference_list is None:
        value_counts = series.value_counts()
        # Use values that appear more than once as reference
        reference_list = value_counts[value_counts > 1].index.tolist()
        if len(reference_list) == 0:
            reference_list = series.unique().tolist()[:10]
    
    corrections = {}
    corrected_series = series.copy()
    
    unique_values = series.dropna().unique()
    
    for value in unique_values:
        if value in reference_list:
            continue
        
        # Find best match in reference list
        best_match = None
        best_score = 0
        
        for ref in reference_list:
            score = similarity(str(value), str(ref))
            if score > best_score and score >= threshold and score < 100:
                best_score = score
                best_match = ref
        
        if best_match:
            corrections[value] = {
                'corrected_to': best_match,
                'similarity': best_score
            }
            corrected_series = corrected_series.replace(value, best_match)
    
    # Print correction log
    if corrections:
        print("Corrections made:")
        for original, info in corrections.items():
            print(f"  '{original}' → '{info['corrected_to']}' (similarity: {info['similarity']:.1f}%)")
    else:
        print("No corrections needed")
    
    return corrected_series, corrections

# Example: Fix name typos
correct_names = ['John Doe', 'Jane Smith', 'Bob Wilson', 'Alice Brown', 
                 'Charlie Davis', 'David Lee', 'Emma Wilson', 'Frank Miller']

df['name_fixed'], name_corrections = find_and_fix_typos(
    normalize_name_case(df['name']), 
    reference_list=correct_names,
    threshold=80
)

print("\nName corrections:")
print(df[['name', 'name_fixed']])
9.9 Comprehensive Text Cleaning Pipeline
Python

def text_cleaning_pipeline(df, config):
    """
    Comprehensive text cleaning pipeline
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Configuration for each column:
        {
            'column_name': {
                'type': 'name' | 'email' | 'phone' | 'address' | 'text' | 'general',
                'operations': ['whitespace', 'case', 'special', 'html', 'nulls'],
                'custom_params': {...}
            }
        }
    
    Returns:
    --------
    Cleaned DataFrame
    """
    print("="*60)
    print("TEXT CLEANING PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    
    for col, settings in config.items():
        if col not in df_cleaned.columns:
            continue
        
        print(f"\n[Processing: {col}]")
        print(f"Type: {settings.get('type', 'general')}")
        
        col_type = settings.get('type', 'general')
        operations = settings.get('operations', ['whitespace', 'nulls'])
        
        # Create working copy
        cleaned = df_cleaned[col].copy()
        
        # Apply standard operations
        if 'nulls' in operations:
            cleaned = standardize_nulls(cleaned)
            print("  ✓ Standardized null values")
        
        if 'whitespace' in operations:
            cleaned = clean_whitespace(cleaned)
            print("  ✓ Cleaned whitespace")
        
        if 'html' in operations:
            cleaned = remove_html_tags(cleaned)
            print("  ✓ Removed HTML tags")
        
        if 'special' in operations:
            keep_chars = settings.get('custom_params', {}).get('keep_chars', "'")
            cleaned = remove_special_characters(cleaned, keep_chars=keep_chars)
            print(f"  ✓ Removed special characters")
        
        if 'case' in operations:
            case_type = settings.get('custom_params', {}).get('case_type', 'title')
            if case_type == 'lower':
                cleaned = cleaned.str.lower()
            elif case_type == 'upper':
                cleaned = cleaned.str.upper()
            elif case_type == 'title':
                cleaned = cleaned.str.title()
            print(f"  ✓ Applied {case_type} case")
        
        # Apply type-specific cleaning
        if col_type == 'name':
            cleaned = normalize_name_case(cleaned)
            print("  ✓ Applied name normalization")
        
        elif col_type == 'email':
            email_results = clean_and_validate_email(cleaned)
            df_cleaned[f'{col}_cleaned'] = email_results['email_cleaned']
            df_cleaned[f'{col}_valid'] = email_results['email_valid']
            print("  ✓ Validated and cleaned emails")
            continue
        
        elif col_type == 'phone':
            phone_format = settings.get('custom_params', {}).get('format', 'standard')
            phone_results = clean_phone_number(cleaned, format_type=phone_format)
            df_cleaned[f'{col}_cleaned'] = phone_results['phone_cleaned']
            df_cleaned[f'{col}_valid'] = phone_results['phone_valid']
            print("  ✓ Validated and cleaned phones")
            continue
        
        elif col_type == 'address':
            cleaned = standardize_address(cleaned)
            print("  ✓ Standardized addresses")
        
        elif col_type == 'text':
            ml_config = settings.get('custom_params', {}).get('ml_config', {})
            cleaned = normalize_text_for_ml(cleaned, ml_config)
            print("  ✓ Normalized text for ML")
        
        # Store cleaned column
        df_cleaned[f'{col}_cleaned'] = cleaned
    
    print("\n" + "="*60)
    print("PIPELINE COMPLETE")
    print("="*60)
    
    return df_cleaned

# Define pipeline configuration
pipeline_config = {
    'name': {
        'type': 'name',
        'operations': ['nulls', 'whitespace', 'html', 'case']
    },
    'email': {
        'type': 'email',
        'operations': ['nulls']
    },
    'phone': {
        'type': 'phone',
        'operations': ['nulls'],
        'custom_params': {'format': 'standard'}
    },
    'address': {
        'type': 'address',
        'operations': ['nulls', 'whitespace']
    },
    'description': {
        'type': 'text',
        'operations': ['nulls', 'whitespace', 'html'],
        'custom_params': {
            'ml_config': {
                'lowercase': True,
                'remove_punctuation': True,
                'remove_stopwords': True
            }
        }
    }
}

# Run pipeline
df_final = text_cleaning_pipeline(df, pipeline_config)

print("\nFinal cleaned data:")
print(df_final.head())
10. Date and Time Data Cleaning
10.1 Understanding Date/Time Issues
Python

"""
COMMON DATE/TIME DATA ISSUES:

1. INCONSISTENT FORMATS
   - "2023-01-15", "01/15/2023", "15-Jan-2023"

2. TIMEZONE ISSUES
   - Data from multiple time zones
   - Missing timezone information

3. INVALID DATES
   - "2023-02-30" (February 30 doesn't exist)
   - "2023-13-01" (Month 13)

4. FUTURE DATES (when they shouldn't be)
   - Birth date in 2050

5. UNREALISTIC DATES
   - Birth date in 1800 for current customer

6. MIXED FORMATS
   - Same column has multiple formats

7. MISSING COMPONENTS
   - Date without year
   - Time without timezone

8. AMBIGUOUS FORMATS
   - "01/02/2023" - Is it Jan 2 or Feb 1?
"""

import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import pytz

# Sample messy date data
data = {
    'id': range(1, 11),
    'date_iso': ['2023-01-15', '2023-02-20', '2023-03-25', '2023-04-10', 
                 '2023-05-30', '2023-06-15', 'Invalid', '2023-08-20',
                 '2050-01-01', '1800-01-01'],
    'date_us': ['01/15/2023', '02/20/2023', 'March 25, 2023', '04-10-2023',
                '05.30.2023', 'Jun 15, 2023', '07/20/23', '08/20/2023',
                '09/30/2023', 'N/A'],
    'date_eu': ['15/01/2023', '20/02/2023', '25/03/2023', '10/04/2023',
                '30/05/2023', '15/06/2023', '20/07/2023', '20/08/2023',
                '30/09/2023', '01/10/2023'],
    'timestamp': ['2023-01-15 14:30:00', '2023-02-20 09:15:00+00:00',
                  '2023-03-25T18:45:00', '2023-04-10 12:00:00 EST',
                  '2023-05-30 16:20:00.123', None, 'Invalid Time',
                  '2023-08-20 10:00:00', '2023-09-25 11:30:00', '2023-10-30 08:00:00'],
    'birth_date': ['1990-05-15', '1985-08-22', '1970-12-01', '2025-06-10',
                   '1850-01-01', '1995-03-17', '2000-11-25', '1988-07-04',
                   '1992-09-30', '1975-02-28']
}

df = pd.DataFrame(data)
print("Original date data:")
print(df)
10.2 Parsing Various Date Formats
Python

def parse_dates_robust(series, formats=None, dayfirst=False, yearfirst=True):
    """
    Robustly parse dates from various formats
    
    Parameters:
    -----------
    series : pd.Series
        Input series with date strings
    formats : list
        List of datetime formats to try
    dayfirst : bool
        Whether to interpret first number as day
    yearfirst : bool
        Whether to interpret first number as year
    
    Returns:
    --------
    Parsed datetime series and parsing report
    """
    if formats is None:
        formats = [
            '%Y-%m-%d',           # 2023-01-15
            '%m/%d/%Y',           # 01/15/2023
            '%d/%m/%Y',           # 15/01/2023
            '%Y-%m-%d %H:%M:%S',  # 2023-01-15 14:30:00
            '%m-%d-%Y',           # 01-15-2023
            '%d-%m-%Y',           # 15-01-2023
            '%B %d, %Y',          # January 15, 2023
            '%b %d, %Y',          # Jan 15, 2023
            '%Y/%m/%d',           # 2023/01/15
            '%m.%d.%Y',           # 01.15.2023
            '%d.%m.%Y',           # 15.01.2023
            '%Y%m%d',             # 20230115
            '%m/%d/%y',           # 01/15/23
            '%d/%m/%y',           # 15/01/23
        ]
    
    parsed_dates = []
    parsing_info = []
    
    for idx, value in series.items():
        if pd.isna(value):
            parsed_dates.append(pd.NaT)
            parsing_info.append({'status': 'null', 'format': None})
            continue
        
        value_str = str(value).strip()
        
        # Check for null representations
        if value_str.lower() in ['null', 'na', 'n/a', 'none', '', 'invalid']:
            parsed_dates.append(pd.NaT)
            parsing_info.append({'status': 'null_repr', 'format': None})
            continue
        
        # Try each format
        parsed = None
        used_format = None
        
        for fmt in formats:
            try:
                parsed = datetime.strptime(value_str, fmt)
                used_format = fmt
                break
            except ValueError:
                continue
        
        # If no format worked, try pandas parser
        if parsed is None:
            try:
                parsed = pd.to_datetime(value_str, dayfirst=dayfirst, yearfirst=yearfirst)
                used_format = 'pandas_auto'
            except:
                parsed = pd.NaT
                used_format = None
        
        parsed_dates.append(parsed)
        parsing_info.append({
            'status': 'success' if pd.notna(parsed) else 'failed',
            'format': used_format,
            'original': value_str
        })
    
    result = pd.Series(parsed_dates, index=series.index)
    result = pd.to_datetime(result)
    
    # Parsing report
    info_df = pd.DataFrame(parsing_info, index=series.index)
    success_count = (info_df['status'] == 'success').sum()
    
    print(f"Parsing Summary:")
    print(f"  Total: {len(series)}")
    print(f"  Successful: {success_count} ({success_count/len(series)*100:.1f}%)")
    print(f"  Failed: {len(series) - success_count}")
    
    # Show format distribution
    print(f"\nFormats used:")
    format_counts = info_df[info_df['status'] == 'success']['format'].value_counts()
    for fmt, count in format_counts.items():
        print(f"  {fmt}: {count}")
    
    return result, info_df

# Parse different date columns
df['date_iso_parsed'], _ = parse_dates_robust(df['date_iso'])
df['date_us_parsed'], _ = parse_dates_robust(df['date_us'], dayfirst=False)
df['date_eu_parsed'], _ = parse_dates_robust(df['date_eu'], dayfirst=True)

print("\nParsed dates:")
print(df[['date_iso', 'date_iso_parsed', 'date_us', 'date_us_parsed']].head())
10.3 Validating Dates
Python

def validate_dates(series, rules=None):
    """
    Validate dates against various rules
    
    Parameters:
    -----------
    series : pd.Series
        Datetime series
    rules : dict
        Validation rules:
        - min_date: earliest allowed date
        - max_date: latest allowed date
        - no_future: bool, if True, no future dates allowed
        - no_weekends: bool, if True, no weekend dates
        - valid_years: list of valid years
    
    Returns:
    --------
    Validation results DataFrame
    """
    if rules is None:
        rules = {
            'min_date': '1900-01-01',
            'max_date': None,
            'no_future': True,
            'no_weekends': False
        }
    
    results = pd.DataFrame(index=series.index)
    results['original'] = series
    results['is_valid'] = True
    results['error'] = ''
    
    # Convert to datetime if needed
    series_dt = pd.to_datetime(series, errors='coerce')
    
    # Check for parsing failures
    parse_failed = series_dt.isna() & series.notna()
    results.loc[parse_failed, 'is_valid'] = False
    results.loc[parse_failed, 'error'] = 'Parse failed'
    
    # Check minimum date
    if rules.get('min_date'):
        min_date = pd.to_datetime(rules['min_date'])
        too_early = series_dt < min_date
        results.loc[too_early, 'is_valid'] = False
        results.loc[too_early, 'error'] = f'Before {min_date.date()}'
    
    # Check maximum date
    if rules.get('max_date'):
        max_date = pd.to_datetime(rules['max_date'])
        too_late = series_dt > max_date
        results.loc[too_late, 'is_valid'] = False
        results.loc[too_late, 'error'] = f'After {max_date.date()}'
    
    # Check no future dates
    if rules.get('no_future', True):
        today = pd.Timestamp.today().normalize()
        future_dates = series_dt > today
        results.loc[future_dates, 'is_valid'] = False
        results.loc[future_dates, 'error'] = 'Future date'
    
    # Check no weekends
    if rules.get('no_weekends', False):
        weekends = series_dt.dt.dayofweek.isin([5, 6])
        results.loc[weekends, 'is_valid'] = False
        results.loc[weekends, 'error'] = 'Weekend'
    
    # Summary
    valid_count = results['is_valid'].sum()
    print(f"Date Validation Summary:")
    print(f"  Valid: {valid_count} ({valid_count/len(series)*100:.1f}%)")
    print(f"  Invalid: {len(series) - valid_count}")
    
    # Error breakdown
    error_counts = results[~results['is_valid']]['error'].value_counts()
    if len(error_counts) > 0:
        print(f"\nError breakdown:")
        for error, count in error_counts.items():
            print(f"  {error}: {count}")
    
    return results

# Validate birth dates
birth_date_validation = validate_dates(
    df['birth_date'],
    rules={
        'min_date': '1900-01-01',
        'max_date': datetime.today().strftime('%Y-%m-%d'),
        'no_future': True
    }
)

print("\nBirth date validation:")
print(birth_date_validation)
10.4 Timezone Handling
Python

def standardize_timezone(series, target_tz='UTC', infer_local_tz='US/Eastern'):
    """
    Standardize timezone for datetime series
    
    Parameters:
    -----------
    series : pd.Series
        Datetime series (may have mixed timezones)
    target_tz : str
        Target timezone to convert to
    infer_local_tz : str
        Timezone to assume for naive datetimes
    
    Returns:
    --------
    Standardized datetime series
    """
    # Convert to datetime if needed
    series_dt = pd.to_datetime(series, errors='coerce')
    
    standardized = []
    
    for idx, dt in series_dt.items():
        if pd.isna(dt):
            standardized.append(pd.NaT)
            continue
        
        try:
            # Check if datetime has timezone info
            if dt.tzinfo is None:
                # Naive datetime - assume local timezone
                local_tz = pytz.timezone(infer_local_tz)
                dt = local_tz.localize(dt)
            
            # Convert to target timezone
            target = pytz.timezone(target_tz)
            dt_converted = dt.astimezone(target)
            
            standardized.append(dt_converted)
        
        except Exception as e:
            print(f"Error converting {dt}: {e}")
            standardized.append(pd.NaT)
    
    result = pd.Series(standardized, index=series.index)
    
    print(f"Timezone Standardization:")
    print(f"  Target timezone: {target_tz}")
    print(f"  Inferred local timezone for naive datetimes: {infer_local_tz}")
    print(f"  Successfully converted: {result.notna().sum()}/{len(series)}")
    
    return result

# Parse timestamps with timezone awareness
df['timestamp_parsed'] = pd.to_datetime(df['timestamp'], errors='coerce')

# Standardize to UTC
df['timestamp_utc'] = standardize_timezone(df['timestamp_parsed'], target_tz='UTC')

print("\nTimezone standardization:")
print(df[['timestamp', 'timestamp_parsed', 'timestamp_utc']].head())
10.5 Date Feature Engineering
Python

def extract_date_features(series, prefix=''):
    """
    Extract useful features from datetime series
    
    Parameters:
    -----------
    series : pd.Series
        Datetime series
    prefix : str
        Prefix for feature column names
    
    Returns:
    --------
    DataFrame with extracted features
    """
    # Convert to datetime
    dt = pd.to_datetime(series, errors='coerce')
    
    features = pd.DataFrame(index=series.index)
    
    # Basic components
    features[f'{prefix}year'] = dt.dt.year
    features[f'{prefix}month'] = dt.dt.month
    features[f'{prefix}day'] = dt.dt.day
    features[f'{prefix}hour'] = dt.dt.hour
    features[f'{prefix}minute'] = dt.dt.minute
    features[f'{prefix}second'] = dt.dt.second
    
    # Day-based features
    features[f'{prefix}day_of_week'] = dt.dt.dayofweek  # Monday=0
    features[f'{prefix}day_of_year'] = dt.dt.dayofyear
    features[f'{prefix}week_of_year'] = dt.dt.isocalendar().week
    features[f'{prefix}quarter'] = dt.dt.quarter
    
    # Boolean features
    features[f'{prefix}is_weekend'] = dt.dt.dayofweek.isin([5, 6]).astype(int)
    features[f'{prefix}is_month_start'] = dt.dt.is_month_start.astype(int)
    features[f'{prefix}is_month_end'] = dt.dt.is_month_end.astype(int)
    features[f'{prefix}is_quarter_start'] = dt.dt.is_quarter_start.astype(int)
    features[f'{prefix}is_quarter_end'] = dt.dt.is_quarter_end.astype(int)
    features[f'{prefix}is_year_start'] = dt.dt.is_year_start.astype(int)
    features[f'{prefix}is_year_end'] = dt.dt.is_year_end.astype(int)
    
    # Cyclical encoding (for ML algorithms)
    # Helps capture cyclical nature (e.g., December is close to January)
    features[f'{prefix}month_sin'] = np.sin(2 * np.pi * dt.dt.month / 12)
    features[f'{prefix}month_cos'] = np.cos(2 * np.pi * dt.dt.month / 12)
    features[f'{prefix}day_sin'] = np.sin(2 * np.pi * dt.dt.day / 31)
    features[f'{prefix}day_cos'] = np.cos(2 * np.pi * dt.dt.day / 31)
    features[f'{prefix}dow_sin'] = np.sin(2 * np.pi * dt.dt.dayofweek / 7)
    features[f'{prefix}dow_cos'] = np.cos(2 * np.pi * dt.dt.dayofweek / 7)
    
    # Time since/until reference date
    reference_date = pd.Timestamp('2020-01-01')
    features[f'{prefix}days_since_ref'] = (dt - reference_date).dt.days
    
    # Age calculation (if it's a birth date)
    today = pd.Timestamp.today()
    features[f'{prefix}age_years'] = (today - dt).dt.days // 365
    
    return features

# Extract features from birth date
birth_features = extract_date_features(df['birth_date'], prefix='birth_')

print("\nExtracted date features:")
print(birth_features.head())
10.6 Date Cleaning Pipeline
Python

def date_cleaning_pipeline(df, config):
    """
    Comprehensive date cleaning pipeline
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Configuration for each date column:
        {
            'column_name': {
                'format': 'iso' | 'us' | 'eu' | 'auto',
                'validate': {
                    'min_date': 'YYYY-MM-DD',
                    'max_date': 'YYYY-MM-DD',
                    'no_future': True/False
                },
                'timezone': {
                    'standardize': True/False,
                    'target_tz': 'UTC',
                    'infer_tz': 'US/Eastern'
                },
                'extract_features': True/False,
                'handle_invalid': 'null' | 'min' | 'max' | 'median'
            }
        }
    
    Returns:
    --------
    Cleaned DataFrame
    """
    print("="*60)
    print("DATE CLEANING PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    
    for col, settings in config.items():
        if col not in df_cleaned.columns:
            continue
        
        print(f"\n[Processing: {col}]")
        
        # Parse dates
        fmt = settings.get('format', 'auto')
        if fmt == 'us':
            parsed, _ = parse_dates_robust(df_cleaned[col], dayfirst=False)
        elif fmt == 'eu':
            parsed, _ = parse_dates_robust(df_cleaned[col], dayfirst=True)
        else:
            parsed, _ = parse_dates_robust(df_cleaned[col])
        
        # Validate
        if 'validate' in settings:
            validation = validate_dates(parsed, settings['validate'])
            invalid_mask = ~validation['is_valid']
            
            # Handle invalid dates
            handle_method = settings.get('handle_invalid', 'null')
            if handle_method == 'null':
                parsed.loc[invalid_mask] = pd.NaT
            elif handle_method == 'min':
                min_date = pd.to_datetime(settings['validate'].get('min_date'))
                parsed.loc[invalid_mask] = min_date
            elif handle_method == 'max':
                max_date = pd.to_datetime(settings['validate'].get('max_date', datetime.today()))
                parsed.loc[invalid_mask] = max_date
            elif handle_method == 'median':
                median_date = parsed.dropna().median()
                parsed.loc[invalid_mask] = median_date
            
            print(f"  Handled {invalid_mask.sum()} invalid dates using '{handle_method}'")
        
        # Timezone standardization
        if settings.get('timezone', {}).get('standardize', False):
            tz_config = settings['timezone']
            parsed = standardize_timezone(
                parsed,
                target_tz=tz_config.get('target_tz', 'UTC'),
                infer_local_tz=tz_config.get('infer_tz', 'US/Eastern')
            )
        
        # Store parsed date
        df_cleaned[f'{col}_cleaned'] = parsed
        
        # Extract features
        if settings.get('extract_features', False):
            features = extract_date_features(parsed, prefix=f'{col}_')
            df_cleaned = pd.concat([df_cleaned, features], axis=1)
            print(f"  Extracted {len(features.columns)} date features")
    
    print("\n" + "="*60)
    print("PIPELINE COMPLETE")
    print("="*60)
    
    return df_cleaned

# Define date cleaning configuration
date_config = {
    'date_iso': {
        'format': 'auto',
        'validate': {
            'min_date': '2020-01-01',
            'max_date': datetime.today().strftime('%Y-%m-%d'),
            'no_future': True
        },
        'handle_invalid': 'null',
        'extract_features': False
    },
    'birth_date': {
        'format': 'auto',
        'validate': {
            'min_date': '1900-01-01',
            'no_future': True
        },
        'handle_invalid': 'null',
        'extract_features': True
    }
}

# Run pipeline
df_dates_cleaned = date_cleaning_pipeline(df, date_config)

print("\nCleaned date data:")
print(df_dates_cleaned[['date_iso', 'date_iso_cleaned', 'birth_date', 'birth_date_cleaned']].head())
11. Data Consistency and Standardization
11.1 Understanding Consistency Issues
Python

"""
DATA CONSISTENCY PROBLEMS:

1. VALUE INCONSISTENCY
   - Same entity, different representations
   - "USA", "United States", "US", "U.S.A."

2. FORMAT INCONSISTENCY
   - Same data, different formats
   - Currency: "$100", "100 USD", "100.00"

3. UNIT INCONSISTENCY
   - Same measurement, different units
   - Weight: "100 kg", "220 lbs"

4. CROSS-FIELD INCONSISTENCY
   - Related fields don't match
   - Age: 25, Birth Year: 1990, Current Year: 2023 (doesn't add up)

5. REFERENTIAL INTEGRITY
   - Foreign keys don't match primary keys

6. BUSINESS RULE VIOLATIONS
   - End date before start date
   - Negative quantities
"""

import pandas as pd
import numpy as np

# Sample inconsistent data
data = {
    'id': range(1, 11),
    'country': ['USA', 'United States', 'US', 'U.S.A.', 'America', 
                'Canada', 'CA', 'CAN', 'UK', 'United Kingdom'],
    'gender': ['Male', 'M', 'male', 'MALE', 'F', 
               'Female', 'female', 'f', 'Other', 'other'],
    'price': ['$100.00', '100 USD', '100', '$150.50', '200.00',
              '€175', '175 EUR', '$225', '300', '$350.25'],
    'weight_value': [70, 154, 80, 176, 65, 143, 90, 198, 75, 165],
    'weight_unit': ['kg', 'lbs', 'kg', 'lbs', 'kg', 'lbs', 'kg', 'lbs', 'kg', 'lbs'],
    'age': [25, 30, 35, 40, 45, 50, 55, 60, 65, 70],
    'birth_year': [1998, 1993, 1988, 1983, 1978, 1973, 1968, 1963, 1958, 1953],
    'start_date': ['2023-01-15', '2023-02-20', '2023-03-25', '2023-01-10',
                   '2023-05-30', '2023-06-15', '2023-07-20', '2023-08-25',
                   '2023-09-30', '2023-10-05'],
    'end_date': ['2023-06-15', '2023-01-10', '2023-08-25', '2023-07-10',
                 '2023-10-30', '2023-11-15', '2023-12-20', '2024-01-25',
                 '2024-02-28', '2023-09-01'],  # Some end dates before start dates
}

df = pd.DataFrame(data)
print("Original inconsistent data:")
print(df)
11.2 Standardizing Categorical Values
Python

def create_value_mapping(values, mappings_dict=None, threshold=80):
    """
    Create mapping for standardizing categorical values
    
    Parameters:
    -----------
    values : list or series
        Unique values to standardize
    mappings_dict : dict
        Predefined mappings {standard_value: [variations]}
    threshold : int
        Fuzzy matching threshold for auto-detection
    
    Returns:
    --------
    Mapping dictionary {original: standard}
    """
    from difflib import SequenceMatcher
    
    if mappings_dict is None:
        mappings_dict = {}
    
    # Create reverse mapping
    reverse_map = {}
    for standard, variations in mappings_dict.items():
        for var in variations:
            reverse_map[var.lower()] = standard
    
    # Generate full mapping
    full_mapping = {}
    
    for val in values:
        if pd.isna(val):
            continue
        
        val_str = str(val).strip()
        val_lower = val_str.lower()
        
        # Check if in predefined mappings
        if val_lower in reverse_map:
            full_mapping[val_str] = reverse_map[val_lower]
        else:
            # Try fuzzy matching to existing standards
            best_match = None
            best_score = 0
            
            for standard in mappings_dict.keys():
                score = SequenceMatcher(None, val_lower, standard.lower()).ratio() * 100
                if score > best_score and score >= threshold:
                    best_score = score
                    best_match = standard
            
            if best_match:
                full_mapping[val_str] = best_match
            else:
                full_mapping[val_str] = val_str  # Keep original
    
    return full_mapping

# Define standard values and variations
country_mappings = {
    'United States': ['USA', 'US', 'U.S.A.', 'U.S.', 'America', 'United States of America'],
    'Canada': ['CA', 'CAN', 'Can'],
    'United Kingdom': ['UK', 'U.K.', 'Britain', 'Great Britain', 'GB'],
}

gender_mappings = {
    'Male': ['M', 'male', 'MALE', 'm', 'Man', 'man'],
    'Female': ['F', 'female', 'FEMALE', 'f', 'Woman', 'woman'],
    'Other': ['other', 'OTHER', 'Non-binary', 'non-binary', 'NB'],
}

def standardize_categorical(series, mappings_dict, case_sensitive=False):
    """
    Standardize categorical values using mapping
    """
    # Create mapping
    unique_vals = series.dropna().unique()
    mapping = create_value_mapping(unique_vals, mappings_dict)
    
    # Apply mapping
    standardized = series.copy()
    if not case_sensitive:
        # Create case-insensitive mapping
        case_mapping = {}
        for k, v in mapping.items():
            case_mapping[k] = v
            case_mapping[k.lower()] = v
            case_mapping[k.upper()] = v
        
        standardized = series.astype(str).str.strip()
        standardized = standardized.map(lambda x: case_mapping.get(x, case_mapping.get(x.lower(), x)))
    else:
        standardized = series.map(mapping)
    
    # Report changes
    changes = (series != standardized).sum()
    print(f"Standardization: {changes} values changed")
    print(f"Unique values: {series.nunique()} → {standardized.nunique()}")
    
    return standardized

# Apply standardization
df['country_std'] = standardize_categorical(df['country'], country_mappings)
df['gender_std'] = standardize_categorical(df['gender'], gender_mappings)

print("\nStandardized categorical values:")
print(df[['country', 'country_std', 'gender', 'gender_std']])
11.3 Unit Standardization
Python

def standardize_units(value_series, unit_series, target_unit, conversions):
    """
    Standardize values to a common unit
    
    Parameters:
    -----------
    value_series : pd.Series
        Numerical values
    unit_series : pd.Series
        Unit for each value
    target_unit : str
        Unit to convert to
    conversions : dict
        Conversion factors {unit: factor_to_target}
    
    Returns:
    --------
    Standardized values in target unit
    """
    standardized = []
    
    for val, unit in zip(value_series, unit_series):
        if pd.isna(val) or pd.isna(unit):
            standardized.append(np.nan)
            continue
        
        unit_lower = str(unit).lower().strip()
        
        if unit_lower in conversions:
            converted = val * conversions[unit_lower]
            standardized.append(converted)
        else:
            print(f"Unknown unit: {unit}")
            standardized.append(val)
    
    result = pd.Series(standardized, index=value_series.index)
    
    print(f"Unit Standardization:")
    print(f"  Target unit: {target_unit}")
    print(f"  Converted {len(result)} values")
    
    return result

# Weight conversion (to kg)
weight_conversions = {
    'kg': 1.0,
    'lbs': 0.453592,
    'lb': 0.453592,
    'g': 0.001,
    'oz': 0.0283495,
}

df['weight_kg'] = standardize_units(
    df['weight_value'],
    df['weight_unit'],
    target_unit='kg',
    conversions=weight_conversions
)

print("\nWeight standardization:")
print(df[['weight_value', 'weight_unit', 'weight_kg']])

# Currency standardization
def standardize_currency(price_series, target_currency='USD', exchange_rates=None):
    """
    Extract numeric value and standardize currency
    """
    if exchange_rates is None:
        exchange_rates = {
            'USD': 1.0,
            '$': 1.0,
            'EUR': 1.1,  # 1 EUR = 1.1 USD
            '€': 1.1,
            'GBP': 1.25,
            '£': 1.25,
        }
    
    standardized = []
    
    for price in price_series:
        if pd.isna(price):
            standardized.append(np.nan)
            continue
        
        price_str = str(price).strip()
        
        # Detect currency
        currency = 'USD'  # Default
        for curr_symbol in exchange_rates.keys():
            if curr_symbol in price_str:
                currency = curr_symbol
                break
        
        # Extract numeric value
        numeric = ''.join(c for c in price_str if c.isdigit() or c == '.')
        
        try:
            value = float(numeric)
            # Convert to target currency
            rate = exchange_rates.get(currency, 1.0)
            converted = value * rate
            standardized.append(round(converted, 2))
        except:
            standardized.append(np.nan)
    
    return pd.Series(standardized, index=price_series.index)

df['price_usd'] = standardize_currency(df['price'])

print("\nPrice standardization:")
print(df[['price', 'price_usd']])
11.4 Cross-Field Validation
Python

def validate_cross_field(df, rules):
    """
    Validate consistency across related fields
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    rules : list of dicts
        Each rule: {
            'name': 'rule_name',
            'fields': ['field1', 'field2'],
            'check': lambda row: boolean expression,
            'fix': lambda row: fixed values (optional)
        }
    
    Returns:
    --------
    Validation report and optionally fixed DataFrame
    """
    df_validated = df.copy()
    validation_results = {}
    
    for rule in rules:
        rule_name = rule['name']
        check_func = rule['check']
        fix_func = rule.get('fix', None)
        
        # Check each row
        violations = []
        for idx, row in df_validated.iterrows():
            try:
                if not check_func(row):
                    violations.append(idx)
            except:
                violations.append(idx)
        
        validation_results[rule_name] = {
            'violations': len(violations),
            'violation_indices': violations
        }
        
        print(f"\nRule: {rule_name}")
        print(f"  Violations: {len(violations)}")
        
        # Apply fix if provided
        if fix_func and len(violations) > 0:
            for idx in violations:
                try:
                    fixed = fix_func(df_validated.loc[idx])
                    for col, val in fixed.items():
                        df_validated.loc[idx, col] = val
                except Exception as e:
                    print(f"  Could not fix row {idx}: {e}")
            
            print(f"  Fixed {len(violations)} violations")
    
    return df_validated, validation_results

# Define cross-field validation rules
current_year = 2023

validation_rules = [
    {
        'name': 'Age matches birth year',
        'fields': ['age', 'birth_year'],
        'check': lambda row: abs(current_year - row['birth_year'] - row['age']) <= 1,
        'fix': lambda row: {'age': current_year - row['birth_year']}
    },
    {
        'name': 'End date after start date',
        'fields': ['start_date', 'end_date'],
        'check': lambda row: pd.to_datetime(row['end_date']) >= pd.to_datetime(row['start_date']),
        'fix': lambda row: {'end_date': row['start_date']}  # Set end = start as placeholder
    },
]

df_validated, validation_report = validate_cross_field(df, validation_rules)

print("\nCross-field validation results:")
print(df_validated[['age', 'birth_year', 'start_date', 'end_date']].head())
11.5 Comprehensive Consistency Pipeline
Python

def consistency_pipeline(df, config):
    """
    Comprehensive data consistency pipeline
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        {
            'categorical_mappings': {
                'column': {standard: [variations]}
            },
            'unit_conversions': {
                'column': {
                    'value_col': 'col_name',
                    'unit_col': 'col_name',
                    'target_unit': 'unit',
                    'conversions': {...}
                }
            },
            'cross_field_rules': [...]
        }
    
    Returns:
    --------
    Cleaned DataFrame
    """
    print("="*60)
    print("DATA CONSISTENCY PIPELINE")
    print("="*60)
    
    df_cleaned = df.copy()
    
    # Standardize categorical values
    if 'categorical_mappings' in config:
        print("\n[Step 1] Standardizing Categorical Values")
        for col, mappings in config['categorical_mappings'].items():
            if col in df_cleaned.columns:
                df_cleaned[f'{col}_std'] = standardize_categorical(
                    df_cleaned[col], mappings
                )
    
    # Standardize units
    if 'unit_conversions' in config:
        print("\n[Step 2] Standardizing Units")
        for output_col, unit_config in config['unit_conversions'].items():
            df_cleaned[output_col] = standardize_units(
                df_cleaned[unit_config['value_col']],
                df_cleaned[unit_config['unit_col']],
                unit_config['target_unit'],
                unit_config['conversions']
            )
    
    # Cross-field validation
    if 'cross_field_rules' in config:
        print("\n[Step 3] Cross-Field Validation")
        df_cleaned, _ = validate_cross_field(df_cleaned, config['cross_field_rules'])
    
    print("\n" + "="*60)
    print("PIPELINE COMPLETE")
    print("="*60)
    
    return df_cleaned

# Define pipeline configuration
consistency_config = {
    'categorical_mappings': {
        'country': country_mappings,
        'gender': gender_mappings
    },
    'unit_conversions': {
        'weight_kg': {
            'value_col': 'weight_value',
            'unit_col': 'weight_unit',
            'target_unit': 'kg',
            'conversions': weight_conversions
        }
    },
    'cross_field_rules': validation_rules
}

df_consistent = consistency_pipeline(df, consistency_config)
12. Feature Engineering During Cleaning
12.1 Creating Derived Features
Python

"""
Feature engineering during data cleaning serves two purposes:
1. Create useful features for ML models
2. Identify data quality issues through derived metrics
"""

import pandas as pd
import numpy as np

# Sample cleaned data
data = {
    'customer_id': range(1, 11),
    'first_name': ['John', 'Jane', 'Bob', 'Alice', 'Charlie', 
                   'Diana', 'Edward', 'Fiona', 'George', 'Helen'],
    'last_name': ['Smith', 'Doe', 'Johnson', 'Williams', 'Brown',
                  'Jones', 'Garcia', 'Miller', 'Davis', 'Rodriguez'],
    'email': ['john.smith@gmail.com', 'jane.doe@yahoo.com', 'bob.j@company.com',
              'alice@outlook.com', 'charlie.brown@gmail.com', 'diana.j@company.com',
              'edward.g@hotmail.com', 'fiona.m@gmail.com', 'george.d@yahoo.com',
              'helen.r@company.com'],
    'age': [25, 30, 35, 28, 45, 33, 42, 29, 38, 52],
    'salary': [50000, 65000, 75000, 55000, 95000, 70000, 88000, 58000, 82000, 105000],
    'hire_date': ['2022-01-15', '2021-03-20', '2019-06-10', '2022-08-05',
                  '2015-02-28', '2020-11-12', '2017-09-03', '2023-01-22',
                  '2018-07-30', '2012-04-18'],
    'department': ['Sales', 'IT', 'IT', 'Marketing', 'Sales',
                   'HR', 'IT', 'Marketing', 'Sales', 'Executive'],
    'transactions': [15, 45, 30, 22, 85, 12, 55, 18, 48, 120],
    'total_spend': [1500, 4500, 3000, 2200, 8500, 1200, 5500, 1800, 4800, 12000]
}

df = pd.DataFrame(data)
df['hire_date'] = pd.to_datetime(df['hire_date'])

print("Sample data:")
print(df.head())
12.2 Numerical Feature Engineering
Python

def engineer_numerical_features(df, config):
    """
    Create derived numerical features
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Feature engineering configuration
    
    Returns:
    --------
    DataFrame with new features
    """
    df_eng = df.copy()
    
    # Ratio features
    if 'ratios' in config:
        for name, (numerator, denominator) in config['ratios'].items():
            if numerator in df.columns and denominator in df.columns:
                df_eng[name] = df[numerator] / df[denominator].replace(0, np.nan)
                print(f"Created ratio: {name} = {numerator}/{denominator}")
    
    # Aggregation features (groupby)
    if 'aggregations' in config:
        for name, agg_config in config['aggregations'].items():
            group_col = agg_config['group_by']
            value_col = agg_config['value']
            agg_func = agg_config['func']
            
            agg_values = df.groupby(group_col)[value_col].transform(agg_func)
            df_eng[name] = agg_values
            print(f"Created aggregation: {name} = {agg_func}({value_col}) by {group_col}")
    
    # Binning features
    if 'bins' in config:
        for name, bin_config in config['bins'].items():
            col = bin_config['column']
            n_bins = bin_config.get('n_bins', 5)
            strategy = bin_config.get('strategy', 'quantile')
            labels = bin_config.get('labels', None)
            
            if strategy == 'quantile':
                df_eng[name] = pd.qcut(df[col], q=n_bins, labels=labels, duplicates='drop')
            elif strategy == 'uniform':
                df_eng[name] = pd.cut(df[col], bins=n_bins, labels=labels)
            elif strategy == 'custom' and 'edges' in bin_config:
                df_eng[name] = pd.cut(df[col], bins=bin_config['edges'], labels=labels)
            
            print(f"Created bins: {name} from {col} ({n_bins} bins)")
    
    # Mathematical transformations
    if 'transforms' in config:
        for name, transform_config in config['transforms'].items():
            col = transform_config['column']
            func = transform_config['func']
            
            if func == 'log':
                min_val = df[col].min()
                if min_val <= 0:
                    df_eng[name] = np.log1p(df[col] - min_val + 1)
                else:
                    df_eng[name] = np.log1p(df[col])
            elif func == 'sqrt':
                df_eng[name] = np.sqrt(df[col].clip(lower=0))
            elif func == 'square':
                df_eng[name] = df[col] ** 2
            elif func == 'reciprocal':
                df_eng[name] = 1 / df[col].replace(0, np.nan)
            
            print(f"Created transform: {name} = {func}({col})")
    
    # Polynomial features
    if 'polynomials' in config:
        for name, poly_config in config['polynomials'].items():
            col = poly_config['column']
            degree = poly_config.get('degree', 2)
            
            for d in range(2, degree + 1):
                df_eng[f'{col}_pow{d}'] = df[col] ** d
            
            print(f"Created polynomial features for {col} up to degree {degree}")
    
    # Interaction features
    if 'interactions' in config:
        for name, cols in config['interactions'].items():
            if all(c in df.columns for c in cols):
                result = df[cols[0]]
                for col in cols[1:]:
                    result = result * df[col]
                df_eng[name] = result
                print(f"Created interaction: {name} = {' * '.join(cols)}")
    
    return df_eng

# Define feature engineering configuration
numerical_config = {
    'ratios': {
        'avg_transaction_value': ('total_spend', 'transactions'),
        'salary_per_age': ('salary', 'age')
    },
    'aggregations': {
        'dept_avg_salary': {
            'group_by': 'department',
            'value': 'salary',
            'func': 'mean'
        },
        'dept_salary_rank': {
            'group_by': 'department',
            'value': 'salary',
            'func': 'rank'
        }
    },
    'bins': {
        'age_group': {
            'column': 'age',
            'n_bins': 4,
            'strategy': 'quantile',
            'labels': ['Young', 'Middle', 'Senior', 'Veteran']
        },
        'salary_tier': {
            'column': 'salary',
            'strategy': 'custom',
            'edges': [0, 60000, 80000, 100000, float('inf')],
            'labels': ['Entry', 'Mid', 'Senior', 'Executive']
        }
    },
    'transforms': {
        'log_salary': {'column': 'salary', 'func': 'log'},
        'sqrt_transactions': {'column': 'transactions', 'func': 'sqrt'}
    },
    'interactions': {
        'age_x_transactions': ['age', 'transactions']
    }
}

df_numerical = engineer_numerical_features(df, numerical_config)

print("\nNumerical features created:")
print(df_numerical[['customer_id', 'avg_transaction_value', 'dept_avg_salary', 
                   'age_group', 'salary_tier', 'log_salary']].head())
12.3 Categorical Feature Engineering
Python

def engineer_categorical_features(df, config):
    """
    Create derived categorical features
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        Feature engineering configuration
    
    Returns:
    --------
    DataFrame with new features
    """
    df_eng = df.copy()
    
    # Combine columns
    if 'combine' in config:
        for name, cols in config['combine'].items():
            if all(c in df.columns for c in cols):
                df_eng[name] = df[cols].astype(str).agg('_'.join, axis=1)
                print(f"Created combined: {name} = {' + '.join(cols)}")
    
    # Extract from text
    if 'extract' in config:
        for name, extract_config in config['extract'].items():
            col = extract_config['column']
            pattern = extract_config.get('pattern', None)
            func = extract_config.get('func', None)
            
            if pattern:
                df_eng[name] = df[col].str.extract(pattern, expand=False)
            elif func == 'email_domain':
                df_eng[name] = df[col].str.split('@').str[-1]
            elif func == 'first_word':
                df_eng[name] = df[col].str.split().str[0]
            elif func == 'last_word':
                df_eng[name] = df[col].str.split().str[-1]
            elif func == 'word_count':
                df_eng[name] = df[col].str.split().str.len()
            elif func == 'char_count':
                df_eng[name] = df[col].str.len()
            
            print(f"Created extraction: {name} from {col}")
    
    # Frequency encoding
    if 'frequency_encode' in config:
        for col in config['frequency_encode']:
            if col in df.columns:
                freq = df[col].value_counts(normalize=True)
                df_eng[f'{col}_freq'] = df[col].map(freq)
                print(f"Created frequency encoding: {col}_freq")
    
    # Target encoding placeholder (requires target variable)
    if 'target_encode' in config and 'target_col' in config:
        target = config['target_col']
        for col in config['target_encode']:
            if col in df.columns and target in df.columns:
                target_means = df.groupby(col)[target].mean()
                df_eng[f'{col}_target_enc'] = df[col].map(target_means)
                print(f"Created target encoding: {col}_target_enc")
    
    # Boolean flags
    if 'flags' in config:
        for name, flag_config in config['flags'].items():
            col = flag_config['column']
            condition = flag_config['condition']
            value = flag_config.get('value', None)
            
            if condition == 'equals':
                df_eng[name] = (df[col] == value).astype(int)
            elif condition == 'contains':
                df_eng[name] = df[col].str.contains(value, case=False, na=False).astype(int)
            elif condition == 'startswith':
                df_eng[name] = df[col].str.startswith(value, na=False).astype(int)
            elif condition == 'endswith':
                df_eng[name] = df[col].str.endswith(value, na=False).astype(int)
            elif condition == 'isin':
                df_eng[name] = df[col].isin(value).astype(int)
            
            print(f"Created flag: {name}")
    
    return df_eng

# Define categorical feature engineering configuration
categorical_config = {
    'combine': {
        'full_name': ['first_name', 'last_name']
    },
    'extract': {
        'email_domain': {
            'column': 'email',
            'func': 'email_domain'
        },
        'email_provider': {
            'column': 'email',
            'pattern': r'@(\w+)\.'
        }
    },
    'frequency_encode': ['department'],
    'flags': {
        'is_gmail': {
            'column': 'email',
            'condition': 'contains',
            'value': 'gmail'
        },
        'is_sales_dept': {
            'column': 'department',
            'condition': 'equals',
            'value': 'Sales'
        },
        'is_senior_role': {
            'column': 'department',
            'condition': 'isin',
            'value': ['Executive', 'IT']
        }
    }
}

df_categorical = engineer_categorical_features(df, categorical_config)

print("\nCategorical features created:")
print(df_categorical[['customer_id', 'full_name', 'email_domain', 
                     'department_freq', 'is_gmail', 'is_sales_dept']].head())
12.4 Date/Time Feature Engineering
Python

def engineer_datetime_features(df, config):
    """
    Create derived datetime features
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        {
            'datetime_cols': ['col1', 'col2'],
            'extract_components': True,
            'cyclical_encoding': True,
            'time_differences': [('col1', 'col2', 'diff_name')],
            'reference_date': 'YYYY-MM-DD'
        }
    
    Returns:
    --------
    DataFrame with datetime features
    """
    df_eng = df.copy()
    reference_date = pd.to_datetime(config.get('reference_date', 'today'))
    
    for col in config.get('datetime_cols', []):
        if col not in df.columns:
            continue
        
        # Ensure datetime type
        dt_col = pd.to_datetime(df[col], errors='coerce')
        
        # Extract components
        if config.get('extract_components', True):
            df_eng[f'{col}_year'] = dt_col.dt.year
            df_eng[f'{col}_month'] = dt_col.dt.month
            df_eng[f'{col}_day'] = dt_col.dt.day
            df_eng[f'{col}_dayofweek'] = dt_col.dt.dayofweek
            df_eng[f'{col}_quarter'] = dt_col.dt.quarter
            df_eng[f'{col}_weekofyear'] = dt_col.dt.isocalendar().week
            df_eng[f'{col}_is_weekend'] = (dt_col.dt.dayofweek >= 5).astype(int)
            df_eng[f'{col}_is_month_start'] = dt_col.dt.is_month_start.astype(int)
            df_eng[f'{col}_is_month_end'] = dt_col.dt.is_month_end.astype(int)
            print(f"Extracted components from {col}")
        
        # Cyclical encoding
        if config.get('cyclical_encoding', True):
            df_eng[f'{col}_month_sin'] = np.sin(2 * np.pi * dt_col.dt.month / 12)
            df_eng[f'{col}_month_cos'] = np.cos(2 * np.pi * dt_col.dt.month / 12)
            df_eng[f'{col}_dow_sin'] = np.sin(2 * np.pi * dt_col.dt.dayofweek / 7)
            df_eng[f'{col}_dow_cos'] = np.cos(2 * np.pi * dt_col.dt.dayofweek / 7)
            print(f"Created cyclical encoding for {col}")
        
        # Days since reference
        df_eng[f'{col}_days_since_ref'] = (reference_date - dt_col).dt.days
        df_eng[f'{col}_years_since_ref'] = df_eng[f'{col}_days_since_ref'] / 365.25
        print(f"Created time since reference for {col}")
    
    # Time differences between columns
    if 'time_differences' in config:
        for col1, col2, diff_name in config['time_differences']:
            if col1 in df.columns and col2 in df.columns:
                dt1 = pd.to_datetime(df[col1], errors='coerce')
                dt2 = pd.to_datetime(df[col2], errors='coerce')
                df_eng[f'{diff_name}_days'] = (dt2 - dt1).dt.days
                df_eng[f'{diff_name}_months'] = df_eng[f'{diff_name}_days'] / 30.44
                df_eng[f'{diff_name}_years'] = df_eng[f'{diff_name}_days'] / 365.25
                print(f"Created time difference: {diff_name}")
    
    return df_eng

# Define datetime feature engineering configuration
datetime_config = {
    'datetime_cols': ['hire_date'],
    'extract_components': True,
    'cyclical_encoding': True,
    'reference_date': '2024-01-01',
    'time_differences': []
}

df_datetime = engineer_datetime_features(df, datetime_config)

print("\nDatetime features created:")
print(df_datetime[['customer_id', 'hire_date', 'hire_date_year', 'hire_date_month',
                  'hire_date_is_weekend', 'hire_date_days_since_ref']].head())
12.5 Comprehensive Feature Engineering Pipeline
Python

def feature_engineering_pipeline(df, config):
    """
    Comprehensive feature engineering pipeline
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    config : dict
        {
            'numerical': {...},
            'categorical': {...},
            'datetime': {...}
        }
    
    Returns:
    --------
    DataFrame with all engineered features
    """
    print("="*60)
    print("FEATURE ENGINEERING PIPELINE")
    print("="*60)
    
    df_eng = df.copy()
    
    # Numerical features
    if 'numerical' in config:
        print("\n[Step 1] Engineering Numerical Features")
        df_eng = engineer_numerical_features(df_eng, config['numerical'])
    
    # Categorical features
    if 'categorical' in config:
        print("\n[Step 2] Engineering Categorical Features")
        df_eng = engineer_categorical_features(df_eng, config['categorical'])
    
    # Datetime features
    if 'datetime' in config:
        print("\n[Step 3] Engineering Datetime Features")
        df_eng = engineer_datetime_features(df_eng, config['datetime'])
    
    # Summary
    new_cols = len(df_eng.columns) - len(df.columns)
    
    print("\n" + "="*60)
    print("FEATURE ENGINEERING SUMMARY")
    print("="*60)
    print(f"Original columns: {len(df.columns)}")
    print(f"New columns created: {new_cols}")
    print(f"Total columns: {len(df_eng.columns)}")
    print("\nNew columns:")
    for col in df_eng.columns:
        if col not in df.columns:
            print(f"  - {col}")
    print("="*60)
    
    return df_eng

# Full configuration
full_fe_config = {
    'numerical': numerical_config,
    'categorical': categorical_config,
    'datetime': datetime_config
}

df_final = feature_engineering_pipeline(df, full_fe_config)
13. Advanced Techniques
13.1 Handling Imbalanced Data During Cleaning
Python

"""
Imbalanced data occurs when one class significantly outnumbers others.
While typically handled during modeling, early detection and documentation
during cleaning is important.
"""

import pandas as pd
import numpy as np
from collections import Counter

# Sample imbalanced data
np.random.seed(42)
n_samples = 1000

data = {
    'id': range(n_samples),
    'feature1': np.random.normal(0, 1, n_samples),
    'feature2': np.random.normal(5, 2, n_samples),
    'target': np.random.choice(['Normal', 'Fraud'], n_samples, p=[0.95, 0.05])
}

df_imbalanced = pd.DataFrame(data)

def analyze_class_imbalance(df, target_col):
    """
    Analyze and report class imbalance
    """
    print("="*60)
    print("CLASS IMBALANCE ANALYSIS")
    print("="*60)
    
    # Class distribution
    class_counts = df[target_col].value_counts()
    class_percentages = df[target_col].value_counts(normalize=True) * 100
    
    print(f"\nClass Distribution:")
    for cls in class_counts.index:
        print(f"  {cls}: {class_counts[cls]} ({class_percentages[cls]:.2f}%)")
    
    # Imbalance ratio
    majority_class = class_counts.idxmax()
    minority_class = class_counts.idxmin()
    imbalance_ratio = class_counts[majority_class] / class_counts[minority_class]
    
    print(f"\nImbalance Metrics:")
    print(f"  Majority class: {majority_class}")
    print(f"  Minority class: {minority_class}")
    print(f"  Imbalance ratio: {imbalance_ratio:.2f}:1")
    
    # Recommendations
    print(f"\nRecommendations:")
    if imbalance_ratio < 3:
        print("  ✅ Mild imbalance - standard ML techniques may work")
    elif imbalance_ratio < 10:
        print("  ⚠️ Moderate imbalance - consider class weights or SMOTE")
    else:
        print("  🚨 Severe imbalance - use specialized techniques:")
        print("     - SMOTE/ADASYN for oversampling")
        print("     - Random undersampling")
        print("     - Class weights in model")
        print("     - Anomaly detection approaches")
    
    print("="*60)
    
    return {
        'class_counts': class_counts.to_dict(),
        'imbalance_ratio': imbalance_ratio,
        'majority_class': majority_class,
        'minority_class': minority_class
    }

# Analyze imbalance
imbalance_info = analyze_class_imbalance(df_imbalanced, 'target')

# Document imbalance for later handling
def create_imbalance_report(df, target_col, output_file=None):
    """
    Create comprehensive imbalance report for documentation
    """
    report = []
    report.append("# Class Imbalance Report\n")
    report.append(f"Dataset shape: {df.shape}\n")
    report.append(f"Target column: {target_col}\n\n")
    
    # Class distribution
    class_counts = df[target_col].value_counts()
    report.append("## Class Distribution\n")
    for cls, count in class_counts.items():
        pct = count / len(df) * 100
        report.append(f"- {cls}: {count} ({pct:.2f}%)\n")
    
    # Feature statistics by class
    report.append("\n## Feature Statistics by Class\n")
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    
    for cls in df[target_col].unique():
        report.append(f"\n### Class: {cls}\n")
        class_df = df[df[target_col] == cls]
        stats = class_df[numerical_cols].describe().round(2)
        report.append(stats.to_string() + "\n")
    
    report_text = ''.join(report)
    
    if output_file:
        with open(output_file, 'w') as f:
            f.write(report_text)
        print(f"Report saved to {output_file}")
    
    return report_text

# Generate report
report = create_imbalance_report(df_imbalanced, 'target')
print(report[:500])  # Print first 500 chars
13.2 Multi-Table Data Cleaning
Python

def clean_multi_table_data(tables_dict, relationships, config):
    """
    Clean multiple related tables while maintaining referential integrity
    
    Parameters:
    -----------
    tables_dict : dict
        {table_name: DataFrame}
    relationships : list
        [(parent_table, child_table, parent_key, child_key), ...]
    config : dict
        Cleaning configuration for each table
    
    Returns:
    --------
    Dictionary of cleaned DataFrames
    """
    print("="*60)
    print("MULTI-TABLE DATA CLEANING")
    print("="*60)
    
    cleaned_tables = {name: df.copy() for name, df in tables_dict.items()}
    
    # Step 1: Clean individual tables
    print("\n[Step 1] Cleaning Individual Tables")
    for table_name, table_config in config.items():
        if table_name in cleaned_tables:
            df = cleaned_tables[table_name]
            
            # Apply basic cleaning
            if 'drop_duplicates' in table_config:
                subset = table_config['drop_duplicates']
                before = len(df)
                df = df.drop_duplicates(subset=subset)
                print(f"  {table_name}: Dropped {before - len(df)} duplicate rows")
            
            if 'handle_nulls' in table_config:
                for col, strategy in table_config['handle_nulls'].items():
                    if col in df.columns:
                        if strategy == 'drop':
                            df = df.dropna(subset=[col])
                        elif strategy == 'mean':
                            df[col] = df[col].fillna(df[col].mean())
                        elif strategy == 'mode':
                            df[col] = df[col].fillna(df[col].mode()[0])
                        print(f"  {table_name}.{col}: Applied {strategy} for nulls")
            
            cleaned_tables[table_name] = df
    
    # Step 2: Validate referential integrity
    print("\n[Step 2] Validating Referential Integrity")
    integrity_issues = []
    
    for parent, child, parent_key, child_key in relationships:
        parent_df = cleaned_tables[parent]
        child_df = cleaned_tables[child]
        
        # Check for orphan records
        parent_keys = set(parent_df[parent_key])
        child_keys = set(child_df[child_key])
        
        orphans = child_keys - parent_keys
        missing_refs = parent_keys - child_keys
        
        if orphans:
            print(f"  ⚠️  {child}.{child_key}: {len(orphans)} orphan records")
            integrity_issues.append({
                'table': child,
                'column': child_key,
                'issue': 'orphan',
                'count': len(orphans),
                'values': list(orphans)[:5]
            })
        else:
            print(f"  ✅ {child}.{child_key}: No orphan records")
    
    # Step 3: Fix referential integrity issues
    print("\n[Step 3] Fixing Referential Integrity")
    
    fix_strategy = config.get('integrity_fix', 'remove_orphans')
    
    for issue in integrity_issues:
        child_table = issue['table']
        child_key = issue['column']
        
        if fix_strategy == 'remove_orphans':
            # Find parent table and key
            for parent, child, pk, ck in relationships:
                if child == child_table and ck == child_key:
                    parent_keys = set(cleaned_tables[parent][pk])
                    before = len(cleaned_tables[child_table])
                    cleaned_tables[child_table] = cleaned_tables[child_table][
                        cleaned_tables[child_table][child_key].isin(parent_keys)
                    ]
                    after = len(cleaned_tables[child_table])
                    print(f"  Removed {before - after} orphan records from {child_table}")
    
    # Summary
    print("\n" + "="*60)
    print("MULTI-TABLE CLEANING SUMMARY")
    print("="*60)
    for name, df in cleaned_tables.items():
        original_len = len(tables_dict[name])
        final_len = len(df)
        print(f"  {name}: {original_len} → {final_len} rows")
    print("="*60)
    
    return cleaned_tables

# Example: Customers and Orders tables
customers = pd.DataFrame({
    'customer_id': [1, 2, 3, 4, 5],
    'name': ['John', 'Jane', 'Bob', 'Alice', 'Charlie'],
    'email': ['john@email.com', 'jane@email.com', 'bob@email.com', None, 'charlie@email.com']
})

orders = pd.DataFrame({
    'order_id': range(1, 11),
    'customer_id': [1, 2, 1, 3, 99, 2, 4, 1, 100, 3],  # 99 and 100 are orphans
    'amount': [100, 200, 150, 300, 250, 175, 225, 125, 350, 275]
})

tables = {
    'customers': customers,
    'orders': orders
}

relationships = [
    ('customers', 'orders', 'customer_id', 'customer_id')
]

cleaning_config = {
    'customers': {
        'drop_duplicates': ['customer_id'],
        'handle_nulls': {'email': 'drop'}
    },
    'orders': {
        'drop_duplicates': ['order_id']
    },
    'integrity_fix': 'remove_orphans'
}

cleaned = clean_multi_table_data(tables, relationships, cleaning_config)
13.3 Handling Large Datasets
Python

def clean_large_dataset_chunked(filepath, chunk_size, cleaning_func, output_path=None):
    """
    Clean large datasets using chunked processing
    
    Parameters:
    -----------
    filepath : str
        Path to input CSV file
    chunk_size : int
        Number of rows per chunk
    cleaning_func : callable
        Function to apply to each chunk
    output_path : str
        Path for output file (None = return combined DataFrame)
    
    Returns:
    --------
    Cleaned DataFrame or path to output file
    """
    print("="*60)
    print("LARGE DATASET CHUNKED CLEANING")
    print("="*60)
    
    total_rows_processed = 0
    total_rows_kept = 0
    chunks_processed = 0
    
    # Initialize output file
    first_chunk = True
    
    # Process chunks
    for chunk in pd.read_csv(filepath, chunksize=chunk_size):
        chunks_processed += 1
        rows_before = len(chunk)
        
        # Apply cleaning function
        cleaned_chunk = cleaning_func(chunk)
        rows_after = len(cleaned_chunk)
        
        total_rows_processed += rows_before
        total_rows_kept += rows_after
        
        print(f"  Chunk {chunks_processed}: {rows_before} → {rows_after} rows")
        
        # Save to output
        if output_path:
            if first_chunk:
                cleaned_chunk.to_csv(output_path, index=False, mode='w')
                first_chunk = False
            else:
                cleaned_chunk.to_csv(output_path, index=False, mode='a', header=False)
    
    # Summary
    print("\n" + "="*60)
    print("CHUNKED PROCESSING SUMMARY")
    print("="*60)
    print(f"Chunks processed: {chunks_processed}")
    print(f"Total rows processed: {total_rows_processed}")
    print(f"Total rows kept: {total_rows_kept}")
    print(f"Rows removed: {total_rows_processed - total_rows_kept}")
    print(f"Removal rate: {((total_rows_processed - total_rows_kept) / total_rows_processed) * 100:.2f}%")
    
    if output_path:
        print(f"Output saved to: {output_path}")
        return output_path
    
    print("="*60)

# Example cleaning function for chunks
def clean_chunk(chunk):
    """
    Example cleaning function for each chunk
    """
    # Remove duplicates within chunk
    chunk = chunk.drop_duplicates()
    
    # Handle missing values
    chunk = chunk.dropna(subset=['important_column'])
    
    # Type conversions
    if 'date_column' in chunk.columns:
        chunk['date_column'] = pd.to_datetime(chunk['date_column'], errors='coerce')
    
    return chunk

# Memory-efficient cleaning with Dask
def clean_with_dask(filepath, cleaning_config):
    """
    Clean large datasets using Dask for parallel processing
    
    Requires: pip install dask[dataframe]
    """
    try:
        import dask.dataframe as dd
        
        print("="*60)
        print("DASK PARALLEL CLEANING")
        print("="*60)
        
        # Read data with Dask
        ddf = dd.read_csv(filepath)
        
        print(f"Partitions: {ddf.npartitions}")
        
        # Apply cleaning operations
        if 'drop_duplicates' in cleaning_config:
            ddf = ddf.drop_duplicates(subset=cleaning_config['drop_duplicates'])
        
        if 'drop_na' in cleaning_config:
            ddf = ddf.dropna(subset=cleaning_config['drop_na'])
        
        # Compute result
        df_cleaned = ddf.compute()
        
        print(f"Cleaned rows: {len(df_cleaned)}")
        print("="*60)
        
        return df_cleaned
    
    except ImportError:
        print("Dask not installed. Use: pip install dask[dataframe]")
        return None
13.4 Data Quality Scoring
Python

def calculate_data_quality_score(df, weights=None):
    """
    Calculate comprehensive data quality score
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    weights : dict
        Weights for each quality dimension
    
    Returns:
    --------
    Quality score and detailed report
    """
    if weights is None:
        weights = {
            'completeness': 0.25,
            'uniqueness': 0.20,
            'validity': 0.20,
            'consistency': 0.15,
            'accuracy': 0.10,
            'timeliness': 0.10
        }
    
    print("="*60)
    print("DATA QUALITY SCORING")
    print("="*60)
    
    scores = {}
    
    # 1. Completeness: Percentage of non-null values
    total_cells = df.shape[0] * df.shape[1]
    non_null_cells = df.count().sum()
    scores['completeness'] = (non_null_cells / total_cells) * 100
    print(f"\n1. COMPLETENESS: {scores['completeness']:.2f}%")
    print(f"   Non-null cells: {non_null_cells}/{total_cells}")
    
    # 2. Uniqueness: Percentage of non-duplicate rows
    duplicate_rows = df.duplicated().sum()
    unique_rows = len(df) - duplicate_rows
    scores['uniqueness'] = (unique_rows / len(df)) * 100
    print(f"\n2. UNIQUENESS: {scores['uniqueness']:.2f}%")
    print(f"   Unique rows: {unique_rows}/{len(df)}")
    
    # 3. Validity: Check data type consistency and valid values
    validity_scores = []
    for col in df.columns:
        # Check for type consistency
        if df[col].dtype == 'object':
            # Check if should be numeric
            numeric_convertible = pd.to_numeric(df[col], errors='coerce').notna().sum()
            non_null = df[col].notna().sum()
            if non_null > 0:
                validity_scores.append(numeric_convertible / non_null if numeric_convertible > non_null * 0.5 else 1)
        else:
            validity_scores.append(1.0)
    scores['validity'] = np.mean(validity_scores) * 100
    print(f"\n3. VALIDITY: {scores['validity']:.2f}%")
    
    # 4. Consistency: Check for inconsistent formats within columns
    consistency_scores = []
    for col in df.select_dtypes(include=['object']).columns:
        unique_patterns = df[col].dropna().apply(lambda x: len(str(x))).std()
        # Lower std = more consistent
        consistency_scores.append(1 / (1 + unique_patterns/10))
    scores['consistency'] = np.mean(consistency_scores) * 100 if consistency_scores else 100
    print(f"\n4. CONSISTENCY: {scores['consistency']:.2f}%")
    
    # 5. Accuracy: Placeholder (requires ground truth)
    # Using outlier-based estimation
    accuracy_scores = []
    for col in df.select_dtypes(include=[np.number]).columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - 1.5 * IQR
        upper = Q3 + 1.5 * IQR
        outliers = ((df[col] < lower) | (df[col] > upper)).sum()
        accuracy_scores.append(1 - (outliers / len(df)))
    scores['accuracy'] = np.mean(accuracy_scores) * 100 if accuracy_scores else 100
    print(f"\n5. ACCURACY (outlier-based): {scores['accuracy']:.2f}%")
    
    # 6. Timeliness: Check datetime columns for freshness
    timeliness_scores = []
    for col in df.select_dtypes(include=['datetime64']).columns:
        latest = df[col].max()
        if pd.notna(latest):
            days_old = (pd.Timestamp.today() - latest).days
            # Score decreases with age
            timeliness_scores.append(max(0, 1 - (days_old / 365)))
    scores['timeliness'] = np.mean(timeliness_scores) * 100 if timeliness_scores else 100
    print(f"\n6. TIMELINESS: {scores['timeliness']:.2f}%")
    
    # Calculate weighted overall score
    overall_score = sum(scores[dim] * weights[dim] for dim in weights.keys())
    
    print("\n" + "="*60)
    print("OVERALL DATA QUALITY SCORE")
    print("="*60)
    print(f"\n  SCORE: {overall_score:.2f}/100")
    
    if overall_score >= 90:
        quality_level = "EXCELLENT"
        emoji = "🌟"
    elif overall_score >= 75:
        quality_level = "GOOD"
        emoji = "✅"
    elif overall_score >= 60:
        quality_level = "FAIR"
        emoji = "⚠️"
    else:
        quality_level = "POOR"
        emoji = "🚨"
    
    print(f"  QUALITY LEVEL: {emoji} {quality_level}")
    print("="*60)
    
    return {
        'overall_score': overall_score,
        'quality_level': quality_level,
        'dimension_scores': scores
    }

# Calculate quality score for our data
quality_report = calculate_data_quality_score(df)
14. Automation and Pipelines
14.1 Building Reusable Cleaning Pipelines
Python

class DataCleaningPipeline:
    """
    Reusable, configurable data cleaning pipeline
    """
    
    def __init__(self, name="DataCleaningPipeline"):
        self.name = name
        self.steps = []
        self.history = []
        self.config = {}
    
    def add_step(self, name, func, params=None):
        """
        Add a cleaning step to the pipeline
        
        Parameters:
        -----------
        name : str
            Step name
        func : callable
            Cleaning function (takes DataFrame, returns DataFrame)
        params : dict
            Parameters to pass to the function
        """
        self.steps.append({
            'name': name,
            'func': func,
            'params': params or {}
        })
        print(f"Added step: {name}")
        return self
    
    def remove_step(self, name):
        """Remove a step by name"""
        self.steps = [s for s in self.steps if s['name'] != name]
        print(f"Removed step: {name}")
        return self
    
    def run(self, df, verbose=True):
        """
        Execute the pipeline
        
        Parameters:
        -----------
        df : DataFrame
            Input dataframe
        verbose : bool
            Print progress
        
        Returns:
        --------
        Cleaned DataFrame
        """
        if verbose:
            print("="*60)
            print(f"RUNNING PIPELINE: {self.name}")
            print("="*60)
        
        df_cleaned = df.copy()
        initial_shape = df_cleaned.shape
        
        self.history = [{
            'step': 'initial',
            'rows': df_cleaned.shape[0],
            'cols': df_cleaned.shape[1]
        }]
        
        for i, step in enumerate(self.steps, 1):
            step_name = step['name']
            func = step['func']
            params = step['params']
            
            if verbose:
                print(f"\n[Step {i}/{len(self.steps)}] {step_name}")
            
            try:
                before_rows = len(df_cleaned)
                df_cleaned = func(df_cleaned, **params)
                after_rows = len(df_cleaned)
                
                self.history.append({
                    'step': step_name,
                    'rows': after_rows,
                    'cols': df_cleaned.shape[1],
                    'rows_removed': before_rows - after_rows
                })
                
                if verbose:
                    print(f"   ✅ Complete: {before_rows} → {after_rows} rows")
            
            except Exception as e:
                if verbose:
                    print(f"   ❌ Error: {str(e)}")
                self.history.append({
                    'step': step_name,
                    'error': str(e)
                })
                raise
        
        if verbose:
            final_shape = df_cleaned.shape
            print("\n" + "="*60)
            print("PIPELINE SUMMARY")
            print("="*60)
            print(f"Initial shape: {initial_shape}")
            print(f"Final shape: {final_shape}")
            print(f"Rows removed: {initial_shape[0] - final_shape[0]}")
            print(f"Columns changed: {final_shape[1] - initial_shape[1]}")
            print("="*60)
        
        return df_cleaned
    
    def get_history(self):
        """Return execution history"""
        return pd.DataFrame(self.history)
    
    def save_config(self, filepath):
        """Save pipeline configuration"""
        import json
        config = {
            'name': self.name,
            'steps': [{'name': s['name'], 'params': s['params']} for s in self.steps]
        }
        with open(filepath, 'w') as f:
            json.dump(config, f, indent=2)
        print(f"Configuration saved to {filepath}")
    
    def __repr__(self):
        return f"DataCleaningPipeline(name='{self.name}', steps={len(self.steps)})"

# Define reusable cleaning functions
def remove_duplicates(df, subset=None, keep='first'):
    """Remove duplicate rows"""
    return df.drop_duplicates(subset=subset, keep=keep)

def handle_missing(df, strategy='drop', columns=None, fill_value=None):
    """Handle missing values"""
    if columns is None:
        columns = df.columns
    
    if strategy == 'drop':
        return df.dropna(subset=columns)
    elif strategy == 'fill_value':
        df[columns] = df[columns].fillna(fill_value)
    elif strategy == 'mean':
        for col in columns:
            if df[col].dtype in ['int64', 'float64']:
                df[col] = df[col].fillna(df[col].mean())
    elif strategy == 'median':
        for col in columns:
            if df[col].dtype in ['int64', 'float64']:
                df[col] = df[col].fillna(df[col].median())
    elif strategy == 'mode':
        for col in columns:
            df[col] = df[col].fillna(df[col].mode()[0])
    
    return df

def remove_outliers_iqr(df, columns=None, multiplier=1.5):
    """Remove outliers using IQR method"""
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    for col in columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - multiplier * IQR
        upper = Q3 + multiplier * IQR
        df = df[(df[col] >= lower) & (df[col] <= upper)]
    
    return df

def standardize_text(df, columns=None, operations=None):
    """Standardize text columns"""
    if columns is None:
        columns = df.select_dtypes(include=['object']).columns
    
    if operations is None:
        operations = ['strip', 'lower']
    
    for col in columns:
        if 'strip' in operations:
            df[col] = df[col].str.strip()
        if 'lower' in operations:
            df[col] = df[col].str.lower()
        if 'upper' in operations:
            df[col] = df[col].str.upper()
        if 'title' in operations:
            df[col] = df[col].str.title()
    
    return df

def convert_types(df, type_dict):
    """Convert column types"""
    for col, dtype in type_dict.items():
        if col in df.columns:
            if dtype == 'datetime':
                df[col] = pd.to_datetime(df[col], errors='coerce')
            elif dtype == 'category':
                df[col] = df[col].astype('category')
            else:
                df[col] = df[col].astype(dtype)
    return df

# Build pipeline
pipeline = DataCleaningPipeline(name="CustomerDataCleaning")

pipeline.add_step("Remove Duplicates", remove_duplicates, {'subset': ['customer_id']})
pipeline.add_step("Handle Missing Values", handle_missing, {'strategy': 'drop', 'columns': ['email']})
pipeline.add_step("Standardize Text", standardize_text, {'columns': ['first_name', 'last_name'], 'operations': ['strip', 'title']})
pipeline.add_step("Remove Outliers", remove_outliers_iqr, {'columns': ['salary'], 'multiplier': 2.0})

# Run pipeline
df_cleaned = pipeline.run(df)

# View history
print("\nExecution History:")
print(pipeline.get_history())
14.2 Automated Data Profiling
Python

def auto_profile_data(df, output_format='dict'):
    """
    Automatically profile a dataset
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    output_format : str
        'dict', 'dataframe', or 'report'
    
    Returns:
    --------
    Profiling results
    """
    print("="*60)
    print("AUTOMATED DATA PROFILING")
    print("="*60)
    
    profile = {
        'overview': {},
        'columns': {}
    }
    
    # Overview
    profile['overview'] = {
        'rows': len(df),
        'columns': len(df.columns),
        'total_cells': df.shape[0] * df.shape[1],
        'missing_cells': df.isnull().sum().sum(),
        'missing_percentage': (df.isnull().sum().sum() / (df.shape[0] * df.shape[1])) * 100,
        'duplicate_rows': df.duplicated().sum(),
        'memory_usage_mb': df.memory_usage(deep=True).sum() / 1024**2
    }
    
    print(f"\nOverview:")
    print(f"  Rows: {profile['overview']['rows']}")
    print(f"  Columns: {profile['overview']['columns']}")
    print(f"  Missing: {profile['overview']['missing_percentage']:.2f}%")
    print(f"  Duplicates: {profile['overview']['duplicate_rows']}")
    print(f"  Memory: {profile['overview']['memory_usage_mb']:.2f} MB")
    
    # Column-level profiling
    print(f"\nColumn Profiles:")
    
    for col in df.columns:
        col_profile = {
            'dtype': str(df[col].dtype),
            'missing_count': df[col].isnull().sum(),
            'missing_percentage': (df[col].isnull().sum() / len(df)) * 100,
            'unique_values': df[col].nunique(),
            'unique_percentage': (df[col].nunique() / len(df)) * 100
        }
        
        # Type-specific profiling
        if df[col].dtype in ['int64', 'float64']:
            col_profile.update({
                'min': df[col].min(),
                'max': df[col].max(),
                'mean': df[col].mean(),
                'median': df[col].median(),
                'std': df[col].std(),
                'skewness': df[col].skew(),
                'zeros': (df[col] == 0).sum(),
                'negatives': (df[col] < 0).sum()
            })
            
            # Outlier detection
            Q1 = df[col].quantile(0.25)
            Q3 = df[col].quantile(0.75)
            IQR = Q3 - Q1
            outliers = ((df[col] < Q1 - 1.5*IQR) | (df[col] > Q3 + 1.5*IQR)).sum()
            col_profile['outliers'] = outliers
            
        elif df[col].dtype == 'object':
            col_profile.update({
                'most_frequent': df[col].mode()[0] if len(df[col].mode()) > 0 else None,
                'most_frequent_count': df[col].value_counts().iloc[0] if len(df[col].dropna()) > 0 else 0,
                'avg_length': df[col].str.len().mean() if df[col].notna().any() else 0,
                'empty_strings': (df[col] == '').sum(),
                'whitespace_issues': df[col].str.strip().ne(df[col]).sum() if df[col].notna().any() else 0
            })
        
        profile['columns'][col] = col_profile
        
        # Print summary
        print(f"\n  {col} ({col_profile['dtype']}):")
        print(f"    Missing: {col_profile['missing_percentage']:.1f}%")
        print(f"    Unique: {col_profile['unique_values']} ({col_profile['unique_percentage']:.1f}%)")
        
        if df[col].dtype in ['int64', 'float64']:
            print(f"    Range: [{col_profile['min']:.2f}, {col_profile['max']:.2f}]")
            print(f"    Outliers: {col_profile['outliers']}")
    
    print("="*60)
    
    # Return in requested format
    if output_format == 'dataframe':
        return pd.DataFrame(profile['columns']).T
    elif output_format == 'report':
        # Generate markdown report
        report = f"# Data Profile Report\n\n"
        report += f"## Overview\n"
        for key, value in profile['overview'].items():
            report += f"- **{key}**: {value}\n"
        report += f"\n## Columns\n"
        for col, stats in profile['columns'].items():
            report += f"\n### {col}\n"
            for key, value in stats.items():
                report += f"- {key}: {value}\n"
        return report
    else:
        return profile

# Profile the data
profile = auto_profile_data(df, output_format='dict')
14.3 Automated Cleaning Recommendations
Python

def generate_cleaning_recommendations(df):
    """
    Automatically generate cleaning recommendations based on data profiling
    
    Parameters:
    -----------
    df : DataFrame
        Input dataframe
    
    Returns:
    --------
    List of recommendations with priority
    """
    print("="*60)
    print("AUTOMATED CLEANING RECOMMENDATIONS")
    print("="*60)
    
    recommendations = []
    
    # 1. Missing values
    for col in df.columns:
        missing_pct = (df[col].isnull().sum() / len(df)) * 100
        if missing_pct > 0:
            if missing_pct > 50:
                rec = {
                    'column': col,
                    'issue': 'High missing values',
                    'detail': f'{missing_pct:.1f}% missing',
                    'priority': 'HIGH',
                    'action': 'Consider dropping column or advanced imputation',
                    'code': f"df.drop(columns=['{col}'])"
                }
            elif missing_pct > 10:
                rec = {
                    'column': col,
                    'issue': 'Moderate missing values',
                    'detail': f'{missing_pct:.1f}% missing',
                    'priority': 'MEDIUM',
                    'action': 'Impute using mean/median/mode or KNN',
                    'code': f"df['{col}'].fillna(df['{col}'].median(), inplace=True)"
                }
            else:
                rec = {
                    'column': col,
                    'issue': 'Low missing values',
                    'detail': f'{missing_pct:.1f}% missing',
                    'priority': 'LOW',
                    'action': 'Drop rows or simple imputation',
                    'code': f"df.dropna(subset=['{col}'], inplace=True)"
                }
            recommendations.append(rec)
    
    # 2. Duplicates
    dup_count = df.duplicated().sum()
    if dup_count > 0:
        recommendations.append({
            'column': 'ALL',
            'issue': 'Duplicate rows',
            'detail': f'{dup_count} duplicates ({(dup_count/len(df))*100:.1f}%)',
            'priority': 'HIGH',
            'action': 'Remove duplicate rows',
            'code': "df.drop_duplicates(inplace=True)"
        })
    
    # 3. Outliers in numerical columns
    for col in df.select_dtypes(include=[np.number]).columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        outliers = ((df[col] < Q1 - 1.5*IQR) | (df[col] > Q3 + 1.5*IQR)).sum()
        outlier_pct = (outliers / len(df)) * 100
        
        if outlier_pct > 5:
            recommendations.append({
                'column': col,
                'issue': 'Significant outliers',
                'detail': f'{outliers} outliers ({outlier_pct:.1f}%)',
                'priority': 'MEDIUM',
                'action': 'Cap outliers or transform data',
                'code': f"df['{col}'] = df['{col}'].clip(lower=Q1-1.5*IQR, upper=Q3+1.5*IQR)"
            })
    
    # 4. Text issues
    for col in df.select_dtypes(include=['object']).columns:
        # Whitespace issues
        if df[col].notna().any():
            whitespace_issues = df[col].str.strip().ne(df[col]).sum()
            if whitespace_issues > 0:
                recommendations.append({
                    'column': col,
                    'issue': 'Whitespace issues',
                    'detail': f'{whitespace_issues} values have leading/trailing whitespace',
                    'priority': 'LOW',
                    'action': 'Strip whitespace',
                    'code': f"df['{col}'] = df['{col}'].str.strip()"
                })
            
            # Case inconsistency
            unique_vals = df[col].dropna().unique()
            lower_unique = set(str(v).lower() for v in unique_vals)
            if len(unique_vals) > len(lower_unique):
                recommendations.append({
                    'column': col,
                    'issue': 'Case inconsistency',
                    'detail': f'Different cases represent same values',
                    'priority': 'MEDIUM',
                    'action': 'Standardize case',
                    'code': f"df['{col}'] = df['{col}'].str.lower()"
                })
    
    # 5. Memory optimization
    for col in df.select_dtypes(include=['int64']).columns:
        if df[col].min() >= 0 and df[col].max() < 255:
            recommendations.append({
                'column': col,
                'issue': 'Memory inefficiency',
                'detail': 'Can use smaller integer type',
                'priority': 'LOW',
                'action': 'Convert to uint8',
                'code': f"df['{col}'] = df['{col}'].astype('uint8')"
            })
    
    # Sort by priority
    priority_order = {'HIGH': 0, 'MEDIUM': 1, 'LOW': 2}
    recommendations.sort(key=lambda x: priority_order[x['priority']])
    
    # Print recommendations
    print(f"\nFound {len(recommendations)} recommendations:\n")
    
    for i, rec in enumerate(recommendations, 1):
        priority_emoji = {'HIGH': '🚨', 'MEDIUM': '⚠️', 'LOW': '💡'}[rec['priority']]
        print(f"{i}. {priority_emoji} [{rec['priority']}] {rec['column']}: {rec['issue']}")
        print(f"   Detail: {rec['detail']}")
        print(f"   Action: {rec['action']}")
        print(f"   Code: {rec['code']}")
        print()
    
    print("="*60)
    
    return recommendations

# Generate recommendations
recommendations = generate_cleaning_recommendations(df)

# Create automated cleaning script
def generate_cleaning_script(recommendations, output_file=None):
    """
    Generate Python cleaning script from recommendations
    """
    script = '''"""
Auto-generated Data Cleaning Script
"""

import pandas as pd
import numpy as np

def clean_data(df):
    """
    Apply all recommended cleaning steps
    """
    df_cleaned = df.copy()
    
'''
    
    for rec in recommendations:
        script += f"    # {rec['issue']} - {rec['column']}\n"
        script += f"    # {rec['action']}\n"
        script += f"    {rec['code']}\n\n"
    
    script += '''    return df_cleaned

if __name__ == "__main__":
    # Load your data
    df = pd.read_csv("your_data.csv")
    
    # Clean data
    df_cleaned = clean_data(df)
    
    # Save cleaned data
    df_cleaned.to_csv("cleaned_data.csv", index=False)
    print("Data cleaning complete!")
'''
    
    if output_file:
        with open(output_file, 'w') as f:
            f.write(script)
        print(f"Script saved to {output_file}")
    
    return script

# Generate script
script = generate_cleaning_script(recommendations)
print("\nGenerated Cleaning Script:")
print(script[:500] + "...")
15. Best Practices and Common Pitfalls
15.1 Best Practices
Python

"""
DATA CLEANING BEST PRACTICES
============================

1. ALWAYS WORK ON A COPY
   - Never modify original data
   - Keep raw data immutable
"""

# Good practice
df_original = pd.read_csv('data.csv')
df_working = df_original.copy()

# Bad practice
# df = pd.read_csv('data.csv')
# df.dropna(inplace=True)  # Original lost!

"""
2. DOCUMENT EVERYTHING
   - Log all cleaning steps
   - Track row/column changes
   - Record decisions and reasons
"""

class CleaningLogger:
    """Logger for tracking cleaning operations"""
    
    def __init__(self):
        self.log = []
    
    def add_entry(self, operation, before_shape, after_shape, details=""):
        entry = {
            'timestamp': pd.Timestamp.now(),
            'operation': operation,
            'rows_before': before_shape[0],
            'rows_after': after_shape[0],
            'rows_changed': before_shape[0] - after_shape[0],
            'cols_before': before_shape[1],
            'cols_after': after_shape[1],
            'details': details
        }
        self.log.append(entry)
        print(f"[LOG] {operation}: {before_shape} → {after_shape}")
    
    def get_log(self):
        return pd.DataFrame(self.log)
    
    def save_log(self, filepath):
        self.get_log().to_csv(filepath, index=False)

# Usage
logger = CleaningLogger()
before = df.shape
df_cleaned = df.dropna()
logger.add_entry("Remove nulls", before, df_cleaned.shape)

"""
3. VALIDATE AT EACH STEP
   - Check data integrity after operations
   - Verify expected outcomes
"""

def validate_cleaning_step(df_before, df_after, operation):
    """Validate a cleaning step"""
    validations = []
    
    # Row count check
    if len(df_after) > len(df_before):
        validations.append(f"⚠️ Row count increased ({len(df_before)} → {len(df_after)})")
    
    # Column check
    missing_cols = set(df_before.columns) - set(df_after.columns)
    if missing_cols:
        validations.append(f"⚠️ Columns removed: {missing_cols}")
    
    # Data type check
    for col in df_after.columns:
        if col in df_before.columns:
            if df_before[col].dtype != df_after[col].dtype:
                validations.append(f"⚠️ {col} dtype changed: {df_before[col].dtype} → {df_after[col].dtype}")
    
    # Null check
    new_nulls = df_after.isnull().sum().sum() - df_before.isnull().sum().sum()
    if new_nulls > 0:
        validations.append(f"⚠️ New nulls introduced: {new_nulls}")
    
    if validations:
        print(f"\nValidation warnings for '{operation}':")
        for v in validations:
            print(f"  {v}")
    else:
        print(f"✅ '{operation}' passed validation")
    
    return len(validations) == 0

"""
4. USE REPRODUCIBLE METHODS
   - Set random seeds
   - Save configurations
   - Version control your code
"""

# Set random seed for reproducibility
np.random.seed(42)

# Save configuration
cleaning_config = {
    'missing_threshold': 0.5,
    'outlier_multiplier': 1.5,
    'datetime_format': '%Y-%m-%d',
    'version': '1.0.0'
}

import json
with open('cleaning_config.json', 'w') as f:
    json.dump(cleaning_config, f, indent=2)

"""
5. HANDLE EDGE CASES
   - Empty DataFrames
   - Single row/column
   - All nulls
   - All duplicates
"""

def safe_clean(df, operations):
    """Safely apply cleaning operations with edge case handling"""
    
    # Check for empty DataFrame
    if df.empty:
        print("Warning: DataFrame is empty")
        return df
    
    # Check for single row
    if len(df) == 1:
        print("Warning: DataFrame has only one row")
        # Skip certain operations
        operations = [op for op in operations if op != 'remove_outliers']
    
    # Apply operations with error handling
    df_cleaned = df.copy()
    for op in operations:
        try:
            df_cleaned = op(df_cleaned)
        except Exception as e:
            print(f"Error in {op.__name__}: {e}")
            # Continue with previous state
    
    return df_cleaned
15.2 Common Pitfalls
Python

"""
COMMON PITFALLS AND HOW TO AVOID THEM
=====================================
"""

# PITFALL 1: Data Leakage
# -----------------------
# Calculating statistics on entire dataset before splitting

# ❌ WRONG: Impute using mean of entire dataset
mean_all = df['value'].mean()
df['value'].fillna(mean_all, inplace=True)
# Then split into train/test
# Test data now contains information from training data!

# ✅ CORRECT: Split first, then impute
from sklearn.model_selection import train_test_split

train, test = train_test_split(df, test_size=0.2, random_state=42)
train_mean = train['value'].mean()
train['value'].fillna(train_mean, inplace=True)
test['value'].fillna(train_mean, inplace=True)  # Use TRAIN mean!

print("Pitfall 1: Always split before calculating statistics for imputation")


# PITFALL 2: Ignoring the Impact on Distribution
# -----------------------------------------------

def check_distribution_impact(before, after, column):
    """Check if cleaning changed distribution significantly"""
    import matplotlib.pyplot as plt
    from scipy import stats
    
    fig, axes = plt.subplots(1, 2, figsize=(12, 4))
    
    axes[0].hist(before[column].dropna(), bins=30, alpha=0.7, label='Before')
    axes[0].hist(after[column].dropna(), bins=30, alpha=0.7, label='After')
    axes[0].legend()
    axes[0].set_title('Distribution Comparison')
    
    # KS test
    stat, pvalue = stats.ks_2samp(before[column].dropna(), after[column].dropna())
    axes[1].text(0.5, 0.5, f'KS Statistic: {stat:.4f}\nP-value: {pvalue:.4f}',
                ha='center', va='center', fontsize=14)
    axes[1].set_title('Distribution Test')
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()
    
    if pvalue < 0.05:
        print("⚠️ Distribution significantly changed!")
    else:
        print("✅ Distribution not significantly changed")

print("Pitfall 2: Always check distribution before and after cleaning")


# PITFALL 3: Incorrect Chained Operations
# ----------------------------------------

# ❌ WRONG: Chained assignment warning
# df[df['col'] > 0]['col2'] = 1  # May not work as expected

# ✅ CORRECT: Use loc
# df.loc[df['col'] > 0, 'col2'] = 1

print("Pitfall 3: Use .loc for chained assignments")


# PITFALL 4: Not Considering Data Types
# -------------------------------------

# ❌ WRONG: Treating all columns the same
def bad_impute(df):
    return df.fillna(0)  # 0 for text columns doesn't make sense

# ✅ CORRECT: Handle types appropriately
def good_impute(df):
    df_cleaned = df.copy()
    
    for col in df_cleaned.columns:
        if df_cleaned[col].dtype in ['int64', 'float64']:
            df_cleaned[col].fillna(df_cleaned[col].median(), inplace=True)
        elif df_cleaned[col].dtype == 'object':
            df_cleaned[col].fillna('Unknown', inplace=True)
        elif df_cleaned[col].dtype == 'datetime64[ns]':
            # Don't fill datetime with arbitrary value
            pass
    
    return df_cleaned

print("Pitfall 4: Handle different data types appropriately")


# PITFALL 5: Over-Cleaning
# ------------------------

def assess_over_cleaning(original_df, cleaned_df):
    """Check if too much data was removed"""
    
    rows_removed = len(original_df) - len(cleaned_df)
    removal_pct = (rows_removed / len(original_df)) * 100
    
    print(f"Rows removed: {rows_removed} ({removal_pct:.1f}%)")
    
    if removal_pct > 30:
        print("🚨 WARNING: More than 30% of data removed!")
        print("   Consider:")
        print("   - Using imputation instead of deletion")
        print("   - Relaxing outlier thresholds")
        print("   - Reviewing cleaning criteria")
    elif removal_pct > 10:
        print("⚠️ CAUTION: More than 10% of data removed")
        print("   Verify this is justified")
    else:
        print("✅ Data removal within acceptable range")
    
    return removal_pct

print("Pitfall 5: Be careful not to over-clean")


# PITFALL 6: Not Handling Categorical Variables Properly
# ------------------------------------------------------

# ❌ WRONG: Creating new categories during test time
train_categories = ['A', 'B', 'C']
# Test data has 'D' which wasn't in training → error

# ✅ CORRECT: Handle unknown categories
def safe_categorical_encoding(train_df, test_df, column):
    """Safely encode categoricals handling unknowns"""
    
    # Get training categories
    known_categories = set(train_df[column].unique())
    
    # Replace unknown categories in test
    test_df[column] = test_df[column].apply(
        lambda x: x if x in known_categories else 'UNKNOWN'
    )
    
    # Ensure 'UNKNOWN' is in training too
    if 'UNKNOWN' not in known_categories:
        train_df.loc[train_df.index[0], column] = 'UNKNOWN'
        train_df.loc[train_df.index[0], column] = train_df[column].mode()[0]
    
    return train_df, test_df

print("Pitfall 6: Handle unknown categories in test data")
15.3 Final Checklist
Python

def data_cleaning_checklist(df, run_checks=True):
    """
    Comprehensive data cleaning checklist
    
    Parameters:
    -----------
    df : DataFrame
        Cleaned dataframe to validate
    run_checks : bool
        Whether to run automated checks
    
    Returns:
    --------
    Checklist results
    """
    print("="*60)
    print("DATA CLEANING FINAL CHECKLIST")
    print("="*60)
    
    checklist = {
        'completeness': [],
        'validity': [],
        'consistency': [],
        'documentation': []
    }
    
    # COMPLETENESS CHECKS
    print("\n📋 COMPLETENESS")
    
    # Missing values
    missing_pct = (df.isnull().sum().sum() / (df.shape[0] * df.shape[1])) * 100
    if missing_pct == 0:
        checklist['completeness'].append("✅ No missing values")
    elif missing_pct < 5:
        checklist['completeness'].append(f"⚠️ Low missing values ({missing_pct:.1f}%)")
    else:
        checklist['completeness'].append(f"❌ High missing values ({missing_pct:.1f}%)")
    
    # Required columns (example)
    # required_cols = ['id', 'date', 'value']
    # missing_required = [c for c in required_cols if c not in df.columns]
    # if missing_required:
    #     checklist['completeness'].append(f"❌ Missing required columns: {missing_required}")
    
    for item in checklist['completeness']:
        print(f"  {item}")
    
    # VALIDITY CHECKS
    print("\n📋 VALIDITY")
    
    # Duplicates
    dup_count = df.duplicated().sum()
    if dup_count == 0:
        checklist['validity'].append("✅ No duplicate rows")
    else:
        checklist['validity'].append(f"❌ {dup_count} duplicate rows found")
    
    # Data types
    object_cols = df.select_dtypes(include=['object']).columns
    if len(object_cols) > 0:
        checklist['validity'].append(f"⚠️ {len(object_cols)} object columns (may need encoding)")
    
    # Negative values in typically positive columns
    for col in df.select_dtypes(include=[np.number]).columns:
        if 'id' in col.lower() or 'count' in col.lower() or 'quantity' in col.lower():
            neg_count = (df[col] < 0).sum()
            if neg_count > 0:
                checklist['validity'].append(f"❌ {col}: {neg_count} negative values")
    
    for item in checklist['validity']:
        print(f"  {item}")
    
    # CONSISTENCY CHECKS
    print("\n📋 CONSISTENCY")
    
    # Consistent formatting
    for col in df.select_dtypes(include=['object']).columns:
        if df[col].notna().any():
            # Check whitespace
            ws_issues = df[col].str.strip().ne(df[col]).sum()
            if ws_issues > 0:
                checklist['consistency'].append(f"⚠️ {col}: {ws_issues} whitespace issues")
            
            # Check case consistency
            unique = df[col].dropna().unique()
            lower_unique = set(str(v).lower() for v in unique)
            if len(unique) > len(lower_unique):
                checklist['consistency'].append(f"⚠️ {col}: Case inconsistency detected")
    
    if not checklist['consistency']:
        checklist['consistency'].append("✅ No consistency issues detected")
    
    for item in checklist['consistency']:
        print(f"  {item}")
    
    # DOCUMENTATION CHECKS
    print("\n📋 DOCUMENTATION")
    checklist['documentation'] = [
        "□ Cleaning steps documented",
        "□ Decisions and rationale recorded",
        "□ Data dictionary updated",
        "□ Version control updated",
        "□ Backup of original data saved"
    ]
    
    for item in checklist['documentation']:
        print(f"  {item}")
    
    # SUMMARY
    total_issues = sum(
        1 for items in checklist.values() 
        for item in items 
        if item.startswith('❌')
    )
    total_warnings = sum(
        1 for items in checklist.values() 
        for item in items 
        if item.startswith('⚠️')
    )
    
    print("\n" + "="*60)
    print("SUMMARY")
    print("="*60)
    print(f"  Issues (❌): {total_issues}")
    print(f"  Warnings (⚠️): {total_warnings}")
    
    if total_issues == 0 and total_warnings == 0:
        print("\n  🎉 DATA IS CLEAN AND READY!")
    elif total_issues == 0:
        print("\n  ✅ Data is clean with minor warnings")
    else:
        print("\n  🚨 Please address issues before proceeding")
    
    print("="*60)
    
    return checklist

# Run checklist
checklist_results = data_cleaning_checklist(df)
15.4 Quick Reference Card
Python

quick_reference = """
╔══════════════════════════════════════════════════════════════════╗
║               DATA CLEANING QUICK REFERENCE CARD                  ║
╠════════════════════════════════════════════════════════════════���═╣
║                                                                   ║
║  MISSING VALUES                                                   ║
║  ─────────────                                                    ║
║  df.isnull().sum()              # Count nulls per column          ║
║  df.dropna()                    # Drop rows with nulls            ║
║  df.fillna(value)               # Fill nulls with value           ║
║  df.fillna(df.mean())           # Fill with mean                  ║
║  df.interpolate()               # Interpolate missing             ║
║                                                                   ║
║  DUPLICATES                                                       ║
║  ──────────                                                       ║
║  df.duplicated().sum()          # Count duplicates                ║
║  df.drop_duplicates()           # Remove duplicates               ║
║  df.drop_duplicates(subset=[])  # By specific columns             ║
║                                                                   ║
║  DATA TYPES                                                       ║
║  ──────────                                                       ║
║  df.dtypes                      # Check types                     ║
║  df.astype(dtype)               # Convert type                    ║
║  pd.to_numeric(s, errors='coerce')  # Convert to numeric         ║
║  pd.to_datetime(s)              # Convert to datetime             ║
║                                                                   ║
║  OUTLIERS                                                         ║
║  ────────                                                         ║
║  Q1, Q3 = df.quantile([0.25, 0.75])  # Quartiles                ║
║  IQR = Q3 - Q1                   # Interquartile range           ║
║  df.clip(lower, upper)           # Cap outliers                   ║
║                                                                   ║
║  TEXT CLEANING                                                    ║
║  ─────────────                                                    ║
║  s.str.strip()                   # Remove whitespace              ║
║  s.str.lower()                   # Lowercase                      ║
║  s.str.replace(pattern, '')      # Remove pattern                 ║
║  s.str.extract(pattern)          # Extract pattern                ║
║                                                                   ║
║  VALIDATION                                                       ║
║  ──────────                                                       ║
║  df.describe()                   # Summary statistics             ║
║  df.info()                       # Column info                    ║
║  df.value_counts()               # Value distribution             ║
║                                                                   ║
╚══════════════════════════════════════════════════════════════════╝
"""

print(quick_reference)
Conclusion
Python


CONGRATULATIONS! 🎉
==================

You have completed the comprehensive Data Cleaning guide!

KEY TAKEAWAYS:
─────────────

1. DATA CLEANING IS ESSENTIAL
   - Garbage In = Garbage Out
   - 60-80% of data science work is cleaning
   - Clean data = Better models

2. SYSTEMATIC APPROACH
   - Always start with exploration
   - Document every step
   - Validate after each operation
   - Keep original data intact

3. KNOW YOUR TECHNIQUES
   - Missing Data: Drop, Impute (Simple, KNN, MICE)
   - Duplicates: Exact matching, Fuzzy matching
   - Outliers: Z-score, IQR, Isolation Forest
   - Text: Standardization, Normalization
   - Dates: Parsing, Validation, Feature extraction

4. CONTEXT MATTERS
   - No one-size-fits-all solution
   - Domain knowledge is crucial
   - Business rules guide decisions

5. AUTOMATION IS KEY
   - Build reusable pipelines
   - Create standardized functions
   - Document configurations

NEXT STEPS:
──────────
1. Practice with real datasets
2. Build your own cleaning library
3. Learn domain-specific techniques
4. Explore advanced tools (Great Expectations, Pandas Profiling)

"""

# Final summary function
def create_study_summary():
    """
    Create a comprehensive study summary for quick revision
    """
    
    summary = """
╔══════════════════════════════════════════════════════════════════════════╗
║                    DATA CLEANING STUDY SUMMARY                            ║
╠══════════════════════════════════════════════════════════════════════════╣
║                                                                           ║
║  CHAPTER 1-4: FOUNDATIONS                                                 ║
║  ────────────────────────                                                 ║
║  • Data Cleaning = Detecting & correcting errors in data                  ║
║  • 6 Quality Dimensions: Accuracy, Completeness, Consistency,             ║
║    Timeliness, Validity, Uniqueness                                       ║
║  • Essential Libraries: pandas, numpy, matplotlib, seaborn, sklearn       ║
║  • First Steps: df.head(), df.info(), df.describe(), df.shape            ║
║                                                                           ║
║  CHAPTER 5: MISSING DATA                                                  ║
║  ───────────────────────                                                  ║
║  • Types: MCAR (random), MAR (related to other data), MNAR (systematic)  ║
║  • Strategies:                                                            ║
║    - Deletion: dropna() - when < 5% missing                              ║
║    - Simple Imputation: fillna(mean/median/mode)                         ║
║    - Advanced: KNN Imputer, MICE (Iterative Imputer)                     ║
║  • Decision: < 5% → delete, 5-20% → simple impute, > 20% → advanced      ║
║                                                                           ║
║  CHAPTER 6: DUPLICATES                                                    ║
║  ─────────────────────                                                    ║
║  • Types: Exact, Partial, Fuzzy                                          ║
║  • Detection: df.duplicated(), df.duplicated(subset=[cols])              ║
║  • Removal: df.drop_duplicates(keep='first'/'last'/False)                ║
║  • Fuzzy Matching: SequenceMatcher, fuzzywuzzy library                   ║
║                                                                           ║
║  CHAPTER 7: DATA TYPES                                                    ║
║  ─────────────────────                                                    ║
║  • Common Types: int64, float64, object, bool, datetime64, category      ║
║  • Conversions:                                                           ║
║    - pd.to_numeric(errors='coerce')                                      ║
║    - pd.to_datetime(format='%Y-%m-%d')                                   ║
║    - df.astype('category') for memory efficiency                         ║
║  • Memory: int8 < int16 < int32 < int64                                  ║
║                                                                           ║
║  CHAPTER 8: OUTLIERS                                                      ║
║  ───────────────────                                                      ║
║  • Detection Methods:                                                     ║
║    - Z-Score: |z| > 3 is outlier                                         ║
║    - IQR: < Q1-1.5*IQR or > Q3+1.5*IQR                                  ║
║    - Isolation Forest: ML-based                                          ║
║    - DBSCAN: Density-based clustering                                    ║
║  • Handling: Remove, Cap/Winsorize, Transform (log, sqrt), Bin           ║
║                                                                           ║
║  CHAPTER 9: TEXT DATA                                                     ║
║  ────────────────────                                                     ║
║  • Basic: strip(), lower(), replace()                                    ║
║  • Advanced: regex patterns, HTML removal, standardization               ║
║  • Validation: Email, Phone, Address patterns                            ║
║  • For NLP: Remove stopwords, punctuation, lemmatization                 ║
║                                                                           ║
║  CHAPTER 10: DATE/TIME                                                    ║
║  ─────────────────────                                                    ║
║  • Parsing: pd.to_datetime() with format strings                         ║
║  • Format Codes: %Y (year), %m (month), %d (day), %H:%M:%S               ║
║  • Validation: Check ranges, no future dates, logical consistency        ║
║  • Features: year, month, day, dayofweek, is_weekend, cyclical encoding  ║
║                                                                           ║
║  CHAPTER 11: CONSISTENCY                                                  ║
║  ───────────────────────                                                  ║
║  • Value Standardization: Create mappings for variations                 ║
║  • Unit Conversion: Convert to standard units                            ║
║  • Cross-field Validation: Check related fields match                    ║
║                                                                           ║
║  CHAPTER 12: FEATURE ENGINEERING                                          ║
║  ───────────────────────────────                                          ║
║  • Numerical: Ratios, Aggregations, Bins, Transformations                ║
║  • Categorical: Combining, Extracting, Frequency encoding                ║
║  • DateTime: Components, Cyclical, Time differences                      ║
║                                                                           ║
║  CHAPTER 13: ADVANCED                                                     ║
║  ────────────────────                                                     ║
║  • Imbalanced Data: Detection and documentation                          ║
║  • Multi-table: Referential integrity                                    ║
║  • Large Data: Chunked processing, Dask                                  ║
║  • Quality Scoring: Automated assessment                                 ║
║                                                                           ║
║  CHAPTER 14: AUTOMATION                                                   ║
║  ───────────────────────                                                  ║
║  • Build reusable pipeline classes                                       ║
║  • Automated profiling and recommendations                               ║
║  • Generate cleaning scripts automatically                               ║
║                                                                           ║
║  CHAPTER 15: BEST PRACTICES                                               ║
║  ───────────────────────────                                              ║
║  • Always work on a copy                                                 ║
║  • Document everything                                                   ║
║  • Validate at each step                                                 ║
║  • Use reproducible methods                                              ║
║  • Handle edge cases                                                     ║
║  • Avoid: Data leakage, Over-cleaning, Ignoring distributions           ║
║                                                                           ║
╚══════════════════════════════════════════════════════════════════════════╝
"""
    
    return summary

# Print study summary
print(create_study_summary())


# Complete code template for any data cleaning project
def create_project_template():
    """
    Create a complete project template for data cleaning
    """
    
    template = '''
"""
DATA CLEANING PROJECT TEMPLATE
==============================
Project: [PROJECT_NAME]
Author: [YOUR_NAME]
Date: [DATE]
Description: [BRIEF_DESCRIPTION]
"""

# ============================================================
# IMPORTS
# ============================================================
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime
import warnings
warnings.filterwarnings('ignore')

# Display settings
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', 100)

# ============================================================
# CONFIGURATION
# ============================================================
CONFIG = {
    'input_file': 'data/raw/input_data.csv',
    'output_file': 'data/processed/cleaned_data.csv',
    'log_file': 'logs/cleaning_log.csv',
    'random_seed': 42,
    
    # Cleaning parameters
    'missing_threshold': 0.5,      # Drop columns with > 50% missing
    'outlier_multiplier': 1.5,     # IQR multiplier for outlier detection
    'duplicate_subset': None,       # Columns to check for duplicates
    
    # Column specifications
    'datetime_columns': [],
    'categorical_columns': [],
    'numerical_columns': [],
    'id_columns': [],
    'target_column': None,
}

np.random.seed(CONFIG['random_seed'])

# ============================================================
# LOGGING CLASS
# ============================================================
class CleaningLog:
    def __init__(self):
        self.entries = []
        self.start_time = datetime.now()
    
    def log(self, step, before_shape, after_shape, details=""):
        self.entries.append({
            'timestamp': datetime.now(),
            'step': step,
            'rows_before': before_shape[0],
            'rows_after': after_shape[0],
            'cols_before': before_shape[1],
            'cols_after': after_shape[1],
            'details': details
        })
        print(f"[{step}] {before_shape} → {after_shape} | {details}")
    
    def save(self, filepath):
        pd.DataFrame(self.entries).to_csv(filepath, index=False)
        print(f"Log saved to {filepath}")
    
    def summary(self):
        if not self.entries:
            return "No entries logged"
        
        first = self.entries[0]
        last = self.entries[-1]
        
        return f"""
Cleaning Summary:
─────────────────
Total steps: {len(self.entries)}
Duration: {datetime.now() - self.start_time}
Rows: {first['rows_before']} → {last['rows_after']} ({first['rows_before'] - last['rows_after']} removed)
Cols: {first['cols_before']} → {last['cols_after']}
"""

log = CleaningLog()

# ============================================================
# HELPER FUNCTIONS
# ============================================================
def load_data(filepath):
    """Load data from file"""
    print(f"Loading data from {filepath}...")
    
    if filepath.endswith('.csv'):
        df = pd.read_csv(filepath)
    elif filepath.endswith('.xlsx'):
        df = pd.read_excel(filepath)
    elif filepath.endswith('.json'):
        df = pd.read_json(filepath)
    else:
        raise ValueError(f"Unsupported file format: {filepath}")
    
    print(f"Loaded {df.shape[0]} rows, {df.shape[1]} columns")
    return df

def save_data(df, filepath):
    """Save data to file"""
    print(f"Saving data to {filepath}...")
    
    if filepath.endswith('.csv'):
        df.to_csv(filepath, index=False)
    elif filepath.endswith('.xlsx'):
        df.to_excel(filepath, index=False)
    elif filepath.endswith('.json'):
        df.to_json(filepath, orient='records')
    
    print(f"Saved {df.shape[0]} rows, {df.shape[1]} columns")

def explore_data(df):
    """Initial data exploration"""
    print("\\n" + "="*60)
    print("DATA EXPLORATION")
    print("="*60)
    
    print(f"\\nShape: {df.shape}")
    print(f"\\nColumn Types:\\n{df.dtypes}")
    print(f"\\nMissing Values:\\n{df.isnull().sum()}")
    print(f"\\nDuplicates: {df.duplicated().sum()}")
    print(f"\\nSample Data:\\n{df.head()}")
    print(f"\\nStatistics:\\n{df.describe()}")

# ============================================================
# CLEANING FUNCTIONS
# ============================================================
def remove_duplicates(df, subset=None):
    """Remove duplicate rows"""
    before = df.shape
    df = df.drop_duplicates(subset=subset)
    log.log("Remove Duplicates", before, df.shape)
    return df

def handle_missing_values(df, threshold=0.5):
    """Handle missing values"""
    before = df.shape
    
    # Drop columns with too many missing values
    missing_pct = df.isnull().mean()
    cols_to_drop = missing_pct[missing_pct > threshold].index.tolist()
    df = df.drop(columns=cols_to_drop)
    
    # Fill remaining missing values
    for col in df.columns:
        if df[col].isnull().any():
            if df[col].dtype in ['int64', 'float64']:
                df[col] = df[col].fillna(df[col].median())
            else:
                df[col] = df[col].fillna(df[col].mode()[0] if len(df[col].mode()) > 0 else 'Unknown')
    
    log.log("Handle Missing", before, df.shape, f"Dropped columns: {cols_to_drop}")
    return df

def handle_outliers(df, columns=None, multiplier=1.5):
    """Handle outliers using IQR method"""
    before = df.shape
    
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    for col in columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - multiplier * IQR
        upper = Q3 + multiplier * IQR
        df[col] = df[col].clip(lower=lower, upper=upper)
    
    log.log("Handle Outliers", before, df.shape, f"Columns: {list(columns)}")
    return df

def clean_text_columns(df, columns=None):
    """Clean text columns"""
    before = df.shape
    
    if columns is None:
        columns = df.select_dtypes(include=['object']).columns
    
    for col in columns:
        df[col] = df[col].str.strip()
        df[col] = df[col].str.replace(r'\\s+', ' ', regex=True)
    
    log.log("Clean Text", before, df.shape, f"Columns: {list(columns)}")
    return df

def convert_data_types(df, datetime_cols=None, categorical_cols=None):
    """Convert data types"""
    before = df.shape
    
    if datetime_cols:
        for col in datetime_cols:
            if col in df.columns:
                df[col] = pd.to_datetime(df[col], errors='coerce')
    
    if categorical_cols:
        for col in categorical_cols:
            if col in df.columns:
                df[col] = df[col].astype('category')
    
    log.log("Convert Types", before, df.shape)
    return df

# ============================================================
# MAIN CLEANING PIPELINE
# ============================================================
def run_cleaning_pipeline(df, config):
    """Run the complete cleaning pipeline"""
    print("\\n" + "="*60)
    print("STARTING CLEANING PIPELINE")
    print("="*60)
    
    # Step 1: Initial exploration
    explore_data(df)
    
    # Step 2: Remove duplicates
    df = remove_duplicates(df, subset=config.get('duplicate_subset'))
    
    # Step 3: Handle missing values
    df = handle_missing_values(df, threshold=config.get('missing_threshold', 0.5))
    
    # Step 4: Clean text columns
    df = clean_text_columns(df, columns=config.get('text_columns'))
    
    # Step 5: Handle outliers
    df = handle_outliers(df, 
                        columns=config.get('numerical_columns'),
                        multiplier=config.get('outlier_multiplier', 1.5))
    
    # Step 6: Convert data types
    df = convert_data_types(df,
                           datetime_cols=config.get('datetime_columns'),
                           categorical_cols=config.get('categorical_columns'))
    
    print("\\n" + "="*60)
    print("PIPELINE COMPLETE")
    print("="*60)
    print(log.summary())
    
    return df

# ============================================================
# MAIN EXECUTION
# ============================================================
if __name__ == "__main__":
    # Load data
    df_raw = load_data(CONFIG['input_file'])
    
    # Run cleaning pipeline
    df_cleaned = run_cleaning_pipeline(df_raw, CONFIG)
    
    # Save cleaned data
    save_data(df_cleaned, CONFIG['output_file'])
    
    # Save log
    log.save(CONFIG['log_file'])
    
    print("\\n✅ Data cleaning complete!")
'''
    
    return template

# Print project template
print("\n" + "="*70)
print("PROJECT TEMPLATE")
print("="*70)
print(create_project_template()[:2000] + "\n... [TEMPLATE CONTINUES]")


# Final interview preparation questions and answers
def interview_prep():
    """
    Common interview questions about data cleaning
    """
    
    qa = """
╔══════════════════════════════════════════════════════════════════════════╗
║              DATA CLEANING INTERVIEW Q&A                                  ║
╠══════════════════════════════════════════════════════════════════════════╣

Q1: What is data cleaning and why is it important?
────────────────────────────────────────────────────
A: Data cleaning is the process of identifying and correcting errors,
   inconsistencies, and inaccuracies in datasets. It's important because:
   - "Garbage In, Garbage Out" - model quality depends on data quality
   - Data scientists spend 60-80% of time on data preparation
   - Clean data leads to accurate insights and predictions
   - Poor data quality costs businesses trillions annually

Q2: How do you handle missing values?
──────────────────────────────────────
A: The approach depends on:
   1. Percentage missing:
      - < 5%: Can delete rows or simple imputation
      - 5-30%: KNN or regression-based imputation
      - > 30%: Consider dropping column or advanced methods
   
   2. Type of missingness:
      - MCAR: Any method works
      - MAR: Use related variables for imputation
      - MNAR: Need domain knowledge
   
   3. Data type:
      - Numerical: Mean, median, or model-based
      - Categorical: Mode or "Unknown" category

Q3: How do you detect outliers?
────────────────────────────────
A: Multiple methods exist:
   1. Statistical: Z-score (> 3 std), IQR (1.5 × IQR rule)
   2. Visual: Box plots, scatter plots, histograms
   3. ML-based: Isolation Forest, DBSCAN, LOF
   
   Handle by:
   - Removal (if errors)
   - Capping/Winsorization
   - Transformation (log, sqrt)
   - Using robust algorithms

Q4: What's the difference between data cleaning and preprocessing?
──────────────────────────────────────────────────────────────────
A: Data Cleaning:
   - Fixing errors, inconsistencies
   - Handling missing values
   - Removing duplicates
   - Standardizing formats
   
   Preprocessing (for ML):
   - Feature scaling/normalization
   - Encoding categorical variables
   - Feature selection
   - Dimensionality reduction

Q5: How do you handle duplicates?
──────────────────────────────────
A: 1. Exact duplicates: drop_duplicates()
   2. Fuzzy duplicates: String similarity matching (Levenshtein, Jaro-Winkler)
   3. Consider which to keep: first, last, or aggregate
   4. Define what makes a "duplicate" (all columns or subset?)

Q6: How would you handle inconsistent data formats?
───────────────────────────────────────────────────
A: 1. Identify variations: df['col'].value_counts()
   2. Create mapping dictionaries for standardization
   3. Use regex for pattern-based cleaning
   4. Implement validation rules
   5. Document transformations

Q7: What is data leakage and how do you prevent it during cleaning?
───────────────────────────────────────────────────────────────────
A: Data leakage occurs when information from outside the training
   dataset is used to create the model.
   
   Prevention:
   - Split data BEFORE any calculations
   - Calculate statistics (mean, median) only on training data
   - Apply same transformations to test data using training parameters
   - Be careful with time-series (no future data)

Q8: How do you validate data quality?
─────────────────────────────────────
A: Six dimensions:
   1. Completeness: Missing value percentage
   2. Uniqueness: Duplicate detection
   3. Validity: Data type and format checks
   4. Consistency: Cross-field validation
   5. Accuracy: Compare with trusted sources
   6. Timeliness: Data freshness
   
   Tools: Great Expectations, Pandas Profiling, custom validators

Q9: What tools do you use for data cleaning?
────────────────────────────────────────────
A: Python:
   - Pandas: Primary tool for manipulation
   - NumPy: Numerical operations
   - Scikit-learn: Imputation, encoding
   - FuzzyWuzzy: String matching
   - Great Expectations: Validation
   
   Other:
   - OpenRefine: Interactive cleaning
   - Trifacta: Visual data wrangling
   - SQL: Database-level cleaning

Q10: How do you document your cleaning process?
───────────────────────────────────────────────
A: 1. Maintain a cleaning log (before/after states)
   2. Version control code (Git)
   3. Create data dictionaries
   4. Document decisions and rationale
   5. Save configuration files
   6. Keep original data immutable
   7. Generate automated reports

╚══════════════════════════════════════════════════════════════════════════╝
"""
    
    return qa

print(interview_prep())


# Certification of completion
def print_certificate():
    """Print completion certificate"""
    
    certificate = """
    
    ╔═══════════════════════════════════════════════════════════════════╗
    ║                                                                   ║
    ║                    🎓 CERTIFICATE OF COMPLETION 🎓                 ║
    ║                                                                   ║
    ║     ─────────────────────────────────────────────────────────    ║
    ║                                                                   ║
    ║                    DATA CLEANING MASTERY COURSE                   ║
    ║                                                                   ║
    ║                     From Beginner to Expert                       ║
    ║                                                                   ║
    ║     ─────────────────────────────────────────────────────────    ║
    ║                                                                   ║
    ║     This certifies successful completion of comprehensive         ║
    ║     training in Data Cleaning covering:                          ║
    ║                                                                   ║
    ║     ✓ Data Exploration & Profiling                               ║
    ║     ✓ Missing Data Handling                                      ║
    ║     ✓ Duplicate Detection & Removal                              ║
    ║     ✓ Data Type Conversions                                      ║
    ║     ✓ Outlier Detection & Treatment                              ║
    ║     ✓ Text Data Cleaning                                         ║
    ║     ✓ Date/Time Processing                                       ║
    ║     ✓ Data Consistency & Standardization                         ║
    ║     ✓ Feature Engineering                                        ║
    ║     ✓ Advanced Techniques                                        ║
    ║     ✓ Pipeline Automation                                        ║
    ║     ✓ Best Practices                                             ║
    ║                                                                   ║
    ║     ─────────────────────────────────────────────────────────    ║
    ║                                                                   ║
    ║          "Clean Data is the Foundation of Great Models"          ║
    ║                                                                   ║
    ║                          🌟 🌟 🌟 🌟 🌟                            ║
    ║                                                                   ║
    ╚═══════════════════════════════════════════════════════════════════╝
    
    
    WHAT'S NEXT?
    ────────────
    1. 📊 Practice with real datasets (Kaggle, UCI ML Repository)
    2. 🛠️ Build your own cleaning library
    3. 📚 Learn specific domain cleaning (Healthcare, Finance, NLP)
    4. 🔧 Explore tools: Great Expectations, Pandas Profiling, Dask
    5. 🎯 Apply in ML projects
    
    RESOURCES:
    ──────────
    • Kaggle Datasets: kaggle.com/datasets
    • UCI ML Repository: archive.ics.uci.edu/ml
    • Pandas Documentation: pandas.pydata.org
    • Scikit-learn: scikit-learn.org
    
    
    Thank you for learning! Good luck with your ML career! 🚀
    
    """
    
    print(certificate)

print_certificate()
Appendix: Complete Code Reference
Python

"""
APPENDIX: COMPLETE CODE REFERENCE
=================================

All essential functions in one place for easy copy-paste
"""

# ============================================================
# MISSING DATA FUNCTIONS
# ============================================================

def analyze_missing(df):
    """Comprehensive missing data analysis"""
    missing = pd.DataFrame({
        'column': df.columns,
        'missing_count': df.isnull().sum().values,
        'missing_pct': (df.isnull().sum().values / len(df)) * 100,
        'dtype': df.dtypes.values
    })
    return missing.sort_values('missing_pct', ascending=False)

def impute_missing(df, strategy='auto'):
    """Impute missing values based on data type"""
    df_imputed = df.copy()
    for col in df_imputed.columns:
        if df_imputed[col].isnull().any():
            if df_imputed[col].dtype in ['int64', 'float64']:
                if strategy == 'mean':
                    df_imputed[col].fillna(df_imputed[col].mean(), inplace=True)
                else:  # median as default for numerical
                    df_imputed[col].fillna(df_imputed[col].median(), inplace=True)
            else:
                df_imputed[col].fillna(df_imputed[col].mode()[0], inplace=True)
    return df_imputed


# ============================================================
# DUPLICATE FUNCTIONS
# ============================================================

def find_duplicates(df, subset=None):
    """Find and return duplicate rows"""
    return df[df.duplicated(subset=subset, keep=False)]

def remove_duplicates(df, subset=None, keep='first'):
    """Remove duplicates with logging"""
    before = len(df)
    df_clean = df.drop_duplicates(subset=subset, keep=keep)
    print(f"Removed {before - len(df_clean)} duplicates")
    return df_clean


# ============================================================
# OUTLIER FUNCTIONS
# ============================================================

def detect_outliers_iqr(df, columns=None, multiplier=1.5):
    """Detect outliers using IQR method"""
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    outliers = {}
    for col in columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - multiplier * IQR
        upper = Q3 + multiplier * IQR
        mask = (df[col] < lower) | (df[col] > upper)
        outliers[col] = {'count': mask.sum(), 'lower': lower, 'upper': upper}
    return outliers

def cap_outliers(df, columns=None, multiplier=1.5):
    """Cap outliers using IQR method"""
    df_capped = df.copy()
    if columns is None:
        columns = df.select_dtypes(include=[np.number]).columns
    
    for col in columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - multiplier * IQR
        upper = Q3 + multiplier * IQR
        df_capped[col] = df_capped[col].clip(lower=lower, upper=upper)
    return df_capped


# ============================================================
# TEXT CLEANING FUNCTIONS
# ============================================================

def clean_text(series, operations=None):
    """Clean text with specified operations"""
    if operations is None:
        operations = ['strip', 'lower', 'remove_extra_spaces']
    
    cleaned = series.astype(str)
    
    if 'strip' in operations:
        cleaned = cleaned.str.strip()
    if 'lower' in operations:
        cleaned = cleaned.str.lower()
    if 'upper' in operations:
        cleaned = cleaned.str.upper()
    if 'title' in operations:
        cleaned = cleaned.str.title()
    if 'remove_extra_spaces' in operations:
        cleaned = cleaned.str.replace(r'\s+', ' ', regex=True)
    if 'remove_special' in operations:
        cleaned = cleaned.str.replace(r'[^a-zA-Z0-9\s]', '', regex=True)
    
    return cleaned

def standardize_nulls(series):
    """Convert various null representations to NaN"""
    null_values = ['null', 'NULL', 'None', 'none', 'NA', 'N/A', 'n/a', 
                   'nan', 'NaN', '', ' ', '-', '--', 'missing', 'unknown']
    cleaned = series.copy()
    mask = series.astype(str).str.strip().str.lower().isin([v.lower() for v in null_values])
    cleaned.loc[mask] = np.nan
    return cleaned


# ============================================================
# DATE FUNCTIONS
# ============================================================

def parse_dates(series, formats=None):
    """Parse dates trying multiple formats"""
    if formats is None:
        formats = ['%Y-%m-%d', '%m/%d/%Y', '%d/%m/%Y', '%Y-%m-%d %H:%M:%S']
    
    for fmt in formats:
        try:
            return pd.to_datetime(series, format=fmt, errors='coerce')
        except:
            continue
    
    return pd.to_datetime(series, infer_datetime_format=True, errors='coerce')

def extract_date_features(series, prefix=''):
    """Extract features from datetime series"""
    dt = pd.to_datetime(series, errors='coerce')
    features = pd.DataFrame()
    features[f'{prefix}year'] = dt.dt.year
    features[f'{prefix}month'] = dt.dt.month
    features[f'{prefix}day'] = dt.dt.day
    features[f'{prefix}dayofweek'] = dt.dt.dayofweek
    features[f'{prefix}is_weekend'] = (dt.dt.dayofweek >= 5).astype(int)
    return features


# ============================================================
# VALIDATION FUNCTIONS
# ============================================================

def validate_data(df, rules):
    """Validate data against rules"""
    results = []
    
    for rule in rules:
        name = rule['name']
        check = rule['check']
        
        try:
            passed = check(df)
            results.append({'rule': name, 'passed': passed, 'error': None})
        except Exception as e:
            results.append({'rule': name, 'passed': False, 'error': str(e)})
    
    return pd.DataFrame(results)

def data_quality_score(df):
    """Calculate overall data quality score"""
    scores = {
        'completeness': (1 - df.isnull().sum().sum() / (df.shape[0] * df.shape[1])) * 100,
        'uniqueness': (len(df) - df.duplicated().sum()) / len(df) * 100
    }
    scores['overall'] = np.mean(list(scores.values()))
    return scores


# ============================================================
# QUICK PIPELINE
# ============================================================

def quick_clean(df, config=None):
    """Quick cleaning with sensible defaults"""
    if config is None:
        config = {
            'drop_duplicates': True,
            'handle_missing': 'auto',
            'cap_outliers': True,
            'clean_text': True
        }
    
    df_clean = df.copy()
    
    if config.get('drop_duplicates'):
        df_clean = remove_duplicates(df_clean)
    
    if config.get('handle_missing'):
        df_clean = impute_missing(df_clean)
    
    if config.get('cap_outliers'):
        df_clean = cap_outliers(df_clean)
    
    if config.get('clean_text'):
        text_cols = df_clean.select_dtypes(include=['object']).columns
        for col in text_cols:
            df_clean[col] = clean_text(df_clean[col])
    
    return df_clean


print("""
╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║                    END OF COMPREHENSIVE GUIDE                    ║
║                                                                  ║
║      Thank you for reading! Now go clean some data! 🧹📊        ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
""")
This completes the comprehensive Data Cleaning guide covering:

✅ Introduction to Data Cleaning
✅ Understanding Data Quality
✅ Setting Up Your Environment
✅ Data Exploration Basics
✅ Handling Missing Data
✅ Dealing with Duplicates
✅ Data Type Conversions
✅ Handling Outliers
✅ Text Data Cleaning
✅ Date and Time Data Cleaning
✅ Data Consistency and Standardization
✅ Feature Engineering During Cleaning
✅ Advanced Techniques
✅ Automation and Pipelines
✅ Best Practices and Common Pitfalls
