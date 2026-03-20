# 🔄 In-Place Algorithms in DSA

## 📌 Table of Contents
- [Introduction](#introduction)
- [What is an In-Place Algorithm?](#what-is-an-in-place-algorithm)
- [What is a Not-In-Place (Out-of-Place) Algorithm?](#what-is-a-not-in-place-out-of-place-algorithm)
- [Key Differences](#key-differences)
- [Visual Diagram](#visual-diagram)
- [Examples of In-Place Algorithms](#examples-of-in-place-algorithms)
  - [Example 1: Swap Two Numbers](#example-1-swap-two-numbers)
  - [Example 2: Reverse an Array](#example-2-reverse-an-array-in-place)
  - [Example 3: Bubble Sort](#example-3-bubble-sort)
  - [Example 4: Remove Duplicates (Sorted Array)](#example-4-remove-duplicates-from-sorted-array)
  - [Example 5: Move Zeroes to End](#example-5-move-zeroes-to-end)
- [Examples of Not-In-Place Algorithms](#examples-of-not-in-place-algorithms)
  - [Example 1: Reverse Array (Not-In-Place)](#example-1-reverse-array-not-in-place)
  - [Example 2: Merge Sort](#example-2-merge-sort)
  - [Example 3: Counting Sort](#example-3-counting-sort)
- [Sorting Algorithms Classification](#sorting-algorithms-classification)
- [The Recursion Debate](#the-recursion-debate)
- [Strict vs Broad Definition](#strict-vs-broad-definition)
- [Advantages & Disadvantages](#advantages--disadvantages)
- [When to Use What?](#when-to-use-what)
- [Classic In-Place Problems (Interview Favorites)](#classic-in-place-problems-interview-favorites)
- [Common Misconceptions](#common-misconceptions)
- [Summary](#summary)

---

## Introduction

In competitive programming and interviews, you'll often hear:

> *"Can you solve this **in-place**?"*

This means: **solve the problem without using significant extra memory**.
In-place algorithms are a cornerstone concept in DSA that directly connects
to **auxiliary space complexity**.

---

## What is an In-Place Algorithm?

> An **In-Place Algorithm** transforms the input data using only a
> **small, constant amount of extra memory** — `O(1)` auxiliary space.

It modifies the **original data structure directly** instead of creating
a new copy.
✅ Auxiliary Space = O(1)
✅ Operates directly on the input
✅ No new arrays / lists / data structures proportional to input size

text


### Formal Definition
An algorithm is IN-PLACE if:

text

Auxiliary Space = O(1)

(Some definitions allow O(log n) for recursive call stack)
text


---

## What is a Not-In-Place (Out-of-Place) Algorithm?

> A **Not-In-Place (Out-of-Place) Algorithm** requires **extra space
> proportional to the input size** — `O(n)` or more auxiliary space.

It typically creates a **new data structure** to store intermediate
or final results.
❌ Auxiliary Space = O(n) or more
❌ Creates new arrays / lists / hash maps proportional to input
❌ Original input may remain unchanged

text


---

## Key Differences

| Aspect                  | In-Place ✅                          | Not-In-Place ❌                         |
|-------------------------|--------------------------------------|-----------------------------------------|
| **Auxiliary Space**     | `O(1)` (constant)                   | `O(n)` or more                          |
| **Modifies Input?**     | Yes — works on original data        | No — creates new copy / structure       |
| **Memory Efficient?**   | ✅ Very                              | ❌ Uses more memory                     |
| **Original Data Safe?** | ❌ Original data is overwritten      | ✅ Original data is preserved           |
| **Code Complexity**     | Sometimes harder to implement        | Usually simpler / more readable         |
| **Speed**               | Often faster (cache-friendly)        | May be slower (extra allocation)        |
| **Examples**            | Bubble Sort, Quick Sort, Swap        | Merge Sort, Counting Sort, Array Copy   |

---

## Visual Diagram
╔══════════════════════════════════════════════════════════════╗
║ ║
║ IN-PLACE ALGORITHM ║
║ ║
║ Input Array: [5, 3, 8, 1, 2] ║
║ │ ║
║ ▼ ║
║ ┌───────────┐ ║
║ │ Algorithm │ ← uses only temp variables ║
║ │ (O(1) │ e.g., temp, i, j ║
║ │ extra) │ ║
║ └───────────┘ ║
║ │ ║
║ ▼ ║
║ SAME Array: [1, 2, 3, 5, 8] ← modified in-place ║
║ ║
║ Extra Memory Used: temp variable only → O(1) ║
║ ║
╠══════════════════════════════════════════════════════════════╣
║ ║
║ NOT-IN-PLACE ALGORITHM ║
║ ║
║ Input Array: [5, 3, 8, 1, 2] ║
║ │ ║
║ ▼ ║
║ ┌───────────┐ ║
║ │ Algorithm │ ← creates a NEW array ║
║ │ (O(n) │ of size n ║
║ │ extra) │ ║
║ └───────────┘ ║
║ │ ║
║ ▼ ║
║ NEW Array: [1, 2, 3, 5, 8] ← result in new array ║
║ Old Array: [5, 3, 8, 1, 2] ← still unchanged ║
║ ║
║ Extra Memory Used: entire new array → O(n) ║
║ ║
╚══════════════════════════════════════════════════════════════╝

text


---

## Examples of In-Place Algorithms

### Example 1: Swap Two Numbers

```python
# ✅ IN-PLACE — O(1) auxiliary space
def swap(arr, i, j):
    temp = arr[i]       # only 1 temp variable
    arr[i] = arr[j]
    arr[j] = temp

# Even simpler in Python:
# arr[i], arr[j] = arr[j], arr[i]
Metric	Value
Auxiliary Space	O(1)
In-Place?	✅ Yes
Example 2: Reverse an Array (In-Place)
Python

# ✅ IN-PLACE — O(1) auxiliary space
def reverse_in_place(arr):
    left = 0
    right = len(arr) - 1

    while left < right:
        # Swap elements using two pointers
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

    # No new array created!
    return arr   # same array, now reversed


# Usage:
arr = [1, 2, 3, 4, 5]
reverse_in_place(arr)
print(arr)  # [5, 4, 3, 2, 1]
text

Step-by-step:
 [1, 2, 3, 4, 5]    left=0, right=4 → swap(1,5)
 [5, 2, 3, 4, 1]    left=1, right=3 → swap(2,4)
 [5, 4, 3, 2, 1]    left=2, right=2 → STOP ✅
Metric	Value
Auxiliary Space	O(1)
In-Place?	✅ Yes
Example 3: Bubble Sort
Python

# ✅ IN-PLACE — O(1) auxiliary space
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]  # swap in-place
                swapped = True
        if not swapped:
            break
    return arr


# Usage:
arr = [64, 34, 25, 12, 22]
bubble_sort(arr)
print(arr)  # [12, 22, 25, 34, 64]
Metric	Value
Time Complexity	O(n²)
Auxiliary Space	O(1)
In-Place?	✅ Yes
Example 4: Remove Duplicates from Sorted Array
Python

# ✅ IN-PLACE — O(1) auxiliary space
# LeetCode #26

def remove_duplicates(arr):
    if not arr:
        return 0

    write_pointer = 0   # position to write next unique element

    for read_pointer in range(1, len(arr)):
        if arr[read_pointer] != arr[write_pointer]:
            write_pointer += 1
            arr[write_pointer] = arr[read_pointer]

    return write_pointer + 1   # length of unique portion


# Usage:
arr = [1, 1, 2, 2, 3, 4, 4, 5]
length = remove_duplicates(arr)
print(arr[:length])  # [1, 2, 3, 4, 5]
text

Visualization:
 arr = [1, 1, 2, 2, 3, 4, 4, 5]
        W  R                        → same, skip
        W     R                     → different, write
           W     R                  → same, skip
           W        R               → different, write
              W        R            → different, write
                 W        R         → same, skip
                 W           R      → different, write

 Result: [1, 2, 3, 4, 5, ...]
          ↑ unique portion ↑
Metric	Value
Time Complexity	O(n)
Auxiliary Space	O(1)
In-Place?	✅ Yes
Example 5: Move Zeroes to End
Python

# ✅ IN-PLACE — O(1) auxiliary space
# LeetCode #283

def move_zeroes(arr):
    write = 0   # position to place next non-zero

    # Pass 1: Move all non-zero elements forward
    for read in range(len(arr)):
        if arr[read] != 0:
            arr[write] = arr[read]
            write += 1

    # Pass 2: Fill remaining positions with zeros
    while write < len(arr):
        arr[write] = 0
        write += 1


# Usage:
arr = [0, 1, 0, 3, 12]
move_zeroes(arr)
print(arr)  # [1, 3, 12, 0, 0]
Metric	Value
Time Complexity	O(n)
Auxiliary Space	O(1)
In-Place?	✅ Yes
Examples of Not-In-Place Algorithms
Example 1: Reverse Array (Not-In-Place)
Python

# ❌ NOT-IN-PLACE — O(n) auxiliary space
def reverse_not_in_place(arr):
    new_arr = []                      # NEW array created
    for i in range(len(arr) - 1, -1, -1):
        new_arr.append(arr[i])        # fills new array
    return new_arr                    # original unchanged


# Usage:
arr = [1, 2, 3, 4, 5]
result = reverse_not_in_place(arr)
print(arr)     # [1, 2, 3, 4, 5]  ← original UNCHANGED
print(result)  # [5, 4, 3, 2, 1]  ← new array
Metric	Value
Auxiliary Space	O(n)
In-Place?	❌ No
Example 2: Merge Sort
Python

# ❌ NOT-IN-PLACE — O(n) auxiliary space
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])      # new sub-array
    right = merge_sort(arr[mid:])     # new sub-array

    return merge(left, right)


def merge(left, right):
    result = []                        # NEW array for merging
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result
Metric	Value
Time Complexity	O(n log n)
Auxiliary Space	O(n)
In-Place?	❌ No
Example 3: Counting Sort
Python

# ❌ NOT-IN-PLACE — O(k) auxiliary space
def counting_sort(arr):
    if not arr:
        return arr

    max_val = max(arr)
    count = [0] * (max_val + 1)      # NEW count array of size k

    for num in arr:
        count[num] += 1

    output = []                       # NEW output array
    for i in range(len(count)):
        output.extend([i] * count[i])

    return output
Metric	Value
Time Complexity	O(n + k)
Auxiliary Space	O(n + k)
In-Place?	❌ No
Sorting Algorithms Classification
text

┌──────────────────────────────────────────────────────────────┐
│                   SORTING ALGORITHMS                         │
│                                                              │
│   ┌─────────────────────┐    ┌───────────────────────────┐   │
│   │    ✅ IN-PLACE       │    │    ❌ NOT-IN-PLACE        │   │
│   │                     │    │                           │   │
│   │  • Bubble Sort      │    │  • Merge Sort             │   │
│   │    Aux: O(1)        │    │    Aux: O(n)              │   │
│   │                     │    │                           │   │
│   │  • Selection Sort   │    │  • Counting Sort          │   │
│   │    Aux: O(1)        │    │    Aux: O(n + k)          │   │
│   │                     │    │                           │   │
│   │  • Insertion Sort   │    │  • Radix Sort             │   │
│   │    Aux: O(1)        │    │    Aux: O(n + k)          │   │
│   │                     │    │                           │   │
│   │  • Heap Sort        │    │  • Bucket Sort            │   │
│   │    Aux: O(1)        │    │    Aux: O(n + k)          │   │
│   │                     │    │                           │   │
│   │  • Quick Sort  ⚠️   │    │  • Tim Sort               │   │
│   │    Aux: O(log n)    │    │    Aux: O(n)              │   │
│   │    (debatable)      │    │                           │   │
│   │                     │    │                           │   │
│   │  • Shell Sort       │    │                           │   │
│   │    Aux: O(1)        │    │                           │   │
│   └─────────────────────┘    └───────────────────────────┘   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
Detailed Comparison Table
Algorithm	Time (Best)	Time (Avg)	Time (Worst)	Auxiliary Space	In-Place?	Stable?
Bubble Sort	O(n)	O(n²)	O(n²)	O(1)	✅	✅
Selection Sort	O(n²)	O(n²)	O(n²)	O(1)	✅	❌
Insertion Sort	O(n)	O(n²)	O(n²)	O(1)	✅	✅
Heap Sort	O(n log n)	O(n log n)	O(n log n)	O(1)	✅	❌
Quick Sort	O(n log n)	O(n log n)	O(n²)	O(log n)	✅*	❌
Merge Sort	O(n log n)	O(n log n)	O(n log n)	O(n)	❌	✅
Counting Sort	O(n + k)	O(n + k)	O(n + k)	O(n + k)	❌	✅
Radix Sort	O(nk)	O(nk)	O(nk)	O(n + k)	❌	✅
*Quick Sort uses O(log n) stack space — considered in-place under the broad definition.

The Recursion Debate
⚠️ Does recursion make an algorithm NOT in-place?
Every recursive call adds a stack frame to memory.

text

factorial(5)
  → factorial(4)
    → factorial(3)
      → factorial(2)
        → factorial(1)

Call Stack uses O(n) space!
Two Schools of Thought:
text

┌─────────────────────────────────────────────────────┐
│                                                     │
│   STRICT Definition:                                │
│   ─────────────────                                 │
│   In-Place = O(1) auxiliary space ONLY              │
│   Recursion stack counts as auxiliary space          │
│                                                     │
│   → Quick Sort is NOT in-place (O(log n) stack)     │
│   → Recursive Binary Search is NOT in-place         │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│   BROAD Definition (More Common):                   │
│   ────────────────────────────────                  │
│   In-Place = O(1) extra data structures             │
│   Recursion stack (O(log n)) is acceptable          │
│                                                     │
│   → Quick Sort IS in-place                          │
│   → Recursive Binary Search IS in-place             │
│                                                     │
└─────────────────────────────────────────────────────┘
💡 In most interviews and textbooks, the BROAD definition is used.
Quick Sort is almost always classified as in-place.

Strict vs Broad Definition
Definition	Auxiliary Space Allowed	Recursion Stack	Quick Sort
Strict	O(1) only	❌ Counts	Not In-Place
Broad	O(1) data + O(log n) stack	✅ Allowed	In-Place ✅
Examples Under Each Definition:
Algorithm	Strict Definition	Broad Definition
Bubble Sort	✅ In-Place	✅ In-Place
Insertion Sort	✅ In-Place	✅ In-Place
Quick Sort	❌ Not In-Place	✅ In-Place
Iterative Binary Search	✅ In-Place	✅ In-Place
Recursive Binary Search	❌ Not In-Place	✅ In-Place
Merge Sort	❌ Not In-Place	❌ Not In-Place
Advantages & Disadvantages
✅ Advantages of In-Place Algorithms
text

1. 💾 MEMORY EFFICIENT
   → No extra data structures needed
   → Critical for embedded systems / low-memory environments

2. ⚡ CACHE FRIENDLY
   → Works on same memory locations
   → Better CPU cache performance
   → Fewer cache misses

3. 🚫 NO ALLOCATION OVERHEAD
   → No time wasted on malloc/new/append
   → No garbage collection pressure

4. 📏 SCALABILITY
   → Can handle very large inputs without running out of memory
❌ Disadvantages of In-Place Algorithms
text

1. 💥 DESTRUCTIVE
   → Original data is modified / lost
   → Can't recover original if needed

2. 🧠 HARDER TO IMPLEMENT
   → More complex logic (pointer manipulation, swaps)
   → More prone to bugs (off-by-one errors)

3. 📖 LESS READABLE
   → Code can be harder to understand
   → Harder to debug

4. ⚠️ THREAD SAFETY
   → Modifying shared data in-place is NOT thread-safe
   → Concurrent access needs synchronization
When to Use What?
text

┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   USE IN-PLACE ✅ WHEN:                                          │
│   ──────────────────────                                         │
│   • Memory is limited (embedded systems, mobile)                 │
│   • Input is very large and can't afford O(n) extra              │
│   • You don't need the original data anymore                     │
│   • Performance / cache efficiency matters                       │
│   • Interview asks "Can you do it in O(1) space?"                │
│                                                                  │
│   USE NOT-IN-PLACE ❌ WHEN:                                      │
│   ────────────────────────                                       │
│   • You need to preserve the original data                       │
│   • Code readability / maintainability is priority                │
│   • Working with immutable data structures                       │
│   • Stability of sort is required (choose Merge Sort)            │
│   • Multi-threaded environment (safer to create copies)          │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
Classic In-Place Problems (Interview Favorites)
#	Problem	Technique Used	LeetCode
1	Reverse an Array	Two Pointers	—
2	Remove Duplicates from Sorted Array	Read/Write Pointers	#26
3	Remove Element	Two Pointers	#27
4	Move Zeroes	Two Pointers	#283
5	Sort Colors (Dutch National Flag)	Three Pointers	#75
6	Rotate Array	Reverse Technique	#189
7	Next Permutation	Scanning + Swap	#31
8	Rearrange Array (positive/negative)	Partitioning	—
9	Merge Sorted Array (in-place)	Merge from End	#88
10	String Reversal	Two Pointers	#344
11	Valid Palindrome	Two Pointers	#125
12	Rotate Matrix 90°	Transpose + Reverse	#48
13	Set Matrix Zeroes	Use first row/col flags	#73
14	Shuffle an Array (Fisher-Yates)	Random Swap	#384
Common Misconceptions
❌ Misconception	✅ Reality
"In-place means ZERO extra memory"	In-place allows O(1) extra — a few variables, pointers, counters are fine
"In-place is always faster"	Not necessarily — Merge Sort O(n log n) beats Bubble Sort O(n²) despite not being in-place
"In-place is always better"	Not if you need original data preserved or code readability matters
"Creating a single variable makes it not in-place"	A constant number of variables is perfectly fine — still O(1)
"Python sort() is not in-place"	list.sort() IS in-place; sorted(list) is NOT in-place
"Recursion = Not in-place"	Under the broad (common) definition, O(log n) recursion stack is acceptable
Python Specific Gotcha:
Python

# ✅ IN-PLACE: Modifies the original list
arr = [3, 1, 2]
arr.sort()              # arr is now [1, 2, 3]

# ❌ NOT-IN-PLACE: Creates a NEW sorted list
arr = [3, 1, 2]
new_arr = sorted(arr)   # arr is still [3, 1, 2], new_arr is [1, 2, 3]
Summary
text

╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║                    IN-PLACE ALGORITHMS                            ║
║                    ══════════════════                             ║
║                                                                  ║
║   DEFINITION:                                                    ║
║   An algorithm that uses O(1) auxiliary space                     ║
║   (constant extra memory, not counting the input)                ║
║                                                                  ║
║   KEY CHARACTERISTICS:                                           ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │  • Modifies input directly (destructive)               │     ║
║   │  • No new arrays/lists proportional to n               │     ║
║   │  • Only uses temp variables, pointers, counters        │     ║
║   │  • Memory efficient → O(1) auxiliary space             │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   COMMON TECHNIQUES:                                             ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │  • Two Pointers (left/right, read/write)               │     ║
║   │  • Swapping elements                                   │     ║
║   │  • Reverse sub-sections                                │     ║
║   │  • Partitioning (Quick Sort style)                     │     ║
║   │  • Using input array as hash/flag storage              │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   FORMULA:                                                       ║
║   ┌────────────────────────────────────────────────────────┐     ║
║   │                                                        │     ║
║   │   In-Place   →  Auxiliary Space = O(1)                 │     ║
║   │   Out-of-Place → Auxiliary Space = O(n) or more        │     ║
║   │                                                        │     ║
║   └────────────────────────────────────────────────────────┘     ║
║                                                                  ║
║   REMEMBER:                                                      ║
║   "In-place ≠ No extra memory"                                   ║
║   "In-place = CONSTANT extra memory"                             ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
🤝 Contributing
Feel free to open an issue or submit a PR to add more examples,
problems, or corrections.

📄 License
This project is licensed under the MIT License.

text


This README covers **everything** about In-Place Algorithms:

- ✅ **Clear definitions** with formal notation
- ✅ **Visual diagrams** showing the difference
- ✅ **5 coded in-place examples** with step-by-step visualization
- ✅ **3 not-in-place counter-examples** for comparison
- ✅ **Sorting algorithms classification** (complete table)
- ✅ **The recursion debate** (strict vs broad)
- ✅ **Advantages & disadvantages**
- ✅ **When to use which** (decision guide)
- ✅ **14 classic interview problems** with LeetCode links
- ✅ **Common misconceptions** busted
- ✅ **Python-specific gotcha** (`sort()` vs `sorted()`)