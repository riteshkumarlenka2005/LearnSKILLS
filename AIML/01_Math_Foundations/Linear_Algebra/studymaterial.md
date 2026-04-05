📐 Linear Algebra for AI/ML - Complete Mastery Guide
From Zero to Hero: Everything you need to know about Linear Algebra for Artificial Intelligence & Machine Learning

📑 Table of Contents
Why Linear Algebra for AI/ML?
Prerequisites
Chapter 1: Scalars, Vectors, and Matrices - The Building Blocks
Chapter 2: Vector Operations
Chapter 3: Matrix Operations
Chapter 4: Special Matrices
Chapter 5: Matrix Transpose and Symmetry
Chapter 6: Linear Transformations
Chapter 7: Determinants
Chapter 8: Matrix Inverse
Chapter 9: Solving Linear Systems
Chapter 10: Vector Spaces and Subspaces
Chapter 11: Linear Independence and Basis
Chapter 12: Rank and Nullity
Chapter 13: Eigenvalues and Eigenvectors
Chapter 14: Matrix Decompositions
Chapter 15: Singular Value Decomposition (SVD)
Chapter 16: Principal Component Analysis (PCA)
Chapter 17: Linear Algebra in Neural Networks
Chapter 18: Advanced Topics
Practice Problems
Cheat Sheet
Resources
1. Why Linear Algebra for AI/ML?
🎯 The Big Picture
Linear Algebra is the LANGUAGE of Machine Learning!

Every single ML algorithm uses linear algebra under the hood. When you train a neural network, recommend movies to users, or compress images, you're doing linear algebra.

text

┌─────────────────────────────────────────────────────────────────┐
│              WHERE LINEAR ALGEBRA APPEARS IN ML                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  🧠 NEURAL NETWORKS                                             │
│     └── Weights are matrices, inputs are vectors                │
│     └── Forward pass = Matrix multiplications                   │
│     └── y = Wx + b (linear transformation)                      │
│                                                                 │
│  📊 DATA REPRESENTATION                                         │
│     └── Dataset = Matrix (rows=samples, cols=features)          │
│     └── Images = 3D Tensors (height × width × channels)         │
│     └── Text embeddings = Vectors                               │
│                                                                 │
│  📉 DIMENSIONALITY REDUCTION                                    │
│     └── PCA uses eigenvalues/eigenvectors                       │
│     └── SVD for matrix factorization                            │
│                                                                 │
│  🎯 RECOMMENDATION SYSTEMS                                      │
│     └── Matrix factorization (users × items)                    │
│                                                                 │
│  📈 OPTIMIZATION                                                │
│     └── Gradient vectors                                        │
│     └── Hessian matrices                                        │
│                                                                 │
│  🔍 COMPUTER VISION                                             │
│     └── Image transformations (rotation, scaling)               │
│     └── Convolutions as matrix operations                       │
│                                                                 │
│  📝 NATURAL LANGUAGE PROCESSING                                 │
│     └── Word embeddings (Word2Vec, GloVe)                       │
│     └── Attention mechanisms                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
🤔 Real-World Analogy
Think of linear algebra like a universal translator for data:

Vectors = Single data points (a person's features, a word's meaning)
Matrices = Collections of data or transformations
Matrix multiplication = Applying transformations or computing relationships
Eigenvalues = Finding the "essence" or principal directions in data
2. Prerequisites
Before diving in, make sure you understand:

text

✅ Basic arithmetic operations
✅ Understanding of coordinate systems (x, y plane)
✅ Basic algebra (solving equations)
✅ Familiarity with Python/NumPy (helpful but not required)
3. Chapter 1: Scalars, Vectors, and Matrices - The Building Blocks
📚 Scalars
A scalar is just a single number.

text

Examples of scalars:
  • Temperature: 25°C
  • Age: 30
  • Learning rate: 0.001
  • Loss value: 0.5

In ML:
  • Scalars are often represented by lowercase letters: a, b, c, x, y
  • They can be integers, real numbers, or complex numbers
📚 Vectors
A vector is an ordered list of numbers (a 1D array).

text

┌─────────────────────────────────────────────────────────────────┐
│                         VECTORS                                 │
│                                                                 │
│   Column Vector:              Row Vector:                       │
│        ┌   ┐                                                    │
│        │ 1 │                  [ 1  2  3 ]                       │
│   v =  │ 2 │                                                    │
│        │ 3 │                  Shape: (1, 3) or just (3,)        │
│        └   ┘                                                    │
│   Shape: (3, 1) or (3,)                                         │
│                                                                 │
│   Notation:                                                     │
│   • Boldface lowercase: 𝐯, 𝐱, 𝐲                                 │
│   • Arrow notation: v⃗                                           │
│   • With subscripts: vᵢ refers to i-th element                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Geometric Interpretation:

text

┌─────────────────────────────────────────────────────────────────┐
│                    VECTOR AS ARROW                              │
│                                                                 │
│         y                                                       │
│         │       ↗ v = [3, 2]                                    │
│       2 │      /                                                │
│         │     /                                                 │
│       1 │    /                                                  │
│         │   /                                                   │
│       0 └──────────────── x                                     │
│         0   1   2   3                                           │
│                                                                 │
│   A vector represents:                                          │
│   • A POINT in space: (3, 2)                                    │
│   • A DIRECTION + MAGNITUDE: arrow from origin                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
ML Examples of Vectors:

Python

import numpy as np

# Feature vector for a house
house_features = np.array([
    1500,    # Square footage
    3,       # Bedrooms
    2,       # Bathrooms
    2020,    # Year built
    1        # Has garage (1=yes, 0=no)
])

# Word embedding (simplified)
word_king = np.array([0.2, 0.5, 0.8, -0.3, 0.1])
word_queen = np.array([0.2, 0.5, 0.8, -0.3, -0.1])

# Prediction probabilities (3 classes)
probabilities = np.array([0.1, 0.7, 0.2])  # Sums to 1

# Gradient vector
gradients = np.array([0.05, -0.02, 0.1, 0.03])
📚 Matrices
A matrix is a 2D array of numbers (rows × columns).

text

┌─────────────────────────────────────────────────────────────────┐
│                         MATRICES                                │
│                                                                 │
│        ┌             ┐                                          │
│        │  1   2   3  │                                          │
│   A =  │  4   5   6  │      Shape: 2 × 3 (2 rows, 3 columns)   │
│        └             ┘                                          │
│                                                                 │
│   Notation:                                                     │
│   • Capital letters: A, B, X, W                                 │
│   • Element notation: Aᵢⱼ = element in row i, column j         │
│   • A₁₂ = 2 (row 1, column 2)                                   │
│   • A₂₃ = 6 (row 2, column 3)                                   │
│                                                                 │
│   Shape notation: A ∈ ℝᵐˣⁿ (m rows, n columns, real numbers)   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
ML Examples of Matrices:

Python

import numpy as np

# Dataset: 5 samples, 3 features each
dataset = np.array([
    [1.2, 3.4, 5.6],   # Sample 1
    [2.1, 4.3, 6.5],   # Sample 2
    [3.0, 5.2, 7.4],   # Sample 3
    [4.9, 6.1, 8.3],   # Sample 4
    [5.8, 7.0, 9.2]    # Sample 5
])
print(f"Dataset shape: {dataset.shape}")  # (5, 3)

# Weight matrix in neural network
# 3 input neurons → 4 output neurons
weights = np.random.randn(4, 3)
print(f"Weights shape: {weights.shape}")  # (4, 3)

# Grayscale image (28x28 pixels)
image = np.random.rand(28, 28)
print(f"Image shape: {image.shape}")  # (28, 28)

# Confusion matrix (3 classes)
confusion_matrix = np.array([
    [45, 2, 3],    # True class 0
    [1, 48, 1],    # True class 1
    [2, 3, 45]     # True class 2
])
📚 Tensors
A tensor is a generalization to N dimensions.

text

┌─────────────────────────────────────────────────────────────────┐
│                    TENSOR HIERARCHY                             │
│                                                                 │
│   Scalar     →  0D Tensor  →  Single number           →  5     │
│   Vector     →  1D Tensor  →  List of numbers         →  [1,2,3]│
│   Matrix     →  2D Tensor  →  Table of numbers        →  m × n │
│   3D Tensor  →  3D Tensor  →  Cube of numbers         →  l×m×n │
│   nD Tensor  →  nD Tensor  →  Hypercube of numbers            │
│                                                                 │
│   Examples in ML:                                               │
│   ─────────────                                                 │
│   • RGB Image: (Height, Width, 3)         → 3D Tensor          │
│   • Batch of images: (Batch, H, W, 3)     → 4D Tensor          │
│   • Video: (Time, H, W, 3)                → 4D Tensor          │
│   • Batch of videos: (Batch, T, H, W, 3)  → 5D Tensor          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

# Scalar (0D)
scalar = np.array(5)
print(f"Scalar shape: {scalar.shape}")  # ()

# Vector (1D)
vector = np.array([1, 2, 3])
print(f"Vector shape: {vector.shape}")  # (3,)

# Matrix (2D)
matrix = np.array([[1, 2], [3, 4], [5, 6]])
print(f"Matrix shape: {matrix.shape}")  # (3, 2)

# 3D Tensor (e.g., RGB image)
rgb_image = np.random.rand(224, 224, 3)
print(f"RGB Image shape: {rgb_image.shape}")  # (224, 224, 3)

# 4D Tensor (batch of images)
batch_images = np.random.rand(32, 224, 224, 3)
print(f"Batch shape: {batch_images.shape}")  # (32, 224, 224, 3)
4. Chapter 2: Vector Operations
📚 Vector Addition
Add corresponding elements:

text

┌─────────────────────────────────────────────────────────────────┐
│                    VECTOR ADDITION                              │
│                                                                 │
│   ┌   ┐   ┌   ┐   ┌       ┐                                    │
│   │ 1 │ + │ 4 │ = │ 1 + 4 │   ┌   ┐                            │
│   │ 2 │   │ 5 │   │ 2 + 5 │ = │ 5 │                            │
│   │ 3 │   │ 6 │   │ 3 + 6 │   │ 7 │                            │
│   └   ┘   └   ┘   └       ┘   │ 9 │                            │
│                               └   ┘                            │
│                                                                 │
│   Geometric: Place vectors head-to-tail                         │
│                                                                 │
│        │      ↗ a + b                                           │
│        │     /                                                  │
│        │  b /     ↗ b                                           │
│        │   /     /                                              │
│        │  ↗─────/                                               │
│        │ a                                                      │
│        └────────────                                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Vector addition
c = a + b
print(f"a + b = {c}")  # [5 7 9]

# Vector subtraction
d = a - b
print(f"a - b = {d}")  # [-3 -3 -3]
📚 Scalar Multiplication
Multiply each element by the scalar:

text

┌─────────────────────────────────────────────────────────────────┐
│                    SCALAR MULTIPLICATION                        │
│                                                                 │
│       ┌   ┐   ┌     ┐   ┌   ┐                                  │
│       │ 1 │   │ 3×1 │   │ 3 │                                  │
│   3 × │ 2 │ = │ 3×2 │ = │ 6 │                                  │
│       │ 3 │   │ 3×3 │   │ 9 │                                  │
│       └   ┘   └     ┘   └   ┘                                  │
│                                                                 │
│   Geometric: Scales the vector                                  │
│                                                                 │
│   • c > 1: Stretches the vector                                │
│   • 0 < c < 1: Shrinks the vector                              │
│   • c < 0: Reverses direction                                  │
│   • c = 0: Zero vector                                         │
│                                                                 │
│        │                                                        │
│        │    ↗ 2v                                                │
│        │   /                                                    │
│        │  ↗ v                                                   │
│        │ /                                                      │
│        └─────────                                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

v = np.array([1, 2, 3])

# Scalar multiplication
print(f"3 × v = {3 * v}")      # [3 6 9]
print(f"0.5 × v = {0.5 * v}")  # [0.5 1.0 1.5]
print(f"-1 × v = {-1 * v}")    # [-1 -2 -3]
📚 Dot Product (Inner Product) ⭐ VERY IMPORTANT!
The dot product is the sum of element-wise products.

text

┌─────────────────────────────────────────────────────────────────┐
│                      DOT PRODUCT                                │
│                                                                 │
│   a · b = Σᵢ aᵢbᵢ = a₁b₁ + a₂b₂ + ... + aₙbₙ                    │
│                                                                 │
│   Example:                                                      │
│   a = [1, 2, 3]                                                 │
│   b = [4, 5, 6]                                                 │
│                                                                 │
│   a · b = (1×4) + (2×5) + (3×6)                                │
│         = 4 + 10 + 18                                           │
│         = 32                                                    │
│                                                                 │
│   Result: A SCALAR (single number)!                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Geometric Interpretation:

text

┌─────────────────────────────────────────────────────────────────┐
│              DOT PRODUCT GEOMETRIC MEANING                      │
│                                                                 │
│   a · b = |a| |b| cos(θ)                                        │
│                                                                 │
│   Where:                                                        │
│   • |a| = magnitude (length) of vector a                        │
│   • |b| = magnitude (length) of vector b                        │
│   • θ = angle between vectors                                   │
│                                                                 │
│        │      b                                                 │
│        │     ↗                                                  │
│        │    /                                                   │
│        │   / θ                                                  │
│        │  /                                                     │
│        │ ────────→ a                                            │
│        │                                                        │
│        └────────────                                            │
│                                                                 │
│   Key Insights:                                                 │
│   • a · b > 0: Vectors point in similar direction (θ < 90°)    │
│   • a · b = 0: Vectors are PERPENDICULAR (θ = 90°)             │
│   • a · b < 0: Vectors point in opposite directions (θ > 90°)  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Dot product - multiple ways
dot1 = np.dot(a, b)
dot2 = a @ b
dot3 = np.sum(a * b)

print(f"a · b = {dot1}")  # 32

# Check perpendicularity
v1 = np.array([1, 0])
v2 = np.array([0, 1])
print(f"v1 · v2 = {np.dot(v1, v2)}")  # 0 (perpendicular!)

# Compute angle between vectors
def angle_between(a, b):
    cos_theta = np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))
    return np.arccos(np.clip(cos_theta, -1, 1)) * 180 / np.pi

print(f"Angle between a and b: {angle_between(a, b):.2f}°")
ML Applications of Dot Product:

text

┌─────────────────────────────────────────────────────────────────┐
│              DOT PRODUCT IN MACHINE LEARNING                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. LINEAR REGRESSION PREDICTION                                │
│     ŷ = w · x + b = w₁x₁ + w₂x₂ + ... + wₙxₙ + b               │
│                                                                 │
│  2. NEURAL NETWORK NEURONS                                      │
│     z = w · x + b  (before activation)                          │
│                                                                 │
│  3. COSINE SIMILARITY                                           │
│     sim(a, b) = (a · b) / (|a| |b|)                             │
│     Used in: recommendation systems, NLP, search                │
│                                                                 │
│  4. ATTENTION MECHANISM                                         │
│     score = query · key                                         │
│                                                                 │
│  5. WORD EMBEDDINGS                                             │
│     Similarity between words = dot product of embeddings        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Vector Norm (Magnitude/Length)
The norm measures the "size" or "length" of a vector.

text

┌─────────────────────────────────────────────────────────────────┐
│                      VECTOR NORMS                               │
│                                                                 │
│   L2 Norm (Euclidean norm) - MOST COMMON:                       │
│   ─────────────────────────────────────────                     │
│   ||v||₂ = √(v₁² + v₂² + ... + vₙ²) = √(v · v)                 │
│                                                                 │
│   Example: v = [3, 4]                                           │
│   ||v||₂ = √(3² + 4²) = √(9 + 16) = √25 = 5                    │
│                                                                 │
│   L1 Norm (Manhattan norm):                                     │
│   ─────────────────────────                                     │
│   ||v||₁ = |v₁| + |v₂| + ... + |vₙ|                             │
│                                                                 │
│   Example: v = [3, 4]                                           │
│   ||v||₁ = |3| + |4| = 7                                        │
│                                                                 │
│   L∞ Norm (Max norm):                                           │
│   ───────────────────                                           │
│   ||v||∞ = max(|v₁|, |v₂|, ..., |vₙ|)                           │
│                                                                 │
│   Example: v = [3, 4]                                           │
│   ||v||∞ = max(3, 4) = 4                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Visual Comparison:

text

┌─────────────────────────────────────────────────────────────────┐
│              UNIT CIRCLES IN DIFFERENT NORMS                    │
│                                                                 │
│   All points where ||v|| = 1:                                   │
│                                                                 │
│   L1 Norm:        L2 Norm:        L∞ Norm:                      │
│                                                                 │
│       ◇              ○             □                            │
│      /│\            /│\           ┌─┬─┐                         │
│     / │ \          / │ \          │ │ │                         │
│    ◇──┼──◇        │──●──│         ├─┼─┤                         │
│     \ │ /          \ │ /          │ │ │                         │
│      \│/            \│/           └─┴─┘                         │
│       ◇              ○                                          │
│                                                                 │
│   Diamond         Circle          Square                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

v = np.array([3, 4])

# L2 norm (Euclidean)
l2 = np.linalg.norm(v)           # or np.sqrt(np.sum(v**2))
print(f"L2 norm: {l2}")           # 5.0

# L1 norm (Manhattan)
l1 = np.linalg.norm(v, ord=1)    # or np.sum(np.abs(v))
print(f"L1 norm: {l1}")           # 7.0

# L∞ norm (Max)
linf = np.linalg.norm(v, ord=np.inf)  # or np.max(np.abs(v))
print(f"L∞ norm: {linf}")         # 4.0

# Unit vector (normalize)
unit_v = v / np.linalg.norm(v)
print(f"Unit vector: {unit_v}")   # [0.6, 0.8]
print(f"Its norm: {np.linalg.norm(unit_v)}")  # 1.0
ML Applications of Norms:

text

┌─────────────────────────────────────────────────────────────────┐
│                 NORMS IN MACHINE LEARNING                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. L2 REGULARIZATION (Ridge)                                   │
│     Loss = MSE + λ||w||₂²                                       │
│     Prevents large weights, reduces overfitting                 │
│                                                                 │
│  2. L1 REGULARIZATION (Lasso)                                   │
│     Loss = MSE + λ||w||₁                                        │
│     Encourages sparsity (some weights become exactly 0)         │
│                                                                 │
│  3. GRADIENT CLIPPING                                           │
│     if ||g|| > threshold: g = g × (threshold / ||g||)          │
│     Prevents exploding gradients                                │
│                                                                 │
│  4. NORMALIZATION                                               │
│     x_normalized = x / ||x||                                    │
│     Makes vectors unit length                                   │
│                                                                 │
│  5. DISTANCE METRICS                                            │
│     Euclidean distance: ||a - b||₂                              │
│     Manhattan distance: ||a - b||₁                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Cross Product (3D Only)
The cross product produces a vector perpendicular to both input vectors.

text

┌─────────────────────────────────────────────────────────────────┐
│                      CROSS PRODUCT                              │
│                                                                 │
│   a × b = |a| |b| sin(θ) n̂                                     │
│                                                                 │
│   Where n̂ is unit vector perpendicular to both a and b         │
│                                                                 │
│   Formula:                                                      │
│   ┌   ┐   ┌   ┐   ┌                 ┐                          │
│   │a₁ │   │b₁ │   │ a₂b₃ - a₃b₂    │                          │
│   │a₂ │ × │b₂ │ = │ a₃b₁ - a₁b₃    │                          │
│   │a₃ │   │b₃ │   │ a₁b₂ - a₂b₁    │                          │
│   └   ┘   └   ┘   └                 ┘                          │
│                                                                 │
│   Result: A VECTOR (not scalar like dot product)                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

a = np.array([1, 0, 0])
b = np.array([0, 1, 0])

cross = np.cross(a, b)
print(f"a × b = {cross}")  # [0 0 1] - points in z direction
5. Chapter 3: Matrix Operations
📚 Matrix Addition
Add corresponding elements (matrices must have same shape):

text

┌─────────────────────────────────────────────────────────────────┐
│                    MATRIX ADDITION                              │
│                                                                 │
│   ┌       ┐   ┌       ┐   ┌             ┐   ┌       ┐          │
│   │ 1  2  │ + │ 5  6  │ = │ 1+5   2+6   │ = │ 6   8 │          │
│   │ 3  4  │   │ 7  8  │   │ 3+7   4+8   │   │ 10 12 │          │
│   └       ┘   └       ┘   └             ┘   └       ┘          │
│                                                                 │
│   Rule: Shapes must match!                                      │
│         (m × n) + (m × n) = (m × n)                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Scalar Multiplication
Multiply every element by the scalar:

text

┌─────────────────────────────────────────────────────────────────┐
│                  SCALAR × MATRIX                                │
│                                                                 │
│       ┌       ┐   ┌         ┐   ┌       ┐                      │
│   3 × │ 1  2  │ = │ 3×1 3×2 │ = │ 3   6 │                      │
│       │ 3  4  │   │ 3×3 3×4 │   │ 9  12 │                      │
│       └       ┘   └         ┘   └       ┘                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Matrix Multiplication ⭐⭐⭐ MOST IMPORTANT!
Matrix multiplication is NOT element-wise! It's a specific operation.

text

┌─────────────────────────────────────────────────────────────────┐
│                  MATRIX MULTIPLICATION                          │
│                                                                 │
│   A (m × n) × B (n × p) = C (m × p)                            │
│                                                                 │
│   Rule: # columns of A must equal # rows of B                   │
│         Inner dimensions must match!                            │
│                                                                 │
│   Each element Cᵢⱼ = (row i of A) · (column j of B)            │
│                    = dot product of row and column              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Step-by-Step Example:

text

┌─────────────────────────────────────────────────────────────────┐
│                  MATRIX MULTIPLICATION EXAMPLE                  │
│                                                                 │
│        A (2×3)           B (3×2)           C (2×2)              │
│   ┌           ┐     ┌         ┐     ┌             ┐            │
│   │ 1   2   3 │  ×  │ 7    8  │  =  │ C₁₁   C₁₂  │            │
│   │ 4   5   6 │     │ 9   10  │     │ C₂₁   C₂₂  │            │
│   └           ┘     │ 11  12  │     └             ┘            │
│                     └         ┘                                 │
│                                                                 │
│   C₁₁ = Row1(A) · Col1(B)                                       │
│       = [1,2,3] · [7,9,11]                                      │
│       = 1×7 + 2×9 + 3×11                                        │
│       = 7 + 18 + 33 = 58                                        │
│                                                                 │
│   C₁₂ = Row1(A) · Col2(B)                                       │
│       = [1,2,3] · [8,10,12]                                     │
│       = 1×8 + 2×10 + 3×12                                       │
│       = 8 + 20 + 36 = 64                                        │
│                                                                 │
│   C₂₁ = Row2(A) · Col1(B)                                       │
│       = [4,5,6] · [7,9,11]                                      │
│       = 4×7 + 5×9 + 6×11                                        │
│       = 28 + 45 + 66 = 139                                      │
│                                                                 │
│   C₂₂ = Row2(A) · Col2(B)                                       │
│       = [4,5,6] · [8,10,12]                                     │
│       = 4×8 + 5×10 + 6×12                                       │
│       = 32 + 50 + 72 = 154                                      │
│                                                                 │
│   Result:                                                       │
│   ┌            ┐                                                │
│   │  58    64  │                                                │
│   │ 139   154  │                                                │
│   └            ┘                                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

A = np.array([[1, 2, 3],
              [4, 5, 6]])  # 2×3

B = np.array([[7, 8],
              [9, 10],
              [11, 12]])   # 3×2

# Matrix multiplication
C = A @ B  # or np.matmul(A, B) or np.dot(A, B)
print("A @ B =")
print(C)
# [[ 58  64]
#  [139 154]]

print(f"\nShapes: {A.shape} @ {B.shape} = {C.shape}")
# Shapes: (2, 3) @ (3, 2) = (2, 2)
Important Properties:

text

┌─────────────────────────────────────────────────────────────────┐
│           MATRIX MULTIPLICATION PROPERTIES                      │
│                                                                 │
│   1. NOT COMMUTATIVE: A×B ≠ B×A (generally)                    │
│                                                                 │
│   2. ASSOCIATIVE: (A×B)×C = A×(B×C)                            │
│                                                                 │
│   3. DISTRIBUTIVE: A×(B+C) = A×B + A×C                         │
│                                                                 │
│   4. IDENTITY: A×I = I×A = A                                   │
│                                                                 │
│   5. TRANSPOSE: (A×B)ᵀ = Bᵀ×Aᵀ                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Demonstrate non-commutativity
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print("A @ B =")
print(A @ B)
# [[19 22]
#  [43 50]]

print("\nB @ A =")
print(B @ A)
# [[23 34]
#  [31 46]]

print("\nA @ B ≠ B @ A:", not np.array_equal(A @ B, B @ A))  # True
📚 Matrix-Vector Multiplication
A matrix times a vector = another vector.

text

┌─────────────────────────────────────────────────────────────────┐
│              MATRIX-VECTOR MULTIPLICATION                       │
│                                                                 │
│   ┌       ┐   ┌   ┐   ┌               ┐   ┌    ┐               │
│   │ 1  2  │ × │ x │ = │ 1×x + 2×y     │ = │ Ax │               │
│   │ 3  4  │   │ y │   │ 3×x + 4×y     │   │    │               │
│   └       ┘   └   ┘   └               ┘   └    ┘               │
│                                                                 │
│   With numbers:                                                 │
│   ┌       ┐   ┌   ┐   ┌           ┐   ┌    ┐                   │
│   │ 1  2  │ × │ 5 │ = │ 1×5 + 2×6 │ = │ 17 │                   │
│   │ 3  4  │   │ 6 │   │ 3×5 + 4×6 │   │ 39 │                   │
│   └       ┘   └   ┘   └           ┘   └    ┘                   │
│                                                                 │
│   This is THE FUNDAMENTAL operation in neural networks!         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
This is Neural Network Forward Pass!

Python

# Neural Network Layer as Matrix-Vector Multiplication
import numpy as np

# Input: 3 features
x = np.array([0.5, 0.3, 0.2])

# Weight matrix: 3 inputs → 4 neurons
W = np.random.randn(4, 3)

# Bias: 4 neurons
b = np.random.randn(4)

# Forward pass (linear transformation)
z = W @ x + b  # This is it! Matrix-vector multiplication

print(f"Input shape: {x.shape}")      # (3,)
print(f"Weight shape: {W.shape}")     # (4, 3)
print(f"Output shape: {z.shape}")     # (4,)
📚 Element-wise Operations (Hadamard Product)
Sometimes we DO want element-wise operations:

text

┌─────────────────────────────────────────────────────────────────┐
│              ELEMENT-WISE (HADAMARD) PRODUCT                    │
│                                                                 │
│   A ⊙ B = element-by-element multiplication                     │
│                                                                 │
│   ┌       ┐   ┌       ┐   ┌         ┐   ┌       ┐              │
│   │ 1  2  │ ⊙ │ 5  6  │ = │ 1×5 2×6 │ = │ 5  12 │              │
│   │ 3  4  │   │ 7  8  │   │ 3×7 4×8 │   │ 21 32 │              │
│   └       ┘   └       ┘   └         ┘   └       ┘              │
│                                                                 │
│   In NumPy: A * B (NOT A @ B!)                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Element-wise multiplication
hadamard = A * B
print("A ⊙ B =")
print(hadamard)
# [[ 5 12]
#  [21 32]]

# This is different from matrix multiplication!
matmul = A @ B
print("\nA @ B =")
print(matmul)
# [[19 22]
#  [43 50]]
📚 Broadcasting
NumPy's broadcasting allows operations between arrays of different shapes:

text

┌─────────────────────────────────────────────────────────────────┐
│                      BROADCASTING                               │
│                                                                 │
│   Matrix + Vector (adds vector to each row):                    │
│                                                                 │
│   ┌       ┐                 ┌         ┐                        │
│   │ 1  2  │ + [10, 20]  =   │ 11  22  │                        │
│   │ 3  4  │                 │ 13  24  │                        │
│   │ 5  6  │                 │ 15  26  │                        │
│   └       ┘                 └         ┘                        │
│                                                                 │
│   The vector [10, 20] is "broadcast" to each row               │
│                                                                 │
│   This is how we add bias in neural networks!                   │
│   z = Wx + b  (b is broadcast across batch)                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Broadcasting example
A = np.array([[1, 2],
              [3, 4],
              [5, 6]])

b = np.array([10, 20])

result = A + b
print("A + b =")
print(result)
# [[11 22]
#  [13 24]
#  [15 26]]
6. Chapter 4: Special Matrices
📚 Identity Matrix (I)
The "1" of matrix multiplication:

text

┌─────────────────────────────────────────────────────────────────┐
│                    IDENTITY MATRIX                              │
│                                                                 │
│   I₂ = ┌       ┐    I₃ = ┌           ┐    I₄ = ┌               ┐│
│        │ 1  0  │         │ 1  0  0   │         │ 1  0  0  0   ││
│        │ 0  1  │         │ 0  1  0   │         │ 0  1  0  0   ││
│        └       ┘         │ 0  0  1   │         │ 0  0  1  0   ││
│                          └           ┘         │ 0  0  0  1   ││
│                                                └               ┘│
│   Properties:                                                   │
│   • Diagonal elements = 1                                       │
│   • All other elements = 0                                      │
│   • AI = IA = A (identity property)                            │
│   • I⁻¹ = I                                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Create identity matrices
I3 = np.eye(3)
print("I₃ =")
print(I3)
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]

# Verify identity property
A = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

print("\nA @ I = A?", np.allclose(A @ I3, A))  # True
print("I @ A = A?", np.allclose(I3 @ A, A))   # True
📚 Zero Matrix
The "0" of matrix addition:

text

┌─────────────────────────────────────────────────────────────────┐
│                      ZERO MATRIX                                │
│                                                                 │
│   O = ┌       ┐         Properties:                             │
│       │ 0  0  │         • A + O = A                             │
│       │ 0  0  │         • A × O = O                             │
│       └       ┘         • O × A = O                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

zeros = np.zeros((3, 4))  # 3×4 zero matrix
📚 Diagonal Matrix
Non-zero elements only on the main diagonal:

text

┌─────────────────────────────────────────────────────────────────┐
│                    DIAGONAL MATRIX                              │
│                                                                 │
│   D = ┌           ┐                                             │
│       │ 2  0  0   │    diag(d) where d = [2, 5, 3]             │
│       │ 0  5  0   │                                             │
│       │ 0  0  3   │                                             │
│       └           ┘                                             │
│                                                                 │
│   Properties:                                                   │
│   • Easy to compute powers: D^n has diagonal elements dᵢⁿ      │
│   • Easy to invert: D⁻¹ has diagonal elements 1/dᵢ             │
│   • D × v scales each component of v by diagonal element        │
│                                                                 │
│   ML Use: Scaling, covariance matrices (sometimes)              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Create diagonal matrix
d = np.array([2, 5, 3])
D = np.diag(d)
print("D =")
print(D)
# [[2 0 0]
#  [0 5 0]
#  [0 0 3]]

# Extract diagonal from matrix
diag_elements = np.diag(D)
print(f"Diagonal: {diag_elements}")  # [2 5 3]
📚 Symmetric Matrix
A matrix equal to its transpose:

text

┌─────────────────────────────────────────────────────────────────┐
│                    SYMMETRIC MATRIX                             │
│                                                                 │
│   A = Aᵀ                                                        │
│                                                                 │
│   S = ┌           ┐     Sᵀ = ┌           ┐                     │
│       │ 1  2  3   │          │ 1  2  3   │                     │
│       │ 2  4  5   │          │ 2  4  5   │   S = Sᵀ ✓          │
│       │ 3  5  6   │          │ 3  5  6   │                     │
│       └           ┘          └           ┘                     │
│                                                                 │
│   Properties:                                                   │
│   • Symmetric about main diagonal                               │
│   • All eigenvalues are REAL                                    │
│   • Eigenvectors are orthogonal                                 │
│                                                                 │
│   ML Examples:                                                  │
│   • Covariance matrix                                           │
│   • Kernel matrices (Gram matrices)                             │
│   • Distance matrices                                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Covariance matrix is always symmetric
data = np.random.randn(100, 3)
cov_matrix = np.cov(data.T)
print("Covariance matrix:")
print(cov_matrix)
print(f"\nIs symmetric? {np.allclose(cov_matrix, cov_matrix.T)}")  # True
📚 Orthogonal Matrix
A matrix whose transpose equals its inverse:

text

┌─────────────────────────────────────────────────────────────────┐
│                   ORTHOGONAL MATRIX                             │
│                                                                 │
│   Q is orthogonal if: QᵀQ = QQᵀ = I                            │
│                       Q⁻¹ = Qᵀ                                  │
│                                                                 │
│   Properties:                                                   │
│   • Columns are orthonormal (perpendicular, unit length)        │
│   • Rows are orthonormal                                        │
│   • Preserves lengths: ||Qx|| = ||x||                          │
│   • Preserves angles                                            │
│   • det(Q) = ±1                                                 │
│                                                                 │
│   Example (rotation matrix):                                    │
│                                                                 │
│   R(θ) = ┌                 ┐                                   │
│          │ cos(θ)  -sin(θ) │   Rotates by angle θ              │
│          │ sin(θ)   cos(θ) │                                   │
│          └                 ┘                                   │
│                                                                 │
│   ML Use: PCA, orthogonal initialization, rotation              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Rotation matrix
theta = np.pi / 4  # 45 degrees
R = np.array([[np.cos(theta), -np.sin(theta)],
              [np.sin(theta), np.cos(theta)]])

print("R =")
print(R)

# Verify orthogonality
print(f"\nRᵀR = I? {np.allclose(R.T @ R, np.eye(2))}")  # True

# Verify it preserves length
v = np.array([3, 4])
rotated_v = R @ v
print(f"\n||v|| = {np.linalg.norm(v):.4f}")           # 5.0
print(f"||Rv|| = {np.linalg.norm(rotated_v):.4f}")   # 5.0
📚 Positive Definite Matrix
A symmetric matrix where xᵀAx > 0 for all non-zero x:

text

┌─────────────────────────────────────────────────────────────────┐
│              POSITIVE DEFINITE MATRIX                           │
│                                                                 │
│   A is positive definite if:                                    │
│   • A is symmetric                                              │
│   • xᵀAx > 0 for all x ≠ 0                                     │
│                                                                 │
│   Equivalent conditions:                                        │
│   • All eigenvalues > 0                                         │
│   • All leading principal minors > 0                            │
│   • Unique Cholesky decomposition exists                        │
│                                                                 │
│   Positive SEMI-definite: xᵀAx ≥ 0 (eigenvalues ≥ 0)           │
│                                                                 │
│   ML Examples:                                                  │
│   • Covariance matrices (positive semi-definite)                │
│   • Kernel matrices                                             │
│   • Hessian at local minimum                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Check if matrix is positive definite
A = np.array([[4, 2],
              [2, 3]])

# Method 1: Check eigenvalues
eigenvalues = np.linalg.eigvalsh(A)  # eigvalsh for symmetric matrices
print(f"Eigenvalues: {eigenvalues}")
print(f"All positive? {np.all(eigenvalues > 0)}")  # True

# Method 2: Try Cholesky decomposition
try:
    L = np.linalg.cholesky(A)
    print("Cholesky decomposition exists - positive definite!")
except np.linalg.LinAlgError:
    print("Not positive definite")
7. Chapter 5: Matrix Transpose and Symmetry
📚 Matrix Transpose
Flip rows and columns:

text

┌─────────────────────────────────────────────────────────────────┐
│                    MATRIX TRANSPOSE                             │
│                                                                 │
│   A = ┌         ┐      Aᵀ = ┌         ┐                        │
│       │ 1  2  3 │           │ 1  4    │                        │
│       │ 4  5  6 │           │ 2  5    │                        │
│       └         ┘           │ 3  6    │                        │
│                             └         ┘                        │
│   (2×3)                     (3×2)                              │
│                                                                 │
│   Rule: (Aᵀ)ᵢⱼ = Aⱼᵢ                                            │
│                                                                 │
│   Properties:                                                   │
│   • (Aᵀ)ᵀ = A                                                   │
│   • (A + B)ᵀ = Aᵀ + Bᵀ                                          │
│   • (cA)ᵀ = cAᵀ                                                 │
│   • (AB)ᵀ = BᵀAᵀ   ← Note the reverse order!                   │
│   • (ABC)ᵀ = CᵀBᵀAᵀ                                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

A = np.array([[1, 2, 3],
              [4, 5, 6]])

print("A =")
print(A)
print(f"Shape: {A.shape}")  # (2, 3)

print("\nAᵀ =")
print(A.T)
print(f"Shape: {A.T.shape}")  # (3, 2)

# Verify (AB)ᵀ = BᵀAᵀ
B = np.array([[1, 2],
              [3, 4],
              [5, 6]])

left = (A @ B).T
right = B.T @ A.T
print(f"\n(AB)ᵀ = BᵀAᵀ? {np.allclose(left, right)}")  # True
📚 Vector Transposes
For vectors, transpose converts between row and column:

text

┌─────────────────────────────────────────────────────────────────┐
│                    VECTOR TRANSPOSE                             │
│                                                                 │
│   Column vector → Row vector:                                   │
│                                                                 │
│   ┌   ┐ᵀ                                                        │
│   │ 1 │  = [1, 2, 3]                                           │
│   │ 2 │                                                         │
│   │ 3 │                                                         │
│   └   ┘                                                         │
│                                                                 │
│   Important for dot product:                                    │
│   xᵀy = x · y (dot product as matrix multiplication)            │
│                                                                 │
│   ┌   ┐ᵀ   ┌   ┐                                               │
│   │ 1 │  × │ 4 │ = [1,2,3] × [4,5,6]ᵀ                          │
│   │ 2 │    │ 5 │                                                │
│   │ 3 │    │ 6 │                                                │
│   └   ┘    └   ┘                                                │
│                                                                 │
│   = 1×4 + 2×5 + 3×6 = 32                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Outer Product
Vector × Vector transpose = Matrix:

text

┌─────────────────────────────────────────────────────────────────┐
│                      OUTER PRODUCT                              │
│                                                                 │
│   Inner (dot) product: xᵀy = scalar                             │
│   Outer product: xyᵀ = matrix                                   │
│                                                                 │
│   ┌   ┐                   ┌               ┐                    │
│   │ 1 │ × [4, 5, 6] =     │ 1×4  1×5  1×6 │   ┌         ┐      │
│   │ 2 │                   │ 2×4  2×5  2×6 │ = │ 4  5  6 │      │
│   │ 3 │                   │ 3×4  3×5  3×6 │   │ 8 10 12 │      │
│   └   ┘                   └               ┘   │12 15 18 │      │
│                                               └         ┘      │
│                                                                 │
│   ML Use: Weight updates, attention matrices, covariance        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

x = np.array([[1], [2], [3]])  # Column vector
y = np.array([[4], [5], [6]])  # Column vector

# Inner product (scalar)
inner = x.T @ y
print(f"Inner product xᵀy = {inner[0,0]}")  # 32

# Outer product (matrix)
outer = x @ y.T
print(f"\nOuter product xyᵀ =")
print(outer)
# [[ 4  5  6]
#  [ 8 10 12]
#  [12 15 18]]
8. Chapter 6: Linear Transformations
📚 What is a Linear Transformation?
Matrix multiplication IS a linear transformation!

text

┌─────────────────────────────────────────────────────────────────┐
│                LINEAR TRANSFORMATION                            │
│                                                                 │
│   A function T: ℝⁿ → ℝᵐ is LINEAR if:                           │
│                                                                 │
│   1. T(u + v) = T(u) + T(v)        (additivity)                │
│   2. T(cu) = cT(u)                 (homogeneity)               │
│                                                                 │
│   Every linear transformation can be represented by a matrix!   │
│                                                                 │
│   T(x) = Ax                                                     │
│                                                                 │
│   The matrix A completely defines the transformation.           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📐 Geometric Examples
text

┌─────────────────────────────────────────────────────────────────┐
│           COMMON LINEAR TRANSFORMATIONS (2D)                    │
│                                                                 │
│   1. SCALING:                                                   │
│      ┌       ┐                                                  │
│      │ 2  0  │  Scales x by 2, y by 3                          │
│      │ 0  3  │                                                  │
│      └       ┘                                                  │
│                                                                 │
│   2. ROTATION (by θ):                                           │
│      ┌                   ┐                                      │
│      │ cos(θ)   -sin(θ)  │                                     │
│      │ sin(θ)    cos(θ)  │                                     │
│      └                   ┘                                      │
│                                                                 │
│   3. REFLECTION (about x-axis):                                 │
│      ┌        ┐                                                 │
│      │  1   0 │                                                 │
│      │  0  -1 │                                                 │
│      └        ┘                                                 │
│                                                                 │
│   4. SHEAR:                                                     │
│      ┌       ┐                                                  │
│      │ 1  k  │  Shears horizontally by factor k                │
│      │ 0  1  │                                                  │
│      └       ┘                                                  │
│                                                                 │
│   5. PROJECTION (onto x-axis):                                  │
│      ┌       ┐                                                  │
│      │ 1  0  │                                                  │
│      │ 0  0  │                                                  │
│      └       ┘                                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np
import matplotlib.pyplot as plt

# Original points (unit square)
square = np.array([[0, 0], [1, 0], [1, 1], [0, 1], [0, 0]]).T

def plot_transformation(A, title):
    transformed = A @ square
    
    plt.figure(figsize=(10, 5))
    
    plt.subplot(1, 2, 1)
    plt.plot(square[0], square[1], 'b-', linewidth=2)
    plt.fill(square[0], square[1], alpha=0.3)
    plt.title('Original')
    plt.xlim(-2, 3)
    plt.ylim(-2, 3)
    plt.grid(True)
    plt.axis('equal')
    
    plt.subplot(1, 2, 2)
    plt.plot(transformed[0], transformed[1], 'r-', linewidth=2)
    plt.fill(transformed[0], transformed[1], alpha=0.3, color='red')
    plt.title(f'After: {title}')
    plt.xlim(-2, 3)
    plt.ylim(-2, 3)
    plt.grid(True)
    plt.axis('equal')
    
    plt.tight_layout()
    plt.show()

# Scaling
A_scale = np.array([[2, 0], [0, 0.5]])
plot_transformation(A_scale, 'Scaling (2x, 0.5y)')

# Rotation (45 degrees)
theta = np.pi / 4
A_rotate = np.array([[np.cos(theta), -np.sin(theta)],
                      [np.sin(theta), np.cos(theta)]])
plot_transformation(A_rotate, 'Rotation (45°)')

# Shear
A_shear = np.array([[1, 0.5], [0, 1]])
plot_transformation(A_shear, 'Shear')
📚 Neural Network as Transformation
Each layer in a neural network is a linear transformation (+ non-linear activation):

text

┌─────────────────────────────────────────────────────────────────┐
│         NEURAL NETWORK = SEQUENCE OF TRANSFORMATIONS            │
│                                                                 │
│   Input x ∈ ℝ³                                                  │
│      │                                                          │
│      ▼                                                          │
│   ┌─────────────────┐                                           │
│   │ z₁ = W₁x + b₁   │  Linear transformation (ℝ³ → ℝ⁴)        │
│   │ h₁ = σ(z₁)      │  Non-linear activation                   │
│   └─────────────────┘                                           │
│      │                                                          │
│      ▼                                                          │
│   ┌─────────────────┐                                           │
│   │ z₂ = W₂h₁ + b₂  │  Linear transformation (ℝ⁴ → ℝ²)        │
│   │ h₂ = σ(z₂)      │  Non-linear activation                   │
│   └─────────────────┘                                           │
│      │                                                          │
│      ▼                                                          │
│   Output y ∈ ℝ²                                                 │
│                                                                 │
│   The network learns W₁, b₁, W₂, b₂ that transform input       │
│   space to output space!                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9. Chapter 7: Determinants
📚 What is a Determinant?
The determinant is a scalar value that describes certain properties of a matrix.

text

┌─────────────────────────────────────────────────────────────────┐
│                      DETERMINANT                                │
│                                                                 │
│   For 2×2 matrix:                                               │
│                                                                 │
│   A = ┌       ┐                                                 │
│       │ a  b  │    det(A) = |A| = ad - bc                      │
│       │ c  d  │                                                 │
│       └       ┘                                                 │
│                                                                 │
│   Example:                                                      │
│   A = ┌       ┐                                                 │
│       │ 3  1  │    det(A) = 3×4 - 1×2 = 12 - 2 = 10           │
│       │ 2  4  │                                                 │
│       └       ┘                                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📐 Geometric Meaning
The determinant represents the scaling factor of area/volume:

text

┌─────────────────────────────────────────────────────────────────┐
│           DETERMINANT = AREA/VOLUME SCALE FACTOR                │
│                                                                 │
│   2D: det(A) = area of parallelogram / unit square area        │
│   3D: det(A) = volume of parallelepiped / unit cube volume     │
│                                                                 │
│   Before transform:        After transform (A):                 │
│                                                                 │
│       ┌──┐                    ╱╲                                │
│       │  │  Area = 1         ╱  ╲    Area = |det(A)|           │
│       └──┘                  ╱    ╲                              │
│                            ╱──────╲                             │
│                                                                 │
│   If det(A) > 0: Orientation preserved                         │
│   If det(A) < 0: Orientation flipped (mirror)                  │
│   If det(A) = 0: Squished to lower dimension (SINGULAR)        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 3×3 Determinant
text

┌─────────────────────────────────────────────────────────────────┐
│                   3×3 DETERMINANT                               │
│                                                                 │
│       ┌           ┐                                             │
│   A = │ a  b  c   │                                             │
│       │ d  e  f   │                                             │
│       │ g  h  i   │                                             │
│       └           ┘                                             │
│                                                                 │
│   det(A) = a(ei - fh) - b(di - fg) + c(dh - eg)                │
│                                                                 │
│   (Expansion along first row using cofactors)                   │
│                                                                 │
│   Or use the "Rule of Sarrus" (diagonals method)               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Computing determinants
A_2x2 = np.array([[3, 1],
                   [2, 4]])
print(f"det(A_2x2) = {np.linalg.det(A_2x2)}")  # 10.0

A_3x3 = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
print(f"det(A_3x3) = {np.linalg.det(A_3x3):.10f}")  # ~0 (singular!)

A_3x3_invertible = np.array([[1, 2, 3],
                              [0, 1, 4],
                              [5, 6, 0]])
print(f"det(A_3x3_inv) = {np.linalg.det(A_3x3_invertible)}")  # 1.0
📚 Properties of Determinants
text

┌─────────────────────────────────────────────────────────────────┐
│              DETERMINANT PROPERTIES                             │
│                                                                 │
│   1. det(I) = 1                                                 │
│                                                                 │
│   2. det(AB) = det(A) × det(B)                                 │
│                                                                 │
│   3. det(Aᵀ) = det(A)                                           │
│                                                                 │
│   4. det(A⁻¹) = 1/det(A)                                        │
│                                                                 │
│   5. det(cA) = cⁿ × det(A)  for n×n matrix                     │
│                                                                 │
│   6. Swapping rows: det changes sign                           │
│                                                                 │
│   7. Row of zeros: det = 0                                     │
│                                                                 │
│   8. Two identical rows: det = 0                               │
│                                                                 │
│   9. det(A) = 0 ⟺ A is SINGULAR (not invertible)              │
│                                                                 │
│   10. det(A) = product of eigenvalues                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 ML Applications
text

┌─────────────────────────────────────────────────────────────────┐
│              DETERMINANTS IN ML                                 │
│                                                                 │
│   1. GAUSSIAN DISTRIBUTION                                      │
│      Normalization constant includes 1/√det(Σ)                  │
│      p(x) = (1/√((2π)ⁿdet(Σ))) exp(-½(x-μ)ᵀΣ⁻¹(x-μ))          │
│                                                                 │
│   2. CHECKING MATRIX INVERTIBILITY                              │
│      det(A) ≠ 0 → A is invertible                              │
│      det(A) = 0 → A is singular, no inverse exists             │
│                                                                 │
│   3. CHANGE OF VARIABLES (Integration)                          │
│      Jacobian determinant for transformations                   │
│                                                                 │
│   4. VOLUME IN HIGH DIMENSIONS                                  │
│      det(Σ) measures "spread" of distribution                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10. Chapter 8: Matrix Inverse
📚 What is the Inverse?
The inverse A⁻¹ is the matrix that "undoes" A:

text

┌─────────────────────────────────────────────────────────────────┐
│                    MATRIX INVERSE                               │
│                                                                 │
│   AA⁻¹ = A⁻¹A = I                                               │
│                                                                 │
│   Think of it as "division" for matrices:                       │
│   If Ax = b, then x = A⁻¹b                                      │
│                                                                 │
│   For 2×2 matrix:                                               │
│   A = ┌       ┐       A⁻¹ = (1/det(A)) ┌        ┐              │
│       │ a  b  │                         │  d  -b │              │
│       │ c  d  │                         │ -c   a │              │
│       └       ┘                         └        ┘              │
│                                                                 │
│   Example:                                                      │
│   A = ┌       ┐       det(A) = 4×4 - 2×3 = 10                  │
│       │ 4  2  │                                                 │
│       │ 3  4  │       A⁻¹ = (1/10) ┌        ┐   ┌           ┐  │
│       └       ┘                     │  4  -2 │ = │ 0.4  -0.2│  │
│                                     │ -3   4 │   │-0.3   0.4│  │
│                                     └        ┘   └           ┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

A = np.array([[4, 2],
              [3, 4]])

# Compute inverse
A_inv = np.linalg.inv(A)
print("A⁻¹ =")
print(A_inv)
# [[ 0.4 -0.2]
#  [-0.3  0.4]]

# Verify AA⁻¹ = I
print("\nAA⁻¹ =")
print(A @ A_inv)
# [[1. 0.]
#  [0. 1.]]

print(f"\nAA⁻¹ ≈ I?