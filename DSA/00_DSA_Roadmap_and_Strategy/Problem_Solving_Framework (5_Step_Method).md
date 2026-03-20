🧩 Problem Solving Frameworks for DSA
You don't need to be a genius. You need a system. A repeatable framework that turns confusion into clarity — every single time.

📌 Table of Contents
Why You Need a Framework
The Master Framework — UMPIRE
Step 1 — Understand
Step 2 — Match
Step 3 — Plan
Step 4 — Implement
Step 5 — Review
Step 6 — Evaluate
The Pattern Recognition System
The Constraint Analysis Framework
The "What Changes, What Stays" Framework
The Brute Force → Optimize Pipeline
The Subproblem Decomposition Framework
The State Machine Framework
The "Work Backwards" Framework
The Input → Output Mapping Framework
The Visualization Framework
When You're Completely Stuck
Framework Selection Guide
Building Your Own Intuition
💡 Why You Need a Framework
text

WITHOUT A FRAMEWORK:
  → Read the problem
  → Stare at it
  → Panic
  → Try random things
  → Google the answer
  → "Understand" it
  → Forget it in 2 days

WITH A FRAMEWORK:
  → Read the problem
  → Ask structured questions
  → Identify the pattern
  → Build from brute force to optimal
  → Understand WHY it works
  → Remember it because you DERIVED it
The Core Principle
text

Every DSA problem in existence is either:

  1. A problem you've seen before (RECALL)
  2. A combination of patterns you've seen before (COMBINE)
  3. A twist on a pattern you've seen before (ADAPT)

You are NEVER truly solving from scratch.
The framework helps you CONNECT the unknown to the known.
🏛️ The Master Framework — UMPIRE
This is your default framework for every single problem.

text

U — UNDERSTAND the problem
M — MATCH to a known pattern
P — PLAN your approach
I — IMPLEMENT the solution
R — REVIEW and debug
E — EVALUATE complexity

Use this EVERY TIME. No exceptions.
Even if the problem seems easy.
Even if you've "seen it before."
Why UMPIRE Works
text

Most people fail NOT because the problem is too hard.
They fail because they:

  → Misunderstood the problem         (skipped U)
  → Couldn't connect it to anything   (skipped M)
  → Started coding without a plan     (skipped P)
  → Wrote buggy, unstructured code    (rushed I)
  → Didn't test before submitting     (skipped R)
  → Couldn't analyze their solution   (skipped E)

UMPIRE prevents ALL of these failures.
Step 1 — UNDERSTAND the Problem
Time allocation: 5-8 minutes (out of 45)
This is where most people fail. Not because they can't solve it — because they solve the wrong problem.

The Understanding Checklist
text

READ the problem statement — TWICE. Then ask yourself:

□ What are the INPUTS?
  → Type? (array, string, tree, graph, number)
  → Size? (constraints)
  → Properties? (sorted? positive? unique?)

□ What are the OUTPUTS?
  → Type? (number, boolean, array, string)
  → What exactly should I return?
  → What if there are multiple valid answers?

□ What are the CONSTRAINTS?
  → Input size (n)
  → Value ranges
  → Time/memory limits

□ What are the EDGE CASES?
  → Empty input
  → Single element
  → All same elements
  → Already solved input (sorted array for "sort this")
  → Minimum and maximum constraints
  → Negative numbers, zeros, overflow possibilities

□ Can I RESTATE the problem in my own words?
  → If you can't explain it simply, you don't understand it.
The Clarifying Questions Toolkit
Ask these BEFORE solving — in interviews, ask the interviewer. In practice, answer them yourself.

text

ABOUT INPUT:
  "Can the input be empty?"
  "Can values be negative?"
  "Can there be duplicates?"
  "Is the input sorted?"
  "Are there any special characters (for strings)?"
  "Is the graph connected? Directed? Weighted?"
  "Can there be cycles?"

ABOUT OUTPUT:
  "Should I return the value or the index?"
  "What if there's no valid answer — return -1, null, empty?"
  "If multiple answers exist, should I return all or any one?"
  "Does the order of the output matter?"

ABOUT CONSTRAINTS:
  "What's the maximum input size?"
  "What's the expected time complexity?"
  "Can I modify the input in-place?"
  "Is extra space allowed?"
The Example Walkthrough
text

FOR EVERY PROBLEM, create at least 3 examples:

Example 1 — The BASIC case
  → Use the given example or create a simple one
  → Trace through manually step by step
  → Verify your understanding matches the expected output

Example 2 — An EDGE case
  → Empty input, single element, or boundary condition
  → Make sure you know what should happen

Example 3 — A TRICKY case
  → Duplicates, negative numbers, or unusual structure
  → This often reveals hidden complexity you missed
🎯 The golden rule: If you can't solve it by hand on paper, you can't solve it in code.

Step 2 — MATCH to a Known Pattern
Time allocation: 3-5 minutes
This is where pattern recognition transforms you from a struggling beginner to a confident problem solver.

The Pattern Matching Decision Tree
text

START: "What type of problem is this?"
│
├─ "Am I searching for something?"
│   ├─ In a SORTED structure? → Binary Search
│   ├─ In a GRAPH/TREE? → BFS / DFS
│   ├─ For a PAIR that satisfies a condition? → Two Pointers / Hashing
│   └─ For an OPTIMAL value? → Binary Search on Answer
│
├─ "Am I looking at SUBARRAYS or SUBSTRINGS?"
│   ├─ Fixed size? → Fixed Sliding Window
│   ├─ Variable size with a condition? → Variable Sliding Window
│   ├─ Need sum of a range? → Prefix Sum
│   └─ Need min/max in a window? → Monotonic Deque
│
├─ "Am I making CHOICES and need the BEST outcome?"
│   ├─ Choices affect future choices? → Dynamic Programming
│   ├─ Local best = Global best? → Greedy
│   └─ Need to TRY all possibilities? → Backtracking
│
├─ "Am I working with a SEQUENCE and ORDER matters?"
│   ├─ Need to sort? → Sorting Algorithm
│   ├─ Need next greater/smaller? → Monotonic Stack
│   ├─ Need to process in a specific order? → Stack / Queue
│   └─ Need to merge sorted things? → Merge technique / Heap
│
├─ "Am I working with a TREE?"
│   ├─ Need to visit all nodes? → DFS (inorder/preorder/postorder)
│   ├─ Need level-by-level? → BFS (level order)
│   ├─ Need to search efficiently? → BST properties
│   └─ Need path/ancestor info? → DFS with backtracking
│
├─ "Am I working with a GRAPH?"
│   ├─ Shortest path (unweighted)? → BFS
│   ├─ Shortest path (weighted)? → Dijkstra / Bellman-Ford
│   ├─ Connected components? → DFS / BFS / Union-Find
│   ├─ Ordering with dependencies? → Topological Sort
│   ├─ Minimum spanning tree? → Kruskal / Prim
│   └─ Cycle detection? → DFS with colors / Union-Find
│
├─ "Am I counting FREQUENCY or checking EXISTENCE?"
│   → Hash Map / Hash Set
│
├─ "Am I working with INTERVALS?"
│   ├─ Merge overlapping? → Sort + Merge
│   ├─ Find conflicts? → Sort + Compare
│   └─ Insert/delete ranges? → Line Sweep / TreeMap
│
└─ "Am I generating ALL COMBINATIONS or PERMUTATIONS?"
    → Backtracking / Recursion
The Quick Pattern Signals
If You See This...	Think This Pattern
"Sorted array"	Binary Search, Two Pointers
"Find pair/triplet with sum"	Two Pointers, Hashing
"Subarray with condition"	Sliding Window, Prefix Sum
"Longest/shortest substring"	Sliding Window (variable)
"Top K" or "K-th largest"	Heap, QuickSelect
"How many ways" or "minimum cost"	Dynamic Programming
"All possible" combinations	Backtracking
"Connected" or "reachable"	BFS / DFS / Union-Find
"Order of tasks with prerequisites"	Topological Sort
"Next greater element"	Monotonic Stack
"Merge K sorted"	Heap
"Interval overlap"	Sorting + Line Sweep
"Palindrome"	Two Pointers, DP
"Parentheses / brackets"	Stack
"Matrix traversal"	BFS / DFS (treat as graph)
"Bitwise operation"	Bit Manipulation
"Maximum/minimum with constraint"	Binary Search on Answer, DP
"Stream of data"	Heap, Design
"LRU / LFU Cache"	Hash Map + Doubly Linked List
"Prefix matching in strings"	Trie
When You Can't Identify the Pattern
text

DON'T PANIC. Do this instead:

1. Look at the CONSTRAINTS → they hint at expected complexity
2. Think about BRUTE FORCE → what would the naive approach be?
3. Identify the BOTTLENECK → what makes brute force slow?
4. Ask "WHAT IF the input were sorted?" → does that help?
5. Ask "WHAT IF I had a hash map of all values?" → does that help?
6. Ask "WHAT IF I processed from right to left?" → does that change things?
7. Try SMALL examples → sometimes patterns emerge from the data
Step 3 — PLAN Your Approach
Time allocation: 5-7 minutes
The plan is your blueprint. Code without a plan is like building without a foundation.

The Planning Template
text

STEP 1: State the approach in plain English
  "I will use a sliding window of variable size because 
   I need the longest subarray where the sum is ≤ k"

STEP 2: List the steps
  1. Initialize two pointers (left, right) at 0
  2. Expand right pointer, adding elements to current sum
  3. While sum > k, shrink from left
  4. Update max length at each valid window
  5. Return max length

STEP 3: Identify the data structures needed
  "I need: two pointers (int), current sum (int), max length (int)"

STEP 4: Think through edge cases
  "Empty array → return 0"
  "All elements > k → return 0"
  "Entire array sum ≤ k → return n"

STEP 5: State the expected complexity
  "Time: O(n) — each element visited at most twice
   Space: O(1) — only using variables"
The "Before You Code" Checklist
text

Before writing a SINGLE line of code, you should be able to answer:

□ What data structure(s) will I use?
□ What variables do I need to track?
□ What is my loop structure? (single loop, nested, while, etc.)
□ What is my termination condition?
□ How do I handle the base case / edge case?
□ What do I return?
□ What is the time complexity?
□ What is the space complexity?

If you can't answer ALL of these → you're not ready to code.
Go back to UNDERSTAND or MATCH.
The Approach Comparison Table
When you see multiple approaches, compare them explicitly:

text

EXAMPLE: Two Sum Problem

| Approach | Time | Space | Pros | Cons |
|----------|------|-------|------|------|
| Brute Force (two loops) | O(n²) | O(1) | Simple | Slow |
| Sort + Two Pointers | O(n log n) | O(1) | No extra space | Modifies order |
| Hash Map | O(n) | O(n) | Fastest | Uses extra space |

DECISION: Hash Map — optimal time, acceptable space.
🎯 In interviews, SAYING this comparison out loud is extremely impressive.

Step 4 — IMPLEMENT the Solution
Time allocation: 15-20 minutes
Write code like someone else will read it in 5 minutes — because in an interview, someone will.

The Implementation Principles
text

PRINCIPLE 1: TRANSLATE your plan, don't improvise
  → Your plan is your pseudocode
  → Each step in your plan = a block of code
  → If you're writing something NOT in your plan → stop and rethink

PRINCIPLE 2: START with the skeleton
  → Function signature
  → Edge case handling
  → Main loop structure
  → Return statement
  → THEN fill in the logic

PRINCIPLE 3: NAME things meaningfully
  → "left" and "right" NOT "i" and "j" (for two pointers)
  → "freq_map" NOT "d" (for frequency hash map)
  → "max_length" NOT "ans" (for tracking the answer)
  → Your variable names should tell a STORY

PRINCIPLE 4: WRITE incrementally
  → Write a few lines
  → Mentally trace through them
  → Then continue
  → DON'T write the entire solution and then check

PRINCIPLE 5: HANDLE EDGE CASES first
  → Put them at the top of your function
  → Get them out of the way
  → Then your main logic can focus on the general case
The Code Structure Template
text

function solve(input):

    // SECTION 1: Edge cases
    if input is empty or invalid:
        return base case answer

    // SECTION 2: Initialize data structures and variables
    create necessary structures
    set tracking variables

    // SECTION 3: Main logic (loop / recursion)
    for each element or state:
        process current element
        update data structures
        update answer if applicable

    // SECTION 4: Return result
    return answer
Common Implementation Mistakes to Prevent
text

MISTAKE 1: Off-by-one errors
  PREVENTION: Be explicit about inclusive vs exclusive bounds.
              When in doubt, trace through a 2-element example.

MISTAKE 2: Not initializing variables correctly
  PREVENTION: Think about what the "identity" value is.
              → For max → initialize to -infinity or smallest possible
              → For min → initialize to +infinity or largest possible
              → For sum → initialize to 0
              → For product → initialize to 1

MISTAKE 3: Modifying a collection while iterating over it
  PREVENTION: Use a copy, or collect changes and apply after.

MISTAKE 4: Forgetting to return a value
  PREVENTION: Write the return statement FIRST, then fill in the logic.

MISTAKE 5: Integer overflow
  PREVENTION: Use appropriate types (long long in C++, long in Java).
              Python handles this automatically.

MISTAKE 6: Wrong loop bounds
  PREVENTION: Ask "what is the FIRST valid index?" and 
              "what is the LAST valid index?" before writing the loop.
Step 5 — REVIEW and Debug
Time allocation: 5-7 minutes
Never say "I'm done" without testing. Testing IS part of solving.

The Review Process
text

PHASE 1: READ your code line by line
  → Pretend you've never seen this code
  → Does each line do what you INTENDED?
  → Are variable names consistent?
  → Any typos or syntax errors?

PHASE 2: DRY RUN with the basic example
  → Trace through your code with Example 1
  → Write down variable values at each step
  → Does it produce the expected output?

PHASE 3: DRY RUN with an edge case
  → Trace through with the edge case
  → Does it handle empty input correctly?
  → Does it handle single element correctly?

PHASE 4: THINK about what could go wrong
  → What if all elements are the same?
  → What if the answer is at the boundary?
  → What if the input is already the answer?

PHASE 5: FIX any bugs found
  → Fix the ROOT CAUSE, not the symptom
  → After fixing, re-run mental tests
The Debugging Framework — When Something Goes Wrong
text

YOUR CODE GIVES WRONG OUTPUT. NOW WHAT?

Step 1: IDENTIFY where it goes wrong
  → Trace through step by step
  → At which step does the actual value differ from expected?
  → That's your bug location

Step 2: CLASSIFY the bug type
  → Off-by-one? (loop bounds, array indexing)
  → Wrong condition? (< vs <=, && vs ||)
  → Wrong update? (updating wrong variable)
  → Missing case? (edge case not handled)
  → Wrong initialization? (starting value incorrect)
  → Wrong data structure operation? (push vs append, etc.)

Step 3: FIX precisely
  → Change the MINIMUM amount of code
  → Don't restructure your entire solution for one bug
  → If you need to restructure → your plan was wrong → go back to PLAN

Step 4: VERIFY the fix
  → Re-trace through the failing example
  → Also re-trace through a passing example (make sure you didn't break it)
The Test Case Generation Strategy
text

ALWAYS test with these categories:

CATEGORY 1 — BASIC
  → The given example
  → A simple case you can verify mentally

CATEGORY 2 — SMALL
  → n = 0 (empty)
  → n = 1 (single element)
  → n = 2 (smallest interesting case)

CATEGORY 3 — BOUNDARY
  → Maximum values
  → Minimum values
  → First/last element is the answer

CATEGORY 4 — SPECIAL
  → All elements identical
  → Already sorted (ascending)
  → Reverse sorted (descending)
  → Alternating pattern

CATEGORY 5 — STRESS (if time permits)
  → Large input (does it TLE?)
  → Random input (compare with brute force)
Step 6 — EVALUATE Complexity
Time allocation: 2-3 minutes
If you can't analyze your own solution, you don't fully understand it.

Time Complexity Analysis Framework
text

STEP 1: Identify the LOOPS
  → Single loop over n elements → O(n)
  → Nested loops (each over n) → O(n²)
  → Loop with halving (binary search) → O(log n)
  → Loop over n with inner binary search → O(n log n)

STEP 2: Identify RECURSIVE calls
  → How many branches at each level?
  → How deep is the recursion?
  → Total work = branches^depth × work_per_call
  → Use the Master Theorem for divide & conquer

STEP 3: Identify DATA STRUCTURE operations
  → Hash map insert/lookup → O(1) average
  → Balanced BST insert/lookup → O(log n)
  → Heap push/pop → O(log n)
  → Sorting → O(n log n)

STEP 4: COMBINE
  → Add complexities for sequential operations: O(n) + O(n log n) = O(n log n)
  → Multiply for nested operations: O(n) × O(log n) = O(n log n)
  → Take the dominant term: O(n² + n) = O(n²)
Space Complexity Analysis Framework
text

COUNT what you're storing:

→ A few variables → O(1)
→ A hash map with up to n entries → O(n)
→ A 2D matrix of n × m → O(n × m)
→ Recursion call stack of depth d → O(d)
→ Creating a copy of the input → O(n)

DON'T FORGET:
→ Recursion stack space
→ The output itself (sometimes counted, sometimes not)
→ Temporary data structures
The Complexity Communication Template
text

"My solution runs in O(n log n) time because:
 - I sort the array first → O(n log n)
 - Then I do a single pass with two pointers → O(n)
 - Dominant term is O(n log n)

 Space complexity is O(1) because:
 - I sort in-place
 - I only use a constant number of variables
 - No additional data structures"
🎯 The Pattern Recognition System
The most powerful skill in DSA is recognizing which problem THIS problem is REALLY asking.

The 15 Core Patterns
text

PATTERN 1 — SLIDING WINDOW
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Contiguous subarray/substring            │
  │   → "Longest", "shortest", "maximum sum"     │
  │   → With a specific condition/constraint     │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Maintain a window [left...right]          │
  │   → Expand right to include more              │
  │   → Shrink left when condition is violated    │
  │   → Update answer at each valid state         │
  │                                               │
  │ VARIATIONS:                                   │
  │   → Fixed size window                         │
  │   → Variable size window                      │
  │   → Window with hash map (frequency tracking) │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "contiguous", "subarray", "substring"     │
  │   → "at most K distinct", "sum ≤ K"           │
  │   → "longest", "shortest", "minimum length"   │
  └─────────────────────────────────────────────┘

PATTERN 2 — TWO POINTERS
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Sorted array, find pairs/triplets        │
  │   → Remove duplicates in-place               │
  │   → Merge two sorted arrays                  │
  │   → Palindrome checking                      │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Two pointers moving toward each other     │
  │   → OR two pointers moving in same direction  │
  │   → OR fast and slow pointers                 │
  │                                               │
  │ VARIATIONS:                                   │
  │   → Opposite direction (start/end)            │
  │   → Same direction (slow/fast)                │
  │   → Multiple arrays                           │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "sorted array", "pair with sum"           │
  │   → "in-place", "remove duplicates"           │
  │   → "palindrome", "reverse"                   │
  └─────────────────────────────────────────────┘

PATTERN 3 — BINARY SEARCH
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Sorted data                              │
  │   → "Find position", "search"                │
  │   → Minimize maximum or maximize minimum     │
  │   → Monotonic condition (T T T F F F)         │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Eliminate half the search space each step │
  │   → If condition is monotonic → binary search │
  │                                               │
  │ VARIATIONS:                                   │
  │   → Classic binary search                     │
  │   → Binary search on answer space             │
  │   → Binary search on rotated array            │
  │   → First/last occurrence                     │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "sorted", "find minimum/maximum"          │
  │   → "is it possible with value X?"            │
  │   → "minimize the maximum"                    │
  │   → Constraints: n ≤ 10^9 (too large for O(n))│
  └─────────────────────────────────────────────┘

PATTERN 4 — HASHING
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Need O(1) lookup                         │
  │   → Counting frequency                       │
  │   → Finding duplicates                       │
  │   → Grouping / categorizing elements         │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Trade space for time                      │
  │   → Store what you've seen, look up instantly │
  │                                               │
  │ VARIATIONS:                                   │
  │   → Hash set (existence check)                │
  │   → Hash map (key-value mapping)              │
  │   → Frequency map (counting occurrences)      │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "find if exists", "count occurrences"     │
  │   → "two sum", "group anagrams"               │
  │   → "first non-repeating"                     │
  └─────────────────────────────────────────────┘

PATTERN 5 — DYNAMIC PROGRAMMING
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Optimal substructure (best = best of parts)│
  │   → Overlapping subproblems                  │
  │   → "Count ways", "min/max cost", "is possible"│
  │                                               │
  │ KEY IDEA:                                     │
  │   → Define STATE clearly                      │
  │   → Define TRANSITION (recurrence relation)   │
  │   → Define BASE CASE                          │
  │   → Build bottom-up or use memoization        │
  │                                               │
  │ VARIATIONS:                                   │
  │   → 1D DP (linear sequence)                   │
  │   → 2D DP (grid, two sequences)               │
  │   → Knapsack variants                         │
  │   → Interval DP                               │
  │   → Bitmask DP                                │
  │   → DP on trees                               │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "how many ways", "minimum cost"           │
  │   → "can you reach", "longest subsequence"    │
  │   → "partition into", "make change for"       │
  │   → Choices at each step that affect the future│
  └─────────────────────────────────────────────┘

PATTERN 6 — GREEDY
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Local optimal leads to global optimal    │
  │   → Sorting + picking best at each step works│
  │   → No "undo" or backtracking needed         │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Make the best choice at each step         │
  │   → Never look back                           │
  │   → Prove (or intuit) that local best = global│
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "minimum number of", "maximum number of"  │
  │   → Interval scheduling, activity selection   │
  │   → "can you do it?" (feasibility)            │
  │   → Problem FEELS like DP but choices don't   │
  │     interact with each other                  │
  └─────────────────────────────────────────────┘

PATTERN 7 — BACKTRACKING
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Generate ALL possibilities               │
  │   → "Find all combinations/permutations"     │
  │   → Constraint satisfaction (Sudoku, N-Queens)│
  │                                               │
  │ KEY IDEA:                                     │
  │   → Make a choice                             │
  │   → Recurse                                   │
  │   → UNDO the choice (backtrack)               │
  │   → Try the next option                       │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "all possible", "generate all"            │
  │   → "permutations", "combinations", "subsets" │
  │   → "place N items such that"                 │
  │   → Small constraints (n ≤ 15-20)             │
  └─────────────────────────────────────────────┘

PATTERN 8 — BFS / LEVEL-ORDER
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Shortest path in UNWEIGHTED graph        │
  │   → Level-by-level processing                │
  │   → "Minimum steps", "nearest"               │
  │   → Multi-source traversal                   │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Use a QUEUE                               │
  │   → Process level by level                    │
  │   → First time you reach a node = shortest    │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "shortest path", "minimum moves"          │
  │   → "nearest", "level order"                  │
  │   → Grid with obstacles                       │
  │   → "spreading" (fire, infection, ripple)     │
  └─────────────────────────────────────────────┘

PATTERN 9 — DFS / DEPTH-FIRST
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Tree/graph traversal                     │
  │   → Path finding                             │
  │   → Connected components                     │
  │   → Cycle detection                          │
  │   → Exhaustive search                        │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Go as DEEP as possible before backtracking│
  │   → Use RECURSION or explicit STACK           │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "is there a path", "connected"            │
  │   → "all paths from A to B"                   │
  │   → "number of islands"                       │
  │   → "has cycle"                               │
  └─────────────────────────────────────────────┘

PATTERN 10 — MONOTONIC STACK
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Next greater / smaller element           │
  │   → Previous greater / smaller element       │
  │   → Largest rectangle in histogram           │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Maintain stack in increasing/decreasing   │
  │     order                                     │
  │   → Pop elements that violate the order       │
  │   → The popped element found its "answer"     │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "next greater", "next smaller"            │
  │   → "days until warmer temperature"           │
  │   → "stock span", "largest rectangle"         │
  └─────────────────────────────────────────────┘

PATTERN 11 — UNION-FIND (Disjoint Set)
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Dynamic connectivity                    │
  │   → "Are A and B connected?"                 │
  │   → Grouping elements into clusters          │
  │   → Kruskal's MST                           │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Union: merge two groups                   │
  │   → Find: which group does X belong to?       │
  │   → Path compression + rank for efficiency    │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "connected components" (dynamic)          │
  │   → "merge groups", "same group"              │
  │   → "earliest time all connected"             │
  └─────────────────────────────────────────────┘

PATTERN 12 — TOPOLOGICAL SORT
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Ordering with dependencies               │
  │   → "Can all tasks be completed?"             │
  │   → "In what order should I process?"         │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Build a Directed Acyclic Graph (DAG)      │
  │   → Process nodes with zero in-degree first   │
  │   → Remove processed nodes, update in-degrees │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "prerequisites", "dependencies"           │
  │   → "course schedule", "build order"          │
  │   → "is there a valid ordering"               │
  └─────────────────────────────────────────────┘

PATTERN 13 — HEAP / PRIORITY QUEUE
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Need repeated access to min/max          │
  │   → Top-K elements                           │
  │   → Merge K sorted lists                     │
  │   → Median from data stream                  │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Efficiently maintain min or max           │
  │   → Push and pop in O(log n)                  │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "K-th largest", "top K frequent"          │
  │   → "merge K sorted"                          │
  │   → "median", "schedule by priority"          │
  └─────────────────────────────────────────────┘

PATTERN 14 — PREFIX SUM
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Range sum queries                        │
  │   → Subarray sum equals K                    │
  │   → Difference array for range updates       │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Precompute cumulative sums               │
  │   → Sum of [i...j] = prefix[j+1] - prefix[i] │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "sum of subarray", "range sum"            │
  │   → "number of subarrays with sum = K"        │
  │   → "equilibrium index"                       │
  └─────────────────────────────────────────────┘

PATTERN 15 — TRIE
  ┌─────────────────────────────────────────────┐
  │ USE WHEN:                                    │
  │   → Prefix-based search                      │
  │   → Autocomplete                             │
  │   → Word dictionary with wildcards           │
  │   → XOR-based problems                       │
  │                                               │
  │ KEY IDEA:                                     │
  │   → Tree where each edge is a character       │
  │   → Shared prefixes share paths               │
  │                                               │
  │ SIGNALS IN PROBLEM:                           │
  │   → "starts with prefix", "word search"       │
  │   → "autocomplete", "dictionary"              │
  │   → "maximum XOR"                             │
  └─────────────────────────────────────────────┘
📏 The Constraint Analysis Framework
Constraints are the BIGGEST hint the problem gives you. Learn to read them like a treasure map.

text

╔══════════════════════════════════════════════════════════╗
║              CONSTRAINT → COMPLEXITY MAP                 ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  n ≤ 10          → O(n!) or O(2^n)                      ║
║                     Brute force, permutations,           ║
║                     backtracking                         ║
║                                                          ║
║  n ≤ 20          → O(2^n) or O(n × 2^n)                ║
║                     Bitmask DP, meet in the middle       ║
║                                                          ║
║  n ≤ 100         → O(n³)                                ║
║                     Triple nested loops, Floyd-Warshall  ║
║                                                          ║
║  n ≤ 500         → O(n³) with small constant            ║
║                     DP on intervals                      ║
║                                                          ║
║  n ≤ 1,000       → O(n²) comfortably                   ║
║                     Nested loops, 2D DP                  ║
║                                                          ║
║  n ≤ 5,000       → O(n²) tightly                       ║
║                     Optimized n² with pruning            ║
║                                                          ║
║  n ≤ 10,000      → O(n²) barely or O(n√n)              ║
║                     Need optimization tricks             ║
║                                                          ║
║  n ≤ 100,000     → O(n log n) or O(n)                  ║
║                     Sorting, binary search, two          ║
║                     pointers, sliding window, heaps      ║
║                                                          ║
║  n ≤ 1,000,000   → O(n) or O(n log n)                  ║
║                     Linear scan, hashing, prefix sum     ║
║                                                          ║
║  n ≤ 10,000,000  → O(n) strictly                       ║
║                     Single pass, no log factor           ║
║                                                          ║
║  n ≤ 10^9        → O(log n) or O(√n)                   ║
║                     Binary search, math formula          ║
║                                                          ║
║  n ≤ 10^18       → O(log n) or O(1)                    ║
║                     Math, binary exponentiation          ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝
How to Use This in Practice
text

EXAMPLE: "Given an array of n integers where n ≤ 10^5, find..."

YOUR THINKING:
  → n = 10^5 → I need O(n log n) or better
  → O(n²) = 10^10 → WAY too slow
  → So brute force with nested loops is OUT
  → I need: sorting, binary search, hashing, 
    two pointers, sliding window, or similar
  → This ELIMINATES many approaches instantly
  → Now I only consider O(n) or O(n log n) techniques
🔄 The "What Changes, What Stays" Framework
When you're stuck, ask: "As I move through the input, what information CHANGES and what STAYS the same?"

text

THIS FRAMEWORK REVEALS:
  → What to TRACK (variables, data structures)
  → What to UPDATE at each step
  → What the INVARIANT is (the thing that should always be true)
How It Works
text

EXAMPLE: "Find the maximum sum subarray of size K"

WHAT CHANGES:
  → The window position (moves right by 1 each step)
  → The current window sum

WHAT STAYS:
  → The window SIZE (always K)
  → The maximum sum seen so far (only increases or stays)

INSIGHT:
  → I don't need to recalculate the sum from scratch each time
  → I just ADD the new element and REMOVE the old one
  → This gives me O(n) instead of O(n × K)
text

EXAMPLE: "Find if any two elements sum to target in an unsorted array"

WHAT CHANGES:
  → The current element I'm looking at
  → The set of elements I've already seen

WHAT STAYS:
  → The target sum

INSIGHT:
  → For each element, I need target - element
  → I can check if that COMPLEMENT exists in what I've already seen
  → A hash set stores what I've seen → O(1) lookup
  → This gives me O(n) instead of O(n²)
text

EXAMPLE: "Find the longest substring without repeating characters"

WHAT CHANGES:
  → The window boundaries (left and right)
  → The set of characters in the current window
  → The length of the current valid window

WHAT STAYS:
  → The condition: "no repeating characters"
  → The maximum length found so far

INSIGHT:
  → Expand RIGHT to add characters
  → When a REPEAT is found, shrink LEFT until it's gone
  → This is a VARIABLE SLIDING WINDOW
🔨 The Brute Force → Optimize Pipeline
Every optimal solution started as a brute force. The journey from brute to optimal is a SYSTEMATIC process, not a lucky guess.

The Pipeline
text

STAGE 1: BRUTE FORCE
  → Try everything
  → Usually involves nested loops or generating all possibilities
  → Don't worry about efficiency — focus on CORRECTNESS
  → This is your SAFETY NET in interviews

         ↓ Ask: "What's making this slow?"

STAGE 2: IDENTIFY THE BOTTLENECK
  → Which operation is repeated unnecessarily?
  → What information am I recalculating that I could cache?
  → Am I comparing all pairs when I only need specific ones?
  → Am I searching linearly when the data has structure?

         ↓ Ask: "How can I eliminate redundant work?"

STAGE 3: APPLY AN OPTIMIZATION TECHNIQUE

  TECHNIQUE A: "Can I SORT the input?"
    → Sorting enables binary search, two pointers, greedy
    → O(n²) search → O(n log n) sort + O(n) scan

  TECHNIQUE B: "Can I use a HASH MAP?"
    → Trading space for time
    → O(n) lookup instead of O(n) search each time

  TECHNIQUE C: "Can I use a SLIDING WINDOW?"
    → Reusing computation from previous window
    → O(n × K) → O(n)

  TECHNIQUE D: "Can I PRECOMPUTE something?"
    → Prefix sums, frequency arrays, etc.
    → O(n) per query → O(1) per query after O(n) setup

  TECHNIQUE E: "Can I DIVIDE AND CONQUER?"
    → Break into smaller subproblems
    → O(n²) → O(n log n)

  TECHNIQUE F: "Can I use DP instead of recursion?"
    → Caching overlapping subproblems
    → O(2^n) → O(n²) or O(n × amount), etc.

  TECHNIQUE G: "Can I use a HEAP for repeated min/max?"
    → Instead of scanning entire array each time
    → O(n) per operation → O(log n) per operation

  TECHNIQUE H: "Can I BINARY SEARCH on the answer?"
    → If the answer is monotonic
    → O(n) search for answer → O(log(range)) checks

         ↓ Ask: "Can I do even better?"

STAGE 4: VERIFY OPTIMALITY
  → Is this the best possible for this problem?
  → Does the lower bound match? (e.g., must look at all elements → Ω(n))
  → Are there known optimal algorithms for this problem class?
The Bottleneck Identification Cheat Sheet
text

IF BRUTE FORCE IS...          THE BOTTLENECK IS...        TRY...

O(n²) from two nested loops   Searching inner loop        Hashing, Sorting + Binary Search
O(n²) from all pairs          Comparing all pairs         Two Pointers, Sorting
O(n × K) from window sum      Recalculating window        Sliding Window
O(2^n) from all subsets       Exploring all subsets       DP (if overlapping subproblems)
O(n!) from all permutations   Too many permutations       Backtracking with pruning, DP
O(n × m) from grid scanning   Repeated BFS/DFS            Precomputation, Union-Find
O(n) per query × Q queries    Linear search each query    Precompute (prefix sum, sparse table)
🧱 The Subproblem Decomposition Framework
Big problems are just small problems stitched together. The trick is finding the RIGHT seam.

How to Decompose
text

ASK: "Can I solve a SMALLER version of this problem?"

EXAMPLE: "Find the longest increasing subsequence"

SMALLER VERSION:
  → What's the longest increasing subsequence ending at index i?
  → If I know this for all i < current, can I compute it for current?
  → YES → dp[i] = max(dp[j] + 1) for all j < i where arr[j] < arr[i]

THIS IS DP. The subproblem is the KEY to finding the recurrence.
The Subproblem Discovery Questions
text

1. "If I only had the FIRST i elements, could I solve it?"
   → Linear DP: dp[i]

2. "If I only had elements from index i to j, could I solve it?"
   → Interval DP: dp[i][j]

3. "If I had unlimited items of the first i types, 
    and capacity j, could I solve it?"
   → Knapsack DP: dp[i][j]

4. "If I matched the first i characters of string A 
    with the first j characters of string B?"
   → Two-sequence DP: dp[i][j]

5. "If I'm at node v in the tree, what's the answer 
    for the subtree rooted at v?"
   → Tree DP: dp[v]

6. "If I've visited the set S of nodes and I'm currently at node v?"
   → Bitmask DP: dp[mask][v]
⚙️ The State Machine Framework
Some problems are best understood as state transitions. At each step, you're IN a state, and you MOVE to another state.

How to Think in States
text

STEP 1: Define your STATES
  → What information do I need to make the next decision?
  → This becomes your DP state or your variable set

STEP 2: Define your TRANSITIONS
  → From each state, what actions can I take?
  → Each action leads to a new state

STEP 3: Define your BASE STATE
  → Where do I start?
  → What's the initial value?

STEP 4: Define your GOAL STATE
  → Where do I want to end up?
  → What am I optimizing?
Classic Example: Best Time to Buy and Sell Stock
text

STATES:
  → Day i, HOLDING a stock
  → Day i, NOT HOLDING a stock

TRANSITIONS:
  → NOT HOLDING → BUY → HOLDING (cost: -price[i])
  → HOLDING → SELL → NOT HOLDING (gain: +price[i])
  → HOLDING → HOLD → HOLDING (no change)
  → NOT HOLDING → SKIP → NOT HOLDING (no change)

BASE STATE:
  → Day 0, NOT HOLDING → profit = 0
  → Day 0, HOLDING → profit = -price[0]

GOAL STATE:
  → Day n-1, NOT HOLDING → maximum profit

This framework makes ALL stock problem variants solvable:
  → One transaction, multiple transactions, K transactions,
    with cooldown, with fee — ALL use this state machine.
⏪ The "Work Backwards" Framework
Sometimes the problem is easier to solve if you start from the END.

When to Use
text

USE WHEN:
  → The end condition is well-defined but the start is ambiguous
  → Forward processing creates too many branches
  → The problem involves "reaching" a target
  → Reverse processing simplifies the logic
Examples
text

EXAMPLE 1: "Given a target, find operations to reach it from 1"
  → FORWARD: From 1, try multiply by 2 or add 1 → exponential branching
  → BACKWARD: From target, if even → divide by 2, if odd → subtract 1
  → Much simpler — only one choice at each step

EXAMPLE 2: "Next greater element" 
  → FORWARD: For each element, scan right → O(n²)
  → BACKWARD: Process from right, use monotonic stack → O(n)

EXAMPLE 3: "Trapping rain water"
  → FORWARD: For each position, find max on left AND right → complex
  → TWO-PASS: Precompute left max (forward), right max (backward)
  → Or use two pointers from both ends → O(n)

EXAMPLE 4: "Reconstruct a path from destination to source"
  → FORWARD: BFS finds shortest path, but how to trace it?
  → BACKWARD: Store parent pointers, trace from destination to source
🗺️ The Input → Output Mapping Framework
Before trying to solve a problem, understand the SHAPE of the transformation.

The Mapping Analysis
text

ASK YOURSELF:

"What type of INPUT do I have?"
  → Single number
  → Array of numbers
  → String
  → Matrix / Grid
  → Tree
  → Graph
  → Two sequences

"What type of OUTPUT do I need?"
  → A single number (count, max, min, sum)
  → A boolean (yes/no, possible/impossible)
  → A modified array or string
  → A specific index or position
  → A subset or subsequence
  → A path or sequence of steps

"What is the RELATIONSHIP between input and output?"
  → Aggregation: Many inputs → one output (sum, max, count)
  → Filtering: Select elements that satisfy condition
  → Transformation: Rearrange, modify, convert
  → Search: Find specific element(s) in input
  → Construction: Build output from input pieces
How This Helps
text

INPUT: Array of numbers
OUTPUT: Single number (maximum sum)
RELATIONSHIP: Aggregation with constraint (contiguous subarray)

→ This tells me I'm looking at SUBARRAY + OPTIMIZATION
→ Pattern match: Sliding Window or Kadane's Algorithm or Prefix Sum

---

INPUT: String
OUTPUT: Boolean (is it valid?)
RELATIONSHIP: Checking a property

→ This tells me I'm VALIDATING a condition
→ Pattern match: Stack (for brackets), Two Pointers (for palindrome),
  Hash Map (for character constraints)

---

INPUT: Grid of 0s and 1s
OUTPUT: Single number (count of islands)
RELATIONSHIP: Counting connected components

→ This tells me I'm finding CONNECTED COMPONENTS in a GRAPH
→ Pattern match: BFS, DFS, or Union-Find
🎨 The Visualization Framework
If you can DRAW it, you can SOLVE it.

When and How to Visualize
text

ALWAYS DRAW WHEN WORKING WITH:

ARRAYS:
  → Draw boxes with values
  → Mark pointers (left, right, i, j)
  → Show window boundaries
  → Highlight the current state

  [ 2 | 3 | 1 | 5 | 4 | 7 | 6 ]
    L           R
    ←── window ──→

TREES:
  → Draw the actual tree structure
  → Mark visited nodes
  → Show recursion path
  → Number the traversal order

        5
       / \
      3   8
     / \ / \
    1  4 7  9

GRAPHS:
  → Draw nodes and edges
  → Mark visited vs unvisited
  → Show BFS layers or DFS stack
  → Highlight the path being explored

  A → B → D
  ↓ ↗   ↓
  C     E

MATRICES/GRIDS:
  → Draw the grid
  → Mark current position
  → Show the direction of traversal
  → Highlight cells that satisfy conditions

  [ 1  0  1 ]
  [ 1  1  0 ]  ← currently here
  [ 0  1  1 ]

DP TABLES:
  → Draw the table
  → Fill in base cases first
  → Show the direction of filling
  → Mark dependencies (which cells compute current cell)

  dp[i][j]:
      ""  a   b   c
  ""  [ 0 | 0 | 0 | 0 ]
  a   [ 0 | 1 | 1 | 1 ]
  c   [ 0 | 1 | 1 | 2 ] ← dp[2][3] = max(dp[1][3], dp[2][2], dp[1][2]+1)
  b   [ 0 | 1 | 2 | 2 ]

STACKS/QUEUES:
  → Show the current contents
  → Mark top/front/rear
  → Show what's being pushed/popped

  Stack: | 3 | 5 | 7 |  ← top
  Push 2: | 3 | 5 | 7 | 2 |  ← new top
🆘 When You're Completely Stuck
It happens to everyone. Here's your emergency toolkit.

The Unstuck Protocol
text

LEVEL 1 — RE-READ THE PROBLEM (2 minutes)
  → You probably missed something
  → Read EVERY word again, especially constraints
  → Look at the examples VERY carefully
  → Is there a property of the input you overlooked?

LEVEL 2 — TRY MORE EXAMPLES (3 minutes)
  → Create your own small example
  → Trace through it by hand
  → What do you NOTICE? Any pattern?
  → Try an example where the answer is trivial — why is it trivial?

LEVEL 3 — SIMPLIFY THE PROBLEM (3 minutes)
  → What if the array were sorted?
  → What if all elements were positive?
  → What if n were very small (like 3-4)?
  → What if there were only 2 choices instead of many?
  → Solve the SIMPLER version, then add complexity back

LEVEL 4 — THINK ABOUT RELATED PROBLEMS (2 minutes)
  → Does this remind you of ANYTHING you've solved before?
  → What if you changed one word in the problem — would you know how to solve that?
  → What's the CLOSEST problem you know?
  → Can you TRANSFORM this into that problem?

LEVEL 5 — CHANGE YOUR ANGLE (3 minutes)
  → Process from right to left instead of left to right
  → Think about the COMPLEMENT (what you DON'T want)
  → Think about the OPPOSITE problem (maximize instead of minimize)
  → Think about what INFORMATION you wish you had
  → If you had a magic oracle that answered one question, what would you ask?

LEVEL 6 — ENUMERATE TECHNIQUES (2 minutes)
  → Go through the patterns list systematically:
    "Is this sliding window? No because..."
    "Is this two pointers? No because..."
    "Is this binary search? Maybe because..."
  → Elimination is just as powerful as identification

LEVEL 7 — ASK FOR A HINT (in interviews)
  → "I'm stuck on [specific part]. I've considered [approaches]. 
     Could you point me in the right direction?"
  → This is 100% acceptable. Interviewers EXPECT it.
  → A well-asked hint shows maturity and self-awareness
The "Obvious in Hindsight" Tricks
These are techniques that unlock many problems but are easy to forget:

text

TRICK 1: SORT THE INPUT
  → Even if the problem doesn't mention sorting
  → Sorting often reveals structure
  → Especially useful for: duplicates, closest pair, intervals

TRICK 2: USE A HASH MAP
  → "What if I could look up any value in O(1)?"
  → Store values you've seen, frequencies, indices, complements
  → Almost always the first optimization to consider

TRICK 3: THINK ABOUT THE COMPLEMENT
  → "Longest subarray with at most K zeros" 
    = "Shortest subarray to remove that has more than K zeros"
  → Sometimes the complement is much easier to compute

TRICK 4: FIX ONE VARIABLE
  → In a 2D problem, fix one dimension and solve the other
  → "For each row, what's the answer?" 
  → Reduces 2D to multiple 1D problems

TRICK 5: DUMMY NODES / SENTINELS
  → Add a fake node at the start/end of a linked list
  → Add boundary values to arrays
  → Eliminates special-case handling for boundaries

TRICK 6: PRECOMPUTE FROM BOTH DIRECTIONS
  → Left max array + Right max array → Trapping Rain Water
  → Prefix product + Suffix product → Product Except Self
  → Forward pass + Backward pass solves many problems

TRICK 7: PIGEONHOLE PRINCIPLE
  → If n+1 items go into n buckets, at least one bucket has 2+
  → Useful for: finding duplicates, cycle detection

TRICK 8: MATHEMATICAL INSIGHT
  → XOR properties (a ^ a = 0, a ^ 0 = a)
  → Sum formula (1+2+...+n = n(n+1)/2)
  → Modular arithmetic
  → Don't underestimate simple math
🧭 Framework Selection Guide
Different problems need different frameworks. Here's how to pick.

text

╔═══════════════════════════════════════════════════════════════╗
║     SITUATION                    → USE THIS FRAMEWORK        ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║ First time seeing a problem      → UMPIRE (always start here)║
║                                                               ║
║ Problem feels familiar           → Pattern Recognition System ║
║                                                               ║
║ No idea what technique to use    → Constraint Analysis        ║
║                                                               ║
║ Know the technique but can't     → "What Changes, What Stays" ║
║ figure out implementation                                     ║
║                                                               ║
║ Brute force works but too slow   → Brute Force → Optimize    ║
║                                                               ║
║ Problem is about optimization    → Subproblem Decomposition   ║
║ (min/max/count ways)               (leads to DP)              ║
║                                                               ║
║ Problem has multiple phases      → State Machine Framework    ║
║ or holding/not-holding states                                 ║
║                                                               ║
║ Forward approach is complex      → Work Backwards Framework   ║
║                                                               ║
║ Can't grasp the transformation   → Input → Output Mapping    ║
║                                                               ║
║ Can't see the structure          → Visualization Framework    ║
║                                                               ║
║ Completely stuck with nothing    → Unstuck Protocol           ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
🌱 Building Your Own Intuition
Frameworks are training wheels. The goal is to INTERNALIZE them until they become instinct.

The 4 Stages of Pattern Mastery
text

STAGE 1 — UNCONSCIOUS INCOMPETENCE (Beginner)
  "I don't know what I don't know"
  → Every problem feels unique and impossible
  → No pattern recognition
  → Need to look up solutions for most problems
  → DURATION: First 50-100 problems

STAGE 2 — CONSCIOUS INCOMPETENCE (Learning)
  "I know the patterns exist but can't apply them quickly"
  → Can identify patterns AFTER seeing the solution
  → Need the framework checklist to guide thinking
  → Starting to see connections between problems
  → DURATION: Problems 100-250

STAGE 3 — CONSCIOUS COMPETENCE (Intermediate)
  "I can apply patterns but need to think deliberately"
  → Can identify patterns within 5-10 minutes
  → Don't need the checklist — but still think through steps
  → Can solve most medium problems independently
  → DURATION: Problems 250-500

STAGE 4 — UNCONSCIOUS COMPETENCE (Advanced)
  "I see the pattern instantly — it's instinct"
  → Pattern recognition is automatic
  → Brain skips to the right approach immediately
  → Focus shifts to optimization and edge cases
  → Can tackle hard problems and novel variations
  → DURATION: 500+ problems over 6+ months
How to Accelerate Through the Stages
text

PRACTICE 1: CATEGORIZE AFTER SOLVING
  → After every problem, TAG it with the pattern used
  → Build a personal spreadsheet:
    Problem | Pattern | Key Insight | Difficulty | Date | Revisit?

PRACTICE 2: SOLVE PATTERN CLUSTERS
  → Solve 5-8 problems of the SAME pattern in a row
  → This builds deep familiarity with one technique
  → Then move to the next pattern
  → Then solve MIXED problems to practice recognition

PRACTICE 3: EXPLAIN TO SOMEONE ELSE
  → Teaching forces understanding
  → If you can't explain WHY a pattern applies, you don't understand it
  → Rubber duck debugging works for learning too

PRACTICE 4: REVISIT AND RE-SOLVE
  → After 1 week, try the problem again WITHOUT looking at your old solution
  → If you can't → the pattern isn't internalized yet
  → If you can → it's becoming instinct

PRACTICE 5: SOLVE THE VARIANTS
  → For every pattern, learn the CLASSIC problem and its VARIANTS
  → Example: Sliding window
    → Classic: Maximum sum subarray of size K
    → Variant 1: Longest substring without repeating characters
    → Variant 2: Minimum window substring
    → Variant 3: Longest subarray with at most K distinct elements
    → Variant 4: Count subarrays with sum equal to K
  → The pattern is the SAME. The details change.

PRACTICE 6: TIME YOURSELF
  → Easy: solve in 15 minutes
  → Medium: solve in 30 minutes
  → Hard: solve in 45 minutes
  → If you can't → you need more practice with that pattern
  → Speed comes from RECOGNITION, not from coding faster

PRACTICE 7: BUILD A "PATTERN NOTEBOOK"
  For each pattern, maintain:
  → Name and one-sentence description
  → When to use (signals)
  → Template approach (steps)
  → Common variations
  → 3-5 representative problems
  → Common mistakes to avoid
  → Personal notes and insights
The Compound Effect
text

WEEK 1:   Everything is hard. You need 1 hour per easy problem.
WEEK 4:   You recognize arrays + hashing. Easy problems take 20 min.
WEEK 8:   Sliding window and two pointers click. Mediums take 40 min.
WEEK 12:  You see patterns before reading the full problem.
WEEK 16:  You can explain WHY approaches work, not just WHAT they are.
WEEK 20:  Binary search on answer and DP start feeling natural.
WEEK 24:  You solve most mediums in 20-25 min. You attempt hards.
WEEK 30:  Patterns are instinct. You focus on edge cases and optimization.

THE KEY: You DON'T see this progress day-to-day.
         You see it month-to-month.
         KEEP GOING.
🏁 The One-Page Summary
text

╔══════════════════════════════════════════════════════════════╗
║              PROBLEM SOLVING — THE COMPLETE SYSTEM           ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  1. UNDERSTAND                                               ║
║     → Read twice, ask questions, create examples             ║
║     → "What is the input? Output? Constraints? Edge cases?"  ║
║                                                              ║
║  2. MATCH                                                    ║
║     → Connect to a known pattern using signals               ║
║     → Constraints tell you the expected complexity            ║
║     → "What changes? What stays? What's the bottleneck?"     ║
║                                                              ║
║  3. PLAN                                                     ║
║     → Start brute force, then optimize                       ║
║     → State your approach in plain English                   ║
║     → Know your data structures and variables before coding  ║
║                                                              ║
║  4. IMPLEMENT                                                ║
║     → Translate the plan, don't improvise                    ║
║     → Clean names, clear structure, edge cases first         ║
║     → Write incrementally, verify as you go                  ║
║                                                              ║
║  5. REVIEW                                                   ║
║     → Dry run with basic + edge case examples                ║
║     → Debug systematically: identify, classify, fix, verify  ║
║                                                              ║
║  6. EVALUATE                                                 ║
║     → State time and space complexity                        ║
║     → Explain WHY it's that complexity                       ║
║                                                              ║
║  ──────────────────────────────────────────────────────────   ║
║                                                              ║
║  WHEN STUCK:                                                 ║
║     → Re-read → More examples → Simplify → Related problems  ║
║     → Change angle → Enumerate techniques → Ask for hint     ║
║                                                              ║
║  THE GOAL:                                                   ║
║     → Not to memorize solutions                              ║
║     → But to build a SYSTEM that derives solutions           ║
║     → Frameworks are training wheels → Intuition is the bike ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
⭐ Star this repo if these frameworks changed how you approach problems. Share it with your study group.