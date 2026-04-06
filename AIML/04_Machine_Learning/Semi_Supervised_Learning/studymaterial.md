🎓 The Ultimate Guide to Semi-Supervised Learning
From Zero to Hero: A Complete Journey
📚 Table of Contents
Chapter 1: Foundation - Understanding the Basics
Chapter 2: Why Semi-Supervised Learning Exists
Chapter 3: Core Assumptions - The Mathematical Foundation
Chapter 4: Self-Training Methods
Chapter 5: Co-Training Approaches
Chapter 6: Graph-Based Methods
Chapter 7: Generative Models
Chapter 8: Low-Density Separation Methods
Chapter 9: Modern Deep Semi-Supervised Learning
Chapter 10: Consistency Regularization
Chapter 11: Pseudo-Labeling & Advanced Techniques
Chapter 12: State-of-the-Art Methods
Chapter 13: Practical Implementation Guide
Chapter 14: Evaluation & Best Practices
Chapter 15: Real-World Applications
Chapter 16: Common Pitfalls & Solutions
Chapter 17: Future Directions
Chapter 18: Interview Questions & Answers
Chapter 1: Foundation - Understanding the Basics
1.1 What is Machine Learning? (Quick Recap)
Before diving into Semi-Supervised Learning, let's ensure we're on the same page.

text

Machine Learning = Teaching computers to learn patterns from data
                   without being explicitly programmed for every scenario
The Three Main Types of Learning
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                        MACHINE LEARNING PARADIGMS                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐         │
│   │   SUPERVISED     │  │ SEMI-SUPERVISED  │  │  UNSUPERVISED    │         │
│   │    LEARNING      │  │    LEARNING      │  │    LEARNING      │         │
│   ├──────────────────┤  ├──────────────────┤  ├──────────────────┤         │
│   │                  │  │                  │  │                  │         │
│   │  ALL data has    │  │  SOME data has   │  │  NO data has     │         │
│   │    labels        │  │    labels        │  │    labels        │         │
│   │                  │  │                  │  │                  │         │
│   │  Example:        │  │  Example:        │  │  Example:        │         │
│   │  Cat/Dog         │  │  10 labeled +    │  │  Customer        │         │
│   │  classifier      │  │  1000 unlabeled  │  │  segmentation    │         │
│   │  with 10000      │  │  images          │  │                  │         │
│   │  labeled images  │  │                  │  │                  │         │
│   └──────────────────┘  └──────────────────┘  └──────────────────┘         │
│                                                                             │
│         100% Labels         1-10% Labels           0% Labels               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
1.2 What Exactly is Semi-Supervised Learning?
Simple Definition (Remember This Forever!)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   SEMI-SUPERVISED LEARNING = Learning from BOTH labeled AND unlabeled data │
│                                                                             │
│   Formula:  SSL = Small Labeled Data + Large Unlabeled Data → Better Model │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Real-World Analogy 🎯
Imagine you're learning to identify different types of birds:

text

SCENARIO: Learning Bird Species

SUPERVISED APPROACH:
├── Expert shows you 1000 bird photos
├── Each photo has a label: "This is a Sparrow", "This is an Eagle"
├── You learn from ALL labeled examples
└── Problem: Expert's time is expensive!

SEMI-SUPERVISED APPROACH:
├── Expert labels only 50 bird photos (expensive, time-consuming)
├── You also get 10,000 unlabeled bird photos (cheap, easy to collect)
├── You learn patterns from unlabeled photos (shape, color, size patterns)
├── Apply these patterns along with the 50 labeled examples
└── Result: Much better learning with less expert involvement!

UNSUPERVISED APPROACH:
├── You get 10,000 bird photos with NO labels
├── You group similar-looking birds together
└── But you don't know WHAT each group represents
1.3 Mathematical Notation (Your Foundation)
Let's establish the notation we'll use throughout this guide:

text

┌─────────────────────────────────────────────────────────────────────────────┐
│                           NOTATION REFERENCE                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  DATASETS:                                                                  │
│  ─────────                                                                  │
│  D_L = {(x₁, y₁), (x₂, y₂), ..., (xₗ, yₗ)}  →  Labeled Dataset (l samples) │
│  D_U = {x_{l+1}, x_{l+2}, ..., x_{l+u}}     →  Unlabeled Dataset (u samples)│
│                                                                             │
│  WHERE:                                                                     │
│  ──────                                                                     │
│  xᵢ ∈ ℝᵈ           →  Input feature vector (d dimensions)                  │
│  yᵢ ∈ {1,2,...,C}  →  Class label (C classes)                              │
│  l                 →  Number of labeled samples                            │
│  u                 →  Number of unlabeled samples                          │
│                                                                             │
│  TYPICAL SCENARIO:                                                          │
│  ─────────────────                                                          │
│  u >> l  (unlabeled samples FAR outnumber labeled samples)                 │
│                                                                             │
│  Example: l = 100, u = 10,000                                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
1.4 Visual Understanding
text

                    THE SEMI-SUPERVISED LEARNING LANDSCAPE
    
    Labeled Data (Expensive)              Unlabeled Data (Cheap)
    ┌─────────────────────┐              ┌─────────────────────┐
    │  ● = Class A        │              │  ○ = Unknown Class  │
    │  ▲ = Class B        │              │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │                     │              │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │  ●     ▲           │              │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │    ●       ▲       │      +       │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │  ●   ●     ▲  ▲    │              │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │                     │              │  ○ ○ ○ ○ ○ ○ ○ ○ ○  │
    │     (5 samples)     │              │    (100+ samples)   │
    └─────────────────────┘              └─────────────────────┘
                          │              │
                          └──────┬───────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │  SEMI-SUPERVISED        │
                    │  LEARNING ALGORITHM     │
                    └─────────────────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │  ● ●   ○→●   ○→●       │
                    │  ● ●     ●     ●       │
                    │        ▲ ▲   ○→▲       │
                    │      ▲ ▲ ▲     ▲       │
                    │                         │
                    │  Unlabeled data now     │
                    │  helps define better    │
                    │  decision boundaries!   │
                    └─────────────────────────┘
1.5 Key Terminology Glossary
Term	Definition	Example
Labeled Data	Data with known output/target	Image with "cat" tag
Unlabeled Data	Data without known output	Image without any tag
Pseudo-label	Predicted label for unlabeled data	Model predicts "cat" for unlabeled image
Confidence Score	How sure the model is about prediction	95% sure it's a cat
Decision Boundary	Line/surface separating classes	Line between cat and dog regions
Manifold	Lower-dimensional structure in data	Images lie on a surface in high-dim space
Cluster	Group of similar data points	All cat images grouped together
Chapter 2: Why Semi-Supervised Learning Exists
2.1 The Labeling Problem
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                        THE FUNDAMENTAL PROBLEM                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   COLLECTING DATA = EASY & CHEAP                                           │
│   ───────────────────────────────                                           │
│   • Web scraping millions of images                                        │
│   • Recording hours of audio                                               │
│   • Gathering millions of text documents                                   │
│   • Sensor data from IoT devices                                           │
│                                                                             │
│   LABELING DATA = HARD & EXPENSIVE                                         │
│   ─────────────────────────────────                                         │
│   • Requires human experts                                                 │
│   • Time-consuming                                                         │
│   • Error-prone                                                            │
│   • Sometimes needs specialized knowledge                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Real Cost Analysis
text

MEDICAL IMAGING EXAMPLE:
────────────────────────

Unlabeled X-ray images:
├── Cost per image: $0.01 (just storage)
├── Collection time: Automatic
└── Available quantity: Millions

Labeled X-ray images:
├── Cost per image: $50-100 (radiologist time)
├── Labeling time: 10-30 minutes per image
├── Availability: Limited by expert availability
└── Additional concerns: Patient privacy, legal compliance

COST COMPARISON FOR 10,000 IMAGES:
┌────────────────────┬────────────────┬────────────────┐
│ Approach           │ Cost           │ Time           │
├────────────────────┼────────────────┼────────────────┤
│ All Labeled        │ $500,000+      │ 6+ months      │
│ Semi-Supervised    │ $5,000-10,000  │ 1-2 weeks      │
│ (100 labeled)      │                │                │
└────────────────────┴────────────────┴────────────────┘
2.2 When to Use Semi-Supervised Learning
Decision Framework
text

                    SHOULD YOU USE SEMI-SUPERVISED LEARNING?
                    
                                 START
                                   │
                                   ▼
                    ┌──────────────────────────┐
                    │ Do you have LOTS of      │
                    │ unlabeled data?          │
                    └──────────────────────────┘
                           │           │
                          YES          NO
                           │           │
                           ▼           ▼
                    ┌─────────────┐   Consider other
                    │ Is labeling │   approaches
                    │ expensive?  │
                    └─────────────┘
                           │           │
                          YES          NO
                           │           │
                           ▼           ▼
                    ┌─────────────┐   Just label more
                    │ Do you have │   data (supervised)
                    │ SOME labels?│
                    └─────────────┘
                           │           │
                          YES          NO
                           │           │
                           ▼           ▼
                    ╔═════════════╗   Consider
                    ║ USE SEMI-   ║   unsupervised or
                    ║ SUPERVISED  ║   active learning
                    ║ LEARNING!   ║
                    ╚═════════════╝
Perfect Use Cases ✅
text

1. MEDICAL DIAGNOSIS
   └── Few expert-labeled scans + Millions of unlabeled scans

2. SENTIMENT ANALYSIS
   └── Few manually labeled reviews + Billions of unlabeled reviews

3. SPEECH RECOGNITION
   └── Few transcribed audio files + Millions of untranscribed recordings

4. IMAGE CLASSIFICATION
   └── Few labeled images + Massive image databases

5. FRAUD DETECTION
   └── Few confirmed fraud cases + Millions of transactions

6. DOCUMENT CLASSIFICATION
   └── Few categorized documents + Corporate document archives
When NOT to Use Semi-Supervised Learning ❌
text

┌─────────────────────────────────────────────────────────────────────────────┐
│  AVOID SSL WHEN:                                                            │
│                                                                             │
│  ❌ You have abundant labeled data (just use supervised learning)          │
│  ❌ Labeling is cheap and fast                                             │
│  ❌ Unlabeled data comes from different distribution than labeled          │
│  ❌ The problem is too simple (linear separability)                        │
│  ❌ High precision is critical and you can't tolerate ANY error            │
│  ❌ Unlabeled data is scarce                                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
2.3 Comparison with Related Paradigms
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    LEARNING PARADIGMS COMPARISON                            │
├────────────────┬────────────────┬────────────────┬────────────────┬─────────┤
│ Aspect         │ Supervised     │ Semi-Supervised│ Unsupervised   │ Self-   │
│                │                │                │                │Supervised│
├────────────────┼────────────────┼────────────────┼────────────────┼─────────┤
│ Labeled Data   │ All            │ Few            │ None           │ None*   │
│                │                │                │                │         │
│ Unlabeled Data │ None           │ Lots           │ All            │ All     │
│                │                │                │                │         │
│ Goal           │ Predict labels │ Predict labels │ Find patterns  │ Learn   │
│                │                │                │                │ repr.   │
│                │                │                │                │         │
│ Output         │ Classifier/    │ Classifier/    │ Clusters/      │ Features│
│                │ Regressor      │ Regressor      │ Embeddings     │         │
│                │                │                │                │         │
│ Example        │ Cat/Dog with   │ Cat/Dog with   │ Group similar  │ Predict │
│                │ 10K labeled    │ 100 labeled +  │ images         │ rotation│
│                │ images         │ 10K unlabeled  │                │         │
└────────────────┴────────────────┴────────────────┴────────────────┴─────────┘

* Self-supervised creates its own labels from data structure
Chapter 3: Core Assumptions - The Mathematical Foundation
3.1 Why Assumptions Matter
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   KEY INSIGHT: Unlabeled data can ONLY help if there's a CONNECTION        │
│                between the input distribution P(X) and the conditional     │
│                distribution P(Y|X)                                          │
│                                                                             │
│   In other words: The STRUCTURE of your data must RELATE to the LABELS     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
3.2 The Three Fundamental Assumptions
Assumption 1: Smoothness Assumption
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                         SMOOTHNESS ASSUMPTION                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STATEMENT:                                                                │
│   "If two points x₁ and x₂ are CLOSE in input space,                       │
│    their labels y₁ and y₂ should also be SIMILAR"                          │
│                                                                             │
│   MATHEMATICAL FORMULATION:                                                 │
│   ──────────────────────────                                                │
│   If ||x₁ - x₂|| is small  →  P(y₁ = y₂) is high                           │
│                                                                             │
│   INTUITION:                                                                │
│   ──────────                                                                │
│   • Nearby images should have similar labels                               │
│   • Small changes to input shouldn't dramatically change output            │
│   • The label function is "smooth" - no wild jumps                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

VISUAL REPRESENTATION:
─────────────────────

    SMOOTHNESS HOLDS ✓              SMOOTHNESS VIOLATED ✗
    
    ● ● ● ● ● │ ▲ ▲ ▲ ▲ ▲          ● ▲ ● ▲ ● │ ▲ ● ▲ ● ▲
    ● ● ● ● ● │ ▲ ▲ ▲ ▲ ▲          ▲ ● ▲ ● ▲ │ ● ▲ ● ▲ ●
    ● ● ● ● ● │ ▲ ▲ ▲ ▲ ▲          ● ▲ ● ▲ ● │ ▲ ● ▲ ● ▲
    
    Same class points are           Classes are randomly
    grouped together                interleaved - no pattern
Assumption 2: Cluster Assumption
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          CLUSTER ASSUMPTION                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STATEMENT:                                                                │
│   "Data points form CLUSTERS, and points in the SAME cluster               │
│    are likely to have the SAME label"                                       │
│                                                                             │
│   EQUIVALENT FORMULATION (Low-Density Separation):                         │
│   ────────────────────────────────────────────────                         │
│   "Decision boundaries should pass through LOW-DENSITY regions,            │
│    not through clusters of points"                                          │
│                                                                             │
│   WHY THIS HELPS:                                                           │
│   ───────────────                                                           │
│   • Unlabeled data reveals cluster structure                               │
│   • One labeled point can "vote" for entire cluster                        │
│   • Decision boundary can be placed between clusters                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

VISUAL REPRESENTATION:
─────────────────────

    CLUSTER ASSUMPTION HOLDS ✓
    
              Cluster 1                    Cluster 2
         ┌─────────────────┐          ┌─────────────────┐
         │  ○ ○ ○ ○ ●      │          │      ▲ ○ ○ ○ ○  │
         │   ○ ○ ○ ○ ○     │   GAP    │     ○ ○ ○ ○ ○   │
         │    ○ ○ ○ ○ ○    │◄───────►│    ○ ○ ○ ○ ○    │
         │   ○ ○ ○ ○ ○     │   LOW    │     ○ ○ ○ ○ ○   │
         │  ○ ○ ○ ○ ○      │  DENSITY │      ○ ○ ○ ○ ○  │
         └─────────────────┘          └─────────────────┘
         
         ● = labeled as Class A       ▲ = labeled as Class B
         ○ = unlabeled (will inherit label from cluster)
         
    RESULT: One labeled point propagates to entire cluster!
Assumption 3: Manifold Assumption
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          MANIFOLD ASSUMPTION                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STATEMENT:                                                                │
│   "High-dimensional data lies on or near a LOW-DIMENSIONAL MANIFOLD        │
│    embedded within the high-dimensional space"                              │
│                                                                             │
│   IMPLICATION:                                                              │
│   ────────────                                                              │
│   • Distances should be measured ALONG the manifold, not through it        │
│   • Points close on the manifold should have similar labels                │
│   • Unlabeled data helps discover the manifold structure                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

VISUAL REPRESENTATION:
─────────────────────

    EUCLIDEAN DISTANCE vs MANIFOLD DISTANCE
    
    Imagine a curved road (manifold) in 2D space:
    
         A●━━━━━━━━━━━━━━━━━━━●B     ← Points on the road (manifold)
          ╲                  ╱
           ╲                ╱
            ╲   Straight   ╱         ← Euclidean: Short but wrong!
             ╲  Line      ╱
              ╲ (wrong!) ╱
               ╲        ╱
                ╲      ╱
                 ╲    ╱
                  ╲  ╱
                   ╲╱
    
    Euclidean distance A→B: SHORT (but goes through empty space)
    Manifold distance A→B:  LONG (but follows actual data structure)
    
    CORRECT APPROACH: Measure distance ALONG the curve!
Real-World Example of Manifold
text

FACE IMAGES EXAMPLE:
────────────────────

Raw Representation:
├── 256 × 256 pixel image
├── 3 color channels
└── Total: 196,608 dimensions! (256 × 256 × 3)

But faces are NOT random pixels!
They lie on a much lower-dimensional manifold defined by:
├── Face shape (~50 parameters)
├── Lighting conditions (~10 parameters)  
├── Expression (~20 parameters)
├── Pose/angle (~6 parameters)
└── Total manifold dimension: ~100 dimensions

This is a 100-dimensional surface embedded in 196,608-dimensional space!

WHY THIS MATTERS FOR SSL:
─────────────────────────
• Unlabeled faces help discover this manifold
• Similar faces (on manifold) should have similar labels
• We can measure "face similarity" more meaningfully
3.3 How Assumptions Enable Learning
text

┌─────────────────────────────────────────────────────────────────────────────┐
│              HOW UNLABELED DATA HELPS (Given Assumptions Hold)              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. SMOOTHNESS ASSUMPTION ENABLES:                                         │
│      └── Transductive methods (propagate labels to nearby points)          │
│                                                                             │
│   2. CLUSTER ASSUMPTION ENABLES:                                            │
│      └── Self-training (confident predictions expand to cluster)           │
│      └── Low-density separation (push boundaries away from data)           │
│                                                                             │
│   3. MANIFOLD ASSUMPTION ENABLES:                                           │
│      └── Graph-based methods (build graph along manifold)                  │
│      └── Representation learning (learn manifold structure)                │
│                                                                             │
│   COMBINED EFFECT:                                                          │
│   ────────────────                                                          │
│   Unlabeled data reveals structure → Structure informs classification      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
3.4 When Assumptions Fail
text

WARNING: IF ASSUMPTIONS DON'T HOLD, SSL CAN HURT PERFORMANCE!

┌─────────────────────────────────────────────────────────────────────────────┐
│                          ASSUMPTION FAILURES                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   SMOOTHNESS FAILS:                                                         │
│   ─────────────────                                                         │
│   • Adversarial examples (tiny change → wrong label)                       │
│   • Highly nonlinear boundaries                                            │
│   • Example: Distinguishing "6" from "9" (rotation matters!)               │
│                                                                             │
│   CLUSTER FAILS:                                                            │
│   ──────────────                                                            │
│   • Multiple classes in same cluster                                       │
│   • One class split across clusters                                        │
│   • Example: Different dog breeds that look similar                        │
│                                                                             │
│   MANIFOLD FAILS:                                                           │
│   ───────────────                                                           │
│   • Data is truly high-dimensional                                         │
│   • Manifolds of different classes overlap                                 │
│   • Example: Random noise data                                             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 4: Self-Training Methods
4.1 Basic Self-Training (Pseudo-Labeling)
The simplest and most intuitive semi-supervised method!

Algorithm Overview
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      SELF-TRAINING ALGORITHM                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   INPUT:  Labeled set D_L, Unlabeled set D_U, Confidence threshold τ       │
│   OUTPUT: Trained model f                                                   │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   1. Train initial model f on D_L only                                     │
│   2. REPEAT until convergence:                                             │
│      a. Use f to predict labels for all x ∈ D_U                            │
│      b. Select predictions with confidence > τ                             │
│      c. Add these (x, predicted_y) to D_L as pseudo-labeled data           │
│      d. Retrain f on expanded D_L                                          │
│   3. RETURN final model f                                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Walkthrough
text

ITERATION 0: Start with labeled data only
─────────────────────────────────────────

    ● ●           ← Class A (labeled)
      ●
                 ○ ○
           ○ ○   ○     ← Unlabeled
         ○   ○ ○
    ▲ ▲               ← Class B (labeled)
      ▲

    Model learns rough boundary from 6 labeled points.


ITERATION 1: Add high-confidence pseudo-labels
──────────────────────────────────────────────

    ● ● ○→●       
      ●   ○→●     ← These unlabeled points are CLEARLY Class A
                     (high confidence)
           ○ ○    ← Still uncertain
         ○   ○ ○
    ▲ ▲   ○→▲     ← This is CLEARLY Class B
      ▲

    3 unlabeled points added with pseudo-labels.


ITERATION 2: More pseudo-labels as model improves
──────────────────────────────────────────────────

    ● ● ● ●       
      ● ● ●       ← Pseudo-labels propagate
            ○→●
           ● ●    ← Model getting more confident
         ○→▲ ○→▲
    ▲ ▲ ▲ ▲
      ▲

    Only 3 uncertain points remain.


ITERATION 3: Convergence
────────────────────────

    ● ● ● ● ● ●   
      ● ● ● ●     ← All points now labeled!
              
           ● ●    
         ▲ ▲ ▲
    ▲ ▲ ▲ ▲ ▲
      ▲

    Final decision boundary is much better than initial!
Python Implementation
Python

import numpy as np
from sklearn.base import clone

def self_training(base_model, X_labeled, y_labeled, X_unlabeled, 
                  threshold=0.95, max_iterations=10):
    """
    Self-Training Algorithm Implementation
    
    Parameters:
    -----------
    base_model : sklearn classifier with predict_proba method
    X_labeled : Initial labeled features
    y_labeled : Initial labels
    X_unlabeled : Unlabeled features
    threshold : Confidence threshold for pseudo-labeling
    max_iterations : Maximum number of iterations
    
    Returns:
    --------
    model : Trained model
    X_labeled_final : Final labeled dataset (original + pseudo-labeled)
    y_labeled_final : Final labels
    """
    
    # Copy to avoid modifying original data
    X_train = X_labeled.copy()
    y_train = y_labeled.copy()
    X_pool = X_unlabeled.copy()
    
    for iteration in range(max_iterations):
        # Step 1: Train model on current labeled data
        model = clone(base_model)
        model.fit(X_train, y_train)
        
        # Step 2: Predict on unlabeled data
        if len(X_pool) == 0:
            print(f"Iteration {iteration}: All data labeled!")
            break
            
        probabilities = model.predict_proba(X_pool)
        max_probs = np.max(probabilities, axis=1)
        predictions = model.predict(X_pool)
        
        # Step 3: Find high-confidence predictions
        confident_mask = max_probs >= threshold
        num_confident = np.sum(confident_mask)
        
        print(f"Iteration {iteration}: Adding {num_confident} pseudo-labels")
        
        if num_confident == 0:
            print("No confident predictions. Stopping.")
            break
        
        # Step 4: Add pseudo-labeled samples to training set
        X_train = np.vstack([X_train, X_pool[confident_mask]])
        y_train = np.concatenate([y_train, predictions[confident_mask]])
        
        # Remove pseudo-labeled samples from pool
        X_pool = X_pool[~confident_mask]
    
    # Final training
    model = clone(base_model)
    model.fit(X_train, y_train)
    
    return model, X_train, y_train


# USAGE EXAMPLE:
# ==============
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import make_classification

# Create sample data
X, y = make_classification(n_samples=1000, n_features=20, 
                           n_informative=10, random_state=42)

# Split into labeled (5%) and unlabeled
n_labeled = 50
X_labeled, y_labeled = X[:n_labeled], y[:n_labeled]
X_unlabeled = X[n_labeled:]
y_unlabeled = y[n_labeled:]  # We have these but pretend we don't!

# Run self-training
base_model = LogisticRegression()
model, X_final, y_final = self_training(
    base_model, X_labeled, y_labeled, X_unlabeled,
    threshold=0.9, max_iterations=20
)

# Evaluate on held-out unlabeled data
accuracy = np.mean(model.predict(X_unlabeled) == y_unlabeled)
print(f"Final Accuracy: {accuracy:.4f}")
4.2 Confidence Threshold Selection
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    CONFIDENCE THRESHOLD TRADEOFFS                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   HIGH THRESHOLD (e.g., τ = 0.99):                                         │
│   ─────────────────────────────────                                         │
│   ✅ Very few errors in pseudo-labels                                      │
│   ✅ Conservative, safe approach                                           │
│   ❌ Slow learning (few samples added per iteration)                       │
│   ❌ May never reach some regions of the data                              │
│                                                                             │
│   LOW THRESHOLD (e.g., τ = 0.60):                                          │
│   ────────────────────────────────                                          │
│   ✅ Fast learning (many samples added)                                    │
│   ✅ Good coverage of data space                                           │
│   ❌ Many incorrect pseudo-labels                                          │
│   ❌ Errors compound over iterations ("confirmation bias")                 │
│                                                                             │
│   RECOMMENDED STRATEGY:                                                     │
│   ─────────────────────                                                     │
│   Start with HIGH threshold, gradually DECREASE it:                        │
│   τ = 0.99 → 0.95 → 0.90 → 0.85 → ...                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
4.3 The Confirmation Bias Problem
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                         CONFIRMATION BIAS IN SELF-TRAINING                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   THE PROBLEM:                                                              │
│   ────────────                                                              │
│   If the initial model makes a MISTAKE on an unlabeled sample,             │
│   and that mistake is added as a pseudo-label, the model will              │
│   REINFORCE that mistake in future iterations.                             │
│                                                                             │
│   EXAMPLE:                                                                  │
│   ────────                                                                  │
│   1. Model wrongly predicts sample X as Class A (confidence: 0.92)         │
│   2. X is added to training set with label "A"                             │
│   3. Model trains on this wrong label                                      │
│   4. Model becomes MORE confident that X is Class A                        │
│   5. Similar samples near X are also wrongly labeled                       │
│   6. Error propagates throughout the dataset!                              │
│                                                                             │
│   SOLUTIONS:                                                                │
│   ──────────                                                                │
│   • Use higher confidence thresholds                                       │
│   • Add samples gradually (few per iteration)                              │
│   • Use curriculum learning (easy samples first)                           │
│   • Combine with other SSL methods                                         │
│   • Periodically reset and retrain                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
4.4 Advanced Self-Training Variants
Curriculum Self-Training
Python

def curriculum_self_training(model, X_labeled, y_labeled, X_unlabeled,
                             initial_threshold=0.99, final_threshold=0.7,
                             decay_rate=0.95, max_iterations=50):
    """
    Curriculum Self-Training: Start conservative, become aggressive
    
    Key Idea: 
    - First iterations: Only add very confident predictions
    - Later iterations: Lower threshold to include more samples
    - This mimics human learning: easy concepts first, then harder ones
    """
    
    threshold = initial_threshold
    
    for iteration in range(max_iterations):
        # ... standard self-training steps ...
        
        # Decrease threshold over time
        threshold = max(final_threshold, threshold * decay_rate)
        
        print(f"Iteration {iteration}: threshold = {threshold:.3f}")
    
    return model
Class-Balanced Self-Training
Python

def class_balanced_self_training(model, X_labeled, y_labeled, X_unlabeled,
                                  threshold=0.9, samples_per_class=10):
    """
    Prevent class imbalance in pseudo-labels
    
    Problem: 
    - Model might be overconfident in one class
    - That class dominates pseudo-labels
    - Training becomes imbalanced
    
    Solution:
    - Select top-k confident samples PER CLASS
    - Ensures balanced pseudo-label distribution
    """
    
    probabilities = model.predict_proba(X_unlabeled)
    predictions = model.predict(X_unlabeled)
    
    selected_indices = []
    
    for class_label in np.unique(y_labeled):
        # Find samples predicted as this class
        class_mask = predictions == class_label
        class_probs = probabilities[class_mask, class_label]
        class_indices = np.where(class_mask)[0]
        
        # Select top-k most confident
        if len(class_indices) > 0:
            top_k = min(samples_per_class, len(class_indices))
            top_indices = class_indices[np.argsort(class_probs)[-top_k:]]
            selected_indices.extend(top_indices)
    
    return selected_indices
Chapter 5: Co-Training Approaches
5.1 The Co-Training Paradigm
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          CO-TRAINING CONCEPT                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   KEY IDEA:                                                                 │
│   ─────────                                                                 │
│   Train TWO (or more) classifiers on DIFFERENT VIEWS of the data.          │
│   Each classifier teaches the other by providing pseudo-labels.            │
│                                                                             │
│   REQUIREMENT:                                                              │
│   ────────────                                                              │
│   Data must have TWO (or more) REDUNDANT but INDEPENDENT views             │
│   (features that can each predict the label on their own)                  │
│                                                                             │
│   EXAMPLES OF NATURAL VIEWS:                                                │
│   ──────────────────────────                                                │
│   • Web pages: (text content) vs (anchor text of incoming links)           │
│   • Videos: (visual frames) vs (audio track)                               │
│   • Medical: (blood tests) vs (imaging results)                            │
│   • Products: (descriptions) vs (reviews)                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Explanation
text

                         CO-TRAINING PROCESS
                         
    ┌────────────────────────────────────────────────────────────────┐
    │                        ORIGINAL DATA                           │
    │                                                                │
    │  Each sample x has TWO views: x = (x^(1), x^(2))              │
    │                                                                │
    │  Example (Web Page):                                           │
    │  x^(1) = page text content                                    │
    │  x^(2) = text of links pointing to page                       │
    │                                                                │
    └────────────────────────────────────────────────────────────────┘
                                │
                    ┌───────────┴───────────┐
                    │                       │
                    ▼                       ▼
            ┌───────────────┐       ┌───────────────┐
            │   VIEW 1      │       │   VIEW 2      │
            │   Features    │       │   Features    │
            │   x^(1)       │       │   x^(2)       │
            └───────────────┘       └───────────────┘
                    │                       │
                    ▼                       ▼
            ┌───────────────┐       ┌───────────────┐
            │  Classifier   │       │  Classifier   │
            │     f₁        │       │     f₂        │
            └───────────────┘       └───────────────┘
                    │                       │
                    │    ┌─────────────┐    │
                    └───►│   EXCHANGE  │◄───┘
                         │   PSEUDO-   │
                         │   LABELS    │
                         └─────────────┘
                               │
                               ▼
                    ┌───────────────────────┐
                    │  f₁ confident on x?   │
                    │  Add f₁'s label to    │
                    │  f₂'s training set    │
                    │                       │
                    │  f₂ confident on x?   │
                    │  Add f₂'s label to    │
                    │  f₁'s training set    │
                    └───────────────────────┘
5.2 Original Co-Training Algorithm (Blum & Mitchell, 1998)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      CO-TRAINING ALGORITHM                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   INPUT:                                                                    │
│   ──────                                                                    │
│   • Labeled set L with views (x^(1), x^(2), y)                             │
│   • Unlabeled set U with views (x^(1), x^(2))                              │
│   • Pool size u' (samples to consider each iteration)                      │
│   • Growth parameters p, n (positives and negatives to add)                │
│   • Number of iterations k                                                 │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   1. Initialize:                                                           │
│      • Train f₁ on L using only view 1 features                           │
│      • Train f₂ on L using only view 2 features                           │
│                                                                             │
│   2. Create pool U' by randomly sampling u' examples from U                │
│                                                                             │
│   3. REPEAT k times:                                                       │
│      a. f₁ predicts labels for U' using view 1                            │
│      b. Select p most confident positive and n most confident              │
│         negative predictions from f₁                                       │
│      c. Add these to f₂'s training set (with pseudo-labels)               │
│      d. f₂ predicts labels for U' using view 2                            │
│      e. Select p most confident positive and n most confident              │
│         negative predictions from f₂                                       │
│      f. Add these to f₁'s training set (with pseudo-labels)               │
│      g. Retrain both f₁ and f₂                                            │
│      h. Replenish U' with samples from U                                  │
│                                                                             │
│   4. Combine f₁ and f₂ for final predictions                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Python Implementation
Python

import numpy as np
from sklearn.base import clone

def co_training(model1, model2, X_labeled_v1, X_labeled_v2, y_labeled,
                X_unlabeled_v1, X_unlabeled_v2, 
                pool_size=75, p=1, n=1, max_iterations=30):
    """
    Co-Training Algorithm
    
    Parameters:
    -----------
    model1, model2 : Base classifiers for each view
    X_labeled_v1 : Labeled data, view 1 features
    X_labeled_v2 : Labeled data, view 2 features
    y_labeled : Labels
    X_unlabeled_v1 : Unlabeled data, view 1 features
    X_unlabeled_v2 : Unlabeled data, view 2 features
    pool_size : Number of unlabeled samples to consider each iteration
    p : Number of positive samples to add per iteration
    n : Number of negative samples to add per iteration
    
    Returns:
    --------
    model1, model2 : Trained models
    """
    
    # Initialize training sets
    L1_X, L1_y = X_labeled_v1.copy(), y_labeled.copy()
    L2_X, L2_y = X_labeled_v2.copy(), y_labeled.copy()
    
    # Unlabeled pools (keep track with indices)
    U_v1, U_v2 = X_unlabeled_v1.copy(), X_unlabeled_v2.copy()
    
    for iteration in range(max_iterations):
        if len(U_v1) == 0:
            break
            
        # Train both classifiers
        clf1 = clone(model1).fit(L1_X, L1_y)
        clf2 = clone(model2).fit(L2_X, L2_y)
        
        # Create random pool
        pool_size_actual = min(pool_size, len(U_v1))
        pool_indices = np.random.choice(len(U_v1), pool_size_actual, replace=False)
        
        # Classifier 1 labels for Classifier 2
        probs1 = clf1.predict_proba(U_v1[pool_indices])
        
        # Find most confident positives and negatives
        pos_confidence = probs1[:, 1]  # Probability of class 1
        neg_confidence = probs1[:, 0]  # Probability of class 0
        
        top_pos_idx = pool_indices[np.argsort(pos_confidence)[-p:]]
        top_neg_idx = pool_indices[np.argsort(neg_confidence)[-n:]]
        
        # Add to classifier 2's training set
        L2_X = np.vstack([L2_X, U_v2[top_pos_idx], U_v2[top_neg_idx]])
        L2_y = np.concatenate([L2_y, np.ones(p), np.zeros(n)])
        
        # Classifier 2 labels for Classifier 1
        probs2 = clf2.predict_proba(U_v2[pool_indices])
        
        pos_confidence = probs2[:, 1]
        neg_confidence = probs2[:, 0]
        
        top_pos_idx = pool_indices[np.argsort(pos_confidence)[-p:]]
        top_neg_idx = pool_indices[np.argsort(neg_confidence)[-n:]]
        
        # Add to classifier 1's training set
        L1_X = np.vstack([L1_X, U_v1[top_pos_idx], U_v1[top_neg_idx]])
        L1_y = np.concatenate([L1_y, np.ones(p), np.zeros(n)])
        
        # Remove used samples from unlabeled pool
        used_indices = np.unique(np.concatenate([top_pos_idx, top_neg_idx]))
        mask = np.ones(len(U_v1), dtype=bool)
        mask[used_indices] = False
        U_v1 = U_v1[mask]
        U_v2 = U_v2[mask]
        
        print(f"Iteration {iteration}: L1 size = {len(L1_X)}, "
              f"L2 size = {len(L2_X)}, U size = {len(U_v1)}")
    
    # Final training
    model1 = clone(model1).fit(L1_X, L1_y)
    model2 = clone(model2).fit(L2_X, L2_y)
    
    return model1, model2
5.3 Multi-View Learning Assumption
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      MULTI-VIEW ASSUMPTION                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   For co-training to work, views must satisfy:                             │
│                                                                             │
│   1. SUFFICIENCY                                                            │
│      Each view alone is SUFFICIENT to learn a good classifier              │
│      Formally: P(Y | X^(1)) ≈ P(Y | X^(2)) ≈ P(Y | X)                      │
│                                                                             │
│   2. CONDITIONAL INDEPENDENCE                                               │
│      Views are INDEPENDENT given the class label                           │
│      Formally: P(X^(1) | X^(2), Y) = P(X^(1) | Y)                          │
│                                                                             │
│   INTUITION:                                                                │
│   ──────────                                                                │
│   • Each view captures different aspects of the same concept               │
│   • When f₁ is wrong on a sample, f₂ might be right (and vice versa)      │
│   • Views provide complementary information                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
5.4 When Natural Views Don't Exist
text

PROBLEM: Most datasets DON'T have natural view separation!

SOLUTION: CREATE ARTIFICIAL VIEWS

┌─────────────────────────────────────────────────────────────────────────────┐
│                      ARTIFICIAL VIEW CREATION                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   METHOD 1: Random Feature Split                                           │
│   ──────────────────────────────                                            │
│   • Randomly divide features into two groups                               │
│   • Each group becomes a view                                              │
│   • Simple but may not satisfy view assumptions                            │
│                                                                             │
│   METHOD 2: Different Representations                                       │
│   ───────────────────────────────────                                       │
│   • View 1: Raw features                                                   │
│   • View 2: Transformed features (PCA, embeddings, etc.)                   │
│                                                                             │
│   METHOD 3: Different Model Architectures (Tri-Training)                   │
│   ─────────────────────────────────────────────────────────                 │
│   • Instead of different features, use different models                    │
│   • Three diverse classifiers vote on pseudo-labels                        │
│                                                                             │
│   METHOD 4: Different Training Procedures                                  │
│   ───────────────────────────────────────                                   │
│   • Same architecture, different random seeds                              │
│   • Different regularization, dropout, etc.                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
5.5 Tri-Training
text

TRI-TRAINING: Co-training without view separation

┌─────────────────────────────────────────────────────────────────────────────┐
│                        TRI-TRAINING ALGORITHM                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   IDEA: Train THREE classifiers. If TWO agree, they teach the THIRD.       │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   1. Train three classifiers h₁, h₂, h₃ on labeled data                   │
│      (use different random seeds or different algorithms)                  │
│                                                                             │
│   2. REPEAT until no changes:                                              │
│      For each classifier hᵢ (i ∈ {1, 2, 3}):                              │
│        a. For each unlabeled sample x:                                     │
│           If h_j(x) == h_k(x) (the OTHER two agree):                      │
│             Add (x, h_j(x)) to hᵢ's training set                          │
│        b. Retrain hᵢ on expanded training set                            │
│                                                                             │
│   3. Final prediction: Majority vote of h₁, h₂, h₃                        │
│                                                                             │
│   ADVANTAGES:                                                               │
│   ───────────                                                               │
│   • No need for separate views                                             │
│   • More robust (requires 2/3 agreement)                                   │
│   • Works with any classifier                                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 6: Graph-Based Methods
6.1 The Graph Perspective
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    GRAPH-BASED SEMI-SUPERVISED LEARNING                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CORE IDEA:                                                                │
│   ──────────                                                                │
│   Represent data as a GRAPH where:                                         │
│   • Nodes = Data points (both labeled and unlabeled)                       │
│   • Edges = Similarity between points                                      │
│   • Edge weights = Degree of similarity                                    │
│                                                                             │
│   Then PROPAGATE labels through the graph!                                 │
│                                                                             │
│   INTUITION:                                                                │
│   ──────────                                                                │
│   "Similar points should have similar labels"                              │
│   "Labels flow from labeled points to unlabeled neighbors"                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Example
text

BEFORE LABEL PROPAGATION:
─────────────────────────

         ● ─── ○ ─── ○ ─── ○
          ╲     ╲     ╲
           ○ ─── ○ ─── ○
            ╲     ╲     
             ○ ─── ○ ─── ▲

  ● = Labeled (Class A)
  ▲ = Labeled (Class B)  
  ○ = Unlabeled
  Lines = Edges (similarity connections)


AFTER LABEL PROPAGATION:
────────────────────────

         ● ─── ● ─── ● ─── ●
          ╲     ╲     ╲
           ● ─── ● ─── ●
            ╲     ╲     
             ▲ ─── ▲ ─── ▲

  Labels have propagated through the graph!
  Upper region → Class A
  Lower region → Class B
6.2 Building the Graph
Step 1: Construct Similarity Graph
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                        GRAPH CONSTRUCTION METHODS                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   METHOD 1: k-Nearest Neighbors (k-NN) Graph                               │
│   ────────────────────────────────────────────                              │
│   • Connect each point to its k nearest neighbors                          │
│   • Edge weight = 1 (unweighted) or based on distance                      │
│   • Parameter: k (typically 5-20)                                          │
│                                                                             │
│   METHOD 2: ε-Neighborhood Graph                                           │
│   ───────────────────────────────                                           │
│   • Connect points within distance ε of each other                         │
│   • Parameter: ε (radius threshold)                                        │
│                                                                             │
│   METHOD 3: Fully Connected Graph with Gaussian Weights                    │
│   ────────────────────────────────────────────────────                      │
│   • Connect ALL points to ALL other points                                 │
│   • Edge weight = exp(-||xᵢ - xⱼ||² / 2σ²)                                │
│   • Parameter: σ (kernel bandwidth)                                        │
│   • High similarity → weight ≈ 1, Low similarity → weight ≈ 0             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Computing the Weight Matrix
Python

import numpy as np
from scipy.spatial.distance import cdist

def compute_weight_matrix(X, method='gaussian', k=10, sigma=1.0, epsilon=1.0):
    """
    Compute the weight matrix W for the graph
    
    Parameters:
    -----------
    X : Data matrix (n_samples, n_features)
    method : 'knn', 'epsilon', or 'gaussian'
    k : Number of neighbors for k-NN
    sigma : Bandwidth for Gaussian kernel
    epsilon : Radius for epsilon-neighborhood
    
    Returns:
    --------
    W : Weight matrix (n_samples, n_samples)
    """
    
    n = len(X)
    distances = cdist(X, X, metric='euclidean')
    
    if method == 'knn':
        W = np.zeros((n, n))
        for i in range(n):
            # Find k nearest neighbors
            knn_indices = np.argsort(distances[i])[1:k+1]  # Exclude self
            W[i, knn_indices] = 1
        # Make symmetric
        W = np.maximum(W, W.T)
        
    elif method == 'epsilon':
        W = (distances < epsilon).astype(float)
        np.fill_diagonal(W, 0)
        
    elif method == 'gaussian':
        W = np.exp(-distances**2 / (2 * sigma**2))
        np.fill_diagonal(W, 0)
    
    return W


# EXAMPLE:
X = np.random.randn(100, 5)
W_knn = compute_weight_matrix(X, method='knn', k=10)
W_gaussian = compute_weight_matrix(X, method='gaussian', sigma=1.0)

print(f"k-NN graph has {np.sum(W_knn > 0)} edges")
print(f"Gaussian graph: Average weight = {W_gaussian.mean():.4f}")
6.3 Label Propagation
The Algorithm
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      LABEL PROPAGATION ALGORITHM                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   SETUP:                                                                    │
│   ──────                                                                    │
│   • n total points (l labeled, u = n - l unlabeled)                        │
│   • Weight matrix W (n × n)                                                │
│   • Initial labels Y⁽⁰⁾ (n × C matrix, C = number of classes)              │
│     - Labeled points: one-hot encoding                                     │
│     - Unlabeled points: zeros (or uniform distribution)                    │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   1. Compute transition matrix: T = D⁻¹W                                   │
│      where D = diag(d₁, d₂, ..., dₙ), dᵢ = Σⱼ wᵢⱼ                         │
│                                                                             │
│   2. REPEAT until convergence:                                             │
│      a. Propagate: Y⁽ᵗ⁺¹⁾ = T · Y⁽ᵗ⁾                                       │
│      b. Clamp labeled points: Y⁽ᵗ⁺¹⁾[labeled] = Y⁽⁰⁾[labeled]              │
│                                                                             │
│   3. Final prediction: argmax over classes for each point                  │
│                                                                             │
│   INTUITION:                                                                │
│   ──────────                                                                │
│   Each point's label becomes a weighted average of its neighbors' labels   │
│   Labeled points stay fixed and "anchor" the propagation                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Python Implementation
Python

import numpy as np

def label_propagation(W, labels, labeled_mask, n_classes, max_iter=1000, tol=1e-6):
    """
    Label Propagation Algorithm
    
    Parameters:
    -----------
    W : Weight matrix (n × n)
    labels : Initial labels (n,) - unlabeled points can be -1 or any value
    labeled_mask : Boolean array indicating which points are labeled
    n_classes : Number of classes
    max_iter : Maximum iterations
    tol : Convergence tolerance
    
    Returns:
    --------
    predictions : Final predicted labels for all points
    Y : Final label distribution matrix
    """
    
    n = len(labels)
    
    # Initialize Y matrix
    Y = np.zeros((n, n_classes))
    for i in range(n):
        if labeled_mask[i]:
            Y[i, labels[i]] = 1.0  # One-hot for labeled
        else:
            Y[i, :] = 1.0 / n_classes  # Uniform for unlabeled
    
    # Store original labels for clamping
    Y_original = Y.copy()
    
    # Compute transition matrix T = D^(-1) W
    D = np.diag(np.sum(W, axis=1))
    D_inv = np.linalg.inv(D + 1e-10 * np.eye(n))  # Add small value for stability
    T = D_inv @ W
    
    # Iterate
    for iteration in range(max_iter):
        Y_new = T @ Y
        
        # Clamp labeled points
        Y_new[labeled_mask] = Y_original[labeled_mask]
        
        # Check convergence
        diff = np.abs(Y_new - Y).max()
        Y = Y_new
        
        if diff < tol:
            print(f"Converged at iteration {iteration}")
            break
    
    # Final predictions
    predictions = np.argmax(Y, axis=1)
    
    return predictions, Y


# EXAMPLE USAGE:
np.random.seed(42)

# Generate data: two clusters
n_per_cluster = 50
X1 = np.random.randn(n_per_cluster, 2) + np.array([0, 0])
X2 = np.random.randn(n_per_cluster, 2) + np.array([4, 4])
X = np.vstack([X1, X2])

# True labels
true_labels = np.array([0] * n_per_cluster + [1] * n_per_cluster)

# Only label 2 points per class
labeled_mask = np.zeros(len(X), dtype=bool)
labeled_mask[0] = labeled_mask[1] = True      # Two Class 0 labels
labeled_mask[50] = labeled_mask[51] = True    # Two Class 1 labels

labels = true_labels.copy()

# Build graph
W = compute_weight_matrix(X, method='gaussian', sigma=1.0)

# Run label propagation
predictions, Y_dist = label_propagation(W, labels, labeled_mask, n_classes=2)

# Evaluate
accuracy = np.mean(predictions == true_labels)
print(f"Accuracy: {accuracy:.4f}")  # Should be very high!
6.4 Label Spreading
text

┌─────────────────────────────────────────────────────────────────────────────┐
│            LABEL SPREADING vs LABEL PROPAGATION                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   LABEL PROPAGATION:                                                        │
│   ──────────────────                                                        │
│   • Hard clamping: labeled points NEVER change                             │
│   • Can be sensitive to labeling errors                                    │
│   • Iteration: Y⁽ᵗ⁺¹⁾ = TY⁽ᵗ⁾, then clamp                                 │
│                                                                             │
│   LABEL SPREADING:                                                          │
│   ─────────────────                                                         │
│   • Soft clamping: labeled points can change slightly                      │
│   • More robust to noise in labels                                         │
│   • Iteration: Y⁽ᵗ⁺¹⁾ = αSY⁽ᵗ⁾ + (1-α)Y⁽⁰⁾                                 │
│     where S = D^(-1/2) W D^(-1/2) (normalized Laplacian)                   │
│     and α controls clamping strength (α=1: no clamping, α=0: hard clamp)  │
│                                                                             │
│   RECOMMENDATION:                                                           │
│   ───────────────                                                           │
│   • Clean labels → Label Propagation                                       │
│   • Noisy labels → Label Spreading with α ≈ 0.2                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
6.5 The Graph Laplacian
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                         GRAPH LAPLACIAN                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   DEFINITION:                                                               │
│   ───────────                                                               │
│   L = D - W                                                                │
│                                                                             │
│   where:                                                                    │
│   • W = weight matrix                                                      │
│   • D = degree matrix = diag(Σⱼ wᵢⱼ)                                       │
│                                                                             │
│   NORMALIZED VERSIONS:                                                      │
│   ────────────────────                                                      │
│   • Symmetric: Lₛ = I - D^(-1/2) W D^(-1/2)                               │
│   • Random Walk: Lᵣᵥ = I - D^(-1) W                                       │
│                                                                             │
│   KEY PROPERTY:                                                             │
│   ─────────────                                                             │
│   For any function f on nodes:                                             │
│                                                                             │
│   f^T L f = Σᵢⱼ wᵢⱼ (fᵢ - fⱼ)²                                            │
│                                                                             │
│   This measures SMOOTHNESS! Small value = similar nodes have similar f     │
│                                                                             │
│   SSL OBJECTIVE:                                                            │
│   ──────────────                                                            │
│   Minimize: Σᵢⱼ wᵢⱼ (ŷᵢ - ŷⱼ)² + λ Σᵢ∈labeled (ŷᵢ - yᵢ)²                  │
│                                                                             │
│   Translation: Be smooth on the graph + Match known labels                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
6.6 Practical Considerations
text

CHOOSING GRAPH CONSTRUCTION PARAMETERS:

┌─────────────────────────────────────────────────────────────────────────────┐
│  PARAMETER        │ TOO SMALL                │ TOO LARGE                   │
├───────────────────┼──────────────────────────┼─────────────────────────────┤
│                   │                          │                             │
│  k (k-NN)         │ Disconnected graph       │ Over-smooth, lose detail    │
│                   │ Labels can't propagate   │ All points similar          │
│  Typical: 5-20    │                          │                             │
│                   │                          │                             │
│  σ (Gaussian)     │ All weights ≈ 0          │ All weights ≈ 1             │
│                   │ No propagation           │ No structure                │
│  Typical: median  │                          │                             │
│  of distances     │                          │                             │
│                   │                          │                             │
│  ε (ε-neighbor)   │ Sparse/disconnected      │ Dense/all connected         │
│                   │ graph                    │                             │
│                   │                          │                             │
└───────────────────┴──────────────────────────┴─────────────────────────────┘

TIPS:
• Use cross-validation on labeled data to tune parameters
• Try multiple parameter values and ensemble results
• Scale features before computing distances
• Consider using local scaling (different σ for different regions)
Chapter 7: Generative Models
7.1 The Generative Approach
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    GENERATIVE VS DISCRIMINATIVE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   DISCRIMINATIVE MODELS (e.g., Logistic Regression, SVM):                  │
│   ────────────────────────────────────────────────────────                  │
│   • Directly model P(Y|X) - probability of label given features            │
│   • Learn decision boundary                                                │
│   • Don't model how data is generated                                      │
│                                                                             │
│   GENERATIVE MODELS (e.g., Naive Bayes, GMM):                              │
│   ─────────────────────────────────────────────                             │
│   • Model P(X|Y) - probability of features given label                     │
│   • Model P(Y) - prior probability of each class                           │
│   • Use Bayes' rule: P(Y|X) = P(X|Y)P(Y) / P(X)                            │
│   • Model how data is GENERATED                                            │
│                                                                             │
│   WHY GENERATIVE FOR SSL?                                                   │
│   ───────────────────────                                                   │
│   • P(X) contains information about data structure                         │
│   • Unlabeled data helps estimate P(X)                                     │
│   • Better P(X) estimate → Better classification                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
7.2 Gaussian Mixture Models for SSL
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                  SEMI-SUPERVISED GMM                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   MODEL ASSUMPTION:                                                         │
│   ─────────────────                                                         │
│   • Data from each class follows a Gaussian distribution                   │
│   • P(X|Y=k) = N(X | μₖ, Σₖ)                                               │
│   • Total data distribution is a mixture:                                  │
│     P(X) = Σₖ πₖ N(X | μₖ, Σₖ)                                             │
│                                                                             │
│   PARAMETERS TO LEARN:                                                      │
│   ────────────────────                                                      │
│   • μₖ = mean of class k                                                   │
│   • Σₖ = covariance matrix of class k                                      │
│   • πₖ = prior probability of class k                                      │
│                                                                             │
│   SSL APPROACH:                                                             │
│   ─────────────                                                             │
│   • Labeled data: directly contributes to class k's Gaussian               │
│   • Unlabeled data: probabilistically assigned to classes (EM algorithm)  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

Chapter 7: Generative Models (Continued)
Visual Representation (Continued)
text

                    SEMI-SUPERVISED GMM LEARNING

    Step 1: Initialize with labeled data
    ────────────────────────────────────
    
              ○ ○ ○           ○ ○ ○
           ○ ○ ○ ○ ○       ○ ○ ○ ○ ○
          ○ ○ ● ○ ○ ○     ○ ○ ○ ▲ ○ ○
           ○ ○ ○ ○ ○       ○ ○ ○ ○ ○
              ○ ○ ○           ○ ○ ○
    
    ● = labeled Class A    ▲ = labeled Class B    ○ = unlabeled


    Step 2: Fit initial Gaussians to labeled points
    ────────────────────────────────────────────────
    
           ┌─────────┐         ┌─────────┐
           │  ○ ○ ○  │         │  ○ ○ ○  │
           │○ ○ ○ ○ ○│         │○ ○ ○ ○ ○│
           │○ ○ ● ○ ○│ ○       │○ ○ ○ ▲ ○│ ○
           │ ○ ○ ○ ○ │○        │ ○ ○ ○ ○ │○
           │   ○ ○ ○ │         │   ○ ○ ○ │
           └─────────┘         └─────────┘
              μ₁, Σ₁              μ₂, Σ₂


    Step 3: E-Step - Assign unlabeled to clusters probabilistically
    ─────────────────────────────────────────────────────────────────
    
           ┌───────────┐       ┌───────────┐
           │  ● ● ●    │       │    ▲ ▲ ▲  │
           │● ● ● ● ●  │       │  ▲ ▲ ▲ ▲ ▲│
           │● ● ● ● ●  │  ?    │  ▲ ▲ ▲ ▲ ▲│
           │ ● ● ● ●   │  ?    │   ▲ ▲ ▲ ▲ │
           │   ● ● ●   │       │     ▲ ▲ ▲ │
           └───────────┘       └───────────┘
    
    ? = uncertain points (between clusters)


    Step 4: M-Step - Update Gaussians using all assignments
    ─────────────────────────────────────────────────────────
    
           ┌─────────────┐     ┌─────────────┐
           │    ● ● ●    │     │    ▲ ▲ ▲    │
           │  ● ● ● ● ●  │     │  ▲ ▲ ▲ ▲ ▲  │
           │  ● ● ● ● ●  │     │  ▲ ▲ ▲ ▲ ▲  │
           │   ● ● ● ●   │     │   ▲ ▲ ▲ ▲   │
           │     ● ● ●   │     │     ▲ ▲ ▲   │
           └─────────────┘     └─────────────┘
              μ₁', Σ₁'            μ₂', Σ₂'
    
    Better Gaussian estimates using unlabeled data!
EM Algorithm for Semi-Supervised GMM
text

┌─────────────────────────────────────────────────────────────────────────────┐
│              EM ALGORITHM FOR SEMI-SUPERVISED GMM                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   NOTATION:                                                                 │
│   ─────────                                                                 │
│   • D_L = {(xᵢ, yᵢ)} : Labeled data                                        │
│   • D_U = {xⱼ} : Unlabeled data                                            │
│   • K = number of classes                                                  │
│   • θ = {μₖ, Σₖ, πₖ} for k = 1,...,K                                       │
│                                                                             │
│   E-STEP (Expectation):                                                     │
│   ─────────────────────                                                     │
│   For labeled data: γᵢₖ = 1 if yᵢ = k, else 0                              │
│                                                                             │
│   For unlabeled data:                                                       │
│   γⱼₖ = P(Y=k|xⱼ,θ) = πₖ N(xⱼ|μₖ,Σₖ) / Σₘ πₘ N(xⱼ|μₘ,Σₘ)                  │
│                                                                             │
│   M-STEP (Maximization):                                                    │
│   ──────────────────────                                                    │
│   Nₖ = Σᵢ γᵢₖ + Σⱼ γⱼₖ  (effective count for class k)                     │
│                                                                             │
│   μₖ = (1/Nₖ) [Σᵢ γᵢₖ xᵢ + Σⱼ γⱼₖ xⱼ]                                      │
│                                                                             │
│   Σₖ = (1/Nₖ) [Σᵢ γᵢₖ(xᵢ-μₖ)(xᵢ-μₖ)ᵀ + Σⱼ γⱼₖ(xⱼ-μₖ)(xⱼ-μₖ)ᵀ]            │
│                                                                             │
│   πₖ = Nₖ / (|D_L| + |D_U|)                                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Python Implementation
Python

import numpy as np
from scipy.stats import multivariate_normal

class SemiSupervisedGMM:
    """
    Semi-Supervised Gaussian Mixture Model
    
    Uses EM algorithm to learn from both labeled and unlabeled data.
    """
    
    def __init__(self, n_classes, max_iter=100, tol=1e-6):
        self.n_classes = n_classes
        self.max_iter = max_iter
        self.tol = tol
        
        # Parameters
        self.means = None      # μₖ for each class
        self.covs = None       # Σₖ for each class
        self.priors = None     # πₖ for each class
        
    def _initialize_parameters(self, X_labeled, y_labeled, X_unlabeled):
        """Initialize parameters from labeled data"""
        n_features = X_labeled.shape[1]
        
        self.means = np.zeros((self.n_classes, n_features))
        self.covs = np.zeros((self.n_classes, n_features, n_features))
        self.priors = np.zeros(self.n_classes)
        
        for k in range(self.n_classes):
            mask = y_labeled == k
            if np.sum(mask) > 0:
                self.means[k] = X_labeled[mask].mean(axis=0)
                # Add regularization for stability
                self.covs[k] = np.cov(X_labeled[mask].T) + 1e-6 * np.eye(n_features)
            else:
                # Random initialization if no labeled samples
                self.means[k] = X_unlabeled[np.random.randint(len(X_unlabeled))]
                self.covs[k] = np.eye(n_features)
            
            self.priors[k] = np.sum(mask) / len(y_labeled)
        
        # Ensure priors sum to 1
        self.priors = np.maximum(self.priors, 1e-6)
        self.priors /= self.priors.sum()
    
    def _compute_responsibilities(self, X, y=None):
        """
        E-Step: Compute responsibilities (soft assignments)
        
        For labeled data: hard assignment (gamma = 1 for correct class)
        For unlabeled data: soft assignment based on current parameters
        """
        n_samples = len(X)
        gamma = np.zeros((n_samples, self.n_classes))
        
        if y is not None:
            # Labeled data: hard assignment
            for i, label in enumerate(y):
                gamma[i, label] = 1.0
        else:
            # Unlabeled data: soft assignment
            for k in range(self.n_classes):
                try:
                    gamma[:, k] = self.priors[k] * multivariate_normal.pdf(
                        X, mean=self.means[k], cov=self.covs[k]
                    )
                except:
                    gamma[:, k] = 1e-10
            
            # Normalize
            gamma_sum = gamma.sum(axis=1, keepdims=True)
            gamma_sum = np.maximum(gamma_sum, 1e-10)
            gamma = gamma / gamma_sum
        
        return gamma
    
    def _update_parameters(self, X_all, gamma_all):
        """
        M-Step: Update parameters based on responsibilities
        """
        n_features = X_all.shape[1]
        
        for k in range(self.n_classes):
            # Effective count
            Nk = gamma_all[:, k].sum()
            
            if Nk > 1e-6:
                # Update mean
                self.means[k] = (gamma_all[:, k:k+1].T @ X_all).flatten() / Nk
                
                # Update covariance
                diff = X_all - self.means[k]
                self.covs[k] = (gamma_all[:, k:k+1] * diff).T @ diff / Nk
                self.covs[k] += 1e-6 * np.eye(n_features)  # Regularization
                
                # Update prior
                self.priors[k] = Nk / len(X_all)
        
        # Normalize priors
        self.priors /= self.priors.sum()
    
    def fit(self, X_labeled, y_labeled, X_unlabeled):
        """
        Fit the semi-supervised GMM
        
        Parameters:
        -----------
        X_labeled : Labeled feature matrix
        y_labeled : Labels (integers 0 to n_classes-1)
        X_unlabeled : Unlabeled feature matrix
        """
        # Initialize
        self._initialize_parameters(X_labeled, y_labeled, X_unlabeled)
        
        # Combine data
        X_all = np.vstack([X_labeled, X_unlabeled])
        n_labeled = len(X_labeled)
        
        prev_log_likelihood = -np.inf
        
        for iteration in range(self.max_iter):
            # E-Step
            gamma_labeled = self._compute_responsibilities(X_labeled, y_labeled)
            gamma_unlabeled = self._compute_responsibilities(X_unlabeled)
            gamma_all = np.vstack([gamma_labeled, gamma_unlabeled])
            
            # M-Step
            self._update_parameters(X_all, gamma_all)
            
            # Compute log-likelihood (for convergence check)
            log_likelihood = self._compute_log_likelihood(X_all)
            
            # Check convergence
            if abs(log_likelihood - prev_log_likelihood) < self.tol:
                print(f"Converged at iteration {iteration}")
                break
            
            prev_log_likelihood = log_likelihood
        
        return self
    
    def _compute_log_likelihood(self, X):
        """Compute log-likelihood of data"""
        ll = 0
        for k in range(self.n_classes):
            try:
                ll += self.priors[k] * multivariate_normal.pdf(
                    X, mean=self.means[k], cov=self.covs[k]
                )
            except:
                pass
        return np.log(ll + 1e-10).sum()
    
    def predict(self, X):
        """Predict class labels"""
        gamma = self._compute_responsibilities(X)
        return np.argmax(gamma, axis=1)
    
    def predict_proba(self, X):
        """Predict class probabilities"""
        return self._compute_responsibilities(X)


# EXAMPLE USAGE:
np.random.seed(42)

# Generate data
n_per_class = 100
X0 = np.random.randn(n_per_class, 2) + np.array([0, 0])
X1 = np.random.randn(n_per_class, 2) + np.array([4, 4])
X = np.vstack([X0, X1])
y = np.array([0]*n_per_class + [1]*n_per_class)

# Simulate SSL scenario: only 5 labels per class
n_labeled = 5
labeled_idx = np.concatenate([
    np.random.choice(n_per_class, n_labeled, replace=False),
    np.random.choice(n_per_class, n_labeled, replace=False) + n_per_class
])
unlabeled_idx = np.setdiff1d(np.arange(len(X)), labeled_idx)

X_labeled = X[labeled_idx]
y_labeled = y[labeled_idx]
X_unlabeled = X[unlabeled_idx]
y_unlabeled = y[unlabeled_idx]  # For evaluation only

# Fit model
model = SemiSupervisedGMM(n_classes=2)
model.fit(X_labeled, y_labeled, X_unlabeled)

# Evaluate
predictions = model.predict(X_unlabeled)
accuracy = np.mean(predictions == y_unlabeled)
print(f"Accuracy: {accuracy:.4f}")
7.3 When Generative Models Work Best
text

┌─────────────────────────────────────────────────────────────────────────────┐
│              GENERATIVE MODELS: WHEN TO USE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ✅ WORKS WELL WHEN:                                                       │
│   ───────────────────                                                       │
│   • Model assumptions match data (e.g., data IS Gaussian)                  │
│   • Very few labeled samples (generative better with tiny data)            │
│   • Classes are well-separated                                             │
│   • Features are continuous                                                │
│   • You need probability estimates                                         │
│                                                                             │
│   ❌ DOESN'T WORK WELL WHEN:                                                │
│   ──────────────────────────                                                │
│   • Model assumptions don't match (non-Gaussian data)                      │
│   • Complex decision boundaries needed                                     │
│   • High-dimensional data (curse of dimensionality)                        │
│   • Features have complex dependencies                                     │
│                                                                             │
│   DANGER ZONE:                                                              │
│   ────────────                                                              │
│   If model assumptions are WRONG, unlabeled data can HURT performance!     │
│   The model will fit the wrong structure and propagate errors.             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 8: Low-Density Separation Methods
8.1 The Core Idea
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                     LOW-DENSITY SEPARATION                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   PRINCIPLE:                                                                │
│   ──────────                                                                │
│   "Decision boundaries should pass through LOW-DENSITY regions"            │
│   "Don't cut through clusters of points!"                                  │
│                                                                             │
│   THIS IS EQUIVALENT TO:                                                    │
│   ──────────────────────                                                    │
│   • Cluster assumption                                                     │
│   • Points near boundary should be uncertain                               │
│   • Points far from boundary should be confident                           │
│                                                                             │
│   HOW TO ACHIEVE THIS:                                                      │
│   ────────────────────                                                      │
│   Push the decision boundary AWAY from unlabeled data points               │
│   = Maximize margin in regions with data                                   │
│   = Encourage confident predictions on unlabeled data                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Explanation
text

    SUPERVISED ONLY (ignores unlabeled data):
    ─────────────────────────────────────────
    
         ●                    ▲
           ●        │       ▲
         ●   ●      │     ▲   ▲
              ○ ○ ○ │ ○ ○ ○
            ○ ○ ○ ○ │ ○ ○ ○ ○
           ○ ○ ○ ○ ○│○ ○ ○ ○ ○
            ○ ○ ○ ○ │ ○ ○ ○ ○
              ○ ○ ○ │ ○ ○ ○
    
    Boundary cuts through unlabeled cluster! ❌


    LOW-DENSITY SEPARATION (uses unlabeled):
    ─────────────────────────────────────────
    
         ●                    ▲
           ●              │ ▲
         ●   ●            │▲   ▲
              ● ● ●       │▲ ▲ ▲
            ● ● ● ●       │▲ ▲ ▲ ▲
           ● ● ● ● ●      │▲ ▲ ▲ ▲ ▲
            ● ● ● ●       │▲ ▲ ▲ ▲
              ● ● ●       │ ▲ ▲ ▲
    
    Boundary passes through gap (low-density)! ✅
    Unlabeled points now have high-confidence predictions
8.2 Transductive SVM (TSVM)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                     TRANSDUCTIVE SVM (TSVM)                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   IDEA:                                                                     │
│   ─────                                                                     │
│   Standard SVM + "unlabeled points should be far from boundary"            │
│                                                                             │
│   STANDARD SVM OBJECTIVE:                                                   │
│   ───────────────────────                                                   │
│   min  ½||w||² + C Σᵢ ξᵢ                                                   │
│   s.t. yᵢ(w·xᵢ + b) ≥ 1 - ξᵢ  for labeled (xᵢ, yᵢ)                        │
│                                                                             │
│   TSVM OBJECTIVE (add unlabeled constraint):                               │
│   ───────────────────────────────────────────                               │
│   min  ½||w||² + C Σᵢ ξᵢ + C* Σⱼ ξⱼ*                                       │
│   s.t. yᵢ(w·xᵢ + b) ≥ 1 - ξᵢ      for labeled (xᵢ, yᵢ)                    │
│        ŷⱼ(w·xⱼ + b) ≥ 1 - ξⱼ*     for unlabeled xⱼ                        │
│                                                                             │
│   where ŷⱼ ∈ {-1, +1} are the UNKNOWN labels we're trying to find!        │
│                                                                             │
│   OPTIMIZATION CHALLENGE:                                                   │
│   ───────────────────────                                                   │
│   • Must find both w, b AND the labels ŷⱼ                                 │
│   • Combinatorial problem (2^|unlabeled| possible labelings)              │
│   • Various heuristics used in practice                                    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
TSVM Algorithm
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      TSVM ALGORITHM (Simplified)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. Train initial SVM on labeled data only                                │
│                                                                             │
│   2. Assign initial labels to unlabeled data:                              │
│      ŷⱼ = sign(w·xⱼ + b)                                                   │
│                                                                             │
│   3. Start with very small C* (unlabeled weight)                           │
│                                                                             │
│   4. REPEAT:                                                                │
│      a. Train SVM with current labels (labeled + pseudo-labeled)           │
│      b. Find unlabeled points that violate margin                          │
│      c. If two points of opposite labels both violate:                     │
│         - Try swapping their labels                                        │
│         - Keep swap if it improves objective                               │
│      d. Gradually increase C*                                              │
│                                                                             │
│   5. UNTIL no more beneficial swaps                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
8.3 Entropy Minimization
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      ENTROPY MINIMIZATION                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   KEY INSIGHT:                                                              │
│   ────────────                                                              │
│   • Low-density separation ↔ Confident predictions                         │
│   • Confident prediction ↔ Low entropy                                     │
│   • Therefore: MINIMIZE ENTROPY on unlabeled data!                         │
│                                                                             │
│   ENTROPY FORMULA:                                                          │
│   ────────────────                                                          │
│   H(p) = -Σₖ pₖ log(pₖ)                                                    │
│                                                                             │
│   where p = model's predicted probability distribution over classes        │
│                                                                             │
│   EXAMPLES:                                                                 │
│   ─────────                                                                 │
│   • Confident: p = [0.99, 0.01] → H ≈ 0.056 (LOW ✓)                       │
│   • Uncertain: p = [0.50, 0.50] → H = 0.693 (HIGH ✗)                      │
│                                                                             │
│   SSL OBJECTIVE:                                                            │
│   ──────────────                                                            │
│   L = L_supervised + λ · L_entropy                                         │
│                                                                             │
│   L_supervised = Σᵢ∈labeled CrossEntropy(f(xᵢ), yᵢ)                        │
│   L_entropy = Σⱼ∈unlabeled H(f(xⱼ))                                        │
│                                                                             │
│   "Fit labeled data + Make confident predictions on unlabeled"             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Understanding of Entropy
text

                    ENTROPY VISUALIZATION
    
    Probability Distribution          Entropy Value
    
    ┌─────────────────────────┐
    │████████████████████░░░░░│  p = [0.8, 0.2]   H = 0.50
    │█████████████████████████│
    │ Very Confident          │
    └─────────────────────────┘
    
    ┌─────────────────────────┐
    │████████████░░░░░░░░░░░░░│  p = [0.5, 0.5]   H = 0.69 (MAX)
    │█████████████████████████│
    │ Maximally Uncertain     │
    └─────────────────────────┘
    
    ┌─────────────────────────┐
    │██████████████████████░░░│  p = [0.9, 0.1]   H = 0.33
    │█████████████████████████│
    │ Confident               │
    └─────────────────────────┘
    
    ┌─────────────────────────┐
    │█████████████████████████│  p = [0.99, 0.01] H = 0.06 (MIN)
    │█████████████████████████│░
    │ Extremely Confident     │
    └─────────────────────────┘
    
    GOAL: Push predictions toward confident (low entropy) states!
Python Implementation
Python

import torch
import torch.nn as nn
import torch.nn.functional as F

class EntropyMinimizationLoss(nn.Module):
    """
    Entropy Minimization for Semi-Supervised Learning
    
    Encourages model to make confident predictions on unlabeled data.
    """
    
    def __init__(self, lambda_entropy=0.1):
        super().__init__()
        self.lambda_entropy = lambda_entropy
    
    def forward(self, logits_labeled, labels, logits_unlabeled):
        """
        Compute combined loss
        
        Parameters:
        -----------
        logits_labeled : Model output for labeled data (N_l, C)
        labels : True labels for labeled data (N_l,)
        logits_unlabeled : Model output for unlabeled data (N_u, C)
        
        Returns:
        --------
        total_loss : Combined supervised + entropy loss
        """
        
        # Supervised loss (standard cross-entropy)
        loss_supervised = F.cross_entropy(logits_labeled, labels)
        
        # Entropy loss on unlabeled data
        probs_unlabeled = F.softmax(logits_unlabeled, dim=1)
        log_probs = F.log_softmax(logits_unlabeled, dim=1)
        
        # Entropy: H = -Σ p * log(p)
        entropy = -(probs_unlabeled * log_probs).sum(dim=1)
        loss_entropy = entropy.mean()
        
        # Combined loss
        total_loss = loss_supervised + self.lambda_entropy * loss_entropy
        
        return total_loss, loss_supervised, loss_entropy


# USAGE IN TRAINING LOOP:
def train_with_entropy_minimization(model, optimizer, 
                                     X_labeled, y_labeled, X_unlabeled,
                                     lambda_entropy=0.1, epochs=100):
    """
    Train model with entropy minimization
    """
    criterion = EntropyMinimizationLoss(lambda_entropy)
    
    for epoch in range(epochs):
        model.train()
        optimizer.zero_grad()
        
        # Forward pass
        logits_labeled = model(X_labeled)
        logits_unlabeled = model(X_unlabeled)
        
        # Compute loss
        total_loss, sup_loss, ent_loss = criterion(
            logits_labeled, y_labeled, logits_unlabeled
        )
        
        # Backward pass
        total_loss.backward()
        optimizer.step()
        
        if epoch % 10 == 0:
            print(f"Epoch {epoch}: Total={total_loss:.4f}, "
                  f"Sup={sup_loss:.4f}, Ent={ent_loss:.4f}")
    
    return model
Chapter 9: Modern Deep Semi-Supervised Learning
9.1 The Deep Learning Revolution in SSL
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                   WHY DEEP LEARNING + SSL?                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   TRADITIONAL SSL LIMITATIONS:                                              │
│   ────────────────────────────                                              │
│   • Required hand-crafted features                                         │
│   • Struggled with high-dimensional data (images, text)                    │
│   • Graph methods didn't scale well                                        │
│   • Generative models had strong assumptions                               │
│                                                                             │
│   DEEP LEARNING BRINGS:                                                     │
│   ──────────────────────                                                    │
│   • Automatic feature learning                                             │
│   • Scales to millions of samples                                          │
│   • Works with images, text, audio directly                                │
│   • Can learn complex decision boundaries                                  │
│   • Natural integration with SSL techniques                                │
│                                                                             │
│   KEY INSIGHT:                                                              │
│   ────────────                                                              │
│   Deep networks learn REPRESENTATIONS                                       │
│   Good representations make SSL assumptions more likely to hold!           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
9.2 Neural Network SSL Framework
text

                    DEEP SSL ARCHITECTURE
    
    ┌─────────────────────────────────────────────────────────────────┐
    │                                                                 │
    │   INPUT                                                         │
    │     │                                                           │
    │     ▼                                                           │
    │   ┌─────────────────────────────────────────────────────┐      │
    │   │              ENCODER / FEATURE EXTRACTOR            │      │
    │   │   (CNN for images, Transformer for text, etc.)      │      │
    │   │                                                     │      │
    │   │   Learns: Raw Input → Rich Representation          │      │
    │   └─────────────────────────────────────────────────────┘      │
    │     │                                                           │
    │     ▼                                                           │
    │   ┌─────────────────┐                                          │
    │   │  REPRESENTATION │  ← This is where the magic happens!      │
    │   │       z         │    Unlabeled data shapes this space      │
    │   └─────────────────┘                                          │
    │     │                                                           │
    │     ▼                                                           │
    │   ┌─────────────────────────────────────────────────────┐      │
    │   │                    CLASSIFIER HEAD                  │      │
    │   │                                                     │      │
    │   │   Learns: Representation → Class Prediction        │      │
    │   └─────────────────────────────────────────────────────┘      │
    │     │                                                           │
    │     ▼                                                           │
    │   OUTPUT (Class Probabilities)                                 │
    │                                                                 │
    └─────────────────────────────────────────────────────────────────┘
    
    
    TRAINING SIGNALS:
    
    ┌──────────────────────────────────────────────────────────────────┐
    │                                                                  │
    │  LABELED DATA ──────────► Supervised Loss (Cross-Entropy)       │
    │                                  │                               │
    │                                  │                               │
    │  UNLABELED DATA ──────────► Unsupervised Loss (various)         │
    │                              • Consistency                       │
    │                              • Entropy                           │
    │                              • Pseudo-labels                     │
    │                              • Contrastive                       │
    │                                  │                               │
    │                                  ▼                               │
    │                           TOTAL LOSS                             │
    │                     L = L_sup + λ · L_unsup                      │
    │                                                                  │
    └──────────────────────────────────────────────────────────────────┘
9.3 Common Deep SSL Loss Functions
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    DEEP SSL LOSS FUNCTION ZOO                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. SUPERVISED LOSS (on labeled data):                                    │
│      L_sup = CrossEntropy(f(x_labeled), y)                                 │
│                                                                             │
│   2. CONSISTENCY LOSS (predictions should be stable):                      │
│      L_cons = ||f(Augment1(x)) - f(Augment2(x))||²                        │
│                                                                             │
│   3. ENTROPY LOSS (predictions should be confident):                       │
│      L_ent = -Σ f(x) log(f(x))                                             │
│                                                                             │
│   4. PSEUDO-LABEL LOSS (treat confident predictions as labels):           │
│      L_pseudo = CrossEntropy(f(x), ŷ) where ŷ = argmax f(x)               │
│                                                                             │
│   5. CONTRASTIVE LOSS (similar samples close, different far):             │
│      L_contrast = -log(similarity of positive pairs / all pairs)          │
│                                                                             │
│   COMBINED OBJECTIVE:                                                       │
│   ───────────────────                                                       │
│   L_total = L_sup + λ₁·L_cons + λ₂·L_ent + λ₃·L_pseudo + ...             │
│                                                                             │
│   Different methods use different combinations!                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 10: Consistency Regularization
10.1 The Consistency Principle
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    CONSISTENCY REGULARIZATION                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CORE PRINCIPLE:                                                           │
│   ───────────────                                                           │
│   "A good model should give CONSISTENT predictions for                     │
│    SIMILAR inputs"                                                          │
│                                                                             │
│   IMPLEMENTATION:                                                           │
│   ───────────────                                                           │
│   1. Take an unlabeled sample x                                            │
│   2. Create two "views" through augmentation: Aug₁(x), Aug₂(x)            │
│   3. Model should predict SAME class for both views                        │
│   4. Minimize difference between predictions                               │
│                                                                             │
│   MATHEMATICAL FORM:                                                        │
│   ──────────────────                                                        │
│   L_consistency = E_x [ D( f(Aug₁(x)), f(Aug₂(x)) ) ]                      │
│                                                                             │
│   where D is a distance/divergence measure (MSE, KL, etc.)                 │
│                                                                             │
│   WHY IT WORKS:                                                             │
│   ─────────────                                                             │
│   • Enforces smoothness in function space                                  │
│   • Encourages robust representations                                      │
│   • Uses unlabeled data to regularize the model                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Explanation
text

            CONSISTENCY REGULARIZATION VISUALIZATION
    
    ORIGINAL IMAGE (unlabeled)
           ┌─────────┐
           │  🐱     │
           │  cat    │
           │ (we don't│
           │  know!)  │
           └─────────┘
                │
        ┌───────┴───────┐
        │               │
        ▼               ▼
    ┌─────────┐     ┌─────────┐
    │ Augment │     │ Augment │
    │ (flip)  │     │ (color) │
    └─────────┘     └─────────┘
        │               │
        ▼               ▼
    ┌─────────┐     ┌─────────┐
    │  🐱←    │     │  🐱     │
    │ flipped │     │ darker  │
    └─────────┘     └─────────┘
        │               │
        ▼               ▼
    ┌─────────┐     ┌─────────┐
    │ Model   │     │ Model   │
    └─────────┘     └─────────┘
        │               │
        ▼               ▼
    p₁ = [0.7, 0.3]  p₂ = [0.6, 0.4]
    (cat, dog)       (cat, dog)
        │               │
        └───────┬───────┘
                │
                ▼
    ┌───────────────────────┐
    │ CONSISTENCY LOSS:     │
    │ ||p₁ - p₂||² = 0.02   │
    │                       │
    │ Force p₁ ≈ p₂        │
    │ (same prediction!)   │
    └───────────────────────┘
10.2 Types of Perturbations
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    PERTURBATION STRATEGIES                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. DATA AUGMENTATION (most common for images):                           │
│      ─────────────────────────────────────────────                          │
│      • Random crop & resize                                                │
│      • Horizontal flip                                                     │
│      • Color jittering (brightness, contrast, saturation)                  │
│      • Rotation                                                            │
│      • Cutout (mask random regions)                                        │
│      • MixUp (blend two images)                                            │
│      • RandAugment (random combination of above)                           │
│                                                                             │
│   2. INPUT NOISE:                                                           │
│      ────────────                                                           │
│      • Add Gaussian noise                                                  │
│      • Dropout on input                                                    │
│                                                                             │
│   3. MODEL NOISE (Π-Model, Temporal Ensembling):                           │
│      ───────────────────────────────────────────                            │
│      • Dropout during inference                                            │
│      • Stochastic depth                                                    │
│                                                                             │
│   4. ADVERSARIAL PERTURBATIONS (VAT):                                      │
│      ────────────────────────────────                                       │
│      • Compute worst-case small perturbation                               │
│      • Most challenging perturbation for consistency                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
10.3 Pi-Model (Π-Model)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                           Π-MODEL                                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   IDEA: Use DROPOUT as a source of stochasticity                          │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   For each sample x (labeled or unlabeled):                                │
│   1. Forward pass 1: z₁ = f(x; dropout_mask_1)                            │
│   2. Forward pass 2: z₂ = f(x; dropout_mask_2)                            │
│   3. Consistency loss: ||z₁ - z₂||²                                       │
│                                                                             │
│   TOTAL LOSS:                                                               │
│   L = L_supervised + λ(t) · L_consistency                                  │
│                                                                             │
│   where λ(t) ramps up during training                                      │
│   (start small, increase gradually)                                        │
│                                                                             │
│   WHY RAMP UP?                                                              │
│   ─────────────                                                             │
│   • Early training: model predictions are garbage                          │
│   • Don't want to enforce consistency on wrong predictions                 │
│   • As model improves, consistency becomes meaningful                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Python Implementation
Python

import torch
import torch.nn as nn
import torch.nn.functional as F
import numpy as np

def ramp_up(current_epoch, rampup_epochs=80):
    """
    Exponential ramp-up for consistency weight
    
    Returns value between 0 and 1
    """
    if current_epoch < rampup_epochs:
        p = current_epoch / rampup_epochs
        return np.exp(-5.0 * (1 - p) ** 2)
    return 1.0


class PiModel(nn.Module):
    """
    Π-Model for Semi-Supervised Learning
    """
    
    def __init__(self, base_model, max_consistency_weight=100.0):
        super().__init__()
        self.model = base_model
        self.max_consistency_weight = max_consistency_weight
        
    def forward(self, x):
        return self.model(x)
    
    def compute_loss(self, x_labeled, y_labeled, x_unlabeled, epoch,
                     rampup_epochs=80):
        """
        Compute Π-Model loss
        """
        # Supervised loss
        logits_labeled = self.model(x_labeled)
        loss_sup = F.cross_entropy(logits_labeled, y_labeled)
        
        # Consistency loss (two forward passes with dropout)
        self.model.train()  # Ensure dropout is active
        
        # Combine labeled and unlabeled for consistency
        x_all = torch.cat([x_labeled, x_unlabeled], dim=0)
        
        # Two forward passes (different dropout masks)
        logits_1 = self.model(x_all)
        logits_2 = self.model(x_all)
        
        # Convert to probabilities
        probs_1 = F.softmax(logits_1, dim=1)
        probs_2 = F.softmax(logits_2, dim=1)
        
        # MSE consistency loss
        loss_cons = F.mse_loss(probs_1, probs_2)
        
        # Ramp up consistency weight
        ramp = ramp_up(epoch, rampup_epochs)
        consistency_weight = self.max_consistency_weight * ramp
        
        # Total loss
        total_loss = loss_sup + consistency_weight * loss_cons
        
        return total_loss, loss_sup, loss_cons, consistency_weight


# TRAINING LOOP:
def train_pi_model(model, optimizer, train_loader_labeled, 
                   train_loader_unlabeled, epochs=100):
    """
    Train Π-Model
    """
    
    for epoch in range(epochs):
        for (x_l, y_l), (x_u, _) in zip(train_loader_labeled, 
                                         train_loader_unlabeled):
            optimizer.zero_grad()
            
            total_loss, sup_loss, cons_loss, weight = model.compute_loss(
                x_l, y_l, x_u, epoch
            )
            
            total_loss.backward()
            optimizer.step()
        
        if epoch % 10 == 0:
            print(f"Epoch {epoch}: Total={total_loss:.4f}, "
                  f"Sup={sup_loss:.4f}, Cons={cons_loss:.4f}, "
                  f"Weight={weight:.2f}")
10.4 Temporal Ensembling
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      TEMPORAL ENSEMBLING                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   PROBLEM WITH Π-MODEL:                                                     │
│   ──────────────────────                                                    │
│   • Need TWO forward passes per sample (slow!)                             │
│   • Targets (z₂) are noisy (single sample)                                 │
│                                                                             │
│   SOLUTION - TEMPORAL ENSEMBLING:                                          │
│   ────────────────────────────────                                          │
│   • Maintain exponential moving average (EMA) of predictions               │
│   • Use EMA as target instead of second forward pass                       │
│   • Only ONE forward pass needed!                                          │
│   • Targets are smoother (averaged over many epochs)                       │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   For each sample xᵢ:                                                      │
│   1. Store prediction history: Zᵢ                                          │
│   2. After each epoch: Zᵢ ← α·Zᵢ + (1-α)·f(xᵢ)                            │
│   3. Target: z̃ᵢ = Zᵢ / (1 - αᵉᵖᵒᶜʰ)  (bias correction)                   │
│   4. Consistency: ||f(xᵢ) - z̃ᵢ||²                                         │
│                                                                             │
│   TYPICAL α = 0.6 to 0.99                                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Visual Comparison
text

              Π-MODEL vs TEMPORAL ENSEMBLING
    
    Π-MODEL (Two Forward Passes):
    ─────────────────────────────
    
           x ────┬────► Forward Pass 1 ───► z₁ ─────┐
                 │                                   │
                 │                                   ├──► MSE Loss
                 │                                   │
                 └────► Forward Pass 2 ───► z₂ ─────┘
    
    
    TEMPORAL ENSEMBLING (One Forward Pass + Memory):
    ────────────────────────────────────────────────
    
                        ┌─────────────────────┐
           x ──────────►│ Forward Pass        │───► zₜ ─────┐
                        └─────────────────────┘              │
                                                             │
                                                             ├──► MSE Loss
                                                             │
    ┌──────────────────────────────────────────────────────┐ │
    │  EMA of past predictions: Z                          │ │
    │                                                      │ │
    │  After epoch: Z ← 0.6·Z + 0.4·zₜ                    │ │
    │                                                      │ │
    │  Target: Z (smoothed over epochs)                    │─┘
    └──────────────────────────────────────────────────────┘
10.5 Mean Teacher
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          MEAN TEACHER                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   PROBLEM WITH TEMPORAL ENSEMBLING:                                        │
│   ──────────────────────────────────                                        │
│   • Targets only update once per epoch (slow!)                             │
│   • Need to store predictions for ALL samples (memory)                     │
│   • Doesn't work well with large datasets                                  │
│                                                                             │
│   SOLUTION - MEAN TEACHER:                                                 │
│   ─────────────────────────                                                 │
│   • Maintain TWO models: Student and Teacher                               │
│   • Teacher = EMA of Student WEIGHTS (not predictions!)                    │
│   • Teacher provides targets, Student learns                               │
│   • Teacher weights: θ' ← α·θ' + (1-α)·θ                                  │
│                                                                             │
│   ADVANTAGES:                                                               │
│   ───────────                                                               │
│   • Targets update every STEP (not every epoch)                            │
│   • No need to store predictions                                           │
│   • Teacher produces better targets (averaged model)                       │
│   • Scales to any dataset size                                             │
│                                                                             │
│   TYPICAL α = 0.999 (slow moving teacher)                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Architecture Diagram
text

                      MEAN TEACHER ARCHITECTURE
    
    ┌────────────────────────────────────────────────────────────────────┐
    │                                                                    │
    │   STUDENT MODEL (θ)                    TEACHER MODEL (θ')         │
    │   ─────────────────                    ──────────────────         │
    │                                                                    │
    │   Input: Augmented x                   Input: Augmented x         │
    │         │                                    │                    │
    │         ▼                                    ▼                    │
    │   ┌───────────┐                        ┌───────────┐             │
    │   │ Student   │                        │ Teacher   │             │
    │   │ Network   │                        │ Network   │             │
    │   │   (θ)     │                        │   (θ')    │             │
    │   └───────────┘                        └───────────┘             │
    │         │                                    │                    │
    │         ▼                                    ▼                    │
    │   Student Pred                          Teacher Pred             │
    │   (gradients)                          (no gradients)            │
    │         │                                    │                    │
    │         │     ┌─────────────────────┐       │                    │
    │         └────►│  CONSISTENCY LOSS   │◄──────┘                    │
    │               │  MSE(student, teacher)│                          │
    │               └─────────────────────┘                            │
    │                                                                    │
    │   After each step:                                                │
    │   θ' ← 0.999 · θ' + 0.001 · θ    (EMA update)                   │
    │                                                                    │
    │   Teacher is a "smoother" version of student!                    │
    │                                                                    │
    └────────────────────────────────────────────────────────────────────┘
Python Implementation
Python

import torch
import torch.nn as nn
import torch.nn.functional as F
import copy

class MeanTeacher:
    """
    Mean Teacher for Semi-Supervised Learning
    """
    
    def __init__(self, student_model, ema_decay=0.999, 
                 consistency_weight=100.0, rampup_epochs=80):
        self.student = student_model
        self.teacher = copy.deepcopy(student_model)
        
        # Freeze teacher (no gradients)
        for param in self.teacher.parameters():
            param.requires_grad = False
        
        self.ema_decay = ema_decay
        self.consistency_weight = consistency_weight
        self.rampup_epochs = rampup_epochs
        self.global_step = 0
    
    def update_teacher(self):
        """
        Update teacher weights as EMA of student weights
        """
        # Use adaptive EMA decay (ramp up)
        ema_decay = min(1 - 1 / (self.global_step + 1), self.ema_decay)
        
        for teacher_param, student_param in zip(
            self.teacher.parameters(), self.student.parameters()
        ):
            teacher_param.data = (
                ema_decay * teacher_param.data + 
                (1 - ema_decay) * student_param.data
            )
        
        self.global_step += 1
    
    def compute_loss(self, x_labeled, y_labeled, x_unlabeled_student, 
                     x_unlabeled_teacher, epoch):
        """
        Compute Mean Teacher loss
        
        x_unlabeled_student: augmented version for student
        x_unlabeled_teacher: differently augmented version for teacher
        """
        
        # === SUPERVISED LOSS ===
        logits_labeled = self.student(x_labeled)
        loss_sup = F.cross_entropy(logits_labeled, y_labeled)
        
        # === CONSISTENCY LOSS ===
        # Student predictions (with gradients)
        self.student.train()
        logits_student = self.student(x_unlabeled_student)
        probs_student = F.softmax(logits_student, dim=1)
        
        # Teacher predictions (no gradients)
        self.teacher.eval()
        with torch.no_grad():
            logits_teacher = self.teacher(x_unlabeled_teacher)
            probs_teacher = F.softmax(logits_teacher, dim=1)
        
        # MSE consistency loss
        loss_cons = F.mse_loss(probs_student, probs_teacher)
        
        # Ramp up consistency weight
        ramp = self._sigmoid_rampup(epoch, self.rampup_epochs)
        current_weight = self.consistency_weight * ramp
        
        # Total loss
        total_loss = loss_sup + current_weight * loss_cons
        
        return total_loss, loss_sup, loss_cons
    
    def _sigmoid_rampup(self, current, rampup_length):
        """Sigmoid ramp-up function"""
        if rampup_length == 0:
            return 1.0
        current = max(0, min(current, rampup_length))
        phase = 1.0 - current / rampup_length
        return float(np.exp(-5.0 * phase * phase))


# DATA AUGMENTATION FOR MEAN TEACHER:
class DualAugmentation:
    """
    Creates two different augmentations of the same image
    """
    
    def __init__(self, weak_augment, strong_augment):
        self.weak = weak_augment
        self.strong = strong_augment
    
    def __call__(self, x):
        return self.weak(x), self.strong(x)
10.6 Virtual Adversarial Training (VAT)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│              VIRTUAL ADVERSARIAL TRAINING (VAT)                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   MOTIVATION:                                                               │
│   ───────────                                                               │
│   Random augmentation might not find the HARDEST perturbation              │
│   What if we find the perturbation that MAXIMALLY changes the output?      │
│                                                                             │
│   IDEA:                                                                     │
│   ─────                                                                     │
│   Find adversarial direction r* that maximizes prediction change:         │
│   r* = argmax_||r||≤ε  D_KL( f(x) || f(x + r) )                           │
│                                                                             │
│   Then minimize consistency in that direction:                             │
│   L_VAT = D_KL( f(x) || f(x + r*) )                                        │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   1. Sample random direction d                                             │
│   2. Approximate gradient: g ≈ ∇_d D_KL(f(x) || f(x + ξd))                │
│   3. Adversarial direction: r* = ε · g / ||g||                             │
│   4. VAT loss: D_KL(f(x) || f(x + r*))                                     │
│                                                                             │
│   KEY PROPERTY:                                                             │
│   ─────────────                                                             │
│   "Virtual" = Uses PREDICTED label, not true label                         │
│   Can be applied to UNLABELED data!                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 11: Pseudo-Labeling & Advanced Techniques
11.1 Pseudo-Labeling for Deep Learning
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                      PSEUDO-LABELING (Lee, 2013)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   SIMPLE BUT POWERFUL IDEA:                                                 │
│   ──────────────────────────                                                │
│   1. Train on labeled data                                                 │
│   2. Use model to predict labels for unlabeled data                        │
│   3. Take predictions as "true" labels                                     │
│   4. Train on both labeled + pseudo-labeled data                           │
│                                                                             │
│   LOSS FUNCTION:                                                            │
│   ──────────────                                                            │
│   L = (1/n_L) Σᵢ H(yᵢ, f(xᵢ)) + λ(t) · (1/n_U) Σⱼ H(ŷⱼ, f(xⱼ))           │
│                                                                             │
│   where:                                                                    │
│   • H = cross-entropy loss                                                 │
│   • ŷⱼ = argmax f(xⱼ) = pseudo-label                                      │
│   • λ(t) = ramp-up weight                                                  │
│                                                                             │
│   KEY INSIGHT:                                                              │
│   ────────────                                                              │
│   Pseudo-labels = implicit entropy minimization!                           │
│   argmax operation forces confident predictions                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Pseudo-Labeling with Confidence Threshold
Python

import torch
import torch.nn as nn
import torch.nn.functional as F

class PseudoLabelLoss(nn.Module):
    """
    Pseudo-labeling with confidence threshold
    """
    
    def __init__(self, threshold=0.95, lambda_u=1.0):
        super().__init__()
        self.threshold = threshold
        self.lambda_u = lambda_u
    
    def forward(self, logits_labeled, labels, logits_unlabeled, epoch,
                rampup_epochs=80):
        """
        Compute pseudo-label loss
        """
        # Supervised loss
        loss_sup = F.cross_entropy(logits_labeled, labels)
        
        # Pseudo-labels for unlabeled data
        with torch.no_grad():
            probs_unlabeled = F.softmax(logits_unlabeled, dim=1)
            max_probs, pseudo_labels = probs_unlabeled.max(dim=1)
            
            # Only keep confident predictions
            mask = max_probs >= self.threshold
            
        if mask.sum() > 0:
            loss_pseudo = F.cross_entropy(
                logits_unlabeled[mask], 
                pseudo_labels[mask]
            )
        else:
            loss_pseudo = torch.tensor(0.0, device=logits_labeled.device)
        
        # Ramp up
        ramp = min(1.0, epoch / rampup_epochs)
        
        # Total loss
        total_loss = loss_sup + self.lambda_u * ramp * loss_pseudo
        
        return total_loss, loss_sup, loss_pseudo, mask.sum().item()
11.2 MixMatch
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                           MIXMATCH (2019)                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   "HOLISTIC" APPROACH - Combines multiple SSL techniques:                  │
│   ─────────────────────────────────────────────────────────                 │
│   1. Consistency regularization (multiple augmentations)                   │
│   2. Entropy minimization (sharpening)                                     │
│   3. MixUp regularization                                                  │
│                                                                             │
│   ALGORITHM STEPS:                                                          │
│   ────────────────                                                          │
│                                                                             │
│   For unlabeled data:                                                       │
│   1. AUGMENT: Create K augmentations of each sample                        │
│   2. AVERAGE: Average predictions across augmentations                     │
│   3. SHARPEN: Apply temperature scaling (reduce entropy)                   │
│   4. Result: pseudo-label q                                                │
│                                                                             │
│   For all data:                                                             │
│   5. MIXUP: Blend labeled and (pseudo-)labeled samples                     │
│   6. TRAIN: Supervised loss on MixUp outputs                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
MixMatch Visual Flow
text

                         MIXMATCH PIPELINE
    
    LABELED DATA (xₗ, yₗ):
    ─────────────────────
    
        xₗ ──► Augment ──► x̂ₗ
               (once)
        yₗ ──────────────► ŷₗ (one-hot)
    
    
    UNLABELED DATA (xᵤ):
    ─────────────────────
    
        xᵤ ──┬──► Aug 1 ──► x̂ᵤ¹ ──► Model ──► p¹ ──┐
             │                                      │
             ├──► Aug 2 ──► x̂ᵤ² ──► Model ──► p² ──┼──► Average ──► p̄
             │                                      │      │
             └──► Aug K ──► x̂ᵤᴷ ──► Model ──► pᴷ ──┘      │
                                                          │
                                                          ▼
                                                     ┌─────────┐
                                                     │ SHARPEN │
                                                     │ (T=0.5) │
                                                     └────┬────┘
                                                          │
                                                          ▼
                                                         q̂ᵤ (pseudo-label)
    
    
    MIXUP (blend all together):
    ───────────────────────────
    
        Labeled: {(x̂ₗ, ŷₗ)}
        Unlabeled: {(x̂ᵤᵏ, q̂ᵤ) for k=1..K}
        
        Combine into single set W, shuffle, and MixUp:
        
        x̃ = λ·wᵢ + (1-λ)·wⱼ
        ỹ = λ·yᵢ + (1-λ)·yⱼ
        
        where λ ~ Beta(α, α)
    
    
    LOSS:
    ─────
        L = L_labeled + λᵤ · L_unlabeled
        
        L_labeled = CrossEntropy on MixUp'd labeled samples
        L_unlabeled = MSE on MixUp'd unlabeled samples
Key Components Explained
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    MIXMATCH COMPONENTS EXPLAINED                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. MULTIPLE AUGMENTATIONS:                                               │
│      ──────────────────────                                                 │
│      • Create K (usually 2) versions of each unlabeled sample             │
│      • Why? Reduces variance of pseudo-label                               │
│                                                                             │
│   2. SHARPENING:                                                            │
│      ───────────                                                            │
│      Sharpen(p, T) = p^(1/T) / Σⱼ pⱼ^(1/T)                                │
│                                                                             │
│      T < 1: Makes distribution more peaked (confident)                     │
│      T = 0.5 is typical                                                    │
│                                                                             │
│      Example:                                                               │
│      p = [0.6, 0.3, 0.1]                                                  │
│      After sharpening (T=0.5): [0.72, 0.23, 0.05]                         │
│                                                                             │
│   3. MIXUP:                                                                 │
│      ──────                                                                 │
│      MixUp(x₁, x₂, λ) = λ·x₁ + (1-λ)·x₂                                  │
│      MixUp(y₁, y₂, λ) = λ·y₁ + (1-λ)·y₂                                  │
│                                                                             │
│      λ ~ Beta(α, α), typically α = 0.75                                    │
│                                                                             │
│      Why? Regularization + smooth decision boundaries                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
11.3 FixMatch
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          FIXMATCH (2020)                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   SIMPLIFICATION OF MIXMATCH:                                              │
│   ────────────────────────────                                              │
│   "Simplicity beats complexity" - achieves SOTA with simpler method       │
│                                                                             │
│   KEY INSIGHT:                                                              │
│   ────────────                                                              │
│   Use WEAK augmentation for pseudo-labels                                  │
│   Use STRONG augmentation for consistency target                           │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   For each unlabeled sample x:                                             │
│   1. Weak augmentation: x_weak = WeakAug(x)                                │
│   2. Strong augmentation: x_strong = StrongAug(x)                          │
│   3. Pseudo-label: ŷ = argmax(f(x_weak))                                   │
│   4. If max(f(x_weak)) > τ:  (confidence threshold)                        │
│      Loss += CrossEntropy(f(x_strong), ŷ)                                  │
│                                                                             │
│   TOTAL LOSS:                                                               │
│   L = L_sup + λ · L_unsup                                                  │
│                                                                             │
│   τ = 0.95 (high threshold, only use confident pseudo-labels)             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
FixMatch Visual Flow
text

                         FIXMATCH PIPELINE
    
    LABELED DATA:
    ─────────────
    
        (x, y) ──► Weak Aug ──► Model ──► CrossEntropy(pred, y)
                                              │
                                              ▼
                                          L_supervised
    
    
    UNLABELED DATA:
    ───────────────
    
                    ┌──► Weak Aug ──────► Model ──► p_weak
        x ──────────┤                               │
                    │                               ▼
                    │                     max(p_weak) > 0.95?
                    │                               │
                    │                    ┌──────────┴──────────┐
                    │                   YES                    NO
                    │                    │                      │
                    │                    ▼                      ▼
                    │            ŷ = argmax(p_weak)         Skip this
                    │                    │                   sample
                    │                    │
                    └──► Strong Aug ──► Model ──► p_strong
                                              │
                                              ▼
                                    CrossEntropy(p_strong, ŷ)
                                              │
                                              ▼
                                         L_unsupervised
    
    
    TOTAL: L = L_supervised + λ · L_unsupervised
FixMatch Implementation
Python

import torch
import torch.nn as nn
import torch.nn.functional as F
import torchvision.transforms as T

class FixMatch:
    """
    FixMatch for Semi-Supervised Learning
    """
    
    def __init__(self, model, threshold=0.95, lambda_u=1.0, T=1.0):
        self.model = model
        self.threshold = threshold
        self.lambda_u = lambda_u
        self.T = T  # Temperature for pseudo-labels
        
        # Define augmentations
        self.weak_aug = T.Compose([
            T.RandomHorizontalFlip(p=0.5),
            T.RandomCrop(32, padding=4),
        ])
        
        # RandAugment for strong augmentation
        self.strong_aug = T.Compose([
            T.RandomHorizontalFlip(p=0.5),
            T.RandomCrop(32, padding=4),
            T.RandAugment(n=2, m=10),  # Strong augmentation
        ])
    
    def compute_loss(self, x_labeled, y_labeled, x_unlabeled):
        """
        Compute FixMatch loss
        """
        batch_size_l = len(x_labeled)
        batch_size_u = len(x_unlabeled)
        
        # === SUPERVISED LOSS ===
        # Weak augmentation for labeled data
        x_labeled_aug = self.weak_aug(x_labeled)
        logits_labeled = self.model(x_labeled_aug)
        loss_sup = F.cross_entropy(logits_labeled, y_labeled)
        
        # === UNSUPERVISED LOSS ===
        # Weak augmentation → pseudo-labels
        x_weak = self.weak_aug(x_unlabeled)
        with torch.no_grad():
            logits_weak = self.model(x_weak)
            probs_weak = F.softmax(logits_weak / self.T, dim=1)
            max_probs, pseudo_labels = probs_weak.max(dim=1)
            
            # Confidence mask
            mask = max_probs >= self.threshold
        
        # Strong augmentation → predictions
        x_strong = self.strong_aug(x_unlabeled)
        logits_strong = self.model(x_strong)
        
        # Unsupervised loss (only confident samples)
        if mask.sum() > 0:
            loss_unsup = F.cross_entropy(
                logits_strong[mask],
                pseudo_labels[mask]
            )
        else:
            loss_unsup = torch.tensor(0.0, device=x_labeled.device)
        
        # Track statistics
        mask_ratio = mask.float().mean().item()
        
        # Total loss
        total_loss = loss_sup + self.lambda_u * loss_unsup
        
        return total_loss, loss_sup, loss_unsup, mask_ratio


# STRONG AUGMENTATION STRATEGIES:

class RandAugment:
    """
    Random Augmentation with N operations of magnitude M
    """
    
    def __init__(self, n=2, m=10):
        self.n = n  # Number of operations
        self.m = m  # Magnitude (0-30)
        
        self.augmentations = [
            'autocontrast', 'equalize', 'rotate', 'solarize',
            'color', 'contrast', 'brightness', 'sharpness',
            'shear_x', 'shear_y', 'translate_x', 'translate_y',
            'posterize'
        ]
    
    def __call__(self, img):
        ops = np.random.choice(self.augmentations, self.n, replace=False)
        for op in ops:
            img = self.apply_op(img, op, self.m)
        return img
Chapter 12: State-of-the-Art Methods
12.1 UDA (Unsupervised Data Augmentation)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                              UDA (2020)                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   COMBINES THREE IDEAS:                                                     │
│   ──────────────────────                                                    │
│   1. Consistency regularization (like Mean Teacher)                        │
│   2. Advanced data augmentation (RandAugment, back-translation)           │
│   3. Training signal annealing (curriculum learning)                       │
│                                                                             │
│   SPECIAL CONTRIBUTION - TSA (Training Signal Annealing):                  │
│   ──────────────────────────────────────────────────────                    │
│   Don't trust ALL labeled data equally from the start!                     │
│                                                                             │
│   Schedule: η(t) increases from 1/K to


12.1 UDA - Training Signal Annealing (Continued)
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    UDA - TRAINING SIGNAL ANNEALING (TSA)                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   PROBLEM:                                                                  │
│   ────────                                                                  │
│   With very few labels, model can OVERFIT to labeled data                  │
│   while ignoring useful unlabeled data signal                              │
│                                                                             │
│   SOLUTION - TSA:                                                           │
│   ───────────────                                                           │
│   Only use labeled samples where model is NOT YET confident                │
│                                                                             │
│   η(t) = threshold that increases over training:                           │
│   • Linear: η(t) = t/T · (1 - 1/K) + 1/K                                  │
│   • Log: η(t) = (1 - exp(-t/T·5)) · (1 - 1/K) + 1/K                       │
│   • Exp: η(t) = exp((t/T - 1)·5) · (1 - 1/K) + 1/K                        │
│                                                                             │
│   RULE: Only compute supervised loss for samples where:                    │
│         max(p(y|x)) < η(t)                                                 │
│                                                                             │
│   INTUITION:                                                                │
│   ──────────                                                                │
│   • Early training: use all labeled samples (η ≈ 1/K)                     │
│   • Late training: only use "hard" samples (η → 1)                        │
│   • Already-learned samples don't dominate training                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
TSA Visualization
text

           TRAINING SIGNAL ANNEALING PROGRESSION
    
    Early Training (η = 0.3):
    ─────────────────────────
    
    Sample Confidences:     [0.2, 0.5, 0.8, 0.3, 0.9, 0.4, 0.7, 0.25]
    Threshold η = 0.3:       ─────────────────────────────────────────
    Use for training?       [ ✓   ✗   ✗   ✗   ✗   ✗   ✗   ✓ ]
    
    Only use samples where model is UNCERTAIN (< 0.3)
    
    
    Mid Training (η = 0.6):
    ───────────────────────
    
    Sample Confidences:     [0.3, 0.7, 0.9, 0.4, 0.95, 0.5, 0.8, 0.35]
    Threshold η = 0.6:       ─────────────────────────────────────────
    Use for training?       [ ✓   ✗   ✗   ✓   ✗    ✓   ✗   ✓ ]
    
    Include more samples as threshold rises
    
    
    Late Training (η = 0.9):
    ────────────────────────
    
    Sample Confidences:     [0.4, 0.85, 0.95, 0.6, 0.98, 0.7, 0.92, 0.5]
    Threshold η = 0.9:       ─────────────────────────────────────────
    Use for training?       [ ✓   ✓    ✗    ✓   ✗    ✓   ✗    ✓ ]
    
    Most samples included except extremely confident ones
12.2 ReMixMatch
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                          REMIXMATCH (2020)                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   BUILDS ON MIXMATCH WITH TWO KEY ADDITIONS:                               │
│   ──────────────────────────────────────────                                │
│                                                                             │
│   1. DISTRIBUTION ALIGNMENT:                                               │
│      ─────────────────────────                                              │
│      Problem: Model's predictions on unlabeled data may not match         │
│               the true class distribution                                  │
│                                                                             │
│      Solution: Align pseudo-label distribution to labeled distribution    │
│                                                                             │
│      p̃(y) = p(y|x) · p(y)_labeled / p(y)_unlabeled                        │
│                                                                             │
│      Then renormalize                                                      │
│                                                                             │
│   2. AUGMENTATION ANCHORING:                                               │
│      ─────────────────────────                                              │
│      Use weakly-augmented sample as "anchor" for strong augmentations     │
│      (Similar to what FixMatch later simplified)                          │
│                                                                             │
│   3. SELF-SUPERVISED LOSS:                                                 │
│      ──────────────────────                                                 │
│      Add rotation prediction task as auxiliary loss                       │
│      Model must predict which rotation was applied (0°, 90°, 180°, 270°) │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Distribution Alignment Explained
text

                    DISTRIBUTION ALIGNMENT
    
    PROBLEM SCENARIO:
    ─────────────────
    
    True class distribution:     [50%, 30%, 20%]  (Class A, B, C)
    Labeled data distribution:   [50%, 30%, 20%]  (representative)
    Model's pseudo-labels:       [70%, 20%, 10%]  (biased toward A!)
    
    Model is OVERCONFIDENT in Class A, UNDERCONFIDENT in Class C
    
    
    DISTRIBUTION ALIGNMENT FIX:
    ───────────────────────────
    
    For each pseudo-label p(y|x):
    
    1. Estimate p(y)_labeled from labeled data:     [0.50, 0.30, 0.20]
    2. Estimate p(y)_unlabeled from model outputs:  [0.70, 0.20, 0.10]
    3. Compute ratio: [0.50/0.70, 0.30/0.20, 0.20/0.10]
                    = [0.71, 1.50, 2.00]
    
    4. Scale pseudo-labels:
       Original p(y|x) = [0.70, 0.20, 0.10]
       Scaled: [0.70×0.71, 0.20×1.50, 0.10×2.00]
             = [0.50, 0.30, 0.20]
    
    5. Renormalize to sum to 1
    
    RESULT: Pseudo-labels now match expected distribution!
12.3 FlexMatch
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                           FLEXMATCH (2021)                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   IMPROVEMENT OVER FIXMATCH:                                               │
│   ──────────────────────────                                                │
│   FixMatch uses FIXED threshold τ = 0.95 for all classes                  │
│   Problem: Some classes are harder than others!                            │
│                                                                             │
│   FLEXMATCH SOLUTION - Curriculum Pseudo Labels (CPL):                     │
│   ─────────────────────────────────────────────────────                     │
│   Use DIFFERENT thresholds for DIFFERENT classes                           │
│   Thresholds ADAPT based on learning progress                              │
│                                                                             │
│   ALGORITHM:                                                                │
│   ──────────                                                                │
│   For each class c:                                                        │
│   1. Track σ(c) = fraction of unlabeled samples with confident            │
│      predictions for class c                                               │
│   2. Flexible threshold: τ(c) = β(c) · τ                                  │
│      where β(c) = σ(c) / max_c'(σ(c'))                                    │
│                                                                             │
│   EFFECT:                                                                   │
│   ───────                                                                   │
│   • Easy classes: higher effective threshold                               │
│   • Hard classes: lower effective threshold (more pseudo-labels)          │
│   • All classes get to contribute to training!                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
FlexMatch Threshold Adaptation
text

                    FLEXMATCH ADAPTIVE THRESHOLDS
    
    SCENARIO: 3-class classification
    ─────────────────────────────────
    
    After some training iterations:
    
    Class A (easy):   70% of predictions confident → σ(A) = 0.70
    Class B (medium): 40% of predictions confident → σ(B) = 0.40
    Class C (hard):   10% of predictions confident → σ(C) = 0.10
    
    
    FIXMATCH (fixed τ = 0.95):
    ─────────────────────────
    
    Class A: Uses 70% × some_factor samples ✓ Good
    Class B: Uses 40% × some_factor samples ~ OK
    Class C: Uses 10% × some_factor samples ✗ Too few!
    
    Class C is underrepresented → model doesn't learn it well
    
    
    FLEXMATCH (adaptive thresholds):
    ────────────────────────────────
    
    β(A) = 0.70 / 0.70 = 1.00  →  τ(A) = 1.00 × 0.95 = 0.95
    β(B) = 0.40 / 0.70 = 0.57  →  τ(B) = 0.57 × 0.95 = 0.54
    β(C) = 0.10 / 0.70 = 0.14  →  τ(C) = 0.14 × 0.95 = 0.13
    
    Now Class C has MUCH lower threshold!
    More Class C samples contribute to training!
    
    
    THRESHOLD PROGRESSION OVER TRAINING:
    ────────────────────────────────────
    
    τ
    │
1.0 │         ────────────────── Class A (easy)
    │     ╱
    │   ╱    ─────────────────── Class B (medium)
0.5 │ ╱  ╱
    │╱ ╱
    │╱        ─────────────────── Class C (hard, catches up!)
0.0 └────────────────────────────────────►
                   Training Progress
12.4 CoMatch
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                            COMATCH (2021)                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   COMBINES SSL WITH CONTRASTIVE LEARNING:                                  │
│   ────────────────────────────────────────                                  │
│                                                                             │
│   KEY INSIGHT:                                                              │
│   ────────────                                                              │
│   Pseudo-labels can be noisy. Contrastive learning can help by:           │
│   • Learning better representations                                        │
│   • Using similarity structure to refine pseudo-labels                    │
│                                                                             │
│   TWO GRAPHS:                                                               │
│   ────────────                                                              │
│   1. Pseudo-label graph: Connect samples with same pseudo-label           │
│   2. Embedding graph: Connect samples close in embedding space            │
│                                                                             │
│   CO-TRAINING THESE GRAPHS:                                                │
│   ──────────────────────────                                                │
│   • Pseudo-labels guide contrastive pairs                                 │
│   • Embeddings help smooth pseudo-labels                                  │
│                                                                             │
│   MEMORY BANK:                                                              │
│   ────────────                                                              │
│   Store embeddings of all samples (like MoCo)                             │
│   Use for finding similar samples for pseudo-label smoothing              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
12.5 Comparison of Modern Methods
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                   MODERN SSL METHODS COMPARISON                             │
├──────────────┬────────────┬────────────┬────────────┬───────────┬──────────┤
│ Method       │ Consistency│ Pseudo-    │ Strong Aug │ Special   │ Year     │
│              │            │ Labels     │            │ Feature   │          │
├──────────────┼────────────┼────────────┼────────────┼───────────┼──────────┤
│ Π-Model      │ ✓          │ ✗          │ ✗          │ Dropout   │ 2017     │
│              │            │            │            │           │          │
│ Mean Teacher │ ✓          │ ✗          │ ✗          │ EMA model │ 2017     │
│              │            │            │            │           │          │
│ VAT          │ ✓          │ ✗          │ ✗          │ Adversarial│ 2018    │
│              │            │            │            │           │          │
│ MixMatch     │ ✓          │ ✓ (soft)   │ ✗          │ MixUp     │ 2019     │
│              │            │            │            │           │          │
│ UDA          │ ✓          │ ✓          │ ✓          │ TSA       │ 2020     │
│              │            │            │            │           │          │
│ ReMixMatch   │ ✓          │ ✓ (soft)   │ ✓          │ Dist Align│ 2020     │
│              │            │            │            │           │          │
│ FixMatch     │ ✓          │ ✓ (hard)   │ ✓          │ Simplicity│ 2020     │
│              │            │            │            │           │          │
│ FlexMatch    │ ✓          │ ✓ (hard)   │ ✓          │ Adaptive τ│ 2021     │
│              │            │            │            │           │          │
│ CoMatch      │ ✓          │ ✓          │ ✓          │ Contrastive│ 2021    │
└──────────────┴────────────┴────────────┴────────────┴───────────┴──────────┘

CIFAR-10 PERFORMANCE WITH 40 LABELS (4 per class):
─────────────────────────────────────────────────────
• Supervised Only:    ~25% accuracy
• Π-Model:            ~54% accuracy
• Mean Teacher:       ~67% accuracy
• MixMatch:           ~88% accuracy
• FixMatch:           ~92% accuracy
• FlexMatch:          ~95% accuracy
Chapter 13: Practical Implementation Guide
13.1 Complete SSL Training Pipeline
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    COMPLETE SSL TRAINING PIPELINE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STEP 1: DATA PREPARATION                                                 │
│   ─────────────────────────                                                 │
│   • Split data into labeled/unlabeled                                      │
│   • Create separate data loaders                                           │
│   • Ensure labeled set is balanced across classes                          │
│                                                                             │
│   STEP 2: MODEL ARCHITECTURE                                               │
│   ──────────────────────────                                                │
│   • Use standard architecture (ResNet, WideResNet, etc.)                   │
│   • No SSL-specific architecture changes needed                            │
│   • Consider capacity vs. data size                                        │
│                                                                             │
│   STEP 3: AUGMENTATION STRATEGY                                            │
│   ─────────────────────────────                                             │
│   • Define weak augmentation (flip, crop)                                  │
│   • Define strong augmentation (RandAugment, CTAugment)                   │
│   • Apply appropriately per SSL method                                     │
│                                                                             │
│   STEP 4: TRAINING LOOP                                                    │
│   ─────────────────────                                                     │
│   • Batch: combine labeled and unlabeled                                   │
│   • Compute supervised + unsupervised loss                                 │
│   • Apply weight ramp-up schedule                                          │
│   • Update model (and teacher if using Mean Teacher)                       │
│                                                                             │
│   STEP 5: EVALUATION                                                       │
│   ────────────────                                                          │
│   • Use held-out test set (not validation from labeled!)                   │
│   • Track both accuracy and pseudo-label quality                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
13.2 Complete FixMatch Implementation
Python

import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
from torch.utils.data import DataLoader, Dataset
import torchvision.transforms as T
import numpy as np
from typing import Tuple, Optional

# ============================================================================
# DATA HANDLING
# ============================================================================

class SSLDataset(Dataset):
    """
    Dataset wrapper for Semi-Supervised Learning
    Returns different augmentations for SSL methods
    """
    
    def __init__(self, data, targets=None, weak_transform=None, 
                 strong_transform=None, is_labeled=True):
        self.data = data
        self.targets = targets
        self.weak_transform = weak_transform
        self.strong_transform = strong_transform
        self.is_labeled = is_labeled
    
    def __len__(self):
        return len(self.data)
    
    def __getitem__(self, idx):
        img = self.data[idx]
        
        if self.is_labeled:
            # Labeled: return weak augmentation + label
            if self.weak_transform:
                img = self.weak_transform(img)
            return img, self.targets[idx]
        else:
            # Unlabeled: return weak AND strong augmentation
            img_weak = self.weak_transform(img) if self.weak_transform else img
            img_strong = self.strong_transform(img) if self.strong_transform else img
            return img_weak, img_strong


def create_ssl_dataloaders(X_train, y_train, n_labeled_per_class,
                           batch_size_labeled=64, batch_size_unlabeled=448):
    """
    Create labeled and unlabeled data loaders for SSL
    """
    
    # Select labeled indices (balanced across classes)
    labeled_idx = []
    for c in np.unique(y_train):
        class_idx = np.where(y_train == c)[0]
        selected = np.random.choice(class_idx, n_labeled_per_class, replace=False)
        labeled_idx.extend(selected)
    labeled_idx = np.array(labeled_idx)
    unlabeled_idx = np.setdiff1d(np.arange(len(y_train)), labeled_idx)
    
    # Define augmentations
    weak_transform = T.Compose([
        T.ToPILImage(),
        T.RandomHorizontalFlip(p=0.5),
        T.RandomCrop(32, padding=4),
        T.ToTensor(),
        T.Normalize((0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010))
    ])
    
    strong_transform = T.Compose([
        T.ToPILImage(),
        T.RandomHorizontalFlip(p=0.5),
        T.RandomCrop(32, padding=4),
        T.RandAugment(num_ops=2, magnitude=10),
        T.ToTensor(),
        T.Normalize((0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010))
    ])
    
    # Create datasets
    labeled_dataset = SSLDataset(
        X_train[labeled_idx], y_train[labeled_idx],
        weak_transform=weak_transform,
        is_labeled=True
    )
    
    unlabeled_dataset = SSLDataset(
        X_train[unlabeled_idx], None,
        weak_transform=weak_transform,
        strong_transform=strong_transform,
        is_labeled=False
    )
    
    # Create loaders
    labeled_loader = DataLoader(
        labeled_dataset, 
        batch_size=batch_size_labeled,
        shuffle=True, 
        drop_last=True
    )
    
    unlabeled_loader = DataLoader(
        unlabeled_dataset,
        batch_size=batch_size_unlabeled,
        shuffle=True,
        drop_last=True
    )
    
    return labeled_loader, unlabeled_loader


# ============================================================================
# MODEL ARCHITECTURE
# ============================================================================

class WideResNetBlock(nn.Module):
    """Basic block for WideResNet"""
    
    def __init__(self, in_channels, out_channels, stride=1, dropout=0.0):
        super().__init__()
        
        self.bn1 = nn.BatchNorm2d(in_channels)
        self.conv1 = nn.Conv2d(in_channels, out_channels, 3, stride, 1, bias=False)
        self.bn2 = nn.BatchNorm2d(out_channels)
        self.conv2 = nn.Conv2d(out_channels, out_channels, 3, 1, 1, bias=False)
        self.dropout = nn.Dropout(dropout)
        
        self.shortcut = nn.Sequential()
        if stride != 1 or in_channels != out_channels:
            self.shortcut = nn.Conv2d(in_channels, out_channels, 1, stride, bias=False)
    
    def forward(self, x):
        out = self.conv1(F.relu(self.bn1(x)))
        out = self.dropout(out)
        out = self.conv2(F.relu(self.bn2(out)))
        out += self.shortcut(x)
        return out


class WideResNet(nn.Module):
    """WideResNet for CIFAR"""
    
    def __init__(self, depth=28, widen_factor=2, num_classes=10, dropout=0.0):
        super().__init__()
        
        n_channels = [16, 16*widen_factor, 32*widen_factor, 64*widen_factor]
        n_blocks = (depth - 4) // 6
        
        self.conv1 = nn.Conv2d(3, n_channels[0], 3, 1, 1, bias=False)
        
        self.layer1 = self._make_layer(n_channels[0], n_channels[1], n_blocks, 1, dropout)
        self.layer2 = self._make_layer(n_channels[1], n_channels[2], n_blocks, 2, dropout)
        self.layer3 = self._make_layer(n_channels[2], n_channels[3], n_blocks, 2, dropout)
        
        self.bn = nn.BatchNorm2d(n_channels[3])
        self.fc = nn.Linear(n_channels[3], num_classes)
    
    def _make_layer(self, in_channels, out_channels, n_blocks, stride, dropout):
        layers = [WideResNetBlock(in_channels, out_channels, stride, dropout)]
        for _ in range(1, n_blocks):
            layers.append(WideResNetBlock(out_channels, out_channels, 1, dropout))
        return nn.Sequential(*layers)
    
    def forward(self, x):
        out = self.conv1(x)
        out = self.layer1(out)
        out = self.layer2(out)
        out = self.layer3(out)
        out = F.relu(self.bn(out))
        out = F.adaptive_avg_pool2d(out, 1)
        out = out.view(out.size(0), -1)
        out = self.fc(out)
        return out


# ============================================================================
# FIXMATCH TRAINER
# ============================================================================

class FixMatchTrainer:
    """
    Complete FixMatch training implementation
    """
    
    def __init__(self, model, device='cuda', 
                 threshold=0.95, lambda_u=1.0, 
                 lr=0.03, momentum=0.9, weight_decay=5e-4,
                 nesterov=True, total_steps=2**20):
        
        self.model = model.to(device)
        self.device = device
        self.threshold = threshold
        self.lambda_u = lambda_u
        self.total_steps = total_steps
        
        # Optimizer
        self.optimizer = optim.SGD(
            self.model.parameters(),
            lr=lr,
            momentum=momentum,
            weight_decay=weight_decay,
            nesterov=nesterov
        )
        
        # Cosine learning rate scheduler
        self.scheduler = optim.lr_scheduler.CosineAnnealingLR(
            self.optimizer, T_max=total_steps
        )
        
        # Tracking
        self.step = 0
        self.best_acc = 0
    
    def train_step(self, x_labeled, y_labeled, x_weak, x_strong):
        """
        Single training step for FixMatch
        """
        self.model.train()
        
        batch_size_l = x_labeled.size(0)
        batch_size_u = x_weak.size(0)
        
        # Move to device
        x_labeled = x_labeled.to(self.device)
        y_labeled = y_labeled.to(self.device)
        x_weak = x_weak.to(self.device)
        x_strong = x_strong.to(self.device)
        
        # === FORWARD PASS ===
        
        # Combine all inputs for efficiency
        inputs = torch.cat([x_labeled, x_weak, x_strong], dim=0)
        logits = self.model(inputs)
        
        # Split outputs
        logits_labeled = logits[:batch_size_l]
        logits_weak = logits[batch_size_l:batch_size_l + batch_size_u]
        logits_strong = logits[batch_size_l + batch_size_u:]
        
        # === SUPERVISED LOSS ===
        loss_supervised = F.cross_entropy(logits_labeled, y_labeled, reduction='mean')
        
        # === UNSUPERVISED LOSS ===
        # Generate pseudo-labels from weak augmentation
        with torch.no_grad():
            probs_weak = F.softmax(logits_weak, dim=1)
            max_probs, pseudo_labels = probs_weak.max(dim=1)
            mask = max_probs >= self.threshold
        
        # Compute loss only for confident samples
        if mask.sum() > 0:
            loss_unsupervised = F.cross_entropy(
                logits_strong[mask],
                pseudo_labels[mask],
                reduction='mean'
            )
        else:
            loss_unsupervised = torch.tensor(0.0, device=self.device)
        
        # === TOTAL LOSS ===
        loss = loss_supervised + self.lambda_u * loss_unsupervised
        
        # === BACKWARD PASS ===
        self.optimizer.zero_grad()
        loss.backward()
        self.optimizer.step()
        self.scheduler.step()
        
        self.step += 1
        
        # Return statistics
        return {
            'loss': loss.item(),
            'loss_sup': loss_supervised.item(),
            'loss_unsup': loss_unsupervised.item(),
            'mask_ratio': mask.float().mean().item(),
            'lr': self.scheduler.get_last_lr()[0]
        }
    
    def train_epoch(self, labeled_loader, unlabeled_loader):
        """
        Train for one epoch
        """
        # Create infinite iterator for unlabeled data
        unlabeled_iter = iter(unlabeled_loader)
        
        epoch_stats = {
            'loss': [], 'loss_sup': [], 'loss_unsup': [], 'mask_ratio': []
        }
        
        for x_labeled, y_labeled in labeled_loader:
            # Get unlabeled batch (cycle if exhausted)
            try:
                x_weak, x_strong = next(unlabeled_iter)
            except StopIteration:
                unlabeled_iter = iter(unlabeled_loader)
                x_weak, x_strong = next(unlabeled_iter)
            
            # Train step
            stats = self.train_step(x_labeled, y_labeled, x_weak, x_strong)
            
            for key in epoch_stats:
                epoch_stats[key].append(stats[key])
        
        # Average statistics
        return {key: np.mean(vals) for key, vals in epoch_stats.items()}
    
    @torch.no_grad()
    def evaluate(self, test_loader):
        """
        Evaluate model on test set
        """
        self.model.eval()
        
        correct = 0
        total = 0
        
        for x, y in test_loader:
            x, y = x.to(self.device), y.to(self.device)
            
            logits = self.model(x)
            preds = logits.argmax(dim=1)
            
            correct += (preds == y).sum().item()
            total += y.size(0)
        
        accuracy = correct / total
        
        if accuracy > self.best_acc:
            self.best_acc = accuracy
        
        return accuracy
    
    def train(self, labeled_loader, unlabeled_loader, test_loader,
              epochs=1024, eval_every=10, log_every=100):
        """
        Full training loop
        """
        
        print("="*60)
        print("Starting FixMatch Training")
        print(f"Threshold: {self.threshold}, Lambda_U: {self.lambda_u}")
        print(f"Total Steps: {self.total_steps}")
        print("="*60)
        
        for epoch in range(epochs):
            # Train
            stats = self.train_epoch(labeled_loader, unlabeled_loader)
            
            # Log
            if epoch % log_every == 0:
                print(f"Epoch {epoch:4d} | "
                      f"Loss: {stats['loss']:.4f} | "
                      f"Sup: {stats['loss_sup']:.4f} | "
                      f"Unsup: {stats['loss_unsup']:.4f} | "
                      f"Mask: {stats['mask_ratio']:.2%}")
            
            # Evaluate
            if epoch % eval_every == 0:
                acc = self.evaluate(test_loader)
                print(f"  → Test Accuracy: {acc:.4f} (Best: {self.best_acc:.4f})")
        
        print("="*60)
        print(f"Training Complete! Best Accuracy: {self.best_acc:.4f}")
        print("="*60)
        
        return self.best_acc


# ============================================================================
# MAIN TRAINING SCRIPT
# ============================================================================

def main():
    """
    Example training script for FixMatch on CIFAR-10
    """
    import torchvision
    
    # Load CIFAR-10
    train_data = torchvision.datasets.CIFAR10(
        root='./data', train=True, download=True
    )
    test_data = torchvision.datasets.CIFAR10(
        root='./data', train=False, download=True
    )
    
    X_train = np.array(train_data.data)
    y_train = np.array(train_data.targets)
    X_test = np.array(test_data.data)
    y_test = np.array(test_data.targets)
    
    # Create data loaders
    # 40 labels total = 4 per class
    labeled_loader, unlabeled_loader = create_ssl_dataloaders(
        X_train, y_train, 
        n_labeled_per_class=4,
        batch_size_labeled=64,
        batch_size_unlabeled=448
    )
    
    # Test loader
    test_transform = T.Compose([
        T.ToTensor(),
        T.Normalize((0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010))
    ])
    test_dataset = torchvision.datasets.CIFAR10(
        root='./data', train=False, transform=test_transform
    )
    test_loader = DataLoader(test_dataset, batch_size=512, shuffle=False)
    
    # Create model
    model = WideResNet(depth=28, widen_factor=2, num_classes=10, dropout=0.0)
    
    # Create trainer
    trainer = FixMatchTrainer(
        model,
        device='cuda' if torch.cuda.is_available() else 'cpu',
        threshold=0.95,
        lambda_u=1.0,
        lr=0.03
    )
    
    # Train
    trainer.train(
        labeled_loader,
        unlabeled_loader,
        test_loader,
        epochs=1024,
        eval_every=50,
        log_every=10
    )


if __name__ == '__main__':
    main()
13.3 Hyperparameter Guidelines
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    HYPERPARAMETER GUIDELINES                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CONFIDENCE THRESHOLD (τ):                                                │
│   ──────────────────────────                                                │
│   • FixMatch default: 0.95                                                 │
│   • Lower (0.7-0.9): More pseudo-labels, but noisier                      │
│   • Higher (0.95-0.99): Fewer but cleaner pseudo-labels                   │
│   • For very few labels: Consider lower threshold                          │
│                                                                             │
│   UNSUPERVISED LOSS WEIGHT (λ_u):                                          │
│   ────────────────────────────────                                          │
│   • FixMatch default: 1.0                                                  │
│   • MixMatch default: 75-100                                               │
│   • Depends on ratio of labeled to unlabeled                               │
│   • Start with 1.0, increase if model ignores unlabeled data              │
│                                                                             │
│   BATCH SIZE RATIO:                                                         │
│   ─────────────────                                                         │
│   • Typical ratio: 1:7 (labeled:unlabeled)                                 │
│   • Example: 64 labeled + 448 unlabeled = 512 total                        │
│   • Larger unlabeled batches generally better                              │
│                                                                             │
│   LEARNING RATE:                                                            │
│   ──────────────                                                            │
│   • Standard: 0.03 with cosine decay                                       │
│   • Use same schedule as supervised training                               │
│                                                                             │
│   TRAINING DURATION:                                                        │
│   ───────────────────                                                       │
│   • SSL needs LONGER training than supervised                              │
│   • 2^20 steps (FixMatch) = ~1M iterations                                 │
│   • Early stopping based on validation set                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 14: Evaluation & Best Practices
14.1 Evaluation Protocol
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    PROPER SSL EVALUATION                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   DATA SPLITS:                                                              │
│   ────────────                                                              │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────┐      │
│   │                        TRAINING DATA                            │      │
│   │  ┌──────────────┐   ┌────────────────────────────────────────┐ │      │
│   │  │   LABELED    │   │            UNLABELED                   │ │      │
│   │  │   (small)    │   │            (large)                     │ │      │
│   │  │              │   │                                        │ │      │
│   │  │  Used for    │   │  Used for unsupervised                │ │      │
│   │  │  supervised  │   │  loss only                            │ │      │
│   │  │  loss        │   │                                        │ │      │
│   │  └──────────────┘   └────────────────────────────────────────┘ │      │
│   └─────────────────────────────────────────────────────────────────┘      │
│                                                                             │
│   ┌─────────────────┐   ┌─────────────────┐                                │
│   │   VALIDATION    │   │      TEST       │                                │
│   │   (optional)    │   │   (held out)    │                                │
│   │                 │   │                 │                                │
│   │  For hyper-     │   │  FINAL          │                                │
│   │  parameter      │   │  evaluation     │                                │
│   │  tuning         │   │  only           │                                │
│   └─────────────────┘   └─────────────────┘                                │
│                                                                             │
│   IMPORTANT RULES:                                                          │
│   ────────────────                                                          │
│   ✓ Test set is NEVER used during training                                │
│   ✓ Labeled samples come from same distribution as unlabeled              │
│   ✓ Report mean ± std over multiple random seeds                          │
│   ✓ Vary which samples are labeled (different random selections)          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
14.2 Metrics Beyond Accuracy
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SSL-SPECIFIC METRICS                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. STANDARD METRICS:                                                      │
│      ─────────────────                                                      │
│      • Accuracy on test set                                                │
│      • Precision, Recall, F1 (especially for imbalanced data)             │
│      • Confusion matrix                                                    │
│                                                                             │
│   2. PSEUDO-LABEL QUALITY:                                                 │
│      ──────────────────────                                                 │
│      • Pseudo-label accuracy (if true labels available for analysis)      │
│      • Confidence distribution of pseudo-labels                           │
│      • Mask ratio (fraction of samples above threshold)                   │
│                                                                             │
│   3. TRAINING DYNAMICS:                                                    │
│      ──────────────────                                                     │
│      • Learning curves (train vs test accuracy over time)                 │
│      • Loss components (supervised vs unsupervised)                       │
│      • Threshold schedule (for adaptive methods)                          │
│                                                                             │
│   4. CONFIDENCE CALIBRATION:                                               │
│      ───────────────────────                                                │
│      • Expected Calibration Error (ECE)                                   │
│      • Reliability diagrams                                               │
│      • Confidence histogram                                               │
│                                                                             │
│   5. CLASS-WISE ANALYSIS:                                                  │
│      ────────────────────                                                   │
│      • Per-class accuracy                                                 │
│      • Per-class pseudo-label accuracy                                    │
│      • Identify classes that benefit most/least from SSL                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
14.3 Best Practices Checklist
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SSL BEST PRACTICES CHECKLIST                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   DATA PREPARATION:                                                         │
│   ☐ Ensure labeled set is BALANCED across classes                          │
│   ☐ Verify labeled and unlabeled come from same distribution              │
│   ☐ Set aside proper test set before ANY training                         │
│   ☐ Apply same preprocessing to all data                                  │
│                                                                             │
│   TRAINING:                                                                 │
│   ☐ Use strong data augmentation (RandAugment, CTAugment)                 │
│   ☐ Apply appropriate ramp-up schedule for unsupervised loss              │
│   ☐ Use larger batch size for unlabeled data                              │
│   ☐ Train for LONGER than supervised baseline                             │
│   ☐ Monitor pseudo-label statistics during training                       │
│                                                                             │
│   EVALUATION:                                                               │
│   ☐ Run multiple times with different random seeds                        │
│   ☐ Report mean AND standard deviation                                    │
│   ☐ Compare against supervised baseline (same labeled data)              │
│   ☐ Compare against supervised with all data (upper bound)               │
│                                                                             │
│   DEBUGGING:                                                                │
│   ☐ Check if mask ratio is reasonable (not 0% or 100%)                    │
│   ☐ Verify augmentations are working correctly                            │
│   ☐ Monitor class distribution of pseudo-labels                          │
│   ☐ Check for confirmation bias (accuracy dropping after initial gains)  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 15: Real-World Applications
15.1 Computer Vision Applications
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    MEDICAL IMAGING                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CHALLENGE:                                                                │
│   ──────────                                                                │
│   • Expert radiologist annotations are expensive ($50-100/image)          │
│   • HIPAA/privacy constraints on data sharing                             │
│   • Rare diseases have very few labeled examples                          │
│                                                                             │
│   SSL SOLUTION:                                                             │
│   ─────────────                                                             │
│   • Hospital has millions of unlabeled X-rays/CT scans                    │
│   • Few hundred expertly labeled cases                                    │
│   • SSL leverages ALL data for better diagnosis                           │
│                                                                             │
│   EXAMPLE ARCHITECTURES:                                                    │
│   ──────────────────────                                                    │
│   • Self-training with uncertainty                                        │
│   • Mean Teacher for consistent predictions                               │
│   • Contrastive pre-training + fine-tuning                               │
│                                                                             │
│   RESULTS:                                                                  │
│   ────────                                                                  │
│   • SSL with 100 labels ≈ Supervised with 1000 labels                     │
│   • 10x reduction in labeling cost                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                    AUTONOMOUS DRIVING                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CHALLENGE:                                                                │
│   ──────────                                                                │
│   • Millions of hours of driving footage                                  │
│   • Labeling every frame (objects, lanes, signs) is impractical           │
│   • Edge cases (rare scenarios) need to be handled                        │
│                                                                             │
│   SSL APPROACHES:                                                           │
│   ───────────────                                                           │
│   1. Object Detection:                                                     │
│      • Pseudo-label confident detections                                  │
│      • Propagate labels across video frames                               │
│                                                                             │
│   2. Semantic Segmentation:                                                │
│      • Self-training with confidence maps                                 │
│      • Consistency across augmented views                                 │
│                                                                             │
│   3. 3D Point Cloud:                                                       │
│      • Graph-based label propagation                                      │
│      • Temporal consistency in LiDAR sequences                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
15.2 Natural Language Processing Applications
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    TEXT CLASSIFICATION                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   APPLICATION: Sentiment Analysis, Topic Classification, Intent Detection  │
│                                                                             │
│   SSL APPROACH - UDA FOR TEXT:                                             │
│   ─────────────────────────────                                             │
│   1. Weak augmentation: Identity (no change)                              │
│   2. Strong augmentation: Back-translation                                │
│      • English → German → English                                         │
│      • Preserves meaning, changes surface form                            │
│                                                                             │
│   EXAMPLE:                                                                  │
│   ────────                                                                  │
│   Original:  "The movie was absolutely fantastic!"                        │
│   Back-trans: "The film was really amazing!"                              │
│                                                                             │
│   Model should predict SAME sentiment for both!                           │
│                                                                             │
│   OTHER TEXT AUGMENTATIONS:                                                │
│   ─────────────────────────                                                 │
│   • Synonym replacement                                                   │
│   • Random insertion/deletion/swap                                        │
│   • TF-IDF based word replacement                                         │
│   • Contextual augmentation (MLM-based)                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                    NAMED ENTITY RECOGNITION (NER)                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CHALLENGE:                                                                │
│   ──────────                                                                │
│   • Sequence labeling (every token needs a label)                         │
│   • Domain-specific entities (medical, legal, etc.)                       │
│   • Entity boundaries matter                                              │
│                                                                             │
│   SSL APPROACHES:                                                           │
│   ───────────────                                                           │
│   1. Self-Training:                                                        │
│      • Predict entities on unlabeled text                                 │
│      • Add confident predictions to training                              │
│                                                                             │
│   2. Cross-View Training:                                                  │
│      • Forward and backward language models                               │
│      • Ensemble predictions for pseudo-labels                             │
│                                                                             │
│   3. Pre-training + Fine-tuning:                                          │
│      • BERT/RoBERTa pre-trained on massive unlabeled text                │
│      • Fine-tune on small labeled NER dataset                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
15.3 Speech and Audio Applications
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SPEECH RECOGNITION                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CHALLENGE:                                                                │
│   ──────────                                                                │
│   • Transcribing audio is VERY expensive (10x real-time)                  │
│   • Different accents, languages, domains                                 │
│   • Millions of hours of unlabeled audio available                        │
│                                                                             │
│   STATE-OF-THE-ART: WAV2VEC 2.0                                           │
│   ─────────────────────────────                                             │
│   Self-supervised pre-training on raw audio:                              │
│   1. Learn representations from 53K hours unlabeled speech               │
│   2. Fine-tune on just 10 minutes of labeled data                        │
│   3. Achieves competitive WER (Word Error Rate)                          │
│                                                                             │
│   PSEUDO-LABELING FOR ASR:                                                 │
│   ─────────────────────────                                                 │
│   1. Train initial ASR on labeled data                                    │
│   2. Transcribe unlabeled audio                                           │
│   3. Filter by confidence (language model score)                          │
│   4. Retrain on combined data                                             │
│                                                                             │
│   NOISY STUDENT FOR ASR:                                                   │
│   ───────────────────────                                                   │
│   1. Teacher generates transcripts                                        │
│   2. Student trained with noise (SpecAugment)                             │
│   3. Student becomes new teacher                                          │
│   4. Iterate                                                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
15.4 Industry Case Studies
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    GOOGLE - NOISY STUDENT                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   TASK: ImageNet Classification                                            │
│                                                                             │
│   APPROACH:                                                                 │
│   ─────────                                                                 │
│   1. Train teacher on 1.2M labeled ImageNet images                        │
│   2. Pseudo-label 300M unlabeled JFT images                               │
│   3. Train student (larger) with noise on combined data                   │
│   4. Student becomes teacher, repeat                                       │
│                                                                             │
│   RESULTS:                                                                  │
│   ────────                                                                  │
│   • 88.4% top-1 accuracy (SOTA at the time)                               │
│   • +1.0% over supervised EfficientNet                                    │
│   • Better robustness to corruptions                                      │
│                                                                             │
│   KEY INSIGHT: Adding noise to student is CRUCIAL                         │
│   • RandAugment                                                           │
│   • Dropout                                                               │
│   • Stochastic depth                                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                    FACEBOOK - BILLION-SCALE SSL                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   TASK: Instagram Image Classification                                     │
│                                                                             │
│   DATA SCALE:                                                               │
│   ───────────                                                               │
│   • 1 billion Instagram images                                            │
│   • Hashtags as noisy labels (not true labels!)                          │
│   • 1500 predefined visual concepts                                       │
│                                                                             │
│   APPROACH:                                                                 │
│   ─────────                                                                 │
│   1. Pre-train on Instagram with hashtag supervision                      │
│   2. Transfer to ImageNet (fine-tune)                                     │
│   3. Achieves competitive results with less labeled data                  │
│                                                                             │
│   LEARNINGS:                                                                │
│   ──────────                                                                │
│   • More unlabeled data helps (even with noise)                          │
│   • SSL enables leveraging web-scale data                                 │
│   • Hashtags ≠ labels, but still useful signal                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 16: Common Pitfalls & Solutions
16.1 Failure Modes
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SSL FAILURE MODES                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   FAILURE MODE 1: CONFIRMATION BIAS                                        │
│   ───────────────────────────────────                                       │
│   SYMPTOM: Accuracy improves initially, then drops                         │
│                                                                             │
│   CAUSE:                                                                    │
│   • Model makes wrong prediction with high confidence                      │
│   • Wrong pseudo-label reinforces the error                               │
│   • Error propagates to similar samples                                   │
│                                                                             │
│   SOLUTION:                                                                 │
│   • Higher confidence threshold                                           │
│   • Curriculum learning (easy samples first)                              │
│   • Regularization (dropout, weight decay)                                │
│   • Use teacher-student framework (Mean Teacher)                          │
│                                                                             │
│   ─────────────────────────────────────────────────────────────────────    │
│                                                                             │
│   FAILURE MODE 2: CLASS IMBALANCE AMPLIFICATION                            │
│   ──────────────────────────────────────────────                            │
│   SYMPTOM: Model predicts majority class for everything                    │
│                                                                             │
│   CAUSE:                                                                    │
│   • Model more confident on majority class                                │
│   • More majority pseudo-labels pass threshold                            │
│   • Training becomes increasingly imbalanced                              │
│                                                                             │
│   SOLUTION:                                                                 │
│   • Per-class thresholds (FlexMatch)                                      │
│   • Distribution alignment (ReMixMatch)                                   │
│   • Class-balanced sampling                                               │
│   • Class-balanced loss weighting                                         │
│                                                                             │
│   ─────────────────────────────────────────────────────────────────────    │
│                                                                             │
│   FAILURE MODE 3: DISTRIBUTION MISMATCH                                    │
│   ──────────────────────────────────────                                    │
│   SYMPTOM: SSL performs WORSE than supervised baseline                     │
│                                                                             │
│   CAUSE:                                                                    │
│   • Unlabeled data from different distribution than labeled               │
│   • Unlabeled data contains classes not in labeled set                    │
│   • Domain shift between labeled and unlabeled                            │
│                                                                             │
│   SOLUTION:                                                                 │
│   • Verify distributions match before applying SSL                        │
│   • Use open-set SSL methods if classes differ                            │
│   • Domain adaptation techniques                                          │
│   • Outlier/anomaly detection to filter unlabeled data                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
16.2 Debugging Guide
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SSL DEBUGGING CHECKLIST                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   STEP 1: VERIFY SUPERVISED BASELINE                                       │
│   ────────────────────────────────────                                      │
│   ☐ Train supervised model on labeled data only                           │
│   ☐ Check if baseline is reasonable                                       │
│   ☐ If baseline is terrible, SSL won't help                               │
│                                                                             │
│   STEP 2: CHECK DATA PIPELINE                                              │
│   ───────────────────────────                                               │
│   ☐ Visualize augmented samples (weak and strong)                         │
│   ☐ Verify augmentations are semantic-preserving                          │
│   ☐ Check batch construction (labeled + unlabeled)                        │
│                                                                             │
│   STEP 3: MONITOR TRAINING DYNAMICS                                        │
│   ──────────────────────────────────                                        │
│   ☐ Plot supervised loss over time (should decrease)                      │
│   ☐ Plot unsupervised loss over time (should decrease)                    │
│   ☐ Plot mask ratio over time (should increase gradually)                 │
│                                                                             │
│   STEP 4: ANALYZE PSEUDO-LABELS                                            │
│   ──────────────────────────────                                            │
│   ☐ Check class distribution of pseudo-labels                             │
│   ☐ If you have unlabeled ground truth: check pseudo-label accuracy      │
│   ☐ Identify which classes have most/least pseudo-labels                 │
│                                                                             │
│   STEP 5: HYPERPARAMETER SENSITIVITY                                       │
│   ────────────────────────────────                                          │
│   ☐ Try different confidence thresholds (0.7, 0.8, 0.9, 0.95)            │
│   ☐ Try different unsupervised loss weights (0.5, 1.0, 2.0)              │
│   ☐ Try different batch size ratios                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
16.3 Problem-Solution Matrix
text

┌────────────────────┬─────────────────────────────────────────────────────────┐
│ PROBLEM            │ SOLUTIONS                                               │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ Mask ratio = 0%    │ • Lower confidence threshold                           │
│ (no pseudo-labels) │ • Train longer before applying SSL                     │
│                    │ • Check if model is learning at all                    │
│                    │                                                         │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ Mask ratio = 100%  │ • Raise confidence threshold                           │
│ (all pass)         │ • Model may be overconfident                           │
│                    │ • Add calibration or temperature scaling               │
│                    │                                                         │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ SSL worse than     │ • Distribution mismatch                                │
│ supervised         │ • Try lower unsupervised weight                        │
│                    │ • Verify data pipeline                                  │
│                    │ • Check if assumptions hold                            │
│                    │                                                         │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ One class          │ • Use per-class thresholds                             │
│ dominates          │ • Distribution alignment                               │
│                    │ • Class-balanced sampling                              │
│                    │                                                         │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ Accuracy           │ • Confirmation bias                                    │
│ oscillates         │ • Lower learning rate                                  │
│                    │ • Stronger regularization                              │
│                    │ • Teacher-student framework                            │
│                    │                                                         │
├────────────────────┼─────────────────────────────────────────────────────────┤
│                    │                                                         │
│ Training very slow │ • Reduce unlabeled batch size                          │
│                    │ • Use fewer augmentation operations                    │
│                    │ • Mixed precision training                             │
│                    │ • Distributed training                                 │
│                    │                                                         │
└────────────────────┴─────────────────────────────────────────────────────────┘
Chapter 17: Future Directions
17.1 Emerging Research Areas
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    FUTURE OF SEMI-SUPERVISED LEARNING                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. SSL + FOUNDATION MODELS                                               │
│   ──────────────────────────                                                │
│   • Large pre-trained models (GPT, CLIP, etc.)                            │
│   • Few-shot learning with prompting                                      │
│   • SSL for efficient fine-tuning                                         │
│                                                                             │
│   2. OPEN-SET SSL                                                          │
│   ──────────────                                                            │
│   • Unlabeled data contains unknown classes                               │
│   • Detect and handle out-of-distribution samples                         │
│   • Combine SSL with novelty detection                                    │
│                                                                             │
│   3. SSL + ACTIVE LEARNING                                                 │
│   ─────────────────────                                                     │
│   • Which samples to label next?                                          │
│   • SSL identifies uncertain samples                                      │
│   • Active learning selects most informative                              │
│   • Optimal labeling budget allocation                                    │
│                                                                             │
│   4. MULTI-MODAL SSL                                                       │
│   ──────────────────                                                        │
│   • Learn from multiple data types (image + text)                         │
│   • Cross-modal consistency                                               │
│   • Leverage alignment between modalities                                 │
│                                                                             │
│   5. FEDERATED SSL                                                         │
│   ────────────────                                                          │
│   • Distributed data across devices/institutions                          │
│   • Privacy-preserving SSL                                                │
│   • Learn without centralizing data                                       │
│                                                                             │
│   6. CONTINUAL/LIFELONG SSL                                                │
│   ──────────────────────                                                    │
│   • Data arrives in streams                                               │
│   • New classes emerge over time                                          │
│   • Avoid forgetting while learning new                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
17.2 SSL + Self-Supervised Learning
text

┌─────────────────────────────────────────────────────────────────────────────┐
│              SSL MEETS SELF-SUPERVISED LEARNING                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   SELF-SUPERVISED LEARNING:                                                │
│   ──────────────────────────                                                │
│   • Creates labels from data itself                                       │
│   • Pretext tasks: rotation prediction, jigsaw, colorization             │
│   • Contrastive learning: SimCLR, MoCo, BYOL                              │
│   • Uses ALL data (no labels needed at all)                               │
│                                                                             │
│   COMBINING APPROACHES:                                                     │
│   ──────────────────────                                                    │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────┐      │
│   │                                                                 │      │
│   │   Stage 1: Self-supervised pre-training                        │      │
│   │   ─────────────────────────────────────                         │      │
│   │   • Train on ALL data (labeled + unlabeled)                    │      │
│   │   • Learn general representations                              │      │
│   │   • No labels used                                             │      │
│   │                                                                 │      │
│   │                         │                                       │      │
│   │                         ▼                                       │      │
│   │                                                                 │      │
│   │   Stage 2: Semi-supervised fine-tuning                         │      │
│   │   ─────────────────────────────────────                         │      │
│   │   • Use few labeled samples                                    │      │
│   │   • Apply SSL techniques (pseudo-labels, consistency)          │      │
│   │   • Leverage unlabeled data structure                          │      │
│   │                                                                 │      │
│   └─────────────────────────────────────────────────────────────────┘      │
│                                                                             │
│   BENEFITS:                                                                 │
│   • Better feature initialization                                          │
│   • Less prone to confirmation bias                                       │
│   • Works with even fewer labels                                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
Chapter 18: Interview Questions & Answers
18.1 Conceptual Questions
text

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q1: What is Semi-Supervised Learning and when should you use it?           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ Semi-Supervised Learning (SSL) is a machine learning paradigm that         │
│ learns from BOTH labeled AND unlabeled data. It sits between supervised    │
│ learning (all labeled) and unsupervised learning (no labels).              │
│                                                                             │
│ USE SSL WHEN:                                                               │
│ • You have lots of unlabeled data but few labels                          │
│ • Labeling is expensive or time-consuming                                  │
│ • Labels require domain expertise                                          │
│                                                                             │
│ DON'T USE SSL WHEN:                                                         │
│ • You have abundant labeled data                                           │
│ • Unlabeled data distribution differs from labeled                        │
│ • Labeling is cheap and fast                                              │
│                                                                             │
│ KEY INSIGHT: SSL works because unlabeled data reveals the STRUCTURE       │
│ of the data distribution, which helps define better decision boundaries.   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q2: Explain the three main assumptions of SSL                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ 1. SMOOTHNESS ASSUMPTION:                                                  │
│    "Points close in input space should have similar labels"               │
│    → Enables: Label propagation, transductive methods                     │
│                                                                             │
│ 2. CLUSTER ASSUMPTION (Low-Density Separation):                           │
│    "Points form clusters, same cluster = same label"                      │
│    "Decision boundaries pass through low-density regions"                 │
│    → Enables: Self-training, entropy minimization, TSVM                   │
│                                                                             │
│ 3. MANIFOLD ASSUMPTION:                                                    │
│    "High-dimensional data lies on lower-dimensional manifolds"            │
│    "Measure distance along manifold, not through space"                   │
│    → Enables: Graph-based methods, representation learning                │
│                                                                             │
│ IMPORTANT: If these assumptions don't hold, SSL can HURT performance!     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q3: What is consistency regularization and why does it work?               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ CONSISTENCY REGULARIZATION enforces that a model's predictions should     │
│ be STABLE under small perturbations of the input.                         │
│                                                                             │
│ FORMULATION:                                                                │
│ L_consistency = E[ D( f(Aug₁(x)), f(Aug₂(x)) ) ]                          │
│                                                                             │
│ The model should predict the SAME CLASS for:                               │
│ • Flipped image and original                                              │
│ • Cropped image and full image                                            │
│ • Image with dropout vs without                                           │
│                                                                             │
│ WHY IT WORKS:                                                               │
│ 1. Enforces smoothness in function space                                  │
│ 2. Leverages unlabeled data for regularization                            │
│ 3. Improves robustness to input variations                                │
│ 4. Pushes decision boundary away from data manifold                       │
│                                                                             │
│ KEY METHODS: Π-Model, Mean Teacher, VAT, UDA, FixMatch                    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q4: Explain pseudo-labeling and its potential problems                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ PSEUDO-LABELING: Use model's predictions on unlabeled data as labels     │
│                                                                             │
│ PROCESS:                                                                    │
│ 1. Train model on labeled data                                            │
│2. Predict labels for unlabeled data                                      │
│ 3. Keep high-confidence predictions as "pseudo-labels"                    │
│ 4. Train on labeled + pseudo-labeled data                                 │
│ 5. Repeat                                                                  │
│                                                                             │
│ PROBLEMS:                                                                   │
│                                                                             │
│ 1. CONFIRMATION BIAS:                                                      │
│    Wrong predictions get reinforced                                       │
│    Solution: High threshold, curriculum learning, Mean Teacher            │
│                                                                             │
│ 2. CLASS IMBALANCE:                                                        │
│    Confident on majority class → more majority pseudo-labels              │
│    Solution: Per-class thresholds, distribution alignment                 │
│                                                                             │
│ 3. THRESHOLD SENSITIVITY:                                                  │
│    Too high: few pseudo-labels, slow learning                             │
│    Too low: noisy pseudo-labels, confirmation bias                        │
│    Solution: Adaptive thresholds (FlexMatch)                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q5: Compare FixMatch and MixMatch                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ ┌─────────────────────┬─────────────────────┬─────────────────────┐        │
│ │ Aspect              │ MixMatch            │ FixMatch            │        │
│ ├─────────────────────┼─────────────────────┼─────────────────────┤        │
│ │ Pseudo-labels       │ Soft (distribution) │ Hard (argmax)       │        │
│ │                     │                     │                     │        │
│ │ # Augmentations     │ K (typically 2)     │ 2 (weak + strong)   │        │
│ │                     │                     │                     │        │
│ │ Sharpening          │ Yes (T=0.5)         │ No (implicit via    │        │
│ │                     │                     │ threshold)          │        │
│ │                     │                     │                     │        │
│ │ MixUp               │ Yes                 │ No                  │        │
│ │                     │                     │                     │        │
│ │ Strong augmentation │ No                  │ Yes (RandAugment)   │        │
│ │                     │                     │                     │        │
│ │ Confidence threshold│ No                  │ Yes (τ=0.95)        │        │
│ │                     │                     │                     │        │
│ │ Complexity          │ Higher              │ Lower               │        │
│ │                     │                     │                     │        │
│ │ Performance         │ Very good           │ Better + simpler    │        │
│ └─────────────────────┴─────────────────────┴─────────────────────┘        │
│                                                                             │
│ KEY INSIGHT: FixMatch achieves better results with a simpler algorithm    │
│ by using strong augmentation and hard pseudo-labels with high threshold.  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q6: What is the Mean Teacher algorithm and why is it effective?            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ MEAN TEACHER uses TWO models:                                              │
│ • STUDENT: Updated via gradient descent (learns)                           │
│ • TEACHER: Updated via Exponential Moving Average of student weights      │
│                                                                             │
│ ALGORITHM:                                                                  │
│ 1. Student predicts on strongly augmented input                           │
│ 2. Teacher predicts on weakly augmented input (no gradients)              │
│ 3. Consistency loss: MSE(student_pred, teacher_pred)                      │
│ 4. Update student with gradient descent                                   │
│ 5. Update teacher: θ_teacher ← α·θ_teacher + (1-α)·θ_student              │
│                                                                             │
│ WHY IT'S EFFECTIVE:                                                        │
│                                                                             │
│ 1. BETTER TARGETS:                                                         │
│    • Teacher is averaged over many training steps                         │
│    • More stable predictions than single model                            │
│    • Acts like an ensemble                                                │
│                                                                             │
│ 2. REDUCES CONFIRMATION BIAS:                                              │
│    • Teacher changes slowly (α ≈ 0.999)                                   │
│    • Student can't immediately reinforce its own errors                   │
│                                                                             │
│ 3. IMPLICIT TEMPORAL ENSEMBLING:                                           │
│    • Without storing predictions for all samples                          │
│    • Scales to large datasets                                             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q7: How does graph-based SSL work? Explain Label Propagation.              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ GRAPH-BASED SSL:                                                           │
│ 1. Build a graph where nodes = data points                                │
│ 2. Edges connect similar points (k-NN or Gaussian kernel)                 │
│ 3. Edge weights represent similarity                                      │
│ 4. Propagate labels from labeled to unlabeled nodes                       │
│                                                                             │
│ LABEL PROPAGATION ALGORITHM:                                               │
│                                                                             │
│ 1. Initialize: Y⁽⁰⁾ = labels for labeled points, 0 for unlabeled         │
│                                                                             │
│ 2. Iterate until convergence:                                             │
│    Y⁽ᵗ⁺¹⁾ = T · Y⁽ᵗ⁾                                                       │
│    Y⁽ᵗ⁺¹⁾[labeled] = Y⁽⁰⁾[labeled]  (clamp labeled points)                │
│                                                                             │
│    where T = D⁻¹W (transition matrix)                                     │
│    W = weight matrix, D = degree matrix                                   │
│                                                                             │
│ 3. Final prediction: argmax of Y for each node                            │
│                                                                             │
│ INTUITION:                                                                  │
│ • Labels "flow" from labeled to unlabeled through edges                   │
│ • Higher edge weight = stronger flow                                      │
│ • Each point becomes weighted average of neighbors                        │
│ • Labeled points stay fixed (anchors)                                     │
│                                                                             │
│ LIMITATION: Doesn't scale well to very large datasets (O(n²) graph)       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q8: What is entropy minimization and how does it relate to SSL?            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ ENTROPY measures uncertainty in a probability distribution:                │
│ H(p) = -Σᵢ pᵢ log(pᵢ)                                                      │
│                                                                             │
│ • Low entropy = confident prediction (e.g., [0.99, 0.01])                 │
│ • High entropy = uncertain prediction (e.g., [0.5, 0.5])                  │
│                                                                             │
│ ENTROPY MINIMIZATION FOR SSL:                                              │
│                                                                             │
│ L = L_supervised + λ · E_unlabeled[H(f(x))]                               │
│                                                                             │
│ "Make confident predictions on unlabeled data"                            │
│                                                                             │
│ CONNECTION TO LOW-DENSITY SEPARATION:                                      │
│ • Confident predictions → points far from decision boundary               │
│ • Uncertain predictions → points near decision boundary                   │
│ • Minimizing entropy pushes boundary to low-density regions              │
│                                                                             │
│ CONNECTION TO PSEUDO-LABELING:                                             │
│ • Pseudo-label: ŷ = argmax f(x)                                           │
│ • Training with pseudo-labels implicitly minimizes entropy                │
│ • argmax is the "hardest" form of entropy minimization                    │
│                                                                             │
│ METHODS USING ENTROPY MINIMIZATION:                                        │
│ • Explicit: Add entropy term to loss                                      │
│ • Implicit: Pseudo-labeling, MixMatch (sharpening)                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q9: Why is strong data augmentation important for modern SSL?              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ STRONG AUGMENTATION is crucial for methods like FixMatch and UDA.         │
│                                                                             │
│ TYPES OF AUGMENTATION:                                                      │
│                                                                             │
│ WEAK:                              STRONG:                                  │
│ • Random crop                      • RandAugment                           │
│ • Horizontal flip                  • AutoAugment                           │
│ • Small rotations                  • CTAugment                             │
│                                    • Cutout                                │
│                                    • Multiple operations                   │
│                                                                             │
│ WHY STRONG AUGMENTATION HELPS:                                             │
│                                                                             │
│ 1. HARDER CONSISTENCY TARGET:                                              │
│    • Model must be invariant to large transformations                     │
│    • Learns more robust features                                          │
│                                                                             │
│ 2. REGULARIZATION:                                                         │
│    • Prevents overfitting to limited labeled data                         │
│    • Increases effective dataset size                                     │
│                                                                             │
│ 3. BETTER PSEUDO-LABELS:                                                   │
│    • Weak aug for pseudo-label: reliable prediction                       │
│    • Strong aug for training: challenging but learnable                   │
│                                                                             │
│ 4. FORCES SEMANTIC UNDERSTANDING:                                          │
│    • Can't rely on low-level statistics                                   │
│    • Must understand semantic content                                     │
│                                                                             │
│ FIXMATCH PATTERN:                                                          │
│ Pseudo-label from WEAK aug → Train on STRONG aug                          │
│ This combination is key to its success!                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q10: What is co-training and when can it be applied?                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ CO-TRAINING trains two classifiers on different "views" of data.          │
│ Each classifier teaches the other via pseudo-labels.                      │
│                                                                             │
│ REQUIREMENTS:                                                               │
│                                                                             │
│ 1. SUFFICIENCY: Each view alone can predict the label                     │
│ 2. CONDITIONAL INDEPENDENCE: Views are independent given label            │
│                                                                             │
│ ALGORITHM:                                                                  │
│ 1. Split features into View 1 and View 2                                  │
│ 2. Train classifier f₁ on View 1, f₂ on View 2                           │
│ 3. f₁ labels confident samples for f₂'s training                         │
│ 4. f₂ labels confident samples for f₁'s training                         │
│ 5. Repeat                                                                  │
│                                                                             │
│ EXAMPLES OF NATURAL VIEWS:                                                  │
│ • Web pages: (page text) vs (anchor text of links)                        │
│ • Videos: (visual frames) vs (audio)                                      │
│ • Medical: (patient history) vs (lab results)                             │
│                                                                             │
│ WHEN NATURAL VIEWS DON'T EXIST:                                            │
│ • Random feature splits                                                   │
│ • Different model architectures (Tri-Training)                            │
│ • Different training runs (different random seeds)                        │
│                                                                             │
│ LIMITATION: Strict view assumptions rarely hold in practice               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
18.2 Technical/Coding Questions
text

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q11: Implement a simple self-training algorithm                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
Python

import numpy as np
from sklearn.base import clone

def self_training(base_classifier, X_labeled, y_labeled, X_unlabeled,
                  threshold=0.95, max_iter=10):
    """
    Simple self-training implementation
    
    Parameters:
    -----------
    base_classifier : sklearn classifier with predict_proba
    X_labeled : array of shape (n_labeled, n_features)
    y_labeled : array of shape (n_labeled,)
    X_unlabeled : array of shape (n_unlabeled, n_features)
    threshold : confidence threshold for pseudo-labeling
    max_iter : maximum iterations
    
    Returns:
    --------
    classifier : trained classifier
    """
    # Initialize training set
    X_train = X_labeled.copy()
    y_train = y_labeled.copy()
    X_pool = X_unlabeled.copy()
    
    for iteration in range(max_iter):
        # Train on current labeled set
        clf = clone(base_classifier)
        clf.fit(X_train, y_train)
        
        if len(X_pool) == 0:
            break
        
        # Predict on unlabeled pool
        probs = clf.predict_proba(X_pool)
        max_probs = probs.max(axis=1)
        predictions = clf.predict(X_pool)
        
        # Select confident predictions
        confident_mask = max_probs >= threshold
        n_confident = confident_mask.sum()
        
        print(f"Iter {iteration}: Adding {n_confident} samples")
        
        if n_confident == 0:
            break
        
        # Add to training set
        X_train = np.vstack([X_train, X_pool[confident_mask]])
        y_train = np.concatenate([y_train, predictions[confident_mask]])
        
        # Remove from pool
        X_pool = X_pool[~confident_mask]
    
    # Final training
    clf = clone(base_classifier)
    clf.fit(X_train, y_train)
    
    return clf
text

└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q12: Implement the consistency loss used in Mean Teacher                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
Python

import torch
import torch.nn.functional as F

def consistency_loss(student_logits, teacher_logits, temperature=1.0):
    """
    Compute consistency loss between student and teacher predictions
    
    Parameters:
    -----------
    student_logits : tensor of shape (batch_size, num_classes)
    teacher_logits : tensor of shape (batch_size, num_classes)
    temperature : softmax temperature
    
    Returns:
    --------
    loss : scalar tensor
    """
    # Convert to probabilities with temperature
    student_probs = F.softmax(student_logits / temperature, dim=1)
    
    # Teacher predictions (detached - no gradients)
    with torch.no_grad():
        teacher_probs = F.softmax(teacher_logits / temperature, dim=1)
    
    # MSE loss between probability distributions
    loss = F.mse_loss(student_probs, teacher_probs)
    
    return loss


def update_ema_model(student_model, teacher_model, alpha=0.999):
    """
    Update teacher model as EMA of student model
    
    Parameters:
    -----------
    student_model : PyTorch model (source)
    teacher_model : PyTorch model (target, updated in-place)
    alpha : EMA decay factor (0.999 typical)
    """
    with torch.no_grad():
        for student_param, teacher_param in zip(
            student_model.parameters(),
            teacher_model.parameters()
        ):
            teacher_param.data = (
                alpha * teacher_param.data +
                (1 - alpha) * student_param.data
            )
text

└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q13: Implement the FixMatch loss function                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
Python

import torch
import torch.nn.functional as F

def fixmatch_loss(model, x_labeled, y_labeled, x_weak, x_strong,
                  threshold=0.95, lambda_u=1.0):
    """
    Compute FixMatch loss
    
    Parameters:
    -----------
    model : PyTorch classifier
    x_labeled : labeled images (batch_size_l, C, H, W)
    y_labeled : labels (batch_size_l,)
    x_weak : weakly augmented unlabeled (batch_size_u, C, H, W)
    x_strong : strongly augmented unlabeled (batch_size_u, C, H, W)
    threshold : confidence threshold for pseudo-labels
    lambda_u : weight for unsupervised loss
    
    Returns:
    --------
    total_loss : combined loss
    stats : dict with loss components and mask ratio
    """
    # Supervised loss
    logits_labeled = model(x_labeled)
    loss_sup = F.cross_entropy(logits_labeled, y_labeled)
    
    # Generate pseudo-labels from weak augmentation
    with torch.no_grad():
        logits_weak = model(x_weak)
        probs_weak = F.softmax(logits_weak, dim=1)
        max_probs, pseudo_labels = probs_weak.max(dim=1)
        
        # Confidence mask
        mask = max_probs >= threshold
    
    # Unsupervised loss on strong augmentation
    logits_strong = model(x_strong)
    
    if mask.sum() > 0:
        loss_unsup = F.cross_entropy(
            logits_strong[mask],
            pseudo_labels[mask]
        )
    else:
        loss_unsup = torch.tensor(0.0, device=x_labeled.device)
    
    # Total loss
    total_loss = loss_sup + lambda_u * loss_unsup
    
    # Statistics
    stats = {
        'loss_total': total_loss.item(),
        'loss_sup': loss_sup.item(),
        'loss_unsup': loss_unsup.item(),
        'mask_ratio': mask.float().mean().item()
    }
    
    return total_loss, stats
text

└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q14: Implement Label Propagation for graph-based SSL                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
Python

import numpy as np
from scipy.spatial.distance import cdist

def label_propagation(X, y_labeled, labeled_mask, n_classes,
                      sigma=1.0, max_iter=1000, tol=1e-6):
    """
    Label Propagation algorithm
    
    Parameters:
    -----------
    X : data matrix (n_samples, n_features)
    y_labeled : labels for labeled points (only used where labeled_mask=True)
    labeled_mask : boolean array, True for labeled points
    n_classes : number of classes
    sigma : Gaussian kernel bandwidth
    max_iter : maximum iterations
    tol : convergence tolerance
    
    Returns:
    --------
    predictions : predicted labels for all points
    Y : label distribution matrix
    """
    n = len(X)
    
    # Build weight matrix (Gaussian kernel)
    distances = cdist(X, X, metric='euclidean')
    W = np.exp(-distances**2 / (2 * sigma**2))
    np.fill_diagonal(W, 0)  # No self-loops
    
    # Compute transition matrix T = D^(-1) W
    D = np.diag(W.sum(axis=1) + 1e-10)
    D_inv = np.linalg.inv(D)
    T = D_inv @ W
    
    # Initialize label matrix
    Y = np.zeros((n, n_classes))
    for i in range(n):
        if labeled_mask[i]:
            Y[i, y_labeled[i]] = 1.0  # One-hot for labeled
        else:
            Y[i, :] = 1.0 / n_classes  # Uniform for unlabeled
    
    Y_original = Y.copy()
    
    # Iterate
    for iteration in range(max_iter):
        Y_new = T @ Y
        
        # Clamp labeled points
        Y_new[labeled_mask] = Y_original[labeled_mask]
        
        # Check convergence
        diff = np.abs(Y_new - Y).max()
        Y = Y_new
        
        if diff < tol:
            print(f"Converged at iteration {iteration}")
            break
    
    # Predictions
    predictions = np.argmax(Y, axis=1)
    
    return predictions, Y


# Example usage:
if __name__ == "__main__":
    # Generate two clusters
    np.random.seed(42)
    X0 = np.random.randn(50, 2) + [0, 0]
    X1 = np.random.randn(50, 2) + [4, 4]
    X = np.vstack([X0, X1])
    y_true = np.array([0]*50 + [1]*50)
    
    # Label only 2 points per class
    labeled_mask = np.zeros(100, dtype=bool)
    labeled_mask[[0, 1, 50, 51]] = True
    
    # Run label propagation
    predictions, Y = label_propagation(
        X, y_true, labeled_mask, n_classes=2, sigma=1.0
    )
    
    accuracy = (predictions == y_true).mean()
    print(f"Accuracy: {accuracy:.4f}")
text

└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q15: How would you implement curriculum learning for SSL?                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
Python

import numpy as np

def curriculum_threshold_schedule(current_step, total_steps, 
                                   min_threshold=0.5, max_threshold=0.95,
                                   schedule='linear'):
    """
    Curriculum learning: gradually increase threshold
    
    Start with lower threshold (more pseudo-labels, easier task)
    End with higher threshold (fewer but cleaner pseudo-labels)
    
    Parameters:
    -----------
    current_step : current training step
    total_steps : total training steps
    min_threshold : starting threshold
    max_threshold : ending threshold
    schedule : 'linear', 'exponential', or 'cosine'
    
    Returns:
    --------
    threshold : current threshold value
    """
    progress = min(1.0, current_step / total_steps)
    
    if schedule == 'linear':
        threshold = min_threshold + progress * (max_threshold - min_threshold)
        
    elif schedule == 'exponential':
        # Slow start, fast end
        threshold = min_threshold + (1 - np.exp(-5 * progress)) * \
                    (max_threshold - min_threshold)
        
    elif schedule == 'cosine':
        # Smooth transition
        threshold = min_threshold + 0.5 * (1 - np.cos(np.pi * progress)) * \
                    (max_threshold - min_threshold)
    
    return threshold


def curriculum_self_training(model, X_labeled, y_labeled, X_unlabeled,
                             epochs=100, samples_per_epoch=1000):
    """
    Self-training with curriculum learning
    
    Easy samples (high confidence) first, gradually include harder ones
    """
    
    for epoch in range(epochs):
        # Compute current threshold
        threshold = curriculum_threshold_schedule(
            epoch, epochs, 
            min_threshold=0.7, 
            max_threshold=0.95
        )
        
        # Get pseudo-labels
        with torch.no_grad():
            probs = model(X_unlabeled).softmax(dim=1)
            max_probs, pseudo_labels = probs.max(dim=1)
            
            # Select samples above current threshold
            mask = max_probs >= threshold
        
        print(f"Epoch {epoch}: threshold={threshold:.3f}, "
              f"using {mask.sum()}/{len(mask)} unlabeled samples")
        
        # Train on selected samples
        # ... training code ...
text

└─────────────────────────────────────────────────────────────────────────────┘
18.3 Scenario-Based Questions
text

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q16: You have 100 labeled images and 100,000 unlabeled images.            │
│      How would you approach this problem?                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ STEP 1: VERIFY ASSUMPTIONS                                                 │
│ • Check that labeled/unlabeled come from same distribution                │
│ • Verify class balance in labeled set                                     │
│ • Ensure labeled set covers all classes                                   │
│                                                                             │
│ STEP 2: ESTABLISH BASELINES                                                │
│ • Supervised baseline on 100 labeled only                                 │
│ • Check if baseline is reasonable (above random)                          │
│                                                                             │
│ STEP 3: CHOOSE SSL METHOD                                                  │
│ For image classification, I would start with FixMatch because:            │
│ • Simple and effective                                                    │
│ • State-of-the-art performance                                           │
│ • Well-documented and reproducible                                        │
│                                                                             │
│ STEP 4: IMPLEMENTATION DETAILS                                             │
│ • Architecture: WideResNet-28-2 or ResNet-50                             │
│ • Strong augmentation: RandAugment(n=2, m=10)                            │
│ • Threshold: Start with 0.95                                              │
│ • Batch ratio: 64 labeled + 448 unlabeled                                │
│ • Training: Long training (100K+ steps)                                   │
│                                                                             │
│ STEP 5: MONITOR AND ADJUST                                                 │
│ • Watch mask ratio (should increase during training)                      │
│ • Check class balance of pseudo-labels                                    │
│ • If one class dominates → use FlexMatch                                  │
│                                                                             │
│ EXPECTED IMPROVEMENT: From ~40% (supervised) to ~85-90% (FixMatch)        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q17: SSL is making your model perform WORSE than supervised baseline.     │
│      How would you debug this?                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ DEBUGGING CHECKLIST:                                                        │
│                                                                             │
│ 1. CHECK DATA DISTRIBUTION                                                 │
│    • Are labeled and unlabeled from same distribution?                    │
│    • Plot samples from both sets - do they look similar?                  │
│    • Does unlabeled contain classes not in labeled?                       │
│    → FIX: Filter unlabeled data or use open-set SSL methods             │
│                                                                             │
│ 2. CHECK AUGMENTATIONS                                                     │
│    • Visualize augmented samples - are they valid?                        │
│    • Is strong augmentation too strong?                                   │
│    • Are augmentations semantic-preserving?                               │
│    → FIX: Reduce augmentation strength or use different operations       │
│                                                                             │
│ 3. CHECK PSEUDO-LABEL QUALITY                                              │
│    • What's the mask ratio? (too low = no learning, too high = noise)    │
│    • If you have ground truth: what's pseudo-label accuracy?             │
│    • Class distribution of pseudo-labels balanced?                        │
│    → FIX: Adjust threshold, use per-class thresholds                     │
│                                                                             │
│ 4. CHECK CONFIRMATION BIAS                                                 │
│    • Does accuracy rise then fall?                                        │
│    • Is model becoming overconfident?                                     │
│    → FIX: Lower unsupervised weight, use Mean Teacher                    │
│                                                                             │
│ 5. CHECK HYPERPARAMETERS                                                   │
│    • Is unsupervised loss weight too high?                               │
│    • Is learning rate appropriate?                                        │
│    • Is training long enough for ramp-up?                                 │
│    → FIX: Grid search on validation set                                  │
│                                                                             │
│ 6. FALLBACK                                                                │
│    • Try simpler SSL method (basic pseudo-labeling)                       │
│    • If nothing works, SSL assumptions may not hold for your data        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q18: How would you apply SSL to text classification?                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ TEXT SSL DIFFERS FROM IMAGE SSL:                                           │
│ • Text augmentation is less obvious than image augmentation               │
│ • Pre-trained models (BERT) are commonly available                        │
│ • Sequences have variable length                                          │
│                                                                             │
│ APPROACH 1: UDA FOR TEXT                                                   │
│ ─────────────────────────                                                   │
│ • Weak augmentation: Identity (no change)                                 │
│ • Strong augmentation: Back-translation                                   │
│   - Translate to another language and back                                │
│   - "I love this movie" → German → "I really like this film"             │
│ • Apply consistency regularization                                        │
│                                                                             │
│ APPROACH 2: SELF-TRAINING WITH BERT                                        │
│ ─────────────────────────────────────                                       │
│ 1. Fine-tune BERT on labeled data                                         │
│ 2. Pseudo-label unlabeled data                                            │
│ 3. Continue training on combined data                                     │
│ 4. Iterate                                                                 │
│                                                                             │
│ TEXT AUGMENTATION OPTIONS:                                                  │
│ • Synonym replacement (WordNet)                                           │
│ • Random insertion/deletion/swap                                          │
│ • Back-translation (best for semantics)                                   │
│ • Contextual word replacement (MLM-based)                                 │
│ • Sentence paraphrase models                                              │
│                                                                             │
│ EXAMPLE PIPELINE:                                                           │
│ 1. Pre-trained BERT encoder                                               │
│ 2. Classification head                                                    │
│ 3. FixMatch-style training:                                               │
│    - Weak: original text                                                  │
│    - Strong: back-translated text                                         │
│    - Threshold: 0.95                                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q19: Compare SSL with Active Learning. When would you use each?            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ ┌────────────────────┬──────────────────────┬──────────────────────┐       │
│ │ Aspect             │ SSL                  │ Active Learning      │       │
│ ├────────────────────┼──────────────────────┼──────────────────────┤       │
│ │ Uses unlabeled     │ ✓ Yes               │ ✓ Yes (to select)    │       │
│ │ data               │                      │                      │       │
│ │                    │                      │                      │       │
│ │ Requires labeling  │ ✗ No (uses          │ ✓ Yes (iteratively) │       │
│ │ oracle             │    existing)         │                      │       │
│ │                    │                      │                      │       │
│ │ Human-in-the-loop  │ ✗ No                │ ✓ Yes               │       │
│ │                    │                      │                      │       │
│ │ Goal               │ Use structure of    │ Choose WHICH samples│       │
│ │                    │ unlabeled data      │ to label            │       │
│ │                    │                      │                      │       │
│ │ When to use        │ Labels expensive,   │ Can label MORE data,│       │
│ │                    │ no more coming      │ need to be efficient│       │
│ └────────────────────┴──────────────────────┴──────────────────────┘       │
│                                                                             │
│ USE SSL WHEN:                                                               │
│ • You cannot label any more data                                          │
│ • Labeling oracle is unavailable                                          │
│ • You have fixed labeled set already                                      │
│                                                                             │
│ USE ACTIVE LEARNING WHEN:                                                   │
│ • You have limited labeling budget                                        │
│ • Expert is available for labeling                                        │
│ • You want to maximize impact of each label                               │
│                                                                             │
│ COMBINE BOTH:                                                               │
│ 1. Use SSL to identify uncertain samples                                  │
│ 2. Query most informative ones for labeling                               │
│ 3. Retrain with new labels + SSL on remaining                             │
│ → Best of both worlds!                                                    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ Q20: How would you evaluate if SSL is working correctly?                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ ANSWER:                                                                     │
│                                                                             │
│ METRICS TO MONITOR:                                                         │
│                                                                             │
│ 1. PRIMARY METRICS:                                                        │
│    • Test accuracy (vs supervised baseline)                               │
│    • Learning curves (train/test over time)                               │
│                                                                             │
│ 2. PSEUDO-LABEL METRICS:                                                   │
│    • Mask ratio over time (should increase gradually)                     │
│    • Pseudo-label accuracy (if ground truth available)                    │
│    • Class distribution of pseudo-labels                                  │
│                                                                             │
│ 3. LOSS COMPONENTS:                                                        │
│    • Supervised loss (should decrease)                                    │
│    • Unsupervised loss (should decrease)                                  │
│    • Ratio between them                                                   │
│                                                                             │
│ 4. CONFIDENCE CALIBRATION:                                                 │
│    • Expected Calibration Error (ECE)                                     │
│    • Reliability diagram                                                  │
│    • Is model overconfident?                                              │
│                                                                             │
│ EXPERIMENTS TO RUN:                                                         │
│                                                                             │
│ 1. BASELINE COMPARISON:                                                    │
│    • Supervised on labeled only                                           │
│    • SSL method on labeled + unlabeled                                    │
│    • (Upper bound) Supervised on all data if labels available            │
│                                                                             │
│ 2. ABLATION STUDIES:                                                       │
│    • Effect of threshold                                                  │
│    • Effect of unsupervised weight                                        │
│    • Effect of augmentation strength                                      │
│    • Effect of amount of unlabeled data                                   │
│                                                                             │
│ 3. ROBUSTNESS CHECKS:                                                      │
│    • Multiple random seeds (report mean ± std)                            │
│    • Different labeled sample selections                                  │
│    • Different amounts of labeled data                                    │
│                                                                             │
│ SUCCESS CRITERIA:                                                           │
│ ✓ SSL > Supervised baseline (statistically significant)                   │
│ ✓ Mask ratio increases over training                                      │
│ ✓ No accuracy collapse after initial gains                               │
│ ✓ Consistent across multiple runs                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
18.4 Quick Reference Cheat Sheet
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    SSL QUICK REFERENCE CHEAT SHEET                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│ WHEN TO USE SSL:                                                           │
│ ✓ Few labels, many unlabeled samples                                      │
│ ✓ Labeling is expensive/time-consuming                                    │
│ ✓ Same distribution for labeled and unlabeled                             │
│ ✗ Lots of labeled data available                                          │
│ ✗ Distribution mismatch                                                   │
│                                                                             │
│ THREE KEY ASSUMPTIONS:                                                      │
│ 1. Smoothness: nearby points → similar labels                             │
│ 2. Cluster: same cluster → same label                                     │
│ 3. Manifold: data lies on low-dimensional manifold                        │
│                                                                             │
│ METHOD SELECTION GUIDE:                                                     │
│ • First try: FixMatch (simple + effective)                                │
│ • Class imbalance: FlexMatch                                              │
│ • Noisy labels: Mean Teacher                                              │
│ • Small data: Graph-based methods                                         │
│ • Text data: UDA with back-translation                                    │
│ • Need interpretability: Self-training                                    │
│                                                                             │
│ KEY HYPERPARAMETERS:                                                        │
│ • Threshold τ: 0.95 (FixMatch default)                                    │
│ • Unsupervised weight λ: 1.0                                              │
│ • Batch ratio (labeled:unlabeled): 1:7                                    │
│ • EMA decay α: 0.999 (Mean Teacher)                                       │
│ • Training: Longer than supervised (2x-10x)                               │
│                                                                             │
│ DEBUGGING CHECKLIST:                                                        │
│ □ Check data distributions match                                          │
│ □ Visualize augmentations                                                 │
│ □ Monitor mask ratio                                                      │
│ □ Check class balance of pseudo-labels                                    │
│ □ Verify supervised loss decreasing                                       │
│                                                                             │
│ COMMON ISSUES:                                                              │
│ • Mask ratio = 0% → Lower threshold                                       │
│ • One class dominates → Per-class thresholds                             │
│ • Accuracy drops → Confirmation bias, use EMA teacher                    │
│ • SSL worse than supervised → Distribution mismatch                       │
│                                                                             │
│ STATE-OF-THE-ART RESULTS (CIFAR-10, 40 labels):                           │
│ • Supervised: ~25%                                                        │
│ • FixMatch: ~92%                                                          │
│ • FlexMatch: ~95%                                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
📚 Summary & Key Takeaways
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    FINAL SUMMARY                                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   WHAT YOU'VE LEARNED:                                                     │
│   ────────────────────                                                      │
│                                                                             │
│   ✓ Fundamentals of Semi-Supervised Learning                              │
│   ✓ Three core assumptions (smoothness, cluster, manifold)                │
│   ✓ Self-training and pseudo-labeling                                     │
│   ✓ Co-training for multi-view data                                       │
│   ✓ Graph-based methods (Label Propagation)                               │
│   ✓ Generative approaches (GMM)                                           │
│   ✓ Consistency regularization (Π-Model, Mean Teacher)                    │
│   ✓ Modern deep SSL (MixMatch, FixMatch, FlexMatch)                       │
│   ✓ Practical implementation from scratch                                 │
│   ✓ Debugging and troubleshooting                                         │
│   ✓ Real-world applications                                               │
│                                                                             │
│   KEY INSIGHTS TO REMEMBER:                                                │
│   ──────────────────────────                                                │
│                                                                             │
│   1. SSL uses DATA STRUCTURE from unlabeled samples                       │
│                                                                             │
│   2. Assumptions MUST hold for SSL to help                                │
│                                                                             │
│   3. Strong augmentation is CRUCIAL for modern SSL                        │
│                                                                             │
│   4. Confirmation bias is the main ENEMY                                  │
│                                                                             │
│   5. Simple methods (FixMatch) often beat complex ones                    │
│                                                                             │
│   6. Monitor pseudo-label quality during training                         │
│                                                                             │
│   7. SSL + Self-supervised pre-training is powerful combo                 │
│                                                                             │
│                                                                             │
│   YOUR NEXT STEPS:                                                         │
│   ────────────────                                                          │
│                                                                             │
│   1. Implement FixMatch on a real dataset                                 │
│   2. Experiment with different augmentation strategies                    │
│   3. Try combining SSL with pre-trained models                            │
│   4. Apply to your domain-specific problem                                │
│   5. Read latest papers (FlexMatch, CoMatch, etc.)                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

                    🎓 CONGRATULATIONS! 🎓
                    
     You now have comprehensive knowledge of Semi-Supervised Learning
            from basic concepts to state-of-the-art methods!
            
          Go forth and build amazing SSL applications! 🚀
📖 Appendix: Recommended Resources
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                    FURTHER READING                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   FOUNDATIONAL PAPERS:                                                     │
│   ────────────────────                                                      │
│   • "Semi-Supervised Learning" - Chapelle et al. (2006) - THE book        │
│   • "Pseudo-Label" - Lee (2013)                                           │
│   • "Mean Teachers" - Tarvainen & Valpola (2017)                          │
│   • "MixMatch" - Berthelot et al. (2019)                                  │
│   • "FixMatch" - Sohn et al. (2020)                                       │
│   • "FlexMatch" - Zhang et al. (2021)                                     │
│                                                                             │
│   CODE REPOSITORIES:                                                       │
│   ──────────────────                                                        │
│   • TorchSSL: github.com/TorchSSL/TorchSSL                               │
│   • USB: github.com/microsoft/Semi-supervised-learning                    │
│   • FixMatch-pytorch: github.com/kekmodel/FixMatch-pytorch               │
│                                                                             │
│   TUTORIALS & COURSES:                                                     │
│   ────────────────────                                                      │
│   • Stanford CS229 (Machine Learning)                                     │
│   • CMU 10-708 (Probabilistic Graphical Models)                          │
│   • Google AI Blog posts on SSL                                           │
│                                                                             │
│   BENCHMARK DATASETS:                                                      │
│   ───────────────────                                                       │
│   • CIFAR-10/100 (images)                                                 │
│   • STL-10 (images, designed for SSL)                                     │
│   • SVHN (street view house numbers)                                      │
│   • Mini-ImageNet (few-shot learning)                                     │
│   • AG News, IMDB (text classification)                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
End of Document

This comprehensive guide covers Semi-Supervised Learning from fundamentals to state-of-the-art methods. Use it as a reference for learning, interviews, and practical implementations.






