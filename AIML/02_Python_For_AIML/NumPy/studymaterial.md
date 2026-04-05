The Complete NumPy Mastery Guide
From Absolute Beginner to Advanced Practitioner
Table of Contents
Introduction - What is NumPy and Why Should You Care?
Installation and Setup
Understanding Arrays - The Heart of NumPy
Creating Arrays - Every Possible Way
Array Attributes - Know Your Arrays
Indexing and Slicing - Accessing Your Data
Array Shape Manipulation
Array Operations - The Power of Vectorization
Broadcasting - The Magic Behind NumPy
Universal Functions (ufuncs)
Aggregation and Statistical Functions
Linear Algebra with NumPy
Random Number Generation
File Input/Output Operations
Advanced Indexing Techniques
Memory Layout and Performance
Structured Arrays and Record Arrays
NumPy for Machine Learning
Best Practices and Common Pitfalls
Real-World Projects and Exercises
Chapter 1: Introduction - What is NumPy and Why Should You Care?
1.1 The Story of NumPy
Imagine you're a chef. You could chop vegetables one by one with a small knife, OR you could use a professional food processor that handles everything at once, faster and more efficiently.

NumPy is that food processor for numerical data in Python.

What Does NumPy Stand For?
Numerical Python = NumPy

The Problem NumPy Solves
Let's understand with a simple example:

Without NumPy (Pure Python):

Python

# Adding two lists of 1 million numbers each
list1 = [1, 2, 3, ..., 1000000]
list2 = [1, 2, 3, ..., 1000000]

# You would need a loop
result = []
for i in range(len(list1)):
    result.append(list1[i] + list2[i])

# This takes ~0.5 seconds
With NumPy:

Python

import numpy as np

arr1 = np.array([1, 2, 3, ..., 1000000])
arr2 = np.array([1, 2, 3, ..., 1000000])

result = arr1 + arr2  # Just this!

# This takes ~0.005 seconds (100x faster!)
1.2 Why is NumPy So Fast?
Three main reasons:

Reason 1: Contiguous Memory Storage
text

Python List:
┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐
│ Ptr │───>│  1  │    │ Ptr │───>│  2  │  (scattered in memory)
└─────┘    └─────┘    └─────┘    └─────┘

NumPy Array:
┌─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  (continuous block in memory)
└─────┴─────┴─────┴─────┘
Reason 2: Homogeneous Data Types
text

Python List:          NumPy Array:
[1, "hello", 3.14]    [1, 2, 3, 4]  ← All same type (integers)
↑
Different types = More checks = Slower
Reason 3: Written in C
NumPy operations are implemented in C, which is much faster than Python.

1.3 NumPy in the ML/AI Ecosystem
text

                    ┌─────────────────────────────────────────┐
                    │           ML/AI ECOSYSTEM               │
                    └─────────────────────────────────────────┘
                                        │
        ┌───────────────────────────────┼───────────────────────────────┐
        │                               │                               │
        ▼                               ▼                               ▼
┌───────────────┐               ┌───────────────┐               ┌───────────────┐
│  TensorFlow   │               │    PyTorch    │               │   Scikit-     │
│               │               │               │               │   Learn       │
└───────────────┘               └───────────────┘               └───────────────┘
        │                               │                               │
        └───────────────────────────────┼───────────────────────────────┘
                                        │
                                        ▼
                            ┌───────────────────────┐
                            │        PANDAS         │
                            │   (Data Manipulation) │
                            └───────────────────────┘
                                        │
                                        ▼
                            ┌───────────────────────┐
                            │        NumPy          │
                            │    (THE FOUNDATION)   │
                            └───────────────────────┘
Everything is built on NumPy!

1.4 Key Terminology You Must Know
Term	Meaning	Example
Array	A collection of elements of the same type	[1, 2, 3, 4, 5]
ndarray	N-dimensional array (NumPy's main object)	1D, 2D, 3D... arrays
Element	A single value in an array	3 in [1, 2, 3]
Axis	A dimension of the array	Row = axis 0, Column = axis 1
Shape	Size of array in each dimension	(3, 4) = 3 rows, 4 columns
Dtype	Data type of elements	int32, float64, etc.
Vectorization	Operating on entire arrays without loops	arr * 2
Broadcasting	Rules for operations on different-shaped arrays	Adding (3,3) and (3,)
Chapter 2: Installation and Setup
2.1 Installing NumPy
Method 1: Using pip (Recommended for beginners)
Bash

pip install numpy
Method 2: Using conda (If you use Anaconda)
Bash

conda install numpy
Method 3: Installing specific version
Bash

pip install numpy==1.24.0
2.2 Verifying Installation
Python

import numpy as np

# Check version
print(np.__version__)  # Output: 1.24.0 (or your version)

# Quick test
arr = np.array([1, 2, 3])
print(arr)  # Output: [1 2 3]

print("NumPy is working perfectly! ✓")
2.3 The Import Convention
Python

import numpy as np  # ← ALWAYS use this convention
Why np?

It's the universal standard
Shorter to type
Every tutorial, documentation, and professional code uses it
Makes your code instantly recognizable
Never do this:

Python

import numpy           # Too long to type numpy.array() every time
import numpy as n      # Non-standard, confuses others
from numpy import *    # Pollutes namespace, causes conflicts
2.4 Your First NumPy Program
Python

import numpy as np

# Create your first array
my_first_array = np.array([1, 2, 3, 4, 5])

# Print it
print("My First NumPy Array:", my_first_array)

# Do some operations
print("Sum:", np.sum(my_first_array))
print("Mean:", np.mean(my_first_array))
print("Each element doubled:", my_first_array * 2)
Output:

text

My First NumPy Array: [1 2 3 4 5]
Sum: 15
Mean: 3.0
Each element doubled: [ 2  4  6  8 10]
🎉 Congratulations! You've written your first NumPy code!

Chapter 3: Understanding Arrays - The Heart of NumPy
3.1 What is an Array?
An array is a grid of values, all of the same type, indexed by a tuple of non-negative integers.

Visual Understanding:
text

1D Array (Vector):
┌───┬───┬───┬───┬───┐
│ 1 │ 2 │ 3 │ 4 │ 5 │
└───┴───┴───┴───┴───┘
  0   1   2   3   4   ← indices


2D Array (Matrix):
         Column 0  Column 1  Column 2
        ┌────────┬────────┬────────┐
Row 0   │   1    │   2    │   3    │
        ├────────┼────────┼────────┤
Row 1   │   4    │   5    │   6    │
        ├────────┼────────┼────────┤
Row 2   │   7    │   8    │   9    │
        └────────┴────────┴────────┘


3D Array (Tensor):
              ┌─────────────┐
             /│  1   2   3 │
            / │  4   5   6 │
           /  │  7   8   9 │
          /   └─────────────┘
         /   /│  10  11  12│
        /   / │  13  14  15│
       /   /  │  16  17  18│
      /   /   └─────────────┘
     ┌───────────┐
     │ 19  20  21│
     │ 22  23  24│
     │ 25  26  27│
     └───────────┘
     
     ↑ This is 3 matrices stacked together
3.2 Array vs Python List - Deep Comparison
Feature	Python List	NumPy Array
Data Types	Can mix types	Same type only
Memory	Scattered	Contiguous
Speed	Slow	Very Fast
Functionality	Basic	Extensive math operations
Size	Can change	Fixed after creation
Dimensions	Nested lists	True n-dimensional
Code Comparison:
Python

import numpy as np

# Python List
py_list = [1, 2, 3, 4, 5]

# NumPy Array
np_array = np.array([1, 2, 3, 4, 5])

# Operation: Multiply each element by 2

# Python List - Need a loop or list comprehension
py_result = [x * 2 for x in py_list]
print("Python:", py_result)  # [2, 4, 6, 8, 10]

# NumPy Array - Direct operation
np_result = np_array * 2
print("NumPy:", np_result)   # [ 2  4  6  8 10]
3.3 Understanding Dimensions (ndim)
Python

import numpy as np

# 0D Array (Scalar)
arr_0d = np.array(42)
print("0D Array:", arr_0d)
print("Dimensions:", arr_0d.ndim)  # 0
# Visual: Just the number 42

# 1D Array (Vector)
arr_1d = np.array([1, 2, 3, 4, 5])
print("\n1D Array:", arr_1d)
print("Dimensions:", arr_1d.ndim)  # 1
# Visual: [1, 2, 3, 4, 5]

# 2D Array (Matrix)
arr_2d = np.array([[1, 2, 3], 
                   [4, 5, 6]])
print("\n2D Array:\n", arr_2d)
print("Dimensions:", arr_2d.ndim)  # 2
# Visual: 
# [[1 2 3]
#  [4 5 6]]

# 3D Array (Tensor)
arr_3d = np.array([[[1, 2], [3, 4]], 
                   [[5, 6], [7, 8]]])
print("\n3D Array:\n", arr_3d)
print("Dimensions:", arr_3d.ndim)  # 3
3.4 Understanding Axes
This is CRUCIAL for Machine Learning!

text

2D Array:
                    axis 1 (columns) →
                    ┌───────────────────┐
                    │                   │
         axis 0    │   1    2    3     │  
         (rows)    │                   │
            ↓      │   4    5    6     │
                   │                   │
                   │   7    8    9     │
                   │                   │
                   └───────────────────┘

Operations along axes:

np.sum(arr, axis=0)  → Sum DOWN each column → [12, 15, 18]
np.sum(arr, axis=1)  → Sum ACROSS each row  → [6, 15, 24]
Memory Trick:

axis=0: Operation goes DOWN (collapses rows)
axis=1: Operation goes ACROSS (collapses columns)
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

print("Original Array:")
print(arr)

print("\nSum along axis=0 (down columns):")
print(np.sum(arr, axis=0))  # [12 15 18]

print("\nSum along axis=1 (across rows):")
print(np.sum(arr, axis=1))  # [ 6 15 24]

print("\nSum of all elements:")
print(np.sum(arr))  # 45
Chapter 4: Creating Arrays - Every Possible Way
4.1 From Python Lists
Python

import numpy as np

# 1D Array from list
arr1 = np.array([1, 2, 3, 4, 5])
print("1D:", arr1)

# 2D Array from nested lists
arr2 = np.array([[1, 2, 3], 
                 [4, 5, 6]])
print("2D:\n", arr2)

# 3D Array from nested nested lists
arr3 = np.array([[[1, 2], [3, 4]], 
                 [[5, 6], [7, 8]]])
print("3D:\n", arr3)

# Specifying data type
arr_float = np.array([1, 2, 3], dtype=float)
print("Float array:", arr_float)  # [1. 2. 3.]

arr_complex = np.array([1, 2, 3], dtype=complex)
print("Complex array:", arr_complex)  # [1.+0.j 2.+0.j 3.+0.j]
4.2 Arrays Filled with Zeros
Python

import numpy as np

# 1D zeros
zeros_1d = np.zeros(5)
print("1D Zeros:", zeros_1d)
# Output: [0. 0. 0. 0. 0.]

# 2D zeros (3 rows, 4 columns)
zeros_2d = np.zeros((3, 4))
print("2D Zeros:\n", zeros_2d)
# Output:
# [[0. 0. 0. 0.]
#  [0. 0. 0. 0.]
#  [0. 0. 0. 0.]]

# 3D zeros
zeros_3d = np.zeros((2, 3, 4))
print("3D Zeros shape:", zeros_3d.shape)  # (2, 3, 4)

# Zeros with specific dtype
zeros_int = np.zeros(5, dtype=int)
print("Integer Zeros:", zeros_int)  # [0 0 0 0 0]
Use Case: Initializing weight matrices, creating empty containers

4.3 Arrays Filled with Ones
Python

import numpy as np

# 1D ones
ones_1d = np.ones(5)
print("1D Ones:", ones_1d)
# Output: [1. 1. 1. 1. 1.]

# 2D ones
ones_2d = np.ones((3, 4))
print("2D Ones:\n", ones_2d)
# Output:
# [[1. 1. 1. 1.]
#  [1. 1. 1. 1.]
#  [1. 1. 1. 1.]]

# Integer ones
ones_int = np.ones((2, 3), dtype=int)
print("Integer Ones:\n", ones_int)
Use Case: Bias initialization, masks

4.4 Arrays Filled with Any Value
Python

import numpy as np

# Fill with 7
sevens = np.full((3, 3), 7)
print("Filled with 7:\n", sevens)
# Output:
# [[7 7 7]
#  [7 7 7]
#  [7 7 7]]

# Fill with pi
pi_array = np.full((2, 4), 3.14159)
print("Filled with pi:\n", pi_array)

# Fill with string (less common)
str_array = np.full((2, 2), "Hi", dtype=object)
print("String array:\n", str_array)
4.5 Empty Arrays (Uninitialized)
Python

import numpy as np

# Empty array - values are whatever is in memory!
empty_arr = np.empty((2, 3))
print("Empty (uninitialized):\n", empty_arr)
# Output: Random garbage values (whatever was in memory)

# ⚠️ WARNING: Never use empty if you need zeros!
# It's only faster because it doesn't initialize values
When to use: Only when you plan to fill ALL values immediately

4.6 Identity Matrix
Python

import numpy as np

# Identity matrix (ones on diagonal, zeros elsewhere)
identity = np.eye(4)
print("Identity Matrix:\n", identity)
# Output:
# [[1. 0. 0. 0.]
#  [0. 1. 0. 0.]
#  [0. 0. 1. 0.]
#  [0. 0. 0. 1.]]

# Non-square identity-like matrix
rect_eye = np.eye(3, 5)
print("Rectangular eye:\n", rect_eye)
# Output:
# [[1. 0. 0. 0. 0.]
#  [0. 1. 0. 0. 0.]
#  [0. 0. 1. 0. 0.]]

# Diagonal with offset
eye_k1 = np.eye(4, k=1)  # Diagonal shifted up by 1
print("Shifted diagonal:\n", eye_k1)
# Output:
# [[0. 1. 0. 0.]
#  [0. 0. 1. 0.]
#  [0. 0. 0. 1.]
#  [0. 0. 0. 0.]]
Use Case: Linear algebra, neural network weight initialization

4.7 Diagonal Arrays
Python

import numpy as np

# Create diagonal matrix from 1D array
diag_arr = np.diag([1, 2, 3, 4])
print("Diagonal matrix:\n", diag_arr)
# Output:
# [[1 0 0 0]
#  [0 2 0 0]
#  [0 0 3 0]
#  [0 0 0 4]]

# Extract diagonal from 2D array
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
diagonal = np.diag(matrix)
print("Extracted diagonal:", diagonal)  # [1 5 9]

# Extract off-diagonal
off_diag = np.diag(matrix, k=1)
print("Upper off-diagonal:", off_diag)  # [2 6]
4.8 Numerical Ranges
arange - Like Python's range()
Python

import numpy as np

# Basic range
arr1 = np.arange(10)
print("0 to 9:", arr1)
# Output: [0 1 2 3 4 5 6 7 8 9]

# Start and stop
arr2 = np.arange(5, 15)
print("5 to 14:", arr2)
# Output: [ 5  6  7  8  9 10 11 12 13 14]

# With step
arr3 = np.arange(0, 20, 2)
print("Even numbers:", arr3)
# Output: [ 0  2  4  6  8 10 12 14 16 18]

# Floating point
arr4 = np.arange(0, 1, 0.1)
print("Decimal step:", arr4)
# Output: [0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9]

# Negative step (countdown)
arr5 = np.arange(10, 0, -1)
print("Countdown:", arr5)
# Output: [10  9  8  7  6  5  4  3  2  1]
linspace - Evenly Spaced Numbers
Python

import numpy as np

# 5 numbers from 0 to 10 (inclusive)
arr1 = np.linspace(0, 10, 5)
print("5 numbers from 0-10:", arr1)
# Output: [ 0.   2.5  5.   7.5 10. ]

# 11 numbers from 0 to 1
arr2 = np.linspace(0, 1, 11)
print("11 numbers from 0-1:", arr2)
# Output: [0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1. ]

# Exclude endpoint
arr3 = np.linspace(0, 10, 5, endpoint=False)
print("Excluding endpoint:", arr3)
# Output: [0. 2. 4. 6. 8.]

# Get the step size too
arr4, step = np.linspace(0, 10, 5, retstep=True)
print("Array:", arr4)
print("Step size:", step)  # 2.5
Key Difference:

arange: You specify the step size
linspace: You specify how many numbers you want
logspace - Logarithmically Spaced Numbers
Python

import numpy as np

# 5 numbers from 10^0 to 10^4
arr1 = np.logspace(0, 4, 5)
print("Logspace:", arr1)
# Output: [1.e+00 1.e+01 1.e+02 1.e+03 1.e+04]
# That's: [1, 10, 100, 1000, 10000]

# For ML learning rates (common use case)
learning_rates = np.logspace(-5, 0, 6)
print("Learning rates:", learning_rates)
# Output: [1.e-05 1.e-04 1.e-03 1.e-02 1.e-01 1.e+00]
Use Case: Hyperparameter search for learning rates

4.9 Creating Arrays Like Other Arrays
Python

import numpy as np

original = np.array([[1, 2, 3], 
                     [4, 5, 6]])
print("Original:\n", original)
print("Original dtype:", original.dtype)

# zeros_like
zeros_like = np.zeros_like(original)
print("\nzeros_like:\n", zeros_like)
# Same shape, same dtype, filled with zeros

# ones_like
ones_like = np.ones_like(original)
print("\nones_like:\n", ones_like)

# full_like
full_like = np.full_like(original, 99)
print("\nfull_like (99):\n", full_like)

# empty_like
empty_like = np.empty_like(original)
print("\nempty_like:\n", empty_like)  # Garbage values
Use Case: Creating masks or result arrays matching input shape

4.10 Special Arrays Summary Table
Function	Purpose	Example
np.zeros()	Array filled with 0s	np.zeros((3,3))
np.ones()	Array filled with 1s	np.ones((3,3))
np.full()	Array filled with value	np.full((3,3), 7)
np.empty()	Uninitialized array	np.empty((3,3))
np.eye()	Identity matrix	np.eye(3)
np.diag()	Diagonal matrix	np.diag([1,2,3])
np.arange()	Range with step	np.arange(0,10,2)
np.linspace()	N evenly spaced	np.linspace(0,10,5)
np.logspace()	Log-spaced	np.logspace(0,4,5)
Chapter 5: Array Attributes - Know Your Arrays
5.1 All Array Attributes Overview
Python

import numpy as np

# Create a sample array
arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

print("Array:\n", arr)
print("\n" + "="*50)
print("ARRAY ATTRIBUTES")
print("="*50)

print(f"ndim     : {arr.ndim}")      # Number of dimensions
print(f"shape    : {arr.shape}")     # Size in each dimension
print(f"size     : {arr.size}")      # Total number of elements
print(f"dtype    : {arr.dtype}")     # Data type
print(f"itemsize : {arr.itemsize}")  # Bytes per element
print(f"nbytes   : {arr.nbytes}")    # Total bytes
print(f"T        : \n{arr.T}")       # Transpose
Output:

text

Array:
 [[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]

==================================================
ARRAY ATTRIBUTES
==================================================
ndim     : 2
shape    : (3, 4)
size     : 12
dtype    : int64
itemsize : 8
nbytes   : 96
T        : 
[[ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]
 [ 4  8 12]]
5.2 Deep Dive: ndim (Number of Dimensions)
Python

import numpy as np

# 0D - Scalar
scalar = np.array(42)
print(f"0D: {scalar}, ndim = {scalar.ndim}")

# 1D - Vector
vector = np.array([1, 2, 3])
print(f"1D: {vector}, ndim = {vector.ndim}")

# 2D - Matrix
matrix = np.array([[1, 2], [3, 4]])
print(f"2D:\n{matrix}\nndim = {matrix.ndim}")

# 3D - Tensor
tensor = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print(f"3D:\n{tensor}\nndim = {tensor.ndim}")

# 4D - For image batches in ML
# Shape: (batch_size, height, width, channels)
image_batch = np.zeros((32, 224, 224, 3))
print(f"4D image batch: ndim = {image_batch.ndim}, shape = {image_batch.shape}")
5.3 Deep Dive: shape
Python

import numpy as np

# Shape is a TUPLE!
arr = np.array([[1, 2, 3],
                [4, 5, 6]])

print(f"Shape: {arr.shape}")        # (2, 3)
print(f"Type: {type(arr.shape)}")   # <class 'tuple'>
print(f"Rows: {arr.shape[0]}")      # 2
print(f"Columns: {arr.shape[1]}")   # 3

# Understanding shape for different dimensions:
# 1D: (n,)          → n elements
# 2D: (m, n)        → m rows, n columns
# 3D: (d, m, n)     → d matrices, each m×n
# 4D: (b, d, m, n)  → b batches of d matrices

# Common ML shapes:
# Images: (batch, height, width, channels)
# Sequences: (batch, timesteps, features)
# Fully connected: (batch, features)
5.4 Deep Dive: dtype (Data Type)
Python

import numpy as np

# Integer types
print("Integer types:")
int8_arr = np.array([1, 2, 3], dtype=np.int8)
print(f"int8: {int8_arr.dtype}, range: -128 to 127")

int16_arr = np.array([1, 2, 3], dtype=np.int16)
print(f"int16: {int16_arr.dtype}, range: -32,768 to 32,767")

int32_arr = np.array([1, 2, 3], dtype=np.int32)
print(f"int32: {int32_arr.dtype}, range: ~±2 billion")

int64_arr = np.array([1, 2, 3], dtype=np.int64)
print(f"int64: {int64_arr.dtype}, range: ~±9 quintillion")

# Unsigned integers
print("\nUnsigned integer types:")
uint8_arr = np.array([1, 2, 3], dtype=np.uint8)
print(f"uint8: {uint8_arr.dtype}, range: 0 to 255")

# Float types
print("\nFloat types:")
float16_arr = np.array([1.0, 2.0, 3.0], dtype=np.float16)
print(f"float16: {float16_arr.dtype}, precision: 3-4 digits")

float32_arr = np.array([1.0, 2.0, 3.0], dtype=np.float32)
print(f"float32: {float32_arr.dtype}, precision: 6-7 digits")

float64_arr = np.array([1.0, 2.0, 3.0], dtype=np.float64)
print(f"float64: {float64_arr.dtype}, precision: 15-16 digits")

# Complex types
print("\nComplex types:")
complex_arr = np.array([1+2j, 3+4j], dtype=np.complex128)
print(f"complex128: {complex_arr.dtype}")

# Boolean
print("\nBoolean type:")
bool_arr = np.array([True, False, True], dtype=np.bool_)
print(f"bool: {bool_arr.dtype}")

# String type
print("\nString type:")
str_arr = np.array(['hello', 'world'], dtype='U10')  # Unicode string, max 10 chars
print(f"string: {str_arr.dtype}")
Choosing the Right Data Type
Use Case	Recommended dtype	Why
ML weights	float32	Good precision, less memory
ML on GPU	float16	Faster, enough for inference
Image pixels	uint8	0-255 range, efficient
High precision	float64	Scientific computing
Labels/Categories	int32	Sufficient for most cases
Masks	bool	Memory efficient
Python

import numpy as np

# Memory comparison
n = 1000000

float64_arr = np.ones(n, dtype=np.float64)
float32_arr = np.ones(n, dtype=np.float32)
float16_arr = np.ones(n, dtype=np.float16)

print(f"float64: {float64_arr.nbytes / 1024 / 1024:.2f} MB")  # 8 MB
print(f"float32: {float32_arr.nbytes / 1024 / 1024:.2f} MB")  # 4 MB
print(f"float16: {float16_arr.nbytes / 1024 / 1024:.2f} MB")  # 2 MB
5.5 Converting Data Types (astype)
Python

import numpy as np

# Integer to float
int_arr = np.array([1, 2, 3, 4, 5])
float_arr = int_arr.astype(np.float32)
print(f"Original: {int_arr.dtype} → Converted: {float_arr.dtype}")

# Float to integer (truncates!)
float_arr = np.array([1.7, 2.2, 3.9])
int_arr = float_arr.astype(np.int32)
print(f"Float to int: {float_arr} → {int_arr}")  # [1 2 3] - Truncated!

# String to numeric
str_arr = np.array(['1', '2', '3', '4'])
num_arr = str_arr.astype(np.int32)
print(f"String to int: {str_arr} → {num_arr}")

# Boolean conversion
bool_arr = np.array([True, False, True])
int_arr = bool_arr.astype(np.int32)
print(f"Bool to int: {bool_arr} → {int_arr}")  # [1 0 1]

# Integer to boolean
int_arr = np.array([0, 1, 2, -1, 0])
bool_arr = int_arr.astype(np.bool_)
print(f"Int to bool: {int_arr} → {bool_arr}")  # [False True True True False]
⚠️ Warning: astype() creates a NEW array. It doesn't modify the original!

Chapter 6: Indexing and Slicing - Accessing Your Data
6.1 Basic Indexing (1D Arrays)
Python

import numpy as np

arr = np.array([10, 20, 30, 40, 50])

#          Index:  0   1   2   3   4
#          Value: 10  20  30  40  50
#   Neg Index:    -5  -4  -3  -2  -1

# Positive indexing
print(arr[0])   # 10 (first element)
print(arr[2])   # 30 (third element)
print(arr[4])   # 50 (last element)

# Negative indexing (from the end)
print(arr[-1])  # 50 (last element)
print(arr[-2])  # 40 (second from last)
print(arr[-5])  # 10 (first element)

# Modifying elements
arr[0] = 100
print(arr)  # [100  20  30  40  50]
6.2 Basic Slicing (1D Arrays)
text

Slicing Syntax: arr[start:stop:step]

- start: Beginning index (inclusive) - default 0
- stop: Ending index (exclusive) - default array length
- step: Step size - default 1
Python

import numpy as np

arr = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

# Basic slicing
print(arr[2:7])     # [2 3 4 5 6] - Index 2 to 6
print(arr[:5])      # [0 1 2 3 4] - First 5 elements
print(arr[5:])      # [5 6 7 8 9] - From index 5 to end
print(arr[::2])     # [0 2 4 6 8] - Every 2nd element
print(arr[1::2])    # [1 3 5 7 9] - Every 2nd element starting from 1

# Negative step (reverse)
print(arr[::-1])    # [9 8 7 6 5 4 3 2 1 0] - Reversed
print(arr[::-2])    # [9 7 5 3 1] - Reversed, every 2nd

# Negative indices in slicing
print(arr[-5:])     # [5 6 7 8 9] - Last 5 elements
print(arr[:-3])     # [0 1 2 3 4 5 6] - All except last 3
print(arr[-7:-2])   # [3 4 5 6 7] - From -7 to -3
6.3 2D Array Indexing
Python

import numpy as np

arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

#           Col 0  Col 1  Col 2  Col 3
# Row 0  [   1      2      3      4   ]
# Row 1  [   5      6      7      8   ]
# Row 2  [   9     10     11     12   ]

# Single element access: arr[row, column]
print(arr[0, 0])    # 1  (first row, first column)
print(arr[1, 2])    # 7  (second row, third column)
print(arr[2, 3])    # 12 (third row, fourth column)
print(arr[-1, -1])  # 12 (last row, last column)

# Entire row
print(arr[0])       # [1 2 3 4] - First row
print(arr[1])       # [5 6 7 8] - Second row
print(arr[-1])      # [9 10 11 12] - Last row

# Entire column
print(arr[:, 0])    # [1 5 9] - First column
print(arr[:, 2])    # [3 7 11] - Third column
print(arr[:, -1])   # [4 8 12] - Last column
6.4 2D Array Slicing
Python

import numpy as np

arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

# Submatrix slicing
print("First 2 rows, first 3 columns:")
print(arr[:2, :3])
# [[1 2 3]
#  [5 6 7]]

print("\nLast 2 rows, last 2 columns:")
print(arr[-2:, -2:])
# [[ 7  8]
#  [11 12]]

print("\nMiddle elements:")
print(arr[1:2, 1:3])
# [[6 7]]

print("\nEvery other row:")
print(arr[::2, :])
# [[ 1  2  3  4]
#  [ 9 10 11 12]]

print("\nEvery other column:")
print(arr[:, ::2])
# [[ 1  3]
#  [ 5  7]
#  [ 9 11]]
6.5 3D Array Indexing
Python

import numpy as np

# 3D array: 2 matrices, each 3x4
arr = np.array([[[1, 2, 3, 4],
                 [5, 6, 7, 8],
                 [9, 10, 11, 12]],
                
                [[13, 14, 15, 16],
                 [17, 18, 19, 20],
                 [21, 22, 23, 24]]])

print("Shape:", arr.shape)  # (2, 3, 4)

# Access: arr[matrix, row, column]
print("First matrix, first row, first element:", arr[0, 0, 0])  # 1
print("Second matrix, second row, third element:", arr[1, 1, 2])  # 19

# Entire first matrix
print("First matrix:")
print(arr[0])

# All matrices, first row
print("First row from each matrix:")
print(arr[:, 0, :])
# [[ 1  2  3  4]
#  [13 14 15 16]]

# All matrices, all rows, first column
print("First column from all matrices:")
print(arr[:, :, 0])
# [[ 1  5  9]
#  [13 17 21]]
6.6 Views vs Copies - CRITICAL CONCEPT!
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# SLICING CREATES A VIEW (NOT A COPY!)
slice_view = arr[1:4]
print("Original:", arr)        # [1 2 3 4 5]
print("Slice:", slice_view)    # [2 3 4]

# Modifying the slice CHANGES the original!
slice_view[0] = 999
print("After modifying slice:")
print("Original:", arr)        # [  1 999   3   4   5] ← CHANGED!
print("Slice:", slice_view)    # [999   3   4]

# To get an independent copy, use .copy()
arr = np.array([1, 2, 3, 4, 5])
slice_copy = arr[1:4].copy()
slice_copy[0] = 999
print("\nUsing .copy():")
print("Original:", arr)        # [1 2 3 4 5] ← UNCHANGED!
print("Copy:", slice_copy)     # [999   3   4]
Visual representation:

text

arr = [1, 2, 3, 4, 5]
        ↑
slice_view = arr[1:4]  →  Points to same memory!
        
When you modify slice_view, you modify arr!

arr.copy() creates NEW memory → Independent array
Rule of thumb:

Slicing → VIEW (shares memory)
Fancy indexing (using arrays) → COPY
.copy() → Always creates a copy
Chapter 7: Array Shape Manipulation
7.1 Reshape - Change Dimensions
Python

import numpy as np

# Original 1D array
arr = np.arange(12)
print("Original:", arr)
# [ 0  1  2  3  4  5  6  7  8  9 10 11]

# Reshape to 2D (3 rows, 4 columns)
arr_2d = arr.reshape(3, 4)
print("\nReshaped to 3x4:\n", arr_2d)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Reshape to 2D (4 rows, 3 columns)
arr_2d = arr.reshape(4, 3)
print("\nReshaped to 4x3:\n", arr_2d)
# [[ 0  1  2]
#  [ 3  4  5]
#  [ 6  7  8]
#  [ 9 10 11]]

# Reshape to 3D
arr_3d = arr.reshape(2, 2, 3)
print("\nReshaped to 2x2x3:\n", arr_3d)
# [[[ 0  1  2]
#   [ 3  4  5]]
#  [[ 6  7  8]
#   [ 9 10 11]]]

# Using -1 for automatic dimension calculation
arr_auto = arr.reshape(3, -1)  # -1 means "figure it out"
print("\nUsing -1:", arr_auto.shape)  # (3, 4)

arr_auto = arr.reshape(-1, 6)
print("Using -1:", arr_auto.shape)    # (2, 6)

# ⚠️ Total elements must remain the same!
# arr.reshape(5, 5)  # Error! 12 ≠ 25
Key Rules for Reshape:

Total elements must stay the same
Use -1 to auto-calculate one dimension
Reshape returns a VIEW (shares memory)
7.2 Flatten vs Ravel - Make 1D
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6]])

# flatten() - Always returns a COPY
flat = arr.flatten()
print("Flattened:", flat)  # [1 2 3 4 5 6]

flat[0] = 999
print("Original unchanged:", arr[0, 0])  # 1 (UNCHANGED)

# ravel() - Returns a VIEW (if possible)
ravel = arr.ravel()
print("Raveled:", ravel)  # [1 2 3 4 5 6]

ravel[0] = 999
print("Original changed:", arr[0, 0])  # 999 (CHANGED!)
When to use which:

flatten(): When you need an independent copy
ravel(): When you want memory efficiency (view)
7.3 Transpose
Python

import numpy as np

# 2D Transpose
arr = np.array([[1, 2, 3],
                [4, 5, 6]])
print("Original (2x3):\n", arr)

print("\nTransposed (3x2):\n", arr.T)
# [[1 4]
#  [2 5]
#  [3 6]]

# Alternative methods
print("\nUsing .transpose():\n", arr.transpose())
print("\nUsing np.transpose():\n", np.transpose(arr))

# 3D Transpose - axes are reversed
arr_3d = np.arange(24).reshape(2, 3, 4)
print("\n3D Original shape:", arr_3d.shape)     # (2, 3, 4)
print("3D Transposed shape:", arr_3d.T.shape)  # (4, 3, 2)

# Custom axis order with transpose
arr_custom = arr_3d.transpose(1, 2, 0)
print("Custom transpose shape:", arr_custom.shape)  # (3, 4, 2)
7.4 Adding and Removing Dimensions
Adding Dimensions with np.newaxis or np.expand_dims
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print("Original shape:", arr.shape)  # (5,)

# Add dimension at front
arr_new = arr[np.newaxis, :]
print("newaxis at front:", arr_new.shape)  # (1, 5)
print(arr_new)  # [[1 2 3 4 5]]

# Add dimension at end
arr_new = arr[:, np.newaxis]
print("newaxis at end:", arr_new.shape)  # (5, 1)
print(arr_new)  
# [[1]
#  [2]
#  [3]
#  [4]
#  [5]]

# Using expand_dims
arr_exp = np.expand_dims(arr, axis=0)
print("expand_dims axis=0:", arr_exp.shape)  # (1, 5)

arr_exp = np.expand_dims(arr, axis=1)
print("expand_dims axis=1:", arr_exp.shape)  # (5, 1)
Removing Dimensions with squeeze
Python

import numpy as np

arr = np.array([[[1, 2, 3, 4]]])
print("Original shape:", arr.shape)  # (1, 1, 4)

# Remove all size-1 dimensions
squeezed = np.squeeze(arr)
print("Squeezed shape:", squeezed.shape)  # (4,)

# Remove specific axis
arr = np.zeros((1, 3, 1, 5))
print("\nOriginal shape:", arr.shape)  # (1, 3, 1, 5)

squeezed = np.squeeze(arr, axis=0)
print("Squeeze axis 0:", squeezed.shape)  # (3, 1, 5)

squeezed = np.squeeze(arr, axis=2)
print("Squeeze axis 2:", squeezed.shape)  # (1, 3, 5)
7.5 Stacking Arrays
Vertical Stack (vstack)
Python

import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Stack vertically (row-wise)
vstacked = np.vstack((arr1, arr2))
print("vstack:\n", vstacked)
# [[1 2 3]
#  [4 5 6]]

# Works with 2D arrays too
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

vstacked = np.vstack((arr1, arr2))
print("\n2D vstack:\n", vstacked)
# [[1 2]
#  [3 4]
#  [5 6]
#  [7 8]]
Horizontal Stack (hstack)
Python

import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Stack horizontally (column-wise)
hstacked = np.hstack((arr1, arr2))
print("hstack:", hstacked)
# [1 2 3 4 5 6]

# Works with 2D arrays
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

hstacked = np.hstack((arr1, arr2))
print("\n2D hstack:\n", hstacked)
# [[1 2 5 6]
#  [3 4 7 8]]
Depth Stack (dstack)
Python

import numpy as np

arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

# Stack along third dimension
dstacked = np.dstack((arr1, arr2))
print("dstack shape:", dstacked.shape)  # (2, 2, 2)
print("dstack:\n", dstacked)
# [[[1 5]
#   [2 6]]
#  [[3 7]
#   [4 8]]]
General Stack with np.stack
Python

import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Stack along new axis=0
stacked0 = np.stack((arr1, arr2), axis=0)
print("stack axis=0:\n", stacked0)
# [[1 2 3]
#  [4 5 6]]

# Stack along new axis=1
stacked1 = np.stack((arr1, arr2), axis=1)
print("\nstack axis=1:\n", stacked1)
# [[1 4]
#  [2 5]
#  [3 6]]
Concatenate
Python

import numpy as np

arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

# Concatenate along axis 0 (rows)
concat0 = np.concatenate((arr1, arr2), axis=0)
print("concat axis=0:\n", concat0)
# [[1 2]
#  [3 4]
#  [5 6]
#  [7 8]]

# Concatenate along axis 1 (columns)
concat1 = np.concatenate((arr1, arr2), axis=1)
print("\nconcat axis=1:\n", concat1)
# [[1 2 5 6]
#  [3 4 7 8]]
7.6 Splitting Arrays
Python

import numpy as np

arr = np.arange(12).reshape(3, 4)
print("Original:\n", arr)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Split into 3 equal parts along axis 1
split = np.array_split(arr, 3, axis=1)
print("\nSplit into 3 along axis 1:")
for i, s in enumerate(split):
    print(f"Part {i}:\n{s}")

# hsplit - split horizontally
left, right = np.hsplit(arr, 2)
print("\nhsplit:")
print("Left:\n", left)
print("Right:\n", right)

# vsplit - split vertically
arr = np.arange(12).reshape(4, 3)
top, bottom = np.vsplit(arr, 2)
print("\nvsplit:")
print("Top:\n", top)
print("Bottom:\n", bottom)
7.7 Shape Manipulation Summary
Operation	Function	Description
Reshape	arr.reshape()	Change dimensions
Flatten	arr.flatten()	Make 1D (copy)
Ravel	arr.ravel()	Make 1D (view)
Transpose	arr.T	Swap axes
Add dim	np.newaxis, expand_dims()	Add size-1 axis
Remove dim	np.squeeze()	Remove size-1 axes
Vertical stack	np.vstack()	Stack rows
Horizontal stack	np.hstack()	Stack columns
Concatenate	np.concatenate()	Join along axis
Split	np.split(), np.array_split()	Divide array
Chapter 8: Array Operations - The Power of Vectorization
8.1 What is Vectorization?
Vectorization = Performing operations on entire arrays without explicit loops.

Python

import numpy as np

# Without vectorization (slow)
def without_vectorization(arr):
    result = []
    for x in arr:
        result.append(x * 2 + 1)
    return result

# With vectorization (fast)
def with_vectorization(arr):
    return arr * 2 + 1

# Speed comparison
arr = np.arange(1000000)

# The vectorized version is 50-100x faster!
8.2 Arithmetic Operations
Python

import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])

# Addition
print("Addition:", a + b)           # [ 6  8 10 12]
print("Addition:", np.add(a, b))    # [ 6  8 10 12]

# Subtraction
print("Subtraction:", a - b)        # [-4 -4 -4 -4]
print("Subtraction:", np.subtract(a, b))

# Multiplication (element-wise)
print("Multiplication:", a * b)     # [ 5 12 21 32]
print("Multiplication:", np.multiply(a, b))

# Division
print("Division:", b / a)           # [5.   3.   2.33 2.  ]
print("Division:", np.divide(b, a))

# Floor Division
print("Floor Division:", b // a)    # [5 3 2 2]

# Modulus
print("Modulus:", b % a)            # [0 0 1 0]

# Power
print("Power:", a ** 2)             # [ 1  4  9 16]
print("Power:", np.power(a, 2))
8.3 Scalar Operations
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Operations with scalars apply to ALL elements
print("arr + 10:", arr + 10)        # [11 12 13 14 15]
print("arr - 5:", arr - 5)          # [-4 -3 -2 -1  0]
print("arr * 3:", arr * 3)          # [ 3  6  9 12 15]
print("arr / 2:", arr / 2)          # [0.5 1.  1.5 2.  2.5]
print("arr ** 2:", arr ** 2)        # [ 1  4  9 16 25]
print("10 / arr:", 10 / arr)        # [10.   5.   3.33 2.5  2.  ]
8.4 Comparison Operations
Python

import numpy as np

a = np.array([1, 2, 3, 4, 5])
b = np.array([5, 4, 3, 2, 1])

# Comparisons return boolean arrays
print("a > b:", a > b)          # [False False False  True  True]
print("a < b:", a < b)          # [ True  True False False False]
print("a == b:", a == b)        # [False False  True False False]
print("a != b:", a != b)        # [ True  True False  True  True]
print("a >= 3:", a >= 3)        # [False False  True  True  True]
print("a <= 3:", a <= 3)        # [ True  True  True False False]

# Combining conditions
print("(a > 2) & (a < 5):", (a > 2) & (a < 5))  # [False False  True  True False]
print("(a < 2) | (a > 4):", (a < 2) | (a > 4))  # [ True False False False  True]
print("~(a > 3):", ~(a > 3))                    # [ True  True  True False False]

# ⚠️ Use & | ~ for arrays, NOT and or not!
8.5 Logical Operations
Python

import numpy as np

a = np.array([True, True, False, False])
b = np.array([True, False, True, False])

# Logical operations
print("AND:", np.logical_and(a, b))  # [ True False False False]
print("OR:", np.logical_or(a, b))    # [ True  True  True False]
print("NOT:", np.logical_not(a))     # [False False  True  True]
print("XOR:", np.logical_xor(a, b))  # [False  True  True False]

# any() and all()
arr = np.array([True, True, False])
print("Any True?:", np.any(arr))     # True
print("All True?:", np.all(arr))     # False

# With conditions
numbers = np.array([1, 2, 3, 4, 5])
print("Any > 3?:", np.any(numbers > 3))   # True
print("All > 0?:", np.all(numbers > 0))   # True
print("All > 3?:", np.all(numbers > 3))   # False
8.6 Mathematical Functions
Python

import numpy as np

arr = np.array([1, 4, 9, 16, 25])

# Square root
print("sqrt:", np.sqrt(arr))        # [1. 2. 3. 4. 5.]

# Exponential
print("exp:", np.exp([0, 1, 2]))    # [1.   2.718 7.389]

# Logarithms
print("log (natural):", np.log([1, np.e, np.e**2]))  # [0. 1. 2.]
print("log10:", np.log10([1, 10, 100]))              # [0. 1. 2.]
print("log2:", np.log2([1, 2, 4, 8]))                # [0. 1. 2. 3.]

# Trigonometric
angles = np.array([0, np.pi/6, np.pi/4, np.pi/3, np.pi/2])
print("sin:", np.sin(angles))
print("cos:", np.cos(angles))
print("tan:", np.tan(angles[:4]))  # Avoid π/2 for tan

# Inverse trigonometric
print("arcsin(0.5):", np.arcsin(0.5))  # π/6 ≈ 0.524

# Absolute value
print("abs:", np.abs([-1, -2, 3, -4]))  # [1 2 3 4]

# Rounding
arr = np.array([1.2, 2.5, 3.7, 4.4])
print("round:", np.round(arr))      # [1. 2. 4. 4.]
print("floor:", np.floor(arr))      # [1. 2. 3. 4.]
print("ceil:", np.ceil(arr))        # [2. 3. 4. 5.]
print("trunc:", np.trunc(arr))      # [1. 2. 3. 4.]
8.7 Matrix Operations
Python

import numpy as np

A = np.array([[1, 2], 
              [3, 4]])

B = np.array([[5, 6], 
              [7, 8]])

# Element-wise multiplication (NOT matrix multiplication!)
print("Element-wise (A * B):\n", A * B)
# [[ 5 12]
#  [21 32]]

# Matrix multiplication
print("\nMatrix multiplication (A @ B):\n", A @ B)
print("Matrix multiplication (np.dot):\n", np.dot(A, B))
print("Matrix multiplication (np.matmul):\n", np.matmul(A, B))
# [[19 22]
#  [43 50]]

# Matrix @ Vector
v = np.array([1, 2])
print("\nMatrix @ Vector:", A @ v)  # [ 5 11]

# Dot product of vectors
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])
print("\nDot product:", np.dot(v1, v2))  # 1*4 + 2*5 + 3*6 = 32

# Cross product
print("Cross product:", np.cross(v1, v2))  # [-3  6 -3]
8.8 In-Place Operations
Python

import numpy as np

# Regular operations create NEW arrays
arr = np.array([1, 2, 3])
arr2 = arr + 5  # arr2 is a new array
print("arr unchanged:", arr)    # [1 2 3]
print("arr2:", arr2)            # [6 7 8]

# In-place operations modify the SAME array
arr = np.array([1, 2, 3])
arr += 5  # Modifies arr in place
print("arr changed:", arr)      # [6 7 8]

# Using out parameter for in-place
arr = np.array([1, 2, 3], dtype=float)
np.sqrt(arr, out=arr)
print("In-place sqrt:", arr)    # [1.  1.414  1.732]

# ⚠️ In-place operations save memory but can be dangerous!
Chapter 9: Broadcasting - The Magic Behind NumPy
9.1 What is Broadcasting?
Broadcasting is NumPy's way of performing operations on arrays with different shapes.

Instead of creating copies to match shapes, NumPy "stretches" the smaller array.

Python

import numpy as np

# Simple example
arr = np.array([1, 2, 3])
scalar = 5

# How does arr + scalar work?
# NumPy "broadcasts" 5 to [5, 5, 5]
result = arr + scalar
print(result)  # [6 7 8]
9.2 Broadcasting Rules
NumPy compares shapes element-wise from RIGHT to LEFT:

text

Rule 1: If dimensions differ, pad the smaller shape with 1s on the LEFT

Rule 2: Arrays with size 1 along a dimension are stretched to match

Rule 3: If sizes don't match and neither is 1, ERROR!
Visual Explanation:
text

Shape A: (3, 4)
Shape B: (4,)

Step 1: Pad B's shape with 1s on left
  A: (3, 4)
  B: (1, 4)

Step 2: Compare from right to left
  Dimension 1: 4 == 4 ✓
  Dimension 0: 3 vs 1 → stretch B to (3, 4) ✓

Result: Broadcasting works! Output shape: (3, 4)
9.3 Broadcasting Examples
Example 1: Scalar and Array
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6]])
scalar = 10

# Shapes: (2, 3) and ()
# After padding: (2, 3) and (1, 1)
# Stretch scalar to (2, 3)

result = arr + scalar
print(result)
# [[11 12 13]
#  [14 15 16]]
Example 2: 1D and 2D Arrays
Python

import numpy as np

# Adding row vector to matrix
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

row = np.array([10, 20, 30])

# Shapes: (3, 3) and (3,)
# After padding: (3, 3) and (1, 3)
# Stretch row to (3, 3)

result = matrix + row
print("Matrix + Row:\n", result)
# [[11 22 33]
#  [14 25 36]
#  [17 28 39]]
text

Visual:
       Matrix              Row (stretched)         Result
    [1  2  3]            [10 20 30]            [11 22 33]
    [4  5  6]     +      [10 20 30]      =     [14 25 36]
    [7  8  9]            [10 20 30]            [17 28 39]
Example 3: Column Vector and Matrix
Python

import numpy as np

matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

column = np.array([[100],
                   [200],
                   [300]])

# Shapes: (3, 3) and (3, 1)
# Stretch column to (3, 3)

result = matrix + column
print("Matrix + Column:\n", result)
# [[101 102 103]
#  [204 205 206]
#  [307 308 309]]
text

Visual:
       Matrix              Column (stretched)      Result
    [1  2  3]            [100 100 100]         [101 102 103]
    [4  5  6]     +      [200 200 200]    =    [204 205 206]
    [7  8  9]            [300 300 300]         [307 308 309]
Example 4: Row and Column Vectors
Python

import numpy as np

row = np.array([1, 2, 3])      # Shape: (3,)
col = np.array([[10],
                [20],
                [30]])          # Shape: (3, 1)

# Shapes: (3,) and (3, 1)
# After padding: (1, 3) and (3, 1)
# Both stretch to (3, 3)

result = row + col
print("Row + Column:\n", result)
# [[11 12 13]
#  [21 22 23]
#  [31 32 33]]
text

Visual:
    Row stretched         Col stretched         Result
    [1  2  3]            [10 10 10]          [11 12 13]
    [1  2  3]     +      [20 20 20]     =    [21 22 23]
    [1  2  3]            [30 30 30]          [31 32 33]
Example 5: Broadcasting Failure
Python

import numpy as np

a = np.array([1, 2, 3])     # Shape: (3,)
b = np.array([1, 2])        # Shape: (2,)

# Shapes: (3,) and (2,)
# 3 vs 2 → Neither is 1 → ERROR!

try:
    result = a + b
except ValueError as e:
    print("Error:", e)
# Error: operands could not be broadcast together with shapes (3,) (2,)
9.4 Broadcasting in ML Context
Python

import numpy as np

# Normalizing features (common ML preprocessing)
# Subtract mean, divide by std for each feature

data = np.array([[1, 200, 3000],
                 [2, 400, 5000],
                 [3, 600, 7000],
                 [4, 800, 9000]])

# Each column is a feature, each row is a sample
print("Original data:\n", data)

# Calculate mean of each feature (along axis=0)
mean = np.mean(data, axis=0)
print("\nFeature means:", mean)  # [2.5, 500, 6000]

# Calculate std of each feature
std = np.std(data, axis=0)
print("Feature stds:", std)

# Normalize using broadcasting
# data shape: (4, 3)
# mean shape: (3,) → broadcasts to (4, 3)
# std shape: (3,) → broadcasts to (4, 3)

normalized = (data - mean) / std
print("\nNormalized data:\n", normalized)
9.5 Broadcasting Shape Compatibility Table
Shape A	Shape B	Result	Works?
(3,)	(3,)	(3,)	✓
(3,)	(1,)	(3,)	✓
(3, 4)	(4,)	(3, 4)	✓
(3, 4)	(3, 1)	(3, 4)	✓
(3, 4)	(1, 4)	(3, 4)	✓
(3, 4)	(3,)	Error	✗
(3, 4, 5)	(4, 5)	(3, 4, 5)	✓
(3, 4, 5)	(5,)	(3, 4, 5)	✓
(3, 4, 5)	(4, 1)	(3, 4, 5)	✓
(3, 4, 5)	(3, 5)	Error	✗
Chapter 10: Universal Functions (ufuncs)
10.1 What are Ufuncs?
Universal Functions (ufuncs) are functions that operate element-wise on arrays.

They are:

Implemented in C (fast!)
Support broadcasting
Support type casting
Support output arrays
Support reduction operations
10.2 Types of Ufuncs
Unary Ufuncs (1 input)
Python

import numpy as np

arr = np.array([-2.5, -1, 0, 1, 2.5])

# Mathematical
print("abs:", np.abs(arr))           # [2.5 1.  0.  1.  2.5]
print("sqrt:", np.sqrt(np.abs(arr))) # [1.58 1.   0.   1.   1.58]
print("exp:", np.exp(arr))           # [0.08 0.37 1.   2.72 12.18]
print("log:", np.log(np.abs(arr)+1)) # [1.25 0.69 0.   0.69 1.25]
print("sign:", np.sign(arr))         # [-1. -1.  0.  1.  1.]

# Trigonometric
angles = np.array([0, np.pi/4, np.pi/2])
print("sin:", np.sin(angles))        # [0.   0.71 1.  ]
print("cos:", np.cos(angles))        # [1.   0.71 0.  ]

# Rounding
arr = np.array([1.2, 2.5, 3.7])
print("floor:", np.floor(arr))       # [1. 2. 3.]
print("ceil:", np.ceil(arr))         # [2. 3. 4.]
print("round:", np.round(arr))       # [1. 2. 4.]
print("trunc:", np.trunc(arr))       # [1. 2. 3.]
Binary Ufuncs (2 inputs)
Python

import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])

# Arithmetic
print("add:", np.add(a, b))           # [ 6  8 10 12]
print("subtract:", np.subtract(a, b)) # [-4 -4 -4 -4]
print("multiply:", np.multiply(a, b)) # [ 5 12 21 32]
print("divide:", np.divide(b, a))     # [5.  3.  2.33 2.  ]
print("power:", np.power(a, 2))       # [ 1  4  9 16]
print("mod:", np.mod(b, a))           # [0 0 1 0]

# Comparison
print("greater:", np.greater(a, 2))   # [False False  True  True]
print("equal:", np.equal(a, b))       # [False False False False]
print("maximum:", np.maximum(a, b))   # [5 6 7 8]
print("minimum:", np.minimum(a, b))   # [1 2 3 4]
10.3 Ufunc Methods
reduce - Reduce array to single value
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Add all elements
result = np.add.reduce(arr)
print("sum:", result)  # 15

# Multiply all elements
result = np.multiply.reduce(arr)
print("product:", result)  # 120

# 2D reduction
arr2d = np.array([[1, 2, 3],
                  [4, 5, 6]])

print("Sum along axis 0:", np.add.reduce(arr2d, axis=0))  # [5 7 9]
print("Sum along axis 1:", np.add.reduce(arr2d, axis=1))  # [6 15]
accumulate - Running reduction
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Cumulative sum
result = np.add.accumulate(arr)
print("cumsum:", result)  # [ 1  3  6 10 15]

# Cumulative product
result = np.multiply.accumulate(arr)
print("cumprod:", result)  # [  1   2   6  24 120]

# Cumulative maximum
arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])
result = np

Python

# Cumulative maximum
arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])
result = np.maximum.accumulate(arr)
print("cummax:", result)  # [3 3 4 4 5 9 9 9]

# Cumulative minimum
result = np.minimum.accumulate(arr)
print("cummin:", result)  # [3 1 1 1 1 1 1 1]
outer - Outer product
Python

import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Multiplication table
result = np.multiply.outer(a, b)
print("Outer product:\n", result)
# [[ 4  5  6]
#  [ 8 10 12]
#  [12 15 18]]

# Addition table
result = np.add.outer(a, b)
print("\nAddition outer:\n", result)
# [[5 6 7]
#  [6 7 8]
#  [7 8 9]]
at - Unbuffered in-place operation
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])
indices = [0, 1, 2, 2, 2]  # Note: index 2 appears 3 times

# Regular indexing (buffered - only adds once at duplicate indices)
arr_copy = arr.copy()
arr_copy[indices] += 1
print("Regular (buffered):", arr_copy)  # [2 3 4 4 5]

# Using at (unbuffered - adds for each occurrence)
arr_copy = arr.copy()
np.add.at(arr_copy, indices, 1)
print("Using at (unbuffered):", arr_copy)  # [2 3 6 4 5]
# Index 2 was incremented 3 times!
10.4 Creating Custom Ufuncs
Python

import numpy as np

# Simple custom function
def my_function(x):
    return x ** 2 + 2 * x + 1

# Convert to ufunc using vectorize
my_ufunc = np.vectorize(my_function)

arr = np.array([1, 2, 3, 4, 5])
result = my_ufunc(arr)
print("Custom ufunc result:", result)  # [ 4  9 16 25 36]

# More complex example with multiple inputs
def custom_formula(x, y):
    if x > y:
        return x - y
    else:
        return x + y

custom_ufunc = np.vectorize(custom_formula)

a = np.array([1, 5, 3, 7])
b = np.array([2, 3, 4, 5])
result = custom_ufunc(a, b)
print("Custom binary ufunc:", result)  # [3 2 7 2]

# ⚠️ Warning: np.vectorize is convenient but NOT fast!
# For performance, use native NumPy operations or numba
10.5 Ufunc Performance Tips
Python

import numpy as np

arr = np.arange(1000000)

# SLOW: Python loop
def slow_square(arr):
    result = []
    for x in arr:
        result.append(x ** 2)
    return np.array(result)

# FAST: NumPy ufunc
def fast_square(arr):
    return np.square(arr)

# FASTEST: Use out parameter to avoid memory allocation
result = np.empty_like(arr)
def fastest_square(arr, out):
    return np.square(arr, out=out)

# The ufunc version is 50-100x faster than the loop!
Chapter 11: Aggregation and Statistical Functions
11.1 Basic Aggregations
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Sum
print("Sum:", np.sum(arr))          # 55
print("Sum (method):", arr.sum())   # 55

# Product
print("Product:", np.prod(arr))     # 3628800

# Mean (Average)
print("Mean:", np.mean(arr))        # 5.5

# Median (Middle value)
print("Median:", np.median(arr))    # 5.5

# Standard Deviation
print("Std:", np.std(arr))          # 2.87

# Variance
print("Var:", np.var(arr))          # 8.25

# Min and Max
print("Min:", np.min(arr))          # 1
print("Max:", np.max(arr))          # 10

# Range (ptp = peak to peak)
print("Range:", np.ptp(arr))        # 9 (10 - 1)
11.2 Aggregations Along Axes
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

print("Array:\n", arr)

# No axis - aggregate ALL elements
print("\nSum (all):", np.sum(arr))  # 45

# axis=0 - aggregate DOWN (collapse rows)
print("\nSum (axis=0):", np.sum(arr, axis=0))  # [12 15 18]

# axis=1 - aggregate ACROSS (collapse columns)
print("\nSum (axis=1):", np.sum(arr, axis=1))  # [ 6 15 24]

# Visual explanation:
#           axis=1 →
#         [1  2  3] → sum=6
# axis=0  [4  5  6] → sum=15
#    ↓    [7  8  9] → sum=24
#         ↓  ↓  ↓
#        12 15 18
11.3 Statistical Functions
Python

import numpy as np

# Create sample data
np.random.seed(42)
data = np.random.normal(100, 15, 1000)  # Mean=100, Std=15, 1000 samples

print("Sample Statistics:")
print(f"Mean: {np.mean(data):.2f}")           # ~100
print(f"Median: {np.median(data):.2f}")       # ~100
print(f"Std Dev: {np.std(data):.2f}")         # ~15
print(f"Variance: {np.var(data):.2f}")        # ~225
print(f"Min: {np.min(data):.2f}")
print(f"Max: {np.max(data):.2f}")

# Percentiles
print(f"\n25th Percentile: {np.percentile(data, 25):.2f}")
print(f"50th Percentile: {np.percentile(data, 50):.2f}")  # Same as median
print(f"75th Percentile: {np.percentile(data, 75):.2f}")
print(f"95th Percentile: {np.percentile(data, 95):.2f}")

# Quantiles (same as percentile / 100)
print(f"\nQ1 (0.25): {np.quantile(data, 0.25):.2f}")
print(f"Q3 (0.75): {np.quantile(data, 0.75):.2f}")
11.4 Index-Based Aggregations
Python

import numpy as np

arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])

# Find INDEX of min/max
print("Array:", arr)
print("argmin (index of min):", np.argmin(arr))  # 1 (value 1 at index 1)
print("argmax (index of max):", np.argmax(arr))  # 5 (value 9 at index 5)

# Verify
print("Min value:", arr[np.argmin(arr)])  # 1
print("Max value:", arr[np.argmax(arr)])  # 9

# 2D arrays
arr2d = np.array([[3, 1, 4],
                  [1, 5, 9],
                  [2, 6, 5]])

print("\n2D Array:\n", arr2d)

# argmax along axes
print("argmax axis=0:", np.argmax(arr2d, axis=0))  # [0 2 1]
print("argmax axis=1:", np.argmax(arr2d, axis=1))  # [2 2 1]

# Flattened index
print("argmax (flat):", np.argmax(arr2d))  # 5 (value 9)

# Convert flat index to 2D index
flat_idx = np.argmax(arr2d)
idx_2d = np.unravel_index(flat_idx, arr2d.shape)
print("2D index of max:", idx_2d)  # (1, 2)
print("Value at index:", arr2d[idx_2d])  # 9
11.5 Cumulative Functions
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Cumulative sum
print("cumsum:", np.cumsum(arr))  # [ 1  3  6 10 15]
# [1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4+5]

# Cumulative product
print("cumprod:", np.cumprod(arr))  # [  1   2   6  24 120]
# [1, 1*2, 1*2*3, 1*2*3*4, 1*2*3*4*5]

# 2D cumulative operations
arr2d = np.array([[1, 2, 3],
                  [4, 5, 6]])

print("\n2D Array:\n", arr2d)
print("\ncumsum axis=0:\n", np.cumsum(arr2d, axis=0))
# [[1 2 3]
#  [5 7 9]]

print("\ncumsum axis=1:\n", np.cumsum(arr2d, axis=1))
# [[ 1  3  6]
#  [ 4  9 15]]
11.6 Handling NaN Values
Python

import numpy as np

# Array with NaN values
arr = np.array([1, 2, np.nan, 4, 5, np.nan, 7])

# Regular functions return NaN
print("Regular mean:", np.mean(arr))  # nan

# Use nan-safe versions
print("nanmean:", np.nanmean(arr))    # 3.8
print("nansum:", np.nansum(arr))      # 19.0
print("nanstd:", np.nanstd(arr))      # 2.04
print("nanmin:", np.nanmin(arr))      # 1.0
print("nanmax:", np.nanmax(arr))      # 7.0
print("nanmedian:", np.nanmedian(arr))  # 3.0

# Count non-NaN values
print("Count non-NaN:", np.count_nonzero(~np.isnan(arr)))  # 5

# Check for NaN
print("isnan:", np.isnan(arr))  # [False False  True False False  True False]
11.7 Correlation and Covariance
Python

import numpy as np

# Generate correlated data
np.random.seed(42)
x = np.random.randn(100)
y = 2 * x + np.random.randn(100) * 0.5  # y is correlated with x
z = np.random.randn(100)  # z is independent

# Correlation coefficient
print("Correlation (x, y):", np.corrcoef(x, y)[0, 1])  # ~0.97 (high correlation)
print("Correlation (x, z):", np.corrcoef(x, z)[0, 1])  # ~0.0 (no correlation)

# Covariance
print("\nCovariance (x, y):", np.cov(x, y)[0, 1])
print("Covariance (x, z):", np.cov(x, z)[0, 1])

# Full covariance matrix
data = np.vstack([x, y, z])
cov_matrix = np.cov(data)
print("\nCovariance Matrix:\n", cov_matrix)
11.8 Histogram
Python

import numpy as np

# Generate data
np.random.seed(42)
data = np.random.normal(0, 1, 1000)

# Create histogram
counts, bin_edges = np.histogram(data, bins=10)
print("Counts:", counts)
print("Bin edges:", bin_edges)

# Custom bins
counts, bins = np.histogram(data, bins=[-3, -2, -1, 0, 1, 2, 3])
print("\nCustom bins:")
for i in range(len(counts)):
    print(f"  [{bins[i]:.1f}, {bins[i+1]:.1f}): {counts[i]}")

# Normalized histogram (density)
density, bins = np.histogram(data, bins=20, density=True)
print("\nDensity histogram sum:", np.sum(density * np.diff(bins)))  # ~1.0
11.9 Summary Statistics Table
Function	Description	NaN-safe version
np.sum()	Sum of elements	np.nansum()
np.prod()	Product of elements	np.nanprod()
np.mean()	Arithmetic mean	np.nanmean()
np.median()	Median value	np.nanmedian()
np.std()	Standard deviation	np.nanstd()
np.var()	Variance	np.nanvar()
np.min()	Minimum value	np.nanmin()
np.max()	Maximum value	np.nanmax()
np.argmin()	Index of minimum	np.nanargmin()
np.argmax()	Index of maximum	np.nanargmax()
np.percentile()	Percentile	np.nanpercentile()
np.cumsum()	Cumulative sum	np.nancumsum()
np.cumprod()	Cumulative product	np.nancumprod()
Chapter 12: Linear Algebra with NumPy
12.1 Introduction to Linear Algebra in NumPy
Linear algebra is the foundation of Machine Learning. NumPy provides extensive support through the numpy.linalg module.

Python

import numpy as np
import numpy.linalg as la  # Common convention
12.2 Vectors and Basic Operations
Python

import numpy as np

# Creating vectors
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])

# Vector addition
print("v1 + v2:", v1 + v2)  # [5 7 9]

# Scalar multiplication
print("3 * v1:", 3 * v1)    # [3 6 9]

# Dot product
dot = np.dot(v1, v2)
print("Dot product:", dot)   # 1*4 + 2*5 + 3*6 = 32

# Alternative dot product syntax
print("v1 @ v2:", v1 @ v2)   # 32

# Vector magnitude (norm)
magnitude = np.linalg.norm(v1)
print("||v1||:", magnitude)  # sqrt(1² + 2² + 3²) = 3.74

# Unit vector (normalized)
unit_v1 = v1 / np.linalg.norm(v1)
print("Unit vector:", unit_v1)
print("Magnitude of unit:", np.linalg.norm(unit_v1))  # 1.0

# Cross product (3D vectors only)
cross = np.cross(v1, v2)
print("Cross product:", cross)  # [-3  6 -3]
12.3 Matrix Operations
Python

import numpy as np

# Creating matrices
A = np.array([[1, 2],
              [3, 4]])

B = np.array([[5, 6],
              [7, 8]])

# Matrix addition
print("A + B:\n", A + B)
# [[ 6  8]
#  [10 12]]

# Matrix multiplication
print("\nA @ B (matrix multiplication):\n", A @ B)
print("\nnp.matmul(A, B):\n", np.matmul(A, B))
print("\nnp.dot(A, B):\n", np.dot(A, B))
# [[19 22]
#  [43 50]]

# Element-wise multiplication (Hadamard product)
print("\nA * B (element-wise):\n", A * B)
# [[ 5 12]
#  [21 32]]

# Matrix-vector multiplication
v = np.array([1, 2])
print("\nA @ v:", A @ v)  # [5, 11]

# Transpose
print("\nA.T:\n", A.T)
# [[1 3]
#  [2 4]]
12.4 Special Matrices
Python

import numpy as np

# Identity matrix
I = np.eye(3)
print("Identity:\n", I)
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]

# Diagonal matrix
D = np.diag([1, 2, 3])
print("\nDiagonal:\n", D)
# [[1 0 0]
#  [0 2 0]
#  [0 0 3]]

# Triangular matrices
A = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

print("\nUpper triangular:\n", np.triu(A))
# [[1 2 3]
#  [0 5 6]
#  [0 0 9]]

print("\nLower triangular:\n", np.tril(A))
# [[1 0 0]
#  [4 5 0]
#  [7 8 9]]

# Zero and ones matrices
zeros = np.zeros((3, 3))
ones = np.ones((3, 3))
12.5 Matrix Properties
Python

import numpy as np

A = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

# Trace (sum of diagonal)
print("Trace:", np.trace(A))  # 1 + 5 + 9 = 15

# Determinant
A = np.array([[1, 2],
              [3, 4]])
print("Determinant:", np.linalg.det(A))  # 1*4 - 2*3 = -2

# Rank
print("Rank:", np.linalg.matrix_rank(A))  # 2

# Condition number (measures numerical stability)
print("Condition number:", np.linalg.cond(A))
12.6 Matrix Inverse
Python

import numpy as np

A = np.array([[1, 2],
              [3, 4]])

# Inverse
A_inv = np.linalg.inv(A)
print("A inverse:\n", A_inv)
# [[-2.   1. ]
#  [ 1.5 -0.5]]

# Verify: A @ A_inv = I
print("\nA @ A_inv:\n", A @ A_inv)
# [[1. 0.]
#  [0. 1.]]

# Pseudo-inverse (works for non-square matrices)
B = np.array([[1, 2, 3],
              [4, 5, 6]])
B_pinv = np.linalg.pinv(B)
print("\nB shape:", B.shape)           # (2, 3)
print("B pseudo-inverse shape:", B_pinv.shape)  # (3, 2)
12.7 Solving Linear Equations
Python

import numpy as np

# System of equations:
# 2x + 3y = 8
# 3x + 4y = 11

# In matrix form: Ax = b
A = np.array([[2, 3],
              [3, 4]])
b = np.array([8, 11])

# Solve using np.linalg.solve (more efficient than inverse)
x = np.linalg.solve(A, b)
print("Solution x:", x)  # [1. 2.]
# x = 1, y = 2

# Verify
print("Verification A @ x:", A @ x)  # [8. 11.]

# Alternative: Using inverse (less efficient)
x_alt = np.linalg.inv(A) @ b
print("Using inverse:", x_alt)  # [1. 2.]

# Least squares solution (for overdetermined systems)
# More equations than unknowns
A = np.array([[1, 1],
              [2, 1],
              [3, 1]])
b = np.array([1, 2, 2])

# np.linalg.lstsq returns: solution, residuals, rank, singular values
x, residuals, rank, s = np.linalg.lstsq(A, b, rcond=None)
print("\nLeast squares solution:", x)
12.8 Eigenvalues and Eigenvectors
Python

import numpy as np

A = np.array([[4, -2],
              [1, 1]])

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)

print("Eigenvalues:", eigenvalues)      # [3. 2.]
print("\nEigenvectors:\n", eigenvectors)
# [[0.89 0.71]
#  [0.45 0.71]]

# Each column is an eigenvector
v1 = eigenvectors[:, 0]  # First eigenvector
lambda1 = eigenvalues[0]  # First eigenvalue

# Verify: A @ v = λ * v
print("\nVerification:")
print("A @ v1:", A @ v1)
print("λ1 * v1:", lambda1 * v1)

# For symmetric matrices (more stable)
A_sym = np.array([[2, 1],
                  [1, 2]])
eigenvalues, eigenvectors = np.linalg.eigh(A_sym)  # Use eigh for symmetric
print("\nSymmetric matrix eigenvalues:", eigenvalues)
12.9 Singular Value Decomposition (SVD)
SVD is crucial for:

Dimensionality reduction (PCA)
Matrix approximation
Recommender systems
Image compression
Python

import numpy as np

A = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

# SVD: A = U @ Σ @ V^T
U, S, Vt = np.linalg.svd(A)

print("U (left singular vectors):\n", U)
print("\nS (singular values):", S)
print("\nVt (right singular vectors transposed):\n", Vt)

# Reconstruct A
S_matrix = np.zeros_like(A, dtype=float)
np.fill_diagonal(S_matrix, S)
A_reconstructed = U @ S_matrix @ Vt
print("\nReconstructed A:\n", A_reconstructed)

# Low-rank approximation (keep only k singular values)
k = 2
A_approx = U[:, :k] @ np.diag(S[:k]) @ Vt[:k, :]
print("\nRank-2 approximation:\n", A_approx)
12.10 Matrix Decompositions
QR Decomposition
Python

import numpy as np

A = np.array([[1, 2],
              [3, 4],
              [5, 6]])

# QR decomposition: A = Q @ R
Q, R = np.linalg.qr(A)

print("Q (orthogonal):\n", Q)
print("\nR (upper triangular):\n", R)

# Verify Q is orthogonal: Q.T @ Q = I
print("\nQ.T @ Q:\n", Q.T @ Q)

# Verify A = Q @ R
print("\nA reconstructed:\n", Q @ R)
Cholesky Decomposition
Python

import numpy as np

# Must be positive definite matrix
A = np.array([[4, 2],
              [2, 3]])

# Cholesky: A = L @ L.T
L = np.linalg.cholesky(A)

print("L (lower triangular):\n", L)
print("\nL @ L.T:\n", L @ L.T)  # Should equal A
12.11 Norms
Python

import numpy as np

v = np.array([3, 4])
A = np.array([[1, 2],
              [3, 4]])

# Vector norms
print("L2 norm (Euclidean):", np.linalg.norm(v))      # sqrt(9+16) = 5
print("L1 norm (Manhattan):", np.linalg.norm(v, 1))   # 3+4 = 7
print("L∞ norm (Max):", np.linalg.norm(v, np.inf))    # max(3,4) = 4

# Matrix norms
print("\nFrobenius norm:", np.linalg.norm(A, 'fro'))  # sqrt(1+4+9+16) = 5.48
print("Nuclear norm:", np.linalg.norm(A, 'nuc'))      # Sum of singular values
print("Spectral norm (2-norm):", np.linalg.norm(A, 2))  # Largest singular value
12.12 Linear Algebra Cheat Sheet
Operation	Function	Description
Dot product	np.dot(a, b) or a @ b	Vector/matrix multiplication
Matrix multiply	np.matmul(A, B) or A @ B	Matrix multiplication
Transpose	A.T	Transpose matrix
Inverse	np.linalg.inv(A)	Matrix inverse
Pseudo-inverse	np.linalg.pinv(A)	Moore-Penrose pseudo-inverse
Determinant	np.linalg.det(A)	Matrix determinant
Rank	np.linalg.matrix_rank(A)	Matrix rank
Trace	np.trace(A)	Sum of diagonal
Eigenvalues	np.linalg.eig(A)	Eigendecomposition
SVD	np.linalg.svd(A)	Singular value decomposition
QR	np.linalg.qr(A)	QR decomposition
Cholesky	np.linalg.cholesky(A)	Cholesky decomposition
Solve Ax=b	np.linalg.solve(A, b)	Linear system solution
Least squares	np.linalg.lstsq(A, b)	Least squares solution
Norm	np.linalg.norm(x)	Vector/matrix norm
Chapter 13: Random Number Generation
13.1 Random Module Overview
NumPy provides a comprehensive random number generation system. The new recommended way uses np.random.default_rng().

Python

import numpy as np

# Old way (still works, but deprecated for new code)
np.random.seed(42)
old_random = np.random.random(5)

# New way (recommended)
rng = np.random.default_rng(42)  # Create a Generator with seed
new_random = rng.random(5)

print("Old style:", old_random)
print("New style:", new_random)
13.2 Basic Random Functions
Python

import numpy as np

rng = np.random.default_rng(42)

# Random floats [0, 1)
print("random(5):", rng.random(5))

# Random floats in range [low, high)
print("uniform(0, 10, 5):", rng.uniform(0, 10, 5))

# Random integers [low, high)
print("integers(0, 10, 5):", rng.integers(0, 10, 5))

# Random integers (inclusive of high)
print("integers(0, 10, 5, endpoint=True):", rng.integers(0, 10, 5, endpoint=True))

# Random choice from array
arr = np.array(['a', 'b', 'c', 'd', 'e'])
print("choice:", rng.choice(arr, 3))

# Random choice with replacement
print("choice with replacement:", rng.choice(arr, 10, replace=True))

# Random choice with probabilities
probs = [0.1, 0.1, 0.1, 0.1, 0.6]  # 'e' is most likely
print("weighted choice:", rng.choice(arr, 5, p=probs))
13.3 Random Distributions
Normal (Gaussian) Distribution
Python

import numpy as np

rng = np.random.default_rng(42)

# Standard normal (mean=0, std=1)
standard_normal = rng.standard_normal(1000)
print("Standard Normal - Mean:", np.mean(standard_normal))
print("Standard Normal - Std:", np.std(standard_normal))

# Custom normal distribution
mean, std = 100, 15
custom_normal = rng.normal(mean, std, 1000)
print("\nCustom Normal - Mean:", np.mean(custom_normal))
print("Custom Normal - Std:", np.std(custom_normal))

# 2D normal distribution
normal_2d = rng.normal(0, 1, (3, 4))
print("\n2D Normal:\n", normal_2d)
Other Common Distributions
Python

import numpy as np

rng = np.random.default_rng(42)

# Uniform distribution
uniform = rng.uniform(low=0, high=10, size=1000)
print("Uniform [0, 10] - Mean:", np.mean(uniform))  # ~5

# Binomial distribution (coin flips, success/failure)
# n trials, p probability of success
binomial = rng.binomial(n=10, p=0.5, size=1000)
print("Binomial (10 flips, p=0.5) - Mean:", np.mean(binomial))  # ~5

# Poisson distribution (events per time interval)
poisson = rng.poisson(lam=5, size=1000)  # lambda = expected events
print("Poisson (λ=5) - Mean:", np.mean(poisson))  # ~5

# Exponential distribution (time between events)
exponential = rng.exponential(scale=2, size=1000)  # scale = 1/λ
print("Exponential (scale=2) - Mean:", np.mean(exponential))  # ~2

# Beta distribution (probabilities)
beta = rng.beta(a=2, b=5, size=1000)
print("Beta (a=2, b=5) - Mean:", np.mean(beta))  # a/(a+b) = 0.286

# Gamma distribution
gamma = rng.gamma(shape=2, scale=2, size=1000)
print("Gamma (shape=2, scale=2) - Mean:", np.mean(gamma))  # shape*scale = 4
13.4 Random Permutations
Python

import numpy as np

rng = np.random.default_rng(42)

arr = np.arange(10)
print("Original:", arr)

# Shuffle in place
arr_copy = arr.copy()
rng.shuffle(arr_copy)
print("Shuffled:", arr_copy)

# Permutation (returns new array, doesn't modify original)
permuted = rng.permutation(arr)
print("Permuted:", permuted)
print("Original unchanged:", arr)

# Permutation of integer range
random_order = rng.permutation(10)
print("Random order of 0-9:", random_order)

# Permute rows of 2D array
arr_2d = np.arange(12).reshape(4, 3)
print("\nOriginal 2D:\n", arr_2d)
permuted_2d = rng.permutation(arr_2d)
print("\nPermuted rows:\n", permuted_2d)
13.5 Random Sampling
Python

import numpy as np

rng = np.random.default_rng(42)

# Population
population = np.arange(100)

# Simple random sample (without replacement)
sample = rng.choice(population, size=10, replace=False)
print("Sample without replacement:", sample)

# Sample with replacement (bootstrap)
bootstrap = rng.choice(population, size=100, replace=True)
print("Bootstrap sample (first 10):", bootstrap[:10])

# Weighted sampling
weights = np.ones(100)
weights[:10] = 10  # First 10 elements are 10x more likely
weights = weights / weights.sum()
weighted_sample = rng.choice(population, size=10, p=weights)
print("Weighted sample:", weighted_sample)
13.6 Setting Seeds for Reproducibility
Python

import numpy as np

# Method 1: Create generator with seed
rng = np.random.default_rng(42)
print("Run 1:", rng.random(3))

rng = np.random.default_rng(42)  # Same seed
print("Run 2:", rng.random(3))   # Same numbers!

# Method 2: Using SeedSequence for parallel reproducibility
from numpy.random import SeedSequence, default_rng

ss = SeedSequence(12345)
# Spawn independent generators for parallel processing
child_seeds = ss.spawn(4)
rngs = [default_rng(s) for s in child_seeds]

for i, rng in enumerate(rngs):
    print(f"Generator {i}: {rng.random(3)}")
13.7 Generating Random Matrices for ML
Python

import numpy as np

rng = np.random.default_rng(42)

# Xavier/Glorot initialization (for neural networks)
def xavier_init(shape):
    fan_in, fan_out = shape[0], shape[1]
    std = np.sqrt(2.0 / (fan_in + fan_out))
    return rng.normal(0, std, shape)

weights = xavier_init((784, 256))
print("Xavier weights - Shape:", weights.shape)
print("Xavier weights - Std:", np.std(weights))

# He initialization (for ReLU networks)
def he_init(shape):
    fan_in = shape[0]
    std = np.sqrt(2.0 / fan_in)
    return rng.normal(0, std, shape)

weights = he_init((784, 256))
print("\nHe weights - Shape:", weights.shape)
print("He weights - Std:", np.std(weights))

# Random orthogonal matrix
def random_orthogonal(n):
    H = rng.normal(0, 1, (n, n))
    Q, R = np.linalg.qr(H)
    return Q

ortho = random_orthogonal(5)
print("\nOrthogonal matrix (Q.T @ Q should be identity):")
print(ortho.T @ ortho)
13.8 Distribution Reference Table
Distribution	Function	Parameters	Use Case
Uniform	rng.uniform(low, high)	low, high	Random in range
Normal	rng.normal(mean, std)	μ, σ	Natural phenomena
Standard Normal	rng.standard_normal()	-	Standardized
Binomial	rng.binomial(n, p)	trials, probability	Success/failure
Poisson	rng.poisson(lam)	λ (rate)	Event counts
Exponential	rng.exponential(scale)	1/λ	Time between events
Beta	rng.beta(a, b)	α, β	Probabilities
Gamma	rng.gamma(shape, scale)	k, θ	Wait times
Multinomial	rng.multinomial(n, pvals)	n, probabilities	Categories
Chapter 14: File Input/Output Operations
14.1 Saving and Loading NumPy Arrays
Binary Format (.npy)
Python

import numpy as np

# Create sample array
arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

# Save single array
np.save('my_array.npy', arr)
print("Array saved!")

# Load array
loaded = np.load('my_array.npy')
print("Loaded array:\n", loaded)

# Verify they're the same
print("Arrays equal:", np.array_equal(arr, loaded))
Multiple Arrays (.npz)
Python

import numpy as np

# Create multiple arrays
arr1 = np.array([1, 2, 3])
arr2 = np.array([[1, 2], [3, 4]])
arr3 = np.random.random((5, 5))

# Save multiple arrays (uncompressed)
np.savez('multiple_arrays.npz', 
         first=arr1, 
         second=arr2, 
         third=arr3)

# Save compressed (smaller file size)
np.savez_compressed('multiple_arrays_compressed.npz',
                    first=arr1,
                    second=arr2,
                    third=arr3)

# Load multiple arrays
data = np.load('multiple_arrays.npz')
print("Keys:", list(data.keys()))
print("First array:", data['first'])
print("Second array:\n", data['second'])

# Don't forget to close!
data.close()

# Or use context manager
with np.load('multiple_arrays.npz') as data:
    arr1_loaded = data['first']
    arr2_loaded = data['second']
14.2 Text Files
Simple Text Files
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

# Save to text file
np.savetxt('array.txt', arr)
print("Saved as text!")

# Load from text file
loaded = np.loadtxt('array.txt')
print("Loaded:\n", loaded)

# With formatting options
np.savetxt('array_formatted.txt', arr, 
           fmt='%d',              # Integer format
           delimiter=',',         # Comma separator
           header='Col1,Col2,Col3',  # Header row
           comments='')           # No comment character

# Load with delimiter
loaded = np.loadtxt('array_formatted.txt', 
                    delimiter=',',
                    skiprows=1)    # Skip header
print("Loaded formatted:\n", loaded)
CSV Files
Python

import numpy as np

# Create data with labels
data = np.array([[1.5, 2.3, 3.1],
                 [4.2, 5.8, 6.4],
                 [7.9, 8.1, 9.6]])

# Save as CSV
np.savetxt('data.csv', data, 
           delimiter=',',
           header='Feature1,Feature2,Feature3',
           comments='',
           fmt='%.2f')

# Load CSV
loaded = np.loadtxt('data.csv', 
                    delimiter=',',
                    skiprows=1)
print("Loaded CSV:\n", loaded)

# For more complex CSV handling, use genfromtxt
# It handles missing values and different dtypes
loaded = np.genfromtxt('data.csv',
                       delimiter=',',
                       skip_header=1,
                       missing_values='NA',
                       filling_values=0)
14.3 Handling Complex Data
Mixed Data Types
Python

import numpy as np

# genfromtxt is more flexible than loadtxt
# Create a complex CSV
csv_content = """name,age,score
Alice,25,95.5
Bob,30,88.0
Charlie,22,92.3
"""

# Write to file
with open('people.csv', 'w') as f:
    f.write(csv_content)

# Load with genfromtxt
data = np.genfromtxt('people.csv',
                     delimiter=',',
                     names=True,      # Use first row as names
                     dtype=None,      # Infer dtypes
                     encoding='utf-8')

print("Loaded data:", data)
print("Names:", data['name'])
print("Ages:", data['age'])
print("Scores:", data['score'])
Missing Values
Python

import numpy as np

# Data with missing values
csv_content = """1,2,3
4,,6
7,8,
"""

with open('missing.csv', 'w') as f:
    f.write(csv_content)

# Load with missing value handling
data = np.genfromtxt('missing.csv',
                     delimiter=',',
                     missing_values='',
                     filling_values=-1)  # Replace missing with -1

print("Data with missing values handled:\n", data)

# Using masked array for missing values
data_masked = np.genfromtxt('missing.csv',
                            delimiter=',',
                            missing_values='',
                            usemask=True)
print("\nMasked array:\n", data_masked)
print("Mask:\n", data_masked.mask)
14.4 Binary Files (Raw)
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5], dtype=np.float64)

# Save raw binary
arr.tofile('raw_array.bin')

# Load raw binary (must know dtype and shape!)
loaded = np.fromfile('raw_array.bin', dtype=np.float64)
print("Loaded from binary:", loaded)

# ⚠️ Warning: Raw binary doesn't store dtype or shape!
# The .npy format is usually better
14.5 Memory-Mapped Files
For arrays too large to fit in memory:

Python

import numpy as np

# Create a large memory-mapped array
# This doesn't load the entire array into RAM
shape = (10000, 10000)

# Create and write
mmap_arr = np.memmap('large_array.dat', 
                     dtype='float32',
                     mode='w+',
                     shape=shape)

# Write some data
mmap_arr[0, :] = np.arange(10000)
mmap_arr.flush()  # Ensure data is written

# Read from memory-mapped file
mmap_read = np.memmap('large_array.dat',
                      dtype='float32',
                      mode='r',
                      shape=shape)

print("First row:", mmap_read[0, :10])

# Delete to release resources
del mmap_arr
del mmap_read
14.6 File I/O Summary
Format	Functions	Pros	Cons
.npy	np.save/load	Fast, preserves dtype	NumPy only
.npz	np.savez/load	Multiple arrays	NumPy only
.txt	np.savetxt/loadtxt	Human readable	Slow, large files
.csv	np.genfromtxt	Universal	Slow, limited dtypes
Raw binary	tofile/fromfile	Very fast	No metadata
Memory-mapped	np.memmap	Handle huge files	Complex setup
Chapter 15: Advanced Indexing Techniques
15.1 Fancy Indexing (Integer Array Indexing)
Python

import numpy as np

arr = np.array([10, 20, 30, 40, 50, 60, 70, 80, 90])

# Index with array of integers
indices = np.array([0, 2, 4, 6, 8])
result = arr[indices]
print("Fancy indexed:", result)  # [10 30 50 70 90]

# Can use lists too
result = arr[[1, 3, 5]]
print("Using list:", result)  # [20 40 60]

# Repeated indices
result = arr[[0, 0, 1, 1, 2]]
print("Repeated indices:", result)  # [10 10 20 20 30]

# Fancy indexing ALWAYS returns a COPY!
fancy_result = arr[indices]
fancy_result[0] = 999
print("Original unchanged:", arr[0])  # 10
2D Fancy Indexing
Python

import numpy as np

arr = np.arange(12).reshape(3, 4)
print("Original:\n", arr)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Select specific rows
rows = [0, 2]
print("\nRows 0 and 2:\n", arr[rows])
# [[ 0  1  2  3]
#  [ 8  9 10 11]]

# Select specific elements (row_indices, col_indices)
rows = [0, 1, 2]
cols = [0, 2, 3]
print("\nElements at (0,0), (1,2), (2,3):", arr[rows, cols])
# [ 0  6 11]

# Select submatrix using np.ix_
rows = [0, 2]
cols = [1, 3]
print("\nSubmatrix using ix_:\n", arr[np.ix_(rows, cols)])
# [[ 1  3]
#  [ 9 11]]
15.2 Boolean Indexing
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Create boolean mask
mask = arr > 5
print("Mask:", mask)
# [False False False False False  True  True  True  True  True]

# Apply mask
result = arr[mask]
print("Values > 5:", result)  # [ 6  7  8  9 10]

# Direct comparison indexing
print("Values > 5:", arr[arr > 5])  # [ 6  7  8  9 10]

# Multiple conditions (use & | ~, NOT and or not)
print("3 < x < 7:", arr[(arr > 3) & (arr < 7)])  # [4 5 6]
print("x < 3 or x > 8:", arr[(arr < 3) | (arr > 8)])  # [ 1  2  9 10]
print("NOT x > 5:", arr[~(arr > 5)])  # [1 2 3 4 5]
2D Boolean Indexing
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

# Boolean mask on elements
mask = arr > 4
print("Mask:\n", mask)
print("Values > 4:", arr[mask])  # [5 6 7 8 9] (flattened!)

# Modify values using boolean indexing
arr_copy = arr.copy()
arr_copy[arr_copy > 5] = 0
print("\nAfter setting >5 to 0:\n", arr_copy)
# [[1 2 3]
#  [4 5 0]
#  [0 0 0]]

# Boolean indexing on rows
# Select rows where first column > 2
row_mask = arr[:, 0] > 2
print("\nRows where first column > 2:\n", arr[row_mask])
# [[4 5 6]
#  [7 8 9]]
15.3 np.where - Conditional Selection
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# np.where returns indices where condition is True
indices = np.where(arr > 3)
print("Indices where > 3:", indices)  # (array([3, 4]),)
print("Values:", arr[indices])        # [4 5]

# np.where with three arguments: conditional assignment
# np.where(condition, value_if_true, value_if_false)
result = np.where(arr > 3, arr, 0)
print("Replace <=3 with 0:", result)  # [0 0 0 4 5]

result = np.where(arr > 3, 'big', 'small')
print("Label:", result)  # ['small' 'small' 'small' 'big' 'big']

# 2D where
arr2d = np.array([[1, 2], [3, 4]])
result = np.where(arr2d > 2, 1, 0)
print("\n2D where:\n", result)
# [[0 0]
#  [1 1]]
15.4 np.select - Multiple Conditions
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Multiple conditions
conditions = [
    arr < 3,
    (arr >= 3) & (arr < 7),
    arr >= 7
]

choices = ['small', 'medium', 'large']

result = np.select(conditions, choices, default='unknown')
print("Categories:", result)
# ['small' 'small' 'medium' 'medium' 'medium' 'medium' 'large' 'large' 'large' 'large']

# With numerical values
choices = [0, 1, 2]
result = np.select(conditions, choices)
print("Numerical categories:", result)
# [0 0 1 1 1 1 2 2 2 2]
15.5 np.take and np.put
Python

import numpy as np

arr = np.array([10, 20, 30, 40, 50])

# np.take - similar to fancy indexing
result = np.take(arr, [0, 2, 4])
print("take:", result)  # [10 30 50]

# np.take with out-of-bounds handling
result = np.take(arr, [0, 2, 10], mode='wrap')  # Wraps around
print("take with wrap:", result)  # [10 30 10]

result = np.take(arr, [0, 2, 10], mode='clip')  # Clips to valid range
print("take with clip:", result)  # [10 30 50]

# np.put - replace values at indices
arr = np.array([1, 2, 3, 4, 5])
np.put(arr, [0, 2, 4], [10, 30, 50])
print("After put:", arr)  # [10  2 30  4 50]
15.6 np.compress - Select by Boolean
Python

import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])

# Compress along axis
row_condition = [True, False, True]
result = np.compress(row_condition, arr, axis=0)
print("Compressed rows:\n", result)
# [[1 2 3]
#  [7 8 9]]

col_condition = [False, True, True]
result = np.compress(col_condition, arr, axis=1)
print("\nCompressed columns:\n", result)
# [[2 3]
#  [5 6]
#  [8 9]]
15.7 Advanced Indexing Examples for ML
Python

import numpy as np

# Example 1: Selecting samples by class
data = np.random.randn(100, 5)  # 100 samples, 5 features
labels = np.random.randint(0, 3, 100)  # 3 classes

# Get all samples of class 0
class_0_samples = data[labels == 0]
print("Class 0 samples:", class_0_samples.shape)

# Get samples of class 0 or 2
class_0_or_2 = data[(labels == 0) | (labels == 2)]
print("Class 0 or 2 samples:", class_0_or_2.shape)

# Example 2: Top-k selection
scores = np.random.random(100)
k = 10
top_k_indices = np.argsort(scores)[-k:][::-1]  # Top k indices
print("Top 10 indices:", top_k_indices)
print("Top 10 scores:", scores[top_k_indices])

# Example 3: Batch selection
def get_batch(data, labels, batch_size, rng):
    indices = rng.choice(len(data), batch_size, replace=False)
    return data[indices], labels[indices]

rng = np.random.default_rng(42)
batch_data, batch_labels = get_batch(data, labels, 32, rng)
print("Batch shape:", batch_data.shape)

# Example 4: One-hot encoding using advanced indexing
num_classes = 3
num_samples = 5
labels = np.array([0, 1, 2, 0, 1])

one_hot = np.zeros((num_samples, num_classes))
one_hot[np.arange(num_samples), labels] = 1
print("One-hot encoding:\n", one_hot)
Chapter 16: Memory Layout and Performance
16.1 Understanding Memory Layout
Row-Major (C) vs Column-Major (Fortran) Order
Python

import numpy as np

# C order (row-major) - default in NumPy
arr_c = np.array([[1, 2, 3],
                  [4, 5, 6]], order='C')

# Fortran order (column-major)
arr_f = np.array([[1, 2, 3],
                  [4, 5, 6]], order='F')

print("C order flags:", arr_c.flags['C_CONTIGUOUS'])  # True
print("F order flags:", arr_f.flags['F_CONTIGUOUS'])  # True

# Memory layout visualization
print("\nC order (row by row):", arr_c.ravel(order='C'))  # [1 2 3 4 5 6]
print("F order (column by column):", arr_f.ravel(order='F'))  # [1 4 2 5 3 6]
text

Memory Layout Visualization:

C Order (Row-Major):
Array:          Memory:
[[1, 2, 3],    [1][2][3][4][5][6]
 [4, 5, 6]]     ↑        ↑
               Row 0   Row 1

F Order (Column-Major):
Array:          Memory:
[[1, 2, 3],    [1][4][2][5][3][6]
 [4, 5, 6]]     ↑  ↑
              Col0 Col1 (etc.)
16.2 Checking Array Properties
Python

import numpy as np

arr = np.arange(12).reshape(3, 4)

print("Array:\n", arr)
print("\nArray Flags:")
print(arr.flags)

# Key flags:
# C_CONTIGUOUS: Memory is row-major
# F_CONTIGUOUS: Memory is column-major
# OWNDATA: Array owns its data
# WRITEABLE: Array can be modified

# Strides - bytes to step in each dimension
print("\nStrides:", arr.strides)
# (32, 8) means: 32 bytes to next row, 8 bytes to next column
# (8 bytes per int64 * 4 columns = 32 bytes per row)
16.3 Views and Memory Sharing
Python

import numpy as np

# Original array
arr = np.arange(12)
print("Original:", arr)

# Reshape creates a VIEW
reshaped = arr.reshape(3, 4)
print("Reshaped is a view:", np.shares_memory(arr, reshaped))  # True

# Slice creates a VIEW
sliced = arr[::2]
print("Slice is a view:", np.shares_memory(arr, sliced))  # True

# Fancy indexing creates a COPY
fancy = arr[[0, 2, 4]]
print("Fancy indexing is a view:", np.shares_memory(arr, fancy))  # False

# Transpose creates a VIEW
arr2d = arr.reshape(3, 4)
transposed = arr2d.T
print("Transpose is a view:", np.shares_memory(arr2d, transposed))  # True

# Check if array is a view
print("Is reshaped a view?:", reshaped.base is not None)  # True
16.4 Contiguous Arrays
Python

import numpy as np

arr = np.arange(12).reshape(3, 4)

# Slicing with step can break contiguity
strided = arr[::2, ::2]
print("Original contiguous:", arr.flags['C_CONTIGUOUS'])  # True
print("Strided contiguous:", strided.flags['C_CONTIGUOUS'])  # False

# Transpose breaks C-contiguity
transposed = arr.T
print("Transposed C-contiguous:", transposed.flags['C_CONTIGUOUS'])  # False
print("Transposed F-contiguous:", transposed.flags['F_CONTIGUOUS'])  # True

# Make a contiguous copy
contiguous = np.ascontiguousarray(strided)
print("After ascontiguousarray:", contiguous.flags['C_CONTIGUOUS'])  # True
16.5 Performance Optimization
Access Patterns Matter
Python

import numpy as np
import time

def time_it(func, *args, iterations=100):
    start = time.perf_counter()
    for _ in range(iterations):
        func(*args)
    return (time.perf_counter() - start) / iterations

arr = np.random.random((1000, 1000))

# Row-wise iteration (fast for C-order)
def row_sum():
    total = 0
    for i in range(arr.shape[0]):
        total += arr[i, :].sum()
    return total

# Column-wise iteration (slow for C-order)
def col_sum():
    total = 0
    for j in range(arr.shape[1]):
        total += arr[:, j].sum()
    return total

print(f"Row-wise: {time_it(row_sum)*1000:.3f} ms")
print(f"Column-wise: {time_it(col_sum)*1000:.3f} ms")

# Row-wise is faster because it accesses contiguous memory!
Vectorization vs Loops
Python

import numpy as np
import time

arr = np.random.random(1000000)

# SLOW: Python loop
def loop_sum():
    total = 0
    for x in arr:
        total += x
    return total

# FAST: Vectorized
def vec_sum():
    return np.sum(arr)

# Time comparison
start = time.perf_counter()
loop_result = loop_sum()
loop_time = time.perf_counter() - start

start = time.perf_counter()
vec_result = vec_sum()
vec_time = time.perf_counter() - start

print(f"Loop: {loop_time*1000:.2f} ms")
print(f"Vectorized: {vec_time*1000:.2f} ms")
print(f"Speedup: {loop_time/vec_time:.0f}x")
Memory Efficiency
Python

import numpy as np

# Tip 1: Use appropriate dtype
arr_float64 = np.random.random(1000000)  # 8 MB
arr_float32 = arr_float64.astype(np.float32)  # 4 MB
print(f"float64: {arr_float64.nbytes / 1e6:.1f} MB")
print(f"float32: {arr_float32.nbytes / 1e6:.1f} MB")

# Tip 2: Use in-place operations
arr = np.random.random(1000000)
arr += 1  # In-place (no extra memory)
# vs
# arr = arr + 1  # Creates new array

# Tip 3: Use out parameter
arr = np.random.random(1000000)
result = np.empty_like(arr)
np.sqrt(arr, out=result)  # No extra allocation

# Tip 4: Delete large arrays when done
del arr
16.6 Profiling Tips
Python

import numpy as np

# Check memory usage
def memory_usage(arr):
    return f"{arr.nbytes / 1024 / 1024:.2f} MB"

arr = np.random.random((10000, 10000))
print(f"Array size: {memory_usage(arr)}")

# Use smaller dtypes when possible
arr_small = arr.astype(np.float32)
print(f"Float32 size: {memory_usage(arr_small)}")

# For profiling, use:
# - %timeit in Jupyter/IPython
# - cProfile for detailed profiling
# - memory_profiler for memory usage
Chapter 17: Structured Arrays and Record Arrays
17.1 What are Structured Arrays?
Structured arrays allow you to store different data types in a single array - like a simple database table.

Python

import numpy as np

# Define a structured dtype
dt = np.dtype([
    ('name', 'U10'),      # Unicode string, max 10 chars
    ('age', 'i4'),        # 4-byte integer
    ('score', 'f8')       # 8-byte float
])

# Create structured array
data = np.array([
    ('Alice', 25, 95.5),
    ('Bob', 30, 88.0),
    ('Charlie', 22, 92.3)
], dtype=dt)

print("Structured Array:\n", data)
print("\nDtype:", data.dtype)

# Access by field name
print("\nNames:", data['name'])
print("Ages:", data['age'])
print("Scores:", data['score'])

# Access individual record
print("\nFirst record:", data[0])
print("First person's name:", data[0]['name'])
17.2 Creating Structured Dtypes
Python

import numpy as np

# Method 1: List of tuples
dt1 = np.dtype([('x', 'f4'), ('y', 'f4')])

# Method 2: Dictionary
dt2 = np.dtype({
    'names': ['x', 'y'],
    'formats': ['f4', 'f4']
})

# Method 3: String shorthand
dt3 = np.dtype('f4, f4')  # Unnamed fields

# Nested structures
dt_nested = np.dtype([
    ('name', 'U20'),
    ('position', [('x', 'f4'), ('y', 'f4'), ('z', 'f4')])
])

# Create nested array
nested_data = np.array([
    ('Point1', (1.0, 2.0, 3.0)),
    ('Point2', (4.0, 5.0, 6.0))
], dtype=dt_nested)

print("Nested data:\n", nested_data)
print("Positions:\n", nested_data['position'])
print("X coordinates:", nested_data['position']['x'])
17.3 Record Arrays
Record arrays allow accessing fields as attributes:

Python

import numpy as np

# Create record array
dt = np.dtype([
    ('name', 'U10'),
    ('age', 'i4'),
    ('score', 'f8')
])

data = np.array([
    ('Alice', 25, 95.5),
    ('Bob', 30, 88.0),
    ('Charlie', 22, 92.3)
], dtype=dt)

# Convert to record array
rec = np.rec.array(data)

# Access as attributes!
print("Names (attribute):", rec.name)
print("Ages (attribute):", rec.age)
print("Scores (attribute):", rec.score)

# Still works with indexing
print("\nFirst record:", rec[0])
print("First name:", rec[0].name)

# Create record array directly
rec2 = np.rec.array([
    ('David', 35, 91.0),
    ('Eve', 28, 97.5)
], dtype=dt)
17.4 Practical Example: Student Database
Python

import numpy as np

# Define student structure
student_dtype = np.dtype([
    ('id', 'i4'),
    ('name', 'U50'),
    ('grades', 'f4', (5,)),  # Array of 5 grades
    ('active', '?')          # Boolean
])

# Create student data
students = np.array([
    (1, 'Alice Johnson', [95, 92, 88, 91, 94], True),
    (2, 'Bob Smith', [78, 82, 85, 79, 81], True),
    (3, 'Charlie Brown', [88, 90, 92, 85, 87], False),
    (4, 'Diana Prince', [98, 97, 99, 96, 95], True),
], dtype=student_dtype)

print("Students:\n", students)

# Query: Active students with average grade > 90
avg_grades = students['grades'].mean(axis=1)
high_achievers = students[(students['active']) & (avg_grades > 90)]
print("\nHigh achievers:")
for student in high_achievers:
    print(f"  {student['name']}: {student['grades'].mean():.1f}")

# Add a new field (create new dtype)
new_dtype = np.dtype(student_dtype.descr + [('avg_grade', 'f4')])
students_new = np.zeros(len(students), dtype=new_dtype)

# Copy old fields
for name in student_dtype.names:
    students_new[name] = students[name]

# Calculate new field
students_new['avg_grade'] = students['grades'].mean(axis=1)
print("\nWith average grades:")
print(students_new[['name', 'avg_grade']])
17.5 When to Use Structured Arrays
Use structured arrays when:

You have heterogeneous data (mixed types)
You want named fields for clarity
You need a simple in-memory database
Performance is critical (faster than Python objects)
Consider Pandas instead when:

You need more data manipulation features
You're doing extensive data analysis
You need to handle missing values (NaN) easily
You want built-in plotting and I/O
Chapter 18: NumPy for Machine Learning
18.1 Data Preprocessing
Normalization and Standardization
Python

import numpy as np

# Sample data (100 samples, 4 features)
np.random.seed(42)
data = np.random.randn(100, 4) * np.array([1, 10, 100, 1000]) + np.array([0, 50, 500, 5000])

print("Original stats:")
print("Mean:", data.mean(axis=0))
print("Std:", data.std(axis=0))

# Min-Max Normalization (scale to [0, 1])
def minmax_normalize(X):
    min_val = X.min(axis=0)
    max_val = X.max(axis=0)
    return (X - min_val) / (max_val - min_val)

normalized = minmax_normalize(data)
print("\nAfter Min-Max Normalization:")
print("Min:", normalized.min(axis=0))
print("Max:", normalized.max(axis=0))

# Z-Score Standardization (mean=0, std=1)
def standardize(X):
    mean = X.mean(axis=0)
    std = X.std(axis=0)
    return (X - mean) / std

standardized = standardize(data)
print("\nAfter Standardization:")
print("Mean:", standardized.mean(axis=0))
print("Std:", standardized.std(axis=0))
Train-Test Split
Python

import numpy as np

def train_test_split(X, y, test_size=0.2, random_state=None):
    """Split data into training and test sets."""
    rng = np.random.default_rng(random_state)
    n_samples = len(X)
    n_test = int(n_samples * test_size)
    
    # Shuffle indices
    indices = rng.permutation(n_samples)
    
    test_indices = indices[:n_test]
    train_indices = indices[n_test:]
    
    return (X[train_indices], X[test_indices],
            y[train_indices], y[test_indices])

# Example usage
X = np.random.randn(1000, 10)  # 1000 samples, 10 features
y = np.random.randint(0, 2, 1000)  # Binary labels

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print(f"Training set: {X_train.shape[0]} samples")
print(f"Test set: {X_test.shape[0]} samples")
One-Hot Encoding
Python

import numpy as np

def one_hot_encode(labels, num_classes=None):
    """Convert labels to one-hot encoded format."""
    if num_classes is None:
        num_classes = labels.max() + 1
    
    one_hot = np.zeros((len(labels), num_classes))
    one_hot[np.arange(len(labels)), labels] = 1
    return one_hot

# Example
labels = np.array([0, 1, 2, 1, 0, 2, 2, 1])
one_hot = one_hot_encode(labels, num_classes=3)
print("Original labels:", labels)
print("One-hot encoded:\n", one_hot)

# Reverse: one-hot to labels
labels_back = np.argmax(one_hot, axis=1)
print("Back to labels:", labels_back)
18.2 Distance Calculations
Python

import numpy as np

# Two sets of points
X = np.array([[1, 2], [3, 4], [5, 6]])
Y = np.array([[1, 1], [2, 2]])

# Euclidean distance between all pairs
def euclidean_distances(X, Y):
    """Compute pairwise Euclidean distances."""
    # Using broadcasting: (n, 1, d) - (1, m, d) = (n, m, d)
    diff = X[:, np.newaxis, :] - Y[np.newaxis, :, :]
    return np.sqrt((diff ** 2).sum(axis=2))

distances = euclidean_distances(X, Y)
print("Pairwise Euclidean distances:\n", distances)

# More efficient using matrix operations
def euclidean_distances_efficient(X, Y):
    """Efficient pairwise Euclidean distances using ||a-b||² = ||a||² + ||b||² - 2<a,b>"""
    XX = (X ** 2).sum(axis=1)[:, np.newaxis]
    YY = (Y ** 2).sum(axis=1)[np.newaxis, :]
    XY = X @ Y.T
    return np.sqrt(np.maximum(XX + YY - 2 * XY, 0))

distances_efficient = euclidean_distances_efficient(X, Y)
print("\nEfficient method:\n", distances_efficient)

# Cosine similarity
def cosine_similarity(X, Y):
    """Compute pairwise cosine similarities."""
    X_norm = X / np.linalg.norm(X, axis=1, keepdims=True)
    Y_norm = Y / np.linalg.norm(Y, axis=1, keepdims=True)
    return X_norm @ Y_norm.T

similarity = cosine_similarity(X, Y)
print("\nCosine similarity:\n", similarity)
18.3 Simple ML Algorithms in NumPy
K-Nearest Neighbors
Python

import numpy as np

class KNNClassifier:
    def __init__(self, k=3):
        self.k = k
        
    def fit(self, X, y):
        self.X_train = X
        self.y_train = y
        
    def predict(self, X):
        predictions = []
        for x in X:
            # Compute distances to all training points
            distances = np.sqrt(((self.X_train - x) ** 2).sum(axis=1))
            
            # Get k nearest neighbors
            k_indices = np.argsort(distances)[:self.k]
            k_labels = self.y_train[k_indices]
            
            # Majority vote
            prediction = np.bincount(k_labels).argmax()
            predictions.append(prediction)
            
        return np.array(predictions)

# Example usage
np.random.seed(42)
X_train = np.random.randn(100, 2)
y_train = (X_train[:, 0] + X_train[:, 1] > 0).astype(int)

X_test = np.random.randn(20, 2)
y_test = (X_test[:, 0] + X_test[:, 1] > 0).astype(int)

knn = KNNClassifier(k=5)
knn.fit(X_train, y_train)
predictions = knn.predict(X_test)

accuracy = (predictions == y_test).mean()
print(f"KNN Accuracy: {accuracy:.2%}")
Linear Regression
Python

import numpy as np

class LinearRegression:
    def __init__(self):
        self.weights = None
        self.bias = None
        
    def fit(self, X, y):
        """Fit using normal equation: w = (X^T X)^(-1) X^T y"""
        # Add bias column
        X_b = np.c_[np.ones(X.shape[0]), X]
        
        # Normal equation
        theta = np.linalg.pinv(X_b.T @ X_b) @ X_b.T @ y
        
        self.bias = theta[0]
        self.weights = theta[1:]
        
    def predict(self, X):
        return X @ self.weights + self.bias
    
    def score(self, X, y):
        """R² score"""
        y_pred = self.predict(X)
        ss_res = ((y - y_pred) ** 2).sum()
        ss_tot = ((y - y.mean()) ** 2).sum()
        return 1 - (ss_res / ss_tot)

# Example usage
np.random.seed(42)
X = np.random.randn(100, 3)
y = 2 * X[:, 0] + 3 * X[:, 1] - X[:, 2] + np.random.randn(100) * 0.5

model = LinearRegression()
model.fit(X, y)

print("Weights:", model.weights)  # Should be close to [2, 3, -1]
print("Bias:", model.bias)        # Should be close to 0
print("R² Score:", model.score(X, y))
Gradient Descent
Python

import numpy as np

def gradient_descent(X, y, learning_rate=0.01, epochs=1000):
    """Linear regression using gradient descent."""
    n_samples, n_features = X.shape
    
    # Initialize weights
    weights = np.zeros(n_features)
    bias = 0
    
    losses = []
    
    for epoch in range(epochs):
        # Forward pass
        y_pred = X @ weights + bias
        
        # Compute loss (MSE)
        loss = ((y_pred - y) ** 2).mean()
        losses.append(loss)
        
        # Compute gradients
        dw = (2 / n_samples) * X.T @ (y_pred - y)
        db = (2 / n_samples) * (y_pred - y).sum()
        
        # Update weights
        weights -= learning_rate * dw
        bias -= learning_rate * db
        
        if epoch % 200 == 0:
            print(f"Epoch { if epoch % 200 == 0:
            print(f"Epoch {epoch}, Loss: {loss:.6f}")
    
    return weights, bias, losses

# Example usage
np.random.seed(42)
X = np.random.randn(100, 3)
y = 2 * X[:, 0] + 3 * X[:, 1] - X[:, 2] + np.random.randn(100) * 0.5

weights, bias, losses = gradient_descent(X, y, learning_rate=0.1, epochs=1000)

print("\nFinal weights:", weights)  # Should be close to [2, 3, -1]
print("Final bias:", bias)
print("Final loss:", losses[-1])
Logistic Regression
Python

import numpy as np

class LogisticRegression:
    def __init__(self, learning_rate=0.01, epochs=1000):
        self.lr = learning_rate
        self.epochs = epochs
        self.weights = None
        self.bias = None
        
    def sigmoid(self, z):
        # Clip to prevent overflow
        z = np.clip(z, -500, 500)
        return 1 / (1 + np.exp(-z))
    
    def fit(self, X, y):
        n_samples, n_features = X.shape
        
        # Initialize parameters
        self.weights = np.zeros(n_features)
        self.bias = 0
        
        # Gradient descent
        for epoch in range(self.epochs):
            # Forward pass
            z = X @ self.weights + self.bias
            y_pred = self.sigmoid(z)
            
            # Compute gradients
            dw = (1 / n_samples) * X.T @ (y_pred - y)
            db = (1 / n_samples) * (y_pred - y).sum()
            
            # Update parameters
            self.weights -= self.lr * dw
            self.bias -= self.lr * db
            
    def predict_proba(self, X):
        z = X @ self.weights + self.bias
        return self.sigmoid(z)
    
    def predict(self, X, threshold=0.5):
        return (self.predict_proba(X) >= threshold).astype(int)
    
    def accuracy(self, X, y):
        predictions = self.predict(X)
        return (predictions == y).mean()

# Example usage
np.random.seed(42)
X = np.random.randn(200, 2)
y = ((X[:, 0] + X[:, 1]) > 0).astype(int)

# Split data
X_train, X_test = X[:160], X[160:]
y_train, y_test = y[:160], y[160:]

model = LogisticRegression(learning_rate=0.1, epochs=1000)
model.fit(X_train, y_train)

print("Training Accuracy:", model.accuracy(X_train, y_train))
print("Test Accuracy:", model.accuracy(X_test, y_test))
print("Weights:", model.weights)
18.4 Neural Network Building Blocks
Activation Functions
Python

import numpy as np

# Sigmoid
def sigmoid(x):
    return 1 / (1 + np.exp(-np.clip(x, -500, 500)))

def sigmoid_derivative(x):
    s = sigmoid(x)
    return s * (1 - s)

# ReLU
def relu(x):
    return np.maximum(0, x)

def relu_derivative(x):
    return (x > 0).astype(float)

# Leaky ReLU
def leaky_relu(x, alpha=0.01):
    return np.where(x > 0, x, alpha * x)

def leaky_relu_derivative(x, alpha=0.01):
    return np.where(x > 0, 1, alpha)

# Tanh
def tanh(x):
    return np.tanh(x)

def tanh_derivative(x):
    return 1 - np.tanh(x) ** 2

# Softmax
def softmax(x):
    # Subtract max for numerical stability
    exp_x = np.exp(x - np.max(x, axis=-1, keepdims=True))
    return exp_x / exp_x.sum(axis=-1, keepdims=True)

# Example
x = np.array([-2, -1, 0, 1, 2])
print("Input:", x)
print("Sigmoid:", sigmoid(x))
print("ReLU:", relu(x))
print("Tanh:", tanh(x))

logits = np.array([[1, 2, 3], [1, 1, 1]])
print("\nSoftmax:\n", softmax(logits))
print("Softmax sum:", softmax(logits).sum(axis=1))  # Should be [1, 1]
Loss Functions
Python

import numpy as np

# Mean Squared Error (MSE)
def mse_loss(y_true, y_pred):
    return ((y_true - y_pred) ** 2).mean()

def mse_gradient(y_true, y_pred):
    return 2 * (y_pred - y_true) / len(y_true)

# Binary Cross-Entropy
def binary_cross_entropy(y_true, y_pred, epsilon=1e-15):
    y_pred = np.clip(y_pred, epsilon, 1 - epsilon)
    return -np.mean(y_true * np.log(y_pred) + (1 - y_true) * np.log(1 - y_pred))

def binary_cross_entropy_gradient(y_true, y_pred, epsilon=1e-15):
    y_pred = np.clip(y_pred, epsilon, 1 - epsilon)
    return (y_pred - y_true) / (y_pred * (1 - y_pred)) / len(y_true)

# Categorical Cross-Entropy
def categorical_cross_entropy(y_true, y_pred, epsilon=1e-15):
    y_pred = np.clip(y_pred, epsilon, 1 - epsilon)
    return -np.mean(np.sum(y_true * np.log(y_pred), axis=1))

# Example
y_true = np.array([1, 0, 1, 1, 0])
y_pred = np.array([0.9, 0.1, 0.8, 0.7, 0.2])

print("MSE Loss:", mse_loss(y_true, y_pred))
print("Binary Cross-Entropy:", binary_cross_entropy(y_true, y_pred))
Simple Neural Network
Python

import numpy as np

class SimpleNeuralNetwork:
    """A simple 2-layer neural network."""
    
    def __init__(self, input_size, hidden_size, output_size, learning_rate=0.01):
        self.lr = learning_rate
        
        # Initialize weights (Xavier initialization)
        self.W1 = np.random.randn(input_size, hidden_size) * np.sqrt(2 / input_size)
        self.b1 = np.zeros((1, hidden_size))
        self.W2 = np.random.randn(hidden_size, output_size) * np.sqrt(2 / hidden_size)
        self.b2 = np.zeros((1, output_size))
        
    def relu(self, x):
        return np.maximum(0, x)
    
    def relu_derivative(self, x):
        return (x > 0).astype(float)
    
    def softmax(self, x):
        exp_x = np.exp(x - np.max(x, axis=1, keepdims=True))
        return exp_x / exp_x.sum(axis=1, keepdims=True)
    
    def forward(self, X):
        # Layer 1
        self.z1 = X @ self.W1 + self.b1
        self.a1 = self.relu(self.z1)
        
        # Layer 2 (output)
        self.z2 = self.a1 @ self.W2 + self.b2
        self.a2 = self.softmax(self.z2)
        
        return self.a2
    
    def backward(self, X, y):
        m = X.shape[0]
        
        # Output layer gradient
        dz2 = self.a2 - y  # Softmax + Cross-entropy gradient
        dW2 = (1 / m) * self.a1.T @ dz2
        db2 = (1 / m) * dz2.sum(axis=0, keepdims=True)
        
        # Hidden layer gradient
        da1 = dz2 @ self.W2.T
        dz1 = da1 * self.relu_derivative(self.z1)
        dW1 = (1 / m) * X.T @ dz1
        db1 = (1 / m) * dz1.sum(axis=0, keepdims=True)
        
        # Update weights
        self.W2 -= self.lr * dW2
        self.b2 -= self.lr * db2
        self.W1 -= self.lr * dW1
        self.b1 -= self.lr * db1
        
    def train(self, X, y, epochs=1000, verbose=True):
        losses = []
        
        for epoch in range(epochs):
            # Forward pass
            output = self.forward(X)
            
            # Compute loss
            loss = -np.mean(np.sum(y * np.log(output + 1e-15), axis=1))
            losses.append(loss)
            
            # Backward pass
            self.backward(X, y)
            
            if verbose and epoch % 100 == 0:
                print(f"Epoch {epoch}, Loss: {loss:.6f}")
                
        return losses
    
    def predict(self, X):
        probs = self.forward(X)
        return np.argmax(probs, axis=1)
    
    def accuracy(self, X, y):
        predictions = self.predict(X)
        true_labels = np.argmax(y, axis=1)
        return (predictions == true_labels).mean()

# Example: XOR problem
np.random.seed(42)

# Generate XOR-like data
X = np.random.randn(200, 2)
y_labels = ((X[:, 0] > 0) != (X[:, 1] > 0)).astype(int)  # XOR logic
y = np.eye(2)[y_labels]  # One-hot encode

# Train network
nn = SimpleNeuralNetwork(input_size=2, hidden_size=8, output_size=2, learning_rate=0.5)
losses = nn.train(X, y, epochs=1000, verbose=True)

print(f"\nFinal Accuracy: {nn.accuracy(X, y):.2%}")
18.5 Batch Processing
Python

import numpy as np

def create_batches(X, y, batch_size, shuffle=True):
    """Create mini-batches for training."""
    n_samples = len(X)
    indices = np.arange(n_samples)
    
    if shuffle:
        np.random.shuffle(indices)
    
    batches = []
    for start_idx in range(0, n_samples, batch_size):
        end_idx = min(start_idx + batch_size, n_samples)
        batch_indices = indices[start_idx:end_idx]
        batches.append((X[batch_indices], y[batch_indices]))
    
    return batches

# Example usage
X = np.random.randn(100, 10)
y = np.random.randint(0, 2, 100)

batches = create_batches(X, y, batch_size=32)
print(f"Number of batches: {len(batches)}")
for i, (X_batch, y_batch) in enumerate(batches):
    print(f"Batch {i}: X shape = {X_batch.shape}, y shape = {y_batch.shape}")
18.6 Evaluation Metrics
Python

import numpy as np

def confusion_matrix(y_true, y_pred, n_classes=None):
    """Compute confusion matrix."""
    if n_classes is None:
        n_classes = max(y_true.max(), y_pred.max()) + 1
    
    cm = np.zeros((n_classes, n_classes), dtype=int)
    for t, p in zip(y_true, y_pred):
        cm[t, p] += 1
    
    return cm

def accuracy_score(y_true, y_pred):
    """Compute accuracy."""
    return (y_true == y_pred).mean()

def precision_score(y_true, y_pred, average='binary'):
    """Compute precision."""
    if average == 'binary':
        tp = ((y_true == 1) & (y_pred == 1)).sum()
        fp = ((y_true == 0) & (y_pred == 1)).sum()
        return tp / (tp + fp) if (tp + fp) > 0 else 0
    
def recall_score(y_true, y_pred, average='binary'):
    """Compute recall."""
    if average == 'binary':
        tp = ((y_true == 1) & (y_pred == 1)).sum()
        fn = ((y_true == 1) & (y_pred == 0)).sum()
        return tp / (tp + fn) if (tp + fn) > 0 else 0

def f1_score(y_true, y_pred, average='binary'):
    """Compute F1 score."""
    prec = precision_score(y_true, y_pred, average)
    rec = recall_score(y_true, y_pred, average)
    return 2 * prec * rec / (prec + rec) if (prec + rec) > 0 else 0

# Example
y_true = np.array([0, 0, 1, 1, 1, 0, 1, 0, 1, 1])
y_pred = np.array([0, 1, 1, 1, 0, 0, 1, 0, 1, 0])

print("Confusion Matrix:")
print(confusion_matrix(y_true, y_pred))
print(f"\nAccuracy: {accuracy_score(y_true, y_pred):.2%}")
print(f"Precision: {precision_score(y_true, y_pred):.2%}")
print(f"Recall: {recall_score(y_true, y_pred):.2%}")
print(f"F1 Score: {f1_score(y_true, y_pred):.2%}")
18.7 Principal Component Analysis (PCA)
Python

import numpy as np

class PCA:
    """Principal Component Analysis implementation."""
    
    def __init__(self, n_components):
        self.n_components = n_components
        self.components = None
        self.mean = None
        self.explained_variance_ratio = None
        
    def fit(self, X):
        # Center the data
        self.mean = X.mean(axis=0)
        X_centered = X - self.mean
        
        # Compute covariance matrix
        cov_matrix = np.cov(X_centered.T)
        
        # Compute eigenvalues and eigenvectors
        eigenvalues, eigenvectors = np.linalg.eigh(cov_matrix)
        
        # Sort by eigenvalue (descending)
        idx = np.argsort(eigenvalues)[::-1]
        eigenvalues = eigenvalues[idx]
        eigenvectors = eigenvectors[:, idx]
        
        # Store components
        self.components = eigenvectors[:, :self.n_components].T
        
        # Explained variance ratio
        total_var = eigenvalues.sum()
        self.explained_variance_ratio = eigenvalues[:self.n_components] / total_var
        
        return self
    
    def transform(self, X):
        X_centered = X - self.mean
        return X_centered @ self.components.T
    
    def fit_transform(self, X):
        self.fit(X)
        return self.transform(X)
    
    def inverse_transform(self, X_transformed):
        return X_transformed @ self.components + self.mean

# Example usage
np.random.seed(42)

# Create correlated data
mean = [0, 0, 0]
cov = [[1, 0.8, 0.2],
       [0.8, 1, 0.4],
       [0.2, 0.4, 1]]
X = np.random.multivariate_normal(mean, cov, 200)

print("Original shape:", X.shape)

# Apply PCA
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)

print("Reduced shape:", X_reduced.shape)
print("Explained variance ratio:", pca.explained_variance_ratio)
print("Total variance explained:", sum(pca.explained_variance_ratio))

# Reconstruct
X_reconstructed = pca.inverse_transform(X_reduced)
reconstruction_error = np.mean((X - X_reconstructed) ** 2)
print("Reconstruction error:", reconstruction_error)
18.8 K-Means Clustering
Python

import numpy as np

class KMeans:
    """K-Means clustering implementation."""
    
    def __init__(self, n_clusters, max_iters=100, random_state=None):
        self.n_clusters = n_clusters
        self.max_iters = max_iters
        self.rng = np.random.default_rng(random_state)
        self.centroids = None
        self.labels = None
        
    def fit(self, X):
        n_samples, n_features = X.shape
        
        # Initialize centroids randomly
        random_indices = self.rng.choice(n_samples, self.n_clusters, replace=False)
        self.centroids = X[random_indices].copy()
        
        for _ in range(self.max_iters):
            # Assign points to nearest centroid
            distances = self._compute_distances(X)
            new_labels = np.argmin(distances, axis=1)
            
            # Check for convergence
            if self.labels is not None and np.all(new_labels == self.labels):
                break
                
            self.labels = new_labels
            
            # Update centroids
            for k in range(self.n_clusters):
                if np.sum(self.labels == k) > 0:
                    self.centroids[k] = X[self.labels == k].mean(axis=0)
        
        return self
    
    def _compute_distances(self, X):
        """Compute distances from each point to each centroid."""
        distances = np.zeros((X.shape[0], self.n_clusters))
        for k in range(self.n_clusters):
            distances[:, k] = np.sqrt(((X - self.centroids[k]) ** 2).sum(axis=1))
        return distances
    
    def predict(self, X):
        distances = self._compute_distances(X)
        return np.argmin(distances, axis=1)
    
    def fit_predict(self, X):
        self.fit(X)
        return self.labels
    
    def inertia(self, X):
        """Compute sum of squared distances to centroids."""
        distances = self._compute_distances(X)
        return np.sum(np.min(distances, axis=1) ** 2)

# Example usage
np.random.seed(42)

# Create clustered data
cluster1 = np.random.randn(50, 2) + [0, 0]
cluster2 = np.random.randn(50, 2) + [5, 5]
cluster3 = np.random.randn(50, 2) + [0, 5]
X = np.vstack([cluster1, cluster2, cluster3])

# Apply K-Means
kmeans = KMeans(n_clusters=3, random_state=42)
labels = kmeans.fit_predict(X)

print("Cluster centers:\n", kmeans.centroids)
print("Inertia:", kmeans.inertia(X))
print("Labels distribution:", np.bincount(labels))
Chapter 19: Best Practices and Common Pitfalls
19.1 Common Pitfalls
Pitfall 1: Views vs Copies Confusion
Python

import numpy as np

# PITFALL: Modifying a slice affects the original
arr = np.array([1, 2, 3, 4, 5])
slice_view = arr[1:4]
slice_view[0] = 999
print("Original modified!", arr)  # [  1 999   3   4   5]

# SOLUTION: Use .copy() when you need independence
arr = np.array([1, 2, 3, 4, 5])
slice_copy = arr[1:4].copy()
slice_copy[0] = 999
print("Original safe:", arr)  # [1 2 3 4 5]
Pitfall 2: Using Python's and/or Instead of &/|
Python

import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# WRONG: Python's 'and' doesn't work with arrays
try:
    result = arr[(arr > 2) and (arr < 5)]  # ValueError!
except ValueError as e:
    print("Error:", e)

# CORRECT: Use & and wrap conditions in parentheses
result = arr[(arr > 2) & (arr < 5)]
print("Correct:", result)  # [3 4]

# Also for 'or' use '|', and for 'not' use '~'
Pitfall 3: Floating Point Comparison
Python

import numpy as np

a = 0.1 + 0.2
b = 0.3

# WRONG: Direct comparison
print("Direct comparison:", a == b)  # False!

# CORRECT: Use np.isclose or np.allclose
print("Using isclose:", np.isclose(a, b))  # True

arr1 = np.array([0.1 + 0.2, 0.2 + 0.3])
arr2 = np.array([0.3, 0.5])
print("Using allclose:", np.allclose(arr1, arr2))  # True
Pitfall 4: Integer Division Truncation
Python

import numpy as np

# Integer arrays truncate division results
arr_int = np.array([1, 2, 3, 4, 5], dtype=np.int64)
result = arr_int / 2
print("Integer division:", result, result.dtype)  # float64

# But in-place division keeps dtype!
arr_int = np.array([1, 2, 3, 4, 5], dtype=np.int64)
arr_int //= 2  # Floor division, stays int
print("In-place floor division:", arr_int)  # [0 1 1 2 2]

# Be careful with casting
arr_float = np.array([1.7, 2.5, 3.9])
arr_int = arr_float.astype(np.int64)  # Truncates, doesn't round!
print("Truncation:", arr_int)  # [1 2 3]
Pitfall 5: Broadcasting Shape Mismatch
Python

import numpy as np

# This works
a = np.array([[1, 2, 3], [4, 5, 6]])  # (2, 3)
b = np.array([1, 2, 3])               # (3,)
print("Works:", (a + b).shape)        # (2, 3)

# This fails!
a = np.array([[1, 2, 3], [4, 5, 6]])  # (2, 3)
b = np.array([1, 2])                  # (2,) - doesn't match!
try:
    result = a + b
except ValueError as e:
    print("Error:", e)

# SOLUTION: Reshape to make broadcasting work
b = np.array([1, 2])[:, np.newaxis]   # (2, 1)
print("After reshape:", (a + b).shape)  # (2, 3)
Pitfall 6: Modifying Array During Iteration
Python

import numpy as np

# WRONG: Can give unexpected results
arr = np.array([1, 2, 3, 4, 5])
for i, val in enumerate(arr):
    if val > 2:
        arr[i] = 0  # Modifying during iteration

# BETTER: Use boolean indexing
arr = np.array([1, 2, 3, 4, 5])
arr[arr > 2] = 0
print("Using boolean indexing:", arr)  # [1 2 0 0 0]

# Or np.where
arr = np.array([1, 2, 3, 4, 5])
arr = np.where(arr > 2, 0, arr)
print("Using where:", arr)  # [1 2 0 0 0]
Pitfall 7: Memory Issues with Large Arrays
Python

import numpy as np

# WRONG: Creating unnecessary copies
def process_data_bad(arr):
    arr = arr + 1           # Creates copy
    arr = arr * 2           # Creates another copy
    arr = arr ** 0.5        # Creates another copy
    return arr

# BETTER: In-place operations
def process_data_good(arr):
    arr = arr.copy()  # Only one copy
    arr += 1
    arr *= 2
    np.sqrt(arr, out=arr)
    return arr

# Or chain operations
def process_data_best(arr):
    return np.sqrt((arr + 1) * 2)  # Single expression, optimized
19.2 Best Practices
Practice 1: Use Vectorized Operations
Python

import numpy as np

# SLOW: Python loop
def slow_normalize(arr):
    result = np.empty_like(arr)
    for i in range(len(arr)):
        result[i] = (arr[i] - arr.min()) / (arr.max() - arr.min())
    return result

# FAST: Vectorized
def fast_normalize(arr):
    return (arr - arr.min()) / (arr.max() - arr.min())

arr = np.random.random(1000000)

# The vectorized version is 100x+ faster!
Practice 2: Preallocate Arrays
Python

import numpy as np

n = 10000

# SLOW: Growing list then converting
result = []
for i in range(n):
    result.append(i ** 2)
result = np.array(result)

# FAST: Preallocate
result = np.empty(n)
for i in range(n):
    result[i] = i ** 2

# FASTEST: Vectorized (when possible)
result = np.arange(n) ** 2
Practice 3: Choose the Right Data Type
Python

import numpy as np

# Use smallest dtype that fits your data
# Images: uint8 (0-255)
image = np.random.randint(0, 256, (1000, 1000), dtype=np.uint8)
print(f"uint8: {image.nbytes / 1e6:.1f} MB")

# ML weights: float32 (usually sufficient)
weights = np.random.randn(1000, 1000).astype(np.float32)
print(f"float32: {weights.nbytes / 1e6:.1f} MB")

# High precision: float64 (when needed)
precise = np.random.randn(1000, 1000)  # Default is float64
print(f"float64: {precise.nbytes / 1e6:.1f} MB")
Practice 4: Use Broadcasting Wisely
Python

import numpy as np

# Good: Broadcasting for normalization
data = np.random.randn(1000, 100)  # 1000 samples, 100 features
mean = data.mean(axis=0)            # (100,)
std = data.std(axis=0)              # (100,)
normalized = (data - mean) / std    # Broadcasting handles shapes

# Good: Outer operations with broadcasting
a = np.arange(5)[:, np.newaxis]  # (5, 1)
b = np.arange(3)[np.newaxis, :]  # (1, 3)
c = a * b                         # (5, 3) - multiplication table
Practice 5: Document Array Shapes
Python

import numpy as np

def process_batch(images, labels):
    """
    Process a batch of images.
    
    Parameters:
    -----------
    images : np.ndarray
        Shape: (batch_size, height, width, channels)
        Image data with values in [0, 255]
        
    labels : np.ndarray
        Shape: (batch_size,)
        Integer class labels
        
    Returns:
    --------
    features : np.ndarray
        Shape: (batch_size, num_features)
        Extracted features
    """
    # Validate shapes
    assert images.ndim == 4, f"Expected 4D array, got {images.ndim}D"
    assert labels.ndim == 1, f"Expected 1D array, got {labels.ndim}D"
    assert len(images) == len(labels), "Batch sizes must match"
    
    batch_size, height, width, channels = images.shape
    
    # Process...
    features = images.reshape(batch_size, -1).astype(np.float32) / 255
    return features
Practice 6: Use Random Generator (New Style)
Python

import numpy as np

# OLD (still works but deprecated for new code)
np.random.seed(42)
old_random = np.random.random(5)

# NEW (recommended)
rng = np.random.default_rng(42)
new_random = rng.random(5)

# Benefits of new style:
# - Better statistical properties
# - Reproducible across different NumPy versions
# - Each generator is independent (good for parallel code)
19.3 Performance Tips Summary
Tip	Description
Vectorize	Replace loops with array operations
Right dtype	Use smallest dtype that works
Preallocate	Create arrays of final size upfront
In-place ops	Use +=, *=, out= when possible
Contiguous	Keep arrays C-contiguous when possible
Views	Use views instead of copies when safe
Broadcasting	Let NumPy handle shape matching
Profile	Use %timeit to find bottlenecks
Chapter 20: Real-World Projects and Exercises
20.1 Project 1: Image Processing
Python

import numpy as np

def load_image_as_array():
    """Simulate loading an image (normally you'd use PIL or cv2)."""
    # Create a fake RGB image (height=100, width=100, channels=3)
    rng = np.random.default_rng(42)
    return rng.integers(0, 256, (100, 100, 3), dtype=np.uint8)

def grayscale(image):
    """Convert RGB to grayscale using luminosity method."""
    # Weights: R=0.299, G=0.587, B=0.114
    weights = np.array([0.299, 0.587, 0.114])
    return np.dot(image[..., :3], weights).astype(np.uint8)

def adjust_brightness(image, factor):
    """Adjust image brightness."""
    adjusted = image.astype(np.float32) * factor
    return np.clip(adjusted, 0, 255).astype(np.uint8)

def adjust_contrast(image, factor):
    """Adjust image contrast."""
    mean = image.mean()
    adjusted = (image.astype(np.float32) - mean) * factor + mean
    return np.clip(adjusted, 0, 255).astype(np.uint8)

def flip_horizontal(image):
    """Flip image horizontally."""
    return image[:, ::-1]

def flip_vertical(image):
    """Flip image vertically."""
    return image[::-1, :]

def rotate_90(image):
    """Rotate image 90 degrees clockwise."""
    return np.rot90(image, k=-1)

def crop_center(image, crop_height, crop_width):
    """Crop the center of the image."""
    h, w = image.shape[:2]
    start_h = (h - crop_height) // 2
    start_w = (w - crop_width) // 2
    return image[start_h:start_h+crop_height, start_w:start_w+crop_width]

def add_noise(image, noise_level=25):
    """Add Gaussian noise to image."""
    rng = np.random.default_rng()
    noise = rng.normal(0, noise_level, image.shape)
    noisy = image.astype(np.float32) + noise
    return np.clip(noisy, 0, 255).astype(np.uint8)

def simple_blur(image, kernel_size=3):
    """Apply simple box blur (mean filter)."""
    from numpy.lib.stride_tricks import sliding_window_view
    
    if image.ndim == 3:
        # Process each channel
        result = np.zeros_like(image)
        for c in range(image.shape[2]):
            result[:,:,c] = simple_blur(image[:,:,c], kernel_size)
        return result
    
    # Pad image
    pad = kernel_size // 2
    padded = np.pad(image, pad, mode='reflect')
    
    # Create sliding windows
    windows = sliding_window_view(padded, (kernel_size, kernel_size))
    
    # Mean of each window
    return windows.mean(axis=(2, 3)).astype(np.uint8)

# Example usage
image = load_image_as_array()
print("Original shape:", image.shape)

gray = grayscale(image)
print("Grayscale shape:", gray.shape)

bright = adjust_brightness(image, 1.5)
contrasted = adjust_contrast(image, 1.3)
flipped = flip_horizontal(image)
cropped = crop_center(image, 50, 50)
noisy = add_noise(image)
blurred = simple_blur(image, 5)

print("All transformations completed!")
20.2 Project 2: Data Analysis Pipeline
Python

import numpy as np

# Simulate a dataset
def generate_sample_data(n_samples=1000, random_state=42):
    """Generate sample data for analysis."""
    rng = np.random.default_rng(random_state)
    
    data = {
        'age': rng.integers(18, 80, n_samples),
        'income': rng.normal(50000, 20000, n_samples).clip(10000, 200000),
        'score': rng.normal(75, 15, n_samples).clip(0, 100),
        'category': rng.integers(0, 5, n_samples)
    }
    
    # Create structured array
    dt = np.dtype([
        ('age', 'i4'),
        ('income', 'f8'),
        ('score', 'f8'),
        ('category', 'i4')
    ])
    
    structured = np.zeros(n_samples, dtype=dt)
    for key in data:
        structured[key] = data[key]
    
    return structured

def describe(arr):
    """Generate descriptive statistics."""
    stats = {}
    for name in arr.dtype.names:
        col = arr[name]
        stats[name] = {
            'count': len(col),
            'mean': np.mean(col),
            'std': np.std(col),
            'min': np.min(col),
            '25%': np.percentile(col, 25),
            '50%': np.percentile(col, 50),
            '75%': np.percentile(col, 75),
            'max': np.max(col)
        }
    return stats

def detect_outliers_iqr(arr, column, multiplier=1.5):
    """Detect outliers using IQR method."""
    col = arr[column]
    q1 = np.percentile(col, 25)
    q3 = np.percentile(col, 75)
    iqr = q3 - q1
    lower = q1 - multiplier * iqr
    upper = q3 + multiplier * iqr
    
    outlier_mask = (col < lower) | (col > upper)
    return outlier_mask, lower, upper

def group_statistics(arr, group_col, value_col):
    """Calculate statistics grouped by category."""
    categories = np.unique(arr[group_col])
    results = {}
    
    for cat in categories:
        mask = arr[group_col] == cat
        values = arr[value_col][mask]
        results[cat] = {
            'count': len(values),
            'mean': np.mean(values),
            'std': np.std(values),
            'median': np.median(values)
        }
    
    return results

def correlation_matrix(arr, columns):
    """Calculate correlation matrix for numeric columns."""
    data = np.column_stack([arr[col] for col in columns])
    return np.corrcoef(data.T), columns

# Example usage
print("="*60)
print("DATA ANALYSIS PIPELINE")
print("="*60)

# Generate data
data = generate_sample_data(1000)
print(f"\nDataset shape: {data.shape}")
print(f"Columns: {data.dtype.names}")

# Descriptive statistics
print("\n--- Descriptive Statistics ---")
stats = describe(data)
for col, col_stats in stats.items():
    print(f"\n{col}:")
    for stat, value in col_stats.items():
        print(f"  {stat}: {value:.2f}")

# Outlier detection
print("\n--- Outlier Detection (Income) ---")
outliers, lower, upper = detect_outliers_iqr(data, 'income')
print(f"Outlier bounds: [{lower:.2f}, {upper:.2f}]")
print(f"Number of outliers: {np.sum(outliers)}")
print(f"Percentage: {np.mean(outliers)*100:.2f}%")

# Group statistics
print("\n--- Group Statistics (Score by Category) ---")
group_stats = group_statistics(data, 'category', 'score')
for cat, stats in group_stats.items():
    print(f"Category {cat}: mean={stats['mean']:.2f}, std={stats['std']:.2f}, n={stats['count']}")

# Correlation matrix
print("\n--- Correlation Matrix ---")
corr_matrix, cols = correlation_matrix(data, ['age', 'income', 'score'])
print("Columns:", cols)
print(corr_matrix.round(3))
20.3 Project 3: Simple Recommender System
Python

import numpy as np

class CollaborativeFilter:
    """Simple collaborative filtering recommender system."""
    
    def __init__(self, n_users, n_items, n_factors=10, learning_rate=0.01, reg=0.01):
        self.n_factors = n_factors
        self.lr = learning_rate
        self.reg = reg
        
        # Initialize latent factors
        rng = np.random.default_rng(42)
        self.user_factors = rng.normal(0, 0.1, (n_users, n_factors))
        self.item_factors = rng.normal(0, 0.1, (n_items, n_factors))
        self.user_bias = np.zeros(n_users)
        self.item_bias = np.zeros(n_items)
        self.global_bias = 0
        
    def predict(self, user, item):
        """Predict rating for user-item pair."""
        return (self.global_bias + 
                self.user_bias[user] + 
                self.item_bias[item] +
                np.dot(self.user_factors[user], self.item_factors[item]))
    
    def fit(self, ratings, epochs=20):
        """Train using SGD."""
        # ratings: list of (user, item, rating) tuples
        self.global_bias = np.mean([r for _, _, r in ratings])
        
        for epoch in range(epochs):
            np.random.shuffle(ratings)
            total_loss = 0
            
            for user, item, rating in ratings:
                # Predict
                pred = self.predict(user, item)
                error = rating - pred
                total_loss += error ** 2
                
                # Update biases
                self.user_bias[user] += self.lr * (error - self.reg * self.user_bias[user])
                self.item_bias[item] += self.lr * (error - self.reg * self.item_bias[item])
                
                # Update factors
                user_factor = self.user_factors[user].copy()
                self.user_factors[user] += self.lr * (error * self.item_factors[item] - 
                                                       self.reg * self.user_factors[user])
                self.item_factors[item] += self.lr * (error * user_factor - 
                                                       self.reg * self.item_factors[item])
            
            rmse = np.sqrt(total_loss / len(ratings))
            if epoch % 5 == 0:
                print(f"Epoch {epoch}, RMSE: {rmse:.4f}")
    
    def recommend(self, user, n=5, exclude_rated=None):
        """Recommend top N items for a user."""
        if exclude_rated is None:
            exclude_rated = set()
        
        predictions = []
        for item in range(len(self.item_factors)):
            if item not in exclude_rated:
                pred = self.predict(user, item)
                predictions.append((item, pred))
        
        predictions.sort(key=lambda x: x[1], reverse=True)
        return predictions[:n]

# Example usage
print("="*60)
print("COLLABORATIVE FILTERING RECOMMENDER")
print("="*60)

# Generate synthetic ratings data
rng = np.random.default_rng(42)
n_users, n_items = 100, 50
n_ratings = 2000

# Create random ratings
ratings = []
for _ in range(n_ratings):
    user = rng.integers(0, n_users)
    item = rng.integers(0, n_items)
    # Simulate some latent preferences
    rating = 3 + rng.normal(0, 1)
    rating = np.clip(rating, 1, 5)
    ratings.append((user, item, rating))

# Train model
model = CollaborativeFilter(n_users, n_items, n_factors=20)
model.fit(ratings, epochs=20)

# Get recommendations for user 0
user_ratings = set(item for u, item, _ in ratings if u == 0)
recommendations = model.recommend(0, n=10, exclude_rated=user_ratings)

print(f"\nTop 10 recommendations for User 0:")
for item, predicted_rating in recommendations:
    print(f"  Item {item}: predicted rating = {predicted_rating:.2f}")
20.4 Practice Exercises
Exercise 1: Array Manipulation (Beginner)
Python

"""
EXERCISE 1: Array Manipulation

Complete the following tasks:
1. Create a 1D array of numbers from 0 to 99
2. Reshape it into a 10x10 matrix
3. Extract the diagonal elements
4. Calculate the sum of each row
5. Find the maximum value in each column
6. Replace all values greater than 50 with -1
"""

import numpy as np

# YOUR CODE HERE
# 1. Create array
arr = np.arange(100)

# 2. Reshape
matrix = arr.reshape(10, 10)

# 3. Extract diagonal
diagonal = np.diag(matrix)

# 4. Sum of each row
row_sums = matrix.sum(axis=1)

# 5. Max of each column
col_maxes = matrix.max(axis=0)

# 6. Replace values > 50 with -1
matrix_modified = matrix.copy()
matrix_modified[matrix_modified > 50] = -1

# Print results
print("Matrix:\n", matrix)
print("\nDiagonal:", diagonal)
print("Row sums:", row_sums)
print("Column maxes:", col_maxes)
print("\nModified matrix:\n", matrix_modified)
Exercise 2: Statistical Analysis (Intermediate)
Python

"""
EXERCISE 2: Statistical Analysis

Given a dataset of student scores:
1. Calculate mean, median, standard deviation
2. Find students scoring above 90th percentile
3. Normalize scores to 0-100 scale
4. Group by class and calculate class averages
5. Find the correlation between homework and exam scores
"""

import numpy as np

# Generate sample data
rng = np.random.default_rng(42)
n_students = 200

data = {
    'student_id': np.arange(n_students),
    'class': rng.integers(1, 5, n_students),  # Classes 1-4
    'homework': rng.normal(75, 15, n_students).clip(0, 100),
    'exam': rng.normal(70, 20, n_students).clip(0, 100)
}

# YOUR CODE HERE
# 1. Basic statistics
print("Homework Statistics:")
print(f"  Mean: {np.mean(data['homework']):.2f}")
print(f"  Median: {np.median(data['homework']):.2f}")
print(f"  Std: {np.std(data['homework']):.2f}")

# 2. 90th percentile
percentile_90 = np.percentile(data['exam'], 90)
top_students = data['student_id'][data['exam'] >= percentile_90]
print(f"\nStudents above 90th percentile: {len(top_students)}")

# 3. Normalize (already 0-100, but let's do min-max normalization)
normalized_exam = (data['exam'] - data['exam'].min()) / (data['exam'].max() - data['exam'].min()) * 100

# 4. Group by class
print("\nClass Averages:")
for class_id in range(1, 5):
    mask = data['class'] == class_id
    avg = data['exam'][mask].mean()
    print(f"  Class {class_id}: {avg:.2f}")

# 5. Correlation
correlation = np.corrcoef(data['homework'], data['exam'])[0, 1]
print(f"\nHomework-Exam Correlation: {correlation:.3f}")
Exercise 3: Matrix Operations (Advanced)
Python

"""
EXERCISE 3: Matrix Operations

1. Create a random 5x5 matrix
2. Compute its eigenvalues and eigenvectors
3. Verify A @ v = λ * v for each eigenpair
4. Compute SVD and verify reconstruction
5. Solve a system of linear equations
"""

import numpy as np

# Set seed for reproducibility
rng = np.random.default_rng(42)

# 1. Create random matrix
A = rng.random((5, 5))
print("Matrix A:\n", A.round(3))

# 2. Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)
print("\nEigenvalues:", eigenvalues.round(3))

# 3. Verify A @ v = λ * v
print("\nVerifying eigenpairs:")
for i in range(5):
    v = eigenvectors[:, i]
    lambda_i = eigenvalues[i]
    lhs = A @ v
    rhs = lambda_i * v
    error = np.linalg.norm(lhs - rhs)
    print(f"  Eigenpair {i}: error = {error:.2e}")

# 4. SVD
U, S, Vt = np.linalg.svd(A)
S_matrix = np.diag(S)
A_reconstructed = U @ S_matrix @ Vt
reconstruction_error = np.linalg.norm(A - A_reconstructed)
print(f"\nSVD reconstruction error: {reconstruction_error:.2e}")

# 5. Solve linear system Ax = b
b = rng.random(5)
x = np.linalg.solve(A, b)
print("\nLinear system solution:")
print(f"  b = {b.round(3)}")
print(f"  x = {x.round(3)}")
print(f"  A @ x = {(A @ x).round(3)}")
print(f"  Error: {np.linalg.norm(A @ x - b):.2e}")
20.5 Final Challenge: Build a Mini ML Framework
Python

"""
FINAL CHALLENGE: Mini ML Framework

Build a small machine learning framework with:
1. Data preprocessing module
2. Model base class
3. Linear regression implementation
4. Logistic regression implementation
5. Evaluation metrics
6. Cross-validation
"""

import numpy as np

# ===== PREPROCESSING =====
class StandardScaler:
    def __init__(self):
        self.mean_ = None
        self.std_ = None
    
    def fit(self, X):
        self.mean_ = X.mean(axis=0)
        self.std_ = X.std(axis=0)
        return self
    
    def transform(self, X):
        return (X - self.mean_) / (self.std_ + 1e-8)
    
    def fit_transform(self, X):
        return self.fit(X).transform(X)

class MinMaxScaler:
    def __init__(self, feature_range=(0, 1)):
        self.min_ = None
        self.max_ = None
        self.feature_range = feature_range
    
    def fit(self, X):
        self.min_ = X.min(axis=0)
        self.max_ = X.max(axis=0)
        return self
    
    def transform(self, X):
        X_scaled = (X - self.min_) / (self.max_ - self.min_ + 1e-8)
        return X_scaled * (self.feature_range[1] - self.feature_range[0]) + self.feature_range[0]
    
    def fit_transform(self, X):
        return self.fit(X).transform(X)

# ===== BASE MODEL =====
class BaseModel:
    def fit(self, X, y):
        raise NotImplementedError
    
    def predict(self, X):
        raise NotImplementedError
    
    def score(self, X, y):
        raise NotImplementedError

# ===== LINEAR REGRESSION =====
class LinearRegressionGD(BaseModel):
    def __init__(self, learning_rate=0.01, epochs=1000):
        self.lr = learning_rate
        self.epochs = epochs
        self.weights = None
        self.bias = None
        self.loss_history = []
    
    def fit(self, X, y):
        n_samples, n_features = X.shape
        self.weights = np.zeros(n_features)
        self.bias = 0
        
        for _ in range(self.epochs):
            y_pred = X @ self.weights + self.bias
            
            loss = np.mean((y_pred - y) ** 2)
            self.loss_history.append(loss)
            
            dw = (2/n_samples) * X.T @ (y_pred - y)
            db = (2/n_samples) * np.sum(y_pred - y)
            
            self.weights -= self.lr * dw
            self.bias -= self.lr * db
        
        return self
    
    def predict(self, X):
        return X @ self.weights + self.bias
    
    def score(self, X, y):
        y_pred = self.predict(X)
        ss_res = np.sum((y - y_pred) ** 2)
        ss_tot = np.sum((y - y.mean()) ** 2)
        return 1 - (ss_res / ss_tot)

# ===== LOGISTIC REGRESSION =====
class LogisticRegressionGD(BaseModel):
    def __init__(self, learning_rate=0.01, epochs=1000):
        self.lr = learning_rate
        self.epochs = epochs
        self.weights = None
        self.bias = None
    
    def sigmoid(self, z):
        return 1 / (1 + np.exp(-np.clip(z, -500, 500)))
    
    def fit(self, X, y):
        n_samples, n_features = X.shape
        self.weights = np.zeros(n_features)
        self.bias = 0
        
        for _ in range(self.epochs):
            z = X @ self.weights + self.bias
            y_pred = self.sigmoid(z)
            
            dw = (1/n_samples) * X.T @ (y_pred - y)
            db = (1/n_samples) * np.sum(y_pred - y)
            
            self.weights -= self.lr * dw
            self.bias -= self.lr * db
        
        return self
    
    def predict_proba(self, X):
        return self.sigmoid(X @ self.weights + self.bias)
    
    def predict(self, X, threshold=0.5):
        return (self.predict_proba(X) >= threshold).astype(int)
    
    def score(self, X, y):
        return np.mean(self.predict(X) == y)

# ===== METRICS =====
class Metrics:
    @staticmethod
    def accuracy(y_true, y_pred):
        return np.mean(y_true == y_pred)
    
    @staticmethod
    def mse(y_true, y_pred):
        return np.mean((y_true - y_pred) ** 2)
    
    @staticmethod
    def rmse(y_true, y_pred):
        return np.sqrt(Metrics.mse(y_true, y_pred))
    
    @staticmethod
    def r2(y_true, y_pred):
        ss_res = np.sum((y_true - y_pred) ** 2)
        ss_tot = np.sum((y_true - y_true.mean()) ** 2)
        return 1 - (ss_res / ss_tot)
    
    @staticmethod
    def confusion_matrix(y_true, y_pred):
        classes = np.unique(np.concatenate([y_true, y_pred]))
        n_classes = len(classes)
        cm = np.zeros((n_classes, n_classes), dtype=int)
        for t, p in zip(y_true, y_pred):
            cm[t, p] += 1
        return cm

# ===== CROSS VALIDATION =====
def cross_validate(model_class, X, y, cv=5, **model_params):
    n_samples = len(X)
    fold_size = n_samples // cv
    scores = []
    
    indices = np.arange(n_samples)
    np.random.shuffle(indices)
    
    for i in range(cv):
        start = i * fold_size
        end = start + fold_size if i < cv - 1 else n_samples
        
        val_indices = indices[start:end]
        train_indices = np.concatenate([indices[:start], indices[end:]])
        
        X_train, X_val = X[train_indices], X[val_indices]
        y_train, y_val = y[train_indices], y[val_indices]
        
        model = model_class(**model_params)
        model.fit(X_train, y_train)
        scores.append(model.score(X_val, y_val))
    
    return np.array(scores)

# ===== DEMO =====
if __name__ == "__main__":
    print("="*60)
    print("MINI ML FRAMEWORK DEMO")
    print("="*60)
    
    # Generate regression data
    rng = np.random.default_rng(42)
    X_reg = rng.random((200, 5))
    y_reg = 3*X_reg[:, 0] + 2*X_reg[:, 1] - X_reg[:, 2] + rng.normal(0, 0.1, 200)
    
    # Preprocess
    scaler = StandardScaler()
    X_reg_scaled = scaler.fit_transform(X_reg)
    
    # Train linear regression
    print("\n--- Linear Regression ---")
    lr_model = LinearRegressionGD(learning_rate=0.1, epochs=500)
    lr_model.fit(X_reg_scaled, y_reg)
    
    y_pred = lr_model.predict(X_reg_scaled)
    print(f"R² Score: {Metrics.r2(y_reg, y_pred):.4f}")
    print(f"RMSE: {Metrics.rmse(y_reg, y_pred):.4f}")
    
    # Cross-validation
    cv_scores = cross_validate(LinearRegressionGD, X_reg_scaled, y_reg, cv=5, 
                               learning_rate=0.1, epochs=500)
    print(f"CV Scores: {cv_scores.round(4)}")
    print(f"CV Mean: {cv_scores.mean():.4f} (+/- {cv_scores.std():.4f})")
    
    # Generate classification data
    X_cls = rng.random((200, 4))
    y_cls = ((X_cls[:, 0] + X_cls[:, 1]) > 1).astype(int)
    
    X_cls_scaled = scaler.fit_transform(X_cls)
    
    # Train logistic regression
    print("\n--- Logistic Regression ---")
    log_model = LogisticRegressionGD(learning_rate=0.5, epochs=500)
    log_model.fit(X_cls_scaled, y_cls)
    
    y_pred_cls = log_model.predict(X_cls_scaled)
    print(f"Accuracy: {Metrics.accuracy(y_cls, y_pred_cls):.4f}")
    print(f"Confusion Matrix:\n{Metrics.confusion_matrix(y_cls, y_pred_cls)}")
    
    # Cross-validation for classification
    cv_scores = cross_validate(LogisticRegressionGD, X_cls_scaled, y_cls, cv=5,
                               learning_rate=0.5, epochs=500)
    print(f"CV Scores: {cv_scores.round(4)}")
    print(f"CV Mean: {cv_scores.mean():.4f} (+/- {cv_scores.std():.4f})")
    
    print("\n" + "="*60)
    print("FRAMEWORK DEMO COMPLETE!")
    print("="*60)
Quick Reference Card
Array Creation
Python

np.array([1, 2, 3])              # From list
np.zeros((3, 4))                  # Zeros
np.ones((3, 4))                   # Ones
np.full((3, 4), 7)                # Fill with value
np.eye(3)                         # Identity matrix
np.arange(0, 10, 2)               # Range with step
np.linspace(0, 1, 5)              # N evenly spaced
np.random.default_rng().random((3, 4))  # Random
Array Properties
Python

arr.shape      # Dimensions
arr.ndim       # Number of dimensions
arr.size       # Total elements
arr.dtype      # Data type
arr.T          # Transpose
Indexing & Slicing
Python

arr[0]              # First element
arr[-1]             # Last element
arr[1:4]            # Slice
arr[::2]            # Every 2nd
arr[::-1]           # Reverse
arr[arr > 5]        # Boolean indexing
arr[[0, 2, 4]]      # Fancy indexing
Shape Manipulation
Python

arr.reshape(3, 4)        # Reshape
arr.flatten()            # To 1D (copy)
arr.ravel()              # To 1D (view)
np.expand_dims(arr, 0)   # Add dimension
np.squeeze(arr)          # Remove size-1 dims
np.concatenate([a, b])   # Join arrays
np.vstack([a, b])        # Stack vertically
np.hstack([a, b])        # Stack horizontally
Mathematical Operations
Python

arr + 1              # Element-wise add
arr * 2              # Element-wise multiply
arr @ arr2           # Matrix multiply
np.dot(a, b)         # Dot product
np.sqrt(arr)         # Square root
np.exp(arr)          # Exponential
np.log(arr)          # Natural log
np.sin(arr)          # Sine
Aggregations
Python

np.sum(arr)          # Sum all
np.sum(arr, axis=0)  # Sum along axis
np.mean(arr)         # Mean
np.std(arr)          # Standard deviation
np.min(arr)          # Minimum
np.max(arr)          # Maximum
np.argmin(arr)       # Index of min
np.argmax(arr)       # Index of max
Linear Algebra
Python

np.linalg.inv(A)        # Inverse
np.linalg.det(A)        # Determinant
np.linalg.eig(A)        # Eigenvalues/vectors
np.linalg.svd(A)        # SVD
np.linalg.solve(A, b)   # Solve Ax=b
np.linalg.norm(v)       # Norm
Random Numbers
Python

rng = np.random.default_rng(42)
rng.random((3, 4))           # Uniform [0, 1)
rng.integers(0, 10, (3, 4))  # Random integers
rng.normal(0, 1, (3, 4))     # Normal distribution
rng.choice(arr, 5)           # Random choice
rng.shuffle(arr)             # Shuffle in place
rng.permutation(arr)         # Shuffled copy
File I/O
Python

np.save('file.npy', arr)      # Save binary
np.load('file.npy')           # Load binary
np.savez('file.npz', a=a, b=b)  # Save multiple
np.savetxt('file.txt', arr)   # Save text
np.loadtxt('file.txt')        # Load text
Conclusion
Congratulations! 🎉 You have completed the comprehensive NumPy guide covering:

✅ Fundamentals: Arrays, dtypes, shapes, and attributes
✅ Creation: All methods to create arrays
✅ Indexing: Basic, fancy, and boolean indexing
✅ Operations: Arithmetic, comparison, and logical
✅ Broadcasting: The magic of NumPy
✅ Universal Functions: Efficient element-wise operations
✅ Aggregations: Statistical functions
✅ Linear Algebra: Matrix operations, decompositions
✅ Random Numbers: Generation and distributions
✅ File I/O: Saving and loading data
✅ Advanced Topics: Memory layout, structured arrays
✅ ML Applications: Preprocessing, algorithms, neural networks
✅ Best Practices: Common pitfalls and optimization
Next Steps:

Practice with the exercises provided
Build the projects to solidify your understanding
Explore Pandas for data manipulation
Move to Scikit-learn for machine learning
Dive into TensorFlow/PyTorch for deep learning
Remember: NumPy is the foundation of the entire Python data science ecosystem. Master it, and everything else becomes easier!

This guide was created to provide crystal-clear understanding of NumPy from beginner to advanced level. Happy coding! 🚀