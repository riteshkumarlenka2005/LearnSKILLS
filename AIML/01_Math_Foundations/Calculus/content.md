1. Why Calculus for AI/ML?
🎯 The Big Picture
Imagine you're trying to teach a computer to recognize cats in photos. The computer starts with random guesses and needs to improve its accuracy. But how does it know which direction to improve? How does it know how much to change its parameters?

The answer is CALCULUS!

text

┌─────────────────────────────────────────────────────────────────┐
│                    WHERE CALCULUS APPEARS IN ML                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📊 TRAINING NEURAL NETWORKS                                    │
│     └── Backpropagation uses derivatives to update weights      │
│                                                                 │
│  📉 OPTIMIZATION                                                │
│     └── Gradient Descent finds minimum of loss function         │
│                                                                 │
│  📈 LOSS FUNCTIONS                                              │
│     └── Derivatives tell us how to reduce errors                │
│                                                                 │
│  🔄 REGULARIZATION                                              │
│     └── Derivatives of penalty terms                            │
│                                                                 │
│  📊 PROBABILITY DISTRIBUTIONS                                   │
│     └── Integrals for continuous probabilities                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
🤔 Real-World Analogy
Think of calculus like a GPS navigation system:

Current Position = Current model parameters
Destination = Optimal model (minimum error)
Derivative/Gradient = Which direction to drive
Learning Rate = How fast to drive
Gradient Descent = The algorithm that follows directions
2. Prerequisites
Before diving in, make sure you understand:

text

✅ Basic Algebra (solving equations, manipulating expressions)
✅ Exponents and Logarithms
✅ Basic Trigonometry (sin, cos, tan)
✅ Coordinate Geometry (x-y plane, plotting points)
✅ Function notation f(x)
Quick Refresher
Python

# Python code to visualize basic concepts
import numpy as np
import matplotlib.pyplot as plt

# Creating a simple function
x = np.linspace(-5, 5, 100)
y = x**2  # Parabola

plt.figure(figsize=(10, 6))
plt.plot(x, y, 'b-', linewidth=2)
plt.xlabel('x')
plt.ylabel('y = x²')
plt.title('A Simple Quadratic Function')
plt.grid(True)
plt.axhline(y=0, color='k', linewidth=0.5)
plt.axvline(x=0, color='k', linewidth=0.5)
plt.show()
3. Chapter 1: Functions - The Building Blocks
📚 What is a Function?
A function is a relationship that assigns exactly ONE output to each input.

text

┌─────────────────────────────────────────────────────────────────┐
│                         FUNCTION                                │
│                                                                 │
│         INPUT ──────► [ FUNCTION BOX ] ──────► OUTPUT           │
│           x   ──────►      f(x)       ──────►    y              │
│                                                                 │
│  Example: f(x) = x²                                             │
│           f(2) = 4                                              │
│           f(3) = 9                                              │
│           f(-2) = 4                                             │
└─────────────────────────────────────────────────────────────────┘
🔢 Types of Functions in ML
1. Linear Function
text

f(x) = mx + b

Where:
  m = slope (how steep the line is)
  b = y-intercept (where line crosses y-axis)
Python

# Linear Function Visualization
x = np.linspace(-5, 5, 100)

plt.figure(figsize=(12, 4))

# Different linear functions
slopes = [0.5, 1, 2]
for m in slopes:
    y = m * x + 1
    plt.plot(x, y, label=f'y = {m}x + 1')

plt.xlabel('x')
plt.ylabel('y')
plt.title('Linear Functions with Different Slopes')
plt.legend()
plt.grid(True)
plt.axhline(y=0, color='k', linewidth=0.5)
plt.axvline(x=0, color='k', linewidth=0.5)
plt.show()
ML Application: Linear Regression uses linear functions!

text

ŷ = w₁x₁ + w₂x₂ + ... + wₙxₙ + b
2. Quadratic Function
text

f(x) = ax² + bx + c

Shape: Parabola (U-shaped or inverted U)
ML Application: Many loss functions are quadratic (MSE)!

3. Exponential Function
text

f(x) = eˣ   (where e ≈ 2.71828...)

Properties:
- Always positive
- Grows very fast
- Its derivative equals itself! (d/dx eˣ = eˣ)
Python

# Exponential function
x = np.linspace(-3, 3, 100)
y = np.exp(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y, 'r-', linewidth=2)
plt.xlabel('x')
plt.ylabel('y = eˣ')
plt.title('Exponential Function')
plt.grid(True)
plt.show()
ML Application: Softmax function, probability calculations!

4. Logarithmic Function
text

f(x) = ln(x)   (natural logarithm, base e)
f(x) = log(x)  (common logarithm, base 10)

Properties:
- Only defined for x > 0
- Inverse of exponential
- ln(eˣ) = x
- e^(ln(x)) = x
ML Application: Cross-entropy loss, information theory!

5. Sigmoid Function (VERY IMPORTANT FOR ML!)
text

σ(x) = 1 / (1 + e⁻ˣ)

Properties:
- Output always between 0 and 1
- S-shaped curve
- Used in binary classification
Python

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

x = np.linspace(-10, 10, 100)
y = sigmoid(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y, 'g-', linewidth=2)
plt.xlabel('x')
plt.ylabel('σ(x)')
plt.title('Sigmoid Function - The Activation Function King!')
plt.axhline(y=0.5, color='r', linestyle='--', alpha=0.5)
plt.axhline(y=0, color='k', linewidth=0.5)
plt.axhline(y=1, color='k', linewidth=0.5)
plt.grid(True)
plt.show()
text

┌─────────────────────────────────────────────────────────────────┐
│                    SIGMOID FUNCTION VISUAL                      │
│                                                                 │
│    1.0 ─────────────────────────────────────██████████████      │
│                                         ████                    │
│                                      ███                        │
│    0.5 ─────────────────────────────█─────────────────────      │
│                                  ███                            │
│                              ████                               │
│    0.0 ██████████████████████─────────────────────────────      │
│        -10          -5          0          5          10        │
│                                                                 │
│    Key: Squishes any input to range (0, 1)                      │
│         Perfect for probabilities!                              │
└─────────────────────────────────────────────────────────────────┘
6. ReLU Function (Most Popular in Deep Learning!)
text

ReLU(x) = max(0, x)

         = 0,  if x < 0
         = x,  if x ≥ 0
Python

def relu(x):
    return np.maximum(0, x)

x = np.linspace(-5, 5, 100)
y = relu(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y, 'b-', linewidth=2)
plt.xlabel('x')
plt.ylabel('ReLU(x)')
plt.title('ReLU - Rectified Linear Unit')
plt.grid(True)
plt.axhline(y=0, color='k', linewidth=0.5)
plt.axvline(x=0, color='k', linewidth=0.5)
plt.show()
4. Chapter 2: Limits - The Foundation
📚 What is a Limit?
A limit describes what value a function approaches as the input approaches some value.

text

┌─────────────────────────────────────────────────────────────────┐
│                         LIMIT CONCEPT                           │
│                                                                 │
│   lim f(x) = L                                                  │
│   x→a                                                           │
│                                                                 │
│   "As x gets closer and closer to 'a',                          │
│    f(x) gets closer and closer to 'L'"                          │
│                                                                 │
│   Example: lim (x²) = 4                                         │
│            x→2                                                  │
│                                                                 │
│   As x approaches 2: 1.9² = 3.61                                │
│                       1.99² = 3.9601                            │
│                       1.999² = 3.996001                         │
│                       2² = 4  ✓                                 │
└─────────────────────────────────────────────────────────────────┘
🎯 Why Limits Matter for Derivatives
Derivatives are DEFINED using limits! Without understanding limits, you can't truly understand derivatives.

text

The derivative is defined as:

f'(x) = lim  [f(x + h) - f(x)]
        h→0  ─────────────────
                    h

This is asking: "What happens to the slope as we make
                the distance between two points infinitely small?"
📝 Limit Laws
text

┌─────────────────────────────────────────────────────────────────┐
│                         LIMIT LAWS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. Sum Rule:      lim [f(x) + g(x)] = lim f(x) + lim g(x)     │
│                    x→a                 x→a         x→a          │
│                                                                 │
│  2. Product Rule:  lim [f(x) · g(x)] = lim f(x) · lim g(x)     │
│                    x→a                 x→a         x→a          │
│                                                                 │
│  3. Quotient Rule: lim [f(x)/g(x)] = lim f(x) / lim g(x)       │
│                    x→a                x→a         x→a           │
│                    (provided lim g(x) ≠ 0)                      │
│                             x→a                                 │
│                                                                 │
│  4. Constant Rule: lim [c · f(x)] = c · lim f(x)               │
│                    x→a                  x→a                     │
│                                                                 │
│  5. Power Rule:    lim [f(x)]ⁿ = [lim f(x)]ⁿ                   │
│                    x→a           x→a                            │
└─────────────────────────────────────────────────────────────────┘
💡 Important Limits to Remember
Python

# Important limits for ML

# 1. lim (1 + 1/n)^n = e ≈ 2.71828
n_values = [1, 10, 100, 1000, 10000, 100000]
for n in n_values:
    result = (1 + 1/n)**n
    print(f"n = {n:6d}: (1 + 1/n)^n = {result:.10f}")

print(f"\ne = {np.e:.10f}")

# Output:
# n =      1: (1 + 1/n)^n = 2.0000000000
# n =     10: (1 + 1/n)^n = 2.5937424601
# n =    100: (1 + 1/n)^n = 2.7048138294
# n =   1000: (1 + 1/n)^n = 2.7169239322
# n =  10000: (1 + 1/n)^n = 2.7181459268
# n = 100000: (1 + 1/n)^n = 2.7182682372
# e = 2.7182818285
text

┌─────────────────────────────────────────────────────────────────┐
│                    IMPORTANT LIMITS FOR ML                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. lim sin(x)/x = 1      (Used in Fourier transforms)         │
│     x→0                                                         │
│                                                                 │
│  2. lim (1 + 1/n)ⁿ = e    (Definition of e)                    │
│     n→∞                                                         │
│                                                                 │
│  3. lim (eˣ - 1)/x = 1    (Useful for exponential limits)      │
│     x→0                                                         │
│                                                                 │
│  4. lim ln(1 + x)/x = 1   (Logarithm approximation)            │
│     x→0                                                         │
│                                                                 │
│  5. lim xⁿ/eˣ = 0         (Exponential dominates polynomial)   │
│     x→∞                                                         │
└─────────────────────────────────────────────────────────────────┘
5. Chapter 3: Derivatives - The Heart of ML
📚 What is a Derivative?
The derivative measures the instantaneous rate of change of a function.

Think of it as: "How fast is the function changing at this exact point?"

🚗 Real-World Analogy: Speedometer
text

┌─────────────────────────────────────────────────────────────────┐
│                    DERIVATIVE = SPEEDOMETER                     │
│                                                                 │
│   Position (where you are)     →  Function f(x)                 │
│   Velocity (how fast moving)   →  First Derivative f'(x)        │
│   Acceleration (speeding up?)  →  Second Derivative f''(x)      │
│                                                                 │
│   Example:                                                      │
│   If position = t²  (you're accelerating)                       │
│   Then velocity = 2t  (speed increases with time)               │
│   And acceleration = 2  (constant acceleration)                 │
└─────────────────────────────────────────────────────────────────┘
📐 Geometric Interpretation
The derivative at a point is the slope of the tangent line at that point.

text

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│     y │                           ╱                             │
│       │                      ╱╱╱╱╱                              │
│       │                  ╱╱╱╱                                   │
│       │              ●━━━━━━━━━━  ← Tangent line at point      │
│       │          ╱╱╱╱│                                          │
│       │      ╱╱╱╱    │                                          │
│       │  ╱╱╱╱        │                                          │
│       │╱╱            │                                          │
│       └──────────────┼───────────────────── x                   │
│                      a                                          │
│                                                                 │
│   The SLOPE of this tangent line = f'(a) = derivative at 'a'   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📝 Formal Definition
text

                    f(x + h) - f(x)
f'(x) = lim         ───────────────
        h→0               h

This is called the "difference quotient" or "first principles"
💻 Computing Derivative from First Principles
Let's derive the derivative of f(x) = x² step by step:

text

Step 1: Write f(x + h)
        f(x + h) = (x + h)²
                 = x² + 2xh + h²

Step 2: Compute f(x + h) - f(x)
        = (x² + 2xh + h²) - x²
        = 2xh + h²

Step 3: Divide by h
        = (2xh + h²) / h
        = 2x + h

Step 4: Take limit as h → 0
        lim (2x + h) = 2x
        h→0

Therefore: f'(x) = 2x  ✓
Python

# Numerical verification of derivative
def f(x):
    return x**2

def numerical_derivative(f, x, h=0.0001):
    return (f(x + h) - f(x)) / h

# Test at x = 3
x = 3
numerical = numerical_derivative(f, x)
analytical = 2 * x  # We derived this above

print(f"At x = {x}:")
print(f"  Numerical derivative:  {numerical:.6f}")
print(f"  Analytical derivative: {analytical:.6f}")
print(f"  Difference:            {abs(numerical - analytical):.10f}")

# Output:
# At x = 3:
#   Numerical derivative:  6.000100
#   Analytical derivative: 6.000000
#   Difference:            0.0001000000
🎯 Why Derivatives Matter for ML
text

┌─────────────────────────────────────────────────────────────────┐
│                DERIVATIVES IN MACHINE LEARNING                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. GRADIENT DESCENT                                            │
│     ───────────────                                             │
│     We use derivatives to find direction of steepest descent    │
│     to minimize loss function.                                  │
│                                                                 │
│     weight_new = weight_old - learning_rate × ∂Loss/∂weight     │
│                                                                 │
│  2. BACKPROPAGATION                                             │
│     ───────────────                                             │
│     Neural networks use chain rule to compute gradients         │
│     for all weights layer by layer.                             │
│                                                                 │
│  3. OPTIMIZATION                                                │
│     ────────────                                                │
│     Finding minimum/maximum of functions:                       │
│     - If f'(x) > 0: function increasing                        │
│     - If f'(x) < 0: function decreasing                        │
│     - If f'(x) = 0: potential min/max (critical point)         │
│                                                                 │
│  4. UNDERSTANDING MODEL SENSITIVITY                             │
│     ──────────────────────────────                              │
│     How much does output change when input changes?             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6. Chapter 4: Differentiation Rules
📋 The Rules That Make Life Easy
Instead of computing derivatives from first principles every time, we use rules!

1. Constant Rule
text

d/dx [c] = 0

"The derivative of a constant is zero"

Example: d/dx [5] = 0
         d/dx [π] = 0
Intuition: A constant doesn't change, so its rate of change is 0.

2. Power Rule ⭐ (MOST USED!)
text

d/dx [xⁿ] = n · xⁿ⁻¹

"Bring down the power, reduce power by 1"

Examples:
  d/dx [x²] = 2x¹ = 2x
  d/dx [x³] = 3x²
  d/dx [x⁵] = 5x⁴
  d/dx [x¹] = 1·x⁰ = 1
  d/dx [x⁻¹] = -1·x⁻² = -1/x²
  d/dx [√x] = d/dx [x^(1/2)] = (1/2)·x^(-1/2) = 1/(2√x)
Python

# Verifying Power Rule
import sympy as sp

x = sp.Symbol('x')

expressions = [x**2, x**3, x**5, x**(-1), sp.sqrt(x)]
for expr in expressions:
    derivative = sp.diff(expr, x)
    print(f"d/dx [{expr}] = {derivative}")

# Output:
# d/dx [x**2] = 2*x
# d/dx [x**3] = 3*x**2
# d/dx [x**5] = 5*x**4
# d/dx [x**(-1)] = -1/x**2
# d/dx [sqrt(x)] = 1/(2*sqrt(x))
3. Constant Multiple Rule
text

d/dx [c · f(x)] = c · f'(x)

"Constants can be pulled out"

Examples:
  d/dx [3x²] = 3 · 2x = 6x
  d/dx [5x³] = 5 · 3x² = 15x²
4. Sum/Difference Rule
text

d/dx [f(x) ± g(x)] = f'(x) ± g'(x)

"Derivative of sum/difference = sum/difference of derivatives"

Example:
  d/dx [x² + 3x - 5] = 2x + 3 - 0 = 2x + 3
5. Product Rule ⭐
text

d/dx [f(x) · g(x)] = f'(x)·g(x) + f(x)·g'(x)

Memory trick: "First times derivative of second, 
              plus second times derivative of first"

Example:
  d/dx [x² · sin(x)] = 2x·sin(x) + x²·cos(x)
text

┌─────────────────────────────────────────────────────────────────┐
│                        PRODUCT RULE                             │
│                                                                 │
│   d/dx [f(x) · g(x)] = f'(x)·g(x) + f(x)·g'(x)                 │
│                                                                 │
│   Visual:                                                       │
│                                                                 │
│        f(x)        g(x)                                         │
│         │           │                                           │
│         ▼           ▼                                           │
│       ┌───┐       ┌───┐                                         │
│       │ × │───────│ × │                                         │
│       └───┘       └───┘                                         │
│         │           │                                           │
│    ┌────┴────┐ ┌────┴────┐                                      │
│    │         │ │         │                                      │
│    ▼         ▼ ▼         ▼                                      │
│  f'(x)·g(x)  +  f(x)·g'(x)                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
6. Quotient Rule
text

d/dx [f(x)/g(x)] = [f'(x)·g(x) - f(x)·g'(x)] / [g(x)]²

Memory trick: "Low d-high minus high d-low, over low squared"

Example:
  d/dx [x²/(x+1)] = [2x·(x+1) - x²·1] / (x+1)²
                  = [2x² + 2x - x²] / (x+1)²
                  = [x² + 2x] / (x+1)²
7. Chain Rule ⭐⭐⭐ (MOST IMPORTANT FOR ML!)
text

d/dx [f(g(x))] = f'(g(x)) · g'(x)

"Derivative of outer function (evaluated at inner) 
 times derivative of inner function"

Memory trick: "Outside-Inside" rule
text

┌─────────────────────────────────────────────────────────────────┐
│                        CHAIN RULE                               │
│                                                                 │
│   If y = f(g(x)), let u = g(x), so y = f(u)                    │
│                                                                 │
│   Then: dy/dx = dy/du · du/dx                                   │
│                                                                 │
│   Visual:                                                       │
│                                                                 │
│   x ──────► g(x) = u ──────► f(u) = y                          │
│       du/dx            dy/du                                    │
│                                                                 │
│   dy/dx = dy/du × du/dx                                         │
│         = f'(u) × g'(x)                                         │
│         = f'(g(x)) × g'(x)                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Examples:

text

Example 1: d/dx [(2x + 1)³]
───────────────────────────
Let u = 2x + 1 (inner function)
Let y = u³ (outer function)

dy/du = 3u²
du/dx = 2

dy/dx = 3u² · 2 = 6u² = 6(2x + 1)²


Example 2: d/dx [sin(x²)]
─────────────────────────
Let u = x² (inner function)
Let y = sin(u) (outer function)

dy/du = cos(u)
du/dx = 2x

dy/dx = cos(u) · 2x = 2x·cos(x²)


Example 3: d/dx [e^(3x)]
─────────────────────────
Let u = 3x (inner function)
Let y = eᵘ (outer function)

dy/du = eᵘ
du/dx = 3

dy/dx = eᵘ · 3 = 3e^(3x)
Python

# Chain Rule Examples in Python
import sympy as sp

x = sp.Symbol('x')

# Example 1: (2x + 1)³
expr1 = (2*x + 1)**3
print(f"d/dx [{expr1}] = {sp.diff(expr1, x)}")

# Example 2: sin(x²)
expr2 = sp.sin(x**2)
print(f"d/dx [{expr2}] = {sp.diff(expr2, x)}")

# Example 3: e^(3x)
expr3 = sp.exp(3*x)
print(f"d/dx [{expr3}] = {sp.diff(expr3, x)}")

# Output:
# d/dx [(2*x + 1)**3] = 6*(2*x + 1)**2
# d/dx [sin(x**2)] = 2*x*cos(x**2)
# d/dx [exp(3*x)] = 3*exp(3*x)
📋 Common Derivatives Table
text

┌────────────────────────────────────────────────────────────────┐
│                    COMMON DERIVATIVES                          │
├────────────────────┬───────────────────────────────────────────┤
│     f(x)           │              f'(x)                        │
├────────────────────┼───────────────────────────────────────────┤
│     c (constant)   │              0                            │
│     x              │              1                            │
│     xⁿ             │              n·xⁿ⁻¹                       │
│     eˣ             │              eˣ                           │
│     e^(kx)         │              k·e^(kx)                     │
│     ln(x)          │              1/x                          │
│     log₁₀(x)       │              1/(x·ln(10))                 │
│     sin(x)         │              cos(x)                       │
│     cos(x)         │              -sin(x)                      │
│     tan(x)         │              sec²(x)                      │
│     1/x            │              -1/x²                        │
│     √x             │              1/(2√x)                      │
│     aˣ             │              aˣ·ln(a)                     │
├────────────────────┴───────────────────────────────────────────┤
│                ML-SPECIFIC FUNCTIONS                           │
├────────────────────┬───────────────────────────────────────────┤
│     σ(x) sigmoid   │  σ(x)·(1 - σ(x))                         │
│     tanh(x)        │  1 - tanh²(x)                            │
│     ReLU(x)        │  0 if x<0, 1 if x>0 (undefined at 0)     │
│     Leaky ReLU     │  α if x<0, 1 if x>0                      │
│     softplus(x)    │  σ(x)                                    │
└────────────────────┴───────────────────────────────────────────┘
🔥 Deriving Sigmoid Derivative (Important for ML!)
text

σ(x) = 1/(1 + e⁻ˣ)

Step 1: Rewrite as σ(x) = (1 + e⁻ˣ)⁻¹

Step 2: Apply chain rule
        Let u = 1 + e⁻ˣ
        σ = u⁻¹
        
        dσ/du = -u⁻² = -1/(1 + e⁻ˣ)²
        du/dx = -e⁻ˣ  (derivative of e⁻ˣ using chain rule)

Step 3: Multiply
        dσ/dx = -1/(1 + e⁻ˣ)² · (-e⁻ˣ)
              = e⁻ˣ/(1 + e⁻ˣ)²

Step 4: Simplify (this is the beautiful part!)
        = 1/(1 + e⁻ˣ) · e⁻ˣ/(1 + e⁻ˣ)
        = σ(x) · e⁻ˣ/(1 + e⁻ˣ)
        = σ(x) · (1 + e⁻ˣ - 1)/(1 + e⁻ˣ)
        = σ(x) · (1 - 1/(1 + e⁻ˣ))
        = σ(x) · (1 - σ(x))

THEREFORE: σ'(x) = σ(x) · (1 - σ(x)) ✓
Python

# Sigmoid and its derivative
def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def sigmoid_derivative(x):
    s = sigmoid(x)
    return s * (1 - s)

x = np.linspace(-6, 6, 100)

plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.plot(x, sigmoid(x), 'b-', linewidth=2, label='σ(x)')
plt.title('Sigmoid Function')
plt.xlabel('x')
plt.ylabel('σ(x)')
plt.grid(True)
plt.legend()

plt.subplot(1, 2, 2)
plt.plot(x, sigmoid_derivative(x), 'r-', linewidth=2, label="σ'(x)")
plt.title('Sigmoid Derivative')
plt.xlabel('x')
plt.ylabel("σ'(x)")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
text

┌─────────────────────────────────────────────────────────────────┐
│              SIGMOID AND ITS DERIVATIVE                         │
│                                                                 │
│   Sigmoid σ(x):              Derivative σ'(x):                  │
│                                                                 │
│   1.0 ───────────████        0.25 ─────────█████───────         │
│                ███                      ███     ███             │
│              ██                       ██           ██           │
│   0.5 ──────█───────────     0.125 ──█───────────────█──        │
│           ██                       ██                 ██        │
│        ███                        █                     █       │
│   0.0 ██────────────────     0.0 █───────────────────────█      │
│       -6    0    6              -6         0         6          │
│                                                                 │
│   Key Insight: Maximum derivative at x=0 (0.25)                 │
│                Derivative → 0 at extremes (vanishing gradient!) │
└─────────────────────────────────────────────────────────────────┘
7. Chapter 5: Partial Derivatives - Multivariable Magic
📚 Why Partial Derivatives?
In real ML, we don't have functions of just one variable. Neural networks have millions of parameters!

text

Loss = f(w₁, w₂, w₃, ..., wₙ, b₁, b₂, ..., bₘ)

We need to know: How does Loss change when we change EACH parameter?
📝 Definition
A partial derivative measures how a function changes with respect to one variable, while keeping all other variables constant.

text

Notation:
  ∂f/∂x  or  fₓ  or  ∂ₓf

"Round d" (∂) means "partial"
🎯 Visual Understanding
text

┌─────────────────────────────────────────────────────────────────┐
│                    PARTIAL DERIVATIVES                          │
│                                                                 │
│   Consider f(x, y) = x² + y²  (a paraboloid - bowl shape)      │
│                                                                 │
│              z                                                  │
│              │    ╱╲                                            │
│              │   ╱  ╲                                           │
│              │  ╱    ╲                                          │
│              │ ╱      ╲                                         │
│              │╱────────╲──────── y                              │
│             ╱│          ╲                                       │
│            ╱ │           ╲                                      │
│           x                                                     │
│                                                                 │
│   ∂f/∂x = 2x  (slope in x-direction, y held constant)          │
│   ∂f/∂y = 2y  (slope in y-direction, x held constant)          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📝 How to Compute
Rule: Treat all other variables as constants!

text

Example 1: f(x, y) = x²y + 3xy² - 2y + 5
───────────────────────────────────────────

∂f/∂x = ?
  Treat y as constant:
  = 2xy + 3y² - 0 + 0
  = 2xy + 3y²

∂f/∂y = ?
  Treat x as constant:
  = x² + 6xy - 2 + 0
  = x² + 6xy - 2


Example 2: f(x, y, z) = x²y + yz² + xz
──────────────────────────────────────────

∂f/∂x = 2xy + 0 + z = 2xy + z
∂f/∂y = x² + z² + 0 = x² + z²
∂f/∂z = 0 + 2yz + x = 2yz + x
Python

import sympy as sp

x, y, z = sp.symbols('x y z')

# Example 1
f1 = x**2 * y + 3*x*y**2 - 2*y + 5
print(f"f(x,y) = {f1}")
print(f"∂f/∂x = {sp.diff(f1, x)}")
print(f"∂f/∂y = {sp.diff(f1, y)}")

print()

# Example 2
f2 = x**2 * y + y*z**2 + x*z
print(f"f(x,y,z) = {f2}")
print(f"∂f/∂x = {sp.diff(f2, x)}")
print(f"∂f/∂y = {sp.diff(f2, y)}")
print(f"∂f/∂z = {sp.diff(f2, z)}")
🔥 ML Example: Linear Regression Loss
text

┌─────────────────────────────────────────────────────────────────┐
│              PARTIAL DERIVATIVES IN LINEAR REGRESSION           │
│                                                                 │
│   Model: ŷ = wx + b                                             │
│                                                                 │
│   Loss (MSE): L = (1/n) Σᵢ (yᵢ - ŷᵢ)²                          │
│             = (1/n) Σᵢ (yᵢ - wxᵢ - b)²                          │
│                                                                 │
│   For ONE data point: L = (y - wx - b)²                         │
│                                                                 │
│   ∂L/∂w = ?                                                     │
│   Let u = y - wx - b                                            │
│   L = u²                                                        │
│   ∂L/∂u = 2u                                                    │
│   ∂u/∂w = -x                                                    │
│   ∂L/∂w = 2u · (-x) = -2x(y - wx - b) = -2x(y - ŷ)             │
│                                                                 │
│   ∂L/∂b = ?                                                     │
│   ∂u/∂b = -1                                                    │
│   ∂L/∂b = 2u · (-1) = -2(y - wx - b) = -2(y - ŷ)               │
│                                                                 │
│   These gradients tell us how to update w and b!                │
└─────────────────────────────────────────────────────────────────┘
Python

# Gradient Descent for Linear Regression
import numpy as np

# Generate sample data
np.random.seed(42)
X = np.random.randn(100)
y_true = 3 * X + 2 + 0.5 * np.random.randn(100)  # y = 3x + 2 + noise

# Initialize parameters
w = 0.0
b = 0.0
learning_rate = 0.1
n = len(X)

# Gradient Descent
for epoch in range(100):
    # Predictions
    y_pred = w * X + b
    
    # Compute gradients (partial derivatives)
    dL_dw = (-2/n) * np.sum(X * (y_true - y_pred))
    dL_db = (-2/n) * np.sum(y_true - y_pred)
    
    # Update parameters
    w = w - learning_rate * dL_dw
    b = b - learning_rate * dL_db
    
    if epoch % 20 == 0:
        loss = np.mean((y_true - y_pred)**2)
        print(f"Epoch {epoch}: w = {w:.4f}, b = {b:.4f}, Loss = {loss:.4f}")

print(f"\nFinal: w = {w:.4f} (true: 3), b = {b:.4f} (true: 2)")
8. Chapter 6: Gradients - The Direction of Steepest Ascent
📚 What is a Gradient?
The gradient is a vector of ALL partial derivatives.

text

For f(x, y, z):

∇f = (∂f/∂x, ∂f/∂y, ∂f/∂z)

     ┌       ┐
     │ ∂f/∂x │
∇f = │ ∂f/∂y │
     │ ∂f/∂z │
     └       ┘
🎯 Key Properties of Gradients
text

┌─────────────────────────────────────────────────────────────────┐
│                    GRADIENT PROPERTIES                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. DIRECTION: Points in direction of STEEPEST ASCENT          │
│                                                                 │
│  2. MAGNITUDE: |∇f| gives the RATE of steepest ascent          │
│                                                                 │
│  3. PERPENDICULAR: Gradient is perpendicular to level curves   │
│                                                                 │
│  4. NEGATIVE GRADIENT: Points toward STEEPEST DESCENT          │
│     (This is what we use in optimization!)                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📐 Visual Understanding
text

┌─────────────────────────────────────────────────────────────────┐
│                    GRADIENT VISUALIZATION                       │
│                                                                 │
│   Consider a mountain (loss surface):                           │
│                                                                 │
│              ╱╲ ← Mountain peak (high loss)                     │
│             ╱  ╲                                                 │
│            ╱    ╲                                                │
│           ╱  ↗   ╲   ← Gradient points UP                       │
│          ╱   │    ╲                                             │
│         ╱    ●     ╲  ← You are here                            │
│        ╱   ↙       ╲  ← Negative gradient points DOWN           │
│       ╱             ╲                                           │
│      ─────────────────  ← Valley (low loss, goal!)              │
│                                                                 │
│   Gradient Descent: Move in direction of -∇f                    │
│   New position = Old position - learning_rate × ∇f              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
💻 Computing Gradients
text

Example: f(x, y) = x² + 2y² + xy

∂f/∂x = 2x + y
∂f/∂y = 4y + x

∇f = [2x + y]
     [4y + x]

At point (1, 2):
∇f(1,2) = [2(1) + 2] = [4]
          [4(2) + 1]   [9]
Python

import numpy as np
import matplotlib.pyplot as plt

def f(x, y):
    return x**2 + 2*y**2 + x*y

def gradient_f(x, y):
    df_dx = 2*x + y
    df_dy = 4*y + x
    return np.array([df_dx, df_dy])

# Create a grid
x = np.linspace(-3, 3, 20)
y = np.linspace(-3, 3, 20)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)

# Compute gradients
U = 2*X + Y
V = 4*Y + X

# Plot
plt.figure(figsize=(12, 5))

# Contour plot with gradient vectors
plt.subplot(1, 2, 1)
plt.contour(X, Y, Z, levels=20)
plt.quiver(X, Y, U, V, alpha=0.5)
plt.xlabel('x')
plt.ylabel('y')
plt.title('Gradient Vectors (Point UP)')
plt.colorbar(label='f(x,y)')

# Negative gradient (descent direction)
plt.subplot(1, 2, 2)
plt.contour(X, Y, Z, levels=20)
plt.quiver(X, Y, -U, -V, color='red', alpha=0.5)
plt.xlabel('x')
plt.ylabel('y')
plt.title('Negative Gradient Vectors (Point DOWN)')
plt.colorbar(label='f(x,y)')

plt.tight_layout()
plt.show()
🔥 Gradient Descent Algorithm
text

┌─────────────────────────────────────────────────────────────────┐
│                    GRADIENT DESCENT                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Algorithm:                                                    │
│   ──────────                                                    │
│   1. Initialize parameters θ randomly                           │
│   2. Repeat until convergence:                                  │
│      a. Compute gradient: ∇L(θ)                                 │
│      b. Update parameters: θ = θ - α∇L(θ)                       │
│                                                                 │
│   Where:                                                        │
│   - θ: parameters (weights and biases)                          │
│   - L(θ): loss function                                         │
│   - α: learning rate                                            │
│   - ∇L(θ): gradient of loss w.r.t. parameters                   │
│                                                                 │
│   Mathematical Form:                                            │
│   ──────────────────                                            │
│   θₙₑw = θₒₗₐ - α · ∂L/∂θ                                       │
│                                                                 │
│   For each weight wᵢ:                                           │
│   wᵢ_new = wᵢ_old - α · ∂L/∂wᵢ                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
Python

# Gradient Descent Visualization
def f(x, y):
    return x**2 + 2*y**2

def gradient(x, y):
    return np.array([2*x, 4*y])

# Gradient descent
x, y = 3.0, 3.0  # Start point
learning_rate = 0.1
history = [(x, y)]

for i in range(50):
    grad = gradient(x, y)
    x = x - learning_rate * grad[0]
    y = y - learning_rate * grad[1]
    history.append((x, y))

history = np.array(history)

# Plot
X_grid = np.linspace(-4, 4, 100)
Y_grid = np.linspace(-4, 4, 100)
X_mesh, Y_mesh = np.meshgrid(X_grid, Y_grid)
Z = f(X_mesh, Y_mesh)

plt.figure(figsize=(10, 8))
plt.contour(X_mesh, Y_mesh, Z, levels=30)
plt.plot(history[:, 0], history[:, 1], 'r.-', markersize=10, linewidth=2)
plt.plot(history[0, 0], history[0, 1], 'go', markersize=15, label='Start')
plt.plot(history[-1, 0], history[-1, 1], 'r*', markersize=20, label='End')
plt.xlabel('x')
plt.ylabel('y')
plt.title('Gradient Descent Path')
plt.legend()
plt.grid(True)
plt.show()

print(f"Final position: ({history[-1, 0]:.6f}, {history[-1, 1]:.6f})")
print(f"Should be: (0, 0)")
9. Chapter 7: Chain Rule - Backbone of Backpropagation
📚 Chain Rule Revisited (Multivariate)
In neural networks, we have compositions of functions. The chain rule is ESSENTIAL!

text

┌─────────────────────────────────────────────────────────────────┐
│                    CHAIN RULE IN NEURAL NETWORKS                │
│                                                                 │
│   Input → Layer 1 → Layer 2 → ... → Layer N → Output → Loss    │
│     x        h₁        h₂             hₙ        ŷ        L     │
│                                                                 │
│   To compute ∂L/∂w₁ (gradient for layer 1 weights):            │
│                                                                 │
│   ∂L/∂w₁ = ∂L/∂ŷ · ∂ŷ/∂hₙ · ... · ∂h₂/∂h₁ · ∂h₁/∂w₁           │
│                                                                 │
│   This is the CHAIN RULE applied repeatedly!                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📐 Visual: Computational Graph
text

┌─────────────────────────────────────────────────────────────────┐
│                    COMPUTATIONAL GRAPH                          │
│                                                                 │
│   Simple Example: L = (y - wx)²                                 │
│                                                                 │
│   Forward Pass:                                                 │
│   ─────────────                                                 │
│        ┌───┐                                                    │
│   w ───┤   │      ┌───┐      ┌───┐                              │
│        │ × ├─ z ──┤ - ├─ u ──┤ ² ├─── L                         │
│   x ───┤   │      └───┘      └───┘                              │
│        └───┘        ↑                                           │
│                     y                                           │
│                                                                 │
│   z = wx                                                        │
│   u = y - z                                                     │
│   L = u²                                                        │
│                                                                 │
│   Backward Pass (Chain Rule):                                   │
│   ───────────────────────────                                   │
│                                                                 │
│   ∂L/∂u = 2u                                                    │
│   ∂u/∂z = -1                                                    │
│   ∂z/∂w = x                                                     │
│                                                                 │
│   ∂L/∂w = ∂L/∂u · ∂u/∂z · ∂z/∂w                                 │
│         = 2u · (-1) · x                                         │
│         = -2x(y - wx)                                           │
│         = -2x(y - ŷ)   ← This is what we derived earlier!      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
💻 Implementing Backpropagation
Python

# Simple Neural Network with Backpropagation
import numpy as np

# Single neuron example
def forward(x, w, b):
    """Forward pass"""
    z = w * x + b          # Linear transformation
    a = 1 / (1 + np.exp(-z))  # Sigmoid activation
    return z, a

def backward(x, y, z, a, w):
    """Backward pass using chain rule"""
    # Loss: L = (y - a)²
    
    # ∂L/∂a = -2(y - a)
    dL_da = -2 * (y - a)
    
    # ∂a/∂z = a(1 - a)  (sigmoid derivative)
    da_dz = a * (1 - a)
    
    # ∂z/∂w = x
    dz_dw = x
    
    # ∂z/∂b = 1
    dz_db = 1
    
    # Chain rule: ∂L/∂w = ∂L/∂a · ∂a/∂z · ∂z/∂w
    dL_dw = dL_da * da_dz * dz_dw
    
    # Chain rule: ∂L/∂b = ∂L/∂a · ∂a/∂z · ∂z/∂b
    dL_db = dL_da * da_dz * dz_db
    
    return dL_dw, dL_db

# Training loop
np.random.seed(42)
w, b = np.random.randn(), np.random.randn()
learning_rate = 0.5

# Training data
X_train = np.array([0.5, 1.5, 2.5, 3.5])
y_train = np.array([0, 0, 1, 1])

print("Training Single Neuron...")
print("=" * 50)

for epoch in range(1000):
    total_loss = 0
    for x, y in zip(X_train, y_train):
        # Forward pass
        z, a = forward(x, w, b)
        
        # Compute loss
        loss = (y - a) ** 2
        total_loss += loss
        
        # Backward pass
        dL_dw, dL_db = backward(x, y, z, a, w)
        
        # Update weights
        w = w - learning_rate * dL_dw
        b = b - learning_rate * dL_db
    
    if epoch % 200 == 0:
        print(f"Epoch {epoch}: Loss = {total_loss/len(X_train):.6f}, w = {w:.4f}, b = {b:.4f}")

print("=" * 50)
print("\nTesting:")
for x, y in zip(X_train, y_train):
    _, pred = forward(x, w, b)
    print(f"Input: {x}, True: {y}, Predicted: {pred:.4f}")
🔥 Multi-Layer Chain Rule
text

┌─────────────────────────────────────────────────────────────────┐
│              CHAIN RULE IN MULTI-LAYER NETWORK                  │
│                                                                 │
│   Network: x → h₁ → h₂ → y → L                                  │
│                                                                 │
│   Forward:                                                      │
│   h₁ = σ(W₁x + b₁)                                              │
│   h₂ = σ(W₂h₁ + b₂)                                             │
│   y = W₃h₂ + b₃                                                 │
│   L = (ytrue - y)²                                              │
│                                                                 │
│   Backward (applying chain rule):                               │
│                                                                 │
│   ∂L/∂W₃ = ∂L/∂y · ∂y/∂W₃                                       │
│                                                                 │
│   ∂L/∂W₂ = ∂L/∂y · ∂y/∂h₂ · ∂h₂/∂z₂ · ∂z₂/∂W₂                   │
│                                                                 │
│   ∂L/∂W₁ = ∂L/∂y · ∂y/∂h₂ · ∂h₂/∂z₂ · ∂z₂/∂h₁ · ∂h₁/∂z₁ · ∂z₁/∂W₁│
│                                                                 │
│   Notice: Gradients get LONGER as we go back!                   │
│   This can cause vanishing/exploding gradients.                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
10. Chapter 8: Integrals - The Reverse Journey
📚 What is Integration?
Integration is the reverse of differentiation. If derivatives give us the rate of change, integrals give us the accumulated total.

text

┌─────────────────────────────────────────────────────────────────┐
│                    INTEGRAL CONCEPT                             │
│                                                                 │
│   Differentiation: f(x) ──────► f'(x)                           │
│                          d/dx                                   │
│                                                                 │
│   Integration:     f'(x) ──────► f(x) + C                       │
│                           ∫ dx                                  │
│                                                                 │
│   Example:                                                      │
│   d/dx [x²] = 2x      (differentiation)                        │
│   ∫ 2x dx = x² + C    (integration)                            │
│                                                                 │
│   Note: C is the "constant of integration"                      │
│         (infinite family of antiderivatives)                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📐 Geometric Interpretation
The definite integral represents the area under a curve.

text

┌─────────────────────────────────────────────────────────────────┐
│                    INTEGRAL AS AREA                             │
│                                                                 │
│    y │                                                          │
│      │          ╱╲                                              │
│      │         ╱██╲                                             │
│      │        ╱████╲                                            │
│      │       ╱██████╲                                           │
│      │      ╱████████╲                                          │
│      │     ╱██████████╲                                         │
│      │    ╱████████████╲                                        │
│      │───────────────────────── x                               │
│          a              b                                       │
│                                                                 │
│   ∫ₐᵇ f(x) dx = Area under f(x) from x=a to x=b                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
📋 Basic Integration Rules
text

┌────────────────────────────────────────────────────────────────┐
│                    INTEGRATION RULES                           │
├────────────────────┬───────────────────────────────────────────┤
│     f(x)           │              ∫ f(x) dx                    │
├────────────────────┼───────────────────────────────────────────┤
│     xⁿ             │              xⁿ⁺¹/(n+1) + C    (n ≠ -1)   │
│     1/x            │              ln|x| + C                    │
│     eˣ             │              eˣ + C                       │
│     e^(kx)         │              (1/k)e^(kx) + C              │
│     sin(x)         │              -cos(x) + C                  │
│     cos(x)         │              sin(x) + C                   │
│     1/(1+x²)       │              arctan(x) + C                │
│     a              │              ax + C                       │
└────────────────────┴───────────────────────────────────────────┘
🎯 Why Integrals Matter for ML
text

┌─────────────────────────────────────────────────────────────────┐
│                INTEGRALS IN MACHINE LEARNING                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. PROBABILITY DISTRIBUTIONS                                   │
│     ─────────────────────────                                   │
│     P(a ≤ X ≤ b) = ∫ₐᵇ f(x) dx                                 │
│     (Area under probability density function)                   │
│                                                                 │
│  2. EXPECTED VALUE                                              │
│     ──────────────                                              │
│     E[X] = ∫ x · f(x) dx                                       │
│                                                                 │
│  3. MARGINAL DISTRIBUTIONS                                      │
│     ──────────────────────                                      │
│     f(x) = ∫ f(x,y) dy                                         │
│     (Integrating out a variable)                                │
│                                                                 │
│  4. GAUSSIAN INTEGRALS                                          │
│     ─────────────────                                           │
│     Used everywhere in ML (normal distributions)                │
│                                                                 │
│  5. EVIDENCE IN BAYESIAN ML                                     │
│     ─────────────────────                                       │
│     P(D) = ∫ P(D|θ)P(θ) dθ                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
💻 Numerical Integration
In practice, we often compute integrals numerically:

Python

import numpy as np
from scipy import integrate

# Example: ∫₀¹ x² dx = [x³/3]₀¹ = 1/3 ≈ 0.333

def f(x):
    return x**2

# Numerical integration
result, error = integrate.quad(f, 0, 1)
print(f"∫₀¹ x² dx ≈ {result:.6f}")
print(f"Exact value: {1/3:.6f}")
print(f"Error: {abs(result - 1/3):.10f}")

# Probability example: Normal distribution
from scipy.stats import norm

# P(-1 ≤ X ≤ 1) for standard normal
prob = norm.cdf(1) - norm.cdf(-1)
print(f"\nP(-1 ≤ X ≤ 1) for N(0,1) = {prob:.4f}")
print("(About 68% of data within 1 standard deviation)")
11. Chapter 9: Calculus in Neural Networks
🧠 Putting It All Together
Now let's see how ALL the calculus concepts come together in neural networks!

📐 Forward Pass (Function Composition)
text

┌─────────────────────────────────────────────────────────────────┐
│                    NEURAL NETWORK FORWARD PASS                  │
│                                                                 │
│   Input: x = [x₁, x₂]                                           │
│                                                                 │
│   Layer 1:                                                      │
│   z₁ = W₁x + b₁                   (Linear transformation)       │
│   a₁ = σ(z₁)                      (Activation function)         │
│                                                                 │
│   Layer 2:                                                      │
│   z₂ = W₂a₁ + b₂                  (Linear transformation)       │
│   a₂ = σ(z₂)                      (Activation function)         │
│                                                                 │
│   Output:                                                       │
│   ŷ = a₂                          (Prediction)                  │
│                                                                 │
│   Loss:                                                         │
│   L = (y - ŷ)²                    (Mean Squared Error)          │
│                                                                 │
│   Calculus Used: Function composition, activation functions     │
└─────────────────────────────────────────────────────────────────┘
📐 Backward Pass (Chain Rule)
text

┌─────────────────────────────────────────────────────────────────┐
│                    BACKPROPAGATION                              │
│                                                                 │
│   Goal: Compute ∂L/∂W₁, ∂L/∂b₁, ∂L/∂W₂, ∂L/∂b₂                 │
│                                                                 │
│   Step 1: Output Layer Gradients                                │
│   ∂L/∂ŷ = -2(y - ŷ)                                            │
│   ∂L/∂z₂ = ∂L/∂ŷ · σ'(z₂)                                       │
│   ∂L/∂W₂ = ∂L/∂z₂ · a₁ᵀ                                         │
│   ∂L/∂b₂ = ∂L/∂z₂                                               │
│                                                                 │
│   Step 2: Hidden Layer Gradients                                │
│   ∂L/∂a₁ = W₂ᵀ · ∂L/∂z₂                                         │
│   ∂L/∂z₁ = ∂L/∂a₁ · σ'(z₁)                                      │
│   ∂L/∂W₁ = ∂L/∂z₁ · xᵀ                                          │
│   ∂L/∂b₁ = ∂L/∂z₁                                               │
│                                                                 │
│   Calculus Used: Chain rule, partial derivatives, gradients     │
└─────────────────────────────────────────────────────────────────┘
💻 Complete Implementation
Python

import numpy as np
import matplotlib.pyplot as plt

class NeuralNetwork:
    def __init__(self, layer_sizes):
        """Initialize network with random weights"""
        self.weights = []
        self.biases = []
        
        for i in range(len(layer_sizes) - 1):
            # Xavier initialization
            w = np.random.randn(layer_sizes[i+1], layer_sizes[i]) * np.sqrt(2 / layer_sizes[i])
            b = np.zeros((layer_sizes[i+1], 1))
            self.weights.append(w)
            self.biases.append(b)
    
    def sigmoid(self, z):
        """Sigmoid activation"""
        return 1 / (1 + np.exp(-np.clip(z, -500, 500)))
    
    def sigmoid_derivative(self, z):
        """Derivative of sigmoid: σ'(z) = σ(z)(1 - σ(z))"""
        s = self.sigmoid(z)
        return s * (1 - s)
    
    def forward(self, X):
        """Forward pass - returns all intermediate values"""
        self.z_values = []
        self.a_values = [X]
        
        a = X
        for i, (w, b) in enumerate(zip(self.weights, self.biases)):
            z = np.dot(w, a) + b
            a = self.sigmoid(z)
            self.z_values.append(z)
            self.a_values.append(a)
        
        return a
    
    def backward(self, X, y, learning_rate=0.1):
        """Backward pass using chain rule"""
        m = X.shape[1]  # Number of samples
        
        # Output layer gradient
        # ∂L/∂ŷ = -(y - ŷ) for MSE
        # ∂L/∂z = ∂L/∂ŷ · σ'(z)
        delta = -(y - self.a_values[-1]) * self.sigmoid_derivative(self.z_values[-1])
        
        # Store gradients
        dW = []
        db = []
        
        # Backpropagate through layers
        for i in range(len(self.weights) - 1, -1, -1):
            # Gradient for weights: ∂L/∂W = δ · aᵀ
            dW_i = np.dot(delta, self.a_values[i].T) / m
            
            # Gradient for biases: ∂L/∂b = δ
            db_i = np.sum(delta, axis=1, keepdims=True) / m
            
            dW.insert(0, dW_i)
            db.insert(0, db_i)
            
            if i > 0:
                # Propagate error to previous layer: δ = Wᵀδ · σ'(z)
                delta = np.dot(self.weights[i].T, delta) * self.sigmoid_derivative(self.z_values[i-1])
        
        # Update weights using gradient descent
        for i in range(len(self.weights)):
            self.weights[i] -= learning_rate * dW[i]
            self.biases[i] -= learning_rate * db[i]
    
    def train(self, X, y, epochs=1000, learning_rate=0.1):
        """Training loop"""
        losses = []
        
        for epoch in range(epochs):
            # Forward pass
            predictions = self.forward(X)
            
            # Compute loss
            loss = np.mean((y - predictions) ** 2)
            losses.append(loss)
            
            # Backward pass
            self.backward(X, y, learning_rate)
            
            if epoch % 100 == 0:
                print(f"Epoch {epoch}: Loss = {loss:.6f}")
        
        return losses

# Create XOR dataset
X = np.array([[0, 0, 1, 1],
              [0, 1, 0, 1]])
y = np.array([[0, 1, 1, 0]])

# Create and train network
nn = NeuralNetwork([2, 4, 1])  # 2 inputs, 4 hidden, 1 output
losses = nn.train(X, y, epochs=5000, learning_rate=1.0)

# Plot training loss
plt.figure(figsize=(10, 5))
plt.plot(losses)
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('XOR Training Loss')
plt.grid(True)
plt.show()

# Test
print("\nPredictions:")
predictions = nn.forward(X)
for i in range(4):
    print(f"Input: ({X[0,i]}, {X[1,i]}) -> Predicted: {predictions[0,i]:.4f}, Actual: {y[0,i]}")
12. Chapter 10: Advanced Topics
📚 Higher-Order Derivatives
text

First derivative:   f'(x)    or  df/dx
Second derivative:  f''(x)   or  d²f/dx²
Third derivative:   f'''(x)  or  d³f/dx³
nth derivative:     f⁽ⁿ⁾(x)  or  dⁿf/dxⁿ
ML Application: Second derivatives (Hessian) used in:

Newton's method optimization
Understanding loss surface curvature
Determining if critical point is min/max/saddle
📚 Hessian Matrix
The Hessian is a matrix of second-order partial derivatives:

text

For f(x, y):

H = ┌                        ┐
    │ ∂²f/∂x²    ∂²f/∂x∂y   │
    │ ∂²f/∂y∂x   ∂²f/∂y²    │
    └                        ┘

Properties:
- Symmetric (∂²f/∂x∂y = ∂²f/∂y∂x)
- Positive definite at local minimum
- Negative definite at local maximum
- Indefinite at saddle point
📚 Taylor Series
Any smooth function can be approximated by a polynomial:

text

f(x) ≈ f(a) + f'(a)(x-a) + f''(a)(x-a)²/2! + f'''(a)(x-a)³/3! + ...

At a = 0 (Maclaurin series):
f(x) ≈ f(0) + f'(0)x + f''(0)x²/2! + ...

Important Taylor Series:
─────────────────────────
eˣ = 1 + x + x²/2! + x³/3! + ...

sin(x) = x - x³/3! + x⁵/5! - ...

cos(x) = 1 - x²/2! + x⁴/4! - ...

ln(1+x) = x - x²/2 + x³/3 - ...  (for |x| < 1)
ML Application: Used in optimization (Newton's method), understanding activation functions