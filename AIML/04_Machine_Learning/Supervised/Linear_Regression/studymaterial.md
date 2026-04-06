Linear Regression: The Complete Masterclass
From Zero to Hero | A 15-Year Professor's Definitive Guide
📚 TABLE OF CONTENTS
Chapter 1: The Foundation - What is Linear Regression?
Chapter 2: The Mathematics Behind the Magic
Chapter 3: Simple Linear Regression - Deep Dive
Chapter 4: Multiple Linear Regression
Chapter 5: Assumptions of Linear Regression
Chapter 6: Model Evaluation Metrics
Chapter 7: Feature Engineering & Selection
Chapter 8: Regularization Techniques
Chapter 9: Polynomial Regression
Chapter 10: Gradient Descent - The Optimization Engine
Chapter 11: Common Problems & Solutions
Chapter 12: Implementation from Scratch
Chapter 13: Real-World Applications
Chapter 14: Interview Questions & Answers
Chapter 15: Advanced Topics & Research Directions
Chapter 1: The Foundation - What is Linear Regression? {#chapter-1-the-foundation}
1.1 The Simplest Explanation Ever
Imagine you're a parent tracking your child's height over the years:

Age (Years)	Height (cm)
5	110
6	116
7	122
8	128
9	134
Question: What will be the height at age 10?

Your Brain's Answer: Around 140 cm (you naturally see the pattern!)

What You Just Did: Linear Regression! 🎉

Linear Regression is simply finding the best straight line that represents the relationship between variables, so you can make predictions.

1.2 Breaking Down the Term
text

LINEAR      +      REGRESSION
   ↓                    ↓
Straight Line    Going back to find
                 the average relationship
Why "Linear"?
We're fitting a straight line (not curves, not zigzags)
The relationship is proportional (when X increases, Y changes proportionally)
Why "Regression"?
The term was coined by Sir Francis Galton in 1886
He studied heights of fathers and sons
Tall fathers had sons who were tall, but "regressed" toward average
The name stuck!
1.3 The Big Picture
text

┌─────────────────────────────────────────────────────────────┐
│                    MACHINE LEARNING                         │
│  ┌─────────────────────┐    ┌─────────────────────┐        │
│  │   SUPERVISED        │    │   UNSUPERVISED      │        │
│  │  ┌───────────────┐  │    │                     │        │
│  │  │ REGRESSION    │  │    │  • Clustering       │        │
│  │  │ ┌───────────┐ │  │    │  • Dimensionality   │        │
│  │  │ │ LINEAR    │ │  │    │    Reduction        │        │
│  │  │ │REGRESSION │ │  │    │                     │        │
│  │  │ │  ⭐ HERE! │ │  │    │                     │        │
│  │  │ └───────────┘ │  │    │                     │        │
│  │  │ • Polynomial  │  │    │                     │        │
│  │  │ • Decision    │  │    │                     │        │
│  │  │   Tree Reg.   │  │    │                     │        │
│  │  └───────────────┘  │    │                     │        │
│  │  ┌───────────────┐  │    │                     │        │
│  │  │CLASSIFICATION │  │    │                     │        │
│  │  └───────────────┘  │    │                     │        │
│  └─────────────────────┘    └─────────────────────┘        │
└─────────────────────────────────────────────────────────────┘
1.4 Types of Variables
text

┌─────────────────────────────────────────────────┐
│                                                 │
│   INDEPENDENT VARIABLE(S)  →  DEPENDENT VARIABLE│
│         (Input/X)                (Output/Y)     │
│        (Features)               (Target)        │
│       (Predictors)              (Response)      │
│                                                 │
│   Example:                                      │
│   Study Hours (X)     →     Exam Score (Y)     │
│   House Size (X)      →     House Price (Y)    │
│                                                 │
└─────────────────────────────────────────────────┘
Memory Trick 🧠
Independent (X): What you CONTROL or KNOW first
Dependent (Y): What DEPENDS on X, what you PREDICT
1.5 When to Use Linear Regression?
✅ USE IT WHEN:
Scenario	Example
Predicting continuous numbers	House prices, temperatures, sales
Relationship looks linear	Scatter plot shows straight-ish pattern
Understanding variable relationships	How much does X affect Y?
You need interpretable results	"Each year of experience adds $5000 salary"
❌ DON'T USE IT WHEN:
Scenario	Better Alternative
Predicting categories (Yes/No)	Logistic Regression
Complex curved relationships	Polynomial/Non-linear models
Data has outliers everywhere	Robust Regression
Features > Samples significantly	Regularized methods
1.6 Real-World Examples
Example 1: Predicting House Prices
text

Features (X):                    Target (Y):
├── Square footage              └── Price ($)
├── Number of bedrooms
├── Age of house
└── Distance to city center
Example 2: Salary Prediction
text

Features (X):                    Target (Y):
├── Years of experience         └── Annual Salary ($)
├── Education level
├── Skills count
└── Location
Example 3: Sales Forecasting
text

Features (X):                    Target (Y):
├── Advertising spend           └── Sales Revenue ($)
├── Season/Month
├── Competitor prices
└── Economic indicators
Chapter 2: The Mathematics Behind the Magic {#chapter-2-the-mathematics}
2.1 The Equation of a Line - Your New Best Friend
Remember middle school math?

text

y = mx + c

Where:
• y = dependent variable (what we predict)
• x = independent variable (what we know)
• m = slope (steepness of line)
• c = intercept (where line crosses y-axis)
In Machine Learning, we write it as:

text

ŷ = β₀ + β₁x

Where:
• ŷ (y-hat) = predicted value
• β₀ (beta-zero) = y-intercept
• β₁ (beta-one) = slope/coefficient
• x = input feature
2.2 Understanding Slope (β₁)
text

POSITIVE SLOPE              NEGATIVE SLOPE           ZERO SLOPE
      ↗                          ↘                      →
     /                            \                   ─────
    /                              \
   /                                \
  
X↑ means Y↑                X↑ means Y↓           X changes, Y same
Example:                   Example:              Example:
More study = Better grade  More age = Less speed Shirt color vs Height
Interpreting Slope Value
Slope (β₁)	Meaning
β₁ = 2	For each 1 unit increase in X, Y increases by 2 units
β₁ = -0.5	For each 1 unit increase in X, Y decreases by 0.5 units
β₁ = 0	X has NO effect on Y
2.3 Understanding Intercept (β₀)
text

Y-axis
  │
  │     /
  │    /
  │   /
β₀├──●        ← This point is the intercept
  │ /            (where line meets Y-axis when X=0)
  │/
  └──────────── X-axis
Real Example:

Predicting salary based on experience
β₀ = $30,000 means: A person with 0 years experience earns $30,000 (base salary)
β₁ = $5,000 means: Each year adds $5,000
Salary = $30,000 + $5,000 × (Years of Experience)

2.4 The Goal: Finding the Best Line
Given data points, infinite lines can pass through/near them:

text

        │  Line A      
    y   │    ╱   Line B
        │   ╱   ╱
        │  ╱   ╱
        │ ● ╱ ●
        │╱ ● 
        ●    ● 
        └────────────── x
        
Which line is BEST?
Answer: The line that minimizes total "error" between predictions and actual values!

2.5 What is Error/Residual?
text

    y   │
        │       ● Actual Point (yᵢ)
        │       │
        │       │ ← Error (residual) = yᵢ - ŷᵢ
        │       │
        │       ▼
        │-------●---- Predicted Point (ŷᵢ) on line
        │      /
        │     /
        │    /
        │   /
        └────────────── x
Error (Residual) = Actual Value - Predicted Value

text

eᵢ = yᵢ - ŷᵢ
2.6 Sum of Squared Errors (SSE) - The Cost Function
Why squared? Let's see:

Problem with Simple Sum:
text

Errors:  +5, -5, +3, -3
Sum:     +5 + (-5) + 3 + (-3) = 0  ← WRONG! We had errors!
Solution - Square the Errors:
text

Squared Errors:  25, 25, 9, 9
Sum:             25 + 25 + 9 + 9 = 68  ← CORRECT! Captures all errors!
The Formula:
text

SSE = Σ(yᵢ - ŷᵢ)² = Σ(yᵢ - (β₀ + β₁xᵢ))²

Where:
• Σ = sum over all data points
• yᵢ = actual value of ith point
• ŷᵢ = predicted value of ith point
• n = number of data points
2.7 Ordinary Least Squares (OLS) - Finding β₀ and β₁
Goal: Find β₀ and β₁ that MINIMIZE SSE

Method: Take derivatives, set to zero, solve!

The Derivation (Step by Step):
Step 1: Write the cost function

text

J(β₀, β₁) = Σ(yᵢ - β₀ - β₁xᵢ)²
Step 2: Take partial derivative with respect to β₀

text

∂J/∂β₀ = -2Σ(yᵢ - β₀ - β₁xᵢ) = 0
Step 3: Take partial derivative with respect to β₁

text

∂J/∂β₁ = -2Σxᵢ(yᵢ - β₀ - β₁xᵢ) = 0
Step 4: Solve the system of equations

The Final Formulas:
text

        Σ(xᵢ - x̄)(yᵢ - ȳ)       Cov(x,y)
β₁ = ─────────────────────── = ──────────
           Σ(xᵢ - x̄)²           Var(x)


β₀ = ȳ - β₁x̄

Where:
• x̄ = mean of x values
• ȳ = mean of y values
• Cov(x,y) = covariance between x and y
• Var(x) = variance of x
2.8 Visual Summary of OLS
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│    DATA POINTS                    BEST FIT LINE             │
│         ●                              /                    │
│       ●   ●                         ● /                     │
│     ●   ●   ●        ──────►      ●──/──●                  │
│       ●   ●                      ●  /  ●                    │
│         ●                          /●                       │
│                                                             │
│    Given: (x₁,y₁), (x₂,y₂)...    Found: ŷ = β₀ + β₁x       │
│                                                             │
│    OLS finds β₀ and β₁ that minimize Σ(yᵢ - ŷᵢ)²           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Chapter 3: Simple Linear Regression - Deep Dive {#chapter-3-simple-linear-regression}
3.1 Definition
Simple Linear Regression = ONE independent variable predicting ONE dependent variable

text

ŷ = β₀ + β₁x
     ↑     ↑
  intercept slope
     
Only ONE x variable!
3.2 Complete Worked Example
The Dataset: Study Hours vs. Exam Scores
Student	Study Hours (X)	Exam Score (Y)
1	1	52
2	2	55
3	3	60
4	4	62
5	5	68
6	6	70
7	7	75
8	8	80
Step 1: Calculate Means
text

x̄ = (1+2+3+4+5+6+7+8)/8 = 36/8 = 4.5
ȳ = (52+55+60+62+68+70+75+80)/8 = 522/8 = 65.25
Step 2: Calculate Components for β₁
xᵢ	yᵢ	xᵢ - x̄	yᵢ - ȳ	(xᵢ-x̄)(yᵢ-ȳ)	(xᵢ-x̄)²
1	52	-3.5	-13.25	46.375	12.25
2	55	-2.5	-10.25	25.625	6.25
3	60	-1.5	-5.25	7.875	2.25
4	62	-0.5	-3.25	1.625	0.25
5	68	0.5	2.75	1.375	0.25
6	70	1.5	4.75	7.125	2.25
7	75	2.5	9.75	24.375	6.25
8	80	3.5	14.75	51.625	12.25
Sum:	166.0	42.0
Step 3: Calculate β₁ (Slope)
text

β₁ = Σ(xᵢ - x̄)(yᵢ - ȳ) / Σ(xᵢ - x̄)²
β₁ = 166.0 / 42.0
β₁ = 3.952 ≈ 3.95
Interpretation: Each additional hour of study increases exam score by ~4 points!

Step 4: Calculate β₀ (Intercept)
text

β₀ = ȳ - β₁x̄
β₀ = 65.25 - (3.952 × 4.5)
β₀ = 65.25 - 17.786
β₀ = 47.464 ≈ 47.46
Interpretation: A student with 0 study hours would score ~47.5 (baseline score)

Step 5: The Final Model
text

┌──────────────────────────────────────┐
│                                      │
│   Exam Score = 47.46 + 3.95 × Hours  │
│                                      │
└──────────────────────────────────────┘
Step 6: Make Predictions
Q: What score for 5.5 hours of study?

text

ŷ = 47.46 + 3.95 × 5.5
ŷ = 47.46 + 21.725
ŷ = 69.185 ≈ 69
Visualizing Our Model
text

Score
  90│                           ●
    │                        ●
  80│                     ●/
    │                   /●
  70│                ●/
    │             /●
  60│          ●/
    │       /●
  50│    ●/
    │  /
  40│/β₀ = 47.46
    │
    └─────────────────────────────── Hours
     0  1  2  3  4  5  6  7  8  9
     
Line equation: ŷ = 47.46 + 3.95x
3.3 Key Properties of Simple Linear Regression
Property 1: The Regression Line Passes Through (x̄, ȳ)
text

ŷ = β₀ + β₁x̄
ŷ = (ȳ - β₁x̄) + β₁x̄
ŷ = ȳ  ✓

The line ALWAYS passes through the point of means!
Property 2: Sum of Residuals = 0
text

Σ(yᵢ - ŷᵢ) = 0

Positive and negative residuals cancel out perfectly!
Property 3: Residuals Are Uncorrelated with Predictions
text

Σ(ŷᵢ × eᵢ) = 0

Where eᵢ = yᵢ - ŷᵢ (residuals)
Chapter 4: Multiple Linear Regression {#chapter-4-multiple-linear-regression}
4.1 Extending to Multiple Variables
Simple: One X → One Y
Multiple: Many X's → One Y

text

SIMPLE LINEAR REGRESSION:
ŷ = β₀ + β₁x

MULTIPLE LINEAR REGRESSION:
ŷ = β₀ + β₁x₁ + β₂x₂ + β₃x₃ + ... + βₙxₙ
4.2 The Matrix Form (Essential for Understanding)
Scalar Form:
text

ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ
Matrix Form:
text

ŷ = Xβ

Where:
• ŷ is (m × 1) vector of predictions
• X is (m × n+1) matrix of features (with column of 1s for intercept)
• β is (n+1 × 1) vector of coefficients
Visual Representation:
text

┌     ┐   ┌                         ┐   ┌    ┐
│ ŷ₁  │   │ 1   x₁₁   x₁₂  ...  x₁ₙ │   │ β₀ │
│ ŷ₂  │   │ 1   x₂₁   x₂₂  ...  x₂ₙ │   │ β₁ │
│ ŷ₃  │ = │ 1   x₃₁   x₃₂  ...  x₃ₙ │ × │ β₂ │
│ ... │   │ ... ...   ...  ...  ... │   │... │
│ ŷₘ  │   │ 1   xₘ₁   xₘ₂  ...  xₘₙ │   │ βₙ │
└     ┘   └                         ┘   └    ┘
 (m×1)              (m×n+1)             (n+1×1)
4.3 The Normal Equation
To find optimal β:

text

β = (XᵀX)⁻¹Xᵀy

Where:
• Xᵀ = transpose of X
• ⁻¹ = matrix inverse
• y = actual target values
Derivation:
text

Step 1: Cost function in matrix form
        J(β) = (y - Xβ)ᵀ(y - Xβ)

Step 2: Expand
        J(β) = yᵀy - 2βᵀXᵀy + βᵀXᵀXβ

Step 3: Take derivative with respect to β
        ∂J/∂β = -2Xᵀy + 2XᵀXβ

Step 4: Set to zero and solve
        XᵀXβ = Xᵀy
        β = (XᵀX)⁻¹Xᵀy  ✓
4.4 Complete Example: House Price Prediction
Dataset:
House	Size (sqft)	Bedrooms	Age (years)	Price ($1000s)
1	1400	3	10	245
2	1600	3	8	312
3	1700	4	5	279
4	1875	4	3	308
5	1100	2	15	199
6	1550	3	12	219
Setting Up Matrices:
text

X (Design Matrix with 1s column):        y (Target):
┌                         ┐              ┌     ┐
│ 1   1400   3    10     │              │ 245 │
│ 1   1600   3    8      │              │ 312 │
│ 1   1700   4    5      │              │ 279 │
│ 1   1875   4    3      │              │ 308 │
│ 1   1100   2    15     │              │ 199 │
│ 1   1550   3    12     │              │ 219 │
└                         ┘              └     ┘
Computing β (Using Normal Equation):
After matrix calculations:

text

β₀ = 89.12    (base price)
β₁ = 0.109   (price per sqft)
β₂ = 12.45   (price per bedroom)
β₃ = -3.21   (price reduction per year of age)
The Final Model:
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Price = 89.12 + 0.109×Size + 12.45×Bedrooms - 3.21×Age    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Interpretation:
Coefficient	Value	Interpretation
β₀ = 89.12	Base Price	Starting price (theoretical)
β₁ = 0.109	Per sqft	Each sqft adds $109 to price
β₂ = 12.45	Per bedroom	Each bedroom adds $12,450
β₃ = -3.21	Per year	Each year old reduces price by $3,210
Making a Prediction:
Predict price for: 1500 sqft, 3 bedrooms, 6 years old

text

Price = 89.12 + 0.109(1500) + 12.45(3) - 3.21(6)
Price = 89.12 + 163.5 + 37.35 - 19.26
Price = $270,710
4.5 When Normal Equation Fails
Problem: XᵀX is Singular (Non-Invertible)
Causes:

Multicollinearity: Features are linearly dependent
More features than samples: n > m
Duplicate features: Redundant columns
Solutions:

Remove correlated features
Use regularization (Ridge, Lasso)
Use Gradient Descent instead
Use pseudo-inverse (Moore-Penrose)
text

Instead of: β = (XᵀX)⁻¹Xᵀy
Use:        β = (XᵀX + λI)⁻¹Xᵀy  (Ridge regression)
Chapter 5: Assumptions of Linear Regression {#chapter-5-assumptions}
5.1 The Five Critical Assumptions
Linear Regression is built on these assumptions. Violate them, and your model may give misleading results!

text

┌─────────────────────────────────────────────────────────────┐
│          THE 5 ASSUMPTIONS (L.I.N.E.R)                      │
│                                                             │
│  L - Linearity                                              │
│  I - Independence                                           │
│  N - Normality (of residuals)                               │
│  E - Equal Variance (Homoscedasticity)                      │
│  R - No multicollinearity (for multiple regression)         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
5.2 Assumption 1: Linearity
What It Means:
The relationship between X and Y should be LINEAR (straight line, not curved).

How to Check:
text

GOOD (Linear):                    BAD (Non-Linear):
    │    ●  ●                         │        ●●●
    │  ●   ●                          │      ●    ●
    │ ●  ●                            │    ●       ●
    │●  ●                             │  ●          ●
    │ ●                               │●●
    └──────────                       └──────────────
    Scatter plot shows                 Scatter plot shows
    linear pattern                     curved pattern
Tests:
Visual: Scatter plot of X vs Y
Residual Plot: Plot residuals vs predicted values (should be random)
Rainbow Test: Statistical test for linearity
If Violated:
Try polynomial regression
Apply transformations (log, sqrt, etc.)
Use non-linear models
5.3 Assumption 2: Independence
What It Means:
Each observation should be independent of others. The error for one data point shouldn't depend on another.

Common Violations:
Time Series Data: Today's stock price depends on yesterday's
Grouped Data: Students in same class may have correlated scores
Spatial Data: Neighboring locations have similar values
How to Check:
text

GOOD (Independent):               BAD (Autocorrelated):
Residuals                         Residuals
    │ ●   ●  ●   ●                   │ ●●●
    │   ●   ●   ●                    │      ●●●
    │  ●  ●   ●                      │          ●●●
    │●    ●     ●                    │              ●●
    └──────────────                  └──────────────────
    Time/Order                       Time/Order
    Random pattern                   Pattern exists (BAD!)
Tests:
Durbin-Watson Test: Tests for autocorrelation
Value near 2: No autocorrelation ✓
Value near 0: Positive autocorrelation ✗
Value near 4: Negative autocorrelation ✗
If Violated:
Use time-series models (ARIMA)
Add lagged variables
Use mixed-effects models for grouped data
5.4 Assumption 3: Normality of Residuals
What It Means:
The residuals (errors) should follow a Normal (Gaussian) distribution.

text

                    ┌───┐
                   ╱     ╲
                  ╱       ╲
                 ╱         ╲
               ╱             ╲
             ╱                 ╲
        ────╱───────────────────╲────
            -2σ  -1σ   0   1σ   2σ
            
Residuals should form this bell curve
How to Check:
1. Histogram of Residuals:

text

GOOD:                           BAD:
Frequency                       Frequency
    │   ████                        │ ██████
    │  ██████                       │ ████
    │ ████████                      │ ██
    │██████████                     │ ██    ██
    │████████████                   │ ████████
    └──────────────                 └──────────────
    Residual Value                  Residual Value
    Bell-shaped                     Skewed
2. Q-Q Plot (Quantile-Quantile):

text

Expected                        Expected
    │      ●●●●●                    │    ●●●●●
    │   ●●●                         │●●●      ●
    │●●●                            │           ●
    └──────────                     └──────────────
    Observed                        Observed
    GOOD: Points on line            BAD: Deviates from line
Tests:
Shapiro-Wilk Test: p-value > 0.05 means normal ✓
Kolmogorov-Smirnov Test: Compares distribution to normal
Jarque-Bera Test: Checks skewness and kurtosis
If Violated:
Transform Y (log, Box-Cox)
Remove outliers
Use robust regression
Note: With large samples (n > 30), this is less critical due to Central Limit Theorem
5.5 Assumption 4: Homoscedasticity (Equal Variance)
What It Means:
The variance of residuals should be constant across all levels of X.

text

GOOD (Homoscedasticity):         BAD (Heteroscedasticity):
Residuals                        Residuals
    │  ●   ●    ●    ●               │             ●●●
    │ ● ● ● ●● ● ● ●                 │        ●  ●  ●
────┼─●─●─●─●─●──●─●─●─●──           │    ● ●  ●
    │● ●   ●  ●  ●   ●               │  ● ●
    │   ●   ●     ●                  │●●
    └──────────────────              └──────────────────
    Predicted Values                 Predicted Values
    Constant spread                  Spread increases (funnel)
Tests:
Breusch-Pagan Test: p-value < 0.05 indicates heteroscedasticity
White's Test: More general test
Goldfeld-Quandt Test: Compares variance in different segments
If Violated:
Transform Y (log transformation often helps)
Use Weighted Least Squares (WLS)
Use robust standard errors
Consider Generalized Least Squares (GLS)
5.6 Assumption 5: No Multicollinearity
What It Means:
Independent variables should NOT be highly correlated with each other.

Why It's a Problem:
text

If X₁ ≈ X₂:

Model: ŷ = β₀ + β₁X₁ + β₂X₂

Problem: Can't tell if Y changes due to X₁ or X₂!

The coefficients become unstable:
- Large standard errors
- Coefficients may flip signs
- Model becomes unreliable for interpretation
How to Detect:
1. Correlation Matrix:

text

         X₁     X₂     X₃
X₁      1.00   0.95   0.15
X₂      0.95   1.00   0.20
X₃      0.15   0.20   1.00

X₁ and X₂ correlation = 0.95 → PROBLEM!
2. Variance Inflation Factor (VIF):

text

VIF = 1 / (1 - R²ⱼ)

Where R²ⱼ is R² from regressing Xⱼ on all other X variables

Interpretation:
• VIF = 1: No multicollinearity ✓
• VIF 1-5: Moderate (usually acceptable)
• VIF 5-10: High (concerning)
• VIF > 10: Severe (must address!)
If Violated:
Remove one of the correlated variables
Combine correlated variables (create index)
Use Principal Component Analysis (PCA)
Use Ridge Regression (L2 regularization)
5.7 Summary Table
Assumption	What to Check	Test/Method	If Violated
Linearity	X vs Y scatter	Residual plot, Rainbow test	Transform variables, polynomial
Independence	Residuals over time	Durbin-Watson	Time-series models, lagged vars
Normality	Distribution of residuals	Q-Q plot, Shapiro-Wilk	Transform Y, robust methods
Homoscedasticity	Residual spread	Breusch-Pagan	WLS, transform Y, robust SE
No Multicollinearity	Correlation between X's	VIF, correlation matrix	Remove/combine variables, Ridge
Chapter 6: Model Evaluation Metrics {#chapter-6-model-evaluation}
6.1 Why Evaluate?
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   "A model is only as good as its ability to be WRONG      │
│    in predictable, measurable ways."                        │
│                                                             │
│   We need metrics to:                                       │
│   • Know if our model is good or bad                        │
│   • Compare different models                                │
│   • Improve our model                                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
6.2 The Metrics Family
text

                    EVALUATION METRICS
                           │
           ┌───────────────┼───────────────┐
           │               │               │
      ERROR BASED    VARIANCE BASED   COMPARISON
           │               │            BASED
    ┌──────┼──────┐        │               │
    │      │      │        │               │
   MAE    MSE   RMSE      R²          Adjusted R²
                          │               │
                      RSS/TSS/ESS         │
                                     AIC/BIC
6.3 Mean Absolute Error (MAE)
Formula:
text

        1   n
MAE = ─── Σ |yᵢ - ŷᵢ|
        n  i=1
Visual:
text

    │
    │       ● yᵢ
    │       │
    │       │ |yᵢ - ŷᵢ| = Absolute Error
    │       │
    │       ▼
    │-------●---- ŷᵢ (predicted)
    │
    
MAE = Average of all these absolute differences
Characteristics:
Property	Description
Units	Same as Y
Range	[0, ∞)
Interpretation	Average prediction error in original units
Outlier Sensitivity	Less sensitive (uses absolute value)
Differentiable	No (at 0) - problem for some optimization
Example:
text

Actual:    [100, 150, 200, 180]
Predicted: [110, 145, 210, 175]
Errors:    [10,  5,   10,  5]
MAE = (10 + 5 + 10 + 5) / 4 = 7.5

"On average, predictions are off by 7.5 units"
6.4 Mean Squared Error (MSE)
Formula:
text

        1   n
MSE = ─── Σ (yᵢ - ŷᵢ)²
        n  i=1
Characteristics:
Property	Description
Units	Y² (squared units)
Range	[0, ∞)
Interpretation	Average squared error
Outlier Sensitivity	HIGH (squares the error)
Differentiable	Yes - good for optimization
Example:
text

Actual:    [100, 150, 200, 180]
Predicted: [110, 145, 210, 175]
Errors:    [10,  5,   10,  5]
Squared:   [100, 25,  100, 25]
MSE = (100 + 25 + 100 + 25) / 4 = 62.5

Units are "dollars squared" if predicting dollars - not intuitive!
Why Use MSE?
Mathematically convenient (differentiable)
Penalizes large errors more
Used in optimization (gradient descent)
6.5 Root Mean Squared Error (RMSE)
Formula:
text

RMSE = √MSE = √(1/n Σ(yᵢ - ŷᵢ)²)
Characteristics:
Property	Description
Units	Same as Y
Range	[0, ∞)
Interpretation	"Standard deviation" of prediction errors
Outlier Sensitivity	HIGH (inherited from MSE)
Example:
text

From previous: MSE = 62.5
RMSE = √62.5 = 7.91

"Typical prediction error is about 7.91 units"
MAE vs RMSE:
text

If MAE ≈ RMSE: Errors are similar in size
If RMSE >> MAE: Some large errors exist (outliers)

Example:
Errors: [1, 1, 1, 1, 100]  (one outlier)
MAE = 20.8
RMSE = 44.8  ← Much larger due to outlier!
6.6 Total Sum of Squares (TSS)
Formula:
text

TSS = Σ(yᵢ - ȳ)²

Where ȳ is the mean of actual Y values
What It Represents:
text

    │
    │  ●      
    │     ●      TSS measures total variation
ȳ  ─┼─────────── (how spread out Y values are
    │  ●         from their mean)
    │       ●
    │
TSS = Total variability in Y that we want to explain

6.7 Explained Sum of Squares (ESS) / Regression Sum of Squares (RSS)
Formula:
text

ESS = Σ(ŷᵢ - ȳ)²
What It Represents:
text

    │
    │     ● (predicted)
    │    /
ȳ  ─┼───/────── ESS measures how much our model's
    │  /         predictions deviate from the mean
    │ /          (variability EXPLAINED by model)
    │/
ESS = Variability explained by the regression

6.8 Residual Sum of Squares (RSS)
Formula:
text

RSS = Σ(yᵢ - ŷᵢ)² = SSE (Same as Sum of Squared Errors)
What It Represents:
RSS = Variability NOT explained by the regression (leftover error)

6.9 The Key Relationship
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│           TSS = ESS + RSS                                   │
│                                                             │
│   Total      Explained    Unexplained                       │
│   Variance = by Model   + (Error)                           │
│                                                             │
│   100% = What model captures + What model misses            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Visual:
text

TSS: |████████████████████████████████████████████| 100%

     |████████████████████████████|░░░░░░░░░░░░░░░|
              ESS (70%)              RSS (30%)
           Model explains        Model doesn't explain
6.10 R-Squared (Coefficient of Determination)
Formula:
text

R² = ESS/TSS = 1 - RSS/TSS = 1 - Σ(yᵢ-ŷᵢ)²/Σ(yᵢ-ȳ)²
Interpretation:
text

R² = 0.85 means:
"The model explains 85% of the variance in Y"
Visual:
text

R² = 0.0                      R² = 0.5                      R² = 1.0
(No relationship)             (Moderate)                    (Perfect fit)
       │   ●                      │    ●                        │  ●
       │ ●   ●                    │  ●  ╱                       │ ╱
       │   ●   ●                  │ ● ╱  ●                      │╱ 
       │●    ●                    │ ╱ ●                         ●
       │  ●    ●                  ●╱   ●                       ╱│
       └────────                  └────────                   └────────
Range:
text

• R² = 1: Perfect fit (all points on line)
• R² = 0: Model explains nothing (predicting mean is just as good)
• R² < 0: Model is WORSE than predicting mean! (possible with test data)
Warning Signs:
text

❌ R² = 0.99 for complex real-world data → Probably overfitting!
❌ R² keeps increasing as you add variables → Use Adjusted R²!
❌ Low R² doesn't always mean bad model → Some relationships are naturally weak
6.11 Adjusted R-Squared
The Problem with R²:
text

R² ALWAYS increases (or stays same) when you add variables,
even if those variables are useless!

Add random noise feature → R² still goes up slightly!
The Solution:
text

Adjusted R² = 1 - [(1-R²)(n-1)/(n-k-1)]

Where:
• n = number of observations
• k = number of features
Comparison:
Metric	Adding Useful Feature	Adding Useless Feature
R²	Increases	Increases (slightly)
Adjusted R²	Increases	Decreases
Rule of Thumb:
text

Use Adjusted R² when comparing models with different numbers of features!
6.12 AIC and BIC (Information Criteria)
Akaike Information Criterion (AIC):
text

AIC = n × ln(RSS/n) + 2k
Bayesian Information Criterion (BIC):
text

BIC = n × ln(RSS/n) + k × ln(n)
Interpretation:
text

• LOWER is BETTER
• Both penalize model complexity
• BIC penalizes more heavily for more features
• Used for model selection (comparing different models)
6.13 Summary Comparison
Metric	Formula	Range	Best Value	Use Case
MAE	Σ|y-ŷ|/n	[0,∞)	0	Robust to outliers
MSE	Σ(y-ŷ)²/n	[0,∞)	0	Optimization
RMSE	√MSE	[0,∞)	0	Interpretable error
R²	1-RSS/TSS	(-∞,1]	1	Variance explained
Adj R²	Adjusted	(-∞,1]	1	Model comparison
AIC	Complex	ℝ	Lower	Model selection
BIC	Complex	ℝ	Lower	Model selection
6.14 Complete Example
text

Data: n = 100 samples, k = 3 features

Actual Y mean (ȳ) = 50
Predictions made...

Calculations:
• TSS = 2500
• RSS = 500
• ESS = 2000

Metrics:
• R² = 1 - 500/2500 = 0.80 (80% variance explained)
• Adjusted R² = 1 - [(1-0.8)(99)/(96)] = 0.79
• RMSE = √(500/100) = 2.24

Interpretation:
"The model explains 80% of variance in Y, with typical
prediction error of 2.24 units."
Chapter 7: Feature Engineering & Selection {#chapter-7-feature-engineering}
7.1 What is Feature Engineering?
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  "Feature Engineering is the ART of transforming raw       │
│   data into features that better represent the underlying  │
│   problem, leading to improved model performance."          │
│                                                             │
│   Raw Data  →  Better Features  →  Better Model            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
7.2 Feature Scaling
Why Scale?
text

Feature 1: Age (range: 0-100)
Feature 2: Income (range: 0-1,000,000)

Without scaling:
- Income dominates the model due to larger values
- Gradient descent converges slowly
- Some algorithms behave poorly
Method 1: Min-Max Scaling (Normalization)
text

           x - x_min
x_scaled = ─────────────
           x_max - x_min

Result: Values between [0, 1]
Example:

text

Original: [10, 20, 30, 40, 50]
Min = 10, Max = 50

Scaled: [(10-10)/(50-10), (20-10)/(50-10), ...]
      = [0, 0.25, 0.5, 0.75, 1.0]
Method 2: Standardization (Z-score)
text

           x - μ
x_scaled = ─────
             σ

Result: Mean = 0, Std = 1
Example:

text

Original: [10, 20, 30, 40, 50]
Mean (μ) = 30, Std (σ) = 14.14

Scaled: [(10-30)/14.14, (20-30)/14.14, ...]
      = [-1.41, -0.71, 0, 0.71, 1.41]
When to Use Which?
Method	Use When	Caution
Min-Max	Need bounded range [0,1]	Sensitive to outliers
Neural networks	
Standardization	Data has outliers	No bounded range
Most ML algorithms	
7.3 Handling Categorical Variables
Problem:
text

Color: ["Red", "Blue", "Green"]

Can't use directly in regression!
Red ≠ 1, Blue ≠ 2 (implies order that doesn't exist)
Solution 1: One-Hot Encoding
text

Original:          One-Hot Encoded:
Color              Color_Red  Color_Blue  Color_Green
─────              ─────────  ──────────  ───────────
Red                    1          0           0
Blue                   0          1           0
Green                  0          0           1
Red                    1          0           0
Solution 2: Label Encoding (for Ordinal Data)
text

Original:          Label Encoded:
Size               Size_Encoded
─────              ────────────
Small                  0
Medium                 1
Large                  2

Use only when order matters!
Dummy Variable Trap:
text

If you have 3 categories, use only 2 dummy variables!

Color_Red  Color_Blue  (Color_Green implied when both = 0)
    1          0
    0          1
    0          0       ← This is Green!

Why? Multicollinearity: Red + Blue + Green = 1 always
7.4 Creating New Features
Polynomial Features:
text

Original: [x₁, x₂]

Degree 2 Polynomial Features:
[x₁, x₂, x₁², x₂², x₁×x₂]

Captures non-linear relationships!
Interaction Features:
text

Feature: Advertising, Feature: Season

Interaction: Advertising × Season

Captures: "Advertising effect depends on season"
Domain-Specific Features:
text

Housing Data:
- Rooms per Person = Total Rooms / Population
- Age per Room = House Age / Number of Rooms

E-commerce:
- Conversion Rate = Purchases / Visits
- Average Order Value = Revenue / Orders
7.5 Feature Selection Methods
text

                    FEATURE SELECTION
                          │
         ┌────────────────┼────────────────┐
         │                │                │
      FILTER          WRAPPER          EMBEDDED
      METHODS         METHODS          METHODS
         │                │                │
   ┌─────┼─────┐    ┌─────┼─────┐    ┌─────┼─────┐
   │     │     │    │     │     │    │     │     │
Corr  Chi² Mutual  RFE  Forward  Back  Lasso Ridge ElasticNet
        Test Info      Select   Elim
Filter Methods:
1. Correlation Analysis:

text

Remove features highly correlated with each other (multicollinearity)
Keep features correlated with target
2. Variance Threshold:

text

Remove features with low variance (they don't change much, so not useful)

If all values are same → Variance = 0 → Remove!
Wrapper Methods:
1. Forward Selection:

text

Start: No features
Step 1: Add best single feature
Step 2: Add next best feature
...
Stop: When adding features doesn't improve model
2. Backward Elimination:

text

Start: All features
Step 1: Remove worst feature
Step 2: Remove next worst feature
...
Stop: When removing features hurts model
3. Recursive Feature Elimination (RFE):

text

1. Train model with all features
2. Rank features by importance
3. Remove least important
4. Repeat until desired number of features
Embedded Methods:
text

Feature selection is BUILT INTO the algorithm

Lasso Regression: Automatically sets some coefficients to 0
Ridge Regression: Shrinks coefficients but doesn't eliminate
7.6 Handling Missing Values
Strategies:
text

┌─────────────────────────────────────────────────────────────┐
│                    MISSING VALUES                           │
│                         │                                   │
│     ┌───────────────────┼───────────────────┐              │
│     │                   │                   │              │
│  DELETION           IMPUTATION          INDICATOR         │
│     │                   │                   │              │
│  ┌──┴──┐         ┌──────┼──────┐            │              │
│  │     │         │      │      │            │              │
│ List  Pair     Mean   Median  Mode    Add column           │
│ wise  wise     /Mode           /        for                │
│                Advanced     KNN      missingness           │
│                (predict)                                    │
└─────────────────────────────────────────────────────────────┘
Method 1: Deletion
text

Listwise: Remove entire row if ANY value missing
Pairwise: Remove only for specific calculations

Use when: < 5% missing and Missing Completely At Random (MCAR)
Method 2: Imputation
text

Numerical:
- Mean: Replace with average
- Median: Replace with middle value (better for skewed data)

Categorical:
- Mode: Replace with most frequent value

Advanced:
- KNN Imputation: Use similar samples
- Regression Imputation: Predict missing values
Method 3: Missing Indicator
text

Original:        After:
Age              Age    Age_Missing
25               25         0
NaN     →        30         1  (imputed mean)
35               35         0

Captures: "This value was missing" as information
Chapter 8: Regularization Techniques {#chapter-8-regularization}
8.1 The Problem: Overfitting
text

UNDERFITTING              GOOD FIT                OVERFITTING
(High Bias)               (Balanced)              (High Variance)

    │                        │                        │   ●
    │  ● ●  ●               │    ●  ●  ●             │  / \
    │ ─────── ●             │   ╱╲    ●             │ ●   ●
    │●        ●             │  ●  ╲  ╱●             │╱  ● ╱
    │                        │      ╲╱               ●    ╲
    └──────────              └──────────             └──────────
    
Too simple                 Just right              Too complex
Misses patterns           Captures signal         Captures noise
8.2 Regularization: The Solution
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Regularization = Adding a PENALTY for model complexity    │
│                                                             │
│  New Cost Function = Original Error + λ × Complexity       │
│                                                             │
│  This prevents coefficients from becoming too large!       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
8.3 Ridge Regression (L2 Regularization)
Formula:
text

Cost = Σ(yᵢ - ŷᵢ)² + λ × Σβⱼ²
       ─────────────   ──────────
       Original MSE    Penalty term
                       (sum of squared coefficients)
What It Does:
text

• SHRINKS coefficients toward zero
• Does NOT make them exactly zero
• All features stay in the model
• Handles multicollinearity well
Closed-Form Solution:
text

β_ridge = (XᵀX + λI)⁻¹Xᵀy

The λI term makes the matrix invertible even with multicollinearity!
Effect of λ (Lambda):
text

λ = 0:          λ = 1:           λ = 10:          λ = ∞:
Pure OLS       Light penalty    Strong penalty   All β → 0
   │               │                │               │
β₁ = 5.0       β₁ = 4.2         β₁ = 2.1         β₁ = 0.0
β₂ = 3.0       β₂ = 2.7         β₂ = 1.5         β₂ = 0.0
β₃ = -2.0      β₃ = -1.8        β₃ = -1.0        β₃ = 0.0
Visual - Ridge Constraint:
text

        β₂
         │
         │    ╭──────╮
         │   ╱        ╲
         │  ╱    ●     ╲     ● = OLS solution
        ─┼─|     ◯     |──   ◯ = Ridge solution (constrained)
         │  ╲         ╱
         │   ╲       ╱
         │    ╰─────╯
         │    Circle: β₁² + β₂² ≤ c
        ─┼─────────────── β₁
8.4 Lasso Regression (L1 Regularization)
Formula:
text

Cost = Σ(yᵢ - ŷᵢ)² + λ × Σ|βⱼ|
       ─────────────   ────────
       Original MSE    Penalty term
                       (sum of absolute coefficients)
What It Does:
text

• SHRINKS coefficients toward zero
• CAN make coefficients EXACTLY zero
• Performs automatic feature selection!
• Produces sparse models
No Closed-Form Solution:
text

Must use iterative methods (coordinate descent, gradient descent)
Effect of λ (Lambda):
text

λ = 0:          λ = 1:           λ = 10:          λ = ∞:
Pure OLS       Light penalty    Strong penalty   All β → 0
   │               │                │               │
β₁ = 5.0       β₁ = 4.0         β₁ = 1.0         β₁ = 0.0
β₂ = 3.0       β₂ = 2.5         β₂ = 0.0 ← ZERO! β₂ = 0.0
β₃ = -2.0      β₃ = -1.5        β₃ = -0.5        β₃ = 0.0
                                  ↑
                               Feature eliminated!
Visual - Lasso Constraint:
text

        β₂
         │
         │    ╱╲
         │   ╱  ╲
         │  ╱    ╲
        ─┼─◇  ●   ╲      ● = OLS solution
         │  ╲  ◯ ╱       ◯ = Lasso solution (at corner!)
         │   ╲  ╱
         │    ╲╱
         │    Diamond: |β₁| + |β₂| ≤ c
        ─┼─────────────── β₁
        
The corners of the diamond often hit axis,
making some coefficients exactly ZERO!
8.5 Elastic Net (L1 + L2 Combined)
Formula:
text

Cost = Σ(yᵢ - ŷᵢ)² + λ₁ × Σ|βⱼ| + λ₂ × Σβⱼ²
       ─────────────   ────────────   ────────
       Original MSE    L1 (Lasso)     L2 (Ridge)
Alternative Form:
text

Cost = MSE + λ × [α × Σ|βⱼ| + (1-α) × Σβⱼ²]

Where:
• α = 1: Pure Lasso
• α = 0: Pure Ridge
• 0 < α < 1: Mix of both
When to Use:
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  RIDGE:      • Multicollinearity present                    │
│              • All features potentially relevant            │
│              • Want to keep all features                    │
│                                                             │
│  LASSO:      • Feature selection needed                     │
│              • Sparse model desired                         │
│              • Some features irrelevant                     │
│                                                             │
│  ELASTIC NET: • Best of both worlds                         │
│               • Correlated features in groups               │
│               • Lasso selects randomly from correlated      │
│               • Elastic Net keeps/removes together          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
8.6 Choosing Lambda (λ) - Cross-Validation
text

┌───────────────────────────────────────────────────────────┐
│                                                           │
│   DATA SPLIT:                                             │
│   ┌─────┬─────┬─────┬─────┬─────┐                        │
│   │  1  │  2  │  3  │  4  │  5  │  5 Folds               │
│   └─────┴─────┴─────┴─────┴─────┘                        │
│                                                           │
│   Iteration 1: Train on 2,3,4,5  | Validate on 1         │
│   Iteration 2: Train on 1,3,4,5  | Validate on 2         │
│   Iteration 3: Train on 1,2,4,5  | Validate on 3         │
│   Iteration 4: Train on 1,2,3,5  | Validate on 4         │
│   Iteration 5: Train on 1,2,3,4  | Validate on 5         │
│                                                           │
│   For each λ value, compute average validation error     │
│   Choose λ with lowest average error!                    │
│                                                           │
└───────────────────────────────────────────────────────────┘
Visual:
text

Validation
Error
    │
    │╲
    │ ╲
    │  ╲__          ___
    │     ╲___  ___╱
    │         ╲╱
    │          ●  ← Optimal λ
    │
    └───────────────────── λ
       0.001  0.01  0.1  1  10

Choose λ where error is minimum!
8.7 Comparison Summary
Property	OLS	Ridge	Lasso	Elastic Net
Penalty	None	L2 (β²)	L1 (|β|)	L1 + L2
Coefficients → 0	No	Shrinks, not 0	Can be 0	Can be 0
Feature Selection	No	No	Yes	Yes
Handles Multicollinearity	No	Yes	Partially	Yes
Closed Form	Yes	Yes	No	No
# Hyperparameters	0	1 (λ)	1 (λ)	2 (λ, α)
Chapter 9: Polynomial Regression {#chapter-9-polynomial-regression}
9.1 When Linear Isn't Enough
text

ACTUAL DATA:                    LINEAR FIT (Bad):
    │      ●●●                     │      ●●●
    │    ●     ●                   │  ___●_____●___
    │   ●       ●                  │ ╱
    │ ●          ●                 │╱●          ●
    │●            ●                │             ●
    └────────────────              └────────────────
    
    Clearly curved!                Linear line misses the pattern!
9.2 The Polynomial Solution
Transform Features:
text

Original: y = β₀ + β₁x  (straight line)

Degree 2:  y = β₀ + β₁x + β₂x²  (parabola)

Degree 3:  y = β₀ + β₁x + β₂x² + β₃x³  (cubic)

Degree n:  y = β₀ + β₁x + β₂x² + ... + βₙxⁿ
It's Still Linear Regression!
text

Think of x, x², x³ as DIFFERENT features!

Let: z₁ = x, z₂ = x², z₃ = x³

Then: y = β₀ + β₁z₁ + β₂z₂ + β₃z₃

This is LINEAR in terms of the parameters (β)!
9.3 Visual: Different Degrees
text

Degree 1 (Linear):        Degree 2 (Quadratic):     Degree 3 (Cubic):
     │                         │    ╭──╮                │   ╭─╮
     │     ╱                   │   ╱    ╲               │  ╱   ╲
     │   ╱                     │  ╱      ╲              │ ╱     ╲
     │ ╱                       │ ╱        ╲             │╱       ╲
     │╱                        │╱          ╲            ╱         ╲
     └────────                 └────────────            └───────────

1 bend possible             1 curve peak/valley      2 direction changes
9.4 Complete Example
Data: Relationship between Speed and Fuel Efficiency
Speed (x)	20	30	40	50	60	70	80
MPG (y)	25	30	35	36	35	32	27
text

MPG peaks around 50mph then decreases - clearly not linear!
Feature Transformation:
x	x²	y
20	400	25
30	900	30
40	1600	35
50	2500	36
60	3600	35
70	4900	32
80	6400	27
Apply Linear Regression on Transformed Data:
text

Model: y = β₀ + β₁x + β₂x²

After fitting:
β₀ = 5.0
β₁ = 1.25
β₂ = -0.0125

Final Model: MPG = 5 + 1.25(Speed) - 0.0125(Speed²)
Prediction:
text

Speed = 55 mph:
MPG = 5 + 1.25(55) - 0.0125(55²)
MPG = 5 + 68.75 - 37.81
MPG = 35.94
9.5 Choosing the Right Degree
Too Low Degree = Underfitting:
text

    │     ●●●●●
    │   ●╱──────●
    │  ●╱        ●
    │ ●╱          ●
    │●╱            
    └────────────────
Degree 1 on curved data - misses the pattern!
Too High Degree = Overfitting:
text

    │    ╭─╮  ╭─╮
    │   ╱●╲●╲●╱●╲●
    │  ●    ╲╱    ●
    │ ●           ●
    │●
    └────────────────
Degree 10 - captures noise, not signal!
Just Right:
text

    │      ╭───╮
    │   ●●●     ●●●
    │  ●           ●
    │ ●             ●
    │●
    └────────────────
Degree 2 - captures underlying pattern!
How to Choose:
Visual inspection of residuals
Cross-validation error
Domain knowledge (physics often suggests quadratic)
Information criteria (AIC, BIC)
9.6 Bias-Variance Tradeoff
text

Error
  │╲                           ╱
  │ ╲                         ╱
  │  ╲ Total Error          ╱
  │   ╲        ╲╲_____╱╱   ╱
  │    ╲         ●       ╱
  │     ╲___    ╱ Optimal
  │    Bias  ╲╱
  │           ╲
  │   Variance ╲________
  │
  └──────────────────────────── Model Complexity
     Low                   High
     (Underfitting)        (Overfitting)
Key Insight:
text

• Low complexity → High Bias, Low Variance → Underfitting
• High complexity → Low Bias, High Variance → Overfitting
• Optimal → Balanced Bias-Variance → Best generalization
Chapter 10: Gradient Descent - The Optimization Engine {#chapter-10-gradient-descent}
10.1 Why Gradient Descent?
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Normal Equation:  β = (XᵀX)⁻¹Xᵀy                          │
│                                                             │
│  PROBLEMS:                                                  │
│  • Matrix inverse: O(n³) complexity                         │
│  • Fails if XᵀX is not invertible                          │
│  • Impossible for large datasets (millions of features)    │
│                                                             │
│  SOLUTION: Gradient Descent!                                │
│  • Iterative approach                                       │
│  • Works with any differentiable function                   │
│  • Scalable to massive datasets                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
10.2 The Intuition
text

Imagine you're blindfolded on a mountain...

Goal: Reach the lowest point (valley)

Strategy:
1. Feel the slope under your feet
2. Take a step in the downward direction
3. Repeat until you can't go lower

        ╱╲
       ╱  ╲
      ╱    ╲         ← Start here
     ╱  ↓   ╲           │
    ╱   ↓    ╲          ↓ Follow slope
   ╱    ↓     ╲      
  ╱     ●      ╲     ← Reach minimum!
  ────────────────
10.3 The Mathematics
Cost Function (What We Minimize):
text

J(β) = (1/2n) × Σ(ŷᵢ - yᵢ)² = (1/2n) × Σ(β₀ + β₁xᵢ - yᵢ)²
Gradient (Direction of Steepest Ascent):
text

∂J/∂β₀ = (1/n) × Σ(ŷᵢ - yᵢ)
∂J/∂β₁ = (1/n) × Σ(ŷᵢ - yᵢ) × xᵢ

General form:
∂J/∂βⱼ = (1/n) × Σ(ŷᵢ - yᵢ) × xᵢⱼ
Update Rule (Move Opposite to Gradient):
text

β_new = β_old - α × ∇J(β)

Where:
• α = learning rate (step size)
• ∇J(β) = gradient vector
Full Algorithm:
text

1. Initialize: β = [0, 0, ..., 0]
2. Repeat until convergence:
   a. Compute predictions: ŷ = Xβ
   b. Compute error: e = ŷ - y
   c. Compute gradient: ∇J = (1/n) × Xᵀe
   d. Update: β = β - α × ∇J
3. Return: β
10.4 Types of Gradient Descent
1. Batch Gradient Descent
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Use ALL data points to compute gradient at each step      │
│                                                             │
│  FOR each iteration:                                        │
│      gradient = 0                                           │
│      FOR each data point (xᵢ, yᵢ):                         │
│          gradient += (ŷᵢ - yᵢ) × xᵢ                        │
│      gradient = gradient / n                                │
│      β = β - α × gradient                                   │
│                                                             │
│  ✓ Stable convergence                                       │
│  ✗ Slow for large datasets                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
2. Stochastic Gradient Descent (SGD)
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Use ONE random data point to compute gradient             │
│                                                             │
│  FOR each iteration:                                        │
│      Randomly pick (xᵢ, yᵢ)                                │
│      gradient = (ŷᵢ - yᵢ) × xᵢ                             │
│      β = β - α × gradient                                   │
│                                                             │
│  ✓ Fast updates                                             │
│  ✓ Can escape local minima                                  │
│  ✗ Noisy, zigzag path                                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
3. Mini-Batch Gradient Descent
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Use a SUBSET (batch) of data points                       │
│                                                             │
│  Batch size: typically 32, 64, 128, 256                    │
│                                                             │
│  FOR each iteration:                                        │
│      Randomly select batch of size b                       │
│      gradient = (1/b) × Σ(ŷᵢ - yᵢ) × xᵢ  (over batch)      │
│      β = β - α × gradient                                   │
│                                                             │
│  ✓ Best of both worlds                                      │
│  ✓ GPU efficient (parallel computation)                     │
│  ✓ Most commonly used in practice                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Visual Comparison:
text

BATCH GD:              SGD:                   MINI-BATCH:
(Smooth path)          (Noisy path)           (Balanced)

    ╱╲                     ╱╲                     ╱╲
   ╱↓ ╲

   ╱↓ ╲                   ╱↘╱╲                   ╱↘ ╲
  ╱ ↓  ╲                 ╱╱↘╲↘╲                 ╱ ↘ ╲
 ╱  ↓   ╲               ╱╱  ↘╲ ╲               ╱  ↘  ╲
╱   ●    ╲             ╱   ↘● ╲               ╱   ●   ╲
───────────            ───────────            ───────────
Straight down          Zigzag but gets there  Moderate noise


10.5 Learning Rate (α) - The Critical Hyperparameter
Too Small:
text

Cost
  │╲
  │ ╲
  │  ╲
  │   ╲
  │    ╲
  │     ╲
  │      ╲
  │       ╲........ Takes forever!
  └──────────────────── Iterations
Too Large:
text

Cost
  │    ╱╲      ╱╲
  │   ╱  ╲    ╱  ╲
  │  ╱    ╲  ╱    ╲   Diverges!
  │ ╱      ╲╱      ╲  Never converges!
  │╱                ╲
  └──────────────────── Iterations
Just Right:
text

Cost
  │╲
  │ ╲
  │  ╲__
  │     ╲___
  │         ╲_________ Converges nicely!
  └──────────────────── Iterations
Typical Values:
text

Start with: α = 0.01 or α = 0.001

Common strategy:
• Start large, decrease over time
• α(t) = α₀ / (1 + decay_rate × t)
10.6 Feature Scaling for Gradient Descent
Without Scaling:
text

β₁ (large scale feature)
  │         ╱  Elongated contours
  │        ╱   Gradient zigzags
  │       ╱↘
  │      ╱ ↘↗
  │     ╱  ↘↗
  │    ╱   ●
  └──────────── β₀ (small scale feature)
With Scaling:
text

β₁ (scaled)
  │    ╭───╮
  │   ╱     ╲   Circular contours
  │  │   ●   │  Gradient goes straight
  │   ╲     ╱   to minimum!
  │    ╰───╯
  └──────────── β₀ (scaled)
Always scale features before using Gradient Descent!

10.7 Convergence Criteria
Python

# Method 1: Fixed number of iterations
for i in range(max_iterations):
    update_parameters()

# Method 2: Cost change threshold
while abs(cost_new - cost_old) > threshold:
    update_parameters()

# Method 3: Gradient magnitude
while ||gradient|| > threshold:
    update_parameters()
10.8 Complete Python-like Pseudocode
Python

def gradient_descent(X, y, learning_rate=0.01, iterations=1000):
    # Add bias column
    X = add_ones_column(X)  # [1, x1, x2, ...]
    n_samples, n_features = X.shape
    
    # Initialize weights
    beta = zeros(n_features)
    
    # Store cost history
    cost_history = []
    
    for i in range(iterations):
        # 1. Make predictions
        y_pred = X @ beta  # Matrix multiplication
        
        # 2. Calculate error
        error = y_pred - y
        
        # 3. Calculate gradient
        gradient = (1/n_samples) * (X.T @ error)
        
        # 4. Update weights
        beta = beta - learning_rate * gradient
        
        # 5. Calculate and store cost
        cost = (1/(2*n_samples)) * sum(error**2)
        cost_history.append(cost)
    
    return beta, cost_history
Chapter 11: Common Problems & Solutions {#chapter-11-problems-solutions}
11.1 Problem: Multicollinearity
What It Is:
text

Feature X₁ and X₂ are highly correlated

Example:
• Height in inches
• Height in centimeters
• These are perfectly correlated!
How to Detect:
text

1. Correlation Matrix:
         X₁     X₂     X₃
   X₁   1.00   0.95   0.10
   X₂   0.95   1.00   0.15    ← X₁ and X₂: 0.95 = PROBLEM!
   X₃   0.10   0.15   1.00

2. VIF (Variance Inflation Factor):
   VIF > 10 → Severe multicollinearity
   VIF > 5  → Moderate (investigate)
   VIF ≈ 1  → No multicollinearity
Solutions:
text

┌─────────────────────────────────────────────────────────────┐
│ SOLUTION                    │ WHEN TO USE                   │
├─────────────────────────────┼───────────────────────────────┤
│ Remove one correlated var   │ One is clearly redundant      │
│ Combine variables (average) │ Both capture same concept     │
│ PCA (Principal Component)   │ Many correlated features      │
│ Ridge Regression            │ Want to keep all features     │
└─────────────────────────────┴───────────────────────────────┘
11.2 Problem: Outliers
Impact:
text

With Outlier:                   Without Outlier:
    │           ● (outlier)        │
    │          ╱                   │        ●●●
    │         ╱                    │      ●╱
    │    ●●●╱                      │    ●╱
    │   ●  ╱                       │  ●╱
    │  ● ╱                         │●╱
    └────────────                  └────────────
Line pulled toward outlier!        Correct fit!
Detection:
text

1. Z-Score: |z| > 3 is outlier
2. IQR Method: Below Q1-1.5*IQR or Above Q3+1.5*IQR
3. Visual: Box plots, scatter plots
Solutions:
text

┌─────────────────────────────────────────────────────────────┐
│ SOLUTION                    │ WHEN TO USE                   │
├─────────────────────────────┼───────────────────────────────┤
│ Remove outliers             │ Data entry errors             │
│ Cap/Floor (Winsorization)   │ Extreme but valid values      │
│ Log transformation          │ Right-skewed data             │
│ Robust Regression           │ Outliers contain information  │
│ Use MAE instead of MSE      │ During model training         │
└─────────────────────────────┴───────────────────────────────┘
11.3 Problem: Heteroscedasticity
What It Looks Like:
text

Residuals vs Fitted:

GOOD (Homoscedastic):          BAD (Heteroscedastic):
    │   ●  ●    ●               │              ●●●●
    │ ●  ●  ●  ●  ●             │         ●  ●  ●
────┼──●──●──●──●───●──         │     ●  ●  ●
    │  ●    ●   ●               │  ● ●  ●
    │    ●                      │●●
    └─────────────────          └─────────────────
    Constant spread             Funnel shape (spread increases)
Solutions:
text

1. Transform Y: log(Y), sqrt(Y), 1/Y
2. Weighted Least Squares (WLS)
3. Robust Standard Errors (HC0, HC1, etc.)
11.4 Problem: Non-Linearity
Detection:
text

Residual Plot:
    │   ●         ●
    │  ● ●       ●
    │      ●   ●
────┼───────●───────
    │      ● ●
    │     ●   ●
    └─────────────────
Pattern in residuals = Non-linearity!
Solutions:
text

1. Polynomial features: x, x², x³
2. Log transform: log(x), log(y)
3. Interaction terms: x₁ × x₂
4. Splines
5. Non-linear models (if severe)
11.5 Problem: Overfitting
Symptoms:
text

Training R² = 0.99  (Excellent!)
Testing R²  = 0.45  (Poor!)

The model memorized training data, can't generalize!
Visual:
text

    │  ●
    │ ╱╲●           Overfitting: Captures noise
    │╱  ╲╱●
    ●    ╲ ●
    │     ●
    └──────────

    │        ●●●
    │    ●●●╱        Good fit: Captures pattern
    │  ●●╱
    │●╱
    └──────────
Solutions:
text

┌─────────────────────────────────────────────────────────────┐
│ SOLUTION                    │ HOW IT HELPS                  │
├─────────────────────────────┼───────────────────────────────┤
│ More training data          │ More patterns to learn        │
│ Feature selection           │ Remove noise features         │
│ Regularization (L1/L2)      │ Penalize complexity           │
│ Cross-validation            │ Detect overfitting early      │
│ Reduce polynomial degree    │ Simpler model                 │
│ Early stopping              │ Stop before overfitting       │
└─────────────────────────────┴───────────────────────────────┘
11.6 Problem: Underfitting
Symptoms:
text

Training R² = 0.40  (Poor!)
Testing R²  = 0.38  (Also poor!)

Model is too simple to capture patterns!
Solutions:
text

1. Add more features
2. Polynomial features
3. Reduce regularization strength
4. Use more complex model
11.7 Problem: Missing Values
Strategies Summary:
text

% Missing   │   Strategy
────────────┼──────────────────────────────
< 5%        │   Remove rows OR simple imputation
5-25%       │   Imputation (mean/median/KNN)
25-50%      │   Advanced imputation + missing indicator
> 50%       │   Consider removing feature
11.8 Quick Diagnostic Checklist
text

┌─────────────────────────────────────────────────────────────┐
│               LINEAR REGRESSION DIAGNOSTIC                  │
│                                                             │
│  □ Check scatter plot (X vs Y) for linearity              │
│  □ Check residuals vs fitted for patterns                  │
│  □ Check residual distribution (normality)                 │
│  □ Check residual spread (homoscedasticity)               │
│  □ Calculate VIF for multicollinearity                     │
│  □ Identify outliers (box plot, z-scores)                 │
│  □ Compare train vs test performance (overfitting)        │
│  □ Check Durbin-Watson for independence                    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Chapter 12: Implementation from Scratch {#chapter-12-implementation}
12.1 Simple Linear Regression - Pure Python
Python

class SimpleLinearRegression:
    """
    Simple Linear Regression from scratch.
    ŷ = β₀ + β₁x
    """
    
    def __init__(self):
        self.beta_0 = None  # Intercept
        self.beta_1 = None  # Slope
    
    def fit(self, X, y):
        """
        Fit the model using Ordinary Least Squares.
        
        Parameters:
        -----------
        X : list or array of shape (n_samples,)
        y : list or array of shape (n_samples,)
        """
        n = len(X)
        
        # Calculate means
        x_mean = sum(X) / n
        y_mean = sum(y) / n
        
        # Calculate β₁ (slope)
        numerator = sum((X[i] - x_mean) * (y[i] - y_mean) for i in range(n))
        denominator = sum((X[i] - x_mean) ** 2 for i in range(n))
        
        self.beta_1 = numerator / denominator
        
        # Calculate β₀ (intercept)
        self.beta_0 = y_mean - self.beta_1 * x_mean
        
        return self
    
    def predict(self, X):
        """
        Make predictions.
        
        Parameters:
        -----------
        X : list or array of shape (n_samples,)
        
        Returns:
        --------
        predictions : list
        """
        return [self.beta_0 + self.beta_1 * x for x in X]
    
    def score(self, X, y):
        """
        Calculate R² score.
        """
        y_pred = self.predict(X)
        y_mean = sum(y) / len(y)
        
        ss_tot = sum((y[i] - y_mean) ** 2 for i in range(len(y)))
        ss_res = sum((y[i] - y_pred[i]) ** 2 for i in range(len(y)))
        
        r_squared = 1 - (ss_res / ss_tot)
        return r_squared


# ═══════════════════════════════════════════════════════════
# EXAMPLE USAGE
# ═══════════════════════════════════════════════════════════

# Data
X = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = [2.1, 4.2, 5.8, 8.1, 10.2, 11.9, 14.1, 16.0, 18.2, 20.1]

# Train model
model = SimpleLinearRegression()
model.fit(X, y)

# Results
print(f"Intercept (β₀): {model.beta_0:.4f}")
print(f"Slope (β₁): {model.beta_1:.4f}")
print(f"Equation: y = {model.beta_0:.4f} + {model.beta_1:.4f}x")
print(f"R² Score: {model.score(X, y):.4f}")

# Prediction
print(f"Prediction for x=15: {model.predict([15])[0]:.4f}")
12.2 Multiple Linear Regression - With NumPy
Python

import numpy as np

class MultipleLinearRegression:
    """
    Multiple Linear Regression using Normal Equation.
    ŷ = Xβ
    β = (XᵀX)⁻¹Xᵀy
    """
    
    def __init__(self):
        self.coefficients = None
        self.intercept = None
    
    def fit(self, X, y):
        """
        Fit model using Normal Equation.
        
        Parameters:
        -----------
        X : numpy array of shape (n_samples, n_features)
        y : numpy array of shape (n_samples,)
        """
        # Convert to numpy arrays
        X = np.array(X)
        y = np.array(y).reshape(-1, 1)
        
        # Add column of ones for intercept
        n_samples = X.shape[0]
        X_with_bias = np.hstack([np.ones((n_samples, 1)), X])
        
        # Normal Equation: β = (XᵀX)⁻¹Xᵀy
        XtX = X_with_bias.T @ X_with_bias
        XtX_inv = np.linalg.inv(XtX)
        Xty = X_with_bias.T @ y
        
        beta = XtX_inv @ Xty
        
        # Separate intercept and coefficients
        self.intercept = beta[0, 0]
        self.coefficients = beta[1:, 0]
        
        return self
    
    def predict(self, X):
        """
        Make predictions.
        """
        X = np.array(X)
        return self.intercept + X @ self.coefficients
    
    def score(self, X, y):
        """
        Calculate R² score.
        """
        y = np.array(y)
        y_pred = self.predict(X)
        
        ss_tot = np.sum((y - np.mean(y)) ** 2)
        ss_res = np.sum((y - y_pred) ** 2)
        
        return 1 - (ss_res / ss_tot)


# ═══════════════════════════════════════════════════════════
# EXAMPLE USAGE
# ═══════════════════════════════════════════════════════════

# Data: Predicting house price based on size and bedrooms
X = np.array([
    [1400, 3],
    [1600, 3],
    [1700, 4],
    [1875, 4],
    [1100, 2],
    [1550, 3],
    [2350, 4],
    [2450, 5]
])
y = np.array([245, 312, 279, 308, 199, 219, 405, 324])

# Train model
model = MultipleLinearRegression()
model.fit(X, y)

# Results
print(f"Intercept: {model.intercept:.4f}")
print(f"Coefficients: {model.coefficients}")
print(f"R² Score: {model.score(X, y):.4f}")

# Prediction
new_house = [[2000, 4]]
print(f"Predicted price: ${model.predict(new_house)[0]:.2f}k")
12.3 Gradient Descent Implementation
Python

import numpy as np

class LinearRegressionGD:
    """
    Linear Regression using Gradient Descent.
    """
    
    def __init__(self, learning_rate=0.01, n_iterations=1000, 
                 tolerance=1e-6, verbose=False):
        self.learning_rate = learning_rate
        self.n_iterations = n_iterations
        self.tolerance = tolerance
        self.verbose = verbose
        self.coefficients = None
        self.intercept = None
        self.cost_history = []
    
    def _add_intercept(self, X):
        """Add column of ones for intercept term."""
        return np.hstack([np.ones((X.shape[0], 1)), X])
    
    def _compute_cost(self, X, y, beta):
        """Compute Mean Squared Error."""
        n = len(y)
        predictions = X @ beta
        cost = (1 / (2 * n)) * np.sum((predictions - y) ** 2)
        return cost
    
    def _compute_gradient(self, X, y, beta):
        """Compute gradient of cost function."""
        n = len(y)
        predictions = X @ beta
        gradient = (1 / n) * (X.T @ (predictions - y))
        return gradient
    
    def fit(self, X, y):
        """
        Fit model using Gradient Descent.
        """
        X = np.array(X)
        y = np.array(y).reshape(-1, 1)
        
        # Add intercept column
        X_with_bias = self._add_intercept(X)
        n_samples, n_features = X_with_bias.shape
        
        # Initialize weights to zeros
        beta = np.zeros((n_features, 1))
        
        # Gradient Descent
        for i in range(self.n_iterations):
            # Compute gradient
            gradient = self._compute_gradient(X_with_bias, y, beta)
            
            # Update weights
            beta_new = beta - self.learning_rate * gradient
            
            # Compute cost
            cost = self._compute_cost(X_with_bias, y, beta_new)
            self.cost_history.append(cost)
            
            # Check convergence
            if np.linalg.norm(beta_new - beta) < self.tolerance:
                if self.verbose:
                    print(f"Converged at iteration {i}")
                break
            
            beta = beta_new
            
            if self.verbose and i % 100 == 0:
                print(f"Iteration {i}, Cost: {cost:.6f}")
        
        # Store results
        self.intercept = beta[0, 0]
        self.coefficients = beta[1:, 0]
        
        return self
    
    def predict(self, X):
        """Make predictions."""
        X = np.array(X)
        return self.intercept + X @ self.coefficients
    
    def score(self, X, y):
        """Calculate R² score."""
        y = np.array(y)
        y_pred = self.predict(X)
        ss_tot = np.sum((y - np.mean(y)) ** 2)
        ss_res = np.sum((y - y_pred) ** 2)
        return 1 - (ss_res / ss_tot)


# ═══════════════════════════════════════════════════════════
# EXAMPLE USAGE WITH FEATURE SCALING
# ═══════════════════════════════════════════════════════════

# Data
X = np.array([
    [1400, 3],
    [1600, 3],
    [1700, 4],
    [1875, 4],
    [1100, 2],
    [1550, 3],
    [2350, 4],
    [2450, 5]
])
y = np.array([245, 312, 279, 308, 199, 219, 405, 324])

# Feature Scaling (IMPORTANT for Gradient Descent!)
X_mean = X.mean(axis=0)
X_std = X.std(axis=0)
X_scaled = (X - X_mean) / X_std

# Train model
model = LinearRegressionGD(learning_rate=0.1, n_iterations=1000, verbose=True)
model.fit(X_scaled, y)

print(f"\nFinal R² Score: {model.score(X_scaled, y):.4f}")
12.4 Ridge Regression Implementation
Python

import numpy as np

class RidgeRegression:
    """
    Ridge Regression (L2 Regularization).
    β = (XᵀX + λI)⁻¹Xᵀy
    """
    
    def __init__(self, alpha=1.0):
        """
        Parameters:
        -----------
        alpha : float
            Regularization strength (λ)
        """
        self.alpha = alpha
        self.coefficients = None
        self.intercept = None
    
    def fit(self, X, y):
        """Fit Ridge Regression model."""
        X = np.array(X)
        y = np.array(y).reshape(-1, 1)
        
        # Add intercept column
        n_samples = X.shape[0]
        X_with_bias = np.hstack([np.ones((n_samples, 1)), X])
        n_features = X_with_bias.shape[1]
        
        # Create identity matrix (but 0 for intercept)
        I = np.eye(n_features)
        I[0, 0] = 0  # Don't regularize intercept
        
        # Ridge formula: β = (XᵀX + λI)⁻¹Xᵀy
        XtX = X_with_bias.T @ X_with_bias
        regularized = XtX + self.alpha * I
        XtX_inv = np.linalg.inv(regularized)
        Xty = X_with_bias.T @ y
        
        beta = XtX_inv @ Xty
        
        self.intercept = beta[0, 0]
        self.coefficients = beta[1:, 0]
        
        return self
    
    def predict(self, X):
        """Make predictions."""
        X = np.array(X)
        return self.intercept + X @ self.coefficients
    
    def score(self, X, y):
        """Calculate R² score."""
        y = np.array(y)
        y_pred = self.predict(X)
        ss_tot = np.sum((y - np.mean(y)) ** 2)
        ss_res = np.sum((y - y_pred) ** 2)
        return 1 - (ss_res / ss_tot)


# ═══════════════════════════════════════════════════════════
# COMPARE OLS vs RIDGE
# ═══════════════════════════════════════════════════════════

print("OLS Coefficients:", model_ols.coefficients)
print("Ridge (α=1) Coefficients:", model_ridge.coefficients)
print("Ridge (α=100) Coefficients:", model_ridge_strong.coefficients)

# Notice: Ridge coefficients are smaller (shrunk toward 0)
12.5 Complete Pipeline Example
Python

import numpy as np
from sklearn.model_selection import train_test_split

class LinearRegressionPipeline:
    """
    Complete pipeline: Scaling → Training → Prediction → Evaluation
    """
    
    def __init__(self):
        self.model = None
        self.X_mean = None
        self.X_std = None
        self.y_mean = None
        self.y_std = None
        
    def standardize_features(self, X, fit=True):
        """Standardize features to zero mean and unit variance."""
        if fit:
            self.X_mean = np.mean(X, axis=0)
            self.X_std = np.std(X, axis=0)
            self.X_std[self.X_std == 0] = 1  # Avoid division by zero
        
        return (X - self.X_mean) / self.X_std
    
    def fit(self, X_train, y_train):
        """Fit the complete pipeline."""
        # Standardize features
        X_scaled = self.standardize_features(X_train, fit=True)
        
        # Add bias term
        X_with_bias = np.hstack([np.ones((X_scaled.shape[0], 1)), X_scaled])
        
        # Fit using normal equation
        y = y_train.reshape(-1, 1)
        beta = np.linalg.pinv(X_with_bias.T @ X_with_bias) @ X_with_bias.T @ y
        
        self.model = beta.flatten()
        return self
    
    def predict(self, X):
        """Make predictions on new data."""
        X_scaled = self.standardize_features(X, fit=False)
        X_with_bias = np.hstack([np.ones((X_scaled.shape[0], 1)), X_scaled])
        return X_with_bias @ self.model
    
    def evaluate(self, X_test, y_test):
        """Compute multiple evaluation metrics."""
        y_pred = self.predict(X_test)
        
        # R² Score
        ss_tot = np.sum((y_test - np.mean(y_test)) ** 2)
        ss_res = np.sum((y_test - y_pred) ** 2)
        r2 = 1 - (ss_res / ss_tot)
        
        # MSE
        mse = np.mean((y_test - y_pred) ** 2)
        
        # RMSE
        rmse = np.sqrt(mse)
        
        # MAE
        mae = np.mean(np.abs(y_test - y_pred))
        
        return {
            'R²': r2,
            'MSE': mse,
            'RMSE': rmse,
            'MAE': mae
        }


# ═══════════════════════════════════════════════════════════
# FULL EXAMPLE
# ═══════════════════════════════════════════════════════════

# Generate sample data
np.random.seed(42)
n_samples = 100

X = np.random.randn(n_samples, 3) * [100, 10, 1]  # Different scales
true_coefficients = [2, 5, 10]
y = X @ true_coefficients + 50 + np.random.randn(n_samples) * 5

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Train and evaluate
pipeline = LinearRegressionPipeline()
pipeline.fit(X_train, y_train)

metrics = pipeline.evaluate(X_test, y_test)
print("Model Performance:")
for metric, value in metrics.items():
    print(f"  {metric}: {value:.4f}")
Chapter 13: Real-World Applications {#chapter-13-applications}
13.1 Application 1: House Price Prediction
text

┌─────────────────────────────────────────────────────────────┐
│                 HOUSE PRICE PREDICTION                      │
│                                                             │
│  Features:                        Target:                   │
│  ├── Square footage              Price ($)                 │
│  ├── Number of bedrooms                                    │
│  ├── Number of bathrooms                                   │
│  ├── Age of house                                          │
│  ├── Lot size                                              │
│  ├── Garage size                                           │
│  ├── School district rating                                │
│  └── Distance to downtown                                  │
│                                                             │
│  Model: Price = β₀ + β₁×sqft + β₂×beds + β₃×baths + ...   │
│                                                             │
│  Interpretation Example:                                    │
│  β₁ = 150 → Each additional sqft adds $150 to price       │
│  β₃ = 25000 → Each bathroom adds $25,000 to price         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
13.2 Application 2: Sales Forecasting
text

┌─────────────────────────────────────────────────────────────┐
│                   SALES FORECASTING                         │
│                                                             │
│  Features:                        Target:                   │
│  ├── Advertising spend           Sales Revenue             │
│  ├── Price                                                 │
│  ├── Competitor prices                                     │
│  ├── Seasonality (month)                                   │
│  ├── Economic indicators                                   │
│  └── Social media mentions                                 │
│                                                             │
│  Business Questions Answered:                              │
│  • "If we increase ad spend by $10K, how much more         │
│     revenue can we expect?"                                │
│  • "What's the optimal price point?"                       │
│  • "Which marketing channel has highest ROI?"              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
13.3 Application 3: Medical Diagnosis Support
text

┌─────────────────────────────────────────────────────────────┐
│              MEDICAL DIAGNOSIS SUPPORT                      │
│                                                             │
│  Predicting: Blood pressure, cholesterol levels,           │
│              Disease progression, Drug dosage              │
│                                                             │
│  Features:                                                  │
│  ├── Age                                                   │
│  ├── Weight, Height, BMI                                   │
│  ├── Blood test results                                    │
│  ├── Lifestyle factors                                     │
│  ├── Genetic markers                                       │
│  └── Previous medical history                              │
│                                                             │
│  Example Model:                                             │
│  Cholesterol = 100 + 1.5×Age + 0.8×BMI - 5×Exercise_hours │
│                                                             │
│  Interpretation:                                            │
│  • Each year of age increases cholesterol by 1.5 mg/dL    │
│  • Each hour of weekly exercise decreases it by 5 mg/dL   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
13.4 Application 4: Financial Modeling
text

┌─────────────────────────────────────────────────────────────┐
│                  FINANCIAL MODELING                         │
│                                                             │
│  Stock Returns (CAPM Model):                               │
│  Rᵢ - Rf = α + β(Rₘ - Rf) + ε                             │
│                                                             │
│  Where:                                                     │
│  • Rᵢ = Return on stock i                                  │
│  • Rf = Risk-free rate                                     │
│  • Rₘ = Market return                                      │
│  • β = Stock's sensitivity to market                       │
│  • α = Alpha (excess return)                               │
│                                                             │
│  Interpretation:                                            │
│  • β = 1.5: Stock moves 1.5× the market movement          │
│  • α = 0.02: Stock generates 2% excess return             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
13.5 Application 5: Marketing Mix Modeling
text

┌─────────────────────────────────────────────────────────────┐
│                MARKETING MIX MODELING                       │
│                                                             │
│  Model:                                                     │
│  Sales = β₀ + β₁×TV_ads + β₂×Radio_ads + β₃×Digital_ads   │
│                                                             │
│  Real Example Results:                                      │
│  ┌──────────────┬────────────┬─────────────────────┐       │
│  │ Channel      │ Coefficient│ Interpretation      │       │
│  ├──────────────┼────────────┼─────────────────────┤       │
│  │ TV           │ 0.045      │ $1 TV → $0.045 sales│       │
│  │ Radio        │ 0.188      │ $1 Radio→$0.19 sales│       │
│  │ Digital      │ 0.002      │ $1 Digital→$0.002   │       │
│  └──────────────┴────────────┴─────────────────────┘       │
│                                                             │
│  Decision: Shift budget from Digital to Radio!             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
13.6 When Linear Regression Wins
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  LINEAR REGRESSION IS BEST WHEN:                           │
│                                                             │
│  ✓ Interpretability is crucial                             │
│    (Need to explain to stakeholders)                       │
│                                                             │
│  ✓ Understanding relationships matters                     │
│    (Which features affect outcome?)                        │
│                                                             │
│  ✓ Data size is limited                                    │
│    (Complex models need more data)                         │
│                                                             │
│  ✓ Quick baseline needed                                   │
│    (Start simple, then add complexity)                     │
│                                                             │
│  ✓ Prediction speed matters                                │
│    (Linear is very fast)                                   │
│                                                             │
│  ✓ Regulatory requirements                                 │
│    (Finance, healthcare need explainable models)           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
Chapter 14: Interview Questions & Answers {#chapter-14-interview}
14.1 Basic Level Questions
Q1: What is Linear Regression?
text

ANSWER:
Linear Regression is a supervised machine learning algorithm that 
predicts a continuous target variable by finding the best linear 
relationship between input features (X) and output (Y).

The model equation: ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ

It minimizes the sum of squared differences between predicted 
and actual values (Ordinary Least Squares).
Q2: What are the assumptions of Linear Regression?
text

ANSWER (L.I.N.E.R):
1. Linearity: Relationship between X and Y is linear
2. Independence: Observations are independent
3. Normality: Residuals follow normal distribution
4. Equal Variance: Homoscedasticity (constant variance)
5. No multicollinearity: Features are not highly correlated

Tip: Remember "LINER" - like the ship that sails STRAIGHT (linear)!
Q3: What is the difference between R² and Adjusted R²?
text

ANSWER:
R² (Coefficient of Determination):
• Measures % of variance in Y explained by model
• ALWAYS increases when adding features (even useless ones)
• Range: 0 to 1 (can be negative on test data)

Adjusted R²:
• Penalizes adding unnecessary features
• Can DECREASE when adding useless features
• Formula: 1 - [(1-R²)(n-1)/(n-k-1)]
• Use when comparing models with different # of features
Q4: What is the difference between MSE, RMSE, and MAE?
text

ANSWER:
┌─────────┬──────────────────┬─────────────────────────┐
│ Metric  │ Formula          │ Key Property            │
├─────────┼──────────────────┼─────────────────────────┤
│ MAE     │ Σ|y-ŷ|/n         │ Robust to outliers      │
│ MSE     │ Σ(y-ŷ)²/n        │ Penalizes large errors  │
│ RMSE    │ √MSE             │ Same unit as Y          │
└─────────┴──────────────────┴─────────────────────────┘

Choose MAE if outliers should be treated equally.
Choose RMSE/MSE if large errors are particularly bad.
14.2 Intermediate Level Questions
Q5: How do you handle multicollinearity?
text

ANSWER:
Detection:
• Correlation matrix (r > 0.8 is concerning)
• VIF > 10 indicates severe multicollinearity

Solutions:
1. Remove one of the correlated features
2. Combine correlated features (create average/index)
3. Use PCA to create uncorrelated components
4. Use Ridge Regression (L2 regularization)
5. Collect more data
Q6: Explain Ridge vs Lasso vs Elastic Net
text

ANSWER:
┌─────────────┬────────────────────┬────────────────────┐
│             │ Ridge (L2)         │ Lasso (L1)         │
├─────────────┼────────────────────┼────────────────────┤
│ Penalty     │ λΣβ²               │ λΣ|β|             │
│ Coefficients│ Shrinks, not zero  │ Can become zero    │
│ Feature Sel │ No                 │ Yes                │
│ Use Case    │ Multicollinearity  │ Sparse models      │
└─────────────┴────────────────────┴────────────────────┘

Elastic Net: Combines both! Best when features are correlated 
AND you want feature selection.
Q7: What is the Normal Equation and when does it fail?
text

ANSWER:
Normal Equation: β = (XᵀX)⁻¹Xᵀy

Advantages:
• Closed-form solution (no iterations)
• Exact answer
• No learning rate to tune

When it fails:
1. XᵀX is singular (not invertible)
   - Causes: Multicollinearity, features > samples
   - Solution: Use regularization or pseudo-inverse

2. Computationally expensive for large datasets
   - Matrix inversion is O(n³)
   - Solution: Use Gradient Descent instead
Q8: Explain Gradient Descent and its variants
text

ANSWER:
Gradient Descent: Iterative optimization to minimize cost function

Update Rule: β = β - α × ∇J(β)

Variants:
┌────────────────┬──────────────────────────────────────┐
│ Batch GD       │ Uses ALL data per iteration          │
│                │ Slow but stable                       │
├────────────────┼──────────────────────────────────────┤
│ Stochastic GD  │ Uses ONE sample per iteration        │
│                │ Fast but noisy                        │
├────────────────┼──────────────────────────────────────┤
│ Mini-batch GD  │ Uses SUBSET per iteration            │
│                │ Best of both, most common             │
└────────────────┴──────────────────────────────────────┘

Key hyperparameter: Learning rate (α)
• Too small → slow convergence
• Too large → divergence/oscillation
14.3 Advanced Level Questions
Q9: How would you handle heteroscedasticity?
text

ANSWER:
Detection:
• Visual: Residual vs Fitted plot (funnel shape)
• Tests: Breusch-Pagan, White's test

Solutions:
1. Transform Y: log(Y), sqrt(Y)
2. Weighted Least Squares (WLS)
   - Give less weight to high-variance observations
3. Use Robust Standard Errors (HC0, HC1, HC3)
4. Generalized Least Squares (GLS)

Code example (WLS):
Weights = 1/variance_estimate
weighted_model.fit(X, y, sample_weight=weights)
Q10: Derive the OLS estimator
text

ANSWER:
Goal: Minimize J(β) = ||y - Xβ||²

Step 1: Expand
J(β) = (y - Xβ)ᵀ(y - Xβ)
     = yᵀy - 2βᵀXᵀy + βᵀXᵀXβ

Step 2: Differentiate w.r.t β
∂J/∂β = -2Xᵀy + 2XᵀXβ

Step 3: Set to zero
XᵀXβ = Xᵀy

Step 4: Solve for β
β = (XᵀX)⁻¹Xᵀy  ✓
Q11: What is the bias-variance tradeoff?
text

ANSWER:
Total Error = Bias² + Variance + Irreducible Error

┌───────────────────────────────────────────────────────────┐
│                                                           │
│  Bias: Error from wrong model assumptions                │
│        (underfitting - model too simple)                 │
│                                                           │
│  Variance: Error from sensitivity to training data       │
│            (overfitting - model too complex)             │
│                                                           │
│  Tradeoff:                                                │
│  ┌─────────────┬─────────────┬────────────┐              │
│  │ Simple Model│ ← Optimal → │Complex Model│             │
│  │ High Bias   │   Balance   │High Variance│             │
│  │ Low Variance│             │Low Bias     │             │
│  └─────────────┴─────────────┴────────────┘              │
│                                                           │
│  Linear Regression: Generally high bias, low variance    │
│  Regularization: Increases bias, decreases variance      │
│                                                           │
└───────────────────────────────────────────────────────────┘
Q12: How do you choose between Normal Equation and Gradient Descent?
text

ANSWER:
┌──────────────────┬─────────────────┬─────────────────────┐
│ Criteria         │ Normal Equation │ Gradient Descent    │
├──────────────────┼─────────────────┼─────────────────────┤
│ # Features       │ n < 10,000      │ Any (even millions) │
│ # Samples        │ Any             │ Large datasets      │
│ Computation      │ O(n³)           │ O(kn) per iteration│
│ Learning Rate    │ Not needed      │ Must tune           │
│ Feature Scaling  │ Not needed      │ Required            │
│ Exact Solution   │ Yes             │ Approximate         │
│ Memory           │ Need XᵀX        │ Batch at a time     │
└──────────────────┴─────────────────┴─────────────────────┘

Rule of thumb:
• Small dataset, few features → Normal Equation
• Large dataset or many features → Gradient Descent
Q13: Why does Lasso produce sparse solutions but Ridge doesn't?
text

ANSWER:
Geometric Interpretation:

Ridge (L2) constraint: Circle
Lasso (L1) constraint: Diamond

┌─────────────────────┬─────────────────────┐
│      RIDGE          │      LASSO          │
│                     │                     │
│     ╭─────╮         │       ╱╲            │
│    ╱   ●   ╲        │      ╱  ╲           │
│   │    ◯   │        │     ╱ ●  ╲          │
│    ╲      ╱         │    ◯      ╲         │ 
│     ╰─────╯         │     ╲    ╱          │
│                     │      ╲  ╱           │
│ Solution (◯) on     │       ╲╱            │
│ curved edge         │ Solution (◯) at     │
│                     │ CORNER (axis)       │
│ → Coefficients      │ → Some coefficients │
│   small but ≠ 0     │   EXACTLY 0         │
└─────────────────────┴─────────────────────┘

The corners of the diamond touch the axes, meaning 
at least one coefficient becomes exactly zero!
14.4 Coding Questions
Q14: Implement Linear Regression from scratch
Python

def linear_regression(X, y):
    """
    Implement OLS Linear Regression.
    Returns: coefficients including intercept
    """
    # Add column of ones for intercept
    n = len(y)
    X_with_bias = np.column_stack([np.ones(n), X])
    
    # Normal Equation: β = (XᵀX)⁻¹Xᵀy
    XtX = X_with_bias.T @ X_with_bias
    Xty = X_with_bias.T @ y
    beta = np.linalg.solve(XtX, Xty)  # More stable than inverse
    
    return beta
Q15: How would you detect and handle outliers in Linear Regression?
Python

def detect_outliers(y, y_pred):
    """
    Detect outliers using standardized residuals.
    """
    residuals = y - y_pred
    std_residuals = (residuals - np.mean(residuals)) / np.std(residuals)
    
    # Points with |standardized residual| > 3 are outliers
    outlier_mask = np.abs(std_residuals) > 3
    
    return outlier_mask, std_residuals

# Options to handle:
# 1. Remove outliers: X_clean = X[~outlier_mask]
# 2. Cap values: y_capped = np.clip(y, lower, upper)
# 3. Use robust regression (Huber loss)
# 4. Transform data: y_log = np.log(y)
Chapter 15: Advanced Topics & Research Directions {#chapter-15-advanced}
15.1 Generalized Linear Models (GLM)
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  GLM extends Linear Regression to different distributions  │
│                                                             │
│  Components:                                                │
│  1. Random Component: Y follows distribution from exp.     │
│     family (Normal, Binomial, Poisson, etc.)               │
│  2. Systematic Component: Linear predictor η = Xβ          │
│  3. Link Function: g(μ) = η, connects mean to predictor    │
│                                                             │
│  Examples:                                                  │
│  ┌──────────────────┬────────────────┬─────────────────┐   │
│  │ Distribution     │ Link Function  │ Use Case        │   │
│  ├──────────────────┼────────────────┼─────────────────┤   │
│  │ Normal           │ Identity       │ Continuous Y    │   │
│  │ Binomial         │ Logit          │ Binary Y        │   │
│  │ Poisson          │ Log            │ Count Y         │   │
│  │ Gamma            │ Inverse        │ Positive cont.  │   │
│  └──────────────────┴────────────────┴─────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
15.2 Robust Regression Methods
text

When OLS assumptions are violated:

1. Huber Regression:
   - Combines MSE (for small errors) and MAE (for large errors)
   - Less sensitive to outliers

2. RANSAC (Random Sample Consensus):
   - Fits model on random subsets
   - Identifies inliers vs outliers
   - Good for data with many outliers

3. Theil-Sen Estimator:
   - Uses median of slopes between all point pairs
   - Highly robust to outliers (up to 29% outliers)

4. Quantile Regression:
   - Predicts different quantiles (median, percentiles)
   - Shows full distribution of Y, not just mean
15.3 Bayesian Linear Regression
text

┌─────────────────────────────────────────────────────────────┐
│            BAYESIAN LINEAR REGRESSION                       │
│                                                             │
│  Key Difference from OLS:                                   │
│  • OLS gives point estimates of β                          │
│  • Bayesian gives DISTRIBUTION of β                        │
│                                                             │
│  Components:                                                │
│  1. Prior: P(β) - Initial belief about β                   │
│  2. Likelihood: P(y|X,β) - How well β explains data        │
│  3. Posterior: P(β|X,y) ∝ P(y|X,β) × P(β)                 │
│                                                             │
│  Advantages:                                                │
│  ✓ Uncertainty quantification                               │
│  ✓ Incorporates prior knowledge                            │
│  ✓ Natural regularization                                  │
│  ✓ Works with small datasets                               │
│                                                             │
│  With conjugate prior (Normal):                            │
│  Posterior is also Normal → Closed-form solution!          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
15.4 Online Learning (Stochastic Methods)
text

For streaming data (data arrives continuously):

Traditional: Train once on all data
Online:      Update model as each new point arrives

Update rule for SGD:
βₜ₊₁ = βₜ - αₜ × ∇J(βₜ; xₜ, yₜ)

Key considerations:
• Learning rate schedule: αₜ = α₀ / (1 + decay × t)
• Forgetting factor: Give less weight to old data
• Mini-batches: Update with small groups of new data
15.5 Interpretability & Explainability
text

┌─────────────────────────────────────────────────────────────┐
│           INTERPRETING LINEAR MODELS                        │
│                                                             │
│  Coefficient Interpretation:                                │
│  β₁ = 2.5 means: "Holding other variables constant,        │
│                   1 unit increase in X₁ leads to           │
│                   2.5 unit increase in Y"                   │
│                                                             │
│  Standardized Coefficients:                                 │
│  β*ⱼ = βⱼ × (σxⱼ/σy)                                       │
│  Shows relative importance of features                     │
│                                                             │
│  Feature Importance:                                        │
│  • |Standardized coefficient|                              │
│  • t-statistic                                             │
│  • Permutation importance                                  │
│                                                             │
│  Confidence Intervals:                                      │
│  β̂ ± t₀.₀₂₅ × SE(β̂)                                        │
│  95% CI: "We're 95% confident true β is in this range"    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
15.6 Extensions & Variations
text

1. Polynomial Regression:
   ŷ = β₀ + β₁x + β₂x² + β₃x³ + ...
   (Still linear in parameters!)

2. Weighted Least Squares:
   Minimize: Σwᵢ(yᵢ - ŷᵢ)²
   Different observations have different importance

3. Generalized Least Squares (GLS):
   Handles correlated errors
   β = (XᵀΩ⁻¹X)⁻¹XᵀΩ⁻¹y

4. Total Least Squares:
   When X also has measurement errors
   Minimizes perpendicular distance to line

5. Partial Least Squares (PLS):
   Combines PCA with regression
   Good when features >> samples

6. Locally Weighted Regression (LOESS/LOWESS):
   Fits local linear models
   Non-parametric, captures curves
15.7 Future Directions & Research
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  1. Automated Feature Engineering                           │
│     - Learning optimal transformations                     │
│     - Neural network + linear interpretability             │
│                                                             │
│  2. Causal Inference                                        │
│     - Moving beyond correlation                            │
│     - Instrumental variables                               │
│     - Double ML                                            │
│                                                             │
│  3. Federated Learning                                      │
│     - Train across distributed data                        │
│     - Privacy-preserving                                   │
│                                                             │
│  4. High-dimensional Statistics                            │
│     - When p >> n                                          │
│     - Sparse estimation                                    │
│     - Compressed sensing                                   │
│                                                             │
│  5. Conformal Prediction                                    │
│     - Distribution-free uncertainty                        │
│     - Guaranteed coverage                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
📝 Quick Reference Cheat Sheet
text

┌─────────────────────────────────────────────────────────────┐
│              LINEAR REGRESSION CHEAT SHEET                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  EQUATION:     ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ          │
│  MATRIX FORM:  ŷ = Xβ                                       │
│  OLS SOLUTION: β = (XᵀX)⁻¹Xᵀy                              │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  ASSUMPTIONS (LINER):                                       │
│  L - Linearity                                              │
│  I - Independence                                           │
│  N - Normality of residuals                                 │
│  E - Equal variance (Homoscedasticity)                     │
│  R - No multicollinearity                                   │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  METRICS:                                                   │
│  R² = 1 - (SS_res/SS_tot)     [Higher is better, max 1]   │
│  MSE = Σ(y-ŷ)²/n              [Lower is better]           │
│  RMSE = √MSE                   [Same units as Y]           │
│  MAE = Σ|y-ŷ|/n                [Robust to outliers]        │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  REGULARIZATION:                                            │
│  Ridge (L2): Cost + λΣβ²      [Shrinks coefficients]      │
│  Lasso (L1): Cost + λΣ|β|     [Makes coefficients zero]   │
│  Elastic:    L1 + L2          [Best of both]               │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  GRADIENT DESCENT:                                          │
│  β_new = β_old - α × ∇J(β)                                 │
│  Always scale features first!                              │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  COMMON PROBLEMS → SOLUTIONS:                               │
│  Overfitting    → Regularization, less features            │
│  Underfitting   → More features, polynomial                │
│  Outliers       → Robust methods, remove/cap               │
│  Multicollinear → Remove, combine, Ridge, PCA              │
│  Heterosced.    → Transform Y, WLS, robust SE              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
🎯 Final Summary
text

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   You've now mastered Linear Regression!                   │
│                                                             │
│   ✓ Fundamentals: Equation, intuition, geometry            │
│   ✓ Mathematics: OLS derivation, matrix form               │
│   ✓ Assumptions: LINER and how to check them               │
│   ✓ Evaluation: R², MSE, RMSE, MAE, Adjusted R²           │
│   ✓ Feature Engineering: Scaling, encoding, selection      │
│   ✓ Regularization: Ridge, Lasso, Elastic Net             │
│   ✓ Optimization: Gradient Descent variants                │
│   ✓ Problems & Solutions: Practical troubleshooting       │
│   ✓ Implementation: From scratch in Python                │
│   ✓ Applications: Real-world use cases                    │
│   ✓ Interview Prep: Common questions with answers         │
│   ✓ Advanced Topics: GLM, Bayesian, Robust methods        │
│                                                             │
│   Remember:                                                 │
│   "Linear Regression is the foundation of ML.              │
│    Master it, and everything else becomes easier!"         │
│                                                             │
│   Good luck with your ML career! 🚀                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘