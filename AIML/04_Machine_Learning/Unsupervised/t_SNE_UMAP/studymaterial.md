The Ultimate Guide to t-SNE & UMAP
From Absolute Zero to Complete Mastery
📚 TABLE OF CONTENTS
Foundation: Why Do We Need Dimensionality Reduction?
Understanding High-Dimensional Data
The Journey to t-SNE: Historical Context
t-SNE: The Complete Deep Dive
UMAP: The Modern Revolution
t-SNE vs UMAP: The Ultimate Comparison
Practical Implementation Guide
Hyperparameter Mastery
Common Pitfalls & How to Avoid Them
Advanced Techniques & Tricks
Real-World Applications
Interview Questions & Answers
Quick Reference Cheat Sheet
<a name="chapter-1"></a>

📖 CHAPTER 1: Foundation - Why Do We Need Dimensionality Reduction?
1.1 The Problem Statement
Imagine you have a spreadsheet with information about 1000 customers. Each customer has 500 different attributes (columns):

Age, income, purchase history, browsing patterns, location data, preferences...
Question: How do you VISUALIZE this data to find patterns?

Problem: Humans can only see in 2D (paper/screen) or 3D (with some tricks). We CANNOT visualize 500 dimensions!

text

Human Vision Capability:
├── 1D: A line ✓
├── 2D: A flat surface (x, y) ✓
├── 3D: A cube (x, y, z) ✓ (with some effort)
├── 4D: ??? ✗
├── 5D: ??? ✗
└── 500D: IMPOSSIBLE ✗
1.2 What is Dimensionality Reduction?
Simple Definition: Converting data from HIGH dimensions to LOW dimensions while PRESERVING important information.

text

BEFORE: Data in 500 dimensions (impossible to visualize)
           ↓
    [Dimensionality Reduction Algorithm]
           ↓
AFTER:  Data in 2 dimensions (easy to plot and see patterns!)
1.3 Real-Life Analogy
The Shadow Analogy 🔦
Imagine a 3D object (like a coffee mug) with light shining on it:

text

        3D Object (Mug)
              │
              │ Light Source
              ▼
    ┌─────────────────┐
    │   2D Shadow     │  ← This shadow is a "dimensionality reduction"
    │   on the wall   │     of the 3D mug!
    └─────────────────┘
The shadow (2D) captures SOME information about the mug (3D), but not everything. The goal of good dimensionality reduction is to capture the MOST IMPORTANT information.

1.4 Types of Dimensionality Reduction
text

Dimensionality Reduction Techniques
│
├── LINEAR Methods (assume straight-line relationships)
│   ├── PCA (Principal Component Analysis)
│   ├── LDA (Linear Discriminant Analysis)
│   └── Factor Analysis
│
└── NON-LINEAR Methods (can capture curved/complex relationships)
    ├── t-SNE ⭐ (Our Focus)
    ├── UMAP ⭐ (Our Focus)
    ├── Isomap
    ├── LLE (Locally Linear Embedding)
    └── Autoencoders
1.5 Why Not Just Use PCA?
PCA is the most famous dimensionality reduction technique. So why do we need t-SNE and UMAP?

PCA Limitation: It's LINEAR
text

Scenario: Data shaped like a SWISS ROLL (spiral in 3D)

PCA Result:           t-SNE/UMAP Result:
                      
  ████████████          ███
  ████████████            ███
  ████████████              ███
  (All squished              ███
   together!)                  ███
                                 ███
                                   ███
                              (Beautiful spiral
                               unrolled!)
Key Insight:

PCA finds the "best straight lines" in data
t-SNE/UMAP find the "best curved surfaces" that preserve local relationships
<a name="chapter-2"></a>

📖 CHAPTER 2: Understanding High-Dimensional Data
2.1 What is a "Dimension"?
One Dimension = One Feature/Attribute/Column of your data

text

Example: Student Data

Student | Height | Weight | Age | GPA | Hours_Studied
--------|--------|--------|-----|-----|---------------
Alice   | 165    | 60     | 20  | 3.8 | 25
Bob     | 180    | 75     | 22  | 3.2 | 15

This data has 5 DIMENSIONS (5 columns of numbers)
2.2 Visualizing Dimensions
text

1 Dimension:
A single number line
├────────────────────────►
0    25    50    75    100


2 Dimensions:
A flat plane (x-y graph)
▲ y
│    •  •
│  •    •  •
│    •  •
└──────────────► x


3 Dimensions:
A cube/space (x-y-z)
      z
      ▲
     /│
    / │
   /  │
  ────┼────► y
 /    │
▼     │
x


4+ Dimensions:
CANNOT be visualized directly by humans!
We need MATHEMATICAL representations only.
2.3 The Curse of Dimensionality
As dimensions increase, strange things happen:

Problem 1: Data Becomes Sparse
text

1D: Line of length 10
    - 10 points fill it nicely
    
2D: Square of 10 × 10 = 100 area
    - Need 100 points to fill it
    
3D: Cube of 10 × 10 × 10 = 1,000 volume
    - Need 1,000 points to fill it
    
100D: Hypercube of 10^100 "volume"
    - Need 10^100 points to fill it (more than atoms in universe!)
Consequence: In high dimensions, all points appear FAR from each other. Data becomes "sparse" and "empty."

Problem 2: Distance Becomes Meaningless
text

In high dimensions:
- Nearest neighbor and farthest neighbor become almost EQUALLY distant
- Traditional distance metrics (Euclidean) become unreliable
2.4 What is "Distance" Between Data Points?
Euclidean Distance (Most Common)
text

For 2D points A(x₁, y₁) and B(x₂, y₂):

Distance = √[(x₂-x₁)² + (y₂-y₁)²]

Example:
A = (0, 0)
B = (3, 4)

Distance = √[(3-0)² + (4-0)²]
         = √[9 + 16]
         = √25
         = 5
For Higher Dimensions
text

For n-dimensional points:

Distance = √[(x₁-y₁)² + (x₂-y₂)² + ... + (xₙ-yₙ)²]

         = √[Σᵢ(xᵢ - yᵢ)²]
2.5 Why Preserving "Neighborhood" Matters
The KEY insight behind t-SNE and UMAP:

If two points are NEIGHBORS (close) in high dimensions, they should REMAIN neighbors in low dimensions!

text

High Dimensional Space (500D):
    
    Point A ←──close──→ Point B
         ↑
         │ far
         ↓
    Point C

After Dimensionality Reduction (2D):

    Point A ←──close──→ Point B    ✓ GOOD! Preserved!
         ↑
         │ far
         ↓
    Point C                        ✓ GOOD! Preserved!
This is called preserving the local structure or neighborhood preservation.

<a name="chapter-3"></a>

📖 CHAPTER 3: The Journey to t-SNE - Historical Context
3.1 The Evolution Timeline
text

1901: PCA invented by Karl Pearson
  │   (Linear dimensionality reduction)
  ▼
1960s-90s: Various nonlinear methods explored
  │   (MDS, Sammon Mapping)
  ▼
2000: Isomap & LLE published
  │   (Manifold learning begins)
  ▼
2002: SNE (Stochastic Neighbor Embedding) by Hinton & Roweis
  │   (Predecessor to t-SNE)
  ▼
2008: t-SNE published by van der Maaten & Hinton ⭐
  │   (Game changer for visualization!)
  ▼
2018: UMAP published by McInnes, Healy & Melville ⭐
      (Faster, more scalable, preserves global structure better)
3.2 Understanding SNE (The Predecessor)
Before t-SNE, there was SNE. Understanding SNE helps understand t-SNE.

Core Idea of SNE
text

Step 1: In HIGH-dimensional space
        - Calculate probability that point j is neighbor of point i
        
Step 2: In LOW-dimensional space (what we're creating)
        - Calculate the SAME probability
        
Step 3: Make these two probabilities MATCH!
        - Adjust the low-dimensional positions until probabilities match
3.3 Why SNE Wasn't Perfect
SNE had problems:

text

Problem 1: CROWDING PROBLEM
          - Points in center get too crowded
          - No space to represent all neighbors
          
Problem 2: ASYMMETRIC PROBABILITIES
          - P(j is neighbor of i) ≠ P(i is neighbor of j)
          - Made optimization difficult
          
Problem 3: DIFFICULT TO OPTIMIZE
          - Cost function had many bad local minima
3.4 How t-SNE Fixed These Problems
text

FIX for Crowding Problem:
└── Use t-distribution instead of Gaussian in low-dimensional space
    └── t-distribution has "heavier tails"
        └── Allows distant points to be modeled further apart

FIX for Asymmetry:
└── Use symmetric probabilities: Pᵢⱼ = (Pⱼ|ᵢ + Pᵢ|ⱼ) / 2n

FIX for Optimization:
└── Better gradient formulas
└── Various tricks (early exaggeration, momentum)
<a name="chapter-4"></a>

📖 CHAPTER 4: t-SNE - The Complete Deep Dive
4.1 What Does t-SNE Stand For?
text

t-SNE = t-distributed Stochastic Neighbor Embedding

t-distributed → Uses Student's t-distribution
Stochastic    → Uses probability-based approach
Neighbor      → Focuses on preserving neighborhood relationships
Embedding     → Maps high-D to low-D (embeds in lower space)
4.2 The Big Picture (30-Second Summary)
text

┌─────────────────────────────────────────────────────────────┐
│                    t-SNE in ONE Picture                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   HIGH-D SPACE (Original)     LOW-D SPACE (Result)          │
│   ─────────────────────       ─────────────────────         │
│                                                              │
│   Calculate probability       Calculate probability          │
│   that points are neighbors   that points are neighbors      │
│         (using Gaussian)          (using t-distribution)     │
│              │                         │                     │
│              │                         │                     │
│              └────────┬────────────────┘                     │
│                       │                                      │
│                       ▼                                      │
│            MINIMIZE THE DIFFERENCE!                          │
│            (Using KL Divergence)                             │
│                       │                                      │
│                       ▼                                      │
│              Adjust low-D positions                          │
│              until probabilities match                       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
4.3 Step-by-Step Algorithm Breakdown
STEP 1: Calculate Pairwise Distances in High-D Space
text

For every pair of points (i, j) in original data:

Calculate Euclidean distance: ||xᵢ - xⱼ||

Example with 4 points:
        
Points: A, B, C, D

Distance Matrix:
      A    B    C    D
A  [  0   2.5  5.0  8.0 ]
B  [ 2.5   0   3.0  6.5 ]
C  [ 5.0  3.0   0   4.0 ]
D  [ 8.0  6.5  4.0   0  ]
STEP 2: Convert Distances to Probabilities (High-D)
This is the CRUCIAL step. We convert distances to probabilities using a Gaussian (bell curve):

text

Formula for conditional probability:

              exp(-||xᵢ - xⱼ||² / 2σᵢ²)
P(j|i) = ────────────────────────────────
          Σₖ≠ᵢ exp(-||xᵢ - xₖ||² / 2σᵢ²)


What this means:
- Numerator: How "close" is point j to point i?
- Denominator: Sum of closeness to ALL other points (for normalization)
- σᵢ: Bandwidth parameter (different for each point!)
Visual Explanation:

text

Gaussian/Bell Curve centered at point i:

Probability
    ▲
    │     ╭─╮
    │    ╱   ╲
    │   ╱     ╲
    │  ╱       ╲
    │ ╱         ╲
    │╱           ╲
    └─────────────────► Distance from point i
        ↑   ↑   ↑
        │   │   │
       j₁  j₂  j₃
       
    j₁ is CLOSE → HIGH probability of being neighbor
    j₃ is FAR → LOW probability of being neighbor
STEP 3: Make Probabilities Symmetric
text

Problem: P(j|i) might ≠ P(i|j)

Solution: Average them!

              P(j|i) + P(i|j)
    Pᵢⱼ = ─────────────────────
                  2n

Where n = number of data points

This makes Pᵢⱼ = Pⱼᵢ (symmetric!)
STEP 4: Initialize Low-D Points Randomly
text

Start with random positions for each point in 2D (or 3D):

High-D: Point A = [0.5, 0.2, 0.8, 0.1, ...]  (many dimensions)
Low-D:  Point a = [0.34, 0.67]  (just 2 dimensions, random start)

We'll MOVE these positions iteratively until optimal.
STEP 5: Calculate Probabilities in Low-D Space
KEY DIFFERENCE: Use Student's t-distribution (not Gaussian)

text

Formula for low-dimensional similarity:

                    (1 + ||yᵢ - yⱼ||²)⁻¹
    Qᵢⱼ = ─────────────────────────────────────
           Σₖ≠ₗ (1 + ||yₖ - yₗ||²)⁻¹


Why t-distribution?
─────────────────
The t-distribution has "heavier tails" than Gaussian:

                Gaussian
                   ╭─╮
                  ╱   ╲
                 ╱     ╲
                ╱       ╲         ← Falls quickly (light tails)
            ───╱─────────╲───

            t-distribution
                   ╭─╮
                  ╱   ╲
                 ╱     ╲
              ──╱───────╲──       ← Falls slowly (heavy tails)
             ╱             ╲
           ╱                 ╲

Heavy tails = More "room" for moderately distant points
            = Solves the CROWDING PROBLEM!
STEP 6: Measure the Mismatch (KL Divergence)
text

We need to measure: How different are P (high-D) and Q (low-D)?

Answer: Kullback-Leibler (KL) Divergence

                          Pᵢⱼ
    KL(P || Q) = Σᵢ Σⱼ Pᵢⱼ log ────
                          Qᵢⱼ

Properties:
- KL = 0 means P and Q are IDENTICAL (perfect!)
- KL > 0 means there's some mismatch
- We want to MINIMIZE KL
Understanding KL Divergence Intuitively:

text

If Pᵢⱼ is HIGH (points are close in high-D):
    We REALLY want Qᵢⱼ to also be high
    Otherwise, Pᵢⱼ log(Pᵢⱼ/Qᵢⱼ) becomes large penalty!
    
If Pᵢⱼ is LOW (points are far in high-D):
    We don't care much about Qᵢⱼ
    Pᵢⱼ log(Pᵢⱼ/Qᵢⱼ) is small anyway

CONCLUSION: t-SNE focuses on preserving CLOSE points (local structure)
            It DOESN'T care much about preserving distant points!
STEP 7: Optimize Using Gradient Descent
text

Goal: Move low-D points (y) to minimize KL divergence

Gradient (force) on each point:

    ∂KL
    ──── = 4 Σⱼ (Pᵢⱼ - Qᵢⱼ)(yᵢ - yⱼ)(1 + ||yᵢ - yⱼ||²)⁻¹
    ∂yᵢ


Update rule:

    yᵢ(t+1) = yᵢ(t) - η × (∂KL/∂yᵢ) + momentum_term

Where:
- η = learning rate
- t = iteration number
- momentum helps escape local minima
Visual Analogy - Springs and Charges:

text

Imagine each point has:
1. SPRINGS connecting to its high-D neighbors (attractive force)
2. ELECTRIC CHARGE repelling from all other points (repulsive force)

              Neighbor
                 │
          Spring │ (pulls closer)
                 │
    ────●────────●────────●────
        ↑                  ↑
        │   Repulsion      │
        └────(pushes away)─┘

The system "relaxes" until forces balance = optimal embedding!
4.4 The Complete Algorithm Summary
text

┌────────────────────────────────────────────────────────────────┐
│                  t-SNE COMPLETE ALGORITHM                       │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  INPUT: X = {x₁, x₂, ..., xₙ} in high-dimensional space        │
│  OUTPUT: Y = {y₁, y₂, ..., yₙ} in 2D (or 3D)                   │
│                                                                 │
│  1. COMPUTE pairwise distances in high-D                       │
│     for all pairs (i,j): dᵢⱼ = ||xᵢ - xⱼ||                     │
│                                                                 │
│  2. COMPUTE σᵢ for each point using binary search              │
│     (based on perplexity parameter)                            │
│                                                                 │
│  3. COMPUTE P matrix (symmetric probabilities)                  │
│     Pᵢⱼ = (P(j|i) + P(i|j)) / 2n                               │
│                                                                 │
│  4. INITIALIZE Y randomly (small random values)                │
│     yᵢ ~ N(0, 10⁻⁴)                                            │
│                                                                 │
│  5. FOR iteration = 1 to T:                                    │
│     │                                                          │
│     ├── 5a. Compute Q matrix using t-distribution              │
│     │                                                          │
│     ├── 5b. Compute gradients ∂KL/∂yᵢ for all points          │
│     │                                                          │
│     ├── 5c. Update: Y = Y - η × gradient + momentum            │
│     │                                                          │
│     └── 5d. (Optional) Apply tricks like early exaggeration   │
│                                                                 │
│  6. RETURN final Y                                             │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
4.5 Understanding Perplexity
Perplexity is the MOST IMPORTANT parameter in t-SNE.

What is Perplexity?
text

Perplexity = 2^(entropy of probability distribution)

In simple terms:
Perplexity ≈ "effective number of neighbors" each point has

Low Perplexity (5):    Focus on VERY local structure
                       Only consider ~5 nearest neighbors
                       
High Perplexity (50):  Focus on broader local structure  
                       Consider ~50 neighbors

Typical range: 5 to 50
Default: Usually 30
How Perplexity Affects σᵢ
text

Perplexity is FIXED by user
σᵢ (Gaussian width) is CALCULATED to achieve that perplexity

Dense region:       σᵢ will be SMALL (narrow Gaussian)
                   ╭╮
                   ││
                 ──┴┴──

Sparse region:      σᵢ will be LARGE (wide Gaussian)
                  ╭──╮
                 ╱    ╲
               ─╱──────╲─

This makes t-SNE ADAPTIVE to local density!
Visual Effect of Different Perplexities
text

Data: Two clusters of points

Perplexity = 5 (too low):
┌─────────────────┐
│  ·· ·           │
│ · ·             │   Clusters might fragment
│        · ··     │   into smaller pieces
│         · ·     │
└─────────────────┘

Perplexity = 30 (good):
┌─────────────────┐
│  ···            │
│  ···            │   Clusters well separated
│         ···     │   and cohesive
│         ···     │
└─────────────────┘

Perplexity = 100 (too high):
┌─────────────────┐
│       ···       │
│      ·····      │   Clusters merge together
│       ···       │
│                 │
└─────────────────┘
4.6 Understanding the Gradients (Forces)
text

The gradient can be decomposed into ATTRACTIVE and REPULSIVE forces:

∂KL/∂yᵢ = 4 × [Σⱼ Pᵢⱼ Qᵢⱼ Z (yᵢ - yⱼ)  -  Σⱼ Qᵢⱼ² Z (yᵢ - yⱼ)]
               \_____________________/    \____________________/
                   ATTRACTIVE FORCE          REPULSIVE FORCE
                   (Spring-like)             (Electric-like)

Where Z = Σₖ≠ₗ (1 + ||yₖ - yₗ||²)⁻¹

ATTRACTIVE: If Pᵢⱼ is high, pull points i and j together
REPULSIVE:  All points push each other away (proportional to Qᵢⱼ²)
4.7 Optimization Tricks in t-SNE
Trick 1: Early Exaggeration
text

For first ~250 iterations:
    Multiply all Pᵢⱼ by 4 (or 12)
    
Why? 
- Makes attractive forces MUCH stronger initially
- Clusters form tightly and separate from each other
- Prevents getting stuck in bad configurations

Timeline:
Iteration:    1 ──────── 250 ──────── 1000
Exaggeration: ████ 4× ████│──── 1× (normal) ────
Trick 2: Momentum
text

Instead of: Y(t+1) = Y(t) - η × gradient

Use:        Y(t+1) = Y(t) - η × gradient + α × (Y(t) - Y(t-1))
                                           \_________________/
                                               momentum term

α = 0.5 (early)
α = 0.8 (later)

Why? Helps "roll past" small local minima, like a ball rolling down a hill.
Trick 3: Learning Rate Adaptation
text

Too HIGH learning rate:
    Points oscillate wildly, never converge
    
Too LOW learning rate:
    Takes forever to converge
    
ADAPTIVE learning rate:
    Start higher, reduce over time
    Or use algorithms like Adam/AdaGrad
4.8 Computational Complexity
text

Naive t-SNE:           O(n²) per iteration
                       - Must compute ALL pairwise similarities
                       - n=10,000 points → 100 million calculations per iteration!
                       
Barnes-Hut t-SNE:      O(n log n) per iteration
                       - Uses tree structures to approximate
                       - Can handle ~100,000 points
                       
FIt-SNE:               O(n) per iteration
                       - Uses interpolation-based approximation
                       - Can handle millions of points
<a name="chapter-5"></a>

📖 CHAPTER 5: UMAP - The Modern Revolution
5.1 What Does UMAP Stand For?
text

UMAP = Uniform Manifold Approximation and Projection

Uniform   → Based on assumptions about uniform data distribution
Manifold  → Assumes data lies on a curved surface (manifold)
Approximation → Approximates this manifold structure
Projection → Projects to lower dimensions
5.2 Why Was UMAP Created?
text

t-SNE Limitations:
├── SLOW for large datasets
├── Doesn't preserve GLOBAL structure well
├── Can't embed NEW points easily
├── Hard to use for general ML (only visualization)
└── No solid theoretical foundation

UMAP Goals:
├── FAST (10-100× faster than t-SNE)
├── Preserve both LOCAL and GLOBAL structure
├── Support adding new points
├── Usable as preprocessing for ML
└── Strong mathematical theory (algebraic topology)
5.3 The Theory Behind UMAP (Simplified)
Core Mathematical Concepts
text

1. MANIFOLD ASSUMPTION:
   "High-dimensional data actually lies on a lower-dimensional
    curved surface (manifold) embedded in the high-D space"
   
   Example: Earth's surface is 2D (lat, long) embedded in 3D space
   
2. RIEMANNIAN GEOMETRY:
   "We can measure distances along the curved surface"
   
3. FUZZY TOPOLOGY:
   "We create 'fuzzy' sets of neighbors rather than hard boundaries"
   
4. CROSS-ENTROPY OPTIMIZATION:
   "We optimize by minimizing differences in fuzzy set structures"
The Fuzzy Set Idea
text

Traditional Neighbor:
    "Point B is a neighbor of A" → YES or NO (binary)
    
Fuzzy Neighbor:
    "Point B is a neighbor of A with strength 0.7" → Continuous [0,1]
    
This allows smooth transitions and better optimization!
5.4 UMAP Algorithm Step-by-Step
STEP 1: Construct High-D Fuzzy Graph
text

For each point i:
1. Find k nearest neighbors (typically k=15)
2. Compute distances to these neighbors
3. Set ρᵢ = distance to NEAREST neighbor

Why ρᵢ?
- Ensures each point has at least one "connected" neighbor
- Handles varying densities automatically

4. Compute σᵢ using binary search such that:
   Σⱼ exp(-(dᵢⱼ - ρᵢ)/σᵢ) = log₂(k)

5. Compute fuzzy membership:
   
   μᵢⱼ = exp(-(dᵢⱼ - ρᵢ)/σᵢ)  if dᵢⱼ > ρᵢ
       = 1                      if dᵢⱼ ≤ ρᵢ
Visual Representation:

text

Point i and its neighbors:

                     j₃ (far, μ=0.1)
                    ╱
        j₂ ───────●i ─────── j₁ (nearest, μ=1.0)
        (medium,   
         μ=0.5)

The fuzzy graph has weighted edges based on μ values.
STEP 2: Symmetrize the Graph
text

Make the fuzzy membership symmetric:

μᵢⱼ(symmetric) = μᵢⱼ + μⱼᵢ - μᵢⱼ × μⱼᵢ

This is fuzzy set union (probabilistic OR)!

Intuition: "If either i thinks j is a neighbor OR j thinks i is a 
            neighbor, then they ARE neighbors"
STEP 3: Initialize Low-D Embedding
text

Options for initialization:
├── Random (like t-SNE)
├── Spectral Embedding (graph Laplacian eigenvectors) ← Default & Better!
└── PCA

Spectral initialization gives MUCH better starting point!
It roughly captures the global structure from the start.
STEP 4: Define Low-D Similarity
text

UMAP uses a different similarity function than t-SNE:

                         1
νᵢⱼ = ─────────────────────────────────
       1 + a × ||yᵢ - yⱼ||^(2b)

Default parameters: a ≈ 1.93, b ≈ 0.79

This is similar to t-distribution but more flexible!
STEP 5: Optimize Using Cross-Entropy
text

UMAP minimizes CROSS-ENTROPY (not KL divergence):

CE = Σᵢⱼ [μᵢⱼ log(μᵢⱼ/νᵢⱼ) + (1-μᵢⱼ) log((1-μᵢⱼ)/(1-νᵢⱼ))]
     \_____________________/   \________________________________/
           Attractive                     Repulsive
      (similar to t-SNE)              (NEW in UMAP!)

Key difference from t-SNE:
- t-SNE only has attractive term for connected pairs
- UMAP has BOTH attractive AND repulsive terms explicitly
- This leads to better GLOBAL structure preservation!
STEP 6: Stochastic Gradient Descent
text

UMAP uses STOCHASTIC (sampling-based) optimization:

For each iteration:
1. Sample a batch of edges (connected pairs)
2. For each edge (i,j):
   - Apply attractive force (pull together)
3. Sample negative examples (non-edges)
4. For each negative (i,k):
   - Apply repulsive force (push apart)
5. Update positions

This is MUCH faster than computing ALL pairs!
5.5 Complete UMAP Algorithm
text

┌────────────────────────────────────────────────────────────────┐
│                   UMAP COMPLETE ALGORITHM                       │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  INPUT: X = {x₁, ..., xₙ}, k (neighbors), d (target dims)     │
│  OUTPUT: Y = {y₁, ..., yₙ} in d dimensions                     │
│                                                                 │
│  1. CONSTRUCT k-NN GRAPH                                       │
│     for each point i:                                          │
│       - Find k nearest neighbors                               │
│       - Compute distances to neighbors                         │
│                                                                 │
│  2. COMPUTE FUZZY SIMPLICIAL SET                               │
│     for each point i:                                          │
│       - Set ρᵢ = distance to nearest neighbor                  │
│       - Binary search for σᵢ to match target entropy          │
│       - Compute membership strengths μᵢⱼ                       │
│                                                                 │
│  3. SYMMETRIZE                                                 │
│     μᵢⱼ = μᵢⱼ + μⱼᵢ - μᵢⱼ × μⱼᵢ                                │
│                                                                 │
│  4. INITIALIZE embedding Y                                     │
│     Using spectral embedding of fuzzy graph                   │
│                                                                 │
│  5. OPTIMIZE using SGD for n_epochs:                           │
│     For each edge (i,j) with weight μᵢⱼ:                       │
│       - With probability μᵢⱼ, apply attractive force          │
│       - Sample negative j', apply repulsive force              │
│       - Update yᵢ, yⱼ, yⱼ'                                     │
│                                                                 │
│  6. RETURN Y                                                   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
5.6 Key UMAP Parameters
n_neighbors (most important!)
text

n_neighbors = number of nearest neighbors considered

┌────────────────────────────────────────────────────────────────┐
│   Low n_neighbors (5-10):                                       │
│   ├── Focus on VERY local structure                            │
│   ├── Small, tight clusters                                    │
│   ├── May fragment natural clusters                            │
│   └── Captures fine details but loses big picture              │
│                                                                 │
│   High n_neighbors (50-200):                                   │
│   ├── Focus on broader structure                               │
│   ├── Larger, more connected regions                           │
│   ├── May merge distinct clusters                              │
│   └── Captures big picture but loses details                   │
│                                                                 │
│   Recommended: 15 (default) - good balance                     │
└────────────────────────────────────────────────────────────────┘
min_dist
text

min_dist = minimum distance between points in embedding

┌────────────────────────────────────────────────────────────────┐
│   Low min_dist (0.0-0.1):                                      │
│   ├── Points can be VERY close together                        │
│   ├── Tight, dense clusters                                    │
│   ├── Good for seeing cluster structure                        │
│   └── May look "clumpy"                                        │
│                                                                 │
│   High min_dist (0.5-1.0):                                     │
│   ├── Points must stay further apart                           │
│   ├── More spread out visualization                            │
│   ├── Better for seeing individual points                      │
│   └── Clusters may look merged                                 │
│                                                                 │
│   Recommended: 0.1 (default) for most cases                    │
└────────────────────────────────────────────────────────────────┘
metric
text

metric = how to measure distance

Options:
├── 'euclidean' (default)  - Standard straight-line distance
├── 'manhattan'            - Sum of absolute differences  
├── 'cosine'              - Angle between vectors (good for text/NLP)
├── 'correlation'         - Pearson correlation
├── 'hamming'            - For binary data
└── Custom functions!     - You can define your own

Choose based on your data type!
n_components
text

n_components = target number of dimensions

Common choices:
├── 2 - For visualization (most common)
├── 3 - For 3D visualization
├── 10-50 - As preprocessing for ML algorithms
└── Higher - For preserving more structure

Unlike t-SNE, UMAP works well with higher dimensions!
5.7 UMAP's Special Features
Feature 1: Transform (Adding New Points)
text

t-SNE: Cannot add new points after training
       Must re-run entire algorithm!
       
UMAP:  CAN add new points!

# Example in code:
mapper = umap.UMAP().fit(X_train)
Y_train = mapper.transform(X_train)  # Original embedding
Y_new = mapper.transform(X_new)      # NEW points embedded!

This is HUGE for production systems!
Feature 2: Inverse Transform
text

UMAP can go BACKWARDS (approximately):

High-D → Low-D: Forward transform (normal)
Low-D → High-D: Inverse transform (generate new data!)

# Example:
mapper = umap.UMAP().fit(X)
Y = mapper.transform(X)

# Create a new point in 2D
new_point_2d = [[0.5, 0.3]]

# Map it back to high-D!
new_point_highD = mapper.inverse_transform(new_point_2d)

Use case: Generate synthetic data, explore latent space
Feature 3: Supervised UMAP
text

UMAP can use LABELS to guide the embedding!

# Unsupervised (normal):
mapper = umap.UMAP().fit(X)

# Supervised (uses labels):
mapper = umap.UMAP().fit(X, y=labels)

Effect:
├── Points with SAME label pushed closer
├── Points with DIFFERENT labels pushed apart
├── Much clearer cluster separation
└── Useful when you know some labels!

# Semi-supervised (some labels known):
labels_partial = [0, 1, -1, -1, 0, 1, ...]  # -1 = unknown
mapper = umap.UMAP().fit(X, y=labels_partial)
Feature 4: Metric Learning
text

UMAP can learn a METRIC for comparing points:

# Learn metric from labeled data
mapper = umap.UMAP(target_metric='categorical').fit(X, y)

# Now compare ANY two points using learned metric
distance = mapper.metric(point1, point2)

Useful for: similarity search, retrieval systems
5.8 Computational Complexity
text

┌────────────────────────────────────────────────────────────────┐
│                   UMAP COMPLEXITY                               │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Step                          | Complexity                    │
│  ─────────────────────────────────────────────────────────────│
│  k-NN graph construction       | O(n^1.5) with NN-Descent     │
│                                | O(n log n) with Annoy/HNSW   │
│  ─────────────────────────────────────────────────────────────│
│  Fuzzy set computation         | O(n × k)                     │
│  ─────────────────────────────────────────────────────────────│
│  SGD optimization              | O(n × n_epochs)              │
│  ─────────────────────────────────────────────────────────────│
│  TOTAL                         | O(n^1.5) approximately       │
│                                                                 │
│  Compare to:                                                    │
│  ├── t-SNE naive: O(n²)                                        │
│  ├── Barnes-Hut t-SNE: O(n log n)                              │
│  └── UMAP: O(n^1.5) but with MUCH smaller constants!           │
│                                                                 │
│  In practice: UMAP is 10-100× faster than t-SNE                │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
<a name="chapter-6"></a>

📖 CHAPTER 6: t-SNE vs UMAP - The Ultimate Comparison
6.1 Side-by-Side Comparison Table
text

┌──────────────────────┬─────────────────────┬─────────────────────┐
│     ASPECT           │       t-SNE         │        UMAP         │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Year Published       │ 2008                │ 2018                │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Speed                │ Slow                │ Fast (10-100× ↑)    │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Scalability          │ ~10,000 points      │ Millions of points  │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Local Structure      │ ✓✓✓ Excellent       │ ✓✓✓ Excellent       │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Global Structure     │ ✗ Poor              │ ✓✓ Good             │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Add New Points       │ ✗ No                │ ✓ Yes (transform)   │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Inverse Transform    │ ✗ No                │ ✓ Yes               │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Supervised Mode      │ ✗ No                │ ✓ Yes               │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Target Dimensions    │ 2-3 only            │ Any                 │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Deterministic?       │ No (random init)    │ More stable         │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Theory Foundation    │ Information theory  │ Algebraic topology  │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Hyperparameters      │ Perplexity, LR      │ n_neighbors,min_dist│
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Use for ML Pipeline  │ ✗ Not recommended   │ ✓ Yes               │
├──────────────────────┼─────────────────────┼─────────────────────┤
│ Cluster Distances    │ Meaningless         │ More meaningful     │
└──────────────────────┴─────────────────────┴─────────────────────┘
6.2 Visual Comparison
text

Same dataset visualized with both algorithms:

t-SNE:                              UMAP:
┌─────────────────────┐             ┌─────────────────────┐
│    ●●●              │             │  ●●●                │
│   ●●●●              │             │   ●●●               │
│     ●●              │             │                     │
│                     │             │           ▲▲        │
│         ■■          │             │            ▲▲▲      │
│        ■■■■         │             │             ▲       │
│         ■■          │             │                     │
│                     │             │      ■■■            │
│             ▲▲▲     │             │       ■■■           │
│            ▲▲▲▲     │             │        ■            │
│              ▲      │             │                     │
└─────────────────────┘             └─────────────────────┘

Note: 
- Both show 3 clusters clearly (local structure preserved)
- UMAP shows more relative positioning between clusters
  (global structure better preserved)
- t-SNE clusters may have arbitrary relative positions
6.3 When to Use Which?
text

USE t-SNE WHEN:
├── You have <10,000 points
├── You ONLY need visualization
├── You want the most "dramatic" cluster separation
├── Local structure is ALL that matters
└── You're following historical papers/tutorials

USE UMAP WHEN:
├── You have >10,000 points (or even millions)
├── You need to add new points later
├── You want to use embedding for downstream ML
├── Global structure matters
├── You want supervised/semi-supervised embedding
├── Speed is important
└── You want reproducible results

GENERAL RECOMMENDATION: Use UMAP by default in 2024+
t-SNE is mostly for legacy/comparison purposes now
6.4 Common Misconceptions
Misconception 1: "t-SNE creates fake clusters"
text

WRONG: t-SNE doesn't CREATE clusters that don't exist

CORRECT: t-SNE can SPLIT continuous data into apparent clusters
         if perplexity is too low, or if you misinterpret the results

Rule: Never claim cluster existence based solely on t-SNE/UMAP
      Always verify with other methods!
Misconception 2: "Distances between clusters are meaningful"
text

t-SNE: Distances between clusters are ARBITRARY
       Only WITHIN-cluster distances have some meaning
       
UMAP: Distances are MORE meaningful but still not precise
      Relative positions somewhat preserved

Rule: Don't measure cluster distances literally from plots!
Misconception 3: "UMAP is just faster t-SNE"
text

WRONG: They have fundamentally different algorithms and theories

t-SNE: Based on probability distributions and KL divergence
UMAP: Based on topological structures and cross-entropy

They often give DIFFERENT results, even if superficially similar!
Misconception 4: "One run is enough"
text

WRONG: Both algorithms have randomness

CORRECT: Run multiple times with different seeds!
         If structure is consistent → it's real
         If structure changes → might be artifact

# Best practice:
results = []
for seed in range(10):
    result = UMAP(random_state=seed).fit_transform(X)
    results.append(result)
# Compare all 10 results
<a name="chapter-7"></a>

📖 CHAPTER 7: Practical Implementation Guide
7.1 Installation
Bash

# Install via pip
pip install scikit-learn     # For t-SNE
pip install umap-learn       # For UMAP

# Or via conda
conda install -c conda-forge scikit-learn umap-learn

# Optional but recommended
pip install matplotlib       # For visualization
pip install seaborn         # For better plots
pip install pandas          # For data handling
pip install numba           # Speed up UMAP
7.2 Basic t-SNE Implementation
Python

# =========================================
# BASIC t-SNE EXAMPLE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from sklearn.manifold import TSNE
from sklearn.datasets import load_digits

# -----------------------------------------
# STEP 1: Load sample data
# -----------------------------------------
digits = load_digits()
X = digits.data      # Shape: (1797, 64) - 64 dimensions
y = digits.target    # Labels: 0-9

print(f"Original shape: {X.shape}")
# Output: Original shape: (1797, 64)

# -----------------------------------------
# STEP 2: Apply t-SNE
# -----------------------------------------
tsne = TSNE(
    n_components=2,      # Target: 2D
    perplexity=30,       # Number of neighbors to consider
    learning_rate=200,   # Step size for optimization
    n_iter=1000,         # Number of iterations
    random_state=42      # For reproducibility
)

X_tsne = tsne.fit_transform(X)

print(f"Reduced shape: {X_tsne.shape}")
# Output: Reduced shape: (1797, 2)

# -----------------------------------------
# STEP 3: Visualize
# -----------------------------------------
plt.figure(figsize=(10, 8))
scatter = plt.scatter(X_tsne[:, 0], X_tsne[:, 1], 
                      c=y, cmap='tab10', alpha=0.7)
plt.colorbar(scatter, label='Digit')
plt.title('t-SNE visualization of Digits dataset')
plt.xlabel('t-SNE 1')
plt.ylabel('t-SNE 2')
plt.show()
7.3 Basic UMAP Implementation
Python

# =========================================
# BASIC UMAP EXAMPLE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
import umap
from sklearn.datasets import load_digits

# -----------------------------------------
# STEP 1: Load sample data
# -----------------------------------------
digits = load_digits()
X = digits.data
y = digits.target

# -----------------------------------------
# STEP 2: Apply UMAP
# -----------------------------------------
reducer = umap.UMAP(
    n_components=2,       # Target: 2D
    n_neighbors=15,       # Number of neighbors
    min_dist=0.1,         # Minimum distance in embedding
    metric='euclidean',   # Distance metric
    random_state=42       # For reproducibility
)

X_umap = reducer.fit_transform(X)

# -----------------------------------------
# STEP 3: Visualize
# -----------------------------------------
plt.figure(figsize=(10, 8))
scatter = plt.scatter(X_umap[:, 0], X_umap[:, 1], 
                      c=y, cmap='tab10', alpha=0.7)
plt.colorbar(scatter, label='Digit')
plt.title('UMAP visualization of Digits dataset')
plt.xlabel('UMAP 1')
plt.ylabel('UMAP 2')
plt.show()
7.4 Comparing t-SNE and UMAP Side by Side
Python

# =========================================
# SIDE-BY-SIDE COMPARISON
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from sklearn.manifold import TSNE
import umap
from sklearn.datasets import load_digits
import time

# Load data
digits = load_digits()
X, y = digits.data, digits.target

# -----------------------------------------
# Run t-SNE with timing
# -----------------------------------------
start = time.time()
X_tsne = TSNE(n_components=2, perplexity=30, 
              random_state=42).fit_transform(X)
tsne_time = time.time() - start
print(f"t-SNE time: {tsne_time:.2f} seconds")

# -----------------------------------------
# Run UMAP with timing
# -----------------------------------------
start = time.time()
X_umap = umap.UMAP(n_components=2, n_neighbors=15,
                   random_state=42).fit_transform(X)
umap_time = time.time() - start
print(f"UMAP time: {umap_time:.2f} seconds")

# -----------------------------------------
# Plot comparison
# -----------------------------------------
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# t-SNE plot
axes[0].scatter(X_tsne[:, 0], X_tsne[:, 1], c=y, cmap='tab10', alpha=0.7)
axes[0].set_title(f't-SNE (Time: {tsne_time:.2f}s)')
axes[0].set_xlabel('t-SNE 1')
axes[0].set_ylabel('t-SNE 2')

# UMAP plot
axes[1].scatter(X_umap[:, 0], X_umap[:, 1], c=y, cmap='tab10', alpha=0.7)
axes[1].set_title(f'UMAP (Time: {umap_time:.2f}s)')
axes[1].set_xlabel('UMAP 1')
axes[1].set_ylabel('UMAP 2')

plt.tight_layout()
plt.show()
7.5 Advanced: Hyperparameter Exploration
Python

# =========================================
# EXPLORING DIFFERENT PARAMETERS
# =========================================

import numpy as np
import matplotlib.pyplot as plt
import umap
from sklearn.datasets import load_digits

digits = load_digits()
X, y = digits.data, digits.target

# -----------------------------------------
# Explore n_neighbors
# -----------------------------------------
n_neighbors_list = [5, 15, 50, 200]

fig, axes = plt.subplots(1, 4, figsize=(20, 4))

for idx, n_neighbors in enumerate(n_neighbors_list):
    reducer = umap.UMAP(n_neighbors=n_neighbors, random_state=42)
    X_embedded = reducer.fit_transform(X)
    
    axes[idx].scatter(X_embedded[:, 0], X_embedded[:, 1], 
                      c=y, cmap='tab10', s=5, alpha=0.7)
    axes[idx].set_title(f'n_neighbors = {n_neighbors}')
    axes[idx].axis('off')

plt.suptitle('Effect of n_neighbors on UMAP', fontsize=14)
plt.tight_layout()
plt.show()

# -----------------------------------------
# Explore min_dist
# -----------------------------------------
min_dist_list = [0.0, 0.1, 0.5, 0.99]

fig, axes = plt.subplots(1, 4, figsize=(20, 4))

for idx, min_dist in enumerate(min_dist_list):
    reducer = umap.UMAP(min_dist=min_dist, random_state=42)
    X_embedded = reducer.fit_transform(X)
    
    axes[idx].scatter(X_embedded[:, 0], X_embedded[:, 1], 
                      c=y, cmap='tab10', s=5, alpha=0.7)
    axes[idx].set_title(f'min_dist = {min_dist}')
    axes[idx].axis('off')

plt.suptitle('Effect of min_dist on UMAP', fontsize=14)
plt.tight_layout()
plt.show()
7.6 Advanced: Using UMAP for ML Pipeline
Python

# =========================================
# UMAP AS PREPROCESSING FOR ML
# =========================================

import numpy as np
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
import umap

# Load data
digits = load_digits()
X, y = digits.data, digits.target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# -----------------------------------------
# Method 1: Train on original 64D data
# -----------------------------------------
clf_original = RandomForestClassifier(random_state=42)
clf_original.fit(X_train, y_train)
acc_original = accuracy_score(y_test, clf_original.predict(X_test))
print(f"Accuracy on original 64D: {acc_original:.4f}")

# -----------------------------------------
# Method 2: Train on UMAP-reduced data
# -----------------------------------------
# IMPORTANT: fit on train, transform both train and test!
reducer = umap.UMAP(n_components=10, random_state=42)
X_train_umap = reducer.fit_transform(X_train)  # fit_transform on train
X_test_umap = reducer.transform(X_test)         # only transform on test

clf_umap = RandomForestClassifier(random_state=42)
clf_umap.fit(X_train_umap, y_train)
acc_umap = accuracy_score(y_test, clf_umap.predict(X_test_umap))
print(f"Accuracy on UMAP 10D: {acc_umap:.4f}")

# -----------------------------------------
# Method 3: Supervised UMAP
# -----------------------------------------
reducer_supervised = umap.UMAP(n_components=10, random_state=42)
X_train_supervised = reducer_supervised.fit_transform(X_train, y=y_train)
X_test_supervised = reducer_supervised.transform(X_test)

clf_supervised = RandomForestClassifier(random_state=42)
clf_supervised.fit(X_train_supervised, y_train)
acc_supervised = accuracy_score(y_test, clf_supervised.predict(X_test_supervised))
print(f"Accuracy on Supervised UMAP 10D: {acc_supervised:.4f}")
7.7 Handling Large Datasets
Python

# =========================================
# HANDLING LARGE DATASETS
# =========================================

import numpy as np
import umap
from sklearn.manifold import TSNE

# Create large dataset (simulated)
np.random.seed(42)
n_samples = 100000
n_features = 100
X_large = np.random.randn(n_samples, n_features)

print(f"Dataset shape: {X_large.shape}")

# -----------------------------------------
# UMAP handles large data well
# -----------------------------------------
import time

start = time.time()
reducer = umap.UMAP(
    n_components=2,
    n_neighbors=15,
    min_dist=0.1,
    low_memory=True,      # Enable for very large datasets
    verbose=True          # Show progress
)
X_embedded = reducer.fit_transform(X_large)
print(f"UMAP time for 100K points: {time.time() - start:.2f} seconds")

# -----------------------------------------
# For t-SNE: Use approximation methods
# -----------------------------------------
# Option 1: Subsample
sample_idx = np.random.choice(n_samples, 5000, replace=False)
X_sample = X_large[sample_idx]

tsne = TSNE(n_components=2, random_state=42)
X_tsne_sample = tsne.fit_transform(X_sample)

# Option 2: Use openTSNE or FIt-SNE for large datasets
# pip install openTSNE
from openTSNE import TSNE as FastTSNE

tsne_fast = FastTSNE(
    n_components=2,
    perplexity=30,
    n_jobs=-1,            # Use all CPUs
    random_state=42
)
# X_embedded_fast = tsne_fast.fit(X_large)  # Much faster!
7.8 Saving and Loading Models
Python

# =========================================
# SAVING AND LOADING UMAP MODELS
# =========================================

import numpy as np
import umap
import pickle

# Train UMAP
X = np.random.randn(1000, 50)
reducer = umap.UMAP(n_components=2)
reducer.fit(X)

# -----------------------------------------
# Method 1: Using pickle
# -----------------------------------------
# Save
with open('umap_model.pkl', 'wb') as f:
    pickle.dump(reducer, f)

# Load
with open('umap_model.pkl', 'rb') as f:
    reducer_loaded = pickle.load(f)

# Use loaded model
X_new = np.random.randn(100, 50)
X_embedded = reducer_loaded.transform(X_new)

# -----------------------------------------
# Method 2: Using joblib (faster for large arrays)
# -----------------------------------------
import joblib

# Save
joblib.dump(reducer, 'umap_model.joblib')

# Load
reducer_loaded = joblib.load('umap_model.joblib')
<a name="chapter-8"></a>

📖 CHAPTER 8: Hyperparameter Mastery
8.1 t-SNE Hyperparameters Deep Dive
Perplexity
text

┌────────────────────────────────────────────────────────────────┐
│                      PERPLEXITY                                 │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Effective number of local neighbors                │
│                                                                 │
│  Formula: Perplexity = 2^H(P)                                  │
│           where H(P) = -Σ P(j|i) log₂ P(j|i)                   │
│                                                                 │
│  Range: Typically 5 to 50                                      │
│  Default: 30                                                    │
│                                                                 │
│  RULES OF THUMB:                                               │
│  ├── Perplexity should be < n_samples / 3                      │
│  ├── Larger datasets can use larger perplexity                 │
│  ├── If clusters fragment → increase perplexity                │
│  ├── If clusters merge → decrease perplexity                   │
│  └── Always try multiple values!                               │
│                                                                 │
│  WHAT HAPPENS:                                                  │
│                                                                 │
│  Low Perplexity (5):                                           │
│  • Very local focus                                            │
│  • Tight, small clusters                                       │
│  • May split natural clusters                                  │
│  • Good for finding sub-structure                              │
│                                                                 │
│  High Perplexity (50):                                         │
│  • Broader local focus                                         │
│  • Larger, more connected clusters                             │
│  • May merge distinct clusters                                 │
│  • Good for seeing overall structure                           │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
Learning Rate
text

┌────────────────────────────────────────────────────────────────┐
│                     LEARNING RATE                               │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Step size during gradient descent                  │
│                                                                 │
│  Range: 10 to 1000                                             │
│  Default: 200 (sklearn), "auto" in newer versions              │
│                                                                 │
│  RECOMMENDED FORMULA:                                          │
│  learning_rate = max(n_samples / early_exaggeration / 4, 50)   │
│                ≈ n_samples / 12                                 │
│                                                                 │
│  SYMPTOMS:                                                      │
│                                                                 │
│  Too Low (<50):                                                │
│  • Embedding looks like a ball/sphere                          │
│  • All points clustered in center                              │
│  • Optimization didn't progress                                │
│                                                                 │
│  Too High (>1000):                                             │
│  • Embedding looks random/chaotic                              │
│  • Points scattered everywhere                                 │
│  • Optimization unstable                                       │
│                                                                 │
│  Just Right:                                                   │
│  • Clear cluster structure                                     │
│  • Well-separated groups                                       │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
Number of Iterations (n_iter)
text

┌────────────────────────────────────────────────────────────────┐
│                    NUMBER OF ITERATIONS                         │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: How many optimization steps to run                 │
│                                                                 │
│  Range: 250 to 5000+                                           │
│  Default: 1000                                                  │
│                                                                 │
│  PHASES:                                                        │
│  Iterations 1-250: Early exaggeration phase                    │
│                    (P values multiplied by 4 or 12)            │
│  Iterations 251+:  Normal optimization                         │
│                                                                 │
│  HOW TO KNOW IF ENOUGH:                                        │
│  • Check if KL divergence has plateaued                        │
│  • Run longer if loss still decreasing                         │
│  • 1000 is usually sufficient for most datasets                │
│                                                                 │
│  MONITORING:                                                    │
│                                                                 │
│  tsne = TSNE(n_iter=1000, verbose=1)  # Shows progress         │
│                                                                 │
│  Output: [t-SNE] Iteration 50: error = 89.5233                 │
│          [t-SNE] Iteration 100: error = 76.8891                │
│          ...                                                   │
│          [t-SNE] Iteration 1000: error = 0.8234                │
│                                                                 │
│  If error still dropping at 1000 → increase n_iter             │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
Early Exaggeration
text

┌────────────────────────────────────────────────────────────────┐
│                   EARLY EXAGGERATION                            │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Multiplier for P values in early iterations       │
│                                                                 │
│  Default: 12 (sklearn)                                         │
│  Range: 4 to 20                                                │
│                                                                 │
│  PURPOSE:                                                       │
│  • Makes attractive forces STRONGER initially                  │
│  • Helps clusters form and separate quickly                    │
│  • Prevents getting stuck in bad configurations                │
│                                                                 │
│  EFFECT:                                                        │
│                                                                 │
│  Without exaggeration:                 With exaggeration:      │
│  ┌────────────────────┐                ┌────────────────────┐   │
│  │    Points slowly   │                │ Clusters form      │   │
│  │    drift around    │                │ quickly then       │   │
│  │    may get stuck   │                │ refine positions   │   │
│  └────────────────────┘                └────────────────────┘   │
│                                                                 │
│  Higher values (15-20):                                        │
│  • More dramatic initial cluster formation                     │
│  • Better for well-separated data                              │
│                                                                 │
│  Lower values (4-8):                                           │
│  • More gradual clustering                                     │
│  • Better for continuous/overlapping data                      │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
8.2 UMAP Hyperparameters Deep Dive
n_neighbors
text

┌────────────────────────────────────────────────────────────────┐
│                      n_neighbors                                │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Number of neighboring points used in graph        │
│                                                                 │
│  Range: 2 to 200                                               │
│  Default: 15                                                    │
│                                                                 │
│  TRADE-OFF:                                                     │
│                                                                 │
│  Low n_neighbors (2-10)    ←────────→    High n_neighbors      │
│  │                                               (50-200) │    │
│  │                                                         │    │
│  ├── Very local focus                ├── Global focus          │
│  ├── Fine details preserved          ├── Big picture           │
│  ├── May fragment clusters           ├── May merge clusters    │
│  ├── Noisier embedding               ├── Smoother embedding    │
│  └── Risk of disconnection           └── May lose details      │
│                                                                 │
│  RECOMMENDATIONS BY DATA SIZE:                                  │
│  ├── <1,000 points:    n_neighbors = 5-15                      │
│  ├── 1,000-10,000:     n_neighbors = 15-30                     │
│  ├── 10,000-100,000:   n_neighbors = 30-50                     │
│  └── >100,000:         n_neighbors = 50-100                    │
│                                                                 │
│  RELATIONSHIP TO t-SNE:                                        │
│  • n_neighbors ≈ perplexity (similar effect)                   │
│  • But not exactly equivalent mathematically                   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
min_dist
text

┌────────────────────────────────────────────────────────────────┐
│                        min_dist                                 │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Minimum distance between embedded points          │
│                                                                 │
│  Range: 0.0 to 0.99                                            │
│  Default: 0.1                                                   │
│                                                                 │
│  VISUAL EFFECT:                                                │
│                                                                 │
│  min_dist = 0.0               min_dist = 0.5                   │
│  ┌──────────────┐             ┌──────────────┐                 │
│  │    ▓▓▓       │             │   · · ·      │                 │
│  │   ▓▓▓▓▓      │             │  · · · ·     │                 │
│  │    ▓▓▓       │             │   · · ·      │                 │
│  │        ▓▓▓   │             │        · · · │                 │
│  │       ▓▓▓▓▓  │             │       · · ·· │                 │
│  └──────────────┘             └──────────────┘                 │
│  Very clumpy                  More spread out                   │
│  Clusters dense               Points distinguishable            │
│                                                                 │
│  USE CASES:                                                     │
│                                                                 │
│  min_dist = 0.0                                                │
│  • Best for seeing cluster structure                           │
│  • Good for clustering downstream                              │
│  • Points stack on top of each other                           │
│                                                                 │
│  min_dist = 0.1 (default)                                      │
│  • Good balance                                                │
│  • Clusters visible, points distinguishable                    │
│                                                                 │
│  min_dist = 0.5-0.99                                           │
│  • Points forced apart                                         │
│  • Good for seeing individual points                           │
│  • Cluster boundaries less clear                               │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
metric
text

┌────────────────────────────────────────────────────────────────┐
│                         metric                                  │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Distance function used to compare points          │
│                                                                 │
│  COMMON OPTIONS:                                               │
│                                                                 │
│  'euclidean' (default)                                         │
│  • Standard "straight line" distance                           │
│  • Good for: numerical data with meaningful scales             │
│  • Formula: √(Σ(xᵢ - yᵢ)²)                                     │
│                                                                 │
│  'manhattan' (L1)                                              │
│  • Sum of absolute differences                                 │
│  • Good for: grid-based data, sparse features                  │
│  • Formula: Σ|xᵢ - yᵢ|                                         │
│                                                                 │
│  'cosine'                                                      │
│  • Angle between vectors (ignores magnitude)                   │
│  • Good for: text/NLP, normalized data                         │
│  • Formula: 1 - (x·y)/(||x|| ||y||)                            │
│                                                                 │
│  'correlation'                                                 │
│  • Pearson correlation distance                                │
│  • Good for: gene expression, patterns                         │
│  • Formula: 1 - correlation(x, y)                              │
│                                                                 │
│  'hamming'                                                     │
│  • Fraction of differing elements                              │
│  • Good for: binary data, categorical features                 │
│                                                                 │
│  'jaccard'                                                     │
│  • For set comparison                                          │
│  • Good for: binary/presence-absence data                      │
│                                                                 │
│  CUSTOM METRICS:                                               │
│                                                                 │
│  from numba import njit                                        │
│                                                                 │
│  @njit                                                         │
│  def custom_distance(x, y):                                    │
│      # Your custom distance logic                              │
│      return distance_value                                     │
│                                                                 │
│  umap.UMAP(metric=custom_distance)                             │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
n_epochs
text

┌────────────────────────────────────────────────────────────────┐
│                        n_epochs                                 │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Definition: Number of training epochs                          │
│                                                                 │
│  Default: None (auto-calculated based on data size)            │
│  • Small datasets: 500 epochs                                  │
│  • Large datasets: 200 epochs                                  │
│                                                                 │
│  WHEN TO MODIFY:                                               │
│                                                                 │
│  Increase n_epochs when:                                       │
│  • Embedding looks unstable                                    │
│  • Clusters not well-formed                                    │
│  • You want more refined results                               │
│                                                                 │
│  Decrease n_epochs when:                                       │
│  • Speed is priority                                           │
│  • Quick exploration                                           │
│  • Results already good enough                                 │
│                                                                 │
│  TYPICAL VALUES:                                               │
│  • Quick preview: 50-100                                       │
│  • Normal use: 200-500 (default)                               │
│  • High quality: 750-1000                                      │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
8.3 Hyperparameter Selection Strategy
text

┌────────────────────────────────────────────────────────────────┐
│           SYSTEMATIC HYPERPARAMETER TUNING                      │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  STEP 1: Start with defaults                                   │
│  ─────────────────────────                                     │
│  • t-SNE: perplexity=30, learning_rate='auto'                  │
│  • UMAP: n_neighbors=15, min_dist=0.1                          │
│                                                                 │
│  STEP 2: Run and inspect                                       │
│  ────────────────────                                          │
│  • Do clusters look reasonable?                                │
│  • Is structure visible?                                       │
│  • Any obvious problems?                                       │
│                                                                 │
│  STEP 3: Diagnose problems                                     │
│  ─────────────────────                                         │
│                                                                 │
│  Problem: Clusters fragmenting into many small pieces          │
│  Solution: Increase n_neighbors/perplexity                     │
│                                                                 │
│  Problem: Everything merged into blob                          │
│  Solution: Decrease n_neighbors/perplexity                     │
│                                                                 │
│  Problem: Points too spread out                                │
│  Solution: Decrease min_dist                                   │
│                                                                 │
│  Problem: Points too clumped                                   │
│  Solution: Increase min_dist                                   │
│                                                                 │
│  Problem: t-SNE shows ball/sphere shape                        │
│  Solution: Increase learning_rate                              │
│                                                                 │
│  STEP 4: Grid search visualization                             │
│  ────────────────────────────────                              │
│  Create grid of plots with different parameters                │
│  Visually compare all results                                  │
│  Pick best looking configuration                               │
│                                                                 │
│  STEP 5: Validate with multiple runs                           │
│  ─────────────────────────────────                             │
│  Run best config with different random seeds                   │
│  Ensure results are consistent                                 │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
8.4 Parameter Selection Code Template
Python

# =========================================
# COMPREHENSIVE PARAMETER EXPLORATION
# =========================================

import numpy as np
import matplotlib.pyplot as plt
import umap
from sklearn.datasets import load_digits

# Load data
digits = load_digits()
X, y = digits.data, digits.target

# -----------------------------------------
# UMAP Grid Search Visualization
# -----------------------------------------
n_neighbors_options = [5, 15, 50, 100]
min_dist_options = [0.0, 0.1, 0.5, 0.9]

fig, axes = plt.subplots(len(n_neighbors_options), 
                          len(min_dist_options), 
                          figsize=(20, 20))

for i, n_neighbors in enumerate(n_neighbors_options):
    for j, min_dist in enumerate(min_dist_options):
        reducer = umap.UMAP(
            n_neighbors=n_neighbors,
            min_dist=min_dist,
            random_state=42
        )
        embedding = reducer.fit_transform(X)
        
        ax = axes[i, j]
        ax.scatter(embedding[:, 0], embedding[:, 1], 
                   c=y, cmap='tab10', s=3, alpha=0.7)
        ax.set_title(f'n_neighbors={n_neighbors}\nmin_dist={min_dist}')
        ax.axis('off')

plt.suptitle('UMAP Parameter Grid Search', fontsize=16)
plt.tight_layout()
plt.savefig('umap_grid_search.png', dpi=150)
plt.show()

# -----------------------------------------
# t-SNE Grid Search Visualization
# -----------------------------------------
from sklearn.manifold import TSNE

perplexity_options = [5, 15, 30, 50]
learning_rate_options = [50, 200, 500, 1000]

fig, axes = plt.subplots(len(perplexity_options), 
                          len(learning_rate_options), 
                          figsize=(20, 20))

for i, perplexity in enumerate(perplexity_options):
    for j, learning_rate in enumerate(learning_rate_options):
        tsne = TSNE(
            perplexity=perplexity,
            learning_rate=learning_rate,
            n_iter=1000,
            random_state=42
        )
        embedding = tsne.fit_transform(X)
        
        ax = axes[i, j]
        ax.scatter(embedding[:, 0], embedding[:, 1], 
                   c=y, cmap='tab10', s=3, alpha=0.7)
        ax.set_title(f'perplexity={perplexity}\nLR={learning_rate}')
        ax.axis('off')

plt.suptitle('t-SNE Parameter Grid Search', fontsize=16)
plt.tight_layout()
plt.savefig('tsne_grid_search.png', dpi=150)
plt.show()
<a name="chapter-9"></a>

📖 CHAPTER 9: Common Pitfalls & How to Avoid Them
9.1 Pitfall #1: Over-interpreting Cluster Sizes
text

┌────────────────────────────────────────────────────────────────┐
│             PITFALL: CLUSTER SIZE INTERPRETATION               │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  "This cluster is bigger, so it must have more points"        │
│                                                                 │
│  THE TRUTH:                                                     │
│  Cluster SIZE in t-SNE/UMAP does NOT reflect:                  │
│  • Number of points                                            │
│  • Density in original space                                   │
│  • Importance or variance                                      │
│                                                                 │
│  WHY?                                                          │
│  Both algorithms optimize LOCAL relationships                  │
│  They can stretch/compress clusters arbitrarily                │
│                                                                 │
│  VISUAL EXAMPLE:                                               │
│                                                                 │
│  Original Space:          t-SNE Result:                        │
│  ┌─────────────┐          ┌─────────────┐                      │
│  │ ▓▓ (100 pts)│          │████ (small) │ ← Same 100 points!  │
│  │ ░ (100 pts) │          │ ░░░░ (big)  │ ← Same 100 points!  │
│  └─────────────┘          └─────────────┘                      │
│                                                                 │
│  SOLUTION:                                                      │
│  • Color points by density                                     │
│  • Add point count labels                                      │
│  • Never assume size = count                                   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.2 Pitfall #2: Over-interpreting Distances Between Clusters
text

┌────────────────────────────────────────────────────────────────┐
│           PITFALL: INTER-CLUSTER DISTANCES                      │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  "Clusters A and B are close in the plot, so they must be     │
│   similar in the original high-dimensional space"              │
│                                                                 │
│  THE TRUTH:                                                     │
│  t-SNE: Inter-cluster distances are essentially RANDOM         │
│  UMAP:  Better, but still not reliable for exact comparison    │
│                                                                 │
│  WHY?                                                          │
│  • Focus is on LOCAL structure preservation                    │
│  • GLOBAL distances are sacrificed                             │
│  • Same data can produce different layouts                     │
│                                                                 │
│  DEMONSTRATION:                                                 │
│                                                                 │
│  Run 1:            Run 2:             Run 3:                   │
│  ┌────────┐        ┌────────┐         ┌────────┐               │
│  │ A  B   │        │ A    C │         │   B    │               │
│  │    C   │        │   B    │         │ C  A   │               │
│  └────────┘        └────────┘         └────────┘               │
│  A close to B      A close to C       C close to A              │
│                                                                 │
│  SOLUTION:                                                      │
│  • Don't measure distances with ruler                          │
│  • Use original high-D data for distance comparisons           │
│  • UMAP preserves global structure BETTER than t-SNE           │
│  • For hierarchical relationships, use dendrogram instead      │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.3 Pitfall #3: Thinking Clusters Are "Real"
text

┌────────────────────────────────────────────────────────────────┐
│              PITFALL: ARTIFICIAL CLUSTERS                       │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  "I see 5 distinct clusters in the t-SNE plot, so there       │
│   must be 5 natural groups in my data"                         │
│                                                                 │
│  THE TRUTH:                                                     │
│  t-SNE/UMAP can create APPARENT clusters from:                 │
│  • Continuous data (no real clusters)                          │
│  • Uniform random data                                         │
│  • Artifacts of hyperparameter choices                         │
│                                                                 │
│  FAMOUS EXAMPLE - CONTINUOUS DATA:                             │
│                                                                 │
│  Original: Continuous gradient                                 │
│  ░░░▒▒▒▓▓▓███  (smooth transition)                             │
│                                                                 │
│  t-SNE with low perplexity:                                    │
│  [░░] [▒▒▒] [▓▓▓] [███]  (artificial clusters!)               │
│                                                                 │
│  SOLUTION:                                                      │
│  1. Always validate clusters with other methods:               │
│     • K-means on original data                                 │
│     • Hierarchical clustering                                  │
│     • Silhouette scores                                        │
│                                                                 │
│  2. Try different perplexity/n_neighbors values               │
│     Real clusters: Appear across parameter ranges             │
│     Fake clusters: Disappear or merge with changes             │
│                                                                 │
│  3. Run multiple times with different random seeds             │
│     Consistent structure → more likely real                    │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.4 Pitfall #4: Ignoring Preprocessing
text

┌────────────────────────────────────────────────────────────────┐
│              PITFALL: POOR PREPROCESSING                        │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  Applying t-SNE/UMAP directly to raw data                      │
│                                                                 │
│  THE TRUTH:                                                     │
│  Preprocessing DRAMATICALLY affects results                    │
│                                                                 │
│  COMMON ISSUES:                                                │
│                                                                 │
│  1. Features on different scales                               │
│     • Feature A: 0-1                                           │
│     • Feature B: 1,000-10,000                                  │
│     • B dominates distance calculations!                       │
│     → SOLUTION: Standardize (StandardScaler)                   │
│                                                                 │
│  2. Too many dimensions                                        │
│     • 10,000 features → slow and noisy                        │
│     → SOLUTION: PCA first (reduce to 50-100 dims)             │
│                                                                 │
│  3. Outliers                                                   │
│     • Extreme values distort the embedding                    │
│     → SOLUTION: Clip or remove outliers                       │
│                                                                 │
│  4. Missing values                                             │
│     • t-SNE/UMAP can't handle NaN                             │
│     → SOLUTION: Impute or remove                              │
│                                                                 │
│  RECOMMENDED PREPROCESSING PIPELINE:                           │
│                                                                 │
│  Raw Data                                                      │
│      ↓                                                         │
│  Handle missing values                                         │
│      ↓                                                         │
│  Remove/clip outliers                                          │
│      ↓                                                         │
│  Standardize features (mean=0, std=1)                         │
│      ↓                                                         │
│  PCA (if dims > 50-100)                                       │
│      ↓                                                         │
│  t-SNE / UMAP                                                  │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.5 Pitfall #5: Single Random Seed
text

┌────────────────────────────────────────────────────────────────┐
│              PITFALL: NOT CHECKING STABILITY                    │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  Running once and assuming the result is definitive            │
│                                                                 │
│  THE TRUTH:                                                     │
│  Both algorithms have random initialization                    │
│  Results can vary significantly between runs                   │
│                                                                 │
│  EXAMPLE:                                                      │
│                                                                 │
│  Seed 1:         Seed 2:         Seed 3:                       │
│  ┌────────┐      ┌────────┐      ┌────────┐                    │
│  │ A      │      │      A │      │   A    │                    │
│  │   B    │      │ B      │      │     B  │                    │
│  │     C  │      │    C   │      │ C      │                    │
│  └────────┘      └────────┘      └────────┘                    │
│                                                                 │
│  Position and orientation can change!                          │
│  But STRUCTURE (relationships) should remain                   │
│                                                                 │
│  SOLUTION:                                                      │
│                                                                 │
│  # Run multiple times                                          │
│  results = []                                                  │
│  for seed in range(10):                                        │
│      embedding = UMAP(random_state=seed).fit_transform(X)      │
│      results.append(embedding)                                 │
│                                                                 │
│  # Compare results                                             │
│  # - Same clusters appearing? ✓ Reliable                       │
│  # - Different structures? ✗ Suspicious                        │
│                                                                 │
│  # For reproducibility, always set random_state                │
│  UMAP(random_state=42)                                         │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.6 Pitfall #6: Wrong Metric for Data Type
text

┌────────────────────────────────────────────────────────────────┐
│              PITFALL: INAPPROPRIATE METRIC                      │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  Using default Euclidean distance for all data types           │
│                                                                 │
│  THE TRUTH:                                                     │
│  Different data types need different distance metrics          │
│                                                                 │
│  RECOMMENDATIONS:                                              │
│                                                                 │
│  ┌─────────────────────┬────────────────────────────────────┐  │
│  │ DATA TYPE           │ RECOMMENDED METRIC                 │  │
│  ├─────────────────────┼────────────────────────────────────┤  │
│  │ General numerical   │ 'euclidean' (default)              │  │
│  │ Text / TF-IDF       │ 'cosine'                           │  │
│  │ Word embeddings     │ 'cosine'                           │  │
│  │ Gene expression     │ 'correlation'                      │  │
│  │ Binary features     │ 'hamming' or 'jaccard'             │  │
│  │ Sparse features     │ 'manhattan' or 'cosine'            │  │
│  │ Probability dists   │ 'hellinger' or 'jensen-shannon'    │  │
│  │ Geographic coords   │ 'haversine'                        │  │
│  └─────────────────────┴────────────────────────────────────┘  │
│                                                                 │
│  EXAMPLE - TEXT DATA:                                          │
│                                                                 │
│  # BAD: Euclidean doesn't account for document length          │
│  umap.UMAP(metric='euclidean').fit_transform(tfidf_matrix)     │
│                                                                 │
│  # GOOD: Cosine ignores magnitude, focuses on direction        │
│  umap.UMAP(metric='cosine').fit_transform(tfidf_matrix)        │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.7 Pitfall #7: Using for Quantitative Analysis
text

┌────────────────────────────────────────────────────────────────┐
│         PITFALL: QUANTITATIVE CONCLUSIONS FROM PLOTS            │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  THE MISTAKE:                                                   │
│  "Point A is 2.5 units from Point B in the t-SNE plot,         │
│   so their true distance is proportional to 2.5"               │
│                                                                 │
│  THE TRUTH:                                                     │
│  t-SNE/UMAP are for QUALITATIVE visualization                  │
│  NOT for quantitative distance/density measurement             │
│                                                                 │
│  WHAT YOU CAN SAY:                                             │
│  ✓ "There appear to be distinct groups"                        │
│  ✓ "Points labeled X tend to cluster together"                 │
│  ✓ "There's some overlap between groups A and B"               │
│                                                                 │
│  WHAT YOU CANNOT SAY:                                          │
│  ✗ "Cluster A is 3x larger than cluster B"                     │
│  ✗ "The distance between clusters A and B is exactly 5"        │
│  ✗ "There are exactly 4 clusters"                              │
│  ✗ "Cluster A is more dense than cluster B"                    │
│                                                                 │
│  FOR QUANTITATIVE ANALYSIS, USE:                               │
│  • Original high-dimensional distances                         │
│  • Clustering algorithms (K-means, DBSCAN)                     │
│  • Statistical tests                                           │
│  • Density estimation in original space                        │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
9.8 Complete Pitfall Avoidance Checklist
text

┌────────────────────────────────────────────────────────────────┐
│             ✓ PRE-ANALYSIS CHECKLIST                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  DATA PREPARATION:                                             │
│  □ Removed/imputed missing values                              │
│  □ Handled outliers (clipped/removed)                          │
│  □ Standardized features (if needed)                           │
│  □ Applied PCA if dimensions > 50                              │
│  □ Chose appropriate distance metric                           │
│                                                                 │
│  ALGORITHM SETTINGS:                                           │
│  □ Started with default parameters                             │
│  □ Set random_state for reproducibility                        │
│  □ Ran with multiple parameter values                          │
│                                                                 │
│  VALIDATION:                                                   │
│  □ Ran multiple times with different seeds                     │
│  □ Checked if structure is consistent                          │
│  □ Validated clusters with other methods                       │
│                                                                 │
│  INTERPRETATION:                                               │
│  □ Not over-interpreting cluster sizes                         │
│  □ Not measuring distances literally                           │
│  □ Not claiming exact cluster counts                           │
│  □ Using for exploration, not definitive conclusions           │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
<a name="chapter-10"></a>

📖 CHAPTER 10: Advanced Techniques & Tricks
10.1 Technique: PCA Preprocessing
Python

# =========================================
# PCA BEFORE t-SNE/UMAP
# =========================================

"""
WHY PCA FIRST?
1. Speed: Reduces computation time significantly
2. Noise reduction: Removes noisy dimensions
3. Memory: Smaller data fits in memory better
4. Often improves results!

RECOMMENDATION:
- If dims > 50: Apply PCA to ~50 components
- Keep 95% variance if unsure about components
"""

from sklearn.decomposition import PCA
from sklearn.manifold import TSNE
import umap
import numpy as np

# High dimensional data
X = np.random.randn(5000, 1000)  # 1000 features!

# -----------------------------------------
# Method 1: Fixed number of components
# -----------------------------------------
pca = PCA(n_components=50)
X_pca = pca.fit_transform(X)
print(f"Variance retained: {sum(pca.explained_variance_ratio_):.2%}")

# Now apply t-SNE/UMAP on reduced data
X_embedded = TSNE(n_components=2).fit_transform(X_pca)

# -----------------------------------------
# Method 2: Keep 95% variance
# -----------------------------------------
pca = PCA(n_components=0.95)  # Keep 95% variance
X_pca = pca.fit_transform(X)
print(f"Components needed for 95%: {pca.n_components_}")

# -----------------------------------------
# Timing comparison
# -----------------------------------------
import time

# Without PCA
start = time.time()
X_direct = umap.UMAP().fit_transform(X)
print(f"Direct UMAP: {time.time() - start:.2f}s")

# With PCA
start = time.time()
X_pca = PCA(n_components=50).fit_transform(X)
X_via_pca = umap.UMAP().fit_transform(X_pca)
print(f"PCA + UMAP: {time.time() - start:.2f}s")  # Usually faster!
10.2 Technique: Parametric UMAP
Python

# =========================================
# PARAMETRIC UMAP (NEURAL NETWORK VERSION)
# =========================================

"""
REGULAR UMAP: Creates embedding, but can't generalize well
PARAMETRIC UMAP: Trains a neural network to learn the mapping

ADVANTAGES:
- Can embed new data faster (just neural network forward pass)
- More consistent embeddings
- Can use GPU acceleration

INSTALLATION:
pip install tensorflow
pip install umap-learn[parametric_umap]
"""

from umap.parametric_umap import ParametricUMAP
import numpy as np

# Create data
X_train = np.random.randn(10000, 100)
X_test = np.random.randn(1000, 100)

# -----------------------------------------
# Train Parametric UMAP
# -----------------------------------------
embedder = ParametricUMAP(
    n_components=2,
    n_neighbors=15,
    min_dist=0.1,
    metric='euclidean',
    n_epochs=100,
    verbose=True
)

# Fit and transform training data
X_train_embedded = embedder.fit_transform(X_train)

# Transform new data (FAST - just neural network inference)
X_test_embedded = embedder.transform(X_test)

# -----------------------------------------
# Access the trained model
# -----------------------------------------
model = embedder.encoder  # This is a Keras model!
model.summary()

# Save and load
embedder.save('/path/to/model')
# loaded_embedder = ParametricUMAP.load('/path/to/model')
10.3 Technique: Supervised and Semi-Supervised UMAP
Python

# =========================================
# SUPERVISED UMAP
# =========================================

import umap
import numpy as np
from sklearn.datasets import load_digits

digits = load_digits()
X, y = digits.data, digits.target

# -----------------------------------------
# Unsupervised UMAP (normal)
# -----------------------------------------
reducer_unsupervised = umap.UMAP(random_state=42)
X_unsupervised = reducer_unsupervised.fit_transform(X)

# -----------------------------------------
# Supervised UMAP (uses labels)
# -----------------------------------------
reducer_supervised = umap.UMAP(random_state=42)
X_supervised = reducer_supervised.fit_transform(X, y=y)

# Supervised version will have MUCH clearer separation
# because it knows which points should be together!

# -----------------------------------------
# Semi-Supervised UMAP (partial labels)
# -----------------------------------------
# Create partial labels (-1 means unknown)
y_partial = y.copy()
unknown_mask = np.random.random(len(y)) > 0.2  # 80% unknown
y_partial[unknown_mask] = -1

reducer_semi = umap.UMAP(random_state=42)
X_semi = reducer_semi.fit_transform(X, y=y_partial)

# -----------------------------------------
# Comparison visualization
# -----------------------------------------
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(18, 5))

axes[0].scatter(X_unsupervised[:, 0], X_unsupervised[:, 1], 
                c=y, cmap='tab10', s=5)
axes[0].set_title('Unsupervised UMAP')

axes[1].scatter(X_supervised[:, 0], X_supervised[:, 1], 
                c=y, cmap='tab10', s=5)
axes[1].set_title('Supervised UMAP')

axes[2].scatter(X_semi[:, 0], X_semi[:, 1], 
                c=y, cmap='tab10', s=5)
axes[2].set_title('Semi-Supervised UMAP (20% labeled)')

plt.tight_layout()
plt.show()
10.4 Technique: Aligning Multiple UMAP Embeddings
Python

# =========================================
# ALIGNED UMAP (Multiple Datasets)
# =========================================

"""
USE CASE: You have multiple related datasets (e.g., time series)
          and want embeddings that are COMPARABLE
          
EXAMPLE: Single-cell RNA data from Day 1, Day 2, Day 3
         Want to see how cells move over time
"""

from umap import AlignedUMAP
import numpy as np

# Create synthetic time series data
np.random.seed(42)
n_samples = 500
n_features = 50

# Three "timepoints" with slight shifts
X_day1 = np.random.randn(n_samples, n_features)
X_day2 = X_day1 + np.random.randn(n_samples, n_features) * 0.2
X_day3 = X_day2 + np.random.randn(n_samples, n_features) * 0.2

# Stack into list
slices = [X_day1, X_day2, X_day3]

# -----------------------------------------
# Aligned UMAP
# -----------------------------------------
aligned_reducer = AlignedUMAP(
    n_neighbors=15,
    n_components=2,
    alignment_regularisation=0.01,  # How much to align
    alignment_window_size=2
)

embeddings = aligned_reducer.fit_transform(slices)

# embeddings is list of 3 arrays, all in same coordinate system!

# -----------------------------------------
# Visualize temporal progression
# -----------------------------------------
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 4))

for idx, (emb, title) in enumerate(zip(embeddings, ['Day 1', 'Day 2', 'Day 3'])):
    axes[idx].scatter(emb[:, 0], emb[:, 1], s=5, alpha=0.7)
    axes[idx].set_title(title)
    axes[idx].set_xlim(-10, 10)  # Same scale for comparison
    axes[idx].set_ylim(-10, 10)

plt.suptitle('Aligned UMAP - Temporal Progression')
plt.tight_layout()
plt.show()
10.5 Technique: UMAP for Clustering
Python

# =========================================
# UMAP + CLUSTERING PIPELINE
# =========================================

"""
UMAP can be used as preprocessing for clustering!
The embedding often makes clusters more separable.
"""

import umap
import numpy as np
from sklearn.cluster import KMeans, DBSCAN, HDBSCAN
from sklearn.metrics import silhouette_score
from sklearn.datasets import make_blobs

# Create data with clusters
X, y_true = make_blobs(n_samples=1000, n_features=50, 
                        centers=5, random_state=42)

# -----------------------------------------
# Method 1: Cluster in UMAP space (2D)
# -----------------------------------------
reducer = umap.UMAP(n_components=2, random_state=42)
X_embedded = reducer.fit_transform(X)

# KMeans on embedded data
kmeans = KMeans(n_clusters=5, random_state=42)
labels_embedded = kmeans.fit_predict(X_embedded)

# -----------------------------------------
# Method 2: Cluster in higher UMAP space
# -----------------------------------------
reducer_high = umap.UMAP(n_components=10, random_state=42)
X_embedded_high = reducer_high.fit_transform(X)

# Cluster in 10D (more structure preserved)
kmeans_high = KMeans(n_clusters=5, random_state=42)
labels_high = kmeans_high.fit_predict(X_embedded_high)

# -----------------------------------------
# Method 3: HDBSCAN (density-based, auto # clusters)
# -----------------------------------------
# pip install hdbscan
import hdbscan

clusterer = hdbscan.HDBSCAN(min_cluster_size=15)
labels_hdbscan = clusterer.fit_predict(X_embedded)

print(f"HDBSCAN found {len(set(labels_hdbscan)) - 1} clusters")
# Note: -1 labels are noise points

# -----------------------------------------
# Compare silhouette scores
# -----------------------------------------
print(f"KMeans on original: {silhouette_score(X, KMeans(5).fit_predict(X)):.3f}")
print(f"KMeans on UMAP 2D: {silhouette_score(X_embedded, labels_embedded):.3f}")
print(f"KMeans on UMAP 10D: {silhouette_score(X_embedded_high, labels_high):.3f}")
10.6 Technique: Interactive Visualization
Python

# =========================================
# INTERACTIVE UMAP VISUALIZATION
# =========================================

"""
Static plots are good, but INTERACTIVE plots are better!
Options:
- Plotly: Easy, web-based
- Bokeh: More customizable
- DataShader: For millions of points
"""

# -----------------------------------------
# Option 1: Plotly (easiest)
# -----------------------------------------
import plotly.express as px
import umap
from sklearn.datasets import load_digits
import pandas as pd

digits = load_digits()
X, y = digits.data, digits.target

# Compute UMAP
reducer = umap.UMAP(random_state=42)
X_embedded = reducer.fit_transform(X)

# Create DataFrame for Plotly
df = pd.DataFrame({
    'UMAP1': X_embedded[:, 0],
    'UMAP2': X_embedded[:, 1],
    'Digit': y.astype(str)
})

# Interactive scatter plot
fig = px.scatter(
    df, x='UMAP1', y='UMAP2', color='Digit',
    title='Interactive UMAP of Digits',
    hover_data=['Digit'],
    width=800, height=600
)
fig.show()  # Opens in browser!

# -----------------------------------------
# Option 2: DataShader (for LARGE datasets)
# -----------------------------------------
"""
pip install datashader holoviews bokeh
"""

# import datashader as ds
# import holoviews as hv
# from holoviews.operation.datashader import datashade

# For millions of points:
# hv.extension('bokeh')
# points = hv.Points(df, ['UMAP1', 'UMAP2'])
# datashade(points, cmap='fire')
10.7 Technique: Custom Distance Functions
Python

# =========================================
# CUSTOM DISTANCE METRICS IN UMAP
# =========================================

import umap
import numpy as np
from numba import njit

# -----------------------------------------
# Custom metric using Numba (required for speed)
# -----------------------------------------
@njit
def weighted_euclidean(x, y):
    """
    Euclidean distance with first half of features
    weighted 2x more than second half
    """
    n = len(x)
    mid = n // 2
    
    result = 0.0
    for i in range(mid):
        result += 2.0 * (x[i] - y[i]) ** 2  # 2x weight
    for i in range(mid, n):
        result += (x[i] - y[i]) ** 2  # 1x weight
    
    return np.sqrt(result)

# Use custom metric
reducer = umap.UMAP(metric=weighted_euclidean)
# X_embedded = reducer.fit_transform(X)

# -----------------------------------------
# Custom metric for specific domain
# -----------------------------------------
@njit
def dna_hamming(x, y):
    """
    Hamming distance for DNA sequences encoded as integers
    (0=A, 1=T, 2=G, 3=C)
    """
    n = len(x)
    mismatches = 0
    for i in range(n):
        if x[i] != y[i]:
            mismatches += 1
    return mismatches / n

# -----------------------------------------
# Using precomputed distance matrix
# -----------------------------------------
from sklearn.metrics import pairwise_distances

# Compute your custom distance matrix
X = np.random.randn(500, 50)
distance_matrix = pairwise_distances(X, metric='cosine')

# Use precomputed distances
reducer = umap.UMAP(metric='precomputed')
X_embedded = reducer.fit_transform(distance_matrix)
10.8 Technique: Reproducibility and Determinism
Python

# =========================================
# ENSURING REPRODUCIBLE RESULTS
# =========================================

import umap
import numpy as np
from sklearn.manifold import TSNE

# -----------------------------------------
# Set all random seeds
# -----------------------------------------
def set_all_seeds(seed=42):
    np.random.seed(seed)
    # If using TensorFlow
    # import tensorflow as tf
    # tf.random.set_seed(seed)
    # If using PyTorch
    # import torch
    # torch.manual_seed(seed)

set_all_seeds(42)

X = np.random.randn(1000, 50)

# -----------------------------------------
# UMAP with fixed seed
# -----------------------------------------
reducer = umap.UMAP(
    random_state=42,
    transform_seed=42,  # For transform() calls
    n_jobs=1            # Single thread for determinism
)
X_umap_1 = reducer.fit_transform(X)

# Run again - should be IDENTICAL
reducer = umap.UMAP(random_state=42, transform_seed=42, n_jobs=1)
X_umap_2 = reducer.fit_transform(X)

print(f"Results identical: {np.allclose(X_umap_1, X_umap_2)}")

# -----------------------------------------
# t-SNE with fixed seed
# -----------------------------------------
tsne = TSNE(
    n_components=2,
    random_state=42,
    n_jobs=1
)
X_tsne_1 = tsne.fit_transform(X)

tsne = TSNE(n_components=2, random_state=42, n_jobs=1)
X_tsne_2 = tsne.fit_transform(X)

print(f"Results identical: {np.allclose(X_tsne_1, X_tsne_2)}")

# -----------------------------------------
# For complete reproducibility, also fix:
# -----------------------------------------
# 1. NumPy random seed
# 2. Python random seed: import random; random.seed(42)
# 3. Environment variable: PYTHONHASHSEED=42
# 4. Single-threaded execution: n_jobs=1
<a name="chapter-11"></a>

📖 CHAPTER 11: Real-World Applications
11.1 Application: Single-Cell RNA Sequencing
Python

# =========================================
# SINGLE-CELL RNA-SEQ ANALYSIS
# =========================================

"""
BACKGROUND:
- Each cell has ~20,000 genes
- We measure expression level of each gene
- Want to find cell types, states, trajectories

This is THE most common use case for t-SNE/UMAP in biology!
"""

import numpy as np
import umap
import scanpy as sc  # pip install scanpy

# -----------------------------------------
# Load example dataset (built into scanpy)
# -----------------------------------------
adata = sc.datasets.pbmc3k()  # 3000 blood cells

print(f"Cells: {adata.n_obs}")
print(f"Genes: {adata.n_vars}")

# -----------------------------------------
# Standard preprocessing pipeline
# -----------------------------------------
# 1. Filter low quality cells and genes
sc.pp.filter_cells(adata, min_genes=200)
sc.pp.filter_genes(adata, min_cells=3)

# 2. Normalize (each cell to same total counts)
sc.pp.normalize_total(adata, target_sum=1e4)

# 3. Log transform
sc.pp.log1p(adata)

# 4. Find highly variable genes (most informative)
sc.pp.highly_variable_genes(adata, n_top_genes=2000)
adata = adata[:, adata.var.highly_variable]

# 5. Scale
sc.pp.scale(adata, max_value=10)

# 6. PCA
sc.tl.pca(adata, n_comps=50)

# -----------------------------------------
# Apply UMAP
# -----------------------------------------
sc.pp.neighbors(adata, n_neighbors=15, n_pcs=50)
sc.tl.umap(adata)

# -----------------------------------------
# Visualize
# -----------------------------------------
# Cluster the cells
sc.tl.leiden(adata, resolution=0.5)

# Plot UMAP colored by cluster
sc.pl.umap(adata, color='leiden', title='Cell Clusters')

# Plot UMAP colored by gene expression
sc.pl.umap(adata, color=['CD3D', 'CD79A', 'LYZ'], 
           title='Marker Genes')
11.2 Application: Image Embeddings Visualization
Python

# =========================================
# VISUALIZING IMAGE EMBEDDINGS (CNNs)
# =========================================

"""
GOAL: Understand what a neural network has learned
- Extract features from CNN
- Visualize in 2D
- See how images cluster by content
"""

import numpy as np
import umap
import matplotlib.pyplot as plt
from tensorflow.keras.applications import VGG16
from tensorflow.keras.applications.vgg16 import preprocess_input
from tensorflow.keras.preprocessing import image
from sklearn.datasets import load_sample_images
import os

# -----------------------------------------
# Load pre-trained CNN
# -----------------------------------------
# Use VGG16 without top classification layers
base_model = VGG16(weights='imagenet', include_top=False, pooling='avg')

# -----------------------------------------
# Extract features from images
# -----------------------------------------
def extract_features(img_path):
    """Extract CNN features from an image"""
    img = image.load_img(img_path, target_size=(224, 224))
    x = image.img_to_array(img)
    x = np.expand_dims(x, axis=0)
    x = preprocess_input(x)
    features = base_model.predict(x, verbose=0)
    return features.flatten()

# For demonstration, using CIFAR-10
from tensorflow.keras.datasets import cifar10

(X_train, y_train), (X_test, y_test) = cifar10.load_data()
X_sample = X_train[:1000]
y_sample = y_train[:1000].flatten()

# Extract features (resize to VGG input size)
from tensorflow.keras.applications.vgg16 import preprocess_input
from skimage.transform import resize

features = []
for img in X_sample:
    img_resized = resize(img, (224, 224), anti_aliasing=True)
    img_preprocessed = preprocess_input(img_resized * 255)
    feat = base_model.predict(np.expand_dims(img_preprocessed, 0), verbose=0)
    features.append(feat.flatten())

X_features = np.array(features)
print(f"Feature shape: {X_features.shape}")  # (1000, 512)

# -----------------------------------------
# Apply UMAP
# -----------------------------------------
reducer = umap.UMAP(n_neighbors=15, min_dist=0.1, random_state=42)
X_embedded = reducer.fit_transform(X_features)

# -----------------------------------------
# Visualize
# -----------------------------------------
class_names = ['airplane', 'automobile', 'bird', 'cat', 'deer',
               'dog', 'frog', 'horse', 'ship', 'truck']

plt.figure(figsize=(12, 10))
scatter = plt.scatter(X_embedded[:, 0], X_embedded[:, 1], 
                      c=y_sample, cmap='tab10', s=10, alpha=0.7)
plt.colorbar(scatter, ticks=range(10), label='Class')
plt.title('UMAP of VGG16 Features on CIFAR-10')
plt.xlabel('UMAP 1')
plt.ylabel('UMAP 2')
plt.show()
11.3 Application: NLP - Document Similarity
Python

# =========================================
# DOCUMENT SIMILARITY VISUALIZATION
# =========================================

"""
GOAL: Visualize how documents relate to each other
- Convert text to vectors
- Apply UMAP
- See topical clusters
"""

import numpy as np
import umap
from sklearn.datasets import fetch_20newsgroups
from sklearn.feature_extraction.text import TfidfVectorizer
import matplotlib.pyplot as plt

# -----------------------------------------
# Load text data
# -----------------------------------------
categories = ['comp.graphics', 'sci.med', 'rec.sport.baseball', 
              'talk.politics.guns', 'soc.religion.christian']

newsgroups = fetch_20newsgroups(subset='all', categories=categories,
                                 remove=('headers', 'footers', 'quotes'))

print(f"Documents: {len(newsgroups.data)}")
print(f"Categories: {newsgroups.target_names}")

# -----------------------------------------
# Convert to TF-IDF vectors
# -----------------------------------------
vectorizer = TfidfVectorizer(max_features=5000, stop_words='english')
X_tfidf = vectorizer.fit_transform(newsgroups.data)

print(f"TF-IDF shape: {X_tfidf.shape}")

# -----------------------------------------
# Apply UMAP with COSINE metric (important for text!)
# -----------------------------------------
reducer = umap.UMAP(
    n_neighbors=15,
    min_dist=0.1,
    metric='cosine',  # Crucial for text data!
    random_state=42
)

X_embedded = reducer.fit_transform(X_tfidf)

# -----------------------------------------
# Visualize
# -----------------------------------------
plt.figure(figsize=(12, 10))
scatter = plt.scatter(X_embedded[:, 0], X_embedded[:, 1],
                      c=newsgroups.target, cmap='Set1', s=5, alpha=0.7)

# Add legend
handles, _ = scatter.legend_elements()
plt.legend(handles, categories, title="Topic", loc='best')

plt.title('UMAP of 20 Newsgroups (TF-IDF)')
plt.xlabel('UMAP 1')
plt.ylabel('UMAP 2')
plt.show()
11.4 Application: Anomaly Detection
Python

# =========================================
# ANOMALY DETECTION VISUALIZATION
# =========================================

"""
GOAL: Identify anomalies/outliers in data
- Normal points form clusters
- Anomalies appear isolated
"""

import numpy as np
import umap
from sklearn.datasets import make_blobs
from sklearn.ensemble import IsolationForest
import matplotlib.pyplot as plt

# -----------------------------------------
# Create data with anomalies
# -----------------------------------------
np.random.seed(42)

# Normal data - 3 clusters
X_normal, _ = make_blobs(n_samples=900, n_features=50, 
                          centers=3, random_state=42)

# Anomalies - random points
X_anomaly = np.random.uniform(-10, 10, size=(100, 50))

# Combine
X = np.vstack([X_normal, X_anomaly])
y_true = np.array([0]*900 + [1]*100)  # 0=normal, 1=anomaly

# -----------------------------------------
# Detect anomalies
# -----------------------------------------
detector = IsolationForest(contamination=0.1, random_state=42)
y_pred = detector.fit_predict(X)
y_pred = (y_pred == -1).astype(int)  # Convert to 0/1

# -----------------------------------------
# Visualize with UMAP
# -----------------------------------------
reducer = umap.UMAP(random_state=42)
X_embedded = reducer.fit_transform(X)

plt.figure(figsize=(12, 5))

# Plot 1: True labels
plt.subplot(1, 2, 1)
colors = ['blue' if label == 0 else 'red' for label in y_true]
plt.scatter(X_embedded[:, 0], X_embedded[:, 1], c=colors, s=10, alpha=0.7)
plt.title('True Labels\n(Blue=Normal, Red=Anomaly)')

# Plot 2: Detected labels
plt.subplot(1, 2, 2)
colors = ['blue' if label == 0 else 'red' for label in y_pred]
plt.scatter(X_embedded[:, 0], X_embedded[:, 1], c=colors, s=10, alpha=0.7)
plt.title('Detected Anomalies\n(Isolation Forest)')

plt.tight_layout()
plt.show()

# -----------------------------------------
# Evaluate
# -----------------------------------------
from sklearn.metrics import classification_report
print(classification_report(y_true, y_pred, 
                            target_names=['Normal', 'Anomaly']))
11.5 Application: Customer Segmentation
Python

# =========================================
# CUSTOMER SEGMENTATION
# =========================================

"""
GOAL: Group customers by behavior for targeted marketing
"""

import numpy as np
import pandas as pd
import umap
from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# -----------------------------------------
# Create synthetic customer data
# -----------------------------------------
np.random.seed(42)
n_customers = 1000

data = {
    'recency': np.random.exponential(30, n_customers),  # Days since last purchase
    'frequency': np.random.poisson(5, n_customers),     # Number of purchases
    'monetary': np.random.exponential(100, n_customers),# Total spend
    'tenure': np.random.uniform(0, 5, n_customers),     # Years as customer
    'support_tickets': np.random.poisson(2, n_customers),
    'website_visits': np.random.poisson(10, n_customers),
    'email_opens': np.random.uniform(0, 1, n_customers),
    'product_views': np.random.poisson(20, n_customers),
}

df = pd.DataFrame(data)

# -----------------------------------------
# Preprocess
# -----------------------------------------
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df)

# -----------------------------------------
# Apply UMAP
# -----------------------------------------
reducer = umap.UMAP(n_neighbors=30, min_dist=0.0, random_state=42)
X_embedded = reducer.fit_transform(X_scaled)

# -----------------------------------------
# Cluster customers
# -----------------------------------------
kmeans = KMeans(n_clusters=4, random_state=42)
clusters = kmeans.fit_predict(X_embedded)

# -----------------------------------------
# Visualize segments
# -----------------------------------------
plt.figure(figsize=(10, 8))
scatter = plt.scatter(X_embedded[:, 0], X_embedded[:, 1],
                      c=clusters, cmap='Set1', s=30, alpha=0.7)
plt.colorbar(scatter, label='Segment')
plt.title('Customer Segments (UMAP + KMeans)')
plt.xlabel('UMAP 1')
plt.ylabel('UMAP 2')
plt.show()

# -----------------------------------------
# Analyze segments
# -----------------------------------------
df['segment'] = clusters

segment_profiles = df.groupby('segment').mean()
print("\nSegment Profiles:")
print(segment_profiles.round(2))
<a name="chapter-12"></a>

📖 CHAPTER 12: Interview Questions & Answers
12.1 Basic Questions
Q1: What is t-SNE and why is it used?
text

ANSWER:

t-SNE (t-distributed Stochastic Neighbor Embedding) is a non-linear 
dimensionality reduction technique used primarily for VISUALIZATION
of high-dimensional data in 2D or 3D.

KEY POINTS:
1. It preserves LOCAL structure (neighborhoods)
2. Uses probability distributions to model similarities
3. Uses Student's t-distribution in low-D space (solves crowding problem)
4. Optimizes using KL divergence

WHEN TO USE:
- Visualizing clusters in high-D data
- Exploring structure in datasets
- Presenting ML results to stakeholders

LIMITATIONS:
- Slow for large datasets
- Non-deterministic
- Can't add new points
- Global structure not preserved
Q2: What is the difference between PCA and t-SNE?
text

ANSWER:

┌─────────────────┬────────────────────┬────────────────────┐
│ ASPECT          │ PCA                │ t-SNE              │
├─────────────────┼────────────────────┼────────────────────┤
│ Type            │ Linear             │ Non-linear         │
├─────────────────┼────────────────────┼────────────────────┤
│ Preserves       │ Global variance    │ Local neighborhood │
├─────────────────┼────────────────────┼────────────────────┤
│ Speed           │ Very fast O(nd²)   │ Slow O(n²)         │
├─────────────────┼────────────────────┼────────────────────┤
│ Deterministic   │ Yes                │ No (random init)   │
├─────────────────┼────────────────────┼────────────────────┤
│ New data        │ Can project        │ Must re-run        │
├─────────────────┼────────────────────┼────────────────────┤
│ Interpretable   │ Yes (loadings)     │ No (dimensions     │
│ dimensions      │                    │ are arbitrary)     │
├─────────────────┼────────────────────┼────────────────────┤
│ Use case        │ Preprocessing,     │ Visualization      │
│                 │ noise reduction    │ only               │
└─────────────────┴────────────────────┴────────────────────┘

PRACTICAL TIP:
Often use PCA first to reduce to 50D, then t-SNE to 2D.
This combines speed of PCA with visualization power of t-SNE.
Q3: What is perplexity in t-SNE?
text

ANSWER:

Perplexity is a hyperparameter that controls the "effective number of 
neighbors" each point considers when building the probability distribution.

MATHEMATICAL DEFINITION:
Perplexity = 2^(Shannon entropy of probability distribution)

INTUITION:
- Low perplexity (5): Only nearest ~5 neighbors matter
  → Very local, fine-grained structure
  → Risk: May fragment natural clusters
  
- High perplexity (50): ~50 neighbors matter
  → Broader structure considered
  → Risk: May merge distinct clusters

GUIDELINES:
- Typical range: 5 to 50
- Default: 30
- Should be < n_samples / 3
- Larger datasets can use larger perplexity
- Always try multiple values!

RULE OF THUMB:
If you see artificial fragmentation → increase perplexity
If clusters merge → decrease perplexity
12.2 Intermediate Questions
Q4: How does t-SNE work step by step?
text

ANSWER:

STEP 1: Compute pairwise similarities in HIGH-D space
- For each pair (i,j), calculate probability P(j|i)
- Use Gaussian distribution centered at point i
- P(j|i) = exp(-d²ᵢⱼ/2σᵢ²) / Σₖ≠ᵢ exp(-d²ᵢₖ/2σᵢ²)

STEP 2: Symmetrize probabilities
- Pᵢⱼ = (P(j|i) + P(i|j)) / 2n
- This makes the similarity symmetric

STEP 3: Initialize LOW-D embedding randomly
- Start with random 2D positions for each point

STEP 4: Compute similarities in LOW-D space
- Use t-distribution (NOT Gaussian!)
- Qᵢⱼ = (1 + ||yᵢ-yⱼ||²)⁻¹ / Σₖ≠ₗ(1 + ||yₖ-yₗ||²)⁻¹

STEP 5: Minimize KL divergence between P and Q
- KL(P||Q) = Σᵢⱼ Pᵢⱼ log(Pᵢⱼ/Qᵢⱼ)
- Use gradient descent to move points in 2D
- Iterate until convergence

KEY INSIGHT:
- KL divergence penalizes putting similar points FAR apart
- t-distribution has heavy tails → distant points have room
Q5: Why does t-SNE use t-distribution in low-D space?
text

ANSWER:

THE PROBLEM (without t-distribution):
The "Crowding Problem" - in high-D, a point can have many equidistant 
neighbors. In 2D, there's not enough "room" to place them all equidistantly.

EXAMPLE:
In 10D, a point can have 10 equidistant neighbors.
In 2D, you can only have ~6 equidistant neighbors (hexagonal packing).

THE SOLUTION:
Use t-distribution instead of Gaussian in low-D space.

┌────────────────────────────────────────────────────────────┐
│                                                            │
│  Gaussian:                t-distribution:                  │
│     ╭╮                         ╭╮                          │
│    ╱  ╲                       ╱  ╲                         │
│   ╱    ╲ (thin tails)       ╱    ╲  (heavy tails)         │
│  ╱──────╲                 ─╱──────╲─                       │
│ ╱        ╲               ╱          ╲                      │
│                                                            │
└────────────────────────────────────────────────────────────┘

WHY IT HELPS:
1. Heavy tails allow moderately distant points to be FURTHER apart
2. This creates MORE SPACE for slightly closer neighbors
3. Prevents everything from collapsing into center
4. Results in better-separated clusters

MATHEMATICAL BENEFIT:
t-distribution with 1 degree of freedom (Cauchy) has infinite variance
→ Can model arbitrarily large distances
→ Solves the space constraint problem
Q6: What is UMAP and how does it differ from t-SNE?
text

ANSWER:

UMAP (Uniform Manifold Approximation and Projection) is a newer (2018) 
dimensionality reduction algorithm based on topological data analysis.

KEY DIFFERENCES:

1. THEORETICAL FOUNDATION:
   - t-SNE: Information theory (KL divergence)
   - UMAP: Algebraic topology (fuzzy simplicial sets)

2. SPEED:
   - t-SNE: O(n²) naive, O(n log n) with Barnes-Hut
   - UMAP: O(n^1.5) with much smaller constants
   - UMAP is typically 10-100x faster

3. GLOBAL STRUCTURE:
   - t-SNE: Poor preservation
   - UMAP: Better preservation (cross-entropy loss)

4. NEW DATA:
   - t-SNE: Must re-run entire algorithm
   - UMAP: Has transform() for new points

5. TARGET DIMENSIONS:
   - t-SNE: Works well only for 2-3D
   - UMAP: Works for any dimensionality

6. USABILITY:
   - t-SNE: Visualization only
   - UMAP: Can be used for ML preprocessing

PRACTICAL RECOMMENDATION:
Use UMAP by default in 2024+. t-SNE mainly for legacy/comparison.
12.3 Advanced Questions
Q7: Explain the mathematics of UMAP
text

ANSWER:

UMAP is based on three mathematical concepts:

1. RIEMANNIAN GEOMETRY
   - Data lies on a manifold (curved surface) in high-D space
   - We want to find this manifold structure

2. FUZZY TOPOLOGY
   - Build a "fuzzy simplicial complex" (weighted graph)
   - Edges represent "fuzzy" neighborhood relationships
   - Weight = membership strength (0 to 1)

3. CATEGORY THEORY
   - Used to formally prove the algorithm's properties

ALGORITHM STEPS:

a) Construct fuzzy graph in HIGH-D:
   - Find k nearest neighbors for each point
   - Compute local connectivity: ρᵢ = distance to nearest neighbor
   - Compute local scale σᵢ to achieve target entropy
   - Membership strength: μᵢⱼ = exp(-(dᵢⱼ - ρᵢ)/σᵢ)
   - Symmetrize: μᵢⱼ = μᵢⱼ + μⱼᵢ - μᵢⱼ × μⱼᵢ

b) Construct fuzzy graph in LOW-D:
   - Use parametric family: νᵢⱼ = 1/(1 + a×||yᵢ-yⱼ||^2b)
   - Parameters a, b chosen to approximate fuzzy set

c) Optimize using CROSS-ENTROPY:
   - CE = Σᵢⱼ [μᵢⱼ log(μᵢⱼ/νᵢⱼ) + (1-μᵢⱼ) log((1-μᵢⱼ)/(1-νᵢⱼ))]
   - First term: attractive (like t-SNE)
   - Second term: repulsive (NEW - better global structure!)
   - Use stochastic gradient descent with negative sampling

KEY INSIGHT:
The cross-entropy has BOTH attractive AND repulsive terms explicitly,
unlike t-SNE's KL divergence which only has attractive terms for 
connected pairs. This is why UMAP preserves global structure better.
Q8: How would you handle a dataset with 10 million points?
text

ANSWER:

For 10 million points, both standard t-SNE and UMAP face challenges.
Here's a comprehensive strategy:

1. PREPROCESSING:
   - Subsample if possible (random or stratified)
   - Reduce with PCA first (to 50-100 dims)

2. ALGORITHM CHOICES:
   
   a) UMAP with optimizations:
      - low_memory=True
      - Approximate nearest neighbors (default)
      - Can handle millions of points
      
   b) Parametric UMAP:
      - Trains neural network
      - Can embed new points very fast
      - Good for streaming data
      
   c) FIt-SNE:
      - Interpolation-based approximation
      - O(n) complexity
      - Can handle millions

3. INFRASTRUCTURE:
   - Use machine with lots of RAM (>64GB)
   - GPU acceleration if available
   - Distributed computing if necessary

4. VISUALIZATION STRATEGY:
   - Use density-based plotting (not scatter)
   - DataShader for rendering millions of points
   - Interactive downsampling

CODE EXAMPLE:
```python
import umap

# For 10M points
reducer = umap.UMAP(
    n_neighbors=15,
    n_components=2,
    low_memory=True,     # Reduce memory usage
    n_jobs=-1,           # Use all CPUs
    verbose=True         # Show progress
)

# Consider processing in batches
# Or use parametric UMAP for very large data
Q9: Can you use t-SNE/UMAP embeddings for machine learning tasks?
text

ANSWER:

SHORT ANSWER: 
- t-SNE: NOT recommended
- UMAP: Yes, with caution

DETAILED EXPLANATION:

t-SNE FOR ML:
× Non-deterministic → different results each run
× Can't embed new points → no train/test split properly
× Dimensions are arbitrary → no interpretability
× Only good for 2-3D → not useful for ML preprocessing
× Optimizes for visualization, not for class separation

UMAP FOR ML:
✓ More deterministic (with fixed seed)
✓ Has transform() for new data
✓ Works well in higher dimensions (10-50)
✓ Can use supervised mode
✓ Better global structure preserved

BEST PRACTICES FOR UMAP IN ML:

1. Always fit on training data ONLY:
   reducer = UMAP().fit(X_train)
   X_train_emb = reducer.transform(X_train)
   X_test_emb = reducer.transform(X_test)  # Use transform, not fit!

2. Use higher n_components (10-50), not 2D:
   UMAP(n_components=30)  # Better for ML than 2

3. Consider supervised UMAP:
   reducer.fit(X_train, y=y_train)  # Uses labels!

4. Always validate:
   - Compare performance to non-UMAP baseline
   - Check if UMAP actually helps

RECOMMENDED PIPELINE:
Raw data → StandardScaler → PCA(50) → UMAP(30, supervised) → Classifier
Q10: How would you explain t-SNE results to a non-technical stakeholder?
text

ANSWER:

SCRIPT FOR STAKEHOLDER PRESENTATION:

"Let me explain this visualization:

1. WHAT IT IS:
   This is a 'map' of our data. Each point represents one [customer/
   sample/document]. Originally, each point had [500] different 
   attributes - impossible to visualize. We've compressed it down 
   to this 2D picture.

2. WHAT POSITION MEANS:
   Points that are CLOSE together are SIMILAR according to our data.
   Points that are FAR apart are DIFFERENT.
   
3. WHAT THE CLUSTERS MEAN:
   The groups you see are natural patterns in the data.
   [Point to specific clusters and explain what they represent]

4. IMPORTANT CAVEATS:
   - The SIZE of clusters doesn't mean anything
   - The exact DISTANCE between clusters isn't precise
   - This is for EXPLORATION, not exact measurement

5. WHAT WE LEARNED:
   [Specific insights from the visualization]
   
6. NEXT STEPS:
   Now that we've identified these groups, we can [specific action]."

TIPS:
- Use analogies: "Like a satellite photo of a city showing neighborhoods"
- Color by something meaningful to them
- Point to specific examples they'd recognize
- Focus on actionable insights, not technical details
12.4 Practical/Coding Questions
Q11: Write code to compare t-SNE and UMAP with proper preprocessing
Python

# =========================================
# COMPLETE COMPARISON CODE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.manifold import TSNE
import umap
import time

def compare_tsne_umap(X, y, title="Comparison"):
    """
    Complete pipeline to compare t-SNE and UMAP
    with proper preprocessing and timing.
    """
    
    # Step 1: Preprocessing
    print("Preprocessing...")
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)
    
    # Step 2: PCA if high-dimensional
    if X.shape[1] > 50:
        print(f"Reducing from {X.shape[1]}D to 50D with PCA...")
        pca = PCA(n_components=50)
        X_reduced = pca.fit_transform(X_scaled)
        print(f"Variance retained: {sum(pca.explained_variance_ratio_):.2%}")
    else:
        X_reduced = X_scaled
    
    # Step 3: Apply t-SNE
    print("Running t-SNE...")
    start = time.time()
    tsne = TSNE(n_components=2, perplexity=30, random_state=42)
    X_tsne = tsne.fit_transform(X_reduced)
    tsne_time = time.time() - start
    print(f"t-SNE completed in {tsne_time:.2f}s")
    
    # Step 4: Apply UMAP
    print("Running UMAP...")
    start = time.time()
    reducer = umap.UMAP(n_components=2, n_neighbors=15, random_state=42)
    X_umap = reducer.fit_transform(X_reduced)
    umap_time = time.time() - start
    print(f"UMAP completed in {umap_time:.2f}s")
    
    # Step 5: Visualize
    fig, axes = plt.subplots(1, 2, figsize=(14, 6))
    
    # t-SNE plot
    scatter1 = axes[0].scatter(X_tsne[:, 0], X_tsne[:, 1], 
                                c=y, cmap='tab10', s=10, alpha=0.7)
    axes[0].set_title(f't-SNE ({tsne_time:.1f}s)')
    axes[0].set_xlabel('t-SNE 1')
    axes[0].set_ylabel('t-SNE 2')
    
    # UMAP plot
    scatter2 = axes[1].scatter(X_umap[:, 0], X_umap[:, 1], 
                                c=y, cmap='tab10', s=10, alpha=0.7)
    axes[1].set_title(f'UMAP ({umap_time:.1f}s)')
    axes[1].set_xlabel('UMAP 1')
    axes[1].set_ylabel('UMAP 2')
    
    plt.suptitle(title, fontsize=14)
    plt.tight_layout()
    plt.savefig('comparison.png', dpi=150)
    plt.show()
    
    return X_tsne, X_umap

# Usage:
from sklearn.datasets import load_digits
digits = load_digits()
X_tsne, X_umap = compare_tsne_umap(digits.data, digits.target, 
                                    "Digits Dataset Comparison")
Q12: How would you debug poor t-SNE/UMAP results?
text

ANSWER:

SYSTEMATIC DEBUGGING PROCESS:

1. CHECK YOUR DATA
   □ Any NaN or infinite values?
   □ Features on different scales? → Standardize
   □ Too many dimensions? → PCA first
   □ Outliers? → Clip or remove

2. CHECK PARAMETERS
   
   t-SNE Issues:
   ┌─────────────────────────────────────────────────────┐
   │ SYMPTOM                │ LIKELY CAUSE & FIX         │
   ├─────────────────────────────────────────────────────┤
   │ Ball/sphere shape      │ Learning rate too low      │
   │                        │ → Increase to 200-500      │
   ├─────────────────────────────────────────────────────┤
   │ Clusters fragmenting   │ Perplexity too low         │
   │                        │ → Increase perplexity      │
   ├─────────────────────────────────────────────────────┤
   │ Everything merged      │ Perplexity too high        │
   │                        │ → Decrease perplexity      │
   ├─────────────────────────────────────────────────────┤
   │ Chaotic result         │ Learning rate too high     │
   │                        │ → Decrease to 100-200      │
   ├─────────────────────────────────────────────────────┤
   │ Not converged          │ Not enough iterations      │
   │                        │ → Increase n_iter          │
   └─────────────────────────────────────────────────────┘
   
   UMAP Issues:
   ┌─────────────────────────────────────────────────────┐
   │ SYMPTOM                │ LIKELY CAUSE & FIX         │
   ├─────────────────────────────────────────────────────┤
   │ Very clumpy            │ min_dist too low           │
   │                        │ → Increase min_dist        │
   ├─────────────────────────────────────────────────────┤
   │ Too spread out         │ min_dist too high          │
   │                        │ → Decrease min_dist        │
   ├─────────────────────────────────────────────────────┤
   │ Fragmenting            │ n_neighbors too low        │
   │                        │ → Increase n_neighbors     │
   ├─────────────────────────────────────────────────────┤
   │ Merging                │ n_neighbors too high       │
   │                        │ → Decrease n_neighbors     │
   ├─────────────────────────────────────────────────────┤
   │ Wrong clusters         │ Wrong metric               │
   │                        │ → Try cosine for text      │
   └─────────────────────────────────────────────────────┘

3. RUN MULTIPLE TIMES
   - Run with 5-10 different random seeds
   - If results inconsistent → structure might be noise

4. TRY PARAMETER GRID
   - Plot grid of different parameter combinations
   - Visually select best configuration

5. VERIFY WITH OTHER METHODS
   - Run PCA to see global variance structure
   - Run clustering on original data
   - Compare with expected groupings
<a name="chapter-13"></a>

📖 CHAPTER 13: Quick Reference Cheat Sheet
13.1 t-SNE Quick Reference
text

┌────────────────────────────────────────────────────────────────┐
│                    t-SNE CHEAT SHEET                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IMPORT:                                                        │
│  from sklearn.manifold import TSNE                              │
│                                                                 │
│  BASIC USAGE:                                                   │
│  X_embedded = TSNE(n_components=2).fit_transform(X)             │
│                                                                 │
│  KEY PARAMETERS:                                                │
│  ┌────────────────┬─────────────────────────────────────────┐  │
│  │ Parameter      │ Description                             │  │
│  ├────────────────┼─────────────────────────────────────────┤  │
│  │ n_components   │ Target dimensions (usually 2)           │  │
│  │ perplexity     │ ~Number of neighbors (5-50, default 30) │  │
│  │ learning_rate  │ Step size (10-1000, default 'auto')     │  │
│  │ n_iter         │ Iterations (default 1000)               │  │
│  │ random_state   │ Seed for reproducibility                │  │
│  │ metric         │ Distance function (default 'euclidean') │  │
│  │ early_exag...  │ Initial P multiplier (default 12)       │  │
│  └────────────────┴─────────────────────────────────────────┘  │
│                                                                 │
│  RECOMMENDED SETTINGS:                                          │
│  tsne = TSNE(                                                   │
│      n_components=2,                                            │
│      perplexity=30,                                             │
│      learning_rate='auto',                                      │
│      n_iter=1000,                                               │
│      random_state=42                                            │
│  )                                                              │
│                                                                 │
│  PREPROCESSING PIPELINE:                                        │
│  1. Handle missing values                                       │
│  2. Remove outliers                                             │
│  3. StandardScaler()                                            │
│  4. PCA(n_components=50) if dims > 50                          │
│  5. TSNE()                                                      │
│                                                                 │
│  COMPLEXITY: O(n²) naive, O(n log n) Barnes-Hut                │
│                                                                 │
│  PROS:                    │  CONS:                             │
│  ✓ Excellent local        │  ✗ Slow                            │
│    structure              │  ✗ No transform()                  │
│  ✓ Great cluster          │  ✗ Poor global structure           │
│    separation             │  ✗ Non-deterministic               │
│  ✓ Widely known           │  ✗ Only 2-3D                       │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
13.2 UMAP Quick Reference
text

┌────────────────────────────────────────────────────────────────┐
│                     UMAP CHEAT SHEET                            │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IMPORT:                                                        │
│  import umap                                                    │
│                                                                 │
│  BASIC USAGE:                                                   │
│  X_embedded = umap.UMAP().fit_transform(X)                      │
│                                                                 │
│  KEY PARAMETERS:                                                │
│  ┌────────────────┬─────────────────────────────────────────┐  │
│  │ Parameter      │ Description                             │  │
│  ├────────────────┼─────────────────────────────────────────┤  │
│  │ n_components   │ Target dimensions (any, default 2)      │  │
│  │ n_neighbors    │ ~Number of neighbors (2-200, default 15)│  │
│  │ min_dist       │ Min distance (0-1, default 0.1)         │  │
│  │ metric         │ Distance function (default 'euclidean') │  │
│  │ random_state   │ Seed for reproducibility                │  │
│  │ n_epochs       │ Training epochs (auto or 200-500)       │  │
│  │ low_memory     │ For large datasets (default False)      │  │
│  └────────────────┴─────────────────────────────────────────┘  │
│                                                                 │
│  RECOMMENDED SETTINGS:                                          │
│  reducer = umap.UMAP(
│      n_components=2,                                            │
│      n_neighbors=15,                                            │
│      min_dist=0.1,                                              │
│      metric='euclidean',                                        │
│      random_state=42                                            │
│  )                                                              │
│                                                                 │
│  SPECIAL FEATURES:                                              │
│  • transform(): Embed new data                                  │
│    X_new_emb = reducer.transform(X_new)                         │
│                                                                 │
│  • Supervised: Use labels                                       │
│    reducer.fit(X, y=labels)                                     │
│                                                                 │
│  • Semi-supervised: Partial labels (-1 = unknown)               │
│    reducer.fit(X, y=partial_labels)                             │
│                                                                 │
│  • Inverse transform: Map back to high-D                        │
│    X_reconstructed = reducer.inverse_transform(X_embedded)      │
│                                                                 │
│  METRIC OPTIONS:                                                │
│  'euclidean', 'manhattan', 'cosine', 'correlation',             │
│  'hamming', 'jaccard', custom function with @njit               │
│                                                                 │
│  COMPLEXITY: O(n^1.5) approximately                             │
│                                                                 │
│  PROS:                    │  CONS:                             │
│  ✓ Fast (10-100x t-SNE)   │  ✗ Less widely known               │
│  ✓ Has transform()        │  ✗ Complex theory                  │
│  ✓ Better global struct   │  ✗ Still some randomness           │
│  ✓ Works any dimension    │                                    │
│  ✓ Supervised mode        │                                    │
│  ✓ Scales to millions     │                                    │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
13.3 Parameter Tuning Quick Reference
text

┌────────────────────────────────────────────────────────────────┐
│                PARAMETER TUNING GUIDE                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PROBLEM → SOLUTION                                             │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ CLUSTERS FRAGMENTING (too many small clusters)          │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ t-SNE: ↑ perplexity (try 40, 50)                        │   │
│  │ UMAP:  ↑ n_neighbors (try 30, 50)                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ CLUSTERS MERGING (everything blobs together)            │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ t-SNE: ↓ perplexity (try 15, 10)                        │   │
│  │ UMAP:  ↓ n_neighbors (try 10, 5)                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ BALL/SPHERE SHAPE (no structure visible)                │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ t-SNE: ↑ learning_rate (try 200, 500)                   │   │
│  │        ↑ n_iter (try 2000, 5000)                        │   │
│  │ UMAP:  ↑ n_epochs (try 500, 1000)                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ POINTS TOO CLUMPED (can't see individual points)        │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ UMAP: ↑ min_dist (try 0.3, 0.5)                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ POINTS TOO SPREAD (no cluster structure)                │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ UMAP: ↓ min_dist (try 0.05, 0.0)                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ CHAOTIC/RANDOM LOOKING                                  │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ t-SNE: ↓ learning_rate (try 100, 50)                    │   │
│  │ Both:  Check preprocessing (scale features!)            │   │
│  │        Try different random seeds                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ TOO SLOW                                                │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │ Both:  Apply PCA first (reduce to 50D)                  │   │
│  │ t-SNE: Use method='barnes_hut' (default)                │   │
│  │ UMAP:  Use low_memory=True                              │   │
│  │        Reduce n_epochs                                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
13.4 Code Templates
Template 1: Complete t-SNE Pipeline
Python

# =========================================
# COMPLETE t-SNE PIPELINE TEMPLATE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.manifold import TSNE

def tsne_pipeline(X, y=None, perplexity=30, random_state=42):
    """
    Complete t-SNE pipeline with preprocessing.
    
    Parameters:
    -----------
    X : array-like, shape (n_samples, n_features)
    y : array-like, shape (n_samples,), optional
        Labels for coloring
    perplexity : int, default=30
    random_state : int, default=42
    
    Returns:
    --------
    X_embedded : array, shape (n_samples, 2)
    """
    
    # Step 1: Handle missing values
    if np.isnan(X).any():
        from sklearn.impute import SimpleImputer
        X = SimpleImputer(strategy='mean').fit_transform(X)
        print("Imputed missing values")
    
    # Step 2: Standardize
    X_scaled = StandardScaler().fit_transform(X)
    print(f"Standardized: mean={X_scaled.mean():.4f}, std={X_scaled.std():.4f}")
    
    # Step 3: PCA if needed
    if X.shape[1] > 50:
        pca = PCA(n_components=50)
        X_reduced = pca.fit_transform(X_scaled)
        print(f"PCA: {X.shape[1]}D → 50D, variance={sum(pca.explained_variance_ratio_):.2%}")
    else:
        X_reduced = X_scaled
    
    # Step 4: t-SNE
    tsne = TSNE(
        n_components=2,
        perplexity=perplexity,
        learning_rate='auto',
        init='pca',
        n_iter=1000,
        random_state=random_state,
        verbose=1
    )
    X_embedded = tsne.fit_transform(X_reduced)
    
    # Step 5: Visualize
    plt.figure(figsize=(10, 8))
    if y is not None:
        scatter = plt.scatter(X_embedded[:, 0], X_embedded[:, 1],
                              c=y, cmap='tab10', s=10, alpha=0.7)
        plt.colorbar(scatter)
    else:
        plt.scatter(X_embedded[:, 0], X_embedded[:, 1], s=10, alpha=0.7)
    
    plt.title(f't-SNE (perplexity={perplexity})')
    plt.xlabel('t-SNE 1')
    plt.ylabel('t-SNE 2')
    plt.tight_layout()
    plt.show()
    
    return X_embedded

# Usage:
# X_embedded = tsne_pipeline(X, y, perplexity=30)
Template 2: Complete UMAP Pipeline
Python

# =========================================
# COMPLETE UMAP PIPELINE TEMPLATE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
import umap

class UMAPPipeline:
    """
    Complete UMAP pipeline with preprocessing and utilities.
    """
    
    def __init__(self, n_neighbors=15, min_dist=0.1, n_components=2,
                 metric='euclidean', random_state=42):
        self.n_neighbors = n_neighbors
        self.min_dist = min_dist
        self.n_components = n_components
        self.metric = metric
        self.random_state = random_state
        
        self.scaler = None
        self.pca = None
        self.reducer = None
        
    def fit_transform(self, X, y=None):
        """Fit and transform data."""
        
        # Step 1: Handle missing values
        if np.isnan(X).any():
            from sklearn.impute import SimpleImputer
            X = SimpleImputer(strategy='mean').fit_transform(X)
            print("Imputed missing values")
        
        # Step 2: Standardize
        self.scaler = StandardScaler()
        X_scaled = self.scaler.fit_transform(X)
        
        # Step 3: PCA if needed
        if X.shape[1] > 50:
            self.pca = PCA(n_components=50)
            X_reduced = self.pca.fit_transform(X_scaled)
            print(f"PCA: {X.shape[1]}D → 50D")
        else:
            X_reduced = X_scaled
        
        # Step 4: UMAP
        self.reducer = umap.UMAP(
            n_neighbors=self.n_neighbors,
            min_dist=self.min_dist,
            n_components=self.n_components,
            metric=self.metric,
            random_state=self.random_state,
            verbose=True
        )
        
        if y is not None:
            X_embedded = self.reducer.fit_transform(X_reduced, y=y)
        else:
            X_embedded = self.reducer.fit_transform(X_reduced)
        
        return X_embedded
    
    def transform(self, X_new):
        """Transform new data using fitted model."""
        
        if self.reducer is None:
            raise ValueError("Must call fit_transform first!")
        
        # Apply same preprocessing
        X_scaled = self.scaler.transform(X_new)
        
        if self.pca is not None:
            X_reduced = self.pca.transform(X_scaled)
        else:
            X_reduced = X_scaled
        
        return self.reducer.transform(X_reduced)
    
    def plot(self, X_embedded, y=None, title="UMAP Embedding"):
        """Visualize embedding."""
        
        plt.figure(figsize=(10, 8))
        
        if y is not None:
            scatter = plt.scatter(X_embedded[:, 0], X_embedded[:, 1],
                                  c=y, cmap='tab10', s=10, alpha=0.7)
            plt.colorbar(scatter)
        else:
            plt.scatter(X_embedded[:, 0], X_embedded[:, 1], s=10, alpha=0.7)
        
        plt.title(f'{title}\n(n_neighbors={self.n_neighbors}, min_dist={self.min_dist})')
        plt.xlabel('UMAP 1')
        plt.ylabel('UMAP 2')
        plt.tight_layout()
        plt.show()

# Usage:
# pipeline = UMAPPipeline(n_neighbors=15, min_dist=0.1)
# X_train_emb = pipeline.fit_transform(X_train, y_train)
# pipeline.plot(X_train_emb, y_train)
# X_test_emb = pipeline.transform(X_test)
Template 3: Parameter Grid Search
Python

# =========================================
# PARAMETER GRID SEARCH TEMPLATE
# =========================================

import numpy as np
import matplotlib.pyplot as plt
import umap
from sklearn.manifold import TSNE
from itertools import product

def umap_grid_search(X, y, n_neighbors_list, min_dist_list, 
                     save_path=None):
    """
    Visualize UMAP results across parameter combinations.
    """
    
    n_rows = len(n_neighbors_list)
    n_cols = len(min_dist_list)
    
    fig, axes = plt.subplots(n_rows, n_cols, 
                              figsize=(4*n_cols, 4*n_rows))
    
    for i, n_neighbors in enumerate(n_neighbors_list):
        for j, min_dist in enumerate(min_dist_list):
            
            reducer = umap.UMAP(
                n_neighbors=n_neighbors,
                min_dist=min_dist,
                random_state=42
            )
            embedding = reducer.fit_transform(X)
            
            ax = axes[i, j] if n_rows > 1 else axes[j]
            ax.scatter(embedding[:, 0], embedding[:, 1],
                       c=y, cmap='tab10', s=5, alpha=0.7)
            ax.set_title(f'nn={n_neighbors}, md={min_dist}')
            ax.axis('off')
    
    plt.suptitle('UMAP Parameter Grid Search', fontsize=14)
    plt.tight_layout()
    
    if save_path:
        plt.savefig(save_path, dpi=150)
    
    plt.show()

def tsne_grid_search(X, y, perplexity_list, lr_list, save_path=None):
    """
    Visualize t-SNE results across parameter combinations.
    """
    
    n_rows = len(perplexity_list)
    n_cols = len(lr_list)
    
    fig, axes = plt.subplots(n_rows, n_cols, 
                              figsize=(4*n_cols, 4*n_rows))
    
    for i, perplexity in enumerate(perplexity_list):
        for j, lr in enumerate(lr_list):
            
            tsne = TSNE(
                n_components=2,
                perplexity=perplexity,
                learning_rate=lr,
                random_state=42
            )
            embedding = tsne.fit_transform(X)
            
            ax = axes[i, j] if n_rows > 1 else axes[j]
            ax.scatter(embedding[:, 0], embedding[:, 1],
                       c=y, cmap='tab10', s=5, alpha=0.7)
            ax.set_title(f'perp={perplexity}, lr={lr}')
            ax.axis('off')
    
    plt.suptitle('t-SNE Parameter Grid Search', fontsize=14)
    plt.tight_layout()
    
    if save_path:
        plt.savefig(save_path, dpi=150)
    
    plt.show()

# Usage:
# umap_grid_search(X, y, 
#                  n_neighbors_list=[5, 15, 50],
#                  min_dist_list=[0.0, 0.1, 0.5])
#
# tsne_grid_search(X, y,
#                  perplexity_list=[5, 30, 50],
#                  lr_list=[50, 200, 500])
13.5 Decision Flowchart
text

┌────────────────────────────────────────────────────────────────┐
│           WHICH ALGORITHM SHOULD I USE?                         │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│                        START                                    │
│                          │                                      │
│                          ▼                                      │
│              ┌───────────────────────┐                         │
│              │ How many data points? │                         │
│              └───────────────────────┘                         │
│                    │           │                                │
│               <10,000     >10,000                               │
│                    │           │                                │
│                    ▼           ▼                                │
│              ┌─────────┐  ┌─────────┐                          │
│              │ Either  │  │  UMAP   │                          │
│              │ works   │  │  (faster)│                          │
│              └─────────┘  └─────────┘                          │
│                    │                                            │
│                    ▼                                            │
│         ┌─────────────────────────┐                            │
│         │ Need to add new points? │                            │
│         └─────────────────────────┘                            │
│              │            │                                     │
│             YES          NO                                     │
│              │            │                                     │
│              ▼            ▼                                     │
│         ┌───────┐    ┌────────┐                                │
│         │ UMAP  │    │ Either │                                │
│         └───────┘    └────────┘                                │
│                           │                                     │
│                           ▼                                     │
│           ┌───────────────────────────┐                        │
│           │ Global structure matters? │                        │
│           └───────────────────────────┘                        │
│                │              │                                 │
│               YES            NO                                 │
│                │              │                                 │
│                ▼              ▼                                 │
│           ┌───────┐     ┌───────┐                              │
│           │ UMAP  │     │ t-SNE │                              │
│           └───────┘     │ (may  │                              │
│                         │ look  │                              │
│                         │better)│                              │
│                         └───────┘                              │
│                                                                 │
│  DEFAULT RECOMMENDATION: Start with UMAP                       │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
13.6 Common Mistakes Checklist
text

┌────────────────────────────────────────────────────────────────┐
│              ✗ COMMON MISTAKES TO AVOID                        │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  □ Using raw data without standardization                      │
│  □ Applying to data with missing values (NaN)                  │
│  □ Using Euclidean metric for text/sparse data                 │
│  □ Running only once (not checking stability)                  │
│  □ Over-interpreting cluster sizes                             │
│  □ Measuring distances between clusters literally              │
│  □ Claiming exact number of clusters                           │
│  □ Using t-SNE embedding for ML training                       │
│  □ Fitting t-SNE/UMAP on test data                             │
│  □ Not setting random_state for reproducibility                │
│  □ Using very low perplexity/n_neighbors (<5)                  │
│  □ Using very high perplexity/n_neighbors (>100)               │
│  □ Skipping PCA for high-dimensional data (>100D)              │
│  □ Assuming t-SNE clusters = real clusters                     │
│  □ Publishing without trying multiple parameters               │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
13.7 Essential Formulas
text

┌────────────────────────────────────────────────────────────────┐
│                    ESSENTIAL FORMULAS                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  t-SNE HIGH-D SIMILARITY (Gaussian):                           │
│                                                                 │
│              exp(-||xᵢ - xⱼ||² / 2σᵢ²)                         │
│  P(j|i) = ──────────────────────────────                       │
│            Σₖ≠ᵢ exp(-||xᵢ - xₖ||² / 2σᵢ²)                      │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  t-SNE SYMMETRIC PROBABILITY:                                   │
│                                                                 │
│           P(j|i) + P(i|j)                                      │
│  Pᵢⱼ = ─────────────────────                                   │
│               2n                                                │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  t-SNE LOW-D SIMILARITY (t-distribution):                      │
│                                                                 │
│              (1 + ||yᵢ - yⱼ||²)⁻¹                              │
│  Qᵢⱼ = ─────────────────────────────                           │
│         Σₖ≠ₗ (1 + ||yₖ - yₗ||²)⁻¹                              │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  t-SNE COST FUNCTION (KL Divergence):                          │
│                                                                 │
│                              Pᵢⱼ                               │
│  KL(P||Q) = Σᵢ Σⱼ Pᵢⱼ log ─────                               │
│                              Qᵢⱼ                               │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  UMAP MEMBERSHIP STRENGTH:                                      │
│                                                                 │
│  μᵢⱼ = exp(-(dᵢⱼ - ρᵢ) / σᵢ)                                  │
│                                                                 │
│  where ρᵢ = distance to nearest neighbor                       │
│        σᵢ = local scale parameter                              │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  UMAP SYMMETRIZATION (Fuzzy Set Union):                        │
│                                                                 │
│  μᵢⱼ(sym) = μᵢⱼ + μⱼᵢ - μᵢⱼ × μⱼᵢ                             │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  UMAP LOW-D SIMILARITY:                                         │
│                                                                 │
│                    1                                           │
│  νᵢⱼ = ─────────────────────────                               │
│         1 + a × ||yᵢ - yⱼ||^(2b)                               │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  UMAP COST FUNCTION (Cross-Entropy):                            │
│                                                                 │
│  CE = Σᵢⱼ [μᵢⱼ log(μᵢⱼ/νᵢⱼ) + (1-μᵢⱼ) log((1-μᵢⱼ)/(1-νᵢⱼ))]  │
│        \_________________/   \_____________________________/   │
│          Attractive term           Repulsive term              │
│                                                                 │
│  ─────────────────────────────────────────────────────────────│
│                                                                 │
│  PERPLEXITY DEFINITION:                                         │
│                                                                 │
│  Perplexity = 2^H(P)                                           │
│                                                                 │
│  where H(P) = -Σⱼ P(j|i) log₂ P(j|i)  (Shannon entropy)        │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
🎓 CONCLUSION
Summary: What You've Learned
text

┌────────────────────────────────────────────────────────────────┐
│                 YOUR LEARNING JOURNEY                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✓ FUNDAMENTALS                                                │
│    • Why dimensionality reduction is needed                    │
│    • What high-dimensional data looks like                     │
│    • The curse of dimensionality                               │
│    • Linear vs non-linear methods                              │
│                                                                 │
│  ✓ t-SNE MASTERY                                               │
│    • Mathematical foundations (probabilities, KL divergence)   │
│    • Step-by-step algorithm understanding                      │
│    • Role of t-distribution (crowding problem solution)        │
│    • Perplexity and its effects                                │
│    • Optimization tricks (early exaggeration, momentum)        │
│                                                                 │
│  ✓ UMAP MASTERY                                                │
│    • Topological foundations (manifolds, fuzzy sets)           │
│    • Algorithm mechanics (k-NN graph, cross-entropy)           │
│    • Key parameters (n_neighbors, min_dist)                    │
│    • Special features (transform, supervised, inverse)         │
│    • Why it's faster and preserves global structure better     │
│                                                                 │
│  ✓ PRACTICAL SKILLS                                            │
│    • Complete implementation in Python                         │
│    • Preprocessing pipelines                                   │
│    • Parameter tuning strategies                               │
│    • Handling large datasets                                   │
│    • Common pitfalls and how to avoid them                     │
│                                                                 │
│  ✓ REAL-WORLD APPLICATIONS                                     │
│    • Single-cell RNA analysis                                  │
│    • Image embedding visualization                             │
│    • NLP document similarity                                   │
│    • Anomaly detection                                         │
│    • Customer segmentation                                     │
│                                                                 │
│  ✓ INTERVIEW READINESS                                         │
│    • Can explain concepts to technical and non-technical       │
│    • Know when to use which algorithm                          │
│    • Understand limitations and caveats                        │
│    • Ready for coding questions                                │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
Final Recommendations
text

┌────────────────────────────────────────────────────────────────┐
│                FINAL RECOMMENDATIONS                            │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. START WITH UMAP                                            │
│     It's faster, more versatile, and generally better.         │
│     Use t-SNE for comparison or specific use cases.            │
│                                                                 │
│  2. ALWAYS PREPROCESS                                          │
│     StandardScaler → PCA (if dims > 50) → UMAP/t-SNE           │
│                                                                 │
│  3. TRY MULTIPLE PARAMETERS                                    │
│     Never trust a single run. Try 3-5 parameter combinations.  │
│                                                                 │
│  4. RUN MULTIPLE SEEDS                                         │
│     Check stability. Consistent = trustworthy.                 │
│                                                                 │
│  5. INTERPRET CAREFULLY                                        │
│     • Clusters visible ≠ clusters real                         │
│     • Sizes don't mean anything                                │
│     • Distances are approximate                                │
│                                                                 │
│  6. VALIDATE WITH OTHER METHODS                                │
│     K-means, hierarchical clustering, silhouette scores        │
│                                                                 │
│  7. KEEP LEARNING                                              │
│     • Read original papers                                     │
│     • Follow new developments (TriMAP, PaCMAP, etc.)           │
│     • Practice on diverse datasets                             │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
📚 Further Reading
text

PAPERS:
• t-SNE: "Visualizing Data using t-SNE" - van der Maaten & Hinton (2008)
• UMAP: "UMAP: Uniform Manifold Approximation" - McInnes et al. (2018)

INTERACTIVE RESOURCES:
• https://distill.pub/2016/misread-tsne/ (How to Use t-SNE Effectively)
• https://pair-code.github.io/understanding-umap/ (Understanding UMAP)

DOCUMENTATION:
• sklearn t-SNE: sklearn.manifold.TSNE
• UMAP: umap-learn.readthedocs.io
Congratulations! 🎉

You now have comprehensive knowledge of t-SNE and UMAP, from the absolute basics to advanced applications. You're ready to:

✅ Implement both algorithms confidently
✅ Choose the right algorithm for your use case
✅ Tune parameters effectively
✅ Avoid common pitfalls
✅ Interpret results correctly
✅ Ace any interview question on these topics
Go forth and visualize high-dimensional data! 🚀