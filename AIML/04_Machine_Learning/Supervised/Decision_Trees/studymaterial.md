🌳 The Ultimate Decision Tree Masterclass
From Zero to Hero: A Complete Journey
📚 Table of Contents
Chapter 1: The Foundation - What is a Decision Tree?
Chapter 2: The Anatomy of a Decision Tree
Chapter 3: How Does a Decision Tree Learn?
Chapter 4: Splitting Criteria - The Heart of Decision Trees
Chapter 5: Building Your First Decision Tree
Chapter 6: The Mathematics Deep Dive
Chapter 7: Overfitting and Underfitting
Chapter 8: Pruning Techniques
Chapter 9: Decision Trees for Regression
Chapter 10: Hyperparameter Tuning
Chapter 11: Advantages and Disadvantages
Chapter 12: Advanced Variants
Chapter 13: Real-World Implementation
Chapter 14: Interview Questions & Answers
Chapter 15: Practice Problems
Chapter 1: The Foundation - What is a Decision Tree? {#chapter-1-the-foundation}
🎯 The Simplest Explanation Ever
Imagine you're a doctor. A patient comes to you with a fever. How do you decide what's wrong?

text

Question 1: Does the patient have a cough?
    → YES: Maybe it's flu or cold
    → NO: Let's check something else

Question 2: Is the temperature above 102°F?
    → YES: Could be serious infection
    → NO: Might be mild fever

Question 3: Does the patient have body aches?
    → YES: Likely flu
    → NO: Likely common cold
Congratulations! You just understood a Decision Tree!

📖 Formal Definition
A Decision Tree is a supervised machine learning algorithm that makes decisions by asking a series of questions, splitting data based on feature values, and arriving at a prediction through a tree-like structure of decisions.

🌍 Real-Life Examples You Already Know
Example 1: Should I Go Outside Today?
text

                    [Is it raining?]
                    /              \
                  YES              NO
                  /                  \
        [Do I have umbrella?]    [Go Outside! ✓]
           /          \
         YES          NO
          /            \
   [Go Outside! ✓]  [Stay Home ✗]
Example 2: Email Spam Detection
text

                [Contains "FREE MONEY"?]
                    /              \
                  YES              NO
                  /                  \
           [SPAM! 🚫]      [From known contact?]
                              /          \
                            YES          NO
                            /              \
                     [NOT SPAM ✓]   [Contains links?]
                                        /      \
                                      YES      NO
                                      /          \
                               [SPAM! 🚫]  [NOT SPAM ✓]
🎓 Key Insight
A Decision Tree mimics human decision-making by breaking down complex decisions into simpler, sequential choices.

Chapter 2: The Anatomy of a Decision Tree {#chapter-2-the-anatomy}
🏗️ Building Blocks
Every Decision Tree has these components:

text

                      [Root Node]          ← WHERE IT ALL BEGINS
                     /          \
                    /            \
            [Internal Node]   [Internal Node]    ← DECISION POINTS
               /    \            /    \
              /      \          /      \
          [Leaf]  [Leaf]    [Leaf]  [Internal Node]  ← SOME ARE FINAL
                                        /    \
                                       /      \
                                   [Leaf]  [Leaf]    ← ALL PATHS END HERE
📝 Components Explained
Component	What It Is	What It Does	Example
Root Node	The topmost node	First decision/question	"Is age > 30?"
Internal Node	Middle nodes	Intermediate decisions	"Is income > 50K?"
Leaf Node	Terminal nodes	Final predictions	"Approve Loan: YES"
Branch/Edge	Connections	Represents decision outcome	"YES" or "NO" path
Depth	Levels count	Distance from root to deepest leaf	Depth = 3
Parent Node	Node above	Node that splits into current node	-
Child Node	Node below	Nodes created from a split	-
🎨 Visual Deep Dive
text

DEPTH 0:              [Root: Age > 30?]              ← Root Node (Parent of all)
                      /              \
                   YES                NO
                   /                    \
DEPTH 1:   [Income > 50K?]        [Student?]         ← Internal Nodes
           /          \            /        \
         YES          NO         YES        NO
         /              \        /            \
DEPTH 2: [APPROVE]    [REJECT] [APPROVE]    [REJECT]  ← Leaf Nodes (Children)
         
         ↑              ↑
    Leaf Node      Leaf Node
    (Prediction)   (Prediction)
📊 Important Terminology
1. Splitting
The process of dividing a node into two or more sub-nodes.

text

Before Split:          After Split:
[100 samples]    →    [60 samples] + [40 samples]
2. Feature/Attribute
The variable used to make a split decision.

text

Features: Age, Income, Education, Gender
3. Threshold
The value at which we split a continuous feature.

text

Age > 30  ← Here, 30 is the threshold
4. Pure Node
A leaf node where all samples belong to ONE class.

text

Pure:     [10 Apples, 0 Oranges]  ← 100% Apples
Impure:   [7 Apples, 3 Oranges]   ← Mixed
Chapter 3: How Does a Decision Tree Learn? {#chapter-3-how-it-learns}
🧠 The Learning Process
Step-by-Step Algorithm
text

ALGORITHM: Build_Decision_Tree(Data, Features)

1. IF all samples belong to same class:
       RETURN Leaf Node with that class label
   
2. IF no features left to split:
       RETURN Leaf Node with majority class
   
3. ELSE:
       a. Find the BEST feature to split on
       b. Create a node with that feature
       c. Split data based on feature values
       d. For each split:
           Recursively call Build_Decision_Tree(subset, remaining_features)
       e. RETURN the node

END ALGORITHM
🎯 The Core Question: "What is the BEST split?"
This is THE most important concept in Decision Trees!

The Goal of Splitting
text

BEFORE SPLIT (Impure):
┌─────────────────────────┐
│ 🍎🍎🍎🍎🍎🍊🍊🍊🍊🍊 │  ← 50% Apple, 50% Orange (MESSY!)
└─────────────────────────┘

AFTER GOOD SPLIT (More Pure):
┌────────────┐    ┌────────────┐
│ 🍎🍎🍎🍎🍎 │    │ 🍊🍊🍊🍊🍊 │  ← 100% each (CLEAN!)
└────────────┘    └────────────┘
  Left Node        Right Node
What Makes a Split "Good"?
A good split creates child nodes that are MORE PURE than the parent.

text

PURITY MEASUREMENT:

Parent Node:     [50 Yes, 50 No]  → Very Impure (50-50 mix)
                      |
                   SPLIT
                   /    \
Child 1: [45 Yes, 5 No]   Child 2: [5 Yes, 45 No]
         ↑                         ↑
    More Pure!                More Pure!
🔄 The Recursive Nature
text

                    START
                      │
                      ▼
            ┌─────────────────┐
            │ Can we split?   │
            └────────┬────────┘
                     │
         ┌───────────┴───────────┐
         │                       │
        YES                      NO
         │                       │
         ▼                       ▼
  ┌──────────────┐       ┌────────────┐
  │ Find best    │       │ Create     │
  │ split        │       │ Leaf Node  │
  └──────┬───────┘       └────────────┘
         │
         ▼
  ┌──────────────┐
  │ Split data   │
  └──────┬───────┘
         │
         ▼
  ┌──────────────┐
  │ For each     │──────┐
  │ subset       │      │
  └──────────────┘      │
                        │
         ┌──────────────┘
         │
         ▼
    RECURSIVELY BUILD
    (Go back to START)
Chapter 4: Splitting Criteria - The Heart of Decision Trees {#chapter-4-splitting-criteria}
🎯 The Big Three Measures
There are three main ways to measure "impurity" and decide the best split:

Measure	Used For	Formula Type
Gini Impurity	Classification	Probability-based
Entropy/Information Gain	Classification	Logarithmic
Variance Reduction	Regression	Statistical
1️⃣ GINI IMPURITY
What is Gini Impurity?
Gini Impurity measures the probability of incorrectly classifying a randomly chosen element if it were labeled according to the distribution of labels in the node.

The Formula
text

Gini(node) = 1 - Σ(pᵢ)²

Where:
- pᵢ = probability of class i in the node
- Σ = sum over all classes
Visual Understanding
text

SCENARIO 1: Pure Node (All same class)
┌──────────────────┐
│ 🔴🔴🔴🔴🔴🔴🔴🔴 │  8 Red, 0 Blue
└──────────────────┘

Gini = 1 - (8/8)² - (0/8)²
     = 1 - 1 - 0
     = 0  ← PERFECT! (No impurity)


SCENARIO 2: Impure Node (50-50 mix)
┌──────────────────┐
│ 🔴🔴🔴🔴🔵🔵🔵🔵 │  4 Red, 4 Blue
└──────────────────┘

Gini = 1 - (4/8)² - (4/8)²
     = 1 - 0.25 - 0.25
     = 0.5  ← MAXIMUM IMPURITY for binary!


SCENARIO 3: Somewhat Pure
┌──────────────────┐
│ 🔴🔴🔴🔴🔴🔴🔵🔵 │  6 Red, 2 Blue
└──────────────────┘

Gini = 1 - (6/8)² - (2/8)²
     = 1 - 0.5625 - 0.0625
     = 0.375  ← Some impurity
Gini Impurity Range
text

0 ──────────────────────────── 0.5 (for binary classification)
│                               │
Pure                        Maximum
(All same class)            Impurity
                            (50-50 split)
Calculating Gini for a Split
text

                    Parent Node
                 [40 Yes, 40 No]
                 Gini = 0.5
                       │
          ┌────────────┴────────────┐
          │                         │
    Feature: Age > 30               │
          │                         │
     ┌────┴────┐              ┌─────┴─────┐
     │  YES    │              │    NO     │
     │         │              │           │
 [35 Yes, 5 No]           [5 Yes, 35 No]
 n=40 samples              n=40 samples
 
 Gini_left = 1 - (35/40)² - (5/40)²
           = 1 - 0.7656 - 0.0156
           = 0.219
           
 Gini_right = 1 - (5/40)² - (35/40)²
            = 1 - 0.0156 - 0.7656
            = 0.219

Weighted Gini = (40/80) × 0.219 + (40/80) × 0.219
              = 0.219

Gini Reduction = 0.5 - 0.219 = 0.281 ← This is GOOD!
2️⃣ ENTROPY & INFORMATION GAIN
What is Entropy?
Entropy measures the disorder or uncertainty in a dataset. Higher entropy = more disorder = more impure.

The Formula
text

Entropy(node) = -Σ pᵢ × log₂(pᵢ)

Where:
- pᵢ = probability of class i
- log₂ = logarithm base 2
Visual Understanding
text

SCENARIO 1: Pure Node
┌──────────────────┐
│ 🔴🔴🔴🔴🔴🔴🔴🔴 │  All Red
└──────────────────┘

Entropy = -(1 × log₂(1)) - (0 × log₂(0))
        = -(1 × 0) - 0
        = 0  ← NO UNCERTAINTY!


SCENARIO 2: Maximum Disorder (50-50)
┌──────────────────┐
│ 🔴🔴🔴🔴🔵🔵🔵🔵 │  Half and Half
└──────────────────┘

Entropy = -(0.5 × log₂(0.5)) - (0.5 × log₂(0.5))
        = -(0.5 × -1) - (0.5 × -1)
        = 0.5 + 0.5
        = 1  ← MAXIMUM UNCERTAINTY!


SCENARIO 3: Partial Purity
┌──────────────────┐
│ 🔴🔴🔴🔴🔴🔴🔵🔵 │  75% Red, 25% Blue
└──────────────────┘

Entropy = -(0.75 × log₂(0.75)) - (0.25 × log₂(0.25))
        = -(0.75 × -0.415) - (0.25 × -2)
        = 0.311 + 0.5
        = 0.811
Entropy Range
text

0 ──────────────────────────── 1 (for binary classification)
│                               │
Pure                        Maximum
(All same class)            Disorder
                            (50-50 split)
Information Gain
Information Gain = How much entropy did we REDUCE by making this split?

text

Information Gain = Entropy(Parent) - Weighted_Avg_Entropy(Children)

IG = E(parent) - Σ (nᵢ/n) × E(childᵢ)
Complete Example: Information Gain
text

                    Parent Node
              [14 samples total]
              [9 Play, 5 Don't Play]
              
Entropy(Parent) = -(9/14)log₂(9/14) - (5/14)log₂(5/14)
                = -(0.643)(-0.637) - (0.357)(-1.486)
                = 0.410 + 0.530
                = 0.940

                        │
          ┌─────────────┴─────────────┐
          │    Split: Outlook         │
          │                           │
    ┌─────┴─────┬─────────┴─────┐
    │           │               │
  Sunny      Overcast        Rainy
 [5 samples]  [4 samples]   [5 samples]
 [2P, 3D]     [4P, 0D]      [3P, 2D]

E(Sunny) = -(2/5)log₂(2/5) - (3/5)log₂(3/5)
         = 0.971

E(Overcast) = -(4/4)log₂(4/4) - (0/4)log₂(0/4)
            = 0  ← PURE!

E(Rainy) = -(3/5)log₂(3/5) - (2/5)log₂(2/5)
         = 0.971

Weighted Entropy = (5/14)×0.971 + (4/14)×0 + (5/14)×0.971
                 = 0.347 + 0 + 0.347
                 = 0.694

INFORMATION GAIN = 0.940 - 0.694 = 0.246
3️⃣ COMPARISON: GINI vs ENTROPY
text

┌─────────────────┬─────────────────────┬─────────────────────┐
│     Aspect      │    Gini Impurity    │       Entropy       │
├─────────────────┼─────────────────────┼─────────────────────┤
│ Range (binary)  │     0 to 0.5        │      0 to 1         │
│                 │                     │                     │
│ Computation     │     Faster          │     Slower          │
│                 │   (no logarithm)    │   (uses log)        │
│                 │                     │                     │
│ Default in      │     sklearn         │     ID3, C4.5       │
│                 │                     │                     │
│ Interpretation  │   Probability of    │  Bits needed to     │
│                 │   misclassification │  encode information │
│                 │                     │                     │
│ Practical       │   Very similar      │   Very similar      │
│ Difference      │   results           │   results           │
└─────────────────┴─────────────────────┴─────────────────────┘
Visual Comparison
text

         │
    1.0  │              Entropy
         │            ╱╲
    0.8  │          ╱    ╲
         │        ╱        ╲
    0.6  │      ╱            ╲
         │    ╱                ╲
    0.5  │   ╱   Gini          ╲
         │  ╱  ╱╲              ╲
    0.4  │ ╱ ╱    ╲              ╲
         │╱╱        ╲            ╲
    0.2  │           ╲            ╲
         │             ╲            ╲
    0.0  │──────────────────────────────
         0    0.25   0.5   0.75    1.0
                   p (probability)
Chapter 5: Building Your First Decision Tree {#chapter-5-building-first-tree}
📊 The Famous "Play Tennis" Dataset
Day	Outlook	Temperature	Humidity	Windy	Play Tennis?
1	Sunny	Hot	High	False	No
2	Sunny	Hot	High	True	No
3	Overcast	Hot	High	False	Yes
4	Rainy	Mild	High	False	Yes
5	Rainy	Cool	Normal	False	Yes
6	Rainy	Cool	Normal	True	No
7	Overcast	Cool	Normal	True	Yes
8	Sunny	Mild	High	False	No
9	Sunny	Cool	Normal	False	Yes
10	Rainy	Mild	Normal	False	Yes
11	Sunny	Mild	Normal	True	Yes
12	Overcast	Mild	High	True	Yes
13	Overcast	Hot	Normal	False	Yes
14	Rainy	Mild	High	True	No
Summary: 14 samples, 9 "Yes", 5 "No"

🔨 Step-by-Step Construction
STEP 1: Calculate Parent Entropy
text

Total: 14 samples
Yes: 9 samples (p = 9/14 = 0.643)
No: 5 samples (p = 5/14 = 0.357)

Entropy(Parent) = -(9/14)log₂(9/14) - (5/14)log₂(5/14)
                = -(0.643)(−0.637) - (0.357)(−1.486)
                = 0.410 + 0.530
                = 0.940
STEP 2: Calculate Information Gain for Each Feature
Feature 1: OUTLOOK
text

Outlook = Sunny (5 samples): 2 Yes, 3 No
Outlook = Overcast (4 samples): 4 Yes, 0 No  ← PURE!
Outlook = Rainy (5 samples): 3 Yes, 2 No

E(Sunny) = -(2/5)log₂(2/5) - (3/5)log₂(3/5) = 0.971
E(Overcast) = 0 (pure node!)
E(Rainy) = -(3/5)log₂(3/5) - (2/5)log₂(2/5) = 0.971

Weighted Entropy = (5/14)(0.971) + (4/14)(0) + (5/14)(0.971)
                 = 0.347 + 0 + 0.347 = 0.694

IG(Outlook) = 0.940 - 0.694 = 0.246 ✓
Feature 2: TEMPERATURE
text

Temperature = Hot (4 samples): 2 Yes, 2 No
Temperature = Mild (6 samples): 4 Yes, 2 No
Temperature = Cool (4 samples): 3 Yes, 1 No

E(Hot) = 1.0 (50-50 split)
E(Mild) = -(4/6)log₂(4/6) - (2/6)log₂(2/6) = 0.918
E(Cool) = -(3/4)log₂(3/4) - (1/4)log₂(1/4) = 0.811

Weighted Entropy = (4/14)(1.0) + (6/14)(0.918) + (4/14)(0.811)
                 = 0.286 + 0.394 + 0.232 = 0.912

IG(Temperature) = 0.940 - 0.912 = 0.028
Feature 3: HUMIDITY
text

Humidity = High (7 samples): 3 Yes, 4 No
Humidity = Normal (7 samples): 6 Yes, 1 No

E(High) = -(3/7)log₂(3/7) - (4/7)log₂(4/7) = 0.985
E(Normal) = -(6/7)log₂(6/7) - (1/7)log₂(1/7) = 0.592

Weighted Entropy = (7/14)(0.985) + (7/14)(0.592)
                 = 0.493 + 0.296 = 0.789

IG(Humidity) = 0.940 - 0.789 = 0.151
Feature 4: WINDY
text

Windy = True (6 samples): 3 Yes, 3 No
Windy = False (8 samples): 6 Yes, 2 No

E(True) = 1.0 (50-50 split)
E(False) = -(6/8)log₂(6/8) - (2/8)log₂(2/8) = 0.811

Weighted Entropy = (6/14)(1.0) + (8/14)(0.811)
                 = 0.429 + 0.463 = 0.892

IG(Windy) = 0.940 - 0.892 = 0.048
STEP 3: Compare Information Gains
text

┌─────────────────┬────────────────────┐
│     Feature     │  Information Gain  │
├─────────────────┼────────────────────┤
│    Outlook      │      0.246 ⭐      │ ← HIGHEST! CHOOSE THIS!
│   Temperature   │      0.028         │
│    Humidity     │      0.151         │
│     Windy       │      0.048         │
└─────────────────┴────────────────────┘
STEP 4: Build the First Split
text

                        [Play Tennis?]
                        14 samples
                        [9 Yes, 5 No]
                              │
                    Split on: OUTLOOK
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
        SUNNY             OVERCAST              RAINY
      5 samples           4 samples           5 samples
      [2 Yes, 3 No]      [4 Yes, 0 No]       [3 Yes, 2 No]
          │                   │                   │
          │              PURE NODE!               │
          │                   │                   │
       CONTINUE          ┌────┴────┐          CONTINUE
       SPLITTING         │   YES   │          SPLITTING
                         │ (Leaf)  │
                         └─────────┘
STEP 5: Continue Building (Sunny Branch)
text

Sunny branch: [2 Yes, 3 No] - 5 samples

Remaining features: Temperature, Humidity, Windy

Calculate IG for each on this subset...

After calculation:
- IG(Humidity) = 0.971 ← HIGHEST!
- IG(Temperature) = 0.571
- IG(Windy) = 0.020

Split on Humidity:
- Humidity = High: [0 Yes, 3 No] → NO (pure!)
- Humidity = Normal: [2 Yes, 0 No] → YES (pure!)
STEP 6: Continue Building (Rainy Branch)
text

Rainy branch: [3 Yes, 2 No] - 5 samples

After calculation:
- IG(Windy) = 0.971 ← HIGHEST!

Split on Windy:
- Windy = True: [0 Yes, 2 No] → NO (pure!)
- Windy = False: [3 Yes, 0 No] → YES (pure!)
FINAL TREE
text

                           [Outlook?]
                         /     |      \
                      /        |         \
                   /           |            \
               Sunny       Overcast        Rainy
                 |             |              |
            [Humidity?]      YES         [Windy?]
              /    \                      /    \
           High   Normal              True    False
            |        |                  |        |
           NO       YES                NO       YES
Tree in Decision Rules
Python

if Outlook == "Overcast":
    Play = "Yes"
elif Outlook == "Sunny":
    if Humidity == "High":
        Play = "No"
    else:  # Humidity == "Normal"
        Play = "Yes"
elif Outlook == "Rainy":
    if Windy == True:
        Play = "No"
    else:  # Windy == False
        Play = "Yes"
Chapter 6: The Mathematics Deep Dive {#chapter-6-mathematics}
🧮 Complete Mathematical Framework
1. Entropy Derivation
Why logarithm?

Entropy comes from Information Theory (Claude Shannon, 1948).

text

Information content of an event = -log₂(p)

Why?
- Rare events (low p) carry MORE information
- Common events (high p) carry LESS information

Example:
- "Sun rises tomorrow" → Very likely, low information
- "Aliens landed today" → Very unlikely, HIGH information!

If p = 1/2: Information = -log₂(0.5) = 1 bit
If p = 1/4: Information = -log₂(0.25) = 2 bits
If p = 1/8: Information = -log₂(0.125) = 3 bits
Expected Information (Entropy):

text

H(X) = E[Information] = E[-log₂(p)]
     = Σ p(x) × (-log₂(p(x)))
     = -Σ p(x) × log₂(p(x))
2. Gini Impurity Derivation
Intuition: Probability of misclassification

text

Imagine randomly picking two samples from a node:
- Pick sample 1 with class label
- Assign class based on distribution
- What's the probability of mismatch?

P(misclassification) = P(pick class i) × P(NOT guessing class i)
                     = Σ pᵢ × (1 - pᵢ)
                     = Σ pᵢ - Σ pᵢ²
                     = 1 - Σ pᵢ²    (since Σpᵢ = 1)
3. Gain Ratio (C4.5 Improvement)
Problem with Information Gain: Bias towards features with many values.

text

Example: "Customer ID" has unique value for each sample
→ Creates perfectly pure nodes!
→ But it's USELESS for generalization!
Solution: Gain Ratio

text

Gain Ratio = Information Gain / Split Information

Split Information = -Σ (|Sᵢ|/|S|) × log₂(|Sᵢ|/|S|)

Where |Sᵢ| = samples in split i
      |S| = total samples
Example:

text

Feature "ID" splits into 14 individual samples:
Split Info = -14 × (1/14)log₂(1/14)
           = -14 × (1/14) × (-3.81)
           = 3.81 (VERY HIGH!)

Gain Ratio = IG / 3.81 = Very LOW!

Feature "Outlook" splits into 3 groups (5,4,5):
Split Info = -(5/14)log₂(5/14) - (4/14)log₂(4/14) - (5/14)log₂(5/14)
           = 1.577

Gain Ratio = 0.246 / 1.577 = 0.156 ← Better!
4. Variance Reduction (Regression Trees)
For continuous target variables:

text

Variance(S) = (1/n) × Σ(yᵢ - ȳ)²

Variance Reduction = Var(Parent) - Weighted_Avg_Var(Children)
Chapter 7: Overfitting and Underfitting {#chapter-7-overfitting-underfitting}
🎯 The Fundamental Problem
What is Overfitting?
Overfitting occurs when the model learns the training data TOO WELL, including its noise and random fluctuations, failing to generalize to new data.

Visual Explanation
text

TRAINING DATA:                 OVERFITTED TREE:
                               
   ●  ✕     ●                     ┌─────┐
    ●    ✕    ●                   │Age>30│
  ●   ✕   ●                       ├──┬──┤
   ●  ✕  ●   ✕                    ... (50 levels deep!)
  ●   ✕    ●                      │
                                  └─ One leaf per sample!

Training Accuracy: 100%         
Test Accuracy: 45%              ← HORRIBLE!
What is Underfitting?
Underfitting occurs when the model is TOO SIMPLE to capture the underlying patterns in the data.

text

UNDERFITTED TREE (Depth = 1):

        [Income > 50K?]
           /        \
         YES        NO
          |          |
      [Buy: Yes]  [Buy: No]

Too simple! Misses important patterns!
Training Accuracy: 60%
Test Accuracy: 58%
📊 The Bias-Variance Tradeoff
text

                    Model Complexity →
       Simple │                              │ Complex
              │                              │
ERROR    High │───Bias────────●              │
         ^    │                ╲             │
         │    │                  ╲    ╱──────│
         │    │                    ╲╱        │
         │    │                    ╱╲        │
         │    │              ╱────╱  ╲───────│
         │    │          ╱───              Variance
        Low   │─────────●                    │
              │      Optimal!                │
              └──────────────────────────────┘
                              
              UNDERFITTING     │     OVERFITTING
                              SWEET
                              SPOT
Key Concepts
text

┌─────────────┬──────────────────────────────────────────────────┐
│   Concept   │                   Description                    │
├─────────────┼──────────────────────────────────────────────────┤
│    Bias     │ Error from wrong assumptions                     │
│             │ High bias → Underfitting                         │
│             │ Model is too simple                              │
├─────────────┼──────────────────────────────────────────────────┤
│  Variance   │ Error from sensitivity to training data          │
│             │ High variance → Overfitting                      │
│             │ Model changes a lot with different training sets │
├─────────────┼──────────────────────────────────────────────────┤
│    Total    │                                                  │
│    Error    │ = Bias² + Variance + Irreducible Error           │
└─────────────┴──────────────────────────────────────────────────┘
🔍 Signs of Overfitting
text

┌────────────────────────────────────────────────────────────────┐
│                    OVERFITTING SYMPTOMS                         │
├────────────────────────────────────────────────────────────────┤
│  1. Training accuracy >> Test accuracy                         │
│     Example: Train = 99%, Test = 65%                           │
│                                                                │
│  2. Very deep tree (many levels)                               │
│     Each leaf has very few samples                             │
│                                                                │
│  3. Many leaf nodes                                            │
│     Almost as many leaves as training samples                  │
│                                                                │
│  4. Complex decision rules                                     │
│     Rules that don't make logical sense                        │
│                                                                │
│  5. Poor performance on new data                               │
│     Model "memorized" instead of "learned"                     │
└────────────────────────────────────────────────────────────────┘
🔍 Signs of Underfitting
text

┌────────────────────────────────────────────────────────────────┐
│                   UNDERFITTING SYMPTOMS                         │
├────────────────────────────────────────────────────────────────┤
│  1. Both training and test accuracy are LOW                    │
│     Example: Train = 60%, Test = 58%                           │
│                                                                │
│  2. Very shallow tree (few levels)                             │
│     Only 1-2 splits                                            │
│                                                                │
│  3. Too few leaf nodes                                         │
│     Not enough to capture patterns                             │
│                                                                │
│  4. Oversimplified rules                                       │
│     Missing important features/interactions                    │
│                                                                │
│  5. High error on all datasets                                 │
│     Model hasn't learned the patterns                          │
└────────────────────────────────────────────────────────────────┘
Chapter 8: Pruning Techniques {#chapter-8-pruning}
✂️ What is Pruning?
Pruning is the process of removing parts of the tree that don't provide additional predictive power, preventing overfitting.

The Pruning Analogy
text

BEFORE PRUNING:                    AFTER PRUNING:
(Overgrown tree)                   (Healthy tree)

         ●                              ●
        /|\                            / \
       ● ● ●                          ●   ●
      /| |\|\                        /|   |\
     ● ●●● ●●●                      ● ●   ● ●
    /|/|\|\|\                         
   ●●●●●●●●●●●  
   
Many unnecessary                   Only important
branches and leaves                branches remain
🌿 Two Types of Pruning
1. Pre-Pruning (Early Stopping)
Stop growing the tree BEFORE it becomes too complex.

text

DURING TREE CONSTRUCTION:

Step 1: Should I split this node?
        ↓
        Check stopping criteria:
        │
        ├── Max depth reached? → STOP! Create leaf.
        │
        ├── Min samples in node? → Too few? STOP!
        │
        ├── Min samples for split? → Not enough? STOP!
        │
        ├── Information gain < threshold? → STOP!
        │
        └── All criteria pass? → CONTINUE splitting.
Pre-Pruning Parameters:

Python

# In scikit-learn:
DecisionTreeClassifier(
    max_depth=5,           # Maximum levels
    min_samples_split=10,  # Minimum samples to split a node
    min_samples_leaf=5,    # Minimum samples in a leaf
    max_leaf_nodes=20,     # Maximum number of leaves
    min_impurity_decrease=0.01  # Minimum gain required
)
2. Post-Pruning (Backward Pruning)
First grow the full tree, then cut back unnecessary parts.

text

AFTER FULL TREE IS BUILT:

Step 1: Build complete tree (may overfit)
        ↓
Step 2: For each internal node (bottom-up):
        │
        ├── Calculate error WITH subtree
        │
        ├── Calculate error WITHOUT subtree (replace with leaf)
        │
        ├── If error doesn't increase significantly:
        │       → PRUNE! Replace subtree with leaf.
        │
        └── Continue until no more pruning possible.
📐 Cost Complexity Pruning (CCP)
The most mathematically rigorous pruning method.

The Formula
text

Cost Complexity = Error + α × (Number of Leaves)

Rα(T) = R(T) + α|T̃|

Where:
- Rα(T) = Total cost of tree T
- R(T) = Misclassification rate
- α = Complexity parameter (alpha)
- |T̃| = Number of leaf nodes
How α Works
text

α = 0:    No penalty for complexity → Full tree (overfitting)
α = ∞:    Huge penalty for leaves → Single node (underfitting)

                    │
    Full Tree ──────┼────── Single Node
    (α = 0)         │         (α = ∞)
                    │
              Optimal α
            (found via CV)
Step-by-Step CCP
text

STEP 1: Build full tree T₀

STEP 2: Calculate "effective α" for each node
        
        g(t) = [R(t) - R(Tₜ)] / [|T̃ₜ| - 1]
        
        Where:
        - R(t) = error if we replace subtree with leaf
        - R(Tₜ) = error of subtree
        - |T̃ₜ| = number of leaves in subtree

STEP 3: Prune node with smallest g(t)
        → Creates tree T₁

STEP 4: Repeat until single node
        → Creates sequence: T₀, T₁, T₂, ..., Tₙ

STEP 5: Use cross-validation to select best tree
Visual Example
text

ORIGINAL TREE (T₀):
         [A]
        /   \
      [B]   [C]
      / \   / \
     D   E F   G

α₀ = 0, 4 leaves


AFTER PRUNING B (T₁):
         [A]
        /   \
       D    [C]
            / \
           F   G

α₁ = 0.01, 3 leaves


AFTER PRUNING C (T₂):
         [A]
        /   \
       D     F

α₂ = 0.03, 2 leaves


AFTER PRUNING A (T₃):
         [A]

α₃ = 0.10, 1 leaf (root only)


Cross-validation selects T₁ as optimal!
🎯 Reduced Error Pruning (REP)
Simplest post-pruning method:

text

ALGORITHM:

1. Divide data: Training set + Validation set

2. Build full tree using training set

3. For each internal node (bottom-up):
   a. Temporarily replace subtree with leaf
   b. Test on validation set
   c. If accuracy doesn't decrease → Make permanent

4. Repeat until no more pruning improves validation accuracy
Chapter 9: Decision Trees for Regression {#chapter-9-regression}
🔢 From Classification to Regression
Key Differences
text

┌────────────────────┬─────────────────────┬─────────────────────┐
│      Aspect        │   Classification    │     Regression      │
├────────────────────┼─────────────────────┼─────────────────────┤
│  Target Variable   │   Categorical       │   Continuous        │
│                    │   (Yes/No, A/B/C)   │   (1.5, 42.3, etc.) │
├────────────────────┼─────────────────────┼─────────────────────┤
│  Leaf Prediction   │   Most common class │   Mean of targets   │
│                    │   (mode)            │   (average)         │
├────────────────────┼─────────────────────┼─────────────────────┤
│  Split Criterion   │   Gini/Entropy      │   Variance/MSE      │
│                    │   (impurity)        │   reduction         │
├────────────────────┼─────────────────────┼─────────────────────┤
│  Error Measure     │   Misclassification │   MSE, MAE          │
│                    │   rate              │                     │
└────────────────────┴─────────────────────┴─────────────────────┘
📊 How Regression Trees Split
The Goal: Minimize Variance
text

BEFORE SPLIT:
┌─────────────────────────────────────┐
│ Targets: [10, 12, 45, 48, 50, 11]   │
│ Mean: 29.3                          │
│ Variance: VERY HIGH!                │
└─────────────────────────────────────┘

AFTER GOOD SPLIT:
┌──────────────────┐  ┌──────────────────┐
│ [10, 12, 11]     │  │ [45, 48, 50]     │
│ Mean: 11         │  │ Mean: 47.7       │
│ Variance: LOW    │  │ Variance: LOW    │
└──────────────────┘  └──────────────────┘
Splitting Criterion: MSE Reduction
text

For each possible split:

1. Calculate MSE of parent:
   MSE_parent = (1/n) × Σ(yᵢ - ȳ)²

2. Calculate weighted MSE of children:
   MSE_children = (n_left/n)×MSE_left + (n_right/n)×MSE_right

3. Calculate reduction:
   Reduction = MSE_parent - MSE_children

4. Choose split with MAXIMUM reduction
Complete Example
text

Data: Predict house price based on size

Size (sq ft) | Price ($K)
-------------|------------
    1000     |    150
    1200     |    180
    1500     |    200
    2000     |    350
    2200     |    380
    2500     |    400

Try split at Size = 1600:

LEFT (Size ≤ 1600): [150, 180, 200]
    Mean = 176.67
    MSE = [(150-176.67)² + (180-176.67)² + (200-176.67)²] / 3
        = [711.11 + 11.11 + 544.45] / 3
        = 422.22

RIGHT (Size > 1600): [350, 380, 400]
    Mean = 376.67
    MSE = [(350-376.67)² + (380-376.67)² + (400-376.67)²] / 3
        = [711.11 + 11.11 + 544.45] / 3
        = 422.22

Total weighted MSE = (3/6)×422.22 + (3/6)×422.22 = 422.22

Compare with parent MSE:
    All prices: [150, 180, 200, 350, 380, 400]
    Mean = 276.67
    MSE = 9177.78

Reduction = 9177.78 - 422.22 = 8755.56 ← GOOD SPLIT!
🌳 Regression Tree Visualization
text

                    [Size?]
                       │
            ┌──────────┴──────────┐
         ≤ 1600              > 1600
            │                    │
       [Bedrooms?]         [Predict: $377K]
            │
    ┌───────┴───────┐
  ≤ 2            > 2
    │              │
 [$165K]       [$200K]

Prediction is AVERAGE of samples in leaf!
📈 Regression Tree Predictions Are Step Functions
text

Actual relationship:          Regression tree approximation:
                              
Price                         Price
  │       ╱                     │         ┌────────
  │     ╱                       │    ┌────┘
  │   ╱                         │────┘
  │ ╱                           │
  └──────────────→ Size         └──────────────→ Size
  
Smooth curve                   Staircase pattern
Chapter 10: Hyperparameter Tuning {#chapter-10-hyperparameters}
⚙️ Complete Hyperparameter Reference
All Important Hyperparameters
text

┌────────────────────────┬────────────────────┬───────────────────────────────┐
│    Hyperparameter      │  Default (sklearn) │        What It Controls       │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ max_depth              │       None         │ Maximum tree depth            │
│                        │                    │ Lower = simpler tree          │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ min_samples_split      │        2           │ Min samples to split a node   │
│                        │                    │ Higher = simpler tree         │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ min_samples_leaf       │        1           │ Min samples in a leaf node    │
│                        │                    │ Higher = simpler tree         │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ max_features           │       None         │ Features considered per split │
│                        │                    │ Lower = more randomness       │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ max_leaf_nodes         │       None         │ Maximum number of leaves      │
│                        │                    │ Lower = simpler tree          │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ min_impurity_decrease  │       0.0          │ Min impurity decrease to split│
│                        │                    │ Higher = fewer splits         │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ criterion              │      "gini"        │ Split quality measure         │
│                        │                    │ "gini" or "entropy"           │
├────────────────────────┼────────────────────┼───────────────────────────────┤
│ ccp_alpha              │       0.0          │ Complexity for pruning        │
│                        │                    │ Higher = more pruning         │
└────────────────────────┴────────────────────┴───────────────────────────────┘
🎛️ Detailed Parameter Analysis
1. max_depth
text

max_depth = 1:              max_depth = 3:              max_depth = None:
                                
    [Root]                      [Root]                      [Root]
    /    \                     /      \                    /      \
 [Leaf] [Leaf]              [N]      [N]                [N]      [N]
                           /   \    /   \              /  \     /   \
Very simple             [L] [N]  [L] [L]            [N] [N]  [N]  [N]
High bias               /   \                       ... (many more levels)
Low variance          [L]  [L]                      
                                                    Very complex
                      Balanced                      Low bias
                                                    High variance
Recommended: Start with max_depth=3-10, tune with CV

2. min_samples_split
text

min_samples_split = 2 (default):
- Node with 2+ samples can be split
- More splits → Complex tree

min_samples_split = 20:
- Need at least 20 samples to split
- Fewer splits → Simpler tree

EFFECT ON TREE:
                    
min_samples_split=2:    min_samples_split=50:
   Deep tree               Shallow tree
   Many leaves            Few leaves
   May overfit            May underfit
Recommended: 1-5% of total samples

3. min_samples_leaf
text

min_samples_leaf = 1 (default):
- Leaves can have just 1 sample
- May create very specific rules

min_samples_leaf = 10:
- Every leaf needs 10+ samples
- More generalizable

VISUAL:
┌─────────────────────────────────────────┐
│  min_samples_leaf = 1                   │
│  Leaf: [●]  ← Only 1 sample!            │
│  Very specific, might be noise!         │
├─────────────────────────────────────────┤
│  min_samples_leaf = 10                  │
│  Leaf: [●●●●●●●●●●] ← 10 samples        │
│  More reliable prediction!              │
└─────────────────────────────────────────┘
4. max_features
text

max_features options:

None (default) → Consider ALL features at each split
"sqrt"         → Consider √(n_features)
"log2"         → Consider log₂(n_features)
int            → Consider exactly that many features
float          → Consider that fraction of features

WHEN TO USE:
- None: Standard decision tree
- "sqrt": When building Random Forests (adds randomness)
- Specific number: When you have too many features
🔧 Tuning Strategies
Strategy 1: Grid Search
Python

from sklearn.model_selection import GridSearchCV

param_grid = {
    'max_depth': [3, 5, 7, 10, None],
    'min_samples_split': [2, 5, 10, 20],
    'min_samples_leaf': [1, 2, 5, 10],
    'criterion': ['gini', 'entropy']
}

grid_search = GridSearchCV(
    DecisionTreeClassifier(),
    param_grid,
    cv=5,
    scoring='accuracy'
)

grid_search.fit(X_train, y_train)
print(f"Best params: {grid_search.best_params_}")
Strategy 2: Randomized Search
Python

from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint

param_dist = {
    'max_depth': randint(1, 20),
    'min_samples_split': randint(2, 50),
    'min_samples_leaf': randint(1, 20),
}

random_search = RandomizedSearchCV(
    DecisionTreeClassifier(),
    param_dist,
    n_iter=100,  # Try 100 random combinations
    cv=5
)
Strategy 3: Start Simple, Increase Complexity
text

STEP 1: Start with constraints
        max_depth=3, min_samples_leaf=10
        
        → Check performance
        
STEP 2: If underfitting, relax constraints
        max_depth=5, min_samples_leaf=5
        
        → Check performance
        
STEP 3: Keep adjusting until:
        Training accuracy - Test accuracy < 5%
        Test accuracy is acceptable
📊 Hyperparameter Effect Summary
text

Parameter              │ Increase Value → │ Effect on Model
───────────────────────┼──────────────────┼──────────────────
max_depth              │        ↑         │ More complex
min_samples_split      │        ↑         │ Less complex
min_samples_leaf       │        ↑         │ Less complex
max_leaf_nodes         │        ↑         │ More complex
max_features           │        ↑         │ More deterministic
min_impurity_decrease  │        ↑         │ Less complex
ccp_alpha              │        ↑         │ Less complex (more pruning)
Chapter 11: Advantages and Disadvantages {#chapter-11-pros-cons}
✅ Advantages
1. Easy to Understand and Interpret
text

                    [Is it raining?]
                       /        \
                     YES        NO
                     /            \
            [Have umbrella?]    [Go outside!]
               /       \
             YES       NO
              |         |
         [Go outside!] [Stay home]

ANYONE can understand this!
Even non-technical stakeholders.
2. No Feature Scaling Required
text

OTHER ALGORITHMS:              DECISION TREES:

Need normalization:            Works directly:
Age: 0.32 → 32                 Age: 32
Salary: 0.65 → 65000           Salary: 65000
                               
Must be same scale!            Any scale is fine!
3. Handles Both Numerical and Categorical Data
text

NUMERICAL:                     CATEGORICAL:
Age > 30?                      Color = Red?
Income > 50000?                City = "NYC"?

BOTH work seamlessly!
4. No Assumptions About Data Distribution
text

LINEAR REGRESSION:             DECISION TREES:
                               
Assumes: y = mx + b            No assumptions!
         Linear relationship   
         Normal residuals      Works with any
         Homoscedasticity      relationship pattern
5. Feature Importance Built-In
Python

# Automatically tells you which features matter!

feature_importance = tree.feature_importances_

# Output:
# Income: 0.45  ← Most important!
# Age: 0.30
# Education: 0.15
# Gender: 0.10  ← Least important
6. Fast Prediction
text

Time complexity for prediction:

Decision Tree: O(depth)    ← Very fast! Usually O(log n)
Neural Network: O(layers × neurons)  ← Slower

For depth=10 tree:
Just 10 comparisons to make prediction!
7. Can Capture Non-Linear Relationships
text

LINEAR MODEL:                  DECISION TREE:

       y                            y
       │     ╱                      │    ┌──┐
       │   ╱                        │ ┌──┘  └──┐
       │ ╱                          │─┘        └──
       └────────→ x                 └──────────────→ x

Only straight lines!           Can model any pattern!
❌ Disadvantages
1. Prone to Overfitting
text

OVERFITTED TREE:

Creates a rule for EVERY training sample!

Training Accuracy: 100% 🎉
Test Accuracy: 45% 😢

SOLUTION: Pruning, setting max_depth, etc.
2. Unstable - Small Data Changes = Very Different Tree
text

ORIGINAL DATA:                 REMOVE 1 SAMPLE:

    [Age > 30?]                    [Income > 50K?]
      /    \                         /      \
   [A]    [B]                     [X]      [Y]
   
Completely different tree structure!
3. Biased Toward Features with More Levels
text

Feature "ID":     100 unique values → Appears important
Feature "Gender": 2 values (M/F)     → Appears less important

But ID is useless! Just memorization.

SOLUTION: Use Gain Ratio, limit max_features
4. Cannot Extrapolate
text

TRAINING DATA RANGE:           PREDICTION FOR NEW DATA:
                               
Income: $20K - $100K           Income: $150K
                               ↓
                               Prediction = same as $100K!
                               
Decision trees can only predict values
seen during training!
5. Greedy Algorithm - Not Globally Optimal
text

GREEDY APPROACH:

At each step, choose locally best split.
May miss globally optimal tree structure.

Example:
- Best first split: Age
- But if we split on Income first,
  overall tree might be better!

This is computationally necessary
(finding optimal tree is NP-hard)
6. Difficult to Express Certain Relationships
text

XOR PROBLEM:
                  ●(0,1)     ○(1,1)
                  
                  ○(0,0)     ●(1,0)

Requires many splits to capture!
Linear model with feature engineering
might be simpler.
⚖️ Summary Comparison
text

┌─────────────────────────┬───────────────────────┐
│      STRENGTHS          │      WEAKNESSES       │
├─────────────────────────┼───────────────────────┤
│ ✅ Interpretable        │ ❌ Overfits easily    │
│ ✅ No preprocessing     │ ❌ Unstable           │
│ ✅ Fast prediction      │ ❌ Greedy algorithm   │
│ ✅ Handles mixed data   │ ❌ Can't extrapolate  │
│ ✅ Feature importance   │ ❌ Biased features    │
│ ✅ Non-linear patterns  │ ❌ XOR-like problems  │
└─────────────────────────┴───────────────────────┘
Chapter 12: Advanced Variants {#chapter-12-advanced-variants}
🌲 ID3 (Iterative Dichotomiser 3)
Created by: Ross Quinlan, 1986

Key Characteristics:

text

- Uses Information Gain for splitting
- Only handles CATEGORICAL features
- No pruning mechanism
- Creates multi-way splits

EXAMPLE SPLIT:
            [Color?]
         /     |     \
       Red   Green   Blue
Limitations:

Can't handle continuous variables
Biased toward features with many values
No handling of missing values
🌲 C4.5 (Successor of ID3)
Created by: Ross Quinlan, 1993

Improvements over ID3:

text

┌─────────────────────────────────────────────────────────────┐
│  IMPROVEMENT               │  HOW IT WORKS                  │
├─────────────────────────────────────────────────────────────┤
│  Handles continuous        │  Finds threshold, creates      │
│  features                  │  binary split (≤ vs >)         │
├─────────────────────────────────────────────────────────────┤
│  Uses Gain Ratio           │  Penalizes features with       │
│  instead of IG             │  many values                   │
├─────────────────────────────────────────────────────────────┤
│  Handles missing values    │  Uses probability distribution │
│                            │  to handle unknowns            │
├─────────────────────────────────────────────────────────────┤
│  Post-pruning              │  Error-based pruning after     │
│                            │  full tree is built            │
└─────────────────────────────────────────────────────────────┘
🌲 C5.0 (Latest Version)
Improvements over C4.5:

text

- Faster and more memory efficient
- Boosting capabilities
- Supports weighted samples
- Better handling of missing values
- Rule-set generation
🌲 CART (Classification and Regression Trees)
Created by: Breiman et al., 1984

Key Characteristics:

text

┌─────────────────────────────────────────────────────────────┐
│  FEATURE                   │  CART APPROACH                 │
├─────────────────────────────────────────────────────────────┤
│  Split type                │  ALWAYS binary (yes/no)        │
│                            │                                │
│  Classification criterion  │  Gini Impurity (default)       │
│                            │                                │
│  Regression criterion      │  MSE / Variance reduction      │
│                            │                                │
│  Pruning                   │  Cost-complexity pruning       │
│                            │  (minimal cost-complexity)     │
│                            │                                │
│  This is what sklearn      │  ✓ YES!                        │
│  implements                │                                │
└─────────────────────────────────────────────────────────────┘
Binary Split Example:

text

ID3/C4.5:                     CART:
   [Color?]                      [Color = Red?]
  /    |    \                      /        \
Red  Green  Blue               YES           NO
                                |             |
                           [Red]        [Color = Green?]
                                           /        \
                                         YES        NO
                                          |          |
                                       [Green]    [Blue]
🌲 CHAID (Chi-squared Automatic Interaction Detection)
Created by: Kass, 1980

Key Characteristics:

text

- Uses Chi-square test for splitting
- Creates multi-way splits
- Primarily used in marketing research
- Handles categorical features well
- Built-in statistical significance testing
🔄 Comparison Table
text

┌──────────┬────────────┬─────────────┬───────────┬───────────┬───────────┐
│  Aspect  │    ID3     │    C4.5     │   C5.0    │   CART    │   CHAID   │
├──────────┼────────────┼─────────────┼───────────┼───────────┼───────────┤
│ Year     │   1986     │    1993     │   1997    │   1984    │   1980    │
│          │            │             │           │           │           │
│ Split    │  Info Gain │ Gain Ratio  │   Gain    │   Gini    │ Chi-sq    │
│ Measure  │            │             │   Ratio   │           │           │
│          │            │             │           │           │           │
│ Split    │  Multi-way │  Multi-way  │ Multi-way │  Binary   │ Multi-way │
│ Type     │            │             │           │   only    │           │
│          │            │             │           │           │           │
│ Contin-  │     No     │    Yes      │    Yes    │   Yes     │    No     │
│ uous     │            │             │           │           │           │
│          │            │             │           │           │           │
│ Pruning  │     No     │ Post-prune  │   Both    │   CCP     │Pre-prune  │
│          │            │             │           │           │           │
│ Missing  │     No     │    Yes      │    Yes    │ Surrogate │    Yes    │
│ Values   │            │             │           │  splits   │           │
│          │            │             │           │           │           │
│ sklearn  │     No     │     No      │    No     │   YES     │    No     │
└──────────┴────────────┴─────────────┴───────────┴───────────┴───────────┘
Chapter 13: Real-World Implementation {#chapter-13-implementation}
🐍 Complete Python Implementation from Scratch
Python

import numpy as np
from collections import Counter

class DecisionTreeFromScratch:
    """
    A Decision Tree Classifier built from scratch.
    Uses Gini Impurity for splitting.
    """
    
    def __init__(self, max_depth=10, min_samples_split=2, min_samples_leaf=1):
        self.max_depth = max_depth
        self.min_samples_split = min_samples_split
        self.min_samples_leaf = min_samples_leaf
        self.tree = None
    
    def gini_impurity(self, y):
        """Calculate Gini Impurity of a node."""
        if len(y) == 0:
            return 0
        
        counter = Counter(y)
        probabilities = [count / len(y) for count in counter.values()]
        gini = 1 - sum(p**2 for p in probabilities)
        return gini
    
    def information_gain(self, y_parent, y_left, y_right):
        """Calculate information gain from a split."""
        n = len(y_parent)
        n_left, n_right = len(y_left), len(y_right)
        
        if n_left == 0 or n_right == 0:
            return 0
        
        parent_impurity = self.gini_impurity(y_parent)
        child_impurity = (n_left/n) * self.gini_impurity(y_left) + \
                         (n_right/n) * self.gini_impurity(y_right)
        
        return parent_impurity - child_impurity
    
    def best_split(self, X, y):
        """Find the best feature and threshold for splitting."""
        best_gain = -1
        best_feature = None
        best_threshold = None
        
        n_features = X.shape[1]
        
        for feature_idx in range(n_features):
            # Get unique values as potential thresholds
            thresholds = np.unique(X[:, feature_idx])
            
            for threshold in thresholds:
                # Split data
                left_mask = X[:, feature_idx] <= threshold
                right_mask = ~left_mask
                
                if sum(left_mask) < self.min_samples_leaf or \
                   sum(right_mask) < self.min_samples_leaf:
                    continue
                
                # Calculate gain
                gain = self.information_gain(y, y[left_mask], y[right_mask])
                
                if gain > best_gain:
                    best_gain = gain
                    best_feature = feature_idx
                    best_threshold = threshold
        
        return best_feature, best_threshold, best_gain
    
    def build_tree(self, X, y, depth=0):
        """Recursively build the decision tree."""
        n_samples, n_features = X.shape
        n_classes = len(np.unique(y))
        
        # Stopping conditions
        if (depth >= self.max_depth or 
            n_classes == 1 or 
            n_samples < self.min_samples_split):
            # Create leaf node
            leaf_value = Counter(y).most_common(1)[0][0]
            return {'type': 'leaf', 'value': leaf_value, 'samples': n_samples}
        
        # Find best split
        best_feature, best_threshold, best_gain = self.best_split(X, y)
        
        if best_gain <= 0:
            leaf_value = Counter(y).most_common(1)[0][0]
            return {'type': 'leaf', 'value': leaf_value, 'samples': n_samples}
        
        # Split data
        left_mask = X[:, best_feature] <= best_threshold
        right_mask = ~left_mask
        
        # Build subtrees
        left_subtree = self.build_tree(X[left_mask], y[left_mask], depth + 1)
        right_subtree = self.build_tree(X[right_mask], y[right_mask], depth + 1)
        
        return {
            'type': 'node',
            'feature': best_feature,
            'threshold': best_threshold,
            'left': left_subtree,
            'right': right_subtree,
            'gain': best_gain,
            'samples': n_samples
        }
    
    def fit(self, X, y):
        """Train the decision tree."""
        self.tree = self.build_tree(np.array(X), np.array(y))
        return self
    
    def predict_sample(self, x, node):
        """Predict class for a single sample."""
        if node['type'] == 'leaf':
            return node['value']
        
        if x[node['feature']] <= node['threshold']:
            return self.predict_sample(x, node['left'])
        else:
            return self.predict_sample(x, node['right'])
    
    def predict(self, X):
        """Predict classes for all samples."""
        return np.array([self.predict_sample(x, self.tree) for x in np.array(X)])
    
    def print_tree(self, node=None, indent=""):
        """Print the tree structure."""
        if node is None:
            node = self.tree
        
        if node['type'] == 'leaf':
            print(f"{indent}Leaf: class={node['value']}, samples={node['samples']}")
        else:
            print(f"{indent}Node: feature[{node['feature']}] <= {node['threshold']:.2f}")
            print(f"{indent}  ├── Left:")
            self.print_tree(node['left'], indent + "  │   ")
            print(f"{indent}  └── Right:")
            self.print_tree(node['right'], indent + "      ")


# ═══════════════════════════════════════════════════════════════
# USAGE EXAMPLE
# ═══════════════════════════════════════════════════════════════

if __name__ == "__main__":
    # Create sample data
    from sklearn.datasets import make_classification
    from sklearn.model_selection import train_test_split
    
    X, y = make_classification(n_samples=1000, n_features=4, 
                               n_informative=3, random_state=42)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
    
    # Train our tree
    tree = DecisionTreeFromScratch(max_depth=5)
    tree.fit(X_train, y_train)
    
    # Predictions
    predictions = tree.predict(X_test)
    accuracy = np.mean(predictions == y_test)
    print(f"Accuracy: {accuracy:.2%}")
    
    # Print tree structure
    tree.print_tree()
📚 Scikit-Learn Complete Example
Python

# ═══════════════════════════════════════════════════════════════
# COMPLETE SCIKIT-LEARN WORKFLOW
# ═══════════════════════════════════════════════════════════════

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, DecisionTreeRegressor
from sklearn.tree import plot_tree, export_text
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
from sklearn.datasets import load_iris, load_wine

# ───────────────────────────────────────────────────────────────
# 1. LOAD AND PREPARE DATA
# ───────────────────────────────────────────────────────────────

# Load iris dataset
iris = load_iris()
X = iris.data
y = iris.target
feature_names = iris.feature_names
class_names = iris.target_names

print("Dataset shape:", X.shape)
print("Features:", feature_names)
print("Classes:", class_names)

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining samples: {len(X_train)}")
print(f"Test samples: {len(X_test)}")

# ───────────────────────────────────────────────────────────────
# 2. TRAIN BASIC MODEL
# ───────────────────────────────────────────────────────────────

# Create and train model
clf = DecisionTreeClassifier(
    criterion='gini',           # 'gini' or 'entropy'
    max_depth=4,               # Maximum depth
    min_samples_split=5,       # Min samples to split
    min_samples_leaf=2,        # Min samples in leaf
    random_state=42
)

clf.fit(X_train, y_train)

# ───────────────────────────────────────────────────────────────
# 3. EVALUATE MODEL
# ───────────────────────────────────────────────────────────────

# Training accuracy
train_predictions = clf.predict(X_train)
train_accuracy = accuracy_score(y_train, train_predictions)
print(f"\nTraining Accuracy: {train_accuracy:.2%}")

# Test accuracy
test_predictions = clf.predict(X_test)
test_accuracy = accuracy_score(y_test, test_predictions)
print(f"Test Accuracy: {test_accuracy:.2%}")

# Cross-validation
cv_scores = cross_val_score(clf, X, y, cv=5)
print(f"Cross-Validation Accuracy: {cv_scores.mean():.2%} (+/- {cv_scores.std()*2:.2%})")

# Classification report
print("\nClassification Report:")
print(classification_report(y_test, test_predictions, target_names=class_names))

# Confusion matrix
print("Confusion Matrix:")
print(confusion_matrix(y_test, test_predictions))

# ───────────────────────────────────────────────────────────────
# 4. VISUALIZE THE TREE (Continued)
# ───────────────────────────────────────────────────────────────

# Method 1: Plot tree
plt.figure(figsize=(20, 10))
plot_tree(
    clf,
    feature_names=feature_names,
    class_names=class_names,
    filled=True,           # Color nodes by class
    rounded=True,          # Rounded boxes
    fontsize=10
)
plt.title("Decision Tree Visualization")
plt.tight_layout()
plt.savefig("decision_tree.png", dpi=300)
plt.show()

# Method 2: Text representation
tree_rules = export_text(clf, feature_names=list(feature_names))
print("\nTree Rules:")
print(tree_rules)

# ───────────────────────────────────────────────────────────────
# 5. FEATURE IMPORTANCE
# ───────────────────────────────────────────────────────────────

# Get feature importances
importances = clf.feature_importances_
indices = np.argsort(importances)[::-1]

print("\nFeature Importances:")
for i, idx in enumerate(indices):
    print(f"  {i+1}. {feature_names[idx]}: {importances[idx]:.4f}")

# Plot feature importances
plt.figure(figsize=(10, 6))
plt.bar(range(len(importances)), importances[indices], align='center')
plt.xticks(range(len(importances)), [feature_names[i] for i in indices], rotation=45)
plt.xlabel('Features')
plt.ylabel('Importance')
plt.title('Feature Importances')
plt.tight_layout()
plt.show()

# ───────────────────────────────────────────────────────────────
# 6. HYPERPARAMETER TUNING WITH GRID SEARCH
# ───────────────────────────────────────────────────────────────

# Define parameter grid
param_grid = {
    'criterion': ['gini', 'entropy'],
    'max_depth': [2, 3, 4, 5, 6, 7, 8, None],
    'min_samples_split': [2, 5, 10, 15, 20],
    'min_samples_leaf': [1, 2, 5, 10],
    'max_features': [None, 'sqrt', 'log2']
}

# Perform grid search
grid_search = GridSearchCV(
    DecisionTreeClassifier(random_state=42),
    param_grid,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,           # Use all CPU cores
    verbose=1
)

grid_search.fit(X_train, y_train)

print("\nBest Parameters:", grid_search.best_params_)
print("Best CV Score:", f"{grid_search.best_score_:.2%}")

# Use best model
best_clf = grid_search.best_estimator_
best_test_accuracy = accuracy_score(y_test, best_clf.predict(X_test))
print(f"Best Model Test Accuracy: {best_test_accuracy:.2%}")

# ───────────────────────────────────────────────────────────────
# 7. COST COMPLEXITY PRUNING
# ───────────────────────────────────────────────────────────────

# Get cost complexity pruning path
path = clf.cost_complexity_pruning_path(X_train, y_train)
ccp_alphas = path.ccp_alphas
impurities = path.impurities

print(f"\nNumber of alpha values: {len(ccp_alphas)}")

# Train trees with different alpha values
clfs = []
for ccp_alpha in ccp_alphas:
    clf_temp = DecisionTreeClassifier(random_state=42, ccp_alpha=ccp_alpha)
    clf_temp.fit(X_train, y_train)
    clfs.append(clf_temp)

# Calculate accuracy for each tree
train_scores = [accuracy_score(y_train, clf.predict(X_train)) for clf in clfs]
test_scores = [accuracy_score(y_test, clf.predict(X_test)) for clf in clfs]

# Plot accuracy vs alpha
plt.figure(figsize=(10, 6))
plt.plot(ccp_alphas, train_scores, marker='o', label='Training')
plt.plot(ccp_alphas, test_scores, marker='o', label='Test')
plt.xlabel('Cost Complexity Parameter (alpha)')
plt.ylabel('Accuracy')
plt.title('Accuracy vs Alpha for Cost Complexity Pruning')
plt.legend()
plt.grid(True)
plt.show()

# Find optimal alpha
best_idx = np.argmax(test_scores)
best_alpha = ccp_alphas[best_idx]
print(f"\nOptimal alpha: {best_alpha:.6f}")
print(f"Optimal test accuracy: {test_scores[best_idx]:.2%}")

# ───────────────────────────────────────────────────────────────
# 8. DECISION BOUNDARY VISUALIZATION (2D)
# ───────────────────────────────────────────────────────────────

# Use only 2 features for visualization
X_2d = X[:, :2]  # First two features
X_train_2d, X_test_2d, y_train_2d, y_test_2d = train_test_split(
    X_2d, y, test_size=0.2, random_state=42
)

# Train model on 2D data
clf_2d = DecisionTreeClassifier(max_depth=4, random_state=42)
clf_2d.fit(X_train_2d, y_train_2d)

# Create mesh grid
x_min, x_max = X_2d[:, 0].min() - 1, X_2d[:, 0].max() + 1
y_min, y_max = X_2d[:, 1].min() - 1, X_2d[:, 1].max() + 1
xx, yy = np.meshgrid(np.arange(x_min, x_max, 0.02),
                     np.arange(y_min, y_max, 0.02))

# Predict on mesh grid
Z = clf_2d.predict(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)

# Plot decision boundary
plt.figure(figsize=(12, 8))
plt.contourf(xx, yy, Z, alpha=0.4, cmap=plt.cm.RdYlBu)
scatter = plt.scatter(X_2d[:, 0], X_2d[:, 1], c=y, cmap=plt.cm.RdYlBu, edgecolors='black')
plt.xlabel(feature_names[0])
plt.ylabel(feature_names[1])
plt.title('Decision Tree Decision Boundaries')
plt.colorbar(scatter)
plt.show()

# ───────────────────────────────────────────────────────────────
# 9. REGRESSION TREE EXAMPLE
# ───────────────────────────────────────────────────────────────

from sklearn.datasets import make_regression
from sklearn.metrics import mean_squared_error, r2_score

# Create regression data
X_reg, y_reg = make_regression(n_samples=500, n_features=5, noise=10, random_state=42)
X_train_reg, X_test_reg, y_train_reg, y_test_reg = train_test_split(
    X_reg, y_reg, test_size=0.2, random_state=42
)

# Train regression tree
reg_tree = DecisionTreeRegressor(
    max_depth=5,
    min_samples_split=10,
    min_samples_leaf=5,
    random_state=42
)
reg_tree.fit(X_train_reg, y_train_reg)

# Predictions
y_pred_reg = reg_tree.predict(X_test_reg)

# Evaluate
mse = mean_squared_error(y_test_reg, y_pred_reg)
rmse = np.sqrt(mse)
r2 = r2_score(y_test_reg, y_pred_reg)

print("\nRegression Tree Results:")
print(f"  MSE: {mse:.2f}")
print(f"  RMSE: {rmse:.2f}")
print(f"  R² Score: {r2:.4f}")

# Plot actual vs predicted
plt.figure(figsize=(10, 6))
plt.scatter(y_test_reg, y_pred_reg, alpha=0.5)
plt.plot([y_test_reg.min(), y_test_reg.max()], 
         [y_test_reg.min(), y_test_reg.max()], 'r--', lw=2)
plt.xlabel('Actual Values')
plt.ylabel('Predicted Values')
plt.title('Regression Tree: Actual vs Predicted')
plt.tight_layout()
plt.show()

# ───────────────────────────────────────────────────────────────
# 10. SAVING AND LOADING MODELS
# ───────────────────────────────────────────────────────────────

import joblib
import pickle

# Method 1: Using joblib (recommended for sklearn)
joblib.dump(clf, 'decision_tree_model.joblib')
loaded_clf_joblib = joblib.load('decision_tree_model.joblib')

# Method 2: Using pickle
with open('decision_tree_model.pkl', 'wb') as f:
    pickle.dump(clf, f)

with open('decision_tree_model.pkl', 'rb') as f:
    loaded_clf_pickle = pickle.load(f)

# Verify loaded model works
print("\nLoaded model prediction:", loaded_clf_joblib.predict(X_test[:5]))
print("Original model prediction:", clf.predict(X_test[:5]))
🎯 Real-World Project: Customer Churn Prediction
Python

# ═══════════════════════════════════════════════════════════════
# COMPLETE PROJECT: CUSTOMER CHURN PREDICTION
# ═══════════════════════════════════════════════════════════════

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import (accuracy_score, precision_score, recall_score, 
                             f1_score, confusion_matrix, classification_report,
                             roc_auc_score, roc_curve)
from sklearn.preprocessing import LabelEncoder

# ───────────────────────────────────────────────────────────────
# STEP 1: CREATE SAMPLE DATA (In real project, load your data)
# ───────────────────────────────────────────────────────────────

np.random.seed(42)
n_samples = 1000

data = {
    'customer_id': range(1, n_samples + 1),
    'age': np.random.randint(18, 70, n_samples),
    'gender': np.random.choice(['Male', 'Female'], n_samples),
    'tenure_months': np.random.randint(1, 72, n_samples),
    'monthly_charges': np.random.uniform(20, 100, n_samples),
    'total_charges': np.random.uniform(100, 5000, n_samples),
    'contract_type': np.random.choice(['Month-to-month', 'One year', 'Two year'], n_samples),
    'payment_method': np.random.choice(['Credit card', 'Bank transfer', 'Electronic check'], n_samples),
    'num_support_tickets': np.random.randint(0, 10, n_samples),
    'num_referrals': np.random.randint(0, 5, n_samples),
}

# Create target variable with some logic
churn_prob = (
    (data['tenure_months'] < 12).astype(float) * 0.3 +
    (data['num_support_tickets'] > 5).astype(float) * 0.25 +
    (np.array(data['contract_type']) == 'Month-to-month').astype(float) * 0.2 +
    np.random.uniform(0, 0.25, n_samples)
)
data['churn'] = (churn_prob > 0.5).astype(int)

df = pd.DataFrame(data)

print("Dataset Shape:", df.shape)
print("\nFirst 5 rows:")
print(df.head())
print("\nChurn Distribution:")
print(df['churn'].value_counts(normalize=True))

# ───────────────────────────────────────────────────────────────
# STEP 2: DATA PREPROCESSING
# ───────────────────────────────────────────────────────────────

# Encode categorical variables
label_encoders = {}
categorical_columns = ['gender', 'contract_type', 'payment_method']

for col in categorical_columns:
    le = LabelEncoder()
    df[col + '_encoded'] = le.fit_transform(df[col])
    label_encoders[col] = le

# Select features
feature_columns = [
    'age', 'tenure_months', 'monthly_charges', 'total_charges',
    'num_support_tickets', 'num_referrals',
    'gender_encoded', 'contract_type_encoded', 'payment_method_encoded'
]

X = df[feature_columns]
y = df['churn']

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining set size: {len(X_train)}")
print(f"Test set size: {len(X_test)}")

# ───────────────────────────────────────────────────────────────
# STEP 3: BUILD AND TRAIN MODEL
# ───────────────────────────────────────────────────────────────

# Create decision tree classifier
churn_model = DecisionTreeClassifier(
    criterion='gini',
    max_depth=5,
    min_samples_split=20,
    min_samples_leaf=10,
    class_weight='balanced',  # Handle imbalanced classes
    random_state=42
)

# Train model
churn_model.fit(X_train, y_train)

# ───────────────────────────────────────────────────────────────
# STEP 4: EVALUATE MODEL
# ───────────────────────────────────────────────────────────────

# Predictions
y_train_pred = churn_model.predict(X_train)
y_test_pred = churn_model.predict(X_test)
y_test_prob = churn_model.predict_proba(X_test)[:, 1]

# Calculate metrics
print("\n" + "="*60)
print("MODEL EVALUATION RESULTS")
print("="*60)

print("\n📊 ACCURACY:")
print(f"  Training Accuracy: {accuracy_score(y_train, y_train_pred):.2%}")
print(f"  Test Accuracy: {accuracy_score(y_test, y_test_pred):.2%}")

print("\n📊 CLASSIFICATION METRICS (Test Set):")
print(f"  Precision: {precision_score(y_test, y_test_pred):.2%}")
print(f"  Recall: {recall_score(y_test, y_test_pred):.2%}")
print(f"  F1-Score: {f1_score(y_test, y_test_pred):.2%}")
print(f"  ROC-AUC: {roc_auc_score(y_test, y_test_prob):.4f}")

print("\n📊 CROSS-VALIDATION (5-Fold):")
cv_scores = cross_val_score(churn_model, X, y, cv=5, scoring='accuracy')
print(f"  Mean CV Accuracy: {cv_scores.mean():.2%} (+/- {cv_scores.std()*2:.2%})")

print("\n📊 CLASSIFICATION REPORT:")
print(classification_report(y_test, y_test_pred, target_names=['No Churn', 'Churn']))

# ───────────────────────────────────────────────────────────────
# STEP 5: VISUALIZATIONS
# ───────────────────────────────────────────────────────────────

fig, axes = plt.subplots(2, 2, figsize=(16, 14))

# 1. Confusion Matrix
cm = confusion_matrix(y_test, y_test_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', ax=axes[0, 0])
axes[0, 0].set_xlabel('Predicted')
axes[0, 0].set_ylabel('Actual')
axes[0, 0].set_title('Confusion Matrix')
axes[0, 0].set_xticklabels(['No Churn', 'Churn'])
axes[0, 0].set_yticklabels(['No Churn', 'Churn'])

# 2. Feature Importance
importances = churn_model.feature_importances_
indices = np.argsort(importances)[::-1]
axes[0, 1].barh(range(len(importances)), importances[indices])
axes[0, 1].set_yticks(range(len(importances)))
axes[0, 1].set_yticklabels([feature_columns[i] for i in indices])
axes[0, 1].set_xlabel('Importance')
axes[0, 1].set_title('Feature Importances')
axes[0, 1].invert_yaxis()

# 3. ROC Curve
fpr, tpr, thresholds = roc_curve(y_test, y_test_prob)
axes[1, 0].plot(fpr, tpr, 'b-', linewidth=2, 
                label=f'ROC Curve (AUC = {roc_auc_score(y_test, y_test_prob):.3f})')
axes[1, 0].plot([0, 1], [0, 1], 'k--', linewidth=1)
axes[1, 0].set_xlabel('False Positive Rate')
axes[1, 0].set_ylabel('True Positive Rate')
axes[1, 0].set_title('ROC Curve')
axes[1, 0].legend(loc='lower right')
axes[1, 0].grid(True, alpha=0.3)

# 4. Prediction Distribution
axes[1, 1].hist(y_test_prob[y_test == 0], bins=20, alpha=0.5, label='No Churn', color='green')
axes[1, 1].hist(y_test_prob[y_test == 1], bins=20, alpha=0.5, label='Churn', color='red')
axes[1, 1].set_xlabel('Predicted Probability of Churn')
axes[1, 1].set_ylabel('Frequency')
axes[1, 1].set_title('Distribution of Predicted Probabilities')
axes[1, 1].legend()

plt.tight_layout()
plt.savefig('churn_model_evaluation.png', dpi=300)
plt.show()

# ───────────────────────────────────────────────────────────────
# STEP 6: VISUALIZE THE DECISION TREE
# ───────────────────────────────────────────────────────────────

plt.figure(figsize=(25, 15))
plot_tree(
    churn_model,
    feature_names=feature_columns,
    class_names=['No Churn', 'Churn'],
    filled=True,
    rounded=True,
    fontsize=9
)
plt.title('Customer Churn Decision Tree', fontsize=16)
plt.tight_layout()
plt.savefig('churn_decision_tree.png', dpi=300)
plt.show()

# ───────────────────────────────────────────────────────────────
# STEP 7: EXTRACT BUSINESS RULES
# ───────────────────────────────────────────────────────────────

from sklearn.tree import export_text

print("\n" + "="*60)
print("DECISION RULES (Business Interpretation)")
print("="*60)
rules = export_text(churn_model, feature_names=feature_columns)
print(rules)

# ───────────────────────────────────────────────────────────────
# STEP 8: MAKE PREDICTIONS FOR NEW CUSTOMERS
# ───────────────────────────────────────────────────────────────

def predict_churn(customer_data):
    """
    Predict churn probability for a new customer.
    
    Parameters:
    -----------
    customer_data : dict
        Customer attributes
        
    Returns:
    --------
    dict : Prediction results
    """
    # Encode categorical variables
    customer_encoded = customer_data.copy()
    for col in categorical_columns:
        if col in customer_data:
            customer_encoded[col + '_encoded'] = label_encoders[col].transform([customer_data[col]])[0]
    
    # Create feature vector
    features = [customer_encoded.get(col, 0) for col in feature_columns]
    features_array = np.array(features).reshape(1, -1)
    
    # Predict
    prediction = churn_model.predict(features_array)[0]
    probability = churn_model.predict_proba(features_array)[0]
    
    return {
        'prediction': 'CHURN' if prediction == 1 else 'NO CHURN',
        'churn_probability': f"{probability[1]:.2%}",
        'no_churn_probability': f"{probability[0]:.2%}",
        'risk_level': 'HIGH' if probability[1] > 0.7 else ('MEDIUM' if probability[1] > 0.3 else 'LOW')
    }

# Example prediction
new_customer = {
    'age': 25,
    'tenure_months': 3,
    'monthly_charges': 85.0,
    'total_charges': 255.0,
    'num_support_tickets': 7,
    'num_referrals': 0,
    'gender': 'Male',
    'contract_type': 'Month-to-month',
    'payment_method': 'Electronic check'
}

result = predict_churn(new_customer)

print("\n" + "="*60)
print("SAMPLE PREDICTION")
print("="*60)
print(f"Customer Profile: {new_customer}")
print(f"\nPrediction: {result['prediction']}")
print(f"Churn Probability: {result['churn_probability']}")
print(f"Risk Level: {result['risk_level']}")
Chapter 14: Interview Questions & Answers {#chapter-14-interview}
🎯 Basic Level Questions
Q1: What is a Decision Tree?
text

ANSWER:

A Decision Tree is a supervised machine learning algorithm that:

1. Makes predictions by asking a sequence of questions
2. Splits data based on feature values
3. Creates a tree-like structure of decisions
4. Can be used for both classification and regression

VISUAL:
                [Is it sunny?]
                   /        \
                 YES        NO
                 /            \
         [Temperature > 25°C?]  [Go Outside]
            /          \
         YES           NO
          |             |
    [Go Swimming]  [Go for Walk]

KEY POINTS TO MENTION:
- Mimics human decision-making
- Easy to interpret and visualize
- Non-parametric (no assumptions about data)
- Greedy algorithm (locally optimal splits)
Q2: What is the difference between Gini Impurity and Entropy?
text

ANSWER:

┌─────────────────────────────────────────────────────────────────┐
│                    GINI IMPURITY vs ENTROPY                     │
├─────────────────┬───────────────────────┬───────────────────────┤
│     Aspect      │    Gini Impurity      │       Entropy         │
├─────────────────┼───────────────────────┼───────────────────────┤
│    Formula      │  1 - Σ(pᵢ)²           │  -Σ pᵢ × log₂(pᵢ)    │
├─────────────────┼───────────────────────┼───────────────────────┤
│    Range        │  0 to 0.5 (binary)    │  0 to 1 (binary)      │
├─────────────────┼───────────────────────┼───────────────────────┤
│   Computation   │  Faster (no log)      │  Slower (uses log)    │
├─────────────────┼───────────────────────┼───────────────────────┤
│  Interpretation │  Probability of       │  Information/bits     │
│                 │  misclassification    │  needed to encode     │
├─────────────────┼───────────────────────┼───────────────────────┤
│   In Practice   │  Very similar results │  Very similar results │
├─────────────────┼───────────────────────┼───────────────────────┤
│   Default in    │  Scikit-learn         │  ID3, C4.5 algorithms │
└─────────────────┴───────────────────────┴───────────────────────┘

EXAMPLE CALCULATION:
For a node with 70% Class A, 30% Class B:

Gini = 1 - (0.7)² - (0.3)² = 1 - 0.49 - 0.09 = 0.42

Entropy = -(0.7 × log₂(0.7)) - (0.3 × log₂(0.3))
        = -(0.7 × -0.515) - (0.3 × -1.737)
        = 0.361 + 0.521 = 0.882

WHEN TO USE WHICH:
- Gini: Faster computation, good for large datasets
- Entropy: When you want to understand information theory aspect
- In practice: Results are usually very similar
Q3: What is Information Gain?
text

ANSWER:

Information Gain measures the REDUCTION in entropy (uncertainty) 
achieved by splitting the data on a particular feature.

FORMULA:
Information Gain = Entropy(Parent) - Weighted_Avg_Entropy(Children)

IG(S, A) = H(S) - Σ (|Sᵥ|/|S|) × H(Sᵥ)

Where:
- H(S) = Entropy of parent node
- Sᵥ = Subset of S for feature value v
- |Sᵥ|/|S| = Weight (proportion of samples)

EXAMPLE:
Parent: [9 Yes, 5 No] → H = 0.940
After split on "Outlook":
- Sunny: [2 Yes, 3 No] → H = 0.971
- Overcast: [4 Yes, 0 No] → H = 0 (pure!)
- Rainy: [3 Yes, 2 No] → H = 0.971

Weighted Entropy = (5/14)×0.971 + (4/14)×0 + (5/14)×0.971 = 0.694

Information Gain = 0.940 - 0.694 = 0.246

INTERPRETATION:
- Higher IG = Better split
- We choose the feature with highest IG
Q4: What is Pruning? Why is it needed?
text

ANSWER:

WHAT IS PRUNING?
Pruning is the process of removing parts of the tree that don't
improve predictive accuracy on unseen data.

WHY IS IT NEEDED?
┌─────────────────────────────────────────────────────────────────┐
│  PROBLEM: Without pruning, trees can OVERFIT                    │
│                                                                 │
│  Unpruned tree:           Pruned tree:                          │
│  - Very deep              - Appropriate depth                   │
│  - Many leaves            - Fewer leaves                        │
│  - Train acc: 100%        - Train acc: 92%                      │
│  - Test acc: 65%          - Test acc: 88%                       │
│    ↑ OVERFIT!               ↑ BETTER GENERALIZATION!            │
└─────────────────────────────────────────────────────────────────┘

TWO TYPES:

1. PRE-PRUNING (Early Stopping):
   - Stop growing before overfitting
   - Parameters: max_depth, min_samples_split, min_samples_leaf
   
2. POST-PRUNING:
   - Grow full tree, then cut back
   - Methods: Reduced Error Pruning, Cost Complexity Pruning
Q5: How does a Decision Tree handle missing values?
text

ANSWER:

Different algorithms handle missing values differently:

┌─────────────────┬────────────────────────────────────────────────┐
│   Algorithm     │              Missing Value Handling             │
├─────────────────┼────────────────────────────────────────────────┤
│    ID3          │  Does NOT handle - requires preprocessing      │
├─────────────────┼────────────────────────────────────────────────┤
│    C4.5         │  Uses fractional instances                     │
│                 │  - Distributes sample across all branches      │
│                 │  - Uses probability weighting                  │
├─────────────────┼────────────────────────────────────────────────┤
│    CART         │  Uses SURROGATE SPLITS                         │
│                 │  - Finds alternative features that             │
│                 │    approximate the primary split               │
│                 │  - If primary feature missing, use surrogate   │
├─────────────────┼────────────────────────────────────────────────┤
│  Scikit-learn   │  Does NOT handle by default                    │
│                 │  - Must impute before training                 │
│                 │  - Or use HistGradientBoosting (handles NaN)   │
└─────────────────┴────────────────────────────────────────────────┘

COMMON PREPROCESSING STRATEGIES:
1. Remove rows with missing values
2. Impute with mean/median (numerical)
3. Impute with mode (categorical)
4. Create "Missing" category
5. Use algorithms that handle missing values natively
🎯 Intermediate Level Questions
Q6: Explain the CART algorithm.
text

ANSWER:

CART = Classification And Regression Trees

KEY CHARACTERISTICS:

1. BINARY SPLITS ONLY
   - Every split creates exactly 2 child nodes
   - "Feature X ≤ threshold" vs "Feature X > threshold"

2. SPLITTING CRITERIA
   - Classification: Gini Impurity (default)
   - Regression: MSE (Mean Squared Error)

3. PRUNING
   - Uses Cost Complexity Pruning (CCP)
   - Rα(T) = R(T) + α|T̃|
   - α is tuned via cross-validation

4. HANDLES BOTH TYPES
   - Classification: Predicts class labels
   - Regression: Predicts continuous values

ALGORITHM STEPS:
┌─────────────────────────────────────────────────────────────────┐
│ 1. Start with all data in root node                            │
│                                                                 │
│ 2. For each feature:                                            │
│    a. Sort values                                               │
│    b. Try all possible thresholds                               │
│    c. Calculate Gini/MSE reduction for each                     │
│                                                                 │
│ 3. Select feature + threshold with best reduction               │
│                                                                 │
│ 4. Split data into two child nodes                              │
│                                                                 │
│ 5. Recursively apply steps 2-4 to each child                    │
│                                                                 │
│ 6. Stop when:                                                   │
│    - Node is pure                                               │
│    - Max depth reached                                          │
│    - Min samples not met                                        │
│                                                                 │
│ 7. Apply post-pruning if needed                                 │
└─────────────────────────────────────────────────────────────────┘

WHY SKLEARN USES CART:
- Simple and elegant
- Works for both classification and regression
- Efficient implementation
- Well-understood mathematically
Q7: What is Cost Complexity Pruning?
text

ANSWER:

Cost Complexity Pruning (CCP) balances tree accuracy with simplicity.

THE FORMULA:
Rα(T) = R(T) + α × |T̃|

Where:
- Rα(T) = Total cost of tree T
- R(T) = Misclassification rate (or MSE for regression)
- α = Complexity parameter (alpha)
- |T̃| = Number of leaf nodes

HOW IT WORKS:

Step 1: Build full tree T₀

Step 2: For each internal node t, calculate effective α:
        g(t) = [R(t) - R(Tₜ)] / [|T̃ₜ| - 1]
        
        Where:
        - R(t) = error if node t becomes leaf
        - R(Tₜ) = error of subtree rooted at t
        - |T̃ₜ| = leaves in subtree

Step 3: Prune node with smallest g(t)
        Create sequence: T₀ → T₁ → T₂ → ... → Tₙ (root only)

Step 4: Use cross-validation to select best α

INTUITION:
α = 0:    No penalty → Full tree (overfit)
α = ∞:    Huge penalty → Single node (underfit)
α = optimal: Right balance!

IN SCIKIT-LEARN:
```python
clf = DecisionTreeClassifier(ccp_alpha=0.01)
# Higher ccp_alpha = more pruning
text


### Q8: How do you handle imbalanced classes in Decision Trees?
ANSWER:

PROBLEM:
If 95% samples are Class A, 5% are Class B:

Tree might always predict Class A
Gets 95% accuracy but misses all Class B!
SOLUTIONS:

CLASS WEIGHTS

Python

# Automatically balance
clf = DecisionTreeClassifier(class_weight='balanced')

# Custom weights
clf = DecisionTreeClassifier(class_weight={0: 1, 1: 10})
Effect: Minority class samples count more in split calculations

RESAMPLING

Oversampling minority: Undersampling majority:
A A A A A A A A A A A A A A A
B B → B B B B B B B B B B

SMOTE (generates synthetic samples):
Creates new minority samples between existing ones

USE APPROPRIATE METRICS

DON'T use: DO use:

Accuracy - Precision
- Recall
- F1-Score
- ROC-AUC
- PR-AUC
ENSEMBLE METHODS

Random Forest with class_weight
Balanced Bagging
EasyEnsemble, RUSBoost
THRESHOLD ADJUSTMENT

Python

# Instead of default 0.5 threshold
y_prob = clf.predict_proba(X_test)[:, 1]
y_pred = (y_prob > 0.3).astype(int)  # Lower threshold
text


### Q9: What are the differences between ID3, C4.5, and CART?
ANSWER:

┌─────────────┬───────────────┬───────────────┬───────────────┐
│ Aspect │ ID3 │ C4.5 │ CART │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Year │ 1986 │ 1993 │ 1984 │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Creator │ Quinlan │ Quinlan │ Breiman │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Split │ Information │ Gain Ratio │ Gini │
│ Measure │ Gain │ │ Impurity │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Split │ Multi-way │ Multi-way │ Binary only │
│ Type │ (per value) │ (per value) │ (yes/no) │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Continuous │ No │ Yes │ Yes │
│ Features │ (discrete │ (threshold) │ (threshold) │
│ │ only) │ │ │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Missing │ No │ Yes │ Yes │
│ Values │ │ (fractional) │ (surrogate) │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Pruning │ No │ Post-pruning │ CCP │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ Regression │ No │ No │ Yes │
├─────────────┼───────────────┼───────────────┼───────────────┤
│ sklearn? │ No │ No │ YES │
└─────────────┴───────────────┴───────────────┴───────────────┘

EXAMPLE OF SPLIT TYPES:

ID3/C4.5 (Multi-way): CART (Binary):
[Color?] [Color = Red?]
/ | \ /
Red Green Blue YES NO
| |
[Red] [Color = Green?]
/
YES NO

text


### Q10: Can Decision Trees be used for multi-output problems?
ANSWER:

YES! Decision Trees can predict multiple targets simultaneously.

TYPES:

MULTI-OUTPUT CLASSIFICATION

Multiple class labels per sample
Example: Image has [cat, outdoor, sunny]
MULTI-OUTPUT REGRESSION

Multiple continuous targets per sample
Example: Predict [temperature, humidity, wind_speed]
HOW IT WORKS:

Tree structure remains the same
Each leaf stores multiple predictions
Splitting considers all targets together
SCIKIT-LEARN IMPLEMENTATION:

Python

from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_multilabel_classification

# Generate multi-label data
X, y = make_multilabel_classification(n_samples=1000, n_features=10,
                                       n_classes=5, n_labels=2)

# Train single tree for multiple outputs
clf = DecisionTreeClassifier()
clf.fit(X, y)

# Predictions shape: (n_samples, n_outputs)
predictions = clf.predict(X_test)
print(predictions.shape)  # (200, 5)
IMPURITY CALCULATION:

Compute impurity for each output
Aggregate (usually average) across outputs
Split to minimize total impurity
text


---

## 🎯 Advanced Level Questions

### Q11: Explain the mathematics behind finding optimal split thresholds for continuous variables.
ANSWER:

For continuous features, we need to find the optimal threshold.

ALGORITHM:

Step 1: Sort feature values
x₁ ≤ x₂ ≤ x₃ ≤ ... ≤ xₙ

Step 2: Consider midpoints as candidate thresholds
t₁ = (x₁ + x₂)/2
t₂ = (x₂ + x₃)/2
...
tₙ₋₁ = (xₙ₋₁ + xₙ)/2

Step 3: For each threshold tᵢ:
- Split data: Left = {x ≤ tᵢ}, Right = {x > tᵢ}
- Calculate impurity reduction

Step 4: Select threshold with maximum impurity reduction

MATHEMATICAL FORMULATION:

For feature f and threshold t:

Impurity Reduction = I(parent) - [nₗ/n × I(left) + nᵣ/n × I(right)]

Where:

I(·) = Impurity function (Gini or Entropy)
nₗ, nᵣ = samples in left, right children
n = total samples
OPTIMIZATION:
Naive: O(n × n_features × n_thresholds) = O(n² × p)
Optimized: O(n log n × p) using sorting + incremental updates

INCREMENTAL UPDATE TRICK:
┌─────────────────────────────────────────────────────────────────┐
│ Instead of recalculating impurity from scratch: │
│ │
│ When moving one sample from left to right: │
│ - Update counts: nₗ -= 1, nᵣ += 1 │
│ - Update class counts incrementally │
│ - Recalculate impurity in O(k) where k = number of classes │
│ │
│ Total: O(n) per feature instead of O(n²) │
└─────────────────────────────────────────────────────────────────┘

text


### Q12: What is the computational complexity of training a Decision Tree?
ANSWER:

TIME COMPLEXITY:

Building the tree:
┌─────────────────────────────────────────────────────────────────┐
│ │
│ At each node: │
│ - Consider p features │
│ - For each feature, consider O(n) thresholds │
│ - Calculate impurity: O(n) │
│ - Per node: O(p × n) │
│ │
│ Number of nodes: │
│ - Balanced tree: O(n) nodes (worst case: each sample = leaf) │
│ - But with max_depth = d: O(2^d) nodes │
│ │
│ TOTAL (worst case): O(p × n² × log n) │
│ With depth limit: O(p × n × 2^d) │
│ │
│ OPTIMIZED (sklearn): O(p × n × log n × log n) │
│ - Uses sorting: O(n log n) │
│ - Incremental updates │
│ │
└─────────────────────────────────────────────────────────────────┘

SPACE COMPLEXITY:

Tree storage: O(number of nodes)
Balanced tree: O(n)
With depth limit: O(2^d)
Training: O(n × p) for data, O(n) for sorting
PREDICTION COMPLEXITY:

Single prediction: O(depth) = O(log n) for balanced tree
Very efficient!
COMPARISON:
┌──────────────────┬────────────────────┬───────────────────┐
│ Operation │ Time │ Space │
├──────────────────┼────────────────────┼───────────────────┤
│ Training │ O(p × n × log²n) │ O(n × p) │
│ Prediction │ O(log n) │ O(1) │
│ Feature Import. │ O(1) │ O(p) │
└──────────────────┴────────────────────┴───────────────────┘

text


### Q13: How would you implement feature importance calculation?
ANSWER:

Feature importance measures how much each feature contributes to
reducing impurity across all splits in the tree.

FORMULA:

Importance(feature) = Σ (weighted impurity reduction at each split using feature)
─────────────────────────────────────────────────────────────
Σ (all weighted impurity reductions)

DETAILED CALCULATION:

For each node that splits on feature f:

importance_f += (n_node / n_total) × (impurity_parent -
(n_left/n_node × impurity_left + n_right/n_node × impurity_right))

Then normalize so all importances sum to 1.

PYTHON IMPLEMENTATION:

Python

def calculate_feature_importance(tree, n_features):
    """
    Calculate feature importances from a trained tree.
    """
    # Get tree structure
    feature = tree.tree_.feature        # Feature used at each node
    threshold = tree.tree_.threshold    # Threshold at each node
    children_left = tree.tree_.children_left
    children_right = tree.tree_.children_right
    impurity = tree.tree_.impurity      # Gini/Entropy at each node
    n_node_samples = tree.tree_.n_node_samples
    
    n_total = n_node_samples[0]  # Total samples (root)
    
    importances = np.zeros(n_features)
    
    # Traverse all nodes
    for node_id in range(tree.tree_.node_count):
        # Skip leaf nodes
        if children_left[node_id] == children_right[node_id]:
            continue
        
        # Get feature used at this node
        f = feature[node_id]
        
        # Calculate weighted impurity decrease
        n_node = n_node_samples[node_id]
        n_left = n_node_samples[children_left[node_id]]
        n_right = n_node_samples[children_right[node_id]]
        
        imp_parent = impurity[node_id]
        imp_left = impurity[children_left[node_id]]
        imp_right = impurity[children_right[node_id]]
        
        decrease = (n_node / n_total) * (
            imp_parent - 
            (n_left / n_node * imp_left + n_right / n_node * imp_right)
        )
        
        importances[f] += decrease
    
    # Normalize
    importances = importances / importances.sum()
    
    return importances
ALTERNATIVE: PERMUTATION IMPORTANCE

Python

from sklearn.inspection import permutation_importance

# More reliable, considers feature interactions
result = permutation_importance(clf, X_test, y_test, n_repeats=10)
importance = result.importances_mean
COMPARISON:
┌─────────────────────┬─────────────────────────────────────────┐
│ MDI (Mean Decrease │ Permutation Importance │
│ Impurity) - Default│ │
├─────────────────────┼─────────────────────────────────────────┤
│ Fast to compute │ Slower (requires multiple predictions) │
│ Biased toward high │ Not biased │
│ cardinality features│ │
│ Can be computed on │ Should use test data │
│ training data │ │
└─────────────────────┴─────────────────────────────────────────┘

text


### Q14: How do Decision Trees compare to other algorithms for different scenarios?
ANSWER:

┌────────────────────┬───────────────────────────────────────────────────────┐
│ Scenario │ Recommendation │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Need │ ✅ Decision Tree │
│ interpretability │ Can explain every decision │
│ │ Show to stakeholders │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Small dataset │ ✅ Decision Tree / Logistic Regression │
│ (<1000 samples) │ Simple models work well │
│ │ Less prone to overfit with proper tuning │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Large dataset │ ⚠️ Consider ensemble methods │
│ (>100K samples) │ Random Forest, Gradient Boosting │
│ │ Single tree may underfit │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ High dimensional │ ❌ Not ideal for raw decision tree │
│ (many features) │ Consider: Random Forest (random feature selection) │
│ │ Or: Feature selection + Decision Tree │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Linear │ ❌ Inefficient │
│ relationships │ Use: Linear/Logistic Regression │
│ │ Tree needs many splits to approximate line │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Complex non-linear │ ✅ Excellent │
│ relationships │ Naturally captures interactions │
│ │ No feature engineering needed │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Missing values │ ⚠️ Depends on implementation │
│ │ CART: Surrogate splits │
│ │ sklearn: Requires imputation │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Categorical │ ✅ Excellent │
│ features │ No encoding needed (except in sklearn) │
│ │ Native handling in C4.5, CART │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Real-time │ ✅ Excellent │
│ predictions │ O(log n) prediction time │
│ │ Very fast inference │
│ │ │
├────────────────────┼───────────────────────────────────────────────────────┤
│ │ │
│ Maximum accuracy │ ❌ Use ensemble methods instead │
│ needed │ Random Forest, XGBoost, LightGBM │
│ │ Single tree rarely wins competitions │
│ │ │
└────────────────────┴───────────────────────────────────────────────────────┘

text


### Q15: Explain how Decision Trees are used as base learners in ensemble methods.
ANSWER:

Decision Trees are the foundation of many powerful ensemble methods.

BAGGING (Bootstrap Aggregating)
┌─────────────────────────────────────────────────────────────────┐
│ │
│ Original Data │
│ ┌─────────┐ │
│ │ D D D D │ │
│ └────┬────┘ │
│ │ │
│ Bootstrap Sampling │
│ ┌─────┼─────┬─────┐ │
│ │ │ │ │ │
│ D₁ D₂ D₃ D₄ (samples with replacement) │
│ │ │ │ │ │
│ Tree₁ Tree₂ Tree₃ Tree₄ │
│ │ │ │ │ │
│ └─────┴─────┴─────┘ │
│ │ │
│ AGGREGATE │
│ (vote/average) │
│ │ │
│ Final Prediction │
│ │
│ → Reduces VARIANCE (overfitting) │
│ → Example: Random Forest │
│ │
└─────────────────────────────────────────────────────────────────┘

RANDOM FOREST
┌─────────────────────────────────────────────────────────────────┐
│ │
│ Bagging + Random Feature Selection │
│ │
│ At each split: │
│ - Only consider random subset of features │
│ - Typically √p features for classification │
│ - Decorrelates trees │
│ │
│ Result: Even lower variance than simple bagging │
│ │
└─────────────────────────────────────────────────────────────────┘

BOOSTING
┌─────────────────────────────────────────────────────────────────┐
│ │
│ Sequential training - each tree focuses on previous errors │
│ │
│ Tree₁ → errors₁ → Tree₂ (focus on errors₁) │
│ ↓ │
│ errors₂ → Tree₃ (focus on errors₂) │
│ ↓ │
│ errors₃ → Tree₄ ... │
│ │
│ Final = weighted sum of all trees │
│ │
│ → Reduces BIAS (underfitting) │
│ → Examples: AdaBoost, Gradient Boosting, XGBoost, LightGBM │
│ │
└─────────────────────────────────────────────────────────────────┘

WHY DECISION TREES AS BASE LEARNERS?

Fast to train
Can capture non-linear relationships
Work with mixed data types
No feature scaling needed
Provide feature importance
Can be made weak (shallow) or strong (deep)
Highly customizable (depth, samples, etc.)
COMPARISON:
┌─────────────────┬──────────────────┬────────────────────────────┐
│ Method │ Base Trees │ Strategy │
├─────────────────┼──────────────────┼────────────────────────────┤
│ Random Forest │ Deep, complex │ Parallel, random features │
│ AdaBoost │ Shallow (stumps)│ Sequential, reweighting │
│ Gradient Boost │ Shallow-medium │ Sequential, gradients │
│ XGBoost │ Shallow-medium │ Regularized, optimized │
│ LightGBM │ Leaf-wise │ Histogram-based, fast │
│ CatBoost │ Ordered │ Handles categoricals │
└─────────────────┴──────────────────┴────────────────────────────┘

text


---

# Chapter 15: Practice Problems {#chapter-15-practice}

## 📝 Problem Set 1: Conceptual Questions

### Problem 1.1
**Given the following data, calculate Information Gain for splitting on "Weather":**

| Day | Weather | Temp  | Play |
|-----|---------|-------|------|
| 1   | Sunny   | Hot   | No   |
| 2   | Sunny   | Cool  | Yes  |
| 3   | Rainy   | Mild  | Yes  |
| 4   | Rainy   | Hot   | No   |
| 5   | Cloudy  | Mild  | Yes  |
| 6   | Cloudy  | Cool  | Yes  |

<details>
<summary><b>Click for Solution</b></summary>
STEP 1: Calculate Parent Entropy
Total: 6 samples, 4 Yes, 2 No

H(Parent) = -(4/6)log₂(4/6) - (2/6)log₂(2/6)
= -(0.667)(-0.585) - (0.333)(-1.585)
= 0.390 + 0.528
= 0.918

STEP 2: Calculate Entropy for each Weather value

Sunny (2 samples): 1 Yes, 1 No
H(Sunny) = -(1/2)log₂(1/2) - (1/2)log₂(1/2)
= 0.5 + 0.5 = 1.0

Rainy (2 samples): 1 Yes, 1 No
H(Rainy) = 1.0

Cloudy (2 samples): 2 Yes, 0 No
H(Cloudy) = 0 (pure!)

STEP 3: Calculate Weighted Average Entropy
H(Children) = (2/6)×1.0 + (2/6)×1.0 + (2/6)×0
= 0.333 + 0.333 + 0
= 0.667

STEP 4: Calculate Information Gain
IG(Weather) = H(Parent) - H(Children)
= 0.918 - 0.667
= 0.251

ANSWER: Information Gain for Weather = 0.251

text

</details>

### Problem 1.2
**Calculate Gini Impurity for a node with 30 samples of Class A and 70 samples of Class B.**

<details>
<summary><b>Click for Solution</b></summary>
Given:

Class A: 30 samples → p(A) = 30/100 = 0.3
Class B: 70 samples → p(B) = 70/100 = 0.7
Gini Impurity = 1 - Σ(pᵢ)²
= 1 - (0.3)² - (0.7)²
= 1 - 0.09 - 0.49
= 1 - 0.58
= 0.42

ANSWER: Gini Impurity = 0.42

INTERPRETATION:

Not pure (would be 0 if all same class)
Not maximum impurity (would be 0.5 for 50-50 split)
Moderate impurity level
text

</details>

### Problem 1.3
**A Decision Tree has training accuracy of 98% and test accuracy of 72%. What is the problem and how would you fix it?**

<details>
<summary><b>Click for Solution</b></summary>
PROBLEM: OVERFITTING

EVIDENCE:

Large gap between training (98%) and test (72%) accuracy
Model memorized training data but doesn't generalize
SOLUTIONS:

PRUNING

Pre-pruning: Set max_depth, min_samples_split, min_samples_leaf
Post-pruning: Use cost-complexity pruning (ccp_alpha)
REDUCE TREE COMPLEXITY

Python

clf = DecisionTreeClassifier(
    max_depth=5,              # Limit depth
    min_samples_split=20,     # Require more samples to split
    min_samples_leaf=10,      # Require more samples in leaves
    max_leaf_nodes=50         # Limit number of leaves
)
CROSS-VALIDATION

Use k-fold CV to find optimal hyperparameters
Select model with best validation performance
MORE DATA

If possible, collect more training samples
More data → less overfitting
FEATURE SELECTION

Remove irrelevant features
Reduce dimensionality
ENSEMBLE METHODS

Use Random Forest instead
Bagging reduces variance
GOAL: Reduce gap between training and test accuracy
while maintaining acceptable test accuracy.

text

</details>

---

## 📝 Problem Set 2: Coding Problems

### Problem 2.1: Build a Decision Tree for Loan Approval

**Dataset:**

| Age  | Income | Student | Credit | Approved |
|------|--------|---------|--------|----------|
| <30  | High   | No      | Fair   | No       |
| <30  | High   | No      | Good   | No       |
| 30-40| High   | No      | Fair   | Yes      |
| >40  | Medium | No      | Fair   | Yes      |
| >40  | Low    | Yes     | Fair   | Yes      |
| >40  | Low    | Yes     | Good   | No       |
| 30-40| Low    | Yes     | Good   | Yes      |
| <30  | Medium | No      | Fair   | No       |
| <30  | Low    | Yes     | Fair   | Yes      |
| >40  | Medium | Yes     | Fair   | Yes      |

<details>
<summary><b>Click for Solution</b></summary>

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder
from sklearn.tree import DecisionTreeClassifier, plot_tree, export_text
import matplotlib.pyplot as plt

# Create dataset
data = {
    'Age': ['<30', '<30', '30-40', '>40', '>40', '>40', '30-40', '<30', '<30', '>40'],
    'Income': ['High', 'High', 'High', 'Medium', 'Low', 'Low', 'Low', 'Medium', 'Low', 'Medium'],
    'Student': ['No', 'No', 'No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'Yes'],
    'Credit': ['Fair', 'Good', 'Fair', 'Fair', 'Fair', 'Good', 'Good', 'Fair', 'Fair', 'Fair'],
    'Approved': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes']
}

df = pd.DataFrame(data)

# Encode categorical variables
le_dict = {}
df_encoded = df.copy()

for col in df.columns:
    le = LabelEncoder()
    df_encoded[col] = le.fit_transform(df[col])
    le_dict[col] = le

# Prepare features and target
X = df_encoded.drop('Approved', axis=1)
y = df_encoded['Approved']

# Build Decision Tree
clf = DecisionTreeClassifier(criterion='entropy', random_state=42)
clf.fit(X, y)

# Visualize
plt.figure(figsize=(15, 10))
plot_tree(clf, 
          feature_names=['Age', 'Income', 'Student', 'Credit'],
          class_names=['No', 'Yes'],
          filled=True,
          rounded=True,
          fontsize=10)
plt.title('Loan Approval Decision Tree')
plt.tight_layout()
plt.show()

# Print rules
rules = export_text(clf, feature_names=['Age', 'Income', 'Student', 'Credit'])
print("Decision Rules:")
print(rules)

# Feature importance
print("\nFeature Importance:")
for name, importance in zip(X.columns, clf.feature_importances_):
    print(f"  {name}: {importance:.4f}")
Expected Output:

text

Decision Rules:
|--- Age <= 0.5
|   |--- Student <= 0.5
|   |   |--- class: 0
|   |--- Student > 0.5
|   |   |--- class: 1
|--- Age > 0.5
|   |--- Credit <= 0.5
|   |   |--- class: 1
|   |--- Credit > 0.5
|   |   |--- Student <= 0.5
|   |   |   |--- class: 0
|   |   |--- Student > 0.5
|   |   |   |--- class: 1

Feature Importance:
  Age: 0.4199
  Income: 0.0000
  Student: 0.3475
  Credit: 0.2326
</details>
Problem 2.2: Implement Gini Impurity and Information Gain from Scratch
<details> <summary><b>Click for Solution</b></summary>
Python

import numpy as np
from collections import Counter

def gini_impurity(y):
    """
    Calculate Gini Impurity.
    
    Parameters:
    -----------
    y : array-like
        Class labels
        
    Returns:
    --------
    float : Gini impurity value (0 to 0.5 for binary)
    """
    if len(y) == 0:
        return 0
    
    counter = Counter(y)
    probabilities = [count / len(y) for count in counter.values()]
    
    gini = 1 - sum(p**2 for p in probabilities)
    return gini


def entropy(y):
    """
    Calculate Entropy.
    
    Parameters:
    -----------
    y : array-like
        Class labels
        
    Returns:
    --------
    float : Entropy value (0 to log2(n_classes))
    """
    if len(y) == 0:
        return 0
    
    counter = Counter(y)
    probabilities = [count / len(y) for count in counter.values()]
    
    # Handle log(0) by filtering out zero probabilities
    ent = -sum(p * np.log2(p) for p in probabilities if p > 0)
    return ent


def information_gain(y_parent, y_left, y_right, criterion='entropy'):
    """
    Calculate Information Gain from a split.
    
    Parameters:
    -----------
    y_parent : array-like
        Labels of parent node
    y_left : array-like
        Labels of left child
    y_right : array-like
        Labels of right child
    criterion : str
        'entropy' or 'gini'
        
    Returns:
    --------
    float : Information gain value
    """
    if criterion == 'entropy':
        impurity_func = entropy
    else:
        impurity_func = gini_impurity
    
    n = len(y_parent)
    n_left = len(y_left)
    n_right = len(y_right)
    
    if n_left == 0 or n_right == 0:
        return 0
    
    # Parent impurity
    parent_impurity = impurity_func(y_parent)
    
    # Weighted child impurity
    child_impurity = (n_left/n) * impurity_func(y_left) + \
                     (n_right/n) * impurity_func(y_right)
    
    # Information gain
    ig = parent_impurity - child_impurity
    
    return ig


# Test the functions
print("="*50)
print("TESTING IMPURITY FUNCTIONS")
print("="*50)

# Test case 1: Pure node
y_pure = [1, 1, 1, 1, 1]
print(f"\nPure node [1,1,1,1,1]:")
print(f"  Gini: {gini_impurity(y_pure):.4f} (expected: 0)")
print(f"  Entropy: {entropy(y_pure):.4f} (expected: 0)")

# Test case 2: Maximum impurity (50-50)
y_max = [0, 0, 0, 0, 1, 1, 1, 1]
print(f"\n50-50 split [0,0,0,0,1,1,1,1]:")
print(f"  Gini: {gini_impurity(y_max):.4f} (expected: 0.5)")
print(f"  Entropy: {entropy(y_max):.4f} (expected: 1.0)")

# Test case 3: 75-25 split
y_partial = [0, 0, 0, 1]
print(f"\n75-25 split [0,0,0,1]:")
print(f"  Gini: {gini_impurity(y_partial):.4f} (expected: 0.375)")
print(f"  Entropy: {entropy(y_partial):.4f} (expected: 0.811)")

# Test Information Gain
print("\n" + "="*50)
print("TESTING INFORMATION GAIN")
print("="*50)

y_parent = [0, 0, 0, 0, 1, 1, 1, 1]  # 50-50
y_left = [0, 0, 0, 1]   # 75-25
y_right = [0, 1, 1, 1]  # 25-75

print(f"\nParent: [0,0,0,0,1,1,1,1]")
print(f"Left:   [0,0,0,1]")
print(f"Right:  [0,1,1,1]")
print(f"\nInformation Gain (Entropy): {information_gain(y_parent, y_left, y_right, 'entropy'):.4f}")
print(f"Information Gain (Gini): {information_gain(y_parent, y_left, y_right, 'gini'):.4f}")

# Perfect split
y_left_perfect = [0, 0, 0, 0]
y_right_perfect = [1, 1, 1, 1]

print(f"\nPerfect split:")
print(f"Left:   [0,0,0,0]")
print(f"Right:  [1,1,1,1]")
print(f"\nInformation Gain (Entropy): {information_gain(y_parent, y_left_perfect, y_right_perfect, 'entropy'):.4f}")
print(f"Information Gain (Gini): {information_gain(y_parent, y_left_perfect, y_right_perfect, 'gini'):.4f}")
Output:

text

==================================================
TESTING IMPURITY FUNCTIONS
==================================================

Pure node [1,1,1,1,1]:
  Gini: 0.0000 (expected: 0)
  Entropy: 0.0000 (expected: 0)

50-50 split [0,0,0,0,1,1,1,1]:
  Gini: 0.5000 (expected: 0.5)
  Entropy: 1.0000 (expected: 1.0)

75-25 split [0,0,0,1]:
  Gini: 0.3750 (expected: 0.375)
  Entropy: 0.8113 (expected: 0.811)

==================================================
TESTING INFORMATION GAIN
==================================================

Parent: [0,0,0,0,1,1,1,1]
Left:   [0,0,0,1]
Right:  [0,1,1,1]

Information Gain (Entropy): 0.1887
Information Gain (Gini): 0.1250

Perfect split:
Left:   [0,0,0,0]
Right:  [1,1,1,1]

Information Gain (Entropy): 1.0000
Information Gain (Gini): 0.5000
</details>
Problem 2.3: Visualize Decision Boundaries for Different Tree Depths
<details> <summary><b>Click for Solution</b></summary>
Python

import numpy as np
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_moons, make_circles, make_classification

def plot_decision_boundary(clf, X, y, ax, title):
    """Plot decision boundary for a classifier."""
    # Create mesh
    h = 0.02
    x_min, x_max = X[:, 0].min() - 1, X[:, 0].max() + 1
    y_min, y_max = X[:, 1].min() - 1, X[:, 1].max() + 1
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h),
                         np.arange(y_min, y_max, h))
    
    # Predict on mesh
    Z = clf.predict(np.c_[xx.ravel(), yy.ravel()])
    Z = Z.reshape(xx.shape)
    
    # Plot
    ax.contourf(xx, yy, Z, alpha=0.4, cmap=plt.cm.RdYlBu)
    ax.scatter(X[:, 0], X[:, 1], c=y, cmap=plt.cm.RdYlBu, edgecolors='black')
    ax.set_title(title)
    ax.set_xlim(xx.min(), xx.max())
    ax.set_ylim(yy.min(), yy.max())

# Generate datasets
np.random.seed(42)
datasets = [
    ("Moons", make_moons(n_samples=300, noise=0.3, random_state=42)),
    ("Circles", make_circles(n_samples=300, noise=0.2, factor=0.5, random_state=42)),
    ("Linear", make_classification(n_samples=300, n_features=2, n_redundant=0,
                                   n_informative=2, n_clusters_per_class=1, random_state=42))
]

# Different depths to try
depths = [1, 3, 5, 10, None]

# Create figure
fig, axes = plt.subplots(len(datasets), len(depths), figsize=(20, 12))

for i, (name, (X, y)) in enumerate(datasets):
    for j, depth in enumerate(depths):
        # Train classifier
        clf = DecisionTreeClassifier(max_depth=depth, random_state=42)
        clf.fit(X, y)
        
        # Calculate accuracy
        acc = clf.score(X, y)
        
        # Plot
        depth_str = str(depth) if depth else "None"
        title = f"{name}\nDepth={depth_str}, Acc={acc:.2%}"
        plot_decision_boundary(clf, X, y, axes[i, j], title)

plt.tight_layout()
plt.savefig('decision_boundaries.png', dpi=150)
plt.show()

print("\nOBSERVATIONS:")
print("="*60)
print("1. Depth=1: Too simple, underfits (can only make 1 split)")
print("2. Depth=3: Good balance for most datasets")
print("3. Depth=5: More complex, captures more patterns")
print("4. Depth=10: May start to overfit")
print("5. Depth=None: Can severely overfit (100% training accuracy)")
print("="*60)
</details>
📝 Problem Set 3: Real-World Scenarios
Problem 3.1: Credit Card Fraud Detection
Task: Build a decision tree to detect fraudulent transactions.

<details> <summary><b>Click for Solution</b></summary>
Python

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import (classification_report, confusion_matrix, 
                             roc_auc_score, precision_recall_curve, 
                             average_precision_score)
from sklearn.preprocessing import StandardScaler
from imblearn.over_sampling import SMOTE  # pip install imbalanced-learn

# Generate synthetic fraud data
np.random.seed(42)
n_samples = 10000
n_fraud = 200  # 2% fraud rate

# Normal transactions
normal_amount = np.random.exponential(100, n_samples - n_fraud)
normal_time = np.random.uniform(0, 24, n_samples - n_fraud)
normal_location_changes = np.random.poisson(1, n_samples - n_fraud)
normal_frequency = np.random.poisson(3, n_samples - n_fraud)

# Fraudulent transactions (different patterns)
fraud_amount = np.random.exponential(500, n_fraud)  # Higher amounts
fraud_time = np.random.choice([2, 3, 4], n_fraud) + np.random.normal(0, 0.5, n_fraud)  # Late night
fraud_location_changes = np.random.poisson(5, n_fraud)  # More location changes
fraud_frequency = np.random.poisson(10, n_fraud)  # Higher frequency

# Combine data
data = pd.DataFrame({
    'amount': np.concatenate([normal_amount, fraud_amount]),
    'hour': np.concatenate([normal_time, fraud_time]) % 24,
    'location_changes': np.concatenate([normal_location_changes, fraud_location_changes]),
    'transaction_frequency': np.concatenate([normal_frequency, fraud_frequency]),
    'is_fraud': np.concatenate([np.zeros(n_samples - n_fraud), np.ones(n_fraud)])
})

# Shuffle data
data = data.sample(frac=1, random_state=42).reset_index(drop=True)

print("Dataset Shape:", data.shape)
print("\nClass Distribution:")
print(data['is_fraud'].value_counts(normalize=True))
print("\nSample Data:")
print(data.head(10))

# Prepare features and target
X = data.drop('is_fraud', axis=1)
y = data['is_fraud']

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

print(f"\nTraining set: {len(X_train)} samples")
print(f"Test set: {len(X_test)} samples")
print(f"Fraud in training: {y_train.sum():.0f} ({y_train.mean()*100:.2f}%)")

# ─────────────────────────────────────────────────────────────
# METHOD 1: Basic Decision Tree (without handling imbalance)
# ─────────────────────────────────────────────────────────────

clf_basic = DecisionTreeClassifier(max_depth=5, random_state=42)
clf_basic.fit(X_train, y_train)

y_pred_basic = clf_basic.predict(X_test)
y_prob_basic = clf_basic.predict_proba(X_test)[:, 1]

print("\n" + "="*60)
print("METHOD 1: Basic Decision Tree (No Imbalance Handling)")
print("="*60)
print(classification_report(y_test, y_pred_basic, target_names=['Normal', 'Fraud']))

# ─────────────────────────────────────────────────────────────
# METHOD 2: Decision Tree with Class Weights
# ─────────────────────────────────────────────────────────────

clf_weighted = DecisionTreeClassifier(
    max_depth=5, 
    class_weight='balanced',  # Automatically balance
    random_state=42
)
clf_weighted.fit(X_train, y_train)

y_pred_weighted = clf_weighted.predict(X_test)
y_prob_weighted = clf_weighted.predict_proba(X_test)[:, 1]

print("\n" + "="*60)
print("METHOD 2: Decision Tree with Balanced Class Weights")
print("="*60)
print(classification_report(y_test, y_pred_weighted, target_names=['Normal', 'Fraud']))

# ─────────────────────────────────────────────────────────────
# METHOD 3: Decision Tree with SMOTE Oversampling
# ─────────────────────────────────────────────────────────────

smote = SMOTE(random_state=42)
X_train_smote, y_train_smote = smote.fit_resample(X_train, y_train)

print(f"\nAfter SMOTE: {len(X_train_smote)} samples")
print(f"Fraud: {y_train_smote.sum():.0f} ({y_train_smote.mean()*100:.2f}%)")

clf_smote = DecisionTreeClassifier(max_depth=5, random_state=42)
clf_smote.fit(X_train_smote, y_train_smote)

y_pred_smote = clf_smote.predict(X_test)
y_prob_smote = clf_smote.predict_proba(X_test)[:, 1]

print("\n" + "="*60)
print("METHOD 3: Decision Tree with SMOTE Oversampling")
print("="*60)
print(classification_report(y_test, y_pred_smote, target_names=['Normal', 'Fraud']))

# ─────────────────────────────────────────────────────────────
# COMPARISON VISUALIZATION
# ─────────────────────────────────────────────────────────────

fig, axes = plt.subplots(2, 3, figsize=(18, 12))

# Confusion Matrices
methods = [
    ('Basic', y_pred_basic, y_prob_basic),
    ('Weighted', y_pred_weighted, y_prob_weighted),
    ('SMOTE', y_pred_smote, y_prob_smote)
]

for idx, (name, y_pred, y_prob) in enumerate(methods):
    # Confusion Matrix
    cm = confusion_matrix(y_test, y_pred)
    axes[0, idx].imshow(cm, cmap='Blues')
    for i in range(2):
        for j in range(2):
            axes[0, idx].text(j, i, cm[i, j], ha='center', va='center', fontsize=14)
    axes[0, idx].set_title(f'{name}: Confusion Matrix')
    axes[0, idx].set_xlabel('Predicted')
    axes[0, idx].set_ylabel('Actual')
    axes[0, idx].set_xticks([0, 1])
    axes[0, idx].set_yticks([0, 1])
    axes[0, idx].set_xticklabels(['Normal', 'Fraud'])
    axes[0, idx].set_yticklabels(['Normal', 'Fraud'])
    
    # Precision-Recall Curve
    precision, recall, _ = precision_recall_curve(y_test, y_prob)
    ap = average_precision_score(y_test, y_prob)
    axes[1, idx].plot(recall, precision, 'b-', linewidth=2)
    axes[1, idx].set_xlabel('Recall')
    axes[1, idx].set_ylabel('Precision')
    axes[1, idx].set_title(f'{name}: PR Curve (AP={ap:.3f})')
    axes[1, idx].set_xlim([0, 1])
    axes[1, idx].set_ylim([0, 1])
    axes[1, idx].grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('fraud_detection_comparison.png', dpi=150)
plt.show()

# ─────────────────────────────────────────────────────────────
# VISUALIZE BEST MODEL (Weighted)
# ─────────────────────────────────────────────────────────────

plt.figure(figsize=(20, 10))
plot_tree(
    clf_weighted,
    feature_names=X.columns.tolist(),
    class_names=['Normal', 'Fraud'],
    filled=True,
    rounded=True,
    fontsize=10
)
plt.title('Fraud Detection Decision Tree (Balanced Weights)')
plt.tight_layout()
plt.savefig('fraud_detection_tree.png', dpi=150)
plt.show()

# ─────────────────────────────────────────────────────────────
# FEATURE IMPORTANCE
# ─────────────────────────────────────────────────────────────

print("\n" + "="*60)
print("FEATURE IMPORTANCE (Weighted Model)")
print("="*60)

importances = clf_weighted.feature_importances_
for name, imp in sorted(zip(X.columns, importances), key=lambda x: -x[1]):
    print(f"  {name}: {imp:.4f}")

# ─────────────────────────────────────────────────────────────
# BUSINESS RECOMMENDATIONS
# ─────────────────────────────────────────────────────────────

print("\n" + "="*60)
print("BUSINESS RECOMMENDATIONS")
print("="*60)
print("""
Based on the Decision Tree analysis:

1. HIGH-RISK INDICATORS:
   - Transactions with high amounts (>$500)
   - Transactions between 2-4 AM
   - Multiple location changes (>3)
   - High transaction frequency (>8/day)

2. RECOMMENDED ACTIONS:
   - Flag transactions matching multiple risk factors
   - Require additional verification for late-night high-value transactions
   - Monitor accounts with unusual location patterns
   - Set alerts for sudden increases in transaction frequency

3. MODEL SELECTION:
   - Use WEIGHTED model for best fraud detection
   - Accept some false positives to catch more fraud
   - Review flagged transactions manually
""")
</details>
Problem 3.2: Medical Diagnosis Decision Support
Task: Build an interpretable decision tree for disease diagnosis.

<details> <summary><b>Click for Solution</b></summary>
Python

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree, export_text
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import classification_report, confusion_matrix

# Generate synthetic medical data
np.random.seed(42)
n_patients = 1000

def generate_patient_data():
    """Generate synthetic patient data with realistic patterns."""
    
    data = []
    
    for _ in range(n_patients):
        # Random base values
        age = np.random.randint(20, 80)
        
        # Generate symptoms based on condition
        condition = np.random.choice(['Healthy', 'Cold', 'Flu', 'COVID'], 
                                      p=[0.4, 0.25, 0.2, 0.15])
        
        if condition == 'Healthy':
            temperature = np.random.normal(98.6, 0.3)
            cough = np.random.choice([0, 1], p=[0.9, 0.1])
            fatigue = np.random.choice([0, 1, 2], p=[0.8, 0.15, 0.05])
            body_ache = np.random.choice([0, 1], p=[0.9, 0.1])
            loss_of_taste = np.random.choice([0, 1], p=[0.98, 0.02])
            runny_nose = np.random.choice([0, 1], p=[0.85, 0.15])
            
        elif condition == 'Cold':
            temperature = np.random.normal(99.0, 0.5)
            cough = np.random.choice([0, 1], p=[0.3, 0.7])
            fatigue = np.random.choice([0, 1, 2], p=[0.4, 0.5, 0.1])
            body_ache = np.random.choice([0, 1], p=[0.7, 0.3])
            loss_of_taste = np.random.choice([0, 1], p=[0.9, 0.1])
            runny_nose = np.random.choice([0, 1], p=[0.2, 0.8])  # Common in cold
            
        elif condition == 'Flu':
            temperature = np.random.normal(101.5, 1.0)  # Higher fever
            cough = np.random.choice([0, 1], p=[0.2, 0.8])
            fatigue = np.random.choice([0, 1, 2], p=[0.1, 0.3, 0.6])  # Severe fatigue
            body_ache = np.random.choice([0, 1], p=[0.2, 0.8])  # Common in flu
            loss_of_taste = np.random.choice([0, 1], p=[0.85, 0.15])
            runny_nose = np.random.choice([0, 1], p=[0.5, 0.5])
            
        else:  # COVID
            temperature = np.random.normal(100.5, 1.2)
            cough = np.random.choice([0, 1], p=[0.15, 0.85])  # Dry cough common
            fatigue = np.random.choice([0, 1, 2], p=[0.15, 0.35, 0.5])
            body_ache = np.random.choice([0, 1], p=[0.4, 0.6])
            loss_of_taste = np.random.choice([0, 1], p=[0.3, 0.7])  # Key indicator
            runny_nose = np.random.choice([0, 1], p=[0.7, 0.3])  # Less common
        
        data.append({
            'age': age,
            'temperature': round(temperature, 1),
            'cough': cough,
            'fatigue_level': fatigue,  # 0=none, 1=mild, 2=severe
            'body_ache': body_ache,
            'loss_of_taste': loss_of_taste,
            'runny_nose': runny_nose,
            'diagnosis': condition
        })
    
    return pd.DataFrame(data)

# Generate data
df = generate_patient_data()

print("="*60)
print("MEDICAL DIAGNOSIS DATASET")
print("="*60)
print(f"\nDataset Shape: {df.shape}")
print("\nDiagnosis Distribution:")
print(df['diagnosis'].value_counts())
print("\nSample Data:")
print(df.head(10))

# ─────────────────────────────────────────────────────────────
# PREPARE DATA
# ─────────────────────────────────────────────────────────────

# Features and target
feature_cols = ['age', 'temperature', 'cough', 'fatigue_level', 
                'body_ache', 'loss_of_taste', 'runny_nose']
X = df[feature_cols]
y = df['diagnosis']

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# ─────────────────────────────────────────────────────────────
# TRAIN INTERPRETABLE MODEL
# ─────────────────────────────────────────────────────────────

# For medical diagnosis, interpretability is CRITICAL
# Keep tree shallow enough for doctors to understand

clf = DecisionTreeClassifier(
    max_depth=4,              # Limited depth for interpretability
    min_samples_split=20,     # Require sufficient evidence
    min_samples_leaf=10,      # Ensure robust leaf predictions
    random_state=42
)

clf.fit(X_train, y_train)

# ─────────────────────────────────────────────────────────────
# EVALUATE MODEL
# ─────────────────────────────────────────────────────────────

y_pred = clf.predict(X_test)

print("\n" + "="*60)
print("MODEL EVALUATION")
print("="*60)

# Cross-validation
cv_scores = cross_val_score(clf, X, y, cv=5)
print(f"\nCross-Validation Accuracy: {cv_scores.mean():.2%} (+/- {cv_scores.std()*2:.2%})")

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

print("\nConfusion Matrix:")
cm = confusion_matrix(y_test, y_pred)
print(pd.DataFrame(cm, 
                   index=['Actual: ' + c for c in clf.classes_],
                   columns=['Pred: ' + c for c in clf.classes_]))

# ─────────────────────────────────────────────────────────────
# VISUALIZE THE DECISION TREE
# ─────────────────────────────────────────────────────────────

plt.figure(figsize=(25, 15))
plot_tree(
    clf,
    feature_names=feature_cols,
    class_names=clf.classes_,
    filled=True,
    rounded=True,
    fontsize=10,
    proportion=True  # Show proportions instead of counts
)
plt.title('Medical Diagnosis Decision Tree', fontsize=16)
plt.tight_layout()
plt.savefig('medical_diagnosis_tree.png', dpi=150, bbox_inches='tight')
plt.show()

# ─────────────────────────────────────────────────────────────
# EXTRACT DECISION RULES (For Medical Staff)
# ─────────────────────────────────────────────────────────────

print("\n" + "="*60)
print("DECISION RULES FOR MEDICAL STAFF")
print("="*60)

rules = export_text(clf, feature_names=feature_cols)
print(rules)

# ─────────────────────────────────────────────────────────────
# CREATE HUMAN-READABLE RULES
# ─────────────────────────────────────────────────────────────

print("\n" + "="*60)
print("SIMPLIFIED DIAGNOSTIC GUIDELINES")
print("="*60)

print("""
STEP 1: Check Temperature
├── If temperature ≤ 99.5°F:
│   └── Likely HEALTHY or MILD COLD
│       → Check for runny nose (indicates cold)
│
├── If temperature 99.5°F - 100.5°F:
│   └── Check for LOSS OF TASTE/SMELL
│       ├── YES → Suspect COVID, recommend testing
│       └── NO → Likely COLD or early FLU
│
└── If temperature > 100.5°F:
    └── Check BODY ACHES and FATIGUE
        ├── Severe fatigue + body aches → Likely FLU
        ├── Loss of taste → Likely COVID
        └── Primarily runny nose → Likely severe COLD

KEY DISTINGUISHING FACTORS:
┌─────────────────┬───────────┬───────────┬───────────┬───────────┐
│    Symptom      │  Healthy  │   Cold    │    Flu    │   COVID   │
├─────────────────┼───────────┼───────────┼───────────┼───────────┤
│ Temperature     │   Normal  │   Mild    │   High    │  Moderate │
│ Runny Nose      │   Rare    │  Common   │  Variable │   Rare    │
│ Body Aches      │   Rare    │   Mild    │  Severe   │  Moderate │
│ Fatigue         │   None    │   Mild    │  Severe   │  Moderate │
│ Loss of Taste   │   Rare    │   Rare    │   Rare    │  COMMON   │
└─────────────────┴───────────┴───────────┴───────────┴───────────┘

IMPORTANT NOTES:
- This is a decision SUPPORT tool, not a replacement for clinical judgment
- COVID cases should always be confirmed with testing
- Consider patient history and other factors
""")

# ─────────────────────────────────────────────────────────────
# FEATURE IMPORTANCE
# ─────────────────────────────────────────────────────────────

print("\n" + "="*60)
print("FEATURE IMPORTANCE FOR DIAGNOSIS")
print("="*60)

importance_df = pd.DataFrame({
    'Feature': feature_cols,
    'Importance': clf.feature_importances_
}).sort_values('Importance', ascending=False)

print(importance_df.to_string(index=False))

# Visualize
plt.figure(figsize=(10, 6))
plt.barh(importance_df['Feature'], importance_df['Importance'])
plt.xlabel('Importance')
plt.title('Feature Importance for Medical Diagnosis')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.savefig('medical_feature_importance.png', dpi=150)
plt.show()

# ─────────────────────────────────────────────────────────────
# PREDICTION FUNCTION FOR NEW PATIENTS
# ─────────────────────────────────────────────────────────────

def diagnose_patient(patient_info):
    """
    Make diagnosis prediction for a new patient.
    
    Parameters:
    -----------
    patient_info : dict
        Patient symptoms and measurements
        
    Returns:
    --------
    dict : Diagnosis and probabilities
    """
    # Create feature vector
    features = pd.DataFrame([patient_info])[feature_cols]
    
    # Predict
    diagnosis = clf.predict(features)[0]
    probabilities = clf.predict_proba(features)[0]
    
    # Create result
    result = {
        'diagnosis': diagnosis,
        'confidence': max(probabilities),
        'all_probabilities': dict(zip(clf.classes_, probabilities))
    }
    
    return result

# Test with sample patients
print("\n" + "="*60)
print("SAMPLE DIAGNOSES")
print("="*60)

sample_patients = [
    {
        'name': 'Patient A',
        'age': 35, 'temperature': 98.4, 'cough': 0, 'fatigue_level': 0,
        'body_ache': 0, 'loss_of_taste': 0, 'runny_nose': 0
    },
    {
        'name': 'Patient B',
        'age': 45, 'temperature': 101.2, 'cough': 1, 'fatigue_level': 2,
        'body_ache': 1, 'loss_of_taste': 0, 'runny_nose': 0
    },
    {
        'name': 'Patient C',
        'age': 28, 'temperature': 100.1, 'cough': 1, 'fatigue_level': 1,
        'body_ache': 0, 'loss_of_taste': 1, 'runny_nose': 0
    },
    {
        'name': 'Patient D',
        'age': 55, 'temperature': 99.2, 'cough': 1, 'fatigue_level': 1,
        'body_ache': 0, 'loss_of_taste': 0, 'runny_nose': 1
    }
]

for patient in sample_patients:
    name = patient.pop('name')
    result = diagnose_patient(patient)
    print(f"\n{name}:")
    print(f"  Symptoms: Temp={patient['temperature']}°F, Cough={'Yes' if patient['cough'] else 'No'}, "
          f"Fatigue={patient['fatigue_level']}, Loss of taste={'Yes' if patient['loss_of_taste'] else 'No'}")
    print(f"  Diagnosis: {result['diagnosis']} (Confidence: {result['confidence']:.1%})")
    print(f"  Probabilities: {', '.join([f'{k}:{v:.1%}' for k,v in result['all_probabilities'].items()])}")
</details>
🎓 Quick Reference Card
text

╔══════════════════════════════════════════════════════════════════╗
║              DECISION TREE QUICK REFERENCE CARD                   ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  SPLITTING CRITERIA:                                              ║
║  ┌─────────────────────────────────────────────────────────────┐ ║
║  │ Classification:                                             │ ║
║  │   • Gini = 1 - Σ(pᵢ)²           [Range: 0 to 0.5]          │ ║
║  │   • Entropy = -Σ pᵢ × log₂(pᵢ)  [Range: 0 to 1]            │ ║
║  │                                                             │ ║
║  │ Regression:                                                 │ ║
║  │   • MSE = (1/n) × Σ(yᵢ - ȳ)²                               │ ║
║  │   • MAE = (1/n) × Σ|yᵢ - ȳ|                                │ ║
║  └─────────────────────────────────────────────────────────────┘ ║
║                                                                   ║
║  KEY HYPERPARAMETERS:                                             ║
║  ┌─────────────────────────────────────────────────────────────┐ ║
║  │ max_depth         → Limit tree depth (prevent overfit)     │ ║
║  │ min_samples_split → Min samples to split a node            │ ║
║  │ min_samples_leaf  → Min samples in leaf node               │ ║
║  │ max_features      → Features to consider per split         │ ║
║  │ ccp_alpha         → Pruning parameter (higher = simpler)   │ ║
║  └─────────────────────────────────────────────────────────────┘ ║
║                                                                   ║
║  SKLEARN QUICK START:                                             ║
║  ┌─────────────────────────────────────────────────────────────┐ ║
║  │ from sklearn.tree import DecisionTreeClassifier            │ ║
║  │                                                             │ ║
║  │ clf = DecisionTreeClassifier(                              │ ║
║  │     max_depth=5,                                           │ ║
║  │     min_samples_leaf=5,                                    │ ║
║  │     random_state=42                                        │ ║
║  │ )                                                          │ ║
║  │ clf.fit(X_train, y_train)                                  │ ║
║  │ predictions = clf.predict(X_test)                          │ ║
║  └─────────────────────────────────────────────────────────────┘ ║
║                                                                   ║
║  WHEN TO USE:                                                     ║
║  ✅ Need interpretability          ❌ Need highest accuracy       ║
║  ✅ Mixed feature types            ❌ Very high dimensions         ║
║  ✅ Non-linear relationships       ❌ Linear relationships         ║
║  ✅ Feature importance needed      ❌ Need to extrapolate          ║
║  ✅ Fast predictions required      ❌ Unstable is unacceptable     ║
║                                                                   ║
║  OVERFITTING SIGNS & FIXES:                                       ║
║  ┌─────────────────────────────────────────────────────────────┐ ║
║  │ Sign: Train acc >> Test acc                                │ ║
║  │ Fix:  Reduce max_depth, increase min_samples_*             │ ║
║  │       Use pruning (ccp_alpha), cross-validation            │ ║
║  └─────────────────────────────────────────────────────────────┘ ║
║                                                                   ║
║  ALGORITHMS COMPARISON:                                           ║
║  ┌──────────┬────────────┬────────────┬────────────────────────┐ ║
║  │   ID3    │    C4.5    │    CART    │      sklearn          │ ║
║  ├──────────┼────────────┼────────────┼────────────────────────┤ ║
║  │ IG only  │ Gain Ratio │   Gini     │ Gini/Entropy          │ ║
║  │ Multi-way│ Multi-way  │  Binary    │ Binary                │ ║
║  │ No cont. │ Continuous │ Continuous │ Continuous            │ ║
║  │ No prune │ Post-prune │   CCP      │ Pre+Post prune        │ ║
║  └──────────┴────────────┴────────────┴────────────────────────┘ ║
║                                                                   ║
╚══════════════════════════════════════════════════════════════════╝
📚 Final Summary
What You've Learned
text

BEGINNER LEVEL ✓
├── What is a Decision Tree
├── Basic terminology (nodes, leaves, splits)
├── How trees make predictions
└── Simple examples and visualizations

INTERMEDIATE LEVEL ✓
├── Gini Impurity and Entropy
├── Information Gain calculation
├── Building trees step-by-step
├── Overfitting and pruning
├── Hyperparameter tuning
└── Sklearn implementation

ADVANCED LEVEL ✓
├── Mathematical foundations
├── Cost Complexity Pruning (CCP)
├── Regression trees
├── Algorithm variants (ID3, C4.5, CART)
├── Ensemble foundations
├── Real-world applications
└── Interview preparation
Key Takeaways
text

1️⃣  Decision Trees split data by asking sequential questions
    → Each split maximizes information gain (reduces impurity)

2️⃣  Gini and Entropy measure node impurity
    → Lower impurity = purer node = better split

3️⃣  Overfitting is the main challenge
    → Control with max_depth, min_samples, pruning

4️⃣  Interpretability is the main strength
    → Can explain every prediction

5️⃣  Single trees are building blocks for powerful ensembles
    → Random Forest, Gradient Boosting, XGBoost
🎯 Your Next Steps
text

PRACTICE:
□ Implement a decision tree from scratch
□ Build trees on Kaggle datasets
□ Compare Gini vs Entropy results
□ Experiment with different hyperparameters
□ Visualize decision boundaries

ADVANCE:
□ Learn Random Forests
□ Study Gradient Boosting
□ Explore XGBoost/LightGBM
□ Understand feature importance deeply
□ Apply to real-world projects

MASTER:
□ Contribute to open-source implementations
□ Publish analysis using decision trees
□ Teach others what you've learned
□ Develop domain-specific applications
Congratulations! 🎉

You now have comprehensive knowledge of Decision Trees from basic concepts to advanced implementations. This knowledge forms the foundation for understanding many modern machine learning algorithms.

Remember: The best way to truly master Decision Trees is through practice. Start with simple datasets, gradually increase complexity, and always focus on understanding WHY the tree makes certain decisions.
