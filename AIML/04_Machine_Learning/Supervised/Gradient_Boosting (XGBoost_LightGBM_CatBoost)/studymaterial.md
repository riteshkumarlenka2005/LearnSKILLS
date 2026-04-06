The Ultimate Guide to Gradient Boosting: XGBoost, LightGBM & CatBoost
From Zero to Hero - A Complete Learning Journey
📚 TABLE OF CONTENTS
Foundation: Understanding the Basics
The Boosting Revolution
Gradient Boosting Deep Dive
XGBoost Mastery
LightGBM Mastery
CatBoost Mastery
Comparative Analysis
Hyperparameter Tuning Bible
Real-World Implementation
Advanced Techniques & Tricks
Production Deployment
Interview Preparation
Chapter 1: Foundation - Understanding the Basics
1.1 What is Machine Learning? (The Simplest Explanation)
Imagine you're teaching a child to recognize fruits:

text

Day 1: You show an apple → "This is apple" (red, round)
Day 2: You show a banana → "This is banana" (yellow, curved)
Day 3: Child sees a new apple → "Apple!" ✓

This is LEARNING FROM EXAMPLES = Machine Learning
The Three Types of Machine Learning
text

┌─────────────────────────────────────────────────────────────────┐
│                    MACHINE LEARNING TYPES                        │
├─────────────────────┬──────────────────────┬────────────────────┤
│   SUPERVISED        │    UNSUPERVISED      │   REINFORCEMENT    │
│                     │                      │                    │
│ • Has labels        │ • No labels          │ • Learn by rewards │
│ • Teacher guides    │ • Find patterns      │ • Trial and error  │
│                     │                      │                    │
│ Examples:           │ Examples:            │ Examples:          │
│ • Spam detection    │ • Customer segments  │ • Game playing     │
│ • Price prediction  │ • Anomaly detection  │ • Robot walking    │
│ • Disease diagnosis │ • Topic modeling     │ • Self-driving car │
└─────────────────────┴──────────────────────┴────────────────────┘
Gradient Boosting = Supervised Learning (We have input-output pairs)

1.2 What is a Decision Tree? (The Building Block)
Real-Life Analogy: The 20 Questions Game
Think of playing "20 Questions" to guess an animal:

text

                    Is it a mammal?
                    /            \
                  YES             NO
                  /                \
         Does it have 4 legs?    Does it fly?
            /        \            /        \
          YES        NO         YES        NO
          /           \          /          \
      Is it big?    Human?   Is it big?    Fish?
       /    \                  /    \
     YES    NO              YES     NO
      |      |               |       |
   Elephant Dog           Eagle   Sparrow
Decision Tree Components
text

┌─────────────────────────────────────────────────────────────────┐
│                    DECISION TREE ANATOMY                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│                        [ROOT NODE]                               │
│                      "Age > 30?"                                 │
│                        /      \                                  │
│                      YES       NO                                │
│                      /          \                                │
│            [INTERNAL NODE]    [INTERNAL NODE]                    │
│            "Income > 50K?"    "Student?"                         │
│               /      \          /      \                         │
│             YES      NO       YES      NO                        │
│              |        |        |        |                        │
│           [LEAF]  [LEAF]   [LEAF]   [LEAF]                       │
│           "Buy"   "No"     "Buy"    "No"                         │
│                                                                  │
├─────────────────────────────────────────────────────────────────┤
│ ROOT NODE    : First question (top of tree)                      │
│ INTERNAL NODE: Questions in the middle                           │
│ LEAF NODE    : Final answers (predictions)                       │
│ BRANCH       : Connections (YES/NO paths)                        │
│ DEPTH        : Number of levels from root to leaf                │
└─────────────────────────────────────────────────────────────────┘
How Does a Tree Make Decisions?
Python

# Simple Decision Tree Logic
def predict_loan_approval(age, income, credit_score):
    # Level 1: Root Question
    if credit_score > 700:
        # Level 2: Left Branch
        if income > 50000:
            return "APPROVED"  # Leaf
        else:
            return "REVIEW"    # Leaf
    else:
        # Level 2: Right Branch
        if age > 25 and income > 40000:
            return "REVIEW"    # Leaf
        else:
            return "REJECTED"  # Leaf
Visual Example with Data
text

DATASET: Should we play tennis?

| Day | Outlook  | Temperature | Humidity | Wind   | Play? |
|-----|----------|-------------|----------|--------|-------|
| 1   | Sunny    | Hot         | High     | Weak   | No    |
| 2   | Sunny    | Hot         | High     | Strong | No    |
| 3   | Overcast | Hot         | High     | Weak   | Yes   |
| 4   | Rain     | Mild        | High     | Weak   | Yes   |
| 5   | Rain     | Cool        | Normal   | Weak   | Yes   |
| 6   | Rain     | Cool        | Normal   | Strong | No    |
| 7   | Overcast | Cool        | Normal   | Strong | Yes   |
| 8   | Sunny    | Mild        | High     | Weak   | No    |
| 9   | Sunny    | Cool        | Normal   | Weak   | Yes   |
| 10  | Rain     | Mild        | Normal   | Weak   | Yes   |

RESULTING TREE:

                        Outlook?
                    /      |       \
                Sunny   Overcast   Rain
                  |        |         |
            Humidity?    YES     Wind?
              /    \              /    \
          High   Normal       Weak   Strong
           |        |           |       |
          NO       YES        YES      NO
1.3 How Trees Split Data (The Math Made Simple)
The Goal: Create Pure Groups
text

IMPURE GROUP                    PURE GROUPS
┌──────────────┐               ┌───────┐ ┌───────┐
│ 🍎🍎🍊🍎🍊🍊 │   SPLIT →   │🍎🍎🍎│ │🍊🍊🍊│
│  Mixed       │               │ Pure  │ │ Pure  │
└──────────────┘               └───────┘ └───────┘
Measuring Impurity: Gini Index
text

GINI FORMULA:
Gini = 1 - Σ(pi)²

Where pi = probability of class i

EXAMPLE:
Group A: 50 apples, 50 oranges
- P(apple) = 0.5, P(orange) = 0.5
- Gini = 1 - (0.5² + 0.5²) = 1 - 0.5 = 0.5 (IMPURE!)

Group B: 100 apples, 0 oranges  
- P(apple) = 1.0, P(orange) = 0.0
- Gini = 1 - (1.0² + 0.0²) = 1 - 1 = 0 (PURE!)
Visual Gini Scale
text

GINI VALUE INTERPRETATION:

0.0                    0.25                   0.5
 |──────────────────────|──────────────────────|
PURE                 MODERATE               MAXIMUM
                                            IMPURITY
🍎🍎🍎🍎              🍎🍎🍎🍊               🍎🍎🍊🍊
All same             Mostly one             Equal mix
Measuring Impurity: Entropy
text

ENTROPY FORMULA:
Entropy = -Σ pi × log₂(pi)

EXAMPLE:
Group: 50% apples, 50% oranges
Entropy = -(0.5 × log₂(0.5) + 0.5 × log₂(0.5))
        = -(0.5 × -1 + 0.5 × -1)
        = -(-0.5 - 0.5)
        = 1.0 (MAXIMUM DISORDER!)

Group: 100% apples
Entropy = -(1.0 × log₂(1.0))
        = -(1.0 × 0)
        = 0 (PERFECT ORDER!)
Information Gain: Choosing the Best Split
text

INFORMATION GAIN = Entropy(Parent) - Weighted Avg Entropy(Children)

EXAMPLE:
Parent Node: 14 samples (9 Yes, 5 No)
- Entropy(Parent) = 0.94

After splitting on "Outlook":
- Sunny: 5 samples (2 Yes, 3 No) → Entropy = 0.97
- Overcast: 4 samples (4 Yes, 0 No) → Entropy = 0
- Rain: 5 samples (3 Yes, 2 No) → Entropy = 0.97

Weighted Average = (5/14)×0.97 + (4/14)×0 + (5/14)×0.97 = 0.69

INFORMATION GAIN = 0.94 - 0.69 = 0.25 ✓

Higher Information Gain = Better Split!
1.4 Single Tree vs Multiple Trees
The Problem with Single Trees
text

SINGLE DECISION TREE PROBLEMS:

1. OVERFITTING (Memorizes training data)
   ┌─────────────────────────────────────────┐
   │ Training Accuracy: 99%  ←── Too good!   │
   │ Testing Accuracy:  60%  ←── Reality     │
   └─────────────────────────────────────────┘

2. HIGH VARIANCE (Small data change = Big tree change)
   Dataset A → Tree Shape: /\
   Dataset B → Tree Shape: \/  (Completely different!)

3. UNSTABLE
   Remove 1 data point → Entire tree structure changes
The Solution: Use Many Trees!
text

ENSEMBLE METHODS (Combining Multiple Trees)

┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│    Tree 1        Tree 2        Tree 3        Tree 4             │
│      /\            |            /|\           /\                │
│     /  \          /|\          / | \         /  \               │
│    ▲    ▲        ▲ ▲ ▲        ▲  ▲  ▲       ▲    ▲              │
│    │    │        │ │ │        │  │  │       │    │              │
│   Cat  Dog      Cat Cat Dog  Cat Dog Cat   Dog  Cat             │
│                                                                  │
│              COMBINE ALL PREDICTIONS                             │
│                      ↓                                           │
│              VOTING: Cat=5, Dog=3                                │
│                      ↓                                           │
│              FINAL: "CAT" ✓                                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
Ensemble Philosophy
text

"The wisdom of the crowd beats individual experts"

Example: Guess the weight of a cow
- Expert 1: 1000 kg (wrong by 200)
- Expert 2: 1300 kg (wrong by 100)
- Expert 3: 1100 kg (wrong by 100)
- Expert 4: 1250 kg (wrong by 50)
- Expert 5: 1150 kg (wrong by 50)

Average: (1000+1300+1100+1250+1150)/5 = 1160 kg
Actual: 1200 kg
Error of average: Only 40 kg! (Better than most experts!)
Chapter 2: The Boosting Revolution
2.1 Understanding Ensemble Methods
The Three Main Ensemble Strategies
text

┌─────────────────────────────────────────────────────────────────────┐
│                    ENSEMBLE METHODS OVERVIEW                         │
├─────────────────────┬─────────────────────┬─────────────────────────┤
│      BAGGING        │      BOOSTING       │       STACKING          │
│                     │                     │                         │
│   Trees in         │   Trees in          │   Different models      │
│   PARALLEL         │   SEQUENCE          │   LAYERED               │
│                     │                     │                         │
│   ┌─┐ ┌─┐ ┌─┐      │   ┌─┐→┌─┐→┌─┐      │   ┌─────────────┐       │
│   │1│ │2│ │3│      │   │1│ │2│ │3│      │   │ Meta-Model  │       │
│   └─┘ └─┘ └─┘      │   └─┘ └─┘ └─┘      │   └─────────────┘       │
│      \  |  /        │                     │     ↑   ↑   ↑          │
│       \ | /         │   Each tree learns  │   ┌─┐ ┌─┐ ┌─┐         │
│      [VOTE]         │   from previous     │   │A│ │B│ │C│         │
│                     │   tree's MISTAKES   │   └─┘ └─┘ └─┘         │
│   Example:          │                     │   Different algorithms │
│   Random Forest     │   Example:          │                        │
│                     │   XGBoost, LightGBM │   Example:             │
│                     │   CatBoost          │   Blend of models      │
└─────────────────────┴─────────────────────┴─────────────────────────┘
2.2 Bagging vs Boosting: Deep Comparison
Bagging (Bootstrap Aggregating)
text

BAGGING PROCESS:

Original Dataset: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

Step 1: Create Bootstrap Samples (Random sampling WITH replacement)
┌────────────────────────────────────────────────────────────┐
│ Sample 1: [1, 1, 3, 5, 5, 6, 8, 8, 9, 10]                  │
│ Sample 2: [2, 2, 3, 4, 4, 6, 7, 9, 9, 10]                  │
│ Sample 3: [1, 3, 3, 4, 5, 7, 7, 8, 10, 10]                 │
└────────────────────────────────────────────────────────────┘

Step 2: Train Independent Trees on Each Sample
┌─────────┐    ┌─────────┐    ┌─────────┐
│ Tree 1  │    │ Tree 2  │    │ Tree 3  │
│  (on    │    │  (on    │    │  (on    │
│Sample 1)│    │Sample 2)│    │Sample 3)│
└─────────┘    └─────────┘    └─────────┘
     │              │              │
     ↓              ↓              ↓
   Pred A        Pred B        Pred C

Step 3: Combine Predictions
┌────────────────────────────────────────────────────────────┐
│ Classification: VOTING (majority wins)                      │
│ Regression: AVERAGING (mean of predictions)                 │
└────────────────────────────────────────────────────────────┘
Boosting (The Star of Our Show!)
text

BOOSTING PROCESS:

Original Dataset with Initial Weights: All samples equal weight

ROUND 1:
┌─────────────────────────────────────────────────────────────┐
│ Train Tree 1 on weighted data                               │
│                                                             │
│ Sample: [1, 2, 3, 4, 5]  Weights: [1, 1, 1, 1, 1]           │
│                                                             │
│ Tree 1 Predictions: [✓, ✓, ✗, ✓, ✗]                         │
│                          ↑       ↑                          │
│                     Wrong predictions!                      │
│                                                             │
│ INCREASE weights of wrong samples!                          │
│ New Weights: [1, 1, 2, 1, 2]                                │
└─────────────────────────────────────────────────────────────┘

ROUND 2:
┌─────────────────────────────────────────────────────────────┐
│ Train Tree 2 on RE-WEIGHTED data                            │
│                                                             │
│ Samples 3 and 5 are now MORE IMPORTANT                      │
│ Tree 2 focuses on fixing those mistakes!                    │
│                                                             │
│ Tree 2 Predictions: [✗, ✓, ✓, ✓, ✓]                         │
│                      ↑                                      │
│                  New mistake!                               │
│                                                             │
│ Update weights again...                                     │
└─────────────────────────────────────────────────────────────┘

FINAL PREDICTION:
┌─────────────────────────────────────────────────────────────┐
│ Combine all trees with their respective weights             │
│                                                             │
│ Final = α₁×Tree1 + α₂×Tree2 + α₃×Tree3 + ...               │
│                                                             │
│ Where α = tree's importance (based on accuracy)             │
└─────────────────────────────────────────────────────────────┘
Side-by-Side Comparison
text

┌────────────────────┬────────────────────────┬────────────────────────┐
│     ASPECT         │        BAGGING         │        BOOSTING        │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Training           │ Parallel               │ Sequential             │
│                    │ (Independent)          │ (One after another)    │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Sample Weights     │ Equal weights          │ Adaptive weights       │
│                    │ (Bootstrap sampling)   │ (Focus on errors)      │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Tree Strength      │ Strong trees (deep)    │ Weak trees (shallow)   │
│                    │                        │ "Weak learners"        │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Error Reduction    │ Reduces VARIANCE       │ Reduces BIAS           │
│                    │ (Stabilizes)           │ (Corrects errors)      │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Overfitting Risk   │ Low                    │ Higher (need control)  │
├────────────────────┼────────────────────────┼────────────────────────┤
│ Example Algorithm  │ Random Forest          │ XGBoost, LightGBM      │
│                    │                        │ CatBoost, AdaBoost     │
└────────────────────┴────────────────────────┴────────────────────────┘
2.3 The Evolution of Boosting Algorithms
text

TIMELINE OF BOOSTING:

1990 ──── 1995 ──── 1999 ──── 2014 ──── 2017 ──── Present
  │         │         │         │         │          │
  ↓         ↓         ↓         ↓         ↓          ↓
┌─────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐
│Boost│  │ Ada  │  │ Grad │  │  XG  │  │Light │  │ Cat  │
│ ing │→ │Boost │→ │Boost │→ │Boost │→ │ GBM  │→ │Boost │
│Idea │  │      │  │      │  │      │  │      │  │      │
└─────┘  └──────┘  └──────┘  └──────┘  └──────┘  └──────┘
  │         │         │         │         │          │
Theory   First     Uses      Fast +    Super     Handles
born    practical  gradients  Scalable  Fast    categories
       algorithm             Regularized Histogram naturally
Chapter 3: Gradient Boosting Deep Dive
3.1 The Intuition: Teaching by Focusing on Mistakes
Real-World Analogy: Learning to Shoot Arrows
text

ARCHERY TRAINING ANALOGY:

Round 1: First attempt
┌─────────────────────────────────────────┐
│                    ○ ← Target center    │
│                  ╱                      │
│                ╱                        │
│              ╱                          │
│            ●   ← Your shot (missed!)    │
│                                         │
│   Error = Distance from target          │
│   Error Vector: →→→ (direction to fix)  │
└─────────────────────────────────────────┘

Round 2: Aim to REDUCE the error
┌─────────────────────────────────────────┐
│                    ○ ← Target           │
│                  ●   ← Closer!          │
│                                         │
│   Previous position: way off            │
│   Current position: getting better      │
│   Remaining error: still some left      │
└─────────────────────────────────────────┘

Round 3, 4, 5...: Keep correcting
┌─────────────────────────────────────────┐
│                    ● ← Almost there!    │
│                    ○                    │
│                                         │
│   Each round: Fix remaining error       │
│   Eventually: Hit the target!           │
└─────────────────────────────────────────┘

This is EXACTLY how Gradient Boosting works!
Each tree fixes the RESIDUAL ERROR of previous trees.
3.2 Mathematical Foundation (Made Simple)
Step-by-Step Gradient Boosting Algorithm
text

THE ALGORITHM IN PLAIN ENGLISH:

1. Start with a simple prediction (usually the average)
2. Calculate errors (residuals) for all samples
3. Train a tree to predict these errors
4. Add this tree's predictions to our model (with a learning rate)
5. Calculate new errors
6. Repeat steps 3-5 until satisfied

MATHEMATICALLY:

Step 1: Initial Prediction
F₀(x) = average(y) for regression
      = log(odds) for classification

Step 2: For m = 1 to M (number of trees):
    
    a) Calculate Residuals (Errors):
       rᵢₘ = yᵢ - Fₘ₋₁(xᵢ)
       
       (What's left to predict = Actual - Current Prediction)
    
    b) Fit a tree hₘ(x) to predict residuals rᵢₘ
    
    c) Update the model:
       Fₘ(x) = Fₘ₋₁(x) + η × hₘ(x)
       
       Where η = learning rate (usually 0.01 to 0.3)

Step 3: Final Prediction:
F(x) = F₀(x) + η×h₁(x) + η×h₂(x) + ... + η×hₘ(x)
Visual Walkthrough with Numbers
text

EXAMPLE: Predicting House Prices

Actual Prices (y): [200, 250, 300, 350, 400] (in $1000s)

══════════════════════════════════════════════════════════════

ITERATION 0: Initial Prediction
┌─────────────────────────────────────────────────────────────┐
│ F₀ = average = (200+250+300+350+400)/5 = 300                │
│                                                             │
│ Initial Predictions: [300, 300, 300, 300, 300]              │
│ Actual Values:       [200, 250, 300, 350, 400]              │
│ Residuals (Errors):  [-100, -50, 0, 50, 100]                │
│                       ↑                    ↑                │
│                  Too high!            Too low!              │
└─────────────────────────────────────────────────────────────┘

══════════════════════════════════════════════════════════════

ITERATION 1: First Tree (Learning Rate η = 0.1)
┌─────────────────────────────────────────────────────────────┐
│ Tree 1 learns to predict residuals: [-100, -50, 0, 50, 100] │
│                                                             │
│ Tree 1 Predictions: [-80, -40, 10, 60, 90]                  │
│ (Not perfect, trees make approximations)                    │
│                                                             │
│ Updated Model: F₁ = F₀ + 0.1 × Tree1                        │
│                                                             │
│ New Predictions:                                            │
│ [300 + 0.1×(-80), 300 + 0.1×(-40), ...]                     │
│ = [292, 296, 301, 306, 309]                                 │
│                                                             │
│ New Residuals:                                              │
│ [200-292, 250-296, 300-301, 350-306, 400-309]               │
│ = [-92, -46, -1, 44, 91]                                    │
│                                                             │
│ Errors reduced slightly! Let's continue...                  │
└─────────────────────────────────────────────────────────────┘

══════════════════════════════════════════════════════════════

ITERATION 2: Second Tree
┌─────────────────────────────────────────────────────────────┐
│ Tree 2 learns NEW residuals: [-92, -46, -1, 44, 91]         │
│                                                             │
│ Tree 2 Predictions: [-85, -50, 5, 50, 85]                   │
│                                                             │
│ Updated Model: F₂ = F₁ + 0.1 × Tree2                        │
│                                                             │
│ New Predictions:                                            │
│ [292 + 0.1×(-85), 296 + 0.1×(-50), ...]                     │
│ = [283.5, 291, 301.5, 311, 317.5]                           │
│                                                             │
│ Errors getting smaller with each iteration!                 │
└─────────────────────────────────────────────────────────────┘

══════════════════════════════════════════════════════════════

AFTER MANY ITERATIONS:
┌─────────────────────────────────────────────────────────────┐
│ Final Predictions: [198, 251, 299, 352, 398]                │
│ Actual Values:     [200, 250, 300, 350, 400]                │
│ Final Errors:      [-2, 1, -1, 2, -2]                       │
│                                                             │
│ Almost perfect! 🎯                                           │
└─────────────────────────────────────────────────────────────┘
3.3 Why "Gradient" in Gradient Boosting?
The Connection to Calculus
text

GRADIENT = Direction of Steepest Descent

Imagine you're blindfolded on a hill, trying to reach the lowest point:

        ∧
       /  \
      /    \
     /      \
    /   YOU  \    ← Current position
   /    ↓     \
  /            \
 /     GOAL     \  ← Lowest point (minimum error)
/________________\

How do you find the way down?
Feel which direction slopes DOWN most steeply!
That direction = NEGATIVE GRADIENT

In Gradient Boosting:
- The "hill" = Loss Function (Error measure)
- "Going down" = Reducing error
- Each tree = One step in the steepest descent direction
Loss Functions Explained
text

COMMON LOSS FUNCTIONS:

FOR REGRESSION:
┌─────────────────────────────────────────────────────────────┐
│ Mean Squared Error (MSE):                                   │
│ L = (1/n) × Σ(yᵢ - ŷᵢ)²                                     │
│                                                             │
│ Example:                                                    │
│ Actual: 100, Predicted: 90                                  │
│ Error: (100-90)² = 100                                      │
│                                                             │
│ Gradient (derivative): -2(y - ŷ) = -2(100-90) = -20         │
│ Negative gradient: +20 (direction to increase prediction)  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ Mean Absolute Error (MAE):                                  │
│ L = (1/n) × Σ|yᵢ - ŷᵢ|                                      │
│                                                             │
│ More robust to outliers than MSE                            │
│ Gradient: sign(y - ŷ) = +1 or -1                            │
└─────────────────────────────────────────────────────────────┘

FOR CLASSIFICATION:
┌─────────────────────────────────────────────────────────────┐
│ Log Loss (Binary Cross-Entropy):                            │
│ L = -[y×log(p) + (1-y)×log(1-p)]                            │
│                                                             │
│ Where p = predicted probability                             │
│                                                             │
│ If actual = 1 and p = 0.9: Loss = -log(0.9) = 0.105 (low!)  │
│ If actual = 1 and p = 0.1: Loss = -log(0.1) = 2.303 (high!) │
└─────────────────────────────────────────────────────────────┘
Gradient Descent Visualization
text

LOSS FUNCTION LANDSCAPE:

Error │
  ▲   │
  │   │    ╱╲
  │   │   ╱  ╲        ╱╲
  │   │  ╱    ╲      ╱  ╲
  │   │ ╱      ╲    ╱    ╲
  │   │╱        ╲  ╱      ╲
  │   │          ╲╱        ╲
  │   │           ●         ╲   ← Global Minimum (Goal!)
  │   └────────────────────────────────▶ Parameters
  
Each tree moves us:
●→●→●→●→●→● (toward minimum)

Learning rate controls step size:
- Large η: Big jumps (might overshoot)
- Small η: Baby steps (slower but stable)
3.4 Residuals: The Heart of Gradient Boosting
Understanding Residuals
text

RESIDUAL = What's left unexplained = Actual - Predicted

VISUAL REPRESENTATION:

  y │
    │                    ● Actual
    │                    │
    │                    │ Residual (error)
    │                    │
    │                    ● Predicted
    │         ●─────────●
    │        ╱│
    │       ╱ │ Residual
    │      ╱  │
    │     ●   ● 
    │    ╱
    │   ╱ ← Prediction Line
    │──────────────────────▶ x

Each subsequent tree tries to predict these residuals!
Why Predicting Residuals Works
text

MATHEMATICAL INSIGHT:

True Value = Prediction + Residual
    y      =    ŷ₁     +   r₁

If we can predict residuals:
    y ≈ ŷ₁ + ŷ(r₁)
    y ≈ ŷ₁ + ŷ₂         (where ŷ₂ predicts r₁)

Still have residuals? Predict those too!
    y ≈ ŷ₁ + ŷ₂ + ŷ₃ + ... + ŷₙ

This is the ADDITIVE MODEL:
F(x) = Σ fₘ(x)

Each fₘ is a tree predicting the residuals from F₁ to Fₘ₋₁
Chapter 4: XGBoost Mastery
4.1 What is XGBoost?
text

XGBoost = eXtreme Gradient Boosting

Created by Tianqi Chen at University of Washington (2014)

WHY "EXTREME"?
┌─────────────────────────────────────────────────────────────────┐
│ 1. Extremely FAST (10x faster than traditional GB)              │
│ 2. Extremely ACCURATE (Won most Kaggle competitions 2015-2020)  │
│ 3. Extremely SCALABLE (Handles billions of rows)                │
│ 4. Extremely FLEXIBLE (Regression, Classification, Ranking)    │
└─────────────────────────────────────────────────────────────────┘

KAGGLE DOMINATION:
- 2015: 17 out of 29 winning solutions used XGBoost
- 2016-2019: Remained the most popular winning algorithm
- Used by almost every top data scientist
4.2 XGBoost's Secret Weapons
Key Innovation 1: Regularization
text

THE OVERFITTING PROBLEM:

Standard Gradient Boosting:
- Can create very complex models
- Tends to overfit on training data
- No built-in control

XGBoost Solution: REGULARIZATION

Objective = Loss + Ω(complexity)

┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│ Objective = Σ L(yᵢ, ŷᵢ) + Σ Ω(fₖ)                                │
│              ↑               ↑                                   │
│         How well we      Penalty for                             │
│         fit the data     complexity                              │
│                                                                  │
│ Where:                                                           │
│ Ω(f) = γT + ½λΣwⱼ²                                               │
│        ↑      ↑                                                  │
│    Penalty   L2 regularization                                   │
│    for       on leaf weights                                     │
│    number                                                        │
│    of leaves                                                     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘

INTUITION:
- γ (gamma): "Each new leaf must improve things by at least γ"
- λ (lambda): "Don't let leaf predictions get too extreme"
- α (alpha): L1 regularization (makes some weights zero)
Visual: Effect of Regularization
text

WITHOUT REGULARIZATION (Overfitting):
┌─────────────────────────────────────────┐
│     ●                                   │
│    ╱╲     ●                             │
│   ╱  ╲   ╱╲    ●                        │
│  ╱    ╲ ╱  ╲  ╱╲     ●                  │
│ ╱      ╳    ╲╱  ╲   ╱╲                  │
│╱       ╲        ╳  ╱  ╲                 │
│         ╲       ╲╱    ╲ ← Overly wiggly │
│                        ╲                │
│ Model memorizes every point!            │
└─────────────────────────────────────────┘

WITH REGULARIZATION (Good fit):
┌─────────────────────────────────────────┐
│     ●                                   │
│    ╱──────●                             │
│   ╱        ╲    ●                       │
│  ╱          ╲──╱╲    ●                  │
│ ╱                ╲──╱╲                  │
│╱                    ╲  ╲                │
│                       ╲──╲ ← Smooth     │
│                           ╲             │
│ Model captures the trend, not noise!    │
└─────────────────────────────────────────┘
Key Innovation 2: Second-Order Gradients
text

TRADITIONAL GB vs XGBOOST:

Traditional Gradient Boosting:
Uses first-order gradient (first derivative)
gᵢ = ∂L/∂ŷᵢ

XGBoost:
Uses BOTH first and second-order gradients!
gᵢ = ∂L/∂ŷᵢ        (gradient - direction)
hᵢ = ∂²L/∂ŷᵢ²      (hessian - curvature)

WHY DOES THIS MATTER?
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│ First derivative tells you: "Go this way"                        │
│ Second derivative tells you: "Go this way, THIS FAST"            │
│                                                                  │
│ Visual:                                                          │
│                                                                  │
│ Loss │                                                           │
│      │    ╱╲     First derivative: negative (go right)           │
│      │   ╱  ╲    Second derivative: large (steep, take small    │
│      │  ╱    ╲   steps)                                          │
│      │ ╱      ╲                                                  │
│      │╱        ╲____╱╲  Second derivative: small (flat,          │
│      │              ↑   can take bigger steps)                   │
│      └──────────────────                                         │
│                                                                  │
│ Result: Faster convergence, better optimization!                 │
└─────────────────────────────────────────────────────────────────┘
Key Innovation 3: Optimal Split Finding
text

XGBOOST SPLIT GAIN FORMULA:

                    (Gₗ)²      (Gᵣ)²      (Gₗ + Gᵣ)²
Gain = ½ [ ────────── + ────────── - ────────────── ] - γ
           Hₗ + λ      Hᵣ + λ       H + λ

Where:
- Gₗ, Gᵣ = Sum of gradients in left/right child
- Hₗ, Hᵣ = Sum of hessians in left/right child  
- λ = L2 regularization parameter
- γ = Minimum gain required to split

INTUITION:
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│        BEFORE SPLIT              AFTER SPLIT                     │
│      ┌───────────────┐        ┌───────┐ ┌───────┐               │
│      │  All samples  │   →    │ Left  │ │ Right │               │
│      │  (Score: S)   │        │(Sₗ)   │ │(Sᵣ)   │               │
│      └───────────────┘        └───────┘ └───────┘               │
│                                                                  │
│ GAIN = (Sₗ + Sᵣ) - S - γ                                        │
│                                                                  │
│ If GAIN > 0: Split is worth it!                                  │
│ If GAIN ≤ 0: Don't split (creates unnecessary complexity)        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
Key Innovation 4: Sparsity Awareness
text

HANDLING MISSING VALUES:

Real-world data is MESSY:
┌──────┬──────┬──────┬────────┐
│ Age  │Income│Score │ Target │
├──────┼──────┼──────┼────────┤
│  25  │  50K │  NaN │   1    │
│ NaN  │  80K │  720 │   0    │
│  35  │ NaN  │  680 │   1    │
│  45  │  60K │  NaN │   1    │
└──────┴──────┴──────┴────────┘

XGBoost's Smart Solution:
┌─────────────────────────────────────────────────────────────────┐
│ For each feature with missing values:                            │
│                                                                  │
│ 1. Try sending ALL missing values LEFT                           │
│    Calculate gain → Gain_left                                    │
│                                                                  │
│ 2. Try sending ALL missing values RIGHT                          │
│    Calculate gain → Gain_right                                   │
│                                                                  │
│ 3. Choose direction with HIGHER gain                             │
│                                                                  │
│ This "default direction" is LEARNED from data!                   │
│ No need to impute missing values beforehand!                     │
└─────────────────────────────────────────────────────────────────┘
Key Innovation 5: System Optimization
text

SPEED OPTIMIZATIONS IN XGBOOST:

1. COLUMN BLOCK STRUCTURE
   ┌─────────────────────────────────────────────────────────────┐
   │ Data is stored sorted by each feature                        │
   │                                                              │
   │ Feature 1: [sorted values] → [1, 3, 5, 7, 9]                 │
   │ Feature 2: [sorted values] → [2, 4, 6, 8, 10]                │
   │                                                              │
   │ Why? Finding best split becomes O(data) instead of O(data²)  │
   └─────────────────────────────────────────────────────────────┘

2. CACHE-AWARE ACCESS
   ┌─────────────────────────────────────────────────────────────┐
   │ Data access patterns optimized for CPU cache                 │
   │ Result: ~2x speedup from better memory access                │
   └─────────────────────────────────────────────────────────────┘

3. OUT-OF-CORE COMPUTATION
   ┌─────────────────────────────────────────────────────────────┐
   │ When data > RAM:                                             │
   │ - Automatically splits data to disk                          │
   │ - Processes in chunks                                        │
   │ - Enables handling datasets larger than memory               │
   └─────────────────────────────────────────────────────────────┘

4. PARALLEL TREE BUILDING
   ┌─────────────────────────────────────────────────────────────┐
   │ Split finding parallelized across:                           │
   │ - Multiple CPU cores                                         │
   │ - Different features                                         │
   │                                                              │
   │ NOT parallel across trees (they're sequential)               │
   │ But split finding WITHIN each tree is parallel!              │
   └─────────────────────────────────────────────────────────────┘
4.3 XGBoost Architecture Deep Dive
text

XGBOOST MODEL STRUCTURE:

Input Data
    │
    ↓
┌─────────────────────────────────────────────────────────────────┐
│                        ENSEMBLE                                  │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐         ┌─────────┐   │
│  │ Tree 1  │ + │ Tree 2  │ + │ Tree 3  │ + ... + │ Tree N  │   │
│  │         │   │(predicts│   │(predicts│         │(predicts│   │
│  │         │   │residuals│   │residuals│         │residuals│   │
│  │         │   │of Tree1)│   │of 1+2)  │         │of 1..N-1)   │
│  └─────────┘   └─────────┘   └─────────┘         └─────────┘   │
│       │             │             │                   │         │
│       ↓             ↓             ↓                   ↓         │
│      ŷ₁     +      ŷ₂     +      ŷ₃     + ... +     ŷₙ        │
│       │             │             │                   │         │
│       └─────────────┴─────────────┴───────────────────┘         │
│                             │                                    │
│                             ↓                                    │
│                    Final Prediction                              │
│                    ŷ = Σ(η × ŷₘ)                                 │
└─────────────────────────────────────────────────────────────────┘
4.4 XGBoost Parameters Encyclopedia
Tree Structure Parameters
text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER         │ DEFAULT │ RANGE      │ DESCRIPTION                     │
├───────────────────┼─────────┼────────────┼─────────────────────────────────┤
│ max_depth         │ 6       │ 1-∞        │ Maximum tree depth              │
│                   │         │            │ Higher = more complex           │
│                   │         │            │ Typical: 3-10                   │
├───────────────────┼─────────┼────────────┼─────────────────────────────────┤
│ min_child_weight  │ 1       │ 0-∞        │ Minimum sum of hessian in child │
│                   │         │            │ Higher = more conservative      │
│                   │         │            │ Prevents learning noise         │
├───────────────────┼─────────┼────────────┼─────────────────────────────────┤
│ max_leaves        │ 0       │ 0-∞        │ Maximum leaves (0 = unlimited)  │
│                   │         │            │ Alternative to max_depth        │
├───────────────────┼─────────┼────────────┼─────────────────────────────────┤
│ max_bin           │ 256     │ 2-∞        │ Bins for histogram method       │
│                   │         │            │ Higher = more precise, slower   │
└────────────────────────────────────────────────────────────────────────────┘

VISUAL: max_depth Effect

max_depth=2:                max_depth=5:
    ┌─┐                         ┌─┐
   ╱   ╲                       ╱   ╲
 ┌─┐   ┌─┐                   ┌─┐   ┌─┐
 │ │   │ │                  ╱   ╲ ╱   ╲
                          ┌─┐ ┌─┐ ┌─┐ ┌─┐
Simple, fast,            ╱ ╲ │ │ │ │ ╱ ╲
maybe underfit         ...deeper...
                       Complex, may overfit
Regularization Parameters
text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER │ DEFAULT │ RANGE      │ DESCRIPTION                             │
├───────────┼─────────┼────────────┼─────────────────────────────────────────┤
│ lambda    │ 1       │ 0-∞        │ L2 regularization on leaf weights       │
│ (reg_λ)   │         │            │ Higher = more conservative              │
│           │         │            │ Prevents extreme predictions            │
├───────────┼─────────┼────────────┼─────────────────────────────────────────┤
│ alpha     │ 0       │ 0-∞        │ L1 regularization on leaf weights       │
│ (reg_α)   │         │            │ Encourages sparsity (some weights → 0)  │
├───────────┼─────────┼────────────┼─────────────────────────────────────────┤
│ gamma     │ 0       │ 0-∞        │ Minimum loss reduction for split        │
│           │         │            │ Higher = fewer splits                   │
│           │         │            │ Acts as pruning                         │
└────────────────────────────────────────────────────────────────────────────┘

VISUAL: Regularization Effects

λ=0 (No L2):              λ=10 (Strong L2):
Predictions: [50, -80, 120, -90]    Predictions: [15, -20, 25, -18]
Very extreme values!                 More moderate values

γ=0 (No pruning):         γ=5 (Strong pruning):
Many splits (complex)     Fewer splits (simpler)
├─┬─┬─┬─┬─┬─┬─┤           ├───┬───┤
Deep trees                 Shallow trees
Sampling Parameters
text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER        │ DEFAULT │ RANGE   │ DESCRIPTION                         │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ subsample        │ 1.0     │ (0,1]   │ Fraction of rows for each tree     │
│                  │         │         │ 0.8 = use 80% of data              │
│                  │         │         │ Reduces overfitting                │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ colsample_bytree │ 1.0     │ (0,1]   │ Fraction of features per tree      │
│                  │         │         │ Similar to Random Forest concept   │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ colsample_bylevel│ 1.0     │ (0,1]   │ Fraction of features per level     │
│                  │         │         │ More fine-grained control          │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ colsample_bynode │ 1.0     │ (0,1]   │ Fraction of features per split     │
│                  │         │         │ Most fine-grained control          │
└────────────────────────────────────────────────────────────────────────────┘

VISUAL: Sampling Process

Original Data:                Subsample=0.6, colsample_bytree=0.75
┌──────────────────┐          
│ F1  F2  F3  F4   │          Actually Used:
├──────────────────┤          ┌───────────────┐
│ r1  r1  r1  r1   │    →     │ F1  F2  F4    │ ← 75% features
│ r2  r2  r2  r2   │          ├───────────────┤
│ r3  r3  r3  r3   │          │ r1  r1  r1    │
│ r4  r4  r4  r4   │          │ r3  r3  r3    │ ← 60% rows
│ r5  r5  r5  r5   │          │ r5  r5  r5    │
└──────────────────┘          └───────────────┘
Learning Parameters
text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER        │ DEFAULT │ RANGE   │ DESCRIPTION                         │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ learning_rate    │ 0.3     │ (0,1]   │ Shrinkage of each tree's contrib.  │
│ (eta)            │         │         │ Lower = more trees needed           │
│                  │         │         │ Lower = better generalization       │
│                  │         │         │ Typical: 0.01-0.3                   │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ n_estimators     │ 100     │ 1-∞     │ Number of trees                     │
│ (num_boost_round)│         │         │ More trees if learning_rate small   │
├──────────────────┼─────────┼─────────┼─────────────────────────────────────┤
│ objective        │'reg:sq' │ string  │ Loss function to optimize           │
│                  │         │         │ 'reg:squarederror' (regression)     │
│                  │         │         │ 'binary:logistic' (binary class.)   │
│                  │         │         │ 'multi:softmax' (multiclass)        │
└────────────────────────────────────────────────────────────────────────────┘

VISUAL: Learning Rate Effect

learning_rate=0.3:
Tree1: ████████░░ (30% contribution)
Tree2: ████████░░
Tree3: ████████░░
Total trees needed: ~100

learning_rate=0.01:
Tree1: █░░░░░░░░░ (1% contribution)
Tree2: █░░░░░░░░░
Tree3: █░░░░░░░░░
Total trees needed: ~3000

Lower learning rate = More trees, but usually better final result!
4.5 XGBoost Code Implementation
Basic Usage
Python

# =============================================================================
# XGBOOST: COMPLETE IMPLEMENTATION GUIDE
# =============================================================================

import xgboost as xgb
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import accuracy_score, mean_squared_error
import matplotlib.pyplot as plt

# -----------------------------------------------------------------------------
# STEP 1: PREPARE DATA
# -----------------------------------------------------------------------------

# Create sample data
np.random.seed(42)
X = np.random.randn(1000, 10)
y_reg = 3*X[:,0] + 2*X[:,1] + np.random.randn(1000)*0.1  # Regression target
y_clf = (X[:,0] + X[:,1] > 0).astype(int)                 # Classification target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y_reg, test_size=0.2, random_state=42
)

# -----------------------------------------------------------------------------
# STEP 2: BASIC REGRESSION MODEL
# -----------------------------------------------------------------------------

# Method 1: Scikit-learn API (Recommended for beginners)
model_sklearn = xgb.XGBRegressor(
    n_estimators=100,
    max_depth=6,
    learning_rate=0.1,
    random_state=42
)

model_sklearn.fit(X_train, y_train)
predictions = model_sklearn.predict(X_test)
rmse = np.sqrt(mean_squared_error(y_test, predictions))
print(f"RMSE: {rmse:.4f}")

# Method 2: Native XGBoost API (More control)
dtrain = xgb.DMatrix(X_train, label=y_train)
dtest = xgb.DMatrix(X_test, label=y_test)

params = {
    'objective': 'reg:squarederror',
    'max_depth': 6,
    'eta': 0.1,
    'eval_metric': 'rmse'
}

model_native = xgb.train(
    params,
    dtrain,
    num_boost_round=100,
    evals=[(dtrain, 'train'), (dtest, 'test')],
    early_stopping_rounds=10,
    verbose_eval=10
)

# -----------------------------------------------------------------------------
# STEP 3: CLASSIFICATION MODEL
# -----------------------------------------------------------------------------

X_train_c, X_test_c, y_train_c, y_test_c = train_test_split(
    X, y_clf, test_size=0.2, random_state=42
)

model_clf = xgb.XGBClassifier(
    n_estimators=100,
    max_depth=4,
    learning_rate=0.1,
    objective='binary:logistic',
    random_state=42
)

model_clf.fit(
    X_train_c, y_train_c,
    eval_set=[(X_test_c, y_test_c)],
    early_stopping_rounds=10,
    verbose=True
)

y_pred = model_clf.predict(X_test_c)
accuracy = accuracy_score(y_test_c, y_pred)
print(f"Accuracy: {accuracy:.4f}")

# -----------------------------------------------------------------------------
# STEP 4: FEATURE IMPORTANCE
# -----------------------------------------------------------------------------

# Get feature importance
importance = model_sklearn.feature_importances_

# Plot
plt.figure(figsize=(10, 6))
plt.barh(range(len(importance)), importance)
plt.yticks(range(len(importance)), [f'Feature {i}' for i in range(len(importance))])
plt.xlabel('Importance')
plt.title('XGBoost Feature Importance')
plt.tight_layout()
plt.show()

# Different importance types
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for idx, importance_type in enumerate(['weight', 'gain', 'cover']):
    xgb.plot_importance(
        model_sklearn, 
        importance_type=importance_type,
        ax=axes[idx],
        title=f'Importance: {importance_type}'
    )
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# STEP 5: CROSS-VALIDATION
# -----------------------------------------------------------------------------

# Using XGBoost's built-in CV
dtrain_full = xgb.DMatrix(X, label=y_reg)

cv_results = xgb.cv(
    params,
    dtrain_full,
    num_boost_round=500,
    nfold=5,
    early_stopping_rounds=10,
    metrics='rmse',
    as_pandas=True,
    seed=42
)

print(f"Best RMSE: {cv_results['test-rmse-mean'].min():.4f}")
print(f"Best iteration: {cv_results['test-rmse-mean'].idxmin()}")

# -----------------------------------------------------------------------------
# STEP 6: SAVING AND LOADING MODELS
# -----------------------------------------------------------------------------

# Save model
model_sklearn.save_model('xgboost_model.json')  # JSON format
# model_sklearn.save_model('xgboost_model.ubj')  # Binary format

# Load model
loaded_model = xgb.XGBRegressor()
loaded_model.load_model('xgboost_model.json')

# Verify it works
new_predictions = loaded_model.predict(X_test)
print(f"Predictions match: {np.allclose(predictions, new_predictions)}")
Advanced XGBoost Techniques
Python

# =============================================================================
# ADVANCED XGBOOST TECHNIQUES
# =============================================================================

# -----------------------------------------------------------------------------
# TECHNIQUE 1: HANDLING IMBALANCED DATA
# -----------------------------------------------------------------------------

# For binary classification with imbalanced classes
# Calculate scale_pos_weight
scale_pos_weight = len(y_train_c[y_train_c==0]) / len(y_train_c[y_train_c==1])

model_imbalanced = xgb.XGBClassifier(
    scale_pos_weight=scale_pos_weight,  # Balances classes
    n_estimators=100,
    max_depth=4,
    learning_rate=0.1
)

# -----------------------------------------------------------------------------
# TECHNIQUE 2: CUSTOM OBJECTIVE FUNCTION
# -----------------------------------------------------------------------------

def custom_mse(y_pred, dtrain):
    """Custom Mean Squared Error with gradient and hessian"""
    y_true = dtrain.get_label()
    
    # Gradient (first derivative of loss)
    grad = y_pred - y_true
    
    # Hessian (second derivative of loss)
    hess = np.ones_like(y_true)
    
    return grad, hess

def custom_rmse_eval(y_pred, dtrain):
    """Custom evaluation metric"""
    y_true = dtrain.get_label()
    rmse = np.sqrt(np.mean((y_pred - y_true)**2))
    return 'custom_rmse', rmse

# Use custom objective
model_custom = xgb.train(
    {'max_depth': 4},
    dtrain,
    num_boost_round=100,
    obj=custom_mse,
    custom_metric=custom_rmse_eval
)

# -----------------------------------------------------------------------------
# TECHNIQUE 3: MONOTONIC CONSTRAINTS
# -----------------------------------------------------------------------------

# Force certain features to have monotonic relationship with target
# +1 = increasing, -1 = decreasing, 0 = no constraint

model_monotonic = xgb.XGBRegressor(
    monotone_constraints=(1, -1, 0, 0, 0, 0, 0, 0, 0, 0),
    # Feature 0: must increase with target
    # Feature 1: must decrease with target
    # Others: no constraint
    n_estimators=100,
    max_depth=4
)

# -----------------------------------------------------------------------------
# TECHNIQUE 4: INTERACTION CONSTRAINTS
# -----------------------------------------------------------------------------

# Limit which features can interact with each other
# Useful when domain knowledge suggests certain features shouldn't interact

model_interaction = xgb.XGBRegressor(
    interaction_constraints=[[0, 1, 2], [3, 4, 5], [6, 7, 8, 9]],
    # Features 0,1,2 can only interact with each other
    # Features 3,4,5 can only interact with each other
    # Features 6,7,8,9 can only interact with each other
    n_estimators=100,
    max_depth=4
)

# -----------------------------------------------------------------------------
# TECHNIQUE 5: GPU ACCELERATION
# -----------------------------------------------------------------------------

# Use GPU for faster training (requires CUDA)
model_gpu = xgb.XGBRegressor(
    tree_method='gpu_hist',  # Use GPU
    gpu_id=0,                # GPU device ID
    n_estimators=1000,
    max_depth=8
)

# Note: Install xgboost with GPU support:
# pip install xgboost --upgrade
# or build from source with CUDA

# -----------------------------------------------------------------------------
# TECHNIQUE 6: EARLY STOPPING BEST PRACTICES
# -----------------------------------------------------------------------------

model_early = xgb.XGBRegressor(
    n_estimators=10000,  # Set high
    max_depth=6,
    learning_rate=0.01,  # Low learning rate
    early_stopping_rounds=50  # Stop if no improvement in 50 rounds
)

model_early.fit(
    X_train, y_train,
    eval_set=[(X_train, y_train), (X_test, y_test)],
    verbose=100
)

print(f"Best iteration: {model_early.best_iteration}")
print(f"Best score: {model_early.best_score}")
Chapter 5: LightGBM Mastery
5.1 What is LightGBM?
text

LightGBM = Light Gradient Boosting Machine

Created by Microsoft Research (2017)

WHY "LIGHT"?
┌─────────────────────────────────────────────────────────────────┐
│ 1. Lighter on MEMORY (uses histogram-based algorithm)          │
│ 2. Lighter on COMPUTATION (up to 20x faster than XGBoost)      │
│ 3. Lighter on CODE (simple API)                                 │
│ 4. But NOT lighter on POWER (often more accurate!)             │
└─────────────────────────────────────────────────────────────────┘

SPEED COMPARISON (Training 10M samples):
┌─────────────────────────────────────────────────────────────────┐
│ XGBoost:  ████████████████████ 120 minutes                      │
│ LightGBM: ████ 20 minutes (6x faster!)                          │
└─────────────────────────────────────────────────────────────────┘
5.2 LightGBM's Key Innovations
Innovation 1: Histogram-Based Splitting
text

TRADITIONAL (Exact) vs HISTOGRAM Splitting

TRADITIONAL APPROACH (XGBoost default):
Feature values: [1.2, 3.5, 2.1, 7.8, 4.2, 6.1, 2.5, 8.9, 3.3, 5.6]

For split finding:
- Sort all values: [1.2, 2.1, 2.5, 3.3, 3.5, 4.2, 5.6, 6.1, 7.8, 8.9]
- Try EVERY possible split point
- Calculate gain for each
- Complexity: O(n × features × depth)

HISTOGRAM APPROACH (LightGBM):
Feature values: [1.2, 3.5, 2.1, 7.8, 4.2, 6.1, 2.5, 8.9, 3.3, 5.6]

Step 1: Bin values into buckets (e.g., 256 bins)
┌────────────────────────────────────────────────────────────────┐
│ Bin 0   │ Bin 1   │ Bin 2   │ Bin 3   │ Bin 4   │ ... │Bin 255│
│ [0-2)   │ [2-4)   │ [4-6)   │ [6-8)   │ [8-10)  │     │       │
│ count:1 │ count:4 │ count:2 │ count:2 │ count:1 │     │       │
│ (1.2)   │(2.1,2.5,│(4.2,5.6)│(6.1,7.8)│ (8.9)   │     │       │
│         │3.3,3.5) │         │         │         │     │       │
└────────────────────────────────────────────────────────────────┘

Step 2: Try split at bin BOUNDARIES only
- Only 256 possibilities (not millions!)
- Complexity: O(bins × features × depth) where bins << n

MEMORY SAVINGS:
┌────────────────────────────────────────────────────────────────┐
│ Original: 10 million float64 values = 80 MB per feature        │
│ Histogram: 256 bins with counts = ~1 KB per feature            │
│ Savings: ~80,000x less memory!                                  │
└────────────────────────────────────────────────────────────────┘
Innovation 2: Leaf-Wise Growth (Best-First)
text

LEVEL-WISE vs LEAF-WISE Growth

LEVEL-WISE (XGBoost default):
Grows all leaves at same depth before going deeper

Level 0:      [Root]
               ↓
Level 1:   [L1]  [R1]     ← Both split before going deeper
               ↓
Level 2: [L2][R2][L3][R3] ← All 4 split before level 3

LEAF-WISE (LightGBM default):
Always splits the leaf with highest gain

Step 1:       [Root]        Gain=100
               ↓
Step 2:    [L1]  [R1]       L1 gain=80, R1 gain=20
            ↓
Step 3: [L2][R2]  [R1]      L2 gain=60, R2 gain=40, R1 gain=20
         ↓
Step 4:[L3][R3][R2][R1]     Split L2 (highest gain=60)

VISUAL COMPARISON:
┌─────────────────────────────────────────────────────────────────┐
│ LEVEL-WISE:                    LEAF-WISE:                       │
│                                                                  │
│       O                              O                           │
│      / \                            / \                          │
│     O   O                          O   O                         │
│    /\   /\                        /\                             │
│   O O  O O                       O O                             │
│                                 /\                               │
│ Balanced tree                  O O                               │
│ (same depth everywhere)        Very deep on one side             │
│                                (unbalanced, but efficient)       │
└─────────────────────────────────────────────────────────────────┘

WHY LEAF-WISE IS FASTER:
- Achieves same accuracy with FEWER leaves
- More targeted: focuses compute on where it helps most
- Risk: Can overfit with small data (use max_depth to control)
Innovation 3: Gradient-based One-Side Sampling (GOSS)
text

THE IDEA:
Not all data points are equally important!

┌─────────────────────────────────────────────────────────────────┐
│ Large gradient = Model is getting this point VERY WRONG         │
│                = This point is VERY IMPORTANT for learning      │
│                                                                  │
│ Small gradient = Model is getting this point mostly right       │
│                = Less important for learning                     │
└─────────────────────────────────────────────────────────────────┘

GOSS ALGORITHM:
Step 1: Sort samples by absolute gradient (|g|)
Step 2: Keep TOP a% samples (large gradients) → Definitely important!
Step 3: RANDOMLY sample b% from remaining → Still need some for accuracy
Step 4: Multiply small gradient samples by (1-a)/b to compensate

VISUAL:
┌─────────────────────────────────────────────────────────────────┐
│ All Data Points (sorted by gradient):                           │
│ ●●●●●●●●●●│○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○            │
│ └──Top a%──┘ └────────────Remaining (1-a)%────────────┘          │
│  (Keep ALL)     (Randomly sample b% of these)                    │
│                                                                  │
│ Example with a=20%, b=10%:                                       │
│ Original: 1,000,000 samples                                      │
│ Keep: 200,000 (top gradients) + 80,000 (random from rest)        │
│ Training on: 280,000 samples (72% reduction!)                    │
│                                                                  │
│ But we multiply the 80,000 by (1-0.2)/0.1 = 8                    │
│ So their contribution is properly weighted!                      │
└─────────────────────────────────────────────────────────────────┘
Innovation 4: Exclusive Feature Bundling (EFB)
text

THE OBSERVATION:
In high-dimensional sparse data, many features are mutually exclusive
(They rarely have non-zero values at the same time)

EXAMPLE:
┌──────┬──────┬──────┬──────┬──────┐
│ F1   │ F2   │ F3   │ F4   │ F5   │
├──────┼──────┼──────┼──────┼──────┤
│ 1.5  │ 0    │ 0    │ 2.3  │ 0    │  ← F1 and F4 non-zero
│ 0    │ 3.2  │ 0    │ 0    │ 1.1  │  ← F2 and F5 non-zero
│ 0    │ 0    │ 4.1  │ 0    │ 0    │  ← Only F3 non-zero
│ 2.0  │ 0    │ 0    │ 0    │ 3.4  │
│ 0    │ 1.5  │ 2.2  │ 0    │ 0    │
└──────┴──────┴──────┴──────┴──────┘

F1 and F2 are MUTUALLY EXCLUSIVE (never both non-zero in same row)
F4 and F5 are MUTUALLY EXCLUSIVE

EFB BUNDLES THEM:
┌──────────────┬──────────────┬──────┐
│ Bundle 1     │ Bundle 2     │ F3   │
│ (F1 + F2)    │ (F4 + F5)    │      │
├──────────────┼──────────────┼──────┤
│ 1.5 (from F1)│ 2.3 (from F4)│ 0    │
│ 103.2 (F2+100)│ 101.1(F5+100)│ 0   │ ← Offset to distinguish
│ 0            │ 0            │ 4.1  │
│ 2.0 (from F1)│ 103.4(F5+100)│ 0    │
│ 101.5(F2+100)│ 2.2 (from F4)│ 2.2  │
└──────────────┴──────────────┴──────┘

Result: 5 features → 3 bundles
Fewer histograms needed = FASTER!
5.3 LightGBM Parameters Encyclopedia
Core Parameters
text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER          │ DEFAULT  │ DESCRIPTION                                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ boosting_type      │ 'gbdt'   │ Algorithm type:                            │
│                    │          │ • 'gbdt' - traditional gradient boosting   │
│                    │          │ • 'dart' - dropouts during training        │
│                    │          │ • 'goss' - one-side sampling               │
│                    │          │ • 'rf' - random forest mode                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ num_leaves         │ 31       │ Max leaves in one tree                     │
│                    │          │ MAIN parameter for complexity              │
│                    │          │ Rule: num_leaves < 2^max_depth             │
│                    │          │ Typical: 20-150                            │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ max_depth          │ -1       │ Limit tree depth (-1=no limit)             │
│                    │          │ Use to prevent overfitting                 │
│                    │          │ Leaf-wise can create deep trees!           │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ learning_rate      │ 0.1      │ Shrinkage rate (same as XGBoost eta)      │
│                    │          │ Typical: 0.01-0.3                          │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ n_estimators       │ 100      │ Number of boosting iterations              │
│                    │          │ More with lower learning_rate              │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ max_bin            │ 255      │ Max bins for histogram                     │
│                    │          │ Higher = more accurate, slower             │
│                    │          │ Lower = faster, may lose accuracy          │
└────────────────────────────────────────────────────────────────────────────┘

VISUAL: num_leaves vs max_depth

num_leaves=7, max_depth=-1:    num_leaves=31, max_depth=5:
      O                              O
     /|\                            /|\
    O O O                          O O O
   /| |\                          /|\ /|\
  O O O O  (7 leaves)            O O O O O O...
                                 (Can have 31 leaves across 5 levels)
Regularization Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER          │ DEFAULT  │ DESCRIPTION                                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ min_data_in_leaf   │ 20       │ Minimum samples in one leaf                │
│                    │          │ CRITICAL for preventing overfitting        │
│                    │          │ Small data: increase this (100-1000)       │
│                    │          │ Large data: can decrease (10-20)           │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ min_sum_hessian_   │ 1e-3     │ Minimum sum of hessian in leaf             │
│ in_leaf            │          │ Similar to XGBoost min_child_weight        │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ lambda_l1          │ 0        │ L1 regularization                          │
│                    │          │ Encourages sparsity                        │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ lambda_l2          │ 0        │ L2 regularization                          │
│                    │          │ Smoother weights                           │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ min_gain_to_split  │ 0        │ Minimum gain to make a split               │
│                    │          │ Similar to XGBoost gamma                   │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ path_smooth        │ 0        │ Smoothing for leaf path (0-∞)              │
│                    │          │ Helps reduce overfitting                   │
│                    │          │ Only for leaf-wise trees                   │
└────────────────────────────────────────────────────────────────────────────┘

OVERFITTING CONTROL STRATEGY:
┌─────────────────────────────────────────────────────────────────┐
│ If overfitting (train score >> validation score):              │
│                                                                  │
│ 1. Increase min_data_in_leaf (20 → 100 → 500)                   │
│ 2. Decrease num_leaves (31 → 20 → 10)                           │
│ 3. Set max_depth (try 5-10)                                     │
│ 4. Increase lambda_l1/lambda_l2 (0 → 1 → 10)                    │
│ 5. Decrease learning_rate + increase n_estimators                │
│ 6. Use more data augmentation/features                           │
└─────────────────────────────────────────────────────────────────┘
Speed and Memory Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER          │ DEFAULT  │ DESCRIPTION                                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ num_threads        │ 0        │ Number of threads (0 = all cores)          │
│                    │          │ Can limit for parallel training            │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ device_type        │ 'cpu'    │ 'cpu' or 'gpu'                             │
│                    │          │ GPU can be 5-10x faster                    │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ histogram_pool_    │ -1.0     │ Memory in MB for histograms                │
│ size               │          │ -1 = auto, can limit for large data        │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ max_bin            │ 255      │ Reduce for faster speed                    │
│                    │          │ 255 → 128 → 64 (faster but less precise)   │
└────────────────────────────────────────────────────────────────────────────┘
GOSS-Specific Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER          │ DEFAULT  │ DESCRIPTION                                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ top_rate           │ 0.2      │ Fraction of large gradients to keep        │
│                    │          │ Only when boosting_type='goss'             │
│                    │          │ Higher = more accurate, slower             │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ other_rate         │ 0.1      │ Fraction of small gradients to sample      │
│                    │          │ Only when boosting_type='goss'             │
└────────────────────────────────────────────────────────────────────────────┘

GOSS CONFIGURATION GUIDE:
┌─────────────────────────────────────────────────────────────────┐
│ Large dataset (>1M rows): Use GOSS for speed                    │
│   boosting_type='goss'                                           │
│   top_rate=0.2, other_rate=0.1                                   │
│                                                                  │
│ Medium dataset: Default GBDT usually best                        │
│   boosting_type='gbdt'                                           │
│                                                                  │
│ Small dataset (<10K rows): Be careful with GOSS                 │
│   May lose important samples                                     │
└─────────────────────────────────────────────────────────────────┘
5.4 LightGBM Code Implementation
Basic Usage

Python

# =============================================================================
# LIGHTGBM: COMPLETE IMPLEMENTATION GUIDE
# =============================================================================

import lightgbm as lgb
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, mean_squared_error, roc_auc_score
import matplotlib.pyplot as plt

# -----------------------------------------------------------------------------
# STEP 1: PREPARE DATA
# -----------------------------------------------------------------------------

# Create sample data
np.random.seed(42)
X = np.random.randn(10000, 20)
y_reg = 3*X[:,0] + 2*X[:,1] - X[:,2] + np.random.randn(10000)*0.5
y_clf = (X[:,0] + X[:,1] - X[:,2] > 0).astype(int)

# Split
X_train, X_test, y_train, y_test = train_test_split(
    X, y_reg, test_size=0.2, random_state=42
)

# -----------------------------------------------------------------------------
# STEP 2: BASIC REGRESSION MODEL
# -----------------------------------------------------------------------------

# Method 1: Scikit-learn API
from lightgbm import LGBMRegressor

model_sklearn = LGBMRegressor(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    random_state=42
)

model_sklearn.fit(
    X_train, y_train,
    eval_set=[(X_test, y_test)],
    eval_metric='rmse',
    callbacks=[lgb.early_stopping(stopping_rounds=10)]
)

predictions = model_sklearn.predict(X_test)
rmse = np.sqrt(mean_squared_error(y_test, predictions))
print(f"RMSE: {rmse:.4f}")

# Method 2: Native LightGBM API (More powerful)
train_data = lgb.Dataset(X_train, label=y_train)
test_data = lgb.Dataset(X_test, label=y_test, reference=train_data)

params = {
    'objective': 'regression',
    'metric': 'rmse',
    'num_leaves': 31,
    'learning_rate': 0.1,
    'feature_fraction': 0.9,
    'bagging_fraction': 0.8,
    'bagging_freq': 5,
    'verbose': -1
}

model_native = lgb.train(
    params,
    train_data,
    num_boost_round=1000,
    valid_sets=[train_data, test_data],
    valid_names=['train', 'valid'],
    callbacks=[
        lgb.early_stopping(stopping_rounds=50),
        lgb.log_evaluation(period=100)
    ]
)

print(f"Best iteration: {model_native.best_iteration}")
print(f"Best score: {model_native.best_score}")

# -----------------------------------------------------------------------------
# STEP 3: CLASSIFICATION MODEL
# -----------------------------------------------------------------------------

X_train_c, X_test_c, y_train_c, y_test_c = train_test_split(
    X, y_clf, test_size=0.2, random_state=42
)

from lightgbm import LGBMClassifier

model_clf = LGBMClassifier(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    random_state=42
)

model_clf.fit(
    X_train_c, y_train_c,
    eval_set=[(X_test_c, y_test_c)],
    eval_metric='auc',
    callbacks=[lgb.early_stopping(stopping_rounds=20)]
)

# Predictions
y_pred = model_clf.predict(X_test_c)
y_pred_proba = model_clf.predict_proba(X_test_c)[:, 1]

accuracy = accuracy_score(y_test_c, y_pred)
auc = roc_auc_score(y_test_c, y_pred_proba)

print(f"Accuracy: {accuracy:.4f}")
print(f"AUC: {auc:.4f}")

# -----------------------------------------------------------------------------
# STEP 4: FEATURE IMPORTANCE
# -----------------------------------------------------------------------------

# Get feature importance (multiple types)
importance_gain = model_sklearn.feature_importances_  # Default: 'split'
importance_split = model_sklearn.booster_.feature_importance(importance_type='split')

# Create feature names
feature_names = [f'Feature_{i}' for i in range(X.shape[1])]

# Plot
fig, axes = plt.subplots(1, 2, figsize=(15, 6))

# Gain importance
lgb.plot_importance(
    model_sklearn,
    importance_type='gain',
    ax=axes[0],
    title='Feature Importance (Gain)',
    max_num_features=10
)

# Split importance
lgb.plot_importance(
    model_sklearn,
    importance_type='split',
    ax=axes[1],
    title='Feature Importance (Split)',
    max_num_features=10
)

plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# STEP 5: CROSS-VALIDATION
# -----------------------------------------------------------------------------

# Create full dataset
full_train = lgb.Dataset(X, label=y_reg)

# CV with native API
cv_results = lgb.cv(
    params,
    full_train,
    num_boost_round=1000,
    nfold=5,
    callbacks=[
        lgb.early_stopping(stopping_rounds=50),
        lgb.log_evaluation(period=100)
    ],
    return_cvbooster=True  # Returns trained models
)

print(f"Best RMSE: {cv_results['valid rmse-mean'][-1]:.4f}")
print(f"Number of iterations: {len(cv_results['valid rmse-mean'])}")

# -----------------------------------------------------------------------------
# STEP 6: HANDLING CATEGORICAL FEATURES
# -----------------------------------------------------------------------------

# LightGBM can handle categorical features natively!
# Create data with categorical features
data = pd.DataFrame({
    'num_feature_1': np.random.randn(1000),
    'num_feature_2': np.random.randn(1000),
    'cat_feature_1': np.random.choice(['A', 'B', 'C', 'D'], 1000),
    'cat_feature_2': np.random.choice(['X', 'Y', 'Z'], 1000),
    'target': np.random.rand(1000)
})

# Specify categorical features
categorical_features = ['cat_feature_1', 'cat_feature_2']

# Convert to category type
for col in categorical_features:
    data[col] = data[col].astype('category')

X_cat = data.drop('target', axis=1)
y_cat = data['target']

# Split
X_train_cat, X_test_cat, y_train_cat, y_test_cat = train_test_split(
    X_cat, y_cat, test_size=0.2, random_state=42
)

# Train with categorical features
model_cat = LGBMRegressor(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1
)

model_cat.fit(
    X_train_cat, y_train_cat,
    categorical_feature=categorical_features,
    eval_set=[(X_test_cat, y_test_cat)],
    callbacks=[lgb.early_stopping(stopping_rounds=10)]
)

# LightGBM automatically handles the categorical encoding!
# No need for one-hot encoding or label encoding!

# -----------------------------------------------------------------------------
# STEP 7: SAVING AND LOADING MODELS
# -----------------------------------------------------------------------------

# Save model (text format)
model_sklearn.booster_.save_model('lgb_model.txt')

# Save model (binary format - faster)
import pickle
with open('lgb_model.pkl', 'wb') as f:
    pickle.dump(model_sklearn, f)

# Load text model
loaded_model = lgb.Booster(model_file='lgb_model.txt')
loaded_predictions = loaded_model.predict(X_test)

# Load pickle model
with open('lgb_model.pkl', 'rb') as f:
    loaded_sklearn_model = pickle.load(f)
loaded_sklearn_predictions = loaded_sklearn_model.predict(X_test)

# Verify
print(f"Predictions match (txt): {np.allclose(predictions, loaded_predictions)}")
print(f"Predictions match (pkl): {np.allclose(predictions, loaded_sklearn_predictions)}")
Advanced LightGBM Techniques

Python

# =============================================================================
# ADVANCED LIGHTGBM TECHNIQUES
# =============================================================================

# -----------------------------------------------------------------------------
# TECHNIQUE 1: USING GOSS (Gradient-based One-Side Sampling)
# -----------------------------------------------------------------------------

# Best for large datasets
model_goss = LGBMRegressor(
    boosting_type='goss',  # Enable GOSS
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    top_rate=0.2,         # Keep top 20% gradients
    other_rate=0.1        # Sample 10% of remaining
)

model_goss.fit(X_train, y_train)

# Speed comparison
import time

start = time.time()
model_gbdt = LGBMRegressor(boosting_type='gbdt', n_estimators=100)
model_gbdt.fit(X_train, y_train)
gbdt_time = time.time() - start

start = time.time()
model_goss.fit(X_train, y_train)
goss_time = time.time() - start

print(f"GBDT time: {gbdt_time:.2f}s")
print(f"GOSS time: {goss_time:.2f}s")
print(f"Speedup: {gbdt_time/goss_time:.2f}x")

# -----------------------------------------------------------------------------
# TECHNIQUE 2: DART (Dropouts meet Multiple Additive Regression Trees)
# -----------------------------------------------------------------------------

# DART adds dropout to boosting (prevents overfitting)
model_dart = LGBMRegressor(
    boosting_type='dart',
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    drop_rate=0.1,           # Dropout rate
    skip_drop=0.5,           # Probability of skipping dropout
    max_drop=50,             # Max number of dropped trees
    uniform_drop=False,      # Use binomial distribution
    random_state=42
)

model_dart.fit(X_train, y_train)

# -----------------------------------------------------------------------------
# TECHNIQUE 3: CUSTOM OBJECTIVE AND METRIC
# -----------------------------------------------------------------------------

def custom_asymmetric_train(y_pred, train_data):
    """
    Custom loss: Penalize overestimation more than underestimation
    Useful for inventory management, cost-sensitive problems
    """
    y_true = train_data.get_label()
    residual = y_true - y_pred
    
    # Asymmetric gradients
    grad = np.where(residual > 0, -2*residual, -0.5*residual)
    hess = np.where(residual > 0, 2, 0.5)
    
    return grad, hess

def custom_asymmetric_eval(y_pred, train_data):
    """Custom evaluation metric"""
    y_true = train_data.get_label()
    residual = y_true - y_pred
    
    # Asymmetric loss
    loss = np.where(residual > 0, 2*residual**2, 0.5*residual**2)
    
    return 'custom_asymmetric', np.mean(loss), False

# Use custom objective
train_data = lgb.Dataset(X_train, label=y_train)
test_data = lgb.Dataset(X_test, label=y_test, reference=train_data)

model_custom = lgb.train(
    {'num_leaves': 31, 'learning_rate': 0.1},
    train_data,
    num_boost_round=100,
    valid_sets=[test_data],
    fobj=custom_asymmetric_train,
    feval=custom_asymmetric_eval
)

# -----------------------------------------------------------------------------
# TECHNIQUE 4: MONOTONE CONSTRAINTS
# -----------------------------------------------------------------------------

# Force monotonic relationships (useful for business logic)
# Example: Price should increase with quality

model_monotone = LGBMRegressor(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    monotone_constraints=[1, -1, 0, 0, 0, 0, 0, 0, 0, 0, 
                          0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    # Feature 0: must increase with target (+1)
    # Feature 1: must decrease with target (-1)
    # Others: no constraint (0)
)

model_monotone.fit(X_train, y_train)

# Verify monotonicity
feature_0_range = np.linspace(X_train[:, 0].min(), X_train[:, 0].max(), 100)
X_test_mono = np.repeat(X_train[0:1, :], 100, axis=0)
X_test_mono[:, 0] = feature_0_range

predictions_mono = model_monotone.predict(X_test_mono)

# Check if predictions increase with feature 0
is_monotone = all(predictions_mono[i] <= predictions_mono[i+1] 
                  for i in range(len(predictions_mono)-1))
print(f"Is monotone: {is_monotone}")

# -----------------------------------------------------------------------------
# TECHNIQUE 5: GPU ACCELERATION
# -----------------------------------------------------------------------------

# Requires LightGBM compiled with GPU support
# pip install lightgbm --install-option=--gpu

model_gpu = LGBMRegressor(
    device='gpu',
    gpu_platform_id=0,
    gpu_device_id=0,
    n_estimators=1000,
    num_leaves=127,
    learning_rate=0.01
)

# GPU can be 5-10x faster for large datasets!

# -----------------------------------------------------------------------------
# TECHNIQUE 6: IMBALANCED CLASSIFICATION
# -----------------------------------------------------------------------------

# For highly imbalanced data
# Calculate class weights
neg_count = np.sum(y_train_c == 0)
pos_count = np.sum(y_train_c == 1)
scale_pos_weight = neg_count / pos_count

model_imbalanced = LGBMClassifier(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1,
    scale_pos_weight=scale_pos_weight,  # Adjust for imbalance
    is_unbalance=True                   # Alternative approach
)

# Or use class weights
from sklearn.utils.class_weight import compute_sample_weight
sample_weights = compute_sample_weight('balanced', y_train_c)

model_weighted = LGBMClassifier(
    n_estimators=100,
    num_leaves=31,
    learning_rate=0.1
)

model_weighted.fit(X_train_c, y_train_c, sample_weight=sample_weights)

# -----------------------------------------------------------------------------
# TECHNIQUE 7: FOCAL LOSS (For extreme imbalance)
# -----------------------------------------------------------------------------

def focal_loss_lgb(y_pred, dtrain, alpha=0.25, gamma=2):
    """
    Focal Loss for imbalanced classification
    Focuses on hard examples
    """
    y_true = dtrain.get_label()
    
    # Convert to probabilities
    y_prob = 1.0 / (1.0 + np.exp(-y_pred))
    
    # Focal loss gradient
    grad = (alpha * y_true + (1 - alpha) * (1 - y_true)) * \
           (y_true - y_prob) * \
           ((1 - y_prob) * y_prob) ** gamma * \
           (gamma * (y_true - y_prob) * np.log(y_prob + 1e-7) + y_prob)
    
    # Hessian (second derivative)
    hess = (y_prob * (1 - y_prob)) ** gamma * \
           alpha * y_true + (1 - alpha) * (1 - y_true)
    
    return grad, hess

# Use focal loss
train_data_clf = lgb.Dataset(X_train_c, label=y_train_c)

model_focal = lgb.train(
    {'num_leaves': 31, 'learning_rate': 0.1},
    train_data_clf,
    num_boost_round=100,
    fobj=focal_loss_lgb
)

# -----------------------------------------------------------------------------
# TECHNIQUE 8: LEARNING RATE SCHEDULING
# -----------------------------------------------------------------------------

# Dynamic learning rate: start high, then decay
def learning_rate_scheduler(current_round):
    """Decrease learning rate as training progresses"""
    base_lr = 0.1
    lr = base_lr * (0.99 ** current_round)
    return lr

params_scheduled = {
    'objective': 'regression',
    'metric': 'rmse',
    'num_leaves': 31,
    'verbose': -1
}

model_scheduled = lgb.train(
    params_scheduled,
    train_data,
    num_boost_round=1000,
    valid_sets=[test_data],
    callbacks=[
        lgb.reset_parameter(learning_rate=learning_rate_scheduler),
        lgb.early_stopping(stopping_rounds=50)
    ]
)
Chapter 6: CatBoost Mastery
6.1 What is CatBoost?
text

CatBoost = Category Boosting

Created by Yandex (Russian tech giant) in 2017

WHY "CAT"?
┌─────────────────────────────────────────────────────────────────┐
│ 1. Handles CATEgorical features automatically and efficiently  │
│ 2. Uses CATEgorical feature combinations                        │
│ 3. No need for manual encoding!                                 │
│ 4. State-of-the-art performance on datasets with categories     │
└─────────────────────────────────────────────────────────────────┘

KEY STRENGTHS:
┌─────────────────────────────────────────────────────────────────┐
│ ✓ Best-in-class categorical feature handling                    │
│ ✓ Robust to overfitting (ordered boosting)                      │
│ ✓ Fast prediction time                                          │
│ ✓ Works great with default parameters                           │
│ ✓ Built-in visualization tools                                  │
│ ✓ GPU support out of the box                                    │
└─────────────────────────────────────────────────────────────────┘

COMPARISON:
┌────────────────────┬──────────────┬───────────────┬──────────────┐
│                    │   XGBoost    │   LightGBM    │   CatBoost   │
├────────────────────┼──────────────┼───────────────┼──────────────┤
│ Categorical        │ Manual       │ Built-in      │ BEST         │
│ Handling           │ encoding     │ (basic)       │ (advanced)   │
├────────────────────┼──────────────┼───────────────┼──────────────┤
│ Overfitting        │ Moderate     │ Can overfit   │ Most robust  │
│ Resistance         │ resistance   │ easily        │              │
├────────────────────┼──────────────┼───────────────┼──────────────┤
│ Training Speed     │ Fast         │ FASTEST       │ Moderate     │
├────────────────────┼──────────────┼───────────────┼──────────────┤
│ Prediction Speed   │ Fast         │ Fast          │ FASTEST      │
├────────────────────┼──────────────┼───────────────┼──────────────┤
│ Tuning Required    │ Moderate     │ More tuning   │ LEAST        │
└────────────────────┴──────────────┴───────────────┴──────────────┘
6.2 CatBoost's Revolutionary Features
Innovation 1: Ordered Target Statistics

text

THE PROBLEM WITH TRADITIONAL TARGET ENCODING:
┌─────────────────────────────────────────────────────────────────┐
│ Dataset:                                                         │
│ ┌──────────┬────────┐                                            │
│ │ Category │ Target │                                            │
│ ├──────────┼────────┤                                            │
│ │    A     │   1    │ ← Calculate mean for A: (1+0+1)/3 = 0.67  │
│ │    A     │   0    │   But we're using THIS ROW in calculation! │
│ │    A     │   1    │   = TARGET LEAKAGE!                        │
│ │    B     │   0    │                                            │
│ │    B     │   1    │                                            │
│ └──────────┴────────┘                                            │
│                                                                  │
│ Traditional approach uses ALL data → Overfits!                  │
└─────────────────────────────────────────────────────────────────┘

CATBOOST'S SOLUTION: Ordered Target Statistics
┌─────────────────────────────────────────────────────────────────┐
│ Randomly shuffle data, then for each row i:                     │
│ Use ONLY rows 1 to i-1 to calculate statistics                  │
│                                                                  │
│ Shuffled Dataset:                                                │
│ ┌────┬──────────┬────────┬──────────────────┐                   │
│ │ i  │ Category │ Target │  Encoded Value   │                   │
│ ├────┼──────────┼────────┼──────────────────┤                   │
│ │ 1  │    B     │   0    │  0.5 (prior)     │ ← No previous B  │
│ │ 2  │    A     │   1    │  0.5 (prior)     │ ← No previous A  │
│ │ 3  │    B     │   1    │  0.0 (from i=1)  │ ← Use row 1      │
│ │ 4  │    A     │   0    │  1.0 (from i=2)  │ ← Use row 2      │
│ │ 5  │    A     │   1    │  0.5 (avg i=2,4) │ ← Use rows 2,4   │
│ └────┴──────────┴────────┴──────────────────┘                   │
│                                                                  │
│ Key: Never use current or future rows! → No leakage!            │
└─────────────────────────────────────────────────────────────────┘

FORMULA:
For sample i with category k:

                    Σ(target values of category k in rows 1 to i-1) + prior
Encoded_value_i = ─────────────────────────────────────────────────────────
                    Count(category k in rows 1 to i-1) + α

Where:
- prior = global mean of target
- α = smoothing parameter (default: 1)
Visual Comparison

text

TRADITIONAL TARGET ENCODING vs CATBOOST:

Dataset: City → House Price
┌──────────┬────────┐
│   City   │ Price  │
├──────────┼────────┤
│ NYC      │  500K  │
│ Boston   │  400K  │
│ NYC      │  600K  │
│ Boston   │  450K  │
│ NYC      │  550K  │
└──────────┴────────┘

TRADITIONAL (Leakage!):
NYC: (500+600+550)/3 = 550K for ALL NYC rows (including themselves!)

CATBOOST (Ordered, No Leakage):
Row 1 (NYC): Use prior (475K)
Row 3 (NYC): Use only row 1 → 500K
Row 5 (NYC): Use rows 1,3 → (500+600)/2 = 550K

Each row uses ONLY PAST information!
Innovation 2: Categorical Feature Combinations

Python

"""
CatBoost automatically creates useful feature combinations!
"""

# Example data
data = {
    'City': ['NYC', 'Boston', 'NYC', 'LA'],
    'Day': ['Mon', 'Mon', 'Tue', 'Mon'],
    'Price': [100, 80, 120, 90]
}

# CatBoost creates combinations like:
# - City_Day: NYC_Mon, Boston_Mon, NYC_Tue, LA_Mon
# - City_Day_Hour: (if Hour feature exists)
# - And more complex combinations!

# These combinations are created DURING training
# No manual feature engineering needed!
text

FEATURE COMBINATION TREE:

Level 0: Individual features
         [City]  [Day]  [Weather]

Level 1: Pairwise combinations
         [City+Day]  [City+Weather]  [Day+Weather]

Level 2: Triple combinations  
         [City+Day+Weather]

CatBoost intelligently selects which combinations help!
Controlled by: max_ctr_complexity parameter
Innovation 3: Oblivious Decision Trees

text

STANDARD TREE vs OBLIVIOUS TREE

STANDARD TREE (XGBoost, LightGBM):
Different split conditions at same level

                    Age > 30?
                   /         \
              Income > 50K?   Score > 700?  ← Different features!
              /    \          /      \
           Leaf1 Leaf2    Leaf3   Leaf4

OBLIVIOUS TREE (CatBoost):
SAME split condition at same level!

                    Age > 30?
                   /         \
              Age > 50?       Age > 50?  ← Same feature!
              /    \          /     \
          Leaf1  Leaf2    Leaf3   Leaf4

ADVANTAGES:
┌─────────────────────────────────────────────────────────────────┐
│ 1. FASTER PREDICTION                                             │
│    - Can use bit operations                                      │
│    - Branch prediction optimized                                 │
│    - Up to 8x faster than standard trees!                        │
│                                                                  │
│ 2. LESS OVERFITTING                                              │
│    - More balanced structure                                     │
│    - Regularization through symmetry                             │
│                                                                  │
│ 3. EASIER TO ANALYZE                                             │
│    - Simpler structure                                           │
│    - Better interpretability                                     │
└─────────────────────────────────────────────────────────────────┘

PREDICTION ALGORITHM:
Instead of traversing tree:
1. Evaluate all splits → Create binary vector
2. Use vector as index into leaf array
3. O(depth) instead of O(depth × comparisons)
Visual: Oblivious Tree Prediction

text

Example: Predict for [Age=35, Income=60K, Score=680]

Oblivious Tree:
Level 0: Age > 30?     → YES (1)
Level 1: Income > 50K? → YES (1)
Level 2: Score > 700?  → NO  (0)

Binary path: 1-1-0 → Index 6 (binary: 110)

Leaf values array: [v0, v1, v2, v3, v4, v5, v6, v7]
                                             ↑
Prediction = v6 (direct array access!)

Standard tree would need to traverse and compare at each node!
6.3 CatBoost Parameters Encyclopedia
Core Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER          │ DEFAULT  │ DESCRIPTION                                │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ iterations         │ 1000     │ Number of trees (like n_estimators)        │
│                    │          │ CatBoost usually needs fewer trees         │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ learning_rate      │ Auto     │ Step size (usually 0.03-0.1)               │
│                    │          │ Auto-selected based on dataset size        │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ depth              │ 6        │ Tree depth                                 │
│                    │          │ Typical: 4-10 (oblivious trees need less)  │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ l2_leaf_reg        │ 3.0      │ L2 regularization (larger = simpler)       │
│                    │          │ Main overfitting control                   │
├────────────────────┼──────────┼────────────────────────────────────────────┤
│ loss_function      │ Auto     │ 'RMSE', 'Logloss', 'MultiClass', etc.      │
│                    │          │ Auto-detected from data                    │
└────────────────────────────────────────────────────────────────────────────┘
Categorical Feature Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER              │ DEFAULT │ DESCRIPTION                             │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ cat_features           │ None    │ List/indices of categorical features    │
│                        │         │ Auto-detect if string/object type       │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ one_hot_max_size       │ 2       │ Max unique values for one-hot encoding  │
│                        │         │ If categories ≤ this → one-hot          │
│                        │         │ If categories > this → target stats     │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ max_ctr_complexity     │ 4       │ Max depth of categorical combinations   │
│                        │         │ Higher = more combinations, slower      │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ ctr_leaf_count_limit   │ None    │ Max leaves with categorical features    │
│                        │         │ Limits model size                       │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ simple_ctr             │ Auto    │ How to encode categories:               │
│                        │         │ 'Borders','Buckets','BinarizedTargetMean'│
└────────────────────────────────────────────────────────────────────────────┘

CTR = Counter (Categorical feature TRansformation)
Ordered Boosting Parameters

text

┌────────────────────────────────────────────────────────────────────────────┐
│ PARAMETER              │ DEFAULT │ DESCRIPTION                             │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ boosting_type          │'Plain'  │ 'Ordered' or 'Plain'                    │
│                        │         │ Ordered = more robust, slower           │
│                        │         │ Plain = faster, may overfit             │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ bootstrap_type         │ 'MVS'   │ Sampling method:                        │
│                        │         │ 'Bayesian','Bernoulli','MVS','Poisson'  │
├────────────────────────┼─────────┼─────────────────────────────────────────┤
│ sampling_frequency     │'PerTree'│ When to sample:                         │
│                        │         │ 'PerTree' or 'PerTreeLevel'             │
└────────────────────────────────────────────────────────────────────────────┘
6.4 CatBoost Code Implementation
Basic Usage

Python

# =============================================================================
# CATBOOST: COMPLETE IMPLEMENTATION GUIDE
# =============================================================================

from catboost import CatBoostRegressor, CatBoostClassifier, Pool
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, mean_squared_error, roc_auc_score
import matplotlib.pyplot as plt

# -----------------------------------------------------------------------------
# STEP 1: PREPARE DATA WITH CATEGORICAL FEATURES
# -----------------------------------------------------------------------------

# Create realistic dataset with categorical features
np.random.seed(42)
n_samples = 10000

data = pd.DataFrame({
    # Numerical features
    'age': np.random.randint(18, 80, n_samples),
    'income': np.random.randint(20000, 150000, n_samples),
    'credit_score': np.random.randint(300, 850, n_samples),
    
    # Categorical features (CatBoost's strength!)
    'city': np.random.choice(['NYC', 'LA', 'Chicago', 'Houston', 'Phoenix'], n_samples),
    'occupation': np.random.choice(['Engineer', 'Doctor', 'Teacher', 'Artist', 'Other'], n_samples),
    'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], n_samples),
    'marital_status': np.random.choice(['Single', 'Married', 'Divorced'], n_samples),
})

# Create target (influenced by both numerical and categorical features)
data['target'] = (
    0.01 * data['age'] +
    0.00002 * data['income'] +
    0.002 * data['credit_score'] +
    np.where(data['city'] == 'NYC', 5, 0) +
    np.where(data['occupation'] == 'Doctor', 3, 0) +
    np.random.randn(n_samples) * 2
)

# Categorical columns
cat_features = ['city', 'occupation', 'education', 'marital_status']

# Split data
X = data.drop('target', axis=1)
y = data['target']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# -----------------------------------------------------------------------------
# STEP 2: BASIC REGRESSION MODEL
# -----------------------------------------------------------------------------

# Method 1: Simple approach
model = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.1,
    depth=6,
    loss_function='RMSE',
    cat_features=cat_features,  # Specify categorical features!
    random_seed=42,
    verbose=100  # Print every 100 iterations
)

model.fit(X_train, y_train)

# Predictions
predictions = model.predict(X_test)
rmse = np.sqrt(mean_squared_error(y_test, predictions))
print(f"RMSE: {rmse:.4f}")

# Method 2: Using Pool (More efficient for large datasets)
train_pool = Pool(
    data=X_train,
    label=y_train,
    cat_features=cat_features
)

test_pool = Pool(
    data=X_test,
    label=y_test,
    cat_features=cat_features
)

model_pool = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.1,
    depth=6,
    random_seed=42,
    verbose=100
)

model_pool.fit(train_pool, eval_set=test_pool)

# -----------------------------------------------------------------------------
# STEP 3: CLASSIFICATION MODEL
# -----------------------------------------------------------------------------

# Create binary target
y_clf = (y > y.median()).astype(int)
X_train_c, X_test_c, y_train_c, y_test_c = train_test_split(
    X, y_clf, test_size=0.2, random_state=42
)

model_clf = CatBoostClassifier(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    loss_function='Logloss',
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_clf.fit(
    X_train_c, y_train_c,
    eval_set=(X_test_c, y_test_c),
    early_stopping_rounds=50
)

# Predictions
y_pred = model_clf.predict(X_test_c)
y_pred_proba = model_clf.predict_proba(X_test_c)[:, 1]

accuracy = accuracy_score(y_test_c, y_pred)
auc = roc_auc_score(y_test_c, y_pred_proba)

print(f"Accuracy: {accuracy:.4f}")
print(f"AUC: {auc:.4f}")

# -----------------------------------------------------------------------------
# STEP 4: FEATURE IMPORTANCE
# -----------------------------------------------------------------------------

# Get feature importance
feature_importance = model.get_feature_importance(train_pool)
feature_names = X_train.columns

# Create DataFrame
importance_df = pd.DataFrame({
    'feature': feature_names,
    'importance': feature_importance
}).sort_values('importance', ascending=False)

print(importance_df)

# Plot
plt.figure(figsize=(10, 6))
plt.barh(importance_df['feature'], importance_df['importance'])
plt.xlabel('Importance')
plt.title('CatBoost Feature Importance')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()

# Different importance types
for importance_type in ['PredictionValuesChange', 'LossFunctionChange']:
    importance = model.get_feature_importance(
        train_pool,
        type=importance_type
    )
    print(f"\n{importance_type}:")
    print(pd.DataFrame({'feature': feature_names, 'importance': importance})
          .sort_values('importance', ascending=False))

# -----------------------------------------------------------------------------
# STEP 5: CATEGORICAL FEATURE STATISTICS
# -----------------------------------------------------------------------------

# See how CatBoost encoded categorical features
cat_feature_indices = [X_train.columns.get_loc(col) for col in cat_features]

# Get statistics for one categorical feature (e.g., 'city')
city_idx = X_train.columns.get_loc('city')

# CatBoost creates multiple transformations
# We can inspect them
print("\nCategorical transformations created by CatBoost:")
print(model.get_all_params()['ctr_description'])

# -----------------------------------------------------------------------------
# STEP 6: CROSS-VALIDATION
# -----------------------------------------------------------------------------

from catboost import cv

# Prepare full dataset as Pool
full_pool = Pool(
    data=X,
    label=y,
    cat_features=cat_features
)

# Cross-validation
cv_results = cv(
    pool=full_pool,
    params={
        'iterations': 1000,
        'learning_rate': 0.1,
        'depth': 6,
        'loss_function': 'RMSE',
        'random_seed': 42,
        'verbose': 100
    },
    fold_count=5,
    early_stopping_rounds=50,
    plot=True  # Visualize CV results!
)

print(f"\nCV Results:")
print(f"Best iteration: {cv_results['test-RMSE-mean'].idxmin()}")
print(f"Best RMSE: {cv_results['test-RMSE-mean'].min():.4f}")

# -----------------------------------------------------------------------------
# STEP 7: HYPERPARAMETER TUNING (Grid Search)
# -----------------------------------------------------------------------------

from catboost import CatBoostRegressor
from sklearn.model_selection import GridSearchCV

# Define parameter grid
param_grid = {
    'depth': [4, 6, 8],
    'learning_rate': [0.01, 0.05, 0.1],
    'l2_leaf_reg': [1, 3, 5, 7],
    'iterations': [500]
}

# Note: CatBoost with sklearn API
model_grid = CatBoostRegressor(
    cat_features=cat_features,
    random_seed=42,
    verbose=0
)

# Grid search
grid_search = GridSearchCV(
    model_grid,
    param_grid,
    cv=3,
    scoring='neg_mean_squared_error',
    n_jobs=-1,
    verbose=2
)

grid_search.fit(X_train, y_train)

print(f"\nBest parameters: {grid_search.best_params_}")
print(f"Best score: {-grid_search.best_score_:.4f}")

# -----------------------------------------------------------------------------
# STEP 8: SAVING AND LOADING MODELS
# -----------------------------------------------------------------------------

# Save model (multiple formats)
model.save_model('catboost_model.cbm')       # CatBoost format
model.save_model('catboost_model.json', format='json')  # JSON
model.save_model('catboost_model.onnx', format='onnx')  # ONNX

# Load model
loaded_model = CatBoostRegressor()
loaded_model.load_model('catboost_model.cbm')

# Verify
loaded_predictions = loaded_model.predict(X_test)
print(f"\nPredictions match: {np.allclose(predictions, loaded_predictions)}")

# -----------------------------------------------------------------------------
# STEP 9: MODEL ANALYSIS AND VISUALIZATION
# -----------------------------------------------------------------------------

# Plot training progress
model.plot()

# Get best iteration
print(f"Best iteration: {model.best_iteration_}")
print(f"Best score: {model.best_score_}")

# Get training metrics history
print("\nMetrics history:")
print(model.evals_result_)

# Feature statistics
print("\nFeature statistics:")
print(model.calc_feature_statistics(X_train, y_train, cat_features=cat_features))# =============================================================================
# ADVANCED CATBOOST TECHNIQUES
# =============================================================================

# -----------------------------------------------------------------------------
# TECHNIQUE 1: ORDERED BOOSTING (Maximum Robustness)
# -----------------------------------------------------------------------------

# Ordered boosting prevents target leakage in categorical encoding
# Best for datasets with many categorical features

model_ordered = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.05,
    depth=6,
    boosting_type='Ordered',  # More robust but slower
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_ordered.fit(X_train, y_train)

# Compare with Plain boosting (faster but may overfit)
model_plain = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.05,
    depth=6,
    boosting_type='Plain',  # Faster
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_plain.fit(X_train, y_train)

# Compare performance
ordered_rmse = np.sqrt(mean_squared_error(y_test, model_ordered.predict(X_test)))
plain_rmse = np.sqrt(mean_squared_error(y_test, model_plain.predict(X_test)))

print(f"Ordered boosting RMSE: {ordered_rmse:.4f}")
print(f"Plain boosting RMSE: {plain_rmse:.4f}")

# -----------------------------------------------------------------------------
# TECHNIQUE 2: CUSTOM LOSS FUNCTIONS
# -----------------------------------------------------------------------------

from catboost import FairLossObjective

# Custom loss: Quantile regression (predict median instead of mean)
model_quantile = CatBoostRegressor(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    loss_function='Quantile:alpha=0.5',  # Median
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_quantile.fit(X_train, y_train)

# Different quantiles
quantiles = [0.1, 0.5, 0.9]
predictions_dict = {}

for q in quantiles:
    model_q = CatBoostRegressor(
        iterations=500,
        loss_function=f'Quantile:alpha={q}',
        cat_features=cat_features,
        random_seed=42,
        verbose=0
    )
    model_q.fit(X_train, y_train)
    predictions_dict[f'q{int(q*100)}'] = model_q.predict(X_test)

# Visualize prediction intervals
plt.figure(figsize=(12, 6))
plt.scatter(range(100), y_test[:100], label='Actual', alpha=0.6)
plt.plot(range(100), predictions_dict['q50'][:100], label='Median (50%)', linewidth=2)
plt.fill_between(
    range(100),
    predictions_dict['q10'][:100],
    predictions_dict['q90'][:100],
    alpha=0.3,
    label='10-90% interval'
)
plt.legend()
plt.title('Quantile Regression: Prediction Intervals')
plt.xlabel('Sample')
plt.ylabel('Target Value')
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# TECHNIQUE 3: HANDLING IMBALANCED DATA
# -----------------------------------------------------------------------------

# For classification with class imbalance
# Calculate class weights
class_counts = y_train_c.value_counts()
class_weight_dict = {
    0: len(y_train_c) / (2 * class_counts[0]),
    1: len(y_train_c) / (2 * class_counts[1])
}

model_weighted = CatBoostClassifier(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    class_weights=class_weight_dict,  # Apply class weights
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_weighted.fit(X_train_c, y_train_c)

# Alternative: Use auto_class_weights
model_auto_weighted = CatBoostClassifier(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    auto_class_weights='Balanced',  # Automatic balancing
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_auto_weighted.fit(X_train_c, y_train_c)

# -----------------------------------------------------------------------------
# TECHNIQUE 4: TEXT FEATURES
# -----------------------------------------------------------------------------

# CatBoost can handle text features automatically!
data_text = pd.DataFrame({
    'text_feature': [
        'great product highly recommend',
        'terrible service never again',
        'average quality okay price',
        'excellent fast delivery',
        'poor quality broke quickly'
    ] * 2000,
    'category': np.random.choice(['A', 'B', 'C'], 10000),
    'price': np.random.randint(10, 100, 10000)
})

data_text['target'] = np.random.rand(10000)

# Specify text features
text_features = ['text_feature']
cat_features_with_text = ['category']

# Train with text features
model_text = CatBoostRegressor(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    text_features=text_features,  # CatBoost tokenizes automatically!
    cat_features=cat_features_with_text,
    random_seed=42,
    verbose=100
)

X_text = data_text.drop('target', axis=1)
y_text = data_text['target']

model_text.fit(X_text, y_text)

# CatBoost automatically:
# 1. Tokenizes text
# 2. Creates n-grams
# 3. Applies TF-IDF weighting
# 4. Uses as features!

# -----------------------------------------------------------------------------
# TECHNIQUE 5: FEATURE INTERACTIONS (Automatic)
# -----------------------------------------------------------------------------

# CatBoost can automatically find feature interactions
model_interactions = CatBoostRegressor(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    max_ctr_complexity=4,  # Max depth of categorical combinations
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_interactions.fit(X_train, y_train)

# Get interaction strength
interaction_strength = model_interactions.get_feature_importance(
    data=train_pool,
    type='Interaction'
)

# Find top interactions
n_features = len(X_train.columns)
interaction_matrix = np.zeros((n_features, n_features))

# CatBoost returns pairwise interactions
for i in range(n_features):
    for j in range(n_features):
        if i != j:
            # This is a simplified version; actual API may differ
            try:
                interaction_matrix[i, j] = interaction_strength[i * n_features + j]
            except:
                pass

# Visualize interaction heatmap
plt.figure(figsize=(10, 8))
plt.imshow(interaction_matrix, cmap='YlOrRd', aspect='auto')
plt.colorbar(label='Interaction Strength')
plt.xticks(range(n_features), X_train.columns, rotation=45, ha='right')
plt.yticks(range(n_features), X_train.columns)
plt.title('Feature Interaction Matrix')
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# TECHNIQUE 6: GPU ACCELERATION
# -----------------------------------------------------------------------------

# Use GPU for massive speedup (requires GPU-enabled CatBoost)
model_gpu = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.1,
    depth=8,
    task_type='GPU',  # Use GPU!
    devices='0',      # GPU device ID
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

# GPU training can be 20-40x faster for large datasets!
# model_gpu.fit(X_train, y_train)

# -----------------------------------------------------------------------------
# TECHNIQUE 7: SNAPSHOT SAVING (For Long Training)
# -----------------------------------------------------------------------------

# Save snapshots during training (useful for very long training runs)
model_snapshot = CatBoostRegressor(
    iterations=10000,
    learning_rate=0.01,
    depth=6,
    cat_features=cat_features,
    random_seed=42,
    save_snapshot=True,  # Enable snapshots
    snapshot_file='catboost_snapshot.cbsnapshot',
    snapshot_interval=100,  # Save every 100 iterations
    verbose=100
)

# If training is interrupted, can resume from snapshot
# model_snapshot.fit(X_train, y_train)

# Resume from snapshot
# model_resumed = CatBoostRegressor()
# model_resumed.load_model('catboost_snapshot.cbsnapshot')
# model_resumed.fit(X_train, y_train)  # Continues from snapshot

# -----------------------------------------------------------------------------
# TECHNIQUE 8: MODEL ANALYSIS - SHAP VALUES
# -----------------------------------------------------------------------------

# CatBoost has built-in SHAP support
shap_values = model.get_feature_importance(
    data=train_pool,
    type='ShapValues'
)

# SHAP values for first prediction
print("\nSHAP values for first sample:")
print(f"Prediction: {model.predict(X_test.iloc[[0]])}")
print(f"SHAP values: {shap_values[0]}")

# Plot SHAP summary
import shap
explainer = shap.TreeExplainer(model)
shap_values_detailed = explainer.shap_values(X_test)

plt.figure(figsize=(10, 6))
shap.summary_plot(shap_values_detailed, X_test, plot_type="bar")
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# TECHNIQUE 9: OBJECT IMPORTANCE
# -----------------------------------------------------------------------------

# Find which training samples are most important
object_importance = model.get_object_importance(
    pool=train_pool,
    update_method='AllPoints',  # or 'TopKLeaves', 'SinglePoint'
    importance_values_sign='All'
)

# Get top influential training samples
top_influential_idx = np.argsort(object_importance)[-10:]
print("\nTop 10 most influential training samples:")
print(X_train.iloc[top_influential_idx])

# -----------------------------------------------------------------------------
# TECHNIQUE 10: PREDICTION INTERVALS WITH VIRTUAL ENSEMBLES
# -----------------------------------------------------------------------------

# CatBoost can create virtual ensembles for uncertainty estimation
model_ensemble = CatBoostRegressor(
    iterations=1000,
    learning_rate=0.1,
    depth=6,
    cat_features=cat_features,
    random_seed=42,
    verbose=0
)

model_ensemble.fit(X_train, y_train)

# Get predictions from different parts of the ensemble
virtual_ensembles_count = 5
predictions_ensemble = model_ensemble.virtual_ensembles_predict(
    data=X_test,
    prediction_type='RawFormulaVal',
    virtual_ensembles_count=virtual_ensembles_count
)

# Calculate prediction intervals
mean_pred = predictions_ensemble.mean(axis=0)
std_pred = predictions_ensemble.std(axis=0)

# 95% confidence intervals
lower_bound = mean_pred - 1.96 * std_pred
upper_bound = mean_pred + 1.96 * std_pred

# Visualize
plt.figure(figsize=(12, 6))
plt.scatter(range(50), y_test[:50], label='Actual', alpha=0.6, color='blue')
plt.plot(range(50), mean_pred[:50], label='Prediction', color='red', linewidth=2)
plt.fill_between(
    range(50),
    lower_bound[:50],
    upper_bound[:50],
    alpha=0.3,
    color='red',
    label='95% CI'
)
plt.legend()
plt.title('Prediction Uncertainty with Virtual Ensembles')
plt.xlabel('Sample')
plt.ylabel('Target Value')
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# TECHNIQUE 11: MULTICLASS CLASSIFICATION
# -----------------------------------------------------------------------------

# Create multiclass target
y_multi = pd.cut(y, bins=5, labels=['Very Low', 'Low', 'Medium', 'High', 'Very High'])

X_train_m, X_test_m, y_train_m, y_test_m = train_test_split(
    X, y_multi, test_size=0.2, random_state=42
)

model_multiclass = CatBoostClassifier(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    loss_function='MultiClass',
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_multiclass.fit(X_train_m, y_train_m)

# Predictions
y_pred_multi = model_multiclass.predict(X_test_m)
y_pred_proba_multi = model_multiclass.predict_proba(X_test_m)

# Accuracy
accuracy_multi = accuracy_score(y_test_m, y_pred_multi)
print(f"\nMulticlass Accuracy: {accuracy_multi:.4f}")

# Confusion matrix
from sklearn.metrics import confusion_matrix
import seaborn as sns

cm = confusion_matrix(y_test_m, y_pred_multi)

plt.figure(figsize=(10, 8))
sns.heatmap(
    cm,
    annot=True,
    fmt='d',
    cmap='Blues',
    xticklabels=['Very Low', 'Low', 'Medium', 'High', 'Very High'],
    yticklabels=['Very Low', 'Low', 'Medium', 'High', 'Very High']
)
plt.title('Confusion Matrix - Multiclass Classification')
plt.ylabel('Actual')
plt.xlabel('Predicted')
plt.tight_layout()
plt.show()

# -----------------------------------------------------------------------------
# TECHNIQUE 12: CUSTOM EVALUATION METRIC
# -----------------------------------------------------------------------------

class CustomMetric(object):
    """Custom evaluation metric: MAPE (Mean Absolute Percentage Error)"""
    
    def get_final_error(self, error, weight):
        return error / weight

    def is_max_optimal(self):
        return False  # Lower is better

    def evaluate(self, approxes, target, weight):
        # approxes - list of predictions
        # target - true values
        # weight - sample weights
        
        assert len(approxes) == 1
        assert len(target) == len(approxes[0])
        
        preds = np.array(approxes[0])
        targets = np.array(target)
        
        # Calculate MAPE
        mask = targets != 0  # Avoid division by zero
        mape = np.mean(np.abs((targets[mask] - preds[mask]) / targets[mask])) * 100
        
        return mape, 1.0

# Use custom metric
model_custom_metric = CatBoostRegressor(
    iterations=500,
    learning_rate=0.1,
    depth=6,
    eval_metric=CustomMetric(),
    cat_features=cat_features,
    random_seed=42,
    verbose=100
)

model_custom_metric.fit(
    X_train, y_train,
    eval_set=(X_test, y_test)
)
Chapter 7: Comparative Analysis
7.1 XGBoost vs LightGBM vs CatBoost - Detailed Comparison
text

┌─────────────────────────────────────────────────────────────────────────────┐
│                        COMPREHENSIVE COMPARISON                              │
├──────────────────┬───────────────┬───────────────┬───────────────────────────┤
│    ASPECT        │   XGBOOST     │   LIGHTGBM    │      CATBOOST             │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ SPEED            │               │               │                           │
│ Training         │ ⭐⭐⭐         │ ⭐⭐⭐⭐⭐     │ ⭐⭐⭐⭐                    │
│ Prediction       │ ⭐⭐⭐⭐       │ ⭐⭐⭐⭐       │ ⭐⭐⭐⭐⭐ (Fastest!)        │
│ Small data       │ Fast          │ Fastest       │ Moderate                  │
│ Large data       │ Moderate      │ Fastest       │ Fast                      │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ ACCURACY         │               │               │                           │
│ Tabular data     │ ⭐⭐⭐⭐⭐     │ ⭐⭐⭐⭐⭐     │ ⭐⭐⭐⭐⭐                   │
│ Categorical      │ ⭐⭐⭐         │ ⭐⭐⭐⭐       │ ⭐⭐⭐⭐⭐ (Best!)          │
│ High-dim sparse  │ ⭐⭐⭐⭐       │ ⭐⭐⭐⭐⭐     │ ⭐⭐⭐⭐                    │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ OVERFITTING      │               │               │                           │
│ Resistance       │ Good          │ Moderate      │ Excellent (Best!)         │
│ Default params   │ May overfit   │ May overfit   │ More robust               │
│ Small data       │ Needs tuning  │ Needs tuning  │ Works well                │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ EASE OF USE      │               │               │                           │
│ Learning curve   │ Moderate      │ Moderate      │ Easiest                   │
│ Default params   │ Need tuning   │ Need tuning   │ Work well!                │
│ Documentation    │ Excellent     │ Good          │ Excellent                 │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ CATEGORICAL      │               │               │                           │
│ Handling         │ Manual        │ Built-in      │ Advanced (Best!)          │
│                  │ encoding      │ (basic)       │ Ordered TS                │
│ Performance      │ ⭐⭐           │ ⭐⭐⭐         │ ⭐⭐⭐⭐⭐                   │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ MISSING VALUES   │               │               │                           │
│ Handling         │ Automatic     │ Automatic     │ Automatic                 │
│ Method           │ Sparsity-aware│ Native        │ Various modes             │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ GPU SUPPORT      │               │               │                           │
│ Availability     │ Yes           │ Yes           │ Yes                       │
│ Maturity         │ Mature        │ Mature        │ Excellent                 │
│ Speedup          │ 5-10x         │ 5-20x         │ 20-40x (Best!)            │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ MEMORY USAGE     │               │               │                           │
│ Training         │ Moderate      │ Low (Best!)   │ Moderate                  │
│ Prediction       │ Moderate      │ Moderate      │ Low                       │
│ Large datasets   │ Can struggle  │ Excellent     │ Good                      │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ INTERPRETABILITY │               │               │                           │
│ Feature import.  │ Yes           │ Yes           │ Yes + more                │
│ SHAP values      │ External lib  │ External lib  │ Built-in                  │
│ Visualization    │ Good          │ Good          │ Excellent                 │
├──────────────────┼───────────────┼───────────────┼───────────────────────────┤
│ SPECIAL FEATURES │               │               │                           │
│                  │ • System opt. │ • GOSS        │ • Ordered boosting        │
│                  │ • Regularized │ • Histogram   │ • Oblivious trees         │
│                  │ • Sparse aware│ • Leaf-wise   │ • Text features           │
│                  │               │ • EFB         │ • Object importance       │
└──────────────────┴───────────────┴───────────────┴───────────────────────────┘
7.2 When to Use Which?
text

┌─────────────────────────────────────────────────────────────────────┐
│                    DECISION FLOWCHART                                │
└─────────────────────────────────────────────────────────────────────┘

START: What is your data like?
    │
    ├─ SMALL DATASET (< 10K rows)
    │   └─> Use: CATBOOST
    │       Reason: Most robust to overfitting with defaults
    │
    ├─ MEDIUM DATASET (10K - 1M rows)
    │   │
    │   ├─ Many categorical features?
    │   │   └─ YES → CATBOOST (best categorical handling)
    │   │   └─ NO  → XGBOOST (most battle-tested)
    │   │
    │   └─ Need fastest training?
    │       └─> LIGHTGBM
    │
    ├─ LARGE DATASET (> 1M rows)
    │   │
    │   ├─ Memory constrained?
    │   │   └─ YES → LIGHTGBM (histogram, GOSS)
    │   │   └─ NO  → LIGHTGBM or XGBOOST
    │   │
    │   └─ High-dimensional sparse?
    │       └─> LIGHTGBM (EFB feature bundling)
    │
    └─ PRODUCTION DEPLOYMENT
        │
        ├─ Need fastest prediction?
        │   └─> CATBOOST (oblivious trees)
        │
        ├─ Need smallest model size?
        │   └─> LIGHTGBM
        │
        └─ Need most mature ecosystem?
            └─> XGBOOST

┌─────────────────────────────────────────────────────────────────────┐
│                    USE CASE RECOMMENDATIONS                          │
├─────────────────────────────────┬───────────────────────────────────┤
│           USE CASE              │       BEST CHOICE                 │
├─────────────────────────────────┼───────────────────────────────────┤
│ Kaggle competitions             │ Try all 3, ensemble               │
│ E-commerce (user behavior)      │ CatBoost (many categories)        │
│ Finance (credit scoring)        │ XGBoost (regulatory, stable)      │
│ Ad click prediction             │ LightGBM (large scale, sparse)    │
│ Medical diagnosis               │ CatBoost (robust, interpretable)  │
│ Time series forecasting         │ XGBoost or LightGBM               │
│ NLP + tabular                   │ CatBoost (text features)          │
│ Real-time predictions           │ CatBoost (fast inference)         │
│ IoT sensor data                 │ LightGBM (memory efficient)       │
│ Fraud detection                 │ XGBoost (imbalanced data tools)   │
└─────────────────────────────────┴───────────────────────────────────┘
7.3 Benchmark Comparison - Code
Python

# =============================================================================
# COMPREHENSIVE BENCHMARK: XGBOOST vs LIGHTGBM vs CATBOOST
# =============================================================================

import xgboost as xgb
import lightgbm as lgb
from catboost import CatBoostRegressor, CatBoostClassifier
import time
import numpy as np
import pandas as pd
from sklearn.datasets import make_classification, make_regression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, roc_auc_score, mean_squared_error
import matplotlib.pyplot as plt

# -----------------------------------------------------------------------------
# DATASET CREATION
# -----------------------------------------------------------------------------

def create_benchmark_datasets():
    """Create various datasets for benchmarking"""
    
    datasets = {}
    
    # 1. Small regression dataset
    X_small, y_small = make_regression(
        n_samples=1000,
        n_features=20,
        n_informative=15,
        noise=10,
        random_state=42
    )
    datasets['small_regression'] = (X_small, y_small)
    
    # 2. Medium regression dataset
    X_medium, y_medium = make_regression(
        n_samples=100000,
        n_features=50,
        n_informative=30,
        noise=10,
        random_state=42
    )
    datasets['medium_regression'] = (X_medium, y_medium)
    
    # 3. Large regression dataset
    X_large, y_large = make_regression(
        n_samples=1000000,
        n_features=100,
        n_informative=50,
        noise=10,
        random_state=42
    )
    datasets['large_regression'] = (X_large, y_large)
    
    # 4. Classification dataset
    X_clf, y_clf = make_classification(
        n_samples=100000,
        n_features=50,
        n_informative=30,
        n_redundant=10,
        n_classes=2,
        random_state=42
    )
    datasets['classification'] = (X_clf, y_clf)
    
    # 5. Dataset with categorical features
    n_samples = 50000
    df_cat = pd.DataFrame({
        'num1': np.random.randn(n_samples),
        'num2': np.random.randn(n_samples),
        'cat1': np.random.choice(['A', 'B', 'C', 'D'], n_samples),
        'cat2': np.random.choice(['X', 'Y', 'Z'], n_samples),
        'cat3': np.random.choice([f'Cat{i}' for i in range(20)], n_samples),
    })
    df_cat['target'] = (
        df_cat['num1'] + 
        df_cat['num2'] + 
        (df_cat['cat1'] == 'A').astype(int) * 2 +
        np.random.randn(n_samples) * 0.5
    )
    datasets['categorical'] = (df_cat.drop('target', axis=1), df_cat['target'])
    
    return datasets

# -----------------------------------------------------------------------------
# BENCHMARK FUNCTION
# -----------------------------------------------------------------------------

def benchmark_model(model_class, X_train, X_test, y_train, y_test, 
                   params, model_name, cat_features=None):
    """Benchmark a single model"""
    
    results = {
        'model': model_name,
        'train_time': 0,
        'predict_time': 0,
        'train_score': 0,
        'test_score': 0,
        'memory_usage': 0
    }
    
    try:
        # Training
        start_time = time.time()
        
        if model_name == 'CatBoost' and cat_features is not None:
            model = model_class(**params, cat_features=cat_features, verbose=0)
        else:
            model = model_class(**params, verbose=0)
        
        model.fit(X_train, y_train)
        results['train_time'] = time.time() - start_time
        
        # Prediction time
        start_time = time.time()
        y_pred_test = model.predict(X_test)
        results['predict_time'] = time.time() - start_time
        
        # Scores
        y_pred_train = model.predict(X_train)
        
        # Regression metrics
        results['train_score'] = mean_squared_error(y_train, y_pred_train)
        results['test_score'] = mean_squared_error(y_test, y_pred_test)
        
    except Exception as e:
        print(f"Error in {model_name}: {str(e)}")
        results['error'] = str(e)
    
    return results

# -----------------------------------------------------------------------------
# RUN BENCHMARKS
# -----------------------------------------------------------------------------

def run_all_benchmarks():
    """Run comprehensive benchmarks"""
    
    datasets = create_benchmark_datasets()
    all_results = []
    
    # Common parameters (roughly equivalent)
    params_xgb = {
        'n_estimators': 100,
        'max_depth': 6,
        'learning_rate': 0.1,
        'random_state': 42
    }
    
    params_lgb = {
        'n_estimators': 100,
        'num_leaves': 31,
        'learning_rate': 0.1,
        'random_state': 42
    }
    
    params_cat = {
        'iterations': 100,
        'depth': 6,
        'learning_rate': 0.1,
        'random_seed': 42
    }
    
    # Benchmark each dataset
    for dataset_name, (X, y) in datasets.items():
        print(f"\n{'='*60}")
        print(f"Benchmarking: {dataset_name}")
        print(f"{'='*60}")
        
        # Handle categorical features
        if dataset_name == 'categorical':
            cat_features = ['cat1', 'cat2', 'cat3']
            # For XGBoost/LightGBM, need to encode
            X_encoded = pd.get_dummies(X, columns=cat_features)
            X_train, X_test, y_train, y_test = train_test_split(
                X_encoded, y, test_size=0.2, random_state=42
            )
            X_train_cat, X_test_cat, _, _ = train_test_split(
                X, y, test_size=0.2, random_state=42
            )
        else:
            X_train, X_test, y_train, y_test = train_test_split(
                X, y, test_size=0.2, random_state=42
            )
            cat_features = None
        
        # Limit large dataset size for faster benchmarking
        if dataset_name == 'large_regression':
            X_train = X_train[:100000]
            y_train = y_train[:100000]
        
        # XGBoost
        print("Testing XGBoost...")
        result_xgb = benchmark_model(
            xgb.XGBRegressor,
            X_train, X_test, y_train, y_test,
            params_xgb,
            'XGBoost'
        )
        result_xgb['dataset'] = dataset_name
        all_results.append(result_xgb)
        
        # LightGBM
        print("Testing LightGBM...")
        result_lgb = benchmark_model(
            lgb.LGBMRegressor,
            X_train, X_test, y_train, y_test,
            params_lgb,
            'LightGBM'
        )
        result_lgb['dataset'] = dataset_name
        all_results.append(result_lgb)
        
        # CatBoost
        print("Testing CatBoost...")
        if dataset_name == 'categorical':
            result_cat = benchmark_model(
                CatBoostRegressor,
                X_train_cat, X_test_cat, y_train, y_test,
                params_cat,
                'CatBoost',
                cat_features=cat_features
            )
        else:
            result_cat = benchmark_model(
                CatBoostRegressor,
                X_train, X_test, y_train, y_test,
                params_cat,
                'CatBoost'
            )
        result_cat['dataset'] = dataset_name
        all_results.append(result_cat)
        
        # Print results
        print(f"\nResults for {dataset_name}:")
        print(f"{'Model':<15} {'Train Time':<12} {'Pred Time':<12} {'Test RMSE':<12}")
        print("-" * 60)
        for result in [result_xgb, result_lgb, result_cat]:
            print(f"{result['model']:<15} "
                  f"{result['train_time']:>10.3f}s  "
                  f"{result['predict_time']:>10.5f}s  "
                  f"{np.sqrt(result['test_score']):>10.4f}")
    
    return pd.DataFrame(all_results)

# Run benchmarks
results_df = run_all_benchmarks()

# -----------------------------------------------------------------------------
# VISUALIZE RESULTS
# -----------------------------------------------------------------------------

# Training time comparison
fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# 1. Training time by dataset
pivot_train = results_df.pivot(index='dataset', columns='model', values='train_time')
pivot_train.plot(kind='bar', ax=axes[0, 0])
axes[0, 0].set_title('Training Time Comparison')
axes[0, 0].set_ylabel('Time (seconds)')
axes[0, 0].legend(title='Model')
axes[0, 0].grid(axis='y', alpha=0.3)

# 2. Prediction time by dataset
pivot_pred = results_df.pivot(index='dataset', columns='model', values='predict_time')
pivot_pred.plot(kind='bar', ax=axes[0, 1])
axes[0, 1].set_title('Prediction Time Comparison')
axes[0, 1].set_ylabel('Time (seconds)')
axes[0, 1].legend(title='Model')
axes[0, 1].grid(axis='y', alpha=0.3)

# 3. Test RMSE by dataset
pivot_rmse = results_df.pivot(index='dataset', columns='model', values='test_score')
pivot_rmse = np.sqrt(pivot_rmse)  # Convert MSE to RMSE
pivot_rmse.plot(kind='bar', ax=axes[1, 0])
axes[1, 0].set_title('Test RMSE Comparison')
axes[1, 0].set_ylabel('RMSE')
axes[1, 0].legend(title='Model')
axes[1, 0].grid(axis='y', alpha=0.3)

# 4. Speed vs Accuracy tradeoff
axes[1, 1].scatter(
    results_df[results_df['model']=='XGBoost']['train_time'],
    np.sqrt(results_df[results_df['model']=='XGBoost']['test_score']),
    s=100, label='XGBoost', alpha=0.6
)
axes[1, 1].scatter(
    results_df[results_df['model']=='LightGBM']['train_time'],
    np.sqrt(results_df[results_df['model']=='LightGBM']['test_score']),
    s=100, label='LightGBM', alpha=0.6
)
axes[1, 1].scatter(
    results_df[results_df['model']=='CatBoost']['train_time'],
    np.sqrt(results_df[results_df['model']=='CatBoost']['test_score']),
    s=100, label='CatBoost', alpha=0.6
)
axes[1, 1].set_xlabel('Training Time (seconds)')
axes[1, 1].set_ylabel('Test RMSE')
axes[1, 1].set_title('Speed vs Accuracy Tradeoff')
axes[1, 1].legend()
axes[1, 1].grid(alpha=0.3)

plt.tight_layout()
plt.savefig('gbm_comparison.png', dpi=300, bbox_inches='tight')
plt.show()

# Summary statistics
print("\n" + "="*60)
print("SUMMARY STATISTICS")
print("="*60)
print("\nAverage Training Time:")
print(results_df.groupby('model')['train_time'].mean().sort_values())

print("\nAverage Prediction Time:")
print(results_df.groupby('model')['predict_time'].mean().sort_values())

print("\nAverage Test RMSE:")
print(np.sqrt(results_df.groupby('model')['test_score'].mean()).sort_values())

# Winner count
print("\n" + "="*60)
print("WINNER COUNT (by metric)")
print("="*60)

for metric in ['train_time', 'predict_time', 'test_score']:
    winners = results_df.loc[results_df.groupby('dataset')[metric].idxmin()]['model']
    print(f"\nBest {metric}:")
    print(winners.value_counts())
Chapter 8: Hyperparameter Tuning Bible
8.1 Understanding Hyperparameters
text

┌─────────────────────────────────────────────────────────────────────┐
│                  HYPERPARAMETER HIERARCHY                            │
└─────────────────────────────────────────────────────────────────────┘

PRIORITY 1: PREVENT OVERFITTING (Most Important!)
├─ max_depth / num_leaves          [Control tree complexity]
├─ min_child_weight / min_data_in_leaf [Minimum samples per leaf]
├─ learning_rate                   [Step size]
├─ n_estimators                    [Number of trees]
└─ regularization (lambda, alpha)  [L1/L2 penalties]

PRIORITY 2: IMPROVE ACCURACY
├─ subsample / bagging_fraction    [Row sampling]
├─ colsample_bytree / feature_fraction [Feature sampling]
└─ gamma / min_gain_to_split       [Minimum gain for split]

PRIORITY 3: SPEED OPTIMIZATION
├─ max_bin                         [Histogram bins]
├─ n_jobs / num_threads            [Parallelization]
└─ device_type                     [CPU vs GPU]

PRIORITY 4: DOMAIN SPECIFIC
├─ monotone_constraints            [Business logic]
├─ scale_pos_weight                [Class imbalance]
└─ objective / loss_function       [Task-specific loss]
8.2 Systematic Tuning Strategy
text

┌─────────────────────────────────────────────────────────────────────┐
│                  TUNING WORKFLOW (Step-by-Step)                      │
└─────────────────────────────────────────────────────────────────────┘

STEP 1: START WITH DEFAULTS
┌───────────────────────────────────────────────────────────────────┐
│ • Use default parameters                                          │
│ • Establish baseline performance                                  │
│ • Check for obvious overfitting (train vs validation gap)         │
└───────────────────────────────────────────────────────────────────┘

STEP 2: FIX LEARNING RATE & NUMBER OF TREES
┌───────────────────────────────────────────────────────────────────┐
│ • Start: learning_rate = 0.1, n_estimators = 1000                 │
│ • Use early stopping (rounds = 50)                                 │
│ • Note: Optimal number of trees at lr=0.1                          │
└───────────────────────────────────────────────────────────────────┘

STEP 3: TUNE TREE STRUCTURE
┌───────────────────────────────────────────────────────────────────┐
│ Grid search:                                                       │
│ • max_depth: [3, 5, 7, 9] (XGBoost/CatBoost)                       │
│ • num_leaves: [15, 31, 63, 127] (LightGBM)                         │
│ • min_child_weight: [1, 3, 5, 7] (XGBoost)                         │
│ • min_data_in_leaf: [10, 20, 50, 100] (LightGBM/CatBoost)          │
└───────────────────────────────────────────────────────────────────┘

STEP 4: TUNE REGULARIZATION
┌───────────────────────────────────────────────────────────────────┐
│ Grid search:                                                       │
│ • lambda (L2): [0.1, 1, 5, 10]                                     │
│ • alpha (L1): [0, 0.1, 1, 5]                                       │
│ • gamma: [0, 0.1, 0.5, 1] (XGBoost)                                │
└───────────────────────────────────────────────────────────────────┘

STEP 5: TUNE SAMPLING
┌───────────────────────────────────────────────────────────────────┐
│ Grid search:                                                       │
│ • subsample: [0.6, 0.7, 0.8, 0.9, 1.0]                             │
│ • colsample_bytree: [0.6, 0.7, 0.8, 0.9, 1.0]                      │
└───────────────────────────────────────────────────────────────────┘

STEP 6: LOWER LEARNING RATE, INCREASE TREES
┌───────────────────────────────────────────────────────────────────┐
│ • Reduce learning_rate: 0.1 → 0.05 → 0.01                          │
│ • Increase n_estimators accordingly                                │
│ • Use early stopping                                               │
│ • Final tuning with cross-validation                               │
└───────────────────────────────────────────────────────────────────┘
8.3 Hyperparameter Tuning Code
Python

# =============================================================================
# COMPREHENSIVE HYPERPARAMETER TUNING GUIDE
# =============================================================================

import xgboost as xgb
import lightgbm as lgb
from catboost import CatBoostRegressor
from sklearn.model_selection import GridSearchCV, RandomizedSearchCV
from sklearn.model_selection import cross_val_score
from scipy.stats import uniform, randint
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Sample data
np.random.seed(42)
X_train = np.random.randn(1000, 20)
y_train = 3*X_train[:,0] + 2*X_train[:,1] - X_train[:,2] + np.random.randn(1000)*0.5

# -----------------------------------------------------------------------------
# METHOD 1: GRID SEARCH (Exhaustive but slow)
# -----------------------------------------------------------------------------

def grid_search_tuning(X, y, model_type='xgboost'):
    """Systematic grid search"""
    
    if model_type == 'xgboost':
        model = xgb.XGBRegressor(random_state=42, n_jobs=-1)
        
        param_grid = {
            'max_depth': [3, 5, 7],
            'learning_rate': [0.01, 0.05, 0.1],
            'n_estimators': [100, 300, 500],
            'min_child_weight': [1, 3, 5],
            'gamma': [0, 0.1, 0.5],
            'subsample': [0.8, 0.9, 1.0],
            'colsample_bytree': [0.8, 0.9, 1.0],
            'reg_alpha': [0, 0.1, 1],
            'reg_lambda': [1, 5, 10]
        }
    
    elif model_type == 'lightgbm':
        model = lgb.LGBMRegressor(random_state=42, n_jobs=-1)
        
        param_grid = {
            'num_leaves': [15, 31, 63],
            'learning_rate': [0.01, 0.05, 0.1],
            'n_estimators': [100, 300, 500],
            'min_child_samples': [10, 20, 50],
            'min_child_weight': [0.001, 0.01, 0.1],
            'subsample': [0.8, 0.9, 1.0],
            'colsample_bytree': [0.8, 0.9, 1.0],
            'reg_alpha': [0, 0.1, 1],
            'reg_lambda': [0, 1, 5]
        }
    
    elif model_type == 'catboost':
        model = CatBoostRegressor(random_seed=42, verbose=0)
        
        param_grid = {
            'depth': [4, 6, 8],
            'learning_rate': [0.01, 0.05, 0.1],
            'iterations': [100, 300, 500],
            'l2_leaf_reg': [1, 3, 5, 7],
            'border_count': [32, 64, 128],
            'bagging_temperature': [0, 0.5, 1]
        }
    
    # Grid search
    grid_search = GridSearchCV(
        estimator=model,
        param_grid=param_grid,
        cv=5,
        scoring='neg_mean_squared_error',
        n_jobs=-1,
        verbose=2
    )
    
    grid_search.fit(X, y)
    
    print(f"\nBest parameters for {model_type}:")
    print(grid_search.best_params_)
    print(f"Best score: {-grid_search.best_score_:.4f}")
    
    return grid_search.best_estimator_, grid_search.best_params_

# -----------------------------------------------------------------------------
# METHOD 2: RANDOMIZED SEARCH (Faster, good exploration)
# -----------------------------------------------------------------------------

def randomized_search_tuning(X, y, model_type='xgboost', n_iter=100):
    """Randomized search for faster tuning"""
    
    if model_type == 'xgboost':
        model = xgb.XGBRegressor(random_state=42, n_jobs=-1)
        
        param_distributions = {
            'max_depth': randint(3, 10),
            'learning_rate': uniform(0.01, 0.29),  # 0.01 to 0.3
            'n_estimators': randint(100, 1000),
            'min_child_weight': randint(1, 10),
            'gamma': uniform(0, 1),
            'subsample': uniform(0.6, 0.4),  # 0.6 to 1.0
            'colsample_bytree': uniform(0.6, 0.4),
            'reg_alpha': uniform(0, 10),
            'reg_lambda': uniform(0, 10)
        }
    
    elif model_type == 'lightgbm':
        model = lgb.LGBMRegressor(random_state=42, n_jobs=-1)
        
        param_distributions = {
            'num_leaves': randint(10, 150),
            'learning_rate': uniform(0.01, 0.29),
            'n_estimators': randint(100, 1000),
            'min_child_samples': randint(5, 100),
            'min_child_weight': uniform(0.001, 0.1),
            'subsample': uniform(0.6, 0.4),
            'colsample_bytree': uniform(0.6, 0.4),
            'reg_alpha': uniform(0, 10),
            'reg_lambda': uniform(0, 10)
        }
    
    elif model_type == 'catboost':
        model = CatBoostRegressor(random_seed=42, verbose=0)
        
        param_distributions = {
            'depth': randint(4, 10),
            'learning_rate': uniform(0.01, 0.29),
            'iterations': randint(100, 1000),
            'l2_leaf_reg': randint(1, 10),
            'border_count': [32, 64, 128, 256],
            'bagging_temperature': uniform(0, 1)
        }
    
    # Randomized search
    random_search = RandomizedSearchCV(
        estimator=model,
        param_distributions=param_distributions,
        n_iter=n_iter,
        cv=5,
        scoring='neg_mean_squared_error',
        n_jobs=-1,
        verbose=2,
        random_state=42
    )
    
    random_search.fit(X, y)
    
    print(f"\nBest parameters for {model_type}:")
    print(random_search.best_params_)
    print(f"Best score: {-random_search.best_score_:.4f}")
    
    return random_search.best_estimator_, random_search.best_params_

# -----------------------------------------------------------------------------
# METHOD 3: BAYESIAN OPTIMIZATION (Most efficient)
# -----------------------------------------------------------------------------

from skopt import BayesSearchCV
from skopt.space import Real, Integer

def bayesian_optimization_tuning(X, y, model_type='xgboost', n_iter=50):
    """Bayesian optimization for intelligent search"""
    
    if model_type == 'xgboost':
        model = xgb.XGBRegressor(random_state=42, n_jobs=-1)
        
        search_spaces = {
            'max_depth': Integer(3, 10),
            'learning_rate': Real(0.01, 0.3, prior='log-uniform'),
            'n_estimators': Integer(100, 1000),
            'min_child_weight': Integer(1, 10),
            'gamma': Real(0, 1),
            'subsample': Real(0.6, 1.0),
            'colsample_bytree': Real(0.6, 1.0),
            'reg_alpha': Real(0, 10, prior='log-uniform'),
            'reg_lambda': Real(0, 10, prior='log-uniform')
        }
    
    elif model_type == 'lightgbm':
        model = lgb.LGBMRegressor(random_state=42, n_jobs=-1)
        
        search_spaces = {
            'num_leaves': Integer(10, 150),
            'learning_rate': Real(0.01, 0.3, prior='log-uniform'),
            'n_estimators': Integer(100, 1000),
            'min_child_samples': Integer(5, 100),
            'subsample': Real(0.6, 1.0),
            'colsample_bytree': Real(0.6, 1.0),
            'reg_alpha': Real(0, 10, prior='log-uniform'),
            'reg_lambda': Real(0, 10, prior='log-uniform')
        }
    
    # Bayesian search
    bayes_search = BayesSearchCV(
        estimator=model,
        search_spaces=search_spaces,
        n_iter=n_iter,
        cv=5,
        scoring='neg_mean_squared_error',
        n_jobs=-1,
        verbose=2,
        random_state=42
    )
    
    bayes_search.fit(X, y)
    
    print(f"\nBest parameters for {model_type}:")
    print(bayes_search.best_params_)
    print(f"Best score: {-bayes_search.best_score_:.4f}")
    
    return bayes_search.best_estimator_, bayes_search.best_params_

# -----------------------------------------------------------------------------
# METHOD 4: OPTUNA (State-of-the-art optimization)
# -----------------------------------------------------------------------------

import optuna

def optuna_tuning(X, y, model_type='xgboost', n_trials=100):
    """Use Optuna for advanced hyperparameter optimization"""
    
    def objective(trial):
        if model_type == 'xgboost':
            params = {
                'max_depth': trial.suggest_int('max_depth', 3, 10),
                'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.3, log=True),
                'n_estimators': trial.suggest_int('n_estimators', 100, 1000),
                'min_child_weight': trial.suggest_int('min_child_weight', 1, 10),
                'gamma': trial.suggest_float('gamma', 0, 1),
                'subsample': trial.suggest_float('subsample', 0.6, 1.0),
                'colsample_bytree': trial.suggest_float('colsample_bytree', 0.6, 1.0),
                'reg_alpha': trial.suggest_float('reg_alpha', 0, 10, log=True),
                'reg_lambda': trial.suggest_float('reg_lambda', 0, 10, log=True),
                'random_state': 42
            }
            model = xgb.XGBRegressor(**params)
        
        elif model_type == 'lightgbm':
            params = {
                'num_leaves': trial.suggest_int('num_leaves', 10, 150),
                'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.3, log=True),
                'n_estimators': trial.suggest_int('n_estimators', 100, 1000),
                'min_child_samples': trial.suggest_int('min_child_samples', 5, 100),
                'subsample': trial.suggest_float('subsample', 0.6, 1.0),
                'colsample_bytree': trial.suggest_float('colsample_bytree', 0.6, 1.0),
                'reg_alpha': trial.suggest_float('reg_alpha', 0, 10, log=True),
                'reg_lambda': trial.suggest_float('reg_lambda', 0, 10, log=True),
                'random_state': 42
            }
            model = lgb.LGBMRegressor(**params)
        
        elif model_type == 'catboost':
            params = {
                'depth': trial.suggest_int('depth', 4, 10),
                'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.3, log=True),
                'iterations': trial.suggest_int('iterations', 100, 1000),
                'l2_leaf_reg': trial.suggest_int('l2_leaf_reg', 1, 10),
                'border_count': trial.suggest_categorical('border_count', [32, 64, 128, 256]),
                'bagging_temperature': trial.suggest_float('bagging_temperature', 0, 1),
                'random_seed': 42,
                'verbose': 0
            }
            model = CatBoostRegressor(**params)
        
        # Cross-validation score
        scores = cross_val_score(
            model, X, y,
            cv=5,
            scoring='neg_mean_squared_error',
            n_jobs=-1
        )
        
        return -scores.mean()
    
    # Create study
    study = optuna.create_study(
        direction='minimize',
        sampler=optuna.samplers.TPESampler(seed=42)
    )
    
    # Optimize
    study.optimize(objective, n_trials=n_trials, show_progress_bar=True)
    
    print(f"\nBest parameters for {model_type}:")
    print(study.best_params)
    print(f"Best score: {study.best_value:.4f}")
    
    # Visualization
    optuna.visualization.plot_optimization_history(study).show()
    optuna.visualization.plot_param_importances(study).show()
    
    return study.best_params

# -----------------------------------------------------------------------------
# METHOD 5: SEQUENTIAL TUNING (Step-by-step approach)
# -----------------------------------------------------------------------------

def sequential_tuning_xgboost(X_train, y_train, X_val, y_val):
    """
    Sequential tuning: Tune parameters in logical order
    This is often more efficient than random search!
    """
    
    print("="*60)
    print("SEQUENTIAL HYPERPARAMETER TUNING")
    print("="*60)
    
    # STEP 1: Find optimal number of trees with default params
    print("\nSTEP 1: Finding optimal number of trees...")
    model = xgb.XGBRegressor(
        learning_rate=0.1,
        random_state=42
    )
    
    eval_set = [(X_train, y_train), (X_val, y_val)]
    model.fit(
        X_train, y_train,
        eval_set=eval_set,
        eval_metric='rmse',
        early_stopping_rounds=50,
        verbose=False
    )
    
    optimal_trees = model.best_iteration
    print(f"Optimal trees at lr=0.1: {optimal_trees}")
    
    # STEP 2: Tune tree-specific parameters
    print("\nSTEP 2: Tuning tree structure...")
    param_grid = {
        'max_depth': [3, 5, 7, 9],
        'min_child_weight': [1, 3, 5, 7]
    }
    
    best_score = float('inf')
    best_params = {}
    
    for max_depth in param_grid['max_depth']:
        for min_child_weight in param_grid['min_child_weight']:
            model = xgb.XGBRegressor(
                max_depth=max_depth,
                min_child_weight=min_child_weight,
                learning_rate=0.1,
                n_estimators=optimal_trees,
                random_state=42
            )
            
            model.fit(X_train, y_train)
            pred = model.predict(X_val)
            score = mean_squared_error(y_val, pred)
            
            if score < best_score:
                best_score = score
                best_params = {
                    'max_depth': max_depth,
                    'min_child_weight': min_child_weight
                }
    
    print(f"Best tree params: {best_params}")
    print(f"Best score: {np.sqrt(best_score):.4f}")
    
    # STEP 3: Tune regularization
    print("\nSTEP 3: Tuning regularization...")
    param_grid = {
        'gamma': [0, 0.1, 0.5, 1, 2],
        'reg_alpha': [0, 0.1, 1, 5],
        'reg_lambda': [1, 5, 10, 20]
    }
    
    reg_best_score = float('inf')
    reg_best_params = {}
    
    for gamma in param_grid['gamma']:
        for reg_alpha in param_grid['reg_alpha']:
            for reg_lambda in param_grid['reg_lambda']:
                model = xgb.XGBRegressor(
                    **best_params,
                    gamma=gamma,
                    reg_alpha=reg_alpha,
                    reg_lambda=reg_lambda,
                    learning_rate=0.1,
                    n_estimators=optimal_trees,
                    random_state=42
                )
                
                model.fit(X_train, y_train)
                pred = model.predict(X_val)
                score = mean_squared_error(y_val, pred)
                
                if score < reg_best_score:
                    reg_best_score = score
                    reg_best_params = {
                        'gamma': gamma,
                        'reg_alpha': reg_alpha,
                        'reg_lambda': reg_lambda
                    }
    
    print(f"Best regularization params: {reg_best_params}")
    print(f"Best score: {np.sqrt(reg_best_score):.4f}")
    
    # STEP 4: Tune sampling parameters
    print("\nSTEP 4: Tuning sampling...")
    param_grid = {
        'subsample': [0.6, 0.7, 0.8, 0.9, 1.0],
        'colsample_bytree': [0.6, 0.7, 0.8, 0.9, 1.0]
    }
    
    sample_best_score = float('inf')
    sample_best_params = {}
    
    for subsample in param_grid['subsample']:
        for colsample in param_grid['colsample_bytree']:
            model = xgb.XGBRegressor(
                **best_params,
                **reg_best_params,
                subsample=subsample,
                colsample_bytree=colsample,
                learning_rate=0.1,
                n_estimators=optimal_trees,
                random_state=42
            )
            
            model.fit(X_train, y_train)
            pred = model.predict(X_val)
            score = mean_squared_error(y_val, pred)
            
            if score < sample_best_score:
                sample_best_score = score
                sample_best_params = {
                    'subsample': subsample,
                    'colsample_bytree': colsample
                }
    
    print(f"Best sampling params: {sample_best_params}")
    print(f"Best score: {np.sqrt(sample_best_score):.4f}")
    
    # STEP 5: Lower learning rate and increase trees
    print("\nSTEP 5: Fine-tuning with lower learning rate...")
    final_model = xgb.XGBRegressor(
        **best_params,
        **reg_best_params,
        **sample_best_params,
        learning_rate=0.01,  # Lower learning rate
        n_estimators=5000,
        random_state=42
    )
    
    final_model.fit(
        X_train, y_train,
        eval_set=[(X_val, y_val)],
        eval_metric='rmse',
        early_stopping_rounds=100,
        verbose=False
    )
    
    final_pred = final_model.predict(X_val)
    final_score = np.sqrt(mean_squared_error(y_val, final_pred))
    
    print(f"\nFinal best iteration: {final_model.best_iteration}")
    print(f"Final RMSE: {final_score:.4f}")
    
    # Combine all best parameters
    all_best_params = {
        **best_params,
        **reg_best_params,
        **sample_best_params,
        'learning_rate': 0.01,
        'n_estimators': final_model.best_iteration
    }
    
    return final_model, all_best_params

# Example usage
X_val = np.random.randn(200, 20)
y_val = 3*X_val[:,0] + 2*X_val[:,1] - X_val[:,2] + np.random.randn(200)*0.5

# Run sequential tuning
best_model, best_params = sequential_tuning_xgboost(X_train, y_train, X_val, y_val)

print("\n" + "="*60)
print("FINAL BEST PARAMETERS:")
print("="*60)
for param, value in best_params.items():
    print(f"{param}: {value}")



# =============================================================================
# CHAPTER 9: REAL-WORLD IMPLEMENTATION
# =============================================================================

# -----------------------------------------------------------------------------
# 9.1 COMPLETE END-TO-END PROJECT: CUSTOMER CHURN PREDICTION
# -----------------------------------------------------------------------------

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split, StratifiedKFold
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, f1_score,
    roc_auc_score, confusion_matrix, classification_report,
    roc_curve, precision_recall_curve
)
import xgboost as xgb
import lightgbm as lgb
from catboost import CatBoostClassifier, Pool
import warnings
warnings.filterwarnings('ignore')

# Create synthetic customer churn dataset
np.random.seed(42)

def create_churn_dataset(n_samples=10000):
    """Create realistic customer churn dataset"""
    
    data = pd.DataFrame({
        # Demographics
        'age': np.random.randint(18, 80, n_samples),
        'gender': np.random.choice(['Male', 'Female'], n_samples),
        
        # Account information
        'tenure_months': np.random.randint(1, 72, n_samples),
        'contract_type': np.random.choice(['Month-to-Month', 'One Year', 'Two Year'], 
                                         n_samples, p=[0.5, 0.3, 0.2]),
        'payment_method': np.random.choice(['Credit Card', 'Bank Transfer', 
                                           'Electronic Check', 'Mailed Check'], n_samples),
        
        # Services
        'internet_service': np.random.choice(['DSL', 'Fiber Optic', 'No'], 
                                            n_samples, p=[0.4, 0.4, 0.2]),
        'online_security': np.random.choice(['Yes', 'No', 'No Internet'], n_samples),
        'tech_support': np.random.choice(['Yes', 'No', 'No Internet'], n_samples),
        'streaming_tv': np.random.choice(['Yes', 'No', 'No Internet'], n_samples),
        
        # Billing
        'monthly_charges': np.random.uniform(20, 120, n_samples),
        'total_charges': 0,  # Will calculate
        
        # Customer behavior
        'num_support_calls': np.random.poisson(2, n_samples),
        'late_payments': np.random.poisson(1, n_samples),
        'avg_call_duration': np.random.uniform(5, 30, n_samples),
        
        # Customer satisfaction (hidden feature - we'll use for target)
        'satisfaction_score': np.random.uniform(1, 10, n_samples)
    })
    
    # Calculate total charges
    data['total_charges'] = data['monthly_charges'] * data['tenure_months']
    
    # Create target based on logical rules
    churn_probability = (
        0.3 +  # Base churn rate
        (data['contract_type'] == 'Month-to-Month') * 0.3 +
        (data['tenure_months'] < 12) * 0.2 +
        (data['num_support_calls'] > 3) * 0.15 +
        (data['late_payments'] > 2) * 0.15 +
        (data['monthly_charges'] > 90) * 0.1 +
        (data['satisfaction_score'] < 5) * 0.2 -
        (data['contract_type'] == 'Two Year') * 0.3 -
        (data['tenure_months'] > 36) * 0.2
    )
    
    # Clip to [0, 1] and convert to binary
    churn_probability = np.clip(churn_probability, 0, 1)
    data['churn'] = (np.random.random(n_samples) < churn_probability).astype(int)
    
    # Remove satisfaction score (hidden feature)
    data = data.drop('satisfaction_score', axis=1)
    
    return data

# Create dataset
df = create_churn_dataset(10000)

print("="*60)
print("CUSTOMER CHURN PREDICTION - END-TO-END PROJECT")
print("="*60)

print("\nDataset shape:", df.shape)
print("\nFirst few rows:")
print(df.head())

print("\nTarget distribution:")
print(df['churn'].value_counts(normalize=True))

print("\nMissing values:")
print(df.isnull().sum())

# -----------------------------------------------------------------------------
# STEP 1: EXPLORATORY DATA ANALYSIS (EDA)
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 1: EXPLORATORY DATA ANALYSIS")
print("="*60)

# Numerical features analysis
numerical_cols = df.select_dtypes(include=[np.number]).columns.tolist()
numerical_cols.remove('churn')

print("\nNumerical features statistics:")
print(df[numerical_cols].describe())

# Categorical features analysis
categorical_cols = df.select_dtypes(include=['object']).columns.tolist()

print("\nCategorical features:")
for col in categorical_cols:
    print(f"\n{col}:")
    print(df[col].value_counts())

# Churn rate by categorical features
fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.ravel()

for idx, col in enumerate(categorical_cols[:6]):
    churn_rate = df.groupby(col)['churn'].mean().sort_values()
    churn_rate.plot(kind='bar', ax=axes[idx], color='steelblue')
    axes[idx].set_title(f'Churn Rate by {col}')
    axes[idx].set_ylabel('Churn Rate')
    axes[idx].axhline(y=df['churn'].mean(), color='r', linestyle='--', 
                     label='Overall Churn Rate')
    axes[idx].legend()
    axes[idx].grid(axis='y', alpha=0.3)

plt.tight_layout()
plt.savefig('churn_analysis_categorical.png', dpi=300, bbox_inches='tight')
plt.show()

# Correlation analysis
correlation_matrix = df[numerical_cols + ['churn']].corr()

plt.figure(figsize=(12, 10))
sns.heatmap(correlation_matrix, annot=True, fmt='.2f', cmap='coolwarm', 
            center=0, square=True, linewidths=1)
plt.title('Feature Correlation Matrix')
plt.tight_layout()
plt.savefig('churn_correlation.png', dpi=300, bbox_inches='tight')
plt.show()

# Distribution plots
fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.ravel()

for idx, col in enumerate(numerical_cols[:6]):
    for churn_val in [0, 1]:
        df[df['churn'] == churn_val][col].hist(
            bins=30, alpha=0.5, ax=axes[idx],
            label=f'Churn={churn_val}'
        )
    axes[idx].set_title(f'Distribution of {col}')
    axes[idx].legend()
    axes[idx].grid(axis='y', alpha=0.3)

plt.tight_layout()
plt.savefig('churn_distributions.png', dpi=300, bbox_inches='tight')
plt.show()

# -----------------------------------------------------------------------------
# STEP 2: FEATURE ENGINEERING
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 2: FEATURE ENGINEERING")
print("="*60)

def engineer_features(df):
    """Create new features from existing ones"""
    
    df = df.copy()
    
    # Tenure-based features
    df['tenure_years'] = df['tenure_months'] / 12
    df['tenure_group'] = pd.cut(
        df['tenure_months'],
        bins=[0, 12, 24, 48, 72],
        labels=['0-1yr', '1-2yr', '2-4yr', '4+yr']
    )
    
    # Billing features
    df['avg_monthly_charge'] = df['total_charges'] / (df['tenure_months'] + 1)
    df['charge_per_service'] = df['monthly_charges'] / (
        (df['internet_service'] != 'No').astype(int) +
        (df['online_security'] == 'Yes').astype(int) +
        (df['tech_support'] == 'Yes').astype(int) +
        (df['streaming_tv'] == 'Yes').astype(int) + 1
    )
    
    # Service usage features
    df['has_internet'] = (df['internet_service'] != 'No').astype(int)
    df['num_services'] = (
        (df['online_security'] == 'Yes').astype(int) +
        (df['tech_support'] == 'Yes').astype(int) +
        (df['streaming_tv'] == 'Yes').astype(int)
    )
    
    # Customer engagement
    df['support_intensity'] = df['num_support_calls'] / (df['tenure_months'] + 1)
    df['payment_issues'] = (df['late_payments'] > 1).astype(int)
    
    # Contract features
    df['is_month_to_month'] = (df['contract_type'] == 'Month-to-Month').astype(int)
    df['is_long_term'] = (df['contract_type'] == 'Two Year').astype(int)
    
    # Age groups
    df['age_group'] = pd.cut(
        df['age'],
        bins=[0, 30, 45, 60, 100],
        labels=['Young', 'Middle', 'Senior', 'Elderly']
    )
    
    # Risk indicators
    df['high_risk'] = (
        (df['is_month_to_month'] == 1) &
        (df['tenure_months'] < 12) &
        (df['num_support_calls'] > 2)
    ).astype(int)
    
    # Interaction features
    df['tenure_x_charges'] = df['tenure_months'] * df['monthly_charges']
    df['age_x_tenure'] = df['age'] * df['tenure_months']
    
    print(f"Created {len(df.columns) - len(create_churn_dataset(10).columns)} new features")
    
    return df

# Apply feature engineering
df_engineered = engineer_features(df)

print("\nNew features created:")
new_cols = set(df_engineered.columns) - set(df.columns)
for col in new_cols:
    print(f"  - {col}")

# -----------------------------------------------------------------------------
# STEP 3: DATA PREPROCESSING
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 3: DATA PREPROCESSING")
print("="*60)

def preprocess_data(df, target_col='churn'):
    """Preprocess data for modeling"""
    
    df = df.copy()
    
    # Separate features and target
    X = df.drop(target_col, axis=1)
    y = df[target_col]
    
    # Identify feature types
    categorical_features = X.select_dtypes(include=['object', 'category']).columns.tolist()
    numerical_features = X.select_dtypes(include=[np.number]).columns.tolist()
    
    print(f"\nCategorical features ({len(categorical_features)}): {categorical_features}")
    print(f"Numerical features ({len(numerical_features)}): {numerical_features}")
    
    # Handle categorical features
    # For XGBoost/LightGBM: Label encode
    X_encoded = X.copy()
    label_encoders = {}
    
    for col in categorical_features:
        le = LabelEncoder()
        X_encoded[col] = le.fit_transform(X[col].astype(str))
        label_encoders[col] = le
    
    # For CatBoost: Keep original (it handles categories natively)
    X_cat = X.copy()
    
    # Split data
    X_train_enc, X_test_enc, y_train, y_test = train_test_split(
        X_encoded, y, test_size=0.2, random_state=42, stratify=y
    )
    
    X_train_cat, X_test_cat, _, _ = train_test_split(
        X_cat, y, test_size=0.2, random_state=42, stratify=y
    )
    
    print(f"\nTrain set size: {len(X_train_enc)}")
    print(f"Test set size: {len(X_test_enc)}")
    print(f"Train churn rate: {y_train.mean():.2%}")
    print(f"Test churn rate: {y_test.mean():.2%}")
    
    return {
        'X_train_enc': X_train_enc,
        'X_test_enc': X_test_enc,
        'X_train_cat': X_train_cat,
        'X_test_cat': X_test_cat,
        'y_train': y_train,
        'y_test': y_test,
        'categorical_features': categorical_features,
        'numerical_features': numerical_features,
        'label_encoders': label_encoders
    }

# Preprocess data
data_dict = preprocess_data(df_engineered)

# -----------------------------------------------------------------------------
# STEP 4: MODEL TRAINING & COMPARISON
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 4: MODEL TRAINING & COMPARISON")
print("="*60)

def train_and_evaluate_models(data_dict):
    """Train XGBoost, LightGBM, and CatBoost models"""
    
    X_train_enc = data_dict['X_train_enc']
    X_test_enc = data_dict['X_test_enc']
    X_train_cat = data_dict['X_train_cat']
    X_test_cat = data_dict['X_test_cat']
    y_train = data_dict['y_train']
    y_test = data_dict['y_test']
    cat_features = data_dict['categorical_features']
    
    models = {}
    results = []
    
    # Calculate class weights for imbalanced data
    scale_pos_weight = len(y_train[y_train==0]) / len(y_train[y_train==1])
    
    # -------------------------------------------------------------------------
    # XGBoost
    # -------------------------------------------------------------------------
    print("\n" + "-"*60)
    print("Training XGBoost...")
    print("-"*60)
    
    xgb_model = xgb.XGBClassifier(
        n_estimators=1000,
        max_depth=6,
        learning_rate=0.05,
        min_child_weight=3,
        gamma=0.1,
        subsample=0.8,
        colsample_bytree=0.8,
        reg_alpha=0.1,
        reg_lambda=1,
        scale_pos_weight=scale_pos_weight,
        random_state=42,
        n_jobs=-1,
        eval_metric='auc'
    )
    
    xgb_model.fit(
        X_train_enc, y_train,
        eval_set=[(X_train_enc, y_train), (X_test_enc, y_test)],
        early_stopping_rounds=50,
        verbose=100
    )
    
    # Predictions
    xgb_pred_proba = xgb_model.predict_proba(X_test_enc)[:, 1]
    xgb_pred = (xgb_pred_proba >= 0.5).astype(int)
    
    # Metrics
    xgb_results = {
        'Model': 'XGBoost',
        'Accuracy': accuracy_score(y_test, xgb_pred),
        'Precision': precision_score(y_test, xgb_pred),
        'Recall': recall_score(y_test, xgb_pred),
        'F1-Score': f1_score(y_test, xgb_pred),
        'ROC-AUC': roc_auc_score(y_test, xgb_pred_proba),
        'Best Iteration': xgb_model.best_iteration
    }
    
    results.append(xgb_results)
    models['xgboost'] = {
        'model': xgb_model,
        'predictions': xgb_pred,
        'probabilities': xgb_pred_proba
    }
    
    print("\nXGBoost Results:")
    for metric, value in xgb_results.items():
        if metric != 'Model':
            print(f"  {metric}: {value:.4f}" if isinstance(value, float) else f"  {metric}: {value}")
    
    # -------------------------------------------------------------------------
    # LightGBM
    # -------------------------------------------------------------------------
    print("\n" + "-"*60)
    print("Training LightGBM...")
    print("-"*60)
    
    lgb_model = lgb.LGBMClassifier(
        n_estimators=1000,
        num_leaves=31,
        max_depth=6,
        learning_rate=0.05,
        min_child_samples=20,
        subsample=0.8,
        colsample_bytree=0.8,
        reg_alpha=0.1,
        reg_lambda=1,
        scale_pos_weight=scale_pos_weight,
        random_state=42,
        n_jobs=-1
    )
    
    lgb_model.fit(
        X_train_enc, y_train,
        eval_set=[(X_train_enc, y_train), (X_test_enc, y_test)],
        eval_metric='auc',
        callbacks=[
            lgb.early_stopping(stopping_rounds=50),
            lgb.log_evaluation(period=100)
        ]
    )
    
    # Predictions
    lgb_pred_proba = lgb_model.predict_proba(X_test_enc)[:, 1]
    lgb_pred = (lgb_pred_proba >= 0.5).astype(int)
    
    # Metrics
    lgb_results = {
        'Model': 'LightGBM',
        'Accuracy': accuracy_score(y_test, lgb_pred),
        'Precision': precision_score(y_test, lgb_pred),
        'Recall': recall_score(y_test, lgb_pred),
        'F1-Score': f1_score(y_test, lgb_pred),
        'ROC-AUC': roc_auc_score(y_test, lgb_pred_proba),
        'Best Iteration': lgb_model.best_iteration_
    }
    
    results.append(lgb_results)
    models['lightgbm'] = {
        'model': lgb_model,
        'predictions': lgb_pred,
        'probabilities': lgb_pred_proba
    }
    
    print("\nLightGBM Results:")
    for metric, value in lgb_results.items():
        if metric != 'Model':
            print(f"  {metric}: {value:.4f}" if isinstance(value, float) else f"  {metric}: {value}")
    
    # -------------------------------------------------------------------------
    # CatBoost
    # -------------------------------------------------------------------------
    print("\n" + "-"*60)
    print("Training CatBoost...")
    print("-"*60)
    
    # Get categorical feature indices
    cat_feature_indices = [X_train_cat.columns.get_loc(col) for col in cat_features]
    
    cat_model = CatBoostClassifier(
        iterations=1000,
        depth=6,
        learning_rate=0.05,
        l2_leaf_reg=3,
        border_count=128,
        auto_class_weights='Balanced',
        cat_features=cat_feature_indices,
        random_seed=42,
        verbose=100,
        early_stopping_rounds=50
    )
    
    cat_model.fit(
        X_train_cat, y_train,
        eval_set=(X_test_cat, y_test),
        use_best_model=True
    )
    
    # Predictions
    cat_pred_proba = cat_model.predict_proba(X_test_cat)[:, 1]
    cat_pred = (cat_pred_proba >= 0.5).astype(int)
    
    # Metrics
    cat_results = {
        'Model': 'CatBoost',
        'Accuracy': accuracy_score(y_test, cat_pred),
        'Precision': precision_score(y_test, cat_pred),
        'Recall': recall_score(y_test, cat_pred),
        'F1-Score': f1_score(y_test, cat_pred),
        'ROC-AUC': roc_auc_score(y_test, cat_pred_proba),
        'Best Iteration': cat_model.best_iteration_
    }
    
    results.append(cat_results)
    models['catboost'] = {
        'model': cat_model,
        'predictions': cat_pred,
        'probabilities': cat_pred_proba
    }
    
    print("\nCatBoost Results:")
    for metric, value in cat_results.items():
        if metric != 'Model':
            print(f"  {metric}: {value:.4f}" if isinstance(value, float) else f"  {metric}: {value}")
    
    # -------------------------------------------------------------------------
    # Comparison Summary
    # -------------------------------------------------------------------------
    print("\n" + "="*60)
    print("MODEL COMPARISON SUMMARY")
    print("="*60)
    
    results_df = pd.DataFrame(results)
    print("\n", results_df.to_string(index=False))
    
    # Identify best model
    best_model_name = results_df.loc[results_df['ROC-AUC'].idxmax(), 'Model']
    print(f"\n🏆 Best Model (by ROC-AUC): {best_model_name}")
    
    return models, results_df

# Train models
models, results_df = train_and_evaluate_models(data_dict)

# -----------------------------------------------------------------------------
# STEP 5: MODEL EVALUATION & VISUALIZATION
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 5: DETAILED MODEL EVALUATION")
print("="*60)

def detailed_evaluation(models, y_test, data_dict):
    """Comprehensive model evaluation with visualizations"""
    
    X_test_enc = data_dict['X_test_enc']
    X_test_cat = data_dict['X_test_cat']
    
    fig, axes = plt.subplots(2, 3, figsize=(18, 12))
    
    colors = {'xgboost': 'blue', 'lightgbm': 'green', 'catboost': 'red'}
    
    # -------------------------------------------------------------------------
    # 1. ROC Curves
    # -------------------------------------------------------------------------
    ax = axes[0, 0]
    
    for model_name, model_dict in models.items():
        y_pred_proba = model_dict['probabilities']
        fpr, tpr, _ = roc_curve(y_test, y_pred_proba)
        auc = roc_auc_score(y_test, y_pred_proba)
        
        ax.plot(fpr, tpr, label=f'{model_name.upper()} (AUC={auc:.3f})',
                color=colors[model_name], linewidth=2)
    
    ax.plot([0, 1], [0, 1], 'k--', linewidth=1, label='Random')
    ax.set_xlabel('False Positive Rate')
    ax.set_ylabel('True Positive Rate')
    ax.set_title('ROC Curves Comparison')
    ax.legend()
    ax.grid(alpha=0.3)
    
    # -------------------------------------------------------------------------
    # 2. Precision-Recall Curves
    # -------------------------------------------------------------------------
    ax = axes[0, 1]
    
    for model_name, model_dict in models.items():
        y_pred_proba = model_dict['probabilities']
        precision, recall, _ = precision_recall_curve(y_test, y_pred_proba)
        
        ax.plot(recall, precision, label=model_name.upper(),
                color=colors[model_name], linewidth=2)
    
    ax.set_xlabel('Recall')
    ax.set_ylabel('Precision')
    ax.set_title('Precision-Recall Curves')
    ax.legend()
    ax.grid(alpha=0.3)
    
    # -------------------------------------------------------------------------
    # 3. Confusion Matrices
    # -------------------------------------------------------------------------
    ax = axes[0, 2]
    ax.axis('off')
    
    # Create separate figure for confusion matrices
    fig_cm, axes_cm = plt.subplots(1, 3, figsize=(15, 4))
    
    for idx, (model_name, model_dict) in enumerate(models.items()):
        y_pred = model_dict['predictions']
        cm = confusion_matrix(y_test, y_pred)
        
        sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
                   ax=axes_cm[idx], cbar=False)
        axes_cm[idx].set_title(f'{model_name.upper()} Confusion Matrix')
        axes_cm[idx].set_xlabel('Predicted')
        axes_cm[idx].set_ylabel('Actual')
    
    plt.tight_layout()
    plt.savefig('confusion_matrices.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    # -------------------------------------------------------------------------
    # 4. Feature Importance Comparison
    # -------------------------------------------------------------------------
    ax = axes[1, 0]
    
    # Get top 10 features from each model
    xgb_importance = pd.Series(
        models['xgboost']['model'].feature_importances_,
        index=X_test_enc.columns
    ).nlargest(10)
    
    lgb_importance = pd.Series(
        models['lightgbm']['model'].feature_importances_,
        index=X_test_enc.columns
    ).nlargest(10)
    
    cat_importance = pd.Series(
        models['catboost']['model'].feature_importances_,
        index=X_test_cat.columns
    ).nlargest(10)
    
    # Plot XGBoost importance (as example)
    xgb_importance.sort_values().plot(kind='barh', ax=ax, color='steelblue')
    ax.set_title('Feature Importance (XGBoost)')
    ax.set_xlabel('Importance')
    ax.grid(axis='x', alpha=0.3)
    
    # -------------------------------------------------------------------------
    # 5. Prediction Distribution
    # -------------------------------------------------------------------------
    ax = axes[1, 1]
    
    for model_name, model_dict in models.items():
        y_pred_proba = model_dict['probabilities']
        ax.hist(y_pred_proba[y_test==0], bins=50, alpha=0.3,
               label=f'{model_name} (No Churn)', color=colors[model_name])
        ax.hist(y_pred_proba[y_test==1], bins=50, alpha=0.3,
               label=f'{model_name} (Churn)', color=colors[model_name],
               edgecolor='black')
    
    ax.set_xlabel('Predicted Probability')
    ax.set_ylabel('Frequency')
    ax.set_title('Prediction Distribution by True Label')
    ax.legend()
    ax.grid(axis='y', alpha=0.3)
    
    # -------------------------------------------------------------------------
    # 6. Metrics Comparison Bar Chart
    # -------------------------------------------------------------------------
    ax = axes[1, 2]
    
    metrics_data = []
    for model_name, model_dict in models.items():
        y_pred = model_dict['predictions']
        y_pred_proba = model_dict['probabilities']
        
        metrics_data.append({
            'Model': model_name.upper(),
            'Accuracy': accuracy_score(y_test, y_pred),
            'Precision': precision_score(y_test, y_pred),
            'Recall': recall_score(y_test, y_pred),
            'F1': f1_score(y_test, y_pred),
            'AUC': roc_auc_score(y_test, y_pred_proba)
        })
    
    metrics_df = pd.DataFrame(metrics_data).set_index('Model')
    metrics_df.plot(kind='bar', ax=ax, width=0.8)
    ax.set_title('Performance Metrics Comparison')
    ax.set_ylabel('Score')
    ax.set_ylim(0, 1)
    ax.legend(loc='lower right')
    ax.grid(axis='y', alpha=0.3)
    plt.setp(ax.xaxis.get_majorticklabels(), rotation=0)
    
    plt.tight_layout()
    plt.savefig('model_evaluation_complete.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    # -------------------------------------------------------------------------
    # Detailed Classification Reports
    # -------------------------------------------------------------------------
    print("\n" + "="*60)
    print("DETAILED CLASSIFICATION REPORTS")
    print("="*60)
    
    for model_name, model_dict in models.items():
        print(f"\n{model_name.upper()}:")
        print("-" * 60)
        print(classification_report(
            y_test,
            model_dict['predictions'],
            target_names=['No Churn', 'Churn']
        ))
    
    # -------------------------------------------------------------------------
    # Business Metrics
    # -------------------------------------------------------------------------
    print("\n" + "="*60)
    print("BUSINESS IMPACT ANALYSIS")
    print("="*60)
    
    # Assume business costs
    cost_false_positive = 50  # Cost of unnecessary retention effort
    cost_false_negative = 500  # Cost of losing a customer
    revenue_per_customer = 100  # Monthly revenue
    
    for model_name, model_dict in models.items():
        y_pred = model_dict['predictions']
        cm = confusion_matrix(y_test, y_pred)
        
        tn, fp, fn, tp = cm.ravel()
        
        # Calculate costs
        total_cost = (fp * cost_false_positive) + (fn * cost_false_negative)
        customers_saved = tp
        revenue_saved = customers_saved * revenue_per_customer * 12  # Annual
        net_benefit = revenue_saved - total_cost
        
        print(f"\n{model_name.upper()}:")
        print(f"  True Negatives: {tn}")
        print(f"  False Positives: {fp} (Cost: ${fp * cost_false_positive:,.0f})")
        print(f"  False Negatives: {fn} (Cost: ${fn * cost_false_negative:,.0f})")
        print(f"  True Positives: {tp} (Customers Saved)")
        print(f"  Total Cost: ${total_cost:,.0f}")
        print(f"  Revenue Saved: ${revenue_saved:,.0f}")
        print(f"  Net Benefit: ${net_benefit:,.0f}")

# Run detailed evaluation
detailed_evaluation(models, data_dict['y_test'], data_dict)

# -----------------------------------------------------------------------------
# STEP 6: THRESHOLD OPTIMIZATION
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 6: THRESHOLD OPTIMIZATION")
print("="*60)

def optimize_threshold(y_true, y_pred_proba, metric='f1'):
    """Find optimal classification threshold"""
    
    thresholds = np.arange(0.1, 0.9, 0.01)
    scores = []
    
    for threshold in thresholds:
        y_pred = (y_pred_proba >= threshold).astype(int)
        
        if metric == 'f1':
            score = f1_score(y_true, y_pred)
        elif metric == 'precision':
            score = precision_score(y_true, y_pred)
        elif metric == 'recall':
            score = recall_score(y_true, y_pred)
        elif metric == 'accuracy':
            score = accuracy_score(y_true, y_pred)
        
        scores.append(score)
    
    optimal_idx = np.argmax(scores)
    optimal_threshold = thresholds[optimal_idx]
    optimal_score = scores[optimal_idx]
    
    return optimal_threshold, optimal_score, thresholds, scores

# Optimize for each model
fig, axes = plt.subplots(1, 3, figsize=(18, 5))

y_test = data_dict['y_test']

for idx, (model_name, model_dict) in enumerate(models.items()):
    y_pred_proba = model_dict['probabilities']
    
    # Optimize for different metrics
    metrics = ['f1', 'precision', 'recall']
    
    for metric in metrics:
        optimal_threshold, optimal_score, thresholds, scores = optimize_threshold(
            y_test, y_pred_proba, metric=metric
        )
        
        axes[idx].plot(thresholds, scores, label=f'{metric.upper()}', linewidth=2)
        axes[idx].axvline(x=optimal_threshold, color='red', linestyle='--',
                         alpha=0.5, label=f'Optimal {metric}={optimal_threshold:.2f}')
    
    axes[idx].set_xlabel('Threshold')
    axes[idx].set_ylabel('Score')
    axes[idx].set_title(f'{model_name.upper()} - Threshold Optimization')
    axes[idx].legend()
    axes[idx].grid(alpha=0.3)

plt.tight_layout()
plt.savefig('threshold_optimization.png', dpi=300, bbox_inches='tight')
plt.show()

# Print optimal thresholds
print("\nOptimal Thresholds (for F1-Score):")
for model_name, model_dict in models.items():
    y_pred_proba = model_dict['probabilities']
    optimal_threshold, optimal_score, _, _ = optimize_threshold(
        y_test, y_pred_proba, metric='f1'
    )
    print(f"  {model_name.upper()}: {optimal_threshold:.3f} (F1={optimal_score:.4f})")

# -----------------------------------------------------------------------------
# STEP 7: FEATURE IMPORTANCE ANALYSIS
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 7: FEATURE IMPORTANCE ANALYSIS")
print("="*60)

def analyze_feature_importance(models, data_dict):
    """Detailed feature importance analysis"""
    
    X_train_enc = data_dict['X_train_enc']
    X_test_enc = data_dict['X_test_enc']
    X_test_cat = data_dict['X_test_cat']
    
    # Get feature importance from all models
    importance_dict = {}
    
    # XGBoost
    importance_dict['XGBoost'] = pd.Series(
        models['xgboost']['model'].feature_importances_,
        index=X_train_enc.columns
    )
    
    # LightGBM
    importance_dict['LightGBM'] = pd.Series(
        models['lightgbm']['model'].feature_importances_,
        index=X_train_enc.columns
    )
    
    # CatBoost
    importance_dict['CatBoost'] = pd.Series(
        models['catboost']['model'].feature_importances_,
        index=X_test_cat.columns
    )
    
    # Combine and normalize
    importance_df = pd.DataFrame(importance_dict)
    
    # Normalize to sum to 1
    importance_df = importance_df.div(importance_df.sum(axis=0), axis=1)
    
    # Get top features (average across models)
    importance_df['Average'] = importance_df.mean(axis=1)
    top_features = importance_df.nlargest(15, 'Average')
    
    # Plot
    fig, axes = plt.subplots(2, 2, figsize=(16, 12))
    
    # Individual model importances
    for idx, model_name in enumerate(['XGBoost', 'LightGBM', 'CatBoost']):
        ax = axes[idx // 2, idx % 2]
        importance_df[model_name].nlargest(15).sort_values().plot(
            kind='barh', ax=ax, color='steelblue'
        )
        ax.set_title(f'Top 15 Features - {model_name}')
        ax.set_xlabel('Importance')
        ax.grid(axis='x', alpha=0.3)
    
    # Average importance
    ax = axes[1, 1]
    top_features['Average'].sort_values().plot(kind='barh', ax=ax, color='coral')
    ax.set_title('Top 15 Features - Average Across Models')
    ax.set_xlabel('Average Importance')
    ax.grid(axis='x', alpha=0.3)
    
    plt.tight_layout()
    plt.savefig('feature_importance_comparison.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    # Print detailed importance
    print("\nTop 20 Features (Average Importance):")
    print(importance_df.nlargest(20, 'Average')[['Average', 'XGBoost', 'LightGBM', 'CatBoost']].to_string())
    
    # Feature agreement analysis
    print("\n" + "="*60)
    print("FEATURE IMPORTANCE AGREEMENT")
    print("="*60)
    
    # Calculate correlation of feature importances between models
    correlation = importance_df[['XGBoost', 'LightGBM', 'CatBoost']].corr()
    
    print("\nCorrelation of Feature Importances:")
    print(correlation.to_string())
    
    plt.figure(figsize=(8, 6))
    sns.heatmap(correlation, annot=True, fmt='.3f', cmap='coolwarm',
                center=0, square=True, linewidths=1)
    plt.title('Feature Importance Correlation Between Models')
    plt.tight_layout()
    plt.savefig('importance_correlation.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    return importance_df

# Analyze feature importance
importance_df = analyze_feature_importance(models, data_dict)

# -----------------------------------------------------------------------------
# STEP 8: PARTIAL DEPENDENCE PLOTS
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 8: PARTIAL DEPENDENCE ANALYSIS")
print("="*60)

from sklearn.inspection import partial_dependence, PartialDependenceDisplay

def plot_partial_dependence(model, X, features, model_name='Model'):
    """Plot partial dependence for top features"""
    
    # Select top numerical features
    top_features_idx = [i for i, col in enumerate(X.columns) if col in features]
    
    fig, ax = plt.subplots(figsize=(15, 10))
    
    display = PartialDependenceDisplay.from_estimator(
        model,
        X,
        features=top_features_idx[:6],  # Top 6 features
        feature_names=X.columns.tolist(),
        n_cols=3,
        grid_resolution=50,
        ax=ax
    )
    
    plt.suptitle(f'Partial Dependence Plots - {model_name}', fontsize=16, y=1.02)
    plt.tight_layout()
    plt.savefig(f'pdp_{model_name.lower()}.png', dpi=300, bbox_inches='tight')
    plt.show()

# Get top numerical features
top_numerical_features = [
    col for col in importance_df.nlargest(10, 'Average').index
    if col in data_dict['numerical_features']
]

# Plot for best model (e.g., XGBoost)
plot_partial_dependence(
    models['xgboost']['model'],
    data_dict['X_test_enc'],
    top_numerical_features,
    'XGBoost'
)

# -----------------------------------------------------------------------------
# STEP 9: SHAP VALUE ANALYSIS
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 9: SHAP VALUE ANALYSIS")
print("="*60)

import shap

def shap_analysis(model, X, model_name='Model', sample_size=1000):
    """Comprehensive SHAP value analysis"""
    
    # Sample data for faster computation
    if len(X) > sample_size:
        X_sample = X.sample(sample_size, random_state=42)
    else:
        X_sample = X
    
    # Create SHAP explainer
    explainer = shap.TreeExplainer(model)
    shap_values = explainer.shap_values(X_sample)
    
    # If binary classification, take positive class
    if isinstance(shap_values, list):
        shap_values = shap_values[1]
    
    # Summary plot
    plt.figure(figsize=(12, 8))
    shap.summary_plot(shap_values, X_sample, plot_type="bar", show=False)
    plt.title(f'{model_name} - SHAP Feature Importance')
    plt.tight_layout()
    plt.savefig(f'shap_importance_{model_name.lower()}.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    # Detailed summary plot
    plt.figure(figsize=(12, 8))
    shap.summary_plot(shap_values, X_sample, show=False)
    plt.title(f'{model_name} - SHAP Summary Plot')
    plt.tight_layout()
    plt.savefig(f'shap_summary_{model_name.lower()}.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    # Individual prediction explanation (first churned customer)
    churn_idx = data_dict['y_test'][data_dict['y_test'] == 1].index[0]
    churn_sample_idx = X_sample.index.get_loc(churn_idx) if churn_idx in X_sample.index else 0
    
    plt.figure(figsize=(12, 6))
    shap.waterfall_plot(
        shap.Explanation(
            values=shap_values[churn_sample_idx],
            base_values=explainer.expected_value if not isinstance(explainer.expected_value, list) 
                        else explainer.expected_value[1],
            data=X_sample.iloc[churn_sample_idx],
            feature_names=X_sample.columns.tolist()
        ),
        show=False
    )
    plt.title(f'{model_name} - SHAP Explanation for Churned Customer')
    plt.tight_layout()
    plt.savefig(f'shap_waterfall_{model_name.lower()}.png', dpi=300, bbox_inches='tight')
    plt.show()
    
    return shap_values

# Run SHAP analysis for XGBoost
shap_values_xgb = shap_analysis(
    models['xgboost']['model'],
    data_dict['X_test_enc'],
    'XGBoost',
    sample_size=500
)

# -----------------------------------------------------------------------------
# STEP 10: MODEL SAVING & DEPLOYMENT PREPARATION
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 10: MODEL SAVING & DEPLOYMENT")
print("="*60)

import pickle
import joblib
import json

def save_models_and_artifacts(models, data_dict, importance_df):
    """Save all models and necessary artifacts for deployment"""
    
    # Create deployment directory
    import os
    os.makedirs('deployment', exist_ok=True)
    
    # Save models
    print("Saving models...")
    
    # XGBoost
    models['xgboost']['model'].save_model('deployment/xgboost_model.json')
    print("  ✓ XGBoost saved")
    
    # LightGBM
    models['lightgbm']['model'].booster_.save_model('deployment/lightgbm_model.txt')
    print("  ✓ LightGBM saved")
    
    # CatBoost
    models['catboost']['model'].save_model('deployment/catboost_model.cbm')
    print("  ✓ CatBoost saved")
    
    # Save preprocessing artifacts
    print("\nSaving preprocessing artifacts...")
    
    artifacts = {
        'label_encoders': data_dict['label_encoders'],
        'categorical_features': data_dict['categorical_features'],
        'numerical_features': data_dict['numerical_features'],
        'feature_names': data_dict['X_train_enc'].columns.tolist()
    }
    
    with open('deployment/preprocessing_artifacts.pkl', 'wb') as f:
        pickle.dump(artifacts, f)
    print("  ✓ Preprocessing artifacts saved")
    
    # Save feature importance
    importance_df.to_csv('deployment/feature_importance.csv')
    print("  ✓ Feature importance saved")
    
    # Save model metadata
    metadata = {
        'training_date': pd.Timestamp.now().isoformat(),
        'models': {
            name: {
                'best_iteration': info['model'].best_iteration if hasattr(info['model'], 'best_iteration') 
                                 else info['model'].best_iteration_,
                'n_features': len(data_dict['X_train_enc'].columns)
            }
            for name, info in models.items()
        },
        'performance': results_df.to_dict('records')
    }
    
    with open('deployment/model_metadata.json', 'w') as f:
        json.dump(metadata, f, indent=2)
    print("  ✓ Model metadata saved")
    
    print("\nAll artifacts saved to 'deployment/' directory")

# Save everything
save_models_and_artifacts(models, data_dict, importance_df)

# -----------------------------------------------------------------------------
# STEP 11: CREATE INFERENCE PIPELINE
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 11: INFERENCE PIPELINE")
print("="*60)

class ChurnPredictor:
    """Production-ready churn prediction pipeline"""
    
    def __init__(self, model_path, artifacts_path):
        """Initialize predictor with saved model and artifacts"""
        
        # Load model
        if 'xgboost' in model_path:
            self.model = xgb.XGBClassifier()
            self.model.load_model(model_path)
            self.model_type = 'xgboost'
        elif 'lightgbm' in model_path:
            self.model = lgb.Booster(model_file=model_path)
            self.model_type = 'lightgbm'
        elif 'catboost' in model_path:
            self.model = CatBoostClassifier()
            self.model.load_model(model_path)
            self.model_type = 'catboost'
        
        # Load preprocessing artifacts
        with open(artifacts_path, 'rb') as f:
            self.artifacts = pickle.load(f)
        
        print(f"✓ Loaded {self.model_type} model")
    
    def preprocess(self, df):
        """Preprocess input data"""
        
        df = df.copy()
        
        # Apply feature engineering (same as training)
        df = engineer_features(df)
        
        # Encode categorical features
        if self.model_type != 'catboost':
            for col in self.artifacts['categorical_features']:
                if col in df.columns:
                    le = self.artifacts['label_encoders'][col]
                    df[col] = df[col].apply(
                        lambda x: le.transform([str(x)])[0] 
                        if str(x) in le.classes_ else -1
                    )
        
        # Ensure all features are present
        for feature in self.artifacts['feature_names']:
            if feature not in df.columns:
                df[feature] = 0
        
        # Select and order features
        df = df[self.artifacts['feature_names']]
        
        return df
    
    def predict(self, df, return_proba=True):
        """Make predictions on new data"""
        
        # Preprocess
        X = self.preprocess(df)
        
        # Predict
        if self.model_type == 'lightgbm':
            predictions = self.model.predict(X)
            if return_proba:
                return predictions
            else:
                return (predictions >= 0.5).astype(int)
        else:
            if return_proba:
                return self.model.predict_proba(X)[:, 1]
            else:
                return self.model.predict(X)
    
    def predict_with_explanation(self, df):
        """Predict with feature contributions"""
        
        X = self.preprocess(df)
        
        # Get base prediction
        prediction_proba = self.predict(df, return_proba=True)
        prediction = (prediction_proba >= 0.5).astype(int)
        
        # Get SHAP values for explanation
        explainer = shap.TreeExplainer(self.model)
        shap_values = explainer.shap_values(X)
        
        if isinstance(shap_values, list):
            shap_values = shap_values[1]
        
        # Get top contributing features
        shap_df = pd.DataFrame({
            'feature': X.columns,
            'value': X.iloc[0].values,
            'shap_value': shap_values[0]
        })
        shap_df['abs_shap'] = abs(shap_df['shap_value'])
        top_features = shap_df.nlargest(5, 'abs_shap')
        
        result = {
            'prediction': int(prediction[0]),
            'probability': float(prediction_proba[0]),
            'risk_level': 'High' if prediction_proba[0] > 0.7 else 'Medium' if prediction_proba[0] > 0.4 else 'Low',
            'top_factors': top_features[['feature', 'value', 'shap_value']].to_dict('records')
        }
        
        return result

# Example: Load and use predictor
predictor = ChurnPredictor(
    'deployment/xgboost_model.json',
    'deployment/preprocessing_artifacts.pkl'
)

# Test on sample customer
sample_customer = df.iloc[[0]].drop('churn', axis=1)
result = predictor.predict_with_explanation(sample_customer)

print("\nSample Prediction:")
print(json.dumps(result, indent=2))

# -----------------------------------------------------------------------------
# STEP 12: BATCH PREDICTION EXAMPLE
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 12: BATCH PREDICTION")
print("="*60)

def batch_predict(predictor, data, batch_size=1000):
    """Efficiently predict on large datasets"""
    
    n_samples = len(data)
    n_batches = (n_samples + batch_size - 1) // batch_size
    
    predictions = []
    probabilities = []
    
    for i in range(n_batches):
        start_idx = i * batch_size
        end_idx = min((i + 1) * batch_size, n_samples)
        
        batch = data.iloc[start_idx:end_idx]
        
        # Predict
        proba = predictor.predict(batch, return_proba=True)
        pred = (proba >= 0.5).astype(int)
        
        predictions.extend(pred)
        probabilities.extend(proba)
        
        if (i + 1) % 10 == 0:
            print(f"  Processed {end_idx}/{n_samples} samples...")
    
    return np.array(predictions), np.array(probabilities)

# Test batch prediction
test_data = df.drop('churn', axis=1).head(5000)
batch_pred, batch_proba = batch_predict(predictor, test_data)

print(f"\nBatch predictions completed: {len(batch_pred)} samples")
print(f"Predicted churn rate: {batch_pred.mean():.2%}")

# -----------------------------------------------------------------------------
# STEP 13: MONITORING DASHBOARD DATA
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("STEP 13: MONITORING METRICS")
print("="*60)

def calculate_monitoring_metrics(y_true, y_pred, y_pred_proba):
    """Calculate metrics for production monitoring"""
    
    metrics = {
        'accuracy': accuracy_score(y_true, y_pred),
        'precision': precision_score(y_true, y_pred),
        'recall': recall_score(y_true, y_pred),
        'f1_score': f1_score(y_true, y_pred),
        'roc_auc': roc_auc_score(y_true, y_pred_proba),
        'confusion_matrix': confusion_matrix(y_true, y_pred).tolist(),
        'churn_rate_predicted': float(y_pred.mean()),
        'churn_rate_actual': float(y_true.mean()),
        'average_probability': float(y_pred_proba.mean()),
        'calibration_score': None  # Would need calibration analysis
    }
    
    # Prediction distribution by decile
    deciles = pd.qcut(y_pred_proba, q=10, labels=False, duplicates='drop')
    metrics['decile_analysis'] = []
    
    for decile in range(10):
        mask = deciles == decile
        if mask.sum() > 0:
            metrics['decile_analysis'].append({
                'decile': int(decile + 1),
                'count': int(mask.sum()),
                'avg_probability': float(y_pred_proba[mask].mean()),
                'actual_churn_rate': float(y_true[mask].mean())
            })
    
    return metrics

# Calculate monitoring metrics for test set
monitoring_metrics = calculate_monitoring_metrics(
    data_dict['y_test'],
    models['xgboost']['predictions'],
    models['xgboost']['probabilities']
)

print("\nMonitoring Metrics:")
print(json.dumps({k: v for k, v in monitoring_metrics.items() 
                  if k not in ['confusion_matrix', 'decile_analysis']}, indent=2))

print("\nDecile Analysis:")
for decile_info in monitoring_metrics['decile_analysis']:
    print(f"  Decile {decile_info['decile']}: "
          f"Avg Prob={decile_info['avg_probability']:.3f}, "
          f"Actual Churn={decile_info['actual_churn_rate']:.2%}")

# Save monitoring metrics
with open('deployment/monitoring_metrics.json', 'w') as f:
    json.dump(monitoring_metrics, f, indent=2)

print("\n" + "="*60)
print("PROJECT COMPLETE!")
print("="*60)
print("\nAll artifacts saved in 'deployment/' directory:")
print("  - Models: xgboost_model.json, lightgbm_model.txt, catboost_model.cbm")
print("  - Artifacts: preprocessing_artifacts.pkl")
print("  - Metadata: model_metadata.json")
print("  - Metrics: monitoring_metrics.json, feature_importance.csv")
print("\nReady for production deployment! 🚀")
Chapter 10: Advanced Techniques & Tricks
10.1 Ensemble Methods: Combining Multiple Models
Python

# =============================================================================
# ADVANCED ENSEMBLE TECHNIQUES
# =============================================================================

print("="*60)
print("CHAPTER 10: ADVANCED TECHNIQUES")
print("="*60)

# -----------------------------------------------------------------------------
# TECHNIQUE 1: WEIGHTED AVERAGING
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE 1: Weighted Averaging Ensemble")
print("-"*60)

def weighted_average_ensemble(predictions_dict, weights=None):
    """
    Combine predictions using weighted average
    
    Args:
        predictions_dict: Dict of {model_name: predictions_array}
        weights: Dict of {model_name: weight} or None for equal weights
    """
    
    if weights is None:
        # Equal weights
        weights = {name: 1/len(predictions_dict) for name in predictions_dict.keys()}
    
    # Normalize weights
    total_weight = sum(weights.values())
    weights = {k: v/total_weight for k, v in weights.items()}
    
    # Weighted average
    ensemble_pred = np.zeros_like(list(predictions_dict.values())[0])
    
    for model_name, predictions in predictions_dict.items():
        ensemble_pred += weights[model_name] * predictions
    
    return ensemble_pred

# Get predictions from all models
ensemble_predictions = {
    'xgboost': models['xgboost']['probabilities'],
    'lightgbm': models['lightgbm']['probabilities'],
    'catboost': models['catboost']['probabilities']
}

# Equal weight ensemble
equal_ensemble = weighted_average_ensemble(ensemble_predictions)

# Performance-based weights (based on ROC-AUC)
performance_weights = {
    'xgboost': results_df[results_df['Model'] == 'XGBoost']['ROC-AUC'].values[0],
    'lightgbm': results_df[results_df['Model'] == 'LightGBM']['ROC-AUC'].values[0],
    'catboost': results_df[results_df['Model'] == 'CatBoost']['ROC-AUC'].values[0]
}

weighted_ensemble = weighted_average_ensemble(ensemble_predictions, performance_weights)

# Evaluate
y_test = data_dict['y_test']

equal_auc = roc_auc_score(y_test, equal_ensemble)
weighted_auc = roc_auc_score(y_test, weighted_ensemble)

print(f"\nEqual Weight Ensemble AUC: {equal_auc:.4f}")
print(f"Performance-Weighted Ensemble AUC: {weighted_auc:.4f}")

# Compare with individual models
print("\nIndividual Model AUCs:")
for name, preds in ensemble_predictions.items():
    auc = roc_auc_score(y_test, preds)
    print(f"  {name.upper()}: {auc:.4f}")

# -----------------------------------------------------------------------------
# TECHNIQUE 2: STACKING (Meta-Model)
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE 2: Stacking Ensemble")
print("-"*60)

from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import cross_val_predict

def create_stacking_ensemble(models_dict, X_train, X_test, y_train, meta_model=None):
    """
    Create stacking ensemble with meta-model
    
    Returns predictions from meta-model trained on base model predictions
    """
    
    if meta_model is None:
        meta_model = LogisticRegression(random_state=42, max_iter=1000)
    
    # Generate out-of-fold predictions for training
    train_meta_features = []
    test_meta_features = []
    
    for model_name, model_info in models_dict.items():
        model = model_info['model']
        
        # Out-of-fold predictions for training set
        if model_name == 'catboost':
            X_train_use = data_dict['X_train_cat']
            X_test_use = data_dict['X_test_cat']
        else:
            X_train_use = data_dict['X_train_enc']
            X_test_use = data_dict['X_test_enc']
        
        # Cross-val predictions for train
        oof_preds = cross_val_predict(
            model, X_train_use, y_train,
            cv=5, method='predict_proba', n_jobs=-1
        )[:, 1]
        
        # Direct predictions for test
        test_preds = model.predict_proba(X_test_use)[:, 1]
        
        train_meta_features.append(oof_preds)
        test_meta_features.append(test_preds)
    
    # Stack features
    X_train_meta = np.column_stack(train_meta_features)
    X_test_meta = np.column_stack(test_meta_features)
    
    # Train meta-model
    meta_model.fit(X_train_meta, y_train)
    
    # Predict
    stacked_predictions = meta_model.predict_proba(X_test_meta)[:, 1]
    
    return stacked_predictions, meta_model

# Create stacking ensemble
stacked_pred, meta_model = create_stacking_ensemble(
    models,
    data_dict['X_train_enc'],
    data_dict['X_test_enc'],
    data_dict['y_train']
)

stacked_auc = roc_auc_score(y_test, stacked_pred)
print(f"\nStacking Ensemble AUC: {stacked_auc:.4f}")

# Meta-model coefficients
print("\nMeta-model coefficients:")
for idx, model_name in enumerate(models.keys()):
    print(f"  {model_name.upper()}: {meta_model.coef_[0][idx]:.4f}")

# -----------------------------------------------------------------------------
# TECHNIQUE 3: BLENDING
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE 3: Blending Ensemble")
print("-"*60)

def create_blending_ensemble(models_dict, X_train, X_val, X_test, 
                             y_train, y_val, blend_model=None):
    """
    Blending: Train base models on train, blend on validation
    """
    
    if blend_model is None:
        blend_model = LogisticRegression(random_state=42, max_iter=1000)
    
    val_meta_features = []
    test_meta_features = []
    
    for model_name, model_info in models_dict.items():
        model = model_info['model']
        
        # Get predictions on validation and test
        if model_name == 'catboost':
            val_preds = model.predict_proba(data_dict['X_test_cat'])[:, 1]
            test_preds = model.predict_proba(data_dict['X_test_cat'])[:, 1]
        else:
            val_preds = model.predict_proba(data_dict['X_test_enc'])[:, 1]
            test_preds = model.predict_proba(data_dict['X_test_enc'])[:, 1]
        
        val_meta_features.append(val_preds)
        test_meta_features.append(test_preds)
    
    # Stack
    X_val_meta = np.column_stack(val_meta_features)
    X_test_meta = np.column_stack(test_meta_features)
    
    # Train blend model on validation predictions
    blend_model.fit(X_val_meta, y_val)
    
    # Predict on test
    blended_predictions = blend_model.predict_proba(X_test_meta)[:, 1]
    
    return blended_predictions, blend_model

# Note: For blending we'd need a separate validation set
# Here we'll use test set as "validation" just for demonstration
blended_pred, blend_model = create_blending_ensemble(
    models,
    data_dict['X_train_enc'],
    data_dict['X_test_enc'],
    data_dict['X_test_enc'],
    data_dict['y_train'],
    y_test
)

# This is overfitting since we used test as validation!
# In practice, split train into train/val
print("\nBlending example created (Note: requires proper train/val/test split)")

# -----------------------------------------------------------------------------
# TECHNIQUE 4: RANK AVERAGING
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE 4: Rank Averaging")
print("-"*60)

def rank_average_ensemble(predictions_dict):
    """
    Average the ranks instead of predictions
    More robust to different scales
    """
    
    # Convert predictions to ranks
    ranked_predictions = {}
    
    for model_name, predictions in predictions_dict.items():
        # Get ranks (higher prediction = higher rank)
        ranks = pd.Series(predictions).rank(pct=True).values
        ranked_predictions[model_name] = ranks
    
    # Average ranks
    avg_ranks = np.mean(list(ranked_predictions.values()), axis=0)
    
    return avg_ranks

# Rank averaging
rank_ensemble = rank_average_ensemble(ensemble_predictions)
rank_auc = roc_auc_score(y_test, rank_ensemble)

print(f"\nRank Averaging Ensemble AUC: {rank_auc:.4f}")

# -----------------------------------------------------------------------------
# TECHNIQUE 5: OPTIM IZED WEIGHT SEARCH
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE 5: Optimized Weight Search")
print("-"*60)

from scipy.optimize import minimize

def optimize_weights(predictions_list, y_true):
    """
    Find optimal weights using optimization
    """
    
    def objective(weights):
        # Ensure weights sum to 1
        weights = weights / weights.sum()
        
        # Weighted average prediction
        ensemble = np.average(predictions_list, axis=0, weights=weights)
        
        # Negative AUC (we minimize)
        return -roc_auc_score(y_true, ensemble)
    
    # Initial guess: equal weights
    n_models = len(predictions_list)
    initial_weights = np.ones(n_models) / n_models
    
    # Constraints: weights must sum to 1 and be non-negative
    constraints = {'type': 'eq', 'fun': lambda w: w.sum() - 1}
    bounds = [(0, 1) for _ in range(n_models)]
    
    # Optimize
    result = minimize(
        objective,
        initial_weights,
        method='SLSQP',
        bounds=bounds,
        constraints=constraints
    )
    
    return result.x

# Find optimal weights
predictions_list = [
    ensemble_predictions['xgboost'],
    ensemble_predictions['lightgbm'],
    ensemble_predictions['catboost']
]

optimal_weights = optimize_weights(predictions_list, y_test)

print("\nOptimized Weights:")
for idx, model_name in enumerate(ensemble_predictions.keys()):
    print(f"  {model_name.upper()}: {optimal_weights[idx]:.4f}")

# Create optimized ensemble
optimized_ensemble = np.average(predictions_list, axis=0, weights=optimal_weights)
optimized_auc = roc_auc_score(y_test, optimized_ensemble)

print(f"\nOptimized Ensemble AUC: {optimized_auc:.4f}")

# -----------------------------------------------------------------------------
# ENSEMBLE COMPARISON
# -----------------------------------------------------------------------------

print("\n" + "="*60)
print("ENSEMBLE METHODS COMPARISON")
print("="*60)

ensemble_results = pd.DataFrame({
    'Method': [
        'XGBoost (Single)',
        'LightGBM (Single)',
        'CatBoost (Single)',
        'Equal Weight Average',
        'Performance-Weighted Average',
        'Stacking',
        'Rank Averaging',
        'Optimized Weights'
    ],
    'ROC-AUC': [
        roc_auc_score(y_test, ensemble_predictions['xgboost']),
        roc_auc_score(y_test, ensemble_predictions['lightgbm']),
        roc_auc_score(y_test, ensemble_predictions['catboost']),
        equal_auc,
        weighted_auc,
        stacked_auc,
        rank_auc,
        optimized_auc
    ]
})

ensemble_results = ensemble_results.sort_values('ROC-AUC', ascending=False)
print("\n", ensemble_results.to_string(index=False))

# Visualization
plt.figure(figsize=(12, 6))
plt.barh(ensemble_results['Method'], ensemble_results['ROC-AUC'], color='steelblue')
plt.xlabel('ROC-AUC Score')
plt.title('Ensemble Methods Performance Comparison')
plt.xlim(ensemble_results['ROC-AUC'].min() - 0.01, 1.0)
plt.grid(axis='x', alpha=0.3)
plt.tight_layout()
plt.savefig('ensemble_comparison.png', dpi=300, bbox_inches='tight')
plt.show()

# =============================================================================
# CHAPTER 10: FINAL ADVANCED TECHNIQUES (QUICK REFERENCE)
# =============================================================================

print("="*60)
print("FINAL ADVANCED TECHNIQUES - QUICK REFERENCE")
print("="*60)

# -----------------------------------------------------------------------------
# 10.2 PROBABILITY CALIBRATION
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE: Probability Calibration")
print("-"*60)

from sklearn.calibration import CalibratedClassifierCV, calibration_curve

# Calibrate XGBoost model
calibrated_model = CalibratedClassifierCV(
    models['xgboost']['model'],
    method='isotonic',  # or 'sigmoid'
    cv=5
)

calibrated_model.fit(data_dict['X_train_enc'], data_dict['y_train'])
calibrated_proba = calibrated_model.predict_proba(data_dict['X_test_enc'])[:, 1]

# Compare calibration
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Before calibration
prob_true_before, prob_pred_before = calibration_curve(
    y_test, models['xgboost']['probabilities'], n_bins=10
)
axes[0].plot(prob_pred_before, prob_true_before, marker='o', linewidth=2)
axes[0].plot([0, 1], [0, 1], 'k--', label='Perfectly Calibrated')
axes[0].set_xlabel('Mean Predicted Probability')
axes[0].set_ylabel('True Probability')
axes[0].set_title('Before Calibration')
axes[0].legend()
axes[0].grid(alpha=0.3)

# After calibration
prob_true_after, prob_pred_after = calibration_curve(
    y_test, calibrated_proba, n_bins=10
)
axes[1].plot(prob_pred_after, prob_true_after, marker='o', linewidth=2, color='green')
axes[1].plot([0, 1], [0, 1], 'k--', label='Perfectly Calibrated')
axes[1].set_xlabel('Mean Predicted Probability')
axes[1].set_ylabel('True Probability')
axes[1].set_title('After Calibration')
axes[1].legend()
axes[1].grid(alpha=0.3)

plt.tight_layout()
plt.savefig('calibration_comparison.png', dpi=300, bbox_inches='tight')
plt.show()

print("✓ Calibration improves probability reliability for decision-making")

# -----------------------------------------------------------------------------
# 10.3 HANDLING CLASS IMBALANCE - SUMMARY
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE: Handling Class Imbalance")
print("-"*60)

print("""
┌─────────────────────────────────────────────────────────────────────┐
│                 CLASS IMBALANCE STRATEGIES                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│ 1. SAMPLING TECHNIQUES:                                              │
│    • SMOTE (Synthetic Minority Oversampling)                         │
│    • Random undersampling                                            │
│    • Tomek links                                                     │
│                                                                      │
│ 2. ALGORITHM-LEVEL:                                                  │
│    • XGBoost: scale_pos_weight parameter                             │
│    • LightGBM: is_unbalance=True or scale_pos_weight                 │
│    • CatBoost: auto_class_weights='Balanced'                         │
│                                                                      │
│ 3. LOSS FUNCTION:                                                    │
│    • Focal Loss (down-weights easy examples)                         │
│    • Weighted cross-entropy                                          │
│                                                                      │
│ 4. THRESHOLD ADJUSTMENT:                                             │
│    • Optimize threshold for F1/Recall                                │
│    • Use precision-recall curve                                      │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
""")

# Quick example
from imblearn.over_sampling import SMOTE

smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(
    data_dict['X_train_enc'], 
    data_dict['y_train']
)

print(f"Original class distribution: {dict(pd.Series(data_dict['y_train']).value_counts())}")
print(f"After SMOTE: {dict(pd.Series(y_resampled).value_counts())}")

# -----------------------------------------------------------------------------
# 10.4 CROSS-VALIDATION STRATEGIES
# -----------------------------------------------------------------------------

print("\n" + "-"*60)
print("TECHNIQUE: Cross-Validation Strategies")
print("-"*60)

print("""
┌─────────────────────────────────────────────────────────────────────┐
│                   CV STRATEGIES BY USE CASE                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│ STANDARD DATA:                                                       │
│    • StratifiedKFold (maintains class balance)                       │
│    • RepeatedStratifiedKFold (more robust estimates)                 │
│                                                                      │
│ TIME SERIES DATA:                                                    │
│    • TimeSeriesSplit (respects temporal order)                       │
│    • Expanding window / Sliding window                               │
│                                                                      │
│ GROUPED DATA (e.g., multiple rows per customer):                     │
│    • GroupKFold (keeps groups together)                              │
│    • StratifiedGroupKFold                                            │
│                                                                      │
│ SMALL DATA:                                                          │
│    • Leave-One-Out (maximum training data)                           │
│    • Nested CV (unbiased performance estimate)                       │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
""")

from sklearn.model_selection import StratifiedKFold, TimeSeriesSplit

# Stratified K-Fold example
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

cv_scores = []
for fold, (train_idx, val_idx) in enumerate(skf.split(data_dict['X_train_enc'], data_dict['y_train'])):
    X_fold_train = data_dict['X_train_enc'].iloc[train_idx]
    y_fold_train = data_dict['y_train'].iloc[train_idx]
    X_fold_val = data_dict['X_train_enc'].iloc[val_idx]
    y_fold_val = data_dict['y_train'].iloc[val_idx]
    
    model = xgb.XGBClassifier(n_estimators=100, max_depth=6, random_state=42, verbosity=0)
    model.fit(X_fold_train, y_fold_train)
    
    score = roc_auc_score(y_fold_val, model.predict_proba(X_fold_val)[:, 1])
    cv_scores.append(score)
    print(f"  Fold {fold+1}: AUC = {score:.4f}")

print(f"\nMean CV AUC: {np.mean(cv_scores):.4f} ± {np.std(cv_scores):.4f}")
Chapter 11: Quick Reference Cheat Sheet
text

╔═══════════════════════════════════════════════════════════════════════════════╗
║                     GRADIENT BOOSTING CHEAT SHEET                              ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║  ┌─────────────────────────────────────────────────────────────────────────┐  ║
║  │                         WHEN TO USE WHICH?                               │  ║
║  ├─────────────────────────────────────────────────────────────────────────┤  ║
║  │ • XGBOOST    → Balanced choice, most mature, great for competitions     │  ║
║  │ • LIGHTGBM   → Large data, need speed, memory constraints               │  ║
║  │ • CATBOOST   → Many categorical features, want robust defaults          │  ║
║  └─────────────────────────────────────────────────────────────────────────┘  ║
║                                                                                ║
║  ┌─────────────────────────────────────────────────────────────────────────┐  ║
║  │                     ESSENTIAL PARAMETERS                                 │  ║
║  ├─────────────────┬───────────────┬───────────────┬───────────────────────┤  ║
║  │ CONCEPT         │ XGBOOST       │ LIGHTGBM      │ CATBOOST              │  ║
║  ├─────────────────┼───────────────┼───────────────┼───────────────────────┤  ║
║  │ Trees           │ n_estimators  │ n_estimators  │ iterations            │  ║
║  │ Learning rate   │ learning_rate │ learning_rate │ learning_rate         │  ║
║  │ Tree depth      │ max_depth     │ max_depth     │ depth                 │  ║
║  │ Leaves          │ max_leaves    │ num_leaves    │ (use depth)           │  ║
║  │ Min samples     │ min_child_w.  │ min_data_in_l.│ min_data_in_leaf      │  ║
║  │ L2 reg          │ reg_lambda    │ lambda_l2     │ l2_leaf_reg           │  ║
║  │ Row sampling    │ subsample     │ bagging_frac. │ subsample             │  ║
║  │ Col sampling    │ colsample_*   │ feature_frac. │ rsm                   │  ║
║  └─────────────────┴───────────────┴───────────────┴───────────────────────┘  ║
║                                                                                ║
║  ┌─────────────────────────────────────────────────────────────────────────┐  ║
║  │                     TUNING PRIORITY ORDER                                │  ║
║  ├─────────────────────────────────────────────────────────────────────────┤  ║
║  │ 1. learning_rate + n_estimators (use early stopping!)                   │  ║
║  │ 2. max_depth / num_leaves (control complexity)                          │  ║
║  │ 3. min_child_weight / min_data_in_leaf (prevent overfitting)            │  ║
║  │ 4. subsample + colsample_bytree (add randomness)                        │  ║
║  │ 5. reg_lambda + reg_alpha (regularization)                              │  ║
║  │ 6. Lower learning_rate, increase n_estimators (final boost)             │  ║
║  └─────────────────────────────────────────────────────────────────────────┘  ║
║                                                                                ║
║  ┌─────────────────────────────────────────────────────────────────────────┐  ║
║  │                     OVERFITTING CHECKLIST                                │  ║
║  ├─────────────────────────────────────────────────────────────────────────┤  ║
║  │ □ Reduce max_depth / num_leaves                                         │  ║
║  │ □ Increase min_child_weight / min_data_in_leaf                          │  ║
║  │ □ Increase regularization (lambda, alpha)                               │  ║
║  │ □ Reduce learning_rate                                                  │  ║
║  │ □ Add subsampling (< 1.0)                                               │  ║
║  │ □ Use early stopping                                                    │  ║
║  │ □ Get more training data                                                │  ║
║  └─────────────────────────────────────────────────────────────────────────┘  ║
║                                                                                ║
║  ┌─────────────────────────────────────────────────────────────────────────┐  ║
║  │                     QUICK START TEMPLATES                                │  ║
║  ├─────────────────────────────────────────────────────────────────────────┤  ║
║  │                                                                          │  ║
║  │ XGBOOST:                                                                 │  ║
║  │   XGBClassifier(n_estimators=1000, max_depth=6, learning_rate=0.05,     │  ║
║  │                 early_stopping_rounds=50, random_state=42)               │  ║
║  │                                                                          │  ║
║  │ LIGHTGBM:                                                                │  ║
║  │   LGBMClassifier(n_estimators=1000, num_leaves=31, learning_rate=0.05,  │  ║
║  │                  callbacks=[early_stopping(50)], random_state=42)        │  ║
║  │                                                                          │  ║
║  │ CATBOOST:                                                                │  ║
║  │   CatBoostClassifier(iterations=1000, depth=6, learning_rate=0.05,      │  ║
║  │                      early_stopping_rounds=50, cat_features=cat_cols)    │  ║
║  │                                                                          │  ║
║  └─────────────────────────────────────────────────────────────────────────┘  ║
║                                                                                ║
╚═══════════════════════════════════════════════════════════════════════════════╝
Chapter 12: Interview Preparation
text

╔═══════════════════════════════════════════════════════════════════════════════╗
║                    TOP INTERVIEW QUESTIONS & ANSWERS                           ║
╠═══════════════════════════════════════════════════════════════════════════════╣

Q1: What is the difference between Bagging and Boosting?
────────────────────────────────────────────────────────────────────────────────
BAGGING:
• Trees trained in PARALLEL on random subsets
• Each tree is INDEPENDENT
• Reduces VARIANCE (stabilizes predictions)
• Example: Random Forest

BOOSTING:
• Trees trained SEQUENTIALLY
• Each tree learns from PREVIOUS tree's errors
• Reduces BIAS (improves accuracy)
• Example: XGBoost, LightGBM, CatBoost

═══════════════════════════════════════════════════════════════════════════════

Q2: How does Gradient Boosting work?
────────────────────────────────────────────────────────────────────────────────
1. Start with initial prediction (usually mean/log-odds)
2. Calculate RESIDUALS (errors) = Actual - Predicted
3. Train a tree to predict these residuals
4. Add tree's prediction to model (scaled by learning rate)
5. Calculate new residuals
6. Repeat until convergence

Key Insight: Each tree corrects the mistakes of the ensemble so far!

═══════════════════════════════════════════════════════════════════════════════

Q3: What makes XGBoost special?
────────────────────────────────────────────────────────────────────────────────
1. REGULARIZATION: L1 and L2 penalties in objective function
2. SECOND-ORDER GRADIENTS: Uses both gradient and hessian
3. SPARSITY AWARENESS: Learns optimal direction for missing values
4. PARALLEL PROCESSING: Split finding parallelized
5. CACHE OPTIMIZATION: Memory-efficient data access
6. TREE PRUNING: Uses gamma parameter for pre-pruning

═══════════════════════════════════════════════════════════════════════════════

Q4: How is LightGBM faster than XGBoost?
────────────────────────────────────────────────────────────────────────────────
1. HISTOGRAM-BASED SPLITTING: Bins continuous features (256 bins)
   → Reduces split points from millions to 256
   
2. LEAF-WISE GROWTH: Expands leaf with max gain
   → More efficient than level-wise
   
3. GOSS: Keeps large gradients, samples small gradients
   → Reduces training data without losing accuracy
   
4. EFB: Bundles mutually exclusive features
   → Reduces number of features to process

═══════════════════════════════════════════════════════════════════════════════

Q5: Why is CatBoost better for categorical features?
────────────────────────────────────────────────────────────────────────────────
1. ORDERED TARGET STATISTICS:
   - Uses only PAST data to encode categories
   - Prevents target leakage
   - No need for separate validation set

2. AUTOMATIC COMBINATIONS:
   - Creates category pairs/triples automatically
   - Captures feature interactions

3. NO PREPROCESSING NEEDED:
   - Handles categories natively
   - No one-hot encoding or label encoding required

═══════════════════════════════════════════════════════════════════════════════

Q6: How do you prevent overfitting in Gradient Boosting?
────────────────────────────────────────────────────────────────────────────────
1. EARLY STOPPING: Monitor validation score, stop when it plateaus
2. REDUCE COMPLEXITY: Lower max_depth, fewer leaves
3. REGULARIZATION: Increase L1/L2 penalties
4. SUBSAMPLING: Use subsample < 1.0 (rows and columns)
5. LOWER LEARNING RATE: Smaller steps = more trees = better generalization
6. INCREASE MIN_SAMPLES: Require more samples per leaf
7. CROSS-VALIDATION: Use CV for parameter tuning

═══════════════════════════════════════════════════════════════════════════════

Q7: What is the bias-variance tradeoff in boosting?
────────────────────────────────────────────────────────────────────────────────
• SHALLOW TREES (weak learners): High bias, low variance
• BOOSTING PROCESS: Reduces bias by combining many weak learners
• TOO MANY TREES: Can increase variance (overfitting)
• LEARNING RATE: Lower rate = more trees needed = lower variance
• REGULARIZATION: Increases bias but reduces variance

Optimal: Find balance where total error is minimized!

═══════════════════════════════════════════════════════════════════════════════

Q8: How do you handle imbalanced data in GBM?
────────────────────────────────────────────────────────────────────────────────
1. CLASS WEIGHTS:
   • XGBoost: scale_pos_weight = neg/pos ratio
   • LightGBM: is_unbalance=True or scale_pos_weight
   • CatBoost: auto_class_weights='Balanced'

2. SAMPLING:
   • SMOTE for oversampling minority
   • Undersampling majority

3. THRESHOLD TUNING:
   • Adjust classification threshold
   • Optimize for F1/Recall instead of accuracy

4. CUSTOM LOSS:
   • Focal loss for hard examples

═══════════════════════════════════════════════════════════════════════════════

Q9: When would you choose each algorithm?
────────────────────────────────────────────────────────────────────────────────
XGBOOST when:
• Need battle-tested, stable algorithm
• Working on Kaggle competition
• Regulatory environment (well-documented)

LIGHTGBM when:
• Large dataset (>100K rows)
• Memory constraints
• Need fastest training

CATBOOST when:
• Many categorical features
• Want robust out-of-box performance
• Need fast prediction time
• Don't want to tune much

═══════════════════════════════════════════════════════════════════════════════

Q10: Explain the learning_rate parameter.
────────────────────────────────────────────────────────────────────────────────
Learning rate (eta) shrinks each tree's contribution:

F_new = F_old + learning_rate × new_tree

• HIGH (0.1-0.3): Faster training, fewer trees, risk of overfitting
• LOW (0.01-0.05): More trees, better generalization, slower

RULE OF THUMB:
• Start with 0.1, use early stopping
• For final model: Lower to 0.01-0.05, increase n_estimators

╚═══════════════════════════════════════════════════════════════════════════════╝
🎯 CONCLUSION
text

╔═══════════════════════════════════════════════════════════════════════════════╗
║                                                                                ║
║                     🎓 CONGRATULATIONS! 🎓                                     ║
║                                                                                ║
║          You've completed the Ultimate Guide to Gradient Boosting!            ║
║                                                                                ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║  WHAT YOU'VE LEARNED:                                                          ║
║  ━━━━━━━━━━━━━━━━━━━━━                                                        ║
║                                                                                ║
║  ✅ Chapter 1-2: Foundations of ML, Decision Trees, and Ensemble Methods      ║
║  ✅ Chapter 3: How Gradient Boosting works (residuals, gradients)             ║
║  ✅ Chapter 4: XGBoost deep dive (regularization, second-order gradients)     ║
║  ✅ Chapter 5: LightGBM mastery (histogram, leaf-wise, GOSS, EFB)             ║
║  ✅ Chapter 6: CatBoost expertise (ordered boosting, categorical handling)    ║
║  ✅ Chapter 7: When to use which algorithm                                    ║
║  ✅ Chapter 8: Hyperparameter tuning strategies                               ║
║  ✅ Chapter 9: Complete real-world project implementation                     ║
║  ✅ Chapter 10: Advanced ensemble techniques                                  ║
║  ✅ Chapter 11-12: Quick reference and interview preparation                  ║
║                                                                                ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║  KEY TAKEAWAYS:                                                                ║
║  ━━━━━━━━━━━━━━                                                               ║
║                                                                                ║
║  1. GRADIENT BOOSTING = Sequential learning from mistakes                     ║
║  2. XGBOOST = Regularized + Second-order optimization                         ║
║  3. LIGHTGBM = Speed through histograms + leaf-wise growth                    ║
║  4. CATBOOST = Superior categorical handling + robustness                     ║
║  5. ALWAYS use EARLY STOPPING                                                 ║
║  6. TUNE IN ORDER: learning_rate → depth → regularization → sampling         ║
║  7. ENSEMBLE multiple models for best results                                 ║
║  8. CALIBRATE probabilities for real-world decisions                          ║
║                                                                                ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║  YOUR NEXT STEPS:                                                              ║
║  ━━━━━━━━━━━━━━━                                                              ║
║                                                                                ║
║  📌 Practice on Kaggle competitions                                           ║
║  📌 Apply to your own datasets                                                ║
║  📌 Experiment with different hyperparameters                                 ║
║  📌 Try ensembling all three algorithms                                       ║
║  📌 Deploy a model to production                                              ║
║  📌 Keep learning about new developments!                                     ║
║                                                                                ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║                          THE GOLDEN RULES                                      ║
║                                                                                ║
║        ┌───────────────────────────────────────────────────────────┐          ║
║        │                                                           │          ║
║        │   "Start simple. Add complexity only when needed."        │          ║
║        │                                                           │          ║
║        │   "Trust your validation set, not your training set."     │          ║
║        │                                                           │          ║
║        │   "When in doubt, lower the learning rate."               │          ║
║        │                                                           │          ║
║        │   "The best model is the one that works in production."   │          ║
║        │                                                           │          ║
║        └───────────────────────────────────────────────────────────┘          ║
║                                                                                ║
╠═══════════════════════════════════════════════════════════════════════════════╣
║                                                                                ║
║                                                                                ║
║                    🚀 NOW GO BUILD SOMETHING AMAZING! 🚀                       ║
║                                                                                ║
║                                                                                ║
╚═══════════════════════════════════════════════════════════════════════════════╝
📚 ADDITIONAL RESOURCES
text

OFFICIAL DOCUMENTATION:
━━━━━━━━━━━━━━━━━━━━━━
• XGBoost: https://xgboost.readthedocs.io/
• LightGBM: https://lightgbm.readthedocs.io/
• CatBoost: https://catboost.ai/docs/

RESEARCH PAPERS:
━━━━━━━━━━━━━━━━
• XGBoost: "XGBoost: A Scalable Tree Boosting System" (Chen & Guestrin, 2016)
• LightGBM: "LightGBM: A Highly Efficient Gradient Boosting Decision Tree" (Ke et al., 2017)
• CatBoost: "CatBoost: unbiased boosting with categorical features" (Prokhorenkova et al., 2018)

PRACTICE PLATFORMS:
━━━━━━━━━━━━━━━━━━
• Kaggle: www.kaggle.com (competitions & datasets)
• UCI ML Repository: archive.ics.uci.edu/ml
• OpenML: www.openml.org

TOOLS & LIBRARIES:
━━━━━━━━━━━━━━━━━
• Optuna: Hyperparameter optimization
• SHAP: Model interpretability
• MLflow: Experiment tracking
• Weights & Biases: ML experiment management
END OF GUIDE

Thank you for reading! This guide took you from zero to hero in Gradient Boosting. Remember: the best way to learn is by doing. Take these concepts, apply them to real problems, and keep experimenting. Good luck on your machine learning journey! 🎯






