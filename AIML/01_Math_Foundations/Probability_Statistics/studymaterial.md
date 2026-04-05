📊 Probability & Statistics for AI/ML - Complete Mastery Guide
From Zero to Hero: Everything you need to know about Probability & Statistics for Artificial Intelligence & Machine Learning

📑 Table of Contents
Why Probability & Statistics for AI/ML?
Prerequisites
Chapter 1: Foundations of Probability
Chapter 2: Conditional Probability & Bayes' Theorem
Chapter 3: Random Variables
Chapter 4: Common Probability Distributions
Chapter 5: Joint, Marginal & Conditional Distributions
Chapter 6: Expectation, Variance & Moments
Chapter 7: Covariance, Correlation & Independence
Chapter 8: Information Theory
Chapter 9: Descriptive Statistics
Chapter 10: Inferential Statistics
Chapter 11: Hypothesis Testing
Chapter 12: Maximum Likelihood Estimation
Chapter 13: Bayesian Statistics
Chapter 14: Sampling Methods
Chapter 15: Probability in Machine Learning
Chapter 16: Advanced Topics
Practice Problems
Cheat Sheet
Resources
1. Why Probability & Statistics for AI/ML?
🎯 The Big Picture
Machine Learning IS Applied Probability & Statistics!

Almost every concept in ML has a probabilistic interpretation. Understanding probability transforms ML from "black magic" into principled science.

text

┌─────────────────────────────────────────────────────────────────┐
│         PROBABILITY & STATISTICS IN ML                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   🎲 PROBABILISTIC FOUNDATIONS                                  │
│                                                                 │
│   Classification:                                               │
│   └── P(class | features) - What's probability of each class?  │
│                                                                 │
│   Regression:                                                   │
│   └── P(y | x) ~ N(f(x), σ²) - Predict distribution, not point│
│                                                                 │
│   Clustering:                                                   │
│   └── P(cluster | data) - Soft assignments via probability     │
│                                                                 │
│   Neural Networks:                                              │
│   └── Softmax outputs ARE probabilities                        │
│   └── Dropout IS random sampling                               │
│   └── Loss functions ARE negative log-likelihoods              │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   📈 STATISTICAL FOUNDATIONS                                    │
│                                                                 │
│   Model Training:                                               │
│   └── Maximum Likelihood Estimation                            │
│   └── Bayesian Inference                                       │
│                                                                 │
│   Model Evaluation:                                             │
│   └── Confidence intervals                                     │
│   └── Statistical significance tests                           │
│   └── Cross-validation (sampling theory)                       │
│                                                                 │
│   Feature Engineering:                                          │
│   └── Correlation analysis                                     │
│   └── Distribution analysis                                    │
│   └── Outlier detection                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
🔥 Specific ML Connections
text

┌─────────────────────────────────────────────────────────────────┐
│            PROBABILITY/STATS → ML ALGORITHM                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Concept                    ML Application                     │
│   ─────────────────────────────────────────────────────────     │
│   Bayes' Theorem         →   Naive Bayes, Bayesian Networks    │
│   Maximum Likelihood     →   Logistic Regression, Neural Nets  │
│   Gaussian Distribution  →   Linear Regression, GMM, VAE       │
│   Bernoulli Distribution →   Binary Classification             │
│   Categorical Dist.      →   Multi-class Classification        │
│   Entropy                →   Decision Trees, Cross-Entropy Loss│
│   KL Divergence          →   VAE loss, Knowledge Distillation  │
│   Covariance Matrix      →   PCA, Mahalanobis Distance         │
│   Hypothesis Testing     →   A/B Testing, Feature Selection    │
│   Confidence Intervals   →   Uncertainty Quantification        │
│   Sampling               →   MCMC, Monte Carlo Methods, Dropout│
│   Central Limit Theorem  →   Why Batch Normalization works     │
│   Law of Large Numbers   →   Why more data helps               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
🤔 Real-World Analogy
text

┌─────────────────────────────────────────────────────────────────┐
│              THE WEATHER FORECASTER ANALOGY                     │
│                                                                 │
│   Weather Forecaster = ML Model                                 │
│                                                                 │
│   "There's a 70% chance of rain tomorrow"                       │
│                                                                 │
│   This IS probability! The forecaster:                          │
│   • Observed historical DATA (training)                         │
│   • Built a MODEL of weather patterns                           │
│   • Makes PROBABILISTIC predictions                             │
│   • Gets evaluated on ACCURACY over time                        │
│                                                                 │
│   ML does the SAME thing:                                       │
│   • Observe data                                                │
│   • Learn patterns (probability distributions)                  │
│   • Make predictions with uncertainty                           │
│   • Evaluate with statistical metrics                           │
│                                                                 │
│   Key insight: ML doesn't give certainty,                       │
│                it quantifies UNCERTAINTY!                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
2. Prerequisites
Before diving in, make sure you understand:

text

✅ Basic arithmetic and algebra
✅ Set theory basics (union, intersection)
✅ Function notation f(x)
✅ Summation notation (Σ)
✅ Basic calculus (derivatives, integrals) - helpful but not required initially
3. Chapter 1: Foundations of Probability
📚 What is Probability?
Probability is a number between 0 and 1 that measures how likely an event is to occur.

text

┌─────────────────────────────────────────────────────────────────┐
│                    PROBABILITY BASICS                           │
│                                                                 │
│   0 ≤ P(A) ≤ 1                                                  │
│                                                                 │
│   P(A) = 0    →  Impossible event                              │
│   P(A) = 1    →  Certain event                                 │
│   P(A) = 0.5  →  50-50 chance                                  │
│                                                                 │
│   Probability Scale:                                            │
│                                                                 │
│   0%────25%────50%────75%────100%                              │
│   │      │      │      │      │                                │
│   ○──────●──────●──────●──────●                                │
│   │      │      │      │      │                                │
│   Never  Unlikely Equal Likely Always                           │
│                                                                 │
│   Examples:                                                     │
│   • P(fair coin = heads) = 0.5                                 │
│   • P(rolling 6 on fair die) = 1/6 ≈ 0.167                     │
│   • P(sun rises tomorrow) ≈ 1.0                                │
│   • P(spam | email has "FREE MONEY") ≈ 0.95                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Key Terminology
text

┌─────────────────────────────────────────────────────────────────┐
│                    PROBABILITY TERMINOLOGY                      │
│                                                                 │
│   EXPERIMENT (Random Experiment):                               │
│   A process with uncertain outcome                              │
│   Example: Flipping a coin, rolling a die, classifying an image│
│                                                                 │
│   SAMPLE SPACE (Ω or S):                                        │
│   Set of ALL possible outcomes                                  │
│   Example:                                                      │
│   • Coin flip: Ω = {Heads, Tails}                              │
│   • Die roll: Ω = {1, 2, 3, 4, 5, 6}                           │
│   • Classification: Ω = {Cat, Dog, Bird}                       │
│                                                                 │
│   EVENT (A, B, C, ...):                                         │
│   A subset of the sample space                                  │
│   Example:                                                      │
│   • "Rolling an even number" = {2, 4, 6}                       │
│   • "Getting heads" = {Heads}                                  │
│                                                                 │
│   OUTCOME:                                                      │
│   A single element of the sample space                          │
│   Example: Rolling a 3                                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Probability Axioms (Kolmogorov)
text

┌─────────────────────────────────────────────────────────────────┐
│              THE THREE AXIOMS OF PROBABILITY                    │
│                                                                 │
│   AXIOM 1: Non-negativity                                       │
│   ─────────────────────────                                     │
│   P(A) ≥ 0 for any event A                                     │
│   (Probabilities can't be negative)                            │
│                                                                 │
│   AXIOM 2: Normalization                                        │
│   ───────────────────────                                       │
│   P(Ω) = 1                                                      │
│   (Something in the sample space MUST happen)                  │
│                                                                 │
│   AXIOM 3: Additivity                                           │
│   ────────────────────                                          │
│   For mutually exclusive events A and B:                        │
│   P(A ∪ B) = P(A) + P(B)                                       │
│                                                                 │
│   (If A and B can't both happen,                               │
│    probability of either = sum of individual probabilities)    │
│                                                                 │
│   From these THREE axioms, ALL probability theory follows!     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Basic Probability Rules
text

┌─────────────────────────────────────────────────────────────────┐
│                    PROBABILITY RULES                            │
│                                                                 │
│   1. COMPLEMENT RULE                                            │
│   ───────────────────                                           │
│   P(not A) = P(Aᶜ) = 1 - P(A)                                  │
│                                                                 │
│   Example: P(not heads) = 1 - 0.5 = 0.5                        │
│                                                                 │
│   Visual:                                                       │
│   ┌──────────────────────┐                                     │
│   │ Sample Space Ω       │                                     │
│   │   ┌─────┐            │                                     │
│   │   │  A  │   Aᶜ       │                                     │
│   │   └─────┘            │                                     │
│   │  P(A)     1-P(A)     │                                     │
│   └──────────────────────┘                                     │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   2. ADDITION RULE (General)                                    │
│   ──────────────────────────                                    │
│   P(A ∪ B) = P(A) + P(B) - P(A ∩ B)                            │
│                                                                 │
│   Visual (Venn Diagram):                                        │
│   ┌──────────────────────────────┐                             │
│   │      ┌─────┬─────┐           │                             │
│   │      │  A  │  B  │           │                             │
│   │      │   ┌─┴─┐   │           │                             │
│   │      │   │A∩B│   │           │                             │
│   │      │   └─┬─┘   │           │                             │
│   │      └─────┴─────┘           │                             │
│   └──────────────────────────────┘                             │
│                                                                 │
│   Why subtract P(A∩B)? Avoid double-counting overlap!          │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   3. ADDITION RULE (Mutually Exclusive)                         │
│   ──────────────────────────────────────                        │
│   If A ∩ B = ∅ (can't both happen):                            │
│   P(A ∪ B) = P(A) + P(B)                                       │
│                                                                 │
│   Example: P(roll 1 OR roll 6) = 1/6 + 1/6 = 2/6 = 1/3        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Counting Methods
text

┌─────────────────────────────────────────────────────────────────┐
│                    COUNTING METHODS                             │
│                                                                 │
│   For equally likely outcomes:                                  │
│   P(A) = |A| / |Ω| = (favorable outcomes) / (total outcomes)   │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   MULTIPLICATION PRINCIPLE                                      │
│   ─────────────────────────                                     │
│   If task 1 has n₁ ways and task 2 has n₂ ways:               │
│   Total ways = n₁ × n₂                                         │
│                                                                 │
│   Example: 3 shirts × 4 pants = 12 outfits                     │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   PERMUTATIONS (order matters)                                  │
│   ─────────────────────────────                                 │
│   P(n, r) = n! / (n-r)!                                        │
│   "Arrange r items from n items"                               │
│                                                                 │
│   Example: How many ways to arrange 3 people in 5 chairs?      │
│   P(5, 3) = 5! / 2! = 120 / 2 = 60                            │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   COMBINATIONS (order doesn't matter)                           │
│   ─────────────────────────────────────                         │
│   C(n, r) = (n choose r) = n! / [r!(n-r)!]                     │
│   "Choose r items from n items"                                │
│                                                                 │
│   Example: How many ways to choose 3 people from 5?            │
│   C(5, 3) = 5! / (3! × 2!) = 120 / 12 = 10                    │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   FACTORIAL                                                     │
│   ──────────                                                    │
│   n! = n × (n-1) × (n-2) × ... × 2 × 1                        │
│   0! = 1 (by definition)                                       │
│                                                                 │
│   5! = 5 × 4 × 3 × 2 × 1 = 120                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np
from math import factorial, comb, perm

# Factorial
print(f"5! = {factorial(5)}")  # 120

# Permutations: P(5,3)
print(f"P(5,3) = {perm(5, 3)}")  # 60

# Combinations: C(5,3) or "5 choose 3"
print(f"C(5,3) = {comb(5, 3)}")  # 10

# Example: Probability of getting exactly 3 heads in 5 coin flips
n = 5  # total flips
k = 3  # heads wanted
p = 0.5  # probability of heads

# Number of ways to get exactly 3 heads
ways = comb(n, k)
# Probability
prob = ways * (p**k) * ((1-p)**(n-k))
print(f"\nP(exactly 3 heads in 5 flips) = {ways} × 0.5³ × 0.5² = {prob}")
# = 10 × 0.125 × 0.25 = 0.3125
4. Chapter 2: Conditional Probability & Bayes' Theorem
📚 Conditional Probability
Conditional probability is the probability of an event given that another event has occurred.

text

┌─────────────────────────────────────────────────────────────────┐
│                 CONDITIONAL PROBABILITY                         │
│                                                                 │
│   P(A | B) = P(A ∩ B) / P(B)                                   │
│                                                                 │
│   Read as: "Probability of A GIVEN B"                          │
│                                                                 │
│   Intuition:                                                    │
│   Given that B happened, what fraction of B also contains A?   │
│                                                                 │
│   Visual:                                                       │
│                                                                 │
│   Before knowing B:          After knowing B happened:          │
│   ┌──────────────────┐       ┌──────────────────┐              │
│   │    ┌───┬───┐     │       │      ┌───┐       │              │
│   │    │ A │A∩B│  B  │   →   │      │A∩B│  B    │              │
│   │    │   │   │     │       │      │   │       │              │
│   │    └───┴───┴─────│       │      └───┴───────│              │
│   │  Full sample space│       │  B is now our   │              │
│   └──────────────────┘       │  sample space!   │              │
│                              └──────────────────┘              │
│                                                                 │
│   P(A|B) = (A∩B overlap) / (entire B)                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Example: Medical Testing
text

┌─────────────────────────────────────────────────────────────────┐
│                 MEDICAL TEST EXAMPLE                            │
│                                                                 │
│   Scenario:                                                     │
│   • 1% of population has Disease X                             │
│   • Test is 99% accurate for positive (sensitivity)            │
│   • Test is 95% accurate for negative (specificity)            │
│                                                                 │
│   Question: If you test positive, what's P(Disease | Positive)?│
│                                                                 │
│   Let's define:                                                 │
│   D = has disease                                              │
│   + = tests positive                                           │
│                                                                 │
│   Given:                                                        │
│   P(D) = 0.01        (prevalence)                              │
│   P(+|D) = 0.99      (true positive rate / sensitivity)        │
│   P(-|Dᶜ) = 0.95     (true negative rate / specificity)        │
│   P(+|Dᶜ) = 0.05     (false positive rate)                     │
│                                                                 │
│   Population breakdown (per 10,000 people):                     │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │              │  Has Disease  │  No Disease  │   Total   │   │
│   │              │   (100)       │   (9,900)    │           │   │
│   ├──────────────┼───────────────┼──────────────┼───────────┤   │
│   │ Test +       │     99        │     495      │    594    │   │
│   │ Test -       │      1        │   9,405      │  9,406    │   │
│   └──────────────┴───────────────┴──────────────┴───────────┘   │
│                                                                 │
│   P(D | +) = 99 / 594 ≈ 0.167 = 16.7%                          │
│                                                                 │
│   SURPRISING! Even with 99% accurate test,                      │
│   only 17% chance you actually have the disease!               │
│   (Because the disease is rare)                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Bayes' Theorem ⭐⭐⭐
The most important formula in ML!

text

┌─────────────────────────────────────────────────────────────────┐
│                    BAYES' THEOREM                               │
│                                                                 │
│                     P(B|A) × P(A)                               │
│   P(A|B) = ─────────────────────────                            │
│                       P(B)                                      │
│                                                                 │
│   Or equivalently:                                              │
│                                                                 │
│                        P(B|A) × P(A)                            │
│   P(A|B) = ──────────────────────────────────────               │
│            P(B|A)×P(A) + P(B|Aᶜ)×P(Aᶜ)                         │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   TERMINOLOGY:                                                  │
│   ─────────────                                                 │
│   P(A|B) = POSTERIOR   (what we want to know)                  │
│   P(B|A) = LIKELIHOOD  (how likely is evidence given A)        │
│   P(A)   = PRIOR       (initial belief before evidence)        │
│   P(B)   = EVIDENCE    (normalizing constant)                  │
│                                                                 │
│   In words:                                                     │
│                                                                 │
│   POSTERIOR ∝ LIKELIHOOD × PRIOR                               │
│                                                                 │
│   "Update your beliefs based on evidence"                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Bayes' Theorem in ML
text

┌─────────────────────────────────────────────────────────────────┐
│                BAYES' THEOREM IN ML                             │
│                                                                 │
│   CLASSIFICATION:                                               │
│   ────────────────                                              │
│                     P(features | class) × P(class)              │
│   P(class|features) = ───────────────────────────────────       │
│                              P(features)                        │
│                                                                 │
│   Example: Spam Classification                                  │
│                                                                 │
│   P(spam | "FREE MONEY")                                        │
│                                                                 │
│        P("FREE MONEY" | spam) × P(spam)                         │
│   = ─────────────────────────────────────                       │
│              P("FREE MONEY")                                    │
│                                                                 │
│   • P(spam) = 0.3 (30% of emails are spam - PRIOR)             │
│   • P("FREE MONEY"|spam) = 0.8 (80% of spam has this phrase)   │
│   • P("FREE MONEY"|not spam) = 0.01 (1% of legitimate emails)  │
│                                                                 │
│   P("FREE MONEY") = 0.8×0.3 + 0.01×0.7 = 0.247                 │
│                                                                 │
│   P(spam|"FREE MONEY") = (0.8 × 0.3) / 0.247 = 0.97           │
│                                                                 │
│   → 97% likely spam!                                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np

def bayes_theorem(prior, likelihood, evidence):
    """
    Calculate posterior probability using Bayes' Theorem
    
    P(A|B) = P(B|A) * P(A) / P(B)
    """
    posterior = (likelihood * prior) / evidence
    return posterior

# Medical test example
p_disease = 0.01         # Prior: P(Disease)
p_positive_given_disease = 0.99  # Likelihood: P(+|D)
p_positive_given_healthy = 0.05  # P(+|Dᶜ)

# Calculate P(+) using law of total probability
p_positive = (p_positive_given_disease * p_disease + 
              p_positive_given_healthy * (1 - p_disease))

# Calculate P(Disease | +)
p_disease_given_positive = bayes_theorem(
    prior=p_disease,
    likelihood=p_positive_given_disease,
    evidence=p_positive
)

print("Medical Test Example:")
print(f"P(Disease) = {p_disease}")
print(f"P(+|Disease) = {p_positive_given_disease}")
print(f"P(+|Healthy) = {p_positive_given_healthy}")
print(f"P(+) = {p_positive:.4f}")
print(f"P(Disease | +) = {p_disease_given_positive:.4f}")
print(f"  → Only {p_disease_given_positive*100:.1f}% chance of disease despite positive test!")

# Spam classification example
print("\nSpam Classification Example:")
p_spam = 0.3
p_word_given_spam = 0.8
p_word_given_ham = 0.01

p_word = p_word_given_spam * p_spam + p_word_given_ham * (1 - p_spam)
p_spam_given_word = (p_word_given_spam * p_spam) / p_word

print(f"P(Spam | 'FREE MONEY') = {p_spam_given_word:.4f}")
print(f"  → {p_spam_given_word*100:.1f}% likely spam!")
📚 Chain Rule of Probability
text

┌─────────────────────────────────────────────────────────────────┐
│                    CHAIN RULE                                   │
│                                                                 │
│   P(A ∩ B) = P(A|B) × P(B) = P(B|A) × P(A)                     │
│                                                                 │
│   For multiple events:                                          │
│   P(A₁ ∩ A₂ ∩ ... ∩ Aₙ) =                                      │
│       P(A₁) × P(A₂|A₁) × P(A₃|A₁,A₂) × ... × P(Aₙ|A₁,...,Aₙ₋₁)│
│                                                                 │
│   Example (drawing cards without replacement):                  │
│   P(1st Ace AND 2nd Ace) = P(1st Ace) × P(2nd Ace | 1st Ace)  │
│                          = (4/52) × (3/51)                      │
│                          = 12/2652 ≈ 0.0045                     │
│                                                                 │
│   ML Application:                                               │
│   Language models use chain rule!                               │
│                                                                 │
│   P("I love ML") = P("I") × P("love"|"I") × P("ML"|"I love")  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Independence
text

┌─────────────────────────────────────────────────────────────────┐
│                    INDEPENDENCE                                 │
│                                                                 │
│   Events A and B are INDEPENDENT if:                            │
│                                                                 │
│   P(A ∩ B) = P(A) × P(B)                                       │
│                                                                 │
│   Equivalently:                                                 │
│   P(A|B) = P(A)    (knowing B doesn't change probability of A) │
│   P(B|A) = P(B)    (knowing A doesn't change probability of B) │
│                                                                 │
│   Example:                                                      │
│   • Two coin flips ARE independent                             │
│   • P(2nd flip = H | 1st flip = H) = P(2nd flip = H) = 0.5    │
│                                                                 │
│   Counter-example:                                              │
│   • Drawing cards WITHOUT replacement: NOT independent          │
│   • P(2nd Ace | 1st Ace) = 3/51 ≠ 4/52 = P(2nd Ace)           │
│                                                                 │
│   ML Note:                                                      │
│   Naive Bayes ASSUMES features are independent given class:    │
│   P(x₁, x₂, ..., xₙ | class) = ∏ᵢ P(xᵢ | class)               │
│   (Often wrong but works surprisingly well!)                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Law of Total Probability
text

┌─────────────────────────────────────────────────────────────────┐
│              LAW OF TOTAL PROBABILITY                           │
│                                                                 │
│   If B₁, B₂, ..., Bₙ partition the sample space:               │
│                                                                 │
│   P(A) = Σᵢ P(A|Bᵢ) × P(Bᵢ)                                    │
│        = P(A|B₁)P(B₁) + P(A|B₂)P(B₂) + ... + P(A|Bₙ)P(Bₙ)     │
│                                                                 │
│   Visual:                                                       │
│   ┌─────────┬─────────┬─────────┐                              │
│   │   B₁    │   B₂    │   B₃    │   ← Partition of Ω          │
│   │  ┌──┐   │ ┌──┐    │   ┌──┐  │                              │
│   │  │A │   │ │A │    │   │A │  │   ← A overlaps each part    │
│   │  │∩B₁│  │ │∩B₂│   │   │∩B₃│ │                              │
│   │  └──┘   │ └──┘    │   └──┘  │                              │
│   └─────────┴─────────┴─────────┘                              │
│                                                                 │
│   P(A) = P(A∩B₁) + P(A∩B₂) + P(A∩B₃)                          │
│        = P(A|B₁)P(B₁) + P(A|B₂)P(B₂) + P(A|B₃)P(B₃)           │
│                                                                 │
│   This is the DENOMINATOR in Bayes' theorem!                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
5. Chapter 3: Random Variables
📚 What is a Random Variable?
A random variable is a function that maps outcomes to numbers.

text

┌─────────────────────────────────────────────────────────────────┐
│                    RANDOM VARIABLES                             │
│                                                                 │
│   Random Variable X: Ω → ℝ                                     │
│   (Maps sample space to real numbers)                          │
│                                                                 │
│   Example: Coin flip                                            │
│   Ω = {Heads, Tails}                                           │
│   X(Heads) = 1                                                 │
│   X(Tails) = 0                                                 │
│                                                                 │
│   Example: Sum of two dice                                      │
│   Ω = {(1,1), (1,2), ..., (6,6)}   (36 outcomes)              │
│   X((1,1)) = 2                                                 │
│   X((1,2)) = X((2,1)) = 3                                      │
│   ...                                                          │
│   X((6,6)) = 12                                                │
│                                                                 │
│   Notation:                                                     │
│   • X, Y, Z = random variables (capital letters)               │
│   • x, y, z = specific values (lowercase)                      │
│   • P(X = x) = probability that X takes value x                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Discrete vs Continuous Random Variables
text

┌─────────────────────────────────────────────────────────────────┐
│            DISCRETE vs CONTINUOUS RANDOM VARIABLES              │
│                                                                 │
│   DISCRETE:                                                     │
│   ──────────                                                    │
│   • Takes on countable values (finite or countably infinite)   │
│   • Has Probability Mass Function (PMF)                        │
│   • P(X = x) > 0 for some specific values                      │
│                                                                 │
│   Examples:                                                     │
│   • Number of heads in 10 flips: {0, 1, 2, ..., 10}           │
│   • Number of customers: {0, 1, 2, 3, ...}                     │
│   • Class labels: {0, 1, 2}                                    │
│                                                                 │
│   PMF: P(X=x) │                                                │
│               │    █                                           │
│               │ █  █  █                                        │
│               │ █  █  █  █                                     │
│               │ █  █  █  █  █                                  │
│               └──────────────────                               │
│                 0  1  2  3  4  x                               │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   CONTINUOUS:                                                   │
│   ────────────                                                  │
│   • Takes on uncountable values (any value in an interval)     │
│   • Has Probability Density Function (PDF)                     │
│   • P(X = x) = 0 for any specific value!                       │
│   • Use P(a ≤ X ≤ b) = ∫ₐᵇ f(x)dx                             │
│                                                                 │
│   Examples:                                                     │
│   • Height: any value in [0, 300] cm                           │
│   • Temperature: any value in [-50, 50] °C                     │
│   • Neural network output (before softmax)                     │
│                                                                 │
│   PDF: f(x)  │                                                 │
│              │     ╱╲                                          │
│              │    ╱  ╲                                         │
│              │   ╱    ╲                                        │
│              │  ╱      ╲                                       │
│              │ ╱        ╲                                      │
│              └────────────────                                  │
│                    μ      x                                    │
│                                                                 │
│   Area under curve = probability                                │
│   Total area = 1                                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 PMF vs PDF
text

┌─────────────────────────────────────────────────────────────────┐
│                    PMF vs PDF                                   │
│                                                                 │
│   PROBABILITY MASS FUNCTION (PMF) - Discrete                    │
│   ───────────────────────────────────────────                   │
│   p(x) = P(X = x)                                              │
│                                                                 │
│   Properties:                                                   │
│   • p(x) ≥ 0 for all x                                         │
│   • Σₓ p(x) = 1                                                │
│   • p(x) IS a probability                                      │
│                                                                 │
│   Example: Fair die                                             │
│   p(1) = p(2) = p(3) = p(4) = p(5) = p(6) = 1/6               │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   PROBABILITY DENSITY FUNCTION (PDF) - Continuous               │
│   ─────────────────────────────────────────────────             │
│   f(x) such that P(a ≤ X ≤ b) = ∫ₐᵇ f(x)dx                     │
│                                                                 │
│   Properties:                                                   │
│   • f(x) ≥ 0 for all x                                         │
│   • ∫_{-∞}^{∞} f(x)dx = 1                                      │
│   • f(x) is NOT a probability (can be > 1!)                    │
│   • f(x) is probability per unit length (density)              │
│                                                                 │
│   Example: Uniform on [0, 1]                                    │
│   f(x) = 1 for x ∈ [0, 1], else 0                              │
│   P(0.3 ≤ X ≤ 0.7) = ∫₀.₃^0.7 1 dx = 0.4                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Cumulative Distribution Function (CDF)
text

┌─────────────────────────────────────────────────────────────────┐
│          CUMULATIVE DISTRIBUTION FUNCTION (CDF)                 │
│                                                                 │
│   F(x) = P(X ≤ x)                                              │
│                                                                 │
│   "Probability that X is less than or equal to x"              │
│                                                                 │
│   Works for BOTH discrete and continuous!                       │
│                                                                 │
│   Properties:                                                   │
│   • F(-∞) = 0                                                   │
│   • F(+∞) = 1                                                   │
│   • F is non-decreasing                                        │
│   • F is right-continuous                                      │
│                                                                 │
│   Discrete CDF (step function):     Continuous CDF (smooth):   │
│                                                                 │
│   F(x)│         ────                F(x)│          ──────      │
│     1 │    ────┘                      1 │       ╱              │
│       │────┘                            │      ╱               │
│       │                                 │     ╱                │
│     0 │                               0 │────╱                 │
│       └──────────                       └──────────            │
│             x                                 x                │
│                                                                 │
│   Relationship to PDF:                                          │
│   F(x) = ∫_{-∞}^{x} f(t)dt                                     │
│   f(x) = dF(x)/dx                                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

# Create discrete and continuous random variables
fig, axes = plt.subplots(2, 3, figsize=(15, 10))

# DISCRETE: Binomial distribution
n, p = 10, 0.5
x_discrete = np.arange(0, n+1)
pmf = stats.binom.pmf(x_discrete, n, p)
cdf_discrete = stats.binom.cdf(x_discrete, n, p)

ax = axes[0, 0]
ax.bar(x_discrete, pmf, color='steelblue', alpha=0.7)
ax.set_xlabel('x')
ax.set_ylabel('P(X = x)')
ax.set_title('Binomial PMF (n=10, p=0.5)')

ax = axes[0, 1]
ax.step(x_discrete, cdf_discrete, where='post', color='steelblue', linewidth=2)
ax.scatter(x_discrete, cdf_discrete, color='steelblue', zorder=5)
ax.set_xlabel('x')
ax.set_ylabel('P(X ≤ x)')
ax.set_title('Binomial CDF')
ax.set_ylim(0, 1.1)

# CONTINUOUS: Normal distribution
mu, sigma = 0, 1
x_continuous = np.linspace(-4, 4, 1000)
pdf = stats.norm.pdf(x_continuous, mu, sigma)
cdf_continuous = stats.norm.cdf(x_continuous, mu, sigma)

ax = axes[1, 0]
ax.plot(x_continuous, pdf, color='coral', linewidth=2)
ax.fill_between(x_continuous, pdf, alpha=0.3, color='coral')
ax.set_xlabel('x')
ax.set_ylabel('f(x)')
ax.set_title('Normal PDF (μ=0, σ=1)')

ax = axes[1, 1]
ax.plot(x_continuous, cdf_continuous, color='coral', linewidth=2)
ax.set_xlabel('x')
ax.set_ylabel('P(X ≤ x)')
ax.set_title('Normal CDF')

# Show probability as area
ax = axes[0, 2]
ax.bar(x_discrete, pmf, color='lightgray', alpha=0.7)
ax.bar([4, 5, 6], pmf[4:7], color='green', alpha=0.7, label='P(4≤X≤6)')
ax.set_xlabel('x')
ax.set_ylabel('P(X = x)')
ax.set_title(f'P(4≤X≤6) = {np.sum(pmf[4:7]):.3f}')
ax.legend()

ax = axes[1, 2]
ax.plot(x_continuous, pdf, color='lightgray', linewidth=2)
mask = (x_continuous >= -1) & (x_continuous <= 1)
ax.fill_between(x_continuous[mask], pdf[mask], alpha=0.5, color='green', 
                label=f'P(-1≤X≤1)')
ax.set_xlabel('x')
ax.set_ylabel('f(x)')
prob = stats.norm.cdf(1) - stats.norm.cdf(-1)
ax.set_title(f'P(-1≤X≤1) = {prob:.3f}')
ax.legend()

plt.tight_layout()
plt.show()
6. Chapter 4: Common Probability Distributions
📚 Discrete Distributions
Bernoulli Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                 BERNOULLI DISTRIBUTION                          │
│                                                                 │
│   Single trial with two outcomes: success (1) or failure (0)   │
│                                                                 │
│   X ~ Bernoulli(p)                                              │
│                                                                 │
│   PMF:                                                          │
│   P(X = 1) = p        (success)                                │
│   P(X = 0) = 1 - p    (failure)                                │
│                                                                 │
│   Or: P(X = x) = pˣ(1-p)¹⁻ˣ  for x ∈ {0, 1}                   │
│                                                                 │
│   E[X] = p                                                      │
│   Var(X) = p(1-p)                                              │
│                                                                 │
│   ML Use:                                                       │
│   • Binary classification output                               │
│   • Single neuron with sigmoid activation                      │
│   • Each label in multi-label classification                   │
│                                                                 │
│   Example: P(X=1)│                                              │
│                  │ █ (p)                                        │
│                  │                                              │
│                  │ █ (1-p)                                      │
│                  └─────────                                     │
│                    0   1                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Binomial Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                  BINOMIAL DISTRIBUTION                          │
│                                                                 │
│   Number of successes in n independent Bernoulli trials        │
│                                                                 │
│   X ~ Binomial(n, p)                                            │
│                                                                 │
│   PMF:                                                          │
│   P(X = k) = C(n,k) × pᵏ × (1-p)ⁿ⁻ᵏ                           │
│            = (n choose k) × pᵏ × (1-p)ⁿ⁻ᵏ                      │
│                                                                 │
│   For k = 0, 1, 2, ..., n                                      │
│                                                                 │
│   E[X] = np                                                     │
│   Var(X) = np(1-p)                                             │
│                                                                 │
│   Example: Flip coin 10 times, count heads                      │
│   n = 10, p = 0.5                                              │
│   P(X = 5) = C(10,5) × 0.5⁵ × 0.5⁵ = 252 × 0.000977 ≈ 0.246   │
│                                                                 │
│   P(X=k)│       █                                              │
│         │     █ █ █                                            │
│         │   █ █ █ █ █                                          │
│         │ █ █ █ █ █ █ █                                        │
│         └──────────────────                                     │
│           0 1 2 3 4 5 6 7 8 9 10                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Categorical/Multinomial Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│            CATEGORICAL / MULTINOMIAL DISTRIBUTION               │
│                                                                 │
│   CATEGORICAL (single trial, K outcomes):                       │
│   ─────────────────────────────────────────                     │
│   X ~ Categorical(p₁, p₂, ..., pₖ)                             │
│   where Σᵢ pᵢ = 1                                              │
│                                                                 │
│   P(X = k) = pₖ                                                │
│                                                                 │
│   Example: Rolling a die                                        │
│   p₁ = p₂ = p₃ = p₄ = p₅ = p₆ = 1/6                           │
│                                                                 │
│   ML Use: Multi-class classification                            │
│   Softmax output = categorical distribution!                    │
│   P(class=k | x) = softmax(z)ₖ                                 │
│                                                                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                 │
│   MULTINOMIAL (n trials, K outcomes):                           │
│   ─────────────────────────────────────                         │
│   Count of each outcome in n independent categorical trials    │
│                                                                 │
│   (X₁,...,Xₖ) ~ Multinomial(n, p₁,...,pₖ)                      │
│                                                                 │
│   P(X₁=x₁,...,Xₖ=xₖ) = n!/(x₁!...xₖ!) × p₁^x₁...pₖ^xₖ        │
│   where Σᵢ xᵢ = n                                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Poisson Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                  POISSON DISTRIBUTION                           │
│                                                                 │
│   Number of events in fixed interval (time, space, etc.)       │
│   when events occur at constant average rate                   │
│                                                                 │
│   X ~ Poisson(λ)                                                │
│                                                                 │
│   PMF:                                                          │
│   P(X = k) = (λᵏ × e⁻λ) / k!   for k = 0, 1, 2, ...           │
│                                                                 │
│   E[X] = λ                                                      │
│   Var(X) = λ                                                   │
│                                                                 │
│   Examples:                                                     │
│   • Website visits per hour                                    │
│   • Emails received per day                                    │
│   • Defects in manufacturing                                   │
│   • Number of accidents per month                              │
│                                                                 │
│   P(X=k)│ λ=1      λ=4         λ=10                           │
│         │ █                        █                           │
│         │ █ █              █ █ █ █ █ █ █                       │
│         │ █ █ █        █ █ █ █ █ █ █ █ █ █                     │
│         │ █ █ █ █ █  █ █ █ █ █ █ █ █ █ █ █ █                   │
│         └──────────────────────────────────────                 │
│           0 1 2 3    0 2 4 6 8    0 4 8 12 16                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Geometric Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                 GEOMETRIC DISTRIBUTION                          │
│                                                                 │
│   Number of trials until first success                         │
│                                                                 │
│   X ~ Geometric(p)                                              │
│                                                                 │
│   PMF:                                                          │
│   P(X = k) = (1-p)ᵏ⁻¹ × p   for k = 1, 2, 3, ...              │
│                                                                 │
│   E[X] = 1/p                                                    │
│   Var(X) = (1-p)/p²                                            │
│                                                                 │
│   Example: How many coin flips until first heads?              │
│   p = 0.5                                                      │
│   E[X] = 1/0.5 = 2 flips on average                           │
│                                                                 │
│   "Memoryless": P(X > m+n | X > m) = P(X > n)                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Continuous Distributions
Uniform Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                 UNIFORM DISTRIBUTION                            │
│                                                                 │
│   Equal probability across an interval                          │
│                                                                 │
│   X ~ Uniform(a, b)                                             │
│                                                                 │
│   PDF:                                                          │
│   f(x) = 1/(b-a)  for a ≤ x ≤ b                                │
│   f(x) = 0        otherwise                                    │
│                                                                 │
│   E[X] = (a+b)/2                                               │
│   Var(X) = (b-a)²/12                                           │
│                                                                 │
│   f(x)│                                                        │
│       │ ┌─────────────┐                                        │
│  1/b-a│ │             │                                        │
│       │ │             │                                        │
│     0 │─┘             └─────                                   │
│       └─────────────────────                                    │
│         a             b                                        │
│                                                                 │
│   ML Use:                                                       │
│   • Random initialization                                      │
│   • Uniform priors in Bayesian methods                        │
│   • Random search hyperparameters                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Normal (Gaussian) Distribution ⭐⭐⭐
THE most important distribution in ML!

text

┌─────────────────────────────────────────────────────────────────┐
│              NORMAL (GAUSSIAN) DISTRIBUTION                     │
│                                                                 │
│   X ~ N(μ, σ²)   or   X ~ Normal(μ, σ²)                        │
│                                                                 │
│   PDF:                                                          │
│                    1                    (x-μ)²                  │
│   f(x) = ─────────────── × exp(- ──────────)                   │
│          σ√(2π)                    2σ²                         │
│                                                                 │
│   Parameters:                                                   │
│   • μ = mean (center of distribution)                          │
│   • σ² = variance (spread)                                     │
│   • σ = standard deviation                                     │
│                                                                 │
│   E[X] = μ                                                      │
│   Var(X) = σ²                                                  │
│                                                                 │
│   Standard Normal: Z ~ N(0, 1)                                 │
│   Standardization: Z = (X - μ) / σ                             │
│                                                                 │
│   f(x) │                                                       │
│        │       ▲                                               │
│        │      ╱│╲                                              │
│        │     ╱ │ ╲                                             │
│        │    ╱  │  ╲         68% within ±1σ                     │
│        │   ╱   │   ╲        95% within ±2σ                     │
│        │  ╱    │    ╲       99.7% within ±3σ                   │
│        │ ╱     │     ╲                                         │
│        └───────┴───────────                                     │
│             μ-2σ  μ  μ+2σ                                      │
│                                                                 │
│   WHY SO IMPORTANT:                                             │
│   • Central Limit Theorem: sums → normal                       │
│   • Many natural phenomena follow normal dist                  │
│   • Maximum entropy dist for given mean & variance            │
│   • Mathematically tractable                                   │
│                                                                 │
│   ML Uses:                                                      │
│   • Linear regression assumes Gaussian errors                  │
│   • Weight initialization: N(0, σ²)                           │
│   • Gaussian Mixture Models                                    │
│   • Variational Autoencoders (latent space)                   │
│   • Gaussian Processes                                         │
│   • Batch Normalization                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Different means
ax = axes[0, 0]
x = np.linspace(-6, 10, 1000)
for mu in [-2, 0, 2, 4]:
    y = stats.norm.pdf(x, mu, 1)
    ax.plot(x, y, label=f'μ={mu}, σ=1')
ax.set_xlabel('x')
ax.set_ylabel('f(x)')
ax.set_title('Normal: Different Means')
ax.legend()

# Different variances
ax = axes[0, 1]
x = np.linspace(-6, 6, 1000)
for sigma in [0.5, 1, 2, 3]:
    y = stats.norm.pdf(x, 0, sigma)
    ax.plot(x, y, label=f'μ=0, σ={sigma}')
ax.set_xlabel('x')
ax.set_ylabel('f(x)')
ax.set_title('Normal: Different Standard Deviations')
ax.legend()

# 68-95-99.7 rule
ax = axes[1, 0]
x = np.linspace(-4, 4, 1000)
y = stats.norm.pdf(x, 0, 1)
ax.plot(x, y, 'k-', linewidth=2)

# Fill regions
ax.fill_between(x[(x >= -1) & (x <= 1)], y[(x >= -1) & (x <= 1)], 
                alpha=0.4, label='68% (±1σ)')
ax.fill_between(x[(x >= -2) & (x <= 2)], y[(x >= -2) & (x <= 2)], 
                alpha=0.3, label='95% (±2σ)')
ax.fill_between(x[(x >= -3) & (x <= 3)], y[(x >= -3) & (x <= 3)], 
                alpha=0.2, label='99.7% (±3σ)')
ax.set_xlabel('x (standard deviations)')
ax.set_ylabel('f(x)')
ax.set_title('68-95-99.7 Rule')
ax.legend()

# CDF
ax = axes[1, 1]
x = np.linspace(-4, 4, 1000)
cdf = stats.norm.cdf(x, 0, 1)
ax.plot(x, cdf, 'b-', linewidth=2)
ax.axhline(0.5, color='gray', linestyle='--', alpha=0.5)
ax.axvline(0, color='gray', linestyle='--', alpha=0.5)
ax.axhline(0.025, color='red', linestyle='--', alpha=0.5)
ax.axhline(0.975, color='red', linestyle='--', alpha=0.5)
ax.set_xlabel('x')
ax.set_ylabel('P(X ≤ x)')
ax.set_title('Standard Normal CDF')

plt.tight_layout()
plt.show()

# Print key quantiles
print("Standard Normal Quantiles:")
for p in [0.025, 0.05, 0.5, 0.95, 0.975]:
    z = stats.norm.ppf(p)
    print(f"  P(Z ≤ {z:.3f}) = {p}")
Exponential Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                EXPONENTIAL DISTRIBUTION                         │
│                                                                 │
│   Time between events in a Poisson process                     │
│                                                                 │
│   X ~ Exponential(λ)   or   X ~ Exp(λ)                         │
│                                                                 │
│   PDF:                                                          │
│   f(x) = λe^(-λx)   for x ≥ 0                                  │
│                                                                 │
│   CDF:                                                          │
│   F(x) = 1 - e^(-λx)                                           │
│                                                                 │
│   E[X] = 1/λ                                                   │
│   Var(X) = 1/λ²                                                │
│                                                                 │
│   f(x)│                                                        │
│       │╲                                                       │
│       │ ╲                                                      │
│       │  ╲                                                     │
│       │   ╲_                                                   │
│       │     ╲__                                                │
│       │        ╲___                                            │
│     0 │____________╲_____                                      │
│       └─────────────────────                                    │
│       0                   x                                    │
│                                                                 │
│   "Memoryless property": P(X > s+t | X > s) = P(X > t)         │
│                                                                 │
│   Examples:                                                     │
│   • Time until next customer arrives                           │
│   • Lifetime of electronic components                          │
│   • Time between radioactive decays                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Beta Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                  BETA DISTRIBUTION                              │
│                                                                 │
│   Distribution on [0, 1] - perfect for probabilities!          │
│                                                                 │
│   X ~ Beta(α, β)                                                │
│                                                                 │
│   PDF:                                                          │
│   f(x) = [Γ(α+β) / (Γ(α)Γ(β))] × x^(α-1) × (1-x)^(β-1)        │
│                                                                 │
│   E[X] = α / (α + β)                                           │
│   Var(X) = αβ / [(α+β)²(α+β+1)]                               │
│                                                                 │
│   Special cases:                                                │
│   • Beta(1, 1) = Uniform(0, 1)                                 │
│   • α = β: symmetric around 0.5                                │
│   • α > β: skewed right (toward 1)                             │
│   • α < β: skewed left (toward 0)                              │
│                                                                 │
│   f(x)│ α=2,β=5    α=5,β=5     α=5,β=2                        │
│       │    ╱╲         ╱╲          ╱╲                          │
│       │   ╱  ╲       ╱  ╲        ╱  ╲                         │
│       │  ╱    ╲     ╱    ╲      ╱    ╲                        │
│       │ ╱      ╲   ╱      ╲    ╱      ╲                       │
│       │╱        ╲_╱        ╲__╱        ╲                      │
│       └──────────────────────────────────                       │
│         0        0.5          1                                │
│                                                                 │
│   ML Use:                                                       │
│   • Prior for Bernoulli parameter p                            │
│   • Bayesian inference for proportions                         │
│   • Conjugate prior (Beta + Bernoulli → Beta)                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Gamma Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                  GAMMA DISTRIBUTION                             │
│                                                                 │
│   Generalizes exponential; models positive continuous values   │
│                                                                 │
│   X ~ Gamma(α, β)   or   Gamma(shape=k, scale=θ)              │
│                                                                 │
│   PDF (shape-rate parameterization):                            │
│   f(x) = [β^α / Γ(α)] × x^(α-1) × e^(-βx)   for x > 0         │
│                                                                 │
│   E[X] = α/β                                                   │
│   Var(X) = α/β²                                                │
│                                                                 │
│   Special cases:                                                │
│   • Gamma(1, β) = Exponential(β)                               │
│   • Gamma(n/2, 1/2) = Chi-squared(n)                          │
│                                                                 │
│   ML Use:                                                       │
│   • Prior for precision (inverse variance)                     │
│   • Modeling waiting times                                     │
│   • Prior for rate parameters                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Distribution Summary Table
text

┌─────────────────────────────────────────────────────────────────┐
│                DISTRIBUTION SUMMARY                             │
├──────────────┬────────────┬─────────┬─────────┬────────────────┤
│ Distribution │ Support    │ E[X]    │ Var(X)  │ ML Use         │
├──────────────┼────────────┼─────────┼─────────┼────────────────┤
│ DISCRETE     │            │         │         │                │
├──────────────┼────────────┼─────────┼─────────┼────────────────┤
│ Bernoulli(p) │ {0, 1}     │ p       │ p(1-p)  │ Binary class   │
│ Binomial(n,p)│ {0,..,n}   │ np      │ np(1-p) │ Count success  │
│ Categorical  │ {1,..,K}   │ -       │ -       │ Multi-class    │
│ Poisson(λ)   │ {0,1,2,..} │ λ       │ λ       │ Count events   │
│ Geometric(p) │ {1,2,3,..} │ 1/p     │(1-p)/p² │ First success  │
├──────────────┼────────────┼─────────┼─────────┼────────────────┤
│ CONTINUOUS   │            │         │         │                │
├──────────────┼────────────┼─────────┼─────────┼────────────────┤
│ Uniform(a,b) │ [a, b]     │ (a+b)/2 │(b-a)²/12│ Random init    │
│ Normal(μ,σ²) │ ℝ          │ μ       │ σ²      │ EVERYWHERE!    │
│ Exponential  │ [0, ∞)     │ 1/λ     │ 1/λ²    │ Time between   │
│ Beta(α,β)    │ [0, 1]     │ α/(α+β) │ complex │ Prob. prior    │
│ Gamma(α,β)   │ (0, ∞)     │ α/β     │ α/β²    │ Precision prior│
│ Chi-sq(k)    │ [0, ∞)     │ k       │ 2k      │ Test statistic │
│ Student's t  │ ℝ          │ 0       │ k/(k-2) │ Small samples  │
└──────────────┴────────────┴─────────┴─────────┴────────────────┘
7. Chapter 5: Joint, Marginal & Conditional Distributions
📚 Joint Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                 JOINT DISTRIBUTION                              │
│                                                                 │
│   Describes probability of MULTIPLE random variables together  │
│                                                                 │
│   DISCRETE:                                                     │
│   ──────────                                                    │
│   P(X = x, Y = y) = joint PMF                                  │
│                                                                 │
│   Example (two dice):                                           │
│   P(X=1, Y=1) = 1/36                                           │
│   P(X=1, Y=2) = 1/36                                           │
│   ...                                                          │
│                                                                 │
│   Joint PMF Table:                                              │
│   ┌─────┬──────┬──────┬──────┬──────┐                          │
│   │     │ Y=1  │ Y=2  │ Y=3  │ ...  │                          │
│   ├─────┼──────┼──────┼──────┼──────┤                          │
│   │ X=1 │ 1/36 │ 1/36 │ 1/36 │ ...  │                          │
│   │ X=2 │ 1/36 │ 1/36 │ 1/36 │ ...  │                          │
│   │ X=3 │ 1/36 │ 1/36 │ 1/36 │ ...  │                          │
│   │ ... │ ...  │ ...  │ ...  │ ...  │                          │
│   └─────┴──────┴──────┴──────┴──────┘                          │
│                                                                 │
│   CONTINUOUS:                                                   │
│   ────────────                                                  │
│   f(x, y) = joint PDF                                          │
│   P(a < X < b, c < Y < d) = ∫ₐᵇ∫ᶜᵈ f(x,y) dy dx               │
│                                                                 │
│   Must satisfy: ∫∫ f(x,y) dx dy = 1                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📚 Marginal Distribution
text

┌─────────────────────────────────────────────────────────────────┐
│                MARGINAL DISTRIBUTION                            │
│                                                                 │
│   Distribution of ONE variable, ignoring the other             │
│   "Sum out" (discrete) or "integrate out" (continuous)         │
│                                                                 │
│   DISCRETE:                                                     │
│   ──────────                                                    │
│   P(X = x) = Σᵧ P(X = x, Y = y)                                │
│   P(Y = y) = Σₓ P(X = x, Y = y)                                │
│                                                                 │
│   CONTINUOUS:                                                   │
│   ────────────                                                  │
│   f_X(x) = ∫ f(x, y) dy                                        │
│   f_Y(y) = ∫ f(x, y) dx                                        │
│                                                                 │
│   Visual (why "marginal"):                                      │
│                                                                 │
│   Joint table with margins:                                     │
│   ┌─────┬──────┬──────┬──────┬─────────┐                       │
│   │     │ Y=1  │ Y=2  │ Y=3  │ P(X=x)  │ ← Marginal of X      │
│   ├─────┼──────┼──────┼──────┼─────────┤                       │
│   │ X=1 │ 0.1  │ 0.1  │ 0.1  │   0.3   │   (row sums)         │
│   │ X=2 │ 0.1  │ 0.2  │ 0.1  │   0.4   │                       │
│   │ X=3 │ 0.1  │ 0.1  │ 0.1  │   0.3   │                       │
│   ├─────┼──────┼──────┼──────┼─────────┤                       │
│   │P(Y) │ 0.3  │ 0.4  │ 0.3  │   1.0   │                       │
│   └─────┴──────┴──────┴──

```markdown
│P(Y) │ 0.3  │ 0.4  │ 0.3  │   1.0   │                       │
│     │──────────┼──────────┼──────────┤         │ ← Sum = P(X,Y)|
└─────┴──────┴──────┴──────┴─────────┘                          │
│                                 ↑                               │
│                         Column Sums                             │
│                                                                 │
│   ML Connection:                                                │
│   • In a dataset, rows = samples, columns = features            │
│   • Marginal = count of a single feature regardless of others  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Conditional Distribution

**Conditional distribution** describes the distribution of one variable given that another is fixed.

```
┌─────────────────────────────────────────────────────────────────┐
│                 CONDITIONAL DISTRIBUTION                        │
│                                                                 │
│   DISCRETE:                                                     │
│   ──────────                                                    │
│   P(X=x | Y=y) = P(X=x, Y=y) / P(Y=y)                          │
│                                                                 │
│   CONTINUOUS:                                                   │
│   ────────────                                                  │
│   f(x|y) = f(x,y) / f_Y(y)                                     │
│                                                                 │
│   Relationship to Bayes' Theorem:                               │
│   P(A|B) = P(B|A)P(A) / P(B)                                   │
│   Rearrange: P(A|B) × P(B) = P(B|A) × P(A)                     │
│   Left side: P(A∩B)                                            │
│   Right side: P(A∩B)                                           │
│   They are equal!                                              │
│                                                                 │
│   ML Application:                                               │
│   • Conditional probability tables (Naive Bayes)                │
│   • Generative models: p(image|class), p(word|sentence)        │
│   • Recommendation: P(click|user, item)                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Example: Medical Diagnosis Revisited (Probabilistic View)

```python
import numpy as np
import pandas as pd

# Create sample data (simulating medical test results)
np.random.seed(42)
n_patients = 10000

# Disease status (prior: 1%)
has_disease = np.random.rand(n_patients) < 0.01

# Test accuracy (conditional prob)
# If disease, 99% positive; if no disease, 5% false positive
test_positive = np.zeros(n_patients, dtype=bool)
for i in range(n_patients):
    if has_disease[i]:
        test_positive[i] = np.random.rand() < 0.99
    else:
        test_positive[i] = np.random.rand() < 0.05

# Create dataframe
df = pd.DataFrame({
    'Disease': ['Yes' if d else 'No' for d in has_disease],
    'Test': ['Positive' if p else 'Negative' for p in test_positive]
})

# Calculate empirical probabilities
total = len(df)
p_disease = df['Disease'].value_counts()['Yes'] / total
p_test_pos = df['Test'].value_counts()['Positive'] / total

# Intersection
both = len(df[(df['Disease'] == 'Yes') & (df['Test'] == 'Positive')])
p_both = both / total

# Conditional P(Disease | Test=Positive)
p_disease_given_positive = p_both / p_test_pos

print(f"P(Disease) [Prior]: {p_disease:.4f}")
print(f"P(Test=Positive) [Evidence]: {p_test_pos:.4f}")
print(f"P(Disease ∩ Positive) [Joint]: {p_both:.4f}")
print(f"P(Disease | Test=Positive) [Posterior]: {p_disease_given_positive:.4f}")
print(f"\nThis matches our Bayes' calculation: ~17%!")
```

### 📚 Transformation of Random Variables

When we apply a function $g(X)$ to a random variable $X$, the distribution changes.

#### Discrete Case

Simple: $Y = g(X)$, find values and sum probabilities.

#### Continuous Case (Change of Variables Formula) ⭐⭐⭐

If $Y = g(X)$ and $g$ is monotonic:

$$
f_Y(y) = f_X(g^{-1}(y)) \cdot \left| \frac{d}{dy} g^{-1}(y) \right|
$$

In terms of Jacobian (multiple dimensions):

$$
f_Y(\mathbf{y}) = f_X(\mathbf{x}) \cdot \left| \det(J) \right|^{-1}
$$

Where $J = \frac{\partial \mathbf{x}}{\partial \mathbf{y}}$.

**ML Connection:** This is critical for:
1.  Normalizing flows (generating complex distributions)
2.  VAE latent space transformations
3.  Reparameterization trick

```python
import scipy.stats as stats
import numpy as np
import matplotlib.pyplot as plt

# Transform X ~ Uniform(0,1) to Y = X^2
# f_X(x) = 1 for x in [0,1]
# y = x^2 => x = sqrt(y)
# dx/dy = 1/(2*sqrt(y))

# Analytical PDF for Y
def f_y_analytic(y):
    return 1 / (2 * np.sqrt(y))  # Only valid for y in [0, 1]

# Monte Carlo simulation
n_samples = 100000
x_uniform = np.random.uniform(0, 1, n_samples)
y_transformed = x_uniform ** 2

# Plot
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Simulated histogram
axes[0].hist(y_transformed, bins=50, density=True, alpha=0.6, label='Monte Carlo')
axes[0].plot(np.linspace(0, 1, 100), f_y_analytic(np.linspace(0, 1, 100)), 
             'r-', linewidth=2, label='Analytical')
axes[0].set_xlabel('y')
axes[0].set_ylabel('Density')
axes[0].set_title('Transformed Distribution: Y = X²')
axes[0].legend()
axes[0].grid(True)

# Verify expectation
print(f"E[Y] simulated: {np.mean(y_transformed):.4f}")
print(f"E[Y] analytical: {2/3:.4f}")

plt.tight_layout()
plt.show()
```

---

## 8. Chapter 6: Expectation, Variance & Moments

### 📚 Expected Value

The expected value is the **weighted average** of all possible outcomes.

```
┌─────────────────────────────────────────────────────────────────┐
│                  EXPECTED VALUE                                 │
│                                                                 │
│   E[X] = ∫ x f(x)dx  (continuous)                              │
│   E[X] = Σ x p(x)  (discrete)                                  │
│                                                                 │
│   Interpretation: "Long-term average outcome"                   │
│                                                                 │
│   Properties:                                                   │
│   • Linearity: E[aX + bY] = aE[X] + bE[Y]                      │
│   • Not necessarily a possible value!                          │
│     (Expected die roll = 3.5, impossible!)                     │
│                                                                 │
│   ML Connection:                                                │
│   • Risk estimation in RL                                        │
│   • Expected utility maximization                              │
│   • Mean Squared Error minimizer: argmin_w E[(Y - w)^2] = μ    │
│   • Absolute Error minimizer: argmin_w E[|Y - w|] = median     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
# Example: Expected value of a biased coin
def expected_value_biased_coin(p_success, payout_success=1, payout_fail=-0.5):
    """
    If you win $1 on success (prob p), lose $0.5 on failure.
    What's your expected gain per game?
    """
    ev = (p_success * payout_success) + ((1-p_success) * payout_fail)
    return ev

p = 0.4
ev = expected_value_biased_coin(p)
print(f"Expected value with p={p}: ${ev:.2f}")

if ev > 0:
    print("You should play! Long-term profit.")
else:
    print("Don't play! Expected loss.")
```

### 📚 Variance

Variance measures **spread** around the mean.

```
┌─────────────────────────────────────────────────────────────────┐
│                     VARIANCE                                    │
│                                                                 │
│   Var(X) = E[(X - E[X])²]                                       │
│   Standard Deviation: σ = √Var(X)                              │
│                                                                 │
│   Computational formula (often easier):                         │
│   Var(X) = E[X²] - (E[X])²                                      │
│                                                                 │
│   Properties:                                                   │
│   • Var(aX + b) = a²Var(X)                                     │
│   • Independent: Var(X+Y) = Var(X) + Var(Y)                    │
│                                                                 │
│   ML Connection:                                                │
│   • Loss functions often minimize variance                     │
│   • Uncertainty quantification (confidence intervals)          │
│   • Exploring reward variance in RL                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Higher Order Moments

```
┌─────────────────────────────────────────────────────────────────┐
│                   HIGHER ORDER MOMENTS                          │
├──────────────┬──────────────────────────────────────────────────┤
│  Moment      │ Description                                      │
├──────────────┼──────────────────────────────────────────────────┤
│  1st         │ Mean (location)                                  │
│  2nd (Centered) │ Variance (scale/spread)                      │
│  3rd (Standardized) │ Skewness (asymmetry)                    │
│  4th (Standardized) │ Kurtosis (tailedness)                   │
└──────────────┴──────────────────────────────────────────────────┘
```

**Skewness:**
- Positive skew: Long tail to right (Income data)
- Negative skew: Long tail to left (Product returns)
- Symmetric: Zero skew (Normal distribution)

**Kurtosis:**
- High kurtosis: Heavy tails (outliers common)
- Low kurtosis: Light tails (data concentrated near mean)

```python
from scipy.stats import skew, kurtosis

# Generate data
np.random.seed(42)
normal_data = np.random.normal(0, 1, 10000)
skewed_data = np.random.exponential(1, 10000)

print(f"Normal Data:")
print(f"  Skewness: {skew(normal_data):.3f} (should be ~0)")
print(f"  Kurtosis: {kurtosis(normal_data):.3f} (should be ~0)")

print(f"\nExponential Data:")
print(f"  Skewness: {skew(skewed_data):.3f} (>0, right skewed)")
print(f"  Kurtosis: {kurtosis(skewed_data):.3f} (>0, heavy tail)")
```

---

## 9. Chapter 7: Covariance, Correlation & Independence

### 📚 Covariance

Measures how two variables vary together.

```
┌─────────────────────────────────────────────────────────────────┐
│                   COVARIANCE                                    │
│                                                                 │
│   Cov(X, Y) = E[(X - E[X])(Y - E[Y])]                         │
│                                                                 │
│   Interpretation:                                               │
│   • Cov > 0: When X increases, Y tends to increase             │
│   • Cov < 0: When X increases, Y tends to decrease             │
│   • Cov = 0: No linear relationship                            │
│                                                                 │
│   Problem: Scale dependent!                                     │
│   Covariance depends on units (cm vs m)                        │
│                                                                 │
│   Solution: Normalize by standard deviations → Correlation      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Correlation Coefficient

Normalized covariance (always between -1 and 1).

```
┌─────────────────────────────────────────────────────────────────┐
│               CORRELATION COEFFICIENT                           │
│                                                                 │
│   ρ(X, Y) = Cov(X, Y) / (σₓ · σᵧ)                              │
│                                                                 │
│   Range: [-1, 1]                                                │
│   • ρ = 1: Perfect positive correlation                        │
│   • ρ = -1: Perfect negative correlation                       │
│   • ρ = 0: No linear correlation (but could have non-linear!)  │
│                                                                 │
│   Visual:                                                       │
│                                                                 │
│     ρ = 1       ρ ≈ 0.8       ρ ≈ 0       ρ ≈ -0.8      ρ = -1│
│                                                                 │
│      ●●              ○○            ○○            ○○           ●●│
│      ○○              ○○            ○○            ○○           ○○│
│      ○○              ○○            ○○            ○○           ○○│
│      ○○              ○○            ○○            ○○           ○○│
│     ○○○            ○○○          ○○○            ○○○         ○○○│
│     ○○○          ○○○            ○○○          ○○○           ○○○│
│                                                                    │
│   Key Insight:                                                    │
│   Correlation ≠ Causation!                                      │
│   (Ice cream sales ↔ Shark attacks both linked to summer heat)   │
│                                                                 │
│   ML Use:                                                       │
│   • Feature selection (remove highly correlated features)      │
│   • PCA assumes uncorrelated components                        │
│   • Multicollinearity detection                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
n = 100

# Generate correlated data
mean = [0, 0]
cov_matrix = [[1, 0.8], [0.8, 1]]
data = np.random.multivariate_normal(mean, cov_matrix, n)

x = data[:, 0]
y = data[:, 1]

corr = np.corrcoef(x, y)[0, 1]
print(f"Correlation coefficient: {corr:.3f}")

plt.figure(figsize=(6, 6))
plt.scatter(x, y, alpha=0.6)
plt.title(f"Scatter Plot\nCorrelation r = {corr:.3f}")
plt.xlabel('X')
plt.ylabel('Y')
plt.grid(True)
plt.axhline(0, color='gray', linewidth=0.5)
plt.axvline(0, color='gray', linewidth=0.5)
plt.tight_layout()
plt.show()
```

### 📚 Independence vs Uncorrelated

```
┌─────────────────────────────────────────────────────────────────┐
│      INDEPENDENCE vs UNCORRELATED: CRUCIAL DISTINCTION          │
│                                                                 │
│   Definition:                                                   │
│   ────────────                                                  │
│   X, Y are independent: P(X,Y) = P(X)P(Y)                      │
│   X, Y are uncorrelated: Cov(X,Y) = 0                          │
│                                                                 │
│   Implications:                                                 │
│   ──────────────────                                            │
│   • Independent → Uncorrelated ✓                               │
│   • Uncorrelated → Independent ✗ (FALSE)!                      │
│                                                                 │
│   Counter-example:                                              │
│   ─────────────────────────────                                 │
│   Let X ~ Uniform(-1, 1)                                        │
│   Let Y = X²                                                   │
│                                                                 │
│   Cov(X, Y) = E[X³] - E[X]E[X²] = 0 - 0 = 0                    │
│   (Uncorrelated!)                                               │
│                                                                 │
│   But P(Y|X) is deterministic! Clearly dependent!              │
│   (Parabola relationship)                                       │
│                                                                 │
│   Special Case: Gaussian Distributions                          │
│   For jointly normal variables: Uncorrelated ⇔ Independent      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 10. Chapter 8: Information Theory

### 📚 Entropy

Measure of uncertainty or "surprise" in a random variable.

```
┌─────────────────────────────────────────────────────────────────┐
│                      ENTROPY                                    │
│                                                                 │
│   H(X) = - Σ p(x) log₂ p(x)                                    │
│                                                                 │
│   Units: Bits (if log base 2) or Nats (natural log)             │
│                                                                 │
│   Meaning: "Average number of bits needed to encode X"         │
│                                                                 │
│   Properties:                                                   │
│   • Maximum entropy when uniform distribution                  │
│   • Minimum entropy when certain (probability 1)               │
│   • Non-negative: H(X) ≥ 0                                     │
│                                                                 │
│   Example (Coin Flip):                                          │
│   ────────────────────                                          │
│   Fair coin (p=0.5):                                            │
│   H = - (0.5·log₂0.5 + 0.5·log₂0.5) = 1 bit                    │
│                                                                 │
│   Biased coin (p=0.9):                                          │
│   H = - (0.9·log₂0.9 + 0.1·log₂0.1) ≈ 0.47 bits                │
│   (Lower entropy = more predictable)                           │
│                                                                 │
│   ML Connection:                                                │
│   • Decision Trees use Entropy/Gini impurity for splits        │
│   • Cross-Entropy loss measures prediction error               │
│   • Mutual information for feature selection                   │
│   • Reinforcement learning (exploration bonus)                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Cross-Entropy

Measure of dissimilarity between two probability distributions $P$ and $Q$.

```
┌─────────────────────────────────────────────────────────────────┐
│                  CROSS-ENTROPY LOSS                             │
│                                                                 │
│   H(P, Q) = - Σ P(x) log Q(x)                                  │
│                                                                 │
│   Interpretation: Average bits needed to encode P using code   │
│   optimized for Q (wrong distribution)                         │
│                                                                 │
│   Decomposition:                                                │
│   H(P, Q) = H(P) + D_KL(P || Q)                                │
│   • H(P): True entropy (constant for problem)                  │
│   • D_KL: KL Divergence (what we optimize)                     │
│                                                                 │
│   Neural Networks:                                              │
│   ──────────────────                                            │
│   Target distribution: One-hot vector P (ground truth)         │
│   Model distribution: Softmax output Q (predictions)           │
│                                                                 │
│   Cross-Entropy Loss:                                           │
│   L = - Σ y_true · log(y_pred)                                 │
│   Which is exactly H(P, Q)!                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 KL Divergence (Kullback-Leibler)

Measure of how much Q differs from P.

```
┌─────────────────────────────────────────────────────────────────┐
│                    KL-DIVERGENCE                                │
│                                                                 │
│   D_KL(P || Q) = Σ P(x) log [P(x) / Q(x)]                     │
│                                                                 │
│   Also called: Relative Entropy                                  │
│                                                                 │
│   Properties:                                                   │
│   • D_KL ≥ 0 (Gibbs inequality)                               │
│   • D_KL = 0 iff P = Q                                        │
│   • Asymmetric: D_KL(P||Q) ≠ D_KL(Q||P)                       │
│   • Not a metric (doesn't satisfy triangle inequality)         │
│                                                                 │
│   Why asymmetric?                                               │
│   ────────────────                                              │
│   D_KL(P||Q) penalizes Q missing where P has mass (Type-I error)│
│   D_KL(Q||P) penalizes P missing where Q has mass (Type-II)    │
│                                                                 │
│   ML Use:                                                       │
│   • Variational Autoencoders (VAE) regularization term         │
│   • Information bottleneck                                     │
│   • Policy updates in RL (PPO)                                 │
│   • Comparing predicted vs true distributions                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
from scipy.special import kl_div

# Define discrete distributions P and Q
P = np.array([0.2, 0.5, 0.3])  # True distribution
Q = np.array([0.3, 0.3, 0.4])  # Approximate distribution

# Calculate KL divergence
kl_PQ = kl_div(P, Q)  # SciPy returns natural log KL
kl_PQ_bits = np.sum(P * np.log2(P/Q))

print(f"D_KL(P || Q) [nats]: {kl_PQ:.4f}")
print(f"D_KL(P || Q) [bits]: {kl_PQ_bits:.4f}")

# Check asymmetry
kl_QP = np.sum(Q * np.log2(Q/P))
print(f"\nD_KL(Q || P) [bits]: {kl_QP:.4f}")
print("KL divergence is asymmetric!")
```

---

## 11. Chapter 9: Descriptive Statistics

### 📚 Measures of Central Tendency

```
┌─────────────────────────────────────────────────────────────────┐
│                MEASURES OF CENTRAL TENDENCY                     │
│                                                                 │
│   MEAN (Arithmetic Average):                                    │
│   • Sum of values / Count                                      │
│   • Sensitive to outliers                                      │
│   • Best for symmetric distributions                           │
│                                                                 │
│   MEDIAN (Middle Value):                                        │
│   • Value separating higher/lower half                         │
│   • Robust to outliers                                         │
│   • Best for skewed distributions (income, housing prices)     │
│                                                                 │
│   MODE (Most Frequent):                                         │
│   • Most common value                                          │
│   • Can be multimodal                                          │
│   • Useful for categorical data                                │
│                                                                 │
│   Example with outliers:                                        │
│   Data: [1, 2, 3, 4, 100]                                      │
│   Mean: 22.0  ← Influenced by outlier                        │
│   Median: 3     ← Represents typical value better            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Quantiles and Percentiles

```
┌─────────────────────────────────────────────────────────────────┐
│                  QUANTILES AND PERCENTILES                      │
│                                                                 │
│   Quantile Q(p): Value such that P(X ≤ Q(p)) = p               │
│   • p = 0.5 → Median                                          │
│   • p = 0.25 → First Quartile (Q1)                            │
│   • p = 0.75 → Third Quartile (Q3)                            │
│                                                                 │
│   Interquartile Range (IQR):                                    │
│   ───────────────────────                                       │
│   IQR = Q3 - Q1                                               │
│                                                                 │
│   Outlier Detection Rule:                                       │
│   • Lower fence: Q1 - 1.5×IQR                                   │
│   • Upper fence: Q3 + 1.5×IQR                                   │
│   • Values outside fences = outliers                           │
│                                                                 │
│   Box Plot: Visual representation of these statistics          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Generate skewed data
np.random.seed(42)
data = np.random.exponential(scale=1, size=1000)

# Plot distribution and boxplot
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

ax = axes[0]
sns.histplot(data, kde=True, ax=ax, bins=50)
ax.axvline(data.mean(), color='red', linestyle='--', label='Mean')
ax.axvline(np.median(data), color='green', linestyle='--', label='Median')
ax.legend()
ax.set_title('Distribution of Exponential Data (Skewed)')

ax = axes[1]
sns.boxplot(x=data, ax=ax)
ax.set_title('Box Plot (Median + IQR)')

plt.tight_layout()
plt.show()

# Calculate quartiles
q1, median, q3 = np.percentile(data, [25, 50, 75])
iqr = q3 - q1
lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

print(f"Q1 (25th percentile): {q1:.2f}")
print(f"Median: {median:.2f}")
print(f"Q3 (75th percentile): {q3:.2f}")
print(f"IQR: {iqr:.2f}")
print(f"Outlier range: [{lower_bound:.2f}, {upper_bound:.2f}]")
```

---

## 12. Chapter 10: Inferential Statistics

### 📚 Estimation

Using sample data to estimate population parameters.

```
┌─────────────────────────────────────────────────────────────────┐
│                  ESTIMATION                                     │
├──────────────┬──────────────────────────────────────────────────┤
│ Type         │ Description                                      │
├──────────────┼──────────────────────────────────────────────────┤
│ Point Estimate│ Single best guess (e.g., sample mean)           │
│ Interval Est. │ Range likely to contain parameter (CI)          │
│ Confidence    │ How sure are we? (95%, 99%)                     │
└──────────────┴──────────────────────────────────────────────────┘
```

#### Sample Mean as Estimator

```
┌─────────────────────────────────────────────────────────────────┐
│           SAMPLE MEAN AS POPULATION ESTIMATOR                   │
│                                                                 │
│   θ̂ = (1/n) Σᵢ xᵢ                                             │
│                                                                 │
│   Good properties:                                              │
│   • Unbiased: E[θ̂] = θ                                        │
│   • Consistent: θ̂ → θ as n → ∞                                │
│   • Efficient: Lowest variance among unbiased estimators       │
│                                                                 │
│   BUT: What if we don't know θ? How confident?                 │
│   Answer: Confidence Interval                                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Confidence Intervals

Range where the true parameter lies with some probability.

```
┌─────────────────────────────────────────────────────────────────┐
│              CONFIDENCE INTERVALS (CI)                          │
│                                                                 │
│   Formula (when σ known):                                       │
│   CI = [μ̂ ± z_(α/2) × (σ/√n)]                                  │
│                                                                 │
│   Where:                                                        │
│   • μ̂ = sample mean                                            │
│   • z_(α/2) = quantile from standard normal (1.96 for 95%)     │
│   • σ = population std dev                                     │
│   • n = sample size                                            │
│                                                                 │
│   95% CI interpretation:                                        │
│   "If we repeated sampling many times, 95% of computed CIs     │
│    would contain the true mean."                               │
│                                                                 │
│   NOT: "There's 95% probability the true mean is in this CI"  │
│        (Mean is fixed; CI is random)                           │
│                                                                 │
│   Impact of n (sample size):                                    │
│   CI width ∝ 1/√n                                               │
│   Need 4x samples to halve interval width                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
from scipy import stats

# Simulate repeated sampling
np.random.seed(42)
population_mean = 50
population_std = 10
sample_size = 100
n_simulations = 1000

coverage = 0
bounds_list = []

for _ in range(n_simulations):
    sample = np.random.normal(population_mean, population_std, sample_size)
    sample_mean = np.mean(sample)
    
    # 95% CI (using t-distribution for unknown sigma)
    se = stats.t.ppf(0.975, sample_size - 1) * sample.std(ddof=1) / np.sqrt(sample_size)
    ci_lower = sample_mean - se
    ci_upper = sample_mean + se
    
    bounds_list.append((ci_lower, ci_upper))
    if ci_lower <= population_mean <= ci_upper:
        coverage += 1

empirical_coverage = coverage / n_simulations
print(f"Theoretical Coverage: 95%")
print(f"Empirical Coverage: {empirical_coverage:.1%}")

# Plot first 20 intervals
plt.figure(figsize=(10, 5))
for i, (lower, upper) in enumerate(bounds_list[:20]):
    plt.hlines(population_mean, lower, upper, colors='blue' if (population_mean >= lower and population_mean <= upper) else 'red', lw=2)
plt.axhline(population_mean, color='black', linestyle='--', label='True Mean')
plt.yticks([])
plt.title('Confidence Intervals (Red miss, Blue hit)')
plt.legend()
plt.tight_layout()
plt.show()
```

### 📚 Central Limit Theorem (CLT) ⭐⭐⭐

**THE most important theorem in statistics.**

```
┌─────────────────────────────────────────────────────────────────┐
│                CENTRAL LIMIT THEOREM                            │
│                                                                 │
│   Statement:                                                    │
│   ──────────                                                    │
│   Given independent, identically distributed random variables   │
│   X₁, ..., Xₙ with mean μ and variance σ²:                     │
│                                                                 │
│   The distribution of the SAMPLE MEAN approaches NORMAL(μ, σ²/n)│
│   as n becomes large (typically n ≥ 30).                       │
│                                                                 │
│   Formula:                                                      │
│   Z = (X̄ - μ) / (σ/√n) → N(0, 1)                              │
│                                                                 │
│   WHY IT MATTERS FOR ML:                                        │
│   ───────────────────────                                       │
│   • Justifies normal assumption for errors                     │
│   • Enables t-tests and hypothesis testing                     │
│   • Explains why BatchNorm works (activations become Gaussian) │
│   • Allows inference even if underlying dist is unknown        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Generate non-normal distribution
np.random.seed(42)
source_dist = lambda n: np.random.exponential(scale=2, size=n)  # Skewed!

sample_sizes = [5, 30, 100]
means_all = []

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for i, n in enumerate(sample_sizes):
    means = []
    for _ in range(10000):  # Many experiments
        sample = source_dist(n)
        sample_mean = np.mean(sample)
        means.append(sample_mean)
    
    means_all.append(means)
    
    # Plot histogram
    axes[i].hist(means, bins=50, density=True, alpha=0.7, edgecolor='black')
    x = np.linspace(min(means), max(means), 100)
    axes[i].plot(x, norm.pdf(x, loc=2, scale=2/np.sqrt(n)), 'r--', linewidth=2)
    
    axes[i].set_title(f'Sampling Dist of Mean (n={n})\nShould look Normal!')
    axes[i].set_xlabel('Sample Mean')
    axes[i].set_ylabel('Density')

plt.tight_layout()
plt.show()
```

---

## 13. Chapter 11: Hypothesis Testing

### 📚 Null Hypothesis Significance Testing

Process to decide if observed effect is real or due to chance.

```
┌─────────────────────────────────────────────────────────────────┐
│              HYPOTHESIS TESTING                                 │
│                                                                 │
│   Step-by-step:                                                 │
│   ──────────────                                                │
│   1. State Null Hypothesis H₀ (status quo, no effect)          │
│   2. State Alternative H₁ (effect exists)                      │
│   3. Choose significance level α (usually 0.05)                │
│   4. Compute Test Statistic                                     │
│   5. Compute p-value (prob of observing result if H₀ true)     │
│   6. Reject H₀ if p < α                                        │
│                                                                 │
│   Types of Errors:                                              │
│   ────────────────────                                          │
│   • Type I (False Positive): Reject H₀ when H₀ is true         │
│     Probability = α                                           │
│   • Type II (False Negative): Fail to reject H₀ when H₁ true   │
│     Probability = β                                           │
│   • Power = 1 - β                                              │
│                                                                 │
│   ML Application:                                               │
│   • A/B testing for model performance                          │
│   • Feature importance significance                            │
│   • Hyperparameter selection validation                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Common Tests

```
┌─────────────────────────────────────────────────────────────────┐
│                  COMMON STATISTICAL TESTS                       │
├──────────────┬──────────────────────────────────────────────────┤
│ Test Name    │ Purpose                                          │
├──────────────┼──────────────────────────────────────────────────┤
│ t-Test       │ Compare means of 2 groups (normal dist)          │
│ ANOVA        │ Compare means of >2 groups                       │
│ Chi-Square   │ Test independence of categorical variables       │
│ Mann-Whitney │ Non-parametric alternative to t-test             │
│ Kolmogorov   │ Compare distributions (KS test)                  │
│ F-Test       │ Compare variances                                  │
│ Pearson      │ Correlation coefficient                          │
└──────────────┴──────────────────────────────────────────────────┘
```

#### Example: A/B Testing

```python
from scipy import stats

# Simulate A/B test for conversion rates
n_users_a = 10000
n_users_b = 10000
conv_rate_a = 0.05
conv_rate_b = 0.055  # 10% improvement

# Generate binary outcomes
users_a = np.random.binomial(1, conv_rate_a, n_users_a)
users_b = np.random.binomial(1, conv_rate_b, n_users_b)

# Proportions
prop_a = np.mean(users_a)
prop_b = np.mean(users_b)

# Pooled proportion
p_pooled = (np.sum(users_a) + np.sum(users_b)) / (n_users_a + n_users_b)

# Standard error
se = np.sqrt(p_pooled * (1 - p_pooled) * (1/n_users_a + 1/n_users_b))

# Z-statistic
z_score = (prop_a - prop_b) / se

# Two-tailed p-value
p_value = 2 * (1 - stats.norm.cdf(abs(z_score)))

print("A/B Test Results:")
print(f"Group A Conversion: {prop_a:.4f}")
print(f"Group B Conversion: {prop_b:.4f}")
print(f"Z-Score: {z_score:.4f}")
print(f"p-value: {p_value:.4f}")

if p_value < 0.05:
    print("\n✓ Result is statistically significant (Reject Null)")
else:
    print("\n✗ Result not significant (Cannot reject Null)")
```

---

## 14. Chapter 12: Maximum Likelihood Estimation

### 📚 Principle of Maximum Likelihood

Find parameters that make the observed data most probable.

```
┌─────────────────────────────────────────────────────────────────┐
│              MAXIMUM LIKELIHOOD ESTIMATION (MLE)                │
│                                                                 │
│   Goal: Find θ that maximizes L(θ | Data)                     │
│                                                                 │
│   Likelihood Function:                                          │
│   ────────────────────                                          │
│   L(θ) = P(Data | θ) = ∏ᵢ P(xᵢ | θ)  (assuming IID)           │
│                                                                 │
│   Usually maximize Log-Likelihood:                              │
│   ℓ(θ) = log(L(θ)) = Σᵢ log P(xᵢ | θ)                         │
│                                                                 │
│   Find maximum: ∇ℓ(θ) = 0                                     │
│   Solve for θ̂ = argmax ℓ(θ)                                   │
│                                                                 │
│   ML Connection:                                                │
│   • Logistic Regression = MLE for Bernoulli                    │
│   • Linear Regression = MLE for Gaussian errors                │
│   • Neural Nets = MLE with Cross-Entropy                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import minimize

# Generate sample data from Gaussian
np.random.seed(42)
true_mu = 5.0
true_sigma = 2.0
data = np.random.normal(true_mu, true_sigma, 50)

# Negative log-likelihood function (to minimize)
def neg_log_likelihood(params, data):
    mu, sigma = params
    if sigma <= 0:
        return np.inf
    nll = 0.5 * len(data) * np.log(2 * np.pi * sigma**2) + \
          0.5 * np.sum(((data - mu) / sigma)**2)
    return nll

# Initial guess
initial_guess = [0.0, 1.0]

# Optimize
result = minimize(neg_log_likelihood, initial_guess, args=(data,), method='Nelder-Mead')

mle_mu = result.x[0]
mle_sigma = result.x[1]

print(f"True Mu: {true_mu}")
print(f"MLE Mu:  {mle_mu:.4f}")
print(f"True Sigma: {true_sigma}")
print(f"MLE Sigma:  {mle_sigma:.4f}")

# Plot likelihood surface
mu_range = np.linspace(3, 7, 50)
sigma_range = np.linspace(0.5, 4, 50)
X, Y = np.meshgrid(mu_range, sigma_range)
NLL = np.zeros_like(X)

for i in range(len(mu_range)):
    for j in range(len(sigma_range)):
        NLL[i, j] = neg_log_likelihood([mu_range[i], sigma_range[j]], data)

fig = plt.figure(figsize=(10, 5))
ax = fig.add_subplot(121)
contour = ax.contour(X, Y, NLL, levels=20)
ax.plot(mle_mu, mle_sigma, 'ro', markersize=10, label='MLE Point')
ax.plot(true_mu, true_sigma, 'gx', markersize=15, label='True Params')
ax.set_title('Log-Likelihood Surface')
ax.legend()

ax = fig.add_subplot(122)
ax.hist(data, bins=15, density=True, alpha=0.6, label='Data')
x_line = np.linspace(min(data), max(data), 100)
gaussian_pdf = 1/(mle_sigma*np.sqrt(2*np.pi)) * np.exp(-0.5*((x_line-mle_mu)/mle_sigma)**2)
ax.plot(x_line, gaussian_pdf, 'r-', linewidth=2, label=f'MLE Fit (μ={mle_mu:.2f}, σ={mle_sigma:.2f})')
ax.legend()

plt.tight_layout()
plt.show()
```

### 📚 Maximum A Posteriori (MAP)

Add prior to MLE.

```
┌─────────────────────────────────────────────────────────────────┐
│              MAXIMUM A POSTERIORI (MAP)                         │
│                                                                 │
│   MLE only uses data: P(Data | θ)                              │
│   MAP adds prior knowledge: P(θ | Data)                        │
│                                                                 │
│   Bayes' Theorem:                                               │
│   P(θ | Data) = P(Data | θ) × P(θ) / P(Data)                   │
│                                                                 │
│   Maximize:                                                     │
│   θ_MAP = argmax [P(Data | θ) × P(θ)]                          │
│   Take log:                                                     │
│   θ_MAP = argmax [log L(θ) + log P(θ)]                         │
│                                                                 │
│   Regularization Connection:                                    │
│   ────────────────────────────                                  │
│   • Gaussian Prior → Ridge Regression (L2 penalty)             │
│   • Laplace Prior → LASSO (L1 penalty)                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 15. Chapter 13: Bayesian Statistics

### 📚 Bayesian Philosophy

Unlike frequentist stats (parameters are fixed, data is random), Bayesian says:

```
┌─────────────────────────────────────────────────────────────────┐
│              FREQUENTIST vs BAYESIAN                            │
├──────────────┬──────────────────────────────────────────────────┤
│ Feature      │ Frequentist          │ Bayesian                 │
├──────────────┼──────────────────────────────────────────────────┤
│ Parameter    │ Fixed, unknown constant│ Random variable         │
│ Prior        │ None (implicit)       │ Explicit prior P(θ)      │
│ Output       │ Point estimate + CI   │ Posterior distribution   │
│ Uncertainty  │ Via data variability  │ Via posterior variance   │
│ Computation  │ Often analytic        │ Often requires MCMC      │
└──────────────┴──────────────────────────────────────────────────┘
```

### 📚 Bayesian Updating Cycle

```
┌─────────────────────────────────────────────────────────────────┐
│                BAYESIAN UPDATING CYCLE                          │
│                                                                 │
│   1. Prior P(θ): Belief before seeing data                     │
│                                                                 │
│   2. Likelihood P(Data | θ): Probability of data under param   │
│                                                                 │
│   3. Evidence P(Data): Normalizing constant                    │
│                                                                 │
│   4. Posterior P(θ | Data): Updated belief after seeing data   │
│                                                                 │
│   Cycle continues:                                              │
│   Posterior today = Prior tomorrow                              │
│                                                                 │
│   Conjugate Priors:                                             │
│   ────────────────────                                          │
│   • Beta Prior + Bernoulli Likelihood → Beta Posterior         │
│   • Gamma Prior + Poisson Likelihood → Gamma Posterior         │
│   • Normal Prior + Normal Likelihood → Normal Posterior        │
│   • Dirichlet + Categorical → Dirichlet                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import beta, binom

# Bayesian updating for Bernoulli parameter (coin bias)
# Prior: Beta(1, 1) = Uniform
alpha_prior, beta_prior = 1, 1

# Coin flip results (heads=success)
flips = [1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1]  # 9 heads, 4 tails

alpha_posterior = alpha_prior + np.sum(flips)
beta_posterior = beta_prior + len(flips) - np.sum(flips)

print(f"Prior: Beta(1, 1) - Mean = 0.5")
print(f"Posterior: Beta({alpha_posterior}, {beta_posterior}) - Mean = {alpha_posterior/(alpha_posterior+beta_posterior):.2f}")

# Plot prior vs posterior
x = np.linspace(0, 1, 100)
plt.figure(figsize=(10, 6))
plt.plot(x, beta.pdf(x, alpha_prior, beta_prior), 'b-', linewidth=2, label='Prior')
plt.plot(x, beta.pdf(x, alpha_posterior, beta_posterior), 'r-', linewidth=2, label='Posterior')
plt.fill_between(x, beta.pdf(x, alpha_posterior, beta_posterior), alpha=0.2, color='red')
plt.title('Bayesian Update: Prior vs Posterior')
plt.xlabel('Coin Bias (p)')
plt.ylabel('Density')
plt.legend()
plt.grid(True)
plt.show()
```

---

## 16. Chapter 14: Sampling Methods

### 📚 Monte Carlo Integration

Approximating integrals using random samples.

```
┌─────────────────────────────────────────────────────────────────┐
│                  MONTE CARLO METHOD                             │
│                                                                 │
│   Problem: Compute ∫_a^b f(x)dx when no closed form exists     │
│                                                                 │
│   Method:                                                       │
│   1. Sample points xᵢ ~ Uniform(a, b)                          │
│   2. Evaluate f(xᵢ)                                            │
│   3. Approximate integral: (b-a) × (1/N) Σ f(xᵢ)               │
│                                                                 │
│   Law of Large Numbers: Sample avg converges to true mean       │
│                                                                 │
│   Variance Reduces: O(1/√N) error                               │
│                                                                 │
│   ML Connection:                                                │
│   • Stochastic gradient descent (sample mini-batches)          │
│   • Dropout (randomly zero neurons)                            │
│   • Importance sampling                                        │
│   • Path planning (Monte Carlo Tree Search)                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Markov Chain Monte Carlo (MCMC)

Sampling from difficult distributions by building a chain.

```
┌─────────────────────────────────────────────────────────────────┐
│                MARKOV CHAIN MONTE CARLO (MCMC)                  │
│                                                                 │
│   Problem: Sample from P(θ|Data) when normalization unknown     │
│                                                                 │
│   Solution: Build Markov chain whose stationary distribution    │
│   is P(θ|Data). Then burn-in period, collect samples later.    │
│                                                                 │
│   Metropolis-Hastings Algorithm:                                │
│   1. Propose candidate θ' from q(θ'|θ_current)                 │
│   2. Accept/reject based on ratio:                             │
│      min(1, [P(θ')q(θ|θ')] / [P(θ)q(θ'|θ)])                   │
│                                                                 │
│   Gibbs Sampling: Special case of M-H                           │
│   1. Update each variable conditioned on others                │
│                                                                 │
│   ML Connection:                                                │
│   • Bayesian Neural Networks                                    │
│   • Topic Modeling (Latent Dirichlet Allocation)               │
│   • Variational Inference comparisons                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 17. Chapter 15: Probability in Machine Learning

### 📚 Generative Models

Models that learn P(Data).

```
┌─────────────────────────────────────────────────────────────────┐
│              GENERATIVE VS DISCRIMINATIVE MODELS                │
├──────────────┬──────────────────────────────────────────────────┤
│ Model Type   │ Learns P(Feature | Label) OR P(Feature, Label)?  │
├──────────────┼──────────────────────────────────────────────────┤
│ Discriminative│ P(Label | Feature) – Class boundaries         │
│ e.g.: LR, SVM, RF, MLP    │ Direct classification             │
├──────────────┼──────────────────────────────────────────────────┤
│ Generative    │ P(Feature, Label) = P(Feature | Label)P(Label)│
│ e.g.: Naive Bayes, GMM, VAE, GAN │ Samples new data possible  │
└──────────────┴──────────────────────────────────────────────────┘
```

### 📚 Probabilistic Neural Networks

Neural networks outputting distributions instead of points.

```
┌─────────────────────────────────────────────────────────────────┐
│           PROBABILISTIC NEURAL NETWORK OUTPUTS                  │
│                                                                 │
│   Deterministic NN:                                             │
│   Input → NN → Output = Scalar/Vector                          │
│                                                                 │
│   Probabilistic NN:                                             │
│   Input → NN → Parameters of Distribution                      │
│   Example: Output = {μ, σ} (Predict Normal Distribution)       │
│                                                                 │
│   Benefits:                                                     │
│   • Uncertainty Quantification                                 │
│   • Better generalization under distribution shift             │
│   • Active learning queries (query where uncertain)            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 18. Chapter 16: Advanced Topics

### 📚 Gaussian Processes

Non-parametric Bayesian approach for regression.

```
┌─────────────────────────────────────────────────────────────────┐
│                  GAUSSIAN PROCESSES                             │
│                                                                 │
│   Concept: Distribution over FUNCTIONS                          │
│                                                                 │
│   Instead of learning weights: Learn Kernel K(x, x')           │
│   Measure similarity between inputs.                           │
│                                                                 │
│   Prior:                                                        │
│   f(x) ~ GP(0, k(x, x'))                                       │
│                                                                 │
│   Prediction:                                                   │
│   • Mean: Predicted value                                      │
│   • Variance: Uncertainty at point                             │
│                                                                 │
│   Pros:                                                         │
│   • Naturally handles uncertainty                              │
│   • Works well with small data                                 │
│   • No need for large datasets                                 │
│                                                                 │
│   Cons:                                                         │
│   • Scaling: O(N³) computation                                 │
│   • Harder to interpret than simple models                     │
│                                                                 │
│   Use cases:                                                    │
│   • Hyperparameter optimization (Bayesian Opt)                 │
│   • Small-data scenarios                                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Latent Variable Models

Modeling hidden structure.

```
┌─────────────────────────────────────────────────────────────────┐
│              LATENT VARIABLE MODELS                             │
├──────────────┬──────────────────────────────────────────────────┤
│ Model        │ Mechanism                                        │
├──────────────┼──────────────────────────────────────────────────┤
│ PCA          │ Latent space = orthogonal projections            │
│ LDA          │ Latent topics generate documents                 │
│ VAE          │ Latent vectors sampled from Gaussian             │
│ Factor Analysis │ Hidden factors drive observations          │
└──────────────┴──────────────────────────────────────────────────┘
```

---

## 19. Practice Problems

### Problem Set 1: Foundations

```
┌─────────────────────────────────────────────────────────────────┐
│                    PRACTICE PROBLEMS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. PROBABILITY CALCULATIONS                                   │
│   • In a deck of cards, what is P(drawing Ace or Heart)?        │
│                                                                 │
│   2. CONDITIONAL PROBABILITY                                    │
│   • P(Fire Alarm | Smoke) vs P(Smoke | Fire Alarm) - Which is  │
│     bigger? Explain intuitively.                                │
│                                                                 │
│   3. RANDOM VARIABLES                                           │
│   • X ~ Uniform(0, 1). What is E[e^X]?                          │
│                                                                 │
│   4. INFERENCE                                                  │
│   • If I draw 100 balls with replacement and observe 60 red,   │
│     construct a 95% confidence interval for proportion red.    │
│                                                                 │
│   5. EXPECTATION                                                │
│   • Roll a fair die. You get paid $x if you roll x dollars.    │
│     What is expected value? Would you pay $4 to play?          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Problem Set 2: ML Applications

```
┌─────────────────────────────────────────────────────────────────┐
│                  ML APPLICATION PROBLEMS                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   6. CROSS-ENTROPY LOSS                                         │
│   • Given true class one-hot vector [0, 0, 1] and pred probs    │
│     [0.2, 0.3, 0.5], compute cross-entropy loss.                │
│                                                                 │
│   7. ENTROPY                                                    │
│   • Calculate entropy for classifier predictions:               │
│     Class probabilities: [0.9, 0.05, 0.05]. Is the model unsure?│
│                                                                 │
│   8. CONJUGATE PRIORS                                           │
│   • If prior for coin bias is Beta(2, 2) and we flip 1 head,   │
│     update to posterior.                                       │
│                                                                 │
│   9. CLT SIMULATION                                             │
│   • Write Python code to demonstrate CLT using exponential dist.│
│                                                                 │
│   10. GAUSSIAN PROCESS INTUITION                                │
│   • If you have a GP with RBF kernel, what does high noise     │
│     parameter (length-scale) imply about the function?         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 20. Cheat Sheet

```
┌─────────────────────────────────────────────────────────────────┐
│             PROBABILITY & STATISTICS CHEAT SHEET                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   PROBABILITY RULES:                                            │
│   ──────────────────                                            │
│   P(A∪B) = P(A)+P(B)-P(A∩B)                                    │
│   P(A|B) = P(A∩B)/P(B)                                         │
│   Bayes: P(A|B) = P(B|A)P(A)/P(B)                              │
│                                                                 │
│   DISTRIBUTIONS KEY PARAMETERS:                                 │
│   ───────────────────────────────                               │
│   Binomial: Mean=np, Var=np(1-p)                               │
│   Normal: Mean=μ, Var=σ²                                       │
│   Poisson: Mean=λ, Var=λ                                       │
│   Bernoulli: Mean=p, Var=p(1-p)                                │
│   Gamma: Mean=α/β, Var=α/β²                                    │
│   Beta: Mean=α/(α+β), Var=complex                              │
│                                                                 │
│   INFO THEORY:                                                  │
│   ────────────                                                  │
│   H(X) = -Σ p log p                                            │
│   D_KL(P||Q) = Σ p log(p/q) ≥ 0                                │
│   CE_loss = -Σ y_true log(y_pred)                              │
│                                                                 │
│   STATS FORMULAS:                                               │
│   ────────────────                                              │
│   E[X] = Σ x p(x) or ∫ xf(x)dx                                │
│   Var(X) = E[X²] - E[X]²                                       │
│   Cov(X,Y) = E[XY] - E[X]E[Y]                                  │
│   Corr(X,Y) = Cov(X,Y)/(σₓσᵧ)                                  │
│                                                                 │
│   ML LOSS CONNECTIONS:                                          │
│   ─────────────────────                                         │
│   MSE ↔ Normal Likelihood                                      │
│   CrossEntropy ↔ Bernoulli/Cat Likelihood                      │
│   Huber ↔ Laplace Likelihood                                   │
│   Weight Decay ↔ Gaussian Prior (MAP)                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 21. Resources

### 📚 Books

```
1. "Introduction to Probability" - Blitzstein & Hwang
   - Excellent intuition, free online

2. "Pattern Recognition and Machine Learning" - Bishop
   - Chapter 1-3 are foundational for ML

3. "Statistical Inference" - Casella & Berger
   - Rigorous statistical theory

4. "Machine Learning: A Probabilistic Perspective" - Murphy
   - Bridge between probability and ML

5. "Think Bayes" - Allen Downey
   - Practical Bayesian computing
```

### 🎓 Courses

```
1. MIT 6.041 Probabilistic Systems Analysis (OCW)
   - Classic calculus-based probability course

2. Stanford CS229 - Machine Learning
   - Statistical perspective on ML

3. Berkeley CS188 - Introduction to AI
   - Probabilistic graphical models
```

### 🛠 Libraries

```
Python:
- numpy: Array operations, random generators
- scipy.stats: All major distributions & tests
- sklearn.preprocessing: Statistical transforms
- pymc3/pymc: Bayesian modeling
- arviz: Bayesian diagnostics
```

---

## 22. Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                KEY TAKEAWAYS - PROBABILITY                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. ML IS PROBABILISTIC                                        │
│      Every model estimates a distribution, not certainty       │
│                                                                 │
│   2. BAYES IS ESSENTIAL                                         │
│      P(Posterior) = Likelihood × Prior                         │
│      Foundation for all generative methods                     │
│                                                                 │
│   3. DISTRIBUTIONS MATTER                                       │
│      Gaussian is everywhere (thanks to CLT)                    │
│      Understand PMF vs PDF                                     │
│                                                                 │
│   4. INFORMATION = UNCERTAINTY REDUCTION                        │
│      Entropy measures unpredictability                         │
│      Cross-entropy measures prediction error                   │
│                                                                 │
│   5. INFERENCE NEEDS DATA                                       │
│      Sample means converge to true means (CLT)                 │
│      Larger samples = tighter confidence intervals             │
│                                                                 │
│   6. REGULARIZATION IS PRIORS                                   │
│      L2 ↔ Gaussian Prior, L1 ↔ Laplace Prior                   │
│      MAP = MLE + Prior Knowledge                               │
│                                                                 │
│   7. SIMULATE TO LEARN                                        │
│      Monte Carlo makes abstract concrete                       │
│      Visualize distributions whenever possible                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

*End of Probability & Statistics Module for AIML*