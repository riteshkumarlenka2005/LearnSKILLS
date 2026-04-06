The Ultimate KNN (K-Nearest Neighbors) Masterclass
From Zero to Hero: A Complete Learning Journey
📚 Table of Contents
Chapter 1: The Foundation - Understanding KNN from Scratch
Chapter 2: The Mathematics Behind KNN
Chapter 3: How KNN Actually Works - Step by Step
Chapter 4: Choosing the Right K Value
Chapter 5: Distance Metrics Deep Dive
Chapter 6: Data Preprocessing for KNN
Chapter 7: KNN for Classification
Chapter 8: KNN for Regression
Chapter 9: Weighted KNN
Chapter 10: Handling Large Datasets
Chapter 11: Advanced Optimization Techniques
Chapter 12: Real-World Implementation
Chapter 13: Common Pitfalls and Solutions
Chapter 14: Interview Questions & Answers
Chapter 15: Projects and Case Studies
Chapter 1: The Foundation - Understanding KNN from Scratch {#chapter-1-the-foundation}
1.1 What is KNN? (The Simplest Explanation Ever)
Imagine you move to a new neighborhood. You want to know if you'll like living there. What do you do? You look at your nearest neighbors!

If most of your neighbors are friendly → You'll probably have a good experience
If most of your neighbors love gardening → The neighborhood is probably garden-friendly
KNN works EXACTLY like this!

KNN Definition: K-Nearest Neighbors is a simple algorithm that stores all available cases and classifies/predicts new cases based on a similarity measure (distance functions).

1.2 The Core Philosophy
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   "Tell me who your neighbors are, and I'll tell you who you   │
│    are"                                                         │
│                                                                 │
│   - The KNN Philosophy                                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
1.3 Real-Life Analogies
Analogy 1: The Fruit Basket
text

You have a mystery fruit. You don't know what it is.

You measure:
- Its color (red)
- Its size (small)
- Its shape (round)

You look at 5 nearest fruits in your database:
- 3 are apples
- 2 are cherries

KNN says: "This mystery fruit is probably an APPLE!" (majority wins)
Analogy 2: Movie Recommendations
text

You want to know if you'll like a new movie.

KNN approach:
1. Find 5 people with similar taste as you
2. See what they rated this movie
3. Average their ratings = Your predicted rating
Analogy 3: House Prices
text

You want to estimate your house price.

KNN approach:
1. Find 5 similar houses nearby (same size, bedrooms, location)
2. Check their prices: $200K, $210K, $195K, $205K, $200K
3. Your estimated price = Average = $202K
1.4 Types of KNN
text

                    ┌─────────────────┐
                    │       KNN       │
                    └────────┬────────┘
                             │
            ┌────────────────┼────────────────┐
            │                │                │
            ▼                ▼                ▼
    ┌───────────────┐ ┌───────────────┐ ┌───────────────┐
    │Classification │ │  Regression   │ │    Search     │
    │               │ │               │ │  (Retrieval)  │
    └───────────────┘ └───────────────┘ └───────────────┘
    
    Predicts a        Predicts a        Finds similar
    category/class    continuous value  items
    
    Example:          Example:          Example:
    Spam or Not?      House Price?      Similar Products
1.5 Why is KNN Called a "Lazy Learner"?
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   EAGER LEARNER (e.g., Decision Tree, Neural Network)          │
│   ─────────────────────────────────────────────────────         │
│   Training Phase: Does heavy computation                        │
│   Prediction Phase: Quick predictions                           │
│                                                                 │
│   Like a student who studies hard BEFORE the exam               │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   LAZY LEARNER (KNN)                                            │
│   ─────────────────────────────────────────────────────         │
│   Training Phase: Does NOTHING! Just stores data                │
│   Prediction Phase: Does all computation here                   │
│                                                                 │
│   Like a student who doesn't study, opens book DURING exam      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
1.6 KNN Characteristics Summary
Characteristic	Description
Type	Supervised Learning
Learning Style	Instance-based / Lazy Learning
Use Cases	Classification & Regression
Training Time	O(1) - Just stores data
Prediction Time	O(n × d) - n=samples, d=features
Memory	High (stores all training data)
Interpretability	High (easy to explain)
Chapter 2: The Mathematics Behind KNN {#chapter-2-the-mathematics}
2.1 The Core Mathematical Concept
At its heart, KNN answers one question:

"How similar are two data points?"

We measure similarity using DISTANCE. Smaller distance = More similar.

2.2 Feature Space Visualization
text

Imagine each data point as a location in space:

2D Example (2 features):
                    │
              ●     │    ○ ○
           ●   ●    │      ○
          ● ●       │   ○
        ────────────┼────────────
             ●      │  ★ ○
           ●        │    ○ ○
                    │

● = Class A
○ = Class B  
★ = New point to classify

KNN asks: "Which class points are closest to ★?"
2.3 Distance Formulas Explained
2.3.1 Euclidean Distance (Most Common)
The straight-line distance between two points.

text

Formula for 2D:
┌────────────────────────────────────────────┐
│                                            │
│   d = √[(x₂-x₁)² + (y₂-y₁)²]              │
│                                            │
└────────────────────────────────────────────┘

Formula for n-dimensions:
┌────────────────────────────────────────────┐
│                                            │
│   d = √[Σᵢ(pᵢ - qᵢ)²]                     │
│                                            │
│   where i goes from 1 to n dimensions      │
│                                            │
└────────────────────────────────────────────┘
Example:

text

Point A = (1, 2)
Point B = (4, 6)

Distance = √[(4-1)² + (6-2)²]
         = √[3² + 4²]
         = √[9 + 16]
         = √25
         = 5

Visual:
        │
      6 │         B(4,6)
      5 │        /│
      4 │       / │ 4 units
      3 │      /  │
      2 │ A(1,2)──┘
      1 │    3 units
        └─────────────────
          1  2  3  4  5
2.3.2 Manhattan Distance (City Block Distance)
The distance if you can only move horizontally or vertically (like city blocks).

text

Formula:
┌────────────────────────────────────────────┐
│                                            │
│   d = Σᵢ|pᵢ - qᵢ|                         │
│                                            │
│   Sum of absolute differences              │
│                                            │
└────────────────────────────────────────────┘
Example:

text

Point A = (1, 2)
Point B = (4, 6)

Distance = |4-1| + |6-2|
         = 3 + 4
         = 7

Visual:
        │
      6 │         B(4,6)
      5 │         │
      4 │         │ Walk up 4
      3 │         │
      2 │ A───────┘ Walk right 3
      1 │    
        └─────────────────
          1  2  3  4  5
          
Total walk = 7 blocks
2.3.3 Minkowski Distance (The Generalized Formula)
text

┌────────────────────────────────────────────┐
│                                            │
│   d = (Σᵢ|pᵢ - qᵢ|ᵖ)^(1/p)                │
│                                            │
│   When p = 1 → Manhattan Distance          │
│   When p = 2 → Euclidean Distance          │
│   When p = ∞ → Chebyshev Distance          │
│                                            │
└────────────────────────────────────────────┘
2.3.4 Comparison Chart
text

                    Point A (1,2) to Point B (4,6)
                    
    ┌───────────────────┬─────────────────────┬─────────────┐
    │  Distance Type    │     Formula         │   Result    │
    ├───────────────────┼─────────────────────┼─────────────┤
    │  Euclidean (p=2)  │  √(3² + 4²)        │     5       │
    │  Manhattan (p=1)  │  |3| + |4|         │     7       │
    │  Chebyshev (p=∞)  │  max(|3|, |4|)     │     4       │
    └───────────────────┴─────────────────────┴─────────────┘
2.3.5 Visual Comparison of Distance Metrics
text

        All points at "distance = 1" from center
        
        Euclidean           Manhattan           Chebyshev
        (Circle)            (Diamond)           (Square)
        
           ···                 ·                 ·····
          ·   ·               ···               ·   ·
         ·     ·             ··+··             ·  +  ·
          ·   ·               ···               ·   ·
           ···                 ·                 ·····
2.4 When to Use Which Distance?
Distance	Best For	Avoid When
Euclidean	Continuous features, spatial data	High dimensions, mixed types
Manhattan	High dimensions, sparse data, grid-like movement	Continuous spatial data
Chebyshev	Chess-like movement, time constraints	General ML problems
Hamming	Categorical/binary data, text	Continuous data
Cosine	Text data, recommendations	Magnitude matters
Chapter 3: How KNN Actually Works - Step by Step {#chapter-3-how-knn-works}
3.1 The Complete KNN Algorithm
text

┌─────────────────────────────────────────────────────────────────┐
│                    KNN ALGORITHM STEPS                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   STEP 1: Load the training data                                │
│           (Store it - that's all for "training"!)              │
│                                                                 │
│   STEP 2: Choose the value of K                                 │
│           (Number of neighbors to consider)                     │
│                                                                 │
│   STEP 3: For each new data point to predict:                   │
│                                                                 │
│           3a. Calculate distance to ALL training points         │
│                                                                 │
│           3b. Sort distances (smallest to largest)              │
│                                                                 │
│           3c. Pick the K nearest neighbors                      │
│                                                                 │
│           3d. For Classification:                               │
│               → Count votes from K neighbors                    │
│               → Predict the majority class                      │
│                                                                 │
│           3e. For Regression:                                   │
│               → Calculate average of K neighbors' values        │
│               → Predict this average                            │
│                                                                 │
│   STEP 4: Return the prediction                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
3.2 Detailed Walkthrough Example
Problem: Classify a new fruit
Training Data:

text

┌──────────────────────────────────────────────────────────────┐
│  Fruit    │  Weight(g)  │  Diameter(cm)  │  Class           │
├───────────┼─────────────┼────────────────┼──────────────────┤
│  A        │     150     │      7         │  Apple           │
│  B        │     170     │      8         │  Apple           │
│  C        │     140     │      6         │  Apple           │
│  D        │     180     │      9         │  Orange          │
│  E        │     190     │     10         │  Orange          │
│  F        │     175     │      9         │  Orange          │
└──────────────────────────────────────────────────────────────┘

New Fruit (?) : Weight = 165g, Diameter = 7.5cm
Question: Is it an Apple or Orange?
Step-by-Step Solution (K=3):
Step 1: Calculate ALL distances

text

New Point: (165, 7.5)

Distance to A (150, 7):
  = √[(165-150)² + (7.5-7)²]
  = √[225 + 0.25]
  = √225.25
  = 15.01

Distance to B (170, 8):
  = √[(165-170)² + (7.5-8)²]
  = √[25 + 0.25]
  = √25.25
  = 5.02

Distance to C (140, 6):
  = √[(165-140)² + (7.5-6)²]
  = √[625 + 2.25]
  = √627.25
  = 25.04

Distance to D (180, 9):
  = √[(165-180)² + (7.5-9)²]
  = √[225 + 2.25]
  = √227.25
  = 15.07

Distance to E (190, 10):
  = √[(165-190)² + (7.5-10)²]
  = √[625 + 6.25]
  = √631.25
  = 25.12

Distance to F (175, 9):
  = √[(165-175)² + (7.5-9)²]
  = √[100 + 2.25]
  = √102.25
  = 10.11
Step 2: Sort by distance

text

┌───────────┬───────────────┬───────────────┐
│  Fruit    │   Distance    │    Class      │
├───────────┼───────────────┼───────────────┤
│  B        │     5.02      │    Apple      │  ← Nearest
│  F        │    10.11      │    Orange     │  ← 2nd
│  A        │    15.01      │    Apple      │  ← 3rd
│  D        │    15.07      │    Orange     │
│  C        │    25.04      │    Apple      │
│  E        │    25.12      │    Orange     │
└───────────┴───────────────┴───────────────┘
Step 3: Select K=3 nearest neighbors

text

Top 3 Neighbors:
1. B → Apple
2. F → Orange  
3. A → Apple
Step 4: Vote!

text

┌────────────────────────────────────────┐
│                                        │
│   Apple:  2 votes  ████████            │
│   Orange: 1 vote   ████                │
│                                        │
│   WINNER: Apple! 🍎                    │
│                                        │
└────────────────────────────────────────┘
Final Prediction: The new fruit is an APPLE!

3.3 Visual Representation
text

                Diameter (cm)
                    │
               10   │              E(Orange)
                    │         ●
                9   │     D(Orange)   F(Orange)
                    │        ●           ●
              8.5   │
                    │
                8   │           B(Apple)
                    │              ●
              7.5   │              ★ ← New Fruit
                    │
                7   │     A(Apple)
                    │        ●
                6   │  C(Apple)
                    │     ●
                    └───────────────────────────
                        140   150   160   170   180   190
                                Weight (g)

★ = New fruit to classify
● = Training data points

The 3 closest points to ★ are: B, F, A
2 are Apples, 1 is Orange
Therefore: ★ = Apple!
3.4 Pseudocode
text

ALGORITHM: K-Nearest Neighbors

INPUT:
    - training_data: List of (features, label) pairs
    - new_point: Features of point to classify
    - K: Number of neighbors

OUTPUT:
    - predicted_class (for classification)
    - predicted_value (for regression)

PROCEDURE:

    1. distances = empty list
    
    2. FOR each (point, label) IN training_data:
           dist = calculate_distance(new_point, point)
           distances.append((dist, label))
    
    3. sorted_distances = SORT(distances, by=distance, ascending=True)
    
    4. k_nearest = sorted_distances[0:K]
    
    5. IF classification:
           labels = [label for (dist, label) in k_nearest]
           predicted_class = MODE(labels)  # Most common
           RETURN predicted_class
           
       ELSE IF regression:
           values = [value for (dist, value) in k_nearest]
           predicted_value = MEAN(values)  # Average
           RETURN predicted_value

END ALGORITHM
Chapter 4: Choosing the Right K Value {#chapter-4-choosing-k}
4.1 Why K Matters So Much
The value of K is THE MOST CRITICAL hyperparameter in KNN.

text

Think of it this way:

K = 1  → "Trust only my SINGLE closest neighbor"
         (Very specific, might be wrong if that neighbor is noisy)

K = 100 → "Ask 100 neighbors and take majority vote"
         (Very general, might miss local patterns)

The BEST K → Balances specificity and generality
4.2 Effect of Different K Values
text

┌─────────────────────────────────────────────────────────────────┐
│                        SMALL K (e.g., K=1)                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✓ Captures local patterns well                                 │
│  ✓ Flexible decision boundary                                   │
│  ✗ Sensitive to noise/outliers                                  │
│  ✗ High variance (overfitting risk)                             │
│  ✗ Unstable predictions                                         │
│                                                                 │
│  Decision Boundary:  Very jagged, complex                       │
│                      ~~~~~∿∿∿~~~~∿∿∿~~~~                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                        LARGE K (e.g., K=50)                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✓ Robust to noise/outliers                                     │
│  ✓ Smooth decision boundary                                     │
│  ✓ Low variance (stable)                                        │
│  ✗ Misses local patterns                                        │
│  ✗ High bias (underfitting risk)                                │
│  ✗ Computationally expensive                                    │
│                                                                 │
│  Decision Boundary:  Very smooth, simple                        │
│                      ─────────────────────                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
4.3 Visual Impact of K
text

Dataset with some noise:

        │  ○ ○ ○ ○ ○ ○
        │    ○ ● ○ ○      ← ● is noise (wrong label in ○ region)
        │  ○ ○ ○ ○ ★      ← ★ is new point to classify
        │────────────────
        │  ● ● ● ● ●
        │    ● ● ● 
        │  ● ● ● ●

K = 1:  Nearest is ●(noise) → Predicts ● (WRONG!)
K = 3:  2 ○'s, 1 ● → Predicts ○ (CORRECT!)
K = 5:  4 ○'s, 1 ● → Predicts ○ (CORRECT!)
4.4 The Bias-Variance Tradeoff
text

                    │
        High        │  ←─ Small K (Overfitting)
        Variance    │     
                    │     ╲
                    │      ╲
                    │       ╲  Sweet
                    │        ╲ Spot
                    │         ╲
        Low         │          ╲
        Variance    │           ╲
                    │            ╲
                    │             ←─ Large K (Underfitting)
                    └───────────────────────────────────────
                    Low Bias ──────────────────→ High Bias
                    
                    Small K ────────────────────→ Large K
4.5 Odd vs Even K (For Classification)
text

⚠️  IMPORTANT RULE: Always use ODD K for binary classification!

Why? To avoid ties!

Example with K = 4 (EVEN):
    Neighbors: Class A, Class A, Class B, Class B
    Votes:     A=2, B=2
    Result:    TIE! 😱 What do we predict?

Example with K = 5 (ODD):
    Neighbors: Class A, Class A, Class A, Class B, Class B
    Votes:     A=3, B=2
    Result:    Clear winner = A ✓
4.6 Methods to Find Optimal K
Method 1: Elbow Method
Python

# Concept: Plot error vs K, find the "elbow"

K values:    1    3    5    7    9    11   13   15
Error:      15%  10%   6%   5%   5%   5%   6%   7%
             │    │    │    │    │    │    │    │
             │    │    │    └────┴────┘    │    │
             │    │    └── Elbow here! ────┘    │
             │    │         K=7 is optimal      │
             ▼    ▼                              ▼
            High  ↘                             ↗ High
            Error   ↘     Low Error plateau    ↗  Error
text

        Error
        │
    15% │●
        │ ╲
    10% │  ●
        │   ╲
     6% │    ●
        │     ╲
     5% │      ●────●────●         ← Plateau
        │                 ╲
     6% │                  ●
        │                   ╲
     7% │                    ●
        └─────────────────────────
            1  3  5  7  9  11 13 15
                      ↑
                 Optimal K (Elbow)
Method 2: Cross-Validation
text

┌─────────────────────────────────────────────────────────────────┐
│                    5-FOLD CROSS-VALIDATION                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   For each K value (1, 3, 5, 7, ...):                          │
│                                                                 │
│   Fold 1: [TEST][TRAIN][TRAIN][TRAIN][TRAIN] → Accuracy₁       │
│   Fold 2: [TRAIN][TEST][TRAIN][TRAIN][TRAIN] → Accuracy₂       │
│   Fold 3: [TRAIN][TRAIN][TEST][TRAIN][TRAIN] → Accuracy₃       │
│   Fold 4: [TRAIN][TRAIN][TRAIN][TEST][TRAIN] → Accuracy₄       │
│   Fold 5: [TRAIN][TRAIN][TRAIN][TRAIN][TEST] → Accuracy₅       │
│                                                                 │
│   Average Accuracy for this K = (Σ Accuracyᵢ) / 5              │
│                                                                 │
│   Select K with HIGHEST average accuracy!                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Method 3: Square Root Rule (Quick Heuristic)
text

┌────────────────────────────────────────────┐
│                                            │
│   K ≈ √n                                   │
│                                            │
│   where n = number of training samples     │
│                                            │
│   Example:                                 │
│   - 100 samples → K ≈ 10                   │
│   - 1000 samples → K ≈ 32                  │
│   - 10000 samples → K ≈ 100                │
│                                            │
│   ⚠️ This is just a starting point!        │
│      Always validate with cross-validation │
│                                            │
└────────────────────────────────────────────┘
4.7 K Selection Decision Tree
text

                        START
                          │
                          ▼
              ┌───────────────────────┐
              │  Is data very noisy?  │
              └───────────┬───────────┘
                    │           │
                   YES          NO
                    │           │
                    ▼           ▼
              Use larger K   Use smaller K
               (K ≥ 10)       (K = 3-7)
                    │           │
                    └─────┬─────┘
                          │
                          ▼
              ┌───────────────────────┐
              │ Is it binary class?  │
              └───────────┬───────────┘
                    │           │
                   YES          NO
                    │           │
                    ▼           ▼
              Make K odd    K can be any
                    │           │
                    └─────┬─────┘
                          │
                          ▼
              ┌───────────────────────┐
              │ Validate with         │
              │ Cross-Validation      │
              └───────────────────────┘
                          │
                          ▼
                    OPTIMAL K!
4.8 Common K Value Guidelines
Dataset Size	Recommended K Range	Notes
< 100	1-5	Small data, keep K small
100-1000	5-15	Medium data
1000-10000	10-50	Larger K acceptable
> 10000	√n	Use heuristic, then validate
Chapter 5: Distance Metrics Deep Dive {#chapter-5-distance-metrics}
5.1 Complete Distance Metrics Encyclopedia
5.1.1 Euclidean Distance (L2 Norm)
text

┌────────────────────────────────────────────────────────────────┐
│ EUCLIDEAN DISTANCE                                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Formula:  d(p,q) = √[Σᵢ(pᵢ - qᵢ)²]                            │
│                                                                │
│ Intuition: "As the crow flies" - straight line distance       │
│                                                                │
│ Properties:                                                    │
│   • Always non-negative                                        │
│   • d(p,q) = 0 if and only if p = q                           │
│   • Symmetric: d(p,q) = d(q,p)                                │
│   • Triangle inequality: d(p,r) ≤ d(p,q) + d(q,r)             │
│                                                                │
│ Best for:                                                      │
│   ✓ Continuous numerical data                                  │
│   ✓ When magnitude of difference matters                       │
│   ✓ Low to medium dimensional data                             │
│                                                                │
│ Avoid when:                                                    │
│   ✗ Features have different scales (normalize first!)         │
│   ✗ Very high dimensions (curse of dimensionality)            │
│   ✗ Categorical data                                           │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.2 Manhattan Distance (L1 Norm / City Block)
text

┌────────────────────────────────────────────────────────────────┐
│ MANHATTAN DISTANCE                                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Formula:  d(p,q) = Σᵢ|pᵢ - qᵢ|                                │
│                                                                │
│ Intuition: Distance if you can only move along grid lines     │
│            (like navigating Manhattan streets)                 │
│                                                                │
│ Visual:                                                        │
│         B──────┐                                               │
│         │      │  Manhattan path                               │
│         │      │                                               │
│         A──────┘                                               │
│                                                                │
│ Best for:                                                      │
│   ✓ High-dimensional data (more robust)                        │
│   ✓ Sparse data                                                │
│   ✓ When features represent counts                             │
│   ✓ Grid-based movement (games, routing)                       │
│                                                                │
│ Avoid when:                                                    │
│   ✗ Spatial/geographical data where diagonal movement ok      │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.3 Minkowski Distance (Generalized)
text

┌────────────────────────────────────────────────────────────────┐
│ MINKOWSKI DISTANCE                                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Formula:  d(p,q) = (Σᵢ|pᵢ - qᵢ|ᵖ)^(1/p)                       │
│                                                                │
│ Special Cases:                                                 │
│   p = 1  →  Manhattan Distance                                 │
│   p = 2  →  Euclidean Distance                                 │
│   p = ∞  →  Chebyshev Distance (max difference)               │
│                                                                │
│ Visualization of "unit circles" for different p:              │
│                                                                │
│    p=1           p=2           p=3           p=∞              │
│   (Diamond)     (Circle)      (Rounded)     (Square)          │
│      /\           ___           ___          ____             │
│     /  \        /     \       /     \       |    |            │
│    <    >      (   +   )     (   +   )      | +  |            │
│     \  /        \_____/       \_____/       |____|            │
│      \/                                                        │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.4 Chebyshev Distance (L∞ Norm)
text

┌────────────────────────────────────────────────────────────────┐
│ CHEBYSHEV DISTANCE                                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Formula:  d(p,q) = maxᵢ|pᵢ - qᵢ|                              │
│                                                                │
│ Intuition: Maximum difference in any single dimension         │
│            "King's move in chess" distance                     │
│                                                                │
│ Example:                                                       │
│   p = (1, 2, 3)                                               │
│   q = (4, 5, 9)                                               │
│   Differences: |4-1|=3, |5-2|=3, |9-3|=6                      │
│   Chebyshev distance = max(3, 3, 6) = 6                       │
│                                                                │
│ Best for:                                                      │
│   ✓ Chess-like movement                                        │
│   ✓ Warehouse logistics (diagonal movement allowed)           │
│   ✓ When worst-case difference matters                         │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.5 Cosine Similarity/Distance
text

┌────────────────────────────────────────────────────────────────┐
│ COSINE SIMILARITY & DISTANCE                                   │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Cosine Similarity:                                             │
│                      p · q           Σᵢ(pᵢ × qᵢ)               │
│   cos(θ) = ───────────────── = ─────────────────────────       │
│            ||p|| × ||q||       √(Σᵢpᵢ²) × √(Σᵢqᵢ²)            │
│                                                                │
│ Cosine Distance:                                               │
│   d(p,q) = 1 - cos(θ)                                         │
│                                                                │
│ Range:                                                         │
│   Similarity: -1 to 1 (1 = identical direction)               │
│   Distance:   0 to 2 (0 = identical direction)                │
│                                                                │
│ Visual:                                                        │
│              ↗ q                                               │
│             /                                                  │
│            / θ (angle)                                         │
│           /                                                    │
│          ↗ p                                                   │
│         ●                                                      │
│                                                                │
│   Small θ = Similar documents                                  │
│   θ = 90° = Completely different                               │
│   θ = 0°  = Identical (in direction)                          │
│                                                                │
│ Best for:                                                      │
│   ✓ Text data (TF-IDF vectors)                                │
│   ✓ Document similarity                                        │
│   ✓ When magnitude doesn't matter, only direction             │
│   ✓ Recommendation systems                                     │
│   ✓ High-dimensional sparse data                               │
│                                                                │
│ Key insight:                                                   │
│   • Ignores magnitude, only cares about angle                  │
│   • "How much do they point in the same direction?"           │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.6 Hamming Distance
text

┌────────────────────────────────────────────────────────────────┐
│ HAMMING DISTANCE                                               │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Formula:  d(p,q) = Number of positions where pᵢ ≠ qᵢ          │
│                                                                │
│ Example 1 (Binary):                                            │
│   p = [1, 0, 1, 1, 0]                                         │
│   q = [1, 1, 0, 1, 0]                                         │
│       [=, ≠, ≠, =, =]                                         │
│   Hamming distance = 2 (two positions differ)                 │
│                                                                │
│ Example 2 (Strings):                                           │
│   p = "karolin"                                               │
│   q = "kathrin"                                               │
│       [k=k, a=a, r≠t, o≠h, l≠r, i=i, n=n]                    │
│   Hamming distance = 3                                        │
│                                                                │
│ Best for:                                                      │
│   ✓ Binary/categorical data                                    │
│   ✓ Error detection (bit flips)                               │
│   ✓ DNA sequence comparison                                    │
│   ✓ One-hot encoded features                                   │
│                                                                │
│ Requirement:                                                   │
│   ⚠️ Both sequences must have SAME length!                    │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.1.7 Jaccard Distance
text

┌────────────────────────────────────────────────────────────────┐
│ JACCARD SIMILARITY & DISTANCE                                  │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ Jaccard Similarity:                                            │
│              |A ∩ B|          Intersection                     │
│   J(A,B) = ─────────── = ────────────────────                  │
│              |A ∪ B|            Union                          │
│                                                                │
│ Jaccard Distance:                                              │
│   d(A,B) = 1 - J(A,B)                                         │
│                                                                │
│ Example:                                                       │
│   A = {apple, banana, cherry}                                  │
│   B = {banana, cherry, date, elderberry}                       │
│                                                                │
│   A ∩ B = {banana, cherry}           → Size = 2               │
│   A ∪ B = {apple, banana, cherry, date, elderberry} → Size = 5│
│                                                                │
│   Jaccard Similarity = 2/5 = 0.4                              │
│   Jaccard Distance = 1 - 0.4 = 0.6                            │
│                                                                │
│ Best for:                                                      │
│   ✓ Set comparison                                             │
│   ✓ Document similarity (word sets)                            │
│   ✓ Market basket analysis                                     │
│   ✓ Binary attributes                                          │
│                                                                │
└────────────────────────────────────────────────────────────────┘
5.2 Distance Metric Selection Guide
text

┌─────────────────────────────────────────────────────────────────┐
│                 WHICH DISTANCE TO USE?                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   START                                                         │
│     │                                                           │
│     ▼                                                           │
│   What type of data?                                            │
│     │                                                           │
│     ├──→ Continuous numeric ──→ Euclidean or Manhattan         │
│     │         │                                                 │
│     │         └──→ High dimensions? ──→ Manhattan              │
│     │                                                           │
│     ├──→ Binary ──→ Hamming                                    │
│     │                                                           │
│     ├──→ Categorical (sets) ──→ Jaccard                        │
│     │                                                           │
│     ├──→ Text/Documents ──→ Cosine                             │
│     │                                                           │
│     └──→ Mixed types ──→ Gower Distance                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
5.3 The Curse of Dimensionality
text

⚠️  CRITICAL CONCEPT FOR KNN ⚠️

As dimensions increase, distance-based methods BREAK DOWN!

Why?

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   In high dimensions, ALL points become roughly equidistant!   │
│                                                                 │
│   Dimensions │  Nearest   │  Farthest  │  Ratio               │
│              │  Neighbor  │  Neighbor  │  (Far/Near)          │
│   ───────────┼────────────┼────────────┼─────────────          │
│       2      │    0.5     │    2.0     │    4.0                │
│      10      │    1.5     │    2.5     │    1.67               │
│     100      │    4.0     │    5.0     │    1.25               │
│    1000      │   10.0     │   10.5     │    1.05  ← Problem!   │
│                                                                 │
│   When nearest ≈ farthest, KNN can't distinguish!             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

Solutions:
1. Dimensionality reduction (PCA, t-SNE, UMAP)
2. Feature selection
3. Use Manhattan distance (more robust in high-D)
4. Use cosine similarity for sparse high-D data
Chapter 6: Data Preprocessing for KNN {#chapter-6-data-preprocessing}
6.1 Why Preprocessing is CRITICAL for KNN
text

⚠️  KNN IS EXTREMELY SENSITIVE TO:
    • Feature scales
    • Outliers
    • Missing values
    • Irrelevant features

Unlike tree-based models, KNN CANNOT handle these automatically!
6.2 Feature Scaling
The Problem:
text

Without scaling:

Feature 1: Age        → Range: 0-100
Feature 2: Salary ($) → Range: 20,000-500,000

Distance dominated by Salary!

Example:
Person A: Age=25, Salary=50,000
Person B: Age=26, Salary=50,001
Person C: Age=25, Salary=100,000

Distance A-B: √[(26-25)² + (50001-50000)²] = √[1 + 1] = 1.41
Distance A-C: √[(25-25)² + (100000-50000)²] = √[0 + 2.5×10⁹] = 50,000

Age difference is COMPLETELY IGNORED!
Solution 1: Min-Max Normalization (0-1 Scaling)
text

┌────────────────────────────────────────────────────────────────┐
│ MIN-MAX NORMALIZATION                                          │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│           x - min(X)                                           │
│   x' = ─────────────────                                       │
│         max(X) - min(X)                                        │
│                                                                │
│ Result: All values between 0 and 1                             │
│                                                                │
│ Example:                                                       │
│   Ages: [20, 25, 30, 35, 40]                                  │
│   min = 20, max = 40                                          │
│                                                                │
│   20 → (20-20)/(40-20) = 0.0                                  │
│   25 → (25-20)/(40-20) = 0.25                                 │
│   30 → (30-20)/(40-20) = 0.5                                  │
│   35 → (35-20)/(40-20) = 0.75                                 │
│   40 → (40-20)/(40-20) = 1.0                                  │
│                                                                │
│ Pros:                                                          │
│   ✓ Bounded range [0, 1]                                       │
│   ✓ Preserves zero values                                      │
│   ✓ Good for neural networks too                               │
│                                                                │
│ Cons:                                                          │
│   ✗ Sensitive to outliers                                      │
│   ✗ New data might fall outside [0, 1]                        │
│                                                                │
└────────────────────────────────────────────────────────────────┘
Solution 2: Standardization (Z-Score)
text

┌────────────────────────────────────────────────────────────────┐
│ STANDARDIZATION (Z-SCORE)                                      │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│         x - μ                                                  │
│   z = ─────────                                                │
│           σ                                                    │
│                                                                │
│   where μ = mean, σ = standard deviation                       │
│                                                                │
│ Result: Mean = 0, Standard Deviation = 1                       │
│                                                                │
│ Example:                                                       │
│   Ages: [20, 25, 30, 35, 40]                                  │
│   μ = 30, σ = 7.07                                            │
│                                                                │
│   20 → (20-30)/7.07 = -1.41                                   │
│   25 → (25-30)/7.07 = -0.71                                   │
│   30 → (30-30)/7.07 =  0.00                                   │
│   35 → (35-30)/7.07 = +0.71                                   │
│   40 → (40-30)/7.07 = +1.41                                   │
│                                                                │
│ Pros:                                                          │
│   ✓ Less affected by outliers                                  │
│   ✓ Handles unbounded features well                            │
│   ✓ Statistical interpretation (z-score)                       │
│                                                                │
│ Cons:                                                          │
│   ✗ Doesn't bound values                                       │
│   ✗ Doesn't preserve zero values                               │
│                                                                │
└────────────────────────────────────────────────────────────────┘
When to Use Which?
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   Use MIN-MAX when:                                             │
│   • You need values in a bounded range                          │
│   • No significant outliers                                     │
│   • Features are uniformly distributed                          │
│   • Neural networks (typically expect 0-1)                      │
│                                                                 │
│   Use STANDARDIZATION when:                                     │
│   • Outliers present                                            │
│   • Features are normally distributed                           │
│   • Algorithm assumes normal distribution                       │
│   • You want to compare z-scores                                │
│                                                                 │
│   For KNN: Both work! Standardization is generally safer.      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6.3 Handling Missing Values
text

┌─────────────────────────────────────────────────────────────────┐
│                 MISSING VALUE STRATEGIES                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Option 1: REMOVE rows with missing values                       │
│   • Simple but loses data                                       │
│   • Use if < 5% data has missing values                        │
│                                                                 │
│ Option 2: IMPUTE with mean/median/mode                          │
│   • Mean: For normally distributed numeric data                 │
│   • Median: For skewed numeric data (robust to outliers)       │
│   • Mode: For categorical data                                  │
│                                                                 │
│ Option 3: KNN IMPUTATION (Ironic but effective!)               │
│   • Use KNN itself to predict missing values                   │
│   • Fills missing based on similar samples                     │
│                                                                 │
│ Option 4: Add MISSING INDICATOR feature                         │
│   • Add binary column: 1 if was missing, 0 otherwise           │
│   • Then impute original column                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6.4 Handling Outliers
text

┌─────────────────────────────────────────────────────────────────┐
│                     OUTLIER DETECTION                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Method 1: IQR (Interquartile Range)                            │
│                                                                 │
│   Q1 = 25th percentile                                          │
│   Q3 = 75th percentile                                          │
│   IQR = Q3 - Q1                                                 │
│                                                                 │
│   Lower bound = Q1 - 1.5 × IQR                                  │
│   Upper bound = Q3 + 1.5 × IQR                                  │
│                                                                 │
│   Values outside bounds = Outliers                              │
│                                                                 │
│ Method 2: Z-Score                                               │
│                                                                 │
│   |z-score| > 3 → Outlier (more than 3σ from mean)             │
│                                                                 │
│ Method 3: Visual (Box plot, Scatter plot)                       │
│                                                                 │
│                    Outliers                                     │
│                    ●     ●                                      │
│             ┌──────┬──────┐                                     │
│     ●───────┤      │      ├───────●                             │
│             └──────┴──────┘                                     │
│           Q1      Q2     Q3                                     │
│                 (Median)                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

HANDLING OPTIONS:
1. Remove outliers (if noise)
2. Cap at bounds (winsorization)
3. Transform (log, sqrt) to reduce impact
4. Use robust scaling: (x - median) / IQR
6.5 Handling Categorical Features
text

KNN requires NUMERICAL distances. Categorical data must be encoded!

┌─────────────────────────────────────────────────────────────────┐
│                    ENCODING METHODS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 1. ONE-HOT ENCODING (Best for KNN with nominal categories)     │
│                                                                 │
│    Color: [Red, Blue, Green]                                   │
│                                                                 │
│    Becomes:                                                     │
│    Color_Red  Color_Blue  Color_Green                          │
│        1          0           0        ← Red                   │
│        0          1           0        ← Blue                  │
│        0          0           1        ← Green                 │
│                                                                 │
│    ✓ No ordinal assumption                                      │
│    ✗ High dimensionality with many categories                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 2. LABEL ENCODING (Only for ordinal categories)                │
│                                                                 │
│    Size: [Small, Medium, Large]                                 │
│                                                                 │
│    Becomes:                                                     │
│    Size_encoded                                                 │
│        0        ← Small                                         │
│        1        ← Medium                                        │
│        2        ← Large                                         │
│                                                                 │
│    ✓ Preserves order                                            │
│    ✓ No dimension increase                                      │
│    ✗ Implies magnitude (Medium is NOT 2× Small!)               │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 3. TARGET ENCODING (Advanced)                                   │
│                                                                 │
│    Replace category with mean of target for that category      │
│                                                                 │
│    City    Target    City_encoded                              │
│    NYC       1       →   0.75   (avg target for NYC)           │
│    LA        0       →   0.25   (avg target for LA)            │
│    NYC       1       →   0.75                                   │
│    LA        0       →   0.25                                   │
│                                                                 │
│    ⚠️ Risk of data leakage! Use with cross-validation.         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6.6 Complete Preprocessing Pipeline
Python

"""
COMPLETE KNN PREPROCESSING PIPELINE
"""

# Step 1: Handle Missing Values
# Step 2: Encode Categorical Variables  
# Step 3: Remove/Handle Outliers
# Step 4: Scale Features
# Step 5: (Optional) Reduce Dimensionality

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   Raw Data                                                      │
│      │                                                          │
│      ▼                                                          │
│   ┌──────────────────┐                                          │
│   │ Handle Missing   │ ← Impute or remove                       │
│   └────────┬─────────┘                                          │
│            ▼                                                    │
│   ┌──────────────────┐                                          │
│   │ Encode Cats      │ ← One-hot, Label, etc.                   │
│   └────────┬─────────┘                                          │
│            ▼                                                    │
│   ┌──────────────────┐                                          │
│   │ Handle Outliers  │ ← Remove, cap, or transform              │
│   └────────┬─────────┘                                          │
│            ▼                                                    │
│   ┌──────────────────┐                                          │
│   │ Scale Features   │ ← StandardScaler or MinMaxScaler         │
│   └────────┬─────────┘                                          │
│            ▼                                                    │
│   ┌──────────────────┐                                          │
│   │ Dimensionality   │ ← PCA if high dimensions                 │
│   │ Reduction        │                                          │
│   └────────┬─────────┘                                          │
│            ▼                                                    │
│   Clean Data Ready for KNN!                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 7: KNN for Classification {#chapter-7-classification}
7.1 Classification Mechanism
text

┌─────────────────────────────────────────────────────────────────┐
│                 KNN CLASSIFICATION PROCESS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. Receive new sample to classify                             │
│                                                                 │
│   2. Calculate distance to all training samples                 │
│                                                                 │
│   3. Select K nearest neighbors                                 │
│                                                                 │
│   4. Count class labels among K neighbors                       │
│                                                                 │
│   5. Assign class with MAJORITY vote                            │
│                                                                 │
│   6. (Optional) Return probability estimates                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
7.2 Voting Mechanisms
Simple Majority Voting
text

K = 5 neighbors found:
[Class A, Class A, Class B, Class A, Class B]

Count:
Class A: 3 votes
Class B: 2 votes

Winner: Class A (majority)
Probability Estimation
text

K = 5 neighbors:
Class A: 3, Class B: 2

Probability estimates:
P(Class A) = 3/5 = 0.60 = 60%
P(Class B) = 2/5 = 0.40 = 40%

Prediction: Class A
Confidence: 60%
7.3 Handling Ties
text

K = 4 (even number - ties possible!)

Scenario:
Class A: 2 votes
Class B: 2 votes

Tie-Breaking Strategies:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│ 1. REDUCE K                                                     │
│    Remove farthest neighbor, try again with K-1                │
│                                                                 │
│ 2. DISTANCE WEIGHTING                                           │
│    Closer neighbors get higher weight                           │
│    Sum of weighted votes breaks the tie                        │
│                                                                 │
│ 3. PRIOR PROBABILITY                                            │
│    Choose class with higher frequency in training data         │
│                                                                 │
│ 4. RANDOM                                                       │
│    Randomly pick one (not recommended)                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

BEST PRACTICE: Use odd K to avoid ties in binary classification!
7.4 Multi-Class Classification
text

KNN naturally handles multiple classes!

Example: Classify flower species (3 classes)

K = 7 neighbors:
- Setosa: 1
- Versicolor: 4  ← Winner!
- Virginica: 2

Prediction: Versicolor

Probabilities:
P(Setosa) = 1/7 = 14.3%
P(Versicolor) = 4/7 = 57.1%
P(Virginica) = 2/7 = 28.6%
7.5 Complete Classification Example
text

┌─────────────────────────────────────────────────────────────────┐
│          CUSTOMER CHURN PREDICTION EXAMPLE                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ TRAINING DATA (after preprocessing):                            │
│                                                                 │
│ Customer │ Age(norm) │ Tenure(norm) │ Balance(norm) │ Churned  │
│ ─────────┼───────────┼──────────────┼───────────────┼──────────│
│    1     │    0.2    │     0.5      │     0.3       │    No    │
│    2     │    0.8    │     0.1      │     0.9       │    Yes   │
│    3     │    0.3    │     0.7      │     0.4       │    No    │
│    4     │    0.7    │     0.2      │     0.8       │    Yes   │
│    5     │    0.4    │     0.6      │     0.3       │    No    │
│    6     │    0.6    │     0.3      │     0.7       │    Yes   │
│                                                                 │
│ NEW CUSTOMER: Age=0.5, Tenure=0.4, Balance=0.5                 │
│ K = 3                                                           │
│                                                                 │
│ STEP 1: Calculate distances                                     │
│                                                                 │
│ d₁ = √[(0.5-0.2)² + (0.4-0.5)² + (0.5-0.3)²] = 0.374           │
│ d₂ = √[(0.5-0.8)² + (0.4-0.1)² + (0.5-0.9)²] = 0.583           │
│ d₃ = √[(0.5-0.3)² + (0.4-0.7)² + (0.5-0.4)²] = 0.374           │
│ d₄ = √[(0.5-0.7)² + (0.4-0.2)² + (0.5-0.8)²] = 0.412           │
│ d₅ = √[(0.5-0.4)² + (0.4-0.6)² + (0.5-0.3)²] = 0.300 ← Nearest │
│ d₆ = √[(0.5-0.6)² + (0.4-0.3)² + (0.5-0.7)²] = 0.245 ← Nearest │
│                                                                 │
│ STEP 2: Sort and select K=3 nearest                            │
│                                                                 │
│ Nearest: Customer 6 (d=0.245, Yes)                              │
│ 2nd:     Customer 5 (d=0.300, No)                               │
│ 3rd:     Customer 1 or 3 (d=0.374, No)                          │
│                                                                 │
│ STEP 3: Vote                                                    │
│                                                                 │
│ Yes: 1 vote                                                     │
│ No:  2 votes ← WINNER                                          │
│                                                                 │
│ PREDICTION: This customer will NOT churn                        │
│ PROBABILITY: P(No) = 2/3 = 66.7%                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
7.6 Evaluation Metrics for KNN Classification
text

┌─────────────────────────────────────────────────────────────────┐
│                   CONFUSION MATRIX                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                        Predicted                                │
│                    │  Positive  │  Negative  │                 │
│         ───────────┼────────────┼────────────┤                 │
│         Positive   │     TP     │     FN     │                 │
│  Actual ───────────┼────────────┼────────────┤                 │
│         Negative   │     FP     │     TN     │                 │
│                                                                 │
│ TP = True Positive   (Correctly predicted positive)            │
│ TN = True Negative   (Correctly predicted negative)            │
│ FP = False Positive  (Type I error - false alarm)              │
│ FN = False Negative  (Type II error - missed detection)        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

KEY METRICS:

┌────────────────────────────────────────────────────────────────┐
│                                                                │
│ Accuracy = (TP + TN) / (TP + TN + FP + FN)                    │
│   "Overall correctness"                                        │
│                                                                │
│ Precision = TP / (TP + FP)                                     │
│   "Of all positive predictions, how many were correct?"       │
│                                                                │
│ Recall = TP / (TP + FN)                                        │
│   "Of all actual positives, how many did we catch?"           │
│                                                                │
│ F1-Score = 2 × (Precision × Recall) / (Precision + Recall)    │
│   "Harmonic mean of Precision and Recall"                     │
│                                                                │
└────────────────────────────────────────────────────────────────┘
Chapter 8: KNN for Regression {#chapter-8-regression}
8.1 Regression Mechanism
text

┌─────────────────────────────────────────────────────────────────┐
│                 KNN REGRESSION PROCESS                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Instead of VOTING for a class, we AVERAGE the values!        │
│                                                                 │
│   1. Receive new sample to predict                              │
│                                                                 │
│   2. Calculate distance to all training samples                 │
│                                                                 │
│   3. Select K nearest neighbors                                 │
│                                                                 │
│   4. Calculate average (or weighted average) of their          │
│      target values                                              │
│                                                                 │
│   5. Return this average as prediction                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
8.2 Averaging Methods
Simple Average
text

K = 5 neighbors with target values:
[100, 120, 110, 115, 105]

Prediction = (100 + 120 + 110 + 115 + 105) / 5 = 110
Weighted Average
text

K = 5 neighbors:
┌───────────┬──────────┬─────────────┬────────────┐
│ Neighbor  │ Distance │ Target      │ Weight     │
├───────────┼──────────┼─────────────┼────────────┤
│    A      │   2.0    │    100      │  1/2 = 0.5 │
│    B      │   4.0    │    120      │  1/4 = 0.25│
│    C      │   2.5    │    110      │  1/2.5 = 0.4│
│    D      │   3.0    │    115      │  1/3 = 0.33│
│    E      │   2.2    │    105      │  1/2.2=0.45│
└───────────┴──────────┴─────────────┴────────────┘

Total weight = 0.5 + 0.25 + 0.4 + 0.33 + 0.45 = 1.93

Weighted Prediction = 
(100×0.5 + 120×0.25 + 110×0.4 + 115×0.33 + 105×0.45) / 1.93
= (50 + 30 + 44 + 37.95 + 47.25) / 1.93
= 209.2 / 1.93
= 108.4

Notice: Closer neighbors (lower distance) have more influence!
8.3 House Price Prediction Example
text

┌─────────────────────────────────────────────────────────────────┐
│                 HOUSE PRICE PREDICTION                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ TRAINING DATA (normalized features):                            │
│                                                                 │
│ House │ Size(norm) │ Beds(norm) │ Age(norm) │ Price($K)        │
│ ──────┼────────────┼────────────┼───────────┼──────────         │
│   1   │    0.3     │    0.33    │    0.5    │   200             │
│   2   │    0.5     │    0.50    │    0.3    │   280             │
│   3   │    0.7     │    0.67    │    0.2    │   350             │
│   4   │    0.4     │    0.50    │    0.6    │   220             │
│   5   │    0.6     │    0.67    │    0.4    │   310             │
│                                                                 │
│ NEW HOUSE: Size=0.5, Beds=0.50, Age=0.4                        │
│ K = 3                                                           │
│                                                                 │
│ DISTANCES:                                                      │
│ d₁ = √[(0.5-0.3)² + (0.5-0.33)² + (0.4-0.5)²] = 0.262          │
│ d₂ = √[(0.5-0.5)² + (0.5-0.50)² + (0.4-0.3)²] = 0.100 ← Near  │
│ d₃ = √[(0.5-0.7)² + (0.5-0.67)² + (0.4-0.2)²] = 0.318          │
│ d₄ = √[(0.5-0.4)² + (0.5-0.50)² + (0.4-0.6)²] = 0.224          │
│ d₅ = √[(0.5-0.6)² + (0.5-0.67)² + (0.4-0.4)²] = 0.197 ← Near  │
│                                                                 │
│ 3 NEAREST: House 2 (280K), House 5 (310K), House 4 (220K)      │
│                                                                 │
│ SIMPLE AVERAGE:                                                 │
│ Predicted Price = (280 + 310 + 220) / 3 = $270,000             │
│                                                                 │
│ WEIGHTED AVERAGE (1/distance weights):                          │
│ w₂ = 1/0.100 = 10.0                                            │
│ w₅ = 1/0.197 = 5.08                                            │
│ w₄ = 1/0.224 = 4.46                                            │
│ Total = 19.54                                                   │
│                                                                 │
│ Weighted = (280×10 + 310×5.08 + 220×4.46) / 19.54             │
│          = (2800 + 1574.8 + 981.2) / 19.54                     │
│          = $274,105                                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
8.4 Evaluation Metrics for KNN Regression
text

┌─────────────────────────────────────────────────────────────────┐
│              REGRESSION EVALUATION METRICS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 1. MEAN ABSOLUTE ERROR (MAE)                                    │
│                                                                 │
│           Σ|yᵢ - ŷᵢ|                                            │
│    MAE = ─────────────                                          │
│               n                                                 │
│                                                                 │
│    "Average absolute difference between predicted and actual"  │
│    Units: Same as target variable                               │
│    Interpretation: "On average, predictions are off by X"      │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 2. MEAN SQUARED ERROR (MSE)                                     │
│                                                                 │
│           Σ(yᵢ - ŷᵢ)²                                           │
│    MSE = ───────────────                                        │
│               n                                                 │
│                                                                 │
│    "Average squared difference"                                 │
│    Penalizes large errors more than small ones                 │
│    Units: Squared target units                                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 3. ROOT MEAN SQUARED ERROR (RMSE)                               │
│                                                                 │
│    RMSE = √MSE                                                  │
│                                                                 │
│    Units: Same as target (interpretable)                        │
│    Most commonly used metric                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 4. R-SQUARED (R²) - Coefficient of Determination               │
│                                                                 │
│           Σ(yᵢ - ŷᵢ)²                                           │
│    R² = 1 - ─────────────                                       │
│           Σ(yᵢ - ȳ)²                                            │
│                                                                 │
│    Range: 0 to 1 (can be negative for bad models!)             │
│    Interpretation: "Proportion of variance explained"          │
│    R² = 0.85 means model explains 85% of variance              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
8.5 Comparison: Classification vs Regression
text

┌─────────────────────────────────────────────────────────────────┐
│           KNN CLASSIFICATION VS REGRESSION                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Aspect          │  Classification      │  Regression           │
│  ────────────────┼──────────────────────┼─────────────────────  │
│  Output          │  Class label         │  Continuous value     │
│  Method          │  Majority voting     │  Averaging            │
│  Weighted method │  Weighted voting     │  Weighted average     │
│  Probabilities   │  Class proportions   │  Not applicable       │
│  Tie handling    │  Need tie-breaker    │  No ties possible     │
│  Metrics         │  Accuracy, F1, etc.  │  MAE, RMSE, R²        │
│  Example         │  Spam detection      │  House price          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 9: Weighted KNN {#chapter-9-weighted-knn}
9.1 Why Weight Neighbors?
text

┌─────────────────────────────────────────────────────────────────┐
│                    THE PROBLEM WITH EQUAL VOTING                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Consider K=5 neighbors:                                       │
│                                                                 │
│   Neighbor │ Distance │ Class │ Equal Vote                     │
│   ─────────┼──────────┼───────┼────────────                     │
│      A     │   0.1    │  Red  │    1        ← Very close!      │
│      B     │   0.2    │  Red  │    1                            │
│      C     │   5.0    │  Blue │    1        ← Far away         │
│      D     │   5.1    │  Blue │    1        ← Far away         │
│      E     │   5.2    │  Blue │    1        ← Far away         │
│                                                                 │
│   Equal voting: Red=2, Blue=3 → Prediction: BLUE               │
│                                                                 │
│   BUT WAIT! The 2 Red neighbors are MUCH closer!               │
│   They should matter MORE!                                      │
│                                                                 │
│   This is where WEIGHTED KNN helps!                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
9.2 Weighting Schemes
9.2.1 Inverse Distance Weighting
text

┌────────────────────────────────────────────────────────────────┐
│ INVERSE DISTANCE WEIGHTING                                     │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│              1                                                 │
│   weight = ─────                                               │
│            distance                                            │
│                                                                │
│   Closer neighbor → Higher weight                              │
│   Farther neighbor → Lower weight                              │
│                                                                │
│   Example from above:                                          │
│                                                                │
│   Neighbor │ Distance │ Class │ Weight (1/d)                   │
│   ─────────┼──────────┼───────┼─────────────                   │
│      A     │   0.1    │  Red  │  10.0                          │
│      B     │   0.2    │  Red  │   5.0                          │
│      C     │   5.0    │  Blue │   0.2                          │
│      D     │   5.1    │  Blue │   0.196                        │
│      E     │   5.2    │  Blue │   0.192                        │
│                                                                │
│   Weighted votes:                                              │
│   Red:  10.0 + 5.0 = 15.0                                     │
│   Blue: 0.2 + 0.196 + 0.192 = 0.588                           │
│                                                                │
│   NEW Prediction: RED! ✓ (Makes more sense!)                  │
│                                                                │
└────────────────────────────────────────────────────────────────┘
9.2.2 Inverse Squared Distance
text

┌────────────────────────────────────────────────────────────────┐
│ INVERSE SQUARED DISTANCE                                       │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│                1                                               │
│   weight = ─────────                                           │
│            distance²                                           │
│                                                                │
│   Even MORE emphasis on closer neighbors                       │
│                                                                │
│   Example:                                                     │
│                                                                │
│   Neighbor │ Distance │ Weight (1/d²)                          │
│   ─────────┼──────────┼──────────────                          │
│      A     │   0.1    │  100.0        (1/0.01)                 │
│      B     │   0.2    │   25.0        (1/0.04)                 │
│      C     │   5.0    │    0.04       (1/25)                   │
│                                                                │
│   Distance 0.1 vs 0.2: Weight ratio is 4:1 (squared)          │
│   Very close neighbors dominate even more!                     │
│                                                                │
└────────────────────────────────────────────────────────────────┘
9.2.3 Gaussian (RBF) Weighting
text

┌────────────────────────────────────────────────────────────────┐
│ GAUSSIAN / RBF WEIGHTING                                       │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│   weight = exp(-distance² / (2σ²))                             │
│                                                                │
│   σ (sigma) controls the "spread" of influence                │
│                                                                │
│   Properties:                                                  │
│   • Weight = 1 when distance = 0                               │
│   • Weight → 0 as distance → ∞                                │
│   • Smooth decay                                               │
│                                                                │
│   Weight Distribution:                                         │
│                                                                │
│   1.0 │●                                                       │
│       │ ●                                                      │
│   0.8 │  ●                                                     │
│       │   ●                                                    │
│   0.5 │    ●●                                                  │
│       │      ●●                                                │
│   0.2 │        ●●●                                             │
│   0.0 │           ●●●●●●●──────                               │
│       └─────────────────────────                               │
│       0    1    2    3    4    5   distance                   │
│                                                                │
└────────────────────────────────────────────────────────────────┘
9.3 Comparison of Weighting Schemes
text

┌─────────────────────────────────────────────────────────────────┐
│              WEIGHTING SCHEME COMPARISON                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Scheme         │  Formula      │  Pros           │  Cons       │
│  ───────────────┼───────────────┼─────────────────┼────────────│
│  Uniform        │  w = 1        │  Simple         │  Ignores   │
│  (no weight)    │               │                 │  distance  │
│  ───────────────┼───────────────┼─────────────────┼────────────│
│  Inverse        │  w = 1/d      │  Balanced       │  Division  │
│  Distance       │               │  influence      │  by zero   │
│  ───────────────┼───────────────┼─────────────────┼────────────│
│  Inverse        │  w = 1/d²     │  Strong local   │  Too       │
│  Squared        │               │  focus          │  sensitive │
│  ───────────────┼───────────────┼─────────────────┼────────────│
│  Gaussian       │  w = e^(-d²/σ)│  Smooth,        │  Extra     │
│  (RBF)          │               │  tunable        │  parameter │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

HANDLING ZERO DISTANCE:
When distance = 0 (exact match):
• Option 1: Return that neighbor's value directly
• Option 2: Add small epsilon: w = 1/(d + ε)
• Option 3: Set weight to very large number
9.4 Weighted KNN Formulas
For Classification:
text

┌────────────────────────────────────────────────────────────────┐
│                                                                │
│                    Σ wᵢ × I(yᵢ = c)                            │
│   P(class = c) = ─────────────────────                         │
│                        Σ wᵢ                                    │
│                                                                │
│   where:                                                       │
│   • wᵢ = weight of neighbor i                                 │
│   • I(yᵢ = c) = 1 if neighbor i has class c, else 0          │
│   • Sum over all K neighbors                                   │
│                                                                │
│   Predict class with highest P(class = c)                     │
│                                                                │
└────────────────────────────────────────────────────────────────┘
For Regression:
text

┌────────────────────────────────────────────────────────────────┐
│                                                                │
│                  Σ wᵢ × yᵢ                                     │
│   ŷ = ─────────────────────                                    │
│              Σ wᵢ                                              │
│                                                                │
│   where:                                                       │
│   • wᵢ = weight of neighbor i                                 │
│   • yᵢ = target value of neighbor i                           │
│   • Sum over all K neighbors                                   │
│                                                                │
│   This is a weighted average!                                  │
│                                                                │
└────────────────────────────────────────────────────────────────┘
9.5 When to Use Weighted KNN
text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   USE WEIGHTED KNN WHEN:                                        │
│                                                                 │
│   ✓ Data has varying densities in different regions            │
│   ✓ You're using larger K values                                │
│   ✓ Closer neighbors should logically matter more              │
│   ✓ You want smoother decision boundaries                       │
│   ✓ Ties are frequent with uniform weights                      │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   STICK WITH UNIFORM WEIGHTS WHEN:                              │
│                                                                 │
│   ✓ Data is uniformly distributed                               │
│   ✓ Using small K (K ≤ 5)                                       │
│   ✓ Simplicity is important                                     │
│   ✓ All neighbors are roughly equidistant                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 10: Handling Large Datasets {#chapter-10-large-datasets}
10.1 The Scalability Problem
text

┌─────────────────────────────────────────────────────────────────┐
│                    KNN COMPLEXITY ANALYSIS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   TRAINING:                                                     │
│   • Time: O(1) - just stores data                              │
│   • Space: O(n × d) - stores all n samples with d features     │
│                                                                 │
│   PREDICTION (for 1 query):                                     │
│   • Time: O(n × d) - calculates n distances, each costs O(d)  │
│   • Plus: O(n log n) for sorting (or O(n log k) with heap)    │
│                                                                 │
│   PROBLEM:                                                      │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │ Dataset Size │ Features │ Distance Calculations         │   │
│   ├──────────────┼──────────┼────────────────────────────────┤   │
│   │     1,000    │    10    │         10,000                │   │
│   │    10,000    │    10    │        100,000                │   │
│   │   100,000    │    10    │      1,000,000                │   │
│   │ 1,000,000    │   100    │    100,000,000 😱             │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│   For 1 million samples: Prediction is VERY SLOW!              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.2 Solution 1: KD-Tree
text

┌─────────────────────────────────────────────────────────────────┐
│                          KD-TREE                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   K-Dimensional Tree: Organizes points in a binary tree        │
│   by recursively splitting space along different dimensions    │
│                                                                 │
│   CONSTRUCTION:                                                 │
│   1. Pick a dimension (cycle through d dimensions)             │
│   2. Find median along that dimension                          │
│   3. Split: points < median go left, ≥ median go right        │
│   4. Recurse on each half                                       │
│                                                                 │
│   EXAMPLE (2D points):                                          │
│                                                                 │
│   Points: (2,3), (5,4), (9,6), (4,7), (8,1), (7,2)             │
│                                                                 │
│            Split on X                                           │
│                 │                                               │
│         ┌───────┴───────┐                                       │
│         │     (7,2)     │  ← Median X                          │
│         └───────────────┘                                       │
│        /                 \                                      │
│   X < 7                   X ≥ 7                                │
│   ┌─────────┐           ┌─────────┐                            │
│   │  (5,4)  │           │  (9,6)  │  Split on Y                │
│   └─────────┘           └─────────┘                            │
│   /         \           /         \                            │
│ (2,3)      (4,7)     (8,1)        -                           │
│                                                                 │
│   QUERY TIME: O(log n) average case!                           │
│   (vs O(n) for brute force)                                    │
│                                                                 │
│   LIMITATIONS:                                                  │
│   ✗ Performance degrades in high dimensions (d > 20)           │
│   ✗ Tree construction takes O(n log n)                         │
│   ✗ Not efficient for very high-dimensional data               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.3 Solution 2: Ball Tree
text

┌─────────────────────────────────────────────────────────────────┐
│                         BALL TREE                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Organizes points into nested hyperspheres ("balls")          │
│   Better than KD-Tree for higher dimensions                    │
│                                                                 │
│   CONSTRUCTION:                                                 │
│   1. Find centroid of all points                               │
│   2. Find point farthest from centroid → split point          │
│   3. Divide points into two groups based on which "ball"       │
│      center they're closer to                                   │
│   4. Recurse                                                    │
│                                                                 │
│   VISUALIZATION:                                                │
│                                                                 │
│         ┌─────────────────────────────┐                        │
│         │    ○ ○                       │                        │
│         │   ┌──○────┐    ┌────────┐   │                        │
│         │   │ ○  ○  │    │  ●  ●  │   │                        │
│         │   │ ○ ○   │    │ ●  ●   │   │                        │
│         │   └───────┘    │  ●     │   │                        │
│         │                └────────┘   │                        │
│         └─────────────────────────────┘                        │
│                   │                                             │
│         Large ball containing all points                       │
│         Two smaller balls (children)                           │
│                                                                 │
│   QUERY: Can skip entire balls if query point is far from     │
│          ball boundary                                          │
│                                                                 │
│   COMPLEXITY: O(log n) average, O(n) worst case                │
│                                                                 │
│   BETTER FOR:                                                   │
│   ✓ Higher dimensions (works up to ~50-100 dimensions)         │
│   ✓ Non-uniform data distributions                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.4 Solution 3: Approximate Nearest Neighbors (ANN)
text

┌─────────────────────────────────────────────────────────────────┐
│                APPROXIMATE NEAREST NEIGHBORS                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Key Insight: We don't always need EXACT nearest neighbors!   │
│   A "close enough" neighbor found quickly is often better.     │
│                                                                 │
│   Popular Methods:                                              │
│                                                                 │
│   1. LOCALITY SENSITIVE HASHING (LSH)                          │
│      ─────────────────────────────────                          │
│      • Hash similar items to same bucket                        │
│      • Only search within relevant buckets                      │
│      • Very fast for high-dimensional data                      │
│                                                                 │
│   2. HNSW (Hierarchical Navigable Small World)                 │
│      ─────────────────────────────────────────                  │
│      • Graph-based approach                                     │
│      • State-of-the-art for many applications                  │
│      • Used by Facebook, Spotify                               │
│                                                                 │
│   3. ANNOY (Approximate Nearest Neighbors Oh Yeah)             │
│      ─────────────────────────────────────────────              │
│      • Random projection trees                                  │
│      • Memory-mapped (handles huge datasets)                   │
│      • Used by Spotify for recommendations                     │
│                                                                 │
│   TRADE-OFF:                                                    │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                                                         │   │
│   │  Exact KNN        ←─────────────────→    Approximate    │   │
│   │  100% accurate              Fast, ~95-99% accurate      │   │
│   │  Slow                       Much faster                 │   │
│   │                                                         │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.5 Solution 4: Dimensionality Reduction
text

┌─────────────────────────────────────────────────────────────────┐
│               DIMENSIONALITY REDUCTION                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Reduce number of features BEFORE applying KNN                │
│                                                                 │
│   PRINCIPAL COMPONENT ANALYSIS (PCA):                          │
│                                                                 │
│   Original Data          After PCA                             │
│   100 features    →      10 features                           │
│                                                                 │
│   Distance calculation:                                        │
│   Before: O(100) per pair                                      │
│   After:  O(10) per pair = 10× faster!                        │
│                                                                 │
│   ────────────────────────────────────────────────             │
│                                                                 │
│   OTHER METHODS:                                                │
│   • t-SNE: For visualization (2D/3D)                           │
│   • UMAP: Fast, preserves structure                            │
│   • Autoencoders: Neural network-based                         │
│   • Feature Selection: Remove irrelevant features             │
│                                                                 │
│   CAUTION:                                                      │
│   ⚠️ Some information is lost!                                 │
│   ⚠️ Choose components that retain >95% variance               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.6 Comparison of Scalability Solutions
text

┌─────────────────────────────────────────────────────────────────┐
│                  SCALABILITY SOLUTIONS COMPARISON                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Method          │ Query Time │ Best For           │ Limitations │
│ ────────────────┼────────────┼────────────────────┼────────────│
│ Brute Force     │ O(n×d)     │ Small datasets     │ Slow        │
│ KD-Tree         │ O(log n)*  │ Low-dim (d<20)     │ High-dim    │
│ Ball Tree       │ O(log n)*  │ Medium-dim (d<100) │ Construction│
│ LSH             │ O(1)**     │ High-dim, large n  │ Approximate │
│ HNSW            │ O(log n)** │ Very large scale   │ Memory      │
│ Dim. Reduction  │ O(n×d')    │ Very high-dim      │ Info loss   │
│                                                                 │
│ * Average case                                                  │
│ ** Approximate                                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10.7 Decision Guide
text

                         START
                           │
                           ▼
               ┌───────────────────────┐
               │ How many samples (n)? │
               └───────────┬───────────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       n < 10K         10K-1M            n > 1M
          │                │                │
          ▼                ▼                ▼
      Brute Force    Check dimensions    Use ANN
          │                │            (LSH, HNSW)
          │         ┌──────┴──────┐
          │         │             │
          │      d < 20        d > 20
          │         │             │
          │         ▼             ▼
          │     KD-Tree      Ball Tree
          │                   or ANN
          │                      │
          └──────────┬───────────┘
                     │
                     ▼
          ┌───────────────────────┐
          │ Still too slow?       │
          │ → Reduce dimensions   │
          │ → Use approximate ANN │
          │ → Sample training data│
          └───────────────────────┘
Chapter 11: Advanced Optimization Techniques {#chapter-11-optimization}
11.1 Feature Weighting
text

┌─────────────────────────────────────────────────────────────────┐
│                     FEATURE WEIGHTING                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Not all features are equally important!                       │
│                                                                 │
│   STANDARD DISTANCE:                                            │
│   d = √[Σ(pᵢ - qᵢ)²]                                           │
│                                                                 │
│   WEIGHTED DISTANCE:                                            │
│   d = √[Σ wᵢ(pᵢ - qᵢ)²]                                        │
│                                                                 │
│   where wᵢ = importance weight for feature i                   │
│                                                                 │
│   ────────────────────────────────────────────────────────────  │
│                                                                 │
│   HOW TO DETERMINE WEIGHTS:                                     │
│                                                                 │
│   1. CORRELATION-BASED:                                         │
│      wᵢ = |correlation(featureᵢ, target)|                      │
│                                                                 │
│   2. MUTUAL INFORMATION:                                        │
│      wᵢ = MI(featureᵢ, target)                                 │
│                                                                 │
│   3. WRAPPER METHODS:                                           │
│      Use cross-validation to find optimal weights              │
│                                                                 │
│   4. GRADIENT DESCENT:                                          │
│      Learn weights that minimize classification error          │
│                                                                 │
│   EXAMPLE:                                                      │
│   Predicting disease: Age(0.8), Height(0.1), BloodPressure(0.9)│
│   BloodPressure matters most, Height matters least             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
11.2 Adaptive K Selection
text

┌─────────────────────────────────────────────────────────────────┐
│                    ADAPTIVE K SELECTION                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Problem: Fixed K doesn't work well for all regions           │
│                                                                 │
│   Dense region:  Many neighbors close by → Use larger K        │
│   Sparse region: Few neighbors nearby → Use smaller K          │
│                                                                 │
│   VISUALIZATION:                                                │
│                                                                 │
│   Dense Area           Sparse Area                              │
│   ●●●●●●●             ●                                         │
│   ●●●★●●●               ●                                       │
│   ●●●●●●●                  ★      ●                             │
│   ●●●●●●●                           ●                           │
│                                                                 │
│   K=15 works well      K=3 better here                          │
│                                                                 │
│   ────────────────────────────────────────────────────────────  │
│                                                                 │
│   METHODS FOR ADAPTIVE K:                                       │
│                                                                 │
│   1. LOCAL DENSITY ESTIMATION:                                  │
│      K = f(local_density) - larger K in dense areas           │
│                                                                 │
│   2. RADIUS-BASED:                                              │
│      Instead of fixed K, use all neighbors within radius r    │
│                                                                 │
│   3. CROSS-VALIDATION PER REGION:                               │
│      Different optimal K for different data clusters           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
11.3 Edited/Condensed KNN
text

┌─────────────────────────────────────────────────────────────────┐
│              EDITED & CONDENSED NEAREST NEIGHBORS                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Goal: Reduce training set size while maintaining accuracy    │
│                                                                 │
│   EDITED NEAREST NEIGHBOR (ENN):                                │
│   ─────────────────────────────                                 │
│   Remove noisy/misclassified points                            │
│                                                                 │
│   Algorithm:                                                    │
│   FOR each point in training set:                              │
│       IF point is misclassified by its K neighbors:            │
│           REMOVE point                                          │
│                                                                 │
│   Before ENN:              After ENN:                          │
│   ●●●●●○●●●●              ●●●●●●●●●                            │
│        ↑ noise removed         (cleaner boundary)               │
│                                                                 │
│   ────────────────────────────────────────────────────────────  │
│                                                                 │
│   CONDENSED NEAREST NEIGHBOR (CNN):                             │
│   ─────────────────────────────────                             │
│   Keep only "important" points (near decision boundary)        │
│                                                                 │
│   Algorithm:                                                    │
│   1. Start with one point from each class                      │
│   2. FOR each remaining point:                                  │
│          IF it's misclassified by current condensed set:       │
│              ADD to condensed set                              │
│                                                                 │
│   Before CNN:              After CNN:                          │
│   ●●●●●●●●●               ●  ●  ●                              │
│   ○○○○○○○○○                 ○  ○  ○                             │
│   (many points)           (few points, same boundary)          │
│                                                                 │
│   BENEFIT: Much faster prediction with minimal accuracy loss   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
11.4 Prototype Selection Methods
text

┌─────────────────────────────────────────────────────────────────┐
│                   PROTOTYPE SELECTION                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Instead of keeping all points, select representative ones    │
│                                                                 │
│   1. K-MEANS PROTOTYPE:                                         │
│      ─────────────────                                          │
│      Cluster each class separately                             │
│      Keep cluster centroids as prototypes                      │
│                                                                 │
│      Class A points         Class A prototypes                 │
│      ●●●●●●●●●●●●     →     ★    ★    ★                       │
│      (100 points)           (3 centroids)                      │
│                                                                 │
│   2. RANDOM SELECTION:                                          │
│      ────────────────                                           │
│      Randomly sample subset from each class                    │
│      Simple but may miss important regions                     │
│                                                                 │
│   3. BORDER POINT SELECTION:                                    │
│      ─────────────────────                                      │
│      Keep only points near class boundaries                    │
│      These are most informative for classification            │
│                                                                 │
│      ●●●●●●│○○○○○○                                             │
│           ↑                                                     │
│      Keep these (near boundary)                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
11.5 Ensemble KNN Methods
text

┌─────────────────────────────────────────────────────────────────┐
│                      ENSEMBLE KNN                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Combine multiple KNN models for better predictions           │
│                                                                 │
│   1. BAGGING KNN:                                               │
│      ────────────                                               │
│      • Create multiple bootstrap samples                        │
│      • Train separate KNN on each                               │
│      • Average predictions (regression) or vote (classification)│
│                                                                 │
│      Data → [Sample 1] → KNN₁ ─┐                               │
│           → [Sample 2] → KNN₂ ─┼→ Combine → Final Prediction  │
│           → [Sample 3] → KNN₃ ─┘                               │
│                                                                 │
│   2. RANDOM SUBSPACE (Feature Bagging):                        │
│      ──────────────                                             │
│      • Use random subsets of features                          │
│      • Different KNN sees different feature views              │
│      • Reduces curse of dimensionality                         │
│                                                                 │
│   3. DIFFERENT K VALUES:                                        │
│      ────────────────                                           │
│      • Run KNN with K=1, 3, 5, 7, 9                            │
│      • Combine their predictions                               │
│      • More robust than single K                               │
│                                                                 │
│   4. DIFFERENT DISTANCE METRICS:                                │
│      ────────────────────────                                   │
│      • KNN with Euclidean                                       │
│      • KNN with Manhattan                                       │
│      • KNN with Cosine                                          │
│      • Combine predictions                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 12: Real-World Implementation {#chapter-12-implementation}
12.1 Complete Python Implementation from Scratch
Python

"""
KNN IMPLEMENTATION FROM SCRATCH
================================
Educational implementation showing every step
"""

import numpy as np
from collections import Counter

class KNNFromScratch:
    """
    K-Nearest Neighbors classifier and regressor
    Built from scratch for complete understanding
    """
    
    def __init__(self, k=5, distance_metric='euclidean', weights='uniform'):
        """
        Initialize KNN
        
        Parameters:
        -----------
        k : int
            Number of neighbors
        distance_metric : str
            'euclidean', 'manhattan', or 'cosine'
        weights : str
            'uniform' or 'distance'
        """
        self.k = k
        self.distance_metric = distance_metric
        self.weights = weights
        self.X_train = None
        self.y_train = None
    
    def fit(self, X, y):
        """
        Fit the model (just stores the data - lazy learning!)
        
        Parameters:
        -----------
        X : array-like, shape (n_samples, n_features)
            Training data
        y : array-like, shape (n_samples,)
            Target values
        """
        self.X_train = np.array(X)
        self.y_train = np.array(y)
        return self
    
    def _calculate_distance(self, x1, x2):
        """
        Calculate distance between two points
        """
        if self.distance_metric == 'euclidean':
            return np.sqrt(np.sum((x1 - x2) ** 2))
        
        elif self.distance_metric == 'manhattan':
            return np.sum(np.abs(x1 - x2))
        
        elif self.distance_metric == 'cosine':
            dot_product = np.dot(x1, x2)
            norm_x1 = np.sqrt(np.sum(x1 ** 2))
            norm_x2 = np.sqrt(np.sum(x2 ** 2))
            cosine_similarity = dot_product / (norm_x1 * norm_x2)
            return 1 - cosine_similarity  # Convert to distance
        
        else:
            raise ValueError(f"Unknown metric: {self.distance_metric}")
    
    def _get_neighbors(self, x):
        """
        Find K nearest neighbors for a single point
        
        Returns:
        --------
        neighbors : list of tuples (distance, index, label)
        """
        distances = []
        
        # Calculate distance to every training point
        for i, x_train in enumerate(self.X_train):
            dist = self._calculate_distance(x, x_train)
            distances.append((dist, i, self.y_train[i]))
        
        # Sort by distance and get K nearest
        distances.sort(key=lambda x: x[0])
        k_nearest = distances[:self.k]
        
        return k_nearest
    
    def _calculate_weights(self, neighbors):
        """
        Calculate weights for neighbors
        """
        if self.weights == 'uniform':
            return [1.0] * len(neighbors)
        
        elif self.weights == 'distance':
            weights = []
            for dist, _, _ in neighbors:
                if dist == 0:
                    weights.append(1e10)  # Very large weight
                else:
                    weights.append(1.0 / dist)
            return weights
        
        else:
            raise ValueError(f"Unknown weights: {self.weights}")
    
    def predict_single(self, x, task='classification'):
        """
        Predict for a single sample
        """
        neighbors = self._get_neighbors(x)
        weights = self._calculate_weights(neighbors)
        
        if task == 'classification':
            # Weighted voting
            class_votes = {}
            for weight, (_, _, label) in zip(weights, neighbors):
                if label not in class_votes:
                    class_votes[label] = 0
                class_votes[label] += weight
            
            # Return class with highest weighted votes
            return max(class_votes, key=class_votes.get)
        
        else:  # regression
            # Weighted average
            weighted_sum = sum(w * label for w, (_, _, label) 
                              in zip(weights, neighbors))
            weight_total = sum(weights)
            return weighted_sum / weight_total
    
    def predict(self, X, task='classification'):
        """
        Predict for multiple samples
        """
        X = np.array(X)
        predictions = [self.predict_single(x, task) for x in X]
        return np.array(predictions)
    
    def predict_proba(self, X):
        """
        Predict class probabilities (classification only)
        """
        X = np.array(X)
        probabilities = []
        
        for x in X:
            neighbors = self._get_neighbors(x)
            weights = self._calculate_weights(neighbors)
            
            # Count weighted votes per class
            class_votes = {}
            total_weight = sum(weights)
            
            for weight, (_, _, label) in zip(weights, neighbors):
                if label not in class_votes:
                    class_votes[label] = 0
                class_votes[label] += weight
            
            # Convert to probabilities
            probs = {label: votes/total_weight 
                    for label, votes in class_votes.items()}
            probabilities.append(probs)
        
        return probabilities
    
    def score(self, X, y, task='classification'):
        """
        Calculate accuracy (classification) or R² (regression)
        """
        predictions = self.predict(X, task)
        y = np.array(y)
        
        if task == 'classification':
            return np.mean(predictions == y)
        else:
            # R² score
            ss_res = np.sum((y - predictions) ** 2)
            ss_tot = np.sum((y - np.mean(y)) ** 2)
            return 1 - (ss_res / ss_tot)


# =============================================================================
# USAGE EXAMPLE
# =============================================================================

if __name__ == "__main__":
    # Sample data
    X_train = [
        [1, 2], [1.5, 1.8], [5, 8], [8, 8],
        [1, 0.6], [9, 11], [8, 2], [10, 2], [9, 3]
    ]
    y_train = [0, 0, 1, 1, 0, 1, 2, 2, 2]  # 3 classes
    
    # Create and train model
    knn = KNNFromScratch(k=3, distance_metric='euclidean', weights='distance')
    knn.fit(X_train, y_train)
    
    # Predict
    X_test = [[1, 1], [8, 9], [9, 2]]
    predictions = knn.predict(X_test)
    
    print("Predictions:", predictions)
    # Output: [0, 1, 2]
12.2 Using Scikit-Learn
Python

"""
KNN WITH SCIKIT-LEARN
======================
Professional implementation for production use
"""

from sklearn.neighbors import KNeighborsClassifier, KNeighborsRegressor
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV
from sklearn.metrics import classification_report, confusion_matrix
from sklearn.pipeline import Pipeline
import numpy as np

# =============================================================================
# CLASSIFICATION EXAMPLE
# =============================================================================

def knn_classification_example():
    """
    Complete KNN classification workflow
    """
    # 1. Load/Create data
    from sklearn.datasets import load_iris
    iris = load_iris()
    X, y = iris.data, iris.target
    
    # 2. Split data
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y
    )
    
    # 3. Create pipeline (scaling + KNN)
    pipeline = Pipeline([
        ('scaler', StandardScaler()),
        ('knn', KNeighborsClassifier())
    ])
    
    # 4. Hyperparameter tuning
    param_grid = {
        'knn__n_neighbors': [3, 5, 7, 9, 11],
        'knn__weights': ['uniform', 'distance'],
        'knn__metric': ['euclidean', 'manhattan']
    }
    
    grid_search = GridSearchCV(
        pipeline, 
        param_grid, 
        cv=5, 
        scoring='accuracy',
        n_jobs=-1
    )
    
    grid_search.fit(X_train, y_train)
    
    # 5. Best parameters
    print("Best Parameters:", grid_search.best_params_)
    print("Best CV Score:", grid_search.best_score_)
    
    # 6. Evaluate on test set
    best_model = grid_search.best_estimator_
    y_pred = best_model.predict(X_test)
    
    print("\nClassification Report:")
    print(classification_report(y_test, y_pred, 
                               target_names=iris.target_names))
    
    print("Confusion Matrix:")
    print(confusion_matrix(y_test, y_pred))
    
    return best_model

# =============================================================================
# REGRESSION EXAMPLE
# =============================================================================

def knn_regression_example():
    """
    Complete KNN regression workflow
    """
    from sklearn.datasets import fetch_california_housing
    from sklearn.metrics import mean_squared_error, r2_score
    
    # 1. Load data
    housing = fetch_california_housing()
    X, y = housing.data, housing.target
    
    # 2. Split data
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42
    )
    
    # 3. Create pipeline
    pipeline = Pipeline([
        ('scaler', StandardScaler()),
        ('knn', KNeighborsRegressor(n_neighbors=5, weights='distance'))
    ])
    
    # 4. Fit and predict
    pipeline.fit(X_train, y_train)
    y_pred = pipeline.predict(X_test)
    
    # 5. Evaluate
    mse = mean_squared_error(y_test, y_pred)
    rmse = np.sqrt(mse)
    r2 = r2_score(y_test, y_pred)
    
    print(f"RMSE: {rmse:.4f}")
    print(f"R² Score: {r2:.4f}")
    
    return pipeline

# =============================================================================
# FINDING OPTIMAL K
# =============================================================================

def find_optimal_k(X, y, k_range=range(1, 31)):
    """
    Find optimal K using cross-validation
    """
    from sklearn.model_selection import cross_val_score
    import matplotlib.pyplot as plt
    
    # Scale data
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)
    
    # Test different K values
    cv_scores = []
    for k in k_range:
        knn = KNeighborsClassifier(n_neighbors=k)
        scores = cross_val_score(knn, X_scaled, y, cv=5, scoring='accuracy')
        cv_scores.append(scores.mean())
    
    # Find best K
    best_k = k_range[np.argmax(cv_scores)]
    best_score = max(cv_scores)
    
    print(f"Best K: {best_k}")
    print(f"Best CV Accuracy: {best_score:.4f}")
    
    # Plot
    plt.figure(figsize=(10, 6))
    plt.plot(k_range, cv_scores, 'bo-')
    plt.axvline(x=best_k, color='r', linestyle='--', label=f'Best K={best_k}')
    plt.xlabel('K')
    plt.ylabel('Cross-Validation Accuracy')
    plt.title('Finding Optimal K')
    plt.legend()
    plt.grid(True)
    plt.show()
    
    return best_k

# Run examples
if __name__ == "__main__":
    print("="*50)
    print("KNN CLASSIFICATION")
    print("="*50)
    knn_classification_example()
    
    print("\n" + "="*50)
    print("KNN REGRESSION")
    print("="*50)
    knn_regression_example()
12.3 Complete ML Pipeline with KNN
Python

"""
PRODUCTION-READY KNN PIPELINE
==============================
Complete workflow for real-world applications
"""

import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, LabelEncoder, OneHotEncoder
from sklearn.impute import SimpleImputer, KNNImputer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import classification_report
import joblib

class KNNPipeline:
    """
    Complete KNN pipeline with all preprocessing steps
    """
    
    def __init__(self, n_neighbors=5, weights='distance'):
        self.n_neighbors = n_neighbors
        self.weights = weights
        self.pipeline = None
        self.label_encoder = None
        
    def create_pipeline(self, numeric_features, categorical_features):
        """
        Create preprocessing + KNN pipeline
        """
        # Numeric preprocessing
        numeric_transformer = Pipeline(steps=[
            ('imputer', SimpleImputer(strategy='median')),
            ('scaler', StandardScaler())
        ])
        
        # Categorical preprocessing
        categorical_transformer = Pipeline(steps=[
            ('imputer', SimpleImputer(strategy='most_frequent')),
            ('onehot', OneHotEncoder(handle_unknown='ignore', sparse=False))
        ])
        
        # Combine preprocessors
        preprocessor = ColumnTransformer(
            transformers=[
                ('num', numeric_transformer, numeric_features),
                ('cat', categorical_transformer, categorical_features)
            ])
        
        # Full pipeline
        self.pipeline = Pipeline(steps=[
            ('preprocessor', preprocessor),
            ('knn', KNeighborsClassifier(
                n_neighbors=self.n_neighbors,
                weights=self.weights,
                n_jobs=-1
            ))
        ])
        
        return self.pipeline
    
    def fit(self, X, y):
        """
        Fit the pipeline
        """
        self.pipeline.fit(X, y)
        return self
    
    def predict(self, X):
        """
        Make predictions
        """
        return self.pipeline.predict(X)
    
    def predict_proba(self, X):
        """
        Predict probabilities
        """
        return self.pipeline.predict_proba(X)
    
    def evaluate(self, X, y):
        """
        Evaluate with cross-validation
        """
        scores = cross_val_score(self.pipeline, X, y, cv=5, scoring='accuracy')
        print(f"CV Accuracy: {scores.mean():.4f} (+/- {scores.std()*2:.4f})")
        return scores
    
    def save(self, filepath):
        """
        Save pipeline to file
        """
        joblib.dump(self.pipeline, filepath)
        print(f"Pipeline saved to {filepath}")
    
    def load(self, filepath):
        """
        Load pipeline from file
        """
        self.pipeline = joblib.load(filepath)
        print(f"Pipeline loaded from {filepath}")
        return self


# =============================================================================
# EXAMPLE USAGE WITH REAL DATA
# =============================================================================

def real_world_example():
    """
    Example with the Titanic-like dataset structure
    """
    # Create sample data (mimicking real-world messiness)
    np.random.seed(42)
    n_samples = 1000
    
    data = {
        'age': np.random.randint(1, 80, n_samples).astype(float),
        'income': np.random.randint(20000, 200000, n_samples).astype(float),
        'credit_score': np.random.randint(300, 850, n_samples).astype(float),
        'gender': np.random.choice(['M', 'F'], n_samples),
        'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n_samples),
        'employed': np.random.choice(['Yes', 'No'], n_samples),
        'approved': np.random.choice([0, 1], n_samples)  # Target
    }
    
    df = pd.DataFrame(data)
    
    # Add some missing values (realistic!)
    df.loc[np.random.choice(df.index, 50), 'age'] = np.nan
    df.loc[np.random.choice(df.index, 30), 'income'] = np.nan
    
    print("Dataset shape:", df.shape)
    print("\nMissing values:\n", df.isnull().sum())
    print("\nFirst few rows:\n", df.head())
    
    # Define features
    numeric_features = ['age', 'income', 'credit_score']
    categorical_features = ['gender', 'education', 'employed']
    
    X = df.drop('approved', axis=1)
    y = df['approved']
    
    # Split
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42
    )
    
    # Create and train pipeline
    knn_pipe = KNNPipeline(n_neighbors=7, weights='distance')
    knn_pipe.create_pipeline(numeric_features, categorical_features)
    
    # Evaluate with cross-validation
    print("\nCross-Validation Results:")
    knn_pipe.evaluate(X_train, y_train)
    
    # Fit on training data
    knn_pipe.fit(X_train, y_train)
    
    # Predict on test set
    y_pred = knn_pipe.predict(X_test)
    
    print("\nTest Set Classification Report:")
    print(classification_report(y_test, y_pred))
    
    # Save the model
    knn_pipe.save('knn_model.joblib')
    
    return knn_pipe

# Run the example
if __name__ == "__main__":
    real_world_example()
Chapter 13: Common Pitfalls and Solutions {#chapter-13-pitfalls}
13.1 Pitfall Checklist
text

┌─────────────────────────────────────────────────────────────────┐
│                   KNN PITFALL CHECKLIST                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  □ Feature Scaling                                              │
│    ✗ Problem: Features with larger ranges dominate distance   │
│    ✓ Solution: Always scale (StandardScaler or MinMaxScaler)  │
│                                                                 │
│  □ Curse of Dimensionality                                      │
│    ✗ Problem: KNN breaks in high dimensions                    │
│    ✓ Solution: Reduce dimensions (PCA) or use ANN             │
│                                                                 │
│  □ Imbalanced Classes                                           │
│    ✗ Problem: Majority class dominates predictions            │
│    ✓ Solution: Weighted KNN, oversampling, or adjust K        │
│                                                                 │
│  □ Noisy Data                                                   │
│    ✗ Problem: Outliers affect nearest neighbors               │
│    ✓ Solution: Larger K, data cleaning, or weighted KNN       │
│                                                                 │
│  □ Missing Values                                               │
│    ✗ Problem: Can't compute distance with missing values      │
│    ✓ Solution: Impute before KNN (KNN imputation!)            │
│                                                                 │
│  □ Categorical Features                                         │
│    ✗ Problem: Distance undefined for categories               │
│    ✓ Solution: One-hot encode or use appropriate distance     │
│                                                                 │
│  □ Wrong K Value                                                │
│    ✗ Problem: Underfitting or overfitting                      │
│    ✓ Solution: Cross-validation to find optimal K             │
│                                                                 │
│  □ Computational Cost                                           │
│    ✗ Problem: Slow predictions on large datasets              │
│    ✓ Solution: KD-Tree, Ball Tree, or ANN libraries           │
│                                                                 │
│  □ Data Leakage                                                 │
│    ✗ Problem: Scaling on full data before split               │
│    ✓ Solution: Fit scaler ONLY on training data               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
13.2 Handling Imbalanced Data
text

┌─────────────────────────────────────────────────────────────────┐
│               IMBALANCED DATA SOLUTIONS                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   THE PROBLEM:                                                  │
│   Class A: 950 samples (95%)                                   │
│   Class B: 50 samples (5%)                                     │
│                                                                 │
│   KNN with K=5: Most neighbors will be Class A!               │
│   Model predicts A for everything → 95% accuracy but useless! │
│                                                                 │
│   ────────────────────────────────────────────────────────────  │
│                                                                 │
│   SOLUTION 1: Weighted KNN                                      │
│   • Give minority class higher weight in voting               │
│                                                                 │
│   SOLUTION 2: Adjust K                                          │
│   • Use smaller K to capture local patterns                   │
│   • Be careful not to overfit                                  │
│                                                                 │
│   SOLUTION 3: Resampling                                        │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │ Oversampling: Duplicate minority class samples          │   │
│   │   - Random oversampling                                 │   │
│   │   - SMOTE (Synthetic Minority Oversampling Technique)   │   │
│   │                                                         │   │
│   │ Undersampling: Remove majority class samples            │   │
│   │   - Random undersampling                                │   │
│   │   - Tomek links (remove borderline majority)            │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│   SOLUTION 4: Cost-Sensitive Learning                           │
│   • Penalize misclassification of minority class more         │
│                                                                 │
│   SOLUTION 5: Use Different Metrics                             │
│   • Don't use accuracy!                                        │
│   • Use: F1-score, Precision, Recall, AUC-ROC                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
13.3 When NOT to Use KNN
text

┌─────────────────────────────────────────────────────────────────┐
│                  WHEN KNN IS NOT IDEAL                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ❌ AVOID KNN WHEN:                                            │
│                                                                 │
│   1. Very High Dimensional Data (d > 50-100)                   │
│      → Use: Random Forest, XGBoost, or Neural Networks         │
│                                                                 │
│   2. Very Large Dataset (n > 1 million)                        │
│      → Use: Approximate methods or simpler models              │
│                                                                 │
│   3. Need for Fast Predictions                                  │
│      → Use: Pre-trained models (Decision Tree, Linear)         │
│                                                                 │
│   4. Limited Memory                                             │
│      → Use: Models that don't store training data              │
│                                                                 │
│   5. Need for Feature Importance                                │
│      → Use: Tree-based models                                  │
│                                                                 │
│   6. Non-Metric Data (complex relationships)                   │
│      → Use: Deep Learning                                      │
│                                                                 │
│   ────────────────────────────────────────────────────────────  │
│                                                                 │
│   ✅ KNN SHINES WHEN:                                           │
│                                                                 │
│   • Dataset is small to medium (< 100K samples)                │
│   • Low to medium dimensions (< 50)                            │
│   • Need interpretable predictions                              │
│   • Quick baseline needed                                       │
│   • Data has clear local patterns                              │
│   • Boundaries between classes are irregular                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 14: Interview Questions & Answers {#chapter-14-interview}
14.1 Basic Level Questions
text

┌─────────────────────────────────────────────────────────────────┐
│ Q1: What is KNN? Explain in simple terms.                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│ KNN is a simple machine learning algorithm that classifies     │
│ or predicts based on similarity. For a new data point, it:     │
│                                                                 │
│ 1. Finds K most similar points from training data             │
│ 2. For classification: Takes majority vote of their classes   │
│ 3. For regression: Takes average of their values              │
│                                                                 │
│ Example: "To predict if you'll like a movie, look at what     │
│ people similar to you thought about it."                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q2: Why is KNN called a "lazy learner"?                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│ KNN is called "lazy" because:                                  │
│                                                                 │
│ • During training: It does NOTHING except store data          │
│ • During prediction: It does ALL the work                     │
│                                                                 │
│ Unlike eager learners (Decision Trees, Neural Networks) that  │
│ build a model during training, KNN delays all computation     │
│ until prediction time.                                         │
│                                                                 │
│ Also called: Instance-based learning, Memory-based learning   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q3: How do you choose the value of K?                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ 1. Use Cross-Validation:                                       │
│    Try different K values, measure performance, pick best     │
│                                                                 │
│ 2. Heuristics:                                                  │
│    • Start with K = √n (square root of samples)               │
│    • Use odd K for binary classification (avoid ties)         │
│                                                                 │
│ 3. Considerations:                                              │
│    • Small K (1-3): More sensitive to noise, complex boundary │
│    • Large K (>20): Smoother boundary, may miss patterns      │
│    • Very large K: Essentially predicts majority class        │
│                                                                 │
│ 4. Common range: K = 3 to 11 for most problems                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q4: Why is feature scaling important for KNN?                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ KNN uses DISTANCE to find neighbors. Without scaling:          │
│                                                                 │
│ Feature 1: Age (0-100)                                         │
│ Feature 2: Income (0-1,000,000)                                │
│                                                                 │
│ Income will DOMINATE distance calculations!                    │
│ Age becomes almost irrelevant.                                 │
│                                                                 │
│ Example:                                                        │
│ Person A: Age=25, Income=50,000                                │
│ Person B: Age=60, Income=50,001                                │
│                                                                 │
│ Distance dominated by income difference (1),                   │
│ ignoring age difference (35)!                                  │
│                                                                 │
│ Solution: Scale all features to same range (0-1 or z-score)   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
14.2 Intermediate Level Questions
text

┌─────────────────────────────────────────────────────────────────┐
│ Q5: What is the curse of dimensionality? How does it affect   │
│     KNN?                                                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ As dimensions increase:                                         │
│                                                                 │
│ 1. Data becomes SPARSE                                          │
│    • Points spread out in high-dimensional space              │
│    • Need exponentially more data to cover space              │
│                                                                 │
│ 2. Distances become MEANINGLESS                                │
│    • All points become roughly equidistant                    │
│    • "Nearest" neighbor isn't much nearer than "farthest"     │
│                                                                 │
│ 3. Impact on KNN:                                               │
│    • Cannot distinguish between neighbors                      │
│    • Distance-based decisions become unreliable               │
│    • Performance degrades significantly                        │
│                                                                 │
│ Solutions:                                                      │
│ • Dimensionality reduction (PCA, UMAP)                         │
│ • Feature selection                                            │
│ • Use Manhattan distance (more robust in high-D)              │
│ • Use approximate nearest neighbors                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q6: Compare Euclidean and Manhattan distance. When to use each?│
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ EUCLIDEAN (L2):                                                 │
│ • Formula: √Σ(xᵢ - yᵢ)²                                        │
│ • Straight-line distance                                       │
│ • More sensitive to outliers (squares differences)            │
│ • Better for: Low dimensions, continuous spatial data         │
│                                                                 │
│ MANHATTAN (L1):                                                 │
│ • Formula: Σ|xᵢ - yᵢ|                                          │
│ • Grid-based distance (city blocks)                            │
│ • Less sensitive to outliers (no squaring)                    │
│ • Better for: High dimensions, sparse data, when outliers     │
│   present                                                       │
│                                                                 │
│ Key insight:                                                    │
│ In high dimensions, Manhattan is more robust because the      │
│ ratio of distances doesn't degrade as quickly.                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q7: How do you handle categorical features in KNN?             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ KNN requires numerical distance. Options for categorical data:│
│                                                                 │
│ 1. ONE-HOT ENCODING:                                            │
│    Color: [Red, Blue] → Color_Red: [1,0], Color_Blue: [0,1]   │
│    ✓ Works well for nominal categories                        │
│    ✗ High dimensionality with many categories                 │
│                                                                 │
│ 2. LABEL ENCODING:                                              │
│    Small=0, Medium=1, Large=2                                  │
│    ✓ Only for ORDINAL categories                              │
│    ✗ Implies numerical relationship                           │
│                                                                 │
│ 3. TARGET ENCODING:                                             │
│    Replace category with mean target value                    │
│    ✓ Reduces dimensions                                        │
│    ✗ Risk of data leakage                                      │
│                                                                 │
│ 4. HAMMING DISTANCE:                                            │
│    Use Hamming distance for categorical features              │
│    ✓ No need to convert                                        │
│    ✗ Treats all categories equally different                  │
│                                                                 │
│ 5. GOWER DISTANCE:                                              │
│    Mixed distance for mixed data types                        │
│    ✓ Handles mixed data elegantly                              │
│    ✗ More complex to implement                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
14.3 Advanced Level Questions
text

┌─────────────────────────────────────────────────────────────────┐
│ Q8: Explain the time and space complexity of KNN.              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ BRUTE FORCE KNN:                                                │
│ ┌───────────────────────────────────────────────────────────┐   │
│ │ Training:                                                  │   │
│ │   Time: O(1) - just stores data                           │   │
│ │   Space: O(n × d) - n samples, d features                 │   │
│ │                                                            │   │
│ │ Prediction (per query):                                    │   │
│ │   Time: O(n × d) - calculate n distances                  │   │
│ │        + O(n log n) - sort distances                      │   │
│ │        = O(n × d + n log n)                               │   │
│ │   Space: O(n) - store distances                           │   │
│ └───────────────────────────────────────────────────────────┘   │
│                                                                 │
│ WITH KD-TREE (d < 20):                                          │
│ ┌───────────────────────────────────────────────────────────┐   │
│ │ Construction: O(n log n)                                   │   │
│ │ Query: O(log n) average, O(n) worst case                  │   │
│ │ Space: O(n)                                               │   │
│ └───────────────────────────────────────────────────────────┘   │
│                                                                 │
│ WITH BALL TREE (d < 100):                                       │
│ ┌───────────────────────────────────────────────────────────┐   │
│ │ Construction: O(n log n)                                   │   │
│ │ Query: O(log n) average                                   │   │
│ │ Space: O(n)                                               │   │
│ └───────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q9: How does KNN handle imbalanced datasets? What are the      │
│     solutions?                                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ PROBLEM:                                                        │
│ With 95% Class A, 5% Class B, most neighbors will be A.       │
│ KNN will almost always predict A.                              │
│                                                                 │
│ SOLUTIONS:                                                      │
│                                                                 │
│ 1. WEIGHTED KNN:                                                │
│    Weight votes by inverse class frequency                    │
│    Minority class gets higher vote weight                     │
│                                                                 │
│ 2. RESAMPLING:                                                  │
│    • Oversample minority (SMOTE)                              │
│    • Undersample majority (random, Tomek links)               │
│                                                                 │
│ 3. ADJUST K:                                                    │
│    Use smaller K to focus on local structure                  │
│                                                                 │
│ 4. THRESHOLD ADJUSTMENT:                                        │
│    Instead of majority vote, use probability threshold        │
│    Adjust threshold to favor minority class                   │
│                                                                 │
│ 5. USE APPROPRIATE METRICS:                                     │
│    F1-score, AUC-ROC instead of accuracy                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ Q10: Compare KNN with other algorithms. When would you choose  │
│      KNN over others?                                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER:                                                         │
│                                                                 │
│ KNN vs DECISION TREE:                                           │
│ • KNN: Non-parametric, no assumptions, slow prediction         │
│ • DT: Fast prediction, interpretable, handles irrelevant feat │
│ → Choose KNN: When boundaries are non-linear, complex         │
│ → Choose DT: When you need speed and interpretability         │
│                                                                 │
│ KNN vs LOGISTIC REGRESSION:                                     │
│ • KNN: No assumptions, captures non-linear                    │
│ • LR: Fast, works with high dimensions, linear boundary       │
│ → Choose KNN: Non-linear relationships                        │
│ → Choose LR: High dimensions, need probability calibration    │
│                                                                 │
│ KNN vs SVM:                                                     │
│ • KNN: Simple, local method                                   │
│ • SVM: Global optimization, handles high-dim better           │
│ → Choose KNN: Simple problems, interpretability needed        │
│ → Choose SVM: High dimensions, complex margins                │
│                                                                 │
│ KNN vs NEURAL NETWORKS:                                         │
│ • KNN: No training, interpretable, limited scalability        │
│ • NN: Learns features, scales well, black box                 │
│ → Choose KNN: Small data, quick baseline                      │
│ → Choose NN: Large data, complex patterns                     │
│                                                                 │
│ CHOOSE KNN WHEN:                                                │
│ ✓ Dataset is small to medium                                   │
│ ✓ Need quick baseline                                          │
│ ✓ Decision boundaries are irregular                            │
│ ✓ Interpretability matters                                     │
│ ✓ Low-dimensional data                                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
14.4 Rapid Fire Questions
text

┌─────────────────────────────────────────────────────────────────┐
│                     RAPID FIRE Q&A                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Q: Is KNN parametric or non-parametric?                        │
│ A: Non-parametric (no fixed parameters/assumptions)            │
│                                                                 │
│ Q: What's the training time of KNN?                            │
│ A: O(1) - It just stores the data!                             │
│                                                                 │
│ Q: What's the prediction time of KNN?                          │
│ A: O(n × d) for brute force (n samples, d features)           │
│                                                                 │
│ Q: Can KNN handle multi-class classification?                  │
│ A: Yes! Naturally handles any number of classes                │
│                                                                 │
│ Q: Does KNN need feature scaling?                              │
│ A: YES! Absolutely critical for KNN                            │
│                                                                 │
│ Q: What happens when K = n (all samples)?                      │
│ A: Always predicts majority class (useless model)             │
│                                                                 │
│ Q: What happens when K = 1?                                    │
│ A: Maximum flexibility, but sensitive to noise                 │
│                                                                 │
│ Q: Which K is better for noisy data?                           │
│ A: Larger K (smooths out noise)                                │
│                                                                 │
│ Q: Can KNN be used for regression?                             │
│ A: Yes! Average values instead of voting                       │
│                                                                 │
│ Q: What distance metric for text data?                         │
│ A: Cosine similarity/distance                                  │
│                                                                 │
│ Q: What distance metric for binary data?                       │
│ A: Hamming distance                                            │
│                                                                 │
│ Q: How to handle ties in KNN classification?                   │
│ A: Use odd K, weighted voting, or reduce K                     │
│                                                                 │
│ Q: Does KNN work with missing values?                          │
│ A: No! Must impute before using KNN                            │
│                                                                 │
│ Q: What's the main disadvantage of KNN?                        │
│ A: Slow prediction time for large datasets                     │
│                                                                 │
│ Q: What makes KNN different from K-Means?                      │
│ A: KNN = supervised (uses labels)                              │
│    K-Means = unsupervised (no labels)                          │
│                                                                 │
│ Q: Can KNN give probability estimates?                         │
│ A: Yes! Proportion of each class among K neighbors             │
│                                                                 │
│ Q: What's the bias-variance tradeoff in KNN?                   │
│ A: Small K = Low bias, High variance (overfitting)             │
│    Large K = High bias, Low variance (underfitting)            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
14.5 Scenario-Based Questions
text

┌─────────────────────────────────────────────────────────────────┐
│ SCENARIO 1: You trained a KNN model but it's very slow during  │
│ prediction. What would you do?                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ANSWER (Step by step approach):                                 │
│                                                                 │
│ 1. CHECK DATA SIZE:                                             │
│    • If n > 10,000, brute force is too slow                    │
│                                                                 │
│ 2. USE TREE-BASED STRUCTURES:                                   │
│    • KD-Tree for d < 20 dimensions                             │
│    • Ball Tree for d < 100 dimensions                          │
│    • In sklearn: algorithm='kd_tree' or 'ball_tree'           │
│                                                                 │
│ 3. REDUCE DIMENSIONS:                                           │
│    • Apply PCA before KNN                                       │
│    • Faster distance calculations                              │
│                                                                 │
│ 4. USE APPROXIMATE METHODS:                                     │
│    • Libraries: FAISS, Annoy, HNSW                              │
│    • Trade small accuracy for huge speed gain                  │
│                                                                 │
│ 5. REDUCE TRAINING SET:                                         │
│    • Condensed Nearest Neighbor                                 │
│    • Prototype selection                                        │
│                                                                 │
│ 6. SAMPLE TRAINING DATA:                                        │
│    • If data is redundant, use stratified sample               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ SCENARIO 2: Your KNN model has 95% accuracy on training data   │
│ but only 60% on test data. What's happening and how to fix it? │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ DIAGNOSIS: This is OVERFITTING!                                 │
│                                                                 │
│ CAUSES:                                                         │
│ • K is too small (probably K=1 or K=3)                         │
│ • Model memorizing training data, not generalizing            │
│                                                                 │
│ SOLUTIONS:                                                      │
│                                                                 │
│ 1. INCREASE K:                                                  │
│    • Try K = 5, 7, 9, 11...                                    │
│    • Use cross-validation to find optimal K                    │
│                                                                 │
│ 2. CHECK FOR DATA LEAKAGE:                                      │
│    • Was scaling done before or after split?                   │
│    • Must fit scaler ONLY on training data                     │
│                                                                 │
│ 3. ADD REGULARIZATION:                                          │
│    • Use weighted KNN (distance weighting)                     │
│    • Reduces impact of outliers                                │
│                                                                 │
│ 4. FEATURE SELECTION:                                           │
│    • Remove irrelevant features                                 │
│    • Reduces noise                                              │
│                                                                 │
│ 5. CROSS-VALIDATION:                                            │
│    • Use k-fold CV to get reliable estimate                    │
│    • Helps detect overfitting early                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ SCENARIO 3: You have a dataset with 1000 features and 500      │
│ samples. Will KNN work well? What would you do?                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ DIAGNOSIS: This is the CURSE OF DIMENSIONALITY!                │
│                                                                 │
│ PROBLEM:                                                        │
│ • 1000 features >> 500 samples                                 │
│ • Data is extremely sparse in high dimensions                  │
│ • All points become roughly equidistant                        │
│ • KNN will perform poorly                                       │
│                                                                 │
│ SOLUTIONS:                                                      │
│                                                                 │
│ 1. DIMENSIONALITY REDUCTION:                                    │
│    • PCA: Reduce to 50-100 components                          │
│    • Keep components explaining 95% variance                   │
│                                                                 │
│ 2. FEATURE SELECTION:                                           │
│    • Remove irrelevant/redundant features                      │
│    • Use correlation analysis, mutual information              │
│    • Select top 50-100 most important features                 │
│                                                                 │
│ 3. USE MANHATTAN DISTANCE:                                      │
│    • More robust in high dimensions                             │
│                                                                 │
│ 4. CONSIDER DIFFERENT ALGORITHM:                                │
│    • Random Forest handles high dimensions better              │
│    • SVM with RBF kernel                                       │
│    • Regularized linear models (Lasso)                         │
│                                                                 │
│ 5. COLLECT MORE DATA:                                           │
│    • If possible, increase sample size                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ SCENARIO 4: Your dataset has 99% Class A and 1% Class B.       │
│ How would you approach this with KNN?                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ PROBLEM: Severe class imbalance                                 │
│ KNN will almost always predict Class A (99% accuracy but       │
│ missing all Class B!)                                           │
│                                                                 │
│ SOLUTIONS:                                                      │
│                                                                 │
│ 1. RESAMPLE DATA:                                               │
│    • SMOTE: Generate synthetic minority samples                │
│    • Random undersampling of majority class                    │
│    • Aim for more balanced distribution                        │
│                                                                 │
│ 2. WEIGHTED KNN:                                                │
│    • Weight Class B votes 99x higher than Class A              │
│    • Or weight inversely proportional to class frequency       │
│                                                                 │
│ 3. ADJUST DECISION THRESHOLD:                                   │
│    • Don't use 50% threshold for class decision               │
│    • Use lower threshold for minority class                    │
│                                                                 │
│ 4. USE SMALLER K:                                               │
│    • Smaller K captures local patterns                         │
│    • May find minority class clusters                          │
│                                                                 │
│ 5. CHANGE EVALUATION METRIC:                                    │
│    • DON'T use accuracy!                                       │
│    • Use: Precision, Recall, F1-score, AUC-ROC                 │
│    • Focus on detecting Class B (minority)                     │
│                                                                 │
│ 6. COST-SENSITIVE LEARNING:                                     │
│    • Penalize misclassification of B more than A               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Chapter 15: Projects and Case Studies {#chapter-15-projects}
15.1 Project 1: Iris Flower Classification (Beginner)
Python

"""
PROJECT 1: IRIS FLOWER CLASSIFICATION
======================================
Difficulty: Beginner
Dataset: Iris (built-in sklearn)
Goal: Classify iris flowers into 3 species
"""

# Import libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import classification_report, confusion_matrix
import seaborn as sns

# =============================================================================
# STEP 1: LOAD AND EXPLORE DATA
# =============================================================================

# Load data
iris = load_iris()
X = pd.DataFrame(iris.data, columns=iris.feature_names)
y = pd.Series(iris.target, name='species')

print("="*60)
print("IRIS DATASET EXPLORATION")
print("="*60)
print(f"\nDataset Shape: {X.shape}")
print(f"Features: {list(X.columns)}")
print(f"Classes: {iris.target_names}")
print(f"\nClass Distribution:\n{y.value_counts()}")
print(f"\nFirst 5 rows:\n{X.head()}")
print(f"\nStatistics:\n{X.describe()}")

# =============================================================================
# STEP 2: VISUALIZE DATA
# =============================================================================

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Pairwise scatter plots
for i, (ax, (f1, f2)) in enumerate(zip(axes.flat, 
    [('sepal length (cm)', 'sepal width (cm)'),
     ('petal length (cm)', 'petal width (cm)'),
     ('sepal length (cm)', 'petal length (cm)'),
     ('sepal width (cm)', 'petal width (cm)')])):
    
    for species_idx, species_name in enumerate(iris.target_names):
        mask = y == species_idx
        ax.scatter(X.loc[mask, f1], X.loc[mask, f2], 
                   label=species_name, alpha=0.7)
    ax.set_xlabel(f1)
    ax.set_ylabel(f2)
    ax.legend()
    ax.set_title(f'{f1} vs {f2}')

plt.tight_layout()
plt.savefig('iris_visualization.png', dpi=100)
plt.show()

# =============================================================================
# STEP 3: PREPARE DATA
# =============================================================================

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining set size: {len(X_train)}")
print(f"Test set size: {len(X_test)}")

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # Use same scaling!

# =============================================================================
# STEP 4: FIND OPTIMAL K
# =============================================================================

k_values = range(1, 31)
cv_scores = []

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k)
    scores = cross_val_score(knn, X_train_scaled, y_train, cv=5, scoring='accuracy')
    cv_scores.append(scores.mean())

# Plot K vs Accuracy
plt.figure(figsize=(10, 6))
plt.plot(k_values, cv_scores, 'bo-', linewidth=2, markersize=6)
plt.xlabel('K (Number of Neighbors)', fontsize=12)
plt.ylabel('Cross-Validation Accuracy', fontsize=12)
plt.title('Finding Optimal K for Iris Classification', fontsize=14)
plt.axvline(x=k_values[np.argmax(cv_scores)], color='r', linestyle='--', 
            label=f'Best K = {k_values[np.argmax(cv_scores)]}')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('optimal_k_iris.png', dpi=100)
plt.show()

best_k = k_values[np.argmax(cv_scores)]
print(f"\nOptimal K: {best_k}")
print(f"Best CV Accuracy: {max(cv_scores):.4f}")

# =============================================================================
# STEP 5: TRAIN FINAL MODEL
# =============================================================================

# Train with best K
final_knn = KNeighborsClassifier(n_neighbors=best_k, weights='distance')
final_knn.fit(X_train_scaled, y_train)

# =============================================================================
# STEP 6: EVALUATE MODEL
# =============================================================================

# Predictions
y_pred = final_knn.predict(X_test_scaled)
y_pred_proba = final_knn.predict_proba(X_test_scaled)

# Print results
print("\n" + "="*60)
print("MODEL EVALUATION")
print("="*60)
print(f"\nTest Accuracy: {final_knn.score(X_test_scaled, y_test):.4f}")
print("\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=iris.target_names))

# Confusion Matrix
plt.figure(figsize=(8, 6))
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
            xticklabels=iris.target_names, yticklabels=iris.target_names)
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix - Iris Classification')
plt.savefig('confusion_matrix_iris.png', dpi=100)
plt.show()

# =============================================================================
# STEP 7: MAKE PREDICTIONS ON NEW DATA
# =============================================================================

# New flower measurements
new_flowers = np.array([
    [5.1, 3.5, 1.4, 0.2],   # Should be setosa
    [6.2, 2.9, 4.3, 1.3],   # Should be versicolor
    [7.7, 3.0, 6.1, 2.3]    # Should be virginica
])

# Scale and predict
new_flowers_scaled = scaler.transform(new_flowers)
predictions = final_knn.predict(new_flowers_scaled)
probabilities = final_knn.predict_proba(new_flowers_scaled)

print("\n" + "="*60)
print("PREDICTIONS ON NEW FLOWERS")
print("="*60)
for i, (flower, pred, proba) in enumerate(zip(new_flowers, predictions, probabilities)):
    print(f"\nFlower {i+1}: {flower}")
    print(f"  Predicted Species: {iris.target_names[pred]}")
    print(f"  Probabilities: {dict(zip(iris.target_names, proba.round(3)))}")
15.2 Project 2: Customer Churn Prediction (Intermediate)
Python

"""
PROJECT 2: CUSTOMER CHURN PREDICTION
=====================================
Difficulty: Intermediate
Goal: Predict if a customer will churn (leave)
Includes: Missing values, categorical features, imbalanced data
"""

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.impute import SimpleImputer
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import (classification_report, confusion_matrix, 
                             roc_auc_score, roc_curve, precision_recall_curve)
from imblearn.over_sampling import SMOTE
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')

# =============================================================================
# STEP 1: CREATE SYNTHETIC DATASET (Simulating real-world data)
# =============================================================================

np.random.seed(42)
n_samples = 2000

# Create imbalanced dataset (80% not churned, 20% churned)
data = {
    'customer_id': range(1, n_samples + 1),
    'age': np.random.randint(18, 70, n_samples),
    'tenure_months': np.random.randint(1, 72, n_samples),
    'monthly_charges': np.random.uniform(20, 100, n_samples).round(2),
    'total_charges': np.random.uniform(100, 5000, n_samples).round(2),
    'num_support_tickets': np.random.poisson(2, n_samples),
    'contract_type': np.random.choice(['Month-to-month', 'One year', 'Two year'], 
                                       n_samples, p=[0.5, 0.3, 0.2]),
    'payment_method': np.random.choice(['Credit card', 'Bank transfer', 'Electronic check'], 
                                        n_samples),
    'internet_service': np.random.choice(['DSL', 'Fiber optic', 'No'], n_samples),
    'churned': np.random.choice([0, 1], n_samples, p=[0.8, 0.2])
}

df = pd.DataFrame(data)

# Add some missing values (realistic!)
df.loc[np.random.choice(df.index, 100), 'age'] = np.nan
df.loc[np.random.choice(df.index, 50), 'monthly_charges'] = np.nan
df.loc[np.random.choice(df.index, 30), 'tenure_months'] = np.nan

# Make churned customers have different patterns
churn_mask = df['churned'] == 1
df.loc[churn_mask, 'tenure_months'] = df.loc[churn_mask, 'tenure_months'] * 0.5
df.loc[churn_mask, 'num_support_tickets'] = df.loc[churn_mask, 'num_support_tickets'] + 3

print("="*60)
print("CUSTOMER CHURN DATASET")
print("="*60)
print(f"\nDataset Shape: {df.shape}")
print(f"\nMissing Values:\n{df.isnull().sum()}")
print(f"\nClass Distribution:\n{df['churned'].value_counts()}")
print(f"\nFirst 5 rows:\n{df.head()}")

# =============================================================================
# STEP 2: EXPLORATORY DATA ANALYSIS
# =============================================================================

fig, axes = plt.subplots(2, 3, figsize=(15, 10))

# Age distribution by churn
sns.histplot(data=df, x='age', hue='churned', ax=axes[0,0], kde=True)
axes[0,0].set_title('Age Distribution by Churn')

# Tenure distribution by churn
sns.histplot(data=df, x='tenure_months', hue='churned', ax=axes[0,1], kde=True)
axes[0,1].set_title('Tenure Distribution by Churn')

# Monthly charges by churn
sns.boxplot(data=df, x='churned', y='monthly_charges', ax=axes[0,2])
axes[0,2].set_title('Monthly Charges by Churn')

# Support tickets by churn
sns.boxplot(data=df, x='churned', y='num_support_tickets', ax=axes[1,0])
axes[1,0].set_title('Support Tickets by Churn')

# Contract type by churn
ct = df.groupby(['contract_type', 'churned']).size().unstack()
ct.plot(kind='bar', ax=axes[1,1])
axes[1,1].set_title('Contract Type by Churn')
axes[1,1].tick_params(axis='x', rotation=45)

# Churn distribution
df['churned'].value_counts().plot(kind='pie', autopct='%1.1f%%', ax=axes[1,2])
axes[1,2].set_title('Churn Distribution')

plt.tight_layout()
plt.savefig('churn_eda.png', dpi=100)
plt.show()

# =============================================================================
# STEP 3: DATA PREPROCESSING
# =============================================================================

# Separate features and target
X = df.drop(['customer_id', 'churned'], axis=1)
y = df['churned']

# Identify column types
numeric_cols = ['age', 'tenure_months', 'monthly_charges', 'total_charges', 'num_support_tickets']
categorical_cols = ['contract_type', 'payment_method', 'internet_service']

# Handle missing values in numeric columns
num_imputer = SimpleImputer(strategy='median')
X[numeric_cols] = num_imputer.fit_transform(X[numeric_cols])

# Encode categorical variables
label_encoders = {}
for col in categorical_cols:
    le = LabelEncoder()
    X[col] = le.fit_transform(X[col])
    label_encoders[col] = le

print(f"\nAfter preprocessing:\n{X.head()}")
print(f"\nMissing values after preprocessing:\n{X.isnull().sum().sum()}")

# =============================================================================
# STEP 4: TRAIN-TEST SPLIT
# =============================================================================

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining set: {len(X_train)} samples")
print(f"Test set: {len(X_test)} samples")
print(f"Training class distribution:\n{y_train.value_counts()}")

# =============================================================================
# STEP 5: HANDLE IMBALANCED DATA WITH SMOTE
# =============================================================================

print("\n" + "="*60)
print("HANDLING IMBALANCED DATA WITH SMOTE")
print("="*60)

smote = SMOTE(random_state=42)
X_train_balanced, y_train_balanced = smote.fit_resample(X_train, y_train)

print(f"\nBefore SMOTE: {y_train.value_counts().to_dict()}")
print(f"After SMOTE: {pd.Series(y_train_balanced).value_counts().to_dict()}")

# =============================================================================
# STEP 6: SCALE FEATURES
# =============================================================================

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train_balanced)
X_test_scaled = scaler.transform(X_test)

# =============================================================================
# STEP 7: HYPERPARAMETER TUNING
# =============================================================================

print("\n" + "="*60)
print("HYPERPARAMETER TUNING")
print("="*60)

param_grid = {
    'n_neighbors': [3, 5, 7, 9, 11, 15, 21],
    'weights': ['uniform', 'distance'],
    'metric': ['euclidean', 'manhattan']
}

grid_search = GridSearchCV(
    KNeighborsClassifier(),
    param_grid,
    cv=5,
    scoring='roc_auc',
    n_jobs=-1,
    verbose=1
)

grid_search.fit(X_train_scaled, y_train_balanced)

print(f"\nBest Parameters: {grid_search.best_params_}")
print(f"Best CV ROC-AUC: {grid_search.best_score_:.4f}")

# =============================================================================
# STEP 8: TRAIN FINAL MODEL
# =============================================================================

best_knn = grid_search.best_estimator_

# =============================================================================
# STEP 9: EVALUATE MODEL
# =============================================================================

# Predictions
y_pred = best_knn.predict(X_test_scaled)
y_pred_proba = best_knn.predict_proba(X_test_scaled)[:, 1]

print("\n" + "="*60)
print("MODEL EVALUATION")
print("="*60)

print("\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=['Not Churned', 'Churned']))

print(f"ROC-AUC Score: {roc_auc_score(y_test, y_pred_proba):.4f}")

# Plot ROC Curve
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

# ROC Curve
fpr, tpr, _ = roc_curve(y_test, y_pred_proba)
axes[0].plot(fpr, tpr, 'b-', linewidth=2, 
             label=f'KNN (AUC = {roc_auc_score(y_test, y_pred_proba):.3f})')
axes[0].plot([0, 1], [0, 1], 'r--', label='Random')
axes[0].set_xlabel('False Positive Rate')
axes[0].set_ylabel('True Positive Rate')
axes[0].set_title('ROC Curve')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# Precision-Recall Curve
precision, recall, _ = precision_recall_curve(y_test, y_pred_proba)
axes[1].plot(recall, precision, 'g-', linewidth=2)
axes[1].set_xlabel('Recall')
axes[1].set_ylabel('Precision')
axes[1].set_title('Precision-Recall Curve')
axes[1].grid(True, alpha=0.3)

# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', ax=axes[2],
            xticklabels=['Not Churned', 'Churned'],
            yticklabels=['Not Churned', 'Churned'])
axes[2].set_xlabel('Predicted')
axes[2].set_ylabel('Actual')
axes[2].set_title('Confusion Matrix')

plt.tight_layout()
plt.savefig('churn_evaluation.png', dpi=100)
plt.show()

# =============================================================================
# STEP 10: FEATURE IMPORTANCE (via permutation)
# =============================================================================

from sklearn.inspection import permutation_importance

perm_importance = permutation_importance(best_knn, X_test_scaled, y_test, 
                                          n_repeats=10, random_state=42)

feature_importance = pd.DataFrame({
    'feature': X.columns,
    'importance': perm_importance.importances_mean
}).sort_values('importance', ascending=False)

plt.figure(figsize=(10, 6))
sns.barplot(data=feature_importance, x='importance', y='feature')
plt.title('Feature Importance (Permutation)')
plt.xlabel('Mean Decrease in Accuracy')
plt.tight_layout()
plt.savefig('feature_importance.png', dpi=100)
plt.show()

print("\nFeature Importance:")
print(feature_importance)
15.3 Project 3: Image Classification (Advanced)
Python

"""
PROJECT 3: HANDWRITTEN DIGIT RECOGNITION
==========================================
Difficulty: Advanced
Dataset: MNIST
Goal: Classify handwritten digits (0-9)
Includes: High dimensionality, large dataset, visualization
"""

import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import fetch_openml
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import classification_report, confusion_matrix
import seaborn as sns
import time

# =============================================================================
# STEP 1: LOAD MNIST DATASET
# =============================================================================

print("Loading MNIST dataset...")
mnist = fetch_openml('mnist_784', version=1, as_frame=False, parser='auto')
X, y = mnist.data, mnist.target.astype(int)

print("="*60)
print("MNIST DATASET")
print("="*60)
print(f"Dataset Shape: {X.shape}")
print(f"Image size: 28x28 = 784 pixels (features)")
print(f"Number of classes: {len(np.unique(y))}")
print(f"Classes: {np.unique(y)}")

# Use subset for faster computation
n_samples = 10000
indices = np.random.choice(len(X), n_samples, replace=False)
X = X[indices]
y = y[indices]
print(f"\nUsing {n_samples} samples for demonstration")

# =============================================================================
# STEP 2: VISUALIZE SAMPLE DIGITS
# =============================================================================

fig, axes = plt.subplots(2, 5, figsize=(12, 5))
for i, ax in enumerate(axes.flat):
    idx = np.random.randint(len(X))
    ax.imshow(X[idx].reshape(28, 28), cmap='gray')
    ax.set_title(f'Label: {y[idx]}')
    ax.axis('off')
plt.suptitle('Sample MNIST Digits', fontsize=14)
plt.tight_layout()
plt.savefig('mnist_samples.png', dpi=100)
plt.show()

# =============================================================================
# STEP 3: PREPROCESS DATA
# =============================================================================

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Scale features (pixel values 0-255 -> normalized)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print(f"\nTraining samples: {len(X_train)}")
print(f"Test samples: {len(X_test)}")

# =============================================================================
# STEP 4: DIMENSIONALITY REDUCTION WITH PCA
# =============================================================================

print("\n" + "="*60)
print("DIMENSIONALITY REDUCTION WITH PCA")
print("="*60)

# Find optimal number of components
pca_full = PCA()
pca_full.fit(X_train_scaled)

# Plot cumulative explained variance
plt.figure(figsize=(10, 6))
cumulative_variance = np.cumsum(pca_full.explained_variance_ratio_)
plt.plot(cumulative_variance, 'b-', linewidth=2)
plt.axhline(y=0.95, color='r', linestyle='--', label='95% variance')
plt.xlabel('Number of Components')
plt.ylabel('Cumulative Explained Variance')
plt.title('PCA - Cumulative Explained Variance')
plt.legend()
plt.grid(True, alpha=0.3)

# Find components for 95% variance
n_components_95 = np.argmax(cumulative_variance >= 0.95) + 1
plt.axvline(x=n_components_95, color='g', linestyle='--', 
            label=f'{n_components_95} components for 95%')
plt.legend()
plt.savefig('pca_variance.png', dpi=100)
plt.show()

print(f"Components for 95% variance: {n_components_95}")

# Apply PCA
pca = PCA(n_components=n_components_95)
X_train_pca = pca.fit_transform(X_train_scaled)
X_test_pca = pca.transform(X_test_scaled)

print(f"Original dimensions: {X_train_scaled.shape[1]}")
print(f"After PCA: {X_train_pca.shape[1]}")
print(f"Dimension reduction: {X_train_scaled.shape[1] - X_train_pca.shape[1]} features removed")

# =============================================================================
# STEP 5: COMPARE KNN WITH AND WITHOUT PCA
# =============================================================================

print("\n" + "="*60)
print("KNN PERFORMANCE COMPARISON")
print("="*60)

results = []

# Without PCA
print("\nTraining KNN without PCA...")
start_time = time.time()
knn_no_pca = KNeighborsClassifier(n_neighbors=5, n_jobs=-1)
knn_no_pca.fit(X_train_scaled, y_train)
train_time_no_pca = time.time() - start_time

start_time = time.time()
accuracy_no_pca = knn_no_pca.score(X_test_scaled, y_test)
pred_time_no_pca = time.time() - start_time

results.append({
    'Method': 'KNN (No PCA)',
    'Dimensions': X_train_scaled.shape[1],
    'Train Time': train_time_no_pca,
    'Predict Time': pred_time_no_pca,
    'Accuracy': accuracy_no_pca
})

# With PCA
print("Training KNN with PCA...")
start_time = time.time()
knn_pca = KNeighborsClassifier(n_neighbors=5, n_jobs=-1)
knn_pca.fit(X_train_pca, y_train)
train_time_pca = time.time() - start_time

start_time = time.time()
accuracy_pca = knn_pca.score(X_test_pca, y_test)
pred_time_pca = time.time() - start_time

results.append({
    'Method': 'KNN (With PCA)',
    'Dimensions': X_train_pca.shape[1],
    'Train Time': train_time_pca,
    'Predict Time': pred_time_pca,
    'Accuracy': accuracy_pca
})

# Display results
results_df = pd.DataFrame(results)
print("\n" + results_df.to_string(index=False))

# =============================================================================
# STEP 6: HYPERPARAMETER TUNING
# =============================================================================

print("\n" + "="*60)
print("HYPERPARAMETER TUNING")
print("="*60)

k_values = [1, 3, 5, 7, 9, 11, 15]
accuracies = []

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k, n_jobs=-1)
    scores = cross_val_score(knn, X_train_pca, y_train, cv=3, scoring='accuracy')
    accuracies.append(scores.mean())
    print(f"K={k}: CV Accuracy = {scores.mean():.4f} (+/- {scores.std():.4f})")

best_k = k_values[np.argmax(accuracies)]
print(f"\nBest K: {best_k}")

# Plot K vs Accuracy
plt.figure(figsize=(10, 6))
plt.plot(k_values, accuracies, 'bo-', linewidth=2, markersize=8)
plt.xlabel('K (Number of Neighbors)', fontsize=12)
plt.ylabel('Cross-Validation Accuracy', fontsize=12)
plt.title('Finding Optimal K for MNIST', fontsize=14)
plt.axvline(x=best_k, color='r', linestyle='--', label=f'Best K = {best_k}')
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig('mnist_optimal_k.png', dpi=100)
plt.show()

# =============================================================================
# STEP 7: FINAL MODEL EVALUATION
# =============================================================================

print("\n" + "="*60)
print("FINAL MODEL EVALUATION")
print("="*60)

# Train final model
final_knn = KNeighborsClassifier(n_neighbors=best_k, weights='distance', n_jobs=-1)
final_knn.fit(X_train_pca, y_train)

# Predictions
y_pred = final_knn.predict(X_test_pca)

print(f"\nTest Accuracy: {final_knn.score(X_test_pca, y_test):.4f}")
print("\nClassification Report:")
print(classification_report(y_test, y_pred))

# Confusion Matrix
plt.figure(figsize=(10, 8))
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel('Predicted Digit')
plt.ylabel('Actual Digit')
plt.title('Confusion Matrix - MNIST Digit Classification')
plt.savefig('mnist_confusion_matrix.png', dpi=100)
plt.show()

# =============================================================================
# STEP 8: VISUALIZE MISCLASSIFIED DIGITS
# =============================================================================

print("\n" + "="*60)
print("MISCLASSIFIED DIGITS")
print("="*60)

# Find misclassified samples
misclassified_idx = np.where(y_pred != y_test)[0]
print(f"Number of misclassified samples: {len(misclassified_idx)}")

# Visualize some misclassified digits
fig, axes = plt.subplots(2, 5, figsize=(12, 5))
for i, ax in enumerate(axes.flat):
    if i < len(misclassified_idx):
        idx = misclassified_idx[i]
        ax.imshow(X_test[idx].reshape(28, 28), cmap='gray')
        ax.set_title(f'True: {y_test[idx]}, Pred: {y_pred[idx]}', color='red')
        ax.axis('off')
plt.suptitle('Misclassified Digits', fontsize=14)
plt.tight_layout()
plt.savefig('mnist_misclassified.png', dpi=100)
plt.show()

# =============================================================================
# STEP 9: VISUALIZE NEAREST NEIGHBORS
# =============================================================================

def visualize_nearest_neighbors(query_idx, X_train, y_train, X_test, knn_model, n_neighbors=5):
    """Visualize query image and its nearest neighbors"""
    
    # Get query image
    query = X_test[query_idx].reshape(1, -1)
    query_scaled = scaler.transform(query)
    query_pca = pca.transform(query_scaled)
    
    # Find nearest neighbors
    distances, indices = knn_model.kneighbors(query_pca, n_neighbors=n_neighbors)
    
    # Plot
    fig, axes = plt.subplots(1, n_neighbors + 1, figsize=(15, 3))
    
    # Query image
    axes[0].imshow(X_test[query_idx].reshape(28, 28), cmap='gray')
    axes[0].set_title(f'Query\n(True: {y_test[query_idx]})', fontsize=10)
    axes[0].axis('off')
    
    # Neighbors
    for i, (dist, idx) in enumerate(zip(distances[0], indices[0])):
        axes[i+1].imshow(X_train[idx].reshape(28, 28), cmap='gray')
        axes[i+1].set_title(f'NN {i+1}\nLabel: {y_train[idx]}\nDist: {dist:.2f}', fontsize=9)
        axes[i+1].axis('off')
    
    plt.suptitle('Query Image and Nearest Neighbors', fontsize=12)
    plt.tight_layout()
    return fig

# Visualize for a few samples
for i in range(3):
    query_idx = np.random.randint(len(X_test))
    fig = visualize_nearest_neighbors(query_idx, X_train, y_train, X_test, final_knn)
    plt.savefig(f'nearest_neighbors_{i}.png', dpi=100)
    plt.show()
15.4 Quick Reference Card
text

┌─────────────────────────────────────────────────────────────────┐
│                    KNN QUICK REFERENCE CARD                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ALGORITHM TYPE:        Supervised, Lazy Learning               │
│  USE CASES:             Classification, Regression              │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  SKLEARN SYNTAX:                                                │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  # Classification                                               │
│  from sklearn.neighbors import KNeighborsClassifier             │
│  knn = KNeighborsClassifier(n_neighbors=5)                      │
│  knn.fit(X_train, y_train)                                      │
│  predictions = knn.predict(X_test)                              │
│                                                                 │
│  # Regression                                                   │
│  from sklearn.neighbors import KNeighborsRegressor              │
│  knn = KNeighborsRegressor(n_neighbors=5)                       │
│  knn.fit(X_train, y_train)                                      │
│  predictions = knn.predict(X_test)                              │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  KEY PARAMETERS:                                                │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  n_neighbors    : Number of neighbors (default: 5)              │
│  weights        : 'uniform' or 'distance'                       │
│  metric         : 'euclidean', 'manhattan', 'minkowski'        │
│  algorithm      : 'auto', 'ball_tree', 'kd_tree', 'brute'      │
│  n_jobs         : -1 for all CPU cores                          │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  MUST-DO PREPROCESSING:                                         │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  1. Handle missing values (imputation)                          │
│  2. Encode categorical variables (one-hot)                      │
│  3. Scale features (StandardScaler or MinMaxScaler)            │
│  4. Consider dimensionality reduction for high-D data          │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  CHOOSING K:                                                    │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  • Start with K = √n (square root of samples)                  │
│  • Use cross-validation to find optimal K                       │
│  • Use ODD K for binary classification                          │
│  • Small K: Complex boundary, may overfit                       │
│  • Large K: Smooth boundary, may underfit                       │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  COMMON DISTANCES:                                              │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  Euclidean  : √Σ(xᵢ-yᵢ)²     (default, low-dim)                │
│  Manhattan  : Σ|xᵢ-yᵢ|       (high-dim, robust)                 │
│  Cosine     : 1 - cos(θ)     (text data)                       │
│  Hamming    : count(xᵢ≠yᵢ)   (binary data)                     │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│  PROS:                         CONS:                            │
│  ─────────────────────────────────────────────────────────────  │
│  ✓ Simple to understand        ✗ Slow prediction               │
│  ✓ No training phase           ✗ Memory intensive              │
│  ✓ No assumptions              ✗ Curse of dimensionality       │
│  ✓ Naturally multi-class       ✗ Sensitive to scale            │
│  ✓ Easy to update              ✗ Sensitive to noise            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
🎓 Conclusion
Congratulations! You have now mastered K-Nearest Neighbors from the very basics to advanced techniques.

What You've Learned:
text

✅ Chapter 1:  Foundation - What is KNN, lazy learning concept
✅ Chapter 2:  Mathematics - Distance formulas and their properties
✅ Chapter 3:  Algorithm - Step-by-step working of KNN
✅ Chapter 4:  Choosing K - Methods to find optimal K value
✅ Chapter 5:  Distance Metrics - When to use which distance
✅ Chapter 6:  Preprocessing - Scaling, encoding, missing values
✅ Chapter 7:  Classification - Voting mechanisms, multi-class
✅ Chapter 8:  Regression - Averaging, weighted predictions
✅ Chapter 9:  Weighted KNN - Distance-based weighting schemes
✅ Chapter 10: Scalability - KD-Tree, Ball Tree, ANN
✅ Chapter 11: Optimization - Feature weighting, ensemble KNN
✅ Chapter 12: Implementation - From scratch and sklearn
✅ Chapter 13: Pitfalls - Common mistakes and solutions
✅ Chapter 14: Interviews - 20+ questions with detailed answers
✅ Chapter 15: Projects - Real-world applications with code
Your Next Steps:
Practice: Implement KNN on Kaggle datasets
Compare: Try KNN vs other algorithms on same data
Experiment: Test different distance metrics and K values
Scale: Learn to handle large datasets with ANN libraries
Deploy: Build a KNN-based application
Happy Learning! 🚀

"The best way to learn is by doing. Now go implement KNN!"