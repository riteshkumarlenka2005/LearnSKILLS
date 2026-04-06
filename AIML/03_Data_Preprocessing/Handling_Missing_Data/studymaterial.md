Handling Missing Data: From Absolute Beginner to Expert
A Complete Guide by Professor AI
15 Years of Teaching Experience Distilled

Table of Contents
Introduction - What is Missing Data?
Types of Missing Data
How to Detect Missing Data
Impact of Missing Data on ML Models
Basic Techniques - Deletion Methods
Simple Imputation Methods
Advanced Imputation Methods
Machine Learning Based Imputation
Deep Learning Based Imputation
Handling Missing Data in Different Data Types
Practical Implementation Guide
Common Pitfalls & How to Avoid Them
Interview Questions & Answers
1. Introduction - What is Missing Data?
1.1 Simple Definition
Missing Data: Values that are NOT present in your dataset where they SHOULD be present.

1.2 Real-Life Examples
Let me explain with everyday scenarios:

text

Example 1: Hospital Patient Records
┌─────────┬─────┬────────┬─────────────┬──────────────┐
│ Patient │ Age │ Weight │ Blood Type  │ Temperature  │
├─────────┼─────┼────────┼─────────────┼──────────────┤
│ John    │ 45  │ 70kg   │ A+          │ 98.6°F       │
│ Mary    │ 32  │ ???    │ B-          │ 99.1°F       │  ← Weight missing!
│ Peter   │ 28  │ 85kg   │ ???         │ 98.2°F       │  ← Blood type missing!
│ Sarah   │ ???│ 55kg   │ O+          │ ???          │  ← Age & Temp missing!
└─────────┴─────┴────────┴─────────────┴──────────────┘

Example 2: E-Commerce Customer Data
┌──────────┬──────────┬────────────┬──────────────┬─────────────┐
│ Customer │ Age      │ Income     │ Last Purchase│ Email       │
├──────────┼──────────┼────────────┼──────────────┼─────────────┤
│ C001     │ 35       │ $75,000    │ 2024-01-15   │ yes@mail.com│
│ C002     │ 28       │ NaN        │ 2024-02-20   │ no@mail.com │ ← Income missing!
│ C003     │ NaN      │ $90,000    │ NaN          │ hi@mail.com │ ← Age & Purchase missing!
│ C004     │ 42       │ $120,000   │ 2024-03-10   │ NaN         │ ← Email missing!
└──────────┴──────────┴────────────┴──────────────┴─────────────┘
1.3 How Missing Values Appear in Data
Python

# In Python/Pandas, missing values appear as:

import numpy as np
import pandas as pd

# Different representations of missing values
missing_representations = {
    'NaN':       np.nan,           # Most common in Pandas
    'None':      None,             # Python's null
    'NA':        pd.NA,            # Pandas NA (newer)
    'NaT':       pd.NaT,           # Not a Time (for datetime)
    'Empty':     '',               # Empty string
    'Whitespace':' ',              # Just spaces
    'Placeholder': -999,           # Custom placeholder
    'Placeholder': 'N/A',          # Text placeholder
    'Placeholder': 'NULL',         # Database null
    'Placeholder': '?',            # Question mark
}
1.4 Visual Representation of Missing Data
text

COMPLETE DATA (Ideal):
┌────┬────┬────┬────┬────┐
│ ■  │ ■  │ ■  │ ■  │ ■  │
├────┼────┼────┼────┼────┤
│ ■  │ ■  │ ■  │ ■  │ ■  │
├────┼────┼────┼────┼────┤
│ ■  │ ■  │ ■  │ ■  │ ■  │
├────┼────┼────┼────┼────┤
│ ■  │ ■  │ ■  │ ■  │ ■  │
└────┴────┴────┴────┴────┘
■ = Data present

DATA WITH MISSING VALUES (Reality):
┌────┬────┬────┬────┬────┐
│ ■  │ ■  │ □  │ ■  │ ■  │  ← Missing in column 3
├────┼────┼────┼────┼────┤
│ ■  │ □  │ ■  │ ■  │ □  │  ← Missing in columns 2 and 5
├────┼────┼────┼────┼────┤
│ □  │ ■  │ ■  │ □  │ ■  │  ← Missing in columns 1 and 4
├────┼────┼────┼────┼────┤
│ ■  │ ■  │ ■  │ ■  │ ■  │  ← Complete row
└────┴────┴────┴────┴────┘
□ = Missing data (NaN)
1.5 Why Do Missing Values Occur?
text

┌────────────────────────┬────────────────────────────────────────────────────┐
│ Reason                 │ Example                                            │
├────────────────────────┼────────────────────────────────────────────────────┤
│ Data Entry Errors      │ Human forgot to fill a field                       │
│ Equipment Malfunction  │ Sensor failed to record temperature                │
│ Survey Non-Response    │ Participant skipped a question                     │
│ Privacy Concerns       │ Customer refused to share income                   │
│ Data Corruption        │ Database error during transfer                     │
│ Not Applicable         │ "Number of children" for unmarried person          │
│ Merge/Join Issues      │ Combining datasets with different IDs              │
│ System Design          │ Optional fields in forms                           │
│ Time-Related           │ Feature didn't exist when older data was collected │
│ Collection Constraints │ Too expensive/difficult to collect certain data    │
└────────────────────────┴────────────────────────────────────────────────────┘
2. Types of Missing Data
2.1 The Three Types - CRUCIAL CONCEPT!
Understanding the TYPE of missing data is THE MOST IMPORTANT CONCEPT because it determines which technique to use!

text

┌──────────────────────────────────────────────────────────────────────────────┐
│                        TYPES OF MISSING DATA                                 │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. MCAR (Missing Completely At Random)                                     │
│     → Missing values have NO relationship with ANY data                      │
│     → Pure random chance                                                     │
│     → EASIEST to handle                                                      │
│                                                                              │
│  2. MAR (Missing At Random)                                                 │
│     → Missing values related to OTHER OBSERVED variables                     │
│     → Not truly random, but predictable from other columns                   │
│     → MODERATE difficulty                                                    │
│                                                                              │
│  3. MNAR (Missing Not At Random)                                            │
│     → Missing values related to THE MISSING VALUE ITSELF                     │
│     → Systematic missingness                                                 │
│     → HARDEST to handle                                                      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
2.2 MCAR - Missing Completely At Random
Definition: The probability of missing data is EQUAL for ALL observations. Missingness has NO relationship with any data (observed or unobserved).

Analogy:

text

Imagine a survey form blown away by random wind.
The wind doesn't care about what's written on the form.
COMPLETELY RANDOM!
Real-World Example:

text

Hospital Blood Test Records:
┌─────────┬─────┬────────────┬──────────────────────────────────────┐
│ Patient │ Age │ Blood Sugar│ Why Missing?                         │
├─────────┼─────┼────────────┼──────────────────────────────────────┤
│ John    │ 45  │ 120        │                                      │
│ Mary    │ 32  │ NaN        │ ← Lab equipment randomly malfunctioned│
│ Peter   │ 28  │ 95         │                                      │
│ Sarah   │ 55  │ NaN        │ ← Sample accidentally dropped        │
│ Mike    │ 40  │ 110        │                                      │
└─────────┴─────┴────────────┴──────────────────────────────────────┘

The missingness has NOTHING to do with:
- The patient's actual blood sugar level
- The patient's age
- Any other factor

It's pure random accident!
Statistical Property:

text

P(Missing) is CONSTANT for all observations

P(Blood Sugar Missing | Any Variable) = P(Blood Sugar Missing)

The probability of missing doesn't depend on anything!
How to Detect:

Python

# Statistical test: Little's MCAR Test
# If p-value > 0.05, data is likely MCAR

# Simple check: Compare distributions
# If means/distributions are similar between complete and incomplete groups
# → Likely MCAR

# Example
complete_age = df[df['income'].notna()]['age'].mean()
incomplete_age = df[df['income'].isna()]['age'].mean()

if abs(complete_age - incomplete_age) < threshold:
    print("Possibly MCAR")
Why MCAR is GOOD NEWS:

text

✅ Simplest to handle
✅ Any imputation method works reasonably
✅ Listwise deletion (removing rows) won't bias results
✅ Analysis on complete cases is still valid
2.3 MAR - Missing At Random
Definition: The probability of missing data depends on OTHER OBSERVED variables, but NOT on the missing value itself.

Important: "Random" is misleading! It's NOT truly random - it's predictable from other columns.

Analogy:

text

Survey about salary:
- Young people often skip the salary question
- The missingness depends on AGE (observed)
- But NOT on the actual salary value itself

Age → Causes → Salary Missing
(We can see age, so we can predict who skips)
Real-World Example:

text

Income Survey:
┌─────────┬─────┬────────────┬────────────┬──────────────────────────┐
│ Person  │ Age │ Education  │ Income     │ Why Missing?             │
├─────────┼─────┼────────────┼────────────┼──────────────────────────┤
│ John    │ 55  │ PhD        │ $150,000   │                          │
│ Mary    │ 22  │ Bachelor   │ NaN        │ ← Young people shy about │
│ Peter   │ 45  │ Master     │ $95,000    │   income (Age effect)    │
│ Sarah   │ 20  │ High School│ NaN        │ ← Same pattern           │
│ Mike    │ 60  │ PhD        │ $200,000   │                          │
│ Lisa    │ 23  │ Bachelor   │ NaN        │ ← Same pattern           │
└─────────┴─────┴────────────┴────────────┴──────────────────────────┘

Pattern: Young people (Age < 25) tend to not report income
- The missingness DEPENDS on AGE (which we observe)
- But NOT on the actual income amount

If we know someone is young → higher chance income is missing
This is MAR!
Statistical Property:

text

P(Missing | Observed Variables) ≠ P(Missing | Missing Value)

P(Income Missing | Age=22) > P(Income Missing | Age=55)

The probability of missing depends on AGE (observed),
but NOT on the actual income value (unobserved)
How to Detect:

Python

# Check if missingness correlates with other variables
import pandas as pd

# Create indicator for missing
df['income_missing'] = df['income'].isna().astype(int)

# Check correlation with other variables
correlations = df.corr()['income_missing']
print(correlations)

# If income_missing correlates with age, education, etc. → MAR

# Visual check
import matplotlib.pyplot as plt
df.groupby('age_group')['income_missing'].mean().plot(kind='bar')
plt.title('Missing Rate by Age Group')
# If bars are different heights → MAR
Why MAR is MANAGEABLE:

text

✅ Can use sophisticated imputation methods
✅ Multiple imputation works well
✅ Model-based imputation (using other variables) is effective
⚠️ Listwise deletion may cause bias (but it's fixable)
2.4 MNAR - Missing Not At Random
Definition: The probability of missing data depends on THE MISSING VALUE ITSELF (even after accounting for observed variables).

Analogy:

text

Survey about income:
- HIGH income people don't report (to avoid attention)
- LOW income people don't report (embarrassment)
- The missingness depends on the ACTUAL income value!

Actual Income → Causes → Income Missing
(We CAN'T see the income, so we CAN'T predict who skips)
Real-World Example:

text

Salary Survey:
┌─────────┬─────┬────────────┬────────────┬──────────────────────────────┐
│ Person  │ Age │ Education  │ Income     │ Why Missing?                 │
├─────────┼─────┼────────────┼────────────┼──────────────────────────────┤
│ John    │ 55  │ PhD        │ $150,000   │                              │
│ Mary    │ 48  │ Master     │ NaN        │ ← Earns $500K, too high to   │
│         │     │            │            │   share (actual value causes │
│         │     │            │            │   missingness!)              │
│ Peter   │ 45  │ Bachelor   │ $75,000    │                              │
│ Sarah   │ 50  │ PhD        │ NaN        │ ← Earns $25K, embarrassed    │
│         │     │            │            │   (actual value causes       │
│         │     │            │            │   missingness!)              │
└─────────┴─────┴────────────┴────────────┴──────────────────────────────┘

Pattern: 
- Very high earners hide income (privacy)
- Very low earners hide income (shame)
- The ACTUAL VALUE determines missingness!

We CANNOT predict this from age, education, etc.
This is MNAR!
More MNAR Examples:

text

┌────────────────────────┬────────────────────────────────────────────────┐
│ Scenario               │ Why it's MNAR                                  │
├────────────────────────┼────────────────────────────────────────────────┤
│ Depression Survey      │ Severely depressed people too ill to respond  │
│                        │ → Depression level causes missingness         │
├────────────────────────┼────────────────────────────────────────────────┤
│ Drug Side Effects      │ Patients with severe side effects drop out    │
│                        │ → Severity causes missingness                 │
├────────────────────────┼────────────────────────────────────────────────┤
│ Weight Measurement     │ Obese patients avoid scale                    │
│                        │ → Actual weight causes missingness            │
├────────────────────────┼────────────────────────────────────────────────┤
│ Exam Scores            │ Students who failed don't report scores       │
│                        │ → Actual score causes missingness             │
└────────────────────────┴────────────────────────────────────────────────┘
Statistical Property:

text

P(Missing | Actual Value) varies with the actual value

P(Income Missing | Income=$500K) > P(Income Missing | Income=$75K)

The probability of missing depends on the actual (unobserved) value!
Why MNAR is PROBLEMATIC:

text

❌ HARDEST to handle
❌ Standard imputation methods FAIL
❌ Will bias ALL analyses
❌ Requires domain knowledge to address
❌ May need special models (selection models, pattern mixture models)
❌ Often requires making assumptions that can't be verified
2.5 Summary Comparison
text

┌─────────────────┬─────────────────────┬─────────────────────┬────────────────────┐
│ Aspect          │ MCAR                │ MAR                 │ MNAR               │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Missingness     │ Pure random         │ Depends on OTHER    │ Depends on THE     │
│ depends on      │                     │ observed variables  │ missing value      │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Predictable?    │ No                  │ Yes (from other     │ No (can't see      │
│                 │                     │ columns)            │ missing value)     │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Example         │ Lab error           │ Young people skip   │ Rich people hide   │
│                 │                     │ income question     │ income             │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Handling        │ Easy                │ Moderate            │ Difficult          │
│ Difficulty      │                     │                     │                    │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Best Approach   │ Any method works    │ Model-based         │ Domain expertise + │
│                 │ Listwise OK         │ imputation          │ special models     │
├─────────────────┼─────────────────────┼─────────────────────┼────────────────────┤
│ Bias Risk       │ Low                 │ Moderate (fixable)  │ High (hard to fix) │
└─────────────────┴─────────────────────┴─────────────────────┴────────────────────┘
2.6 Visual Decision Tree
text

START: Why is the data missing?
    │
    ├─ "I have no idea, seems random" 
    │   └─→ Likely MCAR
    │       (Lab error, random system glitch)
    │
    ├─ "It's related to OTHER columns I can see"
    │   └─→ Likely MAR
    │       (Young people skip income, certain regions have missing data)
    │
    └─ "It's probably related to the ACTUAL missing value"
        └─→ Likely MNAR
            (Rich hide income, sick skip health surveys)
3. How to Detect Missing Data
3.1 Basic Detection Methods
Python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Create sample data with missing values
df = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, np.nan, 55, 30, np.nan, 45, 50],
    'Income': [50000, 60000, np.nan, 80000, 70000, np.nan, 55000, 65000, np.nan, 90000],
    'City': ['NYC', 'LA', 'Chicago', np.nan, 'NYC', 'LA', np.nan, 'Chicago', 'NYC', np.nan],
    'Score': [85, 90, np.nan, np.nan, 88, 92, 78, np.nan, 95, 87]
})

print("Sample DataFrame:")
print(df)
3.2 Method 1: Check for Missing Values
Python

# ============================================================
# CHECK IF MISSING VALUES EXIST
# ============================================================

# Check if ANY missing values exist
print("Any missing values?", df.isnull().any().any())

# Check missing values per column
print("\nMissing values per column:")
print(df.isnull().sum())

# Output:
# Age       3
# Income    3
# City      3
# Score     4
3.3 Method 2: Missing Value Statistics
Python

# ============================================================
# COMPREHENSIVE MISSING VALUE STATISTICS
# ============================================================

def missing_value_analysis(df):
    """
    Complete analysis of missing values in a DataFrame
    """
    # Calculate statistics
    total_cells = df.size
    total_missing = df.isnull().sum().sum()
    total_present = total_cells - total_missing
    
    print("="*60)
    print("MISSING VALUE ANALYSIS")
    print("="*60)
    
    # Overall statistics
    print(f"\n📊 Overall Statistics:")
    print(f"   Total cells:     {total_cells}")
    print(f"   Missing cells:   {total_missing}")
    print(f"   Present cells:   {total_present}")
    print(f"   Missing %:       {(total_missing/total_cells)*100:.2f}%")
    
    # Per-column statistics
    print(f"\n📊 Per-Column Statistics:")
    print("-"*60)
    
    for column in df.columns:
        missing_count = df[column].isnull().sum()
        total_count = len(df[column])
        missing_pct = (missing_count / total_count) * 100
        dtype = df[column].dtype
        
        print(f"   {column:15} | Missing: {missing_count:4} ({missing_pct:5.1f}%) | Type: {dtype}")
    
    # Per-row statistics
    print(f"\n📊 Row Statistics:")
    rows_with_missing = df.isnull().any(axis=1).sum()
    complete_rows = len(df) - rows_with_missing
    print(f"   Rows with missing values:    {rows_with_missing}")
    print(f"   Complete rows:               {complete_rows}")
    print(f"   Complete rows %:             {(complete_rows/len(df))*100:.1f}%")
    
    return df.isnull().sum()

# Run analysis
missing_stats = missing_value_analysis(df)
Output:

text

============================================================
MISSING VALUE ANALYSIS
============================================================

📊 Overall Statistics:
   Total cells:     40
   Missing cells:   13
   Present cells:   27
   Missing %:       32.50%

📊 Per-Column Statistics:
------------------------------------------------------------
   Age             | Missing:    3 ( 30.0%) | Type: float64
   Income          | Missing:    3 ( 30.0%) | Type: float64
   City            | Missing:    3 ( 30.0%) | Type: object
   Score           | Missing:    4 ( 40.0%) | Type: float64

📊 Row Statistics:
   Rows with missing values:    8
   Complete rows:               2
   Complete rows %:             20.0%
3.4 Method 3: Visual Detection
Python

# ============================================================
# VISUAL MISSING VALUE ANALYSIS
# ============================================================

def visualize_missing_data(df):
    """
    Create visualizations for missing data
    """
    fig, axes = plt.subplots(2, 2, figsize=(14, 10))
    
    # 1. Heatmap of missing values
    ax1 = axes[0, 0]
    sns.heatmap(df.isnull(), cbar=True, yticklabels=False, cmap='viridis', ax=ax1)
    ax1.set_title('Missing Value Heatmap\n(Yellow = Missing)')
    
    # 2. Bar chart of missing values per column
    ax2 = axes[0, 1]
    missing_counts = df.isnull().sum()
    missing_counts.plot(kind='bar', ax=ax2, color='coral')
    ax2.set_title('Missing Values per Column')
    ax2.set_ylabel('Count')
    ax2.tick_params(axis='x', rotation=45)
    
    # 3. Percentage missing per column
    ax3 = axes[1, 0]
    missing_pct = (df.isnull().sum() / len(df)) * 100
    missing_pct.plot(kind='bar', ax=ax3, color='steelblue')
    ax3.set_title('Missing Percentage per Column')
    ax3.set_ylabel('Percentage (%)')
    ax3.axhline(y=50, color='red', linestyle='--', label='50% threshold')
    ax3.tick_params(axis='x', rotation=45)
    ax3.legend()
    
    # 4. Missing value pattern (which combinations occur together)
    ax4 = axes[1, 1]
    # Create binary matrix: 1 = present, 0 = missing
    pattern = df.isnull().astype(int)
    pattern_counts = pattern.groupby(list(df.columns)).size().reset_index(name='count')
    pattern_counts = pattern_counts.sort_values('count', ascending=False).head(10)
    
    ax4.text(0.5, 0.5, f'Rows with ANY missing: {df.isnull().any(axis=1).sum()}\n'
                       f'Complete rows: {(~df.isnull().any(axis=1)).sum()}\n'
                       f'Unique missing patterns: {len(pattern_counts)}',
             transform=ax4.transAxes, fontsize=14, verticalalignment='center',
             horizontalalignment='center', bbox=dict(boxstyle='round', facecolor='wheat'))
    ax4.set_title('Missing Data Summary')
    ax4.axis('off')
    
    plt.tight_layout()
    plt.show()

# Create visualization
visualize_missing_data(df)
3.5 Method 4: Using missingno Library
Python

# ============================================================
# ADVANCED VISUALIZATION WITH MISSINGNO
# ============================================================

# Install: pip install missingno
import missingno as msno

# 1. Matrix visualization
msno.matrix(df)
plt.title('Missing Value Matrix')
plt.show()

# 2. Bar chart
msno.bar(df)
plt.title('Missing Value Bar Chart')
plt.show()

# 3. Heatmap - Correlation of missingness
msno.heatmap(df)
plt.title('Missing Value Correlation Heatmap')
plt.show()

# 4. Dendrogram - Hierarchical clustering of missingness
msno.dendrogram(df)
plt.title('Missing Value Dendrogram')
plt.show()
What Each Visualization Shows:

text

┌─────────────────┬────────────────────────────────────────────────────────┐
│ Visualization   │ What It Shows                                          │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Matrix          │ Pattern of missing values across rows and columns      │
│                 │ White = Missing, Black = Present                       │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Bar Chart       │ How many non-missing values in each column             │
│                 │ Shorter bar = More missing                             │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Heatmap         │ Correlation between missing values in different columns│
│                 │ High correlation = Missing together                    │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Dendrogram      │ Hierarchical clustering of missing patterns            │
│                 │ Columns that cluster together have similar patterns    │
└─────────────────┴────────────────────────────────────────────────────────┘
3.6 Method 5: Detecting Missing Data Mechanisms
Python

# ============================================================
# DETECT TYPE OF MISSINGNESS (MCAR, MAR, MNAR)
# ============================================================

def detect_missingness_type(df, column):
    """
    Statistical tests to help determine missingness type
    """
    print(f"\n{'='*60}")
    print(f"MISSINGNESS ANALYSIS FOR: {column}")
    print(f"{'='*60}")
    
    # Create missing indicator
    df['_missing_indicator'] = df[column].isnull().astype(int)
    
    # For each other column, check if it correlates with missingness
    print("\nCorrelation with missingness:")
    print("-"*40)
    
    for other_col in df.columns:
        if other_col not in [column, '_missing_indicator']:
            if df[other_col].dtype in ['int64', 'float64']:
                # For numeric columns: t-test
                present_vals = df[df['_missing_indicator']==0][other_col].dropna()
                missing_vals = df[df['_missing_indicator']==1][other_col].dropna()
                
                if len(present_vals) > 1 and len(missing_vals) > 1:
                    from scipy import stats
                    t_stat, p_value = stats.ttest_ind(present_vals, missing_vals)
                    
                    significance = "***" if p_value < 0.01 else "**" if p_value < 0.05 else "*" if p_value < 0.1 else ""
                    
                    print(f"   {other_col:15} | p-value: {p_value:.4f} {significance}")
                    print(f"                    | Mean (present): {present_vals.mean():.2f}")
                    print(f"                    | Mean (missing):  {missing_vals.mean():.2f}")
    
    # Interpretation
    print("\n📌 Interpretation Guide:")
    print("   p < 0.05 → Missingness likely related to this variable (MAR)")
    print("   p > 0.05 → No evidence of relationship (possibly MCAR)")
    print("   Note: MNAR cannot be detected statistically!")
    
    # Cleanup
    df.drop('_missing_indicator', axis=1, inplace=True)

# Run detection
detect_missingness_type(df, 'Income')
4. Impact of Missing Data on ML Models
4.1 How Different Algorithms Handle Missing Data
text

┌───────────────────────────────────┬─────────────────────────────────────────────┐
│ Algorithm                         │ Handles Missing Natively?                   │
├───────────────────────────────────┼─────────────────────────────────────────────┤
│ Linear Regression (sklearn)       │ ❌ NO - Throws error                        │
│ Logistic Regression (sklearn)     │ ❌ NO - Throws error                        │
│ SVM (sklearn)                     │ ❌ NO - Throws error                        │
│ KNN (sklearn)                     │ ❌ NO - Throws error                        │
│ Neural Networks (TensorFlow/PyTorch)│ ❌ NO - Throws error or produces NaN     │
├───────────────────────────────────┼─────────────────────────────────────────────┤
│ Decision Trees (sklearn)          │ ❌ NO - Throws error (but can with tweaks)  │
│ Random Forest (sklearn)           │ ❌ NO - Throws error                        │
├───────────────────────────────────┼─────────────────────────────────────────────┤
│ XGBoost                          │ ✅ YES - Learns optimal direction for NaN   │
│ LightGBM                         │ ✅ YES - Native handling                     │
│ CatBoost                         │ ✅ YES - Native handling                     │
├───────────────────────────────────┼─────────────────────────────────────────────┤
│ Naive Bayes (sklearn)            │ ⚠️ PARTIAL - Can skip missing in calculation│
└───────────────────────────────────┴─────────────────────────────────────────────┘
4.2 Problems Caused by Missing Data
text

PROBLEM 1: ALGORITHM CRASHES
─────────────────────────────
from sklearn.linear_model import LinearRegression

X = [[1, 2], [3, np.nan], [5, 6]]  # Has NaN!
y = [1, 2, 3]

model = LinearRegression()
model.fit(X, y)  # 💥 ERROR: Input contains NaN!


PROBLEM 2: BIASED RESULTS
─────────────────────────────
If we delete rows with missing values:
- We might delete systematically (not randomly)
- Remaining data doesn't represent original population
- Model learns biased patterns


PROBLEM 3: REDUCED SAMPLE SIZE
─────────────────────────────
Original: 1000 rows
After deleting rows with ANY missing: 200 rows

Lost 800 rows of valuable information!
Model trained on insufficient data.


PROBLEM 4: LOSS OF INFORMATION
─────────────────────────────
Even rows with SOME missing values contain SOME useful info.
Deleting entire row wastes the present values.


PROBLEM 5: WRONG IMPUTATION BIAS
─────────────────────────────
If we impute incorrectly:
- Introduce artificial patterns
- Reduce variance artificially
- Model learns wrong relationships
4.3 Demonstration of Impact
Python

# ============================================================
# DEMONSTRATE IMPACT OF MISSING DATA
# ============================================================

from sklearn.linear_model import LinearRegression
from sklearn.model_selection import cross_val_score
import numpy as np
import pandas as pd

# Create complete dataset
np.random.seed(42)
n = 1000
X_complete = pd.DataFrame({
    'feature1': np.random.normal(50, 10, n),
    'feature2': np.random.normal(100, 20, n),
    'feature3': np.random.normal(75, 15, n)
})
y = 2*X_complete['feature1'] + 0.5*X_complete['feature2'] - X_complete['feature3'] + np.random.normal(0, 10, n)

# Score on complete data
model = LinearRegression()
complete_score = cross_val_score(model, X_complete, y, cv=5).mean()
print(f"Complete data R² score: {complete_score:.4f}")
print(f"Complete data samples: {len(X_complete)}")

# Create data with 30% missing (MCAR)
X_missing = X_complete.copy()
for col in X_missing.columns:
    mask = np.random.random(n) < 0.3  # 30% missing
    X_missing.loc[mask, col] = np.nan

print(f"\nMissing data samples: {len(X_missing)}")
print(f"Rows with ANY missing: {X_missing.isnull().any(axis=1).sum()}")

# Approach 1: Delete rows with missing
X_deleted = X_missing.dropna()
y_deleted = y[X_missing.dropna().index]
deleted_score = cross_val_score(model, X_deleted, y_deleted, cv=5).mean()
print(f"\nAfter deletion:")
print(f"   Remaining samples: {len(X_deleted)}")
print(f"   R² score: {deleted_score:.4f}")
print(f"   Data lost: {(1 - len(X_deleted)/len(X_complete))*100:.1f}%")

# Approach 2: Mean imputation
X_mean = X_missing.fillna(X_missing.mean())
mean_score = cross_val_score(model, X_mean, y, cv=5).mean()
print(f"\nAfter mean imputation:")
print(f"   Samples: {len(X_mean)}")
print(f"   R² score: {mean_score:.4f}")

print(f"\n📊 Summary:")
print(f"   Complete data:      R² = {complete_score:.4f}")
print(f"   After deletion:     R² = {deleted_score:.4f} (samples: {len(X_deleted)})")
print(f"   Mean imputation:    R² = {mean_score:.4f} (samples: {len(X_mean)})")
5. Basic Techniques - Deletion Methods
5.1 Overview of Deletion Methods
text

DELETION METHODS: Remove rows or columns with missing values

Types:
┌──────────────────────────────────────────────────────────────────────┐
│ 1. Listwise Deletion (Complete Case Analysis)                       │
│    → Remove entire ROW if ANY value is missing                       │
│                                                                      │
│ 2. Pairwise Deletion (Available Case Analysis)                       │
│    → Use available data for each analysis                            │
│                                                                      │
│ 3. Column Deletion                                                   │
│    → Remove entire COLUMN if too many values are missing             │
└──────────────────────────────────────────────────────────────────────┘
5.2 Listwise Deletion (Complete Case Analysis)
Concept: Remove any row that has AT LEAST ONE missing value.

text

Before Listwise Deletion:
┌─────┬─────┬─────┬─────┐
│ A   │ B   │ C   │ D   │
├─────┼─────┼─────┼─────┤
│ 1   │ 2   │ 3   │ 4   │  ✓ Keep (complete)
│ 5   │ NaN │ 7   │ 8   │  ✗ Delete (has NaN)
│ 9   │ 10  │ 11  │ 12  │  ✓ Keep (complete)
│ NaN │ 14  │ NaN │ 16  │  ✗ Delete (has NaN)
│ 17  │ 18  │ 19  │ 20  │  ✓ Keep (complete)
└─────┴─────┴─────┴─────┘

After Listwise Deletion:
┌─────┬─────┬─────┬─────┐
│ A   │ B   │ C   │ D   │
├─────┼─────┼─────┼─────┤
│ 1   │ 2   │ 3   │ 4   │
│ 9   │ 10  │ 11  │ 12  │
│ 17  │ 18  │ 19  │ 20  │
└─────┴─────┴─────┴─────┘

Lost: 2 out of 5 rows (40%!)
Code:

Python

# ============================================================
# LISTWISE DELETION
# ============================================================

import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'A': [1, 5, 9, np.nan, 17],
    'B': [2, np.nan, 10, 14, 18],
    'C': [3, 7, 11, np.nan, 19],
    'D': [4, 8, 12, 16, 20]
})

print("Original DataFrame:")
print(df)
print(f"Shape: {df.shape}")

# Method 1: dropna() - Drop rows with ANY missing values
df_listwise = df.dropna()

print("\nAfter Listwise Deletion:")
print(df_listwise)
print(f"Shape: {df_listwise.shape}")
print(f"Rows lost: {len(df) - len(df_listwise)} ({(len(df) - len(df_listwise))/len(df)*100:.1f}%)")
When to Use:

text

✅ Use Listwise Deletion When:
├── Missing data is MCAR (completely random)
├── Percentage of missing is LOW (<5%)
├── You have LOTS of data (can afford to lose some)
├── Quick analysis needed
└── Complete cases are representative

❌ Avoid Listwise Deletion When:
├── High percentage of missing data (>10%)
├── Missing is MAR or MNAR (will introduce bias)
├── Limited sample size
├── Missing values spread across many columns
└── Pattern of missingness is systematic
Pros and Cons:

text

PROS:
✓ Simple and fast
✓ No assumptions about missing data
✓ All analyses use same dataset
✓ No artificial data created

CONS:
✗ Can lose significant amount of data
✗ Reduces statistical power
✗ Can introduce bias (if not MCAR)
✗ Wastes information from partial rows
5.3 Pairwise Deletion (Available Case Analysis)
Concept: Use all available data for each specific calculation. Different analyses use different subsets.

text

Calculating correlations with Pairwise Deletion:

Data:
┌─────┬─────┬─────┐
│ A   │ B   │ C   │
├─────┼─────┼─────┤
│ 1   │ 2   │ NaN │
│ 3   │ NaN │ 5   │
│ 6   │ 7   │ 8   │
│ 9   │ 10  │ 11  │
└─────┴─────┴─────┘

Correlation(A, B):
Uses rows: 1, 3, 4 (where both A and B are present)
A: [1, 6, 9]
B: [2, 7, 10]

Correlation(A, C):
Uses rows: 2, 3, 4 (where both A and C are present)
A: [3, 6, 9]
C: [5, 8, 11]

Correlation(B, C):
Uses rows: 3, 4 (where both B and C are present)
B: [7, 10]
C: [8, 11]

Different sample sizes for each calculation!
Code:

Python

# ============================================================
# PAIRWISE DELETION
# ============================================================

# Pandas automatically uses pairwise deletion for correlations
df = pd.DataFrame({
    'A': [1, 3, 6, 9],
    'B': [2, np.nan, 7, 10],
    'C': [np.nan, 5, 8, 11]
})

print("Data:")
print(df)

# Correlation with pairwise deletion (default)
correlation = df.corr()
print("\nCorrelation Matrix (pairwise deletion):")
print(correlation)

# You can verify the sample sizes used
print("\nSample sizes for each correlation:")
for col1 in df.columns:
    for col2 in df.columns:
        if col1 < col2:
            n = df[[col1, col2]].dropna().shape[0]
            print(f"   {col1}-{col2}: n = {n}")
When to Use:

text

✅ Use Pairwise Deletion When:
├── Computing correlations or covariances
├── Want to maximize data usage
├── Missing is MCAR
└── Exploratory analysis

❌ Avoid Pairwise Deletion When:
├── Building ML models (need consistent rows)
├── Different sample sizes problematic
├── Missing is MAR or MNAR
└── Need interpretable results
5.4 Column Deletion (Feature Deletion)
Concept: Remove entire column if too many values are missing.

text

Before Column Deletion:
┌─────┬─────┬─────┬─────┐
│ A   │ B   │ C   │ D   │
├─────┼─────┼─────┼─────┤
│ 1   │ NaN │ 3   │ 4   │
│ 5   │ NaN │ 7   │ 8   │
│ 9   │ NaN │ 11  │ 12  │
│ 13  │ 14  │ 15  │ 16  │
│ 17  │ NaN │ 19  │ 20  │
└─────┴─────┴─────┴─────┘

Column B has 80% missing → DELETE!

After Column Deletion:
┌─────┬─────┬─────┐
│ A   │ C   │ D   │
├─────┼─────┼─────┤
│ 1   │ 3   │ 4   │
│ 5   │ 7   │ 8   │
│ 9   │ 11  │ 12  │
│ 13  │ 15  │ 16  │
│ 17  │ 19  │ 20  │
└─────┴─────┴─────┘

All rows preserved!
Code:

Python

# ============================================================
# COLUMN DELETION
# ============================================================

def delete_columns_with_missing(df, threshold=0.5):
    """
    Delete columns with missing percentage above threshold
    
    Parameters:
    -----------
    df : DataFrame
    threshold : float (0 to 1)
        Maximum allowed missing percentage
    
    Returns:
    --------
    DataFrame with columns deleted
    """
    # Calculate missing percentage for each column
    missing_pct = df.isnull().sum() / len(df)
    
    # Find columns above threshold
    columns_to_drop = missing_pct[missing_pct > threshold].index.tolist()
    
    print(f"Missing percentage per column:")
    for col in df.columns:
        pct = missing_pct[col] * 100
        drop_status = "← DROP" if col in columns_to_drop else ""
        print(f"   {col}: {pct:.1f}% {drop_status}")
    
    print(f"\nDropping {len(columns_to_drop)} columns: {columns_to_drop}")
    
    # Drop columns
    df_cleaned = df.drop(columns=columns_to_drop)
    
    return df_cleaned

# Example
df = pd.DataFrame({
    'A': [1, 5, 9, 13, 17],
    'B': [np.nan, np.nan, np.nan, 14, np.nan],  # 80% missing
    'C': [3, 7, 11, 15, 19],
    'D': [4, 8, np.nan, 16, 20]  # 20% missing
})

df_cleaned = delete_columns_with_missing(df, threshold=0.5)
print("\nResult:")
print(df_cleaned)
Threshold Guidelines:

text

┌────────────────────┬────────────────────────────────────────────────┐
│ Missing %          │ Recommendation                                 │
├────────────────────┼────────────────────────────────────────────────┤
│ 0% - 5%            │ Keep column, impute missing values             │
│ 5% - 20%           │ Keep column, use careful imputation            │
│ 20% - 50%          │ Consider deletion OR advanced imputation       │
│ 50% - 70%          │ Likely delete, unless very important feature   │
│ > 70%              │ Delete column (too little information)         │
└────────────────────┴────────────────────────────────────────────────┘

BUT ALWAYS CONSIDER:
- How important is this feature?
- Can we get the data from another source?
- Is the missingness informative? (Create "is_missing" indicator)
5.5 Comparison of Deletion Methods
Python

# ============================================================
# COMPARISON OF DELETION METHODS
# ============================================================

def compare_deletion_methods(df):
    """
    Compare different deletion methods
    """
    original_shape = df.shape
    
    print("="*60)
    print("COMPARISON OF DELETION METHODS")
    print("="*60)
    print(f"\nOriginal shape: {original_shape}")
    print(f"Original cells: {df.size}")
    print(f"Missing cells:  {df.isnull().sum().sum()}")
    
    # Method 1: Listwise deletion
    df_listwise = df.dropna()
    print(f"\n1. LISTWISE DELETION:")
    print(f"   Shape: {df_listwise.shape}")
    print(f"   Rows lost: {original_shape[0] - df_listwise.shape[0]}")
    print(f"   Data retained: {df_listwise.size/df.size*100:.1f}%")
    
    # Method 2: Column deletion (50% threshold)
    missing_pct = df.isnull().sum() / len(df)
    cols_to_drop = missing_pct[missing_pct > 0.5].index
    df_col_del = df.drop(columns=cols_to_drop)
    print(f"\n2. COLUMN DELETION (>50% missing):")
    print(f"   Shape: {df_col_del.shape}")
    print(f"   Columns dropped: {list(cols_to_drop)}")
    print(f"   Data retained: {df_col_del.size/df.size*100:.1f}%")
    
    # Method 3: Combined approach
    df_combined = df_col_del.dropna()
    print(f"\n3. COMBINED (Column then Listwise):")
    print(f"   Shape: {df_combined.shape}")
    print(f"   Data retained: {df_combined.size/df.size*100:.1f}%")
    
    return {
        'listwise': df_listwise,
        'column': df_col_del,
        'combined': df_combined
    }

# Example with realistic missing pattern
np.random.seed(42)
df = pd.DataFrame({
    'A': np.random.choice([1, 2, 3, np.nan], 100, p=[0.3, 0.3, 0.3, 0.1]),
    'B': np.random.choice([1, 2, 3, np.nan], 100, p=[0.25, 0.25, 0.25, 0.25]),
    'C': np.random.choice([1, 2, 3, np.nan], 100, p=[0.1, 0.1, 0.1, 0.7]),  # 70% missing
    'D': np.random.choice([1, 2, 3, np.nan], 100, p=[0.32, 0.32, 0.32, 0.04])
})

results = compare_deletion_methods(df)
6. Simple Imputation Methods
6.1 Overview of Imputation
Imputation: Replacing missing values with estimated/calculated values.

text

┌──────────────────────────────────────────────────────────────────────┐
│                     IMPUTATION METHODS                               │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  SIMPLE METHODS:                                                     │
│  ├── Mean Imputation                                                 │
│  ├── Median Imputation                                               │
│  ├── Mode Imputation                                                 │
│  ├── Constant Imputation                                             │
│  └── Forward/Backward Fill                                           │
│                                                                      │
│  ADVANCED METHODS:                                                   │
│  ├── K-Nearest Neighbors (KNN) Imputation                            │
│  ├── Regression Imputation                                           │
│  ├── Multiple Imputation                                             │
│  └── Machine Learning Based (MICE, MissForest, etc.)                │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
6.2 Mean Imputation
Concept: Replace missing values with the MEAN (average) of the column.

text

Before Mean Imputation:
┌─────────┐
│ Salary  │
├─────────┤
│ 50000   │
│ NaN     │  ← Will be replaced with mean
│ 60000   │
│ NaN     │  ← Will be replaced with mean
│ 70000   │
└─────────┘

Mean = (50000 + 60000 + 70000) / 3 = 60000

After Mean Imputation:
┌─────────┐
│ Salary  │
├─────────┤
│ 50000   │
│ 60000   │  ← Filled with mean
│ 60000   │
│ 60000   │  ← Filled with mean
│ 70000   │
└─────────┘
Code:

Python

# ============================================================
# MEAN IMPUTATION
# ============================================================

import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer

# Sample data
df = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, np.nan, 55],
    'Salary': [50000, 60000, np.nan, 80000, 70000, np.nan]
})

print("Original Data:")
print(df)
print(f"\nMean of Age: {df['Age'].mean():.2f}")
print(f"Mean of Salary: {df['Salary'].mean():.2f}")

# Method 1: Using pandas fillna
df_mean_pandas = df.copy()
df_mean_pandas['Age'] = df_mean_pandas['Age'].fillna(df_mean_pandas['Age'].mean())
df_mean_pandas['Salary'] = df_mean_pandas['Salary'].fillna(df_mean_pandas['Salary'].mean())

print("\nAfter Mean Imputation (pandas):")
print(df_mean_pandas)

# Method 2: Using sklearn SimpleImputer
imputer = SimpleImputer(strategy='mean')
df_mean_sklearn = pd.DataFrame(
    imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter Mean Imputation (sklearn):")
print(df_mean_sklearn)
When to Use:

text

✅ Use Mean Imputation When:
├── Data is NUMERICAL and CONTINUOUS
├── Data is roughly NORMALLY distributed
├── Missing is MCAR
├── Quick solution needed
└── Low percentage of missing (<5%)

❌ Avoid Mean Imputation When:
├── Data is SKEWED (use median instead)
├── Data is CATEGORICAL (use mode instead)
├── High percentage of missing (>20%)
├── Missing is MAR or MNAR
└── Data has OUTLIERS
Problems with Mean Imputation:

text

PROBLEM 1: REDUCES VARIANCE
───────────────────────────
Original:  [10, 20, NaN, NaN, 50]
Mean = 26.67

After:     [10, 20, 26.67, 26.67, 50]

All missing values become the SAME number!
This artificially reduces spread/variance.


PROBLEM 2: DISTORTS CORRELATIONS
───────────────────────────
If X and Y are correlated:
- Missing X values should follow the relationship
- But mean doesn't consider Y at all!
- Correlation gets weakened.


PROBLEM 3: DOESN'T HANDLE OUTLIERS
───────────────────────────
Data: [10, 20, 30, NaN, 1000]
Mean = 265 (pulled by outlier!)

Imputing 265 doesn't make sense for this data.
6.3 Median Imputation
Concept: Replace missing values with the MEDIAN of the column.

text

Why Median is Better for Skewed Data:

Data: [10, 20, 30, NaN, 1000]  ← 1000 is outlier

Mean = (10 + 20 + 30 + 1000) / 4 = 265  ← Pulled by outlier!
Median = 25  ← Not affected by outlier!

Median is the MIDDLE value when sorted.
Code:

Python

# ============================================================
# MEDIAN IMPUTATION
# ============================================================

df = pd.DataFrame({
    'Income': [30000, 40000, np.nan, 50000, np.nan, 500000]  # Has outlier!
})

print("Original Data:")
print(df)
print(f"\nMean: ${df['Income'].mean():,.2f}")
print(f"Median: ${df['Income'].median():,.2f}")

# Mean imputation
df_mean = df.copy()
df_mean['Income'] = df_mean['Income'].fillna(df_mean['Income'].mean())

# Median imputation
df_median = df.copy()
df_median['Income'] = df_median['Income'].fillna(df_median['Income'].median())

print("\nMean Imputation:")
print(df_mean)

print("\nMedian Imputation:")
print(df_median)

# Using sklearn
from sklearn.impute import SimpleImputer

imputer_median = SimpleImputer(strategy='median')
df_median_sklearn = pd.DataFrame(
    imputer_median.fit_transform(df),
    columns=df.columns
)

print("\nMedian Imputation (sklearn):")
print(df_median_sklearn)
When to Use:

text

✅ Use Median Imputation When:
├── Data is NUMERICAL
├── Data is SKEWED
├── Data has OUTLIERS
├── Quick robust solution needed
└── Missing is MCAR

❌ Avoid Median Imputation When:
├── Data is CATEGORICAL (use mode)
├── High percentage missing
└── Missing is MAR or MNAR
6.4 Mode Imputation
Concept: Replace missing values with the MODE (most frequent value). Essential for CATEGORICAL data!

text

Before Mode Imputation:
┌─────────┐
│ City    │
├─────────┤
│ NYC     │  ← Occurs 3 times
│ NYC     │
│ NaN     │  ← Will be NYC (most frequent)
│ LA      │  ← Occurs 2 times
│ NYC     │
│ LA      │
│ NaN     │  ← Will be NYC (most frequent)
└─────────┘

Mode = "NYC" (appears most frequently)

After Mode Imputation:
┌─────────┐
│ City    │
├─────────┤
│ NYC     │
│ NYC     │
│ NYC     │  ← Filled with mode
│ LA      │
│ NYC     │
│ LA      │
│ NYC     │  ← Filled with mode
└─────────┘
Code:

Python

# ============================================================
# MODE IMPUTATION
# ============================================================

df = pd.DataFrame({
    'City': ['NYC', 'NYC', np.nan, 'LA', 'NYC', 'LA', np.nan, 'Chicago'],
    'Size': ['Large', 'Medium', np.nan, 'Small', 'Large', np.nan, 'Large', 'Medium']
})

print("Original Data:")
print(df)
print(f"\nMode of City: {df['City'].mode()[0]}")
print(f"Mode of Size: {df['Size'].mode()[0]}")

# Method 1: Using pandas fillna with mode
df_mode = df.copy()
df_mode['City'] = df_mode['City'].fillna(df_mode['City'].mode()[0])
df_mode['Size'] = df_mode['Size'].fillna(df_mode['Size'].mode()[0])

print("\nAfter Mode Imputation:")
print(df_mode)

# Method 2: Using sklearn
from sklearn.impute import SimpleImputer

imputer_mode = SimpleImputer(strategy='most_frequent')

# For categorical data, need to handle separately or use encoding
df_mode_sklearn = df.copy()
for col in df.columns:
    imputer = SimpleImputer(strategy='most_frequent')
    df_mode_sklearn[col] = imputer.fit_transform(df[[col]]).ravel()

print("\nAfter Mode Imputation (sklearn):")
print(df_mode_sklearn)
When to Use:

text

✅ Use Mode Imputation When:
├── Data is CATEGORICAL (nominal or ordinal)
├── Data is DISCRETE numerical with clear mode
├── One category dominates
└── Missing is MCAR

❌ Avoid Mode Imputation When:
├── Multiple modes exist (multimodal data)
├── Categories are roughly equal in frequency
├── High percentage missing
└── Missing is MAR or MNAR
6.5 Constant Imputation
Concept: Replace missing values with a specific constant value.

Code:

Python

# ============================================================
# CONSTANT IMPUTATION
# ============================================================

df = pd.DataFrame({
    'Name': ['John', np.nan, 'Mary', 'Peter'],
    'Score': [85, 90, np.nan, 78],
    'Status': ['Active', 'Active', np.nan, 'Inactive']
})

print("Original Data:")
print(df)

# Method 1: Using fillna with constant
df_const = df.copy()
df_const['Name'] = df_const['Name'].fillna('Unknown')
df_const['Score'] = df_const['Score'].fillna(0)
df_const['Status'] = df_const['Status'].fillna('Unknown')

print("\nAfter Constant Imputation:")
print(df_const)

# Method 2: Using sklearn
from sklearn.impute import SimpleImputer

imputer_const = SimpleImputer(strategy='constant', fill_value=-999)
df_num = pd.DataFrame({'Score': [85, 90, np.nan, 78]})
df_num_imputed = pd.DataFrame(
    imputer_const.fit_transform(df_num),
    columns=df_num.columns
)

print("\nNumerical Constant Imputation (-999):")
print(df_num_imputed)
Common Constant Values:

text

┌─────────────────┬────────────────────────────────────────────────────┐
│ Constant        │ When to Use                                        │
├─────────────────┼────────────────────────────────────────────────────┤
│ 0               │ When 0 is meaningful (e.g., count of purchases)    │
│ -1 or -999      │ As a flag for "missing" in numerical data          │
│ "Unknown"       │ For categorical data when category unknown         │
│ "Missing"       │ To explicitly mark missing values                  │
│ "Other"         │ When missing might be an "other" category          │
│ Minimum value   │ When missing means "none" or "lowest"              │
│ Maximum value   │ When missing might mean "too high to measure"      │
└─────────────────┴────────────────────────────────────────────────────┘
6.6 Forward Fill and Backward Fill
Concept: Fill missing values using the previous (forward) or next (backward) value. Essential for TIME SERIES data!

text

Forward Fill (ffill):
Uses the LAST known value

Original:       [10, NaN, NaN, 40, NaN, 60]
Forward Fill:   [10, 10,  10,  40, 40,  60]
                     ↑    ↑        ↑
                    Uses previous value


Backward Fill (bfill):
Uses the NEXT known value

Original:       [10, NaN, NaN, 40, NaN, 60]
Backward Fill:  [10, 40,  40,  40, 60,  60]
                     ↑    ↑        ↑
                    Uses next value
Code:

Python

# ============================================================
# FORWARD FILL AND BACKWARD FILL
# ============================================================

# Time series data
df = pd.DataFrame({
    'Date': pd.date_range('2024-01-01', periods=10),
    'Temperature': [20, np.nan, np.nan, 23, np.nan, 25, 26, np.nan, np.nan, 30],
    'Humidity': [np.nan, 60, np.nan, 65, 70, np.nan, 75, np.nan, 80, np.nan]
})

print("Original Data:")
print(df)

# Forward fill
df_ffill = df.copy()
df_ffill['Temperature'] = df_ffill['Temperature'].ffill()
df_ffill['Humidity'] = df_ffill['Humidity'].ffill()

print("\nForward Fill:")
print(df_ffill)

# Backward fill
df_bfill = df.copy()
df_bfill['Temperature'] = df_bfill['Temperature'].bfill()
df_bfill['Humidity'] = df_bfill['Humidity'].bfill()

print("\nBackward Fill:")
print(df_bfill)

# Combined: Forward fill first, then backward fill for remaining
df_combined = df.copy()
df_combined = df_combined.ffill().bfill()

print("\nCombined (ffill then bfill):")
print(df_combined)

# With limit (fill at most N consecutive NaN)
df_limited = df.copy()
df_limited['Temperature'] = df_limited['Temperature'].ffill(limit=1)

print("\nForward Fill with limit=1:")
print(df_limited)
When to Use:

text

✅ Use Forward/Backward Fill When:
├── TIME SERIES data
├── Data has temporal order
├── Missing values should follow trend
├── Consecutive missing values
└── "Last observation carried forward" makes sense

❌ Avoid When:
├── No temporal order
├── Cross-sectional data
├── Long gaps in data
└── Values change rapidly
6.7 Interpolation
Concept: Estimate missing values based on values before AND after.

text

Linear Interpolation:

Original:   [10, NaN, NaN, 40]
             ↓         ↓
Linear:     [10, 20,  30, 40]
                 ↑    ↑
            Evenly spaced between 10 and 40

Formula: value = start + (end - start) * position / total_positions
Code:

Python

# ============================================================
# INTERPOLATION
# ============================================================

df = pd.DataFrame({
    'Time': range(10),
    'Value': [10, np.nan, np.nan, 40, np.nan, 60, np.nan, np.nan, np.nan, 100]
})

print("Original Data:")
print(df)

# Linear interpolation (default)
df_linear = df.copy()
df_linear['Value'] = df_linear['Value'].interpolate(method='linear')

print("\nLinear Interpolation:")
print(df_linear)

# Polynomial interpolation
df_poly = df.copy()
df_poly['Value'] = df_poly['Value'].interpolate(method='polynomial', order=2)

print("\nPolynomial Interpolation (order=2):")
print(df_poly)

# Spline interpolation
df_spline = df.copy()
df_spline['Value'] = df_spline['Value'].interpolate(method='spline', order=2)

print("\nSpline Interpolation:")
print(df_spline)

# Time-based interpolation (for datetime index)
df_time = df.copy()
df_time['Date'] = pd.date_range('2024-01-01', periods=10)
df_time = df_time.set_index('Date')
df_time['Value'] = df_time['Value'].interpolate(method='time')

print("\nTime-based Interpolation:")
print(df_time)
Types of Interpolation:

text

┌─────────────────┬────────────────────────────────────────────────────┐
│ Method          │ Description                                        │
├─────────────────┼────────────────────────────────────────────────────┤
│ linear          │ Straight line between known points                 │
│ polynomial      │ Polynomial curve (specify order)                   │
│ spline          │ Smooth curve through points                        │
│ time            │ For datetime index, accounts for time gaps         │
│ index           │ Uses index values for spacing                      │
│ nearest         │ Uses nearest known value                           │
│ zero            │ Zero-order hold (step function)                    │
│ quadratic       │ Quadratic polynomial                               │
│ cubic           │ Cubic polynomial                                   │
└─────────────────┴────────────────────────────────────────────────────┘
6.8 Comparison of Simple Methods
Python

# ============================================================
# COMPARISON OF ALL SIMPLE IMPUTATION METHODS
# ============================================================

def compare_simple_imputation(df, column):
    """
    Compare different simple imputation methods
    """
    results = {}
    
    original = df[column].copy()
    
    # Mean
    results['mean'] = original.fillna(original.mean())
    
    # Median
    results['median'] = original.fillna(original.median())
    
    # Mode (for numerical - takes first mode)
    results['mode'] = original.fillna(original.mode()[0])
    
    # Forward fill
    results['ffill'] = original.ffill()
    
    # Backward fill
    results['bfill'] = original.bfill()
    
    # Linear interpolation
    results['interpolate'] = original.interpolate(method='linear')
    
    # Constant (0)
    results['constant_0'] = original.fillna(0)
    
    # Create comparison DataFrame
    comparison = pd.DataFrame(results)
    comparison['Original'] = original
    comparison = comparison[['Original'] + list(results.keys())]
    
    print(f"Comparison of Imputation Methods for '{column}':")
    print(comparison)
    
    # Statistics comparison
    print("\n Statistics Comparison:")
    stats = pd.DataFrame({
        'Method': ['Original'] + list(results.keys()),
        'Mean': [original.mean()] + [results[m].mean() for m in results],
        'Std': [original.std()] + [results[m].std() for m in results],
        'Min': [original.min()] + [results[m].min() for m in results],
        'Max': [original.max()] + [results[m].max() for m in results]
    })
    print(stats.round(2))
    
    return comparison

# Example
df = pd.DataFrame({
    'Values': [10, np.nan, 30, np.nan, np.nan, 60, np.nan, 80, 90, np.nan]
})

compare_simple_imputation(df, 'Values')
6.9 Decision Guide for Simple Imputation
text

START: What type of data?
    │
    ├─ NUMERICAL (Continuous)
    │   │
    │   ├─ Distribution?
    │   │   ├─ Normal/Symmetric → Mean Imputation
    │   │   └─ Skewed/Outliers → Median Imputation
    │   │
    │   └─ Time Series?
    │       ├─ Yes → Forward/Backward Fill OR Interpolation
    │       └─ No → Mean or Median
    │
    ├─ NUMERICAL (Discrete)
    │   │
    │   └─ Mode Imputation OR treat as categorical
    │
    └─ CATEGORICAL
        │
        └─ Mode Imputation OR Constant ("Unknown")
7. Advanced Imputation Methods
7.1 K-Nearest Neighbors (KNN) Imputation
Concept: Find K most similar rows (neighbors) and use their values to impute missing value.

text

How KNN Imputation Works:

Data:
┌─────┬─────────┬────────┐
│ Age │ Income  │ Score  │
├─────┼─────────┼────────┤
│ 25  │ 50000   │ 80     │  ← Similar to row 3
│ 30  │ 60000   │ 85     │  ← Similar to row 3
│ 28  │ NaN     │ 82     │  ← Missing Income! Find neighbors
│ 45  │ 90000   │ 90     │
│ 50  │ 100000  │ 95     │
└─────┴─────────┴────────┘

Step 1: Find K nearest neighbors of row 3 (based on Age and Score)
        Neighbor 1: Row 1 (Age=25, Score=80) → Income=50000
        Neighbor 2: Row 2 (Age=30, Score=85) → Income=60000

Step 2: Average their Income values
        Imputed Income = (50000 + 60000) / 2 = 55000

Step 3: Fill missing value
        Row 3 Income = 55000
Code:

Python

# ============================================================
# KNN IMPUTATION
# ============================================================

from sklearn.impute import KNNImputer
import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'Age': [25, 30, 28, 45, 50, 35, 40],
    'Income': [50000, 60000, np.nan, 90000, 100000, np.nan, 80000],
    'Score': [80, 85, 82, 90, 95, 88, np.nan]
})

print("Original Data:")
print(df)

# KNN Imputation
knn_imputer = KNNImputer(
    n_neighbors=2,        # Number of neighbors to consider
    weights='uniform',    # 'uniform' or 'distance'
    metric='nan_euclidean'  # Distance metric
)

df_knn = pd.DataFrame(
    knn_imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter KNN Imputation (k=2):")
print(df_knn)

# Compare different k values
print("\nComparing different k values:")
for k in [1, 2, 3, 5]:
    imputer = KNNImputer(n_neighbors=k)
    result = imputer.fit_transform(df)
    print(f"k={k}: Income[2]={result[2,1]:.2f}, Score[6]={result[6,2]:.2f}")
Parameters Explained:

text

┌───────────────────┬────────────────────────────────────────────────────┐
│ Parameter         │ Description                                        │
├───────────────────┼────────────────────────────────────────────────────┤
│ n_neighbors       │ Number of neighbors to use (default=5)             │
│                   │ Higher k = more stable but less local              │
│                   │ Lower k = more local but more sensitive to outliers│
├───────────────────┼────────────────────────────────────────────────────┤
│ weights           │ How to weight neighbors:                           │
│                   │ 'uniform' = equal weight                           │
│                   │ 'distance' = closer neighbors count more           │
├───────────────────┼────────────────────────────────────────────────────┤
│ metric            │ Distance calculation method                        │
│                   │ 'nan_euclidean' = ignores NaN in distance calc     │
└───────────────────┴────────────────────────────────────────────────────┘
When to Use:

text

✅ Use KNN Imputation When:
├── Features are RELATED to each other
├── Missing is MAR (can predict from other features)
├── Dataset is not too large (KNN is slow on big data)
├── Data is properly SCALED (important!)
└── Want more accurate imputation than simple methods

❌ Avoid KNN Imputation When:
├── Very large datasets (>100K rows) - too slow
├── Features are UNRELATED
├── High dimensionality (curse of dimensionality)
├── Data is not scaled
└── Too many missing values in a row
Important: Scale Your Data First!

Python

# ============================================================
# KNN IMPUTATION WITH PROPER SCALING
# ============================================================

from sklearn.preprocessing import StandardScaler
from sklearn.impute import KNNImputer
import numpy as np
import pandas as pd

# Data with different scales
df = pd.DataFrame({
    'Age': [25, 30, 28, 45, 50],           # Range: 25-50
    'Income': [50000, 60000, np.nan, 90000, 100000],  # Range: 50000-100000
    'Score': [80, 85, 82, 90, np.nan]      # Range: 80-95
})

print("Original Data:")
print(df)

# WRONG: KNN without scaling
# Income dominates distance calculation!
knn_wrong = KNNImputer(n_neighbors=2)
df_wrong = pd.DataFrame(knn_wrong.fit_transform(df), columns=df.columns)
print("\nKNN without scaling (WRONG):")
print(df_wrong)

# CORRECT: Scale → Impute → Inverse scale
# Step 1: Remember which values are missing
missing_mask = df.isnull()

# Step 2: Initial fill for scaling (temporary)
df_temp = df.fillna(df.mean())

# Step 3: Scale
scaler = StandardScaler()
df_scaled = pd.DataFrame(
    scaler.fit_transform(df_temp),
    columns=df.columns
)

# Step 4: Put NaN back
df_scaled[missing_mask] = np.nan

# Step 5: KNN imputation on scaled data
knn_imputer = KNNImputer(n_neighbors=2)
df_imputed_scaled = pd.DataFrame(
    knn_imputer.fit_transform(df_scaled),
    columns=df.columns
)

# Step 6: Inverse transform back to original scale
df_correct = pd.DataFrame(
    scaler.inverse_transform(df_imputed_scaled),
    columns=df.columns
)

print("\nKNN with proper scaling (CORRECT):")
print(df_correct)
7.2 Iterative Imputation (MICE)
MICE = Multiple Imputation by Chained Equations

Concept: Impute each missing value using a regression model, iterate until convergence.

text

How MICE Works:

Step 1: Initial imputation (e.g., mean for all missing)

Step 2: For each column with missing values:
        a) Treat this column as the TARGET
        b) Use other columns as FEATURES
        c) Train regression model on complete rows
        d) Predict missing values in this column
        
Step 3: Repeat Step 2 for all columns with missing values

Step 4: Repeat Steps 2-3 until values stabilize (converge)

Visual:
Iteration 1:
    Column A: Use B, C, D to predict missing A
    Column B: Use A, C, D to predict missing B
    Column C: Use A, B, D to predict missing C
    
Iteration 2:
    Same process, but now using imputed values from Iteration 1
    
...continue until values stop changing...
Code:

Python

# ============================================================
# ITERATIVE IMPUTATION (MICE)
# ============================================================

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
from sklearn.linear_model import LinearRegression, BayesianRidge
from sklearn.ensemble import RandomForestRegressor
import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'Age': [25, 30, np.nan, 45, 50, 35, np.nan, 55],
    'Income': [50000, np.nan, 70000, 90000, 100000, np.nan, 85000, 110000],
    'Experience': [2, 5, np.nan, 15, 20, 8, 12, np.nan],
    'Score': [80, 85, 78, np.nan, 95, 88, 92, np.nan]
})

print("Original Data:")
print(df)
print(f"\nMissing values:\n{df.isnull().sum()}")

# Method 1: Default IterativeImputer (BayesianRidge)
iterative_imputer = IterativeImputer(
    max_iter=10,           # Maximum iterations
    random_state=42,
    verbose=0
)

df_iterative = pd.DataFrame(
    iterative_imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter Iterative Imputation (BayesianRidge):")
print(df_iterative.round(2))

# Method 2: With Linear Regression
iterative_lr = IterativeImputer(
    estimator=LinearRegression(),
    max_iter=10,
    random_state=42
)

df_iterative_lr = pd.DataFrame(
    iterative_lr.fit_transform(df),
    columns=df.columns
)

print("\nAfter Iterative Imputation (LinearRegression):")
print(df_iterative_lr.round(2))

# Method 3: With Random Forest (more robust)
iterative_rf = IterativeImputer(
    estimator=RandomForestRegressor(n_estimators=10, random_state=42),
    max_iter=10,
    random_state=42
)

df_iterative_rf = pd.DataFrame(
    iterative_rf.fit_transform(df),
    columns=df.columns
)

print("\nAfter Iterative Imputation (RandomForest):")
print(df_iterative_rf.round(2))
Parameters Explained:

text

┌─────────────────────┬──────────────────────────────────────────────────┐
│ Parameter           │ Description                                      │
├─────────────────────┼──────────────────────────────────────────────────┤
│ estimator           │ Model to use for imputation                      │
│                     │ Default: BayesianRidge                           │
│                     │ Options: LinearRegression, RandomForest, etc.    │
├─────────────────────┼──────────────────────────────────────────────────┤
│ max_iter            │ Maximum number of imputation rounds              │
│                     │ Default: 10                                      │
├─────────────────────┼──────────────────────────────────────────────────┤
│ tol                 │ Tolerance for stopping (convergence threshold)   │
│                     │ Default: 0.001                                   │
├─────────────────────┼──────────────────────────────────────────────────┤
│ initial_strategy    │ Initial imputation: 'mean', 'median', 'most_frequent'│
│                     │ Default: 'mean'                                  │
├─────────────────────┼──────────────────────────────────────────────────┤
│ imputation_order    │ Order to impute columns                          │
│                     │ 'ascending': least missing first                 │
│                     │ 'descending': most missing first                 │
│                     │ 'random': random order                           │
└─────────────────────┴──────────────────────────────────────────────────┘
When to Use:

text

✅ Use Iterative Imputation When:
├── Features are CORRELATED
├── Missing is MAR
├── Want STATISTICALLY SOUND imputation
├── Need to preserve relationships between variables
└── Building models that assume complete data

❌ Avoid When:
├── Features are INDEPENDENT
├── Very large datasets (slow)
├── Missing is MNAR
└── Simple imputation works fine
7.3 Multiple Imputation
Concept: Create MULTIPLE imputed datasets, analyze each, and combine results.

text

Why Multiple Imputation?

Single Imputation Problem:
    Original: [10, NaN, 30]
    Imputed:  [10, 20, 30]
    
    We treat 20 as if it were CERTAIN, but it's an ESTIMATE!
    This underestimates uncertainty.

Multiple Imputation Solution:
    Create multiple versions:
    Dataset 1: [10, 18, 30]
    Dataset 2: [10, 21, 30]
    Dataset 3: [10, 19, 30]
    Dataset 4: [10, 22, 30]
    Dataset 5: [10, 20, 30]
    
    Analyze each, then combine results.
    This properly accounts for imputation uncertainty!
Visual:

text

                    ┌─── Dataset 1 ──→ Analysis 1 ───┐
                    │                                │
Original Data ──────┼─── Dataset 2 ──→ Analysis 2 ───┼──→ Combined
(with missing)      │                                │    Results
                    ├─── Dataset 3 ──→ Analysis 3 ───┤
                    │                                │
                    └─── Dataset M ──→ Analysis M ───┘
Code:

Python

# ============================================================
# MULTIPLE IMPUTATION
# ============================================================

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
from sklearn.linear_model import LinearRegression
import numpy as np
import pandas as pd

def multiple_imputation(df, n_imputations=5, random_state=42):
    """
    Perform multiple imputation and return list of imputed datasets
    """
    imputed_datasets = []
    
    for i in range(n_imputations):
        imputer = IterativeImputer(
            random_state=random_state + i,  # Different random state each time
            max_iter=10,
            sample_posterior=True  # Important: adds randomness
        )
        
        imputed_data = pd.DataFrame(
            imputer.fit_transform(df),
            columns=df.columns
        )
        imputed_datasets.append(imputed_data)
        
    return imputed_datasets

def combine_results(estimates, variances):
    """
    Rubin's rules for combining multiple imputation results
    """
    m = len(estimates)
    
    # Combined estimate (mean of estimates)
    combined_estimate = np.mean(estimates)
    
    # Within-imputation variance (mean of variances)
    within_variance = np.mean(variances)
    
    # Between-imputation variance
    between_variance = np.var(estimates, ddof=1)
    
    # Total variance
    total_variance = within_variance + (1 + 1/m) * between_variance
    
    return combined_estimate, total_variance

# Example
df = pd.DataFrame({
    'X': [1, 2, np.nan, 4, 5, np.nan, 7, 8],
    'Y': [10, np.nan, 30, 40, np.nan, 60, 70, 80]
})

print("Original Data:")
print(df)

# Create multiple imputed datasets
imputed_datasets = multiple_imputation(df, n_imputations=5)

print("\nMultiple Imputed Datasets:")
for i, dataset in enumerate(imputed_datasets):
    print(f"\nDataset {i+1}:")
    print(dataset.round(2))

# Compare the imputed values
print("\nComparison of imputed values for X[2]:")
for i, dataset in enumerate(imputed_datasets):
    print(f"  Dataset {i+1}: {dataset.loc[2, 'X']:.2f}")

print(f"\nMean of imputed X[2]: {np.mean([d.loc[2, 'X'] for d in imputed_datasets]):.2f}")
print(f"Std of imputed X[2]:  {np.std([d.loc[2, 'X'] for d in imputed_datasets]):.2f}")
7.4 MissForest (Random Forest Imputation)
Concept: Use Random Forest to impute missing values iteratively.

Python

# ============================================================
# MISSFOREST IMPUTATION
# ============================================================

# Install: pip install missingpy OR use sklearn's IterativeImputer with RF

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
from sklearn.ensemble import RandomForestRegressor, RandomForestClassifier
import pandas as pd
import numpy as np

def missforest_imputer(df, categorical_columns=None):
    """
    MissForest-style imputation using Random Forest
    """
    if categorical_columns is None:
        categorical_columns = []
    
    # For numerical columns
    numerical_columns = [c for c in df.columns if c not in categorical_columns]
    
    if len(numerical_columns) > 0:
        # Impute numerical columns
        imputer_num = IterativeImputer(
            estimator=RandomForestRegressor(n_estimators=100, random_state=42),
            max_iter=10,
            random_state=42
        )
        
        df_num = df[numerical_columns].copy()
        df[numerical_columns] = imputer_num.fit_transform(df_num)
    
    return df

# Example
df = pd.DataFrame({
    'Age': [25, 30, np.nan, 45, 50, 35, np.nan],
    'Income': [50000, np.nan, 70000, 90000, np.nan, 75000, 85000],
    'Score': [80, 85, np.nan, 90, 95, np.nan, 88]
})

print("Original Data:")
print(df)

df_imputed = missforest_imputer(df.copy())

print("\nAfter MissForest Imputation:")
print(df_imputed.round(2))
Advantages of MissForest:

text

✅ Handles BOTH numerical and categorical data
✅ Captures NON-LINEAR relationships
✅ Doesn't require scaling
✅ Handles interactions between features
✅ Works well with mixed data types

❌ Disadvantages:
✗ SLOW on large datasets
✗ Can overfit if not careful
✗ Computationally expensive
8. Machine Learning Based Imputation
8.1 Regression Imputation
Concept: Build a regression model to predict missing values.

Python

# ============================================================
# REGRESSION IMPUTATION
# ============================================================

from sklearn.linear_model import LinearRegression
from sklearn.model_selection import cross_val_score
import pandas as pd
import numpy as np

def regression_imputation(df, target_column, feature_columns):
    """
    Impute missing values using regression
    """
    df_copy = df.copy()
    
    # Split data into complete and incomplete
    complete_mask = df_copy[target_column].notna()
    incomplete_mask = df_copy[target_column].isna()
    
    # Check if we have any missing values
    if not incomplete_mask.any():
        print(f"No missing values in {target_column}")
        return df_copy
    
    # Prepare training data (complete rows)
    X_train = df_copy.loc[complete_mask, feature_columns]
    y_train = df_copy.loc[complete_mask, target_column]
    
    # Prepare prediction data (incomplete rows)
    X_predict = df_copy.loc[incomplete_mask, feature_columns]
    
    # Handle missing values in features (simple mean imputation)
    X_train = X_train.fillna(X_train.mean())
    X_predict = X_predict.fillna(X_train.mean())
    
    # Train model
    model = LinearRegression()
    model.fit(X_train, y_train)
    
    # Predict missing values
    predictions = model.predict(X_predict)
    
    # Fill missing values
    df_copy.loc[incomplete_mask, target_column] = predictions
    
    # Print model performance
    cv_scores = cross_val_score(model, X_train, y_train, cv=min(5, len(X_train)))
    print(f"R² score for {target_column}: {cv_scores.mean():.4f}")
    
    return df_copy

# Example
df = pd.DataFrame({
    'Age': [25, 30, 35, 40, 45, 50, 55, 60],
    'Experience': [2, 5, 8, 12, 15, 18, 22, 25],
    'Income': [50000, 60000, np.nan, 80000, np.nan, 100000, 110000, np.nan]
})

print("Original Data:")
print(df)

# Impute Income using Age and Experience
df_imputed = regression_imputation(
    df, 
    target_column='Income',
    feature_columns=['Age', 'Experience']
)

print("\nAfter Regression Imputation:")
print(df_imputed)
8.2 Classification Imputation (for Categorical)
Concept: Use classification model to predict missing categorical values.

Python

# ============================================================
# CLASSIFICATION IMPUTATION FOR CATEGORICAL DATA
# ============================================================

from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import LabelEncoder
import pandas as pd
import numpy as np

def classification_imputation(df, target_column, feature_columns):
    """
    Impute missing categorical values using classification
    """
    df_copy = df.copy()
    
    # Encode target if categorical
    le = LabelEncoder()
    
    # Get complete rows for training
    complete_mask = df_copy[target_column].notna()
    incomplete_mask = df_copy[target_column].isna()
    
    if not incomplete_mask.any():
        print(f"No missing values in {target_column}")
        return df_copy
    
    # Encode non-null values
    known_values = df_copy.loc[complete_mask, target_column]
    le.fit(known_values)
    
    # Prepare data
    X_train = df_copy.loc[complete_mask, feature_columns].fillna(-999)
    y_train = le.transform(known_values)
    
    X_predict = df_copy.loc[incomplete_mask, feature_columns].fillna(-999)
    
    # Train classifier
    clf = RandomForestClassifier(n_estimators=100, random_state=42)
    clf.fit(X_train, y_train)
    
    # Predict
    predictions = clf.predict(X_predict)
    predicted_labels = le.inverse_transform(predictions)
    
    # Fill missing values
    df_copy.loc[incomplete_mask, target_column] = predicted_labels
    
    print(f"Predicted classes: {predicted_labels}")
    
    return df_copy

# Example
df = pd.DataFrame({
    'Age': [25, 30, 35, 40, 45, 50, 55, 60],
    'Income': [30000, 50000, 60000, 80000, 90000, 100000, 120000, 150000],
    'Category': ['Low', 'Low', np.nan, 'Medium', np.nan, 'High', 'High', np.nan]
})

print("Original Data:")
print(df)

df_imputed = classification_imputation(
    df,
    target_column='Category',
    feature_columns=['Age', 'Income']
)

print("\nAfter Classification Imputation:")
print(df_imputed)
8.3 Deep Learning Based Imputation
Concept: Use neural networks (autoencoders) to learn patterns and impute.

Python

# ============================================================
# AUTOENCODER IMPUTATION
# ============================================================

import numpy as np
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Using TensorFlow/Keras
try:
    import tensorflow as tf
    from tensorflow.keras.models import Model
    from tensorflow.keras.layers import Input, Dense, Dropout
    from tensorflow.keras.callbacks import EarlyStopping
    
    def autoencoder_imputation(df, epochs=100, batch_size=32):
        """
        Impute missing values using autoencoder
        """
        df_copy = df.copy()
        
        # Remember missing positions
        missing_mask = df_copy.isnull()
        
        # Initial imputation with mean
        df_filled = df_copy.fillna(df_copy.mean())
        
        # Scale data
        scaler = StandardScaler()
        data_scaled = scaler.fit_transform(df_filled)
        
        # Build autoencoder
        input_dim = data_scaled.shape[1]
        
        # Encoder
        input_layer = Input(shape=(input_dim,))
        encoded = Dense(64, activation='relu')(input_layer)
        encoded = Dropout(0.2)(encoded)
        encoded = Dense(32, activation='relu')(encoded)
        encoded = Dense(16, activation='relu')(encoded)
        
        # Decoder
        decoded = Dense(32, activation='relu')(encoded)
        decoded = Dropout(0.2)(decoded)
        decoded = Dense(64, activation='relu')(decoded)
        decoded = Dense(input_dim, activation='linear')(decoded)
        
        # Model
        autoencoder = Model(input_layer, decoded)
        autoencoder.compile(optimizer='adam', loss='mse')
        
        # Train (using non-missing data as both input and target)
        early_stop = EarlyStopping(patience=10, restore_best_weights=True)
        
        autoencoder.fit(
            data_scaled, data_scaled,
            epochs=epochs,
            batch_size=batch_size,
            validation_split=0.2,
            callbacks=[early_stop],
            verbose=0
        )
        
        # Predict (reconstruct)
        reconstructed = autoencoder.predict(data_scaled, verbose=0)
        
        # Inverse transform
        reconstructed = scaler.inverse_transform(reconstructed)
        
        # Replace only missing values
        result = df_filled.values.copy()
        result[missing_mask.values] = reconstructed[missing_mask.values]
        
        return pd.DataFrame(result, columns=df.columns)
    
    # Example usage (uncomment to run)
    # df = pd.DataFrame({
    #     'A': [1, 2, np.nan, 4, 5],
    #     'B': [10, np.nan, 30, 40, 50],
    #     'C': [100, 200, 300, np.nan, 500]
    # })
    # df_imputed = autoencoder_imputation(df)
    # print(df_imputed)
    
except ImportError:
    print("TensorFlow not installed. Skipping autoencoder example.")
8.4 Using DataWig (Deep Learning Library for Imputation)
Python

# ============================================================
# DATAWIG - Amazon's Deep Learning Imputation Library
# ============================================================

# Install: pip install datawig

try:
    import datawig
    
    def datawig_imputation(df, target_column):
        """
        Impute using DataWig (handles mixed data types well)
        """
        # DataWig automatically handles:
        # - Numerical columns
        # - Categorical columns
        # - Text columns
        
        imputer = datawig.SimpleImputer(
            input_columns=list(df.columns.drop(target_column)),
            output_column=target_column,
            output_path='./datawig_models'
        )
        
        # Train
        imputer.fit(train_df=df)
        
        # Impute
        imputed = imputer.predict(df)
        
        return imputed
    
except ImportError:
    print("DataWig not installed. Install with: pip install datawig")
9. Handling Missing Data in Different Data Types
9.1 Numerical Data
Python

# ============================================================
# COMPREHENSIVE NUMERICAL IMPUTATION
# ============================================================

import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer, KNNImputer
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

def impute_numerical(df, column, method='median'):
    """
    Impute numerical missing values with various methods
    """
    df_copy = df.copy()
    
    if method == 'mean':
        df_copy[column] = df_copy[column].fillna(df_copy[column].mean())
    
    elif method == 'median':
        df_copy[column] = df_copy[column].fillna(df_copy[column].median())
    
    elif method == 'mode':
        df_copy[column] = df_copy[column].fillna(df_copy[column].mode()[0])
    
    elif method == 'zero':
        df_copy[column] = df_copy[column].fillna(0)
    
    elif method == 'ffill':
        df_copy[column] = df_copy[column].ffill()
    
    elif method == 'bfill':
        df_copy[column] = df_copy[column].bfill()
    
    elif method == 'interpolate':
        df_copy[column] = df_copy[column].interpolate(method='linear')
    
    elif method == 'knn':
        imputer = KNNImputer(n_neighbors=5)
        df_copy[[column]] = imputer.fit_transform(df_copy[[column]])
    
    elif method == 'iterative':
        imputer = IterativeImputer(max_iter=10, random_state=42)
        df_copy[[column]] = imputer.fit_transform(df_copy[[column]])
    
    return df_copy

# Decision guide for numerical data
def recommend_numerical_method(series):
    """
    Recommend imputation method based on data characteristics
    """
    print(f"\n📊 Analysis of '{series.name}':")
    print(f"   Missing: {series.isnull().sum()} ({series.isnull().mean()*100:.1f}%)")
    
    # Check for skewness
    skewness = series.skew()
    print(f"   Skewness: {skewness:.2f}")
    
    # Check for outliers (IQR method)
    Q1 = series.quantile(0.25)
    Q3 = series.quantile(0.75)
    IQR = Q3 - Q1
    outliers = ((series < (Q1 - 1.5 * IQR)) | (series > (Q3 + 1.5 * IQR))).sum()
    print(f"   Outliers: {outliers}")
    
    # Recommendation
    print("\n📌 Recommendation:")
    if abs(skewness) < 0.5 and outliers == 0:
        print("   → Mean imputation (symmetric, no outliers)")
        return 'mean'
    elif outliers > 0 or abs(skewness) > 1:
        print("   → Median imputation (outliers or skewed)")
        return 'median'
    else:
        print("   → Median imputation (safe default)")
        return 'median'

# Example
df = pd.DataFrame({
    'normal_data': np.random.normal(50, 10, 100),
    'skewed_data': np.random.exponential(50, 100),
    'with_outliers': np.concatenate([np.random.normal(50, 5, 95), [200, 250, 300, 400, 500]])
})

# Add missing values
for col in df.columns:
    df.loc[np.random.choice(df.index, 20, replace=False), col] = np.nan

for col in df.columns:
    recommend_numerical_method(df[col])
9.2 Categorical Data
Python

# ============================================================
# COMPREHENSIVE CATEGORICAL IMPUTATION
# ============================================================

import pandas as pd
import numpy as np

def impute_categorical(df, column, method='mode'):
    """
    Impute categorical missing values
    """
    df_copy = df.copy()
    
    if method == 'mode':
        # Most frequent value
        mode_value = df_copy[column].mode()[0]
        df_copy[column] = df_copy[column].fillna(mode_value)
    
    elif method == 'unknown':
        # Add "Unknown" category
        df_copy[column] = df_copy[column].fillna('Unknown')
    
    elif method == 'missing':
        # Add "Missing" category (explicit)
        df_copy[column] = df_copy[column].fillna('Missing')
    
    elif method == 'random':
        # Random sampling from existing values
        existing_values = df_copy[column].dropna()
        missing_count = df_copy[column].isnull().sum()
        random_values = np.random.choice(existing_values, missing_count)
        df_copy.loc[df_copy[column].isnull(), column] = random_values
    
    elif method == 'proportional':
        # Proportional random sampling
        value_counts = df_copy[column].value_counts(normalize=True)
        missing_mask = df_copy[column].isnull()
        missing_count = missing_mask.sum()
        
        random_values = np.random.choice(
            value_counts.index,
            size=missing_count,
            p=value_counts.values
        )
        df_copy.loc[missing_mask, column] = random_values
    
    return df_copy

# Example
df = pd.DataFrame({
    'City': ['NYC', 'LA', np.nan, 'Chicago', 'NYC', np.nan, 'LA', 'NYC', np.nan, 'Chicago'],
    'Size': ['Large', np.nan, 'Small', 'Medium', np.nan, 'Large', 'Small', np.nan, 'Medium', 'Large']
})

print("Original Data:")
print(df)

# Try different methods
methods = ['mode', 'unknown', 'proportional']
for method in methods:
    df_imputed = impute_categorical(df.copy(), 'City', method)
    print(f"\nAfter {method} imputation:")
    print(df_imputed['City'].value_counts())
9.3 Time Series Data
Python

# ============================================================
# TIME SERIES IMPUTATION
# ============================================================

import pandas as pd
import numpy as np

def impute_timeseries(df, column, method='linear'):
    """
    Impute time series data with temporal methods
    """
    df_copy = df.copy()
    
    if method == 'ffill':
        # Forward fill (last observation carried forward)
        df_copy[column] = df_copy[column].ffill()
    
    elif method == 'bfill':
        # Backward fill
        df_copy[column] = df_copy[column].bfill()
    
    elif method == 'linear':
        # Linear interpolation
        df_copy[column] = df_copy[column].interpolate(method='linear')
    
    elif method == 'time':
        # Time-weighted interpolation (requires datetime index)
        df_copy[column] = df_copy[column].interpolate(method='time')
    
    elif method == 'spline':
        # Spline interpolation (smooth curve)
        df_copy[column] = df_copy[column].interpolate(method='spline', order=2)
    
    elif method == 'polynomial':
        # Polynomial interpolation
        df_copy[column] = df_copy[column].interpolate(method='polynomial', order=2)
    
    elif method == 'seasonal':
        # Seasonal decomposition and imputation
        from statsmodels.tsa.seasonal import seasonal_decompose
        
        # Requires complete data for decomposition
        temp_filled = df_copy[column].interpolate()
        decomposition = seasonal_decompose(temp_filled, period=7, extrapolate_trend='freq')
        
        # Use trend + seasonal for imputation
        trend = decomposition.trend
        seasonal = decomposition.seasonal
        
        missing_mask = df_copy[column].isnull()
        df_copy.loc[missing_mask, column] = (trend + seasonal)[missing_mask]
    
    elif method == 'rolling_mean':
        # Rolling mean imputation
        window = 3
        rolling = df_copy[column].rolling(window=window, min_periods=1, center=True).mean()
        df_copy[column] = df_copy[column].fillna(rolling)
    
    return df_copy

# Example
dates = pd.date_range('2024-01-01', periods=30, freq='D')
df = pd.DataFrame({
    'date': dates,
    'temperature': [20, 21, np.nan, 23, 24, np.nan, np.nan, 27, 28, 29,
                   30, np.nan, 32, 33, 34, np.nan, 36, 37, 38, 39,
                   np.nan, np.nan, 42, 43, 44, 45, np.nan, 47, 48, 49]
})
df = df.set_index('date')

print("Original Data:")
print(df.head(15))

# Compare methods
methods = ['ffill', 'linear', 'spline', 'rolling_mean']
results = {}

for method in methods:
    results[method] = impute_timeseries(df.copy(), 'temperature', method)

print("\nComparison of methods:")
comparison = pd.DataFrame({
    'Original': df['temperature'],
    **{m: results[m]['temperature'] for m in methods}
})
print(comparison.head(15))
9.4 Mixed Data Types
Python

# ============================================================
# HANDLING MIXED DATA TYPES
# ============================================================

import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer

def impute_mixed_dataframe(df):
    """
    Impute DataFrame with mixed data types
    """
    df_copy = df.copy()
    
    # Separate columns by type
    numeric_columns = df_copy.select_dtypes(include=[np.number]).columns.tolist()
    categorical_columns = df_copy.select_dtypes(include=['object', 'category']).columns.tolist()
    datetime_columns = df_copy.select_dtypes(include=['datetime64']).columns.tolist()
    boolean_columns = df_copy.select_dtypes(include=['bool']).columns.tolist()
    
    print(f"Numeric columns: {numeric_columns}")
    print(f"Categorical columns: {categorical_columns}")
    print(f"Datetime columns: {datetime_columns}")
    print(f"Boolean columns: {boolean_columns}")
    
    # Impute numeric columns
    if numeric_columns:
        # Use median for numeric (robust to outliers)
        imputer_num = SimpleImputer(strategy='median')
        df_copy[numeric_columns] = imputer_num.fit_transform(df_copy[numeric_columns])
    
    # Impute categorical columns
    if categorical_columns:
        # Use mode for categorical
        imputer_cat = SimpleImputer(strategy='most_frequent')
        df_copy[categorical_columns] = imputer_cat.fit_transform(df_copy[categorical_columns])
    
    # Impute datetime columns
    if datetime_columns:
        for col in datetime_columns:
            # Forward fill for datetime
            df_copy[col] = df_copy[col].ffill().bfill()
    
    # Impute boolean columns
    if boolean_columns:
        for col in boolean_columns:
            # Mode for boolean
            df_copy[col] = df_copy[col].fillna(df_copy[col].mode()[0])
    
    return df_copy

# Example
df = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, np.nan],
    'Income': [50000, 60000, np.nan, 80000, 90000],
    'City': ['NYC', np.nan, 'LA', 'Chicago', np.nan],
    'Category': pd.Categorical(['A', 'B', np.nan, 'A', 'C']),
    'Date': pd.to_datetime(['2024-01-01', '2024-01-02', None, '2024-01-04', '2024-01-05']),
    'IsActive': [True, False, None, True, None]
})

print("Original Data:")
print(df)
print(f"\nData types:\n{df.dtypes}")

df_imputed = impute_mixed_dataframe(df)

print("\nAfter Imputation:")
print(df_imputed)
10. Practical Implementation Guide
10.1 Complete Missing Data Pipeline
Python

# ============================================================
# COMPLETE MISSING DATA HANDLING PIPELINE
# ============================================================

import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer, KNNImputer
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.model_selection import train_test_split
import warnings
warnings.filterwarnings('ignore')


class MissingDataHandler:
    """
    Comprehensive missing data handling class
    """
    
    def __init__(self, df):
        self.df_original = df.copy()
        self.df = df.copy()
        self.imputers = {}
        self.scalers = {}
        self.encoders = {}
        self.missing_indicators = {}
    
    # ---------------------------------------------------------
    # STEP 1: ANALYSIS
    # ---------------------------------------------------------
    def analyze_missing(self):
        """
        Comprehensive missing data analysis
        """
        print("="*70)
        print("MISSING DATA ANALYSIS")
        print("="*70)
        
        total_cells = self.df.size
        total_missing = self.df.isnull().sum().sum()
        
        print(f"\n📊 Overall Statistics:")
        print(f"   Total cells:     {total_cells:,}")
        print(f"   Missing cells:   {total_missing:,} ({total_missing/total_cells*100:.2f}%)")
        print(f"   Complete cells:  {total_cells - total_missing:,}")
        
        # Per column analysis
        print(f"\n📊 Per-Column Analysis:")
        print("-"*70)
        
        analysis = []
        for col in self.df.columns:
            missing_count = self.df[col].isnull().sum()
            missing_pct = missing_count / len(self.df) * 100
            dtype = self.df[col].dtype
            unique = self.df[col].nunique()
            
            analysis.append({
                'Column': col,
                'Type': str(dtype),
                'Missing': missing_count,
                'Missing%': missing_pct,
                'Unique': unique
            })
        
        analysis_df = pd.DataFrame(analysis)
        analysis_df = analysis_df.sort_values('Missing%', ascending=False)
        print(analysis_df.to_string(index=False))
        
        # Per row analysis
        rows_with_missing = self.df.isnull().any(axis=1).sum()
        complete_rows = len(self.df) - rows_with_missing
        
        print(f"\n📊 Row Analysis:")
        print(f"   Rows with missing: {rows_with_missing} ({rows_with_missing/len(self.df)*100:.1f}%)")
        print(f"   Complete rows:     {complete_rows} ({complete_rows/len(self.df)*100:.1f}%)")
        
        return analysis_df
    
    # ---------------------------------------------------------
    # STEP 2: CREATE MISSING INDICATORS
    # ---------------------------------------------------------
    def create_missing_indicators(self, columns=None, threshold=0.05):
        """
        Create binary indicators for missing values
        (Useful when missingness itself is informative)
        """
        if columns is None:
            # Create indicators for columns with significant missingness
            missing_pct = self.df.isnull().sum() / len(self.df)
            columns = missing_pct[missing_pct >= threshold].index.tolist()
        
        for col in columns:
            indicator_name = f'{col}_was_missing'
            self.df[indicator_name] = self.df[col].isnull().astype(int)
            self.missing_indicators[col] = indicator_name
            print(f"Created indicator: {indicator_name}")
        
        return self
    
    # ---------------------------------------------------------
    # STEP 3: DELETION
    # ---------------------------------------------------------
    def delete_columns(self, threshold=0.5):
        """
        Delete columns with missing percentage above threshold
        """
        missing_pct = self.df.isnull().sum() / len(self.df)
        cols_to_drop = missing_pct[missing_pct > threshold].index.tolist()
        
        if cols_to_drop:
            print(f"Dropping columns (>{threshold*100}% missing): {cols_to_drop}")
            self.df = self.df.drop(columns=cols_to_drop)
        else:
            print(f"No columns exceed {threshold*100}% missing threshold")
        
        return self
    
    def delete_rows(self, threshold=0.5):
        """
        Delete rows with missing percentage above threshold
        """
        missing_pct = self.df.isnull().sum(axis=1) / len(self.df.columns)
        rows_to_drop = missing_pct[missing_pct > threshold].index.tolist()
        
        if rows_to_drop:
            print(f"Dropping {len(rows_to_drop)} rows (>{threshold*100}% missing)")
            self.df = self.df.drop(index=rows_to_drop)
        else:
            print(f"No rows exceed {threshold*100}% missing threshold")
        
        return self
    
    # ---------------------------------------------------------
    # STEP 4: IMPUTATION
    # ---------------------------------------------------------
    def impute_numerical(self, columns=None, method='median'):
        """
        Impute numerical columns
        """
        if columns is None:
            columns = self.df.select_dtypes(include=[np.number]).columns.tolist()
        
        print(f"\nImputing numerical columns with {method}:")
        
        for col in columns:
            if self.df[col].isnull().any():
                if method == 'mean':
                    value = self.df[col].mean()
                elif method == 'median':
                    value = self.df[col].median()
                elif method == 'zero':
                    value = 0
                
                self.df[col] = self.df[col].fillna(value)
                self.imputers[col] = ('simple', method, value)
                print(f"   {col}: filled with {method} = {value:.2f}")
        
        return self
    
    def impute_categorical(self, columns=None, method='mode'):
        """
        Impute categorical columns
        """
        if columns is None:
            columns = self.df.select_dtypes(include=['object', 'category']).columns.tolist()
        
        print(f"\nImputing categorical columns with {method}:")
        
        for col in columns:
            if self.df[col].isnull().any():
                if method == 'mode':
                    value = self.df[col].mode()[0]
                elif method == 'unknown':
                    value = 'Unknown'
                elif method == 'missing':
                    value = 'Missing'
                
                self.df[col] = self.df[col].fillna(value)
                self.imputers[col] = ('simple', method, value)
                print(f"   {col}: filled with {method} = {value}")
        
        return self
    
    def impute_knn(self, columns=None, n_neighbors=5):
        """
        KNN imputation for numerical columns
        """
        if columns is None:
            columns = self.df.select_dtypes(include=[np.number]).columns.tolist()
        
        columns_with_missing = [c for c in columns if self.df[c].isnull().any()]
        
        if not columns_with_missing:
            print("No missing values to impute with KNN")
            return self
        
        print(f"\nKNN imputation (k={n_neighbors}):")
        
        # Scale first
        scaler = StandardScaler()
        df_scaled = pd.DataFrame(
            scaler.fit_transform(self.df[columns].fillna(0)),
            columns=columns,
            index=self.df.index
        )
        
        # Put NaN back
        for col in columns_with_missing:
            df_scaled.loc[self.df[col].isnull(), col] = np.nan
        
        # KNN impute
        imputer = KNNImputer(n_neighbors=n_neighbors)
        df_imputed = pd.DataFrame(
            imputer.fit_transform(df_scaled),
            columns=columns,
            index=self.df.index
        )
        
        # Inverse transform
        df_imputed = pd.DataFrame(
            scaler.inverse_transform(df_imputed),
            columns=columns,
            index=self.df.index
        )
        
        # Update original dataframe
        for col in columns_with_missing:
            missing_mask = self.df[col].isnull()
            self.df.loc[missing_mask, col] = df_imputed.loc[missing_mask, col]
            print(f"   {col}: imputed {missing_mask.sum()} values")
        
        self.imputers['knn'] = imputer
        self.scalers['knn'] = scaler
        
        return self
    
    def impute_iterative(self, columns=None, max_iter=10):
        """
        Iterative (MICE) imputation
        """
        if columns is None:
            columns = self.df.select_dtypes(include=[np.number]).columns.tolist()
        
        columns_with_missing = [c for c in columns if self.df[c].isnull().any()]
        
        if not columns_with_missing:
            print("No missing values to impute")
            return self
        
        print(f"\nIterative imputation (max_iter={max_iter}):")
        
        imputer = IterativeImputer(max_iter=max_iter, random_state=42)
        df_imputed = pd.DataFrame(
            imputer.fit_transform(self.df[columns]),
            columns=columns,
            index=self.df.index
        )
        
        for col in columns_with_missing:
            missing_mask = self.df[col].isnull()
            self.df.loc[missing_mask, col] = df_imputed.loc[missing_mask, col]
            print(f"   {col}: imputed {missing_mask.sum()} values")
        
        self.imputers['iterative'] = imputer
        
        return self
    
    # ---------------------------------------------------------
    # STEP 5: VALIDATION
    # ---------------------------------------------------------
    def validate(self):
        """
        Validate that all missing values are handled
        """
        print("\n" + "="*70)
        print("VALIDATION")
        print("="*70)
        
        remaining_missing = self.df.isnull().sum().sum()
        
        if remaining_missing == 0:
            print("✅ SUCCESS: No missing values remaining!")
        else:
            print(f"⚠️ WARNING: {remaining_missing} missing values still remain")
            print("\nRemaining missing values:")
            print(self.df.isnull().sum()[self.df.isnull().sum() > 0])
        
        return remaining_missing == 0
    
    # ---------------------------------------------------------
    # STEP 6: GET RESULT
    # ---------------------------------------------------------
    def get_result(self):
        """
        Return the processed DataFrame
        """
        return self.df
    
    def get_comparison(self):
        """
        Compare original and processed DataFrames
        """
        print("\n" + "="*70)
        print("BEFORE vs AFTER COMPARISON")
        print("="*70)
        
        print(f"\nOriginal shape: {self.df_original.shape}")
        print(f"Processed shape: {self.df.shape}")
        
        print(f"\nOriginal missing: {self.df_original.isnull().sum().sum()}")
        print(f"Processed missing: {self.df.isnull().sum().sum()}")
        
        return self.df_original, self.df


# ============================================================
# USAGE EXAMPLE
# ============================================================

def demo_missing_data_pipeline():
    """
    Demonstrate the complete pipeline
    """
    # Create sample data with missing values
    np.random.seed(42)
    n = 100
    
    df = pd.DataFrame({
        'Age': np.random.randint(20, 60, n).astype(float),
        'Income': np.random.randint(30000, 150000, n).astype(float),
        'Experience': np.random.randint(0, 30, n).astype(float),
        'Score': np.random.randint(0, 100, n).astype(float),
        'City': np.random.choice(['NYC', 'LA', 'Chicago', 'Houston'], n),
        'Department': np.random.choice(['Sales', 'IT', 'HR', 'Marketing'], n)
    })
    
    # Introduce missing values
    for col in ['Age', 'Income', 'Experience']:
        df.loc[np.random.choice(df.index, 15, replace=False), col] = np.nan
    
    df.loc[np.random.choice(df.index, 10, replace=False), 'Score'] = np.nan
    df.loc[np.random.choice(df.index, 8, replace=False), 'City'] = np.nan
    df.loc[np.random.choice(df.index, 5, replace=False), 'Department'] = np.nan
    
    print("Original Data Sample:")
    print(df.head(10))
    
    # Process with pipeline
    handler = MissingDataHandler(df)
    
    # Step 1: Analyze
    handler.analyze_missing()
    
    # Step 2: Create missing indicators (for important features)
    handler.create_missing_indicators(columns=['Income'], threshold=0.1)
    
    # Step 3: Impute
    handler.impute_numerical(method='median')
    handler.impute_categorical(method='mode')
    
    # Step 4: Validate
    handler.validate()
    
    # Step 5: Get result
    df_processed = handler.get_result()
    
    print("\nProcessed Data Sample:")
    print(df_processed.head(10))
    
    return df_processed

# Run demo
# df_result = demo_missing_data_pipeline()
10.2 Train-Test Split Considerations
Python

# ============================================================
# CRITICAL: HANDLING MISSING DATA IN TRAIN-TEST SPLIT
# ============================================================

"""
IMPORTANT RULES:
1. Split data BEFORE imputation
2. Fit imputers on TRAINING data only
3. Transform BOTH train and test with same imputer
4. NEVER fit imputer on test data (data leakage!)
"""

from sklearn.model_selection import train_test_split
from sklearn.impute import SimpleImputer
import pandas as pd
import numpy as np

def proper_train_test_imputation(df, target_column, test_size=0.2):
    """
    Properly handle missing data with train-test split
    """
    # Separate features and target
    X = df.drop(columns=[target_column])
    y = df[target_column]
    
    # Split FIRST (before imputation!)
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=test_size, random_state=42
    )
    
    print(f"Train shape: {X_train.shape}")
    print(f"Test shape:  {X_test.shape}")
    print(f"\nMissing in train:\n{X_train.isnull().sum()}")
    print(f"\nMissing in test:\n{X_test.isnull().sum()}")
    
    # Separate numeric and categorical columns
    numeric_cols = X_train.select_dtypes(include=[np.number]).columns.tolist()
    categorical_cols = X_train.select_dtypes(include=['object']).columns.tolist()
    
    # Impute numeric columns
    if numeric_cols:
        imputer_num = SimpleImputer(strategy='median')
        
        # FIT on train only!
        imputer_num.fit(X_train[numeric_cols])
        
        # TRANSFORM both
        X_train[numeric_cols] = imputer_num.transform(X_train[numeric_cols])
        X_test[numeric_cols] = imputer_num.transform(X_test[numeric_cols])
        
        print(f"\nNumeric imputation values: {dict(zip(numeric_cols, imputer_num.statistics_))}")
    
    # Impute categorical columns
    if categorical_cols:
        imputer_cat = SimpleImputer(strategy='most_frequent')
        
        # FIT on train only!
        imputer_cat.fit(X_train[categorical_cols])
        
        # TRANSFORM both
        X_train[categorical_cols] = imputer_cat.transform(X_train[categorical_cols])
        X_test[categorical_cols] = imputer_cat.transform(X_test[categorical_cols])
        
        print(f"Categorical imputation values: {dict(zip(categorical_cols, imputer_cat.statistics_))}")
    
    print(f"\nAfter imputation:")
    print(f"Missing in train: {X_train.isnull().sum().sum()}")
    print(f"Missing in test:  {X_test.isnull().sum().sum()}")
    
    return X_train, X_test, y_train, y_test

# Example
df = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, 45, np.nan, 55, 60, np.nan, 70],
    'Income': [50000, 60000, np.nan, 80000, np.nan, 100000, 110000, np.nan, 130000, 140000],
    'City': ['NYC', np.nan, 'LA', 'NYC', 'LA', np.nan, 'Chicago', 'NYC', 'LA', np.nan],
    'Target': [0, 1, 0, 1, 0, 1, 0, 1, 0, 1]
})

print("Original Data:")
print(df)

X_train, X_test, y_train, y_test = proper_train_test_imputation(df, 'Target')
10.3 Using Sklearn Pipeline
Python

# ============================================================
# SKLEARN PIPELINE FOR MISSING DATA
# ============================================================

from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score, train_test_split
import pandas as pd
import numpy as np

def create_complete_pipeline(numeric_features, categorical_features):
    """
    Create sklearn pipeline that handles missing data
    """
    # Numeric pipeline: impute then scale
    numeric_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='median')),
        ('scaler', StandardScaler())
    ])
    
    # Categorical pipeline: impute then encode
    categorical_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='most_frequent')),
        ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
    ])
    
    # Combine transformers
    preprocessor = ColumnTransformer(
        transformers=[
            ('num', numeric_transformer, numeric_features),
            ('cat', categorical_transformer, categorical_features)
        ],
        remainder='drop'  # Drop any columns not specified
    )
    
    # Full pipeline with model
    full_pipeline = Pipeline(steps=[
        ('preprocessor', preprocessor),
        ('classifier', RandomForestClassifier(n_estimators=100, random_state=42))
    ])
    
    return full_pipeline

# Example usage
df = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, np.nan, 50, 55, np.nan, 65, 70],
    'Income': [50000, 60000, np.nan, 80000, 90000, np.nan, 110000, 120000, np.nan, 140000],
    'City': ['NYC', np.nan, 'LA', 'NYC', 'LA', 'Chicago', np.nan, 'NYC', 'LA', np.nan],
    'Department': ['Sales', 'IT', np.nan, 'HR', 'Sales', 'IT', 'HR', np.nan, 'Sales', 'IT'],
    'Target': [0, 1, 0, 1, 0, 1, 0, 1, 0, 1]
})

# Define feature types
numeric_features = ['Age', 'Income']
categorical_features = ['City', 'Department']

# Create pipeline
pipeline = create_complete_pipeline(numeric_features, categorical_features)

# Split data
X = df.drop(columns=['Target'])
y = df['Target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train pipeline (automatically handles missing values!)
pipeline.fit(X_train, y_train)

# Evaluate
train_score = pipeline.score(X_train, y_train)
test_score = pipeline.score(X_test, y_test)

print(f"Train accuracy: {train_score:.4f}")
print(f"Test accuracy: {test_score:.4f}")

# Cross-validation
cv_scores = cross_val_score(pipeline, X, y, cv=5)
print(f"CV scores: {cv_scores}")
print(f"CV mean: {cv_scores.mean():.4f} (+/- {cv_scores.std()*2:.4f})")
11. Common Pitfalls & How to Avoid Them
11.1 Pitfall 1: Imputing BEFORE Train-Test Split
text

❌ WRONG:
    1. Impute missing values on ENTIRE dataset
    2. Then split into train/test
    
    Problem: Test data statistics leak into training!
             This is DATA LEAKAGE!

✅ CORRECT:
    1. Split into train/test FIRST
    2. Fit imputer on TRAINING data only
    3. Transform both train and test with SAME imputer
Code Example:

Python

# ❌ WRONG - Data Leakage!
df_imputed = df.fillna(df.mean())  # Uses ALL data including test
X_train, X_test = train_test_split(df_imputed)

# ✅ CORRECT
X_train, X_test = train_test_split(df)  # Split FIRST
imputer = SimpleImputer()
imputer.fit(X_train)  # Fit on train ONLY
X_train = imputer.transform(X_train)
X_test = imputer.transform(X_test)  # Use SAME imputer
11.2 Pitfall 2: Ignoring Why Data is Missing
text

❌ WRONG:
    "I'll just use mean imputation for everything"
    
    Problem: Ignores missingness mechanism!
    - If MNAR: Mean imputation will be BIASED
    - If MAR: Should use model-based imputation

✅ CORRECT:
    1. Analyze WHY data is missing
    2. Check if missingness correlates with other variables
    3. Choose appropriate method based on mechanism
11.3 Pitfall 3: Using Mean for Skewed Data
text

❌ WRONG:
    Income: [30K, 35K, 40K, NaN, 1M]
    Mean = $276K  ← Heavily influenced by outlier!
    Imputing $276K doesn't make sense.

✅ CORRECT:
    Use Median instead:
    Median = $37.5K  ← Not affected by outlier
    Much more reasonable imputation!
11.4 Pitfall 4: Imputing Target Variable
text

❌ WRONG:
    df['Target'] = df['Target'].fillna(df['Target'].mean())
    model.fit(X, df['Target'])
    
    Problem: 
    - You're creating fake labels!
    - Model learns from fabricated data
    - Results will be unreliable

✅ CORRECT:
    # Remove rows where TARGET is missing
    df = df.dropna(subset=['Target'])
    
    # Only impute FEATURES, not target
11.5 Pitfall 5: Not Creating Missing Indicators
text

❌ WRONG:
    # Just impute and forget
    df['income'] = df['income'].fillna(df['income'].median())
    
    Problem: Lost information about WHICH values were missing!
             Missingness itself might be predictive.

✅ CORRECT:
    # Create indicator BEFORE imputing
    df['income_was_missing'] = df['income'].isnull().astype(int)
    
    # Then impute
    df['income'] = df['income'].fillna(df['income'].median())
    
    # Now model can learn from both the imputed value
    # AND the fact that it was missing
11.6 Pitfall 6: Using Wrong Method for Data Type
text

❌ WRONG:
    # Mean for categorical
    df['City'] = df['City'].fillna(df['City'].mean())  # ERROR!
    
    # Mode for continuous numerical
    df['Temperature'] = df['Temperature'].fillna(df['Temperature'].mode()[0])
    # May not be appropriate for continuous data

✅ CORRECT:
    # Mode for categorical
    df['City'] = df['City'].fillna(df['City'].mode()[0])
    
    # Mean/Median for continuous numerical
    df['Temperature'] = df['Temperature'].fillna(df['Temperature'].median())
11.7 Pitfall 7: Not Checking for All Missing Representations
text

❌ WRONG:
    # Only checking for NaN
    df.isnull().sum()  # Misses other representations!

✅ CORRECT:
    # Check for ALL possible missing representations
    missing_representations = ['', ' ', 'NA', 'N/A', 'NULL', 'null', 
                               'None', 'none', '-', '--', '?', 'NaN', 
                               -999, 999, 0]
    
    for rep in missing_representations:
        count = (df == rep).sum().sum()
        if count > 0:
            print(f"Found {count} occurrences of '{rep}'")
    
    # Replace all with NaN
    df = df.replace(missing_representations, np.nan)
11.8 Summary of Pitfalls
text

┌─────┬────────────────────────────────────────────┬─────────────────────────────────────┐
│ #   │ Pitfall                                    │ Solution                            │
├─────┼────────────────────────────────────────────┼─────────────────────────────────────┤
│ 1   │ Imputing before train-test split          │ Split FIRST, then fit on train only │
│ 2   │ Ignoring missingness mechanism            │ Analyze MCAR/MAR/MNAR first         │
│ 3   │ Using mean for skewed data                │ Use median for skewed/outliers      │
│ 4   │ Imputing target variable                  │ Drop rows with missing target       │
│ 5   │ Not creating missing indicators           │ Create indicator before imputing    │
│ 6   │ Wrong method for data type                │ Mode for categorical, median/mean   │
│ 7   │ Missing non-standard representations      │ Check for '', 'NA', -999, etc.      │
│ 8   │ Over-imputing (imputing everything)       │ Consider if imputation is needed    │
│ 9   │ Not validating after imputation           │ Always check remaining missing      │
│ 10  │ Forgetting to save imputer for production │ Save fitted imputer for inference   │
└─────┴────────────────────────────────────────────┴─────────────────────────────────────┘
12. Interview Questions & Answers
Q1: What is missing data? What are the types of missing data?
Answer:

Missing data refers to values that are not present in a dataset where they should be present.

Three types of missing data:

text

1. MCAR (Missing Completely At Random)
   - Missingness is completely random
   - No relationship with any data
   - Example: Lab equipment randomly fails
   
2. MAR (Missing At Random)
   - Missingness related to OTHER observed variables
   - Can predict who is missing from other columns
   - Example: Young people skip income question (age predicts missingness)
   
3. MNAR (Missing Not At Random)
   - Missingness related to THE MISSING VALUE ITSELF
   - Cannot predict from other variables
   - Example: High earners hide their income
Importance:

MCAR: Any method works, listwise deletion is OK
MAR: Use model-based imputation
MNAR: Hardest to handle, requires domain knowledge
Q2: Why is mean imputation problematic? When should you use it?
Answer:

Problems with mean imputation:

text

1. REDUCES VARIANCE
   Original:  [10, 20, NaN, NaN, 50]
   After:     [10, 20, 26.7, 26.7, 50]
   
   All missing values become the same number!
   Artificially reduces data variability.

2. DISTORTS CORRELATIONS
   If X and Y are correlated, mean doesn't consider this.
   Correlation gets weakened.

3. DOESN'T WORK FOR SKEWED DATA
   Income: [30K, 35K, 40K, NaN, 1M]
   Mean = $276K (pulled by outlier!)
   Should use median = $37.5K

4. IGNORES RELATIONSHIPS
   Doesn't use information from other features.
When to use mean imputation:

text

✅ ACCEPTABLE when:
├── Data is MCAR
├── Data is normally distributed (symmetric)
├── No significant outliers
├── Low percentage of missing (<5%)
├── Quick baseline needed
└── Features are independent
Q3: Explain KNN Imputation. What are its advantages and disadvantages?
Answer:

How KNN Imputation works:

text

1. For each row with missing value:
   a. Find K most similar rows (neighbors) based on other features
   b. Use their values to impute the missing value
   c. Typically take mean/median of neighbors' values

Example:
Row 3: Age=28, Income=?, Score=82

Find K=2 neighbors with similar Age and Score:
- Row 1: Age=25, Income=50000, Score=80
- Row 2: Age=30, Income=60000, Score=85

Imputed Income = (50000 + 60000) / 2 = 55000
Advantages:

text

✅ Uses relationships between features
✅ Better than simple mean/median
✅ Can handle MAR data
✅ Works for both numerical imputation
✅ Considers local structure of data
Disadvantages:

text

❌ SLOW for large datasets (O(n²) complexity)
❌ Requires SCALING (features on different scales cause problems)
❌ Sensitive to K value
❌ Suffers from curse of dimensionality
❌ Memory intensive
❌ Only works for numerical features
Important consideration:

Python

# ALWAYS scale before KNN imputation!
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
df_scaled = scaler.fit_transform(df)
# Then apply KNN imputation
Q4: What is Multiple Imputation? Why is it better than single imputation?
Answer:

Single Imputation Problem:

text

Original: [10, NaN, 30]
Imputed:  [10, 20, 30]

We treat 20 as if it were CERTAIN!
But it's just an ESTIMATE with uncertainty.
This underestimates variance in subsequent analyses.
Multiple Imputation Solution:

text

Create M (typically 5-20) imputed datasets:

Dataset 1: [10, 18, 30]
Dataset 2: [10, 21, 30]
Dataset 3: [10, 19, 30]
Dataset 4: [10, 22, 30]
Dataset 5: [10, 20, 30]

Analyze each dataset separately.
Combine results using Rubin's rules.
Why it's better:

text

✅ Accounts for imputation uncertainty
✅ Provides valid statistical inference
✅ Doesn't underestimate standard errors
✅ More accurate confidence intervals
✅ Statistically sound approach
When to use:

Statistical inference (hypothesis testing, confidence intervals)
When imputation uncertainty matters
Research publications
Q5: How do you handle missing data in a machine learning pipeline?
Answer:

Step-by-step approach:

text

STEP 1: ANALYZE
├── Check missing percentage per column
├── Check missing patterns
├── Determine missingness type (MCAR/MAR/MNAR)

STEP 2: DECIDE STRATEGY
├── Delete columns with >50-70% missing
├── Consider creating missing indicators
├── Choose imputation method based on data type

STEP 3: SPLIT DATA
├── Split into train/test BEFORE imputation
├── CRITICAL: Prevents data leakage!

STEP 4: IMPUTE
├── Fit imputer on TRAINING data only
├── Transform both train and test
├── Use sklearn Pipeline for clean code

STEP 5: VALIDATE
├── Check no missing values remain
├── Verify imputed values are reasonable
Code example:

Python

from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer

# Create preprocessing pipeline
preprocessor = ColumnTransformer([
    ('num', SimpleImputer(strategy='median'), numeric_cols),
    ('cat', SimpleImputer(strategy='most_frequent'), categorical_cols)
])

# Full pipeline
pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('model', RandomForestClassifier())
])

# Split FIRST
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Fit pipeline (handles imputation automatically)
pipeline.fit(X_train, y_train)
Q6: What is the difference between deletion and imputation? When would you use each?
Answer:

text

DELETION:
├── Removes rows or columns with missing values
├── Loses information
├── Simple and fast
└── Can introduce bias if not MCAR

IMPUTATION:
├── Fills missing values with estimates
├── Preserves data size
├── Introduces artificial data
└── Can preserve relationships
When to use DELETION:

text

✅ Column deletion:
├── Column has >50-70% missing
├── Column is not important
└── Imputation would be too inaccurate

✅ Row deletion:
├── Missing is MCAR
├── Low percentage missing (<5%)
├── Have lots of data
└── Complete case analysis needed
When to use IMPUTATION:

text

✅ Use imputation when:
├── Missing is <50%
├── Missing is MAR (can predict from other features)
├── Feature is important
├── Need to preserve sample size
└── Relationships between features matter
Q7: How do you detect whether data is MCAR, MAR, or MNAR?
Answer:

MCAR Detection:

Python

# Little's MCAR Test (statistical)
# If p-value > 0.05, likely MCAR

# Simple check: Compare groups
missing_group = df[df['income'].isna()]['age'].mean()
complete_group = df[df['income'].notna()]['age'].mean()

# If means are similar → Possibly MCAR
# If significantly different → Likely MAR
MAR Detection:

Python

# Check correlation between missingness and other variables
df['income_missing'] = df['income'].isnull().astype(int)

# Correlation with other features
correlations = df.corr()['income_missing']

# If income_missing correlates with age, education, etc. → MAR
MNAR Detection:

text

MNAR CANNOT be statistically detected!

Why?
- Missingness depends on the missing value itself
- We can't see the missing value
- Need domain knowledge

Example indicators of MNAR:
- Rich people hiding income (sensitive data)
- Severely ill patients dropping out
- Failed students not reporting grades
Q8: What is the "Missing Indicator" approach? When should you use it?
Answer:

Concept:

Python

# Before imputing, create a binary indicator
df['income_was_missing'] = df['income'].isnull().astype(int)

# Then impute
df['income'] = df['income'].fillna(df['income'].median())

# Now you have BOTH:
# 1. The imputed value
# 2. Information that it WAS missing
Why it's useful:

text

Missingness itself can be INFORMATIVE!

Example:
- In credit scoring, missing income might indicate financial problems
- In healthcare, missing lab results might indicate patient didn't visit
- This information would be LOST without the indicator

The model can learn:
"When income_was_missing=1, this pattern tends to occur..."
When to use:

text

✅ Use missing indicators when:
├── Missingness might be predictive
├── Using tree-based models (they can use indicators well)
├── Percentage of missing is significant (>5%)
├── Missing is MAR or MNAR
└── Want to preserve missingness information
Q9: How do you handle missing values in production/inference?
Answer:

Key principle: Use the SAME imputation parameters from training!

Python

# TRAINING PHASE
imputer = SimpleImputer(strategy='median')
imputer.fit(X_train)  # Learn parameters
X_train_imputed = imputer.transform(X_train)

# SAVE the imputer
import joblib
joblib.dump(imputer, 'imputer.pkl')

# ================================

# PRODUCTION/INFERENCE PHASE
# Load saved imputer
imputer = joblib.load('imputer.pkl')

# Apply to new data
new_data_imputed = imputer.transform(new_data)

# Make prediction
prediction = model.predict(new_data_imputed)
Using sklearn Pipeline (recommended):

Python

# Pipeline handles everything
pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler()),
    ('model', RandomForestClassifier())
])

# Train
pipeline.fit(X_train, y_train)

# Save entire pipeline
joblib.dump(pipeline, 'model_pipeline.pkl')

# In production
pipeline = joblib.load('model_pipeline.pkl')
prediction = pipeline.predict(new_data)  # Handles imputation automatically!
Q10: Compare different imputation methods. Which would you choose for different scenarios?
Answer:

text

┌─────────────────────┬────────────────────────────────────────────────────────┐
│ Scenario            │ Recommended Method                                     │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Quick baseline      │ Mean (normal data) or Median (skewed/outliers)        │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Categorical data    │ Mode or "Unknown" category                            │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Time series         │ Forward fill, Interpolation                           │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Related features    │ KNN or Iterative (MICE)                               │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Non-linear relations│ MissForest (Random Forest based)                      │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Statistical analysis│ Multiple Imputation                                    │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Large dataset       │ Simple methods (mean/median) - KNN too slow           │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Small dataset       │ KNN or Iterative - preserve every sample              │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Mixed data types    │ Iterative with appropriate estimators                 │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Deep learning       │ Autoencoder or DataWig                                │
├─────────────────────┼────────────────────────────────────────────────────────┤
│ Production system   │ Simple methods in Pipeline (fast, reliable)           │
└─────────────────────┴────────────────────────────────────────────────────────┘
Decision flowchart:

text

START: What type of data?
    │
    ├─ NUMERICAL
    │   │
    │   ├─ Skewed or has outliers?
    │   │   ├─ Yes → MEDIAN
    │   │   └─ No → MEAN or MEDIAN
    │   │
    │   ├─ Features correlated?
    │   │   ├─ Yes → KNN or ITERATIVE
    │   │   └─ No → MEAN/MEDIAN
    │   │
    │   └─ Time series?
    │       └─ Yes → FORWARD FILL or INTERPOLATION
    │
    ├─ CATEGORICAL
    │   │
    │   ├─ One dominant category?
    │   │   └─ Yes → MODE
    │   │
    │   └─ No dominant category?
    │       └─ → "UNKNOWN" or CLASSIFICATION
    │
    └─ MIXED
        └─ → ITERATIVE with mixed estimators
           → or handle separately
Q11: What are the consequences of not handling missing data properly?
Answer:

text

CONSEQUENCE 1: MODEL FAILURE
────────────────────────────
Most ML algorithms crash with NaN values:
- LinearRegression → Error
- RandomForest (sklearn) → Error
- Neural Networks → NaN propagation

Only some handle missing natively:
- XGBoost, LightGBM, CatBoost → OK


CONSEQUENCE 2: BIASED RESULTS
────────────────────────────
If missing is NOT random (MAR/MNAR):
- Deleting rows removes specific patterns
- Mean imputation ignores relationships
- Model learns from distorted data
- Predictions systematically wrong for certain groups


CONSEQUENCE 3: REDUCED STATISTICAL POWER
────────────────────────────
Deleting rows with missing values:
- Loses sample size
- Wider confidence intervals
- May fail to detect real effects
- Less reliable conclusions


CONSEQUENCE 4: WRONG IMPUTATION BIAS
────────────────────────────
Bad imputation introduces:
- Artificial patterns (all missing become same value)
- Reduced variance (underestimate uncertainty)
- Weakened correlations
- Overfitting to imputed values


CONSEQUENCE 5: DATA LEAKAGE
────────────────────────────
If imputation uses test data:
- Model sees future information
- Overly optimistic performance metrics
- Poor real-world performance
Q12: How would you handle a dataset where 40% of values in an important feature are missing?
Answer:

This is a challenging scenario requiring careful consideration:

text

STEP 1: UNDERSTAND THE MISSINGNESS
─────────────────────────────────
- Why is 40% missing?
- Is it MCAR, MAR, or MNAR?
- Is the missingness pattern informative?

Questions to ask:
- Can we get the data from another source?
- Is there a systematic reason for missingness?
- Does missingness correlate with other features?


STEP 2: CREATE MISSING INDICATOR
─────────────────────────────────
df['feature_was_missing'] = df['feature'].isnull().astype(int)

This preserves the information that 40% was missing.
The model can learn from this pattern.


STEP 3: CHOOSE IMPUTATION STRATEGY
─────────────────────────────────
Option A: Model-based imputation (if MAR)
    - Use KNN or Iterative imputation
    - Leverages relationships with other features
    
Option B: Multiple Imputation (for statistical analysis)
    - Create 5-10 imputed datasets
    - Accounts for uncertainty
    
Option C: Conditional imputation
    - Different imputation for different subgroups
    - E.g., different median for different categories


STEP 4: VALIDATE IMPUTATION
─────────────────────────────────
- Check if imputed values are reasonable
- Compare distributions before/after
- Test model with and without the feature
- Consider feature importance


STEP 5: ALTERNATIVE APPROACHES
─────────────────────────────────
- Use algorithms that handle missing (XGBoost, LightGBM)
- Create a "missing" category (for categorical)
- Feature engineering: combine with other features
- Collect more data if possible
Code example:

Python

import pandas as pd
import numpy as np
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

# Check missingness pattern
print(f"Missing: {df['important_feature'].isnull().sum()}")
print(f"Missing %: {df['important_feature'].isnull().mean()*100:.1f}%")

# Check if missingness correlates with other variables
df['is_missing'] = df['important_feature'].isnull().astype(int)
correlations = df.corr()['is_missing'].sort_values()
print(f"Correlations with missingness:\n{correlations}")

# If MAR (missingness correlates with other features):
# Use iterative imputation

# Step 1: Create missing indicator
df['feature_was_missing'] = df['important_feature'].isnull().astype(int)

# Step 2: Iterative imputation
imputer = IterativeImputer(max_iter=10, random_state=42)
df['important_feature'] = imputer.fit_transform(df[['important_feature']])

# Step 3: Validate
print(f"After imputation - Missing: {df['important_feature'].isnull().sum()}")
print(f"Imputed statistics: {df['important_feature'].describe()}")
Q13: Explain the concept of data leakage in the context of missing data handling.
Answer:

What is Data Leakage?

text

Data leakage occurs when information from OUTSIDE the training set
is used to create the model.

In missing data context:
- Using test set statistics to impute training set
- Fitting imputer on entire dataset before splitting
- Using future values to fill past values (time series)
Example of Data Leakage:

Python

# ❌ WRONG - DATA LEAKAGE!

# Step 1: Impute using ENTIRE dataset
df['income'] = df['income'].fillna(df['income'].mean())  # Uses test data!

# Step 2: Then split
X_train, X_test = train_test_split(df)

# Problem:
# The mean includes TEST data values!
# Training data "knows" something about test data.
# Model performance will be OVEROPTIMISTIC.
Why it's problematic:

text

Training Data:     Income = [50K, 60K, NaN, 70K]
Test Data:         Income = [100K, 120K, NaN]

Combined Mean = (50 + 60 + 70 + 100 + 120) / 5 = 80K

If we impute training NaN with 80K:
- Training set now "knows" test values are high
- This information leaks into model training
- Model appears to perform better than it actually will
- REAL-WORLD PERFORMANCE WILL BE WORSE!
Correct Approach:

Python

# ✅ CORRECT - NO LEAKAGE

# Step 1: Split FIRST
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Step 2: Fit imputer on TRAINING data only
imputer = SimpleImputer(strategy='mean')
imputer.fit(X_train)  # Only sees training data!

# Step 3: Transform both sets with SAME imputer
X_train_imputed = imputer.transform(X_train)
X_test_imputed = imputer.transform(X_test)

# Now:
# - Training imputation uses ONLY training statistics
# - Test set uses training statistics (as in production)
# - No leakage!
Using Pipeline (Best Practice):

Python

from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

# Pipeline ensures correct order of operations
pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='mean')),
    ('scaler', StandardScaler()),
    ('model', LogisticRegression())
])

# Split first
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Fit pipeline on training data
# (imputer learns from training data only)
pipeline.fit(X_train, y_train)

# Evaluate on test data
# (uses training imputation parameters)
score = pipeline.score(X_test, y_test)
Q14: What is MICE (Multiple Imputation by Chained Equations)? How does it work?
Answer:

MICE Overview:

text

MICE = Multiple Imputation by Chained Equations
Also known as: Fully Conditional Specification (FCS)
                Sequential Regression Imputation

Key idea: Impute each variable using a regression model,
          iterating until values stabilize.
How MICE Works - Step by Step:

text

Initial State:
┌─────┬─────┬─────┐
│  A  │  B  │  C  │
├─────┼─────┼─────┤
│ 10  │ NaN │ 30  │
│ NaN │ 50  │ NaN │
│ 70  │ 80  │ 90  │
└─────┴─────┴─────┘

STEP 1: Initial Imputation (e.g., mean)
┌─────┬─────┬─────┐
│  A  │  B  │  C  │
├─────┼─────┼─────┤
│ 10  │ 65* │ 30  │  (* = imputed)
│ 40* │ 50  │ 60* │
│ 70  │ 80  │ 90  │
└─────┴─────┴─────┘

STEP 2: Iteration 1 - Impute A
- Set A's imputed values back to NaN
- Use B and C to predict A
- Train regression: A ~ B + C (on complete rows)
- Predict missing A values

STEP 3: Iteration 1 - Impute B
- Set B's imputed values back to NaN
- Use A and C to predict B
- Train regression: B ~ A + C
- Predict missing B values

STEP 4: Iteration 1 - Impute C
- Set C's imputed values back to NaN
- Use A and B to predict C
- Train regression: C ~ A + B
- Predict missing C values

STEP 5: Repeat Steps 2-4 until convergence
- Typically 5-10 iterations
- Values stabilize as iterations progress

Final Result:
More accurate imputations that preserve
relationships between variables!
Code Implementation:

Python

from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer
from sklearn.linear_model import BayesianRidge
import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'A': [10, np.nan, 70, 40, 50],
    'B': [np.nan, 50, 80, 60, np.nan],
    'C': [30, np.nan, 90, 70, 80]
})

print("Original Data:")
print(df)

# MICE imputation
mice_imputer = IterativeImputer(
    estimator=BayesianRidge(),  # Regression model
    max_iter=10,                # Number of iterations
    random_state=42,
    verbose=2                   # Show progress
)

df_imputed = pd.DataFrame(
    mice_imputer.fit_transform(df),
    columns=df.columns
)

print("\nAfter MICE Imputation:")
print(df_imputed)
Advantages of MICE:

text

✅ Preserves relationships between variables
✅ Handles different variable types (with appropriate models)
✅ Can use different models for different variables
✅ Produces reasonable imputations for MAR data
✅ Statistically principled approach
Disadvantages:

text

❌ Computationally expensive (multiple iterations)
❌ Assumes relationships are correctly specified
❌ May not converge for complex data
❌ Can be slow for large datasets
Q15: How do tree-based algorithms (XGBoost, LightGBM) handle missing values natively?
Answer:

Native Missing Value Handling:

text

Tree-based algorithms can handle missing values WITHOUT imputation!

How they work:

At each split decision:
1. Algorithm considers: "Where should missing values go?"
2. Tries BOTH options: send missing left OR send missing right
3. Chooses the direction that minimizes loss
4. Learns OPTIMAL direction for each split

Example:
              Split: Age > 30?
                    │
           ┌───────┴───────┐
           │               │
        ≤ 30            > 30
           │               │
    Where does NaN go?
    
    Option A: NaN goes LEFT  → Calculate loss
    Option B: NaN goes RIGHT → Calculate loss
    
    Choose option with lower loss!
XGBoost Approach:

Python

import xgboost as xgb
import numpy as np
import pandas as pd

# Data WITH missing values
X = pd.DataFrame({
    'Age': [25, np.nan, 35, 40, np.nan, 50],
    'Income': [50000, 60000, np.nan, 80000, 70000, np.nan]
})
y = [0, 1, 0, 1, 0, 1]

# XGBoost handles NaN automatically!
model = xgb.XGBClassifier(
    use_label_encoder=False,
    eval_metric='logloss'
)
model.fit(X, y)  # No error! Works with NaN!

# Make predictions (also handles NaN)
predictions = model.predict(X)
print(predictions)
LightGBM Approach:

Python

import lightgbm as lgb

# LightGBM also handles NaN natively
model = lgb.LGBMClassifier()
model.fit(X, y)  # Works with NaN!

predictions = model.predict(X)
CatBoost Approach:

Python

from catboost import CatBoostClassifier

# CatBoost handles NaN and categorical features
model = CatBoostClassifier(verbose=0)
model.fit(X, y)  # Works with NaN!
Advantages of Native Handling:

text

✅ No preprocessing needed
✅ No imputation bias introduced
✅ Algorithm learns optimal handling
✅ Can treat "missingness" as informative
✅ Simpler pipeline
When to still consider imputation:

text

Even with native handling, imputation may help when:
- Using ensemble with other algorithms (that need imputation)
- Want consistent preprocessing across models
- Need interpretable imputations
- Very high missing percentage
Final Summary & Quick Reference
Missing Data Handling Flowchart
text

┌──────────────────────────────────────────────────────────────────────────────┐
│                     MISSING DATA HANDLING FLOWCHART                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  STEP 1: DETECT                                                              │
│  ├── df.isnull().sum()                                                       │
│  ├── Check percentage: df.isnull().mean() * 100                              │
│  ├── Visualize: missingno.matrix(df)                                         │
│  └── Check for hidden missing: '', 'NA', -999, etc.                          │
│                                                                              │
│  STEP 2: ANALYZE                                                             │
│  ├── Determine type: MCAR, MAR, or MNAR                                      │
│  ├── Check correlations with missingness                                     │
│  └── Understand WHY data is missing                                          │
│                                                                              │
│  STEP 3: DECIDE                                                              │
│  │                                                                           │
│  │  Missing % > 50-70%?                                                      │
│  │  └── YES → Consider DELETING column                                       │
│  │                                                                           │
│  │  Missing % < 5% and MCAR?                                                 │
│  │  └── YES → LISTWISE DELETION is OK                                        │
│  │                                                                           │
│  │  Otherwise?                                                               │
│  │  └── Use IMPUTATION                                                       │
│  │                                                                           │
│  STEP 4: IMPUTE                                                              │
│  ├── Numerical: Mean/Median/KNN/Iterative                                    │
│  ├── Categorical: Mode/"Unknown"                                             │
│  ├── Time Series: Forward Fill/Interpolation                                 │
│  └── Create missing indicators if informative                                │
│                                                                              │
│  STEP 5: VALIDATE                                                            │
│  ├── Confirm no missing values remain                                        │
│  ├── Check imputed values are reasonable                                     │
│  └── Compare model performance with/without imputation                       │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
Quick Reference: Method Selection
text

┌────────────────────────┬──────────────────────────────────────────────────────┐
│ Data Type              │ Recommended Methods                                  │
├────────────────────────┼──────────────────────────────────────────────────────┤
│ Numerical (Normal)     │ Mean, KNN, Iterative                                 │
│ Numerical (Skewed)     │ Median, KNN, Iterative                               │
│ Numerical (Outliers)   │ Median, KNN                                          │
│ Categorical            │ Mode, "Unknown" constant                             │
│ Time Series            │ Forward Fill, Interpolation                          │
│ Mixed Types            │ Iterative (MICE), separate handling                  │
│ Large Dataset          │ Simple methods (Mean/Median/Mode)                    │
│ Small Dataset          │ KNN, Iterative (preserve samples)                    │
│ High % Missing         │ Model-based + Missing Indicator                      │
└────────────────────────┴──────────────────────────────────────────────────────┘
Quick Reference: Missingness Type
text

┌─────────────┬─────────────────────────────────┬───────────────────────────────┐
│ Type        │ Characteristic                  │ Best Approach                 │
├─────────────┼─────────────────────────────────┼───────────────────────────────┤
│ MCAR        │ Completely random               │ Any method works              │
│             │ No pattern                      │ Listwise deletion OK          │
├─────────────┼─────────────────────────────────┼───────────────────────────────┤
│ MAR         │ Related to OTHER variables      │ Model-based imputation        │
│             │ Predictable from data           │ KNN, Iterative, Multiple      │
├─────────────┼─────────────────────────────────┼───────────────────────────────┤
│ MNAR        │ Related to MISSING value itself │ Domain expertise needed       │
│             │ Cannot predict                  │ Selection models              │
│             │                                 │ Missing indicator + caution   │
└─────────────┴─────────────────────────────────┴───────────────────────────────┘
Quick Reference: Code Templates
Python

# ============================================================
# TEMPLATE 1: Simple Imputation
# ============================================================
from sklearn.impute import SimpleImputer

# Numerical: Median
imputer_num = SimpleImputer(strategy='median')
df[num_cols] = imputer_num.fit_transform(df[num_cols])

# Categorical: Mode
imputer_cat = SimpleImputer(strategy='most_frequent')
df[cat_cols] = imputer_cat.fit_transform(df[cat_cols])


# ============================================================
# TEMPLATE 2: KNN Imputation
# ============================================================
from sklearn.impute import KNNImputer
from sklearn.preprocessing import StandardScaler

# Scale first!
scaler = StandardScaler()
df_scaled = scaler.fit_transform(df)

# KNN impute
imputer = KNNImputer(n_neighbors=5)
df_imputed = imputer.fit_transform(df_scaled)

# Inverse transform
df_imputed = scaler.inverse_transform(df_imputed)


# ============================================================
# TEMPLATE 3: Iterative (MICE) Imputation
# ============================================================
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

imputer = IterativeImputer(max_iter=10, random_state=42)
df_imputed = imputer.fit_transform(df)


# ============================================================
# TEMPLATE 4: Complete Pipeline (Production Ready)
# ============================================================
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder

# Define transformers
numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('encoder', OneHotEncoder(handle_unknown='ignore'))
])

# Combine
preprocessor = ColumnTransformer([
    ('num', numeric_transformer, numeric_columns),
    ('cat', categorical_transformer, categorical_columns)
])

# Full pipeline
pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('model', YourModel())
])

# Use
pipeline.fit(X_train, y_train)
predictions = pipeline.predict(X_test)
Common Mistakes Checklist
text

Before submitting your code, verify:

□ Did I split data BEFORE imputation?
□ Did I fit imputer on TRAINING data only?
□ Did I use the same imputer for test data?
□ Did I create missing indicators where appropriate?
□ Did I use appropriate method for each data type?
□ Did I check for non-standard missing representations?
□ Did I validate that no missing values remain?
□ Did I save the imputer for production use?
□ Did I avoid imputing the target variable?
□ Did I consider if missingness is informative?
Congratulations! 🎉
You now have complete mastery of Handling Missing Data from basic to advanced level!

What you've learned:

✅ What missing data is and why it occurs
✅ Three types of missingness (MCAR, MAR, MNAR) and how to detect them
✅ How to detect and visualize missing data
✅ Impact of missing data on ML models
✅ Deletion methods (listwise, pairwise, column deletion)
✅ Simple imputation (mean, median, mode, constant, forward/backward fill)
✅ Advanced imputation (KNN, Iterative/MICE, Multiple Imputation)
✅ Machine learning based imputation (regression, classification, deep learning)
✅ Handling different data types (numerical, categorical, time series, mixed)
✅ Production-ready pipelines
✅ Common pitfalls and how to avoid them
✅ Interview-ready answers
Next Steps:

Practice on real datasets with various missing patterns
Experiment with different imputation methods and compare results
Build production pipelines that handle missing data properly
Read research papers on advanced imputation methods
Keep this guide handy - it's your complete reference for Handling Missing Data! 📚

Good luck in your ML career! 🚀