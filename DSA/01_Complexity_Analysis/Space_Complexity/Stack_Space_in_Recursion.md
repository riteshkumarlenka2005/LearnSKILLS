# 📚 Stack Space in Recursion — DSA

## 📌 Table of Contents
- [Introduction](#introduction)
- [What is a Call Stack?](#what-is-a-call-stack)
- [How Recursion Uses the Stack](#how-recursion-uses-the-stack)
- [What is a Stack Frame?](#what-is-a-stack-frame)
- [Visualizing Stack Growth](#visualizing-stack-growth)
- [How to Calculate Stack Space](#how-to-calculate-stack-space)
- [Detailed Examples](#detailed-examples)
  - [Example 1: Factorial — Linear Recursion](#example-1-factorial--linear-recursion)
  - [Example 2: Fibonacci — Binary Recursion (Tree Recursion)](#example-2-fibonacci--binary-recursion-tree-recursion)
  - [Example 3: Binary Search — Logarithmic Recursion](#example-3-binary-search--logarithmic-recursion)
  - [Example 4: Merge Sort — Divide and Conquer](#example-4-merge-sort--divide-and-conquer)
  - [Example 5: Tower of Hanoi — Exponential Calls, Linear Depth](#example-5-tower-of-hanoi--exponential-calls-linear-depth)
  - [Example 6: Nested Recursion](#example-6-nested-recursion)
  - [Example 7: Tail Recursion](#example-7-tail-recursion)
  - [Example 8: Multi-Branch Recursion (Permutations)](#example-8-multi-branch-recursion-permutations)
- [Key Insight: Depth vs Total Calls](#key-insight-depth-vs-total-calls)
- [Recursion Types and Their Stack Space](#recursion-types-and-their-stack-space)
- [Stack Overflow](#stack-overflow)
- [Tail Call Optimization (TCO)](#tail-call-optimization-tco)
- [Recursion vs Iteration — Stack Comparison](#recursion-vs-iteration--stack-comparison)
- [How to Reduce Stack Space](#how-to-reduce-stack-space)
- [Common Mistakes](#common-mistakes)
- [Quick Reference Table](#quick-reference-table)
- [Interview Tips](#interview-tips)
- [Summary](#summary)

---

## Introduction

Every recursive call **costs memory**. Each call is pushed onto the
**call stack**, consuming space until it returns. Understanding how much
stack space a recursive algorithm uses is **critical** for analyzing
auxiliary space complexity and avoiding **stack overflow** errors.

> **Stack space in recursion = O(maximum depth of the recursion tree)**

---

## What is a Call Stack?

> The **Call Stack** is a special **stack data structure** maintained by the
> operating system / runtime to keep track of **active function calls**.
┌─────────────────────────────────────────────────────┐
│ MEMORY LAYOUT │
│ │
│ ┌─────────────────────────┐ ← High Address │
│ │ STACK │ ← Function calls │
│ │ (grows downward ↓) │ go here │
│ │ │ │
│ ├─────────────────────────┤ │
│ │ ↕ │ ← Free Space │
│ ├─────────────────────────┤ │
│ │ │ │
│ │ HEAP │ ← Dynamic allocation │
│ │ (grows upward ↑) │ (new, malloc) │
│ ├─────────────────────────┤ │
│ │ STATIC / GLOBAL │ ← Global variables │
│ ├─────────────────────────┤ │
│ │ CODE (TEXT) │ ← Program code │
│ └─────────────────────────┘ ← Low Address │
│ │
└─────────────────────────────────────────────────────┘

text


### Key Properties of Call Stack:
• LIFO (Last In, First Out) structure
• Each function call → PUSH a new frame
• Each function return → POP the top frame
• Limited size (typically 1MB - 8MB)
• Exceeding limit → STACK OVERFLOW 💥

text


---

## How Recursion Uses the Stack
When a recursive function calls itself:

1️⃣ A new STACK FRAME is created
2️⃣ The frame is PUSHED onto the call stack
3️⃣ The function executes in this new frame
4️⃣ When it hits the BASE CASE, it RETURNS
5️⃣ The frame is POPPED from the stack
6️⃣ Control returns to the PREVIOUS frame
7️⃣ This continues until the original call returns

text


### Analogy: Stack of Plates 🍽️
Each recursive call = placing a new plate on the stack
Each return = removing the top plate

Too many calls without returning = stack of plates falls over = STACK OVERFLOW

text


---

## What is a Stack Frame?

> A **Stack Frame** (also called **Activation Record**) is a block of memory
> allocated on the call stack for **each function call**.

### Contents of a Stack Frame:
┌─────────────────────────────────────┐
│ STACK FRAME │
│ │
│ ┌───────────────────────────────┐ │
│ │ Return Address │ │ ← Where to go back after return
│ ├───────────────────────────────┤ │
│ │ Parameters / Arguments │ │ ← Values passed to function
│ ├───────────────────────────────┤ │
│ │ Local Variables │ │ ← Variables declared inside
│ ├───────────────────────────────┤ │
│ │ Saved Registers │ │ ← CPU register values
│ ├───────────────────────────────┤ │
│ │ Previous Frame Pointer │ │ ← Link to caller's frame
│ └───────────────────────────────┘ │
│ │
│ Size: Typically 64-256+ bytes │
│ per frame (depends on function) │
│ │
└─────────────────────────────────────┘

text


### Each Frame Stores:
| Component          | Description                                  |
|--------------------|----------------------------------------------|
| Return Address     | Where to resume execution after return       |
| Arguments          | Parameters passed to the function            |
| Local Variables    | Variables declared within the function       |
| Saved Registers    | CPU state to restore on return               |
| Frame Pointer      | Pointer to the previous stack frame          |

---

## Visualizing Stack Growth

### Linear Recursion: `factorial(4)`
CALL PHASE (Stack Growing ↓) RETURN PHASE (Stack Shrinking ↑)
═══════════════════════════ ════════════════════════════════

Call: factorial(4) factorial(4) returns 24
┌──────────────┐ ┌──────────────┐
│ factorial(4) │ │ factorial(4) │ ← 4 × 6 = 24 ✅
└──────┬───────┘ └──────────────┘
│
▼ calls factorial(3)
┌──────────────┐ ┌──────────────┐
│ factorial(4) │ │ factorial(4) │
├──────────────┤ └──────────────┘
│ factorial(3) │ ↑ returns 6
└──────┬───────┘ ┌──────────────┐
│ │ factorial(3) │ ← 3 × 2 = 6
▼ calls factorial(2) └──────────────┘
┌──────────────┐ ↑ returns 2
│ factorial(4) │ ┌──────────────┐
├──────────────┤ │ factorial(2) │ ← 2 × 1 = 2
│ factorial(3) │ └──────────────┘
├──────────────┤ ↑ returns 1
│ factorial(2) │ ┌──────────────┐
└──────┬───────┘ │ factorial(1) │ ← BASE CASE = 1
│ └──────────────┘
▼ calls factorial(1)
┌──────────────┐ ← MAXIMUM
│ factorial(4) │ DEPTH = 4
├──────────────┤ (4 frames)
│ factorial(3) │
├──────────────┤
│ factorial(2) │
├──────────────┤
│ factorial(1) │ ← BASE CASE HIT!
└──────────────┘ Start returning ↑

Stack Space = O(n) = O(4)

text


---

## How to Calculate Stack Space

### 🔑 The Golden Rule
╔══════════════════════════════════════════════════════════════╗
║ ║
║ Stack Space = O( MAXIMUM DEPTH of the recursion tree ) ║
║ ║
║ NOT the total number of calls! ║
║ NOT the total number of nodes in the tree! ║
║ ║
║ It's the LONGEST PATH from ROOT to any LEAF. ║
║ ║
╚══════════════════════════════════════════════════════════════╝

text


### Step-by-Step Process:
Step 1: Draw the recursion tree
Step 2: Find the DEEPEST level (longest root-to-leaf path)
Step 3: That depth = Stack space complexity

WHY? Because at any point in time, only ONE path from root
to the current node exists on the stack. Other branches
have already been popped off.

text


### Quick Formulas:

| Recursion Pattern            | Depth         | Stack Space  |
|------------------------------|:-------------:|:------------:|
| `f(n) → f(n-1)`             | n             | **O(n)**     |
| `f(n) → f(n/2)`             | log₂(n)      | **O(log n)** |
| `f(n) → f(n-1) + f(n-2)`    | n             | **O(n)**     |
| `f(n) → 2 × f(n/2)`        | log₂(n)      | **O(log n)** |
| `f(n) → f(n-1) + f(n-1)`    | n             | **O(n)**     |
| `f(n,m) → f(n-1,m) or f(n,m-1)` | n + m    | **O(n + m)** |

---

## Detailed Examples

### Example 1: Factorial — Linear Recursion

```python
def factorial(n):
    if n <= 1:           # Base case
        return 1
    return n * factorial(n - 1)   # One recursive call

# factorial(5) → factorial(4) → factorial(3) → factorial(2) → factorial(1)
Recursion Tree:
text

factorial(5)
    │
factorial(4)
    │
factorial(3)
    │
factorial(2)
    │
factorial(1)  ← BASE CASE

Depth = n = 5
Shape: Straight line (linear chain)
Stack at Maximum Depth:
text

┌──────────────────┐
│  factorial(5)    │  Frame 1
├──────────────────┤
│  factorial(4)    │  Frame 2
├──────────────────┤
│  factorial(3)    │  Frame 3
├──────────────────┤
│  factorial(2)    │  Frame 4
├──────────────────┤
│  factorial(1)    │  Frame 5  ← MAX DEPTH
└──────────────────┘

5 frames on stack simultaneously
Metric	Value
Total Calls	n
Max Depth	n
Stack Space	O(n)
Time Complexity	O(n)
Example 2: Fibonacci — Binary Recursion (Tree Recursion)
Python

def fib(n):
    if n <= 1:            # Base case
        return n
    return fib(n - 1) + fib(n - 2)   # TWO recursive calls

# fib(5) calls fib(4) and fib(3)
# fib(4) calls fib(3) and fib(2)
# ... and so on
Recursion Tree:
text

                         fib(5)
                        /      \
                   fib(4)       fib(3)
                  /     \       /     \
              fib(3)  fib(2)  fib(2)  fib(1)
              /   \    /  \    /  \
          fib(2) fib(1) fib(1) fib(0) fib(1) fib(0)
          /  \
      fib(1) fib(0)

Total Calls = 15 (exponential ~ 2ⁿ)
Max Depth   = 5  (follows the LEFT-MOST path)
🔑 KEY INSIGHT: Stack Space ≠ Total Calls!
text

WHY O(n) and NOT O(2ⁿ)?

The stack only holds frames along ONE PATH at a time.
When fib(1) returns, its frame is POPPED before fib(0) is called.

STEP-BY-STEP STACK TRACE:

Step 1: fib(5) → calls fib(4)
  Stack: [fib(5), fib(4)]

Step 2: fib(4) → calls fib(3)
  Stack: [fib(5), fib(4), fib(3)]

Step 3: fib(3) → calls fib(2)
  Stack: [fib(5), fib(4), fib(3), fib(2)]

Step 4: fib(2) → calls fib(1)
  Stack: [fib(5), fib(4), fib(3), fib(2), fib(1)]  ← MAX DEPTH = 5

Step 5: fib(1) returns → POP
  Stack: [fib(5), fib(4), fib(3), fib(2)]

Step 6: fib(2) → calls fib(0)
  Stack: [fib(5), fib(4), fib(3), fib(2), fib(0)]  ← Still depth 5

Step 7: fib(0) returns → POP
  Stack: [fib(5), fib(4), fib(3), fib(2)]

Step 8: fib(2) returns → POP
  Stack: [fib(5), fib(4), fib(3)]

... and so on. Stack NEVER exceeds depth n.
Visual: Stack at Maximum Depth
text

┌──────────────────┐
│     fib(5)       │  Frame 1
├──────────────────┤
│     fib(4)       │  Frame 2
├──────────────────┤
│     fib(3)       │  Frame 3
├──────────────────┤
│     fib(2)       │  Frame 4
├──────────────────┤
│     fib(1)       │  Frame 5  ← MAX DEPTH (leftmost path)
└──────────────────┘

Only 5 frames despite 15 total calls!
Metric	Value
Total Calls	O(2ⁿ) ≈ 15
Max Depth	n = 5
Stack Space	O(n)
Time Complexity	O(2ⁿ)
⚠️ This is the #1 interview mistake! People say stack space = O(2ⁿ)
because there are 2ⁿ calls. WRONG! It's O(n) because the maximum
depth is n.

Example 3: Binary Search — Logarithmic Recursion
Python

def binary_search(arr, target, low, high):
    if low > high:           # Base case
        return -1
    
    mid = (low + high) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, high)  # Right half
    else:
        return binary_search(arr, target, low, mid - 1)   # Left half

# Only ONE branch is taken each time (not both!)
Recursion Tree:
text

For arr = [1, 3, 5, 7, 9, 11, 13, 15], target = 13

binary_search(0, 7)   mid=3, arr[3]=7 < 13 → go RIGHT
        │
binary_search(4, 7)   mid=5, arr[5]=11 < 13 → go RIGHT
        │
binary_search(6, 7)   mid=6, arr[6]=13 = 13 → FOUND! ✅

Depth = log₂(8) = 3
Shape: Single path (only one branch taken)
Stack at Maximum Depth:
text

┌──────────────────────┐
│ binary_search(0, 7)  │  Frame 1
├──────────────────────┤
│ binary_search(4, 7)  │  Frame 2
├──────────────────────┤
│ binary_search(6, 7)  │  Frame 3  ← MAX DEPTH = log₂(n)
└──────────────────────┘
Metric	Value
Total Calls	O(log n)
Max Depth	log₂(n)
Stack Space	O(log n)
Time Complexity	O(log n)
Example 4: Merge Sort — Divide and Conquer
Python

def merge_sort(arr, l, r):
    if l >= r:               # Base case: single element
        return
    
    mid = (l + r) // 2
    merge_sort(arr, l, mid)       # Sort left half
    merge_sort(arr, mid + 1, r)   # Sort right half
    merge(arr, l, mid, r)         # Merge halves
Recursion Tree:
text

                     merge_sort(0,7)
                    /               \
           merge_sort(0,3)      merge_sort(4,7)
            /         \          /         \
     merge_sort(0,1) merge_sort(2,3) merge_sort(4,5) merge_sort(6,7)
       /    \          /    \          /    \          /    \
     ms(0) ms(1)    ms(2) ms(3)    ms(4) ms(5)    ms(6) ms(7)

Total Calls = 2n - 1 = 15
Max Depth   = log₂(8) + 1 = 4
Stack Trace (Following Left-Most Path):
text

Step 1: merge_sort(0,7)
  Stack: [ms(0,7)]

Step 2: merge_sort(0,3)
  Stack: [ms(0,7), ms(0,3)]

Step 3: merge_sort(0,1)
  Stack: [ms(0,7), ms(0,3), ms(0,1)]

Step 4: merge_sort(0,0) — base case
  Stack: [ms(0,7), ms(0,3), ms(0,1), ms(0,0)]  ← MAX DEPTH = 4

Step 5: ms(0,0) returns → POP
  Stack: [ms(0,7), ms(0,3), ms(0,1)]

Step 6: merge_sort(1,1) — base case
  Stack: [ms(0,7), ms(0,3), ms(0,1), ms(1,1)]  ← Still depth 4

... Stack never exceeds log₂(n) + 1 depth
Stack at Maximum Depth:
text

┌──────────────────────┐
│  merge_sort(0, 7)    │  Frame 1  (Level 0)
├──────────────────────┤
│  merge_sort(0, 3)    │  Frame 2  (Level 1)
├──────────────────────┤
│  merge_sort(0, 1)    │  Frame 3  (Level 2)
├──────────────────────┤
│  merge_sort(0, 0)    │  Frame 4  (Level 3)  ← MAX DEPTH
└──────────────────────┘

Depth = log₂(n) = log₂(8) = 3 levels + 1 = 4 frames
Metric	Value
Total Calls	O(n)
Max Depth	log₂(n)
Stack Space	O(log n)
Auxiliary Space	O(n) (temp arrays for merging)
Total Aux Space	O(n) (merge arrays dominate)
Time Complexity	O(n log n)
Note: Merge Sort's stack space is O(log n), but its total auxiliary
space is O(n) because of the temporary arrays created during merging.

Example 5: Tower of Hanoi — Exponential Calls, Linear Depth
Python

def tower_of_hanoi(n, source, destination, auxiliary):
    if n == 0:                  # Base case
        return
    
    tower_of_hanoi(n - 1, source, auxiliary, destination)
    print(f"Move disk {n} from {source} to {destination}")
    tower_of_hanoi(n - 1, auxiliary, destination, source)
Recursion Tree (n=3):
text

                        TOH(3, A, C, B)
                       /                \
              TOH(2,A,B,C)           TOH(2,B,C,A)
              /         \            /         \
        TOH(1,A,C,B) TOH(1,C,B,A) TOH(1,B,A,C) TOH(1,A,C,B)
         /    \        /    \        /    \        /    \
      TOH(0) TOH(0) TOH(0) TOH(0) TOH(0) TOH(0) TOH(0) TOH(0)

Total Calls = 2ⁿ - 1 = 7 (+ 8 base cases)
Max Depth   = n = 3
Stack at Maximum Depth:
text

┌──────────────────────┐
│   TOH(3, A, C, B)    │  Frame 1
├──────────────────────┤
│   TOH(2, A, B, C)    │  Frame 2
├──────────────────────┤
│   TOH(1, A, C, B)    │  Frame 3  ← MAX DEPTH = n
└──────────────────────┘
Metric	Value
Total Calls	O(2ⁿ)
Max Depth	n
Stack Space	O(n) ← NOT O(2ⁿ)!
Time Complexity	O(2ⁿ)
Despite 2ⁿ total calls, stack space is only O(n)!

Example 6: Nested Recursion
Python

# Each call makes ONE call but to a deeply nested value
def ackermann(m, n):
    if m == 0:
        return n + 1
    elif n == 0:
        return ackermann(m - 1, 1)
    else:
        return ackermann(m - 1, ackermann(m, n - 1))
text

Stack Depth: Grows EXTREMELY fast
  • ackermann(4, 2) has depth > 2^65536 !
  • Practically causes stack overflow for small inputs

Stack Space: Hyper-exponential (not practical)
Metric	Value
Stack Space	Hyper-exponential 🤯
Practical Use	Theoretical / Computability only
Example 7: Tail Recursion
Python

# ❌ NOT Tail Recursive — Must multiply AFTER recursive call returns
def factorial_normal(n):
    if n <= 1:
        return 1
    return n * factorial_normal(n - 1)   # n * (result) → NOT tail position

# ✅ Tail Recursive — Recursive call is the LAST operation
def factorial_tail(n, accumulator=1):
    if n <= 1:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)  # LAST operation = call itself

# Both compute same result:
# factorial_normal(5) = 120
# factorial_tail(5)   = 120
Stack Comparison:
text

❌ Normal Recursion (Stack grows):
┌────────────────────────┐
│ factorial_normal(5)    │  Waiting for result...
├────────────────────────┤
│ factorial_normal(4)    │  Waiting for result...
├────────────────────────┤
│ factorial_normal(3)    │  Waiting for result...
├────────────────────────┤
│ factorial_normal(2)    │  Waiting for result...
├────────────────────────┤
│ factorial_normal(1)    │  Returns 1
└────────────────────────┘
Then: 2×1=2, 3×2=6, 4×6=24, 5×24=120

Stack Space: O(n)

═══════════════════════════════════════

✅ Tail Recursion (Stack can be REUSED — with TCO):
┌──────────────────────────────┐
│ factorial_tail(5, 1)         │  → replace with ↓
├──────────────────────────────┤
│ factorial_tail(4, 5)         │  → replace with ↓
├──────────────────────────────┤
│ factorial_tail(3, 20)        │  → replace with ↓
├──────────────────────────────┤
│ factorial_tail(2, 60)        │  → replace with ↓
├──────────────────────────────┤
│ factorial_tail(1, 120)       │  Returns 120
└──────────────────────────────┘

WITH Tail Call Optimization (TCO):
  Only 1 frame is reused → Stack Space: O(1) ✅

WITHOUT TCO (Python, Java):
  Still O(n) frames → Stack Space: O(n) ❌
Metric	Normal Recursion	Tail Recursion (with TCO)	Tail Recursion (without TCO)
Stack Space	O(n)	O(1) ✅	O(n) ❌
TCO Support	N/A	C, Scheme, Kotlin, Scala	Python ❌, Java ❌
Example 8: Multi-Branch Recursion (Permutations)
Python

def permutations(arr, l, r):
    if l == r:
        print(arr)
        return
    
    for i in range(l, r + 1):
        arr[l], arr[i] = arr[i], arr[l]         # Choose
        permutations(arr, l + 1, r)              # Explore
        arr[l], arr[i] = arr[i], arr[l]          # Un-choose (backtrack)

# permutations([1, 2, 3], 0, 2)
Recursion Tree:
text

                       perm(0)
                    /    |    \
              perm(1)  perm(1)  perm(1)
              /   \    /   \    /   \
          perm(2) perm(2) perm(2) perm(2) perm(2) perm(2)

Total Calls = n! (leaves) + internal nodes
Max Depth   = n (levels: 0 to n-1)
Stack at Maximum Depth:
text

┌──────────────────────┐
│    perm(0)           │  Frame 1 — choosing 1st position
├──────────────────────┤
│    perm(1)           │  Frame 2 — choosing 2nd position
├──────────────────────┤
│    perm(2)           │  Frame 3 — choosing 3rd position (base case)
└──────────────────────┘

Stack Space = O(n) despite n! total permutations
Metric	Value
Total Calls	O(n × n!)
Max Depth	n
Stack Space	O(n) ← NOT O(n!)
Time Complexity	O(n × n!)
Key Insight: Depth vs Total Calls
text

╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║   🔑 THE MOST IMPORTANT INSIGHT:                                 ║
║                                                                  ║
║   Stack Space = O(MAX DEPTH)    ≠    O(TOTAL CALLS)              ║
║                                                                  ║
║   WHY?                                                           ║
║   Because the stack only holds frames along the                  ║
║   CURRENT PATH from root to the active call.                     ║
║   Completed calls have already been POPPED OFF.                  ║
║                                                                  ║
║   ANALOGY:                                                       ║
║   You're hiking a tree-shaped trail.                             ║
║   Total calls = ALL paths you'll walk                            ║
║   Stack depth = How far you are from the trailhead RIGHT NOW     ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   Example: Fibonacci fib(5)                                      ║
║                                                                  ║
║   Total calls  = 15    → O(2ⁿ)                                  ║
║   Max depth    = 5     → O(n)                                    ║
║   Stack Space  = O(n)  ✅                                        ║
║   Stack Space ≠ O(2ⁿ) ❌                                        ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
Side-by-Side Comparison:
text

                    fib(4)
                   /      \
              fib(3)       fib(2)         ← Level 1
              /   \        /   \
          fib(2) fib(1) fib(1) fib(0)     ← Level 2
          /   \
      fib(1) fib(0)                        ← Level 3

Total nodes (calls) = 9          → O(2ⁿ)
Max depth           = 4          → O(n)
Frames on stack at any time ≤ 4  → O(n) ✅
Recursion Types and Their Stack Space
text

┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   RECURSION TYPE           │ DEPTH      │ STACK SPACE            │
│   ─────────────────────────┼────────────┼────────────────────    │
│                            │            │                        │
│   LINEAR                   │ n          │ O(n)                   │
│   f(n) → f(n-1)           │            │                        │
│   e.g., Factorial          │            │                        │
│                            │            │                        │
│   BINARY (TREE)            │ n          │ O(n)                   │
│   f(n) → f(n-1) + f(n-2)  │            │ (depth, NOT calls)     │
│   e.g., Fibonacci          │            │                        │
│                            │            │                        │
│   DIVIDE & CONQUER         │ log n      │ O(log n)               │
│   f(n) → f(n/2)           │            │                        │
│   e.g., Binary Search      │            │                        │
│                            │            │                        │
│   MULTI-BRANCH             │ n          │ O(n)                   │
│   f(n) → n × f(n-1)       │            │ (depth, NOT branches)  │
│   e.g., Permutations       │            │                        │
│                            │            │                        │
│   TWO-VARIABLE             │ n + m      │ O(n + m)               │
│   f(n,m) → f(n-1,m)       │            │                        │
│         or f(n,m-1)        │            │                        │
│   e.g., Grid Paths         │            │                        │
│                            │            │                        │
│   TAIL RECURSION (+ TCO)   │ n          │ O(1)  ← Optimized!    │
│   f(n) → f(n-1) as LAST op│            │                        │
│                            │            │                        │
│   NESTED RECURSION         │ varies     │ Can be enormous        │
│   f(n) → f(f(n-1))        │            │                        │
│   e.g., Ackermann          │            │                        │
│                            │            │                        │
└──────────────────────────────────────────────────────────────────┘
Stack Overflow
What Causes It?
text

Stack Overflow occurs when:
  • Recursion depth exceeds the system's stack size limit
  • No base case (infinite recursion)
  • Base case never reached
  • Very deep recursion (n > ~10,000 in Python)
Example: Stack Overflow in Python
Python

# ❌ STACK OVERFLOW
def infinite_recursion(n):
    return infinite_recursion(n + 1)   # No base case!

# RecursionError: maximum recursion depth exceeded

# ─────────────────────────────────────────────

# ❌ STACK OVERFLOW (deep but finite)
def deep_recursion(n):
    if n == 0:
        return 0
    return deep_recursion(n - 1)

deep_recursion(1000000)  # Python default limit: ~1000

# ─────────────────────────────────────────────

# ✅ FIX: Increase recursion limit (use cautiously!)
import sys
sys.setrecursionlimit(1000000)
Stack Limits by Language:
text

┌──────────────┬───────────────────┬─────────────────────────┐
│   Language   │  Default Limit    │  How to Modify          │
├──────────────┼───────────────────┼─────────────────────────┤
│   Python     │  ~1,000 frames    │  sys.setrecursionlimit()│
│   Java       │  ~5,000-10,000    │  -Xss flag (stack size) │
│   C/C++      │  ~10,000-100,000  │  ulimit -s / linker     │
│   JavaScript │  ~10,000-25,000   │  Varies by engine       │
│   Go         │  ~1,000,000+      │  goroutine stack grows  │
└──────────────┴───────────────────┴─────────────────────────┘
Prevention Strategies:
text

1. Always have a BASE CASE
2. Ensure recursion PROGRESSES toward the base case
3. Convert to ITERATION for deep recursion
4. Use TAIL RECURSION where supported
5. Use MEMOIZATION to avoid redundant calls (won't reduce depth though)
Tail Call Optimization (TCO)
What is TCO?
Tail Call Optimization is a compiler/interpreter optimization where
the current stack frame is REUSED for the next recursive call
if the recursive call is the LAST operation in the function.

text

WITHOUT TCO:
  Frame 1 → Frame 2 → Frame 3 → ... → Frame n
  Stack Space: O(n)

WITH TCO:
  Frame 1 → reuse → reuse → reuse → ... → reuse
  Stack Space: O(1)
Tail vs Non-Tail Position:
Python

# ❌ NOT Tail Recursive
def sum_normal(n):
    if n == 0:
        return 0
    return n + sum_normal(n - 1)    # Addition happens AFTER recursive call
    #      ^^^
    #      Must wait for recursive call to return, THEN add n
    #      So frame can't be reused

# ✅ Tail Recursive
def sum_tail(n, acc=0):
    if n == 0:
        return acc
    return sum_tail(n - 1, acc + n)  # Recursive call is the LAST thing
    #                                   No operation pending after return
    #                                   Frame can be reused!
TCO Support by Language:
text

┌─────────────────────────────────────────────────────────┐
│                                                         │
│   ✅ SUPPORTS TCO:              ❌ DOES NOT SUPPORT:    │
│   ─────────────────             ─────────────────────   │
│   • Scheme / Racket             • Python                │
│   • Haskell                     • Java                  │
│   • Scala                       • JavaScript (partial)  │
│   • Kotlin                      • Ruby (partial)        │
│   • Erlang / Elixir             • C# (partial)          │
│   • C / C++ (compiler flag)     • Go                    │
│   • Swift                       • Rust (not guaranteed) │
│                                                         │
└─────────────────────────────────────────────────────────┘
⚠️ Python does NOT support TCO! Even tail-recursive Python code
will still use O(n) stack space and hit recursion limits.

Recursion vs Iteration — Stack Comparison
Python

# ─────────────────────────────────────────────
# RECURSIVE Version
# ─────────────────────────────────────────────
def sum_recursive(n):
    if n == 0:
        return 0
    return n + sum_recursive(n - 1)

# Stack Space: O(n) — n frames on call stack
# Risk: Stack overflow for large n

# ─────────────────────────────────────────────
# ITERATIVE Version
# ─────────────────────────────────────────────
def sum_iterative(n):
    total = 0
    for i in range(1, n + 1):
        total += i
    return total

# Stack Space: O(1) — single frame, loop variable
# Risk: None (no stack growth)
Full Comparison:
text

┌──────────────────┬──────────────────┬──────────────────┐
│     Aspect       │   RECURSIVE      │   ITERATIVE      │
├──────────────────┼──────────────────┼──────────────────┤
│ Stack Space      │ O(depth)         │ O(1)             │
│ Call Overhead     │ High (push/pop) │ Low (loop)       │
│ Stack Overflow   │ Possible ⚠️      │ Not possible ✅  │
│ Code Readability │ Often cleaner    │ Sometimes verbose│
│ Performance      │ Slower (frames)  │ Faster (no frames)│
│ Use Cases        │ Trees, graphs,   │ Simple loops,    │
│                  │ divide & conquer │ accumulators     │
│ Debugging        │ Harder (deep)    │ Easier (flat)    │
└──────────────────┴──────────────────┴──────────────────┘
Converting Recursion to Iteration (Explicit Stack):
Python

# ─────────────────────────────────────────────
# RECURSIVE DFS (uses call stack)
# ─────────────────────────────────────────────
def dfs_recursive(node, visited):
    if node is None or node in visited:
        return
    visited.add(node)
    print(node.val)
    for neighbor in node.neighbors:
        dfs_recursive(neighbor, visited)

# Stack Space: O(V) — depth of graph

# ─────────────────────────────────────────────
# ITERATIVE DFS (uses explicit stack on heap)
# ─────────────────────────────────────────────
def dfs_iterative(start):
    stack = [start]          # Explicit stack (on HEAP, not call stack)
    visited = set()

    while stack:
        node = stack.pop()
        if node in visited:
            continue
        visited.add(node)
        print(node.val)
        for neighbor in node.neighbors:
            if neighbor not in visited:
                stack.append(neighbor)

# Call Stack Space: O(1)
# Heap Space: O(V) — explicit stack
# Benefit: No stack overflow! Heap is much larger.
text

KEY INSIGHT:
Converting recursion to iteration doesn't eliminate space usage —
it moves it from the CALL STACK (limited) to the HEAP (much larger).

Call Stack: ~1MB - 8MB
Heap:       ~GBs (limited by RAM)
How to Reduce Stack Space
text

┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   TECHNIQUE 1: Convert to Iteration                              │
│   ──────────────────────────────────                             │
│   • Use loops instead of recursion                               │
│   • Use explicit stack (on heap) if needed                       │
│   • Stack space: O(1) for call stack                             │
│                                                                  │
│   TECHNIQUE 2: Tail Recursion + TCO                              │
│   ──────────────────────────────────                             │
│   • Make recursive call the LAST operation                       │
│   • Use accumulator parameters                                   │
│   • Works in: Scheme, Scala, Kotlin, C (with -O2)               │
│   • Stack space: O(1) with TCO                                   │
│                                                                  │
│   TECHNIQUE 3: Divide & Conquer (Balanced Split)                 │
│   ──────────────────────────────────────────────                 │
│   • Split into halves: depth = O(log n)                          │
│   • Process ONE half first, then the other                       │
│   • Stack space: O(log n)                                        │
│                                                                  │
│   TECHNIQUE 4: Morris Traversal (Tree-specific)                  │
│   ──────────────────────────────────────────────                 │
│   • Tree traversal WITHOUT recursion or stack                    │
│   • Uses threaded binary tree concept                            │
│   • Stack space: O(1) 🎉                                        │
│                                                                  │
│   TECHNIQUE 5: Bottom-Up DP (instead of Top-Down)                │
│   ───────────────────────────────────────────────                │
│   • Iterative tabulation instead of recursive memoization        │
│   • Stack space: O(1) for call stack                             │
│   • Table space: O(n) on heap                                    │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
Before & After Example:
Python

# ❌ BEFORE: Top-Down DP (Recursive) — O(n) stack
def fib_top_down(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_top_down(n-1, memo) + fib_top_down(n-2, memo)
    return memo[n]

# Stack Space: O(n) — recursion depth

# ─────────────────────────────────────────────

# ✅ AFTER: Bottom-Up DP (Iterative) — O(1) stack
def fib_bottom_up(n):
    if n <= 1:
        return n
    prev2, prev1 = 0, 1
    for i in range(2, n + 1):
        curr = prev1 + prev2
        prev2 = prev1
        prev1 = curr
    return prev1

# Stack Space: O(1) — no recursion!
# Extra Space: O(1) — just two variables!
Common Mistakes
#	❌ Mistake	✅ Correct Understanding
1	"Fibonacci uses O(2ⁿ) stack space"	Stack space = O(n) (max depth, not total calls)
2	"Stack space = Total recursive calls"	Stack space = MAX DEPTH of recursion tree
3	"Memoization reduces stack space"	Memoization reduces TIME, not stack depth
4	"Tail recursion always uses O(1) space"	Only with TCO support (not Python/Java)
5	"Converting to iteration eliminates all extra space"	It moves space from call stack to heap
6	"Merge sort has O(n) stack space"	Stack space is O(log n); O(n) is for temp arrays
7	"More branches = more stack space"	Only depth matters, not breadth
8	"Recursion is always bad for space"	O(log n) recursion (binary search) is very efficient
Mistake #1 Deep Dive:
text

Fibonacci fib(5):

                     fib(5)
                    /      \
               fib(4)       fib(3)
              /     \       /     \
          fib(3)  fib(2)  fib(2)  fib(1)
          /   \
      fib(2) fib(1)

❌ WRONG: "15 calls = O(2ⁿ) stack space"

✅ RIGHT: At any instant, only ONE root-to-node path is on the stack.
          Longest path = 5 levels = O(n) stack space.

          When fib(3) on the RIGHT starts executing,
          fib(4) and all its children are ALREADY FINISHED and POPPED.
Quick Reference Table
Algorithm / Function	Total Calls	Max Depth	Stack Space	Time
Factorial(n)	n	n	O(n)	O(n)
Fibonacci(n) — naive	2ⁿ	n	O(n)	O(2ⁿ)
Fibonacci(n) — memoized	n	n	O(n)	O(n)
Binary Search	log n	log n	O(log n)	O(log n)
Merge Sort	2n	log n	O(log n)	O(n log n)
Quick Sort (avg)	2n	log n	O(log n)	O(n log n)
Quick Sort (worst)	n	n	O(n)	O(n²)
Tower of Hanoi	2ⁿ	n	O(n)	O(2ⁿ)
Permutations(n)	n × n!	n	O(n)	O(n × n!)
DFS (Graph with V nodes)	V + E	V	O(V)	O(V + E)
Tree Traversal (balanced)	n	log n	O(log n)	O(n)
Tree Traversal (skewed)	n	n	O(n)	O(n)
Power(x, n) — fast	log n	log n	O(log n)	O(log n)
Grid Paths(m, n) — naive	C(m+n, m)	m + n	O(m + n)	O(2^(m+n))
Subset Generation	2ⁿ	n	O(n)	O(2ⁿ)
Interview Tips
text

┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   🎯 INTERVIEW TIPS FOR STACK SPACE                              │
│   ─────────────────────────────────                              │
│                                                                  │
│   1. ALWAYS mention stack space for recursive solutions          │
│      "This uses O(n) auxiliary space due to the recursion        │
│       call stack."                                               │
│                                                                  │
│   2. DIFFERENTIATE between stack space and other auxiliary space  │
│      "Merge sort uses O(log n) stack + O(n) for temp arrays      │
│       = O(n) total auxiliary space."                             │
│                                                                  │
│   3. KNOW the depth formula for common patterns                  │
│      • f(n-1) → O(n)                                            │
│      • f(n/2) → O(log n)                                        │
│      • f(n-1) + f(n-2) → O(n) (NOT O(2ⁿ))                     │
│                                                                  │
│   4. OFFER to convert to iterative if asked about space          │
│      "I can convert this to iterative to reduce stack space      │
│       from O(n) to O(1)."                                       │
│                                                                  │
│   5. MENTION stack overflow risk for large inputs                │
│      "For n > 10⁴ in Python, this might hit the recursion        │
│       limit. I'd use an iterative approach instead."             │
│                                                                  │
│   6. DON'T confuse total calls with stack depth                  │
│      WRONG: "Fibonacci has O(2ⁿ) space"                         │
│      RIGHT: "Fibonacci has O(n) stack space and O(2ⁿ) time"     │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
Summary
text

╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║          STACK SPACE IN RECURSION — COMPLETE SUMMARY              ║
║          ═══════════════════════════════════════════              ║
║                                                                  ║
║   WHAT IT IS:                                                    ║
║   Memory consumed by stack frames during recursive calls.        ║
║   Each call → 1 frame pushed. Each return → 1 frame popped.     ║
║                                                                  ║
║   HOW TO CALCULATE:                                              ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │                                                        │     ║
║   │   Stack Space = O( MAX DEPTH of recursion tree )       │     ║
║   │                                                        │     ║
║   │   NOT total calls. NOT total nodes. Just DEPTH.        │     ║
║   │                                                        │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   KEY FORMULAS:                                                  ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │  f(n) → f(n-1)              → Depth: n    → O(n)      │     ║
║   │  f(n) → f(n/2)              → Depth: logn → O(log n)  │     ║
║   │  f(n) → f(n-1) + f(n-2)    → Depth: n    → O(n)      │     ║
║   │  f(n) → f(n/2) + f(n/2)    → Depth: logn → O(log n)  │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   CRITICAL RULE:                                                 ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │                                                        │     ║
║   │   At any moment, the stack holds ONLY the frames       │     ║
║   │   along the CURRENT PATH from root to active call.     │     ║
║   │                                                        │     ║
║   │   Completed branches are already POPPED OFF.           │     ║
║   │                                                        │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   TO REDUCE STACK SPACE:                                         ║
║   • Convert to iteration                                         ║
║   • Use tail recursion (+ TCO)                                   ║
║   • Use bottom-up DP                                             ║
║   • Use explicit stack on heap                                   ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
🤝 Contributing
Found an error? Want to add more examples? Open an issue or submit a PR!

📄 License
This project is licensed under the MIT License.

text


This README provides **complete coverage** of Stack Space in Recursion:

- ✅ **Call stack & stack frame** internals explained visually
- ✅ **8 detailed coded examples** — Factorial, Fibonacci, Binary Search, Merge Sort, Tower of Hanoi, Nested, Tail, and Permutations
- ✅ **Step-by-step stack traces** showing frames being pushed & popped
- ✅ **The #1 interview mistake** — depth vs total calls (with proof)
- ✅ **Tail Call Optimization** — with language support table
- ✅ **Recursion vs Iteration** — side-by-side comparison
- ✅ **5 techniques to reduce stack space**
- ✅ **Stack overflow** causes, limits by language, and prevention
- ✅ **Quick reference table** for 15+ common algorithms
- ✅ **Interview tips** for communicating stack space correctly
