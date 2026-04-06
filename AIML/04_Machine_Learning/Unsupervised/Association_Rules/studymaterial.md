The Ultimate Guide to Association Rules
From Zero to Hero: A Complete Learning Journey
📚 Table of Contents
Chapter 1: The Foundation - What is Association Rule Mining?
Chapter 2: Key Terminology - Building Your Vocabulary
Chapter 3: Essential Metrics - The Mathematics Behind
Chapter 4: The Apriori Algorithm - Your First Algorithm
Chapter 5: FP-Growth Algorithm - The Efficient Alternative
Chapter 6: ECLAT Algorithm - The Vertical Approach
Chapter 7: Advanced Metrics & Interestingness Measures
Chapter 8: Multi-Level Association Rules
Chapter 9: Sequential Pattern Mining
Chapter 10: Constraint-Based Mining
Chapter 11: Rare & Negative Association Rules
Chapter 12: Real-World Applications
Chapter 13: Implementation Guide with Python
Chapter 14: Performance Optimization & Scalability
Chapter 15: Interview Questions & Answers
Chapter 1: The Foundation - What is Association Rule Mining? {#chapter-1}
🎯 The Simplest Explanation
Imagine you're a shopkeeper. Every day, you notice patterns:

People who buy bread often buy butter
People who buy diapers often buy beer (yes, this is a famous real discovery!)
People who buy chips often buy cola
Association Rule Mining is the science of automatically discovering these hidden patterns in data.

📖 Formal Definition
Association Rule Mining is a data mining technique used to discover interesting relationships, patterns, correlations, or associations among a set of items in large databases.

🛒 The Classic Example: Market Basket Analysis
text

Transaction 1: {Bread, Milk, Eggs}
Transaction 2: {Bread, Butter, Milk}
Transaction 3: {Bread, Butter}
Transaction 4: {Beer, Diapers, Bread}
Transaction 5: {Beer, Diapers, Milk}
From this data, we might discover:

text

Rule: {Bread} → {Butter}
Meaning: If someone buys Bread, they are likely to buy Butter
🎨 Visual Understanding
text

┌─────────────────────────────────────────────────────────────┐
│                    ASSOCIATION RULE                        │
│                                                             │
│    ANTECEDENT (IF)          CONSEQUENT (THEN)              │
│    ┌──────────────┐         ┌──────────────┐               │
│    │   Bread      │   →     │   Butter     │               │
│    │   Milk       │         │              │               │
│    └──────────────┘         └──────────────┘               │
│                                                             │
│    "If a customer buys Bread and Milk,                     │
│     then they will likely buy Butter"                      │
└─────────────────────────────────────────────────────────────┘
🔑 Key Components
Component	Symbol	Description	Example
Itemset	I	Collection of items	{Bread, Milk, Butter}
Transaction	T	A single purchase/event	{Bread, Milk}
Database	D	Collection of all transactions	All shopping receipts
Rule	X → Y	If X then Y relationship	{Bread} → {Butter}
💡 Why Should You Care?
text

┌─────────────────────────────────────────────────────────────┐
│                 REAL-WORLD IMPACT                          │
├─────────────────────────────────────────────────────────────┤
│ 🏪 Retail: Product placement, cross-selling                │
│ 🏥 Healthcare: Disease correlation, drug interactions      │
│ 🌐 Web: Page recommendations, click patterns               │
│ 🏦 Banking: Fraud detection, customer behavior             │
│ 📱 Telecom: Service bundling, churn prediction             │
└─────────────────────────────────────────────────────────────┘
📝 Chapter 1 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 1: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Association Rules find hidden patterns in data         ║
║  ✓ Format: IF (Antecedent) → THEN (Consequent)           ║
║  ✓ Born from Market Basket Analysis                       ║
║  ✓ Used across many industries                            ║
║  ✓ Foundation of recommendation systems                   ║
╚═══════════════════════════════════════════════════════════╝
Chapter 2: Key Terminology - Building Your Vocabulary {#chapter-2}
📚 Essential Terms You MUST Know
1. Item
text

Definition: A single element or object in your dataset

Example: In a grocery store
- Bread is an item
- Milk is an item  
- Butter is an item
2. Itemset
text

Definition: A collection of one or more items

Types:
┌─────────────────────────────────────────────────┐
│  1-itemset: {Bread}                             │
│  2-itemset: {Bread, Milk}                       │
│  3-itemset: {Bread, Milk, Butter}               │
│  k-itemset: Contains k items                    │
└─────────────────────────────────────────────────┘
3. Transaction
text

Definition: A single record containing a set of items

Example:
Transaction ID: T001
Items: {Bread, Milk, Eggs, Butter}

This represents ONE shopping trip by ONE customer
4. Transaction Database
text

Definition: Complete collection of all transactions

┌────────────┬─────────────────────────┐
│ Trans. ID  │ Items                   │
├────────────┼─────────────────────────┤
│ T001       │ {Bread, Milk, Eggs}     │
│ T002       │ {Bread, Butter}         │
│ T003       │ {Milk, Butter, Cheese}  │
│ T004       │ {Bread, Milk, Butter}   │
│ T005       │ {Bread, Milk}           │
└────────────┴─────────────────────────┘
5. Support Count (Absolute Support)
text

Definition: Number of transactions containing an itemset

Example: How many transactions contain {Bread}?
- T001: ✓ Has Bread
- T002: ✓ Has Bread
- T003: ✗ No Bread
- T004: ✓ Has Bread
- T005: ✓ Has Bread

Support Count of {Bread} = 4
6. Frequent Itemset
text

Definition: An itemset whose support count is ≥ minimum threshold

Example:
If minimum support count = 3
{Bread} appears 4 times → FREQUENT ✓
{Cheese} appears 1 time → NOT FREQUENT ✗
7. Association Rule
text

Definition: An implication expression X → Y

Components:
┌─────────────────────────────────────────────────┐
│  X → Y                                          │
│  │   │                                          │
│  │   └── Consequent (RIGHT side, THEN part)    │
│  │                                              │
│  └────── Antecedent (LEFT side, IF part)       │
└─────────────────────────────────────────────────┘

Example: {Bread, Milk} → {Butter}
- Antecedent: {Bread, Milk}
- Consequent: {Butter}
- Meaning: Customers who buy Bread AND Milk also buy Butter
8. Candidate Itemset
text

Definition: Potentially frequent itemsets being evaluated

Symbol: Cₖ (candidates of size k)

These are "suspects" before we confirm they're frequent
9. Maximal Frequent Itemset
text

Definition: A frequent itemset with NO frequent superset

Example:
Frequent itemsets: {A}, {B}, {AB}, {ABC}

Is {AB} maximal? 
- {ABC} contains {AB} and is frequent
- So {AB} is NOT maximal

Is {ABC} maximal?
- No larger frequent itemset contains {ABC}
- So {ABC} IS maximal ✓
10. Closed Itemset
text

Definition: An itemset with no superset having the same support

Example:
{AB} appears in 5 transactions
{ABC} appears in 3 transactions

Since {ABC} has different support than {AB},
{AB} is a CLOSED itemset ✓
🎯 Visual Comparison: Maximal vs Closed
text

              All Itemsets
                  │
         ┌───────┴───────┐
         │               │
    Frequent         Infrequent
    Itemsets         Itemsets
         │
    ┌────┴────┐
    │         │
  Closed   Not Closed
  Itemsets
    │
    ├── Some are Maximal
    │
    └── Some are Not Maximal

RELATIONSHIP:
╔═══════════════════════════════════════════════════════════╗
║  Maximal Frequent ⊂ Closed Frequent ⊂ All Frequent       ║
╚═══════════════════════════════════════════════════════════╝
📊 Complete Terminology Table
Term	Symbol	Formula/Description
Item	i	Single element
Itemset	X, Y	Set of items
k-itemset	Lₖ	Itemset with k items
Transaction	T	Single record
Database	D	All transactions
Support Count	σ(X)	Count of X in D
Candidate Set	Cₖ	Potential frequent k-itemsets
Frequent Set	Fₖ or Lₖ	Confirmed frequent k-itemsets
Min Support	min_sup	User-defined threshold
Min Confidence	min_conf	User-defined threshold
📝 Chapter 2 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 2: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Item = single element                                  ║
║  ✓ Itemset = collection of items                          ║
║  ✓ Transaction = one record/purchase                      ║
║  ✓ Frequent = meets minimum support threshold             ║
║  ✓ Rule = Antecedent → Consequent                        ║
║  ✓ Maximal ⊂ Closed ⊂ Frequent                           ║
╚═══════════════════════════════════════════════════════════╝
Chapter 3: Essential Metrics - The Mathematics Behind {#chapter-3}
🎯 The Three Pillars of Association Rules
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│              THE HOLY TRINITY OF METRICS                    │
│                                                             │
│         ┌─────────┐  ┌────────────┐  ┌──────┐             │
│         │ SUPPORT │  │ CONFIDENCE │  │ LIFT │             │
│         └─────────┘  └────────────┘  └──────┘             │
│              │              │            │                  │
│         How often?    How reliable?   How strong?          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📊 Metric 1: SUPPORT
What is Support?
Support measures how frequently an itemset appears in the database.

Formula
text

                    Number of transactions containing X
Support(X) = ──────────────────────────────────────────────
                    Total number of transactions

                         σ(X)
Support(X) = ─────
                          N
Example Walkthrough
text

Database D:
┌─────┬─────────────────────┐
│ TID │ Items               │
├─────┼─────────────────────┤
│ T1  │ {Bread, Milk}       │
│ T2  │ {Bread, Butter}     │
│ T3  │ {Milk, Butter}      │
│ T4  │ {Bread, Milk, Butter}│
│ T5  │ {Bread, Milk}       │
└─────┴─────────────────────┘

Total Transactions (N) = 5

Calculate Support({Bread}):
- T1: ✓ Contains Bread
- T2: ✓ Contains Bread
- T3: ✗ No Bread
- T4: ✓ Contains Bread
- T5: ✓ Contains Bread

Support({Bread}) = 4/5 = 0.80 = 80%

Calculate Support({Bread, Milk}):
- T1: ✓ Contains both
- T2: ✗ Missing Milk
- T3: ✗ Missing Bread
- T4: ✓ Contains both
- T5: ✓ Contains both

Support({Bread, Milk}) = 3/5 = 0.60 = 60%
Support Interpretation
text

┌─────────────────────────────────────────────────────────────┐
│  SUPPORT VALUE          │  INTERPRETATION                  │
├─────────────────────────────────────────────────────────────┤
│  0.01 (1%)              │  Very rare, appears 1 in 100     │
│  0.10 (10%)             │  Uncommon                        │
│  0.30 (30%)             │  Moderately common               │
│  0.50 (50%)             │  Common, appears half the time   │
│  0.80 (80%)             │  Very common                     │
│  1.00 (100%)            │  Appears in ALL transactions     │
└─────────────────────────────────────────────────────────────┘
📊 Metric 2: CONFIDENCE
What is Confidence?
Confidence measures how often the rule is correct - the probability of Y given X.

Formula
text

                         Support(X ∪ Y)
Confidence(X → Y) = ─────────────────────
                          Support(X)

Also written as:

                    P(Y | X) = P(X and Y) / P(X)
Example Walkthrough
text

Using same database:

Calculate Confidence({Bread} → {Milk}):

Step 1: Find Support({Bread, Milk})
        = 3/5 = 0.60

Step 2: Find Support({Bread})
        = 4/5 = 0.80

Step 3: Calculate Confidence
        = 0.60 / 0.80
        = 0.75 = 75%

INTERPRETATION: 
When customers buy Bread, 75% of the time they also buy Milk
⚠️ Important: Confidence is NOT Symmetric!
text

Confidence({Bread} → {Milk}) ≠ Confidence({Milk} → {Bread})

Let's prove it:

Confidence({Bread} → {Milk}):
= Support({Bread, Milk}) / Support({Bread})
= 0.60 / 0.80 = 0.75 = 75%

Confidence({Milk} → {Bread}):
= Support({Bread, Milk}) / Support({Milk})

Support({Milk}) = 4/5 = 0.80 (appears in T1, T3, T4, T5)

= 0.60 / 0.80 = 0.75 = 75%

(In this case they happen to be equal, but that's coincidental!)
Confidence Interpretation
text

┌─────────────────────────────────────────────────────────────┐
│  CONFIDENCE VALUE       │  INTERPRETATION                  │
├─────────────────────────────────────────────────────────────┤
│  0.50 (50%)             │  Rule correct half the time      │
│  0.70 (70%)             │  Reasonably reliable             │
│  0.85 (85%)             │  Highly reliable                 │
│  0.95 (95%)             │  Very strong rule                │
│  1.00 (100%)            │  Always true (deterministic)     │
└─────────────────────────────────────────────────────────────┘
📊 Metric 3: LIFT
What is Lift?
Lift measures how much more likely Y is purchased when X is purchased, compared to Y's general popularity.

Formula
text

                         Confidence(X → Y)
Lift(X → Y) = ──────────────────────────────────
                       Support(Y)

Also written as:

                    Support(X ∪ Y)
Lift(X → Y) = ─────────────────────────────
               Support(X) × Support(Y)
Example Walkthrough
text

Calculate Lift({Bread} → {Milk}):

Step 1: Find Confidence({Bread} → {Milk})
        = 0.75

Step 2: Find Support({Milk})
        = 4/5 = 0.80

Step 3: Calculate Lift
        = 0.75 / 0.80
        = 0.9375

INTERPRETATION:
Lift < 1 means buying Bread slightly DECREASES 
the likelihood of buying Milk compared to random chance!
🎯 Lift Interpretation Guide
text

┌─────────────────────────────────────────────────────────────┐
│                      LIFT VALUES                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Lift = 1.0    │  INDEPENDENT                              │
│                │  X and Y have no relationship              │
│                │  Buying X doesn't affect Y                 │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Lift > 1.0    │  POSITIVE CORRELATION                     │
│                │  X and Y appear together more often        │
│                │  than expected by chance                   │
│                │  Example: Lift = 2.5 means 2.5x more       │
│                │  likely to buy Y when buying X             │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Lift < 1.0    │  NEGATIVE CORRELATION                     │
│                │  X and Y appear together LESS often        │
│                │  Buying X decreases likelihood of Y        │
│                │  Example: Lift = 0.5 means half as         │
│                │  likely to buy Y when buying X             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🔢 Complete Example: All Three Metrics
text

DATABASE:
┌─────┬──────────────────────────┐
│ TID │ Items                    │
├─────┼──────────────────────────┤
│ T1  │ {Bread, Milk, Butter}    │
│ T2  │ {Bread, Milk}            │
│ T3  │ {Bread, Butter}          │
│ T4  │ {Milk, Butter, Cheese}   │
│ T5  │ {Bread, Milk, Butter}    │
│ T6  │ {Bread, Milk}            │
│ T7  │ {Milk, Cheese}           │
│ T8  │ {Bread, Butter}          │
│ T9  │ {Bread, Milk, Butter}    │
│ T10 │ {Milk, Butter}           │
└─────┴──────────────────────────┘

N = 10 transactions

STEP 1: Calculate Individual Supports
────────────────────────────────────
Support(Bread)  = 8/10 = 0.80
Support(Milk)   = 8/10 = 0.80
Support(Butter) = 7/10 = 0.70

STEP 2: Calculate Itemset Supports
────────────────────────────────────
Support(Bread, Milk)   = 6/10 = 0.60
Support(Bread, Butter) = 5/10 = 0.50
Support(Milk, Butter)  = 5/10 = 0.50

STEP 3: Evaluate Rule {Bread} → {Milk}
────────────────────────────────────

Support = Support(Bread, Milk) = 0.60 = 60%
✓ This rule applies to 60% of all transactions

Confidence = Support(Bread, Milk) / Support(Bread)
           = 0.60 / 0.80
           = 0.75 = 75%
✓ When customers buy Bread, 75% also buy Milk

Lift = Confidence / Support(Milk)
     = 0.75 / 0.80
     = 0.9375
✓ Slightly negative correlation (Lift < 1)

STEP 4: Evaluate Rule {Butter} → {Bread}
────────────────────────────────────

Support = Support(Bread, Butter) = 0.50 = 50%

Confidence = Support(Bread, Butter) / Support(Butter)
           = 0.50 / 0.70
           = 0.714 = 71.4%

Lift = 0.714 / 0.80 = 0.893
📐 Summary Formulas Card
text

╔═══════════════════════════════════════════════════════════════╗
║                    FORMULA QUICK REFERENCE                    ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  SUPPORT(X → Y)                                              ║
║  ─────────────────                                           ║
║  = σ(X ∪ Y) / N                                              ║
║  = P(X and Y)                                                 ║
║  Range: [0, 1]                                                ║
║                                                               ║
║  CONFIDENCE(X → Y)                                           ║
║  ─────────────────────                                       ║
║  = Support(X ∪ Y) / Support(X)                               ║
║  = P(Y | X)                                                   ║
║  Range: [0, 1]                                                ║
║                                                               ║
║  LIFT(X → Y)                                                 ║
║  ─────────────                                               ║
║  = Confidence(X → Y) / Support(Y)                            ║
║  = Support(X ∪ Y) / (Support(X) × Support(Y))                ║
║  Range: [0, ∞)                                                ║
║  Interpretation: =1 independent, >1 positive, <1 negative    ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
📝 Chapter 3 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 3: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Support = How frequently items appear together         ║
║  ✓ Confidence = How often the rule is correct             ║
║  ✓ Lift = True correlation strength                       ║
║  ✓ Always check ALL THREE metrics                         ║
║  ✓ Lift > 1 = meaningful positive relationship            ║
║  ✓ High confidence can be misleading without lift         ║
╚═══════════════════════════════════════════════════════════╝
Chapter 4: The Apriori Algorithm - Your First Algorithm {#chapter-4}
🎯 The Big Idea
The Problem
Finding all frequent itemsets by brute force is computationally impossible:

100 items = 2¹⁰⁰ possible itemsets (more than atoms in universe!)
We need a smarter approach
The Solution: Apriori Principle
text

╔═══════════════════════════════════════════════════════════════╗
║                  THE APRIORI PRINCIPLE                        ║
║                 (Most Important Concept!)                     ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  "If an itemset is INFREQUENT, then ALL its                  ║
║   supersets must also be INFREQUENT"                         ║
║                                                               ║
║  EQUIVALENTLY:                                                ║
║  "All subsets of a FREQUENT itemset must be FREQUENT"        ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
Visual Understanding
text

                    {A, B, C, D}
                    /    |    \
              {A,B,C} {A,B,D} {B,C,D}  {A,C,D}
               / \      |  \    / \      / \
           {A,B} {A,C} {B,C} {A,D} {B,D} {C,D}
             |     |     |     |     |     |
            {A}   {B}   {C}   {D}
            
If {A,B} is INFREQUENT:
- {A,B,C} must be INFREQUENT
- {A,B,D} must be INFREQUENT  
- {A,B,C,D} must be INFREQUENT

We can PRUNE entire branches! This saves massive computation!
🔄 The Apriori Algorithm Steps
High-Level Overview
text

┌─────────────────────────────────────────────────────────────┐
│                    APRIORI WORKFLOW                         │
│                                                             │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐ │
│  │ Find    │    │Generate │    │  Prune  │    │ Repeat  │ │
│  │Frequent │ →  │Candidate│ →  │Infreq.  │ →  │ Until   │ │
│  │1-items  │    │(k+1)    │    │Candidates│   │ Empty   │ │
│  └─────────┘    └─────────┘    └─────────┘    └─────────┘ │
│       │              ↑                              │       │
│       └──────────────┴──────────────────────────────┘       │
└─────────────────────────────────────────────────────────────┘
Detailed Algorithm
text

APRIORI ALGORITHM:
═══════════════════

INPUT:
- D: Transaction database
- min_sup: Minimum support threshold

OUTPUT:
- L: All frequent itemsets

ALGORITHM:
──────────

Step 1: Generate L₁ (frequent 1-itemsets)
        Scan database, count each item
        Keep items with support ≥ min_sup

Step 2: k = 1

Step 3: REPEAT while Lₖ is not empty:
        
        3a. CANDIDATE GENERATION
            Generate Cₖ₊₁ from Lₖ
            (Join step + Prune step)
        
        3b. CANDIDATE PRUNING
            Remove candidates with infrequent subsets
        
        3c. SUPPORT COUNTING
            Scan database to count support of each candidate
        
        3d. CANDIDATE ELIMINATION
            Lₖ₊₁ = candidates in Cₖ₊₁ with support ≥ min_sup
        
        3e. k = k + 1

Step 4: RETURN L = L₁ ∪ L₂ ∪ L₃ ∪ ... ∪ Lₖ
🔢 Complete Worked Example
text

TRANSACTION DATABASE:
┌─────┬───────────────────┐
│ TID │ Items             │
├─────┼───────────────────┤
│ T1  │ {A, B, E}         │
│ T2  │ {B, D}            │
│ T3  │ {B, C}            │
│ T4  │ {A, B, D}         │
│ T5  │ {A, C}            │
│ T6  │ {B, C}            │
│ T7  │ {A, C}            │
│ T8  │ {A, B, C, E}      │
│ T9  │ {A, B, C}         │
└─────┴───────────────────┘

N = 9 transactions
Minimum Support = 2 (or 2/9 = 22.2%)

════════════════════════════════════════════════════════════════
ITERATION 1: Find Frequent 1-itemsets
════════════════════════════════════════════════════════════════

Scan database and count each item:

┌────────────────────────────────────────────────┐
│  CANDIDATE 1-ITEMSETS (C₁)                     │
├──────────┬───────────────┬─────────────────────┤
│  Itemset │ Support Count │ Support             │
├──────────┼───────────────┼─────────────────────┤
│  {A}     │ 6             │ 6/9 = 66.7%         │
│  {B}     │ 7             │ 7/9 = 77.8%         │
│  {C}     │ 6             │ 6/9 = 66.7%         │
│  {D}     │ 2             │ 2/9 = 22.2%         │
│  {E}     │ 2             │ 2/9 = 22.2%         │
└──────────┴───────────────┴─────────────────────┘

Filter: Keep items with count ≥ 2

┌────────────────────────────────────────────────┐
│  FREQUENT 1-ITEMSETS (L₁)                      │
├──────────┬───────────────┬─────────────────────┤
│  Itemset │ Support Count │ Status              │
├──────────┼───────────────┼─────────────────────┤
│  {A}     │ 6             │ ✓ Frequent          │
│  {B}     │ 7             │ ✓ Frequent          │
│  {C}     │ 6             │ ✓ Frequent          │
│  {D}     │ 2             │ ✓ Frequent          │
│  {E}     │ 2             │ ✓ Frequent          │
└──────────┴───────────────┴─────────────────────┘

L₁ = {{A}, {B}, {C}, {D}, {E}}

════════════════════════════════════════════════════════════════
ITERATION 2: Find Frequent 2-itemsets
════════════════════════════════════════════════════════════════

STEP 2a: Generate Candidates (Join L₁ with L₁)
─────────────────────────────────────────────────

Combine all pairs from L₁:

C₂ = {{A,B}, {A,C}, {A,D}, {A,E}, {B,C}, {B,D}, {B,E}, {C,D}, {C,E}, {D,E}}

STEP 2b: Prune (All 1-subsets are in L₁, so no pruning needed)
───────────────────────────────────────────────────────────────

STEP 2c: Scan database and count:
─────────────────────────────────

┌──────────┬───────────────┬─────────────────────────────────────┐
│  Itemset │ Support Count │ Transactions                        │
├──────────┼───────────────┼─────────────────────────────────────┤
│  {A,B}   │ 4             │ T1, T4, T8, T9                      │
│  {A,C}   │ 4             │ T5, T7, T8, T9                      │
│  {A,D}   │ 1             │ T4                                  │
│  {A,E}   │ 2             │ T1, T8                              │
│  {B,C}   │ 4             │ T3, T6, T8, T9                      │
│  {B,D}   │ 2             │ T2, T4                              │
│  {B,E}   │ 2             │ T1, T8                              │
│  {C,D}   │ 0             │ -                                   │
│  {C,E}   │ 1             │ T8                                  │
│  {D,E}   │ 0             │ -                                   │
└──────────┴───────────────┴─────────────────────────────────────┘

STEP 2d: Filter with min_sup = 2:
─────────────────────────────────

┌────────────────────────────────────────────────┐
│  FREQUENT 2-ITEMSETS (L₂)                      │
├──────────┬───────────────┬─────────────────────┤
│  Itemset │ Support Count │ Status              │
├──────────┼───────────────┼─────────────────────┤
│  {A,B}   │ 4             │ ✓ Frequent          │
│  {A,C}   │ 4             │ ✓ Frequent          │
│  {A,E}   │ 2             │ ✓ Frequent          │
│  {B,C}   │ 4             │ ✓ Frequent          │
│  {B,D}   │ 2             │ ✓ Frequent          │
│  {B,E}   │ 2             │ ✓ Frequent          │
└──────────┴───────────────┴─────────────────────┘

L₂ = {{A,B}, {A,C}, {A,E}, {B,C}, {B,D}, {B,E}}

PRUNED: {A,D}, {C,D}, {C,E}, {D,E} - Support < 2

════════════════════════════════════════════════════════════════
ITERATION 3: Find Frequent 3-itemsets  
════════════════════════════════════════════════════════════════

STEP 3a: Generate Candidates (Join L₂ with L₂)
─────────────────────────────────────────────────

Rule: Join itemsets that share (k-1) items

{A,B} ∪ {A,C} → {A,B,C} ✓ (share {A})
{A,B} ∪ {A,E} → {A,B,E} ✓ (share {A})
{A,B} ∪ {B,C} → {A,B,C} ✓ (already have)
{A,B} ∪ {B,D} → {A,B,D} ✓ (share {B})
{A,B} ∪ {B,E} → {A,B,E} ✓ (already have)
{A,C} ∪ {A,E} → {A,C,E} ✓ (share {A})
{A,C} ∪ {B,C} → {A,B,C} ✓ (already have)
{A,E} ∪ {B,E} → {A,B,E} ✓ (already have)
{B,C} ∪ {B,D} → {B,C,D} ✓ (share {B})
{B,C} ∪ {B,E} → {B,C,E} ✓ (share {B})
{B,D} ∪ {B,E} → {B,D,E} ✓ (share {B})

Candidates: {A,B,C}, {A,B,E}, {A,B,D}, {A,C,E}, {B,C,D}, {B,C,E}, {B,D,E}

STEP 3b: Prune using Apriori Principle
──────────────────────────────────────

For each candidate, check if ALL 2-subsets are in L₂:

{A,B,C}: Subsets = {A,B}✓ {A,C}✓ {B,C}✓ → KEEP
{A,B,E}: Subsets = {A,B}✓ {A,E}✓ {B,E}✓ → KEEP
{A,B,D}: Subsets = {A,B}✓ {A,D}✗ {B,D}✓ → PRUNE (A,D not in L₂)
{A,C,E}: Subsets = {A,C}✓ {A,E}✓ {C,E}✗ → PRUNE (C,E not in L₂)
{B,C,D}: Subsets = {B,C}✓ {B,D}✓ {C,D}✗ → PRUNE (C,D not in L₂)
{B,C,E}: Subsets = {B,C}✓ {B,E}✓ {C,E}✗ → PRUNE (C,E not in L₂)
{B,D,E}: Subsets = {B,D}✓ {B,E}✓ {D,E}✗ → PRUNE (D,E not in L₂)

C₃ after pruning = {{A,B,C}, {A,B,E}}

STEP 3c: Scan database and count:
─────────────────────────────────

┌──────────┬───────────────┬─────────────────────┐
│  Itemset │ Support Count │ Transactions        │
├──────────┼───────────────┼─────────────────────┤
│  {A,B,C} │ 2             │ T8, T9              │
│  {A,B,E} │ 2             │ T1, T8              │
└──────────┴───────────────┴─────────────────────┘

Both have support ≥ 2, so:

L₃ = {{A,B,C}, {A,B,E}}

════════════════════════════════════════════════════════════════
ITERATION 4: Find Frequent 4-itemsets
════════════════════════════════════════════════════════════════

STEP 4a: Generate Candidates
────────────────────────────

{A,B,C} ∪ {A,B,E} → {A,B,C,E} (share {A,B})

C₄ = {{A,B,C,E}}

STEP 4b: Prune
──────────────

{A,B,C,E}: Check all 3-subsets
- {A,B,C} ✓ in L₃
- {A,B,E} ✓ in L₃
- {A,C,E} ✗ NOT in L₃
- {B,C,E} ✗ NOT in L₃

PRUNED! C₄ becomes empty.

════════════════════════════════════════════════════════════════
FINAL RESULT
════════════════════════════════════════════════════════════════

ALL FREQUENT ITEMSETS:
┌─────────────────────────────────────────────────┐
│  L₁ = {{A}, {B}, {C}, {D}, {E}}                │
│  L₂ = {{A,B}, {A,C}, {A,E}, {B,C}, {B,D}, {B,E}}│
│  L₃ = {{A,B,C}, {A,B,E}}                       │
└─────────────────────────────────────────────────┘
🔧 Candidate Generation: The Join Step
text

JOIN PROCEDURE (Fₖ-1 × Fₖ-1 → Cₖ):
═══════════════════════════════════

Two itemsets can be joined if they differ only in the LAST item
(assuming items are sorted)

Example: Generating C₃ from L₂

L₂ sorted: {A,B}, {A,C}, {A,E}, {B,C}, {B,D}, {B,E}

Joinable pairs (share first k-2 items):
- {A,B} and {A,C} → share {A} → join to get {A,B,C}
- {A,B} and {A,E} → share {A} → join to get {A,B,E}
- {A,C} and {A,E} → share {A} → join to get {A,C,E}
- {B,C} and {B,D} → share {B} → join to get {B,C,D}
- {B,C} and {B,E} → share {B} → join to get {B,C,E}
- {B,D} and {B,E} → share {B} → join to get {B,D,E}
⏱️ Complexity Analysis
text

┌─────────────────────────────────────────────────────────────┐
│                 APRIORI COMPLEXITY                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  TIME COMPLEXITY:                                           │
│  - Candidate generation: O(|Lₖ|²)                          │
│  - Database scanning: O(N × C) per iteration                │
│  - Total: O(N × Σ|Cₖ|) where N = #transactions             │
│                                                             │
│  SPACE COMPLEXITY:                                          │
│  - O(|Cₖ|) to store candidates                             │
│                                                             │
│  BOTTLENECK:                                                │
│  - Multiple database scans (one per iteration)              │
│  - Large number of candidates                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
✅ Advantages & ❌ Disadvantages
text

┌─────────────────────────────────────────────────────────────┐
│  ADVANTAGES ✅                                              │
├─────────────────────────────────────────────────────────────┤
│  • Simple and easy to understand                            │
│  • Uses Apriori principle for efficient pruning             │
│  • Works well with sparse data                              │
│  • Guaranteed to find all frequent itemsets                 │
│  • Highly parallelizable                                    │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│  DISADVANTAGES ❌                                           │
├─────────────────────────────────────────────────────────────┤
│  • Multiple database scans (expensive I/O)                  │
│  • Generates too many candidates                            │
│  • Struggles with low minimum support                       │
│  • Not suitable for dense data                              │
│  • Memory intensive for large candidate sets                │
└─────────────────────────────────────────────────────────────┘
📝 Chapter 4 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 4: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Apriori Principle: Infrequent subset = Infrequent set  ║
║  ✓ Level-wise approach: L₁ → L₂ → L₃ → ...               ║
║  ✓ Generate-and-Test: Create candidates, then verify      ║
║  ✓ Join Step: Combine (k-1) itemsets to get k-itemsets    ║
║  ✓ Prune Step: Remove candidates with infrequent subsets  ║
║  ✓ Major bottleneck: Multiple database scans              ║
╚═══════════════════════════════════════════════════════════╝
Chapter 5: FP-Growth Algorithm - The Efficient Alternative {#chapter-5}
🎯 Why FP-Growth?
text

┌─────────────────────────────────────────────────────────────┐
│           APRIORI'S PROBLEMS → FP-GROWTH'S SOLUTIONS       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  APRIORI PROBLEM          │  FP-GROWTH SOLUTION            │
│  ─────────────────────────│───────────────────────────────  │
│  Multiple DB scans        │  Only 2 DB scans               │
│  Generates many candidates │  No candidate generation       │
│  Slow for low min_sup     │  Efficient at low min_sup      │
│  Memory for candidates    │  Compact FP-Tree structure     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📊 The FP-Tree Structure
What is an FP-Tree?
An FP-Tree (Frequent Pattern Tree) is a compressed representation of the database that stores frequency information.

FP-Tree Components
text

┌─────────────────────────────────────────────────────────────┐
│                    FP-TREE COMPONENTS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. ROOT NODE: Labeled "null" or "root"                    │
│                                                             │
│  2. ITEM-PREFIX SUBTREES: Children of root                 │
│     - Each node contains: item name, count, node-link      │
│                                                             │
│  3. HEADER TABLE: Links to same items in tree              │
│     - Item name                                             │
│     - Support count                                         │
│     - Head of node-link                                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🔄 FP-Growth Algorithm Steps
text

FP-GROWTH ALGORITHM:
════════════════════

PHASE 1: FP-Tree Construction
─────────────────────────────
1. Scan DB to find frequent 1-itemsets
2. Sort items by descending frequency
3. Scan DB again, build FP-Tree:
   - For each transaction:
     a. Sort items by frequency order
     b. Insert into tree (create/update path)

PHASE 2: Mining Frequent Patterns
─────────────────────────────────
1. Start from header table (bottom item)
2. For each item:
   a. Construct conditional pattern base
   b. Build conditional FP-Tree
   c. Recursively mine patterns
🔢 Complete Worked Example
text

TRANSACTION DATABASE:
┌─────┬───────────────────┐
│ TID │ Items             │
├─────┼───────────────────┤
│ T1  │ {A, B, E}         │
│ T2  │ {B, D}            │
│ T3  │ {B, C}            │
│ T4  │ {A, B, D}         │
│ T5  │ {A, C}            │
│ T6  │ {B, C}            │
│ T7  │ {A, C}            │
│ T8  │ {A, B, C, E}      │
│ T9  │ {A, B, C}         │
└─────┴───────────────────┘

Minimum Support = 2

════════════════════════════════════════════════════════════════
PHASE 1: FP-TREE CONSTRUCTION
════════════════════════════════════════════════════════════════

STEP 1: First DB Scan - Count frequencies
──────────────────────────────────────────

┌──────┬───────────────┐
│ Item │ Support Count │
├──────┼───────────────┤
│  A   │ 6             │
│  B   │ 7             │ ← Most frequent
│  C   │ 6             │
│  D   │ 2             │
│  E   │ 2             │ ← Least frequent
└──────┴───────────────┘

All items have support ≥ 2, so all are frequent.

STEP 2: Sort items by descending frequency
──────────────────────────────────────────

Frequency order: B(7) > A(6) = C(6) > D(2) = E(2)
For ties, use alphabetical: B > A > C > D > E

STEP 3: Create Header Table
───────────────────────────

┌────────────────────────────────────────┐
│         HEADER TABLE                   │
├──────┬───────────────┬─────────────────┤
│ Item │ Support Count │ Node-Link       │
├──────┼───────────────┼─────────────────┤
│  B   │ 7             │ → (first B node)│
│  A   │ 6             │ → (first A node)│
│  C   │ 6             │ → (first C node)│
│  D   │ 2             │ → (first D node)│
│  E   │ 2             │ → (first E node)│
└──────┴───────────────┴─────────────────┘

STEP 4: Second DB Scan - Build FP-Tree
──────────────────────────────────────

Process each transaction (items sorted by frequency):

T1: {A, B, E} → Sorted: {B, A, E}
    Insert path: root → B:1 → A:1 → E:1

                [root]
                   │
                 [B:1]
                   │
                 [A:1]
                   │
                 [E:1]

T2: {B, D} → Sorted: {B, D}
    Insert: root → B (increment) → D:1

                [root]
                   │
                 [B:2]
                 /   \
             [A:1]   [D:1]
               │
             [E:1]

T3: {B, C} → Sorted: {B, C}
    Insert: root → B (increment) → C:1

                   [root]
                      │
                    [B:3]
                   /  |  \
               [A:1][C:1][D:1]
                 │
               [E:1]

T4: {A, B, D} → Sorted: {B, A, D}
    Insert: root → B (increment) → A (increment) → D:1

                     [root]
                        │
                      [B:4]
                    /  |   \
                [A:2] [C:1] [D:1]
                /   \
             [E:1] [D:1]

T5: {A, C} → Sorted: {A, C}
    New path from root: root → A:1 → C:1

                        [root]
                       /      \
                    [B:4]     [A:1]
                  /  |   \       \
              [A:2][C:1][D:1]   [C:1]
              /   \
           [E:1] [D:1]

T6: {B, C} → Sorted: {B, C}
    Insert: root → B (increment) → C (increment)

                        [root]
                       /      \
                    [B:5]     [A:1]
                  /  |   \       \
              [A:2][C:2][D:1]   [C:1]
              /   \
           [E:1] [D:1]

T7: {A, C} → Sorted: {A, C}
    Insert: root → A (increment) → C (increment)

                        [root]
                       /      \
                    [B:5]     [A:2]
                  /  |   \       \
              [A:2][C:2][D:1]   [C:2]
              /   \
           [E:1] [D:1]

T8: {A, B, C, E} → Sorted: {B, A, C, E}
    Insert: root → B (increment) → A (increment) → C:1 → E:1

                        [root]
                       /      \
                    [B:6]     [A:2]
                  /  |   \       \
              [A:3][C:2][D:1]   [C:2]
              /   \
           [E:1] [D:1]
             \
            [C:1]
              \
             [E:1]

T9: {A, B, C} → Sorted: {B, A, C}
    Insert: root → B (increment) → A (increment) → C (increment)

FINAL FP-TREE:
══════════════

                           [root]
                          /      \
                       [B:7]     [A:2]
                      / |  \        \
                 [A:4][C:2][D:1]   [C:2]
                /  |  \
             [E:1][D:1][C:2]
                        \
                       [E:1]

HEADER TABLE WITH NODE-LINKS:
┌──────┬───────┬────────────────────────────────────────┐
│ Item │ Count │ Node-Links                             │
├──────┼───────┼────────────────────────────────────────┤
│  B   │   7   │ [B:7]                                  │
│  A   │   6   │ [A:4] → [A:2]                         │
│  C   │   6   │ [C:2] → [C:2] → [C:2]                 │
│  D   │   2   │ [D:1] → [D:1]                         │
│  E   │   2   │ [E:1] → [E:1]                         │
└──────┴───────┴────────────────────────────────────────┘

════════════════════════════════════════════════════════════════
PHASE 2: MINING FREQUENT PATTERNS
════════════════════════════════════════════════════════════════

Start from the bottom of header table (least frequent item).

MINING FOR ITEM E:
──────────────────

Step 1: Find all paths containing E

Path 1: root → B:7 → A:4 → E:1  (count = 1)
Path 2: root → B:7 → A:4 → C:2 → E:1  (count = 1)

Step 2: Construct Conditional Pattern Base for E

┌──────────────────────────────────────┐
│  CONDITIONAL PATTERN BASE FOR E      │
├──────────────────────────────────────┤
│  {B, A}: 1                           │
│  {B, A, C}: 1                        │
└──────────────────────────────────────┘

Step 3: Build Conditional FP-Tree for E

Count items in conditional pattern base:
- B: 1 + 1 = 2 ✓
- A: 1 + 1 = 2 ✓
- C: 0 + 1 = 1 ✗ (less than min_sup)

Conditional FP-Tree for E:
       [root]
          │
        [B:2]
          │
        [A:2]

Step 4: Mine conditional FP-Tree recursively

From single path: {B, A}
- Pattern: {E} - support 2
- Pattern: {A, E} - support 2
- Pattern: {B, E} - support 2
- Pattern: {B, A, E} - support 2

FREQUENT PATTERNS CONTAINING E:
{E}:2, {A,E}:2, {B,E}:2, {B,A,E}:2

MINING FOR ITEM D:
──────────────────

Conditional Pattern Base for D:
- Path: root → B → A → D:1 → gives {B, A}:1
- Path: root → B → D:1 → gives {B}:1

┌──────────────────────────────────────┐
│  CONDITIONAL PATTERN BASE FOR D      │
├──────────────────────────────────────┤
│  {B, A}: 1                           │
│  {B}: 1                              │
└──────────────────────────────────────┘

Count items:
- B: 1 + 1 = 2 ✓
- A: 1 + 0 = 1 ✗

Conditional FP-Tree for D:
       [root]
          │
        [B:2]

FREQUENT PATTERNS CONTAINING D:
{D}:2, {B,D}:2

MINING FOR ITEM C:
──────────────────

Conditional Pattern Base for C:
- Path 1: {B}: 2
- Path 2: {B, A}: 2
- Path 3: {A}: 2

Count items:
- B: 2 + 2 = 4 ✓
- A: 0 + 2 + 2 = 4 ✓

Conditional FP-Tree for C:
          [root]
         /      \
      [B:4]    [A:2]
         |
      [A:2]

Mining this tree:
- {C}: 6
- {B, C}: 4
- {A, C}: 4
- {B, A, C}: 2

FREQUENT PATTERNS CONTAINING C:
{C}:6, {B,C}:4, {A,C}:4, {B,A,C}:2

MINING FOR ITEM A:
──────────────────

Conditional Pattern Base for A:
- {B}: 4

FREQUENT PATTERNS CONTAINING A:
{A}:6, {B,A}:4

MINING FOR ITEM B:
──────────────────

B is at root level, single pattern:
{B}:7

════════════════════════════════════════════════════════════════
COMPLETE RESULTS
════════════════════════════════════════════════════════════════

┌────────────────────────────────────────────────────────────┐
│             ALL FREQUENT ITEMSETS                          │
├──────────────────────┬─────────────────────────────────────┤
│  1-itemsets          │  {B}:7, {A}:6, {C}:6, {D}:2, {E}:2 │
├──────────────────────┼─────────────────────────────────────┤
│  2-itemsets          │  {B,A}:4, {B,C}:4, {A,C}:4,        │
│                      │  {B,D}:2, {A,E}:2, {B,E}:2         │
├──────────────────────┼─────────────────────────────────────┤
│  3-itemsets          │  {B,A,C}:2, {B,A,E}:2              │
└──────────────────────┴─────────────────────────────────────┘
📐 FP-Tree Properties
text

┌─────────────────────────────────────────────────────────────┐
│              FP-TREE PROPERTIES                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. COMPLETENESS                                            │
│     Contains all information needed for mining              │
│     No information loss from original database              │
│                                                             │
│  2. COMPACTNESS                                             │
│     Shared prefixes reduce storage                          │
│     More frequent items near root = more sharing            │
│                                                             │
│  3. ORDERING PROPERTY                                       │
│     Items ordered by decreasing frequency                   │
│     Guarantees optimal compression                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
⏱️ Complexity Comparison
text

┌─────────────────────────────────────────────────────────────┐
│           APRIORI vs FP-GROWTH COMPARISON                   │
├──────────────────────┬──────────────┬───────────────────────┤
│  Aspect              │   Apriori    │    FP-Growth          │
├──────────────────────┼──────────────┼───────────────────────┤
│  Database Scans      │   Multiple   │    Exactly 2          │
│  Candidate Gen       │   Yes        │    No                 │
│  Memory Usage        │   High       │    Moderate           │
│  Performance         │   Slower     │    2x-10x faster      │
│  Low Min Support     │   Poor       │    Good               │
│  Sparse Data         │   Good       │    Excellent          │
│  Dense Data          │   Moderate   │    Can be worse       │
└──────────────────────┴──────────────┴───────────────────────┘
📝 Chapter 5 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 5: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ FP-Growth uses only 2 database scans                   ║
║  ✓ No candidate generation needed                         ║
║  ✓ FP-Tree compresses database efficiently                ║
║  ✓ Mining uses divide-and-conquer approach                ║
║  ✓ Conditional pattern base → Conditional FP-Tree         ║
║  ✓ Generally faster than Apriori                          ║
╚═══════════════════════════════════════════════════════════╝
Chapter 6: ECLAT Algorithm - The Vertical Approach {#chapter-6}
🎯 The Key Difference
text

┌─────────────────────────────────────────────────────────────┐
│         HORIZONTAL vs VERTICAL DATA FORMAT                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  HORIZONTAL (Apriori, FP-Growth):                          │
│  ┌─────┬──────────────┐                                    │
│  │ TID │ Items        │                                    │
│  ├─────┼──────────────┤                                    │
│  │ T1  │ {A, B, C}    │                                    │
│  │ T2  │ {A, C}       │                                    │
│  │ T3  │ {B, C}       │                                    │
│  └─────┴──────────────┘                                    │
│                                                             │
│  VERTICAL (ECLAT):                                         │
│  ┌──────┬────────────────┐                                 │
│  │ Item │ TID-set        │                                 │
│  ├──────┼────────────────┤                                 │
│  │ A    │ {T1, T2}       │                                 │
│  │ B    │ {T1, T3}       │                                 │
│  │ C    │ {T1, T2, T3}   │                                 │
│  └──────┴────────────────┘                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📊 ECLAT Algorithm
What is ECLAT?
ECLAT (Equivalence Class Clustering and bottom-up Lattice Traversal) uses set intersection on TID-sets to find frequent itemsets.

Key Insight
text

╔═══════════════════════════════════════════════════════════════╗
║                  THE ECLAT INSIGHT                            ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  TID-set of itemset X ∪ Y = TID-set(X) ∩ TID-set(Y)          ║
║                                                               ║
║  Example:                                                     ║
║  TID-set(A) = {T1, T2}                                        ║
║  TID-set(B) = {T1, T3}                                        ║
║  TID-set(A,B) = {T1, T2} ∩ {T1, T3} = {T1}                   ║
║                                                               ║
║  Support(A,B) = |TID-set(A,B)| = |{T1}| = 1                   ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
Algorithm
text

ECLAT ALGORITHM:
════════════════

INPUT: 
- D: Database
- min_sup: Minimum support threshold

OUTPUT:
- F: All frequent itemsets

ALGORITHM:
──────────

1. Transform database to vertical format
   For each item i, compute TID-set(i)

2. Remove infrequent items
   Keep only items where |TID-set(i)| ≥ min_sup

3. ECLAT(prefix P, items with prefix P):
   
   FOR each item i in items:
       F = F ∪ {P ∪ i}  // Add to frequent itemsets
       
       new_items = {}
       FOR each item j after i:
           new_TID = TID-set(i) ∩ TID-set(j)
           IF |new_TID| ≥ min_sup:
               Add (i∪j, new_TID) to new_items
       
       ECLAT(P ∪ i, new_items)  // Recurse

4. Return F
🔢 Complete Worked Example
text

TRANSACTION DATABASE:
┌─────┬───────────────────┐
│ TID │ Items             │
├─────┼───────────────────┤
│ T1  │ {A, C, D}         │
│ T2  │ {B, C, E}         │
│ T3  │ {A, B, C, E}      │
│ T4  │ {B, E}            │
│ T5  │ {A, B, C, E}      │
└─────┴───────────────────┘

Minimum Support Count = 2

════════════════════════════════════════════════════════════════
STEP 1: Convert to Vertical Format
════════════════════════════════════════════════════════════════

┌──────┬─────────────────┬─────────────────┐
│ Item │ TID-set         │ Support Count   │
├──────┼─────────────────┼─────────────────┤
│  A   │ {T1, T3, T5}    │ 3               │
│  B   │ {T2, T3, T4, T5}│ 4               │
│  C   │ {T1, T2, T3, T5}│ 4               │
│  D   │ {T1}            │ 1 ✗ (< min_sup) │
│  E   │ {T2, T3, T4, T5}│ 4               │
└──────┴─────────────────┴─────────────────┘

After removing infrequent items:
Frequent 1-itemsets: {A}, {B}, {C}, {E}

════════════════════════════════════════════════════════════════
STEP 2: Find 2-itemsets using Set Intersection
════════════════════════════════════════════════════════════════

Compute TID-sets for all pairs:

{A,B}: TID(A) ∩ TID(B) = {T1,T3,T5} ∩ {T2,T3,T4,T5} = {T3,T5}
       |{T3,T5}| = 2 ✓ Frequent

{A,C}: TID(A) ∩ TID(C) = {T1,T3,T5} ∩ {T1,T2,T3,T5} = {T1,T3,T5}
       |{T1,T3,T5}| = 3 ✓ Frequent

{A,E}: TID(A) ∩ TID(E) = {T1,T3,T5} ∩ {T2,T3,T4,T5} = {T3,T5}
       |{T3,T5}| = 2 ✓ Frequent

{B,C}: TID(B) ∩ TID(C) = {T2,T3,T4,T5} ∩ {T1,T2,T3,T5} = {T2,T3,T5}
       |{T2,T3,T5}| = 3 ✓ Frequent

{B,E}: TID(B) ∩ TID(E) = {T2,T3,T4,T5} ∩ {T2,T3,T4,T5} = {T2,T3,T4,T5}
       |{T2,T3,T4,T5}| = 4 ✓ Frequent

{C,E}: TID(C) ∩ TID(E) = {T1,T2,T3,T5} ∩ {T2,T3,T4,T5} = {T2,T3,T5}
       |{T2,T3,T5}| = 3 ✓ Frequent

Frequent 2-itemsets: {A,B}, {A,C}, {A,E}, {B,C}, {B,E}, {C,E}

════════════════════════════════════════════════════════════════
STEP 3: Find 3-itemsets
════════════════════════════════════════════════════════════════

Using equivalence classes [A], [B], [C] (prefix-based grouping):

Class [A]: Generate from {A,B}, {A,C}, {A,E}
─────────────────────────────────────────────

{A,B,C}: TID(A,B) ∩ TID(A,C) = {T3,T5} ∩ {T1,T3,T5} = {T3,T5}
         Or: TID(A,B) ∩ TID(C) = {T3,T5} ∩ {T1,T2,T3,T5} = {T3,T5}
         |{T3,T5}| = 2 ✓ Frequent

{A,B,E}: TID(A,B) ∩ TID(E) = {T3,T5} ∩ {T2,T3,T4,T5} = {T3,T5}
         |{T3,T5}| = 2 ✓ Frequent

{A,C,E}: TID(A,C) ∩ TID(E) = {T1,T3,T5} ∩ {T2,T3,T4,T5} = {T3,T5}
         |{T3,T5}| = 2 ✓ Frequent

Class [B]: Generate from {B,C}, {B,E}
─────────────────────────────────────

{B,C,E}: TID(B,C) ∩ TID(E) = {T2,T3,T5} ∩ {T2,T3,T4,T5} = {T2,T3,T5}
         |{T2,T3,T5}| = 3 ✓ Frequent

Frequent 3-itemsets: {A,B,C}, {A,B,E}, {A,C,E}, {B,C,E}

════════════════════════════════════════════════════════════════
STEP 4: Find 4-itemsets
════════════════════════════════════════════════════════════════

{A,B,C,E}: TID(A,B,C) ∩ TID(E) = {T3,T5} ∩ {T2,T3,T4,T5} = {T3,T5}
           |{T3,T5}| = 2 ✓ Frequent

Frequent 4-itemsets: {A,B,C,E}

════════════════════════════════════════════════════════════════
STEP 5: Find 5-itemsets
════════════════════════════════════════════════════════════════

No 5-itemsets possible (only 4 frequent items remain)

════════════════════════════════════════════════════════════════
FINAL RESULTS
════════════════════════════════════════════════════════════════

┌─────────────┬─────────────────────────────────────────────────┐
│   Size      │   Frequent Itemsets                             │
├─────────────┼─────────────────────────────────────────────────┤
│ 1-itemsets  │ {A}:3, {B}:4, {C}:4, {E}:4                     │
│ 2-itemsets  │ {A,B}:2, {A,C}:3, {A,E}:2, {B,C}:3,           │
│             │ {B,E}:4, {C,E}:3                               │
│ 3-itemsets  │ {A,B,C}:2, {A,B,E}:2, {A,C,E}:2, {B,C,E}:3    │
│ 4-itemsets  │ {A,B,C,E}:2                                    │
└─────────────┴─────────────────────────────────────────────────┘
🔍 Equivalence Classes Visualization
text

                           ∅
            ┌──────────────┼──────────────┐
            │              │              │
          [A]            [B]            [C]
         /│ \           / \             |
      [AB][AC][AE]   [BC][BE]         [CE]
       / \    |        |
   [ABC][ABE][ACE]   [BCE]
       \     |      /
        \    |    /
         [ABCE]

Each branch represents an equivalence class
Intersections happen within and across classes
⏱️ ECLAT COMPLEXITY ANALYSIS

┌─────────────────────────────────────────────────────────────┐
│               ECLAT COMPLEXITY ANALYSIS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  TIME COMPLEXITY:                                           │
│  - Set intersection: O(min(|A|, |B|))                      │
│  - Total: O(n × m²) where n = #transactions,               │
│           m = #frequent items                               │
│                                                             │
│  SPACE COMPLEXITY:                                          │
│  - O(n × m) for storing TID-sets                           │
│  - Can be memory-intensive for large databases             │
│                                                             │
│  ADVANTAGES:                                                │
│  • No candidate generation needed                          │
│  • No database scan for support counting                   │
│  • Simple set intersection operation                       │
│  • Efficient for medium-sized datasets                     │
│                                                             │
│  DISADVANTAGES:                                             │
│  • High memory usage for TID-sets                          │
│  • Not suitable for very large databases                   │
│  • Worst for dense databases                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🆚 Algorithm Comparison Summary
text

┌──────────────────────────────────────────────────────────────────┐
│           APRIORI vs FP-GROWTH vs ECLAT                          │
├────────────┬────────────┬─────────────┬────────────────────────┤
│  Feature   │  Apriori   │ FP-Growth   │      ECLAT             │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Data       │ Horizontal │ Horizontal  │ Vertical (TID-sets)    │
│ Format     │            │             │                        │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ DB Scans   │ Multiple   │ 2           │ 1 (+ transformation)   │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Candidate  │ Yes        │ No          │ No                     │
│ Generation │            │             │                        │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Memory     │ Moderate   │ Moderate    │ High (TID-sets)        │
│ Usage      │            │             │                        │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Speed      │ Slowest    │ Fastest     │ Fast                   │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Best For   │ Sparse     │ Dense       │ Medium, sparse         │
│            │ data       │ data        │ datasets               │
├────────────┼────────────┼─────────────┼────────────────────────┤
│ Core       │ Pruning    │ Tree        │ Set intersection       │
│ Operation  │            │ structure   │                        │
└────────────┴────────────┴─────────────┴────────────────────────┘
📝 Chapter 6 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 6: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ ECLAT uses vertical database format (TID-sets)         ║
║  ✓ Support counting via set intersection                  ║
║  ✓ No candidate generation needed                         ║
║  ✓ Depth-first search with equivalence classes            ║
║  ✓ Trade-off: Speed vs Memory usage                       ║
║  ✓ Best for medium-sized, sparse datasets                 ║
╚═══════════════════════════════════════════════════════════╝
Chapter 7: Advanced Metrics & Interestingness Measures {#chapter-7}
🎯 Why Do We Need More Metrics?
text

THE PROBLEM WITH SUPPORT & CONFIDENCE:
═══════════════════════════════════════

Example Database (1000 transactions):
- {Coffee}: 800 transactions (80%)
- {Tea}: 200 transactions (20%)
- {Coffee, Tea}: 160 transactions (16%)

Rule: {Coffee} → {Tea}
- Support = 16% ✓ Seems okay
- Confidence = 160/800 = 20% ✓ Seems okay

BUT WAIT! Tea appears in 20% of ALL transactions anyway!
Buying coffee doesn't actually increase tea purchases!

This is where LIFT and other metrics come in...
📊 Complete Metrics Collection
1. Lift (Interest Factor)
Already covered in Chapter 3, but let's see it in action:

text

FORMULA:
                    Support(X ∪ Y)
Lift(X → Y) = ─────────────────────────────
               Support(X) × Support(Y)

EXAMPLE:
Support({Coffee, Tea}) = 0.16
Support({Coffee}) = 0.80
Support({Tea}) = 0.20

Lift = 0.16 / (0.80 × 0.20) = 0.16 / 0.16 = 1.0

✓ Lift = 1.0 means INDEPENDENT
  Coffee and Tea purchases are unrelated!

INTERPRETATION:
┌─────────────────────────────────────────────┐
│  Lift = 1     │ Independent (no relation)   │
│  Lift > 1     │ Positive correlation        │
│  Lift < 1     │ Negative correlation        │
│  Lift = 2     │ 2× more likely together     │
│  Lift = 0.5   │ 50% less likely together    │
└─────────────────────────────────────────────┘
2. Conviction
text

FORMULA:
                        1 - Support(Y)
Conviction(X → Y) = ──────────────────────
                     1 - Confidence(X → Y)

PURPOSE: Measures how much X → Y is affected by chance

EXAMPLE:
Support({Tea}) = 0.20
Confidence({Coffee} → {Tea}) = 0.20

Conviction = (1 - 0.20) / (1 - 0.20)
           = 0.80 / 0.80
           = 1.0

INTERPRETATION:
┌──────────────────────────────────────────────────────┐
│  Conviction = 1   │ Rule not better than random      │
│  Conviction > 1   │ Rule better than random          │
│  Conviction = ∞   │ Perfect implication (Conf = 1)   │
│  Conviction → ∞   │ Very strong rule                 │
└──────────────────────────────────────────────────────┘

SPECIAL CASE:
If Confidence = 1, then Conviction = ∞
(The rule is always true)
3. Leverage
text

FORMULA:
Leverage(X → Y) = Support(X ∪ Y) - Support(X) × Support(Y)

PURPOSE: Difference between observed and expected frequency

EXAMPLE:
Support({Coffee, Tea}) = 0.16
Support({Coffee}) = 0.80
Support({Tea}) = 0.20

Leverage = 0.16 - (0.80 × 0.20)
         = 0.16 - 0.16
         = 0

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Leverage = 0  │ Items are independent     │
│  Leverage > 0  │ Positive association      │
│  Leverage < 0  │ Negative association      │
└────────────────────────────────────────────┘

Range: [-1, 1]
Higher absolute value = stronger relationship
4. Jaccard Coefficient
text

FORMULA:
                    Support(X ∪ Y)
Jaccard(X, Y) = ─────────────────────────────────────
                 Support(X) + Support(Y) - Support(X ∪ Y)

Also:
                  |X ∩ Y|
Jaccard(X, Y) = ───────────
                 |X ∪ Y|

PURPOSE: Measures overlap between itemsets

EXAMPLE:
Support({Coffee, Tea}) = 0.16
Support({Coffee}) = 0.80
Support({Tea}) = 0.20

Jaccard = 0.16 / (0.80 + 0.20 - 0.16)
        = 0.16 / 0.84
        = 0.19

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Range: [0, 1]                             │
│  0     │ No overlap                        │
│  1     │ Perfect overlap (identical sets)  │
│  0.5   │ Moderate similarity               │
└────────────────────────────────────────────┘
5. Cosine Similarity
text

FORMULA:
                      Support(X ∪ Y)
Cosine(X, Y) = ─────────────────────────────────
                √(Support(X) × Support(Y))

PURPOSE: Normalized correlation measure

EXAMPLE:
Support({Coffee, Tea}) = 0.16
Support({Coffee}) = 0.80
Support({Tea}) = 0.20

Cosine = 0.16 / √(0.80 × 0.20)
       = 0.16 / √0.16
       = 0.16 / 0.4
       = 0.4

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Range: [0, 1]                             │
│  0     │ Orthogonal (no relation)          │
│  1     │ Perfect correlation               │
│  > 0.5 │ Strong similarity                 │
└────────────────────────────────────────────┘
6. Kulczynski Measure
text

FORMULA:
                    1   ⎡ Support(X ∪ Y)   Support(X ∪ Y) ⎤
Kulc(X → Y) = ─── × ⎢ ─────────────── + ─────────────── ⎥
                    2   ⎣   Support(X)       Support(Y)    ⎦

             = (Confidence(X→Y) + Confidence(Y→X)) / 2

PURPOSE: Symmetric measure, average of both directions

EXAMPLE:
Support({Coffee, Tea}) = 0.16
Support({Coffee}) = 0.80
Support({Tea}) = 0.20

Conf(Coffee → Tea) = 0.16/0.80 = 0.20
Conf(Tea → Coffee) = 0.16/0.20 = 0.80

Kulc = (0.20 + 0.80) / 2 = 0.50

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Range: [0, 1]                             │
│  0     │ No association                    │
│  1     │ Perfect association               │
│  > 0.5 │ Strong bidirectional relation     │
└────────────────────────────────────────────┘
7. Imbalance Ratio (IR)
text

FORMULA:
                |Support(X) - Support(Y)|
IR(X, Y) = ───────────────────────────────────
            Support(X) + Support(Y) - Support(X ∪ Y)

PURPOSE: Measures imbalance in item frequencies

EXAMPLE:
Support({Coffee}) = 0.80
Support({Tea}) = 0.20
Support({Coffee, Tea}) = 0.16

IR = |0.80 - 0.20| / (0.80 + 0.20 - 0.16)
   = 0.60 / 0.84
   = 0.714

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Range: [0, 1]                             │
│  0     │ Balanced (similar frequencies)    │
│  1     │ Highly imbalanced                 │
│  > 0.5 │ Significant imbalance             │
└────────────────────────────────────────────┘
8. Correlation Coefficient (φ-coefficient)
text

For binary data only:

CONTINGENCY TABLE:
┌────────┬─────────┬─────────┬───────┐
│        │   Y     │  ¬Y     │ Total │
├────────┼─────────┼─────────┼───────┤
│   X    │   n₁₁   │  n₁₀    │  n₁•  │
│   ¬X   │   n₀₁   │  n₀₀    │  n₀•  │
│  Total │   n•₁   │  n•₀    │   N   │
└────────┴─────────┴─────────┴───────┘

FORMULA:
            n₁₁ × n₀₀ - n₁₀ × n₀₁
φ = ─────────────────────────────────────
     √(n₁• × n₀• × n•₁ × n•₀)

EXAMPLE:
N = 1000 transactions
{Coffee, Tea}: 160
{Coffee, ¬Tea}: 640
{¬Coffee, Tea}: 40
{¬Coffee, ¬Tea}: 160

φ = (160×160 - 640×40) / √(800×200×200×800)
  = (25600 - 25600) / √(25,600,000,000)
  = 0 / 160,000
  = 0

INTERPRETATION:
┌────────────────────────────────────────────┐
│  Range: [-1, 1]                            │
│  -1    │ Perfect negative correlation      │
│   0    │ No correlation                    │
│  +1    │ Perfect positive correlation      │
└────────────────────────────────────────────┘
🔢 Complete Example with All Metrics
text

DATABASE: 10,000 transactions
═══════════════════════════════

Individual Items:
- {Bread}: 4,000 transactions (40%)
- {Butter}: 2,500 transactions (25%)

Together:
- {Bread, Butter}: 1,500 transactions (15%)

CALCULATE ALL METRICS:
══════════════════════

1. SUPPORT
   Support({Bread, Butter}) = 1500/10000 = 0.15 = 15%

2. CONFIDENCE
   Conf({Bread} → {Butter}) = 1500/4000 = 0.375 = 37.5%
   Conf({Butter} → {Bread}) = 1500/2500 = 0.60 = 60%

3. LIFT
   Lift = 0.15 / (0.40 × 0.25)
        = 0.15 / 0.10
        = 1.5 ✓ POSITIVE CORRELATION

4. CONVICTION
   Conviction({Bread} → {Butter}) = (1 - 0.25) / (1 - 0.375)
                                   = 0.75 / 0.625
                                   = 1.2

5. LEVERAGE
   Leverage = 0.15 - (0.40 × 0.25)
            = 0.15 - 0.10
            = 0.05 ✓ POSITIVE

6. JACCARD
   Jaccard = 0.15 / (0.40 + 0.25 - 0.15)
           = 0.15 / 0.50
           = 0.30

7. COSINE
   Cosine = 0.15 / √(0.40 × 0.25)
          = 0.15 / √0.10
          = 0.15 / 0.316
          = 0.474

8. KULCZYNSKI
   Kulc = (0.375 + 0.60) / 2
        = 0.4875

9. IMBALANCE RATIO
   IR = |0.40 - 0.25| / (0.40 + 0.25 - 0.15)
      = 0.15 / 0.50
      = 0.30

CONCLUSION:
───────────
✓ Lift = 1.5: People buying Bread are 50% more likely to buy Butter
✓ Leverage = 0.05: 5% more co-occurrence than random
✓ Conviction = 1.2: Rule is 20% better than random
✓ This is a MEANINGFUL association worth acting on!
📊 Metrics Decision Tree
text

                    START: Evaluate Rule X → Y
                              │
                    ┌─────────┴─────────┐
                    │                   │
              Check SUPPORT         Check CONFIDENCE
                    │                   │
              Is it ≥ min_sup?    Is it ≥ min_conf?
                    │                   │
                   YES                 YES
                    │                   │
                    └─────────┬─────────┘
                              │
                        Check LIFT
                              │
              ┌───────────────┼───────────────┐
              │               │               │
          Lift > 1        Lift = 1        Lift < 1
              │               │               │
         POSITIVE         INDEPENDENT     NEGATIVE
       CORRELATION       (Misleading!)   CORRELATION
              │               │               │
       Check CONVICTION    REJECT        Usually REJECT
              │
       ┌──────┴──────┐
       │             │
   Conv > 1.5    Conv ≤ 1.5
       │             │
   STRONG RULE   WEAK RULE
       │
   ACCEPT ✓
🎯 When to Use Which Metric?
text

┌──────────────────────────────────────────────────────────────┐
│                  METRIC SELECTION GUIDE                      │
├────────────────┬─────────────────────────────────────────────┤
│   METRIC       │          USE WHEN...                        │
├────────────────┼─────────────────────────────────────────────┤
│ Support        │ You need minimum frequency threshold        │
├────────────────┼─────────────────────────────────────────────┤
│ Confidence     │ You need rule reliability                   │
├────────────────┼─────────────────────────────────────────────┤
│ Lift           │ PRIMARY metric - always check this!         │
│                │ Eliminates misleading high-confidence rules │
├────────────────┼─────────────────────────────────────────────┤
│ Conviction     │ You want asymmetric dependence measure      │
│                │ Complements lift                            │
├────────────────┼─────────────────────────────────────────────┤
│ Leverage       │ You need absolute difference measure        │
├────────────────┼─────────────────────────────────────────────┤
│ Jaccard        │ Comparing item set similarities             │
├────────────────┼─────────────────────────────────────────────┤
│ Cosine         │ Normalized similarity needed                │
├────────────────┼─────────────────────────────────────────────┤
│ Kulczynski     │ You want symmetric measure                  │
│                │ Both X→Y and Y→X matter equally             │
├────────────────┼─────────────────────────────────────────────┤
│ Imbalance      │ Detecting skewed frequency distributions    │
│ Ratio          │                                             │
├────────────────┼─────────────────────────────────────────────┤
│ Correlation    │ Statistical correlation analysis needed     │
│ (φ-coefficient)│                                             │
└────────────────┴─────────────────────────────────────────────┘
⚠️ Common Pitfalls
text

PITFALL #1: High Confidence, Low Lift
══════════════════════════════════════
Rule: {Any Item} → {Milk}
Confidence: 80%
But Milk appears in 80% of ALL transactions anyway!
Lift = 1.0 → Rule is MEANINGLESS

LESSON: Always check LIFT!

PITFALL #2: Ignoring Support
══════════════════════════════════════
Rule: {Caviar} → {Champagne}
Confidence: 95%
Lift: 3.5
But Support: 0.01% (10 transactions out of 1 million)

LESSON: Too rare to be actionable!

PITFALL #3: Asymmetric Misunderstanding
══════════════════════════════════════
Conf({Bread} → {Butter}) = 40%
Conf({Butter} → {Bread}) = 70%

These are DIFFERENT rules!
Use Kulczynski for symmetric measure.

PITFALL #4: Correlation ≠ Causation
══════════════════════════════════════
{Umbrella Sales} ↔ {Ice Cream Sales}
Negative correlation, but no causal relationship
Both caused by third factor: Weather

LESSON: Domain knowledge required!
📝 Chapter 7 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 7: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Lift is the MOST IMPORTANT metric (filters noise)      ║
║  ✓ Use multiple metrics for robust evaluation             ║
║  ✓ Support + Confidence alone are often misleading        ║
║  ✓ Conviction measures directional dependence             ║
║  ✓ Kulczynski provides symmetric measure                  ║
║  ✓ Always consider domain knowledge                       ║
║  ✓ Recommended: Support + Confidence + Lift + Conviction  ║
╚═══════════════════════════════════════════════════════════╝
Chapter 8: Multi-Level Association Rules {#chapter-8}
🎯 The Concept
text

SINGLE-LEVEL vs MULTI-LEVEL
════════════════════════════

SINGLE-LEVEL (What we've seen so far):
{Milk, Bread} → {Butter}

MULTI-LEVEL (Hierarchical):
{Dairy, Bakery} → {Dairy}
{2% Milk, Whole Wheat Bread} → {Organic Butter}

            Food
       ┌──────┼──────┐
    Dairy  Bakery  Beverages
      │       │        │
   ┌──┼──┐    │     ┌──┼──┐
  Milk Cheese Bread Tea Coffee
   │              │
┌──┼──┐        ┌──┼──┐
2% Whole    White Wheat
📊 Concept Hierarchy Example
text

PRODUCT TAXONOMY:
═════════════════

Level 1 (Category):        Electronics
                              │
Level 2 (Subcategory):   ┌────┼────┐
                      Computer  TV  Phone
                         │
Level 3 (Product):   ┌───┼───┐
                   Laptop Desktop Tablet
                     │
Level 4 (Brand):  ┌──┼──┐
                Dell HP Lenovo
                  │
Level 5 (Model): T14 T15 X1
🔢 Multi-Level Mining Strategies
Strategy 1: Uniform Support
text

UNIFORM SUPPORT APPROACH:
═════════════════════════

Same min_support for ALL levels

Example: min_sup = 5%

Level 1: {Electronics} → Support must be ≥ 5%
Level 2: {Computer} → Support must be ≥ 5%
Level 3: {Laptop} → Support must be ≥ 5%

PROBLEM:
───────
                Electronics: 20% ✓
                    │
               Computer: 12% ✓
                    │
                Laptop: 8% ✓
                    │
            ┌───────┼───────┐
         Dell: 3% ✗  HP: 2% ✗  Lenovo: 3% ✗

Specific brands get filtered out!
(Cross-level rules lost)
Strategy 2: Reduced Support
text

REDUCED/LEVEL-BY-LEVEL SUPPORT:
═══════════════════════════════

Different min_support for each level

Level 1: min_sup = 10%
Level 2: min_sup = 5%
Level 3: min_sup = 3%
Level 4: min_sup = 1%

EXAMPLE:
────────
Level 1: {Electronics}: 20% ≥ 10% ✓
Level 2: {Computer}: 8% ≥ 5% ✓
Level 3: {Laptop}: 4% ≥ 3% ✓
Level 4: {Dell}: 1.5% ≥ 1% ✓

✓ All levels can produce interesting rules!
Strategy 3: Group-Based Support
text

GROUP-BASED APPROACH:
═══════════════════════

Different support for different branches

Electronics: min_sup = 5%
  ├─ Computer: min_sup = 2%
  ├─ TV: min_sup = 3%
  └─ Phone: min_sup = 4%

Clothing: min_sup = 8%
  ├─ Men: min_sup = 4%
  └─ Women: min_sup = 5%

Based on domain knowledge & business needs
🔍 Types of Multi-Level Rules
text

TYPE 1: INTER-LEVEL RULES
══════════════════════════
Rules across different levels

Example 1:
{Dairy} → {Bakery}  (both Level 1)
Support: 15%, Confidence: 70%

Example 2:
{Milk} → {Bread}  (both Level 2)
Support: 12%, Confidence: 65%

Example 3:
{2% Milk} → {Whole Wheat Bread}  (both Level 3)
Support: 5%, Confidence: 60%

TYPE 2: CROSS-LEVEL RULES
══════════════════════════
Rules mixing different levels

Example 1:
{Dairy} → {Whole Wheat Bread}
(Level 1 → Level 3)

Example 2:
{2% Milk, Bread} → {Dairy}
(Level 3, Level 2 → Level 1)

Example 3:
{Laptop} → {Electronics, Software}
(Level 3 → Level 1, Level 2)
🔢 Complete Worked Example
text

TRANSACTION DATABASE:
═══════════════════════

Hierarchy:
         Food
      ┌────┼────┐
   Dairy Bakery Snacks
     │      │      │
   ┌─┼─┐    │    ┌─┼─┐
  Milk Yogurt Bread Chips Candy

Transactions:
┌─────┬───────────────────────────────────────────┐
│ TID │ Items (Lowest Level)                      │
├─────┼───────────────────────────────────────────┤
│ T1  │ {2% Milk, Whole Wheat Bread, Chips}       │
│ T2  │ {Whole Milk, White Bread}                 │
│ T3  │ {Greek Yogurt, Whole Wheat Bread, Candy}  │
│ T4  │ {2% Milk, White Bread, Chips}             │
│ T5  │ {Whole Milk, Whole Wheat Bread}           │
│ T6  │ {2% Milk, Whole Wheat Bread}              │
│ T7  │ {Greek Yogurt, White Bread, Candy}        │
│ T8  │ {2% Milk, Whole Wheat Bread, Candy}       │
│ T9  │ {Whole Milk, Chips}                       │
│ T10 │ {2% Milk, White Bread, Chips}             │
└─────┴───────────────────────────────────────────┘

N = 10 transactions

STEP 1: Encode with hierarchy
══════════════════════════════

Expanded representation:

T1: {Food, Dairy, Milk, 2% Milk, Food, Bakery, Bread, 
     Whole Wheat Bread, Food, Snacks, Chips}

Simplified (remove duplicates):
T1: {Food, Dairy, Milk, 2% Milk, Bakery, Bread, 
     Whole Wheat Bread, Snacks, Chips}

All transactions encoded...

STEP 2: Set support thresholds
═══════════════════════════════

Level 1 (Food): min_sup = 50% (5 transactions)
Level 2 (Dairy, Bakery, Snacks): min_sup = 40% (4 trans)
Level 3 (Milk, Bread, etc.): min_sup = 30% (3 trans)
Level 4 (2% Milk, etc.): min_sup = 20% (2 trans)

STEP 3: Mine Level 1
═════════════════════

┌──────────┬───────┬─────────┐
│ Itemset  │ Count │ Support │
├──────────┼───────┼─────────┤
│ {Food}   │ 10    │ 100%    │
└──────────┴───────┴─────────┘

All transactions contain Food (root)
✓ Frequent at Level 1

STEP 4: Mine Level 2
═════════════════════

┌──────────┬───────┬─────────┬────────────┐
│ Itemset  │ Count │ Support │ Status     │
├──────────┼───────┼─────────┼────────────┤
│ {Dairy}  │ 9     │ 90%     │ ✓ Frequent │
│ {Bakery} │ 8     │ 80%     │ ✓ Frequent │
│ {Snacks} │ 6     │ 60%     │ ✓ Frequent │
└──────────┴───────┴─────────┴────────────┘

2-itemsets:
┌────────────────┬───────┬─────────┬────────────┐
│ Itemset        │ Count │ Support │ Status     │
├────────────────┼───────┼─────────┼────────────┤
│ {Dairy,Bakery} │ 7     │ 70%     │ ✓ Frequent │
│ {Dairy,Snacks} │ 5     │ 50%     │ ✓ Frequent │
│ {Bakery,Snacks}│ 5     │ 50%     │ ✓ Frequent │
└────────────────┴───────┴─────────┴────────────┘

STEP 5: Mine Level 3
═════════════════════

┌──────────┬───────┬─────────┬────────────┐
│ Itemset  │ Count │ Support │ Status     │
├──────────┼───────┼─────────┼────────────┤
│ {Milk}   │ 6     │ 60%     │ ✓ Frequent │
│ {Yogurt} │ 2     │ 20%     │ ✗ Infr.    │
│ {Bread}  │ 8     │ 80%     │ ✓ Frequent │
│ {Chips}  │ 5     │ 50%     │ ✓ Frequent │
│ {Candy}  │ 3     │ 30%     │ ✓ Frequent │
└──────────┴───────┴─────────┴────────────┘

Cross-level 2-itemsets:
┌───────────────┬───────┬─────────┬────────────┐
│ Itemset       │ Count │ Support │ Status     │
├───────────────┼───────┼─────────┼────────────┤
│ {Milk,Bread}  │ 6     │ 60%     │ ✓ Frequent │
│ {Milk,Chips}  │ 4     │ 40%     │ ✓ Frequent │
│ {Bread,Chips} │ 3     │ 30%     │ ✓ Frequent │
│ {Bread,Candy} │ 2     │ 20%     │ ✗ Infr.    │
└───────────────┴───────┴─────────┴────────────┘

STEP 6: Generate Rules
═══════════════════════

LEVEL 2 RULES:
──────────────
{Dairy} → {Bakery}
Support: 70%, Confidence: 7/9 = 77.8%

{Bakery} → {Dairy}
Support: 70%, Confidence: 7/8 = 87.5%

LEVEL 3 RULES:
──────────────
{Milk} → {Bread}
Support: 60%, Confidence: 6/6 = 100%

{Bread} → {Milk}
Support: 60%, Confidence: 6/8 = 75%

CROSS-LEVEL RULES:
──────────────────
{Milk} → {Bakery}  (Level 3 → Level 2)
Support: 60%, Confidence: 6/6 = 100%

{Dairy, Bread} → {Snacks}  (Mixed levels)
Support: 50%, Confidence: 5/7 = 71.4%
🎨 Redundancy Filtering
text

PROBLEM: Redundant Rules
═════════════════════════

Consider:
Rule 1: {Dairy} → {Bakery}  
        Support: 70%, Confidence: 77.8%

Rule 2: {Milk} → {Bread}
        Support: 60%, Confidence: 100%

Rule 2 is MORE SPECIFIC but provides similar information.

REDUNDANCY CHECK:
═════════════════

Rule R1 is redundant if there exists R2 where:
1. R2 is more specific (ancestor relationship)
2. support(R2) ≈ support(R1)  (within threshold)
3. confidence(R2) ≥ confidence(R1)

EXAMPLE:
────────
{Milk} → {Bread}: 60%, 100%
  vs
{2% Milk} → {Whole Wheat Bread}: 40%, 100%

If we set threshold = 10% support difference:
60% - 40% = 20% > 10%

✓ NOT redundant (support drop too large)
  Both rules are kept

FILTERING STRATEGY:
═══════════════════
1. Keep most specific rules with high confidence
2. Remove ancestor rules if descendant has:
   - Similar support (within 5-10%)
   - Equal or higher confidence
⚙️ Multi-Level Apriori Algorithm
text

MULTI-LEVEL APRIORI:
════════════════════

INPUT:
- Transaction database D
- Concept hierarchy H
- min_support per level: {ms₁, ms₂, ..., msₖ}

ALGORITHM:
──────────

1. Transform D using hierarchy H
   For each transaction T:
       Expand items to include all ancestor concepts

2. L₁ = Find frequent 1-itemsets at Level 1 (ms₁)

3. FOR each level i = 2 to max_level:
   
   a. Generate candidates Cᵢ from Lᵢ₋₁
   
   b. Scan database:
      Count support for candidates
   
   c. Lᵢ = candidates in Cᵢ with support ≥ msᵢ
   
   d. OPTIONAL: Apply cross-level pruning
      If ancestor is infrequent, prune descendants
   
4. Generate rules from all L₁, L₂, ..., Lₖ

5. Filter redundant rules

6. Return non-redundant frequent itemsets and rules
📝 Chapter 8 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 8: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Multi-level mining uses concept hierarchies            ║
║  ✓ Three strategies: Uniform, Reduced, Group-based        ║
║  ✓ Reduced support (lower at deeper levels) works best    ║
║  ✓ Cross-level rules provide valuable insights            ║
║  ✓ Redundancy filtering prevents information overload     ║
║  ✓ More actionable rules at appropriate granularity       ║
╚═══════════════════════════════════════════════════════════╝

Chapter 9: Sequential Pattern Mining {#chapter-9}
🎯 What is Sequential Pattern Mining?
text

THE KEY DIFFERENCE:
═══════════════════

ASSOCIATION RULES (Previous chapters):
- Items in a SINGLE transaction
- NO order/time consideration
- "Bought together"

SEQUENTIAL PATTERNS:
- Items across MULTIPLE transactions over TIME
- ORDER matters
- "Bought in sequence"

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Association Rule:    {Bread, Butter} → {Milk}             │
│                       "In same shopping trip"               │
│                                                             │
│  Sequential Pattern:  <{Phone} → {Case} → {Screen Guard}>  │
│                       "Over time, in this order"            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📚 Key Terminology
text

1. SEQUENCE
═══════════
An ordered list of itemsets (events)

Notation: <e₁, e₂, e₃, ..., eₙ>
Where each eᵢ is an itemset

Example:
<{iPhone}, {Case, Charger}, {AirPods}>
   ↓           ↓              ↓
 Event 1    Event 2        Event 3
 (Day 1)    (Day 5)        (Day 15)


2. SEQUENCE DATABASE
════════════════════
Collection of sequences, one per customer/entity

┌──────────┬────────────────────────────────────────────┐
│ Seq. ID  │ Sequence                                   │
├──────────┼────────────────────────────────────────────┤
│ S1       │ <{a}, {a,b,c}, {a,c}, {d}, {c,f}>         │
│ S2       │ <{a,d}, {c}, {b,c}, {a,e}>                │
│ S3       │ <{e,f}, {a,b}, {d,f}, {c}, {b}>           │
│ S4       │ <{e}, {g}, {a,b,f}, {c}, {b,c}>           │
└──────────┴────────────────────────────────────────────┘


3. SUBSEQUENCE
══════════════
A sequence α is a SUBSEQUENCE of β if every element 
of α appears in β in the same order

α = <{a}, {b,c}, {d}>
β = <{a,e}, {b,c,f}, {a,d}, {c}>

Is α ⊆ β?
- {a} ⊆ {a,e}? ✓
- {b,c} ⊆ {b,c,f}? ✓
- {d} ⊆ {a,d}? ✓

Yes! α is a subsequence of β ✓


4. SUPPORT OF A SEQUENCE
════════════════════════
Number (or fraction) of sequences containing 
the pattern as a subsequence

Support(<{a}, {b}>) = Number of sequences 
                       where {a} comes before {b}


5. SEQUENTIAL PATTERN
═════════════════════
A subsequence with support ≥ minimum support threshold
🔍 Subsequence Examples
text

EXAMPLE DATABASE:
═════════════════

┌─────┬──────────────────────────────────┐
│ SID │ Sequence                         │
├─────┼──────────────────────────────────┤
│ S1  │ <{1,2}, {3}, {1,2,3}, {1,4}>    │
│ S2  │ <{1}, {2}, {1,2,3}>             │
│ S3  │ <{1}, {2}, {3,4}>               │
│ S4  │ <{2}, {3}, {4}>                 │
└─────┴──────────────────────────────────┘

Minimum Support = 2 (50%)

QUESTION: Is <{1}, {2,3}> a frequent sequential pattern?

Check each sequence:

S1: <{1,2}, {3}, {1,2,3}, {1,4}>
    - Need {1} first: {1,2} contains {1} ✓
    - Need {2,3} after: {1,2,3} contains {2,3} ✓
    ✓ S1 contains the pattern

S2: <{1}, {2}, {1,2,3}>
    - Need {1} first: {1} contains {1} ✓
    - Need {2,3} after: {1,2,3} contains {2,3} ✓
    ✓ S2 contains the pattern

S3: <{1}, {2}, {3,4}>
    - Need {1} first: {1} contains {1} ✓
    - Need {2,3} after: {2} has 2, {3,4} has 3, but NOT together
    ✗ S3 does NOT contain the pattern

S4: <{2}, {3}, {4}>
    - Need {1} first: No element contains {1}
    ✗ S4 does NOT contain the pattern

Support(<{1}, {2,3}>) = 2 (S1, S2)
2 ≥ min_sup(2) ✓ FREQUENT PATTERN!
🔄 GSP Algorithm (Generalized Sequential Patterns)
text

GSP ALGORITHM:
══════════════

Similar to Apriori but for sequences!

APRIORI PRINCIPLE FOR SEQUENCES:
────────────────────────────────
"If a sequence is infrequent, all its super-sequences 
 are also infrequent"

Super-sequence: Adding items OR adding events

<{a}, {b}> is subsequence of:
- <{a,c}, {b}>      (item added to element)
- <{a}, {d}, {b}>   (element added)
- <{a}, {b,c}>      (item added)


ALGORITHM STEPS:
────────────────

1. Find all frequent 1-sequences (single items)

2. k = 1

3. REPEAT until no more frequent sequences:
   
   a. CANDIDATE GENERATION:
      Generate (k+1)-sequences from k-sequences
      
   b. CANDIDATE PRUNING:
      Remove candidates with infrequent subsequences
      
   c. SUPPORT COUNTING:
      Scan database, count support of each candidate
      
   d. FILTERING:
      Keep candidates with support ≥ min_sup
   
   e. k = k + 1

4. Return all frequent sequences
🔢 Complete GSP Example
text

SEQUENCE DATABASE:
══════════════════

┌─────┬────────────────────────────────┐
│ SID │ Sequence                       │
├─────┼────────────────────────────────┤
│ S1  │ <{a}, {a,b,c}, {a,c}, {d}>    │
│ S2  │ <{a}, {c}, {b,c}>             │
│ S3  │ <{a,b}, {c}, {b,c}>           │
│ S4  │ <{a}, {b}, {b,c}>             │
└─────┴────────────────────────────────┘

Minimum Support = 2 (50%)

════════════════════════════════════════════════════════════════
ITERATION 1: Find Frequent 1-Sequences
════════════════════════════════════════════════════════════════

Count each item:

┌──────────┬───────┬────────────┐
│ Sequence │ Count │ Status     │
├──────────┼───────┼────────────┤
│ <{a}>    │ 4     │ ✓ Frequent │
│ <{b}>    │ 4     │ ✓ Frequent │
│ <{c}>    │ 4     │ ✓ Frequent │
│ <{d}>    │ 1     │ ✗ Infreq.  │
└──────────┴───────┴────────────┘

L₁ = {<{a}>, <{b}>, <{c}>}

════════════════════════════════════════════════════════════════
ITERATION 2: Find Frequent 2-Sequences
════════════════════════════════════════════════════════════════

CANDIDATE GENERATION:
─────────────────────

Two ways to extend a 1-sequence:
1. Add item to existing element: <{a}> → <{a,b}>
2. Add new element: <{a}> → <{a}, {b}>

From L₁, generate C₂:

Within-element (itemsets):
- <{a,b}>, <{a,c}>, <{b,c}>

Across-element (sequences):
- <{a}, {a}>, <{a}, {b}>, <{a}, {c}>
- <{b}, {a}>, <{b}, {b}>, <{b}, {c}>
- <{c}, {a}>, <{c}, {b}>, <{c}, {c}>

C₂ = {<{a,b}>, <{a,c}>, <{b,c}>, 
      <{a},{a}>, <{a},{b}>, <{a},{c}>,
      <{b},{a}>, <{b},{b}>, <{b},{c}>,
      <{c},{a}>, <{c},{b}>, <{c},{c}>}

SUPPORT COUNTING:
─────────────────

┌────────────┬───────┬────────────────────────────────────┐
│ Candidate  │ Count │ Explanation                        │
├────────────┼───────┼────────────────────────────────────┤
│ <{a,b}>    │ 2     │ S1:{a,b,c}, S3:{a,b}              │
│ <{a,c}>    │ 2     │ S1:{a,b,c},{a,c}, S3 doesn't have │
│ <{b,c}>    │ 4     │ All sequences have it             │
│ <{a},{a}>  │ 1     │ Only S1                           │
│ <{a},{b}>  │ 4     │ All sequences                     │
│ <{a},{c}>  │ 4     │ All sequences                     │
│ <{b},{a}>  │ 0     │ None (b before a)                 │
│ <{b},{b}>  │ 1     │ Only S4                           │
│ <{b},{c}>  │ 3     │ S1, S3, S4                        │
│ <{c},{a}>  │ 0     │ None (c before a)                 │
│ <{c},{b}>  │ 1     │ S2? No, S2 has a then c then bc   │
│ <{c},{c}>  │ 0     │ None                              │
└────────────┴───────┴────────────────────────────────────┘

Wait, let me recount <{b},{c}>:
S1: <{a}, {a,b,c}, {a,c}, {d}> - {b} in {a,b,c}, {c} in {a,c} ✓
S2: <{a}, {c}, {b,c}> - {b} in {b,c}... but {c} comes before! 
    Need b THEN c. {b,c} has both but as same event. Does {b,c} count?
    No! We need {b} in earlier element, then {c} in later element.
    Actually {c} appears alone, then {b,c}. So b is in {b,c}, 
    but c already appeared. b→c? c is at position 2, b at position 3.
    So b comes AFTER c. ✗
S3: <{a,b}, {c}, {b,c}> - {b} in {a,b}, {c} in {c} ✓
S4: <{a}, {b}, {b,c}> - {b} in {b}, {c} in {b,c} ✓

<{b},{c}> count = 3 (S1, S3, S4) ✓

L₂ = {<{a,b}>:2, <{a,c}>:2, <{b,c}>:4, 
      <{a},{b}>:4, <{a},{c}>:4, <{b},{c}>:3}

════════════════════════════════════════════════════════════════
ITERATION 3: Find Frequent 3-Sequences
════════════════════════════════════════════════════════════════

CANDIDATE GENERATION (Join Step):
─────────────────────────────────

Merge sequences that share (k-1) suffix/prefix

<{a,b}> and <{a,c}> → <{a,b,c}>
<{a,b}> and <{a},{b}> → <{a,b},{b}> (add element)
<{a},{b}> and <{a},{c}> → <{a},{b},{c}> or <{a},{b,c}>
<{a},{b}> and <{b},{c}> → <{a},{b},{c}>
<{a},{c}> and <{b},{c}> → <{a,b},{c}> (if merge front)
...

Generated candidates (subset):
<{a,b,c}>, <{a},{b,c}>, <{a},{b},{c}>, <{a,b},{c}>, etc.

PRUNING:
────────
Remove if any 2-subsequence is not in L₂

<{a,b,c}>: Subsequences = <{a,b}>, <{a,c}>, <{b,c}>
           All in L₂ ✓ Keep

<{a},{b,c}>: Subsequences = <{a},{b}>, <{a},{c}>, <{b,c}>
             All in L₂ ✓ Keep

<{a},{b},{c}>: Subsequences = <{a},{b}>, <{a},{c}>, <{b},{c}>
               All in L₂ ✓ Keep

SUPPORT COUNTING:
─────────────────

┌───────────────┬───────┬────────────┐
│ Candidate     │ Count │ Status     │
├───────────────┼───────┼────────────┤
│ <{a,b,c}>     │ 1     │ ✗ Infreq.  │
│ <{a},{b,c}>   │ 4     │ ✓ Frequent │
│ <{a},{b},{c}> │ 2     │ ✓ Frequent │
│ <{a,b},{c}>   │ 2     │ ✓ Frequent │
│ <{b},{b,c}>   │ 1     │ ✗ Infreq.  │
└───────────────┴───────┴────────────┘

L₃ = {<{a},{b,c}>:4, <{a},{b},{c}>:2, <{a,b},{c}>:2}

════════════════════════════════════════════════════════════════
ITERATION 4: Find Frequent 4-Sequences
════════════════════════════════════════════════════════════════

CANDIDATE GENERATION:
─────────────────────

<{a},{b,c}> + <{a},{b},{c}> → <{a},{b,c},{c}>? 
                            → <{a},{b},{b,c}>?

Let's check: <{a,b},{c}> + <{a},{b,c}> → <{a,b},{b,c}>

SUPPORT COUNTING:
─────────────────

Most 4-sequences have support < 2

L₄ = {} (empty)

════════════════════════════════════════════════════════════════
FINAL RESULT
════════════════════════════════════════════════════════════════

ALL FREQUENT SEQUENTIAL PATTERNS:
┌─────────────────────────────────────────────────────┐
│ Length │ Patterns                                   │
├────────┼────────────────────────────────────────────┤
│   1    │ <{a}>:4, <{b}>:4, <{c}>:4                 │
├────────┼────────────────────────────────────────────┤
│   2    │ <{a,b}>:2, <{a,c}>:2, <{b,c}>:4           │
│        │ <{a},{b}>:4, <{a},{c}>:4, <{b},{c}>:3     │
├────────┼────────────────────────────────────────────┤
│   3    │ <{a},{b,c}>:4, <{a},{b},{c}>:2,           │
│        │ <{a,b},{c}>:2                             │
└────────┴────────────────────────────────────────────┘
🚀 PrefixSpan Algorithm
text

PREFIXSPAN: Pattern-Growth Approach
════════════════════════════════════

Key Idea: Instead of candidate generation, 
          GROW patterns by prefix extension

ADVANTAGES OVER GSP:
- No candidate generation
- Projected databases are smaller
- More efficient for long patterns


ALGORITHM:
──────────

PrefixSpan(prefix α, projected_database S|α):

1. Scan S|α to find frequent items b

2. For each frequent item b:
   
   a. Create new prefix α' = α + b
   
   b. Create projected database S|α'
      (Only suffixes after first occurrence of b)
   
   c. Recursively call PrefixSpan(α', S|α')


PROJECTED DATABASE CONCEPT:
───────────────────────────

Original: <{a}, {a,b,c}, {a,c}, {d}, {c,f}>
Prefix: <{a}>

Find first {a}: position 1
Projected suffix: <{_,b,c}, {a,c}, {d}, {c,f}>
                   ↑
                   (_) means remaining items in same element

Prefix: <{a}, {b}>
Find {a} then {b}: {a} at pos 1, {b} at pos 2 (in {a,b,c})
Projected suffix: <{_,c}, {a,c}, {d}, {c,f}>
🔢 PrefixSpan Example
text

DATABASE:
═════════

┌─────┬────────────────────────┐
│ SID │ Sequence               │
├─────┼────────────────────────┤
│ S1  │ <{a}, {a,b}, {c}>     │
│ S2  │ <{a,b}, {c}>          │
│ S3  │ <{a}, {b}, {a,c}>     │
│ S4  │ <{b}, {a,c}>          │
└─────┴────────────────────────┘

min_sup = 2

════════════════════════════════════════════════════════════════
STEP 1: Initial Scan - Find Frequent 1-sequences
════════════════════════════════════════════════════════════════

┌───────┬───────┐
│ Item  │ Count │
├───────┼───────┤
│ a     │ 4     │ ✓
│ b     │ 4     │ ✓
│ c     │ 4     │ ✓
└───────┴───────┘

Frequent 1-sequences: <{a}>, <{b}>, <{c}>

════════════════════════════════════════════════════════════════
STEP 2: Build Projected Databases
════════════════════════════════════════════════════════════════

PROJECTED DATABASE for prefix <{a}>:
────────────────────────────────────

S1: <{a}, {a,b}, {c}> 
    First {a} at position 1
    Projection: <{_}, {a,b}, {c}> → <{a,b}, {c}>

S2: <{a,b}, {c}>
    First {a} at position 1 (within {a,b})
    Projection: <{_b}, {c}> → <{b}, {c}>
    (Note: {_b} means items after 'a' in same element)

S3: <{a}, {b}, {a,c}>
    First {a} at position 1
    Projection: <{b}, {a,c}>

S4: <{b}, {a,c}>
    First {a} at position 2 (within {a,c})
    Projection: <{_c}> → <{c}>

Projected DB for <{a}>:
┌─────┬─────────────────┐
│ SID │ Projection      │
├─────┼─────────────────┤
│ S1  │ <{a,b}, {c}>    │
│ S2  │ <{b}, {c}>      │
│ S3  │ <{b}, {a,c}>    │
│ S4  │ <{c}>           │
└─────┴─────────────────┘

════════════════════════════════════════════════════════════════
STEP 3: Mine Projected Database for <{a}>
════════════════════════════════════════════════════════════════

Scan projected DB to find locally frequent items:

┌───────┬───────┬──────────────────────────┐
│ Item  │ Count │ Extension Type           │
├───────┼───────┼──────────────────────────┤
│ _a    │ 1     │ Same element (S1)        │
│ _b    │ 2     │ Same element (S1,S2)     │
│ a     │ 2     │ New element (S1,S3)      │
│ b     │ 3     │ New element (S1,S2,S3)   │
│ c     │ 4     │ New element (all)        │
└───────┴───────┴──────────────────────────┘

Frequent extensions from <{a}>:
- <{a},{b}> (support 3) ✓
- <{a},{c}> (support 4) ✓
- <{a,b}> (support 2) ✓

════════════════════════════════════════════════════════════════
STEP 4: Recursively Mine <{a},{b}>
════════════════════════════════════════════════════════════════

Projected DB for <{a},{b}>:
(From <{a}>'s projected DB, find {b}, take suffix)

S1: <{a,b}, {c}> → after {b}: <{c}>
S2: <{b}, {c}> → after {b}: <{c}>
S3: <{b}, {a,c}> → after {b}: <{a,c}>

┌─────┬─────────────────┐
│ SID │ Projection      │
├─────┼─────────────────┤
│ S1  │ <{c}>           │
│ S2  │ <{c}>           │
│ S3  │ <{a,c}>         │
└─────┴─────────────────┘

Frequent items: c (count 3)

New pattern: <{a},{b},{c}> (support 3) ✓

Continue recursively...

════════════════════════════════════════════════════════════════
COMPLETE RESULTS (Summary)
════════════════════════════════════════════════════════════════

All Frequent Sequential Patterns:

Length 1: <{a}>:4, <{b}>:4, <{c}>:4

Length 2: <{a},{b}>:3, <{a},{c}>:4, <{a,b}>:2
          <{b},{c}>:3, <{b},{a}>:2

Length 3: <{a},{b},{c}>:3, <{a,b},{c}>:2
          <{a},{b,c}>:2
📊 Constraints in Sequential Mining
text

TIME CONSTRAINTS:
═════════════════

┌─────────────────────────────────────────────────────────────┐
│  min_gap: Minimum time between consecutive events          │
│  max_gap: Maximum time between consecutive events          │
│  max_span: Maximum total time of sequence                  │
│  window: Time window for same-event items                  │
└─────────────────────────────────────────────────────────────┘

Example:
min_gap = 1 day
max_gap = 7 days
max_span = 30 days

Sequence with timestamps:
<{iPhone}(Day 1), {Case}(Day 3), {AirPods}(Day 25)>

Check constraints:
- Gap between iPhone and Case: 2 days ≥ 1 ✓ and ≤ 7 ✓
- Gap between Case and AirPods: 22 days ≥ 1 ✓ but > 7 ✗
- Total span: 24 days ≤ 30 ✓

This sequence VIOLATES max_gap constraint!


ITEM CONSTRAINTS:
═════════════════

- Must contain specific items
- Must not contain specific items
- Item taxonomy constraints


PATTERN CONSTRAINTS:
════════════════════

- Minimum/maximum length
- Regular expression patterns
- Closed sequential patterns
🔍 Applications of Sequential Pattern Mining
text

┌─────────────────────────────────────────────────────────────┐
│            SEQUENTIAL PATTERN APPLICATIONS                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🛒 RETAIL                                                  │
│     Customer purchase sequences over time                   │
│     Example: Phone → Case → Screen Protector                │
│                                                             │
│  🌐 WEB ANALYTICS                                           │
│     User clickstream patterns                               │
│     Example: Home → Products → Cart → Checkout              │
│                                                             │
│  🏥 HEALTHCARE                                              │
│     Disease progression, treatment sequences                │
│     Example: Symptom A → Test B → Diagnosis C               │
│                                                             │
│  🧬 BIOINFORMATICS                                          │
│     DNA/Protein sequences                                   │
│     Gene expression patterns                                │
│                                                             │
│  💰 FINANCE                                                 │
│     Stock price movements                                   │
│     Transaction fraud patterns                              │
│                                                             │
│  📱 TELECOM                                                 │
│     Call patterns, service usage                            │
│     Churn prediction                                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📝 Chapter 9 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 9: KEY TAKEAWAYS                                 ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Sequential patterns consider ORDER of events           ║
║  ✓ Notation: <{e₁}, {e₂}, ...> for ordered elements      ║
║  ✓ GSP: Apriori-like approach with join/prune             ║
║  ✓ PrefixSpan: Pattern-growth with projections           ║
║  ✓ Subsequence relationship determines support            ║
║  ✓ Time constraints add real-world applicability          ║
║  ✓ Key applications: Web, retail, healthcare, bioinfo     ║
╚═══════════════════════════════════════════════════════════╝
Chapter 10: Constraint-Based Mining {#chapter-10}
🎯 Why Constraints?
text

THE PROBLEM:
════════════

Mining without constraints produces:
- TOO MANY patterns (millions!)
- IRRELEVANT patterns
- DIFFICULT to interpret results
- WASTED computational resources

THE SOLUTION:
═════════════

Use constraints to:
- Focus on INTERESTING patterns
- REDUCE search space
- IMPROVE efficiency
- GET actionable results
📚 Types of Constraints
text

┌─────────────────────────────────────────────────────────────┐
│              CONSTRAINT CLASSIFICATION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. ITEM CONSTRAINTS                                        │
│     - Must contain / must not contain specific items        │
│                                                             │
│  2. AGGREGATE CONSTRAINTS                                   │
│     - Based on aggregate functions (sum, avg, count)        │
│                                                             │
│  3. SUPPORT/CONFIDENCE CONSTRAINTS                          │
│     - Minimum thresholds (already covered)                  │
│                                                             │
│  4. TEMPORAL CONSTRAINTS                                    │
│     - Time windows, sequences                               │
│                                                             │
│  5. DIMENSIONAL CONSTRAINTS                                 │
│     - Based on item attributes                              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🔍 Constraint Properties
text

ANTI-MONOTONE CONSTRAINT:
═════════════════════════

If itemset S VIOLATES the constraint,
then ANY superset of S also VIOLATES it.

Examples:
─────────
• support(S) ≥ min_sup
  If {A,B} has support < min_sup, 
  {A,B,C} will also have support < min_sup ✓

• sum(price) ≤ 100
  If sum({A,B}) > 100,
  adding more items only increases sum ✓

• count(items) ≤ 5
  If |{A,B,C,D,E}| = 5 already,
  any superset violates ✓

USE: Can PRUNE search space early!


MONOTONE CONSTRAINT:
════════════════════

If itemset S SATISFIES the constraint,
then ANY superset of S also SATISFIES it.

Examples:
─────────
• sum(price) ≥ 100
  If sum({A,B}) ≥ 100,
  adding items only keeps it ≥ 100 ✓

• S contains item 'Milk'
  If {A, Milk} contains Milk,
  {A, Milk, B} also contains Milk ✓

USE: Once satisfied, no need to check again!


SUCCINCT CONSTRAINT:
════════════════════

Can enumerate all satisfying itemsets DIRECTLY
without checking against database.

Examples:
─────────
• S contains item 'A'
  → Direct enumeration: All itemsets including A

• S ⊆ {A, B, C, D}
  → Direct enumeration: All subsets of {A,B,C,D}

• min(price) ≤ 50
  → Start with items having price ≤ 50

USE: Generate candidates directly!


CONVERTIBLE CONSTRAINT:
═══════════════════════

Can be made anti-monotone or monotone by
ORDERING items appropriately.

Examples:
─────────
• avg(price) ≥ 100
  Order items by descending price
  If avg drops below 100, adding cheaper items won't help

• avg(price) ≤ 100
  Order items by ascending price
  If avg exceeds 100, adding more expensive items won't help

USE: With proper ordering, can enable pruning!
📊 Constraint Classification Table
text

┌────────────────────────┬────────────┬──────────┬──────────┬────────────┐
│ Constraint             │ Anti-Mono  │ Monotone │ Succinct │Convertible │
├────────────────────────┼────────────┼──────────┼──────────┼────────────┤
│ support ≥ min_sup      │     ✓      │          │          │            │
│ support ≤ max_sup      │            │    ✓     │          │            │
│ S contains A           │            │    ✓     │    ✓     │            │
│ S ⊆ V (subset)         │            │    ✓     │    ✓     │            │
│ S ⊇ V (superset)       │     ✓      │          │    ✓     │            │
│ min(S) ≥ v             │            │    ✓     │    ✓     │            │
│ min(S) ≤ v             │     ✓      │          │    ✓     │            │
│ max(S) ≥ v             │            │    ✓     │    ✓     │            │
│ max(S) ≤ v             │     ✓      │          │    ✓     │            │
│ sum(S) ≥ v             │            │    ✓     │          │            │
│ sum(S) ≤ v             │     ✓      │          │          │            │
│ count(S) ≥ v           │            │    ✓     │          │            │
│ count(S) ≤ v           │     ✓      │          │          │            │
│ avg(S) ≥ v             │            │          │          │     ✓      │
│ avg(S) ≤ v             │            │          │          │     ✓      │
│ range(S) ≥ v           │            │    ✓     │          │            │
│ range(S) ≤ v           │     ✓      │          │          │            │
└────────────────────────┴────────────┴──────────┴──────────┴────────────┘
🔢 Constraint-Based Mining Example
text

DATABASE:
═════════

┌─────┬─────────────────┬─────────────────────────────┐
│ TID │ Items           │ Prices                      │
├─────┼─────────────────┼─────────────────────────────┤
│ T1  │ {A, B, D, E}    │ A=$20, B=$50, D=$10, E=$40 │
│ T2  │ {A, C, E}       │ A=$20, C=$80, E=$40        │
│ T3  │ {B, C, D}       │ B=$50, C=$80, D=$10        │
│ T4  │ {A, B, C, D}    │ A=$20, B=$50, C=$80, D=$10 │
│ T5  │ {A, B, E}       │ A=$20, B=$50, E=$40        │
└─────┴─────────────────┴─────────────────────────────┘

Item Prices: A=$20, B=$50, C=$80, D=$10, E=$40

CONSTRAINTS:
────────────
C1: support ≥ 2 (anti-monotone)
C2: sum(price) ≥ 100 (monotone)
C3: must contain item A (monotone, succinct)

GOAL: Find all frequent itemsets satisfying ALL constraints

════════════════════════════════════════════════════════════════
STEP 1: Apply Succinct Constraint C3 First
════════════════════════════════════════════════════════════════

C3: Must contain A

Only consider itemsets containing A:
Candidates: All subsets of {A,B,C,D,E} that include A

This eliminates {B}, {C}, {D}, {E}, {B,C}, {B,D}, etc.

Remaining search space:
{A}, {A,B}, {A,C}, {A,D}, {A,E}, {A,B,C}, {A,B,D}, {A,B,E},
{A,C,D}, {A,C,E}, {A,D,E}, {A,B,C,D}, {A,B,C,E}, {A,B,D,E},
{A,C,D,E}, {A,B,C,D,E}

════════════════════════════════════════════════════════════════
STEP 2: Apply Anti-Monotone Constraint C1
════════════════════════════════════════════════════════════════

C1: support ≥ 2

Count support for candidates:

1-itemsets with A:
{A}: T1,T2,T4,T5 → support = 4 ✓

2-itemsets:
{A,B}: T1,T4,T5 → support = 3 ✓
{A,C}: T2,T4 → support = 2 ✓
{A,D}: T1,T4 → support = 2 ✓
{A,E}: T1,T2,T5 → support = 3 ✓

3-itemsets:
{A,B,D}: T1,T4 → support = 2 ✓
{A,B,E}: T1,T5 → support = 2 ✓
{A,C,D}: T4 only → support = 1 ✗ PRUNE
{A,C,E}: T2 only → support = 1 ✗ PRUNE
{A,D,E}: T1 only → support = 1 ✗ PRUNE
{A,B,C}: T4 only → support = 1 ✗ PRUNE

Since {A,C,D}, {A,C,E}, {A,D,E}, {A,B,C} are infrequent,
all their supersets are also pruned (anti-monotone property)

4-itemsets:
{A,B,D,E}: T1 only → support = 1 ✗ PRUNE
(All others already pruned due to infrequent subsets)

Frequent itemsets with A: 
{A}:4, {A,B}:3, {A,C}:2, {A,D}:2, {A,E}:3, {A,B,D}:2, {A,B,E}:2

════════════════════════════════════════════════════════════════
STEP 3: Apply Monotone Constraint C2
════════════════════════════════════════════════════════════════

C2: sum(price) ≥ 100

Check each frequent itemset:

{A}: sum = 20 < 100 ✗
{A,B}: sum = 20+50 = 70 < 100 ✗
{A,C}: sum = 20+80 = 100 ≥ 100 ✓
{A,D}: sum = 20+10 = 30 < 100 ✗
{A,E}: sum = 20+40 = 60 < 100 ✗
{A,B,D}: sum = 20+50+10 = 80 < 100 ✗
{A,B,E}: sum = 20+50+40 = 110 ≥ 100 ✓

FINAL ANSWER:
─────────────
Itemsets satisfying ALL constraints:
┌────────────┬─────────┬─────────┬────────────┐
│ Itemset    │ Support │ Sum     │ Contains A │
├────────────┼─────────┼─────────┼────────────┤
│ {A,C}      │ 2       │ $100    │ ✓          │
│ {A,B,E}    │ 2       │ $110    │ ✓          │
└────────────┴─────────┴─────────┴────────────┘
🔄 Convertible Constraints: avg() Example
text

CONVERTIBLE CONSTRAINT EXAMPLE:
═══════════════════════════════

Constraint: avg(price) ≥ 50

Items with prices:
A=$20, B=$50, C=$80, D=$10, E=$40

STEP 1: Order items by DESCENDING price
─────────────────────────────────────────
C($80) > B($50) > E($40) > A($20) > D($10)

STEP 2: Mine with ordered items
─────────────────────────────────

Start with highest: {C}
avg({C}) = 80 ≥ 50 ✓

Extend with next item:
{C,B}: avg = (80+50)/2 = 65 ≥ 50 ✓
{C,E}: avg = (80+40)/2 = 60 ≥ 50 ✓

{C,B,E}: avg = (80+50+40)/3 = 56.67 ≥ 50 ✓
{C,B,A}: avg = (80+50+20)/3 = 50 ≥ 50 ✓

{C,B,E,A}: avg = (80+50+40+20)/4 = 47.5 < 50 ✗

PRUNING RULE (with descending order):
─────────────────────────────────────
If avg(S) < threshold after adding next item,
adding any SMALLER item will only decrease avg further.

So if {C,B,E,A} fails, {C,B,E,A,D} will also fail!
(D=$10 is smallest)

This converts avg constraint to ANTI-MONOTONE behavior
with proper ordering!
🎯 Constraint Pushing Strategies
text

CONSTRAINT PUSHING:
═══════════════════

Apply constraints as EARLY as possible in mining process

┌─────────────────────────────────────────────────────────────┐
│                  PUSHING STRATEGIES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  LEVEL 1: Data Pre-processing                               │
│  ─────────────────────────────                              │
│  • Remove items that can never satisfy constraints          │
│  • Example: If min(price) ≥ 50, remove all items < $50     │
│                                                             │
│  LEVEL 2: Candidate Generation                              │
│  ─────────────────────────────                              │
│  • Only generate candidates that COULD satisfy              │
│  • Use succinct constraints here                            │
│                                                             │
│  LEVEL 3: Candidate Pruning                                 │
│  ─────────────────────────────                              │
│  • Apply anti-monotone constraints                          │
│  • Prune entire subtrees early                              │
│                                                             │
│  LEVEL 4: Support Counting                                  │
│  ─────────────────────────────                              │
│  • Check constraints during counting                        │
│  • Avoid counting obviously invalid candidates              │
│                                                             │
│  LEVEL 5: Post-processing                                   │
│  ─────────────────────────────                              │
│  • Apply monotone constraints at end                        │
│  • Filter final results                                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘


OPTIMAL STRATEGY:
─────────────────

1. Apply SUCCINCT constraints first (generate candidates)
2. Apply ANTI-MONOTONE constraints during mining (pruning)
3. Apply CONVERTIBLE constraints with ordering
4. Apply MONOTONE constraints at the end (filtering)
📝 Chapter 10 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 10: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Constraints focus mining on relevant patterns          ║
║  ✓ Anti-monotone: If S fails, supersets fail (PRUNING)    ║
║  ✓ Monotone: If S passes, supersets pass (no re-check)    ║
║  ✓ Succinct: Direct enumeration possible                  ║
║  ✓ Convertible: Becomes anti/monotone with ordering       ║
║  ✓ Push constraints as early as possible                  ║
║  ✓ Order: Succinct → Anti-mono → Convertible → Monotone   ║
╚═══════════════════════════════════════════════════════════╝
Chapter 11: Rare & Negative Association Rules {#chapter-11}
🎯 Why Rare Patterns Matter
text

THE OVERLOOKED PATTERNS:
════════════════════════

Traditional mining focuses on FREQUENT patterns.
But RARE patterns can be extremely valuable!

┌─────────────────────────────────────────────────────────────┐
│              RARE PATTERN APPLICATIONS                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🔒 FRAUD DETECTION                                         │
│     Unusual transaction patterns (rare by definition!)      │
│                                                             │
│  🏥 MEDICAL DIAGNOSIS                                       │
│     Rare disease symptoms, drug side effects                │
│                                                             │
│  🛡️ SECURITY                                                │
│     Intrusion detection, anomaly patterns                   │
│                                                             │
│  🔬 SCIENTIFIC DISCOVERY                                    │
│     Novel gene combinations, rare chemical reactions        │
│                                                             │
│  📉 RISK MANAGEMENT                                         │
│     Black swan events, unlikely but critical scenarios      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📊 The Rare Itemset Problem
text

PROBLEM WITH LOW SUPPORT:
═════════════════════════

If we lower min_support to catch rare items:
→ EXPLOSION of frequent itemsets
→ Many false positives
→ Computational nightmare

Example:
min_sup = 5% → 1,000 patterns
min_sup = 1% → 100,000 patterns
min_sup = 0.1% → 10,000,000 patterns!


THE RARE ITEM PROBLEM:
══════════════════════

Item frequencies vary wildly:

{Bread}: 80% support (very common)
{Milk}: 70% support (common)
{Caviar}: 0.5% support (rare)
{Truffle}: 0.1% support (very rare)

With uniform min_sup = 5%:
- Find {Bread, Milk} patterns ✓
- Miss {Caviar, Champagne} patterns ✗

With uniform min_sup = 0.5%:
- Find rare patterns ✓
- Overwhelmed with trivial common patterns ✗
🔧 Solutions for Rare Pattern Mining
Solution 1: Multiple Minimum Supports (MSApriori)
text

MULTIPLE MINIMUM SUPPORT (MMS):
═══════════════════════════════

Assign DIFFERENT min_support to each item based on frequency

Formula:
MIS(i) = max(β × support(i), LS)

Where:
- β: User-defined proportion (e.g., 0.5)
- LS: Lowest minimum support (floor)

Example:
─────────
Item frequencies:
A: 80%, B: 60%, C: 20%, D: 5%, E: 1%

β = 0.3, LS = 0.5%

MIS(A) = max(0.3 × 80%, 0.5%) = max(24%, 0.5%) = 24%
MIS(B) = max(0.3 × 60%, 0.5%) = max(18%, 0.5%) = 18%
MIS(C) = max(0.3 × 20%, 0.5%) = max(6%, 0.5%) = 6%
MIS(D) = max(0.3 × 5%, 0.5%) = max(1.5%, 0.5%) = 1.5%
MIS(E) = max(0.3 × 1%, 0.5%) = max(0.3%, 0.5%) = 0.5%

For itemset {A,C,E}:
min_support = min(MIS(A), MIS(C), MIS(E))
            = min(24%, 6%, 0.5%)
            = 0.5%

This allows rare items to be included!
Solution 2: Relative Support
text

RELATIVE SUPPORT:
═════════════════

Instead of absolute support, use relative measure

RelativeSupport(X → Y) = Support(X ∪ Y) / Support(X)
                        = Confidence(X → Y)

Example:
─────────
{Caviar, Champagne}: absolute support = 0.1%
{Caviar}: support = 0.5%

RelativeSupport = 0.1% / 0.5% = 20%

Even though absolute support is tiny,
20% of caviar buyers also buy champagne!
This is a STRONG relationship worth finding.
Solution 3: Affinity-Based Measures
text

AFFINITY MEASURE:
═════════════════

              Support(X ∪ Y)
Affinity = ────────────────────────
            √(Support(X) × Support(Y))

This normalizes by item frequencies.

Example:
─────────
Support({Caviar, Champagne}) = 0.001
Support({Caviar}) = 0.005
Support({Champagne}) = 0.008

Affinity = 0.001 / √(0.005 × 0.008)
         = 0.001 / √0.00004
         = 0.001 / 0.00632
         = 0.158 = 15.8%

Compare to:
Support({Bread, Milk}) = 0.50
Support({Bread}) = 0.80
Support({Milk}) = 0.70

Affinity = 0.50 / √(0.80 × 0.70)
         = 0.50 / √0.56
         = 0.50 / 0.748
         = 0.668 = 66.8%

Both relationships are meaningful in their contexts!
🔄 Negative Association Rules
text

WHAT ARE NEGATIVE RULES?
════════════════════════

Standard (Positive): A → B (If A then B)
Negative Rules:      A → ¬B (If A then NOT B)
                    ¬A → B (If NOT A then B)
                    ¬A → ¬B (If NOT A then NOT B)

Examples:
─────────
{Butter} → ¬{Margarine}
"Customers who buy butter do NOT buy margarine"

{Laptop} → ¬{Desktop}
"Customers who buy laptop do NOT buy desktop"

{Premium_Membership} → ¬{Coupon_Usage}
"Premium members don't use coupons"
📊 Mining Negative Association Rules
text

COMPUTING NEGATIVE SUPPORT:
═══════════════════════════

Support(¬A) = 1 - Support(A)
Support(A ∧ ¬B) = Support(A) - Support(A ∧ B)

Example:
─────────
Total transactions: N = 1000
Support(Coffee) = 600/1000 = 0.60
Support(Tea) = 400/1000 = 0.40
Support(Coffee, Tea) = 100/1000 = 0.10

Support(Coffee ∧ ¬Tea) = Support(Coffee) - Support(Coffee ∧ Tea)
                       = 0.60 - 0.10 = 0.50

Confidence(Coffee → ¬Tea) = Support(Coffee ∧ ¬Tea) / Support(Coffee)
                          = 0.50 / 0.60 = 0.833 = 83.3%

"83% of coffee buyers do NOT buy tea!"


WHEN IS A NEGATIVE RULE INTERESTING?
════════════════════════════════════

Rule {A} → ¬{B} is interesting if:

1. Support(A ∧ ¬B) ≥ min_support
2. Confidence(A → ¬B) ≥ min_confidence  
3. Support(A ∧ B) < Expected under independence

Expected under independence:
E[Support(A ∧ B)] = Support(A) × Support(B)

If actual Support(A ∧ B) << Expected:
→ Negative correlation exists!

Example:
─────────
Expected(Coffee ∧ Tea) = 0.60 × 0.40 = 0.24
Actual(Coffee ∧ Tea) = 0.10

0.10 << 0.24 → Strong NEGATIVE association!
🔢 Complete Negative Rule Example
text

DATABASE ANALYSIS:
══════════════════

N = 1000 transactions

┌─────────────┬──────────────┬─────────────┐
│ Item        │ Transactions │ Support     │
├─────────────┼──────────────┼─────────────┤
│ Laptop      │ 300          │ 30%         │
│ Desktop     │ 250          │ 25%         │
│ Laptop,Desk │ 20           │ 2%          │
└─────────────┴──────────────┴─────────────┘

STEP 1: Check for Negative Association
───────────────────────────────────────

Expected(Laptop ∧ Desktop) = 0.30 × 0.25 = 0.075 = 7.5%
Actual(Laptop ∧ Desktop) = 0.02 = 2%

Difference: 7.5% - 2% = 5.5%
Ratio: 2% / 7.5% = 0.267

Strong negative association! (Only 26.7% of expected)


STEP 2: Calculate Negative Rule Metrics
───────────────────────────────────────

Rule: {Laptop} → ¬{Desktop}

Support(Laptop ∧ ¬Desktop) = Support(Laptop) - Support(Laptop ∧ Desktop)
                           = 0.30 - 0.02 = 0.28 = 28%

Confidence(Laptop → ¬Desktop) = 0.28 / 0.30 = 0.933 = 93.3%

Lift(Laptop → ¬Desktop) = Conf(Laptop → ¬Desktop) / Support(¬Desktop)
                        = 0.933 / 0.75 = 1.244

STEP 3: Interpret Results
─────────────────────────

Support = 28% ≥ 5% ✓
Confidence = 93.3% ≥ 50% ✓
Lift = 1.244 > 1 ✓ (Positive correlation for the negative rule)

CONCLUSION:
───────────
╔═══════════════════════════════════════════════════════════╗
║ Rule: {Laptop} → ¬{Desktop}                               ║
║                                                           ║
║ "93.3% of laptop buyers do NOT buy desktops"             ║
║                                                           ║
║ Business Insight: Cross-selling desktop to laptop         ║
║ buyers is unlikely to succeed. Focus on accessories!      ║
╚═══════════════════════════════════════════════════════════╝
🎯 Identifying Negative Associations
text

CORRELATION COEFFICIENT METHOD:
═══════════════════════════════

Use φ-coefficient (phi) for binary data:

         P(A∧B) - P(A)×P(B)
φ = ──────────────────────────────
     √(P(A)×P(B)×P(¬A)×P(¬B))

φ < 0 → Negative association
φ = 0 → No association  
φ > 0 → Positive association

Example:
─────────
P(Laptop) = 0.30
P(Desktop) = 0.25
P(Laptop ∧ Desktop) = 0.02
P(¬Laptop) = 0.70
P(¬Desktop) = 0.75

φ = (0.02 - 0.30×0.25) / √(0.30×0.25×0.70×0.75)
  = (0.02 - 0.075) / √0.039375
  = -0.055 / 0.1984
  = -0.277

φ = -0.277 < 0 → NEGATIVE ASSOCIATION ✓


MINIMUM INTERESTINGNESS:
════════════════════════

Only report negative rules where:
|φ| ≥ threshold (e.g., 0.2)

This filters out weak/random correlations.
📊 Rare vs Negative: Summary
text

┌────────────────────────────────────────────────────────────────┐
│          RARE vs NEGATIVE ASSOCIATION RULES                    │
├────────────────┬───────────────────┬───────────────────────────┤
│   Aspect       │   Rare Rules      │   Negative Rules          │
├────────────────┼───────────────────┼───────────────────────────┤
│ Pattern Type   │ Low frequency     │ Inverse relationship      │
│                │ items/itemsets    │ between items             │
├────────────────┼───────────────────┼───────────────────────────┤
│ Example        │ {Caviar}→         │ {Butter}→                 │
│                │ {Champagne}       │ ¬{Margarine}              │
├────────────────┼───────────────────┼───────────────────────────┤
│ Support        │ Low but           │ Can be high               │
│                │ significant       │ (for the negation)        │
├────────────────┼───────────────────┼───────────────────────────┤
│ Challenge      │ Distinguishing    │ Avoiding trivial          │
│                │ from noise        │ negations                 │
├────────────────┼───────────────────┼───────────────────────────┤
│ Use Case       │ Fraud, anomaly,   │ Substitutes,              │
│                │ niche markets     │ incompatible products     │
└────────────────┴───────────────────┴───────────────────────────┘
📝 Chapter 11 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 11: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Rare patterns: Low support but high value              ║
║  ✓ Multiple min-support handles varying item frequencies  ║
║  ✓ Relative/affinity measures normalize for frequency     ║
║  ✓ Negative rules: A → ¬B (items bought separately)       ║
║  ✓ φ-coefficient identifies negative correlations         ║
║  ✓ Applications: Fraud, substitutes, incompatibilities    ║
╚═══════════════════════════════════════════════════════════╝
Chapter 12: Real-World Applications {#chapter-12}
🛒 Application 1: Retail & Market Basket Analysis
text

MARKET BASKET ANALYSIS:
═══════════════════════

The original application of association rules!

┌─────────────────────────────────────────────────────────────┐
│                 RETAIL USE CASES                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📦 PRODUCT PLACEMENT                                       │
│     Rule: {Bread} → {Butter}                               │
│     Action: Place bread near butter section                 │
│                                                             │
│  🏷️ CROSS-SELLING                                          │
│     Rule: {Phone} → {Phone Case, Screen Protector}         │
│     Action: Recommend accessories at checkout               │
│                                                             │
│  📢 PROMOTIONAL BUNDLES                                     │
│     Rule: {Chips, Dip, Soda} (frequently together)          │
│     Action: Create "Party Bundle" promotion                 │
│                                                             │
│  📊 INVENTORY MANAGEMENT                                    │
│     Rule: {Summer Items} appear together seasonally         │
│     Action: Stock related items together                    │
│                                                             │
└─────────────────────────────────────────────────────────────┘


REAL CASE STUDY: The Beer-Diapers Legend
═════════════════════════════════════════

Discovery: {Diapers} → {Beer} (Friday evenings)

Analysis:
- Young fathers sent to buy diapers
- Also picked up beer for the weekend
- Correlation found in evening transaction data

Business Action:
- Placed beer near diapers section
- Sales of both increased!

Whether true or myth, it illustrates the power of 
unexpected pattern discovery!
🌐 Application 2: Web Mining & Recommendation Systems
text

WEB USAGE MINING:
═════════════════

┌─────────────────────────────────────────────────────────────┐
│              WEB PATTERN EXAMPLES                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  CLICKSTREAM PATTERNS:                                      │
│  {Homepage, Products, Cart} → {Checkout}                   │
│  Action: Optimize conversion funnel                         │
│                                                             │
│  SESSION PATTERNS:                                          │
│  {Search_Query} → {Category_Browse} → {Purchase}           │
│  Action: Improve search relevance                           │
│                                                             │
│  CONTENT ASSOCIATION:                                       │
│  {Article_A} → {Article_B}                                 │
│  Action: "Related articles" recommendations                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘


COLLABORATIVE FILTERING:
═══════════════════════

User-Item Association Mining

Database:
┌─────────┬─────────────────────────────┐
│ User    │ Items Purchased/Liked       │
├─────────┼─────────────────────────────┤
│ User1   │ {Movie_A, Movie_B, Movie_D} │
│ User2   │ {Movie_A, Movie_C}          │
│ User3   │ {Movie_A, Movie_B, Movie_C} │
│ User4   │ {Movie_B, Movie_D}          │
└─────────┴─────────────────────────────┘

Rule: {Movie_A, Movie_B} → {Movie_C}

For User1 (has A, B but not C):
→ Recommend Movie_C!

AMAZON: "Customers who bought X also bought Y"
NETFLIX: "Because you watched X, you might like Y"
SPOTIFY: "Fans also like..."
🏥 Application 3: Healthcare & Medical Diagnosis
text

MEDICAL PATTERN MINING:
═══════════════════════

┌─────────────────────────────────────────────────────────────┐
│              HEALTHCARE APPLICATIONS                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🔬 DISEASE-SYMPTOM ASSOCIATIONS                            │
│     {Symptom_A, Symptom_B} → {Disease_X}                   │
│     Assists in diagnosis                                    │
│                                                             │
│  💊 DRUG INTERACTION DETECTION                              │
│     {Drug_A, Drug_B} → {Adverse_Effect}                    │
│     Prevents harmful combinations                           │
│                                                             │
│  📋 TREATMENT PATTERNS                                      │
│     {Diagnosis_X} → {Treatment_Y, Treatment_Z}             │
│     Identifies effective treatment protocols                │
│                                                             │
│  📈 RISK FACTOR ANALYSIS                                    │
│     {Smoking, High_BP} → {Heart_Disease}                   │
│     Preventive care recommendations                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘


EXAMPLE: Drug Side Effect Detection
════════════════════════════════════

Patient Database:
┌─────────┬──────────────────────────────────────┐
│ Patient │ {Drugs, Conditions, Side Effects}    │
├─────────┼──────────────────────────────────────┤
│ P1      │ {DrugA, DrugB, Nausea, Dizziness}   │
│ P2      │ {DrugA, DrugC, Fatigue}             │
│ P3      │ {DrugB, DrugC, Nausea}              │
│ P4      │ {DrugA, DrugB, Nausea, Headache}    │
│ P5      │ {DrugA, DrugB, Dizziness}           │
└─────────┴──────────────────────────────────────┘

Discovered Rule:
{DrugA, DrugB} → {Nausea}
Support: 40%, Confidence: 66%, Lift: 2.5

WARNING: Combining DrugA and DrugB may cause nausea!
This could reveal previously unknown drug interactions.
🏦 Application 4: Banking & Fraud Detection
text

FRAUD DETECTION PATTERNS:
═════════════════════════

┌─────────────────────────────────────────────────────────────┐
│              BANKING APPLICATIONS                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🚨 SUSPICIOUS PATTERNS                                     │
│     {Large_Withdrawal, Foreign_Location, Night_Time}       │
│     → Potential fraud alert                                 │
│                                                             │
│  💳 CREDIT CARD FRAUD                                       │
│     {Gas_Station_Purchase} → {High_Value_Electronics}      │
│     within 1 hour = fraud indicator                         │
│                                                             │
│  🔐 ACCOUNT TAKEOVER                                        │
│     {Password_Change, Email_Change, Phone_Change}          │
│     in sequence → account compromise                        │
│                                                             │
│  💰 MONEY LAUNDERING                                        │
│     {Multiple_Small_Deposits} → {Large_Transfer_Offshore}  │
│     Structuring pattern detection                           │
│                                                             │
└─────────────────────────────────────────────────────────────┘


NEGATIVE RULES IN FRAUD:
═══════════════════════

Normal Pattern: {Regular_Customer} → {Consistent_Spending}

Anomaly Detection:
If Customer_X VIOLATES this pattern → FLAG

{VIP_Customer} → ¬{ATM_Max_Withdrawal}
Violation triggers fraud investigation
🧬 Application 5: Bioinformatics
text

BIOINFORMATICS APPLICATIONS:
════════════════════════════

┌─────────────────────────────────────────────────────────────┐
│              BIOLOGICAL PATTERN MINING                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🧬 GENE EXPRESSION ANALYSIS                                │
│     {Gene_A, Gene_B} → {Gene_C}                            │
│     Co-expression patterns                                  │
│                                                             │
│  🦠 PROTEIN INTERACTION                                     │
│     {Protein_X} → {Protein_Y, Protein_Z}                   │
│     Protein complex discovery                               │
│                                                             │
│  💊 DRUG DISCOVERY                                          │
│     {Molecular_Feature_A} → {Drug_Efficacy}                │
│     Identifying drug candidates                             │
│                                                             │
│  🔬 DISEASE MARKERS                                         │
│     {Biomarker_Set} → {Disease_Subtype}                    │
│     Precision medicine                                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘


SEQUENTIAL PATTERNS IN GENOMICS:
════════════════════════════════

DNA Motif Discovery:
<{A,T}, {G,C}, {A,T}, {G,G}> → Promoter Region

Protein Folding Sequences:
<{Alpha_Helix}, {Loop}, {Beta_Sheet}> → Structural Pattern
📊 Application Summary Table
text

┌────────────────┬─────────────────────┬─────────────────────────┐
│   Domain       │   Pattern Type      │   Business Value        │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Retail         │ Market basket       │ Cross-selling,          │
│                │ analysis            │ store layout            │
├────────────────┼─────────────────────┼─────────────────────────┤
│ E-commerce     │ Click patterns,     │ Recommendations,        │
│                │ purchase sequences  │ personalization         │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Healthcare     │ Symptom-disease,    │ Diagnosis support,      │
│                │ drug interactions   │ patient safety          │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Banking        │ Fraud patterns,     │ Loss prevention,        │
│                │ transaction anomaly │ security                │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Telecom        │ Call patterns,      │ Churn prediction,       │
│                │ service usage       │ service bundles         │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Manufacturing  │ Defect patterns,    │ Quality control,        │
│                │ failure sequences   │ predictive maintenance  │
├────────────────┼─────────────────────┼─────────────────────────┤
│ Education      │ Learning paths,     │ Curriculum design,      │
│                │ course associations │ personalized learning   │
└────────────────┴─────────────────────┴─────────────────────────┘
📝 Chapter 12 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 12: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Association rules apply to virtually every industry    ║
║  ✓ Retail: Product placement, cross-selling, bundles      ║
║  ✓ Web: Recommendations, click analysis, personalization  ║
║  ✓ Healthcare: Diagnosis, drug safety, treatment paths    ║
║  ✓ Banking: Fraud detection, customer behavior            ║
║  ✓ Success requires domain expertise + data mining        ║
╚═══════════════════════════════════════════════════════════╝
Chapter 13: Implementation Guide with Python {#chapter-13}
🛠️ Required Libraries
Python

# Installation commands
# pip install pandas numpy mlxtend

# Core libraries
import pandas as pd
import numpy as np
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, fpgrowth, association_rules
import warnings
warnings.filterwarnings('ignore')
📊 Data Preparation
Python

"""
DATA PREPARATION FOR ASSOCIATION RULE MINING
=============================================
"""

# Sample transaction data
transactions = [
    ['Bread', 'Milk', 'Eggs'],
    ['Bread', 'Butter', 'Milk'],
    ['Bread', 'Butter'],
    ['Beer', 'Diapers', 'Bread'],
    ['Beer', 'Diapers', 'Milk'],
    ['Bread', 'Milk', 'Butter', 'Eggs'],
    ['Bread', 'Milk', 'Butter'],
    ['Beer', 'Bread'],
    ['Bread', 'Milk'],
    ['Beer', 'Diapers']
]

# Method 1: Using TransactionEncoder (for list format)
te = TransactionEncoder()
te_array = te.fit(transactions).transform(transactions)
df = pd.DataFrame(te_array, columns=te.columns_)

print("Transaction Matrix:")
print(df)

"""
OUTPUT:
   Beer  Bread  Butter  Diapers   Eggs   Milk
0  False   True   False    False   True   True
1  False   True    True    False  False   True
2  False   True    True    False  False  False
3   True   True   False     True  False  False
4   True  False   False     True  False   True
5  False   True    True    False   True   True
6  False   True    True    False  False   True
7   True   True   False    False  False  False
8  False   True   False    False  False   True
9   True  False   False     True  False  False
"""

# Method 2: From DataFrame with one-hot encoding
# If your data is already in transaction format:
data = {
    'Transaction_ID': [1, 1, 1, 2, 2, 3, 3, 3],
    'Item': ['Bread', 'Milk', 'Eggs', 'Bread', 'Butter', 
             'Bread', 'Milk', 'Butter']
}
df_transactions = pd.DataFrame(data)

# Create pivot table (one-hot encoded)
df_encoded = df_transactions.pivot_table(
    index='Transaction_ID', 
    columns='Item', 
    aggfunc=lambda x: True,
    fill_value=False
)
🔄 Apriori Implementation
Python

"""
APRIORI ALGORITHM IMPLEMENTATION
================================
"""

from mlxtend.frequent_patterns import apriori, association_rules

# Using our transaction dataframe
# df from previous cell

# Step 1: Find frequent itemsets
min_support = 0.3  # 30% minimum support

frequent_itemsets = apriori(
    df, 
    min_support=min_support, 
    use_colnames=True
)

print("=" * 60)
print("FREQUENT ITEMSETS (min_support = 30%)")
print("=" * 60)
print(frequent_itemsets.sort_values('support', ascending=False))

"""
OUTPUT:
          support             itemsets
0         0.80               (Bread)
1         0.60                (Milk)
2         0.40              (Butter)
3         0.40                (Beer)
4         0.30             (Diapers)
5         0.50          (Bread, Milk)
6         0.40        (Bread, Butter)
7         0.40    (Butter, Milk)
8         0.30  (Bread, Butter, Milk)
"""

# Step 2: Generate association rules
rules = association_rules(
    frequent_itemsets, 
    metric="confidence", 
    min_threshold=0.6
)

# Sort by lift for most interesting rules
rules_sorted = rules.sort_values('lift', ascending=False)

print("\n" + "=" * 60)
print("ASSOCIATION RULES (min_confidence = 60%)")
print("=" * 60)
print(rules_sorted[['antecedents', 'consequents', 
                     'support', 'confidence', 'lift']])

"""
OUTPUT:
            antecedents    consequents  support  confidence     lift
0           (Butter)        (Bread)      0.4       1.00      1.25
1           (Butter)         (Milk)      0.4       1.00      1.67
2   (Butter, Milk)        (Bread)      0.3       0.75      0.94
3           (Bread)        (Butter)      0.4       0.50      1.25
...
"""
🚀 FP-Growth Implementation
Python

"""
FP-GROWTH ALGORITHM IMPLEMENTATION
==================================
"""

from mlxtend.frequent_patterns import fpgrowth

# FP-Growth is faster than Apriori!
frequent_itemsets_fp = fpgrowth(
    df, 
    min_support=0.3, 
    use_colnames=True
)

print("=" * 60)
print("FP-GROWTH FREQUENT ITEMSETS")
print("=" * 60)
print(frequent_itemsets_fp)

# Generate rules (same function works for both algorithms)
rules_fp = association_rules(
    frequent_itemsets_fp,
    metric="lift", 
    min_threshold=1.0  # Only rules with lift > 1
)

print("\n" + "=" * 60)
print("ASSOCIATION RULES FROM FP-GROWTH (Lift > 1)")
print("=" * 60)
print(rules_fp[['antecedents', 'consequents', 
                'support', 'confidence', 'lift']])
📈 Complete Analysis Pipeline
Python

"""
COMPLETE ASSOCIATION RULE MINING PIPELINE
==========================================
"""

import pandas as pd
import numpy as np
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, fpgrowth, association_rules
import matplotlib.pyplot as plt

class AssociationRuleMiner:
    """
    A complete class for association rule mining
    """
    
    def __init__(self, transactions):
        """Initialize with transaction data"""
        self.transactions = transactions
        self.df = None
        self.frequent_itemsets = None
        self.rules = None
        self._prepare_data()
    
    def _prepare_data(self):
        """Convert transactions to binary matrix"""
        te = TransactionEncoder()
        te_array = te.fit(self.transactions).transform(self.transactions)
        self.df = pd.DataFrame(te_array, columns=te.columns_)
        print(f"✓ Prepared {len(self.df)} transactions with {len(self.df.columns)} unique items")
    
    def find_frequent_itemsets(self, min_support=0.1, algorithm='fpgrowth'):
        """Find frequent itemsets using specified algorithm"""
        print(f"\nFinding frequent itemsets with min_support={min_support}...")
        
        if algorithm == 'apriori':
            self.frequent_itemsets = apriori(
                self.df, 
                min_support=min_support, 
                use_colnames=True
            )
        elif algorithm == 'fpgrowth':
            self.frequent_itemsets = fpgrowth(
                self.df, 
                min_support=min_support, 
                use_colnames=True
            )
        
        # Add itemset length
        self.frequent_itemsets['length'] = self.frequent_itemsets['itemsets'].apply(len)
        
        print(f"✓ Found {len(self.frequent_itemsets)} frequent itemsets")
        return self.frequent_itemsets
    
    def generate_rules(self, metric='confidence', min_threshold=0.5):
        """Generate association rules"""
        if self.frequent_itemsets is None:
            raise ValueError("Run find_frequent_itemsets() first!")
        
        print(f"\nGenerating rules with {metric} >= {min_threshold}...")
        
        self.rules = association_rules(
            self.frequent_itemsets, 
            metric=metric, 
            min_threshold=min_threshold
        )
        
        # Round numeric columns for readability
        numeric_cols = ['support', 'confidence', 'lift', 'leverage', 'conviction']
        for col in numeric_cols:
            if col in self.rules.columns:
                self.rules[col] = self.rules[col].round(4)
        
        print(f"✓ Generated {len(self.rules)} rules")
        return self.rules
    
    def get_top_rules(self, n=10, sort_by='lift'):
        """Get top N rules sorted by specified metric"""
        if self.rules is None:
            raise ValueError("Run generate_rules() first!")
        
        return self.rules.nlargest(n, sort_by)[
            ['antecedents', 'consequents', 'support', 'confidence', 'lift']
        ]
    
    def filter_rules(self, min_support=None, min_confidence=None, 
                     min_lift=None, contains_item=None):
        """Filter rules by multiple criteria"""
        if self.rules is None:
            raise ValueError("Run generate_rules() first!")
        
        filtered = self.rules.copy()
        
        if min_support:
            filtered = filtered[filtered['support'] >= min_support]
        if min_confidence:
            filtered = filtered[filtered['confidence'] >= min_confidence]
        if min_lift:
            filtered = filtered[filtered['lift'] >= min_lift]
        if contains_item:
            filtered = filtered[
                filtered['antecedents'].apply(lambda x: contains_item in x) |
                filtered['consequents'].apply(lambda x: contains_item in x)
            ]
        
        return filtered
    
    def get_rules_for_item(self, item, as_antecedent=True, as_consequent=True):
        """Get all rules containing a specific item"""
        if self.rules is None:
            raise ValueError("Run generate_rules() first!")
        
        results = []
        
        if as_antecedent:
            ant_rules = self.rules[
                self.rules['antecedents'].apply(lambda x: item in x)
            ]
            results.append(ant_rules)
        
        if as_consequent:
            cons_rules = self.rules[
                self.rules['consequents'].apply(lambda x: item in x)
            ]
            results.append(cons_rules)
        
        return pd.concat(results).drop_duplicates()
    
    def summary_statistics(self):
        """Print summary statistics"""
        print("\n" + "=" * 60)
        print("SUMMARY STATISTICS")
        print("=" * 60)
        
        print(f"\nDataset:")
        print(f"  - Transactions: {len(self.df)}")
        print(f"  - Unique items: {len(self.df.columns)}")
        
        if self.frequent_itemsets is not None:
            print(f"\nFrequent Itemsets:")
            print(f"  - Total: {len(self.frequent_itemsets)}")
            for length in sorted(self.frequent_itemsets['length'].unique()):
                count = len(self.frequent_itemsets[self.frequent_itemsets['length'] == length])
                print(f"  - {length}-itemsets: {count}")
        
        if self.rules is not None:
            print(f"\nAssociation Rules:")
            print(f"  - Total rules: {len(self.rules)}")
            print(f"  - Avg support: {self.rules['support'].mean():.4f}")
            print(f"  - Avg confidence: {self.rules['confidence'].mean():.4f}")
            print(f"  - Avg lift: {self.rules['lift'].mean():.4f}")
            print(f"  - Max lift: {self.rules['lift'].max():.4f}")
    
    def plot_rules(self, x='support', y='confidence', size='lift'):
        """Visualize rules"""
        if self.rules is None or len(self.rules) == 0:
            print("No rules to plot!")
            return
        
        plt.figure(figsize=(10, 6))
        scatter = plt.scatter(
            self.rules[x], 
            self.rules[y], 
            c=self.rules[size], 
            s=self.rules[size] * 50,
            alpha=0.6,
            cmap='viridis'
        )
        plt.colorbar(scatter, label=size.capitalize())
        plt.xlabel(x.capitalize())
        plt.ylabel(y.capitalize())
        plt.title('Association Rules Visualization')
        plt.tight_layout()
        plt.show()


# USAGE EXAMPLE
# =============

# Sample retail transactions
retail_transactions = [
    ['Bread', 'Milk', 'Eggs'],
    ['Bread', 'Butter', 'Milk'],
    ['Bread', 'Butter'],
    ['Beer', 'Diapers', 'Bread'],
    ['Beer', 'Diapers', 'Milk'],
    ['Bread', 'Milk', 'Butter', 'Eggs'],
    ['Bread', 'Milk', 'Butter'],
    ['Beer', 'Bread'],
    ['Bread', 'Milk'],
    ['Beer', 'Diapers'],
    ['Bread', 'Milk', 'Eggs', 'Butter'],
    ['Beer', 'Diapers', 'Bread', 'Milk'],
    ['Bread', 'Butter', 'Eggs'],
    ['Milk', 'Butter'],
    ['Beer', 'Bread', 'Milk']
]

# Initialize miner
miner = AssociationRuleMiner(retail_transactions)

# Find frequent itemsets
frequent = miner.find_frequent_itemsets(min_support=0.2, algorithm='fpgrowth')
print("\nFrequent Itemsets:")
print(frequent.sort_values('support', ascending=False).head(10))

# Generate rules
rules = miner.generate_rules(metric='confidence', min_threshold=0.5)

# Get top rules
print("\nTop 10 Rules by Lift:")
print(miner.get_top_rules(n=10, sort_by='lift'))

# Filter rules
print("\nStrong Rules (support≥0.2, confidence≥0.7, lift≥1.2):")
strong_rules = miner.filter_rules(
    min_support=0.2, 
    min_confidence=0.7, 
    min_lift=1.2
)
print(strong_rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])

# Rules for specific item
print("\nAll rules involving 'Bread':")
bread_rules = miner.get_rules_for_item('Bread')
print(bread_rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']].head())

# Summary
miner.summary_statistics()

# Visualize (uncomment to show plot)
# miner.plot_rules()
🔢 Custom Metrics Implementation
Python

"""
CUSTOM METRICS IMPLEMENTATION
=============================
"""

def calculate_all_metrics(rules_df):
    """
    Calculate additional interestingness measures
    """
    rules = rules_df.copy()
    
    # Jaccard coefficient
    # Jaccard = support(X∪Y) / (support(X) + support(Y) - support(X∪Y))
    rules['jaccard'] = rules['support'] / (
        rules['antecedent support'] + rules['consequent support'] - rules['support']
    )
    
    # Cosine similarity
    # Cosine = support(X∪Y) / sqrt(support(X) * support(Y))
    rules['cosine'] = rules['support'] / np.sqrt(
        rules['antecedent support'] * rules['consequent support']
    )
    
    # Kulczynski measure
    # Kulc = 0.5 * (confidence(X→Y) + confidence(Y→X))
    rules['kulczynski'] = 0.5 * (
        rules['confidence'] + 
        rules['support'] / rules['consequent support']
    )
    
    # Imbalance Ratio
    rules['imbalance_ratio'] = abs(
        rules['antecedent support'] - rules['consequent support']
    ) / (
        rules['antecedent support'] + rules['consequent support'] - rules['support']
    )
    
    # Certainty Factor
    # CF = (confidence - consequent_support) / (1 - consequent_support)
    rules['certainty_factor'] = (
        rules['confidence'] - rules['consequent support']
    ) / (1 - rules['consequent support'])
    
    # Added Value (AV)
    # AV = confidence - consequent_support
    rules['added_value'] = rules['confidence'] - rules['consequent support']
    
    # Round all new metrics
    new_metrics = ['jaccard', 'cosine', 'kulczynski', 'imbalance_ratio', 
                   'certainty_factor', 'added_value']
    for metric in new_metrics:
        rules[metric] = rules[metric].round(4)
    
    return rules


# Example usage
# First generate rules with full output
full_rules = association_rules(
    frequent_itemsets, 
    metric="support", 
    min_threshold=0.2
)

# Add custom metrics
enhanced_rules = calculate_all_metrics(full_rules)

print("Enhanced Rules with All Metrics:")
print(enhanced_rules[['antecedents', 'consequents', 'support', 'confidence', 
                       'lift', 'jaccard', 'cosine', 'kulczynski']].head(10))
📊 Visualization Functions
Python

"""
VISUALIZATION FUNCTIONS
=======================
"""

import matplotlib.pyplot as plt
import seaborn as sns
import networkx as nx

def plot_support_distribution(frequent_itemsets):
    """Plot distribution of support values"""
    plt.figure(figsize=(10, 5))
    
    plt.subplot(1, 2, 1)
    plt.hist(frequent_itemsets['support'], bins=20, edgecolor='black', alpha=0.7)
    plt.xlabel('Support')
    plt.ylabel('Frequency')
    plt.title('Distribution of Support Values')
    
    plt.subplot(1, 2, 2)
    length_counts = frequent_itemsets['length'].value_counts().sort_index()
    plt.bar(length_counts.index, length_counts.values, edgecolor='black', alpha=0.7)
    plt.xlabel('Itemset Size')
    plt.ylabel('Count')
    plt.title('Itemset Size Distribution')
    
    plt.tight_layout()
    plt.show()


def plot_rules_heatmap(rules, top_n=20):
    """Create heatmap of rule metrics"""
    if len(rules) == 0:
        print("No rules to visualize!")
        return
    
    # Select top rules by lift
    top_rules = rules.nlargest(top_n, 'lift').copy()
    
    # Create rule labels
    top_rules['rule'] = top_rules.apply(
        lambda x: f"{set(x['antecedents'])} → {set(x['consequents'])}", 
        axis=1
    )
    
    # Select metrics for heatmap
    metrics = ['support', 'confidence', 'lift', 'leverage']
    available_metrics = [m for m in metrics if m in top_rules.columns]
    
    # Create matrix
    matrix = top_rules.set_index('rule')[available_metrics]
    
    # Normalize for visualization
    matrix_normalized = (matrix - matrix.min()) / (matrix.max() - matrix.min())
    
    plt.figure(figsize=(10, max(6, len(top_rules) * 0.4)))
    sns.heatmap(matrix_normalized, annot=matrix.round(3), 
                cmap='YlOrRd', fmt='', linewidths=0.5)
    plt.title(f'Top {top_n} Association Rules by Lift')
    plt.tight_layout()
    plt.show()


def plot_rules_network(rules, top_n=15, min_lift=1.0):
    """Create network graph of association rules"""
    # Filter rules
    filtered = rules[rules['lift'] >= min_lift].nlargest(top_n, 'lift')
    
    if len(filtered) == 0:
        print("No rules to visualize!")
        return
    
    # Create graph
    G = nx.DiGraph()
    
    for _, row in filtered.iterrows():
        for ant in row['antecedents']:
            for cons in row['consequents']:
                G.add_edge(ant, cons, 
                          weight=row['lift'],
                          confidence=row['confidence'])
    
    # Layout
    pos = nx.spring_layout(G, k=2, iterations=50)
    
    # Edge weights for line width
    edge_weights = [G[u][v]['weight'] for u, v in G.edges()]
    
    plt.figure(figsize=(12, 8))
    
    # Draw nodes
    nx.draw_networkx_nodes(G, pos, node_color='lightblue', 
                           node_size=2000, alpha=0.9)
    
    # Draw edges
    nx.draw_networkx_edges(G, pos, edge_color='gray', 
                           width=[w/max(edge_weights)*3 for w in edge_weights],
                           alpha=0.6, arrows=True, 
                           arrowsize=20, connectionstyle="arc3,rad=0.1")
    
    # Draw labels
    nx.draw_networkx_labels(G, pos, font_size=10, font_weight='bold')
    
    plt.title(f'Association Rules Network (Top {top_n} by Lift)')
    plt.axis('off')
    plt.tight_layout()
    plt.show()


def plot_rules_scatter_3d(rules):
    """3D scatter plot of rules"""
    from mpl_toolkits.mplot3d import Axes3D
    
    fig = plt.figure(figsize=(10, 8))
    ax = fig.add_subplot(111, projection='3d')
    
    scatter = ax.scatter(
        rules['support'],
        rules['confidence'],
        rules['lift'],
        c=rules['lift'],
        cmap='plasma',
        s=50,
        alpha=0.6
    )
    
    ax.set_xlabel('Support')
    ax.set_ylabel('Confidence')
    ax.set_zlabel('Lift')
    ax.set_title('Association Rules in 3D Space')
    
    fig.colorbar(scatter, ax=ax, label='Lift', shrink=0.5)
    plt.tight_layout()
    plt.show()


# Usage examples:
# plot_support_distribution(frequent_itemsets)
# plot_rules_heatmap(rules, top_n=15)
# plot_rules_network(rules, top_n=20, min_lift=1.0)
# plot_rules_scatter_3d(rules)
🔄 Sequential Pattern Mining Implementation
Python

"""
SEQUENTIAL PATTERN MINING WITH PREFIXSPAN
==========================================
"""

# pip install prefixspan
from prefixspan import PrefixSpan

# Sequential database (each sublist is a sequence of events)
sequential_db = [
    [['a'], ['a', 'b', 'c'], ['a', 'c'], ['d'], ['c', 'f']],
    [['a', 'd'], ['c'], ['b', 'c'], ['a', 'e']],
    [['e', 'f'], ['a', 'b'], ['d', 'f'], ['c'], ['b']],
    [['e'], ['g'], ['a', 'b', 'f'], ['c'], ['b', 'c']]
]

# Initialize PrefixSpan
ps = PrefixSpan(sequential_db)

# Mine frequent sequential patterns
min_support = 2  # Absolute support

print("Frequent Sequential Patterns (min_support = 2):")
print("=" * 50)

# Get patterns with support count
patterns = ps.frequent(min_support)

for support, pattern in sorted(patterns, key=lambda x: -x[0]):
    print(f"Support: {support}, Pattern: {pattern}")

"""
OUTPUT:
Support: 4, Pattern: [['a']]
Support: 4, Pattern: [['b']]
Support: 4, Pattern: [['c']]
Support: 4, Pattern: [['a'], ['b']]
Support: 4, Pattern: [['a'], ['c']]
Support: 3, Pattern: [['a'], ['b'], ['c']]
...
"""

# Top-k patterns
print("\nTop 10 Sequential Patterns:")
top_patterns = ps.topk(10)
for support, pattern in top_patterns:
    print(f"Support: {support}, Pattern: {pattern}")


# Custom implementation of GSP (simplified)
def simple_gsp(sequences, min_support):
    """
    Simplified GSP implementation for educational purposes
    """
    from collections import defaultdict
    
    n_sequences = len(sequences)
    min_count = min_support if isinstance(min_support, int) else int(min_support * n_sequences)
    
    # Flatten to get all items
    all_items = set()
    for seq in sequences:
        for event in seq:
            all_items.update(event)
    
    # Find frequent 1-sequences
    item_counts = defaultdict(int)
    for seq in sequences:
        items_in_seq = set()
        for event in seq:
            items_in_seq.update(event)
        for item in items_in_seq:
            item_counts[item] += 1
    
    freq_1 = {item: count for item, count in item_counts.items() if count >= min_count}
    
    print(f"Frequent 1-sequences: {freq_1}")
    
    # Find frequent 2-sequences (simplified)
    pair_counts = defaultdict(int)
    for seq in sequences:
        # Get all items in order
        items_order = []
        for event in seq:
            items_order.extend(sorted(event))
        
        # Count pairs where first appears before second
        for i, item1 in enumerate(items_order):
            for item2 in items_order[i+1:]:
                if item1 in freq_1 and item2 in freq_1:
                    pair_counts[(item1, item2)] += 1
    
    freq_2 = {pair: count for pair, count in pair_counts.items() if count >= min_count}
    
    print(f"Frequent 2-sequences: {freq_2}")
    
    return {'1-seq': freq_1, '2-seq': freq_2}

# Test simple GSP
result = simple_gsp(sequential_db, min_support=2)
📝 Chapter 13 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 13: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ mlxtend library provides Apriori and FP-Growth         ║
║  ✓ TransactionEncoder converts lists to binary matrix     ║
║  ✓ association_rules() generates rules from itemsets      ║
║  ✓ Multiple metrics available: support, confidence, lift  ║
║  ✓ Custom metrics can be calculated easily                ║
║  ✓ Visualization helps interpret results                  ║
║  ✓ prefixspan library for sequential pattern mining       ║
╚═══════════════════════════════════════════════════════════╝
Chapter 14: Performance Optimization & Scalability {#chapter-14}
🎯 The Scalability Challenge
text

SCALABILITY CHALLENGES:
═══════════════════════

┌─────────────────────────────────────────────────────────────┐
│              WHY SCALING IS HARD                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📊 DATA VOLUME                                             │
│     - Millions of transactions                              │
│     - Thousands of unique items                             │
│     - 2^n possible itemsets                                 │
│                                                             │
│  ⏱️ TIME COMPLEXITY                                         │
│     - Multiple database scans                               │
│     - Exponential candidate generation                      │
│     - Support counting overhead                             │
│                                                             │
│  💾 MEMORY CONSTRAINTS                                      │
│     - Storing candidates                                    │
│     - Storing intermediate results                          │
│     - TID-sets for vertical methods                         │
│                                                             │
│  🔄 DYNAMIC DATA                                            │
│     - New transactions arriving                             │
│     - Incremental mining needed                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🔧 Optimization Techniques
Technique 1: Transaction Reduction
text

TRANSACTION REDUCTION:
══════════════════════

Idea: Remove transactions that cannot contribute 
      to future frequent itemsets

After finding L(k), a transaction that doesn't contain
any L(k) itemset is useless for L(k+1), L(k+2), ...

Example:
─────────
L₂ = {{A,B}, {A,C}, {B,C}}

Transaction T = {A, D, E}
- Contains no 2-itemset from L₂
- Remove T from further processing!

IMPLEMENTATION:
───────────────
def reduce_transactions(transactions, frequent_itemsets):
    """Remove transactions with no frequent itemsets"""
    reduced = []
    freq_items = set()
    for itemset in frequent_itemsets:
        freq_items.update(itemset)
    
    for trans in transactions:
        # Keep only if transaction has at least k frequent items
        if len(set(trans) & freq_items) >= k:
            reduced.append(trans)
    
    return reduced

# Can reduce database by 30-70% in later iterations!
Technique 2: Partitioning
text

PARTITION ALGORITHM:
════════════════════

Idea: Divide database into partitions, mine locally,
      then combine results

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  DATABASE D (N transactions)                                │
│  ┌─────────┬─────────┬─────────┬─────────┐                │
│  │ Part 1  │ Part 2  │ Part 3  │ Part 4  │                │
│  │ N/4     │ N/4     │ N/4     │ N/4     │                │
│  └────┬────┴────┬────┴────┬────┴────┬────┘                │
│       │         │         │         │                      │
│       ▼         ▼         ▼         ▼                      │
│     Local     Local     Local     Local                    │
│     Mining    Mining    Mining    Mining                   │
│       │         │         │         │                      │
│       └─────────┴────┬────┴─────────┘                      │
│                      │                                      │
│                      ▼                                      │
│              CANDIDATE ITEMSETS                             │
│              (Union of local frequent)                      │
│                      │                                      │
│                      ▼                                      │
│              Global Support Count                           │
│              (One full DB scan)                             │
│                      │                                      │
│                      ▼                                      │
│              GLOBAL FREQUENT ITEMSETS                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘

PROPERTY:
─────────
Any globally frequent itemset must be locally frequent 
in at least ONE partition.

BENEFIT:
────────
- Each partition fits in memory
- Can be parallelized
- Only 2 database scans total!
Technique 3: Sampling
text

SAMPLING APPROACH:
══════════════════

Idea: Mine a sample of the database, 
      verify on full database

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Full Database D                                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │   │
│  └─────────────────────────────────────────────────────┘   │
│                          │                                  │
│                    Random Sample                            │
│                    (1-10% of D)                             │
│                          │                                  │
│                          ▼                                  │
│  Sample S           ┌─────────┐                            │
│                     │ ░░░░░░░ │                            │
│                     └────┬────┘                            │
│                          │                                  │
│                  Mine with LOWER                            │
│                  min_support                                │
│                          │                                  │
│                          ▼                                  │
│              Candidate Frequent Itemsets                    │
│                          │                                  │
│                 Verify on Full D                            │
│                          │                                  │
│                          ▼                                  │
│              TRUE Frequent Itemsets                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘

FORMULA FOR ADJUSTED SUPPORT:
─────────────────────────────
sample_min_sup = min_sup - ε

Where ε depends on:
- Sample size
- Confidence level desired
- Margin of error acceptable


IMPLEMENTATION:
───────────────
import random

def sample_based_mining(transactions, min_support, sample_ratio=0.1):
    """
    Sample-based association rule mining
    """
    n = len(transactions)
    sample_size = int(n * sample_ratio)
    
    # Take random sample
    sample = random.sample(transactions, sample_size)
    
    # Use lower support threshold on sample
    # This catches itemsets that might be borderline
    epsilon = 0.1 * min_support  # 10% margin
    sample_support = min_support - epsilon
    
    # Mine sample
    sample_frequent = mine_frequent(sample, sample_support)
    
    # Verify on full database
    verified_frequent = verify_support(transactions, sample_frequent, min_support)
    
    return verified_frequent
Technique 4: Hashing (DHP - Direct Hashing and Pruning)
text

DHP ALGORITHM:
══════════════

Idea: Use hash table to eliminate candidates early

HASH FUNCTION:
──────────────
For itemset {A, B}: h(A,B) = (order(A)*10 + order(B)) mod bucket_size

Example with bucket_size = 7:
h(1,2) = (1*10 + 2) mod 7 = 12 mod 7 = 5
h(1,4) = (1*10 + 4) mod 7 = 14 mod 7 = 0


PROCESS:
────────

During L₁ generation:
┌──────────────────────────────────────────────────────────┐
│ For each transaction T = {A, B, C, D}:                   │
│   - Count items for L₁                                   │
│   - Hash all 2-item pairs to buckets                     │
│   - {A,B} → bucket 5, count++                           │
│   - {A,C} → bucket 2, count++                           │
│   - {A,D} → bucket 0, count++                           │
│   - {B,C} → bucket 6, count++                           │
│   - etc.                                                 │
└──────────────────────────────────────────────────────────┘

During C₂ generation:
┌──────────────────────────────────────────────────────────┐
│ For candidate {X, Y}:                                    │
│   - Compute h(X, Y) = bucket                            │
│   - If bucket_count < min_support:                      │
│       PRUNE! {X, Y} cannot be frequent                  │
└──────────────────────────────────────────────────────────┘

BENEFIT:
────────
Can eliminate 50-80% of candidates before counting!
Technique 5: Parallel and Distributed Mining
text

PARALLEL APPROACHES:
════════════════════

1. DATA PARALLELISM
───────────────────
Partition data across processors
Each processor mines its portion
Combine results

┌───────┐  ┌───────┐  ┌───────┐  ┌───────┐
│ CPU 1 │  │ CPU 2 │  │ CPU 3 │  │ CPU 4 │
│Data 1 │  │Data 2 │  │Data 3 │  │Data 4 │
└───┬───┘  └───┬───┘  └───┬───┘  └───┬───┘
    │          │          │          │
    └──────────┴────┬─────┴──────────┘
                    │
              COMBINE RESULTS


2. CANDIDATE PARALLELISM
────────────────────────
Distribute candidates across processors
Each processor counts its candidates
All access same data (shared memory)

┌─────────────────────────────────┐
│         SHARED DATABASE         │
└─────────────────────────────────┘
        ▲      ▲      ▲      ▲
        │      │      │      │
┌───────┴┐ ┌───┴───┐ ┌┴──────┐ ┌┴──────┐
│ CPU 1  │ │ CPU 2 │ │ CPU 3 │ │ CPU 4 │
│Cand 1-K│ │K+1-2K │ │2K+1-3K│ │3K+1-4K│
└────────┘ └───────┘ └───────┘ └───────┘


3. TASK PARALLELISM (FP-Growth)
───────────────────────────────
Different conditional FP-trees mined in parallel

    FP-Tree
    /  |  \  \
   A   B   C   D  (conditional trees)
   │   │   │   │
  CPU1 CPU2 CPU3 CPU4
🚀 MapReduce for Association Rules
text

MAPREDUCE IMPLEMENTATION:
═════════════════════════

PHASE 1: Parallel Counting (Finding L₁)
────────────────────────────────────────

MAP (for each transaction T):
    for each item i in T:
        emit(i, 1)

REDUCE (for each item i):
    count = sum(all values)
    if count >= min_support:
        emit(i, count)


PHASE 2: Candidate Generation & Counting
─────────────────────────────────────────

MAP (for each transaction T):
    # Generate local candidates from L(k-1)
    candidates = generate_candidates(T, L_prev)
    for each candidate c in candidates:
        if c ⊆ T:
            emit(c, 1)

REDUCE (for each candidate c):
    count = sum(all values)
    if count >= min_support:
        emit(c, count)


SPARK IMPLEMENTATION:
─────────────────────
from pyspark.ml.fpm import FPGrowth

# Assuming df is a DataFrame with transactions
fpGrowth = FPGrowth(
    itemsCol="items",
    minSupport=0.1,
    minConfidence=0.5
)

model = fpGrowth.fit(df)

# Display frequent itemsets
model.freqItemsets.show()

# Display association rules
model.associationRules.show()
📊 Performance Comparison
text

┌────────────────────────────────────────────────────────────────┐
│            ALGORITHM PERFORMANCE COMPARISON                     │
├──────────────┬──────────┬───────────┬────────────┬─────────────┤
│  Algorithm   │ DB Scans │ Memory    │ Speed      │ Best For    │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ Apriori      │ Multiple │ Moderate  │ Slow       │ Small data  │
│              │ (k+1)    │           │            │ sparse      │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ AprioriTID   │ 1 (+mem) │ High      │ Medium     │ Small data  │
│              │          │           │            │             │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ DHP          │ Multiple │ Moderate  │ Faster     │ Medium data │
│              │ (fewer)  │ (+hash)   │            │             │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ Partition    │ 2        │ Low       │ Fast       │ Large data  │
│              │          │ (per part)│            │ parallel    │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ Sampling     │ 1-2      │ Very Low  │ Very Fast  │ Very large  │
│              │          │           │ (approx)   │ data        │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ FP-Growth    │ 2        │ Moderate  │ Fast       │ Dense data  │
│              │          │ (FP-tree) │            │ low support │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ ECLAT        │ 1        │ High      │ Fast       │ Medium data │
│              │          │ (TID-sets)│            │ sparse      │
├──────────────┼──────────┼───────────┼────────────┼─────────────┤
│ Spark FP     │ 2        │ Distrib.  │ Scalable   │ Big data    │
│ (distributed)│          │           │            │ clusters    │
└──────────────┴──────────┴───────────┴────────────┴─────────────┘
💡 Practical Optimization Tips
text

OPTIMIZATION CHECKLIST:
═══════════════════════

□ DATA PREPROCESSING
  ├─ Remove very rare items (support < 0.1%)
  ├─ Remove very frequent items (support > 99%)
  ├─ Encode items as integers (faster comparison)
  └─ Sort transactions by length

□ PARAMETER TUNING
  ├─ Start with higher min_support, lower gradually
  ├─ Use relative support for varying item frequencies
  └─ Set max itemset length if domain allows

□ ALGORITHM SELECTION
  ├─ Sparse data → Apriori or ECLAT
  ├─ Dense data → FP-Growth
  ├─ Very large data → Partition/Sampling/Spark
  └─ Real-time → Pre-computed rules

□ MEMORY MANAGEMENT
  ├─ Use generators instead of lists
  ├─ Process in batches
  ├─ Use memory-mapped files for large datasets
  └─ Clear intermediate results

□ RESULT FILTERING
  ├─ Filter by lift > 1 (eliminate noise)
  ├─ Set maximum rule length
  ├─ Use domain-specific constraints
  └─ Remove redundant rules


PYTHON OPTIMIZATION EXAMPLE:
────────────────────────────

# Bad: Storing all candidates in memory
candidates = [generate_candidate(i,j) for i in L for j in L]

# Good: Using generator
def candidate_generator(L):
    for i in L:
        for j in L:
            yield generate_candidate(i, j)

# Process in chunks
for candidate in candidate_generator(L):
    if is_valid(candidate):
        process(candidate)
📝 Chapter 14 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 14: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Transaction reduction removes useless transactions     ║
║  ✓ Partitioning enables parallel processing               ║
║  ✓ Sampling provides fast approximate results             ║
║  ✓ Hashing (DHP) prunes candidates early                  ║
║  ✓ Choose algorithm based on data characteristics         ║
║  ✓ Spark/MapReduce for truly big data                     ║
║  ✓ Preprocessing and filtering are critical               ║
╚═══════════════════════════════════════════════════════════╝
Chapter 15: Interview Questions & Answers {#chapter-15}
📚 Basic Level Questions
text

Q1: What is Association Rule Mining?
════════════════════════════════════

ANSWER:
Association Rule Mining is a data mining technique used to discover 
interesting relationships, patterns, correlations, or associations 
among items in large datasets.

Key Points:
• Originated from Market Basket Analysis
• Format: X → Y (If X then Y)
• X = Antecedent, Y = Consequent
• Measured by Support, Confidence, and Lift

Example:
{Bread, Butter} → {Milk}
"Customers who buy bread and butter often buy milk"
text

Q2: Explain Support, Confidence, and Lift.
══════════════════════════════════════════

ANSWER:

SUPPORT:
────────
• Measures frequency of itemset in database
• Formula: Support(X→Y) = P(X ∪ Y) = count(X,Y) / N
• Example: If {Bread,Milk} appears in 300 of 1000 transactions
  Support = 300/1000 = 30%

CONFIDENCE:
───────────
• Measures reliability of the rule
• Formula: Confidence(X→Y) = P(Y|X) = Support(X,Y) / Support(X)
• Example: Support({Bread,Milk})=30%, Support({Bread})=50%
  Confidence = 30%/50% = 60%
• Meaning: 60% of bread buyers also buy milk

LIFT:
─────
• Measures correlation strength
• Formula: Lift(X→Y) = Confidence(X→Y) / Support(Y)
• Interpretation:
  - Lift = 1: Independent (no correlation)
  - Lift > 1: Positive correlation
  - Lift < 1: Negative correlation
• Example: Confidence=60%, Support({Milk})=40%
  Lift = 60%/40% = 1.5 (positive correlation)
text

Q3: What is the Apriori Principle?
══════════════════════════════════

ANSWER:

"If an itemset is infrequent, all its supersets must also be infrequent."

Equivalently:
"All subsets of a frequent itemset must be frequent."

Example:
If {A, B} is infrequent:
- {A, B, C} must be infrequent
- {A, B, D} must be infrequent
- {A, B, C, D} must be infrequent

WHY IT MATTERS:
• Enables efficient pruning of search space
• Reduces number of candidates to check
• Foundation of Apriori algorithm
• Anti-monotone property
text

Q4: Describe the Apriori Algorithm.
═══════════════════════════════════

ANSWER:

Apriori is a level-wise algorithm for finding frequent itemsets.

STEPS:
1. Scan DB to find frequent 1-itemsets (L₁)
2. Generate candidate (k+1)-itemsets from Lₖ
3. Prune candidates with infrequent subsets
4. Scan DB to count candidate support
5. Keep candidates meeting min_support as Lₖ₊₁
6. Repeat until no new frequent itemsets

KEY OPERATIONS:
• Join: Combine k-itemsets to form (k+1)-itemsets
• Prune: Remove candidates with infrequent subsets

COMPLEXITY:
• Time: O(N × Σ|Cₖ|) - multiple DB scans
• Space: O(|Cₖ|) for candidates

LIMITATIONS:
• Multiple database scans
• Large number of candidates
• I/O intensive
text

Q5: What is FP-Growth and how does it differ from Apriori?
══════════════════════════════════════════════════════════

ANSWER:

FP-Growth (Frequent Pattern Growth) is a faster algorithm that 
uses a compressed data structure called FP-Tree.

DIFFERENCES:

┌────────────────┬──────────────────┬──────────────────────┐
│  Aspect        │     Apriori      │     FP-Growth        │
├────────────────┼──────────────────┼──────────────────────┤
│ DB Scans       │ Multiple (k+1)   │ Exactly 2            │
│ Candidates     │ Generated        │ None                 │
│ Data Structure │ None special     │ FP-Tree              │
│ Approach       │ Generate & Test  │ Pattern Growth       │
│ Memory         │ For candidates   │ For FP-Tree          │
│ Speed          │ Slower           │ 2-10x faster         │
└────────────────┴──────────────────┴──────────────────────┘

FP-GROWTH STEPS:
1. First scan: Count item frequencies
2. Build FP-Tree (second scan)
3. Mine patterns from FP-Tree using:
   - Conditional pattern bases
   - Conditional FP-Trees
   - Divide and conquer
📊 Intermediate Level Questions
text

Q6: Explain ECLAT Algorithm.
════════════════════════════

ANSWER:

ECLAT (Equivalence Class Clustering and bottom-up Lattice Traversal)
uses a VERTICAL database format with TID-sets.

VERTICAL FORMAT:
• Instead of Transaction → Items
• Uses Item → {Transaction IDs}

KEY INSIGHT:
Support(X ∪ Y) = |TID-set(X) ∩ TID-set(Y)|

EXAMPLE:
TID-set(Bread) = {T1, T2, T4, T5}
TID-set(Milk) = {T1, T3, T5}
TID-set(Bread, Milk) = {T1, T5}
Support = 2

ADVANTAGES:
• No database scans for counting
• Simple set intersection
• Depth-first search

DISADVANTAGES:
• High memory for TID-sets
• Not suitable for very large databases
text

Q7: What are Closed and Maximal Frequent Itemsets?
══════════════════════════════════════════════════

ANSWER:

CLOSED ITEMSET:
───────────────
An itemset X is closed if no superset has the same support.

Example:
{A}: support = 5
{A,B}: support = 5  ← {A} is NOT closed (superset has same support)
{A,B,C}: support = 3  ← {A,B} IS closed (no superset with support 5)

MAXIMAL ITEMSET:
────────────────
A frequent itemset X is maximal if no superset is frequent.

Example:
Frequent itemsets: {A}, {B}, {AB}, {AC}, {ABC}
{ABC} is maximal (no frequent superset)
{AB} is NOT maximal ({ABC} is frequent superset)

RELATIONSHIP:
Maximal ⊂ Closed ⊂ Frequent

WHY USEFUL:
• Closed: Lossless compression, can derive all supports
• Maximal: Lossy compression, minimal representation
text

Q8: How do you handle imbalanced item frequencies?
══════════════════════════════════════════════════

ANSWER:

PROBLEM: 
Common items (milk: 80%) vs rare items (caviar: 0.5%)
Single min_support either misses rare items or floods with trivial rules.

SOLUTIONS:

1. MULTIPLE MINIMUM SUPPORTS (MSApriori)
   • Assign different min_support to each item
   • MIS(item) = max(β × frequency(item), LS)
   • Example: MIS(milk)=24%, MIS(caviar)=0.5%

2. RELATIVE SUPPORT
   • Use confidence or lift instead of raw support
   • Relative_support = Support(X,Y) / Support(X)

3. AFFINITY MEASURE
   • Normalize by item frequencies
   • Affinity = Support(X,Y) / √(Support(X) × Support(Y))

4. STRATIFIED MINING
   • Mine different item groups separately
   • Combine results with appropriate thresholds
text

Q9: Explain constraint-based mining.
════════════════════════════════════

ANSWER:

CONCEPT:
Apply constraints to focus mining on relevant patterns.

CONSTRAINT TYPES:

1. ANTI-MONOTONE: If S violates, all supersets violate
   • Support ≥ threshold
   • Sum ≤ value
   • Count ≤ value
   → Use for PRUNING

2. MONOTONE: If S satisfies, all supersets satisfy
   • Sum ≥ value
   • Contains item X
   → Use for early termination

3. SUCCINCT: Can directly enumerate satisfying itemsets
   • Item ∈ set V
   • Min(S) ≤ value
   → Use for candidate generation

4. CONVERTIBLE: Becomes anti/monotone with ordering
   • Avg(S) ≥ value (order by descending value)
   → Use special ordering

PUSHING STRATEGY:
1. Apply succinct first (generate candidates)
2. Apply anti-monotone during mining (prune)
3. Apply convertible with ordering
4. Apply monotone at end (filter)
text

Q10: What is Sequential Pattern Mining?
════════════════════════════════════════

ANSWER:

DEFINITION:
Finding frequent subsequences in sequence databases where ORDER matters.

DIFFERENCE FROM ASSOCIATION RULES:
• Association: Items in same transaction (no order)
• Sequential: Events over time (ordered)

NOTATION:
<{A}, {B,C}, {D}>  = Event1 then Event2 then Event3

EXAMPLE:
Customer purchase history:
<{iPhone}, {Case}, {AirPods}>  (bought in this order)

ALGORITHMS:
1. GSP (Generalized Sequential Patterns)
   - Apriori-like approach
   - Level-wise candidate generation

2. PrefixSpan
   - Pattern-growth approach
   - No candidate generation
   - Uses projected databases

APPLICATIONS:
• Web clickstream analysis
• Customer purchase sequences
• DNA sequence analysis
• Medical treatment patterns
🎯 Advanced Level Questions
text

Q11: How would you handle incremental mining?
═════════════════════════════════════════════

ANSWER:

PROBLEM:
New transactions arrive continuously. Re-mining entire database is expensive.

SOLUTION: FUP (Fast Update) Algorithm

CONCEPT:
Itemsets fall into categories when new data arrives:

┌──────────────┬──────────────────────────────────────────────┐
│   Category   │   Description                                │
├──────────────┼──────────────────────────────────────────────┤
│ Winner       │ Infrequent → Frequent (gained support)       │
│ Loser        │ Frequent → Infrequent (lost support)         │
│ Stable       │ Remained frequent or infrequent              │
└──────────────┴──────────────────────────────────────────────┘

FUP APPROACH:
1. For new transactions (increment db):
   - Scan increment only for existing frequent itemsets
   - Update support counts
   
2. For losers:
   - Scan original DB to verify loss
   - Remove from frequent set if confirmed
   
3. For winners:
   - Scan original DB to verify gain
   - Add to frequent set if confirmed
   
4. Generate new candidates only from changed itemsets

BENEFIT:
Typically only 5-20% of work compared to full re-mining
text

Q12: Explain how to mine negative association rules.
════════════════════════════════════════════════════

ANSWER:

NEGATIVE RULES:
• A → ¬B (If A then NOT B)
• ¬A → B (If NOT A then B)

COMPUTATION:
Support(A ∧ ¬B) = Support(A) - Support(A ∧ B)
Confidence(A → ¬B) = Support(A ∧ ¬B) / Support(A)

INTERESTINGNESS CHECK:
Rule A → ¬B is interesting if:

1. Support(A ∧ B) << Expected
   Expected = Support(A) × Support(B)
   If actual << expected → negative correlation exists

2. Use correlation coefficient (φ):
   φ = [P(AB) - P(A)P(B)] / √[P(A)P(B)P(¬A)P(¬B)]
   φ < 0 indicates negative association

EXAMPLE:
{Laptop} → ¬{Desktop}
• People buying laptops rarely buy desktops
• Useful for understanding substitutes

CHALLENGES:
• Many trivial negative rules
• Need domain knowledge to filter
• Computationally expensive (¬A has high support)
text

Q13: How do you evaluate association rules in production?
═════════════════════════════════════════════════════════

ANSWER:

EVALUATION FRAMEWORK:

1. STATISTICAL SIGNIFICANCE
   • Chi-square test
   • Fisher's exact test
   • Is the pattern real or by chance?

2. BUSINESS METRICS
   • Revenue impact
   • Customer conversion
   • Cross-sell success rate

3. A/B TESTING
   • Test recommendations in real environment
   • Measure actual lift in sales
   • Compare control vs treatment groups

4. COVERAGE ANALYSIS
   • What % of transactions does rule cover?
   • Are we missing important segments?

5. RULE QUALITY METRICS
   • Lift (> 1.5 often considered strong)
   • Conviction (> 1.2 is meaningful)
   • Kulczynski (symmetric measure)

6. REDUNDANCY CHECK
   • Remove rules subsumed by others
   • Keep most specific actionable rules

MONITORING IN PRODUCTION:
• Track rule validity over time
• Support/confidence drift detection
• Automatic retraining triggers
text

Q14: Design a real-time recommendation system using association rules.
══════════════════════════════════════════════════════════════════════

ANSWER:

ARCHITECTURE:

┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────────┐ │
│  │   OFFLINE    │    │    CACHE     │    │      ONLINE         │ │
│  │   MINING     │    │   (Redis)    │    │      SERVING        │ │
│  │              │    │              │    │                     │ │
│  │ Daily batch  │───▶│ Rules index  │───▶│ Real-time lookup   │ │
│  │ FP-Growth    │    │ Item→Rules   │    │ User cart → Rules  │ │
│  │              │    │              │    │                     │ │
│  └──────────────┘    └──────────────┘    └──────────────────────┘ │
│         ▲                                          │               │
│         │                                          ▼               │
│  ┌──────────────┐                        ┌──────────────────────┐ │
│  │  Transaction │                        │   RECOMMENDATION     │ │
│  │   Database   │                        │      ENGINE          │ │
│  │              │                        │                      │ │
│  │  Historical  │                        │ Filter by inventory  │ │
│  │  + Streaming │                        │ Rank by lift/profit  │ │
│  │              │                        │ Personalize          │ │
│  └──────────────┘                        └──────────────────────┘ │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘

IMPLEMENTATION:

1. OFFLINE COMPONENT:
   • Daily batch mining with FP-Growth
   • Generate rules with lift > 1.2
   • Pre-compute item→rules mapping

2. CACHE LAYER (Redis):
   • Key: item_id
   • Value: [{consequent, confidence, lift, profit}]
   • TTL: 24 hours (refresh daily)

3. ONLINE SERVING:
   def get_recommendations(cart_items, n=5):
       all_rules = []
       for item in cart_items:
           rules = redis.get(f"rules:{item}")
           all_rules.extend(rules)
       
       # Filter already in cart
       filtered = [r for r in all_rules 
                   if r.consequent not in cart_items]
       
       # Score and rank
       scored = [(r, r.lift * r.profit * in_stock(r))
                 for r in filtered]
       
       return sorted(scored, key=lambda x: -x[1])[:n]

4. FEEDBACK LOOP:
   • Log recommendations shown
   • Log click-through and purchase
   • Compute actual lift
   • Retrain if performance drops
text

Q15: Compare Association Rules with Collaborative Filtering.
════════════════════════════════════════════════════════════

ANSWER:

┌─────────────────┬──────────────────────┬──────────────────────────┐
│    Aspect       │ Association Rules    │ Collaborative Filtering  │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Input Data      │ Transaction records  │ User-item ratings/       │
│                 │ (items only)         │ interactions             │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ User Model      │ None (item-based)    │ User preferences         │
│                 │                      │ modeled explicitly       │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Personalization │ Same for all users   │ Personalized per user    │
│                 │ (within session)     │                          │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Cold Start      │ Works for new users  │ User cold start problem  │
│                 │ Item cold start issue│ Both cold start issues   │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Interpretability│ High (explicit rules)│ Lower (latent factors)   │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Computation     │ Offline mining,      │ Can be expensive         │
│                 │ fast serving         │ for large matrices       │
├─────────────────┼──────────────────────┼──────────────────────────┤
│ Best For        │ Cross-selling,       │ Long-term personalized   │
│                 │ session-based reco   │ recommendations          │
└─────────────────┴──────────────────────┴──────────────────────────┘

WHEN TO USE WHAT:

ASSOCIATION RULES:
• "Customers who bought X also bought Y"
• In-session recommendations
• Anonymous users
• Explainable recommendations required
• Retail, e-commerce checkout

COLLABORATIVE FILTERING:
• "Users like you also liked"
• Long-term user preferences
• Known users with history
• Content platforms (Netflix, Spotify)
• Higher accuracy when user data available

HYBRID APPROACH:
• Use association rules for cold-start/anonymous
• Use CF for logged-in users with history
• Combine scores: Score = α × AR_score + (1-α) × CF_score
📝 Quick Reference: Interview Cheat Sheet
text

╔═══════════════════════════════════════════════════════════════════╗
║                 ASSOCIATION RULES CHEAT SHEET                     ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  FORMULAS:                                                        ║
║  ─────────                                                        ║
║  Support(X→Y) = P(X∪Y) = count(X,Y)/N                            ║
║  Confidence(X→Y) = P(Y|X) = Support(X,Y)/Support(X)              ║
║  Lift(X→Y) = Confidence/Support(Y) = P(X,Y)/(P(X)×P(Y))          ║
║  Conviction = (1-Supp(Y))/(1-Conf)                               ║
║  Leverage = Supp(X,Y) - Supp(X)×Supp(Y)                          ║
║                                                                   ║
║  ALGORITHMS:                                                      ║
║  ───────────                                                      ║
║  Apriori: Level-wise, multiple scans, candidate generation        ║
║  FP-Growth: 2 scans, FP-tree, no candidates, fastest              ║
║  ECLAT: Vertical format, TID-sets, set intersection               ║
║                                                                   ║
║  KEY PRINCIPLES:                                                  ║
║  ───────────────                                                  ║
║  Apriori: Infrequent subset → Infrequent superset                ║
║  Lift > 1: Positive correlation (USE THIS!)                       ║
║  Lift < 1: Negative correlation                                   ║
║  Lift = 1: Independent (IGNORE rule)                              ║
║                                                                   ║
║  CONSTRAINTS:                                                     ║
║  ────────────                                                     ║
║  Anti-monotone: Support≥min (enables pruning)                     ║
║  Monotone: Contains item X (no re-check needed)                   ║
║  Succinct: Can enumerate directly                                 ║
║  Convertible: Avg≥v (with ordering)                               ║
║                                                                   ║
║  REMEMBER:                                                        ║
║  ─────────                                                        ║
║  • High confidence ≠ meaningful (check lift!)                     ║
║  • Use multiple metrics for evaluation                            ║
║  • Domain knowledge is essential                                  ║
║  • FP-Growth for most practical applications                      ║
║  • Consider scalability from the start                            ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
📝 Chapter 15 Summary Box
text

╔═══════════════════════════════════════════════════════════╗
║  CHAPTER 15: KEY TAKEAWAYS                                ║
╠═══════════════════════════════════════════════════════════╣
║  ✓ Know formulas: Support, Confidence, Lift               ║
║  ✓ Understand Apriori principle and why it works          ║
║  ✓ Compare algorithms: Apriori vs FP-Growth vs ECLAT      ║
║  ✓ Explain closed vs maximal itemsets                     ║
║  ✓ Handle real-world issues: imbalance, scalability       ║
║  ✓ Design production systems: caching, real-time          ║
║  ✓ Know when to use AR vs Collaborative Filtering         ║
╚═══════════════════════════════════════════════════════════╝
🎓 Final Summary: The Complete Journey
text

╔═══════════════════════════════════════════════════════════════════╗
║            ASSOCIATION RULES: COMPLETE GUIDE SUMMARY              ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  CHAPTER 1-3: FOUNDATIONS                                         ║
║  ├─ What is association rule mining                               ║
║  ├─ Key terminology (itemsets, transactions, rules)               ║
║  └─ Core metrics (Support, Confidence, Lift)                      ║
║                                                                   ║
║  CHAPTER 4-6: ALGORITHMS                                          ║
║  ├─ Apriori (level-wise, candidate generation)                    ║
║  ├─ FP-Growth (tree-based, pattern growth)                        ║
║  └─ ECLAT (vertical format, TID-sets)                             ║
║                                                                   ║
║  CHAPTER 7-11: ADVANCED TOPICS                                    ║
║  ├─ Additional metrics (Conviction, Leverage, etc.)               ║
║  ├─ Multi-level mining (concept hierarchies)                      ║
║  ├─ Sequential patterns (order matters)                           ║
║  ├─ Constraint-based mining (focused discovery)                   ║
║  └─ Rare & negative rules (special patterns)                      ║
║                                                                   ║
║  CHAPTER 12-15: PRACTICAL APPLICATION                             ║
║  ├─ Real-world applications (retail, web, healthcare)             ║
║  ├─ Python implementation (mlxtend, custom code)                  ║
║  ├─ Performance optimization (scaling techniques)                 ║
║  └─ Interview preparation (Q&A, cheat sheets)                     ║
║                                                                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  🎯 KEY TAKEAWAY:                                                 ║
║  Association rules are powerful for discovering hidden patterns.  ║
║  Success requires understanding algorithms, metrics, constraints, ║
║  AND domain knowledge to interpret results meaningfully.          ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
🎉 Congratulations! You've completed the comprehensive guide to Association Rules - from zero to hero!

This guide covered:

✅ Theoretical foundations
✅ Core algorithms with worked examples
✅ Advanced techniques
✅ Real-world applications
✅ Python implementations
✅ Performance optimization
✅ Interview preparation
Good luck with your data mining journey! 🚀 