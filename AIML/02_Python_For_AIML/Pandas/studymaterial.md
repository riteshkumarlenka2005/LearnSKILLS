The Complete Pandas Mastery Guide
From Absolute Beginner to Advanced Data Scientist
Table of Contents
Introduction - What is Pandas and Why Should You Care?
Installation and Setup
Series - The Foundation of Pandas
DataFrame - The Heart of Pandas
Data Input/Output - Loading and Saving Data
Data Selection and Indexing
Data Filtering and Boolean Indexing
Data Cleaning and Preprocessing
Handling Missing Data
Data Transformation
String Operations
Working with Dates and Times
Grouping and Aggregation
Merging, Joining, and Concatenating
Reshaping Data - Pivot and Melt
Multi-Index and Advanced Indexing
Window Functions and Rolling Calculations
Categorical Data
Performance Optimization
Pandas for Machine Learning
Real-World Projects and Exercises
Best Practices and Common Pitfalls
Chapter 1: Introduction - What is Pandas and Why Should You Care?
1.1 The Story of Pandas
Imagine you're a chef with a huge recipe book. You could flip through every page manually to find recipes with chicken, OR you could have a magical assistant that instantly shows you all chicken recipes, sorted by cooking time, filtered by calories.

Pandas is that magical assistant for your data.

What Does Pandas Stand For?
Panel Data + System = Pandas

(Originally designed for analyzing financial panel data)

The Problem Pandas Solves
Without Pandas (Pure Python):

Python

# Reading a CSV file and finding average salary
data = []
with open('employees.csv', 'r') as f:
    headers = f.readline().strip().split(',')
    for line in f:
        values = line.strip().split(',')
        data.append(dict(zip(headers, values)))

# Find average salary
total = 0
count = 0
for row in data:
    if row['department'] == 'Engineering':
        total += float(row['salary'])
        count += 1
avg_salary = total / count

# This takes 15 lines and is error-prone!
With Pandas:

Python

import pandas as pd

df = pd.read_csv('employees.csv')
avg_salary = df[df['department'] == 'Engineering']['salary'].mean()

# Just 2 lines! Clear, readable, and fast!
1.2 Why is Pandas Essential for ML/Data Science?
text

                        ML/Data Science Pipeline
                        
    ┌──────────────────────────────────────────────────────────────────┐
    │                                                                   │
    │  ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────┐ │
    │  │  Data   │ → │  Data   │ → │  Data   │ → │  Model  │ → │ Model│ │
    │  │  Load   │   │ Clean   │   │  Prep   │   │ Training│   │ Eval │ │
    │  └─────────┘   └─────────┘   └─────────┘   └─────────┘   └─────┘ │
    │       ↑             ↑             ↑                               │
    │       └─────────────┴─────────────┘                               │
    │                     │                                              │
    │               ┌─────┴─────┐                                        │
    │               │  PANDAS   │                                        │
    │               │  80% of   │                                        │
    │               │  the work │                                        │
    │               └───────────┘                                        │
    │                                                                   │
    └──────────────────────────────────────────────────────────────────┘
80% of a Data Scientist's time is spent on data preparation using Pandas!

1.3 Pandas in the Python Ecosystem
text

                    ┌─────────────────────────────────────────┐
                    │           ML/AI LIBRARIES               │
                    └─────────────────────────────────────────┘
                                        │
        ┌───────────────────────────────┼───────────────────────────────┐
        │                               │                               │
        ▼                               ▼                               ▼
┌───────────────┐               ┌───────────────┐               ┌───────────────┐
│  Scikit-Learn │               │  TensorFlow   │               │   PyTorch     │
└───────────────┘               └───────────────┘               └───────────────┘
        │                               │                               │
        └───────────────────────────────┼───────────────────────────────┘
                                        │
                            ┌───────────┴───────────┐
                            │                       │
                            ▼                       ▼
                    ┌───────────────┐       ┌───────────────┐
                    │    PANDAS     │       │   Matplotlib  │
                    │  (Data Prep)  │       │    Seaborn    │
                    │               │       │  (Visualize)  │
                    └───────────────┘       └───────────────┘
                            │
                            ▼
                    ┌───────────────┐
                    │     NumPy     │
                    │ (Foundation)  │
                    └───────────────┘
1.4 Key Concepts You Must Understand
The Two Main Data Structures
text

┌─────────────────────────────────────────────────────────────────────┐
│                         PANDAS DATA STRUCTURES                       │
├─────────────────────────────────┬───────────────────────────────────┤
│            SERIES               │           DATAFRAME               │
├─────────────────────────────────┼───────────────────────────────────┤
│                                 │                                   │
│  • 1-Dimensional               │  • 2-Dimensional                  │
│  • Like a single column        │  • Like a spreadsheet/table       │
│  • Has index + values          │  • Has rows + columns             │
│  • Homogeneous data            │  • Each column can be different   │
│                                 │    type                           │
│     Index   Values              │                                   │
│       0  →   10                 │        Col1   Col2   Col3        │
│       1  →   20                 │   0  │   A  │  10  │  1.5        │
│       2  →   30                 │   1  │   B  │  20  │  2.5        │
│       3  →   40                 │   2  │   C  │  30  │  3.5        │
│                                 │                                   │
└─────────────────────────────────┴───────────────────────────────────┘
Key Terminology
Term	Meaning	Example
DataFrame	2D table with rows and columns	Entire spreadsheet
Series	1D array with labels	Single column
Index	Row labels	0, 1, 2 or 'a', 'b', 'c'
Column	Vertical data with a name	'Age', 'Salary'
Row	Horizontal record	One person's data
Cell	Single value	25 (one age value)
dtype	Data type of a column	int64, float64, object
NaN	Missing value	Not a Number
axis=0	Rows (down)	Operations on rows
axis=1	Columns (across)	Operations on columns
1.5 Pandas vs Excel vs SQL
Feature	Pandas	Excel	SQL
Data Size	Millions of rows	~1M rows max	Billions of rows
Speed	Very Fast	Slow	Fast
Automation	Full automation	Limited	Moderate
ML Integration	Perfect	Poor	Requires export
Complex Analysis	Excellent	Limited	Moderate
Learning Curve	Moderate	Easy	Moderate
Reproducibility	Excellent	Poor	Good
Chapter 2: Installation and Setup
2.1 Installing Pandas
Method 1: Using pip (Recommended)
Bash

pip install pandas
Method 2: Using conda (Anaconda/Miniconda)
Bash

conda install pandas
Method 3: Installing with dependencies
Bash

pip install pandas numpy matplotlib seaborn jupyter
2.2 Verifying Installation
Python

import pandas as pd
import numpy as np

# Check versions
print(f"Pandas version: {pd.__version__}")
print(f"NumPy version: {np.__version__}")

# Quick test
df = pd.DataFrame({'A': [1, 2, 3], 'B': ['x', 'y', 'z']})
print(df)

print("\n✓ Pandas is working correctly!")
2.3 The Import Convention
Python

import pandas as pd    # ← ALWAYS use this convention
import numpy as np     # ← NumPy is often needed with Pandas
Why pd?

Universal standard in the data science community
Every tutorial, documentation, and professional code uses it
Short and memorable
Never do this:

Python

import pandas              # Too verbose: pandas.DataFrame()
import pandas as p         # Non-standard, confuses others
from pandas import *       # Namespace pollution, causes conflicts
2.4 Pandas Display Options
Python

import pandas as pd

# Set display options for better readability
pd.set_option('display.max_rows', 100)        # Show more rows
pd.set_option('display.max_columns', 20)      # Show more columns
pd.set_option('display.width', 200)           # Wider display
pd.set_option('display.precision', 2)         # 2 decimal places
pd.set_option('display.max_colwidth', 50)     # Column width

# Reset all options to default
# pd.reset_option('all')

# View current options
print(pd.get_option('display.max_rows'))
2.5 Your First Pandas Program
Python

import pandas as pd

# Create your first DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'City': ['New York', 'Paris', 'London', 'Tokyo'],
    'Salary': [50000, 60000, 70000, 55000]
}

df = pd.DataFrame(data)

# Display the DataFrame
print("My First DataFrame:")
print(df)

# Basic operations
print("\nBasic Statistics:")
print(df.describe())

print("\nColumn Names:", df.columns.tolist())
print("Shape:", df.shape)
print("Data Types:\n", df.dtypes)

print("\n🎉 Congratulations! You've created your first DataFrame!")
Output:

text

My First DataFrame:
      Name  Age      City  Salary
0    Alice   25  New York   50000
1      Bob   30     Paris   60000
2  Charlie   35    London   70000
3    Diana   28     Tokyo   55000

Basic Statistics:
             Age        Salary
count   4.000000      4.000000
mean   29.500000  58750.000000
std     4.203173   8539.125638
min    25.000000  50000.000000
25%    27.250000  53750.000000
50%    29.000000  57500.000000
75%    31.250000  62500.000000
max    35.000000  70000.000000

Column Names: ['Name', 'Age', 'City', 'Salary']
Shape: (4, 4)
Data Types:
 Name      object
Age        int64
City      object
Salary     int64
dtype: object

🎉 Congratulations! You've created your first DataFrame!
Chapter 3: Series - The Foundation of Pandas
3.1 What is a Series?
A Series is a one-dimensional labeled array capable of holding any data type.

Think of it as a single column from a spreadsheet, with an index.

text

Visual Representation:

    Index │ Values
    ──────┼────────
      0   │   10
      1   │   20
      2   │   30
      3   │   40
      4   │   50
      
OR with custom index:

    Index │ Values
    ──────┼────────
     'a'  │   10
     'b'  │   20
     'c'  │   30
     'd'  │   40
     'e'  │   50
3.2 Creating a Series
From a List
Python

import pandas as pd

# Simple Series from list
s = pd.Series([10, 20, 30, 40, 50])
print("Series from list:")
print(s)
print()

# Output:
# 0    10
# 1    20
# 2    30
# 3    40
# 4    50
# dtype: int64
With Custom Index
Python

import pandas as pd

# Series with custom index
s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
print("Series with custom index:")
print(s)
print()

# Output:
# a    10
# b    20
# c    30
# d    40
# e    50
# dtype: int64
From a Dictionary
Python

import pandas as pd

# Series from dictionary (keys become index)
data = {'apple': 100, 'banana': 200, 'cherry': 150, 'date': 50}
s = pd.Series(data)
print("Series from dictionary:")
print(s)

# Output:
# apple     100
# banana    200
# cherry    150
# date       50
# dtype: int64
From a NumPy Array
Python

import pandas as pd
import numpy as np

# Series from NumPy array
arr = np.array([1.1, 2.2, 3.3, 4.4])
s = pd.Series(arr, index=['w', 'x', 'y', 'z'])
print("Series from NumPy array:")
print(s)

# Output:
# w    1.1
# x    2.2
# y    3.3
# z    4.4
# dtype: float64
Scalar Value (Repeated)
Python

import pandas as pd

# Series from scalar (repeated for each index)
s = pd.Series(5, index=['a', 'b', 'c', 'd'])
print("Series from scalar:")
print(s)

# Output:
# a    5
# b    5
# c    5
# d    5
# dtype: int64
3.3 Series Attributes
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], 
              index=['a', 'b', 'c', 'd', 'e'],
              name='My Numbers')

print("Series:")
print(s)
print()

# Attributes
print("="*40)
print("SERIES ATTRIBUTES")
print("="*40)
print(f"values:     {s.values}")          # NumPy array of values
print(f"index:      {s.index.tolist()}")  # Index labels
print(f"dtype:      {s.dtype}")           # Data type
print(f"name:       {s.name}")            # Series name
print(f"size:       {s.size}")            # Number of elements
print(f"shape:      {s.shape}")           # Tuple of dimensions
print(f"nbytes:     {s.nbytes}")          # Memory usage
print(f"is_unique:  {s.is_unique}")       # Are all values unique?
print(f"hasnans:    {s.hasnans}")         # Contains NaN?
3.4 Accessing Series Elements
By Position (iloc)
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# Access by position
print("First element (position 0):", s.iloc[0])      # 10
print("Last element (position -1):", s.iloc[-1])     # 50
print("Elements 1-3:", s.iloc[1:4].tolist())         # [20, 30, 40]
By Label (loc)
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# Access by label
print("Element at 'a':", s.loc['a'])                 # 10
print("Element at 'c':", s.loc['c'])                 # 30
print("Elements 'a' to 'c':", s.loc['a':'c'].tolist())  # [10, 20, 30]

# Direct access (works for labels)
print("Direct access s['b']:", s['b'])               # 20
Multiple Elements
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# Access multiple elements
print("Elements at 'a', 'c', 'e':")
print(s[['a', 'c', 'e']])

# Output:
# a    10
# c    30
# e    50
# dtype: int64
3.5 Series Operations
Arithmetic Operations
Python

import pandas as pd

s1 = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
s2 = pd.Series([1, 2, 3], index=['a', 'b', 'c'])

print("s1:")
print(s1)
print("\ns2:")
print(s2)

# Element-wise operations
print("\ns1 + s2:")
print(s1 + s2)

print("\ns1 - s2:")
print(s1 - s2)

print("\ns1 * s2:")
print(s1 * s2)

print("\ns1 / s2:")
print(s1 / s2)

# Scalar operations
print("\ns1 + 100:")
print(s1 + 100)

print("\ns1 * 2:")
print(s1 * 2)
Operations with Different Indices (Alignment)
Python

import pandas as pd

s1 = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
s2 = pd.Series([1, 2, 3], index=['b', 'c', 'd'])

print("s1:", s1.tolist(), "index:", s1.index.tolist())
print("s2:", s2.tolist(), "index:", s2.index.tolist())

# Pandas aligns by index!
result = s1 + s2
print("\ns1 + s2 (aligned by index):")
print(result)

# Output:
# a     NaN    # 'a' only in s1
# b    21.0    # 20 + 1
# c    32.0    # 30 + 2
# d     NaN    # 'd' only in s2
# dtype: float64
Statistical Operations
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50, 15, 25, 35])

print("Series:", s.tolist())
print()
print("="*30)
print("STATISTICAL OPERATIONS")
print("="*30)
print(f"sum():      {s.sum()}")
print(f"mean():     {s.mean()}")
print(f"median():   {s.median()}")
print(f"std():      {s.std():.2f}")
print(f"var():      {s.var():.2f}")
print(f"min():      {s.min()}")
print(f"max():      {s.max()}")
print(f"count():    {s.count()}")
print(f"quantile(0.25): {s.quantile(0.25)}")
print(f"quantile(0.75): {s.quantile(0.75)}")

# All at once
print("\ndescribe():")
print(s.describe())
Boolean Operations
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# Comparison (returns boolean Series)
print("s > 25:")
print(s > 25)

# Filtering with boolean
print("\nValues greater than 25:")
print(s[s > 25])

# Multiple conditions
print("\nValues between 20 and 40 (inclusive):")
print(s[(s >= 20) & (s <= 40)])

# Using isin
print("\nValues in [10, 30, 50]:")
print(s[s.isin([10, 30, 50])])
3.6 Series Methods
Python

import pandas as pd
import numpy as np

s = pd.Series([3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5])

print("Original Series:", s.tolist())
print()

# Sorting
print("sorted (values):", s.sort_values().tolist())
print("sorted (index):", s.sort_index().tolist())

# Unique values
print("\nunique values:", s.unique())
print("number of unique:", s.nunique())

# Value counts
print("\nvalue_counts():")
print(s.value_counts())

# Ranking
print("\nrank():", s.rank().tolist())

# Cumulative operations
print("\ncumsum():", s.cumsum().tolist())
print("cumprod():", s.cumprod().tolist())
print("cummax():", s.cummax().tolist())

# Shifting
print("\nshift(1):", s.shift(1).tolist())  # Shift down
print("shift(-1):", s.shift(-1).tolist())  # Shift up

# Percentage change
print("\npct_change():", s.pct_change().round(2).tolist())
3.7 Modifying a Series
Python

import pandas as pd

s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# Modify single value
s['a'] = 100
print("After s['a'] = 100:")
print(s)

# Modify multiple values
s[['b', 'c']] = [200, 300]
print("\nAfter s[['b', 'c']] = [200, 300]:")
print(s)

# Add new element
s['f'] = 600
print("\nAfter adding s['f'] = 600:")
print(s)

# Delete element
del s['f']
print("\nAfter deleting 'f':")
print(s)

# Replace values
s = s.replace(100, 1000)
print("\nAfter replacing 100 with 1000:")
print(s)
3.8 Series Summary
Operation	Method/Syntax	Example
Create	pd.Series(data)	pd.Series([1,2,3])
Access by position	s.iloc[0]	First element
Access by label	s.loc['a']	Element at 'a'
Slice	s[1:4] or s['a':'c']	Range of elements
Statistics	s.mean(), s.sum()	Aggregate values
Filter	s[s > 5]	Boolean indexing
Sort	s.sort_values()	Sort by values
Unique	s.unique()	Unique values
Count	s.value_counts()	Frequency count
Apply function	s.apply(func)	Apply to each element
Chapter 4: DataFrame - The Heart of Pandas
4.1 What is a DataFrame?
A DataFrame is a two-dimensional, size-mutable, tabular data structure with labeled axes (rows and columns).

Think of it as:

A spreadsheet or Excel table
A SQL table
A dictionary of Series objects
text

Visual Representation:

              Column A   Column B   Column C
              ────────   ────────   ────────
    Index 0  │   10    │  'apple' │   1.5   │
    Index 1  │   20    │  'banana'│   2.5   │
    Index 2  │   30    │  'cherry'│   3.5   │
    Index 3  │   40    │  'date'  │   4.5   │
              ────────   ────────   ────────
              
    - Each COLUMN is a Series
    - Each ROW is also accessible as a Series
    - Columns can have DIFFERENT data types
4.2 Creating a DataFrame
From a Dictionary (Most Common)
Python

import pandas as pd

# Dictionary where keys become column names
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'City': ['New York', 'Paris', 'London', 'Tokyo'],
    'Salary': [50000, 60000, 70000, 55000]
}

df = pd.DataFrame(data)
print("DataFrame from dictionary:")
print(df)
Output:

text

      Name  Age      City  Salary
0    Alice   25  New York   50000
1      Bob   30     Paris   60000
2  Charlie   35    London   70000
3    Diana   28     Tokyo   55000
From a List of Dictionaries
Python

import pandas as pd

# Each dictionary is a row
data = [
    {'Name': 'Alice', 'Age': 25, 'City': 'New York'},
    {'Name': 'Bob', 'Age': 30, 'City': 'Paris'},
    {'Name': 'Charlie', 'Age': 35, 'City': 'London'},
    {'Name': 'Diana', 'Age': 28}  # Missing 'City' becomes NaN
]

df = pd.DataFrame(data)
print("DataFrame from list of dicts:")
print(df)
From a List of Lists
Python

import pandas as pd

# Each inner list is a row
data = [
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'Paris'],
    ['Charlie', 35, 'London'],
    ['Diana', 28, 'Tokyo']
]

df = pd.DataFrame(data, columns=['Name', 'Age', 'City'])
print("DataFrame from list of lists:")
print(df)
From NumPy Array
Python

import pandas as pd
import numpy as np

# 2D NumPy array
arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

df = pd.DataFrame(arr, 
                  columns=['A', 'B', 'C'],
                  index=['row1', 'row2', 'row3'])
print("DataFrame from NumPy array:")
print(df)
With Custom Index
Python

import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
}

df = pd.DataFrame(data, index=['emp1', 'emp2', 'emp3'])
print("DataFrame with custom index:")
print(df)

# Output:
#        Name  Age
# emp1  Alice   25
# emp2    Bob   30
# emp3  Charlie 35
4.3 DataFrame Attributes
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'Salary': [50000.0, 60000.0, 70000.0, 55000.0],
    'Active': [True, True, False, True]
})

print("DataFrame:")
print(df)
print()

print("="*50)
print("DATAFRAME ATTRIBUTES")
print("="*50)

print(f"shape:       {df.shape}")           # (rows, columns)
print(f"size:        {df.size}")            # Total elements
print(f"ndim:        {df.ndim}")            # Number of dimensions
print(f"columns:     {df.columns.tolist()}") # Column names
print(f"index:       {df.index.tolist()}")   # Row indices
print(f"dtypes:\n{df.dtypes}")              # Data type of each column
print(f"\nvalues (numpy array):\n{df.values}")
print(f"\nT (transpose):\n{df.T}")
print(f"\nempty:       {df.empty}")         # Is DataFrame empty?
4.4 Viewing DataFrame Data
Python

import pandas as pd
import numpy as np

# Create a larger DataFrame
np.random.seed(42)
df = pd.DataFrame({
    'A': np.random.randint(1, 100, 20),
    'B': np.random.random(20).round(2),
    'C': np.random.choice(['X', 'Y', 'Z'], 20),
    'D': pd.date_range('2024-01-01', periods=20)
})

print("Full DataFrame shape:", df.shape)
print()

# First N rows
print("head() - First 5 rows:")
print(df.head())
print()

# Last N rows
print("tail(3) - Last 3 rows:")
print(df.tail(3))
print()

# Random sample
print("sample(3) - Random 3 rows:")
print(df.sample(3))
print()

# Info about DataFrame
print("info():")
df.info()
print()

# Statistical summary
print("describe():")
print(df.describe())
print()

# Memory usage
print("memory_usage():")
print(df.memory_usage(deep=True))
4.5 Accessing Columns
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# Single column (returns Series)
print("Single column using df['Name']:")
print(df['Name'])
print(type(df['Name']))  # <class 'pandas.core.series.Series'>
print()

# Single column using dot notation
print("Using df.Age:")
print(df.Age)
print()

# Multiple columns (returns DataFrame)
print("Multiple columns df[['Name', 'Salary']]:")
print(df[['Name', 'Salary']])
print(type(df[['Name', 'Salary']]))  # <class 'pandas.core.frame.DataFrame'>
When to use dot notation vs bracket notation:

Situation	Use	Example
Column name has spaces	Bracket	df['First Name']
Column name is a Python keyword	Bracket	df['class']
Column name conflicts with method	Bracket	df['count']
Creating new column	Bracket	df['new_col'] = values
Simple column access	Either	df.Age or df['Age']
4.6 Accessing Rows
Using loc (Label-Based)
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}, index=['a', 'b', 'c'])

print("DataFrame:")
print(df)
print()

# Single row by label
print("df.loc['a'] (row with label 'a'):")
print(df.loc['a'])
print()

# Multiple rows by label
print("df.loc[['a', 'c']]:")
print(df.loc[['a', 'c']])
print()

# Row range by label (inclusive on both ends!)
print("df.loc['a':'b']:")
print(df.loc['a':'b'])
Using iloc (Position-Based)
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}, index=['a', 'b', 'c'])

print("DataFrame:")
print(df)
print()

# Single row by position
print("df.iloc[0] (first row):")
print(df.iloc[0])
print()

# Multiple rows by position
print("df.iloc[[0, 2]]:")
print(df.iloc[[0, 2]])
print()

# Row range by position (exclusive on end!)
print("df.iloc[0:2]:")
print(df.iloc[0:2])
print()

# Last row
print("df.iloc[-1]:")
print(df.iloc[-1])
loc vs iloc - Key Differences
text

┌──────────────────────────────────────────────────────────────────┐
│                    loc vs iloc COMPARISON                         │
├────────────────────────────┬─────────────────────────────────────┤
│           loc              │             iloc                     │
├────────────────────────────┼─────────────────────────────────────┤
│  Label-based               │  Position-based (integer)           │
│  df.loc['a']               │  df.iloc[0]                         │
│  Includes both endpoints   │  Excludes end (like Python)         │
│  df.loc['a':'c'] → a,b,c   │  df.iloc[0:2] → 0,1                 │
│  Use with string indices   │  Use with integer positions         │
└────────────────────────────┴─────────────────────────────────────┘
4.7 Accessing Specific Cells
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}, index=['a', 'b', 'c'])

print("DataFrame:")
print(df)
print()

# Using loc[row, column]
print("df.loc['a', 'Name']:", df.loc['a', 'Name'])
print("df.loc['b', 'Salary']:", df.loc['b', 'Salary'])

# Using iloc[row, column]
print("df.iloc[0, 0]:", df.iloc[0, 0])
print("df.iloc[1, 2]:", df.iloc[1, 2])

# Using at (faster for single value with label)
print("df.at['a', 'Name']:", df.at['a', 'Name'])

# Using iat (faster for single value with position)
print("df.iat[0, 0]:", df.iat[0, 0])
4.8 Selecting Rows and Columns Together
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'City': ['New York', 'Paris', 'London', 'Tokyo'],
    'Salary': [50000, 60000, 70000, 55000]
})

print("DataFrame:")
print(df)
print()

# Select specific rows and columns with loc
print("df.loc[0:2, ['Name', 'Age']]:")
print(df.loc[0:2, ['Name', 'Age']])
print()

# Select specific rows and columns with iloc
print("df.iloc[0:2, 0:2]:")
print(df.iloc[0:2, 0:2])
print()

# Mix: All rows, specific columns
print("df.loc[:, ['Name', 'Salary']]:")
print(df.loc[:, ['Name', 'Salary']])
print()

# Mix: Specific rows, all columns
print("df.iloc[1:3, :]:")
print(df.iloc[1:3, :])
4.9 Adding and Modifying Columns
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

print("Original DataFrame:")
print(df)
print()

# Add new column (scalar value)
df['Country'] = 'USA'
print("After adding 'Country' column:")
print(df)
print()

# Add new column (list of values)
df['Bonus'] = [5000, 6000, 7000]
print("After adding 'Bonus' column:")
print(df)
print()

# Add calculated column
df['Total'] = df['Salary'] + df['Bonus']
print("After adding 'Total' column:")
print(df)
print()

# Modify existing column
df['Age'] = df['Age'] + 1
print("After incrementing 'Age':")
print(df)
print()

# Using assign() to add columns (returns new DataFrame)
df2 = df.assign(
    Tax=df['Total'] * 0.2,
    Net=lambda x: x['Total'] - x['Total'] * 0.2
)
print("Using assign():")
print(df2)
4.10 Adding and Modifying Rows
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30],
    'Salary': [50000, 60000]
})

print("Original DataFrame:")
print(df)
print()

# Add single row using loc
df.loc[2] = ['Charlie', 35, 70000]
print("After adding row with loc:")
print(df)
print()

# Add row using concat (preferred for adding multiple rows)
new_row = pd.DataFrame({
    'Name': ['Diana'],
    'Age': [28],
    'Salary': [55000]
})
df = pd.concat([df, new_row], ignore_index=True)
print("After concat:")
print(df)
print()

# Modify existing row
df.loc[0] = ['Alice Smith', 26, 52000]
print("After modifying first row:")
print(df)
4.11 Deleting Columns and Rows
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'City': ['New York', 'Paris', 'London', 'Tokyo'],
    'Salary': [50000, 60000, 70000, 55000]
})

print("Original DataFrame:")
print(df)
print()

# Delete column using drop (returns new DataFrame)
df_no_city = df.drop(columns=['City'])
print("After dropping 'City' column:")
print(df_no_city)
print()

# Delete multiple columns
df_minimal = df.drop(columns=['City', 'Salary'])
print("After dropping 'City' and 'Salary':")
print(df_minimal)
print()

# Delete column using del (modifies in place)
df_copy = df.copy()
del df_copy['City']
print("After del df['City']:")
print(df_copy)
print()

# Delete rows using drop
df_no_row = df.drop(index=[0, 2])
print("After dropping rows 0 and 2:")
print(df_no_row)
print()

# Delete in place
df_inplace = df.copy()
df_inplace.drop(columns=['City'], inplace=True)
print("After inplace drop:")
print(df_inplace)
4.12 DataFrame Summary Table
Operation	Syntax	Returns
Create	pd.DataFrame(data)	DataFrame
View first rows	df.head(n)	DataFrame
View last rows	df.tail(n)	DataFrame
Shape	df.shape	Tuple (rows, cols)
Column names	df.columns	Index object
Data types	df.dtypes	Series
Info	df.info()	Prints info
Statistics	df.describe()	DataFrame
Single column	df['col']	Series
Multiple columns	df[['col1', 'col2']]	DataFrame
Row by label	df.loc[label]	Series
Row by position	df.iloc[pos]	Series
Cell value	df.loc[row, col]	Scalar
Add column	df['new'] = values	None (modifies df)
Drop column	df.drop(columns=['col'])	DataFrame
Drop row	df.drop(index=[idx])	DataFrame
Chapter 5: Data Input/Output - Loading and Saving Data
5.1 Overview of Data Formats
text

┌──────────────────────────────────────────────────────────────────┐
│                    DATA FORMATS IN PANDAS                         │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│   TEXT-BASED                     BINARY                          │
│   ──────────                     ──────                          │
│   • CSV (.csv)                   • Excel (.xlsx, .xls)           │
│   • JSON (.json)                 • Parquet (.parquet)            │
│   • HTML (.html)                 • Pickle (.pkl)                 │
│   • Fixed-width                  • HDF5 (.h5)                    │
│                                  • Feather (.feather)            │
│                                                                   │
│   DATABASE                       CLOUD/API                        │
│   ────────                       ─────────                        │
│   • SQL databases                • Google BigQuery               │
│   • SQLite                       • AWS S3                        │
│   • PostgreSQL                   • REST APIs                     │
│   • MySQL                                                        │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
5.2 Reading CSV Files
Basic CSV Reading
Python

import pandas as pd

# Basic read
df = pd.read_csv('data.csv')

# Preview the data
print(df.head())
CSV with Various Options
Python

import pandas as pd

# Most common options
df = pd.read_csv(
    'data.csv',
    
    # Column options
    header=0,                    # Row number for header (0 = first row)
    names=['A', 'B', 'C'],       # Custom column names
    usecols=['A', 'C'],          # Read only specific columns
    
    # Index options
    index_col='id',              # Use a column as index
    
    # Data type options
    dtype={'A': int, 'B': str},  # Specify dtypes
    parse_dates=['date_col'],    # Parse as datetime
    
    # Missing values
    na_values=['NA', 'N/A', ''], # Values to treat as NaN
    keep_default_na=True,        # Keep default NaN values
    
    # Performance options
    nrows=1000,                  # Read only first N rows
    skiprows=[1, 2],             # Skip specific rows
    skipfooter=5,                # Skip last N rows
    
    # Format options
    sep=',',                     # Delimiter (comma is default)
    encoding='utf-8',            # File encoding
    decimal='.',                 # Decimal character
    thousands=',',               # Thousands separator
    
    # Memory options
    low_memory=False,            # Load entire file at once
    memory_map=True,             # Map file into memory
)
Practical Examples
Python

import pandas as pd
from io import StringIO

# Example 1: Simple CSV
csv_data = """Name,Age,Salary
Alice,25,50000
Bob,30,60000
Charlie,35,70000"""

df = pd.read_csv(StringIO(csv_data))
print("Example 1 - Basic CSV:")
print(df)
print()

# Example 2: CSV with different separator
tsv_data = """Name\tAge\tSalary
Alice\t25\t50000
Bob\t30\t60000"""

df = pd.read_csv(StringIO(tsv_data), sep='\t')
print("Example 2 - Tab-separated:")
print(df)
print()

# Example 3: CSV with missing values
csv_missing = """Name,Age,Salary
Alice,25,50000
Bob,NA,60000
Charlie,35,"""

df = pd.read_csv(StringIO(csv_missing), na_values=['NA', ''])
print("Example 3 - Missing values:")
print(df)
print()

# Example 4: CSV with custom column names
csv_no_header = """Alice,25,50000
Bob,30,60000"""

df = pd.read_csv(StringIO(csv_no_header), 
                 header=None, 
                 names=['Name', 'Age', 'Salary'])
print("Example 4 - Custom headers:")
print(df)
5.3 Writing CSV Files
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# Basic write
df.to_csv('output.csv')

# Common options
df.to_csv(
    'output.csv',
    index=False,           # Don't write index
    columns=['Name', 'Age'],  # Write only specific columns
    header=True,           # Include header row
    sep=',',               # Delimiter
    encoding='utf-8',      # Encoding
    na_rep='NULL',         # Represent NaN as this
    float_format='%.2f',   # Format for floats
    date_format='%Y-%m-%d' # Format for dates
)

print("File saved successfully!")
5.4 Reading Excel Files
Python

import pandas as pd

# Basic read (requires openpyxl or xlrd)
df = pd.read_excel('data.xlsx')

# With options
df = pd.read_excel(
    'data.xlsx',
    sheet_name='Sheet1',     # Specific sheet (name or index)
    header=0,                # Header row
    index_col=0,             # Index column
    usecols='A:D',           # Columns to read
    skiprows=2,              # Skip first N rows
    nrows=100,               # Read only N rows
    dtype={'col1': str},     # Data types
    na_values=['NA'],        # Missing value markers
)

# Read multiple sheets
all_sheets = pd.read_excel('data.xlsx', sheet_name=None)
# Returns dict: {'Sheet1': df1, 'Sheet2': df2, ...}

# Read specific sheets
sheets = pd.read_excel('data.xlsx', sheet_name=['Sheet1', 'Sheet3'])
5.5 Writing Excel Files
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# Basic write
df.to_excel('output.xlsx', index=False)

# With options
df.to_excel(
    'output.xlsx',
    sheet_name='Employees',
    index=False,
    startrow=2,              # Start writing from row 2
    startcol=1,              # Start writing from column B
)

# Write multiple sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df.to_excel(writer, sheet_name='Employees', index=False)
    df.describe().to_excel(writer, sheet_name='Summary')
    
print("Excel file saved!")
5.6 Reading JSON Files
Python

import pandas as pd
from io import StringIO

# Different JSON structures

# Structure 1: Records (list of dicts)
json_records = '''[
    {"Name": "Alice", "Age": 25},
    {"Name": "Bob", "Age": 30}
]'''
df = pd.read_json(StringIO(json_records))
print("Records format:")
print(df)
print()

# Structure 2: Columns (dict of lists)
json_columns = '''{
    "Name": ["Alice", "Bob"],
    "Age": [25, 30]
}'''
df = pd.read_json(StringIO(json_columns))
print("Columns format:")
print(df)
print()

# Structure 3: Index (nested dict)
json_index = '''{
    "0": {"Name": "Alice", "Age": 25},
    "1": {"Name": "Bob", "Age": 30}
}'''
df = pd.read_json(StringIO(json_index), orient='index')
print("Index format:")
print(df)
5.7 Writing JSON Files
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30]
})

# Different orientations
print("records:", df.to_json(orient='records'))
print("columns:", df.to_json(orient='columns'))
print("index:", df.to_json(orient='index'))
print("values:", df.to_json(orient='values'))
print("table:", df.to_json(orient='table'))

# Write to file
df.to_json('output.json', orient='records', indent=2)
5.8 Reading from SQL Databases
Python

import pandas as pd
import sqlite3

# Create a sample SQLite database
conn = sqlite3.connect(':memory:')  # In-memory database

# Create sample data
df = pd.DataFrame({
    'id': [1, 2, 3],
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35]
})
df.to_sql('employees', conn, index=False)

# Read entire table
df_from_sql = pd.read_sql('SELECT * FROM employees', conn)
print("From SQL (entire table):")
print(df_from_sql)
print()

# Read with WHERE clause
df_filtered = pd.read_sql(
    "SELECT * FROM employees WHERE age > 25",
    conn
)
print("From SQL (filtered):")
print(df_filtered)
print()

# Read with parameters
df_param = pd.read_sql(
    "SELECT * FROM employees WHERE name = ?",
    conn,
    params=['Bob']
)
print("From SQL (with params):")
print(df_param)

conn.close()
5.9 Writing to SQL Databases
Python

import pandas as pd
import sqlite3

df = pd.DataFrame({
    'name': ['Diana', 'Eve'],
    'age': [28, 32],
    'salary': [55000, 65000]
})

conn = sqlite3.connect('company.db')

# Write to SQL
df.to_sql(
    'employees',           # Table name
    conn,
    if_exists='replace',   # 'fail', 'replace', 'append'
    index=False,           # Don't write index as column
    dtype={                # Specify SQL dtypes
        'name': 'TEXT',
        'age': 'INTEGER',
        'salary': 'REAL'
    }
)

# Verify
result = pd.read_sql('SELECT * FROM employees', conn)
print("Data in SQL table:")
print(result)

conn.close()
5.10 Reading Parquet Files (Fast Binary Format)
Python

import pandas as pd

# Parquet is fast and efficient for large datasets
# Requires: pip install pyarrow or pip install fastparquet

# Read parquet
df = pd.read_parquet('data.parquet')

# Read specific columns (very efficient with parquet)
df = pd.read_parquet('data.parquet', columns=['col1', 'col2'])

# Write parquet
df.to_parquet('output.parquet', index=False)

# With compression
df.to_parquet('output.parquet', compression='snappy')  # or 'gzip', 'brotli'
5.11 Reading from URLs
Python

import pandas as pd

# Read CSV from URL
url = 'https://raw.githubusercontent.com/datasets/covid-19/main/data/countries-aggregated.csv'
df = pd.read_csv(url)
print("Data from URL:")
print(df.head())

# Read JSON from URL
json_url = 'https://api.example.com/data.json'
# df = pd.read_json(json_url)

# Read Excel from URL
excel_url = 'https://example.com/data.xlsx'
# df = pd.read_excel(excel_url)
5.12 Clipboard Operations
Python

import pandas as pd

# Read from clipboard (copy data from Excel/website first)
# df = pd.read_clipboard()

# Write to clipboard
df = pd.DataFrame({'A': [1, 2, 3], 'B': ['x', 'y', 'z']})
# df.to_clipboard(index=False)  # Now paste into Excel!
5.13 Reading HTML Tables
Python

import pandas as pd

# Read all tables from HTML (requires lxml)
html_content = """
<html>
<body>
<table>
    <tr><th>Name</th><th>Age</th></tr>
    <tr><td>Alice</td><td>25</td></tr>
    <tr><td>Bob</td><td>30</td></tr>
</table>
</body>
</html>
"""

tables = pd.read_html(html_content)
print("First table from HTML:")
print(tables[0])

# Read tables from URL
# tables = pd.read_html('https://en.wikipedia.org/wiki/List_of_countries_by_GDP')
5.14 File I/O Summary
Format	Read	Write	Best For
CSV	read_csv()	to_csv()	Universal compatibility
Excel	read_excel()	to_excel()	Business users
JSON	read_json()	to_json()	Web APIs
SQL	read_sql()	to_sql()	Databases
Parquet	read_parquet()	to_parquet()	Big data, ML
Pickle	read_pickle()	to_pickle()	Python-only, fastest
HTML	read_html()	to_html()	Web scraping
Clipboard	read_clipboard()	to_clipboard()	Quick data transfer
Chapter 6: Data Selection and Indexing
6.1 Overview of Selection Methods
text

┌─────────────────────────────────────────────────────────────────────┐
│                    PANDAS SELECTION METHODS                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   []           → Basic selection (columns or row slices)            │
│   .loc[]       → Label-based selection (rows and columns)           │
│   .iloc[]      → Position-based selection (integer indices)         │
│   .at[]        → Fast single label-based value access               │
│   .iat[]       → Fast single position-based value access            │
│                                                                      │
├─────────────────────────────────────────────────────────────────────┤
│                         WHEN TO USE WHAT                             │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   Selecting columns:        df['col'] or df[['col1', 'col2']]       │
│   Selecting rows by label:  df.loc['label']                         │
│   Selecting rows by index:  df.iloc[0]                              │
│   Selecting cell by label:  df.loc['row', 'col'] or df.at[r, c]     │
│   Selecting cell by index:  df.iloc[0, 0] or df.iat[0, 0]           │
│   Boolean filtering:        df[df['col'] > value]                   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
6.2 Sample DataFrame for Examples
Python

import pandas as pd
import numpy as np

# Create a comprehensive sample DataFrame
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales'],
    'Salary': [50000, 80000, 90000, 55000, 60000],
    'Years': [2, 5, 8, 3, 4],
    'Rating': [4.5, 4.8, 4.2, 4.9, 4.6]
}, index=['emp1', 'emp2', 'emp3', 'emp4', 'emp5'])

print("Sample DataFrame:")
print(df)
print()
6.3 Basic Selection with []
Selecting Columns
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# Single column → Returns Series
print("df['Name'] (returns Series):")
print(df['Name'])
print(f"Type: {type(df['Name'])}")
print()

# Multiple columns → Returns DataFrame
print("df[['Name', 'Age']] (returns DataFrame):")
print(df[['Name', 'Age']])
print(f"Type: {type(df[['Name', 'Age']])}")
Selecting Rows by Slicing
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32]
})

# Row slicing with []
print("df[0:2] (first 2 rows):")
print(df[0:2])
print()

print("df[2:4] (rows 2 and 3):")
print(df[2:4])
print()

print("df[::2] (every other row):")
print(df[::2])
6.4 Label-Based Selection with .loc[]
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 60000, 70000, 55000, 65000]
}, index=['a', 'b', 'c', 'd', 'e'])

print("DataFrame with string index:")
print(df)
print()

# Single row
print("df.loc['a'] (single row):")
print(df.loc['a'])
print()

# Multiple rows
print("df.loc[['a', 'c', 'e']] (multiple rows):")
print(df.loc[['a', 'c', 'e']])
print()

# Row range (INCLUSIVE on both ends!)
print("df.loc['a':'c'] (row range - inclusive):")
print(df.loc['a':'c'])
print()

# Single cell
print("df.loc['a', 'Name']:", df.loc['a', 'Name'])

# Specific rows and columns
print("\ndf.loc[['a', 'b'], ['Name', 'Age']]:")
print(df.loc[['a', 'b'], ['Name', 'Age']])

# Row range and column range
print("\ndf.loc['a':'c', 'Name':'Age']:")
print(df.loc['a':'c', 'Name':'Age'])

# All rows, specific columns
print("\ndf.loc[:, ['Name', 'Salary']]:")
print(df.loc[:, ['Name', 'Salary']])
6.5 Position-Based Selection with .iloc[]
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 60000, 70000, 55000, 65000]
}, index=['a', 'b', 'c', 'd', 'e'])

print("DataFrame:")
print(df)
print()

# Single row by position
print("df.iloc[0] (first row):")
print(df.iloc[0])
print()

# Multiple rows by position
print("df.iloc[[0, 2, 4]] (rows 0, 2, 4):")
print(df.iloc[[0, 2, 4]])
print()

# Row range (EXCLUSIVE on end - like Python!)
print("df.iloc[0:3] (rows 0, 1, 2):")
print(df.iloc[0:3])
print()

# Negative indexing
print("df.iloc[-1] (last row):")
print(df.iloc[-1])
print()

print("df.iloc[-3:] (last 3 rows):")
print(df.iloc[-3:])
print()

# Single cell
print("df.iloc[0, 0]:", df.iloc[0, 0])

# Specific rows and columns
print("\ndf.iloc[[0, 1], [0, 2]]:")
print(df.iloc[[0, 1], [0, 2]])

# Row range and column range
print("\ndf.iloc[0:3, 0:2]:")
print(df.iloc[0:3, 0:2])

# Step slicing
print("\ndf.iloc[::2, :] (every other row):")
print(df.iloc[::2, :])
6.6 Fast Scalar Access with .at[] and .iat[]
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}, index=['a', 'b', 'c'])

# .at[] - Label-based, single value (faster than loc for single values)
print("df.at['a', 'Name']:", df.at['a', 'Name'])
print("df.at['b', 'Salary']:", df.at['b', 'Salary'])

# .iat[] - Position-based, single value (faster than iloc for single values)
print("df.iat[0, 0]:", df.iat[0, 0])
print("df.iat[1, 2]:", df.iat[1, 2])

# Setting values
df.at['a', 'Age'] = 26
df.iat[0, 2] = 52000
print("\nAfter modifications:")
print(df)

# Performance comparison (at/iat are faster for single values)
# Use at/iat when accessing single cells in loops
6.7 Selection Summary Matrix
Python

import pandas as pd

df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9]
}, index=['x', 'y', 'z'])

print("DataFrame:")
print(df)
print()

print("="*60)
print("SELECTION SUMMARY")
print("="*60)

# Column selection
print("\n--- COLUMNS ---")
print(f"df['A']           → Series: {df['A'].tolist()}")
print(f"df[['A', 'B']]    → DataFrame")
print(f"df.A              → Series: {df.A.tolist()}")

# Row selection
print("\n--- ROWS ---")
print(f"df.loc['x']       → Series: {df.loc['x'].tolist()}")
print(f"df.loc[['x','y']] → DataFrame")
print(f"df.iloc[0]        → Series: {df.iloc[0].tolist()}")
print(f"df.iloc[[0,1]]    → DataFrame")
print(f"df[0:2]           → DataFrame (first 2 rows)")

# Cell selection
print("\n--- CELLS ---")
print(f"df.loc['x', 'A']  → {df.loc['x', 'A']}")
print(f"df.iloc[0, 0]     → {df.iloc[0, 0]}")
print(f"df.at['x', 'A']   → {df.at['x', 'A']} (fast)")
print(f"df.iat[0, 0]      → {df.iat[0, 0]} (fast)")

# Combined selection
print("\n--- COMBINED ---")
print(f"df.loc['x':'y', 'A':'B'] → Subframe (inclusive)")
print(f"df.iloc[0:2, 0:2]        → Subframe (exclusive end)")
6.8 Common Selection Patterns
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Dept': ['Sales', 'Eng', 'Eng', 'HR', 'Sales'],
    'Salary': [50000, 80000, 90000, 55000, 60000]
})

print("DataFrame:")
print(df)
print()

# Pattern 1: First/Last N rows
print("First 3 rows:", df.head(3).index.tolist())
print("Last 2 rows:", df.tail(2).index.tolist())

# Pattern 2: Random sample
print("Random 2 rows:", df.sample(2).index.tolist())

# Pattern 3: Rows where column meets condition
print("\nAge > 28:")
print(df.loc[df['Age'] > 28])

# Pattern 4: Specific value in column
print("\nDept == 'Eng':")
print(df.loc[df['Dept'] == 'Eng'])

# Pattern 5: Multiple conditions
print("\n(Age > 25) AND (Salary > 60000):")
print(df.loc[(df['Age'] > 25) & (df['Salary'] > 60000)])

# Pattern 6: Select columns by type
print("\nNumeric columns only:")
print(df.select_dtypes(include='number'))

# Pattern 7: Select columns by name pattern
print("\nColumns containing 'a':")
print(df[[col for col in df.columns if 'a' in col.lower()]])
Chapter 7: Data Filtering and Boolean Indexing
7.1 Understanding Boolean Indexing
Boolean indexing is one of the most powerful features in Pandas. It allows you to filter data based on conditions.

text

How Boolean Indexing Works:

Step 1: Create boolean condition
    df['Age'] > 30
    → Returns: [False, False, True, False, True]
    
Step 2: Use boolean series to filter
    df[df['Age'] > 30]
    → Returns only rows where condition is True
7.2 Single Condition Filtering
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 80000, 90000, 55000, 60000],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales']
})

print("Original DataFrame:")
print(df)
print()

# Comparison operators: >, <, >=, <=, ==, !=

# Greater than
print("Age > 30:")
print(df[df['Age'] > 30])
print()

# Less than or equal
print("Salary <= 60000:")
print(df[df['Salary'] <= 60000])
print()

# Equal to
print("Department == 'Engineering':")
print(df[df['Department'] == 'Engineering'])
print()

# Not equal to
print("Department != 'Sales':")
print(df[df['Department'] != 'Sales'])
7.3 Multiple Conditions
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 80000, 90000, 55000, 60000],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales']
})

# IMPORTANT: Use & (and), | (or), ~ (not)
# NOT: and, or, not (Python keywords don't work!)
# ALWAYS wrap each condition in parentheses!

# AND condition
print("(Age > 28) AND (Salary > 60000):")
print(df[(df['Age'] > 28) & (df['Salary'] > 60000)])
print()

# OR condition
print("(Department == 'Sales') OR (Department == 'HR'):")
print(df[(df['Department'] == 'Sales') | (df['Department'] == 'HR')])
print()

# NOT condition
print("NOT (Age > 30):")
print(df[~(df['Age'] > 30)])
print()

# Complex combinations
print("(Age > 25) AND ((Salary > 70000) OR (Department == 'HR')):")
print(df[(df['Age'] > 25) & ((df['Salary'] > 70000) | (df['Department'] == 'HR'))])
7.4 Using isin() for Multiple Values
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales'],
    'City': ['NYC', 'LA', 'NYC', 'Chicago', 'LA']
})

print("Original DataFrame:")
print(df)
print()

# Filter for multiple values in a column
print("Department in ['Sales', 'HR']:")
print(df[df['Department'].isin(['Sales', 'HR'])])
print()

# NOT in multiple values
print("Department NOT in ['Engineering']:")
print(df[~df['Department'].isin(['Engineering'])])
print()

# Multiple columns with isin
print("City in ['NYC', 'LA']:")
print(df[df['City'].isin(['NYC', 'LA'])])
7.5 Using between() for Ranges
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 80000, 90000, 55000, 60000]
})

print("Original DataFrame:")
print(df)
print()

# between() is inclusive on both ends by default
print("Age between 28 and 32 (inclusive):")
print(df[df['Age'].between(28, 32)])
print()

# Equivalent to:
print("Same using comparison operators:")
print(df[(df['Age'] >= 28) & (df['Age'] <= 32)])
print()

# between for salary
print("Salary between 55000 and 80000:")
print(df[df['Salary'].between(55000, 80000)])
7.6 String Filtering Methods
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice Smith', 'Bob Johnson', 'Charlie Brown', 'Diana Prince', 'Eve Wilson'],
    'Email': ['alice@gmail.com', 'bob@yahoo.com', 'charlie@gmail.com', 'diana@hotmail.com', 'eve@gmail.com'],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales']
})

print("Original DataFrame:")
print(df)
print()

# String contains
print("Name contains 'son':")
print(df[df['Name'].str.contains('son')])
print()

# String starts with
print("Email starts with 'a' or 'b':")
print(df[df['Email'].str.startswith(('a', 'b'))])
print()

# String ends with
print("Email ends with 'gmail.com':")
print(df[df['Email'].str.endswith('gmail.com')])
print()

# Case-insensitive contains
print("Name contains 'ALICE' (case insensitive):")
print(df[df['Name'].str.contains('ALICE', case=False)])
print()

# Regular expression matching
print("Name matches pattern (ends with vowel):")
print(df[df['Name'].str.match(r'.*[aeiouAEIOU]$', na=False)])
print()

# String length
print("Name length > 12:")
print(df[df['Name'].str.len() > 12])
7.7 Using query() for Readable Filtering
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Salary': [50000, 80000, 90000, 55000, 60000],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales']
})

print("Original DataFrame:")
print(df)
print()

# query() uses a string expression (more readable!)
print("query: Age > 30")
print(df.query('Age > 30'))
print()

print("query: Age > 28 and Salary > 60000")
print(df.query('Age > 28 and Salary > 60000'))
print()

print("query: Department == 'Engineering'")
print(df.query('Department == "Engineering"'))
print()

# Using variables with @
min_age = 28
max_salary = 70000
print(f"query: Age > {min_age} and Salary < {max_salary}")
print(df.query('Age > @min_age and Salary < @max_salary'))
print()

# Backticks for column names with spaces
df_spaces = df.rename(columns={'Department': 'Dept Name'})
print("query with backticks for spaces:")
print(df_spaces.query('`Dept Name` == "Sales"'))
7.8 Filtering with where() and mask()
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': [10, 20, 30, 40, 50]
})

print("Original DataFrame:")
print(df)
print()

# where() - Keep values where condition is True, replace others with NaN
print("where(df['A'] > 2) - Keep if A > 2, else NaN:")
print(df.where(df['A'] > 2))
print()

# where() with replacement value
print("where(df['A'] > 2, other=-1) - Keep if A > 2, else -1:")
print(df.where(df['A'] > 2, other=-1))
print()

# mask() - Opposite of where(): Replace values where condition is True
print("mask(df['A'] > 2) - Replace with NaN if A > 2:")
print(df.mask(df['A'] > 2))
print()

# mask() with replacement value
print("mask(df['A'] > 2, other=0) - Replace with 0 if A > 2:")
print(df.mask(df['A'] > 2, other=0))
7.9 Filtering Null Values
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', None, 'Diana', 'Eve'],
    'Age': [25, np.nan, 35, 28, np.nan],
    'Salary': [50000, 60000, 70000, np.nan, 60000]
})

print("DataFrame with null values:")
print(df)
print()

# Find rows with any null
print("Rows with ANY null value:")
print(df[df.isnull().any(axis=1)])
print()

# Find rows with all values present (no nulls)
print("Rows with NO null values:")
print(df[df.notnull().all(axis=1)])
print()

# Find rows where specific column is null
print("Rows where Age is null:")
print(df[df['Age'].isnull()])
print()

# Find rows where specific column is NOT null
print("Rows where Age is NOT null:")
print(df[df['Age'].notna()])
print()

# Count nulls per column
print("Null count per column:")
print(df.isnull().sum())
7.10 Filtering Summary
Method	Use Case	Example
df[condition]	Basic filtering	df[df['Age'] > 30]
&, |, ~	Multiple conditions	df[(A > 1) & (B < 5)]
isin()	Match multiple values	df[df['Col'].isin([1,2,3])]
between()	Range filtering	df[df['Col'].between(1,10)]
str.contains()	String matching	df[df['Name'].str.contains('A')]
query()	Readable syntax	df.query('Age > 30')
where()	Keep or replace	df.where(condition)
mask()	Opposite of where	df.mask(condition)
isnull()	Find missing	df[df['Col'].isnull()]
notna()	Find non-missing	df[df['Col'].notna()]
Chapter 8: Data Cleaning and Preprocessing
8.1 Overview of Data Cleaning
text

┌──────────────────────────────────────────────────────────────────┐
│                    DATA CLEANING TASKS                            │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  1. MISSING DATA           4. DUPLICATES                         │
│     • Find missing            • Find duplicates                  │
│     • Drop missing            • Remove duplicates                │
│     • Fill missing            • Keep first/last                  │
│                                                                   │
│  2. DATA TYPES             5. OUTLIERS                           │
│     • Check types             • Detect outliers                  │
│     • Convert types           • Handle outliers                  │
│     • Parse dates             • Cap/floor values                 │
│                                                                   │
│  3. TEXT CLEANING          6. INCONSISTENT DATA                  │
│     • Strip whitespace        • Standardize categories           │
│     • Change case             • Fix typos                        │
│     • Remove special chars    • Validate data                    │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
8.2 Checking Data Quality
Python

import pandas as pd
import numpy as np

# Create a messy DataFrame
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'bob', 'Charlie', None, 'Diana', 'Alice'],
    'Age': [25, 30, 30, np.nan, 28, 150, 25],  # 150 is outlier
    'Email': ['alice@mail.com', 'BOB@MAIL.COM', 'bob@mail.com', 
              'charlie@mail', None, 'diana@mail.com', 'alice@mail.com'],
    'Salary': ['50000', '60,000', '60000', '70000', '55000', '-5000', '50000'],
    'Join_Date': ['2020-01-15', '2019/06/20', 'Jan 5, 2021', 
                  '2018-12-01', '2022-03-10', '2017-08-15', '2020-01-15']
})

print("Messy DataFrame:")
print(df)
print()

# Data quality checks
print("="*60)
print("DATA QUALITY REPORT")
print("="*60)

print(f"\n1. Shape: {df.shape[0]} rows, {df.shape[1]} columns")

print(f"\n2. Data Types:")
print(df.dtypes)

print(f"\n3. Missing Values:")
print(df.isnull().sum())

print(f"\n4. Duplicate Rows: {df.duplicated().sum()}")

print(f"\n5. Unique Values per Column:")
for col in df.columns:
    print(f"   {col}: {df[col].nunique()} unique")

print(f"\n6. Sample Values:")
print(df.head(3))
8.3 Handling Duplicates
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob'],
    'Age': [25, 30, 25, 35, 30],
    'City': ['NYC', 'LA', 'NYC', 'Chicago', 'LA']
})

print("Original DataFrame:")
print(df)
print()

# Check for duplicates
print("Duplicated rows (boolean):")
print(df.duplicated())
print()

# Show duplicate rows
print("Show duplicate rows:")
print(df[df.duplicated(keep=False)])  # keep=False shows ALL duplicates
print()

# Check duplicates based on specific columns
print("Duplicated based on 'Name' only:")
print(df.duplicated(subset=['Name']))
print()

# Remove duplicates
print("After drop_duplicates():")
print(df.drop_duplicates())
print()

# Keep last occurrence instead of first
print("drop_duplicates(keep='last'):")
print(df.drop_duplicates(keep='last'))
print()

# Remove duplicates based on specific columns
print("drop_duplicates(subset=['Name']):")
print(df.drop_duplicates(subset=['Name']))
8.4 Changing Data Types
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'ID': ['1', '2', '3', '4', '5'],
    'Price': ['10.5', '20.3', '15.0', '25.7', '30.2'],
    'Quantity': [10, 20, 30, 40, 50],
    'Active': ['True', 'False', 'True', 'True', 'False'],
    'Date': ['2020-01-15', '2020-02-20', '2020-03-25', '2020-04-30', '2020-05-05']
})

print("Original DataFrame:")
print(df)
print("Original dtypes:")
print(df.dtypes)
print()

# Convert string to integer
df['ID'] = df['ID'].astype(int)

# Convert string to float
df['Price'] = df['Price'].astype(float)

# Convert string to boolean
df['Active'] = df['Active'].map({'True': True, 'False': False})

# Convert string to datetime
df['Date'] = pd.to_datetime(df['Date'])

print("After type conversion:")
print(df)
print("\nNew dtypes:")
print(df.dtypes)
Handling Type Conversion Errors
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Numbers': ['1', '2', 'three', '4', 'N/A', '6']
})

print("Original DataFrame:")
print(df)
print()

# This would raise an error:
# df['Numbers'].astype(int)

# Use pd.to_numeric with errors='coerce' (converts errors to NaN)
df['Numbers_converted'] = pd.to_numeric(df['Numbers'], errors='coerce')
print("After pd.to_numeric with errors='coerce':")
print(df)
print()

# errors='ignore' keeps original values
df['Numbers_ignored'] = pd.to_numeric(df['Numbers'], errors='ignore')
print("After pd.to_numeric with errors='ignore':")
print(df)
8.5 Renaming Columns
Python

import pandas as pd

df = pd.DataFrame({
    'First Name': ['Alice', 'Bob', 'Charlie'],
    'last_name': ['Smith', 'Jones', 'Brown'],
    'AGE': [25, 30, 35],
    'Annual Salary ($)': [50000, 60000, 70000]
})

print("Original DataFrame:")
print(df)
print()

# Rename specific columns using dict
df_renamed = df.rename(columns={
    'First Name': 'first_name',
    'last_name': 'last_name',  # already good
    'AGE': 'age',
    'Annual Salary ($)': 'annual_salary'
})
print("After rename():")
print(df_renamed)
print()

# Rename all columns using a function
df_lower = df.rename(columns=str.lower)
print("All columns to lowercase:")
print(df_lower)
print()

# Replace spaces with underscores
df_clean = df.rename(columns=lambda x: x.lower().replace(' ', '_').replace('($)', ''))
print("Clean column names:")
print(df_clean)
print()

# Set columns directly
df.columns = ['first_name', 'last_name', 'age', 'salary']
print("Set columns directly:")
print(df)
8.6 Cleaning Text Data
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['  Alice  ', 'BOB', 'charlie', '  Diana Smith  ', 'EVE'],
    'Email': ['ALICE@MAIL.COM', 'bob@mail.com', 'CHARLIE@Mail.Com', 
              'diana@mail.com', 'eve@MAIL.com'],
    'Phone': ['123-456-7890', '(234) 567-8901', '345.678.9012', 
              '456 789 0123', '5678901234']
})

print("Original DataFrame:")
print(df)
print()

# Strip whitespace
df['Name'] = df['Name'].str.strip()
print("After stripping whitespace:")
print(df['Name'].tolist())

# Convert to lowercase
df['Name'] = df['Name'].str.lower()
print("After lowercase:")
print(df['Name'].tolist())

# Convert to title case
df['Name'] = df['Name'].str.title()
print("After title case:")
print(df['Name'].tolist())

# Standardize email (lowercase)
df['Email'] = df['Email'].str.lower()
print("Email standardized:")
print(df['Email'].tolist())

# Clean phone numbers (keep only digits)
df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)
print("Phone numbers cleaned:")
print(df['Phone'].tolist())

print("\nFinal DataFrame:")
print(df)
8.7 Replacing Values
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Status': ['Active', 'active', 'ACTIVE', 'Inactive', 'inactive', 'Unknown'],
    'Score': [100, 200, 300, -999, 500, -999],  # -999 represents missing
    'Grade': ['A', 'B', 'C', 'D', 'F', 'X']  # X is invalid
})

print("Original DataFrame:")
print(df)
print()

# Replace single value
df['Status'] = df['Status'].replace('Unknown', 'Inactive')
print("After replacing 'Unknown' with 'Inactive':")
print(df['Status'].tolist())

# Replace multiple values with single value
df['Status'] = df['Status'].replace(['active', 'ACTIVE'], 'Active')
print("After standardizing 'Active':")
print(df['Status'].tolist())

# Replace using dictionary
df['Status'] = df['Status'].replace({
    'inactive': 'Inactive'
})
print("After dict replacement:")
print(df['Status'].tolist())

# Replace special values with NaN
df['Score'] = df['Score'].replace(-999, np.nan)
print("\nScore after replacing -999 with NaN:")
print(df['Score'].tolist())

# Replace in entire DataFrame
df = df.replace({'X': np.nan, -999: np.nan})
print("\nDataFrame after replacing X and -999 with NaN:")
print(df)
8.8 Handling Outliers
Python

import pandas as pd
import numpy as np

# Create data with outliers
np.random.seed(42)
df = pd.DataFrame({
    'Age': [25, 30, 35, 28, 150, 32, -5, 27, 29, 31],  # 150 and -5 are outliers
    'Salary': [50000, 60000, 70000, 55000, 1000000, 65000, 58000, 52000, 61000, 63000]
})

print("Original DataFrame:")
print(df)
print()

# Method 1: IQR method
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    return df[(df[column] >= lower_bound) & (df[column] <= upper_bound)]

df_clean = remove_outliers_iqr(df, 'Age')
print("After IQR outlier removal (Age):")
print(df_clean)
print()

# Method 2: Capping (Winsorization)
def cap_outliers(series, lower_percentile=0.05, upper_percentile=0.95):
    lower = series.quantile(lower_percentile)
    upper = series.quantile(upper_percentile)
    return series.clip(lower=lower, upper=upper)

df['Salary_capped'] = cap_outliers(df['Salary'])
print("Salary after capping at 5th and 95th percentile:")
print(df[['Salary', 'Salary_capped']])
print()

# Method 3: Z-score method
from scipy import stats

def remove_outliers_zscore(df, column, threshold=3):
    z_scores = np.abs(stats.zscore(df[column].dropna()))
    return df[z_scores < threshold]

# Method 4: Set valid range
df['Age_valid'] = df['Age'].clip(lower=0, upper=120)
print("Age after clipping to 0-120 range:")
print(df[['Age', 'Age_valid']])
8.9 Data Validation
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Email': ['alice@mail.com', 'invalid-email', 'bob@mail.com', '', 'charlie@mail'],
    'Age': [25, -5, 150, 30, 28],
    'Phone': ['1234567890', '123', 'abcdefghij', '9876543210', '5551234567'],
    'Status': ['Active', 'active', 'Inactive', 'Unknown', 'Active']
})

print("Original DataFrame:")
print(df)
print()

# Validate email (simple check for @)
df['Email_valid'] = df['Email'].str.contains('@', na=False)
print("Email validation:")
print(df[['Email', 'Email_valid']])
print()

# Validate age (reasonable range)
df['Age_valid'] = df['Age'].between(0, 120)
print("Age validation (0-120):")
print(df[['Age', 'Age_valid']])
print()

# Validate phone (10 digits)
df['Phone_valid'] = df['Phone'].str.match(r'^\d{10}$', na=False)
print("Phone validation (10 digits):")
print(df[['Phone', 'Phone_valid']])
print()

# Validate status (allowed values)
allowed_status = ['Active', 'Inactive']
df['Status_valid'] = df['Status'].isin(allowed_status)
print("Status validation:")
print(df[['Status', 'Status_valid']])
print()

# Summary of validation
print("Validation Summary:")
print(f"Valid emails: {df['Email_valid'].sum()}/{len(df)}")
print(f"Valid ages: {df['Age_valid'].sum()}/{len(df)}")
print(f"Valid phones: {df['Phone_valid'].sum()}/{len(df)}")
print(f"Valid status: {df['Status_valid'].sum()}/{len(df)}")
Chapter 9: Handling Missing Data
9.1 Understanding Missing Data in Pandas
text

┌──────────────────────────────────────────────────────────────────┐
│                    MISSING DATA IN PANDAS                         │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  Missing values are represented as:                               │
│  • np.nan (Not a Number) - for float data                        │
│  • None - Python's null object                                   │
│  • pd.NA - Pandas nullable integer/boolean NA                    │
│  • pd.NaT - Not a Time (for datetime)                            │
│                                                                   │
│  Why data is missing:                                             │
│  • Not collected (survey non-response)                           │
│  • Not applicable (N/A)                                          │
│  • Data corruption                                                │
│  • Join/merge mismatches                                         │
│                                                                   │
│  Strategies:                                                      │
│  • Detection - Find missing values                               │
│  • Removal - Drop rows/columns with missing                      │
│  • Imputation - Fill with meaningful values                      │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
9.2 Detecting Missing Values
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': [np.nan, 2, 3, np.nan, 5],
    'C': [1, 2, 3, 4, 5],
    'D': [np.nan, np.nan, np.nan, np.nan, np.nan]
})

print("DataFrame with missing values:")
print(df)
print()

# Check for missing values (returns boolean DataFrame)
print("isnull() - True where values are missing:")
print(df.isnull())
print()

# Equivalent: isna()
print("isna() - Same as isnull():")
print(df.isna())
print()

# Check for non-missing values
print("notna() - True where values are NOT missing:")
print(df.notna())
print()

# Count missing values per column
print("Missing count per column:")
print(df.isnull().sum())
print()

# Count missing values per row
print("Missing count per row:")
print(df.isnull().sum(axis=1))
print()

# Percentage of missing values
print("Percentage missing per column:")
print((df.isnull().sum() / len(df) * 100).round(2))
print()

# Total missing values in DataFrame
print(f"Total missing values: {df.isnull().sum().sum()}")

# Any missing in each column?
print("\nAny missing per column:")
print(df.isnull().any())

# Any missing in entire DataFrame?
print(f"\nAny missing in DataFrame: {df.isnull().any().any()}")
9.3 Missing Data Visualization (Conceptual)
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, np.nan, 6, 7, np.nan, 9, 10],
    'B': [np.nan, 2, 3, np.nan, 5, np.nan, 7, 8, np.nan, 10],
    'C': [1, np.nan, 3, 4, 5, 6, np.nan, 8, 9, np.nan],
    'D': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
})

# Create a missing data summary
def missing_data_summary(df):
    """Create a comprehensive missing data summary."""
    total = df.isnull().sum()
    percent = (df.isnull().sum() / len(df) * 100).round(2)
    
    missing_df = pd.DataFrame({
        'Total Missing': total,
        'Percent Missing': percent,
        'Data Type': df.dtypes
    })
    
    missing_df = missing_df[missing_df['Total Missing'] > 0]
    missing_df = missing_df.sort_values('Percent Missing', ascending=False)
    
    return missing_df

print("Missing Data Summary:")
print(missing_data_summary(df))
print()

# Visual representation using characters
def visualize_missing(df, max_rows=10):
    """Create a text-based visualization of missing data."""
    print("\nMissing Data Pattern (• = present, ○ = missing):")
    print("-" * (len(df.columns) * 4 + 10))
    print(f"{'Row':<6}", end="")
    for col in df.columns:
        print(f"{col:>4}", end="")
    print()
    print("-" * (len(df.columns) * 4 + 10))
    
    for idx in df.index[:max_rows]:
        print(f"{idx:<6}", end="")
        for col in df.columns:
            if pd.isna(df.loc[idx, col]):
                print("   ○", end="")
            else:
                print("   •", end="")
        print()

visualize_missing(df)
9.4 Removing Missing Data
Dropping Rows
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': [np.nan, 2, 3, np.nan, 5],
    'C': [1, 2, 3, 4, 5]
})

print("Original DataFrame:")
print(df)
print()

# Drop rows with ANY missing values
print("dropna() - Drop rows with any missing:")
print(df.dropna())
print()

# Drop rows where ALL values are missing
df_with_empty_row = df.copy()
df_with_empty_row.loc[5] = [np.nan, np.nan, np.nan]
print("DataFrame with empty row:")
print(df_with_empty_row)
print("\ndropna(how='all') - Drop only completely empty rows:")
print(df_with_empty_row.dropna(how='all'))
print()

# Drop rows with missing in specific columns
print("dropna(subset=['A']) - Drop if A is missing:")
print(df.dropna(subset=['A']))
print()

# Drop rows with at least N non-null values
print("dropna(thresh=2) - Keep rows with at least 2 non-null:")
print(df.dropna(thresh=2))
Dropping Columns
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': [np.nan, 2, np.nan, 4, np.nan],  # 60% missing
    'C': [np.nan, np.nan, np.nan, np.nan, np.nan],  # 100% missing
    'D': [1, 2, 3, 4, 5]
})

print("Original DataFrame:")
print(df)
print()

# Drop columns with ANY missing values
print("dropna(axis=1) - Drop columns with any missing:")
print(df.dropna(axis=1))
print()

# Drop columns where ALL values are missing
print("dropna(axis=1, how='all') - Drop only completely empty columns:")
print(df.dropna(axis=1, how='all'))
print()

# Drop columns with more than 50% missing
threshold = len(df) * 0.5
print(f"Drop columns with more than 50% missing (thresh={threshold}):")
print(df.dropna(axis=1, thresh=threshold))
9.5 Filling Missing Values
Fill with Constants
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, np.nan, 3, np.nan, 5],
    'B': [np.nan, 2, np.nan, 4, np.nan],
    'C': ['x', np.nan, 'z', np.nan, 'w']
})

print("Original DataFrame:")
print(df)
print()

# Fill all missing with a single value
print("fillna(0) - Fill all with 0:")
print(df.fillna(0))
print()

# Fill different columns with different values
print("fillna({'A': 0, 'B': -1, 'C': 'unknown'}):")
print(df.fillna({'A': 0, 'B': -1, 'C': 'unknown'}))
print()

# Fill only specific column
df_copy = df.copy()
df_copy['A'] = df_copy['A'].fillna(0)
print("Fill only column A with 0:")
print(df_copy)
Fill with Statistics
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5, np.nan, 7, 8],
    'B': [10, np.nan, 30, 40, np.nan, 60, 70, 80]
})

print("Original DataFrame:")
print(df)
print()

# Fill with mean
print("fillna(df.mean()) - Fill with column mean:")
print(df.fillna(df.mean()))
print()

# Fill with median
print("fillna(df.median()) - Fill with column median:")
print(df.fillna(df.median()))
print()

# Fill with mode (most frequent value)
print("Fill with mode:")
print(df.fillna(df.mode().iloc[0]))

# Fill specific column with its mean
df_copy = df.copy()
df_copy['A'] = df_copy['A'].fillna(df_copy['A'].mean())
print("\nColumn A filled with its mean:")
print(df_copy)
Forward Fill and Backward Fill
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Date': pd.date_range('2024-01-01', periods=8),
    'Value': [100, np.nan, np.nan, 103, np.nan, 105, np.nan, np.nan]
})

print("Original DataFrame (time series with gaps):")
print(df)
print()

# Forward fill (propagate last valid value forward)
print("ffill() - Forward fill:")
print(df.fillna(method='ffill'))  # or df.ffill()
print()

# Backward fill (propagate next valid value backward)
print("bfill() - Backward fill:")
print(df.fillna(method='bfill'))  # or df.bfill()
print()

# Limit the number of consecutive fills
print("ffill(limit=1) - Forward fill with limit:")
print(df.ffill(limit=1))
Interpolation
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Linear': [0, np.nan, np.nan, 6, np.nan, 10],
    'Index': [0, np.nan, np.nan, 6, np.nan, 10]
}, index=[0, 1, 2, 4, 5, 8])

print("Original DataFrame:")
print(df)
print()

# Linear interpolation
print("interpolate() - Linear interpolation:")
print(df.interpolate())
print()

# Interpolation based on index
print("interpolate(method='index') - Index-based interpolation:")
print(df.interpolate(method='index'))
print()

# Different interpolation methods
df_methods = pd.DataFrame({
    'Value': [0, np.nan, np.nan, np.nan, 10]
})

print("Original for comparison:")
print(df_methods['Value'].tolist())
print()

for method in ['linear', 'quadratic', 'cubic']:
    result = df_methods['Value'].interpolate(method=method)
    print(f"{method}: {result.round(2).tolist()}")
9.6 Advanced Missing Data Handling
Group-Based Imputation
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Sales', 'IT', 'IT', 'IT'],
    'Salary': [50000, np.nan, 55000, 80000, np.nan, 85000]
})

print("Original DataFrame:")
print(df)
print()

# Fill missing with group mean
df['Salary_filled'] = df.groupby('Department')['Salary'].transform(
    lambda x: x.fillna(x.mean())
)
print("Fill with department mean:")
print(df)
Conditional Filling
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Category': ['A', 'A', 'B', 'B', 'C', 'C'],
    'Value': [10, np.nan, 20, np.nan, 30, np.nan]
})

print("Original DataFrame:")
print(df)
print()

# Fill based on condition
fill_values = {'A': 15, 'B': 25, 'C': 35}
df['Value_filled'] = df.apply(
    lambda row: fill_values[row['Category']] if pd.isna(row['Value']) else row['Value'],
    axis=1
)
print("Conditional fill based on Category:")
print(df)
9.7 Missing Data Summary
Method	Use Case	Example
isnull()	Detect missing	df.isnull()
notna()	Detect non-missing	df.notna()
dropna()	Remove missing	df.dropna()
fillna(value)	Fill with constant	df.fillna(0)
fillna(df.mean())	Fill with statistic	df.fillna(df.mean())
ffill()	Forward fill	df.ffill()
bfill()	Backward fill	df.bfill()
interpolate()	Interpolate values	df.interpolate()
Chapter 10: Data Transformation
10.1 Overview of Transformation Methods
text

┌──────────────────────────────────────────────────────────────────┐
│                    DATA TRANSFORMATION METHODS                    │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  APPLY            Transform data using custom functions          │
│  • apply()        Apply function to rows/columns/elements        │
│  • map()          Element-wise transformation (Series)           │
│  • applymap()     Element-wise transformation (DataFrame)        │
│                                                                   │
│  MATHEMATICAL     Numeric transformations                        │
│  • Arithmetic     +, -, *, /, //, %, **                          │
│  • Logarithmic    np.log(), np.log10()                          │
│  • Normalization  (x - min) / (max - min)                       │
│  • Standardization (x - mean) / std                              │
│                                                                   │
│  BINNING          Convert continuous to categorical              │
│  • cut()          Equal-width bins                               │
│  • qcut()         Equal-frequency bins                           │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
10.2 Using apply()
Apply to Columns (Default)
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': [10, 20, 30, 40, 50],
    'C': [100, 200, 300, 400, 500]
})

print("Original DataFrame:")
print(df)
print()

# Apply function to each column
print("Apply sum to each column:")
print(df.apply(sum))  # Same as df.sum()
print()

print("Apply mean to each column:")
print(df.apply(np.mean))
print()

# Custom function
def range_func(x):
    return x.max() - x.min()

print("Apply custom range function to each column:")
print(df.apply(range_func))
print()

# Lambda function
print("Apply lambda (max - min) / mean:")
print(df.apply(lambda x: (x.max() - x.min()) / x.mean()))
Apply to Rows
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Math': [90, 85, 78],
    'Science': [88, 92, 85],
    'English': [95, 80, 82]
}, index=['Alice', 'Bob', 'Charlie'])

print("Original DataFrame (student scores):")
print(df)
print()

# Apply to rows (axis=1)
print("Sum of each row (total score):")
print(df.apply(sum, axis=1))
print()

print("Mean of each row (average score):")
print(df.apply(np.mean, axis=1))
print()

# Add total column
df['Total'] = df.apply(sum, axis=1)
df['Average'] = df.apply(lambda row: row[:-1].mean(), axis=1)  # Exclude Total
print("With Total and Average:")
print(df)
Apply with Custom Functions
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Score': [85, 92, 78],
    'Hours_Studied': [10, 15, 8]
})

print("Original DataFrame:")
print(df)
print()

# Function returning single value
def score_efficiency(row):
    return row['Score'] / row['Hours_Studied']

df['Efficiency'] = df.apply(score_efficiency, axis=1)
print("After adding Efficiency:")
print(df)
print()

# Function returning multiple values
def analyze_score(score):
    if score >= 90:
        return pd.Series(['A', 'Excellent'])
    elif score >= 80:
        return pd.Series(['B', 'Good'])
    else:
        return pd.Series(['C', 'Average'])

df[['Grade', 'Comment']] = df['Score'].apply(analyze_score)
print("After adding Grade and Comment:")
print(df)
10.3 Using map() for Series
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Grade': ['A', 'B', 'C'],
    'Status': ['active', 'inactive', 'active']
})

print("Original DataFrame:")
print(df)
print()

# Map using dictionary
grade_to_points = {'A': 4.0, 'B': 3.0, 'C': 2.0, 'D': 1.0, 'F': 0.0}
df['GPA'] = df['Grade'].map(grade_to_points)
print("After mapping Grade to GPA:")
print(df)
print()

# Map using function
df['Name_Upper'] = df['Name'].map(str.upper)
print("After mapping Name to uppercase:")
print(df)
print()

# Map with lambda
df['Status_Code'] = df['Status'].map(lambda x: 1 if x == 'active' else 0)
print("After mapping Status to code:")
print(df)
10.4 Using applymap() for Element-wise Operations
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1.234, 2.567, 3.891],
    'B': [4.123, 5.456, 6.789],
    'C': [7.012, 8.345, 9.678]
})

print("Original DataFrame:")
print(df)
print()

# Apply function to every element
# Note: In newer pandas versions, use df.map() instead of df.applymap()
print("Round to 1 decimal place:")
print(df.applymap(lambda x: round(x, 1)))
print()

print("Format as string with 2 decimals:")
print(df.applymap(lambda x: f'{x:.2f}'))
print()

# Multiple transformations
print("Square each element:")
print(df.applymap(lambda x: x ** 2))
10.5 Mathematical Transformations
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Value': [1, 10, 100, 1000, 10000],
    'Price': [10, 20, 30, 40, 50]
})

print("Original DataFrame:")
print(df)
print()

# Logarithmic transformation
df['Log_Value'] = np.log10(df['Value'])
df['Log_Price'] = np.log(df['Price'])
print("After log transformations:")
print(df)
print()

# Square root transformation
df['Sqrt_Value'] = np.sqrt(df['Value'])
print("After sqrt transformation:")
print(df)
print()

# Power transformation
df['Price_Squared'] = df['Price'] ** 2
print("After power transformation:")
print(df)
10.6 Normalization and Standardization
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Age': [25, 30, 35, 40, 45],
    'Salary': [50000, 60000, 70000, 80000, 90000],
    'Score': [85, 90, 78, 95, 88]
})

print("Original DataFrame:")
print(df)
print()

# Min-Max Normalization (scales to 0-1)
def min_max_normalize(col):
    return (col - col.min()) / (col.max() - col.min())

df_normalized = df.apply(min_max_normalize)
print("Min-Max Normalized (0-1 scale):")
print(df_normalized)
print()

# Z-Score Standardization (mean=0, std=1)
def z_score_standardize(col):
    return (col - col.mean()) / col.std()

df_standardized = df.apply(z_score_standardize)
print("Z-Score Standardized (mean=0, std=1):")
print(df_standardized)
print()

# Verify standardization
print("Verification of standardization:")
print(f"Mean: {df_standardized.mean().round(10).tolist()}")
print(f"Std: {df_standardized.std().round(2).tolist()}")
10.7 Binning with cut() and qcut()
Equal-Width Bins with cut()
Python

import pandas as pd
import numpy as np

# Sample data
ages = pd.Series([22, 25, 28, 32, 35, 38, 42, 45, 48, 55, 62, 68])

print("Original ages:")
print(ages.tolist())
print()

# Cut into equal-width bins
bins_equal = pd.cut(ages, bins=4)
print("Equal-width bins (4 bins):")
print(bins_equal)
print()

print("Value counts:")
print(bins_equal.value_counts().sort_index())
print()

# Custom bin edges
bins_custom = pd.cut(ages, bins=[0, 30, 40, 50, 100], labels=['Young', 'Adult', 'Middle', 'Senior'])
print("Custom bins with labels:")
print(bins_custom)
print()

print("Value counts:")
print(bins_custom.value_counts())
Equal-Frequency Bins with qcut()
Python

import pandas as pd
import numpy as np

# Sample data (skewed distribution)
income = pd.Series([20000, 25000, 30000, 35000, 40000, 
                    45000, 50000, 80000, 100000, 500000])

print("Original income:")
print(income.tolist())
print()

# Quantile-based bins (equal frequency)
bins_quantile = pd.qcut(income, q=4, labels=['Q1', 'Q2', 'Q3', 'Q4'])
print("Quantile bins (4 equal-frequency groups):")
print(bins_quantile)
print()

print("Value counts (should be equal):")
print(bins_quantile.value_counts().sort_index())
print()

# With specific percentiles
bins_percentile = pd.qcut(income, q=[0, 0.25, 0.5, 0.75, 1], 
                          labels=['Bottom 25%', '25-50%', '50-75%', 'Top 25%'])
print("Percentile-based labels:")
print(bins_percentile)
Comparison: cut() vs qcut()
Python

import pandas as pd
import numpy as np

# Skewed data
data = pd.Series([1, 2, 3, 4, 5, 6, 7, 8, 9, 100])

print("Original data:", data.tolist())
print()

print("cut() - Equal-width bins:")
cut_result = pd.cut(data, bins=4)
print(cut_result.value_counts().sort_index())
print()

print("qcut() - Equal-frequency bins:")
qcut_result = pd.qcut(data, q=4)
print(qcut_result.value_counts().sort_index())

# Note: qcut() distributes data more evenly across bins
# cut() creates bins of equal width, which may be empty for skewed data
10.8 Ranking Data
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Score': [85, 92, 78, 92, 88]
})

print("Original DataFrame:")
print(df)
print()

# Default ranking (average for ties)
df['Rank_avg'] = df['Score'].rank(ascending=False)
print("Rank (average method for ties):")
print(df)
print()

# Different ranking methods
df['Rank_min'] = df['Score'].rank(ascending=False, method='min')
df['Rank_max'] = df['Score'].rank(ascending=False, method='max')
df['Rank_first'] = df['Score'].rank(ascending=False, method='first')
df['Rank_dense'] = df['Score'].rank(ascending=False, method='dense')

print("Different ranking methods:")
print(df)
print()

# Explanation of methods for tied scores (92, 92):
# average: Both get average of positions (1+2)/2 = 1.5
# min: Both get minimum position = 1
# max: Both get maximum position = 2
# first: First occurrence gets 1, second gets 2
# dense: Both get 1, next value gets 2 (no gaps)
10.9 Transformation Summary
Method	Use Case	Example
apply(func)	Apply to columns/rows	df.apply(np.mean)
map(dict/func)	Transform Series elements	s.map({'A': 1})
applymap(func)	Transform all elements	df.applymap(str.upper)
transform(func)	Same shape output	df.transform(lambda x: x - x.mean())
cut()	Equal-width binning	pd.cut(s, bins=4)
qcut()	Equal-frequency binning	pd.qcut(s, q=4)
rank()	Rank values	s.rank(ascending=False)
clip()	Limit values	s.clip(lower=0, upper=100)
Chapter 11: String Operations
11.1 Introduction to String Methods
Pandas provides the .str accessor for string operations on Series.

Python

import pandas as pd

s = pd.Series(['Alice', 'Bob', 'Charlie', 'Diana'])

# Access string methods via .str
print("Original:")
print(s)

print("\nUppercase:")
print(s.str.upper())

print("\nLowercase:")
print(s.str.lower())
11.2 Case Conversion
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['alice smith', 'BOB JONES', 'Charlie Brown', 'DIANA prince']
})

print("Original:")
print(df)
print()

# Different case conversions
df['Upper'] = df['Name'].str.upper()
df['Lower'] = df['Name'].str.lower()
df['Title'] = df['Name'].str.title()
df['Capitalize'] = df['Name'].str.capitalize()
df['Swapcase'] = df['Name'].str.swapcase()

print("Case conversions:")
print(df)
11.3 String Cleaning
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['  Alice  ', '  Bob', 'Charlie  ', '  Diana  '],
    'Code': ['ABC123', 'DEF456', 'GHI789', 'JKL012']
})

print("Original:")
print(df)
print(f"Name values: {df['Name'].tolist()}")
print()

# Strip whitespace
df['Name_stripped'] = df['Name'].str.strip()
df['Name_lstrip'] = df['Name'].str.lstrip()
df['Name_rstrip'] = df['Name'].str.rstrip()

print("After stripping:")
print(f"strip:  {df['Name_stripped'].tolist()}")
print(f"lstrip: {df['Name_lstrip'].tolist()}")
print(f"rstrip: {df['Name_rstrip'].tolist()}")
print()

# Remove specific characters
df['Code_no_digits'] = df['Code'].str.replace(r'\d', '', regex=True)
df['Code_no_letters'] = df['Code'].str.replace(r'[A-Z]', '', regex=True)

print("Character removal:")
print(df[['Code', 'Code_no_digits', 'Code_no_letters']])
11.4 String Searching
Python

import pandas as pd

df = pd.DataFrame({
    'Email': ['alice@gmail.com', 'bob@yahoo.com', 'charlie@gmail.com', 
              'diana@hotmail.com', 'eve@gmail.com'],
    'Text': ['Hello World', 'hello world', 'HELLO WORLD', 
             'Hello Python', 'Goodbye World']
})

print("Original:")
print(df)
print()

# Contains
print("Email contains 'gmail':")
print(df[df['Email'].str.contains('gmail')])
print()

# Case-insensitive contains
print("Text contains 'hello' (case-insensitive):")
print(df[df['Text'].str.contains('hello', case=False)])
print()

# Starts with
print("Email starts with 'a' or 'b':")
print(df[df['Email'].str.startswith(('a', 'b'))])
print()

# Ends with
print("Email ends with '.com':")
print(df[df['Email'].str.endswith('.com')])
print()

# Find position
df['World_pos'] = df['Text'].str.find('World')
print("Position of 'World' (-1 if not found):")
print(df[['Text', 'World_pos']])
print()

# Count occurrences
df['o_count'] = df['Text'].str.count('o')
print("Count of 'o':")
print(df[['Text', 'o_count']])
11.5 String Splitting and Joining
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice Smith', 'Bob Jones', 'Charlie Brown'],
    'Tags': ['python,data,ml', 'java,web,api', 'python,ml,ai']
})

print("Original:")
print(df)
print()

# Split into list
df['Name_split'] = df['Name'].str.split(' ')
print("Split Name:")
print(df[['Name', 'Name_split']])
print()

# Split and expand into columns
name_expanded = df['Name'].str.split(' ', expand=True)
name_expanded.columns = ['First', 'Last']
print("Split and expand:")
print(name_expanded)
print()

# Get specific part after split
df['First_Name'] = df['Name'].str.split(' ').str[0]
df['Last_Name'] = df['Name'].str.split(' ').str[1]
print("Extract parts:")
print(df[['Name', 'First_Name', 'Last_Name']])
print()

# Split with limit
df['Tags_first_two'] = df['Tags'].str.split(',', n=1, expand=True)[0]
print("First tag only:")
print(df[['Tags', 'Tags_first_two']])
print()

# Join
tags_joined = df['Tags'].str.split(',').str.join(' | ')
print("Join with different separator:")
print(tags_joined)
11.6 String Slicing and Indexing
Python

import pandas as pd

df = pd.DataFrame({
    'Code': ['ABC123', 'DEF456', 'GHI789'],
    'Phone': ['123-456-7890', '234-567-8901', '345-678-9012']
})

print("Original:")
print(df)
print()

# Get specific characters
df['First_char'] = df['Code'].str[0]
df['Last_char'] = df['Code'].str[-1]
df['First_three'] = df['Code'].str[:3]
df['Last_three'] = df['Code'].str[-3:]

print("Character extraction:")
print(df)
print()

# Extract area code from phone
df['Area_code'] = df['Phone'].str[:3]
df['Rest'] = df['Phone'].str[4:]

print("Phone parsing:")
print(df[['Phone', 'Area_code', 'Rest']])
11.7 String Padding and Alignment
Python

import pandas as pd

df = pd.DataFrame({
    'ID': ['1', '12', '123', '1234'],
    'Name': ['Al', 'Bob', 'Charlie', 'Di']
})

print("Original:")
print(df)
print()

# Padding
df['ID_padded'] = df['ID'].str.zfill(5)  # Zero-fill
df['ID_left_pad'] = df['ID'].str.pad(5, side='left', fillchar='0')
df['ID_right_pad'] = df['ID'].str.pad(5, side='right', fillchar='_')

print("Padding:")
print(df)
print()

# Centering
df['Name_center'] = df['Name'].str.center(10, '*')
df['Name_ljust'] = df['Name'].str.ljust(10, '_')
df['Name_rjust'] = df['Name'].str.rjust(10, '_')

print("Alignment:")
print(df[['Name', 'Name_center', 'Name_ljust', 'Name_rjust']])
11.8 Regular Expressions
Python

import pandas as pd

df = pd.DataFrame({
    'Text': ['Call me at 123-456-7890', 
             'My number is 987-654-3210',
             'Contact: 555-123-4567 or 555-987-6543',
             'No phone here'],
    'Email': ['alice@gmail.com', 'bob.smith@yahoo.co.uk', 
              'charlie123@company.org', 'invalid-email']
})

print("Original:")
print(df)
print()

# Extract using regex
df['First_phone'] = df['Text'].str.extract(r'(\d{3}-\d{3}-\d{4})')
print("Extract first phone number:")
print(df[['Text', 'First_phone']])
print()

# Extract all matches
df['All_phones'] = df['Text'].str.findall(r'\d{3}-\d{3}-\d{4}')
print("Extract all phone numbers:")
print(df[['Text', 'All_phones']])
print()

# Extract email parts
df['Email_user'] = df['Email'].str.extract(r'^([^@]+)@')
df['Email_domain'] = df['Email'].str.extract(r'@(.+)$')
print("Extract email parts:")
print(df[['Email', 'Email_user', 'Email_domain']])
print()

# Replace using regex
df['Text_masked'] = df['Text'].str.replace(r'\d{3}-\d{3}-\d{4}', 'XXX-XXX-XXXX', regex=True)
print("Mask phone numbers:")
print(df[['Text', 'Text_masked']])
11.9 String Methods Summary
Method	Description	Example
str.upper()	Convert to uppercase	s.str.upper()
str.lower()	Convert to lowercase	s.str.lower()
str.title()	Convert to title case	s.str.title()
str.strip()	Remove whitespace	s.str.strip()
str.contains()	Check if contains	s.str.contains('x')
str.startswith()	Check prefix	s.str.startswith('A')
str.endswith()	Check suffix	s.str.endswith('z')
str.split()	Split string	s.str.split(',')
str.replace()	Replace substring	s.str.replace('a', 'b')
str.extract()	Extract regex groups	s.str.extract(r'(\d+)')
str.len()	Get string length	s.str.len()
str.zfill()	Zero-fill	s.str.zfill(5)
str[:]	Slice string	s.str[:3]
Chapter 12: Working with Dates and Times
12.1 Introduction to Datetime in Pandas
text

┌──────────────────────────────────────────────────────────────────┐
│                    DATETIME IN PANDAS                             │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  Data Types:                                                      │
│  • Timestamp    - Single datetime value                          │
│  • DatetimeIndex - Index of datetime values                      │
│  • Period       - Time span (e.g., "January 2024")               │
│  • Timedelta    - Duration/difference between times              │
│                                                                   │
│  Common Operations:                                               │
│  • Parsing strings to datetime                                   │
│  • Extracting components (year, month, day, etc.)                │
│  • Date arithmetic                                                │
│  • Resampling time series                                        │
│  • Timezone handling                                              │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
12.2 Creating Datetime Objects
Converting Strings to Datetime
Python

import pandas as pd

# Single timestamp
ts = pd.Timestamp('2024-01-15')
print(f"Single timestamp: {ts}")
print()

# Series of dates
dates = pd.Series(['2024-01-15', '2024-02-20', '2024-03-25'])
print("Original string series:")
print(dates)
print(f"dtype: {dates.dtype}")
print()

# Convert to datetime
dates_dt = pd.to_datetime(dates)
print("After pd.to_datetime():")
print(dates_dt)
print(f"dtype: {dates_dt.dtype}")
Different Date Formats
Python

import pandas as pd

# Pandas can parse many formats automatically
dates = pd.Series([
    '2024-01-15',
    '01/15/2024',
    '15-Jan-2024',
    'January 15, 2024',
    '2024.01.15',
    '15/01/2024'
])

print("Various date formats:")
print(dates)
print()

# Parse automatically (infer format)
parsed = pd.to_datetime(dates, dayfirst=False)  # Month first for ambiguous
print("Parsed dates:")
print(parsed)
print()

# Specify exact format for better performance
dates_formatted = pd.Series(['15-01-2024', '20-02-2024', '25-03-2024'])
parsed_exact = pd.to_datetime(dates_formatted, format='%d-%m-%Y')
print("Parsed with specific format:")
print(parsed_exact)
Creating Date Ranges
Python

import pandas as pd

# Date range with daily frequency
daily = pd.date_range(start='2024-01-01', end='2024-01-10', freq='D')
print("Daily range:")
print(daily)
print()

# Date range with specific number of periods
weekly = pd.date_range(start='2024-01-01', periods=10, freq='W')
print("Weekly (10 periods):")
print(weekly)
print()

# Business days
business = pd.date_range(start='2024-01-01', periods=10, freq='B')
print("Business days:")
print(business)
print()

# Monthly start
monthly = pd.date_range(start='2024-01-01', periods=12, freq='MS')
print("Monthly start:")
print(monthly)
print()

# Hourly
hourly = pd.date_range(start='2024-01-01 09:00', periods=8, freq='H')
print("Hourly:")
print(hourly)
Common Frequency Codes
Code	Description	Example
D	Calendar day	Every day
B	Business day	Weekdays only
W	Weekly	Every week
M	Month end	Last day of month
MS	Month start	First day of month
Q	Quarter end	End of quarter
Y	Year end	Dec 31
H	Hourly	Every hour
T or min	Minutely	Every minute
S	Secondly	Every second
12.3 Extracting Date Components
Python

import pandas as pd

df = pd.DataFrame({
    'Date': pd.date_range('2024-01-15 10:30:45', periods=5, freq='M')
})

print("Original DataFrame:")
print(df)
print()

# Extract components using .dt accessor
df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
df['Day'] = df['Date'].dt.day
df['Hour'] = df['Date'].dt.hour
df['Minute'] = df['Date'].dt.minute
df['Second'] = df['Date'].dt.second

print("Extracted components:")
print(df)
print()

# Additional useful extractions
df['Day_of_week'] = df['Date'].dt.dayofweek  # 0=Monday, 6=Sunday
df['Day_name'] = df['Date'].dt.day_name()
df['Month_name'] = df['Date'].dt.month_name()
df['Quarter'] = df['Date'].dt.quarter
df['Week'] = df['Date'].dt.isocalendar().week
df['Is_month_end'] = df['Date'].dt.is_month_end

print("Additional extractions:")
print(df[['Date', 'Day_name', 'Month_name', 'Quarter', 'Week', 'Is_month_end']])
12.4 Date Arithmetic
Python

import pandas as pd
from datetime import timedelta

df = pd.DataFrame({
    'Date': pd.date_range('2024-01-15', periods=5, freq='D')
})

print("Original DataFrame:")
print(df)
print()

# Add/subtract days
df['Plus_7_days'] = df['Date'] + pd.Timedelta(days=7)
df['Minus_3_days'] = df['Date'] - pd.Timedelta(days=3)

print("Date arithmetic:")
print(df)
print()

# Add different time units
df['Plus_1_week'] = df['Date'] + pd.Timedelta(weeks=1)
df['Plus_1_month'] = df['Date'] + pd.DateOffset(months=1)
df['Plus_1_year'] = df['Date'] + pd.DateOffset(years=1)

print("Different time units:")
print(df[['Date', 'Plus_1_week', 'Plus_1_month', 'Plus_1_year']])
print()

# Difference between dates
df['Days_since_first'] = (df['Date'] - df['Date'].iloc[0]).dt.days
print("Days since first date:")
print(df[['Date', 'Days_since_first']])
12.5 Filtering by Date
Python

import pandas as pd

# Create time series data
df = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', '2024-12-31', freq='D'),
    'Value': range(731)  # 2 years of daily data
})

print(f"Dataset: {len(df)} rows from {df['Date'].min()} to {df['Date'].max()}")
print()

# Filter by specific date
print("January 15, 2024:")
print(df[df['Date'] == '2024-01-15'])
print()

# Filter by date range
print("First week of 2024:")
print(df[(df['Date'] >= '2024-01-01') & (df['Date'] <= '2024-01-07')])
print()

# Filter by year
print("Year 2024 only (first 5 rows):")
print(df[df['Date'].dt.year == 2024].head())
print()

# Filter by month
print("March 2024:")
print(df[(df['Date'].dt.year == 2024) & (df['Date'].dt.month == 3)].head())
print()

# Filter by day of week (0=Monday)
print("Mondays in January 2024:")
print(df[(df['Date'].dt.year == 2024) & 
         (df['Date'].dt.month == 1) & 
         (df['Date'].dt.dayofweek == 0)])
12.6 Setting DateTime as Index
Python

import pandas as pd
import numpy as np

# Create time series
df = pd.DataFrame({
    'Date': pd.date_range('2024-01-01', periods=100, freq='D'),
    'Value': np.random.randn(100).cumsum()
})

print("Original DataFrame:")
print(df.head())
print()

# Set date as index
df.set_index('Date', inplace=True)
print("With Date as index:")
print(df.head())
print()

# Now you can slice by date directly
print("January 2024 (using string slicing):")
print(df['2024-01'])
print()

print("Specific date range:")
print(df['2024-01-15':'2024-01-20'])
print()

# Partial string indexing
print("March 2024:")
print(df['2024-03'].head())
12.7 Resampling Time Series
Python

import pandas as pd
import numpy as np

# Create hourly data
np.random.seed(42)
df = pd.DataFrame({
    'Timestamp': pd.date_range('2024-01-01', periods=168, freq='H'),  # 1 week hourly
    'Value': np.random.randn(168) * 10 + 100
})
df.set_index('Timestamp', inplace=True)

print("Hourly data (first 5 rows):")
print(df.head())
print()

# Resample to daily
daily = df.resample('D').mean()
print("Resampled to daily mean:")
print(daily)
print()

# Different aggregations
print("Daily statistics:")
daily_stats = df.resample('D').agg(['mean', 'min', 'max', 'sum'])
print(daily_stats)
print()

# Resample to weekly
weekly = df.resample('W').sum()
print("Weekly sum:")
print(weekly)
print()

# Custom resampling with multiple columns
df['Count'] = 1
resampled = df.resample('D').agg({
    'Value': ['mean', 'std'],
    'Count': 'sum'
})
print("Custom aggregation:")
print(resampled)
12.8 Time Zone Handling
Python

import pandas as pd

# Create datetime series
df = pd.DataFrame({
    'Time': pd.date_range('2024-01-15 10:00', periods=5, freq='H')
})

print("Original (no timezone):")
print(df)
print()

# Localize to timezone (assign timezone to naive datetime)
df['Time_UTC'] = df['Time'].dt.tz_localize('UTC')
print("Localized to UTC:")
print(df)
print()

# Convert to different timezone
df['Time_NYC'] = df['Time_UTC'].dt.tz_convert('America/New_York')
df['Time_Tokyo'] = df['Time_UTC'].dt.tz_convert('Asia/Tokyo')
df['Time_London'] = df['Time_UTC'].dt.tz_convert('Europe/London')

print("Multiple timezones:")
print(df[['Time_UTC', 'Time_NYC', 'Time_Tokyo', 'Time_London']])
12.9 Working with Periods
Python

import pandas as pd

# Create period (represents a span of time)
month_period = pd.Period('2024-01', freq='M')
print(f"Month period: {month_period}")
print(f"Start: {month_period.start_time}")
print(f"End: {month_period.end_time}")
print()

# Period range
quarters = pd.period_range('2024Q1', periods=4, freq='Q')
print("Quarterly periods:")
print(quarters)
print()

# Convert timestamp to period
df = pd.DataFrame({
    'Date': pd.date_range('2024-01-15', periods=5, freq='M')
})
df['Month'] = df['Date'].dt.to_period('M')
df['Quarter'] = df['Date'].dt.to_period('Q')
df['Year'] = df['Date'].dt.to_period('Y')

print("Converted to periods:")
print(df)
12.10 DateTime Summary
Operation	Method	Example
Parse strings	pd.to_datetime()	pd.to_datetime('2024-01-15')
Create range	pd.date_range()	pd.date_range('2024-01-01', periods=10)
Extract year	.dt.year	df['Date'].dt.year
Extract month	.dt.month	df['Date'].dt.month
Day of week	.dt.dayofweek	df['Date'].dt.dayofweek
Add days	+ pd.Timedelta()	date + pd.Timedelta(days=7)
Resample	.resample()	df.resample('D').mean()
Localize tz	.dt.tz_localize()	df['Date'].dt.tz_localize('UTC')
Convert tz	.dt.tz_convert()	df['Date'].dt.tz_convert('US/Eastern')
To period	.dt.to_period()	df['Date'].dt.to_period('M')
Chapter 13: Grouping and Aggregation
13.1 Introduction to GroupBy
The groupby() operation is one of the most powerful features in Pandas. It follows the Split-Apply-Combine pattern.

text

┌──────────────────────────────────────────────────────────────────┐
│                    SPLIT-APPLY-COMBINE                            │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│   ORIGINAL DATA                                                   │
│   ┌──────────────────────┐                                       │
│   │ Category │ Value     │                                       │
│   │    A     │   10      │                                       │
│   │    B     │   20      │                                       │
│   │    A     │   30      │                                       │
│   │    B     │   40      │                                       │
│   │    A     │   50      │                                       │
│   └──────────────────────┘                                       │
│                │                                                  │
│                ▼ SPLIT                                           │
│   ┌─────────────┐    ┌─────────────┐                             │
│   │ Category: A │    │ Category: B │                             │
│   │  10, 30, 50 │    │  20, 40     │                             │
│   └─────────────┘    └─────────────┘                             │
│         │                  │                                      │
│         ▼ APPLY            ▼ APPLY                               │
│   ┌─────────────┐    ┌─────────────┐                             │
│   │  sum = 90   │    │  sum = 60   │                             │
│   └─────────────┘    └─────────────┘                             │
│         │                  │                                      │
│         └────────┬─────────┘                                      │
│                  ▼ COMBINE                                       │
│   ┌──────────────────────┐                                       │
│   │ Category │   Sum     │                                       │
│   │    A     │   90      │                                       │
│   │    B     │   60      │                                       │
│   └──────────────────────┘                                       │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
13.2 Basic GroupBy Operations
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Engineering', 'Engineering', 'HR', 'HR'],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank'],
    'Salary': [50000, 55000, 80000, 85000, 45000, 48000],
    'Years': [2, 3, 5, 4, 1, 2]
})

print("Original DataFrame:")
print(df)
print()

# Group by single column
grouped = df.groupby('Department')
print(f"GroupBy object: {type(grouped)}")
print()

# Apply aggregation
print("Mean salary by department:")
print(grouped['Salary'].mean())
print()

print("Sum of years by department:")
print(grouped['Years'].sum())
print()

# All numeric columns
print("Mean of all numeric columns by department:")
print(grouped.mean())
13.3 Multiple Aggregations
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Engineering', 'Engineering', 'HR', 'HR'],
    'Salary': [50000, 55000, 80000, 85000, 45000, 48000],
    'Bonus': [5000, 5500, 8000, 8500, 4500, 4800],
    'Years': [2, 3, 5, 4, 1, 2]
})

print("Original DataFrame:")
print(df)
print()

# Multiple aggregations on single column
print("Multiple aggregations on Salary:")
print(df.groupby('Department')['Salary'].agg(['mean', 'min', 'max', 'sum', 'count']))
print()

# Different aggregations for different columns
print("Different aggregations per column:")
print(df.groupby('Department').agg({
    'Salary': ['mean', 'sum'],
    'Bonus': 'sum',
    'Years': 'max'
}))
print()

# Named aggregations (cleaner output)
print("Named aggregations:")
print(df.groupby('Department').agg(
    Avg_Salary=('Salary', 'mean'),
    Total_Salary=('Salary', 'sum'),
    Total_Bonus=('Bonus', 'sum'),
    Max_Years=('Years', 'max'),
    Employee_Count=('Salary', 'count')
))
13.4 Grouping by Multiple Columns
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Sales', 'Engineering', 'Engineering', 'Engineering'],
    'Level': ['Junior', 'Senior', 'Junior', 'Junior', 'Senior', 'Senior'],
    'Salary': [45000, 65000, 48000, 70000, 95000, 90000],
    'Count': [1, 1, 1, 1, 1, 1]
})

print("Original DataFrame:")
print(df)
print()

# Group by multiple columns
print("Group by Department and Level:")
print(df.groupby(['Department', 'Level']).agg({
    'Salary': 'mean',
    'Count': 'sum'
}))
print()

# Reset index to get flat DataFrame
result = df.groupby(['Department', 'Level']).agg({
    'Salary': 'mean',
    'Count': 'sum'
}).reset_index()

print("With reset_index():")
print(result)
13.5 Custom Aggregation Functions
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Sales', 'Engineering', 'Engineering'],
    'Salary': [50000, 55000, 60000, 80000, 85000]
})

print("Original DataFrame:")
print(df)
print()

# Custom function
def salary_range(x):
    return x.max() - x.min()

def coefficient_of_variation(x):
    return x.std() / x.mean() * 100

# Apply custom functions
print("Custom aggregations:")
print(df.groupby('Department')['Salary'].agg([
    'mean',
    'std',
    ('range', salary_range),
    ('cv', coefficient_of_variation)
]))
print()


# Lambda functions
print("Using lambda functions:")
print(df.groupby('Department')['Salary'].agg([
    ('mean', 'mean'),
    ('range', lambda x: x.max() - x.min()),
    ('above_avg', lambda x: (x > x.mean()).sum())
]))
13.6 Transform vs Aggregate
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Sales', 'Engineering', 'Engineering'],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Salary': [50000, 55000, 60000, 80000, 85000]
})

print("Original DataFrame:")
print(df)
print()

# Aggregate: Returns reduced result (one row per group)
print("AGGREGATE (reduces data):")
print(df.groupby('Department')['Salary'].mean())
print()

# Transform: Returns same-sized result (broadcasts back to original)
print("TRANSFORM (same size as original):")
df['Dept_Avg_Salary'] = df.groupby('Department')['Salary'].transform('mean')
print(df)
print()

# Use case: Calculate deviation from group mean
df['Deviation'] = df['Salary'] - df.groupby('Department')['Salary'].transform('mean')
print("With deviation from department mean:")
print(df)
print()

# Use case: Normalize within groups
df['Normalized'] = df.groupby('Department')['Salary'].transform(
    lambda x: (x - x.mean()) / x.std()
)
print("With within-group normalization:")
print(df)
13.7 Filter Groups
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Engineering', 'Engineering', 'Engineering', 'HR'],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank'],
    'Salary': [50000, 55000, 80000, 85000, 90000, 45000]
})

print("Original DataFrame:")
print(df)
print()

# Filter: Keep only groups meeting a condition
# Keep departments with more than 2 employees
filtered = df.groupby('Department').filter(lambda x: len(x) > 2)
print("Departments with more than 2 employees:")
print(filtered)
print()

# Keep departments with average salary > 50000
filtered = df.groupby('Department').filter(lambda x: x['Salary'].mean() > 50000)
print("Departments with average salary > 50000:")
print(filtered)
print()

# Keep departments where all salaries > 40000
filtered = df.groupby('Department').filter(lambda x: (x['Salary'] > 40000).all())
print("Departments where all salaries > 40000:")
print(filtered)
13.8 Apply Custom Functions to Groups
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Sales', 'Engineering', 'Engineering'],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Salary': [50000, 55000, 60000, 80000, 85000],
    'Performance': [85, 90, 78, 92, 88]
})

print("Original DataFrame:")
print(df)
print()

# Apply function to each group
def top_performer(group):
    """Return the top performer in each group."""
    return group.loc[group['Performance'].idxmax()]

print("Top performer in each department:")
print(df.groupby('Department').apply(top_performer))
print()

# Apply function that returns DataFrame
def add_rank(group):
    """Add rank within group."""
    group = group.copy()
    group['Rank'] = group['Performance'].rank(ascending=False)
    return group

print("With performance rank within department:")
print(df.groupby('Department').apply(add_rank))
print()

# Return summary DataFrame
def group_summary(group):
    """Return summary statistics for group."""
    return pd.Series({
        'Count': len(group),
        'Avg_Salary': group['Salary'].mean(),
        'Max_Performance': group['Performance'].max(),
        'Top_Performer': group.loc[group['Performance'].idxmax(), 'Name']
    })

print("Group summaries:")
print(df.groupby('Department').apply(group_summary))
13.9 Iterating Over Groups
Python

import pandas as pd

df = pd.DataFrame({
    'Department': ['Sales', 'Sales', 'Engineering', 'Engineering', 'HR'],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Salary': [50000, 55000, 80000, 85000, 45000]
})

print("Original DataFrame:")
print(df)
print()

# Iterate over groups
print("Iterating over groups:")
print("-" * 40)

for name, group in df.groupby('Department'):
    print(f"\nGroup: {name}")
    print(f"Size: {len(group)}")
    print(f"Avg Salary: ${group['Salary'].mean():,.0f}")
    print(group)

print()

# Get specific group
print("Get specific group (Engineering):")
print(df.groupby('Department').get_group('Engineering'))
13.10 Pivot Tables (GroupBy on Steroids)
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Date': pd.date_range('2024-01-01', periods=12, freq='M'),
    'Region': ['North', 'South', 'North', 'South'] * 3,
    'Product': ['A', 'A', 'B', 'B'] * 3,
    'Sales': [100, 150, 200, 250, 120, 160, 220, 270, 110, 140, 190, 230],
    'Quantity': [10, 15, 20, 25, 12, 16, 22, 27, 11, 14, 19, 23]
})

print("Original DataFrame:")
print(df)
print()

# Basic pivot table
print("Pivot table - Sales by Region and Product:")
pivot = pd.pivot_table(df, 
                       values='Sales', 
                       index='Region', 
                       columns='Product',
                       aggfunc='sum')
print(pivot)
print()

# Multiple aggregations
print("Pivot table - Multiple aggregations:")
pivot = pd.pivot_table(df,
                       values='Sales',
                       index='Region',
                       columns='Product',
                       aggfunc=['sum', 'mean', 'count'])
print(pivot)
print()

# Multiple values
print("Pivot table - Multiple values:")
pivot = pd.pivot_table(df,
                       values=['Sales', 'Quantity'],
                       index='Region',
                       columns='Product',
                       aggfunc='sum')
print(pivot)
print()

# With margins (totals)
print("Pivot table - With totals:")
pivot = pd.pivot_table(df,
                       values='Sales',
                       index='Region',
                       columns='Product',
                       aggfunc='sum',
                       margins=True,
                       margins_name='Total')
print(pivot)
13.11 Crosstab
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Gender': ['M', 'F', 'M', 'F', 'M', 'F', 'M', 'F', 'M', 'F'],
    'Department': ['Sales', 'Sales', 'Engineering', 'Engineering', 'HR',
                   'Sales', 'Engineering', 'HR', 'Sales', 'Engineering'],
    'Level': ['Junior', 'Senior', 'Senior', 'Junior', 'Junior',
              'Junior', 'Senior', 'Senior', 'Senior', 'Junior']
})

print("Original DataFrame:")
print(df)
print()

# Basic crosstab (frequency count)
print("Crosstab - Gender vs Department:")
print(pd.crosstab(df['Gender'], df['Department']))
print()

# With margins
print("Crosstab - With margins:")
print(pd.crosstab(df['Gender'], df['Department'], margins=True))
print()

# Normalized (percentages)
print("Crosstab - Normalized (row percentages):")
print(pd.crosstab(df['Gender'], df['Department'], normalize='index').round(2))
print()

# Multiple indices
print("Crosstab - Gender and Level vs Department:")
print(pd.crosstab([df['Gender'], df['Level']], df['Department']))
13.12 GroupBy Summary
Operation	Method	Returns
Basic aggregation	groupby().agg()	Reduced DataFrame
Multiple functions	groupby().agg([funcs])	Multi-column result
Different per column	groupby().agg({col: func})	Customized result
Transform	groupby().transform()	Same-size result
Filter groups	groupby().filter()	Filtered DataFrame
Custom apply	groupby().apply()	Flexible result
Get single group	groupby().get_group()	Single group DataFrame
Iterate	for name, group in groupby()	Name and DataFrame
Pivot table	pd.pivot_table()	Reshaped aggregation
Crosstab	pd.crosstab()	Frequency table
Chapter 14: Merging, Joining, and Concatenating
14.1 Overview of Combining Data
text

┌──────────────────────────────────────────────────────────────────┐
│                    COMBINING DATA IN PANDAS                       │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  CONCAT                                                           │
│  • Stack DataFrames vertically (rows) or horizontally (columns)  │
│  • Like "gluing" DataFrames together                              │
│  • No matching on keys                                            │
│                                                                   │
│  MERGE                                                            │
│  • Combine based on common columns (like SQL JOIN)               │
│  • Matches rows based on key values                               │
│  • Different join types: inner, outer, left, right               │
│                                                                   │
│  JOIN                                                             │
│  • Combine based on index                                         │
│  • Convenience method for merge on index                          │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
14.2 Concatenation (concat)
Vertical Concatenation (Stacking Rows)
Python

import pandas as pd

df1 = pd.DataFrame({
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30]
})

df2 = pd.DataFrame({
    'Name': ['Charlie', 'Diana'],
    'Age': [35, 28]
})

df3 = pd.DataFrame({
    'Name': ['Eve'],
    'Age': [32]
})

print("DataFrame 1:")
print(df1)
print("\nDataFrame 2:")
print(df2)
print("\nDataFrame 3:")
print(df3)
print()

# Vertical concatenation (default axis=0)
result = pd.concat([df1, df2, df3])
print("Concatenated (vertical):")
print(result)
print()

# Reset index
result = pd.concat([df1, df2, df3], ignore_index=True)
print("With ignore_index=True:")
print(result)
print()

# Add keys to identify source
result = pd.concat([df1, df2, df3], keys=['First', 'Second', 'Third'])
print("With keys:")
print(result)
Horizontal Concatenation (Adding Columns)
Python

import pandas as pd

df1 = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
})

df2 = pd.DataFrame({
    'Salary': [50000, 60000, 70000],
    'Department': ['Sales', 'Engineering', 'HR']
})

print("DataFrame 1:")
print(df1)
print("\nDataFrame 2:")
print(df2)
print()

# Horizontal concatenation (axis=1)
result = pd.concat([df1, df2], axis=1)
print("Concatenated (horizontal):")
print(result)
Handling Mismatched Columns
Python

import pandas as pd

df1 = pd.DataFrame({
    'A': [1, 2],
    'B': [3, 4]
})

df2 = pd.DataFrame({
    'B': [5, 6],
    'C': [7, 8]
})

print("DataFrame 1:")
print(df1)
print("\nDataFrame 2:")
print(df2)
print()

# Default: outer join (keep all columns)
result = pd.concat([df1, df2])
print("Concat with default (outer):")
print(result)
print()

# Inner join (keep only common columns)
result = pd.concat([df1, df2], join='inner')
print("Concat with join='inner':")
print(result)
14.3 Merge (SQL-Style Joins)
Basic Merge
Python

import pandas as pd

# Employee data
employees = pd.DataFrame({
    'emp_id': [1, 2, 3, 4, 5],
    'name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'dept_id': [101, 102, 101, 103, 102]
})

# Department data
departments = pd.DataFrame({
    'dept_id': [101, 102, 103, 104],
    'dept_name': ['Sales', 'Engineering', 'HR', 'Marketing']
})

print("Employees:")
print(employees)
print("\nDepartments:")
print(departments)
print()

# Default merge (inner join on common column)
result = pd.merge(employees, departments)
print("Merged (inner join on dept_id):")
print(result)
Join Types Explained
Python

import pandas as pd

left = pd.DataFrame({
    'key': ['A', 'B', 'C'],
    'value_left': [1, 2, 3]
})

right = pd.DataFrame({
    'key': ['B', 'C', 'D'],
    'value_right': [4, 5, 6]
})

print("Left DataFrame:")
print(left)
print("\nRight DataFrame:")
print(right)
print()

# INNER JOIN: Only matching keys
inner = pd.merge(left, right, on='key', how='inner')
print("INNER JOIN (only matching):")
print(inner)
print()

# LEFT JOIN: All from left + matching from right
left_join = pd.merge(left, right, on='key', how='left')
print("LEFT JOIN (all from left):")
print(left_join)
print()

# RIGHT JOIN: All from right + matching from left
right_join = pd.merge(left, right, on='key', how='right')
print("RIGHT JOIN (all from right):")
print(right_join)
print()

# OUTER JOIN: All keys from both
outer = pd.merge(left, right, on='key', how='outer')
print("OUTER JOIN (all keys):")
print(outer)
Visual Representation of Join Types
text

LEFT DataFrame        RIGHT DataFrame
┌─────┬───────┐      ┌─────┬────────┐
│ key │ value │      │ key │ value  │
├─────┼───────┤      ├─────┼────────┤
│  A  │   1   │      │  B  │   4    │
│  B  │   2   │      │  C  │   5    │
│  C  │   3   │      │  D  │   6    │
└─────┴───────┘      └─────┴────────┘

INNER JOIN (B, C only)
┌─────┬───────┬────────┐
│ key │ left  │ right  │
├─────┼───────┼────────┤
│  B  │   2   │   4    │
│  C  │   3   │   5    │
└─────┴───────┴────────┘

LEFT JOIN (A, B, C)
┌─────┬───────┬────────┐
│ key │ left  │ right  │
├─────┼───────┼────────┤
│  A  │   1   │  NaN   │
│  B  │   2   │   4    │
│  C  │   3   │   5    │
└─────┴───────┴────────┘

RIGHT JOIN (B, C, D)
┌─────┬───────┬────────┐
│ key │ left  │ right  │
├─────┼───────┼────────┤
│  B  │   2   │   4    │
│  C  │   3   │   5    │
│  D  │  NaN  │   6    │
└─────┴───────┴────────┘

OUTER JOIN (A, B, C, D)
┌─────┬───────┬────────┐
│ key │ left  │ right  │
├─────┼───────┼────────┤
│  A  │   1   │  NaN   │
│  B  │   2   │   4    │
│  C  │   3   │   5    │
│  D  │  NaN  │   6    │
└─────┴───────┴────────┘
Merge on Multiple Columns
Python

import pandas as pd

sales = pd.DataFrame({
    'year': [2023, 2023, 2024, 2024],
    'quarter': [1, 2, 1, 2],
    'sales': [100, 150, 120, 180]
})

targets = pd.DataFrame({
    'year': [2023, 2023, 2024, 2024],
    'quarter': [1, 2, 1, 2],
    'target': [90, 140, 110, 170]
})

print("Sales:")
print(sales)
print("\nTargets:")
print(targets)
print()

# Merge on multiple columns
result = pd.merge(sales, targets, on=['year', 'quarter'])
print("Merged on year and quarter:")
print(result)
Merge with Different Column Names
Python

import pandas as pd

employees = pd.DataFrame({
    'emp_id': [1, 2, 3],
    'name': ['Alice', 'Bob', 'Charlie'],
    'manager_id': [101, 102, 101]
})

managers = pd.DataFrame({
    'mgr_id': [101, 102],
    'mgr_name': ['Sarah', 'Tom']
})

print("Employees:")
print(employees)
print("\nManagers:")
print(managers)
print()

# Merge with different column names
result = pd.merge(employees, managers, 
                  left_on='manager_id', 
                  right_on='mgr_id')
print("Merged with different column names:")
print(result)
Handling Duplicate Column Names
Python

import pandas as pd

df1 = pd.DataFrame({
    'key': ['A', 'B', 'C'],
    'value': [1, 2, 3]
})

df2 = pd.DataFrame({
    'key': ['A', 'B', 'C'],
    'value': [4, 5, 6]
})

print("DataFrame 1:")
print(df1)
print("\nDataFrame 2:")
print(df2)
print()

# Default suffixes
result = pd.merge(df1, df2, on='key')
print("With default suffixes (_x, _y):")
print(result)
print()

# Custom suffixes
result = pd.merge(df1, df2, on='key', suffixes=('_left', '_right'))
print("With custom suffixes:")
print(result)
14.4 Join (Index-Based)
Python

import pandas as pd

# DataFrames with meaningful indices
df1 = pd.DataFrame({
    'A': [1, 2, 3]
}, index=['a', 'b', 'c'])

df2 = pd.DataFrame({
    'B': [4, 5, 6]
}, index=['a', 'b', 'd'])

print("DataFrame 1:")
print(df1)
print("\nDataFrame 2:")
print(df2)
print()

# Join (default is left join on index)
result = df1.join(df2)
print("Left join on index:")
print(result)
print()

# Inner join
result = df1.join(df2, how='inner')
print("Inner join on index:")
print(result)
print()

# Outer join
result = df1.join(df2, how='outer')
print("Outer join on index:")
print(result)
14.5 Merge vs Join vs Concat
Python

"""
WHEN TO USE WHAT:

CONCAT:
- Stacking DataFrames vertically (more rows)
- Stacking DataFrames horizontally (more columns)
- No need to match on keys
- Example: Combining monthly data files

MERGE:
- Combining based on column values
- SQL-style joins (inner, outer, left, right)
- When you have foreign key relationships
- Example: Joining customers with orders

JOIN:
- Combining based on index
- Convenient when index is the join key
- Faster than merge for index joins
- Example: Time series data with same dates as index
"""

import pandas as pd

# Example showing all three

# CONCAT example
jan = pd.DataFrame({'sales': [100, 200]}, index=['A', 'B'])
feb = pd.DataFrame({'sales': [150, 250]}, index=['A', 'B'])
combined = pd.concat([jan, feb], keys=['Jan', 'Feb'])
print("CONCAT (stack monthly data):")
print(combined)
print()

# MERGE example
orders = pd.DataFrame({
    'order_id': [1, 2],
    'customer_id': [101, 102]
})
customers = pd.DataFrame({
    'customer_id': [101, 102],
    'name': ['Alice', 'Bob']
})
merged = pd.merge(orders, customers, on='customer_id')
print("MERGE (join on column):")
print(merged)
print()

# JOIN example
prices = pd.DataFrame({'price': [10, 20]}, index=['A', 'B'])
quantities = pd.DataFrame({'qty': [5, 3]}, index=['A', 'B'])
joined = prices.join(quantities)
print("JOIN (join on index):")
print(joined)
14.6 Combining Summary
Method	Use Case	Syntax
concat	Stack DataFrames	pd.concat([df1, df2])
concat axis=1	Add columns	pd.concat([df1, df2], axis=1)
merge inner	Match only	pd.merge(df1, df2, how='inner')
merge left	All from left	pd.merge(df1, df2, how='left')
merge right	All from right	pd.merge(df1, df2, how='right')
merge outer	All records	pd.merge(df1, df2, how='outer')
join	Index-based	df1.join(df2)
Chapter 15: Reshaping Data - Pivot and Melt
15.1 Understanding Wide vs Long Format
text

WIDE FORMAT (Human-readable)
┌────────┬─────────┬─────────┬─────────┐
│  Name  │  Jan    │  Feb    │  Mar    │
├────────┼─────────┼─────────┼─────────┤
│ Alice  │   100   │   150   │   200   │
│  Bob   │   120   │   180   │   220   │
└────────┴─────────┴─────────┴─────────┘

LONG FORMAT (Machine-friendly, better for analysis)
┌────────┬─────────┬─────────┐
│  Name  │  Month  │  Sales  │
├────────┼─────────┼─────────┤
│ Alice  │   Jan   │   100   │
│ Alice  │   Feb   │   150   │
│ Alice  │   Mar   │   200   │
│  Bob   │   Jan   │   120   │
│  Bob   │   Feb   │   180   │
│  Bob   │   Mar   │   220   │
└────────┴─────────┴─────────┘
15.2 Melt (Wide to Long)
Python

import pandas as pd

# Wide format data
df_wide = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Jan': [100, 120, 90],
    'Feb': [150, 180, 110],
    'Mar': [200, 220, 150]
})

print("Wide format:")
print(df_wide)
print()

# Melt to long format
df_long = pd.melt(df_wide, 
                  id_vars=['Name'],  # Columns to keep
                  value_vars=['Jan', 'Feb', 'Mar'],  # Columns to unpivot
                  var_name='Month',  # Name for the variable column
                  value_name='Sales')  # Name for the value column

print("Long format (melted):")
print(df_long)
print()

# Simplified melt (all non-id columns are melted)
df_long = df_wide.melt(id_vars=['Name'], var_name='Month', value_name='Sales')
print("Same result with simplified syntax:")
print(df_long)
15.3 Pivot (Long to Wide)
Python

import pandas as pd

# Long format data
df_long = pd.DataFrame({
    'Name': ['Alice', 'Alice', 'Alice', 'Bob', 'Bob', 'Bob'],
    'Month': ['Jan', 'Feb', 'Mar', 'Jan', 'Feb', 'Mar'],
    'Sales': [100, 150, 200, 120, 180, 220]
})

print("Long format:")
print(df_long)
print()

# Pivot to wide format
df_wide = df_long.pivot(index='Name', 
                        columns='Month', 
                        values='Sales')

print("Wide format (pivoted):")
print(df_wide)
print()

# Reset index to get regular DataFrame
df_wide = df_wide.reset_index()
df_wide.columns.name = None  # Remove the columns name
print("With reset index:")
print(df_wide)
15.4 Pivot Table (with Aggregation)
Python

import pandas as pd
import numpy as np

# Data with duplicates (multiple sales per person per month)
df = pd.DataFrame({
    'Name': ['Alice', 'Alice', 'Alice', 'Alice', 'Bob', 'Bob', 'Bob', 'Bob'],
    'Month': ['Jan', 'Jan', 'Feb', 'Feb', 'Jan', 'Jan', 'Feb', 'Feb'],
    'Sales': [100, 110, 150, 160, 120, 130, 180, 190]
})

print("Data with duplicates:")
print(df)
print()

# Regular pivot would fail due to duplicates
# Use pivot_table instead with aggregation

# Sum of sales
pivot_sum = pd.pivot_table(df, 
                           values='Sales', 
                           index='Name', 
                           columns='Month', 
                           aggfunc='sum')
print("Pivot table (sum):")
print(pivot_sum)
print()

# Mean of sales
pivot_mean = pd.pivot_table(df, 
                            values='Sales', 
                            index='Name', 
                            columns='Month', 
                            aggfunc='mean')
print("Pivot table (mean):")
print(pivot_mean)
print()

# Multiple aggregations
pivot_multi = pd.pivot_table(df, 
                             values='Sales', 
                             index='Name', 
                             columns='Month', 
                             aggfunc=['sum', 'mean', 'count'])
print("Pivot table (multiple aggregations):")
print(pivot_multi)
15.5 Stack and Unstack
Python

import pandas as pd

# Create a multi-index DataFrame
df = pd.DataFrame({
    ('Sales', 'Jan'): [100, 120],
    ('Sales', 'Feb'): [150, 180],
    ('Profit', 'Jan'): [20, 25],
    ('Profit', 'Feb'): [30, 35]
}, index=['Alice', 'Bob'])

print("Multi-column DataFrame:")
print(df)
print()

# Stack: Move column level to row index
stacked = df.stack()
print("Stacked (column to row):")
print(stacked)
print()

# Unstack: Move row index to column
unstacked = stacked.unstack()
print("Unstacked (row to column):")
print(unstacked)
print()

# Unstack specific level
print("Unstack level 0:")
print(stacked.unstack(level=0))
15.6 Practical Reshaping Example
Python

import pandas as pd
import numpy as np

# Sales data in database format (long)
sales_data = pd.DataFrame({
    'date': pd.date_range('2024-01-01', periods=12, freq='M'),
    'product': ['A', 'B'] * 6,
    'region': ['North', 'North', 'South', 'South'] * 3,
    'sales': np.random.randint(100, 500, 12)
})

print("Original sales data (long format):")
print(sales_data)
print()

# Create report: Products as columns, Regions as rows
report = pd.pivot_table(sales_data,
                        values='sales',
                        index='region',
                        columns='product',
                        aggfunc='sum',
                        margins=True)
print("Sales Report (wide format):")
print(report)
print()

# Create time series view
timeseries = pd.pivot_table(sales_data,
                            values='sales',
                            index='date',
                            columns='product',
                            aggfunc='sum')
print("Time Series View:")
print(timeseries)
15.7 Reshaping Summary
Operation	Method	Direction
Wide to Long	pd.melt()	Columns → Rows
Long to Wide	df.pivot()	Rows → Columns
Long to Wide (agg)	pd.pivot_table()	With aggregation
Column to Row Index	df.stack()	Columns → Index level
Row Index to Column	df.unstack()	Index level → Columns
Chapter 16: Multi-Index and Advanced Indexing
16.1 Creating Multi-Index
Python

import pandas as pd
import numpy as np

# Method 1: From tuples
index = pd.MultiIndex.from_tuples([
    ('A', 1), ('A', 2), ('B', 1), ('B', 2)
])
df = pd.DataFrame({'Value': [10, 20, 30, 40]}, index=index)
print("From tuples:")
print(df)
print()

# Method 2: From arrays
arrays = [
    ['A', 'A', 'B', 'B'],
    [1, 2, 1, 2]
]
index = pd.MultiIndex.from_arrays(arrays, names=['Letter', 'Number'])
df = pd.DataFrame({'Value': [10, 20, 30, 40]}, index=index)
print("From arrays with names:")
print(df)
print()

# Method 3: From product (all combinations)
index = pd.MultiIndex.from_product(
    [['A', 'B'], [1, 2, 3]],
    names=['Letter', 'Number']
)
df = pd.DataFrame({'Value': range(6)}, index=index)
print("From product:")
print(df)
print()

# Method 4: Using set_index on DataFrame
df = pd.DataFrame({
    'Letter': ['A', 'A', 'B', 'B'],
    'Number': [1, 2, 1, 2],
    'Value': [10, 20, 30, 40]
})
df_multi = df.set_index(['Letter', 'Number'])
print("Using set_index:")
print(df_multi)
16.2 Multi-Index Columns
Python

import pandas as pd
import numpy as np

# Create DataFrame with multi-level columns
columns = pd.MultiIndex.from_tuples([
    ('Sales', 'Q1'), ('Sales', 'Q2'),
    ('Profit', 'Q1'), ('Profit', 'Q2')
])

df = pd.DataFrame(
    np.random.randint(100, 500, (3, 4)),
    index=['Product A', 'Product B', 'Product C'],
    columns=columns
)

print("Multi-Index columns:")
print(df)
print()

# Access columns
print("Sales columns only:")
print(df['Sales'])
print()

print("Q1 from all categories:")
print(df.xs('Q1', level=1, axis=1))
16.3 Selecting from Multi-Index
Python

import pandas as pd
import numpy as np

# Create multi-index DataFrame
index = pd.MultiIndex.from_product(
    [['A', 'B', 'C'], [1, 2]],
    names=['Letter', 'Number']
)
df = pd.DataFrame({
    'Value1': np.random.randint(10, 100, 6),
    'Value2': np.random.randint(100, 200, 6)
}, index=index)

print("Multi-Index DataFrame:")
print(df)
print()

# Select by first level
print("Select Letter 'A':")
print(df.loc['A'])
print()

# Select by both levels
print("Select ('A', 1):")
print(df.loc[('A', 1)])
print()

# Select range in first level
print("Select 'A' to 'B':")
print(df.loc['A':'B'])
print()

# Cross-section with xs
print("Cross-section: Number = 1:")
print(df.xs(1, level='Number'))
print()

# Using slice(None) for "all"
print("All Letters, Number = 2:")
print(df.loc[(slice(None), 2), :])
16.4 Manipulating Multi-Index
Python

import pandas as pd
import numpy as np

# Create multi-index DataFrame
df = pd.DataFrame({
    'Letter': ['A', 'A', 'B', 'B'],
    'Number': [1, 2, 1, 2],
    'Value': [10, 20, 30, 40]
}).set_index(['Letter', 'Number'])

print("Original Multi-Index:")
print(df)
print()

# Reset all levels
print("reset_index() - All levels:")
print(df.reset_index())
print()

# Reset specific level
print("reset_index(level='Letter'):")
print(df.reset_index(level='Letter'))
print()

# Swap levels
print("swaplevel():")
print(df.swaplevel())
print()

# Sort index
df_unsorted = df.iloc[[3, 1, 0, 2]]
print("Unsorted:")
print(df_unsorted)
print("\nSorted:")
print(df_unsorted.sort_index())
16.5 Multi-Index Aggregation
Python

import pandas as pd
import numpy as np

# Create multi-index DataFrame
np.random.seed(42)
index = pd.MultiIndex.from_product(
    [['East', 'West'], ['2023', '2024'], ['Q1', 'Q2']],
    names=['Region', 'Year', 'Quarter']
)
df = pd.DataFrame({
    'Sales': np.random.randint(100, 500, 8),
    'Profit': np.random.randint(10, 100, 8)
}, index=index)

print("Multi-Index DataFrame:")
print(df)
print()

# Sum by first level
print("Sum by Region:")
print(df.groupby(level='Region').sum())
print()

# Sum by multiple levels
print("Sum by Region and Year:")
print(df.groupby(level=['Region', 'Year']).sum())
print()

# Mean across a level
print("Mean across Quarters (by Region and Year):")
print(df.groupby(level=['Region', 'Year']).mean())
Chapter 17: Window Functions and Rolling Calculations
17.1 Introduction to Window Functions
text

Window functions perform calculations across a set of rows
that are related to the current row.

┌─────────────────────────────────────────────────────────────┐
│                                                              │
│   Rolling Window (window=3)                                  │
│                                                              │
│   Data:  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]                    │
│                                                              │
│   Row 1:  [1] → Not enough data (NaN)                       │
│   Row 2:  [1, 2] → Not enough data (NaN)                    │
│   Row 3:  [1, 2, 3] → mean = 2                              │
│   Row 4:  [2, 3, 4] → mean = 3                              │
│   Row 5:  [3, 4, 5] → mean = 4                              │
│   ...                                                        │
│                                                              │
└─────────────────────────────────────────────────────────────┘
17.2 Rolling Windows
Python

import pandas as pd
import numpy as np

# Create time series data
np.random.seed(42)
dates = pd.date_range('2024-01-01', periods=20, freq='D')
df = pd.DataFrame({
    'Date': dates,
    'Value': np.random.randint(10, 100, 20)
})
df.set_index('Date', inplace=True)

print("Original Data (first 10 rows):")
print(df.head(10))
print()

# Rolling mean (moving average)
df['MA_3'] = df['Value'].rolling(window=3).mean()
df['MA_5'] = df['Value'].rolling(window=5).mean()
df['MA_7'] = df['Value'].rolling(window=7).mean()

print("With Moving Averages:")
print(df.head(10))
print()

# Other rolling statistics
df['Rolling_Sum'] = df['Value'].rolling(3).sum()
df['Rolling_Std'] = df['Value'].rolling(3).std()
df['Rolling_Min'] = df['Value'].rolling(3).min()
df['Rolling_Max'] = df['Value'].rolling(3).max()

print("Various Rolling Statistics:")
print(df[['Value', 'Rolling_Sum', 'Rolling_Std', 'Rolling_Min', 'Rolling_Max']].head(10))
17.3 Expanding Windows
Python

import pandas as pd
import numpy as np

# Create simple series
df = pd.DataFrame({
    'Value': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
})

print("Original:")
print(df)
print()

# Expanding mean (cumulative average)
df['Expanding_Mean'] = df['Value'].expanding().mean()
df['Expanding_Sum'] = df['Value'].expanding().sum()
df['Expanding_Max'] = df['Value'].expanding().max()

print("Expanding Statistics:")
print(df)

# Note: Expanding = Rolling with window from start to current row
17.4 Exponentially Weighted Moving Average (EWMA)
Python

import pandas as pd
import numpy as np

# Create data
df = pd.DataFrame({
    'Value': [10, 20, 30, 40, 50, 40, 30, 20, 10, 20]
})

print("Original:")
print(df['Value'].tolist())
print()

# EWMA - gives more weight to recent observations
df['EWM_span3'] = df['Value'].ewm(span=3).mean()
df['EWM_span5'] = df['Value'].ewm(span=5).mean()

# Compare with simple moving average
df['SMA_3'] = df['Value'].rolling(3).mean()

print("Comparison of EWMA vs SMA:")
print(df.round(2))

# EWMA is useful for:
# - Smoothing noisy data
# - Giving more importance to recent values
# - Financial time series analysis
17.5 Shift and Diff
Python

import pandas as pd

df = pd.DataFrame({
    'Value': [100, 110, 105, 120, 115, 130]
})

print("Original:")
print(df)
print()

# Shift: Move data up or down
df['Prev_Value'] = df['Value'].shift(1)   # Previous row
df['Next_Value'] = df['Value'].shift(-1)  # Next row

print("With shifted values:")
print(df)
print()

# Diff: Difference from previous row
df['Change'] = df['Value'].diff()         # Current - Previous
df['Change_2'] = df['Value'].diff(2)      # Current - 2 rows ago

print("With differences:")
print(df)
print()

# Percent change
df['Pct_Change'] = df['Value'].pct_change() * 100

print("With percent change:")
print(df.round(2))
17.6 Practical Example: Stock Analysis
Python

import pandas as pd
import numpy as np

# Simulated stock data
np.random.seed(42)
dates = pd.date_range('2024-01-01', periods=100, freq='D')
prices = 100 + np.cumsum(np.random.randn(100) * 2)

df = pd.DataFrame({
    'Date': dates,
    'Close': prices
})
df.set_index('Date', inplace=True)

print("Stock Data (first 10 rows):")
print(df.head(10))
print()

# Technical indicators
df['MA_7'] = df['Close'].rolling(7).mean()
df['MA_21'] = df['Close'].rolling(21).mean()
df['EMA_12'] = df['Close'].ewm(span=12).mean()
df['Daily_Return'] = df['Close'].pct_change() * 100
df['Volatility_7d'] = df['Daily_Return'].rolling(7).std()

# Bollinger Bands
df['BB_Middle'] = df['Close'].rolling(20).mean()
df['BB_Std'] = df['Close'].rolling(20).std()
df['BB_Upper'] = df['BB_Middle'] + 2 * df['BB_Std']
df['BB_Lower'] = df['BB_Middle'] - 2 * df['BB_Std']

print("Technical Analysis (last 10 rows):")
print(df[['Close', 'MA_7', 'MA_21', 'BB_Upper', 'BB_Lower']].tail(10).round(2))
Chapter 18: Categorical Data
18.1 Introduction to Categorical Data
Python

import pandas as pd

# Without categorical type (stored as strings)
df = pd.DataFrame({
    'Size': ['Small', 'Medium', 'Large', 'Small', 'Large', 'Medium'] * 1000
})

print("String dtype:")
print(f"Memory usage: {df['Size'].memory_usage(deep=True):,} bytes")
print(f"dtype: {df['Size'].dtype}")
print()

# Convert to categorical
df['Size_Cat'] = df['Size'].astype('category')

print("Categorical dtype:")
print(f"Memory usage: {df['Size_Cat'].memory_usage(deep=True):,} bytes")
print(f"dtype: {df['Size_Cat'].dtype}")
print()

# Memory savings can be significant!
18.2 Creating Categorical Data
Python

import pandas as pd

# Method 1: From existing data
df = pd.DataFrame({
    'Grade': ['A', 'B', 'A', 'C', 'B', 'A']
})
df['Grade'] = df['Grade'].astype('category')
print("Method 1 - From existing:")
print(df['Grade'])
print()

# Method 2: Using pd.Categorical
cat = pd.Categorical(['Low', 'Medium', 'High', 'Medium', 'Low'])
print("Method 2 - pd.Categorical:")
print(cat)
print()

# Method 3: With explicit categories
cat = pd.Categorical(
    ['Low', 'Medium', 'High', 'Medium'],
    categories=['Low', 'Medium', 'High', 'Very High'],  # All possible values
    ordered=True  # Has natural order
)
print("Method 3 - With explicit categories:")
print(cat)
print(f"Categories: {cat.categories.tolist()}")
18.3 Ordered Categorical Data
Python

import pandas as pd

# Create ordered categorical
sizes = pd.Categorical(
    ['M', 'L', 'S', 'XL', 'M', 'S'],
    categories=['XS', 'S', 'M', 'L', 'XL'],
    ordered=True
)

df = pd.DataFrame({'Size': sizes})
print("Ordered categorical:")
print(df)
print()

# Comparison operations work with ordered categories
print("Sizes >= 'M':")
print(df[df['Size'] >= 'M'])
print()

# Sorting respects the order
print("Sorted by size:")
print(df.sort_values('Size'))
print()

# Min and Max work correctly
print(f"Min size: {df['Size'].min()}")
print(f"Max size: {df['Size'].max()}")
18.4 Modifying Categories
Python

import pandas as pd

df = pd.DataFrame({
    'Grade': pd.Categorical(['A', 'B', 'C', 'A', 'B'])
})

print("Original:")
print(df['Grade'].cat.categories.tolist())
print()

# Add categories
df['Grade'] = df['Grade'].cat.add_categories(['D', 'F'])
print("After adding D, F:")
print(df['Grade'].cat.categories.tolist())
print()

# Remove unused categories
df['Grade'] = df['Grade'].cat.remove_unused_categories()
print("After removing unused:")
print(df['Grade'].cat.categories.tolist())
print()

# Rename categories
df['Grade'] = df['Grade'].cat.rename_categories({
    'A': 'Excellent',
    'B': 'Good',
    'C': 'Average'
})
print("After renaming:")
print(df)
18.5 Categorical and GroupBy
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Category': pd.Categorical(['A', 'B', 'A', 'B', 'A'], categories=['A', 'B', 'C']),
    'Value': [10, 20, 15, 25, 12]
})

print("DataFrame with unused category 'C':")
print(df)
print()

# GroupBy includes all categories (even unused)
print("GroupBy sum (observed=False):")
print(df.groupby('Category', observed=False)['Value'].sum())
print()

# Exclude unused categories
print("GroupBy sum (observed=True):")
print(df.groupby('Category', observed=True)['Value'].sum())
Chapter 19: Performance Optimization
19.1 Memory Optimization
Python

import pandas as pd
import numpy as np

# Create sample data
n = 100000
df = pd.DataFrame({
    'int_col': np.random.randint(0, 100, n),
    'float_col': np.random.random(n),
    'str_col': np.random.choice(['A', 'B', 'C', 'D'], n),
    'bool_col': np.random.choice([True, False], n)
})

print("Before optimization:")
print(df.dtypes)
print(f"Memory usage: {df.memory_usage(deep=True).sum() / 1024 / 1024:.2f} MB")
print()

# Optimization
def optimize_df(df):
    """Optimize DataFrame memory usage."""
    df_optimized = df.copy()
    
    for col in df_optimized.columns:
        col_type = df_optimized[col].dtype
        
        # Optimize integers
        if col_type == 'int64':
            if df_optimized[col].min() >= 0:
                if df_optimized[col].max() < 255:
                    df_optimized[col] = df_optimized[col].astype('uint8')
                elif df_optimized[col].max() < 65535:
                    df_optimized[col] = df_optimized[col].astype('uint16')
            else:
                if df_optimized[col].max() < 127:
                    df_optimized[col] = df_optimized[col].astype('int8')
                elif df_optimized[col].max() < 32767:
                    df_optimized[col] = df_optimized[col].astype('int16')
        
        # Optimize floats
        elif col_type == 'float64':
            df_optimized[col] = df_optimized[col].astype('float32')
        
        # Convert strings to category
        elif col_type == 'object':
            if df_optimized[col].nunique() / len(df_optimized) < 0.5:
                df_optimized[col] = df_optimized[col].astype('category')
    
    return df_optimized

df_opt = optimize_df(df)
print("After optimization:")
print(df_opt.dtypes)
print(f"Memory usage: {df_opt.memory_usage(deep=True).sum() / 1024 / 1024:.2f} MB")
19.2 Vectorization vs Loops
Python

import pandas as pd
import numpy as np
import time

n = 100000
df = pd.DataFrame({
    'A': np.random.random(n),
    'B': np.random.random(n)
})

# SLOW: Using a loop
start = time.time()
result_loop = []
for i in range(len(df)):
    result_loop.append(df.iloc[i]['A'] + df.iloc[i]['B'])
time_loop = time.time() - start
print(f"Loop time: {time_loop:.3f} seconds")

# FAST: Vectorized operation
start = time.time()
result_vec = df['A'] + df['B']
time_vec = time.time() - start
print(f"Vectorized time: {time_vec:.6f} seconds")

print(f"Speedup: {time_loop / time_vec:.0f}x faster")
19.3 Using eval() and query()
Python

import pandas as pd
import numpy as np

# For large DataFrames, eval() and query() can be faster
n = 1000000
df = pd.DataFrame({
    'A': np.random.random(n),
    'B': np.random.random(n),
    'C': np.random.random(n)
})

# Traditional way
result1 = df['A'] + df['B'] * df['C']

# Using eval (can be faster for large data)
result2 = df.eval('A + B * C')

# Query for filtering
# Traditional
filtered1 = df[(df['A'] > 0.5) & (df['B'] < 0.5)]

# Using query
filtered2 = df.query('A > 0.5 and B < 0.5')

print("Results are equal:", result1.equals(result2))
print("Filtered shapes:", filtered1.shape, filtered2.shape)
19.4 Chunked Processing
Python

import pandas as pd

# For very large files that don't fit in memory
# Read in chunks

"""
# Reading large file in chunks
chunk_size = 10000
chunks = []

for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    # Process each chunk
    processed = chunk[chunk['value'] > 0]  # Example filter
    chunks.append(processed)

# Combine results
result = pd.concat(chunks, ignore_index=True)
"""

# Example with iteration
def process_in_chunks(filename, chunk_size=10000):
    """Process large file in chunks."""
    result_list = []
    
    for chunk in pd.read_csv(filename, chunksize=chunk_size):
        # Apply any processing
        processed = chunk.groupby('category').sum()
        result_list.append(processed)
    
    # Combine chunk results
    final = pd.concat(result_list).groupby(level=0).sum()
    return final

print("Chunk processing pattern ready!")
19.5 Performance Tips Summary
Tip	Description
Use appropriate dtypes	int8/16/32 instead of int64
Use categorical for strings	Low cardinality strings → category
Avoid loops	Use vectorized operations
Use query() for filtering	More efficient for large DataFrames
Use eval() for expressions	Faster for complex expressions
Read in chunks	For files larger than memory
Use inplace=True carefully	Avoid for method chaining
Select columns early	Don't load unused columns
Chapter 20: Pandas for Machine Learning
20.1 Data Preparation Workflow
Python

import pandas as pd
import numpy as np

# Create sample ML dataset
np.random.seed(42)
n = 1000

df = pd.DataFrame({
    'age': np.random.randint(18, 80, n),
    'income': np.random.normal(50000, 20000, n).round(2),
    'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n),
    'city': np.random.choice(['NYC', 'LA', 'Chicago', 'Houston', 'Phoenix'], n),
    'purchased': np.random.choice([0, 1], n, p=[0.7, 0.3])
})

# Add some missing values
df.loc[np.random.choice(n, 50), 'income'] = np.nan
df.loc[np.random.choice(n, 30), 'age'] = np.nan

print("Raw Dataset:")
print(df.head(10))
print(f"\nShape: {df.shape}")
print(f"\nMissing values:\n{df.isnull().sum()}")
print(f"\nData types:\n{df.dtypes}")
20.2 Feature Engineering
Python

import pandas as pd
import numpy as np

# Using previous df
# Create new features

# Age groups
df['age_group'] = pd.cut(df['age'], 
                         bins=[0, 25, 35, 50, 65, 100],
                         labels=['18-25', '26-35', '36-50', '51-65', '65+'])

# Income bins
df['income_level'] = pd.qcut(df['income'].dropna(), 
                             q=4, 
                             labels=['Low', 'Medium', 'High', 'Very High'])

# Log transform for skewed data
df['log_income'] = np.log1p(df['income'].fillna(df['income'].median()))

# Interaction features
df['age_income'] = df['age'] * df['income']

print("With engineered features:")
print(df.head())
20.3 Encoding Categorical Variables
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'color': ['red', 'blue', 'green', 'red', 'blue'],
    'size': ['S', 'M', 'L', 'M', 'S'],
    'price': [10, 20, 30, 15, 25]
})

print("Original:")
print(df)
print()

# One-Hot Encoding
one_hot = pd.get_dummies(df, columns=['color', 'size'], prefix=['color', 'size'])
print("One-Hot Encoded:")
print(one_hot)
print()

# Label Encoding (for ordinal data)
size_order = {'S': 1, 'M': 2, 'L': 3}
df['size_encoded'] = df['size'].map(size_order)
print("Label Encoded size:")
print(df)
print()

# Using factorize
df['color_code'], color_labels = pd.factorize(df['color'])
print("Factorized color:")
print(df)
print(f"Labels: {color_labels.tolist()}")
20.4 Train-Test Split
Python

import pandas as pd
import numpy as np

# Create dataset
np.random.seed(42)
df = pd.DataFrame({
    'feature1': np.random.random(100),
    'feature2': np.random.random(100),
    'feature3': np.random.random(100),
    'target': np.random.choice([0, 1], 100)
})

# Manual train-test split
def train_test_split_df(df, test_size=0.2, random_state=None):
    """Split DataFrame into train and test sets."""
    if random_state:
        np.random.seed(random_state)
    
    # Shuffle indices
    indices = np.random.permutation(len(df))
    test_count = int(len(df) * test_size)
    
    test_indices = indices[:test_count]
    train_indices = indices[test_count:]
    
    return df.iloc[train_indices].reset_index(drop=True), \
           df.iloc[test_indices].reset_index(drop=True)

train_df, test_df = train_test_split_df(df, test_size=0.2, random_state=42)

print(f"Training set: {len(train_df)} rows")
print(f"Test set: {len(test_df)} rows")
print()

# Separate features and target
X_train = train_df.drop('target', axis=1)
y_train = train_df['target']
X_test = test_df.drop('target', axis=1)
y_test = test_df['target']

print(f"X_train shape: {X_train.shape}")
print(f"y_train shape: {y_train.shape}")
20.5 Scaling Features
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'age': [25, 30, 35, 40, 45],
    'income': [30000, 50000, 70000, 90000, 110000],
    'score': [0.5, 0.7, 0.6, 0.8, 0.9]
})

print("Original:")
print(df)
print()

# Min-Max Scaling (0-1)
def min_max_scale(df, columns):
    df_scaled = df.copy()
    for col in columns:
        min_val = df[col].min()
        max_val = df[col].max()
        df_scaled[col] = (df[col] - min_val) / (max_val - min_val)
    return df_scaled

df_minmax = min_max_scale(df, ['age', 'income', 'score'])
print("Min-Max Scaled:")
print(df_minmax)
print()

# Standard Scaling (Z-score)
def standard_scale(df, columns):
    df_scaled = df.copy()
    for col in columns:
        mean = df[col].mean()
        std = df[col].std()
        df_scaled[col] = (df[col] - mean) / std
    return df_scaled

df_standard = standard_scale(df, ['age', 'income', 'score'])
print("Standard Scaled:")
print(df_standard)
20.6 Complete ML Pipeline Example
Python

import pandas as pd
import numpy as np

# Complete preprocessing pipeline
class DataPipeline:
    def __init__(self):
        self.encoders = {}
        self.scalers = {}
        
    def fit_transform(self, df, target_col):
        """Fit and transform training data."""
        df_processed = df.copy()
        
        # Separate target
        y = df_processed.pop(target_col)
        
        # Handle missing values
        for col in df_processed.columns:
            if df_processed[col].dtype in ['float64', 'int64']:
                median = df_processed[col].median()
                self.scalers[f'{col}_median'] = median
                df_processed[col].fillna(median, inplace=True)
            else:
                mode = df_processed[col].mode()[0]
                self.encoders[f'{col}_mode'] = mode
                df_processed[col].fillna(mode, inplace=True)
        
        # Encode categorical
        cat_cols = df_processed.select_dtypes(include=['object']).columns
        df_processed = pd.get_dummies(df_processed, columns=cat_cols)
        self.columns = df_processed.columns.tolist()
        
        # Scale numerical
        num_cols = df.select_dtypes(include=['float64', 'int64']).columns
        num_cols = [c for c in num_cols if c != target_col]
        
        for col in num_cols:
            if col in df_processed.columns:
                mean = df_processed[col].mean()
                std = df_processed[col].std()
                self.scalers[f'{col}_mean'] = mean
                self.scalers[f'{col}_std'] = std
                df_processed[col] = (df_processed[col] - mean) / std
        
        return df_processed, y
    
    def transform(self, df):
        """Transform new data using fitted parameters."""
        df_processed = df.copy()
        
        # Handle missing values using stored values
        for col in df_processed.columns:
            if df_processed[col].dtype in ['float64', 'int64']:
                median = self.scalers.get(f'{col}_median')
                if median:
                    df_processed[col].fillna(median, inplace=True)
            else:
                mode = self.encoders.get(f'{col}_mode')
                if mode:
                    df_processed[col].fillna(mode, inplace=True)
        
        # Encode categorical
        cat_cols = df_processed.select_dtypes(include=['object']).columns
        df_processed = pd.get_dummies(df_processed, columns=cat_cols)
        
        # Ensure same columns as training
        for col in self.columns:
            if col not in df_processed.columns:
                df_processed[col] = 0
        df_processed = df_processed[self.columns]
        
        # Scale numerical
        for col in df_processed.columns:
            mean = self.scalers.get(f'{col}_mean')
            std = self.scalers.get(f'{col}_std')
            if mean is not None and std is not None:
                df_processed[col] = (df_processed[col] - mean) / std
        
        return df_processed

# Usage example
np.random.seed(42)
df = pd.DataFrame({
    'age': [25, 30, np.nan, 40, 45],
    'income': [30000, 50000, 70000, np.nan, 110000],
    'city': ['NYC', 'LA', 'NYC', 'Chicago', 'LA'],
    'purchased': [0, 1, 1, 0, 1]
})

print("Original data:")
print(df)
print()

pipeline = DataPipeline()
X_processed, y = pipeline.fit_transform(df, 'purchased')

print("Processed features:")
print(X_processed)
print()
print("Target:")
print(y.tolist())
Chapter 21: Real-World Projects and Exercises
21.1 Project 1: Sales Data Analysis
Python

import pandas as pd
import numpy as np

# Generate realistic sales data
np.random.seed(42)
n_records = 1000

sales_data = pd.DataFrame({
    'order_date': pd.date_range('2023-01-01', periods=n_records, freq='4H'),
    'product_id': np.random.choice(['P001', 'P002', 'P003', 'P004', 'P005'], n_records),
    'category': np.random.choice(['Electronics', 'Clothing', 'Home', 'Sports'], n_records),
    'region': np.random.choice(['North', 'South', 'East', 'West'], n_records),
    'quantity': np.random.randint(1, 10, n_records),
    'unit_price': np.random.choice([19.99, 29.99, 49.99, 99.99, 149.99], n_records),
    'customer_id': np.random.randint(1000, 2000, n_records)
})

sales_data['revenue'] = sales_data['quantity'] * sales_data['unit_price']

print("="*60)
print("SALES DATA ANALYSIS")
print("="*60)

print("\n1. Dataset Overview:")
print(sales_data.head())
print(f"\nShape: {sales_data.shape}")
print(f"\nDate Range: {sales_data['order_date'].min()} to {sales_data['order_date'].max()}")

print("\n2. Revenue Summary:")
print(f"   Total Revenue: ${sales_data['revenue'].sum():,.2f}")
print(f"   Average Order Value: ${sales_data['revenue'].mean():.2f}")
print(f"   Median Order Value: ${sales_data['revenue'].median():.2f}")

print("\n3. Revenue by Category:")
print(sales_data.groupby('category')['revenue'].agg(['sum', 'mean', 'count']).round(2))

print("\n4. Revenue by Region:")
print(sales_data.groupby('region')['revenue'].sum().sort_values(ascending=False))

print("\n5. Monthly Revenue Trend:")
monthly = sales_data.set_index('order_date').resample('M')['revenue'].sum()
print(monthly)

print("\n6. Top Products by Revenue:")
print(sales_data.groupby('product_id')['revenue'].sum().sort_values(ascending=False))

print("\n7. Customer Analysis:")
customer_stats = sales_data.groupby('customer_id').agg({
    'revenue': 'sum',
    'order_date': 'count'
}).rename(columns={'order_date': 'order_count'})
print(f"   Unique Customers: {sales_data['customer_id'].nunique()}")
print(f"   Avg Orders per Customer: {customer_stats['order_count'].mean():.2f}")
print(f"   Avg Revenue per Customer: ${customer_stats['revenue'].mean():.2f}")
21.2 Project 2: Customer Churn Analysis
Python

import pandas as pd
import numpy as np

# Generate customer data
np.random.seed(42)
n_customers = 500

customers = pd.DataFrame({
    'customer_id': range(1, n_customers + 1),
    'age': np.random.randint(18, 70, n_customers),
    'tenure_months': np.random.randint(1, 72, n_customers),
    'monthly_charges': np.random.uniform(20, 100, n_customers).round(2),
    'total_charges': np.random.uniform(100, 5000, n_customers).round(2),
    'contract': np.random.choice(['Month-to-month', 'One year', 'Two year'], n_customers, 
                                 p=[0.5, 0.3, 0.2]),
    'payment_method': np.random.choice(['Credit card', 'Bank transfer', 'Electronic check'], n_customers),
    'num_support_tickets': np.random.poisson(2, n_customers),
    'churned': np.random.choice([0, 1], n_customers, p=[0.75, 0.25])
})

print("="*60)
print("CUSTOMER CHURN ANALYSIS")
print("="*60)

print("\n1. Dataset Overview:")
print(customers.info())
print(customers.describe())

print("\n2. Churn Rate:")
churn_rate = customers['churned'].mean() * 100
print(f"   Overall Churn Rate: {churn_rate:.1f}%")

print("\n3. Churn by Contract Type:")
contract_churn = customers.groupby('contract')['churned'].agg(['mean', 'count'])
contract_churn['mean'] = (contract_churn['mean'] * 100).round(1)
contract_churn.columns = ['Churn Rate %', 'Count']
print(contract_churn)

print("\n4. Churn by Tenure Groups:")
customers['tenure_group'] = pd.cut(customers['tenure_months'], 
                                   bins=[0, 12, 24, 48, 100],
                                   labels=['0-12', '13-24', '25-48', '49+'])
tenure_churn = customers.groupby('tenure_group')['churned'].mean() * 100
print(tenure_churn.round(1))

print("\n5. Churned vs Non-Churned Customer Comparison:")
comparison = customers.groupby('churned').agg({
    'monthly_charges': 'mean',
    'tenure_months': 'mean',
    'num_support_tickets': 'mean',
    'age': 'mean'
}).round(2)
comparison.index = ['Retained', 'Churned']
print(comparison)

print("\n6. Risk Factors (High churn correlation):")
# Calculate correlation of numeric features with churn
numeric_cols = customers.select_dtypes(include=[np.number]).columns
correlations = customers[numeric_cols].corrwith(customers['churned']).drop('churned')
print(correlations.sort_values(ascending=False))
21.3 Exercises
Exercise 1: Basic Operations
Python

"""
EXERCISE 1: DataFrame Basics

Given the following data, complete the tasks:
"""

import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank'],
    'Age': [25, 30, 35, 28, 32, 45],
    'Department': ['Sales', 'Engineering', 'Engineering', 'HR', 'Sales', 'HR'],
    'Salary': [50000, 80000, 90000, 55000, 60000, 75000],
    'Years': [2, 5, 8, 3, 4, 15]
}
df = pd.DataFrame(data)

# Task 1: Display employees over 30 years old
print("Task 1 - Employees over 30:")
print(df[df['Age'] > 30])
print()

# Task 2: Calculate average salary by department
print("Task 2 - Average salary by department:")
print(df.groupby('Department')['Salary'].mean())
print()

# Task 3: Find the employee with the highest salary
print("Task 3 - Highest salary employee:")
print(df.loc[df['Salary'].idxmax()])
print()

# Task 4: Add a 'Bonus' column (10% of salary)
df['Bonus'] = df['Salary'] * 0.10
print("Task 4 - With Bonus column:")
print(df)
print()

# Task 5: Sort by Years of experience (descending)
print("Task 5 - Sorted by Years (descending):")
print(df.sort_values('Years', ascending=False))
Exercise 2: Data Cleaning
Python

"""
EXERCISE 2: Data Cleaning

Clean the following messy dataset:
"""

import pandas as pd
import numpy as np

# Messy data
messy_data = pd.DataFrame({
    'name': ['  alice  ', 'BOB', 'charlie', 'DIANA', None, 'eve'],
    'age': [25, 30, -5, 150, 28, np.nan],  # -5 and 150 are invalid
    'email': ['alice@mail.com', 'bob@mail', 'charlie@mail.com', 
              'diana@mail.com', 'eve@mail.com', 'invalid'],
    'salary': ['50000', '60,000', '70000', 'N/A', '55000', '65000']
})

print("Original messy data:")
print(messy_data)
print()

# Solution
df = messy_data.copy()

# Clean name: strip whitespace and title case
df['name'] = df['name'].str.strip().str.title()

# Handle age: Replace invalid values with NaN
df.loc[~df['age'].between(0, 120), 'age'] = np.nan

# Clean salary: Remove commas, convert to numeric
df['salary'] = df['salary'].str.replace(',', '').replace('N/A', np.nan)
df['salary'] = pd.to_numeric(df['salary'], errors='coerce')

# Validate email: Check for @ symbol
df['email_valid'] = df['email'].str.contains('@', na=False)

print("Cleaned data:")
print(df)
Exercise 3: Time Series Analysis
Python

"""
EXERCISE 3: Time Series Analysis

Analyze the following daily temperature data:
"""

import pandas as pd
import numpy as np

# Generate temperature data
np.random.seed(42)
dates = pd.date_range('2024-01-01', periods=365, freq='D')
temps = 15 + 10 * np.sin(np.arange(365) * 2 * np.pi / 365) + np.random.randn(365) * 3

df = pd.DataFrame({
    'date': dates,
    'temperature': temps.round(1)
})
df.set_index('date', inplace=True)

print("Temperature Data (first 10 days):")
print(df.head(10))
print()

# Task 1: Calculate monthly average temperature
print("Task 1 - Monthly averages:")
print(df.resample('M')['temperature'].mean().round(1))
print()

# Task 2: Find the hottest and coldest days
print("Task 2 - Extreme temperatures:")
print(f"Hottest day: {df['temperature'].idxmax()} ({df['temperature'].max():.1f}°C)")
print(f"Coldest day: {df['temperature'].idxmin()} ({df['temperature'].min():.1f}°C)")
print()

# Task 3: Calculate 7-day moving average
df['MA_7'] = df['temperature'].rolling(7).mean()
print("Task 3 - With 7-day moving average:")
print(df.head(10))
print()

# Task 4: Find days with temperature > 2 standard deviations from mean
mean_temp = df['temperature'].mean()
std_temp = df['temperature'].std()
unusual_days = df[abs(df['temperature'] - mean_temp) > 2 * std_temp]
print(f"Task 4 - Unusual temperature days: {len(unusual_days)}")
print(unusual_days)
Chapter 22: Best Practices and Common Pitfalls
22.1 Common Pitfalls to Avoid
Pitfall 1: SettingWithCopyWarning
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': [10, 20, 30, 40, 50]
})

# WRONG: Chained indexing (may not work as expected)
# df[df['A'] > 2]['B'] = 100  # SettingWithCopyWarning!

# CORRECT: Use .loc
df.loc[df['A'] > 2, 'B'] = 100
print("Correct way using .loc:")
print(df)
Pitfall 2: Modifying a View vs Copy
Python

import pandas as pd

df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
})

# This creates a VIEW (changes affect original!)
subset = df[df['A'] > 1]
# subset['B'] = 100  # May modify df!


# CORRECT: Use .copy() when you need independence
subset = df[df['A'] > 1].copy()
subset['B'] = 100  # Safe - doesn't affect original df
print("Original df unchanged:")
print(df)
print("\nModified subset:")
print(subset)
Pitfall 3: Using Python's and/or Instead of &/|
Python

import pandas as pd

df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': [10, 20, 30, 40, 50]
})

# WRONG: Python's 'and' doesn't work with Series
# df[(df['A'] > 2) and (df['B'] < 40)]  # ValueError!

# CORRECT: Use & for AND, | for OR, ~ for NOT
# AND always wrap conditions in parentheses!
result = df[(df['A'] > 2) & (df['B'] < 40)]
print("Using & (correct):")
print(result)

# OR example
result = df[(df['A'] < 2) | (df['A'] > 4)]
print("\nUsing | (OR):")
print(result)

# NOT example
result = df[~(df['A'] > 3)]
print("\nUsing ~ (NOT):")
print(result)
Pitfall 4: Forgetting inplace Doesn't Return Anything
Python

import pandas as pd

df = pd.DataFrame({
    'A': [3, 1, 2],
    'B': [6, 4, 5]
})

# WRONG: inplace=True returns None!
result = df.sort_values('A', inplace=True)
print(f"Result of inplace operation: {result}")  # None!

# Reset for demonstration
df = pd.DataFrame({'A': [3, 1, 2], 'B': [6, 4, 5]})

# CORRECT Option 1: Don't use inplace, reassign
df = df.sort_values('A')
print("Reassigned result:")
print(df)

# CORRECT Option 2: Use inplace without assignment
df = pd.DataFrame({'A': [3, 1, 2], 'B': [6, 4, 5]})
df.sort_values('A', inplace=True)  # No assignment needed
print("\nUsing inplace correctly:")
print(df)
Pitfall 5: Comparing with NaN
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, np.nan, 3, np.nan, 5]
})

# WRONG: NaN == NaN is False!
print("df['A'] == np.nan:")
print(df['A'] == np.nan)  # All False!

# CORRECT: Use isna() or isnull()
print("\ndf['A'].isna():")
print(df['A'].isna())

# CORRECT: Use notna() for non-null
print("\ndf['A'].notna():")
print(df['A'].notna())

# Filter correctly
print("\nRows where A is null:")
print(df[df['A'].isna()])
Pitfall 6: Losing Index After Operations
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Score': [85, 90, 78]
}, index=['a', 'b', 'c'])

print("Original with custom index:")
print(df)
print()

# After some operations, index might not be what you expect
filtered = df[df['Score'] > 80]
print("After filtering (index preserved):")
print(filtered)
print()

# Reset index when needed
filtered_reset = df[df['Score'] > 80].reset_index(drop=True)
print("After reset_index(drop=True):")
print(filtered_reset)
Pitfall 7: Integer vs Float Index After Missing Data
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4.0, np.nan, 6.0]
})

print("Original dtypes:")
print(df.dtypes)
print()

# Integer columns with missing values become float64
df.loc[1, 'A'] = np.nan
print("After adding NaN to integer column:")
print(df.dtypes)
print(df)

# Use nullable integer dtype to keep int with NaN
df = pd.DataFrame({
    'A': pd.array([1, 2, 3], dtype='Int64'),  # Nullable integer
    'B': [4.0, np.nan, 6.0]
})
df.loc[1, 'A'] = pd.NA
print("\nWith nullable Int64:")
print(df.dtypes)
print(df)
22.2 Best Practices
Practice 1: Method Chaining
Python

import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'name': ['  alice  ', '  BOB  ', '  charlie  '],
    'age': [25, 30, 35],
    'salary': [50000, 60000, 70000]
})

# BAD: Multiple intermediate variables
# df1 = df.copy()
# df1['name'] = df1['name'].str.strip()
# df1['name'] = df1['name'].str.title()
# df1 = df1[df1['age'] > 25]
# df1 = df1.sort_values('salary')
# result = df1

# GOOD: Method chaining
result = (df
    .assign(name=lambda x: x['name'].str.strip().str.title())
    .query('age > 25')
    .sort_values('salary')
    .reset_index(drop=True)
)

print("Result of method chaining:")
print(result)
Practice 2: Use Explicit Column Selection
Python

import pandas as pd

df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9],
    'D': [10, 11, 12]
})

# BAD: Selecting by position (fragile if columns change)
# result = df.iloc[:, 0:2]

# GOOD: Explicit column names
result = df[['A', 'B']]
print("Explicit column selection:")
print(result)

# GOOD: Using filter for pattern matching
result = df.filter(like='A')  # Columns containing 'A'
print("\nUsing filter:")
print(result)

result = df.filter(regex='^[AB]')  # Columns starting with A or B
print("\nUsing filter with regex:")
print(result)
Practice 3: Handle Missing Data Explicitly
Python

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, np.nan, 3, np.nan, 5],
    'B': [np.nan, 2, np.nan, 4, 5]
})

print("Original with NaN:")
print(df)
print()

# Always check for missing data
print("Missing data summary:")
print(df.isnull().sum())
print()

# Be explicit about how you handle NaN
# Option 1: Fill with specific value
df_filled = df.fillna({'A': df['A'].median(), 'B': 0})
print("After explicit fill:")
print(df_filled)

# Option 2: Drop with clear criteria
df_dropped = df.dropna(subset=['A'])  # Drop only if A is null
print("\nAfter dropping rows with null A:")
print(df_dropped)
Practice 4: Use Appropriate Data Types
Python

import pandas as pd
import numpy as np

# Create DataFrame
n = 100000
df = pd.DataFrame({
    'id': range(n),
    'category': np.random.choice(['A', 'B', 'C', 'D'], n),
    'value': np.random.randint(0, 100, n),
    'amount': np.random.random(n)
})

print("Before optimization:")
print(df.dtypes)
print(f"Memory: {df.memory_usage(deep=True).sum() / 1024 / 1024:.2f} MB")
print()

# Optimize
df_opt = df.copy()
df_opt['id'] = df_opt['id'].astype('int32')
df_opt['category'] = df_opt['category'].astype('category')
df_opt['value'] = df_opt['value'].astype('int8')
df_opt['amount'] = df_opt['amount'].astype('float32')

print("After optimization:")
print(df_opt.dtypes)
print(f"Memory: {df_opt.memory_usage(deep=True).sum() / 1024 / 1024:.2f} MB")
Practice 5: Document Your Data Transformations
Python

import pandas as pd
import numpy as np

def clean_customer_data(df):
    """
    Clean and prepare customer data for analysis.
    
    Transformations:
    1. Remove duplicate customer IDs (keep last record)
    2. Clean name field (strip whitespace, title case)
    3. Replace invalid ages (<0 or >120) with NaN
    4. Convert signup_date to datetime
    5. Create customer tenure in days
    
    Parameters:
    -----------
    df : DataFrame
        Raw customer data with columns: customer_id, name, age, signup_date
        
    Returns:
    --------
    DataFrame
        Cleaned customer data with additional tenure_days column
    """
    df_clean = (df
        .drop_duplicates(subset=['customer_id'], keep='last')
        .assign(
            name=lambda x: x['name'].str.strip().str.title(),
            age=lambda x: x['age'].where(x['age'].between(0, 120)),
            signup_date=lambda x: pd.to_datetime(x['signup_date']),
            tenure_days=lambda x: (pd.Timestamp.now() - pd.to_datetime(x['signup_date'])).dt.days
        )
    )
    
    return df_clean

# Example usage
df = pd.DataFrame({
    'customer_id': [1, 2, 3, 2],  # Duplicate ID
    'name': ['  alice  ', 'BOB', '  charlie  ', 'bob updated'],
    'age': [25, -5, 150, 30],  # Invalid ages
    'signup_date': ['2023-01-15', '2022-06-20', '2024-01-01', '2023-08-10']
})

print("Original data:")
print(df)
print()

cleaned = clean_customer_data(df)
print("Cleaned data:")
print(cleaned)
Practice 6: Write Reusable Functions
Python

import pandas as pd
import numpy as np

def create_summary_stats(df, group_col, value_col):
    """
    Create comprehensive summary statistics by group.
    
    Parameters:
    -----------
    df : DataFrame
        Input data
    group_col : str
        Column to group by
    value_col : str
        Column to calculate statistics for
        
    Returns:
    --------
    DataFrame
        Summary statistics including count, mean, median, std, min, max
    """
    summary = df.groupby(group_col)[value_col].agg([
        ('count', 'count'),
        ('mean', 'mean'),
        ('median', 'median'),
        ('std', 'std'),
        ('min', 'min'),
        ('max', 'max'),
        ('sum', 'sum')
    ]).round(2)
    
    # Add percentage of total
    summary['pct_of_total'] = (summary['sum'] / summary['sum'].sum() * 100).round(1)
    
    return summary.sort_values('sum', ascending=False)

# Example usage
df = pd.DataFrame({
    'region': np.random.choice(['North', 'South', 'East', 'West'], 100),
    'sales': np.random.randint(100, 1000, 100)
})

print("Sales Summary by Region:")
print(create_summary_stats(df, 'region', 'sales'))
Practice 7: Use Context Managers for Display Options
Python

import pandas as pd
import numpy as np

# Create a large DataFrame
df = pd.DataFrame(np.random.randn(100, 20))

# Temporarily change display options
with pd.option_context('display.max_rows', 10, 
                       'display.max_columns', 5,
                       'display.precision', 2):
    print("With limited display:")
    print(df)

# Options are restored after the with block
print("\nOriginal options restored")
print(f"Max rows: {pd.get_option('display.max_rows')}")
22.3 Performance Best Practices Summary
Do This	Instead of This	Why
df.loc[condition, col] = value	Chained indexing	Avoids SettingWithCopyWarning
df['col'].isna()	df['col'] == np.nan	NaN != NaN
(cond1) & (cond2)	cond1 and cond2	Proper elementwise logic
.copy() when modifying	Direct assignment	Prevents unintended modifications
Method chaining	Multiple variables	Cleaner, more readable code
Explicit column names	Position-based selection	More maintainable
query() for filtering	Complex boolean indexing	More readable
Categorical for repeated strings	Object dtype	Memory efficient
to_datetime() once	Multiple parse calls	Parse dates at load time
Vectorized operations	For loops	Much faster
22.4 Debugging Tips
Python

import pandas as pd
import numpy as np

# Tip 1: Check intermediate results
df = pd.DataFrame({
    'A': [1, 2, 3, 4, 5],
    'B': ['a', 'b', 'c', 'd', 'e']
})

# Debug by breaking chain
result = df[df['A'] > 2]
print("After filtering:", len(result), "rows")

# Tip 2: Use .info() and .describe()
print("\nDataFrame info:")
df.info()

print("\nStatistics:")
print(df.describe(include='all'))

# Tip 3: Check for duplicates
print(f"\nDuplicate rows: {df.duplicated().sum()}")

# Tip 4: Verify dtypes after operations
print(f"\nColumn types: {df.dtypes.to_dict()}")

# Tip 5: Sample for large DataFrames
# df.sample(5)  # Random sample for inspection
Quick Reference Card
Creating DataFrames
Python

pd.DataFrame(dict)           # From dictionary
pd.DataFrame(list_of_dicts)  # From list of dicts
pd.read_csv('file.csv')      # From CSV
pd.read_excel('file.xlsx')   # From Excel
pd.read_json('file.json')    # From JSON
pd.read_sql(query, conn)     # From SQL
Viewing Data
Python

df.head(n)        # First n rows
df.tail(n)        # Last n rows
df.sample(n)      # Random n rows
df.shape          # (rows, columns)
df.info()         # Column info
df.describe()     # Statistics
df.dtypes         # Data types
df.columns        # Column names
df.index          # Row index
Selection
Python

df['col']                     # Single column (Series)
df[['col1', 'col2']]          # Multiple columns (DataFrame)
df.loc[label]                 # Row by label
df.iloc[position]             # Row by position
df.loc[row, col]              # Cell by label
df.iloc[row_idx, col_idx]     # Cell by position
df.at[row, col]               # Fast single cell by label
df.iat[row_idx, col_idx]      # Fast single cell by position
Filtering
Python

df[df['col'] > value]                    # Comparison
df[(cond1) & (cond2)]                    # AND
df[(cond1) | (cond2)]                    # OR
df[~condition]                           # NOT
df[df['col'].isin([val1, val2])]         # In list
df[df['col'].between(low, high)]         # Range
df[df['col'].str.contains('text')]       # String contains
df.query('col > value')                  # Query string
Data Cleaning
Python

df.dropna()                   # Drop rows with NaN
df.fillna(value)              # Fill NaN
df.drop_duplicates()          # Remove duplicates
df.rename(columns={})         # Rename columns
df.astype(dtype)              # Change dtype
df.replace(old, new)          # Replace values
df['col'].str.strip()         # Strip whitespace
df['col'].str.lower()         # Lowercase
pd.to_datetime(df['col'])     # Convert to datetime
Aggregation
Python

df.sum()                      # Sum
df.mean()                     # Mean
df.median()                   # Median
df.std()                      # Standard deviation
df.min() / df.max()           # Min/Max
df.count()                    # Count non-null
df.nunique()                  # Unique count
df.value_counts()             # Frequency count
df.agg(['sum', 'mean'])       # Multiple aggregations
GroupBy
Python

df.groupby('col').mean()                       # Group and aggregate
df.groupby(['c1', 'c2']).agg({})               # Multiple columns
df.groupby('col').transform(func)              # Transform (same size)
df.groupby('col').filter(func)                 # Filter groups
df.groupby('col').apply(func)                  # Custom function
pd.pivot_table(df, values, index, columns)     # Pivot table
Reshaping
Python

pd.melt(df, id_vars, value_vars)     # Wide to long
df.pivot(index, columns, values)     # Long to wide
pd.concat([df1, df2])                # Stack vertically
pd.concat([df1, df2], axis=1)        # Stack horizontally
pd.merge(df1, df2, on='key')         # Join on column
df1.join(df2)                        # Join on index
Time Series
Python

pd.to_datetime(df['col'])            # Parse dates
pd.date_range(start, periods, freq)  # Date range
df['col'].dt.year / .month / .day    # Extract components
df.resample('D').mean()              # Resample
df['col'].shift(1)                   # Shift values
df['col'].diff()                     # Difference
df['col'].rolling(n).mean()          # Rolling window
df['col'].ewm(span=n).mean()         # Exponential weighted
Saving Data
Python

df.to_csv('file.csv', index=False)
df.to_excel('file.xlsx', index=False)
df.to_json('file.json')
df.to_parquet('file.parquet')
df.to_sql('table', connection)
Conclusion
Congratulations! 🎉 You have completed the comprehensive Pandas guide covering:

✅ Fundamentals: Series and DataFrames
✅ Data I/O: Loading and saving data in various formats
✅ Selection & Indexing: loc, iloc, and boolean indexing
✅ Data Cleaning: Handling missing data, duplicates, and type conversion
✅ Transformation: Apply, map, and data manipulation
✅ String Operations: Text processing and pattern matching
✅ DateTime: Time series analysis and manipulation
✅ Aggregation: GroupBy, pivot tables, and summary statistics
✅ Merging: Combining datasets with merge, join, and concat
✅ Reshaping: Pivot and melt operations
✅ Advanced Topics: Multi-index, window functions, categorical data
✅ Performance: Memory optimization and efficient operations
✅ ML Preparation: Feature engineering and preprocessing
✅ Best Practices: Writing clean, maintainable code
Your ML Journey with Pandas:

text

┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│   PANDAS MASTERY ACHIEVED! 🏆                                   │
│                                                                  │
│   You can now:                                                   │
│   ✓ Load and explore any dataset                                │
│   ✓ Clean and preprocess data effectively                      │
│   ✓ Transform and engineer features                            │
│   ✓ Analyze and summarize data                                  │
│   ✓ Prepare data for machine learning                          │
│   ✓ Write efficient, maintainable code                         │
│                                                                  │
│   Next Steps:                                                    │
│   → Practice with real datasets                                  │
│   → Learn Matplotlib/Seaborn for visualization                  │
│   → Move to Scikit-learn for ML models                          │
│   → Explore deep learning with TensorFlow/PyTorch               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
Remember: Pandas is the foundation of data science in Python. Master it, and everything else becomes easier!

This guide was created to provide crystal-clear understanding of Pandas from beginner to advanced level. Happy data wrangling! 🐼🚀